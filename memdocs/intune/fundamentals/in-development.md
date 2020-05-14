---
title: Under utveckling – Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-funktioner under utveckling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7827c85585d630f64ba9c6d342b6275fca506b1d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906959"
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

### <a name="support-for-multiple-accounts-in-company-portal-for-mac---5779449----"></a>Stöd för flera konton i Företagsportal för Mac<!-- 5779449  -->
Företagsportal för macOS-enheter cachelagrar nu användarkonton, vilket gör det enklare att logga in. Användare behöver inte längre logga in i Företagsportal varje gång de startar programmet. Dessutom visar Företagsportal en kontoväljare om flera användarkonton är cachelagrade, så att användarna inte behöver ange sitt användarnamn. 

### <a name="auto-update-vpp-available-apps---3640511----"></a>Uppdatera VPP-tillgängliga appar automatiskt<!-- 3640511  -->
Appar som är publicerade som VPP-tillgängliga appar (VPP) uppdateras automatiskt när **Automatisk uppdatering av appar** är aktiverat för VPP-token. För närvarande uppdateras inte VPP-tillgängliga appar automatiskt. Slutanvändarna måste i stället gå till Företagsportal och installera om appen om det finns en nyare version. Obligatoriska appar har dock för närvarande stöd för automatiska uppdateringar.

### <a name="customize-self-service-device-actions-in-the-company-portal--4393379----"></a>Anpassa åtgärder för självbetjäningsenhet i Företagsportal<!--4393379  -->
Du kan anpassa de tillgängliga åtgärderna för självbetjäning som visas för slutanvändare i appen Företagsportal och på webbplatsen. För att förhindra oavsiktliga enhetsåtgärder kan du konfigurera inställningarna för appen Företagsportal genom att välja **Administration av klientorganisation** > **Anpassning** > **Skapa** > **Dölj funktioner**. Följande alternativ är tillgängliga:
- Dölj knappen **Ta bort** på Windows-företagsenheter.
- Dölj knappen **Återställ** på Windows-företagsenheter.
- Dölj knappen **Återställ** på iOS-företagsenheter.
- Dölj knappen **Ta bort** på iOS-företagsenheter.

Mer information finns i [Åtgärder för självbetjäningsenhet för användare från företagsportalen](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

### <a name="unified-delivery-of-azure-ad-enterprise-or-office-online-applications-in-the-company-portal--4404429---"></a>Enhetlig leverans av Azure AD Enterprise- eller Office Online-program i Företagsportal<!--4404429 -->
Du kan växla (**Dölj** eller **Visa**) visning av Azure AD Enterprise- eller Office Online-program i Företagsportal. Användarna ser hela programkatalogen från den valda Microsoft-tjänsten. Som standard är **Dölj** valt för alla ytterligare appkällor. Den här funktionen börjar gälla först i Företagsportal-webbplatsen från version 2005 och stöd för Windows-, iOS/iPad- och macOS-företagsportaler förväntas följa. Du hittar den här kommande inställningen i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) genom att välja **Administration av klientorganisation** > **Anpassning**. Mer information finns i [Anpassa Intune Företagsportal-appar, företagsportalens webbplats och Intune-appen](../apps/company-portal-app.md).

### <a name="search-the-intune-docs-from-the-company-portal---1736480---"></a>Söka i Intune-dokument från Företagsportal<!-- 1736480 -->
Nu kan du söka i Intune-dokumentationen direkt från appen Företagsportal för macOS. Välj **Hjälp** > **Sök** i menyfältet och ange några nyckelord för att snabbt hitta svar på dina frågor.

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Företagsportal för Android hjälper användarna att hämta appar utifrån registreringen av arbetsprofilen <!-- 6103999  -->
Vi förbättrar vägledningen i appen i Företagsportal så att användarna enklare kan hitta och installera appar.  När användaren har registrerat sin arbetsprofil visas ett meddelande som talar om att de kan hitta föreslagna appar i den märkta versionen av Google Play. Användarna ser också den nya länken **Hämta appar** i Företagsportal-lådan till vänster. För att möjliggöra det här har vi tagit bort fliken **APPAR**. 

