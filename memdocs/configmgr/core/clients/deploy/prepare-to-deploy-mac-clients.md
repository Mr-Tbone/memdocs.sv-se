---
title: Förbered för att distribuera klienten till Mac
titleSuffix: Configuration Manager
description: Konfigurations uppgifter innan du distribuerar Configuration Manager-klienten till Mac.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d0968a61be4e450bb145b309f61de0d6c212549
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713998"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Förbereda distribution av klient program vara till Mac

*Gäller för: Configuration Manager (aktuell gren)*

Följ dessa steg för att se till att du är redo att [distribuera Configuration Manager-klienten till Mac-datorer](deploy-clients-to-macs.md).



## <a name="mac-prerequisites"></a>Mac-krav

Installations paketet för Mac-klienten levereras inte med Configuration Manager mediet. Hämta **klienter för ytterligare operativ system** från [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=525184).  

En lista över versioner som stöds finns i [operativ system som stöds för klienter och enheter](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).



## <a name="certificate-requirements"></a>Certifikatkrav

Klient installation och hantering av Mac-datorer kräver PKI-certifikat (Public Key Infrastructure). PKI-certifikat skyddar kommunikationen mellan Mac-datorerna och Configuration Managers platsen med hjälp av ömsesidig autentisering och krypterade data överföringar. Configuration Manager kan begära och installera ett användar klient certifikat. Den använder certifikat tjänster med en utfärdare av företags certifikat och den Configuration Manager registrerings platsen och proxyn för registrerings platsen. Du kan också begära och installera ett dator certifikat oberoende av Configuration Manager. Certifikatet måste uppfylla Configuration Manager certifikat krav.  

Configuration Manager Mac-klienter söker alltid efter certifikat åter kallelse. Du kan inte inaktivera den här funktionen.  

Om Mac-klienterna inte kan hitta listan över återkallade certifikat (CRL) kan de inte ansluta till Configuration Manager-plats system. I synnerhet för Mac-klienter i en annan skog till den utfärdande certifikat utfärdaren, kontrol lera CRL-designen. Kontrol lera att Mac-klienter kan hitta och hämta en CRL.  

Innan du installerar Configuration Manager-klienten på en Mac-dator måste du bestämma hur klient certifikatet ska installeras:  

