---
title: Under utveckling – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-funktioner under utveckling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f53096f25b4bb05b80d11246ac2fa01486f6e42
ms.sourcegitcommit: 252e718dc58da7d3e3d3a4bb5e1c2950757f50e2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/07/2020
ms.locfileid: "80808158"
---
# <a name="in-development-for-microsoft-intune---april-2020"></a>Under utveckling för Microsoft Intune – april 2020

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

### <a name="update-to-android-app-configuration-policies---6113334----"></a>Uppdatering av konfigurationsprinciper för Android-appar<!-- 6113334  -->
Konfigurationsprinciperna för Android-appar kommer att uppdateras så att administratörer kan välja typ av enhetsregistrering innan de skapar konfigurationsprofiler för appar. Funktionen läggs till i kontot för certifikatprofiler som baseras på registreringstyp (arbetsprofil eller enhetsägare).  Vid lanseringen inträffar följande:

- För de befintliga principer som skapats före lanseringen av den här funktionen och som inte har några associerade certifikatprofiler, används som standard arbetsprofil och enhetsägarprofil som enhetsregistreringstyp.
- För de befintliga principer som skapats före lanseringen av den här funktionen och som har associerade certifikatprofiler, används som standard endast arbetsprofil.
- Om en ny profil skapas och arbetsprofil och enhetsägarprofil väljs som enhetsregistreringstyp kan du inte associera en certifikatprofil med appkonfigurationsprincipen.
- Om en ny profil skapas och Endast arbetsprofil har valts kan de certifikatprinciper för arbetsprofil som skapats under Enhetskonfiguration användas.
- Om en ny profil skapas och Endast enhetens ägare har valts kan de certifikatprinciper för enhetsägare som skapats under Enhetskonfiguration användas.

Befintliga principer kan inte åtgärda eller utfärda nya certifikat.

Vi har också lagt till e-postkonfigurationsprofiler för Gmail och Nine som fungerar för både registreringstypen Arbetsprofil och Enhetsägare. Detta innefattar användning av certifikatprofiler på båda e-postkonfigurationstyperna.  Alla Gmail- eller Nine-principer som du har skapat under Enhetskonfiguration för arbetsprofiler fortsätter att gälla för enheten och du behöver inte flytta dem till appkonfigurationsprinciper.

I [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) hittar du appkonfigurationsprinciperna genom att välja **Appar** > **Appkonfigurationsprinciper**. Mer information om appkonfigurationsprinciper finns i [Appkonfigurationsprinciper för Microsoft Intune](../apps/app-configuration-policies-overview.md).

### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams ingår nu i Office 365-paketet för macOS<!-- 5903936  -->
Användare som tilldelas Microsoft Office för macOS i Microsoft Endpoint Manager får förutom de vanliga Microsoft Office-apparna (Word, Excel, PowerPoint, Outlook och OneNote) nu även Microsoft Teams. Intune identifierar befintliga Mac-enheter som har andra Office för macOS-appar installerade och kommer att försöka installera Microsoft Teams nästa gång enheten checkar in med Intune. I [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) kan du hitta **Office 365-paketet** för macOS genom att välja **Appar** > **macOS** > **Lägg till**. Mer information finns i [Tilldela Office 365 till macOS-enheter med Microsoft Intune](../apps/apps-add-office365-macos.md).

### <a name="group-targeting-support-for-customization-pane----4722837----"></a>Stöd för riktning till grupper i fönstret Anpassning <!-- 4722837  -->
Du kommer att kunna rikta inställningarna i fönstret Anpassning till användargrupper. Välj **Klientappar** > **Anpassning** i Intune-portalen. Mer information finns i [Anpassa Intune-företagsportalens appar, företagsportalens webbplats och Intune-appen](company-portal-app.md].

<!-- ***********************************************-->
## <a name="device-configuration"></a>Enhetskonfiguration

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Enhetskonfigurationsprofiler för fast nätverk för macOS-enheter<!-- 3508686  -->
En ny konfigurationsprofil för macOS-enheter kommer att bli tillgänglig, som konfigurerar kabelanslutna nätverk (**Enhetskonfiguration** > **Profiler** > **Skapa profil** > **macOS** för plattformen > **Kabelanslutet nätverk** för profiltypen). Använd den här funktionen för att skapa 802.1 x-profiler för att hantera kabelanslutna nätverk och distribuera dessa kabelanslutna nätverk till dina macOS-enheter.

