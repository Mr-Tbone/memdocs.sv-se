---
title: Under utveckling – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-funktioner under utveckling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5afca831e2f3cbcda69150adcbbcff996bf99554
ms.sourcegitcommit: 01c1ca337e82c5e8e92153079ed89f79e20bde9e
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86157815"
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

### <a name="smime-for-outlook-on-ios-and-android-enterprise-devices-managed-without-enrollment---6517155----"></a>S/MIME för Outlook på iOS- och Android Enterprise-enheter som hanteras utan registrering<!-- 6517155  -->
Du kommer att kunna aktivera S/MIME för Outlook på iOS- och Android Enterprise-enheter med appkonfigurationsprinciper för enheter hanterade utan registrering. I [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), väljer du **Appar** > **Appkonfigurationsprinciper** > **Lägg till** > **Hanterade appar**. Dessutom kan du välja om du vill tillåta användare att ändra den här inställningen i Outlook. Mer information om konfigurationsinställningar för Outlook finns i [Konfigurationsinställningar för Microsoft Outlook](../apps/app-configuration-policies-outlook.md).

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS Företagsportalen kommer att stödja Apples automatiserade enhetsregistrering utan användartillhörighet<!-- 7282707  --> 
iOS Företagsportalen kommer att stödjas på enheter som har registrerats med Apples automatiserade enhetsregistrering utan att kräva en tilldelad användare. En slutanvändare kan logga in på iOS Företagsportalen för att etablera sig själva som primär användare på en iOS/iPad-enhet som registrerats utan enhetstillhörighet. Mer information om automatiserad enhetsregistrering finns i [Registrera iOS/iPadOS-enheter automatiskt med Apples automatiska enhetsregistrering](../enrollment/device-enrollment-program-enroll-ios.md).

