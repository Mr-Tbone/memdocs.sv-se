---
title: Funktioner och inställningar för enheter i Microsoft Intune – Azure | Microsoft Docs
description: Översikt över de olika enhetsprofilerna i Microsoft Intune. Få information om funktioner, begränsningar, e-post, Wi-Fi, VPN, utbildning, certifikat, uppgradering av Windows 10, BitLocker och Microsoft Defender, Windows Information Protection, administrativa mallar och anpassade inställningar för enhetskonfiguration i administrationscentret för Microsoft Endpoint Manager. Använd dessa profiler för att hantera och skydda data och enheter i företaget.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3437a1b9fe3c663844d366bbfda6c0bcb463c3ab
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983802"
---
# <a name="apply-features-and-settings-on-your-devices-using-device-profiles-in-microsoft-intune"></a>Tillämpa funktioner och inställningar på dina enheter med enhetsprofiler i Microsoft Intune

Microsoft Intune innehåller inställningar och funktioner som du kan aktivera eller inaktivera på olika enheter i din organisation. Dessa inställningar och funktioner läggs till i ”konfigurationsprofiler”. Du kan skapa profiler för olika enheter och plattformar, bland annat iOS/iPadOS, Android-enhetsadministratör, Android Enterprise och Windows. Använd sedan Intune för att tillämpa eller ”tilldela” profilen till enheterna.

Använd dessa konfigurationsprofiler som en del av din lösning för hantering av mobilenheter till att utföra olika uppgifter. Några profilexempel:

- På Windows 10-enheter använder du en profilmall som blockerar ActiveX-kontroller i Internet Explorer.
- Tillåt användare på iOS/iPadOS- och macOS-enheter att använda AirPrint-skrivare i organisationen.
- Tillåt eller förhindra åtkomst till Bluetooth på enheten.
- Skapa en WiFi- eller VPN-profil som ger olika enheter åtkomst till företagsnätverket.
- Hantera programuppdateringar, till exempel när de installeras.
- Kör en Android-enhet som en dedikerad kioskenhet som kan köra en eller flera appar.

I den här artikeln ges en översikt över de olika profiltyper som du kan skapa. Med de här profilerna kan du tillåta eller förhindra vissa funktioner på enheterna.

## <a name="administrative-templates"></a>Administrativa mallar

[Administrativa mallar](administrative-templates-windows.md) innehåller hundratals inställningar som du kan konfigurera för Internet Explorer, OneDrive, fjärrskrivbord, Word, Excel och andra Office-program.

Dessa mallar ger administratörer en förenklad vy över inställningar som liknar grupprinciper, men de är helt molnbaserade.

Den här funktionen stöder:

- Windows 10 och senare

## <a name="certificates"></a>Certifikat

[Certifikat](../protect/certificates-configure.md) konfigurerar betrodda certifikat, SCEP- och PKCS-certifikat som har tilldelats till enheter. De här certifikaten autentiserar Wi-Fi-, VPN- och e-postprofiler.

Den här funktionen stöder:

- Android-enhetsadministratör
- Android enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1
- Windows 8,1
- Windows 10 och senare

## <a name="custom-profile"></a>Anpassad profil

Med [Anpassade inställningar](custom-settings-configure.md) kan administratörer tilldela enhetsinställningar som inte är inbyggda i Intune. Du kan ange OMA-URI-värden på Android-enheter. På iOS/iPadOS-enheter kan du importera en konfigurationsfil som du har skapat i Apple Configurator.

Den här funktionen stöder:

- Android-enhetsadministratör
- Android enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1

## <a name="delivery-optimization"></a>Leveransoptimering

[Leveransoptimering](delivery-optimization-windows.md) ger en bättre upplevelse vid leverans av programuppdateringar. De här inställningarna ersätter inställningarna i **Programuppdateringar** > **Windows 10-uppdateringsring**.

Använd inställningarna för att styra hur programuppdateringar laddas ned till enheter i din organisation. Du kan exempelvis låta användarna hämta sina egna uppdateringar, eller hämta uppdateringar med hjälp av leveransoptimeringens molntjänster i en enhetsprofil.