-   Använd Configuration Manager-registrering med [verktyget CMEnroll](deploy-clients-to-macs.md#client-and-certificate-automation-with-cmenroll). Registrerings processen har inte stöd för automatisk certifikat förnyelse. Omregistrera Mac-datorer innan certifikatet upphör att gälla.  

-   [Använd en certifikatbegäran och en installations metod som är oberoende av Configuration Manager](deploy-clients-to-macs.md#bkmk_external).  

Mer information om krav för Mac-klientcertifikat finns i avsnittet [om krav för PKI-certifikat för Configuration Manager](../../plan-design/network/pki-certificate-requirements.md).  

Mac-klienter tilldelas automatiskt den Configuration Manager plats som hanterar dem. Mac-klienter installeras som endast Internet klienter, även om kommunikationen är begränsad till intranätet. Den här konfigurationen innebär att de kommunicerar med Internet-aktiverade hanterings platser och distributions platser på deras tilldelade plats. Mac-datorer kommunicerar inte med plats system utanför deras tilldelade plats.  

> [!IMPORTANT]  
>  Configuration Manager-klienten för macOS kan inte användas för att ansluta till en hanterings plats som har kon figurer ATS för att använda en [databas replik](../../servers/deploy/configure/database-replicas-for-management-points.md).  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Distribuera ett webb server certifikat till plats system servrar  

Om dessa plats system inte har det, distribuerar du ett webb server certifikat till de datorer som har dessa plats system roller:  

-   Hanteringsplats  

-   Distributionsplats  

-   Registreringsplats  

-   Registreringsproxyplats  

Webb Server certifikatet måste innehålla det Internet-FQDN som anges i plats systemets egenskaper. Servern behöver inte vara tillgänglig från Internet för att stödja Mac-datorer. Om du inte behöver Internetbaserad klient hantering kan du ange intranätets FQDN-värde för Internet-FQDN.  

Ange plats systemets Internet-FQDN-värde i webb Server certifikatet för hanterings platsen, distributions platsen och proxyn för registrerings platsen.

Mer information om ett exempel på distribution finns i [distribuera webb Server certifikatet för plats system som kör IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Distribuera ett certifikat för klientautentisering till plats system servrar  

Om dessa plats system inte har det kan du distribuera ett certifikat för klientautentisering till de datorer som är värdar för dessa plats system roller:  

-   Hanteringsplats  

-   Distributionsplats  

En exempel distribution som skapar och installerar klient certifikatet för hanterings platser finns i [distribuera klient certifikatet för Windows-datorer](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

En exempel distribution som skapar och installerar klient certifikatet för distributions platser finns i [distribuera klient certifikatet för distributions platser](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

> [!IMPORTANT]  
>  För att distribuera-klienten till enheter som kör macOS Sierra måste ämnes namnet för hanterings plats certifikatet vara korrekt konfigurerat. Använd till exempel FQDN för hanterings plats servern.  



## <a name="prepare-the-client-certificate-template-for-macs"></a>Förbered klient certifikat mal len för Mac  

Certifikat mal len måste ha behörigheterna **Läs** och **Registrera** för det användar konto som registrerar certifikatet på Mac-datorn.  

Mer information finns i [distribuera klient certifikatet för Mac-datorer](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  



## <a name="configure-the-management-point-and-distribution-point"></a>Konfigurera hanterings platsen och distributions platsen  

Konfigurera hanteringsplatserna med följande alternativ:  

-   HTTPS  

-   Tillåt klient anslutningar från Internet. Det här konfigurationsvärdet krävs för att hantera Mac-datorer. Det innebär dock inte att plats system servrarna måste vara tillgängliga från Internet.  

-   Tillåt att mobila enheter och Mac-datorer använder den här hanteringsplatsen  

Distributions platser krävs inte för att installera klienten för Mac. Om du vill distribuera program vara till dessa datorer när du har installerat-klienten konfigurerar du distributions platser så att de tillåter klient anslutningar från Internet.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Konfigurera hanterings platser och distributions platser så att de stöder Mac  

Innan du börjar den här proceduren ska du se till att konfigurera hanterings platsen och distributions platsen med en Internet-FQDN. Om dessa servrar inte stöder internetbaserad klient hantering anger du intranätets FQDN som Internet-FQDN-värde.

Plats system rollerna måste finnas på en primär plats.  

1.  Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **servrar och plats system roller** . Välj sedan den server som har rätt plats system roller.  

2.  I informations fönstret markerar du **hanterings plats** rollen och väljer **Egenskaper** i menyfliksområdet. I fönstret **Egenskaper för hanterings plats** konfigurerar du följande alternativ:  

    1.  Välj **https**.  

    2.  Välj **Tillåt endast Internet-klientanslutningar** eller **Tillåt intranät-och Internet klient anslutningar**. De här alternativen kräver ett fullständigt domän namn för Internet eller intranät.  

    3.  Välj **Tillåt att mobila enheter och Mac-datorer använder den här hanterings platsen**.  

    4. Spara konfigurationen genom att välja **OK**.  

3.  I informations fönstret i noden Server-och plats system roller väljer du **distributions plats** rollen och väljer **Egenskaper** i menyfliksområdet. I fönstret **Egenskaper för distributions plats** konfigurerar du följande alternativ:  

    -   Välj **https**.  

    -   Välj **Tillåt endast Internet-klientanslutningar** eller **Tillåt intranät-och Internet klient anslutningar**. De här alternativen kräver ett fullständigt domän namn för Internet eller intranät.  

    -   Välj **Importera certifikat**, bläddra till den exporterade certifikat filen för klient distributions platsen och ange sedan lösen ordet.  

4.  Upprepa proceduren för alla hanterings platser och distributions platser på primära platser som hanterar Mac-datorer.  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Konfigurera proxyn för registrerings platsen och registrerings platsen  

Installera båda rollerna på samma plats. Du behöver inte installera dem på samma plats system Server, eller i samma Active Directory skog.  

Mer information om placering och överväganden för plats system roller finns i [plats system roller](../../plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles).  

Information om hur du lägger till plats system roller som stöder Mac-datorer finns i [Installera plats system roller](../../servers/deploy/configure/install-site-system-roles.md).

På sidan **urval för system roll** väljer du **Proxy för registrerings** plats och **registrerings plats** i listan över tillgängliga roller.  



## <a name="install-the-reporting-services-point"></a>Installera repor ting Services-platsen  

Mer information finns i [Installera repor ting Services-platsen](../../servers/manage/configuring-reporting.md).  



## <a name="next-steps"></a>Nästa steg

[Distribuera Configuration Manager-klienten till Mac-datorer](deploy-clients-to-macs.md)  
