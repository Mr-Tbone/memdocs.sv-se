---
title: Under utveckling – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-funktioner under utveckling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: e76816768090a624247db7a84da8c6bdffb800bc
ms.sourcegitcommit: 45657123a5db50aaecdb96d068712623d775f31c
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/30/2020
ms.locfileid: "87443832"
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

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>Uppdatera till enhet-ikoner i Företagsportalen och Intune-appar på Android<!-- 6057023  -->
Vi uppdaterar enhetsikonerna i Företagsportalen och Intune-appar på Android-enheter för att skapa ett modernt utseende och att anpassa sig till designsystemet Microsoft Fluent. Relaterad information finns i [Uppdatera till ikoner i företagsportalappen för iOS/iPadOS och macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS Företagsportalen kommer att stödja Apples automatiserade enhetsregistrering utan användartillhörighet<!-- 7282707  --> 
iOS Företagsportalen kommer att stödjas på enheter som har registrerats med Apples automatiserade enhetsregistrering utan att kräva en tilldelad användare. En slutanvändare kan logga in på iOS Företagsportalen för att etablera sig själva som primär användare på en iOS/iPad-enhet som registrerats utan enhetstillhörighet. Mer information om automatiserad enhetsregistrering finns i [Registrera iOS/iPadOS-enheter automatiskt med Apples automatiska enhetsregistrering](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="the-windows-company-portal-adds-configuration-manager-application-support---4297660---"></a>Windows Företagsportalen lägger till stöd för appen Configuration Manager<!-- 4297660 -->
Windows Företagsportalen har nu stöd för Configuration Manager-appar. Med den här funktionen kan slutanvändare se distribuerade appar i Configuration Manager och Intune i Windows Företagsportalen för samhanterade kunder. Det här stödet hjälper administratörer att konsolidera sina olika portalmiljöer för slutanvändare. Mer information finns i [Använd Företagsportalappen på samhanterade enheter](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Enhetskonfiguration

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Ställ in enhetsefterlevnadstillståndet från MDM-tredjepartspartners<!-- 6361689   -->
Microsoft 365-kunder som äger MDM-lösningar från tredje part kommer att kunna tillämpa principer för villkorsstyrd åtkomst för Microsoft 365-appar i iOS och Android via integrering med Microsoft Intune-tjänsten för enhetsefterlevnad. Tredjepartsleverantörerna använder Intune-tjänsten för enhetsefterlevnad till att skicka efterlevnadsdata om enheter till Intune. Intune utvärderar sedan dessa data, avgör om enheten är betrodd och ställer in attribut för villkorsstyrd åtkomst i Azure AD.  Kunder måste ange principer för villkorsstyrd åtkomst i Azure AD antingen från administrationscentret för Microsoft Endpoint Manager eller i Azure AD-portalen.

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Skapa PKCS-certifikatsprofiler för fullständigt hanterade Android Enterprise-enheter (COBO)<!-- 4839686 -->
Du kan skapa PKCS-certifikatsprofiler när du ska distribuera certifikat till Android Enterprise-enhetsägaren och arbetsprofilsenheter (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise > Enbart enhetens ägare**, eller **Android Enterprise > Enbart arbetsprofil** för plattform > **PKCS** för profil).

Snart kommer du att kunna skapa PKCS-certifikatsprofiler för fullständigt hanterade Android Enterprise-enheter. Anslutningsprogram för Intune PFX-certifikat krävs. Om du inte använder SCEP, och bara använder PKCS, kan du ta bort NDES-anslutningsprogrammet när du har installerat det nya PFX-anslutningsprogrammet. Det nya PFX-anslutningsprogrammet importerar PFX-filer och distribuerar PKCS-certifikat till alla plattformar.

Mer information om PKCS-certifikat finns i [Konfigurera och använda PKCS-certifikat med Intune](../protect/certficates-pfx-configure.md).

Gäller för:
- Fullständigt hanterat Android Enterprise (COBO)

### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631---"></a>Använd NetMotion som VPN-anslutningstyp för iOS/iPad- och macOS-enheter<!-- 1333631 -->
När du skapar en VPN-profil är NetMotion tillgängligt som en VPN-anslutningstyp (**Enheter** > **Enhetskonfiguration** > **Skapa profil** > **iOS/iPad** eller **macOS** för plattform > **VPN-** för profil > **NetMotion** för anslutningstyp).

Mer information om VPN-profiler i Intune finns i [Skapa VPN-profiler för att ansluta till VPN-servrar](../configuration/vpn-settings-configure.md).

Gäller för:
- iOS/iPadOS
- macOS

### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024---"></a>Fler PEAP-alternativ (Protected Extensible Authentication Protocol) för Windows 10 Wi-Fi-profiler<!-- 3805024 -->
På Windows 10-enheter kan du skapa Wi-Fi-profiler med EAP (Extensible Authentication Protocol) för att autentisera Wi-Fi-anslutningar (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Windows 10 och senare** som plattform > **Wi-Fi** som profil > **Företag**). När du väljer skyddad EAP (PEAP) finns det nya tillgängliga inställningar:

- **Utför serververifiering i PEAP fas 1**: I PEAP-förhandlingsfas 1 validerar enheterna certifikatet och verifierar servern.
  - **Inaktivera användaruppmaningar om att verifiera servern i PEAP fas 1**: I PEAP-förhandlingsfas 1 visas inte uppmaningar som ber användare att auktorisera nya PEAP-servrar för betrodda certifikatutfärdare.
- **Kräv kryptografisk bindning**: Förhindrar anslutningar till PEAP-servrar som inte använder krypteringsbindning under PEAP-förhandlingen.

Om du vill se de inställningar som du kan konfigurera för tillfället, så gå till [Lägga till Wi-Fi-inställningar för enheter med Windows 10 och senare](../configuration/wi-fi-settings-windows.md).

Gäller för: 
- Windows 10 och senare

### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576---"></a>Konfigurera macOS Microsoft Enterprise SSO-plugin-programmet<!-- 5627576 -->
Microsoft Azure AD-teamet skapade en app för omdirigering med enkel inloggning som gör att användare med macOS 10.15+ kan få åtkomst till Microsoft-appar, organisationsappar och webbplatser som stöder Apples SSO-funktion och autentisera med Azure AD. Med Microsoft Enterprises SSO-tillägget kan du konfigurera SSO-tillägget med den nya typen av Microsoft Azure AD-apptillägg (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **macOS** för plattform > **Enhetsfunktioner** > för profil > **Apptillägg för enkel inloggning** > Typ av SSO-apptillägg > **Microsoft Azure AD**).

För att få enkel inloggning med Microsoft Azure AD SSO-apptilläggstypen måste användarna installera och logga in på företagsportalsappen på sina macOS-enheter. 

Mer information om macOS-apptillägg för enkel inloggning finns i [Apptillägg för enkel inloggning](../configuration/device-features-configure.md#single-sign-on-app-extension).

Gäller för:
- macOS 10.15 och senare

### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991---"></a>Använd SSO-apptillägg på fler iOS/iPad-appar med Microsoft Enterprise SSO-plugin-programmet<!-- 7369991 -->
[Microsoft Enterprise SSO-plugin-programmet för Apple-enheter](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin) kan användas med alla appar som stöder SSO-apptillägg. I Intune innebär den här funktionen att plugin-programmet fungerar med mobila iOS/iPad-appar som inte använder Microsoft Authentication Library (MSAL) för Apple-enheter. Apparna behöver inte använda MSAL, men de måste autentiseras med Azure AD-slutpunkter.

Konfigurera dina iOS/iPad-appar så att de kan använda SSO med plugin-programmet genom att lägga till appaketidentifierarna i en iOS/iPad-konfigurationsprofil (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPad** för plattform > **Enhetsfunktioner** för profil > **Apptillägg för enkel inloggning** > **Microsoft Azure AD** för SSO-apptilläggstyp > **Appakets-ID:n**).

Om du vill se de aktuella inställningarna för SSO-tillägg som du kan konfigurera, så gå till [Enkel inloggning för apptillägg](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

Gäller för:
- iOS/iPadOS

### <a name="improvement-to-update-device-settings-page-in-company-portal-app-for-android-to-show-descriptions---7414768---"></a>Förbättring av visning av beskrivningar på sidan Uppdatera enhetsinställningar i företagsportalsappen för Android<!-- 7414768 -->
I företagsportalsappen på Android-enheter visar sidan **Uppdatera enhetsinställningar** de inställningar som en användare behöver uppdatera för att följa standard. Vi har förbättrat användarupplevelsen så att listade inställningar utökas som standard så att beskrivningen och knappen **Lös** (om tillämpligt) visas. Tidigare doldes dessa som standard. Det nya standardbeteendet minskar antalet klick, så att användarna kan lösa problem snabbare.

<!-- ***********************************************-->
<!-- ## Device enrollment-->




<!-- ***********************************************-->
## <a name="device-management"></a>Enhetshantering

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Stöd för PowerShell-skript för BYOD-enheter<!-- 1862833  -->
PowerShell-skript kommer att stödja Azure AD-registrerade enheter i Intune. Mer information om PowerShell finns i [Använda PowerShell-skript på Windows 10-enheter i Intune](../apps/intune-management-extension.md). Den här funktionen stöder inte enheter som kör Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics innehåller enhetsinformationslogg<!--6014987  -->
Loggar med Intune-enhetsinformation kommer att vara tillgängliga i **Rapporter** > **Logganalys**. Du kan korrelera enhetsinformationen för att bygga anpassade frågor och Azure-arbetsböcker.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Klientkoppling: Enhetstidslinje i administrationscentret<!--7220536, CM7141381 -->
När Configuration Manager synkroniserar en enhet till Microsoft Endpoint Manager via klientanslutning kan du se en tidslinje med händelser. Den här tidslinjen visar tidigare aktivitet på enheten som kan hjälpa dig att felsöka problem. Mer information finns i [Teknisk förhandsversion av Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline).  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Klientkoppling: Installera ett program från administrationscentret<!-- 7220536, CM6024389 -->
Du kommer att kunna initiera en programinstallation i realtid för en klientansluten enhet från administrationscentret för Microsoft Endpoint Management. Mer information finns i [Teknisk förhandsversionen av Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps).

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Klientkoppling: CMPivot från administrationscentret<!--7220536, CM6024392 -->
Du kommer att kunna utnyttja kraften hos [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) i administrationscentret för Microsoft Endpoint Manager. Gör det möjligt för fler, till exempel supportavdelningen, att starta realtidsfrågor från molnet till en enskild ConfigMgr-hanterad enhet och returnera resultaten till administrationscentret. Detta ger alla de traditionella fördelarna med CMPivot, vilket gör det möjligt för IT-administratörer och andra utsedda personer att snabbt bedöma status för enheter i deras miljöer och vidta åtgärder. Mer information finns i [Teknisk förhandsversionen av Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot). 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Klientkoppling: Kör skript från administrationscentret<!--7220536, CM6234688 -->
Du har möjlighet att utnyttja kraften i Configuration Managers lokala [Run Scripts](../../configmgr/apps/deploy-use/create-deploy-scripts.md)-funktion i administrationscentret för Microsoft Endpoint Manager. Tillåt ytterligare personer, som supportavdelningen, att köra PowerShell-skript från molnet mot en enskild Configuration Manager-hanterad enhet. Detta ger alla traditionella fördelar med PowerShell-skript som redan har definierats och godkänts av Configuration Manager-administratören till den nya miljön. Mer information finns i [Teknisk förhandsversionen av Configuration Manager 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts). 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Distribuera programuppdateringar till macOS-enheter <!-- 3194876 -->
Du kommer att kunna distribuera programuppdateringar till grupper med macOS-enheter. Den här funktionen inkluderar kritisk, inbyggd programvara, konfigurationsfil och andra uppdateringar. Du kommer att kunna skicka uppdateringar nästa gång enheten checkar in eller välja ett veckoschema för att distribuera uppdateringar inom eller utanför tidsfönster som du anger. Detta hjälper dig när du vill uppdatera enheter utanför standard arbetstid eller när din help desk är fullständigt bemannad. Du får också en detaljerad rapport om alla macOS-enheter med distribuerade uppdateringar. Du kan gå in på detaljnivå i rapporten på enhetsbas för att se status för särskilda uppdateringar.

### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322---"></a>Tillhörande licenser återkallades innan en Apple VPP-token togs bort<!--6195322 -->
När du tar bort en Apple VPP-token i Microsoft Endpoint Manager i en framtida uppdatering, så återkallas alla Intune-tilldelade licenser som är kopplade till denna token automatiskt innan token tas bort.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Mall för Power BI-efterlevnadsrapport V2.0<!-- 636958  -->
Administratörer kan uppdatera versionen av Power BI-efterlevnadsrapporten från V1.0 till V2.0. V2.0 har en förbättrad design och ändringar av de beräkningar och data som visas som en del av mallen. Mer information finns i [Ansluta till Data Warehouse med Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Säkerhet

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Stöd för appskyddsprinciper för Symantec Endpoint Security och Check Point Sandblast<!--  4452423, 4731168 -->

I oktober 2019 utökades Intunes appskyddsprinciper med möjligheten att använda data från några av våra Microsoft Threat Defense-partner (MTD-partner). Vi lägger till stöd för följande partner så att du kan använda en appskyddsprincip för att blockera eller selektivt rensa användarnas företagsdata baserat på hälsotillståndet för en enhet:

- **Check Point Sandblast** på Android, iOS och iPadOS
- **Symantec Endpoint Security** på Android, iOS och iPadOS

Information om hur du använder appskyddsprinciper med MTD-partner finns i [Skapa en Mobile Threat Defense-appskyddsprincip med Intune](../protect/mtd-app-protection-policy.md).

### <a name="microsoft-defender-atp-creates-endpoint-manager-security-task-with-vulnerability-details---5568193----"></a>Microsoft Defender ATP skapar en Endpoint Manager-säkerhetsuppgift med säkerhetsrisksinformation<!-- 5568193  -->
Hot- och säkerhetsriskshantering (TVM) i Microsoft Defender ATP identifierar felkonfigurerade säkerhetsinställningar på enheterna. Administratörer använder den här informationen för att uppdatera sårbara enheter.

Snart kan Microsoft Defender ATP skapa en Endpoint Manager-säkerhetsuppgift (**Endpoint Manager** > **Slutpunktssäkerhet** > **Säkerhetsuppgifter**) med information om säkerhetsrisken och vilke enheter som berörs. IT-administratörer kan acceptera säkerhetsrisksuppgiften och distribuera den nödvändiga konfigurationen. 

Mer information om säkerhetsuppgifter finns i [Använda Intune till att åtgärda säkerhetsrisker som identifierats av Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md).

### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119----"></a>Ändringar av undantag för antiviruspolicyn för slutpunktssäkerhet<!--5583940, 6018119  -->
Vi presenterar två ändringar för att hantera listorna för Microsoft Defender Antivirus-undantag som du kan konfigurera som en del av en Endpoint Security-princip för antivirus. (**Slutpunktssäkerhet** > **Antivirus** > **Skapa princip** > **Windows 10 och senare** för plattform). Dessa två ändringar bidrar till att förhindra konflikter mellan principer, och befintliga principer som stod i konflikt kommer inte längre att stå i konflikt med listan över undantag:

- Först lägger vi till en ny profiltyp för Windows 10 och senare. **Microsoft Defender Antivirus-undantag**.  Den här nya profiltypen inkluderar bara inställningarna för att ange en lista över Defender-*processer*, *filnamnstillägg* och *filer* och *mappar* som du inte vill att Microsoft Defender ska genomsöka. Detta kan hjälpa dig att förenkla hanteringen av dina undantagslistor genom att de skiljs från andra principkonfigurationer.
- Den andra ändringen innebär att listan över undantag som du definierar i olika profiler sammanfogas till en enda lista över undantag för varje enhet eller användare, baserat på de enskilda principer som gäller för en viss användare eller enhet. När du exempelvis fokuserar på en användare med tre separata principer, så slås undantagslistorna från dessa tre principer samman till en enda stor uppsättning av Microsoft Defender Antivirus-undantag, som sedan tillämpas på användaren. Den här sammanslagningen innehåller undantagslistorna från den nya profiltypen som har lagts till, samt från befintliga principer som har konfigurerats i en *Microsoft Defender Antivirus*-profil.



<!-- ***********************************************-->
## <a name="notices"></a>Meddelanden

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Se även

Mer information om den senaste utvecklingen finns i [Nyheter i Microsoft Intune](whats-new.md).
