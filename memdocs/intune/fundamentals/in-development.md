---
title: Under utveckling – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-funktioner under utveckling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2bb971da483cd86e143673b57e8e5e09f943a5
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764211"
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

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Företagsportal för Android hjälper användarna att hämta appar utifrån registreringen av arbetsprofilen <!-- 6103999  -->
Vi förbättrar vägledningen i appen i Företagsportal så att användarna enklare kan hitta och installera appar.  När användaren har registrerat sin arbetsprofil visas ett meddelande som talar om att de kan hitta föreslagna appar i den märkta versionen av Google Play. Användarna ser också den nya länken **Hämta appar** i Företagsportal-lådan till vänster. För att möjliggöra det här har vi tagit bort fliken **APPAR**. 

<!-- ***********************************************-->
## <a name="device-configuration"></a>Enhetskonfiguration

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>Inställningar och värden för enhetskonfigurationsprofiler kommer att uppdateras för Windows-plattformar<!-- 4091122 -->
När du skapar enhetskonfigurationsprofiler för Windows-plattformar (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > valfritt **Windows**-alternativ för plattform) kommer vissa inställningar och deras värden att skilja sig från molnlösningsleverantören och kan vara svåra att förstå. Inställningsnamn och deras värden kommer att uppdateras så att de blir tydligare.

Gäller för:

- Enhetskonfigurationsprofiler för Windows 10 och senare
- Enhetskonfigurationsprofiler för Windows Holographic for Business
- Enhetskonfigurationsprofiler för Windows 8.1
- Enhetskonfigurationsprofiler för Windows Phone 8.1

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>Ny FileVault-inställning för macOS-enhetskonfigurationsprincip för slutpunktsskydd<!-- 5459801   -->
Vi lägger till en ny inställning i FileVault-kategorin i mallen [macOS-slutpunktsskydd](../protect/endpoint-protection-macos.md): Dölj återställningsnyckel. (**Enheter** > **Konfigurationsprofiler** > **Skapa profil**, välj **macOS** för *Plattform* och sedan **Slutpunktsskydd** för *Profiltyp*). Den här inställningen döljer den personliga nyckeln från slutanvändaren under FileVault 2-kryptering. Enhetsanvändare kan visa sin personliga återställningsnyckel när som helst från iOS-företagsportalappen eller från företagsportalens webbplats för den krypterade macOS-enheten. De kan visa den personliga återställningsnyckeln genom att gå till enhetsinformation och klicka på *hämta återställningsnyckel*.

Den här inställningen kommer inte att vara tillgänglig i tidigare skapade principer. Du behöver återskapa FileVault-principer för att konfigurera den här inställningen och använda den. 


<!-- ***********************************************-->
## <a name="device-enrollment"></a>Enhetsregistrering

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>VPN kan användas för att distribuera egna enheter (BYOD, Bring Your Own Device)<!--5015344 -->
Den här funktionen kan vara försenad.

### <a name="shared-ipads-for-business--6367326---"></a>Delat iPad for Business<!--6367326 -->
Du kan använda Intune och Apple Business Manager till att enkelt och säkert konfigurera delade iPads så att flera medarbetare kan dela enheter. Apples [Delad iPad](https://developer.apple.com/education/shared-ipad/) får en ny anpassad upplevelse för flera användare samtidigt som användardata bevaras. Med ett hanterat Apple-ID kan användare komma åt sina appar, data och inställningar efter att ha loggat in på en delad iPad i organisationen. Delad iPad fungerar med federerade identiteter.

Du ser den här funktionen genom att gå till [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **iOS** > **iOS-registrering** > **Registreringsprogramtoken** > välj en token** > **Profiler** > **Skapa profil** > **iOS**. På sidan **Hanteringsinställningar** väljer du **Registrera utan användartillhörighet** så visas alternativet **Delad iPad**.

**Gäller för:** macOS 13.4 och senare. Den här versionen innehåller stöd för tillfälliga sessioner med delad iPad så att användarna kan komma åt en enhet utan ett hanterat Apple-ID. Vid utloggning raderar enheten all användarinformation så att enheten omedelbart kan användas, vilket eliminerar behovet av enhetsrensning. 

<!-- ***********************************************-->
## <a name="device-management"></a>Enhetshantering

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Stöd för PowerShell-skript för BYOD-enheter<!-- 1862833  -->
PowerShell-skript kommer att stödja Azure AD-registrerade enheter i Intune. Mer information om PowerShell finns i [Använda PowerShell-skript på Windows 10-enheter i Intune](../apps/intune-management-extension.md). Den här funktionen stöder inte enheter som kör Windows 10 Home Edition.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics innehåller enhetsinformationslogg<!--6014987  -->
Loggar med Intune-enhetsinformation kommer att vara tillgängliga i **Rapporter** > **Logganalys**. Du kan korrelera enhetsinformationen för att bygga anpassade frågor och Azure-arbetsböcker.


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
## <a name="security"></a>Säkerhet


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Duplicera policyer i Endpoint Security<!-- 5892558   -->
Du kan välja en policy du har skapat i Endpoint Security-noden i administrationscentret för Microsoft Endpoint Manager och sedan kopiera den.  Du kan kopiera följande policyer: 

- Antivirus
- Diskkryptering
- Brandvägg
- Slutpunktsidentifiering och svar
- Minska attackytan
- Kontoskydd

Den ursprungliga policyn kopieras, och sedan kan du byta namn på och redigera den. Kopian innehåller inte samma tilldelningar som originalet.

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Ny profil för Endpoint Security Firewall-policy<!-- 5653324   -->
I en förhandsversion har vi lagt till ytterligare en profil för Windows 10 och senare i Firewall-policyn för Intunes Endpoint Security (**Endpoint Security** > **Brandvägg** > **Skapa policy** > välj **Windows 10 och senare**). 

Varje instans av den här nya profilen har stöd för upp till 150 anpassade *Microsoft Defender Firewall-regler*. Med Microsoft Defender Firewall-regelpolicyn kan du definiera detaljerade regler för Windows Firewall som tillåter eller blockerar portar och program i Windows 10.

<!-- ***********************************************-->
## <a name="notices"></a>Meddelanden

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Se även

Mer information om den senaste utvecklingen finns i [Nyheter i Microsoft Intune](whats-new.md).