### <a name="android-company-portal-user-experience---5736084---"></a>Användarupplevelsen i företagsportalen för Android<!-- 5736084 -->
I 2005-versionen av Android Företagsportal kommer slutanvändare på Android-enheter som får en varning, blockering eller rensning via en appskyddspolicy att se en ny användarupplevelse. I stället för den nuvarande dialogrutan ser slutanvändarna ett meddelande som beskriver orsaken till varningen, blockeringen eller rensningen och stegen för att åtgärda problemet. Mer information finns i [Appskyddsupplevelse för Android-enheter](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) och [Inställningar för Android-appskyddsprinciper i Microsoft Intune](../apps/app-protection-policy-settings-android.md).


<!-- ***********************************************-->
## <a name="device-configuration"></a>Enhetskonfiguration

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

### <a name="configure-system-extensions-on-macos-devices---6255624----"></a>Konfigurera systemtillägg på macOS-enheter<!-- 6255624  -->
På macOS-enheter kan du skapa en kernel-tilläggsprofil för att konfigurera inställningar på kernelnivå (**Enheter** > **Konfigurationsprofiler** > **macOS** för plattformen > **Kernel-tillägg** för profiler). Apple håller på att återkalla kerneltillägg och ersätter dem med systemtillägg i en framtida version. Systemtillägg körs i användarutrymmet och ger inte tillgång till kerneln. Målet är att öka säkerheten och ge mer kontroll till slutanvändaren, samtidigt som attacker på kernelnivå begränsas. Med både kerneltillägg och systemtillägg kan användare installera apptillägg som utökar de inbyggda funktionerna i operativsystemet.

I Intune kan du konfigurera både kerneltillägg och systemtillägg (**Enheter** > **Konfigurationsprofiler** > **macOS** för plattformen > **Systemtillägg** för profiler). Kerneltillägg gäller för 10.13.2 och senare. Systemtillägg gäller för 10.15 och senare. Från macOS 10.15 till macOS 10.15.4 kan kerneltillägg och systemtillägg användas tillsammans. 

Information om kerneltillägg på macOS-enheter finns i [Lägga till kerneltillägg i macOS](../configuration/kernel-extensions-overview-macos.md).

Gäller för:
- macOS 10.15 och senare

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Enhetsregistrering

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>VPN kan användas för att distribuera egna enheter (BYOD, Bring Your Own Device)<!--5015344 -->
Den här funktionen kan vara försenad.

### <a name="automated-device-sync-interval-down-to-12-hours--3077535---"></a>Automatiskt intervall för synkronisering av enheter sänks till 12 timmar<!--3077535 -->
För Apples Automated Device Enrollment sänks det automatiserade synkroniseringsintervallet mellan Intune och Apple Business Manager från 24 timmar till 12 timmar. Mer information om synkronisering finns i [Synkronisering av hanterade enheter](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).

### <a name="autopilot-support-for-hololens-2-devices--6305220--"></a>Autopilot-stöd för HoloLens 2-enheter<!--6305220-->
Windows Autopilot får stöd för HoloLens 2-enheter. Mer information om att använda Autopilot i Intune finns i [Registrera Windows-enheter i Intune med hjälp av Windows Autopilot](../enrollment/enrollment-autopilot.md).

