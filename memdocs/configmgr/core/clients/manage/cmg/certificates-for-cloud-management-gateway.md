---
title: CMG-certifikat
titleSuffix: Configuration Manager
description: Lär dig mer om de olika digitala certifikat som ska användas med Cloud Management Gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: 33e4ecbac965206ec4043f5adf91d2dbfb9602d8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714082"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certifikat för Cloud Management Gateway

*Gäller för: Configuration Manager (aktuell gren)*

Beroende på vilket scenario du använder för att hantera klienter på Internet med CMG (Cloud Management Gateway) behöver du ett eller flera av följande digitala certifikat:  

- [Certifikat för CMG-serverautentisering](#bkmk_serverauth)  
  - [CMG betrodda rot certifikat till klienter](#bkmk_cmgroot)  
  - [Certifikat för serverautentisering som utfärdats av en offentlig Provider](#bkmk_serverauthpublic)  
  - [Certifikat för serverautentisering som utfärdats från företags-PKI](#bkmk_serverauthpki)  

- [Certifikat för klientautentisering](#bkmk_clientauth)  
  - [Klientens betrodda rot certifikat till CMG](#bkmk_clientroot)  

- [Aktivera hanterings plats för HTTPS](#bkmk_mphttps)  

- [Hanterings certifikat för Azure](#bkmk_azuremgmt)  

Mer information om olika scenarier finns i [Planera för Cloud Management Gateway](plan-cloud-management-gateway.md).

## <a name="general-information"></a>Allmän information

<!--SCCMDocs issue #779-->
Certifikat för Cloud Management Gateway stöder följande konfigurationer:  

- 2048-bitars eller 4096-bitars nyckel längd

- Nyckel lagrings leverantörer för certifikatets privata nycklar. Mer information finns i [Översikt över CNG-certifikat](../../../plan-design/network/cng-certificates-overview.md).  

- När du konfigurerar Windows med följande princip: **system kryptografi: Använd FIPS-kompatibla algoritmer för kryptering, hashing och signering**  

- **TLS 1,2**. Mer information finns i [så här aktiverar du TLS 1,2](../../../plan-design/security/enable-tls-1-2.md).  

## <a name="cmg-server-authentication-certificate"></a><a name="bkmk_serverauth"></a>Certifikat för CMG-serverautentisering

*Detta certifikat krävs i alla scenarier.*

Du anger det här certifikatet när du skapar CMG i Configuration Manager-konsolen.

CMG skapar en HTTPS-tjänst som Internetbaserade klienter ansluter till. Servern kräver ett certifikat för serverautentisering för att bygga en säker kanal. Hämta ett certifikat för det här syftet från en offentlig leverantör eller utfärda den från din infrastruktur för offentliga nycklar (PKI). Mer information finns i [CMG-betrott rot certifikat till klienter](#bkmk_cmgroot).

> [!NOTE]
> Certifikatet för CMG-serverautentisering stöder jokertecken. Vissa certifikat utfärdare utfärdar certifikat med hjälp av ett jokertecken för värd namnet. Till exempel `*.contoso.com`. Vissa organisationer använder jokertecken för att förenkla sin PKI och minska underhållskostnaderna.<!--491233-->  
>
> Mer information om hur du använder ett certifikat med jokertecken med en CMG finns i [Konfigurera en CMG](setup-cloud-management-gateway.md#set-up-a-cmg).<!--SCCMDocs issue #565-->  

Det här certifikatet kräver ett globalt unikt namn för att identifiera tjänsten i Azure. Innan du begär ett certifikat bör du kontrol lera att Azure-domännamnet som du vill ha är unikt. Till exempel *GraniteFalls.CloudApp.net*.

1. Logga in på [Azure Portal](https://portal.azure.com).
1. Välj **alla resurser**och välj sedan **Lägg till**.
1. Sök efter **moln tjänst**. Välj **Skapa**.
1. I fältet **DNS-namn** anger du det prefix som du vill använda, till exempel *GraniteFalls*. Gränssnittet visar om domän namnet är tillgängligt eller redan används av en annan tjänst.

    > [!Important]  
    > Skapa inte tjänsten i portalen. Använd bara den här processen för att kontrol lera namn tillgänglighet.

Om du även vill aktivera CMG för innehåll kontrollerar du att namnet på CMG-tjänsten också är ett unikt namn för Azure Storage-kontot. Om CMG moln tjänst namnet är unikt, men lagrings konto namnet inte är det, Configuration Manager inte att etablera tjänsten i Azure. Upprepa proceduren ovan i Azure Portal med följande ändringar:

- Sök efter **lagrings konto**
- Testa ditt namn i fältet **namn på lagrings konto**

DNS-namnets prefix, till exempel *GraniteFalls*, ska vara 3 till 24 tecken långt och endast använda alfanumeriska tecken. Använd inte specialtecken, t. ex. ett`-`bindestreck ().<!-- SCCMDocs#1080 -->

### <a name="cmg-trusted-root-certificate-to-clients"></a><a name="bkmk_cmgroot"></a>CMG betrodda rot certifikat till klienter

Klienter måste lita på certifikatet för CMG-serverautentisering. Det finns två metoder för att göra detta förtroende:

- Använd ett certifikat från en offentlig och globalt betrodd certifikat leverantör. Till exempel, men inte begränsat till, DigiCert, Thawte eller VeriSign. Windows-klienterna innehåller betrodda rot certifikat utfärdare (CAs) från dessa leverantörer. Genom att använda ett certifikat för serverautentisering som utfärdats av någon av dessa providers, litar klienterna automatiskt på det.  

- Använd ett certifikat utfärdat av en företags certifikat utfärdare från din infrastruktur för offentliga nycklar (PKI). De flesta Enterprise PKI-implementeringar lägger till betrodda rot certifikat utfärdare till Windows-klienter. Till exempel, med hjälp av Active Directory Certificate Services med grup princip. Om du utfärdar certifikatet för CMG från en certifikat utfärdare som klienterna inte automatiskt litar på, lägger du till det betrodda rot certifikatet för certifikat utfärdaren på Internetbaserade klienter.  

  - Du kan också använda Configuration Manager certifikat profiler för att etablera certifikat på klienter. Mer information finns i [Introduktion till certifikat profiler](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).

  - Om du planerar att [installera Configuration Manager-klienten från Intune](../../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)kan du även använda Intune-certifikat profiler för att etablera certifikat på klienter. Mer information finns i [Konfigurera en certifikat profil](https://docs.microsoft.com/intune/certificates-configure).

### <a name="server-authentication-certificate-issued-by-public-provider"></a><a name="bkmk_serverauthpublic"></a>Certifikat för serverautentisering som utfärdats av en offentlig Provider

En tredjeparts-certifikat leverantör kan inte skapa ett certifikat för CloudApp.net, eftersom den domänen ägs av Microsoft. Du kan bara få ett certifikat utfärdat för en domän som du äger. Det främsta skälet till att skaffa ett certifikat från en tredjepartsleverantör är att klienterna redan har förtroende för providerns rot certifikat.

Använd följande process för att skapa ett DNS-alias:

1. Skapa en kanonisk namn post (CNAME) i din organisations offentliga DNS. Den här posten skapar ett alias för CMG till ett eget namn som du använder i det offentliga certifikatet.

    Contoso namnger till exempel sina CMG- **GraniteFalls**. Det här namnet blir **GraniteFalls.CloudApp.net** i Azure. I Contosos offentliga DNS contoso.com-namnområde skapar DNS-administratören en ny CNAME-post för **GraniteFalls.contoso.com** för det faktiska värd namnet, **GraniteFalls.CloudApp.net**.  

2. Begär ett certifikat för serverautentisering från en offentlig Provider med hjälp av det egna namnet (CN) för CNAME-aliaset.
Contoso använder till exempel **GraniteFalls.contoso.com** för certifikatets CN.  

3. Skapa CMG i Configuration Manager-konsolen med det här certifikatet. På sidan **Inställningar** i guiden skapa Cloud Management Gateway:  

    - När du lägger till Server certifikatet för den här moln tjänsten (från **certifikat filen**) extraherar guiden värd namnet från certifikatets CN-namn.  

    - Den lägger sedan till det värd namnet till **cloudapp.net**eller **usgovcloudapp.net** för Azures offentliga Azure-moln, som tjänstens FQDN för att skapa tjänsten i Azure.  

    - Om contoso till exempel skapar CMG extraherar Configuration Manager hostname- **GraniteFalls** från certifikatets CN. Azure skapar den faktiska tjänsten som **GraniteFalls.CloudApp.net**.  

När du skapar CMG-instansen i Configuration Manager, och certifikatet har GraniteFalls.Contoso.com, extraherar Configuration Manager bara värd namnet, till exempel: GraniteFalls. Den lägger till detta värdnamn till CloudApp.net, som Azure kräver när en moln tjänst skapas. CNAME-aliaset i DNS-namnområdet för din domän, Contoso.com, mappar samman dessa två FQDN. Configuration Manager ger klienterna en princip för att få åtkomst till den här CMG. DNS-mappningen kopplar ihop den så att de kan få säker åtkomst till tjänsten i Azure.<!--SCCMDocs issue #565-->  

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a><a name="bkmk_serverauthpki"></a>Certifikat för serverautentisering som utfärdats från företags-PKI

Skapa ett anpassat SSL-certifikat för CMG på samma sätt som för en moln distributions plats. Följ anvisningarna för att [distribuera tjänst certifikatet för molnbaserade distributions platser](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) , men gör följande saker på olika sätt:

- När du begär det anpassade webb Server certifikatet anger du ett fullständigt domän namn för certifikatets egna namn. Namnet kan vara ett offentligt domän namn som du äger eller så kan du använda cloudapp.net-domänen. Om du använder en egen offentlig domän, se processen ovan för att skapa ett DNS-alias i din organisations offentliga DNS.  

- När du använder den offentliga cloudapp.net-domänen för CMG-webb Server certifikatet:  

  - Använd ett namn som slutar på **cloudapp.net** i det offentliga Azure-molnet  

  - Använd ett namn som slutar på **usgovcloudapp.net** för Azures Azures myndigheter för amerikanska myndigheter  

## <a name="client-authentication-certificate"></a><a name="bkmk_clientauth"></a>Certifikat för klientautentisering

*Detta certifikat krävs för Internetbaserade klienter som kör Windows 8,1 och Windows 10-enheter som inte är anslutna till Azure Active Directory (Azure AD). Det krävs också på CMG-anslutnings punkten. Det krävs inte för Windows 10-klienter som är anslutna till Azure AD.*

Klienterna använder det här certifikatet för att autentisera med CMG. Windows 10-enheter som är hybrid-eller molnbaserad domänanslutna kräver inte det här certifikatet eftersom de använder Azure AD för att autentisera sig.

Etablera det här certifikatet utanför Configuration Managers kontext. Använd exempelvis Active Directory Certificate Services och grup princip för att utfärda certifikat för klientautentisering. Mer information finns i [distribuera klient certifikatet för Windows-datorer](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).

För att på ett säkert sätt vidarebefordra klient begär Anden kräver CMG-anslutningen ett certifikat för klientautentisering som motsvarar certifikatet för serverautentisering på HTTPS-hanterings platsen. Om klienter använder Azure AD-autentisering, eller om du konfigurerar hanterings platsen för utökad HTTP, krävs inte det här certifikatet. Mer information finns i [Aktivera hanterings plats för https](#bkmk_mphttps).

> [!NOTE]
> Microsoft rekommenderar att du ansluter enheter till Azure AD. Internet-baserade enheter kan använda Azure AD för att autentisera med Configuration Manager. Det aktiverar också både enhets-och användar scenarier oavsett om enheten är ansluten till Internet eller om den är ansluten till det interna nätverket. Mer information finns i [Installera och registrera klienten med hjälp av Azure AD-identitet](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).
>
> Från och med version 2002,<!--5686290--> Configuration Manager utökar sitt stöd för Internetbaserade enheter som inte ofta ansluter till det interna nätverket, kan inte ansluta Azure Active Directory (Azure AD) och har inte någon metod för att installera ett PKI-utfärdat certifikat. Mer information finns i [tokenbaserad autentisering för CMG](../../deploy/deploy-clients-cmg-token.md).

### <a name="client-trusted-root-certificate-to-cmg"></a><a name="bkmk_clientroot"></a>Klientens betrodda rot certifikat till CMG

*Det här certifikatet krävs när du använder certifikat för klientautentisering. När alla klienter använder Azure AD för autentisering krävs inte det här certifikatet.*

Du anger det här certifikatet när du skapar CMG i Configuration Manager-konsolen.

CMG måste lita på certifikat för klientautentisering. Ange den betrodda rot certifikat kedjan för att åstadkomma detta förtroende. Se till att lägga till alla certifikat i förtroende kedjan. Om certifikatet för klientautentisering till exempel utfärdas av en mellanliggande certifikat utfärdare, Lägg till både mellanliggande certifikat och rot certifikat UTFÄRDAre.

> [!Note]  
> När du skapar en CMG behöver du inte längre ange ett betrott rot certifikat på sidan Inställningar. Detta certifikat krävs inte när du använder Azure Active Directory (Azure AD) för klientautentisering, men som används för att krävas i guiden. Om du använder certifikat för PKI-klientautentisering måste du fortfarande lägga till ett betrott rot certifikat till CMG.<!--SCCMDocs-pr issue #2872 SCCMDocs issue #1319-->
>
> I version 1902 och tidigare kan du bara lägga till två betrodda rot certifikat utfärdare och fyra mellanliggande certifikat utfärdare (underordnade).

#### <a name="export-the-client-certificates-trusted-root"></a>Exportera klient certifikatets betrodda rot

När du har utfärdat ett certifikat för klientautentisering till en dator, använder du den här processen på den datorn för att exportera den betrodda roten.

1. Öppna Start-menyn. Skriv "kör" för att öppna körnings fönstret. Öppna `mmc`.  

2. I menyn Arkiv väljer du **Lägg till/ta bort snapin-modul..**..  

3. I dialog rutan Lägg till eller ta bort snapin-moduler väljer du **certifikat**och väljer sedan **Lägg till**.  

    1. I dialog rutan snapin-modulen certifikat väljer **du dator konto**och väljer sedan **Nästa**.  

    1. I dialog rutan Välj dator väljer du **lokal dator**och sedan **Slutför**.  

    1. I dialog rutan Lägg till eller ta bort snapin-moduler väljer du **OK**.  

4. Expandera **certifikat**, expandera **personliga**och välj **certifikat**.  

5. Välj ett certifikat vars avsedda syfte är **klientautentisering**.  

    1. Från menyn Åtgärd väljer du **Öppna**.  

    1. Gå till fliken **certifierings Sök väg** .  

    1. Välj nästa certifikat i kedjan och välj **Visa certifikat**.  

6. I dialog rutan nytt certifikat går du till fliken **information** . Välj **Kopiera till fil.**...  

7. Slutför guiden Exportera certifikat med standard certifikat formatet, der- **kodad binär X. 509 (. CER)**. Anteckna namnet och platsen för det exporterade certifikatet.  

8. Exportera alla certifikat i certifierings Sök vägen för det ursprungliga certifikatet för klientautentisering. Anteckna vilka exporterade certifikat som är mellanliggande certifikat utfärdare och vilka som är betrodda rot certifikat utfärdare.  

## <a name="enable-management-point-for-https"></a><a name="bkmk_mphttps"></a>Aktivera hanterings plats för HTTPS

Etablera det här certifikatet utanför Configuration Managers kontext. Använd exempelvis Active Directory Certificate Services och grup princip för att utfärda ett webb server certifikat. Mer information finns i [krav på PKI-certifikat](../../../plan-design/network/pki-certificate-requirements.md) och [distribuera webb Server certifikatet för plats system som kör IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).

När du använder alternativet plats för att **använda Configuration Manager-genererade certifikat för HTTP-plats system**kan hanterings platsen vara http. Mer information finns i [Enhanced http](../../../plan-design/hierarchy/enhanced-http.md).

> [!Tip]  
> Om du inte använder utökat HTTP och din miljö har flera hanterings platser behöver du inte använda HTTPS – aktivera dem för CMG. Konfigurera de CMG-aktiverade hanterings platserna som **endast Internet**. Sedan försöker dina lokala klienter inte använda dem.<!-- SCCMDocs#1676 -->

### <a name="enhanced-http-certificate-for-management-points"></a>Förbättrat HTTP-certifikat för hanterings platser

När du aktiverar utökat HTTP genererar plats servern ett självsignerat certifikat med namnet **SMS-roll SSL-certifikat**som utfärdats av rot certifikatet för utfärdande. Hanterings platsen lägger till det här certifikatet på IIS standard webbplats som är kopplad till port 443.

### <a name="management-point-client-connection-mode-summary"></a>Sammanfattning av hanterings plats klientens anslutnings läge

Dessa tabeller sammanfattar om hanterings platsen kräver HTTP eller HTTPS, beroende på typ av klient och plats version.

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>För Internetbaserade klienter som kommunicerar med Cloud Management Gateway

Konfigurera en lokal hanterings plats för att tillåta anslutningar från CMG med följande klient anslutnings läge:

| Typ av klient   | Hanteringsplats |
|------------------|------------------|
| Arbetsgrupp        | E-HTTP-<sup>[anteckning 1](#bkmk_note1)</sup>, https |
| AD-domänansluten | E-HTTP-<sup>[anteckning 1](#bkmk_note1)</sup>, https |
| Azure AD-ansluten  | E-HTTP, HTTPS |
| Hybrid-ansluten    | E-HTTP, HTTPS |

<a name="bkmk_note1"></a>

> [!Note]  
> **Anmärkning 1**: den här konfigurationen kräver att klienten har ett certifikat för klientautentisering och stöder endast enhets [säkra](#bkmk_clientauth)scenarier.  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>För lokala klienter som kommunicerar med den lokala hanterings platsen

Konfigurera en lokal hanterings plats med följande klient anslutnings läge:

| Typ av klient   | Hanteringsplats |
|------------------|------------------|
| Arbetsgrupp        | HTTP, HTTPS |
| AD-domänansluten | HTTP, HTTPS |
| Azure AD-ansluten  | HTTPS       |
| Hybrid-ansluten    | HTTP, HTTPS |

> [!NOTE]  
> AD-domänanslutna klienter stöder både enhets-och användarbaserade scenarier som kommunicerar med en HTTP-eller HTTPS-hanterings plats.  
>
> Azure AD-anslutna och hybrid-anslutna klienter kan kommunicera via HTTP för enhets drivna scenarier, men behöver E-HTTP eller HTTPS för att aktivera användarvänliga scenarier. Annars fungerar de likadant som arbets grupps klienter.  

#### <a name="legend-of-terms"></a>Förklaring av villkor

- *Arbets grupp*: enheten är inte ansluten till en domän eller Azure AD, men har ett [certifikat för klientautentisering](#bkmk_clientauth)  
- *AD-* domänansluten: du ansluter enheten till en lokal Active Directory domän  
- *Azure AD-ansluten*: även känd som molnbaserad domän ansluten, ansluter du enheten till en Azure Active Directory klient  
- *Hybrid-ansluten*: du ansluter enheten till både en Active Directory domän och en Azure AD-klient  
- *Http*: på hanterings platsens egenskaper anger du klient anslutningarna till **http**  
- *Https*: i egenskaperna för hanterings platsen anger du klient anslutningarna till **https**  
- *E-http*: på fliken plats egenskaper, fliken **klient dator kommunikation** , anger du plats system inställningarna till **https eller http**, och du aktiverar alternativet att **använda Configuration Manager-genererade certifikat för http-plats system**. Du konfigurerar hanterings platsen för HTTP, HTTP-hanterings platsen är klar för både HTTP-och HTTPS-kommunikation (token-auth-scenarier).  
    > [!Note]
    > Från och med version 1906 kallas den här fliken **kommunikations säkerhet**.<!-- SCCMDocs#1645 -->  

## <a name="azure-management-certificate"></a><a name="bkmk_azuremgmt"></a>Hanterings certifikat för Azure

*Detta certifikat krävs för klassiska tjänst distributioner. Det krävs inte för Azure Resource Manager-distributioner.*

> [!Important]  
> Från och med version 1810 föråldras klassiska tjänst distributioner i Azure i Configuration Manager. Börja använda Azure Resource Manager distributioner för Cloud Management Gateway. Mer information finns i [plan for CMG](plan-cloud-management-gateway.md#azure-resource-manager).
>
> Från och med Configuration Manager version 1902 är Azure Resource Manager den enda distributions metoden för nya instanser av Cloud Management Gateway. Detta certifikat krävs inte i Configuration Manager version 1902 eller senare.<!-- 3605704 -->

Du anger det här certifikatet i Azure Portal och när du skapar CMG i Configuration Manager-konsolen.

För att skapa CMG i Azure måste Configuration Manager tjänst anslutnings punkt först autentisera till din Azure-prenumeration. När du använder en klassisk tjänst distribution används Azures hanterings certifikat för den här autentiseringen. En Azure-administratör överför det här certifikatet till din prenumeration. När du skapar CMG i Configuration Manager-konsolen anger du det här certifikatet.

Mer information och anvisningar om hur du laddar upp ett hanterings certifikat finns i följande artiklar i Azure-dokumentationen:

- [Cloud Services och hanterings certifikat](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Ladda upp ett Azure Service Management-certifikat](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Se till att kopiera det prenumerations-ID som är associerat med hanterings certifikatet. Du använder den för att skapa CMG i Configuration Manager-konsolen.

## <a name="next-steps"></a>Nästa steg

- [Konfigurera en molnhanteringsgateway](setup-cloud-management-gateway.md)  

- [Vanliga frågor och svar om Cloud Management Gateway](cloud-management-gateway-faq.md)  

- [Säkerhet och sekretess för molnhanteringsgateway](security-and-privacy-for-cloud-management-gateway.md)  