Den här funktionen stöder:

- Windows 10 och senare

## <a name="derived-credential"></a>Härledd autentiseringsuppgift

[Härledda autentiseringsuppgifter](../protect/derived-credentials.md) är certifikat på smartkort som kan autentisera, signera och kryptera. I Intune kan du skapa profiler med dessa autentiseringsuppgifter för användning i appar, e-postprofiler, anslutning till VPN, S/MIME och Wi-Fi.

Den här funktionen stöder:

- Android enterprise
- iOS/iPadOS

## <a name="device-features"></a>Enhetsfunktioner

[Enhetsfunktioner](device-features-configure.md) styr funktioner på iOS/iPadOS- och macOS-enheter, t.ex. AirPrint, meddelanden och låsskärmsmeddelanden.

Den här funktionen stöder:

- iOS/iPadOS
- macOS

## <a name="device-firmware-configuration-interface"></a>Konfigurationsgränssnitt för enhetens inbyggda programvara

[DFCI (Device Firmware Configuration Interface, konfigurationsgränssnitt för enhetens inbyggda programvara)](device-firmware-configuration-interface-windows.md) gör att administratörer kan aktivera eller inaktivera UEFI-inställningar (BIOS) med hjälp av Intune. Använd de här inställningarna för att förbättra säkerheten på nivån för inbyggd programvara, som vanligtvis är mer motståndskraftig mot skadliga attacker.

Den här funktionen stöder:

- Windows 10 1809 och senare med inbyggd programvara som stöds

## <a name="device-restrictions"></a>Enhetsbegränsningar

[Enhetsbegränsningar](device-restrictions-configure.md) styr säkerhet, maskinvara, delning av data och fler inställningar på enheter. Du kan till exempel skapa en profil för enhetsbegränsningar som förhindrar användare av iOS/iPadOS-enheter från att använda kameran på enheten. 

Den här funktionen stöder:

- Android-enhetsadministratör
- Android enterprise
- iOS/iPadOS
- macOS
- Windows 10 och senare
- Windows 10-teamet

## <a name="domain-join"></a>Domänanslutning

[Domänanslutning](domain-join-configure.md) konfigurerar domäninformation för det lokala Active Directory. Den här informationen distribueras till Hybrid Azure AD-anslutna enheter när de etableras med hjälp av Windows Autopilot och Intune. Den här profilen talar om för enheter vilken domän och OU de ska ansluta till.

Den här funktionen stöder:

- Windows 10 och senare

## <a name="edition-upgrade"></a>Versionsuppgradering

Med [Windows 10-versionsuppgraderingar](edition-upgrade-configure-windows-10.md) kan du automatiskt uppgradera enheter som kör vissa versioner av Windows 10 till en senare version.

Den här funktionen stöder:

- Windows 10 och senare

## <a name="education"></a>Utbildning

