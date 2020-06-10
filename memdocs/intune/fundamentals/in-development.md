---
title: Under utveckling – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-funktioner under utveckling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 90039e9bb75bcf7c266ac033408f87d37e27ef8d
ms.sourcegitcommit: 7a5196d4d9736c5cd52a23155c479523e52a097d
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2020
ms.locfileid: "84436762"
---
# <a name="in-development-for-microsoft-intune"></a>Under utveckling för Microsoft Intune

För att hjälpa dig med förberedelser och planering innehåller den här sidan information om uppdateringar av och funktioner i användargränssnittet i Intune som är under utveckling, men som inte släppts än. Förutom informationen på den här sidan: 

- Om vi tror att du behöver vidta åtgärder innan en ändring genomförs, publicerar vi ett extra inlägg i meddelandecentret för Office.
- När en funktion går in i produktion, oavsett om det är en förhandsversion eller en allmänt tillgänglig version, flyttas funktionsbeskrivningen från den här sidan till [Nyheter](whats-new.md).
- Den här sidan och sidan [Nyheter](whats-new.md) uppdateras regelbundet. Kom tillbaka och se om det finns nya uppdateringar.
- Information om planerade produktlanseringar och tidslinjer finns i [Microsoft 365-översikten](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS).

> [!NOTE]
> Den här informationen återspeglar våra planer gällande Intune-funktioner i kommande versioner. Datum och enskilda funktioner kan ändras. Den här sidan beskriver inte alla funktioner som utvecklas.

**RSS-feed**: Få reda på när den här sidan uppdateras genom att kopiera och klistra in följande webbadress i feed-läsaren: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**Den här artikeln uppdaterades senast det datum som anges i rubriken ovan.**

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>Apphantering

### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001----"></a>Förbättringar av sidan Enheter i företagsportalerna för ioS/iPad och macOS<!-- 6055001  -->
Vi har gjort flera förbättringar av sidan **Enheter** i Företagsportal-appen för iOS/iPad och Mac. Vi har gjort om sidan **Enheter** så att den har fått en mer modern känsla och blivit bättre organiserad när det gäller enhetsinformationen. Genom att använda en enda kolumn med definierade avsnittsrubriker kan din organisations iOS/iPad- och macOS-användare enkelt kontrollera statusen för sina enheter och på så vis säkerställa att de håller sig skyddade och upprätthåller åtkomsten till organisationens resurser. Dessutom har vi lagt till tydligare meddelanden och ytterligare felsökningssteg för användare vars enheter inte uppfyller kraven. Mer information om företagsportalen finns i [Anpassa Intune-företagsportalappar, företagsportalens webbplats och Intune-appen](../apps/company-portal-app.md).

### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>Förbättringar av registreringsfunktionen i macOS-företagsportalappen<!-- 6444452  -->
Företagsportalen för macOS-registrering kommer att ha en enklare registreringsprocess som stämmer bättre överens med företagsportalen för iOS-registrering. De enheter som användarna ser:  
- Ett mer elegant användargränssnitt.  
- En förbättrad checklista för registrering.  
- Tydligare instruktioner för hur man registrerar sina enheter.  
- Förbättrade felsökningsalternativ.  

Mer information om företagsportalen finns i [Anpassa Intune-företagsportalappar, företagsportalens webbplats och Intune-appen](../apps/company-portal-app.md).

### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-to-be-a-sign-insign-out-app---7055619----"></a>Använd inställningarna för Autonomt enappsläge när du ska konfigurera iOS-företagsportalen till att bli en app för in- och utloggning<!-- 7055619  -->
Du kan konfigurera iOS-företagsportalappen till att använda autonomt enappsläge (ASAM). Du kan använda ASAM-inställningarna på Microsoft Endpoint Manager-konsolen till att konfigurera iOS-företagsportalen så att den kan gå in i och utur enappsläge i samband med in- och utloggning. När företagsportalen är i autonomt enappsläge kan användarna inte använda några andra appar eller enhetens hemknapp förrän de har loggat in på företagsportalen. Vid utloggning återgår företagsportalen till enappsläge. 

