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
ms.openlocfilehash: 107ac1e2aef18bcb72a6fe1f94eade23c3f85319
ms.sourcegitcommit: 79ffc8afed164c408db6994806d71f64d1fc0b8f
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85216526"
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
<!--## App management-->


<!-- ***********************************************-->
## <a name="device-configuration"></a>Enhetskonfiguration

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>Ställ in enhetsefterlevnadstillståndet från MDM-tredjepartspartners<!-- 6361689   -->
Microsoft 365-kunder som äger MDM-lösningar från tredje part kommer att kunna tillämpa principer för villkorsstyrd åtkomst för Microsoft 365-appar i iOS och Android via integrering med Microsoft Intune-tjänsten för enhetsefterlevnad. Tredjepartsleverantörerna använder Intune-tjänsten för enhetsefterlevnad till att skicka efterlevnadsdata om enheter till Intune. Intune utvärderar sedan dessa data, avgör om enheten är betrodd och ställer in attribut för villkorsstyrd åtkomst i Azure AD.  Kunder måste ange principer för villkorsstyrd åtkomst i Azure AD antingen från administrationscentret för Microsoft Endpoint Manager eller i Azure AD-portalen.  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Nya inställningar för Windows 10 och nyare enheter<!-- 6602122  -->
När du skapar en VPN-profil med IKEv2-anslutningstypen, så finns det nya inställningar som du kan konfigurera (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Windows 10 och senare** för plattform > **VPN** för profil > **Bas-VPN**):

- **Enhetstunnel**: Tillåter enheter att automatiskt ansluta till VPN utan krav på interaktion från användarens sida, inklusive användarinloggning. Den här funktionen kräver att du aktiverar **Alltid på**, och använder **Datorcertifikat** som autentiseringsmetod.
- Kryptografisvitsinställningar: Konfigurera de algoritmer som används för att skydda IKE och underordnade säkerhetskopplingar, vilket gör det möjligt för dig att matcha klient- och serverinställningar.

Om du vill se vilka inställningar du kan konfigurera kan du gå till [Windows-enhetsinställningar för att lägga till VPN-anslutningar med Intune](../configuration/vpn-settings-windows-10.md).

Gäller för:
- Windows 10 och senare


<!-- ***********************************************-->
<!--## Device enrollment-->



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

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Ny sammanslagningslogik för Windows 10-enheter<!--179048-->
Om en kund återskapar en enhet idag och sedan registrerar om den, visas flera poster för enheten i administrationskonsolen för Microsoft Endpoint Manager. I den nya sammanslagningslogik som är under utveckling slås sådana dubblettposter samman för Windows 10-enheter.

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
