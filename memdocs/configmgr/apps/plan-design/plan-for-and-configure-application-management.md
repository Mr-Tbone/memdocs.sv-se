---
title: Planera för program hantering
titleSuffix: Configuration Manager
description: Implementera och konfigurera nödvändiga beroenden för distribution av program i Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03fda62774b930a1cc3603415f3b872050b9cb71
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709945"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Planera för och konfigurera program hantering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd informationen i den här artikeln för att hjälpa dig att implementera de nödvändiga beroendena för att distribuera program i Configuration Manager.  



## <a name="dependencies-external-to-configuration-manager"></a>Beroenden utanför Configuration Manager  


### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)

IIS krävs på de servrar som kör följande plats system roller:

- Hanteringsplats  
- Distributionsplats  

Mer information finns i [krav för plats och plats system](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

> [!Note]  
> Program katalogen kräver också IIS. Men dess Silverlight-användar upplevelse stöds inte som aktuell gren version 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Certifikat för kod signerade program för mobila enheter

När du använder kod signerings program för att distribuera dem till mobila enheter ska du inte använda ett certifikat som har genererats med hjälp av en mall i version 3 (**Windows Server 2008, Enterprise Edition**). Den här certifikat mal len skapar ett certifikat som inte är kompatibelt med Configuration Manager program för mobila enheter.

Om du använder Active Directory certifikat tjänster för kod signerings program för mobila enhets program ska du inte använda en certifikatmall av version 3.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Granska inloggnings händelser för mappning mellan användare och enhet  

Om du vill skapa mappningar mellan användare och enheter automatiskt konfigurerar du klienter för att granska inloggnings händelser.

Configuration Manager klienten läser in inloggnings händelser av typen **lyckades** från säkerhets händelse loggen i Windows för att fastställa automatisk mappning mellan användare och enheter. Aktivera dessa händelser med följande två gransknings principer:

- **Granska kontoinloggningshändelser**
- **Granska inloggningshändelser**

Kontrollera att de två inställningarna är aktiverade på klientdatorerna, om du vill att mappningar mellan användare och enheter skapas automatiskt. Du kan använda grupprincipen i Windows för att konfigurera inställningarna.

Mer information om mappning mellan användare och enhet finns i [Länka användare och enheter med mappning mellan användare och enhet](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  



## <a name="configuration-manager-dependencies"></a>Beroenden i Configuration Manager


### <a name="management-point"></a>Hanteringsplats

Klienterna kontaktar en hanterings plats för att ladda ned klient principer för att hitta innehåll.

Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare.

I version 1902 och tidigare använder klienter hanterings platsen för att ansluta till program katalogen. Om klienterna inte kan komma åt en hanterings plats kan de inte använda program katalogen.

> [!Note]  
> Från och med version 1806 krävs inte längre program katalog roller för att Visa användar tillgängliga program i Software Center. Mer information finns i [Konfigurera Software Center](plan-for-software-center.md#bkmk_userex).<!--1358309-->  
>
> Från och med version 1906 kan du inte installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
  

### <a name="distribution-point"></a>Distributionsplats

Innan du kan distribuera program till klienter behöver du minst en distributions plats i hierarkin. Som standard har platsservern en distributionsplatsroll aktiverad under en vanlig installation. Antalet och platsen för distributions platser varierar beroende på miljöns särskilda krav.

Mer information om hur du installerar distributions platser och hanterar innehåll finns i [Hantera innehåll och innehålls infrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="reporting-services-point"></a>Rapporteringstjänstpunkt

Om du vill använda rapporterna i Configuration Manager för program hantering måste du först installera och konfigurera en repor ting Services-plats.

Mer information finns i [Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="client-settings"></a>Klientinställningar

Många klient inställningar styr hur klienten installerar program och användar upplevelsen på enheten. De här klient inställningarna omfattar följande grupper:

- Dator agent  
- Omstart av dator  
- Software Center  
- Programvarudistribution  
- Mappning mellan användare och enhet  

Mer information finns i följande artiklar:

- [Om klientinställningar](../../core/clients/deploy/about-client-settings.md)  
- [Konfigurera klientinställningar](../../core/clients/deploy/configure-client-settings.md)  


### <a name="security-permissions-for-application-management"></a>Säkerhetsbehörighet för programhantering

- Säkerhets rollen **program författare** innehåller de behörigheter som krävs för att skapa, ändra och dra tillbaka program.  

- Säkerhets rollen **Programdistributionsansvarig** innehåller de behörigheter som krävs för att distribuera program.  

- Säkerhets rollen **program administratör** har alla behörigheter både från **program författaren** och **Programdistributionsansvarig** säkerhets roller.  

Mer information finns i [Konfigurera rollbaserad administration](../../core/servers/deploy/configure/configure-role-based-administration.md).  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>Köra virtuella program på klient med App-V 4.6 SP1 eller senare

Om du vill skapa virtuella program i Configuration Manager installerar du App-V 4,6 SP1 eller senare på enheter.

Innan du distribuerar virtuella program uppdaterar du även App-V-klienten med snabb korrigeringen som beskrivs i [Microsoft Support artikel 2645225](https://support.microsoft.com/help/2645225).  


### <a name="application-catalog"></a>Program katalog

> [!Important]  
> Support upphör för program katalog rollerna med version 1910.. Mer information finns i [ta bort program katalogen](#bkmk_remove-appcat).  

#### <a name="application-catalog-web-service-point"></a>Webb service punkt för program katalog

Webb tjänst platsen för program katalogen är en plats system roll som ger information om tillgänglig program vara från program varu biblioteket till webbplatsen för program katalogen som användarna har åtkomst till.

Mer information om hur du konfigurerar den här plats system rollen finns i [Installera och konfigurera programkatalog](#bkmk_appcat).  

#### <a name="application-catalog-website-point"></a>Plats för program katalog

Webbplatsen för program katalogen är en plats system roll som förser användare med en lista över tillgänglig program vara.

Mer information om hur du konfigurerar den här plats system rollen finns i [Installera och konfigurera programkatalog](#bkmk_appcat).

#### <a name="discovered-user-accounts-for-application-catalog"></a>Identifierade användar konton för program katalogen

Configuration Manager måste först identifiera användar konton innan användarna kan visa och begära program från program katalogen. Mer information finns i [Kör identifiering](../../core/servers/deploy/configure/run-discovery.md).  



## <a name="configure-software-center"></a><a name="bkmk_userex"></a>Konfigurera Software Center  

Mer information om hur du konfigurerar och varumärkerar Software Center finns i [Planera för Software Center](plan-for-software-center.md).


## <a name="remove-the-application-catalog"></a><a name="bkmk_remove-appcat"></a>Ta bort program katalogen

<!-- SCCMDocs-pr issue 3051 -->

Support upphör för program katalog rollerna med version 1910. Mer information finns i [borttagna och föråldrade funktioner](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). I följande lista sammanfattas ändringarna:

- Från och med version 1806 stöds inte längre **Silverlight-användar upplevelsen** för program katalog webbplatsen.<!--1358309--> Rollen webb tjänst för program katalog *krävs*inte längre, men *stöds*fortfarande.

- Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller.

- Support upphör för program katalog rollerna med version 1910.  

De här iterativa förbättringarna av Software Center och hanterings platsen är att förenkla infrastrukturen och ta bort behovet av program katalogen för distributioner som är tillgängliga för användare. Software Center kan leverera alla app-distributioner utan program katalogen. Om du aktiverar TLS 1,2 och använder HTTP med program katalogen kan användarna inte se användar mål, tillgängliga distributioner. Uppdatera Configuration Manager till version 1906 eller senare för att dra nytta av dessa förbättringar.

1. Uppdatera alla klienter till version 1806 eller senare. Version 1906 rekommenderas.  

1. Ange anpassning för Software Center i stället för i egenskaperna för program katalogens webbplats roll. Mer information finns i [klient inställningar för Software Center](../../core/clients/deploy/about-client-settings.md#software-center).  

1. Granska standard-och anpassade klient inställningar. I gruppen **dator agent** kontrollerar du att **standard programkatalog webbplats** är `(none)`.  

    I version 1902 och tidigare växlar klienten bara till att använda hanterings platsen när det inte finns några program katalog roller i hierarkin. Annars fortsätter klienter att använda en av program katalog instanserna i hierarkin. Det här beteendet gäller för separata primära platser.  

1. Ta bort plats system rollerna för webb tjänsten för **program katalogen** och **webb tjänsten för program katalogen** från alla primära platser.

När du har tagit bort program katalogens roller börjar Software Center med hanterings platsen för användar mål, tillgängliga distributioner. I version 1902 och tidigare kan det ta upp till 65 minuter innan ändringen sker. Om du vill kontrol lera detta beteende på en speciell klient `SCClient_<username>.log`granskar du och söker efter en post som liknar följande rad:

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`


## <a name="install-and-configure-the-application-catalog"></a><a name="bkmk_appcat"></a>Installera och konfigurera program katalogen  

> [!Important]  
> Support upphör för program katalog rollerna med version 1910. Mer information finns i [ta bort program katalogen](#bkmk_remove-appcat).  

### <a name="step-1-web-server-certificate-for-https"></a>Steg 1: webb server certifikat för HTTPS

Om du använder HTTPS-anslutningar distribuerar du ett webb server certifikat till plats system servrarna för webbplatsen för program katalogen och webb tjänst platsen för program katalogen.

Om du vill att klienter ska använda program katalogen från Internet distribuerar du ett webb server certifikat till minst en hanterings plats. Konfigurera den för klient anslutningar från Internet.

Mer information om certifikat krav finns i [krav för PKI-certifikat](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-2-client-authentication-certificate-for-https"></a>Steg 2: certifikat för klientautentisering för HTTPS

Om du använder ett klient-PKI-certifikat för anslutningar till hanterings platser distribuerar du ett certifikat för klientautentisering till klient datorerna. Även om klienter inte använder ett PKI-klientcertifikat för att ansluta till program katalogen, måste de ansluta till en hanterings plats innan de kan använda program katalogen.

Distribuera ett certifikat för klientautentisering till klient datorer i följande scenarier:

- Alla hanterings platser i intranätet accepterar bara HTTPS-klientanslutningar.
- Klienterna ansluter till program katalogen från Internet.

Mer information om certifikat krav finns i [krav för PKI-certifikat](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Steg 3: installera och konfigurera program katalog roller

Installera både program katalogens webb tjänst plats och webbplats rollerna för program katalogen på samma plats. Du behöver inte installera dem på samma server eller i samma Active Directory skog. Program katalogens webb tjänst plats måste dock vara i samma skog som plats databasen.

Mer information om server placering finns i [Planera för plats system servrar och plats system roller](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

> [!NOTE]  
> Installera program katalogen på en primär plats. Du kan inte installera den på en sekundär eller Central administrations plats.  

Installera program katalogen på en ny plats system Server eller en befintlig server på platsen. Mer information om den allmänna proceduren finns i [Installera plats system roller](../../core/servers/deploy/configure/install-site-system-roles.md). I guiden för att lägga till en plats system roll eller skapa en plats system server väljer du följande roller i listan:  

- **Webb service punkt för program katalog**  
- **Plats för program katalog**  

> [!TIP]  
> Om du vill att klient datorer ska använda program katalogen via Internet anger du det fullständigt kvalificerade domän namnet (FQDN) för Internet.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Verifiera installationen av dessa plats system roller  

- Statusmeddelanden: Använd komponenterna **SMS_PORTALWEB_CONTROL_MANAGER** och **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Till exempel, status-ID **1015** för **SMS_PORTALWEB_CONTROL_MANAGER** bekräftar att Platskomponenthanteraren har installerat webbplatsen för program katalogen.  

- Loggfiler: Sök efter **SMSAWEBSVCSetup.log** och **SMSPORTALWEBSetup.log**.  

    Mer information hittar du i loggfilerna **awebsvcMSI. log** och **portlwebMSI. log** .  


### <a name="step-4-configure-client-settings"></a>Steg 4: Konfigurera klient inställningar

Konfigurera standard klient inställningarna om du vill att alla användare ska ha samma inställningar. I annat fall konfigurerar du anpassade klientinställningar för enskilda samlingar.

Mer information finns i följande artiklar:

- [Om klientinställningar](../../core/clients/deploy/about-client-settings.md)  
    - Dator agent  
    - Omstart av dator  
    - Software Center  
    - Programvarudistribution  
    - Mappning mellan användare och enhet  
- [Konfigurera klientinställningar](../../core/clients/deploy/configure-client-settings.md)  

Configuration Manager-klienten konfigurerar enheter med de här inställningarna nästa gång en klient princip laddas ned. Information om hur du aktiverar princip hämtning för en enskild klient finns i [Hantera klienter](../../core/clients/manage/manage-clients.md).


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Steg 5: kontrol lera att program katalogen fungerar

Använd följande procedurer för att kontrol lera att program katalogen fungerar.

> [!NOTE]  
> Användar upplevelsen för program katalogen kräver Microsoft Silverlight. Om du använder program katalogen direkt från en webbläsare kontrollerar du först att Microsoft Silverlight är installerat på datorn.  

> [!TIP]  
> Krav som saknas är bland de vanligaste orsakerna till att program katalogen fungerar felaktigt efter installationen. Bekräfta roll kraven för program katalogens plats system roller. Mer information finns i [krav för plats och plats system](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

Ange adressen till program katalogens webbplats i en webbläsare. Bekräfta att webb sidan visar tre flikar: **programkatalog**, **Mina program förfrågningar**och **Mina enheter**.  

Använd lämplig adress för program katalogen från följande lista, där `<server>` är dator namnet, intranätets FQDN eller Internet-FQDN:  

- Inställningar för HTTPS-klientanslutningar och standard plats system roll:`https://<server>/CMApplicationCatalog`  

- Inställningar för HTTP-klientanslutningar och standard plats system roll:`http://<server>/CMApplicationCatalog`  

- Inställningar för HTTPS-klientanslutningar och anpassad plats system roll:`https://<server>:<port>/<web application name>`  

- Inställningar för HTTP-klientanslutningar och anpassad plats system roll:`http://<server>:<port>/<web application name>`  

> [!NOTE]  
> Om du har loggat in på enheten med ett domän administratörs konto visas inte meddelanden i Configuration Manager-klienten. Till exempel meddelanden som visar att ny program vara är tillgänglig.  