### <a name="win32-app-installation-notifications-and-the-company-portal---7485945----"></a>Installationsmeddelanden för Win32-appar och Företagsportalen<!-- 7485945  -->
Slutanvändare kommer att kunna bestämma om de program som visas i [Microsoft Intune Web Företagsportalen](https://portal.manage.microsoft.com/) ska öppnas av Företagsportal-appen eller webbföretagsportalen. Det här alternativet är bara tillgängligt om slutanvändaren har installerat Företagsportal-appen och startar ett webbföretagsportal-program utanför en webbläsare.

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>Företagsportalen lägger till stöd för Konfigurationshanterarprogram<!-- 4297660 -->
Företagsportalen stöder nu Konfigurationshanterarprogram. Med den här funktionen kan slutanvändare se både program från Konfigurationshanteraren och sådana som distribuerats av Intune i Företagsportalen för samhanterade kunder. Det här stödet hjälper administratörer att konsolidera sina olika portalmiljöer för slutanvändare. Mer information finns i [Använd Företagsportalappen på samhanterade enheter](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal).

<!-- ***********************************************-->
## <a name="device-configuration"></a>Enhetskonfiguration

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Ställ in enhetsefterlevnadstillståndet från MDM-tredjepartspartners<!-- 6361689   -->
Microsoft 365-kunder som äger MDM-lösningar från tredje part kommer att kunna tillämpa principer för villkorsstyrd åtkomst för Microsoft 365-appar i iOS och Android via integrering med Microsoft Intune-tjänsten för enhetsefterlevnad. Tredjepartsleverantörerna använder Intune-tjänsten för enhetsefterlevnad till att skicka efterlevnadsdata om enheter till Intune. Intune utvärderar sedan dessa data, avgör om enheten är betrodd och ställer in attribut för villkorsstyrd åtkomst i Azure AD.  Kunder måste ange principer för villkorsstyrd åtkomst i Azure AD antingen från administrationscentret för Microsoft Endpoint Manager eller i Azure AD-portalen.  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Nya inställningar för Windows 10 och nyare enheter<!-- 6602122  -->
När du skapar en VPN-profil med IKEv2-anslutningstypen, så finns det nya inställningar som du kan konfigurera (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Windows 10 och senare** för plattform > **VPN** för profil > **Bas-VPN**):

- **Enhetstunnel**: Gör att enheter automatiskt kan ansluta till VPN utan krav på interaktion från användarens sida, inklusive användarinloggning. Den här funktionen kräver att du aktiverar **Alltid på**, och använder **Datorcertifikat** som autentiseringsmetod.
- Kryptografisvitsinställningar: Konfigurera de algoritmer som används för att skydda IKE och underordnade säkerhetskopplingar, vilket gör det möjligt för dig att matcha klient- och serverinställningar.

Om du vill se vilka inställningar du kan konfigurera kan du gå till [Windows-enhetsinställningar för att lägga till VPN-anslutningar med Intune](../configuration/vpn-settings-windows-10.md).

Gäller för:
- Windows 10 och senare

### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184----"></a>Nya funktioner för hanterad Startskärm på Android Enterprise-enhetsägars dedikerade enheter (COSU)<!-- 7414175 7133328 7133720 7134873 7135184  -->
På Android Enterprise-enheter kommer administratörer att kunna använda enhetskonfigurationsprofiler för att anpassa den hanterade startskärmen på dedikerade enheter som använder helskärmsläge med flera appar (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise** för plattform > **enbart enhetsägare** > **Enhetsbegränsningar** för profil > **Enhetsupplevelse**).

Mer specifikt kan du:

- Anpassa ikoner, ändra skärmorientering och visa appmeddelanden i aktivitetsikoner <!--7414175-->
- Dölja startpunkten för Hanterade inställningar <!--7133328-->
- Enklare åtkomst till felsökningsmenyn <!--7133720-->
- Skapa en lista med tillåtna Wi Fi-nätverk <!-- 7134873-->
- Få enklare åtkomst till enhetsinformationen <!-- 7135184-->

Mer information finns i [Enhetsinställningarna för Android Enterprise tillåter eller begränsar funktioner](../configuration/device-restrictions-android-for-work.md).

Gäller för:

- Android Enterprise-enhetsägare, dedikerade enheter (COBO)

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Enhetsregistrering

### <a name="corporate-owned-personally-enabled-devices-preview--4442275---"></a>Företagsägda, personligt aktiverade enheter (förhandsversion)<!--4442275 -->
Intune stöder Android Enterprise-företagsägda enheter med en arbetsprofil för OS-versionerna Android 8 och senare. Företagsägda enheter med en arbetsprofil är ett av företagshanteringsscenarierna i Android Enterprise-lösningen. Det här scenariot gäller för enheter för enkelanvändare som är avsedda för företagsbruk och personligt bruk. Det här företagsägda, personligt aktiverade (COPE) scenariot erbjuder:

- containerisering av arbetsprofiler och personlig profiler
- kontroll på enhetsnivå för administratörer
- en garanti för slutanvändare att deras personliga data och program kommer att förbli privata

Den första offentliga förhandsversionen kommer att innehålla en delmängd av de funktioner som kommer att ingå i den allmänt tillgängliga versionen. Ytterligare funktioner kommer att läggas till löpande. De funktioner som är tillgängliga i den första förhandsgranskningen är:

- Registrering: Administratörer kan skapa flera registreringsprofiler med unika token som inte upphör att gälla. Enhetsregistrering kan göras via NFC, tokeninmatning, QR-kod, Zero Touch eller Knox Mobile-registrering.
- Enhetskonfiguration: En delmängd av de befintliga fullständigt hanterade och dedikerade enhetsinställningarna.
- Enhetsefterlevnad: Efterlevnadsprinciper som är tillgängliga för tillfället för fullständigt hanterade enheter.
- Enhetsåtgärder: Ta bort enheten (fabriksåterställning), starta om enheten och lås enheten.  
- Apphantering: Apptilldelningar, appkonfiguration och tillhörande rapporteringsfunktioner 
- Villkorlig åtkomst



<!-- ***********************************************-->
## <a name="device-management"></a>Enhetshantering

### <a name="device-compliance-logs-now-in-english--6014904---"></a>Enhetsefterlevnadsloggarna finns nu på engelska<!--6014904 -->
IntuneDeviceComplianceOrg-loggarna har bara uppräkningar för ComplianceState, OwnerType och DeviceHealthThreatLevel. I en framtida uppdatering kommer dessa loggar att ha engelsk information i kolumnerna.

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

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Ny sammanslagningslogik för Windows 10-enheter<!--179048-->
Om en kund återskapar en enhet idag och sedan registrerar om den, visas flera poster för enheten i administrationskonsolen för Microsoft Endpoint Manager. I den nya sammanslagningslogik som är under utveckling slås sådana dubblettposter samman för Windows 10-enheter.

### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805---"></a>Uppdateringar av fjärrlåsningsåtgärden för macOS-enheter<!--7032805 -->
Uppdateringar av fjärrlåsningsåtgärden för macOS-enheter kommer att innehålla:
- PIN-koden för återställning visas i 30 dagar innan den tas bort (i stället för sju dagar).
- Om en administratör har en andra webbläsare öppen och försöker att utlösa kommandot igen från en annan flik eller webbläsare, tillåter Intune att kommandot går igenom. Men rapporteringsstatus kommer att anges till misslyckad i stället för att skapa en ny PIN-kod.
- Administratören kommer inte kunna utfärda ett till fjärrlåsningskommando om det tidigare kommandot fortfarande är väntande eller om enheten inte har checkat in igen.
Dessa ändringar är utformade för att förhindra att rätt PIN-kod skrivs över efter flera fjärrlåsnings-kommandon.

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Distribuera programuppdateringar till macOS-enheter <!-- 3194876 -->
Du kommer att kunna distribuera programuppdateringar till grupper med macOS-enheter. Den här funktionen inkluderar kritisk, inbyggd programvara, konfigurationsfil och andra uppdateringar. Du kommer att kunna skicka uppdateringar nästa gång enheten checkar in eller välja ett veckoschema för att distribuera uppdateringar inom eller utanför tidsfönster som du anger. Detta hjälper dig när du vill uppdatera enheter utanför standard arbetstid eller när din help desk är fullständigt bemannad. Du får också en detaljerad rapport om alla macOS-enheter med distribuerade uppdateringar. Du kan gå in på detaljnivå i rapporten på enhetsbas för att se status för särskilda uppdateringar.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

### <a name="additional-data-warehouse-v10-properties---6125732-----"></a>Ytterligare egenskaper för Data Warehouse v 1.0<!-- 6125732   -->
Ytterligare egenskaper finns tillgängliga med Intune Data Warehouse v 1.0. Följande egenskaper exponeras nu via [enheter](../developer/reports-ref-devices.md#devices)-entiteten:
- `ethernetMacAddress` – den unika nätverksidentifieraren för den här enheten.
- `office365Version` – den version av Office 365 som är installerad på enheten.

Följande egenskaper är nu tillgängliga via [devicepropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories)-entiteten:
- `physicalMemoryInBytes` – fysiskt minne i bytes.
- `totalStorageSpaceInBytes` – Total lagringskapacitet i bytes.

Mer information finns i [Microsoft Intune-API:et Data Warehouse](../developer/reports-nav-intune-data-warehouse.md).

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Mall för Power BI-efterlevnadsrapport V2.0<!-- 636958  -->
Administratörer kan uppdatera versionen av Power BI-efterlevnadsrapporten från V1.0 till V2.0. V2.0 har en förbättrad design och ändringar av de beräkningar och data som visas som en del av mallen. Mer information finns i [Ansluta till Data Warehouse med Power BI](../developer/reports-proc-get-a-link-powerbi.md).

<!-- ***********************************************-->
## <a name="role-based-access-control"></a>Rollbaserad åtkomstkontroll

### <a name="scope-tag-support-for-customization-policies--6182440---"></a>Stöd för omfångstaggar för anpassningsprinciper<!--6182440 -->
Du kommer att kunna tilldela omfångstaggar till anpassningsprinciper. Det gör du genom att gå till [Administrationscenter för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Klientadministration**> **Anpassning** där du ser konfigurationsalternativ för **Omfångstaggar**.

### <a name="assign-profile-and-update-profile-permission-changes--7177586---"></a>Behörighetsändringar för Tilldela profil och Uppdatera profil<!--7177586 -->
Rollbaserade åtkomstkontrollbehörigheter ändras för Tilldela profil och Uppdatera profil:
- Tilldela profil: Administratörer med den här behörigheten kan också tilldela profiler till tokens och tilldela en standardprofil till en token.
- Uppdatera profil: Administratörer med den här behörigheten kan bara uppdatera befintliga profiler.

<!-- ***********************************************-->
## <a name="security"></a>Säkerhet

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Stöd för appskyddsprinciper för Symantec Endpoint Security och Check Point Sandblast<!--  4452423, 4731168 -->

I oktober 2019 utökades Intunes appskyddsprinciper med möjligheten att använda data från några av våra Microsoft Threat Defense-partner (MTD-partner). Vi lägger till stöd för följande partner så att du kan använda en appskyddsprincip för att blockera eller selektivt rensa användarnas företagsdata baserat på hälsotillståndet för en enhet:

- **Check Point Sandblast** på Android, iOS och iPadOS
- **Symantec Endpoint Security** på Android, iOS och iPadOS

Information om hur du använder appskyddsprinciper med MTD-partner finns i [Skapa en Mobile Threat Defense-appskyddsprincip med Intune](../protect/mtd-app-protection-policy.md).

### <a name="store-the-recovery-key-for-a-macos-device-that-was-encrypted-with-filevault-before-enrolling-with-intune--5239424-----"></a>Lagra återställningsnyckeln för en macOS-enhet som har krypterats med FileVault innan du registrerar med Intune<!--5239424   -->
Snart behöver slutanvändare av en macOS-enhet som inte krypterats av FileVault-principen från Intune, eller som har krypterats innan de registrerades med Intune, inte dekryptera sin enhet så att den sedan kan krypteras om av Intune. I stället kan den aktuella krypteringen vara på plats och användaren kan gå till Företagsportalwebbplatsen där de kan välja *Lagra återställningsnyckel* för att skicka in sin personliga återställningsnyckel för den krypterade macOS-enheten. När en giltig nyckel skickas in roterar Intune den personliga nyckeln för att generera en ny nyckel som är tillgänglig för användaren via Företagsportalwebbplatsen, iOS/Företagsportalen, Android Företagsportalen eller Intune-appen. Användarna kan sedan komma åt dessa platser från vilken enhet som helst för att visa nyckeln om de skulle bli utlåsta från sin macOS-enhet.

### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632----"></a>Dölj den personliga återställningsnyckeln från en enhetsanvändare vid diskkrypteringen i macOS FileVault<!--  5475632  -->
Vi lägger till en ny inställning som heter *Dölj återställningsnyckeln* till en princip för återställning av slutpunktens säkerhetsdiskar för FileVault (**Endpoint Security** > **Diskkryptering** > **Skapa profil** > **macOS** > **FileVault**). När du aktiverar den nya inställningen döljer Intune den personliga återställningsnyckeln från användaren av macOS-enheten vid kryptering. Genom att dölja nyckeln för tillfället kan du hålla den säker eftersom användarna inte kan skriva ned den medan de väntar på att enheten ska krypteras. Om återställning behövs kan en användare i stället alltid använda valfri enhet för att visa sin personliga återställningsnyckel via Intune Företagsportalwebbplatsen.

### <a name="improved-view-of-security-baseline-details-for-devices---5536846-----"></a>Förbättrad vy av säkerhetsbaslinjeinformation för enheter<!-- 5536846   -->
Vi arbetar för att förbättra visningen av information för inställningarna för säkerhetsbaslinjen, när du går in på detaljnivå för en enhet (**Endpoint Security** > **Enheter**).  För varje tilldelad säkerhetsbaslinje kan du visa en platt lista med information om varje inställning som inkluderar inställningskategorier, inställningsnamn och status för varje inställning på enheten.

### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801----"></a>Hantera källplatser för definitionsuppdateringar med Endpoint Security Antivirus-principen för Windows 10-enheter<!-- 6347801  -->  
Vi lägger till två nya inställningar i *Uppdateringar*-kategorin för Enpoint Security Antivirus-principen för Windows 10-enheter som kan hjälpa dig att hantera hur enheter hämtar uppdateringsdefinitioner (**Slutpunktssäkerhet** > ** Antivirus** > **Skapa princip** > **Windows 10 och senare** > **Microsoft Defender Antivirus**).

Med de nya inställningarna kan du lägga till UNC-filresurser som källplatser för nedladdning av definitionsuppdateringar och definiera den i ordning i vilken olika källplatser kontaktas. De nya inställningarna hanterar följande Defender-kryptografiproviders:

- [signatureupdatefilesharessources](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)
- [signatureupdatefallbackorder](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-moving-out-of-preview---7303816-----"></a>Princip för slutpunktsidentifiering och svar för registrering av klientanslutna enheter till MDATP flyttas ut ur förhandsversionen<!-- 7303816   -->
Som en del av Endpoint Security i Intune kommer stöd för principerna slutpunktsidentifiering och svar (EDR) att användas med enheter som hanteras av konfigurationshanteraren snart att gå ut ur förhandsversion och bli allmänt tillgängliga (**Endpoint Security** > **Slutpunktsidentifiering och svar** > **Skapa princip** > **Windows 10 och Windows Server**). När du konfigurerar [Klientanslutning för konfigurationshanteraren](../../configmgr/tenant-attach/device-sync-actions.md) kan du sedan använda EDR-principerna för att publicera enheter som hanteras av konfigurationshanteraren till Microsoft Defender Avancerat skydd (Microsoft Defender ATP). 

### <a name="improvements-for-the-security-baselines-node---7433136-----"></a>Förbättringar av säkerhetsbaslinjenoden<!-- 7433136   -->
För att förbättra användbarheten för säkerhetsbaslinjenoden i administrationscenter för Microsoft Endpoint Manager, tar vi bort fliken *Översikt* för varje baslinje och öppnar i stället baslinjernas **Profil**-flik (**Endpoint Security** > **Säkerhetsbaslinjer** > *baslinje*).

*Översikt*-sidan för varje baslinje visar diagram och paneler som sammanställer resultat från den senaste baslinjeversionen som du har distribuerat. Informationen är en dubblett av vad du ser om du går in på detaljnivå i en version för mer information. När du har tagit bort *Översikt*-sidan kommer dessa diagram och den sammanställda informationen vara kvar när du går in direkt på detaljnivå för versionen.  

### <a name="firewall-rule-migration-tool-preview---6423187----"></a>Migreringsverktyg för brandväggsregel förhandsversion<!-- 6423187  -->
Som en offentlig förhandsversion så arbetar vi med ett PowerShell-baserat verktyg som kommer att migrera Windows Defender brandväggsregler. När du installerar och kör verktyget skapas automatiskt Endpoint Security brandväggsregelprinciper för Intune som baseras på den aktuella konfigurationen av en Windows 10-klient.

### <a name="new-settings-for-the-device-control-profile-in-endpoint-security-attack-surface-reduction-policy--7032084---"></a>Nya inställningar för enhetskontrollprofilen i Endpoint Security-principen för minskning av attackytan<!--7032084 -->
Vi lägger till flera inställningar för Windows 10-enheter i enhetskontrollprofilen för en Endpoint Security-princip för minskning av attackytan (**Endpoint Security** > **Minskning av attackytan** > **Skapa princip** > **Windows 10 och senare** > **Enhetskontroll**). 

De nya inställningarna kommer att vara desamma som de inställningar som finns tillgängliga idag i [Profiler för enhetsbegränsning](../configuration/device-restrictions-windows-10.md) för *Enhetskonfiguration*. Inställningarna som läggs till i profilen för *Enhetskontroll* ska innehålla olika Bluetooth-inställningar.  


<!-- ***********************************************-->
## <a name="notices"></a>Meddelanden

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Se även

Mer information om den senaste utvecklingen finns i [Nyheter i Microsoft Intune](whats-new.md).