Konfigurationsalternativen [Utbildningsinställningar – Windows 10](education-settings-configure.md) för [appen Windows Take a Test](https://docs.microsoft.com/education/windows/take-tests-in-windows-10). När du konfigurerar dessa alternativ kan inga andra appar köras på enheten förrän provet har slutförts.

I [Utbildningsinställningar – iOS/iPadOS](../fundamentals/education-settings-configure-ios-shared.md) används iOS/iPadOS-appen Classroom som hjälp för och stöd till elevernas enheter i klassrummet. Du kan konfigurera iPad-enheter så att många elever kan dela en enda enhet.

## <a name="email"></a>E-post

I [E-postinställningar](email-settings-configure.md) skapas, tilldelas och övervakas Exchange ActiveSyncs e-postinställningar för enheterna. Med e-postprofiler uppnår du konsekvens, minskar supportsamtalen och ger slutanvändarna åtkomst till företagets e-post på sina personliga enheter, utan de behöver konfigurera något själva. 

Den här funktionen stöder:

- Android-enhetsadministratör
- Android enterprise
- iOS/iPadOS
- Windows Phone 8.1
- Windows 10 och senare

## <a name="endpoint-protection"></a>Endpoint Protection

Med [slutpunktsskydd](../protect/endpoint-protection-configure.md) kan du konfigurera BitLocker- och Microsoft Defender-inställningar för Windows 10-enheter. Du kan även konfigurera brandvägg, gateway och andra resurser på macOS-enheter.

Om du vill publicera Microsoft Defender Avancerat skydd (WDATP) med Microsoft Intune kan du läsa informationen om att [konfigurera slutpunkter med verktyg för hantering av mobilenheter (MDM)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-mdm).

Den här funktionen stöder:

- macOS
- Windows 10 och senare

## <a name="esim-cellular---public-preview"></a>eSIM-mobilnät – offentlig förhandsversion

Med [Profiler för eSIM-mobilnät](esim-device-configuration.md) kan administratörer konfigurera mobildataabonnemang på dina hanterade enheter för åtkomst till Internet och data. När du har fått aktiveringskoder från mobiloperatören kan du använda Intune för att importera dessa aktiveringskoder och sedan tilldela dem till dina eSIM-kompatibla enheter.

Den här funktionen stöder:

- Windows 10 Fall Creators Update och senare

## <a name="extensions"></a>Tillägg

[Systemtillägg och kerneltillägg i macOS](kernel-extensions-overview-macos.md) gör att administratörer kan lägga till funktioner och program som utökar de inbyggda funktionerna i operativsystemet. Konfigurera de här inställningarna om du vill lita på alla tillägg från en viss utvecklare eller partner, eller tillåt specifika tillägg.

Den här funktionen stöder:

- macOS

## <a name="identity-protection"></a>Identity Protection

[Identity protection](../protect/identity-protection-configure.md) styr upplevelsen av Windows Hello for Business på Windows 10- och Windows 10 Mobile-enheter. Konfigurera dessa inställningar för att göra Windows Hello for Business tillgängligt för användare och enheter, samt för att ange krav på PIN-koder för enheter och gester.  

Den här funktionen stöder:  

- Windows 10 och senare
- Windows 10 Holographic for Business  

## <a name="kiosk"></a>Helskärmsläge

Profilen [Inställningar för helskärmsläge](kiosk-settings.md) konfigurerar en enhet till att köra en eller flera appar. Du kan också anpassa andra funktioner i helskärmsläget, som en startmeny och en webbläsare.

Den här funktionen stöder:

- Windows 10 och senare

Inställningar för helskärmsläge finns också som enhetsbegränsningar för [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) och [iOS/iPadOS](device-restrictions-ios.md#kiosk).

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

[Microsoft Defender Avancerat skydd](../protect/advanced-threat-protection.md) integreras med Intune för att övervaka och skydda enheter. Du anger risknivåer och bestämmer vad som ska hända om enheterna överskrider den nivån. I kombination med villkorsstyrd åtkomst kan du bidra till att förhindra skadlig aktivitet i din organisation.

Den här funktionen stöder:

- Windows 10 och senare

## <a name="oemconfig"></a>OEMConfig

[OEMConfig](android-oem-configuration-overview.md) är en standard som gör det möjligt för OEM-tillverkare (originalutrustningstillverkare) och EMM:er (Enterprise Mobility Management) att bygga och stödja OEM-specifika funktioner på ett standardiserat sätt på Android Enterprise-enheter. Med OEMConfig skapar en OEM ett schema som definierar OEM-/regionsspecifika hanteringsfunktioner och bäddar in dem i en app som laddats upp till Google Play. Intune läser in schemat från appen så att Intune-administratörer kan konfigurera inställningarna i schemat.

Den här funktionen stöder:

- Android Enterprise (OEMConfig)

## <a name="powershell-scripts"></a>PowerShell-skript

[PowerShell-skript på Windows 10-enheter](../apps/intune-management-extension.md) använder Intune Management-tillägget för att ladda upp dina PowerShell-skript i Intune och sedan köra dessa skript på dina enheter. Se även vad som krävs för att använda tillägget, hur du lägger till dem i Intune och annan viktig information.

Den här funktionen stöder:

- Windows 10 och senare
- Windows 10 Holographic for Business

## <a name="preference-file"></a>Inställningsfil

[Inställningsfilerna](preference-file-settings-macos.md) på macOS-enheter innehåller information om appar. Du kan till exempel använda inställningsfiler för att styra webbläsarinställningar, anpassa appar med mera.

Den här funktionen stöder:

- macOS

## <a name="shared-multi-user-device"></a>Delad enhet för flera användare

[Windows 10](shared-user-device-settings-windows.md) och [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) innehåller inställningar för att hantera enheter med flera användare, som också kallas för delade enheter eller delade datorer. När en användare loggar in på enheten väljer du om användaren kan ändra strömsparalternativen eller spara filer på enheten. I ett annat exempel kan du för att spara utrymme skapa en princip som tar bort inaktiva autentiseringsuppgifter från Windows HoloLens-enheter.

Med dessa inställningar för delade enheter för flera användare kan en administratör kontrollera några av enhetens funktioner och hantera dessa delade enheter med Intune.

Den här funktionen stöder:

- Windows 10 och senare
- Windows 10 Holographic for Business

## <a name="update-policies"></a>Uppdateringsprinciper

I [Uppdateringsprinciper för iOS/iPadOS](../protect/software-updates-ios.md) visas hur du skapar och tilldelar iOS/iPadOS-principer för installering av programuppdateringar på iOS/iPadOS-enheterna. Du kan också granska installationsstatusen.

Se [Leveransoptimering](delivery-optimization-windows.md) för uppdateringsprinciper på Windows-enheter. 

Den här funktionen stöder:

- iOS/iPadOS

## <a name="vpn"></a>VPN

Med [VPN-inställningar](vpn-settings-configure.md) kan du tilldela VPN-profiler till användare och enheter i din organisation, så att de enkelt och säkert kan ansluta till nätverket. 

Virtuella privata nätverk (VPN, Virtual Private Networks) ger användarna säker fjärråtkomst till företagets nätverk. Enheter använder en VPN-anslutningsprofil för att initiera en anslutning till VPN-servern. 

Den här funktionen stöder: 

- Android-enhetsadministratör
- Android enterprise
- iOS/iPadOS
- macOS
- Windows Phone 8.1
- Windows 8,1
- Windows 10 och senare

## <a name="wi-fi"></a>Wi-Fi

Med [Wi-Fi-inställningar](wi-fi-settings-configure.md) kan du tilldela trådlösa nätverksinställningar till användare och enheter. När du tilldelar en Wi-Fi-profil får användarna åtkomst till ditt företags trådlösa nätverk utan att de behöver göra några inställningar själva. 

Den här funktionen stöder: 

- Android-enhetsadministratör
- Android enterprise
- iOS/iPadOS
- macOS
- Windows 8.1 (endast import)
- Windows 10 och senare

## <a name="zebra-mobility-extensions-mx"></a>Zebra Mobility Extensions (MX)

Med [Zebra Mobility Extensions (MX)](android-zebra-mx-overview.md) kan administratörer använda och hantera Zebra-enheter i Intune. Du skapar StageNow-profiler med dina inställningar och använder sedan Intune för att tilldela och distribuera profilerna till dina Zebra-enheter. [StageNow-loggar och vanliga problem](android-zebra-mx-logs-troubleshoot.md) är en bra resurs om du vill felsöka profiler och se vissa potentiella problem som kan uppstå när du använder StageNow.

Den här funktionen stöder:

- Android-enhetsadministratör (Mobility Extensions)

## <a name="manage-and-troubleshoot"></a>Hantering och felsökning

[Hantera dina profiler](device-profile-monitor.md) för att kontrollera statusen för enheter och tilldelade profiler. Du får även hjälp med att lösa konflikter genom att se inställningarna som orsakar en konflikt och de profiler som innehåller dessa inställningar. I [Vanliga problem och lösningar](device-profile-troubleshoot.md) får administratörer hjälp med att arbeta med profiler. Där beskrivs vad som händer när en profil tas bort, vad som orsakar att meddelanden skickas till enheter och mycket mer.

## <a name="next-steps"></a>Nästa steg

Välj din plattform och sätt igång.
