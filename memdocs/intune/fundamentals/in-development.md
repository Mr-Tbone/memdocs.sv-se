---
title: Under utveckling – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-funktioner under utveckling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18b42dffc2c34adea1f70c4587b5eb5384d0a778
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220140"
---
# <a name="in-development-for-microsoft-intune---march-2020"></a>Under utveckling för Microsoft Intune – mars 2020

För att hjälpa dig med förberedelser och planering innehåller den här sidan information om uppdateringar av och funktioner i användargränssnittet i Intune som är under utveckling, men som inte släppts än. Förutom informationen på den här sidan: 

- Om vi tror att du behöver vidta åtgärder innan en ändring genomförs, publicerar vi ett extra inlägg i meddelandecentret för Office.
- När en funktion går in i produktion, oavsett om det är en förhandsversion eller en allmänt tillgänglig version, flyttas funktionsbeskrivningen från den här sidan till [Nyheter](whats-new.md).
- Den här sidan och sidan [Nyheter](whats-new.md) uppdateras regelbundet. Kom tillbaka och se om det finns nya uppdateringar.
- Information om planerade produktlanseringar och tidslinjer finns i [Microsoft 365-översikten](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS).

> [!NOTE]
> Den här informationen återspeglar våra planer gällande Intune-funktioner i kommande versioner. Datum och enskilda funktioner kan ändras. Den här sidan beskriver inte alla funktioner som utvecklas.

**RSS-feed**: Få reda på när den här sidan uppdateras genom att kopiera och klistra in följande webbadress i feed-läsaren: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

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

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>Företagsportal för iOS för att stödja liggande läge<!--6048329  -->
Användare kommer att kunna registrera sina enheter, hitta appar och få IT-support med hjälp av valfri skärmorientering. Appen identifieras automatiskt och anpassar skärmen till stående eller liggande läge, såvida inte användaren låser skärmen i stående läge.

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>Förbättrad inloggningsupplevelse i Företagsportal för Android<!-- 6103997  -->
Vi uppdaterar layouten för flera inloggningsskärmar i företagsportalappen för Android så att upplevelsen blir modernare, enklare och tydligare för användare.

<!-- ***********************************************-->
## <a name="device-configuration"></a>Enhetskonfiguration

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Enhetskonfigurationsprofiler för fast nätverk för macOS-enheter<!-- 3508686  -->
En ny konfigurationsprofil för macOS-enheter kommer att bli tillgänglig, som konfigurerar kabelanslutna nätverk (**Enhetskonfiguration** > **Profiler** > **Skapa profil** > **macOS** för plattformen > **Kabelanslutet nätverk** för profiltypen). Använd den här funktionen för att skapa 802.1 x-profiler för att hantera kabelanslutna nätverk och distribuera dessa kabelanslutna nätverk till dina macOS-enheter.

Gäller för:
- macOS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>Förbättrat användargränssnitt när du skapar konfigurationsprofiler på iOS/iPadOS- och macOS-enheter<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
När du skapar en profil för iOS/iPadOS- eller macOS-enheter uppdateras funktionen i administrationscentret för slutpunktshantering. Den här ändringen påverkar följande enhetskonfigurationsprofiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS** eller **macOS** för plattformen):

- Anpassad: iOS/iPadOS, macOS
- Enhetsfunktioner: iOS/iPadOS, macOS
- Enhetsbegränsningar: iOS/iPadOS, macOS
- Slutpunktsskydd: macOS
- Tillägg: macOS
- Inställningsfil: macOS

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>Förbättrat användargränssnitt när du skapar OEMConfig-konfigurationsprofiler på Android Enterprise-enheter<!-- 5568645   -->
När du skapar eller redigerar en OEMConfig-profil för Android Enterprise-enheter uppdateras funktionen i administrationscentret för slutpunktshantering. Den uppdaterade funktionen ger en snabb översikt över inställningar som du har konfigurerat. Den här ändringen påverkar OEMConfig-profilen för enhetskonfigurationen (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise** för plattformen > **OEMConfig** för profiltypen).