Om du vill konfigurera företagsportalen till autonomt enappsläge i Microsoft Endpoint Manager, så välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**. Välj **iOS/iPadOS** som plattform och välj **Enhetsbegränsningar** som profil. Välj **Autonomt enappsläge** på fliken **Konfigurationsinställningar**. Ställ in **Appnamn** på `Company Portal` och ställ in **Appsamlings-ID** på `com.app.CompanyPortal`. Mer information finns i [Autonomt enappsläge (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) och [enappsläge](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Enhetskonfiguration

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Ställ in enhetsefterlevnadstillståndet från MDM-tredjepartspartners<!-- 6361689   -->
Snart kan du tillåta att efterlevnadstillståndet för iOS- och Android-enheter som hanteras av tredjepartspartners för hantering av mobilenheter konfigureras i Azure Active Directory (Azure AD).

När Intune konfigureras för parterefterlevnad, så skickas efterlevnadsdata för enheter som hanteras av tredjepartspartnern för hantering av mobilenheter till Intune för efterlevnadsutvärdering. Resultatet skickas sedan till Azure AD, där efterlevnadsdata används för att påtvinga dessa enheter dina principer för villkorsstyrd åtkomst.

Supporten kommer snart att omfatta följande partners:
- VMware WorkspaceONE (tidigare känt som AirWatch)

Om du vill aktivera en enhetsefterlevnadspartner så använder du en ny nod i administrationscentret för Microsoft Endpoint Manager: **Innehavaradministration** > **Anslutningsprogram och token** > **Hantering av partnerefterlevnad** där du väljer **Add Efterlevnadspartner**.

### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Lägg till en länk till din företagsportals supportwebbplats dit e-postmeddelanden om inkompatibilitet kan skickas<!-- 7225498    -->
När du lägger till en ny inställning till mallen för e-postaviseringar, som innebär att länken till din företagsportals webbplats läggs till för e-postaviseringar som skickas till användare av ej kompatibla enheter. (**Slutpunktsskydd** > **Enhetsefterlevnad** > **Meddelanden** > **Skapa meddelande**).  Användare som får ett e-postmeddelande därför att de har en inkompatibel enhet kan använda länken till att öppna en webbplats där de kan lära sig mer om varför deras enhet inte är kompatibel.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Ny FileVault-inställning för macOS-enhetskonfigurationsprincip för slutpunktsskydd<!-- 5459801   -->
Vi lägger till en ny inställning i FileVault-kategorin i mallen [macOS-slutpunktsskydd](../protect/endpoint-protection-macos.md): Dölj återställningsnyckel. (**Enheter** > **Konfigurationsprofiler** > **Skapa profil**, välj **macOS** för *Plattform* och sedan **Slutpunktsskydd** för *Profiltyp*). Den här inställningen döljer den personliga nyckeln från slutanvändaren under FileVault 2-kryptering. Enhetsanvändare kan visa sin personliga återställningsnyckel när som helst från iOS-företagsportalappen eller från företagsportalens webbplats för den krypterade macOS-enheten. De kan visa den personliga återställningsnyckeln genom att gå till enhetsinformation och klicka på *hämta återställningsnyckel*.

Den här inställningen kommer inte att vara tillgänglig i tidigare skapade principer. Du behöver återskapa FileVault-principer för att konfigurera den här inställningen och använda den. 

### <a name="configure-content-caching-on-macos-devices---7106872---"></a>Konfigurera cachelagring av innehåll på macOS-enheter<!-- 7106872 -->
På macOS-enheter kan du skapa en konfigurationsprofil som konfigurerar cachelagring av innehåll (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **macOS** för plattformen**Enhetsfunktioner** för profilen). Använd de här inställningarna om du vill ta bort cache, tillåta delad cache, ställa in en cachegräns för disken med mera.

Mer information om innehållscachelagring finns i [Innehållscachelagring](https://developer.apple.com/documentation/devicemanagement/contentcaching) (öppnar Apples webbplats).

Om du vill visa de inställningar som du kan konfigurera går du till [Funktionsinställningar för macOS-enheter i Intune](../configuration/macos-device-features-settings.md).

Gäller för:
- macOS

### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Nya inställningar för Windows 10 och nyare enheter<!-- 6602122  -->
När du skapar en VPN-profil med IKEv2-anslutningstypen, så finns det nya inställningar som du kan konfigurera (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Windows 10 och senare** för plattform > **VPN** för profil > **Bas-VPN**):

- **Enhetstunnel**: Tillåter enheter att automatiskt ansluta till VPN utan krav på interaktion från användarens sida, inklusive användarinloggning. Den här funktionen kräver att du aktiverar **Alltid på**, och använder **Datorcertifikat** som autentiseringsmetod.
- Kryptografisvitsinställningar: Konfigurera de algoritmer som används för att skydda IKE och underordnade säkerhetskopplingar, vilket gör det möjligt för dig att matcha klient- och serverinställningar.

Om du vill se vilka inställningar du kan konfigurera kan du gå till [Windows-enhetsinställningar för att lägga till VPN-anslutningar med Intune](../configuration/vpn-settings-windows-10.md).

Gäller för:
- Windows 10 och senare

### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794---"></a>Blockera delade tillfälliga iPad-sessioner på delade iPad-enheter<!-- 6613794 -->
I Intune finns det en ny inställning, **Blockera delade tillfälliga iPad-sessioner**, som blockerar tillfälliga sessioner på delade iPad-enheter (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPad** för plattform > **Enhetsbegränsningar** för profiltyp > **Delad iPad**). När detta har aktiverats kan slutanvändarna inte använda gästkontot. De måste logga in på enheten med sina hanterade Apple-ID:n och lösenord. 

Mer information om den inställning som du kan konfigurera finns i [Inställningar för iOS- och IPadOS-enheter för att tillåta eller begränsa funktioner](../configuration/device-restrictions-ios.md).

Gäller för:
- Delade iPad-enheter som kör iOS/iPad 13.4 och senare

### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976----"></a>Använd Microsoft Launcher som standardstartprogram för fullständigt hanterade Android Enterprise-enheter<!-- 4927976  -->
På Android Enterprise-ägarenheter kan du ställa in Microsoft Launcher som standardstartprogram för fullständigt hanterade enheter (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise** för plattform > **Enhetsägare** > **Enhetsbegränsningar** för profil > **Enhetsupplevelse**). Om du vill konfigurera alla andra inställningar för Microsoft Launcher, så använd appkonfigurationsprinciper. 

Det finns också några andra UI-uppdateringar, inklusive **Dedikerade enheter** som har bytt namn till **Enhetsupplevelse**.

Om du vill se alla inställningar som du kan begränsa går du till [Inställningar för Android Enterprise-enheter för att tillåta eller begränsa funktioner med Intune](../configuration/device-restrictions-android-for-work.md). 

Gäller för:
- Ägare av fullständigt hanterade Android Enterprise-enheter (COBO)

### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386----"></a>Lägg till nya schemainställningar och sök efter befintliga schemainställningar med OEMConfig på Android Enterprise<!-- 6394386  -->
I Intune kan du använda OEMConfig för att hantera inställningar för Android Enterprise-enheter (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise** för plattformen > **OEMConfig** för profilen). När du använder **Configuration Designer** så visas egenskaperna i appens schema. I **Configuration Designer** kan du:
- Lägg till nya inställningar i appens schema.
- Sök efter nya och befintliga inställningar i appens schema.

Mer information om OEMConfig-profiler i Intune finns i [Använda och hantera Android Enterprise-enheter med OEMConfig i Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Gäller för:
- Android enterprise

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Enhetsregistrering

### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Synkroniseringsfel vid automatisk enhetsregistrering<!-- 6988214 -->
Nya fel rapporteras för iOS/iPad- och macOS-enheter, inklusive
- Ogiltiga tecken i telefonnumret eller om fältet är tomt. 
- Ogiltigt eller tomt konfigurationsnamn för profilen. 
- Ogiltigt/utgånget markörvärde eller saknad markör.
- Nekad eller förfallen token. 
- Avdelningsfältet i profilen är tomt eller för långt. 
- Apple kunde inte hitta profilen, och en ny måste skapas. 
- Antalet borttagna Apple Business Manager-enheter kommer att läggas till på översiktssidan, där dina enheters status visas.

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>VPN kan användas för att distribuera egna enheter (BYOD, Bring Your Own Device)<!--5015344 -->
Med den nya växlingsknappen **Hoppa över kontroll av domänanslutning** för Autopilot-profil kan du distribuera Hybrid Azure AD-anslutna enheter utan åtkomst till ditt företagsnätverk med hjälp av din egen Win32 VPN-klient från 3:e part. Om du vill se den nya växlingsknappen kan du gå till [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter**  > **Windows** > **Windows-registrering** > **Distributionsprofiler** > **Skapa profil** > **Välkomstupplevelse (OOBE)** .

### <a name="shared-ipads-for-business--6367326---"></a>Delat iPad for Business<!--6367326 -->
Du kan använda Intune och Apple Business Manager till att enkelt och säkert konfigurera delade iPads så att flera medarbetare kan dela enheter. Apples [Delad iPad](https://developer.apple.com/education/shared-ipad/) får en ny anpassad upplevelse för flera användare samtidigt som användardata bevaras. Med ett hanterat Apple-ID kan användare komma åt sina appar, data och inställningar efter att ha loggat in på en delad iPad i organisationen. Delad iPad fungerar med federerade identiteter.

Du ser den här funktionen genom att gå till [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **iOS** > **iOS-registrering** > **Registreringsprogramtoken** > välj en token > **Profiler** > **Skapa profil** > **iOS**. På sidan **Hanteringsinställningar** väljer du **Registrera utan användartillhörighet** så visas alternativet **Delad iPad**.

**Gäller för:** macOS 13.4 och senare. Den här versionen innehåller stöd för tillfälliga sessioner med delad iPad så att användarna kan komma åt en enhet utan ett hanterat Apple-ID. Vid utloggning raderar enheten all användarinformation så att enheten omedelbart kan användas, vilket eliminerar behovet av enhetsrensning. 

<!-- ***********************************************-->
## <a name="device-management"></a>Enhetshantering

### <a name="change-primary-user-on-co-managed-devices--7319183---"></a>Ändra primär användare på samhanterade enheter<!--7319183 -->
Du kan ändra en enhets primära användare för samhanterade Windows-enheter. Mer information om hur du hittar och ändrar detta finns i [Hitta en Intune-enhets primära användare](../remote-actions/find-primary-user.md).

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Stöd för PowerShell-skript för BYOD-enheter<!-- 1862833  -->
PowerShell-skript kommer att stödja Azure AD-registrerade enheter i Intune. Mer information om PowerShell finns i [Använda PowerShell-skript på Windows 10-enheter i Intune](../apps/intune-management-extension.md). Den här funktionen stöder inte enheter som kör Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics innehåller enhetsinformationslogg<!--6014987  -->
Loggar med Intune-enhetsinformation kommer att vara tillgängliga i **Rapporter** > **Logganalys**. Du kan korrelera enhetsinformationen för att bygga anpassade frågor och Azure-arbetsböcker.

### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Om du anger en primär Intune-användare anges också egenskapen Azure AD Owner<!--7319227 -->
Den här kommande funktionen ställer automatiskt in egenskapen Owner på nyligen registrerade Hybrid Azure AD-anslutna enheter samtidigt som den primära Intune-användaren anges. Mer information om den primär användare finns i [Hitta en Intune-enhets primära användare](../remote-actions/find-primary-user.md).

Detta är en ändring i registreringsprocessen och gäller endast nyligen registrerade enheter. För befintliga Hybrid Azure AD-anslutna enheter måste du uppdatera egenskapen för Azure AD-ägare manuellt. Om du vill göra detta kan du använda funktionen [Ändra primär användare](../remote-actions/find-primary-user.md#change-a-devices-primary-user) eller [ett skript](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices).

När Windows 10-enheter ansluts till Azure-katalogen för Hybrid Azure blir enhetens första användare den primära användaren i Endpoint Manager.  Användaren har för tillfället inte konfigurerats för motsvarande Azure AD-enhetsobjekt. Detta orsakar en inkonsekvens när du jämför egenskapen *ägare* från en Azure AD-portal med egenskapen *primär användare* i administrationscentret för Microsoft Endpoint Manager. Egenskapen Azure AD-ägare används för att skydda åtkomsten till BitLocker-återställningsnycklar. Egenskapen har inte fyllts i på Hybrid Azure AD-anslutna enheter. Den här begränsningen förhindrar konfiguration av självbetjäning av BitLocker-återställning från Azure AD. Denna kommande funktion löser den här begränsningen.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Klientkoppling: Enhetstidslinje i administrationscentret<!--7220536, CM7141381 -->
När Configuration Manager synkroniserar en enhet till Microsoft Endpoint Manager via klientanslutning kan du se en tidslinje med händelser. Den här tidslinjen visar tidigare aktivitet på enheten som kan hjälpa dig att felsöka problem. Mer information finns i [Teknisk förhandsversion av Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Klientkoppling: Installera ett program från administrationscentret<!-- 7220536, CM6024389 -->
Du kommer att kunna initiera en programinstallation i realtid för en klientansluten enhet från administrationscentret för Microsoft Endpoint Management. Mer information finns i [Teknisk förhandsversionen av Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Klientkoppling: CMPivot från administrationscentret<!--7220536, CM6024392 -->
Du kommer att kunna utnyttja kraften hos [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) i administrationscentret för Microsoft Endpoint Manager. Gör det möjligt för fler, till exempel supportavdelningen, att starta realtidsfrågor från molnet till en enskild ConfigMgr-hanterad enhet och returnera resultaten till administrationscentret. Detta ger alla de traditionella fördelarna med CMPivot, vilket gör det möjligt för IT-administratörer och andra utsedda personer att snabbt bedöma status för enheter i deras miljöer och vidta åtgärder. Mer information finns i [Teknisk förhandsversionen av Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Klientkoppling: Kör skript från administrationscentret<!--7220536, CM6234688 -->
Du har möjlighet att utnyttja kraften i Configuration Managers lokala [Run Scripts](../../configmgr/apps/deploy-use/create-deploy-scripts.md)-funktion i administrationscentret för Microsoft Endpoint Manager. Tillåt ytterligare personer, som supportavdelningen, att köra PowerShell-skript från molnet mot en enskild Configuration Manager-hanterad enhet. Detta ger alla traditionella fördelar med PowerShell-skript som redan har definierats och godkänts av Configuration Manager-administratören till den nya miljön. Mer information finns i [Teknisk förhandsversionen av Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Ny sammanslagningslogik för Windows 10-enheter<!--179048-->
Om en kund återskapar en enhet idag och sedan registrerar om den, visas flera poster för enheten i administrationskonsolen för Microsoft Endpoint Manager. I den nya sammanslagningslogik som är under utveckling slås sådana dubblettposter samman för Windows 10-enheter.

### <a name="remote-lock-pin-availability-for-macos-devices--7281557--"></a>PIN-kodstillgängliget för fjärrlås för macOS-enheter<!--7281557-->
Tillgängligheten för macOS-enheters PIN-koder för fjärrlåsning kommer att ökas från 7 till 30 dagar.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Mall för Power BI-efterlevnadsrapport V2.0<!-- 636958  -->
Administratörer kan uppdatera versionen av Power BI-efterlevnadsrapporten från V1.0 till V2.0. V2.0 har en förbättrad design och ändringar av beräkningar och data som visas i mallen. Mer information finns i [Ansluta till Data Warehouse med Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
<!--## Security-->


<!-- ***********************************************-->
## <a name="notices"></a>Meddelanden

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Se även

Mer information om den senaste utvecklingen finns i [Nyheter i Microsoft Intune](whats-new.md).