Gäller för:
- macOS

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Inställningar och värden för enhetskonfigurationsprofiler kommer att uppdateras för Windows-plattformar<!-- 4091122 -->
När du skapar enhetskonfigurationsprofiler för Windows-plattformar (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > valfritt **Windows**-alternativ för plattform) kommer vissa inställningar och deras värden att skilja sig från molnlösningsleverantören och kan vara svåra att förstå. Inställningsnamn och deras värden kommer att uppdateras så att de blir tydligare.

Gäller för:

- Enhetskonfigurationsprofiler för Windows 10 och senare
- Enhetskonfigurationsprofiler för Windows Holographic for Business
- Enhetskonfigurationsprofiler för Windows 8.1
- Enhetskonfigurationsprofiler för Windows Phone 8.1

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>Konfigurera Microsoft Defender ATP-appen för macOS  <!-- 5520115  -->
Du kommer snart att kunna konfigurera [inställningar](../protect/endpoint-protection-macos.md) för Microsoft Defender ATP-appen för enheter som kör macOS som en del av en enhetskonfigurationsprofilen för slutpunktsskydd (**Enheter** > **Konfigurationsprofiler** > **Skapa profil**, välj **macOS** för *Plattform* och sedan **Slutpunktsskydd** för *Profiltyp*). Det kommer att finnas åtta inställningar för macOS-enhetskonfiguration. 

Defender ATP stöds på macOS 10.13 (High Sierra) och senare, och [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md)-appen måste distribueras till enheten *efter* att dessa inställningar har tillämpats. Inställningarna ska skickas till enheten innan appen distribueras. Betaversioner av macOS stöds inte.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Ny FileVault-inställning för macOS-enhetskonfigurationsprincip för slutpunktsskydd<!-- 5459801   -->
Vi lägger till en ny inställning i FileVault-kategorin i mallen [macOS-slutpunktsskydd](../protect/endpoint-protection-macos.md): Dölj återställningsnyckel. (**Enheter** > **Konfigurationsprofiler** > **Skapa profil**, välj **macOS** för *Plattform* och sedan **Slutpunktsskydd** för *Profiltyp*). Den här inställningen döljer den personliga nyckeln från slutanvändaren under FileVault 2-kryptering. Enhetsanvändare kan visa sin personliga återställningsnyckel när som helst från iOS-företagsportalappen eller från företagsportalens webbplats för den krypterade macOS-enheten. De kan visa den personliga återställningsnyckeln genom att gå till enhetsinformation och klicka på *hämta återställningsnyckel*.

Den här inställningen kommer inte att vara tillgänglig i tidigare skapade principer. Du behöver återskapa FileVault-principer för att konfigurera den här inställningen och använda den. 

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Skicka push-meddelanden som en åtgärd för inkompatibilitet <!-- 1733150   -->
För iOS- och Android-plattformar lägger vi till en ny åtgärd för inkompatibilitet som innebär att ett push-meddelande skickas via företagsportalsappen. När en användare klickar på det här meddelandet startas företagsportalsappen, och i appen visas information om inkompatibilitetsorsaken. Administratörer kan konfigurera den nya åtgärden för inkompatibilitet i Microsoft Endpoint Manager admin center genom att gå till **Enheter** > **Kompatibilitetsprinciper** > **Skapa princip** och sedan välja *Åtgärd* för att skicka ett push-meddelande via app.

### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Förhandstestning för hanterade Google Play-appar<!-- 2681933  -->
Organisationer som använder [Google Plays slutna testkanaler för förhandstestning av appar](https://support.google.com/googleplay/android-developer/answer/3131213) kommer att kunna hantera dessa kanaler med Intune. Du kommer att kunna selektivt tilldela verksamhetsspecifika appar (som publiceras på Google Plays förproduktionskanaler) till pilotgrupper för testning. I Intune kommer du också att kunna se om en app har en testkanal med en publicerad förproduktionsversion, och du kommer att kunna tilldela den kanalen till grupper med AAD-användare eller -enheter. Den här funktionen är tillgänglig för alla våra aktuella Android Enterprise-scenarier (arbetsprofil, fullständigt hanterad, särskilt avsedd). I [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) kan du lägga till en hanterad Google Play-app genom att välja **Appar** > **Android** > **Lägg till**. Du hittar mer information i [Lägg till hanterade Google Play-appar till Android enterprise-enheter med Intune](../apps/apps-add-android-for-work.md).

### <a name="manage-smime-settings-for-outlook-on-android---6517085-----"></a>Hantera S/MIME-inställningar för Outlook på Android<!-- 6517085   -->
Du kommer att kunna använda appkonfigurationsprinciper för att hantera S/MIME-inställningen för Outlook på enheter som kör Android Enterprise. Du kommer också att kunna välja om enhetsanvändare ska kunna aktivera eller inaktivera S/MIME i Outlook-inställningarna eller inte. Om du vill använda appkonfigurationsprinciper för Android går du till [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) och väljer **Appar** > **Appkonfigurationsprinciper** > **Lägg till** > **Hanterade enheter**.

### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155----"></a>Ytterligare alternativ i SSO- och SSO-apptilläggsprofiler på iOS/iPadOS-enheter<!-- 6504155  -->
På iOS/iPadOS-enheter kan du:

- Ange SAM-kontonamnet (Hanteraren för kontosäkerhet) som Kerberos-huvudnamn i SSO-profiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** som plattform > **Enhetsfunktioner** som profil > **Enkel inloggning**). 
- Konfigurera Microsoft Azure AD-tillägget för iOS/iPadOS med färre klick med hjälp av den nya SSO-apptilläggstypen i SSO-apptilläggsprofiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** som plattform > **Enhetsfunktioner** som profil > **Tillägg för enkel inloggning**). Du kan aktivera Azure AD-tillägget för delade enheter och skicka tilläggsspecifika data till tillägget.

Gäller för:
- iOS/iPadOS 13.0+

Mer information om hur du använder enkel inloggning på iOS/iPadOS-enheter finns i [Tilläggsöversikten för enkel inloggning](../configuration/device-features-configure.md#single-sign-on-app-extension) och [listan med inställningar för enkel inloggning](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Enhetsregistrering

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>VPN kan användas för att distribuera egna enheter (BYOD, Bring Your Own Device)<!--5015344 -->
Med den nya Autopilot-profilens **Hoppa över kontroll av domänanslutning**-växlingsknapp kan du distribuera Hybrid Azure AD-anslutna enheter utan åtkomst till ditt företagsnätverk med hjälp av din egen Win 32 VPN-tredjepartsklient. Om du vill se den nya växlingsknappen kan du gå till [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter**  > **Windows** > **Windows-registrering** > **Distributionsprofiler** > **Skapa profil** > **Välkomstupplevelse (OOBE)** .

<!-- ***********************************************-->
## <a name="device-management"></a>Enhetshantering

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Stöd för PowerShell-skript för BYOD-enheter<!-- 1862833  -->
PowerShell-skript kommer att stödja Azure AD-registrerade enheter i Intune. Mer information om PowerShell finns i [Använda PowerShell-skript på Windows 10-enheter i Intune](../apps/intune-management-extension.md). Den här funktionen stöder inte enheter som kör Windows 10 Home Edition.

### <a name="script-support-for-macos-devices---4280361----"></a>Skriptstöd för macOS-enheter<!-- 4280361  -->
Du kommer att kunna lägga till och distribuera skript till macOS-enheter. Det här stödet utökar din möjlighet att konfigurera macOS-enheter utöver vad som är möjligt med hjälp av interna MDM-funktioner på macOS-enheter.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics innehåller enhetsinformationslogg<!--6014987  -->
Loggar med Intune-enhetsinformation kommer att vara tillgängliga i **Rapporter** > **Logganalys**. Du kan korrelera enhetsinformationen för att bygga anpassade frågor och Azure-arbetsböcker.

### <a name="push-notification-when-device-ownership-type-is-changed---5575875----"></a>Push-meddelande när ägarskapstypen för enheten ändras<!-- 5575875  -->
Du kommer att kunna konfigurera ett push-meddelande till användarna av företagsportalsappen (både Android och iOS) när deras ägarskapstyp ändras från Personlig till Företag som en integritetsmeddelande. Den här inställningen hittar du i Microsoft Endpoint Manager genom att välja **Administration av klientorganisation** > **Anpassning**. Mer information om hur enhetsägarskapet påverkar slutanvändarna finns i [Ändra enhetsägande](../enrollment/corporate-identifiers-add.md#change-device-ownership).

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



