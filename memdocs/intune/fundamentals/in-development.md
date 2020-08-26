---
title: Under utveckling – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-funktioner under utveckling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0d443cb784c19956f52347a10f4123c622ab82a8
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820077"
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

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>Skapa PKCS-certifikatsprofiler för fullständigt hanterade Android Enterprise-enheter (COBO)<!-- 4839686 -->
Du kan skapa PKCS-certifikatsprofiler när du ska distribuera certifikat till Android Enterprise-enhetsägaren och arbetsprofilsenheter (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise > Enbart enhetens ägare**, eller **Android Enterprise > Enbart arbetsprofil** för plattform > **PKCS** för profil).

Snart kommer du att kunna skapa PKCS-certifikatsprofiler för fullständigt hanterade Android Enterprise-enheter. Anslutningsprogram för Intune PFX-certifikat krävs. Om du inte använder SCEP, och bara använder PKCS, kan du ta bort NDES-anslutningsprogrammet när du har installerat det nya PFX-anslutningsprogrammet. Det nya PFX-anslutningsprogrammet importerar PFX-filer och distribuerar PKCS-certifikat till alla plattformar.

Mer information om PKCS-certifikat finns i [Konfigurera och använda PKCS-certifikat med Intune](../protect/certficates-pfx-configure.md).

Gäller för:
- Fullständigt hanterat Android Enterprise (COBO)

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


<!-- ***********************************************-->
## <a name="notices"></a>Meddelanden

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Se även

Mer information om den senaste utvecklingen finns i [Nyheter i Microsoft Intune](whats-new.md).
