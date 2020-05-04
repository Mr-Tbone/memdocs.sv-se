---
title: CMG säkerhet och sekretess
titleSuffix: Configuration Manager
description: Lär dig mer om vägledning och rekommendationer för säkerhet och sekretess med Cloud Management Gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.openlocfilehash: 93427cb34b2216bf16f713818481e69573a4b0de
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712892"
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>Säkerhet och sekretess för Cloud Management Gateway

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller säkerhets-och sekretess information för Configuration Manager Cloud Management Gateway (CMG). Mer information finns i [Planera för Cloud Management Gateway](plan-cloud-management-gateway.md).

## <a name="cmg-security-details"></a>CMG säkerhets information

- CMG accepterar och hanterar anslutningar från CMG-anslutnings punkter. Den använder ömsesidig SSL-autentisering med certifikat och anslutnings-ID: n.
- CMG accepterar och vidarebefordrar klient begär Anden med följande metoder:
    - Förautentiserar anslutningar med hjälp av ömsesidig SSL med det PKI-baserade certifikatet för klientautentisering eller Azure AD.
      - IIS på CMG VM-instanserna verifierar certifikat Sök vägen baserat på de betrodda rot certifikaten som överförts till CMG.
      - IIS på VM-instansen verifierar också återkallning av klient certifikat, om det är aktiverat. Mer information finns i [publicera listan över återkallade certifikat](#bkmk_crl).
    - Listan över betrodda certifikat kontrollerar roten för certifikatet för klientautentisering. Den utför också samma verifiering som hanterings platsen för-klienten. Mer information finns i [granska poster i platsens lista över betrodda certifikat](#bkmk_ctl).
    - Verifierar och filtrerar klient begär Anden (URL: er) för att kontrol lera om någon CMG anslutnings punkt kan betjäna begäran.  
    - Kontrollerar innehålls längd för varje publicerings slut punkt.
    - Använder Round-Robin-beteende för att belastningsutjämna CMG anslutnings punkter på samma plats.
- CMG-anslutnings punkten använder följande metoder:
    - Skapar konsekventa HTTPS/TCP-anslutningar till alla VM-instanser av CMG. Den kontrollerar och underhåller dessa anslutningar varje minut.
    - Använder ömsesidig SSL-autentisering med CMG med hjälp av certifikat.
    - Vidarebefordrar klient begär Anden baserat på URL-mappningar.
    - Rapporterar anslutnings status för att Visa tjänstens hälso status i-konsolen.
    - Rapporterar trafik per slut punkt var femte minut.

### <a name="configuration-manager-client-facing-roles"></a>Configuration Manager klient riktade roller

Hanterings platsen och program uppdaterings platsens värd slut punkter i IIS till att betjäna klient begär Anden. CMG visar inte alla interna slut punkter. Varje slut punkt som publiceras till CMG har en URL-mappning.

- Den externa URL: en är den som klienten använder för att kommunicera med CMG.
- Den interna URL: en är den CMG-anslutnings punkt som används för att vidarebefordra begär anden till den interna servern.

#### <a name="url-mapping-example"></a>Exempel på URL-mappning

När du aktiverar CMG trafik på en hanterings plats skapar Configuration Manager en intern uppsättning URL-mappningar för varje hanterings plats Server. Exempel: ccm_system, ccm_incoming och sms_mp. Den externa URL: en för hanterings platsens ccm_system slut punkten kan se ut så här:  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
URL: en är unik för varje hanterings plats. Configuration Manager klienten placerar sedan CMG-aktiverade hanterings platsens namn i listan över Internet hanterings platser. Det här namnet ser ut så här:  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
Platsen överför automatiskt alla publicerade externa URL: er till CMG. Med det här beteendet kan CMG göra URL-filtrering. Alla URL-mappningar replikeras till CMG-anslutnings punkten. Den vidarebefordrar sedan kommunikationen till interna servrar enligt den externa URL: en från klient förfrågan.


## <a name="security-guidance-for-cmg"></a>Säkerhets vägledning för CMG

<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>Publicera listan över återkallade certifikat

Publicera din PKI: s lista över återkallade certifikat (CRL) för Internetbaserade klienter för åtkomst. När du distribuerar en CMG med PKI konfigurerar du tjänsten för att **Verifiera åter kallelse av klient certifikat** på fliken Inställningar. Den här inställningen konfigurerar tjänsten att använda en publicerad lista över återkallade certifikat (CRL). Mer information finns i [Planera för åter kallelse av PKI-certifikat](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

Detta CMG-alternativ verifierar certifikatet för klientautentisering.

- Om klienten använder Azure AD-autentisering spelar det ingen roll i listan.
- Aktivera det här alternativet (rekommenderas) om du använder PKI och externt publicerar CRL: n.
- Om du använder PKI ska du inte publicera listan över återkallade certifikat och sedan inaktivera det här alternativet.
- Om du inte konfigurerar det här alternativet kan det orsaka ytterligare trafik från klienter till CMG. Den ytterligare trafiken kan öka de utgående Azure-data, vilket kan öka dina Azure-kostnader.<!-- SCCMDocs#1434 -->

<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>Granska poster i platsens lista över betrodda certifikat

<!--503739-->
Varje Configuration Manager-plats innehåller en lista över betrodda rot certifikat utfärdare, listan över betrodda certifikat (CTL). Visa och ändra listan genom att gå till arbets ytan administration, expandera plats konfiguration och välja platser. Välj en plats och klicka på egenskaper i menyfliksområdet. Växla till fliken **klient dator kommunikation** och klicka sedan på **Ange** under betrodda rot certifikat utfärdare.

> [!Note]
> Från och med version 1906 kallas den här fliken **kommunikations säkerhet**.<!-- SCCMDocs#1645 -->  

Använd en mer restriktiv lista över betrodda certifikat för en plats med en CMG med PKI-klientautentisering. Annars godkänns klienter med certifikat för klientautentisering som utfärdats av en betrodd rot som redan finns på hanterings platsen automatiskt för klient registrering.

Den här del mängden ger administratörer större kontroll över säkerheten. CTL begränsar servern till att endast acceptera klient certifikat som utfärdas från certifikat utfärdarna i listan över betrodda certifikat. Windows levereras till exempel med ett antal välkända certifikat från tredjeparts certifikat utfärdare (CA), till exempel VeriSign och Thawte. Som standard har datorn som kör IIS förtroende för certifikat som går med i kedjan till dessa välkända certifikat utfärdare. Om du inte konfigurerar IIS med en CTL godkänns alla datorer som har ett klient certifikat som utfärdats från dessa certifikat utfärdare som en giltig Configuration Manager-klient. Om du konfigurerar IIS med en lista över betrodda certifikat som inte innehåller de här certifikat utfärdarna, nekas klient anslutningar om certifikatet är länkat till dessa certifikat utfärdare.

### <a name="enforce-tls-12"></a><a name="bkmk_tls"></a>Framtvinga TLS 1,2

<!-- SCCMDocs-pr#4021 -->

Från och med version 1906 använder du CMG-inställningen för att **genomdriva TLS 1,2**. Den gäller endast för den virtuella Azure-moln tjänsten. Den gäller inte för lokala Configuration Manager plats servrar eller klienter. Mer information om TLS 1,2 finns i [så här aktiverar du tls 1,2](../../../plan-design/security/enable-tls-1-2.md).


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>Nästa steg

- [Planera för en molnhanteringsgateway](plan-cloud-management-gateway.md)
- [Konfigurera en molnhanteringsgateway](setup-cloud-management-gateway.md)
- [Vanliga frågor och svar om Cloud Management Gateway](cloud-management-gateway-faq.md)
- [Certifikat för molnhanteringsgateway](certificates-for-cloud-management-gateway.md)