Den här funktionen gäller för:
- Android enterprise 

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Inställningar och värden för enhetskonfigurationsprofiler kommer att uppdateras för Windows-plattformar<!-- 4091122 -->
När du skapar enhetskonfigurationsprofiler för Windows-plattformar (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > valfritt **Windows**-alternativ för plattform) kommer vissa inställningar och deras värden att skilja sig från molnlösningsleverantören och kan vara svåra att förstå. Inställningarnas namn och värden kommer att uppdateras så att de blir tydligare.

Gäller för:

- Enhetskonfigurationsprofiler för Windows 10 och senare
- Enhetskonfigurationsprofiler för Windows Holographic for Business
- Enhetskonfigurationsprofiler för Windows 8.1
- Enhetskonfigurationsprofiler för Windows Phone 8.1

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Förbättrat användargränssnitt när vid skapande av enhetskonfigurationsprofiler på enheter med Android eller Android Enterprise<!-- 5841361 -->
När du skapar en profil för enheter med Android eller Android Enterprise kommer upplevelsen i administrationscentret för slutpunktshantering att vara uppdaterad. Den här ändringen påverkar följande enhetskonfigurationsprofiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android-enhetsadministratör** eller **Android Enterprise** för plattformen):

- Enhetsbegränsningar: Android-enhetsadministratör
- Enhetsbegränsningar: Android Enterprise-enhetsägare
- Enhetsbegränsningar: Android Enterprise-arbetsprofil