### <a name="enrollment-restrictions-will-support-scope-tags--4209550---"></a>Vi inför stöd för omfångstaggar i registreringen<!--4209550 -->
Du kan tilldela omfångstaggar i registreringsbegränsningar. Det gör du genom att gå till [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **Registreringsbegränsningar** > **Skapa begränsning**. Skapa någon typ av begränsning så visas sidan **Omfångstaggar**.

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


### <a name="macos-script-support---6376978----"></a>stöd för macOS-skript<!-- 6376978  -->
Nu är skriptstöd för macOS allmänt tillgängligt. Dessutom lägger vi till stöd för både användartilldelade skript och macOS-enheter som har registrerats med Apples Automated Device Enrollment (tidigare Programmet för enhetsregistrering). Mer information finns i [Använda Shell-skript på macOS-enheter i Intune](../apps/macos-shell-scripts.md).

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

### <a name="derived-credentials-support-for-disa-purebred-on-android-devices--4839592---"></a>Stöd för härledda autentiseringsuppgifter för DISA Purebred på Android-enheter<!--4839592 -->
Du kommer att kunna använda *DISA Purebred* som en leverantör för [härledda autentiseringsuppgifter](../protect/derived-credentials.md) på fullständigt hanterade Android Enterprise-enheter (**klientadministration** > **Anslutningar och token** > **Härledda autentiseringsuppgifter**). Support kommer att inkluderas för att hämta en härledd autentiseringsuppgift för DISA Purebred. Du kan använda en härledd autentiseringsuppgift för appautentisering, Wi-Fi, VPN eller S/MIME-signering och/eller kryptering med appar som stöder det. 

I april lade Intune till stöd för *Entrust Datacard* och *Intercede* som leverantörer för härledda autentiseringsuppgifter. 

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Sekretessinställningar för macOS-enheter<!-- 2934232 --> 
Med lanseringen av macOS Catalina 10.15 har Apple lagt till nya förbättringar av säkerhet och sekretess. Som standard kan program och processer inte komma åt specifika data utan användarmedgivande. Om användarna inte ger medgivande kan det hända att programmen och processerna inte fungerar. Intune lägger till stöd för inställningar som gör att IT-administratörer kan tillåta eller neka medgivande för dataåtkomst åt slutanvändare på enheter som kör macOS 10.14 och senare. De här inställningarna ser till att program och processer fortsätter att fungera korrekt och minskar det antal meddelanden som slutanvändarna får.


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Duplicera policyer i Endpoint Security<!-- 5892558   -->
Du kan välja en policy du har skapat i Endpoint Security-noden i administrationscentret för Microsoft Endpoint Manager och sedan kopiera den.  Du kan kopiera följande policyer: 

- Antivirus
- Diskkryptering
- Brandvägg
- Slutpunktsidentifiering och svar
- Minska attackytan
- Kontoskydd

Den ursprungliga policyn kopieras, och sedan kan du byta namn på och redigera den. Kopian innehåller inte samma tilldelningar som originalet.

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Skicka push-meddelanden som en åtgärd för inkompatibilitet <!-- 1733150   -->
För iOS och Android lägger vi till en ny åtgärd för inkompatibilitet som skickar ett push-meddelande via företagsportalsappen. När en användare klickar på det här meddelandet startas företagsportalsappen, och i appen visas information om inkompatibilitetsorsaken. Administratörer kan konfigurera den nya åtgärden för inkompatibilitet i Microsoft Endpoint Manager admin center genom att gå till **Enheter** > **Kompatibilitetsprinciper** > **Skapa princip** och sedan välja *Åtgärd* för att skicka ett push-meddelande via app. 

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Ny profil för Endpoint Security Firewall-policy<!-- 5653324   -->
I en förhandsversion har vi lagt till ytterligare en profil för Windows 10 och senare i Firewall-policyn för Intunes Endpoint Security (**Endpoint Security** > **Brandvägg** > **Skapa policy** > välj **Windows 10 och senare**). 

Varje instans av den här nya profilen har stöd för upp till 150 anpassade *Microsoft Defender Firewall-regler*. Med Microsoft Defender Firewall-regelpolicyn kan du definiera detaljerade regler för Windows Firewall som tillåter eller blockerar portar och program i Windows 10.

<!-- ***********************************************-->
## <a name="notices"></a>Meddelanden

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Se även

Mer information om den senaste utvecklingen finns i [Nyheter i Microsoft Intune](whats-new.md).