Mer information om enhetsbegränsningar som du kan konfigurera finns i [Android-enhetsadministratör](../configuration/device-restrictions-android.md) och [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Konfigurera Microsoft Defender ATP-appen för macOS  <!-- 5520115  -->
Du kommer snart att kunna konfigurera [inställningar](../protect/endpoint-protection-macos.md) för Microsoft Defender ATP-appen för enheter som kör macOS som en del av en enhetskonfigurationsprofilen för slutpunktsskydd (**Enheter** > **Konfigurationsprofiler** > **Skapa profil**, välj **macOS** för *Plattform* och sedan **Slutpunktsskydd** för *Profiltyp*). Det kommer att finnas åtta inställningar för macOS-enhetskonfiguration. 

Defender ATP stöds på macOS 10.13 (High Sierra) och senare, och [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md)-appen måste distribueras till enheten *efter* att dessa inställningar har tillämpats. Inställningarna ska skickas till enheten innan appen distribueras. Betaversioner av macOS stöds inte.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Ny FileVault-inställning för macOS-enhetskonfigurationsprincip för slutpunktsskydd<!-- 5459801   -->
Vi lägger till en ny inställning i FileVault-kategorin i mallen [macOS-slutpunktsskydd](../protect/endpoint-protection-macos.md): Dölj återställningsnyckel. (**Enheter** > **Konfigurationsprofiler** > **Skapa profil**, välj **macOS** för *Plattform* och sedan **Slutpunktsskydd** för *Profiltyp*). Den här inställningen döljer den personliga nyckeln från slutanvändaren under FileVault 2-kryptering. Enhetsanvändare kan visa sin personliga återställningsnyckel när som helst från iOS-företagsportalappen eller från företagsportalens webbplats för den krypterade macOS-enheten. De kan visa den personliga återställningsnyckeln genom att gå till enhetsinformation och klicka på *hämta återställningsnyckel*.

Den här inställningen kommer inte att vara tillgänglig i tidigare skapade principer. Du behöver återskapa FileVault-principer för att konfigurera den här inställningen och använda den. 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>Konfigurera leveransoptimeringsagent vid nedladdning av Win32-appinnehåll<!-- 5410945  -->
Du kommer att kunna konfigurera leveransoptimeringsagenten att ladda ned Win32-appinnehåll antingen i bakgrunds- eller förgrundsläge baserat på tilldelning. För befintliga Win32-appar fortsätter innehållet att laddas ned i bakgrundsläge. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Appar** > **Alla appar** > *Win32-appen* > **Egenskaper**. Välj **Redigera** bredvid **Tilldelningar**.  Redigera tilldelningen genom att välja **Inkludera** under **Läge** i avsnittet **Krävs**.  Du hittar den nya inställningen i avsnittet **Appinställningar** när den blir tillgänglig. Mer information om leveransoptimering finns i [Win32-apphantering – Leveransoptimering](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>Enhetshantering

### <a name="change-primary-user-for-windows-devices----3794742---"></a>Ändra primär användare för Windows-enheter <!-- 3794742 -->
Du kommer att kunna ändra den primära användaren för Windows-hybridanslutna och Azure AD-anslutna enheter. Om du vill göra det går du till **Intune** > - **Enheter** > **Alla enheter** > väljer en enhet > **Egenskaper** > **Primär användare**.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Stöd för PowerShell-skript för BYOD-enheter<!-- 1862833  -->
PowerShell-skript kommer att stödja Azure AD-registrerade enheter i Intune. Mer information om PowerShell finns i [Använda PowerShell-skript på Windows 10-enheter i Intune](../apps/intune-management-extension.md). Den här funktionen stöder inte enheter som kör Windows 10 Home Edition.

### <a name="new-information-in-device-details---5604099---"></a>Ny enhetsinformation<!-- 5604099 -->
Följande information kommer att finnas på sidan **Översikt** för enheter:

- Lagringskapacitet (mängden fysisk lagring på enheten)
- Minneskapacitet (mängden fysiskt minne på enheten)

### <a name="script-support-for-macos-devices---4280361----"></a>Skriptstöd för macOS-enheter<!-- 4280361  -->
Du kommer att kunna lägga till och distribuera skript till macOS-enheter. Det här stödet utökar din möjlighet att konfigurera macOS-enheter utöver vad som är möjligt med hjälp av interna MDM-funktioner på macOS-enheter.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--
## Monitor and troubleshoot
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Säkerhet

### <a name="derived-credentials-support-on-android-fully-managed-devices--4839592--"></a>Stöd för härledda autentiseringsuppgifter på fullständigt hanterade Android-enheter<!--4839592-->
Du kommer att kunna använda härledda autentiseringsuppgifter på fullständigt hanterade Android Enterprise-enheter. Support kommer att inkluderas för att hämta en härledd autentiseringsuppgift för Entrust Datacard, Intercede och DISA Purebred. Du kan använda en härledd autentiseringsuppgift för appautentisering, Wi-Fi, VPN eller S/MIME-signering och/eller kryptering med appar som stöder det.

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Sekretessinställningar för macOS-enheter<!-- 2934232 --> 
Med lanseringen av macOS Catalina 10.15 har Apple lagt till nya förbättringar av säkerhet och sekretess. Som standard kan program och processer inte komma åt specifika data utan användarmedgivande. Om användarna inte ger medgivande kan det hända att programmen och processerna inte fungerar. Intune lägger till stöd för inställningar som gör att IT-administratörer kan tillåta eller neka medgivande för dataåtkomst åt slutanvändare på enheter som kör macOS 10.14 och senare. De här inställningarna ser till att program och processer fortsätter att fungera korrekt och minskar det antal meddelanden som slutanvändarna får.

### <a name="updated-ui-text-and-labels-for-windows-10-endpoint-protection-profile-settings---5983747---"></a>Uppdatering av text och etiketter för användargränssnittet i inställningarna för Windows 10-slutpunktsskyddsprofil<!-- 5983747 -->
Vi uppdaterar texten för olika inställningar som du konfigurerar som Windows 10-enhetskonfigurationsprofiler så att det blir enklare att förstå avsedd användning och avsett syfte med inställningarna.

De inställningar som vi uppdaterar inkluderar Windows 10-enhetskonfigurationsprofiler för:

- [Enhetsbegränsningar](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) > Microsoft Defender Antivirus  
- [Endpoint Protection](../protect/endpoint-protection-windows-10.md) > Microsoft Defender Antivirus

De inställningar som stöds med Intune ändras inte. Detta är endast en uppdatering av texten i användargränssnittet i administrationscentret för Microsoft-slutpunktshantering.

<!-- ***********************************************-->
## <a name="notices"></a>Meddelanden

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Se även

Mer information om den senaste utvecklingen finns i [Nyheter i Microsoft Intune](whats-new.md).
