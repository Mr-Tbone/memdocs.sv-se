---
title: Nyheter i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Ta reda på vad som är nytt i Intune Azure-portalen
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: ca3ec1605bd4d63c182511c32297da0bdb503d8b
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83824174"
---
# <a name="whats-new-in-microsoft-intune"></a>Nyheter i Microsoft Intune

Lär dig mer om nyheter i Microsoft Intune varje vecka i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Du kan också hitta [viktiga meddelanden](#notices), [tidigare versioner](whats-new-archive.md) och information om [hur uppdateringar av Intune-tjänsten släpps](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728). 

> [!Note]
> Varje [månadsuppdatering](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) kan ta upp till tre dagar att distribuera och sker i följande ordning:
>
> - Dag 1: Asien och stillahavsområdet
> - Dag 2: Europa, Mellanöstern och Afrika
> - Dag 3: Nordamerika
> - Dag 4+: Intune för myndigheter
>
> Vissa funktioner kan distribueras över flera veckor och kanske inte är tillgängliga för alla kunder den första veckan.
>
> Titta närmare på sidan [Under utveckling ](in-development.md) för en lista över kommande funktioner i en version.

**RSS-feed**: Håll dig informerad när den här sidan uppdateras genom att kopiera och klistra in följande webbadress i feed-läsaren: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot

<!-- ########################## -->

## <a name="week-of-may-18-2020"></a>Den vecka som börjar 18 maj 2020

### <a name="device-security"></a>Enhetssäkerhet

#### <a name="use-endpoint-detection-and-response-policy-to-onboard-devices-to-defender-atp---7130165----"></a>Använd policyn Slutpunktsidentifiering och svar till att registrera enheter i Defender ATP<!-- 7130165  -->

Använd Endpoint Security-policyn [Slutpunktsidentifiering och svar](../protect/endpoint-security-edr-policy.md) (EDR) till att registrera och konfigurera enheter i distributionen av Microsoft Defender Advanced Threat Protection (Defender ATP). EDR har stöd för policyer för Windows-enheter som hanteras via Intune (MDM) och en separat policy för Windows-enheter som hanteras via Configuration Manager. 

Om du vill använda policyn för Configuration Manager-enheter måste du [konfigurera Configuration Manager med stödet för EDR-policyn](../protect/endpoint-security-edr-policy.md#set-up-configuration-manager-to-support-edr-policy). I konfigurationen måste du bland annat:

- Konfigurera Configuration Manager for *anslutning av klientorganisationen*.
- Installera en konsoluppdatering för Configuration Manager som aktiverar stödet för EDR-policyer. Den här uppdateringen gäller endast för hierarkier som har aktiverat *anslutning av klientorganisationer*.
- Synkronisera dina enhetssamlingar från hierarkin till administrationscentret för Microsoft Endpoint Manager.


## <a name="week-of-may-11-2020-2005-service-release"></a>Veckan som börjar den 11 maj 2020 (2005 Service Release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="customize-self-service-device-actions-in-the-company-portal--4393379---"></a>Anpassa åtgärder för självbetjäningsenhet i Företagsportal<!--4393379 -->
Du kan anpassa vilka självbetjäningsåtgärder som visas för slutanvändare i appen Företagsportal och på webbplatsen. För att förhindra oavsiktliga enhetsåtgärder kan du konfigurera de här inställningarna för appen Företagsportal genom att välja **Administration av klientorganisation** > **Anpassning**. Följande alternativ är tillgängliga:
- Dölj knappen **Ta bort** på Windows-företagsenheter.
- Dölj knappen **Återställ** på Windows-företagsenheter.
- Dölj knappen **Återställ** på iOS-företagsenheter.
- Dölj knappen **Ta bort** på iOS-företagsenheter.
Mer information finns i [Åtgärder för självbetjäningsenhet för användare från företagsportalen](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

#### <a name="auto-update-vpp-available-apps---3640511----"></a>Uppdatera VPP-tillgängliga appar automatiskt<!-- 3640511  -->
Appar som är publicerade som VPP-tillgängliga appar (VPP) uppdateras automatiskt när **Automatisk uppdatering av appar** är aktiverat för VPP-token. Tidigare uppdaterades inte VPP-tillgängliga appar automatiskt. Slutanvändarna behövde i stället gå till Företagsportal och installera om appen om det fanns en nyare version. Obligatoriska appar har fortfarande stöd för automatiska uppdateringar.


#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---4404429-----"></a>Enhetlig leverans av Azure AD Enterprise- och Office Online-program i Företagsportal<!-- 4404429   -->
*Den här funktionen har skjutits upp.*
I fönstret **Anpassning** i Intune kan du välja att **Dölja** eller **Visa** både **Azure AD Enterprise-program** och **Office Online-program** i Företagsportal. Slutanvändarna ser hela programkatalogen från den valda Microsoft-tjänsten. Som standard är **Dölj** valt för alla ytterligare appkällor. Den här funktionen börjar först gälla på Företagsportal-webbplatsen. Stödet för Windows-, iOS/iPad- och macOS-företagsportaler förväntas komma. Du hittar den här konfigurationsinställningen i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) genom att välja **Administration av klientorganisation** > **Anpassning**. Mer information finns i [Anpassa Intune Företagsportal-appar, företagsportalens webbplats och Intune-appen](../apps/company-portal-app.md).

#### <a name="android-company-portal-user-experience---5736084----"></a>Användarupplevelsen i företagsportalen för Android<!-- 5736084  -->
I 2005-versionen av Android Företagsportal kommer slutanvändare på Android-enheter som får en varning, blockering eller rensning via en appskyddspolicy att se en ny användarupplevelse. I stället för den nuvarande dialogrutan ser slutanvändarna ett meddelande som beskriver orsaken till varningen, blockeringen eller rensningen och stegen för att åtgärda problemet. Mer information finns i [Appskyddsupplevelse för Android-enheter](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) och [Inställningar för Android-appskyddsprinciper i Microsoft Intune](../apps/app-protection-policy-settings-android.md).

#### <a name="support-for-multiple-accounts-in-company-portal-for-macos---5779449----"></a>Stöd för flera konton i Företagsportal för macOS<!-- 5779449  -->
Företagsportal för macOS-enheter cachelagrar nu användarkonton, vilket gör det enklare att logga in. Användare behöver inte längre logga in i Företagsportal varje gång de startar programmet. Dessutom visar Företagsportal en kontoväljare om flera användarkonton är cachelagrade, så att användarna inte behöver ange sitt användarnamn. 

#### <a name="newly-available-protected-apps---7060934-----"></a>Nyligen tillgängliga skyddade appar<!-- 7060934   -->
Följande skyddade appar är nu tillgängliga:
- Board Papers
- Breezy for Intune
- Hearsay Relate for Intune
- ISEC7 Mobile Exchange Delegate for Intune
- Lexmark for Intune
- Meetio Enterprise
- Microsoft Whiteboard
- Now® Mobile - Intune
- Qlik Sense Mobile 
- ServiceNow® Agent - Intune
- ServiceNow® Onboarding - Intune
- Smartcrypt for Intune
- Tact for Intune
- Zero - email for attorneys

Mer information om skyddade appar finns i [Microsoft Intune-skyddade appar](../apps/apps-supported-intune-apps.md).

#### <a name="search-the-intune-docs-from-the-company-portal---1736480-----"></a>Söka i Intune-dokument från Företagsportal<!-- 1736480   -->
Nu kan du söka i Intune-dokumentationen direkt från appen Företagsportal för macOS. Välj **Hjälp** > **Sök** i menyfältet och ange några nyckelord för att snabbt hitta svar på dina frågor.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="improvements-to-oemconfig-support-for-zebra-technologies-devices---4184154---"></a>Förbättringar av OEMConfig-stödet för Zebra Technologies-enheter<!-- 4184154 -->
Intune har fullständigt stöd för alla funktioner som tillhandahålls av Zebra OEMConfig. Kunder som hanterar Zebra Technologies-enheter med Android Enterprise och OEMConfig kan distribuera flera OEMConfig-profiler till samma enhet. Kunder kan också visa omfattande rapportering om statusen för sina Zebra OEMConfig-profiler.

Mer information finns i [Distribuera flera OEMConfig-profiler till Zebra-enheter i Microsoft Intune](../configuration/oemconfig-zebra-android-devices.md).

OEMConfig-beteendet ändras inte för andra OEM-tillverkare.

Gäller för:
- Android enterprise
- Zebra Technologies-enheter med stöd för OEMConfig. Om du vill veta mer om support kontaktar du Zebra.

#### <a name="configure-system-extensions-on-macos-devices---6255624---"></a>Konfigurera systemtillägg på macOS-enheter<!-- 6255624 -->
På macOS-enheter kan du skapa en kernel-tilläggsprofil för att konfigurera inställningar på kernelnivå (**Enheter** > **Konfigurationsprofiler** > **macOS** för plattformen > **Kernel-tillägg** för profiler). Apple håller på att återkalla kerneltillägg och ska ersätta dem med systemtillägg i en framtida version.

Systemtillägg körs i användarmiljön och har inte tillgång till kerneln. Målet är att öka säkerheten och ge mer kontroll till slutanvändaren, samtidigt som attacker på kernelnivå begränsas. Med både kerneltillägg och systemtillägg kan användare installera apptillägg som utökar de inbyggda funktionerna i operativsystemet.

I Intune kan du konfigurera både kerneltillägg och systemtillägg (**Enheter** > **Konfigurationsprofiler** > **macOS** för plattformen > **Systemtillägg** för profiler). Kerneltillägg gäller för 10.13.2 och senare. Systemtillägg gäller för 10.15 och senare. Från macOS 10.15 till macOS 10.15.4 kan kerneltillägg och systemtillägg användas tillsammans. 

Information om de här tilläggen för macOS-enheter finns i [Lägga till macOS-tillägg](../configuration/kernel-extensions-overview-macos.md).

Gäller för:
- macOS 10.15 och senare

#### <a name="configure-app-and-process-privacy-preferences-on-macos-devices---2934232-----"></a>Konfigurera sekretessinställningar för appar och processer på macOS-enheter<!-- 2934232   --> 
Med lanseringen av macOS Catalina 10.15 har Apple lagt till nya förbättringar av säkerhet och sekretess. Som standard kan program och processer inte komma åt specifika data utan användarmedgivande. Om användarna inte samtycker kanske inte programmen och processerna fungerar. Intune lägger till stöd för inställningar som gör att IT-administratörer kan tillåta eller neka medgivande för dataåtkomst åt slutanvändare på enheter som kör macOS 10.14 och senare. De här inställningarna ser till att program och processer fortsätter att fungera korrekt och minskar antalet uppmaningar. 

Mer information om de inställningar du kan hantera finns i [Sekretessinställningar i macOS](../configuration/device-restrictions-macos.md#privacy-preferences).

Gäller för:
- macOS 10.14 och senare

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Enhetsregistrering

#### <a name="enrollment-restrictions-support-scope-tags--4209550----"></a>Stöd för omfångstaggar i registreringsbegränsningar<!--4209550  -->
Nu kan du tilldela omfångstaggar i registreringsbegränsningar. Det gör du genom att gå till [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **Registreringsbegränsningar** > **Skapa begränsning**. Skapa någon typ av begränsning så visas sidan **Omfångstaggar**. Mer information finns i [Konfigurera registreringsrestriktioner](../enrollment/enrollment-restrictions-set.md).

#### <a name="autopilot-support-for-hololens-2-devices--6305220----"></a>Autopilot-stöd för HoloLens 2-enheter<!--6305220  -->
Windows Autopilot har nu stöd för HoloLens 2-enheter. Mer information om att använda Autopilot för Hololens finns i [Windows Autopilot för HoloLens 2](https://docs.microsoft.com/hololens/hololens2-autopilot).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="use-sync-remote-action-in-bulk-for-ios--6440956--idmiss--"></a>Använda fjärrsynkronisering som massåtgärd i iOS<!--6440956  idmiss-->
Nu kan du använda åtgärden fjärrsynkronisering för upp till 100 iOS-enheter åt gången. Om du vill se den här funktionen går du till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **Alla enheter** > **Massåtgärder för enheter**. 

#### <a name="automated-device-sync-interval-down-to-12-hours--3077535----"></a>Automatiskt intervall för synkronisering av enheter sänks till 12 timmar<!--3077535  -->
För Apples Automated Device Enrollment har det automatiserade synkroniseringsintervallet mellan Intune och Apple Business Manager sänkts från 24 timmar till 12 timmar. Mer information om synkronisering finns i [Synkronisering av hanterade enheter](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Enhetssäkerhet

#### <a name="derived-credentials-support-for-disa-purebred-on-android-devices---6939073-------"></a>Stöd för härledda autentiseringsuppgifter för DISA Purebred på Android-enheter<!-- 6939073     -->
Nu kan du använda *DISA Purebred* som provider för [härledda autentiseringsuppgifter](../protect/derived-credentials.md) på helt hanterade Android Enterprise-enheter. I stödet ingår att du kan hämta en härledd autentiseringsuppgift för DISA Purebred. Du kan använda en härledd autentiseringsuppgift till appautentisering, Wi-Fi, VPN eller S/MIME-signering och/eller kryptering med appar som har stöd för det. 

#### <a name="send-push-notifications-as-an-action-for-noncompliance----1733150-----"></a>Skicka push-meddelanden som en åtgärd när efterlevnadsreglerna inte uppfylls <!-- 1733150   -->
Nu kan du konfigurera en [åtgärd när efterlevnadsreglerna inte uppfylls](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) som skickar ett push-meddelande till användaren om enheten inte uppfyller ett av villkoren i en efterlevnadspolicy. Den nya åtgärden är **Skicka push-meddelande till slutanvändaren** kan användas på Android- och iOS-enheter.

När användarna väljer push-meddelandet på enheten öppnas Företagsportal- eller Intune-appen med information om vilken regel som inte uppfylls.

#### <a name="endpoint-security-content-and-new-features---5720009-5892558-7130145-5653324-7140602----"></a>Endpoint Security-innehåll och nya funktioner<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

Nu är dokumentationen för [Endpoint Security](../protect/endpoint-security.md) tillgänglig. I noden Endpoint Security i administrationscentret för Microsoft Endpoint Manager kan du nu:

- Skapa och distribuera fokuserade säkerhetspolicyer till dina hanterade enheter
- Konfigurera integrering med Microsoft Defender Advanced Threat Protection och hantera säkerhetsaktiviteter som åtgärdar de enheter utsatta för risk som ATP-teamet identifierar
- Konfigurera säkerhetsbaslinjer
- Hantera policyer för enheters efterlevnad och villkorsstyrd åtkomst
- Visa efterlevnadsstatus för alla enheter från både Intune och Configuration Manager när Configuration Manager är konfigurerat för klientanslutning.

Utöver tillgängligheten för innehåll är det här några nyheter i Endpoint Security den här månaden:

- [**Endpoint Security-policyer**](../protect/endpoint-security-policy.md) **är inte längre i** ***förhandsversion*** och är nu redo att användas i produktionsmiljöer, som *allmänt tillgängliga*, med två undantag:

  - I en ny *offentlig förhandsversion* kan du använda profilen [**Microsoft Defender-brandväggsregler** ](../protect/endpoint-security-firewall-policy.md#firewall-profiles) som brandväggspolicy i Windows 10. Med varje instans av den här profilen kan du konfigurera upp till 150 brandväggsregler som komplement till dina Microsoft Defender-brandväggsprofiler. 
  - Policyn för kontoskydd är fortfarande i förhandsversion. 

- Nu kan du [**kopiera policyer för slutpunktsskydd**](../protect/endpoint-security-policy.md#duplicate-a-policy). Kopiorna behåller samma inställningskonfiguration som den ursprungliga principen, men får ett nytt namn. Den nya policyinstansen innehåller inte några tilldelningar till grupper förrän du redigerar den nya policyinstansen och lägger till dem. Du kan kopiera följande policyer:
  - Antivirus
  - Diskkryptering
  - Brandvägg
  - Slutpunktsidentifiering och svar
  - Minska attackytan
  - Kontoskydd

- Nu kan du [**kopiera en säkerhetsbaslinje**](../protect/security-baselines.md#duplicate-a-security-baseline). Kopian behåller samma inställningskonfiguration som den ursprungliga baslinjen, men får ett nytt namn. Den nya baslinjeinstansen innehåller inga tilldelningar till grupper förrän du redigerar den nya baslinjeinstansen och lägger till dem.

- Det finns en ny rapport för Endpoint Security-policyn Antivirus: [**Defekta slutpunkter i Windows 10**](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints). Den här rapporten är en ny sida du kan välja när du visar Endpoint Security-policyn Antivirus. Rapporten visar antivirusstatus för dina MDM-hanterade Windows 10-enheter.  

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android---7207474----"></a>Stöd för S/MIME-signering och krypteringscertifikat med Outlook i Android<!-- 7207474  -->
Nu kan du använda certifikat för S/MIME-signering och kryptering med Outlook i Android. Med det här stödet kan du etablera certifikaten med hjälp av SCEP, PKCS och importerade PKCS-certifikatprofiler. Följande Android-plattformar stöds:

- Android Enterprise-arbetsprofil
- Android-enhetsadministratör

Stödet för helt hanterade Android Enterprise-enheter kommer snart.

Mer information om det här stödet finns i [Känslighetsetiketter och skydd i Outlook för iOS och Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) i Exchange-dokumentationen.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

#### <a name="device-reports-ui-update---6269408---"></a>Uppdatering av gränssnittet för enhetsrapporter<!-- 6269408 -->
I rapportöversikten finns nu flikarna **Sammanfattning** och **Rapporter**. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Rapporter** och sedan fliken **Rapporter** för att se de tillgängliga rapporttyperna. Mer information finns i [Intune-rapporter](../fundamentals/reports.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Använda skript

#### <a name="macos-script-support---6376978----"></a>stöd för macOS-skript<!-- 6376978  -->
Nu är skriptstöd för macOS allmänt tillgängligt. Dessutom har vi lagt till stöd för både användartilldelade skript och macOS-enheter som har registrerats med Apples Automated Device Enrollment (tidigare Programmet för enhetsregistrering). Mer information finns i [Använda Shell-skript på macOS-enheter i Intune](../apps/macos-shell-scripts.md).


<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>Den vecka som börjar 4 maj 2020  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>Företagsportal för Android hjälper användarna att hämta appar utifrån registreringen av arbetsprofilen <!-- 6103999 -->
Vi förbättrar vägledningen i appen i Företagsportal så att användarna enklare kan hitta och installera appar. När användaren har registrerat sin arbetsprofil ser de ett meddelande som förklarar att de kan hitta föreslagna appar i den märkta versionen av Google Play. Det sista steget i [Registrera enhet med Android-profil](../user-help/enroll-device-android-work-profile.md) har uppdaterats för att visa det nya meddelandet. Användarna ser också den nya länken **Hämta appar** i Företagsportal-lådan till vänster. För att möjliggöra det här har vi tagit bort fliken **APPAR**. Om du vill se de uppdaterade skärmarna går du till [Uppdateringar i användargränssnittet för Intunes slutanvändarappar](./whats-new-app-ui.md). 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>Veckan som börjar 20 april 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758----"></a>Ansluta Microsoft Endpoint Manager-klientorganisation: Enhetssynkronisering och enhetsåtgärder<!-- 6317104, CM3555758  -->
Microsoft Endpoint Manager sammanfogar Configuration Manager och Intune i en enda konsol. Från och med Configuration Manager version 2002 kan du ladda upp dina Configuration Manager-enheter till molntjänsten och vidta åtgärder i administrationscentret. Mer information finns i [Microsoft Endpoint Manager-klientorganisation: Enhetssynkronisering och enhetsåtgärder](../../configmgr/tenant-attach/device-sync-actions.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>Nytt namn för Microsoft Office 365 ProPlus<!-- 6368143 -->
Microsoft Office 365 ProPlus har bytt namn till **Microsoft 365 Apps for enterprise**. Läs mer i [Nytt namn för Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). I vår dokumentation kallar vi det ofta för Microsoft 365 Apps. I [administrationscenter för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) hittar du Apps-serien genom att välja **Apps** > **Windows** > **Lägg till**. Mer information om hur du lägger till appar finns i [Lägga till appar i Microsoft Intune](../apps/apps-add.md).

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>Veckan för den 13 april 2020 (2004 tjänstversion)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>Hantera S/MIME-inställningar för Outlook på Android Enterprise-enheter<!-- 6517085   -->
Du kan använda appkonfigurationsprinciper för att hantera S/MIME-inställningen för Outlook på enheter som kör Android Enterprise. Du kan också välja om enhetsanvändare ska kunna aktivera eller inaktivera S/MIME i Outlook-inställningarna eller inte. Om du vill använda appkonfigurationsprinciper för Android går du till [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) och väljer **Appar** > **Appkonfigurationsprinciper** > **Lägg till** > **Hanterade enheter**. Mer information om hur du konfigurerar inställningar för Outlook finns i [konfigurationsinställningar för Microsoft Outlook](../apps/app-configuration-policies-outlook.md).

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Förhandstestning för hanterade Google Play-appar<!-- 2681933  -->
Organisationer som använder [Google Plays slutna testkanaler för förhandstestning av appar](https://support.google.com/googleplay/android-developer/answer/3131213) kan hantera dessa kanaler med Intune. Du kan selektivt tilldela appar (som publiceras på Google Plays förproduktionskanaler) till pilotgrupper för testning. I Intune kan du se om en app har en testkanal med en publicerad förproduktionsversion, och du kommer att kunna tilldela den kanalen till grupper med AAD-användare eller -enheter. Den här funktionen är tillgänglig för alla våra aktuella Android Enterprise-scenarier (arbetsprofil, fullständigt hanterad, särskilt avsedd). I [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) kan du lägga till en hanterad Google Play-app genom att välja **Appar** > **Android** > **Lägg till**. Mer information finns i [Working with Managed Google Play Closed Testing Tracks](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks) (arbeta med testspår på Hanterat Google Play-konto).

#### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams ingår nu i Office 365-paketet för macOS<!-- 5903936  -->
Användare som tilldelas Microsoft Office för macOS i Microsoft Endpoint Manager får förutom de vanliga Microsoft Office-apparna (Word, Excel, PowerPoint, Outlook och OneNote) nu även Microsoft Teams. Intune identifierar befintliga Mac-enheter som har andra Office för macOS-appar installerade och kommer att försöka installera Microsoft Teams nästa gång enheten checkar in med Intune. I [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) kan du hitta **Office 365-paketet** för macOS genom att välja **Appar** > **macOS** > **Lägg till**. Mer information finns i [Tilldela Office 365 till macOS-enheter med Microsoft Intune](../apps/apps-add-office365-macos.md).

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>Uppdatering av konfigurationsprinciper för Android-appar<!-- 6113334  -->
Konfigurationsprinciperna för Android-appar har uppdaterats så att administratörer kan välja typ av enhetsregistrering innan de skapar konfigurationsprofiler för appar. Funktionen läggs till i kontot för certifikatprofiler som baseras på registreringstyp (arbetsprofil eller enhetsägare).  Den här uppdateringen innehåller följande:

1. Om en ny profil skapas och arbetsprofil och enhetsägarprofil väljs som enhetsregistreringstyp kan du inte associera en certifikatprofil med appkonfigurationsprincipen.
2. Om en ny profil skapas och Endast arbetsprofil har valts kan de certifikatprinciper för arbetsprofil som skapats under Enhetskonfiguration användas.
3. Om en ny profil skapas och Endast enhetens ägare har valts kan de certifikatprinciper för enhetsägare som skapats under Enhetskonfiguration användas. 

> [!IMPORTANT]
> För de befintliga principer som skapats före lanseringen av den här funktionen (april 2020, version 2004) och som inte har några associerade certifikatprofiler, används som standard arbetsprofil och enhetsägarprofil som enhetsregistreringstyp. Även för de befintliga principer som skapats före lanseringen av den här funktionen och som har associerade certifikatprofiler, används som standard endast arbetsprofil.

Vi lägger också till e-postkonfigurationsprofiler för Gmail och Nine som fungerar för både registreringstypen Arbetsprofil och Enhetsägare. Detta innefattar användning av certifikatprofiler på båda e-postkonfigurationstyperna.  Alla Gmail- eller Nine-principer som du har skapat under Enhetskonfiguration för arbetsprofiler fortsätter att gälla för enheten och du behöver inte flytta dem till appkonfigurationsprinciper.

I [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) hittar du appkonfigurationsprinciperna genom att välja **Appar** > **Appkonfigurationsprinciper**. Mer information om appkonfigurationsprinciper finns i [Appkonfigurationsprinciper för Microsoft Intune](../apps/app-configuration-policies-overview.md).

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>Push-meddelande när ägarskapstypen för enheten ändras<!-- 5575875 -->
Du kan konfigurera ett push-meddelande till användarna av företagsportalsappen (både Android och iOS) när deras ägarskapstyp ändras från Personlig till Företag som en integritetsmeddelande. Push-meddelandet är inställt på av som standard. Inställningen hittar du i Microsoft Endpoint Manager genom att välja **Innehavaradministration** > **Anpassning**. Mer information om hur enhetsägarskapet påverkar slutanvändarna finns i [Ändra enhetsägande](../enrollment/corporate-identifiers-add.md#change-device-ownership).

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>Stöd för riktning till grupper i fönstret Anpassning<!-- 4722837  -->
Du kan rikta inställningarna i fönstret **Anpassning** till användargrupper. Du hittar de här inställningarna i Intune genom att gå till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), välja **Administration av klientorganisation** > **Anpassning**. Mer information om anpassning finns i [Anpassa Intune-företagsportalens appar, företagsportalens webbplats och Intune-appen](../apps/company-portal-app.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>Flera VPN-regler på begäran för att utvärdera varje anslutningsförsök som stöds på iOS, iPad och macOS<!-- 6424615  -->
Användarupplevelsen i Intune tillåter flera VPN-regler på begäran i samma VPN-profil med åtgärden **Utvärdera varje anslutningsförsök** (**enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPad** eller **macOS** för plattform > **VPN** för profilen > **Automatisk VPN** > **På begäran**).

Den använde enbart den första regeln i listan. Det här beteendet har åtgärdats, och Intune utvärderar alla regler i listan. Varje regel utvärderas i den ordning som den visas i listan över regler på begäran.

> [!NOTE]
> Om du har befintliga VPN-profiler som använder dessa VPN-regler på begäran tillämpas åtgärden nästa gång du ändrar VPN-profilen. Du kan till exempel göra en mindre ändring, t. ex. ändra anslutningens namn, och sedan spara profilen.
>
> Om du använder SCEP-certifikat för autentisering orsakar den här ändringen att certifikaten för VPN-profilen utfärdas igen.

Gäller för:
- iOS/iPadOS
- macOS

Mer information om VPN-profiler finns i [Skapa VPN-profiler](../configuration/vpn-settings-configure.md).

#### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155-----"></a>Ytterligare alternativ i SSO- och SSO-apptilläggsprofiler på iOS/iPadOS-enheter<!-- 6504155   -->

På iOS/iPadOS-enheter kan du:
- Ange SAM-kontonamnet (Hanteraren för kontosäkerhet) som Kerberos-huvudnamn i SSO-profiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** som plattform > **Enhetsfunktioner** som profil > **Enkel inloggning**). 
- Konfigurera Microsoft Azure AD-tillägget för iOS/iPadOS med färre klick med hjälp av den nya SSO-apptilläggstypen i SSO-apptilläggsprofiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** som plattform > **Enhetsfunktioner** som profil > **Tillägg för enkel inloggning**). Du kan aktivera Azure AD-tillägget för enheter i läget för delade enheter och skicka tilläggsspecifika data till tillägget.

Gäller för:
- iOS/iPadOS 13.0+

Mer information om hur du använder enkel inloggning på iOS/iPadOS-enheter finns i [Tilläggsöversikten för enkel inloggning](../configuration/device-features-configure.md#single-sign-on-app-extension) och [listan med inställningar för enkel inloggning](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Enhetsregistrering

#### <a name="delete-apple-automated-device-enrollment-token-when-default-profile-is-present--6393220---"></a>Ta bort Apples token för automatisk enhetsregistrering när standardprofilen finns<!--6393220 -->
Tidigare gick det inte att ta bort en standardprofil, vilket innebar att du inte kunde ta bort det token för automatisk enhetsregistrering som var associerat med profilen. Nu kan du ta bort ett token när:
- inga enheter har tilldelats till token
- det finns en standardprofil för detta. Ta bort standardprofilen och ta sedan bort associerat token.
Mer information finns i [Ta bort en ADE-token från Intune](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-ade-token-from-intune).

#### <a name="scaled-up-support-for-apple-automated-device-enrollment-and-apple-configurator-2-devices-profiles-and-tokens--3542402---"></a>Skalbart stöd för Apples automatiserade enhetsregistrering och Apple Configurator 2-enheter, profiler och token<!--3542402 -->
För att hjälpa distribuerade IT-avdelningar och organisationer stöder Intune nu upp till 1 000 registreringsprofiler per token, 2 000 token för automatiserad enhetsregistrering (kallades tidigare DEP) per Intune-konto, och 75 000 enheter per token. Det finns ingen specifik gräns för enheter per registreringsprofil under det högsta antalet enheter per token.

Intune stöder nu upp till 1 000 Apple Configurator 2-profiler.

Mer information finns i [Volym som stöds](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume).

#### <a name="all-devices-page-column-entry-changes--6967616---"></a>Ändrade kolumnposter på sidan Alla enheter<!--6967616 -->
På sidan **Alla enheter** har posterna för kolumnen **Hanterad av** ändrats:
- *Intune* visas nu i stället för *MDM*
- *Samhanterade* visas nu i stället för *MDM/ConfigMgr-agenten*

Exportvärdena är oförändrade.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>Versionsinformation för Trusted Platform Manager (TPM) nu på enhetens maskinvarusida<!--6224914 idmiss -->
Nu kan du se TPM-versionsnumret på enhetens maskinvarusida ([administrationscenter för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > välja en enhet > **Maskinvara** > titta under **Systemomslutning**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

#### <a name="collect-logs-to-better-troubleshoot-scripts-assigned-to-macos-devices---6359853----"></a>Samla in loggar för bättre felsökning av skript som är tilldelade till macOS-enheter<!-- 6359853  -->
Du kan nu samla in loggar för bättre felsökning av skript som har tilldelats macOS-enheter. Du kan samla in loggar upp till 60 MB (komprimerade) eller 25 filer, beroende på vilket som inträffar först. Mer information finns i [Troubleshoot macOS shell script policies using log collection](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection) (felsöka principer för macOS-kommandoskript med logginsamling).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Säkerhet

#### <a name="derived-credentials-to-provision-android-enterprise-fully-managed-devices-with-certificates--4839592------"></a>Härledda autentiseringsuppgifter för att etablera fullständigt hanterade Android Enterprise-enheter med certifikat<!--4839592    -->
Intune stöder nu användning av [härledda autentiseringsuppgifter](../protect/derived-credentials.md) som autentiseringsmetod för Android-enheter. Härledda autentiseringsuppgifter är en implementering av National Institute of Standards and Technology (NIST) 800-157-standarden för distribution av certifikat till enheter. Vårt stöd för Android är en utveckling av vårt stöd för enheter som kör iOS/iPad.

Härledda autentiseringsuppgifter är beroende av att ett PIV-kort (Personal Identity Verification) eller ett CAC-kort (Common Access Card) används, till exempel ett smartkort. För att få en härledd autentiseringsuppgift för sin mobila enhet börjar användare i Microsoft Intune-appen och följer ett registreringsarbetsflöde som är unikt för den provider som du använder. Gemensamt för alla providrar är kravet på användning av ett smartkort på en dator för autentisering till providern för den härledda autentiseringsuppgiften. Providern utfärdar sedan ett certifikat till den enhet som härleds från användarens smartkort.

Du kan använda härledda autentiseringsuppgifter som autentiseringsmetod för enhetskonfigurationsprofiler för VPN och Wi-Fi. Du kan även använda dem för appautentisering samt för S/MIME-signering och -kryptering för program som har stöd för det.

Intune stöder nu följande leverantörer för härledda autentiseringsuppgifter med Android:
- Entrust Datacard
- Intercede

En tredje leverantör, DISA Purebred, blir tillgänglig för Android i en framtida version.

#### <a name="microsoft-edge-security-baseline-is-now-generally-available--6586139---"></a>Microsoft Edge säkerhetsbaslinje är nu allmänt tillgängligt<!--6586139 -->

En ny version av [Microsoft Edge säkerhetsbaslinje](../protect/security-baselines.md#available-security-baselines) är nu tillgänglig och släpps som allmänt tillgänglig (GA). Den tidigare Edge-baslinjen fanns som förhandsversion.  Den nya baslinjeversionen är april 2020 (Edge version 80 och senare). 

I och med lanseringen av den nya baslinjen kan du inte längre skapa profiler baserade på tidigare baslinjeversioner, men du kan fortsätta att använda profiler som du har skapat med dessa versioner. Du kan också välja att [uppdatera dina befintliga profiler så att de använder den senaste baslinjeversionen](../protect/security-baselines.md#change-the-baseline-version-for-a-profile). 

<!-- ########################## -->
## <a name="week-of-april-6-2020"></a>Veckan som börjar 6 april 2020

#### <a name="new-shell-script-settings-for-macos-devices---6884363---"></a>Nya Shell-skript-inställningar för macOS-enheter<!-- 6884363 -->
När du konfigurerar Shell-skript för macOS-enheter, kan du nu konfigurera följande nya inställningar: 
- Dölja skriptmeddelanden på enheter
- Skriptfrekvens
- Maximalt antal nya försök om skriptet misslyckas

Mer information finns i [Använda Shell-skript på macOS-enheter i Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>Den vecka som börjar 30 mars 2020

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Ny URL för administrationscentret för Microsoft Endpoint Manager<!-- 3704810 -->
För att anpassa efter tillkännagivandet om Microsoft Endpoint Manager på Ignite förra året har vi ändrat URL:en för administrationscentret för Microsoft Endpoint Manager (tidigare Microsoft 365-enhetshantering) till [https://endpoint.microsoft.com](https://endpoint.microsoft.com). Den gamla URL:en för administrationscentret ([https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com)) fortsätter att fungera, men vi rekommenderar att du börjar använda den nya URL:en för administrationscentret för Microsoft Endpoint Manager.

Mer information finns i [Förenkla IT-uppgifter med hjälp av administrationscentret för Microsoft Endpoint Manager](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center).  


### <a name="app-management"></a>Apphantering  

#### <a name="company-portal-for-ios-supports-landscape-mode--6048329----"></a>Företagsportalen för iOS stödjer liggande läge<!--6048329  -->   
Användare kan nu registrera sina enheter, hitta appar och få IT-support med hjälp av valfri skärmorientering. Appen identifieras automatiskt och anpassar skärmen till stående eller liggande läge, såvida inte användaren låser skärmen i stående läge.  

#### <a name="script-support-for-macos-devices-public-preview---4280361----"></a>Skriptstöd för macOS-enheter (offentlig förhandsversion)<!-- 4280361  -->
Du kan lägga till och distribuera skript till macOS-enheter. Det här stödet utökar din möjlighet att konfigurera macOS-enheter utöver vad som är möjligt med hjälp av interna MDM-funktioner på macOS-enheter. Mer information finns i [Använda Shell-skript på macOS-enheter i Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## <a name="week-of-march-24-2020"></a>Den vecka som börjar 24 mars 2020

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Förbättrat användargränssnitt när vid skapande av enhetskonfigurationsprofiler på enheter med Android eller Android Enterprise<!-- 5841361 -->
När du skapar en profil för enheter med Android eller Android Enterprise kommer upplevelsen i administrationscentret för slutpunktshantering att uppdateras. Den här ändringen påverkar följande enhetskonfigurationsprofiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android-enhetsadministratör** eller **Android Enterprise** för plattformen):

- Enhetsbegränsningar: Android-enhetsadministratör
- Enhetsbegränsningar: Android Enterprise-enhetsägare
- Enhetsbegränsningar: Android Enterprise-arbetsprofil

Mer information om enhetsbegränsningar som du kan konfigurera finns i [Android-enhetsadministratör](../configuration/device-restrictions-android.md) och [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>Förbättrat användargränssnitt när du skapar konfigurationsprofiler på iOS/iPadOS- och macOS-enheter<!-- 5569002 5568997 -->
När du skapar en profil för iOS- eller macOS-enheter uppdateras funktionen i administrationscentret för slutpunktshantering. Den här ändringen påverkar följande enhetskonfigurationsprofiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** eller **macOS** för plattformen):

- Anpassad: iOS/iPadOS, macOS
- Enhetsfunktioner: iOS/iPadOS, macOS
- Enhetsbegränsningar: iOS/iPadOS, macOS
- Slutpunktsskydd: macOS
- Tillägg: macOS
- Inställningsfil: macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>Dölj från inställningen för användarkonfiguration i enhetsfunktionerna på macOS-enheter<!-- 6524869 -->

När du skapar en konfigurationsprofil för enhetsfunktioner på macOS-enheter finns nu den nya inställningen **Dölj från användarkonfiguration** (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **macOS** för plattformen > **Enhetsfunktioner** för profilen > **Inloggningsalternativ**).

Den här funktionen anger appens markering för dölj i listan **Användare och grupper** för inloggningsalternativ för appen på macOS-enheter. Befintliga profiler visar den här inställningen i listan som inte konfigurerad. Administratörer kan uppdatera befintliga profiler för att konfigurera den här inställningen.

När inställningen är **Dölj** markeras kryssrutan Dölj för appen och användarna kan inte ändra den. Den döljer också appen från användare när användare har loggat in på sina enheter.

> [!div class="mx-imgBorder"]
> ![Dölj appar på macOS-enheter när användare loggar in på enheten i Microsoft Intune och Endpoint Manager](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

Mer information om de inställningar som du kan konfigurera finns i [Funktionsinställningar för macOS-enheter](../configuration/macos-device-features-settings.md).

Den här funktionen gäller för:

- macOS

## <a name="week-of-march-16-2020-2003-service-release"></a>Veckan den 16 mars 2020 (2003 Service Release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>Uppdateringar av företagsportalen för macOS och iOS<!-- 5779439, 5780234  -->
Profilfönstret i företagsportalen för macOS och iOS har uppdaterats så att det inkluderar utloggningsknappen. Förbättringar av användargränssnittet har gjorts i profilfönstret i macOS-företagsportalen. Mer information om företagsportalen finns i [Så här konfigurerar du Microsoft Intune-företagsportalappen](../apps/company-portal-app.md).

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>Omdirigera webbklipp till Microsoft Edge på iOS-enheter<!-- 5455276   -->
Nyligen distribuerade webbklipp (fästa webbappar) på iOS-enheter öppnas i Microsoft Edge i stället för Intune Managed Browser om det behövs för att öppna i en skyddad webbläsare. Du måste omdirigera befintliga webbklipp för att se till att de öppnas i Microsoft Edge i stället för Managed Browser. Mer information finns i [Hantera webbåtkomst med hjälp av Microsoft Edge med Microsoft Intune](../apps/manage-microsoft-edge.md) och [Lägg till webbappar i Microsoft Intune](../apps/web-app.md).

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>Använd Intune-diagnostikverktyg med Microsoft Edge för Android<!-- 4735244  -->
Microsoft Edge för Android är nu integrerat med Intune-diagnostikverktyget. På samma sätt som med Microsoft Edge för iOS startar du Intune-diagnostikverktyget genom att ange ”about: intunehelp” i URL-fältet (adressrutan) för Microsoft Edge på enheten. Med det här verktyget får du detaljerade loggar. Användare kan vägledas till att samla in och skicka loggar till IT-avdelningen eller visa MAM-loggar för särskilda appar.

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>Uppdateringar av Intune-varumärkesanpassning och anpassning<!-- 5236032  -->
Vi har uppdaterat det Intune-fönster som hette ”Varumärkesanpassning och anpassning” med förbättringar såsom följande:

- Byter namn på fönstret till **Anpassning**.
- Förbättrar organiseringen och utformningen av inställningar.
- Förbättrar text och knappbeskrivningar för inställningar.

Du hittar de här inställningarna i Intune genom att gå till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), välja **Administration av klientorganisation** > **Anpassning**. Information om befintlig anpassning finns i [Så här konfigurerar du Microsoft Intune-företagsportalappen](../apps/company-portal-app.md).

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>Användarens personliga krypterade återställningsnyckel<!-- 6273943  -->
En ny Intune-funktion är tillgänglig som gör att användare kan hämta sin personliga krypterade **FileVault**-återställningsnyckel för Mac-enheter via Android-företagsportalappen eller via Android Intune-programmet. Det finns en länk i både företagsportalappen och Intune-programmet som öppnar en Chrome-webbläsare till webbföretagsportalen, där användaren kan se den **FileVault**-återställningsnyckel som krävs för åtkomst till Mac-enheterna. Mer information om kryptering finns i [Använda enhetskryptering med Intune](../protect/encrypt-devices.md).

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>Optimerad registrering av dedikerad enhet <!-- 6114580  -->
Vi optimerar registreringen för dedikerade Android Enterprise-enheter och gör det enklare för SCEP-certifikat som är kopplade till Wi-Fi att gälla för dedikerade enheter som registrerats före den 22 november 2019. För nya registreringar fortsätter Intune-appen att installeras, men slutanvändare kommer inte längre behöva utföra steget **Aktivera Intune-agent** under registreringen. Installationen sker automatiskt i bakgrunden och SCEP-certifikat som är kopplade till Wi-Fi kan distribueras och konfigureras utan åtgärder från slutanvändaren.  

Dessa ändringar kommer att lanseras i faser under mars månad samtidigt som Intune-tjänstens serverdel distribueras. Alla klienter kommer att ha det här nya beteendet i slutet av mars. Relaterad information finns i [Stöd för SCEP-certifikat i Android Enterprise-dedikerade enheter](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>Ny användarupplevelse när du skapar administrativa mallar på Windows-enheter<!--5096036 -->
Baserat på kundfeedback och vår förflyttning till den nya Azure-helskärmsupplevelsen har vi byggt om profilupplevelsen för administrativa mallar med en mappvy. Vi har inte gjort några ändringar i några inställningar eller befintliga profiler. Det innebär att befintliga profiler förblir desamma och kan användas i den nya vyn. Du kan fortfarande navigera bland alla inställningsalternativ genom att välja **Alla inställningar** och använda Sök. Trädvyn delas av dator- och användarkonfigurationer. Du hittar Windows-, Office- och Edge-inställningar i deras associerade mappar.  

Gäller för:
- Windows 10 och senare

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>VPN-profiler med IKEv2 VPN-anslutningar kan använda Alltid på med iOS/iPadOS-enheter<!-- 1947932   -->
På iOS/iPadOS-enheter kan du skapa en VPN-profil som använder en IKEv2-anslutning (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** för plattformen > **VPN** för profiltypen). Nu kan du uppdatera och konfigurera Alltid på med IKEv2. När IKEv2 VPN-profiler har konfigurerats ansluter de automatiskt och förblir anslutna (eller återansluter snabbt) till VPN-anslutningen. Den förblir ansluten även när du flyttar mellan nätverk eller startar om enheter.

På iOS/iPadOS är Alltid på för VPN begränsat till IKEv2-profiler.

Om du vill se de IKEv2-inställningar som du kan konfigurera går du till [Lägg till VPN-inställningar på iOS-enheter i Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Gäller för:
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>Ta bort paket och paketmatriser i OEMConfig-enhetskonfigurationsprofiler på Android Enterprise-enheter<!-- 5550355   -->
På Android Enterprise-enheter kan du uppdatera OEMConfig-profiler (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **Android Enterprise** för plattformen > **OEMConfig** för profiltypen). Användare kan nu ta bort paket och paketmatriser med hjälp av **Configuration Designer** i Intune.

Mer information om OEMConfig-profiler finns i [Använda och hantera Android Enterprise-enheter med OEMConfig i Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Gäller för:
- Android enterprise

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>Konfigurera Microsoft Azure AD SSO-apptillägget för enkel inloggning för iOS/iPadOS<!-- 5672534   -->
Microsoft Azure AD-teamet skapade en app för omdirigering med enkel inloggning som gör att användare med iOS/iPadOS 13.0+ kan få åtkomst till Microsofts appar och webbplatser med en enda inloggning. Alla appar som tidigare hade en asynkron autentisering med Microsoft Authenticator-appen fortsätter att få SSO med det nya SSO-tillägget. Med Azure AD SSO-tillägget för SSO-appen kan du konfigurera SSO-tillägget med apptillägget av typen enkel inloggning (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPad** för plattform > **Enhetsfunktioner** > för profiltyp **Apptillägg för enkel inloggning**).

Gäller för:
- iOS 13.0 och senare
- iPadOS 13.0 och senare

Mer information om iOS-apptillägg för enkel inloggning finns i [Apptillägg för enkel inloggning](../configuration/device-features-configure.md#single-sign-on-app-extension).

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>Inställningen Ändringar av inställningar för att lita på företagsappar tas bort från profiler för iOS-/iPadOS-enhetsbegränsningar<!-- 6225131   -->
På enheter med iOS/iPadOS skapar du en enhetsbegränsningsprofil (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **iOS/iPadOS** för plattform > **Enhetsbegränsningar** för profiltyp). Inställningen **Ändringar av inställningar för att lita på företagsappar** tas bort av Apple och tas bort från Intune. Om du för närvarande använder den här inställningen i en profil har den ingen effekt och tas bort från befintliga profiler. Den här inställningen tas även bort från all rapportering i Intune.

Gäller för:
- iOS/iPadOS

Om du vill se de inställningar som du kan begränsa går du till [Inställningar för iOS- och iPadOS-enheter för att tillåta eller begränsa funktioner](../configuration/device-restrictions-ios.md).

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>Felsökning: Väntande MAM-principmeddelande ändrades till informationsikon<!--6348954 -->
Meddelandeikonen för en väntande MAM-princip på felsökningsbladet har ändrats till en informationsikon.

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>Uppdatering av användargränssnittet vid konfiguration av efterlevnadsprinciper<!-- 3961639    -->

Vi har uppdaterat gränssnittet för att [skapa efterlevnadsprinciper](../protect/create-compliance-policy.md#create-the-policy) i Microsoft Endpoint Manager (**Enheter** > **Efterlevnadsprinciper** > **Principer** > **Skapa princip**). Vi har en ny användarupplevelse som inkluderar samma inställningar och information som du har använt tidigare. Den nya upplevelsen följer en guideliknande process för skapande av efterlevnadsprincip och innehåller den sida där du lägger till *Tilldelningar* för principen och en *Granska + Skapa*-sida, där du kan granska konfigurationen innan du skapar principen.

#### <a name="retire-noncompliant-devices---1827291---------"></a>Ta icke-kompatibla enheter ur bruk<!-- 1827291       -->
Vi har lagt till en ny åtgärd för icke-kompatibla enheter som du kan lägga till i en princip, för att [ta icke-kompatibel enhet ur bruk](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance).  Den nya åtgärden, **Ta icke-kompatibel enhet ur bruk**, innebär att alla företagsdata tas bort från enheten och att enheten inte kan hanteras av Intune.  Den här åtgärden körs när det konfigurerade värdet i dagar nås och vid det här tillfället blir enheten berättigad att tas ur bruk. Minsta värde är 30 dagar.  Explicit IT-administratörsgodkännande kommer att krävas för att dra tillbaka enheterna med hjälp av avsnittet *Dra tillbaka icke-kompatibla enheter*, där administratörer kan dra tillbaka alla berättigade enheter.

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>Stöd för WPA och WPA2 i iOS Enterprise Wi-Fi-profiler<!--6215273   -->
[Enterprise Wi-Fi-profiler för iOS](../configuration/wi-fi-settings-ios.md#enterprise-profiles) har nu stöd för fältet *Säkerhetstyp*. För *Säkerhetstyp* kan du välja antingen **WPA Enterprise** eller **WPA/WPA2 Enterprise**, och sedan ange ett val för *EAP-typ*.  (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** och välj **iOS/iPad** för *Platform* och **Wi-Fi** för *Profil*). 

De nya företagsalternativen är som de som har varit tillgängliga för en enkel Wi-Fi-profil för iOS.

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>Ny användarupplevelse för certifikat, e-post, VPN, Wi-Fi, och VPN-profiler<!-- 5615208   -->
Vi har uppdaterat [användarupplevelsen](../configuration/device-profile-create.md) i administrationscentret för slutpunktshantering (**Enheter** > **Konfigurationsprofiler** > **Skapa profil**) för skapande och ändring av följande profiltyper. Den nya upplevelsen visar samma inställningar som tidigare men använder en guideliknande upplevelse som inte kräver lika mycket horisontell rullning. Du behöver inte ändra befintliga konfigurationer med den nya upplevelsen.

- Härledd autentiseringsuppgift
- E-post
- PKCS-certifikat
- PKCS-importerat certifikat
- SCEP-certifikat
- Betrott certifikat
- VPN
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Enhetsregistrering

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>Konfigurera huruvida registrering är tillgänglig i Företagsportal för Android och iOS<!-- 4260128  -->
Du kan konfigurera huruvida enhetsregistrering i Företagsportal på enheter med Android eller iOS är tillgänglig med prompter, tillgänglig utan prompter eller inte tillgänglig för användare. Du hittar de här inställningarna i Intune genom att gå till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välja **Administration av klientorganisation** > **Anpassning** > **Redigera** > **Enhetsregistrering**.  

Stöd för inställningen för enhetsregistrering kräver att slutanvändarna har följande Företagsportal-versioner:
-    Företagsportal på iOS: version 4.4 eller senare
-    Företagsportal på Android: version 5.0.4715.0 eller senare

Mer information om befintlig anpassning av Företagsportal finns i [Så här konfigurerar du Microsoft Intune-företagsportalappen](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Ny Android-rapport på översiktssidan för Android-enheter<!-- 5435435   -->
Vi har lagt till en rapport i Microsoft Endpoint Manager-administratörskonsolen på översiktssidan för Android-enheter. Där visas hur många Android-enheter som har registrerats i varje lösning för enhetshantering. Det här diagrammet (liksom samma diagram som redan finns i Azure-konsolen) visar antal arbetsprofilenheter samt fullständigt hanterade, dedikerade och enhetsadministratörsregistrerade enheter. Om du vill se rapporten väljer du **Enheter** > **Android** > **Översikt**.

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-----"></a>Vägled användare från administratörshantering av Android-enheter till arbetsprofilhantering<!--5857738   -->
Vi släpper en ny efterlevnadsinställning för administratörsplattformen för Android-enheter. Med den här inställningen kan du göra en enhet icke-kompatibel om den hanteras med enhetsadministratör.

På dessa icke-kompatibla enheter kommer användare att på sidan **Uppdatera enhetsinställningar** se meddelandet **Flytta till konfiguration av enhetshantering**. Om de trycker på knappen **Lös** vägleds de genom:

1. Avregistrering från enhetsadministratörshantering
2. Registrering i arbetsprofilhantering
3. Lösa efterlevnadsproblem 
 
Google minskar stödet för enhetsadministration i nya versioner av Android för att kunna övergå till en modern, mer omfattande och säkrare enhetshantering med Android Enterprise.  Intune kan endast erbjuda fullt stöd för enhetsadministratörshanterade Android-enheter som kör Android 10 och senare till och med andra kvartalet 2020. Enhetsadministratörshanterade enheter (förutom Samsung) som kör Android 10 eller senare efter denna tidpunkt kommer inte längre att kunna hanteras fullt ut. Det innebär exempelvis att berörda enheter inte får de nya lösenordskraven.

Mer information om den här inställningen finns i [Flytta Android-enheter från enhetsadministratören till arbetsprofilhantering](../enrollment/android-move-device-admin-work-profile.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>Data Warehouse tillhandahåller nu MAC-adressen<!-- 6123680  -->
Intune Data Warehouse tillhandahåller MAC-adressen som en ny egenskap (`EthernetMacAddress`) i entiteten `device` så att administratörer kan korrelera mellan användaren och Mac-adressen. Den här egenskapen hjälper till att komma åt vissa användare och felsöka incidenter som inträffar i nätverket. Administratörer kan också använda den här egenskapen i [Power BI-rapporter](../developer/reports-proc-get-a-link-powerbi.md) för att skapa mer omfattande rapporter. Mer information finns i Intune Data Warehouse-[enheten](../developer/intune-data-warehouse-collections.md#devices).

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Ytterligare egenskaper för Data Warehouse-enhetsinventering<!-- 6125732  -->
Ytterligare egenskaper för enhetsinventering är tillgängliga via Intune Data Warehouse. Följande egenskaper är nu tillgängliga via betasamlingen [devices](../developer/reports-ref-devices.md#devices):
- `ethernetMacAddress` – den unika nätverksidentifieraren för den här enheten.
- `model` – enhetsmodellen.
- `office365Version` – den version av Office 365 som är installerad på enheten.
- `windowsOsEdition` – operativsystemversionen.

Följande egenskaper är nu tillgängliga via betasamlingen [devicepropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories):
- `physicalMemoryInBytes` – fysiskt minne i bytes.
- `totalStorageSpaceInBytes` – Total lagringskapacitet i bytes.

Mer information finns i [Microsoft Intune-API:et Data Warehouse](../developer/reports-nav-intune-data-warehouse.md).

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>Uppdatering av arbetsflöde för hjälp och support för att stödja ytterligare tjänster<!-- 5654170   -->
Vi har uppdaterat sidan Hjälp och support i administrationscentret för Microsoft Endpoint Manager där du nu [väljer den hanteringstyp som du använder](../fundamentals/get-support.md#options-to-access-help-and-support). Med den här ändringen kommer du att kunna välja bland följande hanteringstyper:

- Configuration Manager (inkluderar Desktop Analytics)
- Intune
- Samhantering

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Säkerhet

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>Använd en förhandsversion med principer fokuserade på säkerhetsadministratören som en del av slutpunktssäkerheten<!--6131401  -->
Som en offentlig förhandsversion har vi lagt till flera nya principgrupper under noden för slutpunktssäkerhet i administrationscentret för Microsoft Endpoint Management. Som säkerhetsadministratör kan du använda de här nya principerna för att fokusera på vissa aspekter av enhetssäkerhet för att hantera diskreta grupper av relaterade inställningar utan att den större delen av enhetskonfigurationsprinciper används.

Med undantag för den nya *Antivirusprincipen för Microsoft Defender Antivirus* (se nedan), är inställningarna i var och en av de här nya förhandsversionsprinciperna och -profilerna samma inställningar som du kanske redan konfigurerar via [enhetskonfigurationsprofiler](../configuration/device-profile-create.md) idag.

Följande är de nya principtyperna som är tillgängliga i förhandsversionen och deras tillgängliga profiltyper:

- **Antivirusprogram (förhandsversion)** :
  - macOS:
    - **Antivirus** – hantera [Principinställningar för Antivirus](../protect/antivirus-microsoft-defender-settings-macos.md) för macOS för att hantera [Microsoft Defender ATP för Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).

  - Windows 10 och senare:
    - **Microsoft Defender Antivirus** – hantera [Principinställningar för Antivirus](../protect/antivirus-microsoft-defender-settings-windows.md) för molnskydd, antivirusundantag, reparation, genomsökningsalternativ med mera.

      Antivirusprofilen för *Microsoft Defender Antivirus* är ett undantag som introducerar en ny instans av inställningar som finns som en del av en enhetsbegränsningsprofil. De här nya antivirusinställningarna:

        - Är samma inställningar som finns i enhetsbegränsningar, men har stöd för ett tredje alternativ för konfiguration som inte är tillgängligt när de har konfigurerats som en enhetsbegränsning.
        - Gäller för enheter som är samhanterade med Configuration Manager när [skjutreglaget för arbetsbelastning](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) för samhantering av Endpoint Protection har angetts till Intune.

     Planerar att använda den nya *Antivirus* > *Microsoft Defender Antivirus*-profilen i stället för att konfigurera dem via en enhetsbegränsningsprofil.

  - **Windows-säkerhetsupplevelse** – Hantera Windows-säkerhetsinställningar som slutanvändare kan visa i Microsoft Defender Security Center och vilka meddelanden de får. De här inställningarna är oförändrade från de som är tillgängliga som en Endpoint Protection-profil för enhetskonfiguration.

- **Diskkryptering (förhandsversion)** :
  - macOS:
    - **FileVault**
  - Windows 10 och senare:
    - **BitLocker**
- **Brandvägg (förhandsversion)** :
  - macOS:
    - **macOS-brandvägg**
  - Windows 10 och senare:
    - **Microsoft Defender-brandväggen**
- **Slutpunktsidentifiering och svar (förhandsgranskning)** :
  - Windows 10 och senare: -**Windows 10 Intune**
- **Minskning av attackytan (förhandsversion)** :
  - Windows 10 och senare:
    - **App- och webbläsarisolering**
    - **Webbskydd**
    - **Programregleringstyp**
    - **Regler för att minska attackytan**
    - **Enhetskontroll**
    - **Sårbarhetsskydd**
- **Kontoskydd (förhandsversion)** :
  - Windows 10 och senare:
    - **Kontoskydd**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>Den vecka som börjar 9 mars 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>Konfigurera leveransoptimeringsagent vid nedladdning av Win32-appinnehåll<!-- 5410945 -->

Du kan konfigurera att leveransoptimeringsagenten laddar ned Win32-appinnehåll, antingen i bakgrunds- eller förgrundsläge baserat på tilldelning. För befintliga Win32-appar fortsätter innehållet att laddas ned i bakgrundsläge. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Appar** > **Alla appar** > *Win32-appen* > **Egenskaper**. Välj **Redigera** bredvid **Tilldelningar**.  Redigera tilldelningen genom att välja **Inkludera** under **Läge** i avsnittet **Krävs**.  Du hittar den nya inställningen i avsnittet **Appinställningar**. Mer information om leveransoptimering finns i [Win32-apphantering – Leveransoptimering](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>Ändra primär användare för Windows-enheter<!-- 3794742   -->
Du kan ändra den primära användaren för Windows-hybridanslutna och Azure AD-anslutna enheter. Om du vill göra det går du till **Intune** > - **Enheter** > **Alla enheter** > väljer en enhet > **Egenskaper** > **Primär användare**. Mer information finns i [Ändra en enhets primära användare](../remote-actions/find-primary-user.md#change-a-devices-primary-user).

En ny RBAC-behörighet (Hanterade enheter/ange primär användare) har också skapats för den här uppgiften. Behörigheten har lagts till i inbyggda roller som supportavdelning, skoladministratör och slutpunktssäkerhetshanterare.

Den här funktionen distribueras till kunder globalt som en förhandsversion. Du bör se funktionen inom de närmaste veckorna.


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>Den vecka som börjar 2 mars 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Ansluta Microsoft Endpoint Manager-klientorganisation: Enhetssynkronisering och enhetsåtgärder<!-- 6317104, CM3555758-->
Microsoft Endpoint Manager sammanfogar Configuration Manager och Intune i en enda konsol. Från och med den tekniska förhandsversionen av Configuration Manager version 2002.2 kan du ladda upp dina Configuration Manager-enheter till molntjänsten och vidta åtgärder i administrationscentret. Mer information finns i [Funktioner i den tekniska förhandsversionen av Configuration Manager version 2002.2](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach).

Läs artikeln om [den tekniska förhandsversionen av Configuration Manager](https://docs.microsoft.com/configmgr/core/get-started/technical-preview) innan du installerar uppdateringen. I artikeln beskrivs de allmänna kraven och begränsningarna för att använda en teknisk förhandsversion, hur du uppdaterar mellan versioner och hur du ger feedback.

#### <a name="bulk-remote-actions--4576882--"></a>Massfjärråtgärder<!--4576882-->
Nu kan du utfärda masskommandon för följande fjärråtgärder: starta om, byt namn på, autopilot-återställning, rensning och borttagning. Om du vill se de nya massåtgärderna går du till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **Alla enheter** > **Massåtgärder**.

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>Listan Alla enheter har förbättrad sökning, sortering och filtrering<!--6179023-->
Prestanda, sökning, sortering och filtrering har förbättrats för listan Alla enheter. Mer information finns i [detta supporttips](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946).  

### <a name="app-management"></a>Apphantering  
####  <a name="improved-sign-in-experience-in-company-portal-for-android"></a>Förbättrad inloggningsupplevelse i Företagsportal för Android    
Vi har uppdaterat layouten för flera inloggningsskärmar i företagsportalappen för Android så att upplevelsen blir modernare, enklare och tydligare för användare. En titt på förbättringarna finns i [Nyheter i användargränssnittet för appen](https://docs.microsoft.com/mem/intune/fundamentals/whats-new-app-ui).

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>Den vecka som börjar den 24 februari 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>Förbättringar av användarupplevelsen i företagsportalen för macOS<!-- 5568987 -->
Vi har förbättrat registreringsupplevelsen för macOS-enheter och företagsportalappen för Mac. Du kommer att se följande förbättringar:
- En bättre Microsoft **AutoUpdate**-upplevelse under registreringen som ser till att användarna har den senaste versionen av företagsportalen.
- En bättre kompatibilitetskontroll under registreringen.
- Stöd för kopierade incident-ID:n så att användarna snabbare kan skicka fel från sina enheter till företagets supportteam.

Mer information om registrering och företagsportalappen för Mac finns i [Registrera din macOS-enhet med hjälp av företagsportalappen](../user-help/enroll-your-device-in-intune-macos-cp.md).

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>Appskyddspolicyerna för Better Mobile har nu stöd för iOS och iPadOS<!-- 6224512  -->

I oktober 2019 utökades appskyddspolicyerna i Intune med möjligheten att använda data från Microsoft Threat Defense-partner. Den här uppdateringen gör att du kan använda en appskyddspolicy till att blockera eller selektivt rensa användarnas företagsdata baserat på hälsotillståndet för enheter som använder Better Mobile i iOS och iPadOS.  Mer information finns i [Skapa en Mobile Threat Defense-appskyddsprincip med Intune](../protect/mtd-app-protection-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>Nu kan du exportera från listan Alla enheter i zippat CSV-format<!--6343117-->
Exporter från sidan **Enheter** > **Alla enheter** är nu i zippat CSV-format.


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>Den vecka som börjar den 17 februari 2020 (tjänstversionen 2002)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>Appen Microsoft Defender Avancerat skydd (ATP) för macOS<!-- 5424618 -->
Intune tillhandahåller ett enkelt sätt att distribuera appen Microsoft Defender Avancerat skydd (ATP) för macOS till hanterade Mac-enheter. Mer information finns i [Add Microsoft Defender ATP to macOS devices using Microsoft Intune](../apps/apps-advanced-threat-protection-macos.md) (Lägga till Microsoft Defender ATP i macOS-enheter med Microsoft Intune) och [Microsoft Defender Advanced Threat Protection for Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (Microsoft Defender Avancerat skydd för Mac).  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>Aktivera nätverksåtkomstkontroll med Cisco AnyConnect VPN på iOS-enheter<!-- 4860111  -->
På iOS-enheter kan du skapa en VPN-profil och använda olika anslutningstyper, inklusive Cisco AnyConnect (**Enhetskonfiguration** > **Profiler** > **Skapa profil** > **iOS** som plattform > **VPN** som profiltyp > **Cisco AnyConnect** som anslutningstyp).

Du kan aktivera nätverksåtkomstkontroll med Cisco AnyConnect. Gör så här för att använda funktionen:

1. I [Cisco Identity Services Engine Administrator Guide](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html) använder du anvisningarna i **Configuring Microsoft Intune as an MDM Server** (Konfigurera Microsoft Intune som en MDM-server) för att konfigurera Cisco Identity Services Engine (ISE) i Azure.
2. I enhetskonfigurationsprofilen för Intune väljer du inställningen **Aktivera nätverksåtkomstkontroll**.

Om du vill se alla tillgängliga VPN-inställningar går du till [Konfigurera VPN-inställningar på iOS-enheter](../configuration/vpn-settings-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Enhetsregistrering

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Serienummer på sidan för Apple MDM-pushcertifikat<!--5947765  -->
Nu visas serienumret på sidan för Apple MDM-pushcertifikat. Serienumret behövs för att få åtkomst till Apple MDM-pushcertifikatet om åtkomsten till det Apple-ID som skapade certifikatet skulle förloras. Om du vill visa serienumret går du till **Devices (Enheter)**  > **iOS** > **iOS enrollment (iOS-registrering)**  > **Apple MDM Push certificate (Apple MDM-pushcertifikat)** .

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>Nya alternativ för uppdateringsschemat för att skicka OS-uppdateringar till registrerade iOS/iPadOS-enheter<!--5879689  -->
Du kan använda följande alternativ när du schemalägger operativsystemsuppdateringar för iOS/iPadOS-enheter. Dessa alternativ gäller för enheter som använde registreringstypen Apple Business Manager eller Apple School Manager.
- Uppdatera vid nästa incheckning
- Uppdatera under schemalagd tid
- Uppdatera utanför schemalagd tid

För de två sista alternativen kan du skapa flera tidsperioder.

Om du vill se de nya alternativen går du till MEM > **Devices (Enheter)**  > **iOS** > **Update policies for iOS/iPadOS (Uppdateringsprinciper för iOS/iPadOS)**  > **Create profile (Skapa profil)** .

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>Välja vilka iOS/iPadOS-uppdateringar som ska skickas till registrerade enheter<!--5879689  -->
Du kan välja en specifik iOS/iPadOS-uppdatering (med undantag för den senaste uppdateringen) som ska skickas till enheter som har registrerats med hjälp av antingen Apple Business Manager eller Apple School Manager. För dessa enheter måste en enhetskonfigurationsprincip anges för att fördröja programuppdateringens synlighet ett antal dagar. Om du vill se den här funktionen går du till MEM > **Devices (Enheter)**  > **iOS** > **Update policies for iOS/iPadOS (Uppdateringsprinciper för iOS/iPadOS)**  > **Create profile (Skapa profil)** .



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Enhetssäkerhet

#### <a name="improved-intune-reporting-experience---3791418-----"></a>Förbättrad rapporteringsupplevelse i Intune<!-- 3791418   -->
Intune har nu en förbättrad rapporteringsupplevelse, inklusive nya rapporttyper, bättre rapportorganisation, mer fokuserade vyer, förbättrade rapportfunktioner samt mer konsekventa och tidsrelevanta data. Rapporteringsupplevelsen kommer att flyttas från allmänt tillgänglig förhandsversion till GA (allmän tillgänglighet). Dessutom tillhandahåller GA-versionen lokaliseringsstöd, felkorrigeringar, designförbättringar och aggregerade enhetsefterlevnadsdata på paneler i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

De nya rapporttyperna fokuserar på följande information:

- **Drift** – tillhandahåller färska poster med fokus på driftproblem. 
- **Organisation** – innehåller en bred sammanfattning av det övergripande läget.
- **Historisk** – visar mönster och trender under en viss tidsperiod.
- **Specialist** – låter dig använda rådata för att skapa dina egna anpassade rapporter.

Den första uppsättningen nya rapporter fokuserar på enhetsefterlevnad. Mer information finns i [Blogg – Rapporteringsramverk i Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) och [Intune-rapporter](reports.md).

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>Platsen för säkerhetsbaslinjer i användargränssnittet har konsoliderats<!-- 6177074   -->
Vi har konsoliderat sökvägarna till [säkerhetsbaslinjer](../protect/security-baselines.md) i administrationscentret för Microsoft Endpoint Manager genom att ta bort *Säkerhetsbaslinjer* från flera platser i användargränssnittet. Nu använder du följande sökväg för att nå säkerhetsbaslinjer:  **Slutpunktssäkerhet** > **Säkerhetsbaslinjer**.

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>Utökat stöd för importerade PKCS-certifikat<!-- 6044197  -->
Vi har utökat stödet för användning av [importerade PKCS-certifikat](../protect/certificates-imported-pfx-configure.md#supported-platforms) för att stödja *fullständigt hanterade Android Enterprise-enheter*. Normalt används import av PFX-certifikat för S/MIME-krypteringsscenarier, där användaren måste ha krypteringscertifikat på alla sina enheter för att e-postkrypteringen ska kunna utföras.

Import av PFX-certifikat stöds för följande plattformar:

- Android – enhetsadministratör
- Android Enterprise – fullständigt hanterad
- Android Enterprise – arbetsprofil
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>Visa konfiguration av slutpunktssäkerhet för enheter<!-- 6206460  -->
Vi har ändrat namnet på det alternativ i administrationscentret för Microsoft Endpoint Manager som visar de [slutpunktssäkerhetsinställningar som gäller för en viss enhet](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device). Namnet på det här alternativet har ändrats till **Konfiguration av slutpunktssäkerhet** eftersom det visar tillämpliga säkerhetsbaslinjer och ytterligare principer som skapats utanför säkerhetsbaslinjerna. Tidigare hette det här alternativet *Säkerhetsbaslinjer*.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rollbaserad åtkomstkontroll

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Användargränssnittsändringar i Intune-roller kommer<!--5801612   -->
Användargränssnittet för [Microsoft Endpoint Manager-administrationscenter](https://go.microsoft.com/fwlink/?linkid=2109431) > **Administration av klientorganisation** > **Roller** har fått en mer användarvänlig och intuitiv design. De här funktionerna tillhandahåller samma inställningar och information som du använder nu, men de nya funktionerna använder en guideliknande process.

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>Den vecka som börjar den 17 februari 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="microsofts-new-office-app---5859926---"></a>Microsofts nya Office-app<!-- 5859926 -->
Microsofts nya Office-app är nu allmänt tillgänglig för hämtning och användning. Med Office-appen kan du arbeta i Word, Excel och PowerPoint från en enda app. Du kan använda en appskyddsprincip för appen för att skydda åtkomsten till data.

Mer information finns i [How to enable Intune app protection policies with the Office mobile preview app](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493) (Aktivera appskyddsprinciper i Intune med förhandsversionen av Office-appen).

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>Den vecka som börjar den 10 februari 2020

### <a name="windows-7-ends-extended-support--3042987---"></a>Utökad support för Windows 7 avslutas<!--3042987 -->
Utökad support för Windows 7 avslutades den 14 januari 2020. Inaktuella Intunes stöd för enheter som kör Windows 7 avslutas på samma gång. Teknisk hjälp och automatiska uppdateringar som hjälper till att skydda din dator är inte längre tillgängliga. Du bör uppgradera till Windows 10. Mer information finns i blogginlägget [Planera för förändring](https://aka.ms/Windows7_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Microsoft Edge version 77 och senare på Windows 10-enheter<!-- 5843584 -->
Intune stöder nu avinstallation av Microsoft Edge version 77 och senare på Windows 10-enheter. Mer information finns i [Lägga till Microsoft Edge för Windows 10 till Microsoft Intune](../apps/apps-windows-edge.md).

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>En skärm har tagits bort från registreringen av Android-arbetsprofiler i företagsportalen<!--6103987 -->
Skärmen **Vad händer nu?** har tagits bort från registreringsflödet för Android-arbetsprofiler i företagsportalen för att effektivisera användarupplevelsen. Gå till [Registrera med Android-arbetsprofilen](../user-help/enroll-device-android-work-profile.md) om du vill se det uppdaterade registreringsflödet för Android-arbetsprofiler.  

#### <a name="company-portal-app-improved-performance---6178652---"></a>Förbättrade prestanda för Företagsportal-appen<!-- 6178652 -->
Företagsportal-appen har uppdaterats för att ge stöd för förbättrade prestanda för enheter som använder ARM64-processorer, t.ex. Surface Pro X. Tidigare använde Företagsportal ett emulerat ARM32-läge. Nu kompileras Företagsportal-appen, i version 10.4.7080.0 och senare, internt för ARM64. Mer information om Företagsportal-appen finns i [Så här konfigurerar du Microsoft Intune-företagsportalsappen](../apps/company-portal-app.md).

<!-- ########################## -->
## <a name="week-of-january-27-2020"></a>Veckan som börjar den 27 januari 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="intune-support-for-additional-microsoft-edge-version-77-deployment-channel-for-macos---5983950----"></a>Intune-stöd för ytterligare en Microsoft Edge version 77-distributionskanal för macOS<!-- 5983950  -->
Microsoft Intune har nu stöd för ytterligare en **Stabil** distributionskanal för Microsoft Edge-appen för macOS. Kanalen **Stabil** är den rekommenderade kanalen för att brett distribuera Microsoft Edge i företagsmiljöer. Den uppdateras var sjätte vecka, och varje utgåva innehåller förbättringar från **beta**kanalen. Förutom kanalerna **Stabil** och **Beta** så stöder Intune en **Dev**-kanal. Den offentliga förhandsversionen tillhandahåller stabila kanaler och dev-kanaler för Microsoft Edge version 77 och senare för macOS. Automatiska uppdateringar av webbläsaren är aktiverade som standard. Mer information finns i [Lägga till Microsoft Edge till macOS-enheter med hjälp av Microsoft Intune](../apps/apps-edge-macos.md).

#### <a name="retirement-of-intune-managed-browser--5728447---"></a>Tillbakadragande av Microsoft Intune Managed Browser<!--5728447 -->
Intune Managed Browser kommer att dras tillbaka. Skydda din Intune-webbläsarupplevelse genom att använda Microsoft Edge. 

<!-- ########################## -->
## <a name="week-of-january-20-2020-2001-service-release"></a>Veckan den 20 juli 2020 (tjänstversionen 2001)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="user-experience-change-when-adding-apps-to-intune---4705829-----"></a>Användarupplevelsen ändras när appar läggs till i Intune<!-- 4705829   -->
Du ser en ny användarupplevelse när du lägger till appar via Intune. De här funktionerna tillhandahåller samma inställningar och information som du har använt tidigare, men de nya funktionerna följer en guideliknande process innan en app läggs till i Intune. Den här nya funktionen tillhandhåller också en granskningssida innan appen läggs till. Välj **Appar** > **Alla appar** > **Lägg till** i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Du hittar mer information i [Lägg till appar i Microsoft Intune](../apps/apps-add.md).

#### <a name="require-win32-apps-to-restart----5622282-----"></a>Kräv att Win32-appar startas om <!-- 5622282   -->
Du kan kräva att en Win32-app måste startas om efter det att den har installerats. Du kan också välja hur lång tid (respitperiod) det ska ta innan omstarten måste ske.

#### <a name="user-experience-change-when-configuring-apps-in-intune---4207990-----"></a>Användarupplevelsen ändras när appar konfigureras i Intune<!-- 4207990   -->
En ny användarupplevelse uppstår när du skapar appkonfigurationsprinciper i Intune. De här funktionerna tillhandahåller samma inställningar och information som du har använt tidigare, men de nya funktionerna följer en guideliknande process innan en policy läggs till i Intune. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Appar** > **Appkonfigurationsprinciper** > **Lägg till**. Mer information finns i [Appkonfigurationsprinciper för Microsoft Intune](../apps/app-configuration-policies-overview.md). 

#### <a name="intune-support-for-additional-microsoft-edge-for-windows-10-deployment-channel---5861774---"></a>Intune-stöd för ytterligare en distributionskanal för Microsoft Edge för Windows 10<!-- 5861774 -->
Microsoft Intune har nu stöd för ytterligare en **Stabil** distributionskanal för Microsoft Edge-appen (version 77 och senare) för Windows 10. Kanalen **Stabil** är den rekommenderade kanalen för att brett distribuera Microsoft Edge för Windows 10 i företagsmiljöer. Den här kanalen uppdateras var sjätte vecka, och varje utgåva innehåller förbättringar från **Beta**-kanalen. Förutom kanalerna **Stabil** och **Beta** så stöder Intune en **Dev**-kanal. Mer information finns i [Microsoft Edge för Windows 10 – konfigurera appinställningar](../apps/apps-windows-edge.md#configure-app-settings).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="improved-user-interface-experience-when-configuring-exchange-activesync-on-premises-connector-ui---5695492-----"></a>Förbättrad användargränssnittsupplevelse när användargränssnittet för den lokala Exchange ActiveSync-anslutningsappen konfigureras<!-- 5695492   -->
Vi har uppdaterat funktionen för att [konfigurera den lokala Exchange ActiveSync-anslutningsappen](../protect/exchange-connector-install.md). Den uppdaterade upplevelsen använder ett enda fönster för att konfigurera, redigera och sammanfatta information om dina lokala anslutningsappar.

#### <a name="add-automatic-proxy-settings-to-wi-fi-profiles-for-android-enterprise-work-profiles---4490822-----"></a>Lägg till automatiska proxyinställningar i Wi-Fi-profiler för Android Enterprise-arbetsprofiler<!-- 4490822   -->
Du kan skapa Wi-Fi-profiler på Android Enterprise-arbetsprofilenheter. När du väljer Wi-Fi-företagstypen kan du också ange den EAP-typ (Extensible Authentication Protocol) som används i ditt Wi-Fi-nätverk.

Nu när du väljer företagstyp kan du också ange automatiska proxyinställningar, inklusive en proxyserver-URL, som exempelvis `proxy.contoso.com`.

Om du vill se vilka aktuella Wi-Fi-inställningar som du kan konfigurera, så gå till [Lägga till Wi-Fi-inställningar för enheter som kör Android Enterprise och Android Kiosk i Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md#work-profile-only).

Gäller för:
- Android Enterprise-arbetsprofil

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Enhetsregistrering

#### <a name="block-android-enrollments-by-device-manufacturer--5197392----"></a>Blockera Android-registreringar efter enhetstillverkare<!--5197392  -->
Du kan blockera enheter från att registreras baserat på deras tillverkare. Denna funktion gäller för Android-enhetsadministratörs- och Android Enterprise-arbetsprofilsenheter. Om du vill se registreringsbegränsningar går du till [Administrationscenter för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **Registreringsbegränsningar**.

#### <a name="improvements-to-the-iosipados-create-enrollment-type-profile-ui---6055005---"></a>Förbättringar av iOS/iPad-gränssnittet för att skapa registreringstypsprofil<!-- 6055005 -->
För användarregistrering i iOS/iPad så har sidan **Skapa registreringstypsprofil** **Inställningar** anpassats för att förbättra processen att välja **Registreringstyp** samtidigt som du behåller samma funktioner. Om du vill se det nya användargränssnittet går du till sidan [Administrationscenter för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Enheter** > **iOS** > **iOS-registrering** > **Registreringstyper** > **Skapa profil** > **Inställningar**. Mer information finns i [Skapa en Användarregistreringsprofil i Intune](../enrollment/ios-user-enrollment.md#create-a-user-enrollment-profile-in-intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="new-information-in-device-details---4471759-5604099----"></a>Ny enhetsinformation<!-- 4471759 5604099  -->
Följande information finns nu på sidan **Översikt** för enheter:
- Minneskapacitet (mängden fysiskt minne på enheten)
- Minneskapacitet (mängden fysisk lagring på enheten) 
- CPU-arkitektur

#### <a name="ios-bypass-activation-lock-remote-action-renamed-to-disable-activation-lock---5904591----"></a>iOS-fjärråtgärden Kringå aktiveringslås har bytt namn till att Inaktivera aktiveringslås <!--5904591  -->
Fjärråtgärden **Kringå aktiveringslås** har bytt namn till **Inaktivera aktiveringslås**. Mer information finns i [Inaktivera iOS-aktiveringslås med Intune](../remote-actions/device-activation-lock-disable.md).

#### <a name="windows-10-feature-update-deployment-support-for-autopilot-devices---5948137-----"></a>Stöd för distribution av funktionsuppdateringar i Windows 10 för Autopilot-enheter<!-- 5948137   -->
Intune har nu stöd för registrerade Autopilot-enheter genom [distribution av funktionsuppdateringar i Windows 10](../protect/windows-update-for-business-configure.md#windows-10-feature-updates).

Policyer för funktionsuppdateringar för Windows 10 kan inte tillämpas samtidigt som Autopilot-välkomstprogrammet körs och tillämpas endast vid den första Windows Update-genomsökningen när en enhet har etablerats färdigt (detta tar vanligtvis en dag).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

#### <a name="windows-autopilot-deployment-reports-preview----3856172-----"></a>Windows Autopilot-distributionsrapporter (förhandsversion) <!-- 3856172   -->
En ny rapport innehåller information om varje enhet som distribueras via Windows Autopilot. Mer information finns i [distributionsrapporten för Autopilot](../enrollment/enrollment-autopilot.md#autopilot-deployments-report).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rollbaserad åtkomstkontroll

#### <a name="new-intune-built-in-role-endpoint-security-manager--4253397-----"></a>Ny inbyggd roll i Intune för slutpunktssäkerhetshantering<!--4253397   -->
En ny inbyggd roll i Intune är tillgänglig: slutpunktssäkerhetshantering. Den här nya rollen ger administratörer fullständig åtkomst till slutpunktshanterarnoden i Intune och läsåtkomst till andra områden. Rollen är en utökning av rollen ”Säkerhetsadministratör” från Azure AD. Om du för närvarande bara har globala administratörer som roller, behövs inga ändringar. Om du använder roller och du vill ha den granularitet som finns i Endpoint Security Manager, tilldelar du rollen när den är tillgänglig. Mer information om inbyggda roller finns i [Rollbaserad åtkomstkontroll](role-based-access-control.md).

<!-- ########################## -->
## <a name="week-of-january-6-2020"></a>Veckan som börjar den 6 januari 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="smime-support-for-microsoft-outlook-for-ios---2669398---"></a>S/MIME-stöd för Microsoft Outlook för iOS<!-- 2669398 -->
Intune stöder leverans av S/MIME-signering och -krypteringscertifikat som kan användas med Outlook för iOS på iOS-enheter. Mer information finns i avsnittet om [känslighetsetiketter och skydd i Outlook för iOS och Android](https://aka.ms/omsmime).

#### <a name="cache-win32-app-content-using-microsoft-connected-cache-server---6030314---"></a>Cachelagra Win32-appinnehåll med en Microsoft-ansluten cacheserver<!-- 6030314 -->
Du kan installera en Microsoft-ansluten cacheserver på dina Configuration Manager-distributionsplatser om du ska cachelagra Intune Win32-appinnehåll. Mer information finns i [Microsoft-ansluten cache i Configuration Manager – Support för Intune Win32-appar](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rollbaserad åtkomstkontroll

#### <a name="windows-10-administrative-templates-admx-profiles-now-support-scope-tags---5137390---"></a>Profiler för administrativa mallar för Windows 10 (ADMX) stöder nu omfångstaggar <!--5137390 -->
Nu kan du tilldela administrativa mallprofiler (ADMX) omfångstaggar. Det gör du genom att gå till **Intune** > **Enheter** > **Konfigurationsprofiler** > välja en profil för administrativa mallar i listan > **Egenskaper** > **Omfångstaggar**. Mer information om omfångstaggar finns i [Tilldela andra objekt omfångstaggar](../fundamentals/scope-tags.md#assign-scope-tags-to-other-objects).

<!-- ########################## -->
## <a name="week-of-december-30-2019"></a>Veckan som börjar med 30 december 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices---4851745---"></a>Hämta personlig återställningsnyckel från MEM-krypterade macOS-enheter<!-- 4851745 -->
Slutanvändarna kan hämta sin personliga återställningsnyckel (FileVault Key) med hjälp av iOS-företagsportalappen. Den enhet som har den personliga återställningsnyckeln måste registreras med Intune och krypteras med FileVault via Intune. Med hjälp av iOS-företagsportalappen kan en slutanvändare hämta sin personliga återställningsnyckel på sin krypterade macOS-enhet genom att klicka på **Hämta återställningsnyckel**. Du kan också hämta återställningsnyckeln från Intune genom att välja **Enheter** > *den krypterade och registrerade macOS-enheten* > **Hämta återställningsnyckel**. Mer information om FileVault finns i [FileVault-kryptering för macOS](../protect/encrypt-devices-filevault.md).

#### <a name="ios-and-ipados-user-licensed-vpp-apps---5619268---"></a>Användarlicenserade VPP-appar för iOS och iPadOS<!-- 5619268 -->
För användarregistrerade iOS- och iPadOS-enheter visas inte längre nyskapade enhetslicenserade VPP-program som tillgängliga för slutanvändare. Slutanvändare kommer dock fortfarande att se alla användarlicensierade VPP-appar inom företagsportalen. Mer information om VPP-appar finns i [Så här hanterar du iOS- och macOS-appar som köpts genom ett Apples volymköpsprogram med Microsoft Intune](../apps/vpp-apps-ios.md).

<!-- ########################## -->
## <a name="week-of-december-23-2019"></a>Veckan som börjar med 23 december 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="notice---windows-10-1703-rs2-will-be-moving-out-of-support----5026679---"></a>Meddelande – Windows 10 1703 (RS2) kommer att tas bort från supporten <!-- 5026679 -->
Från och med 9 oktober 2018 togs Windows 10 1703 (RS2) bort från Microsofts plattformssupport for Home-, Pro- och Pro for Workstations-versionerna. För Windows 10 Enterprise-och Education-versionerna togs Windows 10 1703 (RS2) bort från plattformssupporten den 8 oktober 2019. Från den 26 december 2019 kommer vi att uppdatera den lägsta versionen av Windows Företagsportal-programmet till Windows 10 1709 (RS3). Datorer som kör tidigare versioner än 1709 kommer inte längre att ta emot uppdaterade versioner för programmet från Microsoft Store. Vi har tidigare informerat om den här ändringen till kunder som hanterar äldre versioner av Windows 10 via meddelandecentret. Mer information finns i [faktabladet om Windows livscykel](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)

<!-- ########################## -->

## <a name="week-of-december-16-2019"></a>Veckan som börjar med 16 december 2019

### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="updates-to-administrative-templates-for-windows-10-devices----5941568---"></a>Uppdateringar till administrativa mallar för Windows 10-enheter <!-- 5941568 -->

Du kan använda ADMX-mallar i Microsoft Intune för att kontrollera och hantera inställningar för Microsoft Edge, Office och Windows. Administrativa mallar i Intune har gjort följande uppdateringar av principinställningen:

- Stöd har lagts till för Microsoft Edge-versionerna 78 och 79.
- Innehåller 2019 ADMX-filerna från den 11 november i [Administrativa mallfiler (ADMX/ADML) och Office-anpassnings verktyg för Office 365 ProPlus, Office 2019 och Office 2016](https://www.microsoft.com/download/details.aspx?id=49030).

Mer information om ADMX-mallar i Intune finns i [Använda Windows 10-mallar till att konfigurera grupprincipinställningar i Microsoft Intune](../configuration/administrative-templates-windows.md).

Gäller för:

- Windows 10 och senare

## <a name="week-of-december-9-2019-1912-service-release"></a>Veckan som börjar med den 9 december 2019 (1912 tjänstversion)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="migrating-to-microsoft-edge-for-managed-browsing-scenarios---5173762---"></a>Migrera till Microsoft Edge för scenarier med hanterade webbläsare<!-- 5173762 -->
Nu när vi närmar oss tillbakadragningen av Intune Managed Browser, har vi gjort ändringar i appskyddsprinciperna för att förenkla de steg som krävs för att flytta användare till Edge. Vi har uppdaterat alternativen i inställningen av appskyddsprincipen **Begränsa överföring av webbinnehåll till andra appar** till att vara något av följande:

- Alla appar
- Intune Managed Browser
- Microsoft Edge
- Ohanterad webbläsare 

När du väljer **Microsoft Edge** visas ett meddelande om villkorsstyrd åtkomst för användarna som informerar om att Microsoft Edge krävs för hanterad webbsökning. De uppmanas att ladda ned och logga in på Microsoft Edge med sina AAD-konton, om de inte redan har gjort det.  Detta motsvarar när du har riktat dina MAM-aktiverade appar med appens konfigurationsinställning `com.microsoft.intune.useEdge` inställd på **Sant**. Befintliga appskyddsprinciper som använde inställningen **Principhanterade webbläsare** har nu **Intune Managed Browser** valt och du upplever inte någon ändring av funktionerna. Det innebär att användarna kommer att se meddelanden om att använda Microsoft Edge om du har angett appkonfigurationsinställningen **useEdge** som **Sant**. Vi uppmuntrar alla kunder som använder scenarier med hanterad webbsökning till att uppdatera sina appskyddsprinciper med **Begränsa överföring av webbinnehåll till andra appar** att säkerställa att användarna ser rätt vägledning för övergången till Microsoft Edge, oavsett vilken app de öppnar länkarna från. 

#### <a name="configure-app-notification-content-for-organization-accounts---2576686----"></a>Konfigurera innehåll i appmeddelande för organisationskonton<!-- 2576686  -->
Med Intunes appskyddsprinciper (APP) på Android- och iOS-enheter kan du styra appens meddelandeinnehåll för organisationskonton. Du kan välja ett alternativ (tillåt, blockera organisationsdata eller blockerade) för att ange hur meddelanden för organisationskonton visas för den valda appen. Den här funktionen kräver stöd från program och är kanske inte tillgänglig för alla APP-aktiverade program. Outlook för iOS-version 4.15.0 (eller senare) och Outlook för Android 4.83.0 (eller senare) kommer att ha stöd för den här inställningen. Inställningen är tillgänglig i-konsolen, men funktionen börjar gälla efter 16 december 2019. Mer information om APP finns i [Vad är appskyddsprinciper?](../apps/app-protection-policy.md).

#### <a name="microsoft-app-icons-update--4677605----"></a>Uppdatering av Microsofts appikoner<!--4677605  -->
Ikonerna som används för Microsoft-appar i appens målfönster för appskyddsprinciper och appkonfigurationsprinciper har uppdaterats.

#### <a name="require-use-of-approved-keyboards-on-android--4761794----"></a>Kräv användning av godkända tangentbord på Android<!--4761794  -->
Som en del av en appskyddsprincip kan du ange inställningen [**Godkända tangentbord**](../apps/app-protection-policy-settings-android.md#data-protection) för att hantera vilka Android-tangentbord som kan användas med hanterade Android-appar. När en användare öppnar den hanterade appen och inte redan använder tangentbord som är godkänt för den appen, uppmanas de att byta till ett av de godkända tangentbord som redan har installerats på enheten. Vid behov visas en länk för att ladda ner ett godkänt tangentbord från Google Play Store, som användaren kan installera och konfigurera. Om användarens aktiva tangentbord inte är ett av de godkända tangentborden kan användaren bara redigera textfält i en hanterad app.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="updated-single-sign-on-experience-for-apps-and-websites-on-your-ios-ipados-and-macos-devices---4999578----"></a>Uppdaterad enkel inloggning för appar och webbplatser på iOS-, iPadOS- och macOS-enheter<!-- 4999578  -->
Intune har lagt till fler SSO-inställningar för iOS-, iPadOS-och macOS-enheter. Nu kan du konfigurera och omdirigera SSO-apptillägg som skrivits av din organisation eller av din identitetsleverantör. Använd de här inställningarna för att konfigurera en smidig och enkel inloggning till appar och webbplatser som använder moderna autentiseringsmetoder, till exempel OAuth och SAML2. 

De nya inställningarna utökar de tidigare inställningarna för SSO-apptillägg och Apples inbyggda Kerberos-tillägg (**Enheter** > **Enhetskonfiguration** > **Profiler** > **Skapa profil** > **iOS/iPad** eller **macOS** för plattformstyp > **Enhetsfunktioner** för profiltyp). 

Om du vill se en fullständig uppsättning inställningar för SSO-tillägg som du kan konfigurera går du till [SSO på iOS](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) och [SSO på macOS](../configuration/macos-device-features-settings.md#single-sign-on-app-extension).

Gäller för:

- iOS/iPadOS
- macOS

#### <a name="we-have-updated-two-device-restriction-settings-for-ios-and-ipados-devices-to-correct-their-behavior---5701352------"></a>Vi har uppdaterat två enhetsbegränsningsinställningar för iOS-och iPad-enheter för att åtgärda deras beteende<!-- 5701352    -->
För iOS-enheter kan du skapa enhetsbegränsningsprofiler som **tillåter trådlösa PKI-uppdateringar** och **blockerar USB-begränsat läge** (**Enheter** > **Enhetskonfiguration** > **Profiler** > **Skapa profil** > **iOS/iPad** för plattform > **Enhetsbegränsningar** för profiltyp). Före den här versionen var användargränssnittsinställningar och beskrivningar för följande inställningar felaktiga och de har nu korrigerats. Från och med den här versionen är inställningsbeteendet följande:

**Blockera trådlösa PKI-uppdateringar**: **Blockera** hindrar användarna från att ta emot programuppdateringar om inte enheten är ansluten till en dator. **Inte konfigurerad** (standard): tillåter att en enhet tar emot programuppdateringar utan att vara ansluten till en dator.
- Tidigare kunde den här inställningen konfigureras som: **Tillåt**, vilket lät användarna ta emot programuppdateringar utan att ansluta sina enheter till en dator.
**Tillåt USB-tillbehör när enheten är låst**: **Tillåt** låter USB-tillbehör utbyta data med en enhet som har varit låst i över en timme. **Inte konfigurerad** (standard) uppdaterar inte USB-begränsat läge på enheten och USB-tillbehören kommer att blockeras från att överföra data från enheten om den är låst i mer än en timme.
- Tidigare kunde den här inställningen konfigureras som: **Blockera** för att inaktivera USB-begränsat läge på övervakade enheter.

Mer information om den inställning som du kan konfigurera finns i [Inställningar för iOS- och IPadOS-enheter för att tillåta eller begränsa funktioner med Intune](../configuration/device-restrictions-ios.md).

Den här funktionen gäller för:

- iOS/iPadOS

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Enhetskonfigurationsprofiler för fast nätverk för macOS-enheter<!-- 3508686  -->
   > [!NOTE]
   > Den här funktionen är försenad, men kommer snart att lanseras.

#### <a name="block-users-from-configuring-certificate-credentials-in-the-managed-keystore-on-android-enterprise-device-owner-devices---3311998---"></a>Blockera användare från att konfigurera autentiseringsuppgifter för certifikat i det hanterade nyckellagret på Android Enterprise-enhetsägarenheter<!-- 3311998 -->
På Android Enterprise-enhetsägarenheter kan du konfigurera en ny inställning som blockerar användare från att konfigurera sina certifikatsuppgifter i det hanterade nyckellagret (**Enhetskonfiguration** > **Profiler** > **Skapa profil** > **Android Enterprise** för plattform > **Endast enhetens ägare > Enhetsbegränsningar** för profiltypen > **Användare och konton**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="protected-wipe-action-now-available--51150000---"></a>Åtgärden för skyddad rensning är nu tillgänglig<!--51150000 -->
Nu har du möjlighet att använda åtgärden Rensa enhet för att utföra en skyddad rensning av en enhet. Skyddade rensningar är desamma som standardrensningar, förutom att de inte kan kringgås genom att stänga av enheten. En skyddad rensning försöker återställa enheten tills den har lyckats. I vissa konfigurationer kan den här åtgärden medföra att enheten inte kan startas om. Mer information finns i [Dra tillbaka eller rensa enheter](../remote-actions/devices-wipe.md).

#### <a name="device-ethernet-mac-address-added-to-devices-overview-page--5562275---"></a>Enhetens Ethernet MAC-adress har lagts till på enhetens översiktssida<!--5562275 -->
Nu kan du se en enhets Ethernet MAC-adress på sidan med enhetsinformation (**Enheter** > **Alla enheter** > Välj en enhet > **Översikt**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Enhetssäkerhet

#### <a name="improved-experience-on-a-shared-device-when-device-based-conditional-access-policies-are-enabled---1734096----"></a>Förbättrad upplevelse på en delad enhet när enhetbaserade principer för villkorlig åtkomst är aktiverade<!-- 1734096  -->
Vi har förbättrat upplevelsen på en delad enhet med flera användare som är riktade till enhetsbaserade villkorliga åtkomstprinciper genom att kontrollera den senaste utvärderingen av kompatibilitet för användaren när principen tillämpas. Mer information finns i följande översiktsartiklar:
- [Azure-översikt för villkorsstyrd åtkomst](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Översikt över enhetskompatibilitet för Intune](../protect/device-compliance-get-started.md)

#### <a name="use-pkcs-certificate-profiles-to-provision-devices-with-certificates---2317124-2317130-2317139-2340517-2340528-2340529----"></a>Använd PKCS-certifikatsprofiler för att etablera enheter med certifikat<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529  -->
Du kan nu använda PKCS-certifikatprofiler för att utfärda certifikat till *enheter* som kör Android for Work, iOS/iPadOS och Windows, när de är kopplade till profiler som till exempel Wi-Fi och VPN. Tidigare har de tre plattformarna endast haft stöd för användarbaserade certifikat, med enhetsbaserad support som är begränsad till macOS.

> [!NOTE]
> PKCS-certifikatprofiler stöds inte med Wi-Fi-profiler. Använd i stället SCEP-certifikatsprofiler när du använder en [EAP-typ](../configuration/wi-fi-settings-windows.md#enterprise-profile).

Om du vill använda ett enhetsbaserat certifikat medan du [skapar en PKCS-certifikatfil](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile) för de plattformar som stöds ska du välja **Inställningar**. Du ser nu inställningen för **Certifikattyp**, som stöder alternativen för Enhet eller Användare.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

#### <a name="centralized-audit-logs--5603185-5697164---"></a>Centraliserade granskningsloggar<!--5603185, 5697164 -->
En ny centraliserad upplevelse av granskningsloggen samlar nu in granskningsloggar för alla kategorier på en sida. Du kan filtrera loggarna för att hämta de data du söker. Om du vill se granskningsloggarna går du till **Klientadministration** > **Granskningsloggar**. 

#### <a name="scope-tag-information-included-in-audit-log-activity-details--5763534---"></a>Information om omfångstaggar som ingår i granskningsloggens aktivitetsinformation<!--5763534 -->
Granskningsloggens aktivitetsinformation innehåller nu information om omfångstaggar (för Intune-objekt som stöder omfångstaggar). Mer information om gransknings loggar finns [Använda granskningsloggar för att spåra och övervaka händelser](monitor-audit-logs.md).

<!-- ########################## -->
## <a name="week-of-december-2-2019"></a>Veckan som börjar med 2 december 2019

#### <a name="new-microsoft-endpoint-configuration-manager-co-management-licensing--5027281--"></a>Ny licensiering av samhantering i Microsoft Endpoint Configuration Manager<!--5027281-->
Configuration Manager-kunder med Software Assurance kan få Intune-samhantering för Windows 10-datorer utan att behöva köpa ytterligare en Intune-licens för samhantering. Kunderna behöver inte längre tilldela enskilda Intune/EMS-licenser till sina slutanvändare för samhantering av Windows 10.
- Enheter som hanteras i Configuration Manager och registreras för samhantering har nästan samma rättigheter som fristående MDM-hanterade datorer i Intune. När du har återställt dem kan du dock inte etablera dem igen med hjälp av Autopilot.
- Windows 10-enheter som har registrerats i Intune med hjälp av andra metoder kräver fullständiga Intune-licenser.
- Enheter på andra plattformar kräver fortfarande fullständiga Intune-licenser.

Mer information finns i [Licensvillkor](https://www.microsoft.com/en-us/Licensing/product-licensing/products).

<!-- ########################## -->
## <a name="week-of-november-18-2019-1911-service-release"></a>Veckan den 18 november 2019 (1911 Service Release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering

#### <a name="ui-update-when-selectively-wiping-app-data---4102028---"></a>Uppdaterat gränssnitt för selektiv rensning av appdata<!-- 4102028 -->
Gränssnittet för att selektivt rensa appdata i Intune har uppdaterats. Gränssnittsändringarna omfattar:
- En förenklad upplevelse med hjälp av ett format i guidestil som komprimerats till ett enskilt blad.
- En uppdatering av skapandeflödet så att tilldelningar inkluderas.
- En sammanfattningssida för alla saker som anges vid visning av egenskaper, innan en ny princip skapas eller när en egenskap redigeras. Vid redigering av egenskaper visar sammanfattningen dessutom bara en lista över objekt från kategorin med de egenskaper som redigeras.

Mer information finns i [Hur du rensar endast företagsdata från Intune-hanterade appar](../apps/apps-selective-wipe.md).

#### <a name="ios-and-ipados-third-party-keyboard-support---4922950---"></a>Stöd för tangentbord från tredje part för iOS och iPad<!-- 4922950 -->
I mars 2019 informerade vi om att supporten för iOS-appens skyddsprincipinställning "tangentbord från tredje part" upphör. Funktionen återkommer till Intune med stöd för både iOS och iPad. Om du vill aktivera den här inställningen går du till fliken **Dataskydds** i en ny eller befintlig iOS/iPad-appskyddsprincip och hittar inställningen **Tredje parts tangentbord** under **Dataöverföring**.

Beteendet för den här inställningen skiljer sig något från föregående implementering. I appar med flera identiteter som använder SDK-version 12.0.16 och senare som omfattas av skyddsprinciper för appar där den här inställningen är konfigurerad som **Blockera** kan slutanvändare inte välja att använda tangentbord från tredje part i både organisationens och personliga konton. Appar som använder SDK-versioner 12.0.12 och tidigare kommer att fortsätta att följa det beteende som dokumenteras i blogginlägget [Känt problem: Tangentbord från tredje part blockeras inte i iOS för personliga konton](https://aka.ms/3rdparty_iOS_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Enhetskonfiguration

#### <a name="target-macos-user-groups-to-require-jamf-management---4061739----"></a>Välj att användargrupper med macOS ska kräva JAMF-hantering<!-- 4061739  --> 
Du kan rikta in specifika grupper av användare vars [macOS-enheter hanteras av JAMF](../protect/conditional-access-integrate-jamf.md). Denna inriktning låter dig använda JAMF-efterlevnadsintegreringen för en delmängd av macOS-enheter medan andra enheter hanteras av Intune. Om du redan använder JAMF-integreringen är omfattas alla användare av integreringen som standard.

#### <a name="new-exchange-activesync-settings-when-creating-an-email-device-configuration-profile-on-ios-devices---4892824-----"></a>Nya Exchange ActiveSync-inställningar när du skapar en profil för e-postenhetskonfiguration på iOS-enheter<!-- 4892824   --> 
På iOS/iPad-enheter kan du konfigurera e-postanslutningen i en enhetskonfigurationsprofil (**Enhetskonfiguration** > **Profiler** > **Skapa profil** > **iOS/iPad** för plattform > **E-post** för profiltyp). 

Det finns nya Exchange ActiveSync-inställningar, inklusive:
- **Exchange-data att synkronisera**: Välj vilka Exchange-tjänster som ska synkroniseras (eller blockera synkronisering) för kalender, kontakter, påminnelser, anteckningar och e-post.
- **Tillåt användare att ändra inställningar för synkronisering**: Tillåt (eller blockera) användare att ändra synkroniseringsinställningarna för dessa tjänster på sina enheter.  

Mer information om de här inställningarna finns i [E-postprofilinställningar för iOS-enheter i Intune](../configuration/email-settings-ios.md). 

Gäller för:

- iOS 13.0 och senare
- iPadOS 13.0 och senare

#### <a name="prevent-users-from-adding-personal-google-accounts-to-android-enterprise-fully-managed-and-dedicated-devices---5353228-----"></a>Hindra användare från att lägga till personliga Google-konton i fullständigt hanterade och dedikerade Android Enterprise-enheter<!-- 5353228   -->
På fullständigt hanterade och dedikerade Android Enterprise-enheter finns det en ny inställning som hindrar användare från att skapa personliga Google-konton (**Enhetskonfiguration** > **Profiler** > **Skapa profil** > **Android Enterprise** för plattform > **Endast enhetens ägare > Enhetsbegränsningar** för profiltypen > **Användar- och kontoinställningar** > **Personliga Google-konton**).

Om du vill se alla inställningar som du kan konfigurera går du till [Inställningar för Android Enterprise-enheter för att tillåta eller begränsa funktioner med Intune](../configuration/device-restrictions-android-for-work.md).

Gäller för:

- Fullständigt hanterade Android Enterprise-enheter
- Dedikerade Android Enterprise-enheter

#### <a name="server-side-logging-for-siri-commands-setting-is-removed-in-iosipados-device-restrictions-profile----5468501-----"></a>Loggning på serversidan för Siri-kommandon tas bort från enhetsbegränsningsprofilen för iOS/iPadOS <!-- 5468501   -->
På iOS- och iPad-enheter tas inställningen **Loggning på serversidan för Siri-kommandon** bort från administratörskonsolen för Microsoft Endpoint Manager (**Enhetskonfiguration** > **Profiler** > **Skapa profil** > **iOS/iPadOS** för plattform > **Enhetsbegränsningar** för profiltyp > **Inbyggda appar**). 

Den här inställningen har ingen påverkan på enheter. Om du vill ta bort inställningen från befintliga profiler öppnar du profilen, gör eventuella ändringar och sparar sedan profilen. Profilen uppdateras och inställningen tas bort från enheterna.

Om du vill se alla de inställningar som du kan konfigurera går du till [Inställningar för iOS- och IPadOS-enheter för att tillåta eller begränsa funktioner med Intune](../configuration/device-restrictions-ios.md).

Gäller för:

- iOS/iPadOS

#### <a name="windows-10-feature-updates-public-preview---2384877---"></a>Funktionsuppdateringar för Windows 10 (offentlig förhandsversion)<!-- 2384877 -->
Nu kan du distribuera [Windows 10-funktionsuppdateringar](../protect/windows-update-for-business-configure.md#windows-10-feature-updates) till Windows 10-enheter. Windows 10-funktionsuppdateringar är en ny programuppdateringsprincip som gör det möjligt att fastställa den version av Windows 10 som du vill installera på enheterna och sedan stanna på. Du kan använda den här nya principtypen tillsammans med dina befintliga Windows 10-uppdateringsringar.

Enheter som tar emot en princip för Windows 10-funktionsuppdateringar får den fastställda versionen av Windows installerad. Enheterna stannar sedan kvar på den fastställda versionen tills principen redigeras eller tas bort. Enheter med en senare version av Windows stannar kvar på sina respektive aktuella versioner. Enheter som stannar kvar på en fastställd version av Windows kan fortfarande installera kvalitets- och säkerhetsuppdateringar för den versionen via Windows 10-uppdateringsringarna.

Den här nya principtypen börjar distribueras till klientorganisationer nu i veckan. Om principen inte är tillgänglig för din klientorganisation än, kommer den att bli det inom kort.

#### <a name="add-and-change-key-information-in-plist-files-for-macos-applications---4736278---"></a>Lägga till och ändra nyckelinformation i PLIST-filer för macOS-program<!-- 4736278 -->
På macOS-enheter kan du nu skapa en enhetskonfigurationsprofil som laddar upp en fil med egenskapslistan (. plist) som är associerad med en app eller med enheten (**Enheter** > **Konfigurationsprofiler** > **Skapa profil** > **macOS** för plattform > **Inställningsfil** för profiltyp).

Endast vissa appar har stöd för hanterade inställningar och de här apparna kanske inte tillåter att du hanterar alla inställningar. Se till att ladda upp en fil med en egenskapslista som konfigurerar enhetskanalinställningarna och inte användarkanalinställningarna.

Mer information om den här funktionen finns i [Lägga till en fil med en egenskapslista i macOS-enheter med Microsoft Intune](../configuration/preference-file-settings-macos.md).

Gäller för:

- macOS-enheter som kör 10.7 och senare

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Enhetshantering

#### <a name="edit-device-name-value-for-autopilot-devices---2640074---"></a>Redigera enhetsnamnvärde för Autopilot-enheter<!-- 2640074 -->
Du kan redigera enhetsnamnsvärdet för Azure AD-anslutna Autopilot-enheter.  Mer information finns i [Redigera attribut för Autopilot-enheter](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

#### <a name="edit-group-tag-value-for-autopilot-devices---4816775-----"></a>Redigera grupptaggvärde för Autopilot-enheter<!-- 4816775   -->
Du kan redigera grupptaggvärdet för Autopilot-enheter. Mer information finns i [Redigera attribut för Autopilot-enheter](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Övervaka och felsöka

#### <a name="updated-support-experience---5012398---"></a>Uppdaterad supportupplevelse<!-- 5012398 -->

Från och med idag distribueras en uppdaterad och strömlinjeformad konsolupplevelse för att få [hjälp och support](get-support.md). Om den nya upplevelsen inte är tillgänglig för dig än, kommer den att bli det inom kort.

Vi har förbättrat sökning och feedback i konsolen för vanliga problem, samt det arbetsflöde som du använder för att kontakta supporten. När du öppnar ett supportärende kan du se beräkningar i realtid för när du kan förvänta dig ett telefonsamtal eller e-postsvar. Premier och Unified Support-kunder kan dessutom ange en allvarlighetsgrad för problemet för att få hjälp snabbare.

#### <a name="improved-intune-reporting-experience-public-preview----3791418---"></a>Förbättrad rapporterings upplevelse i Intune (offentlig förhandsversion) <!-- 3791418 -->
Intune har nu en förbättrad rapporteringsupplevelse, inklusive nya rapporttyper, bättre rapportorganisation, mer fokuserade vyer, förbättrade rapportfunktioner samt mer konsekventa och tidsrelevanta data. De nya rapporttyperna fokuserar på följande:

- **Drift** – tillhandahåller färska poster med fokus på driftproblem. 
- **Organisation** – innehåller en bred sammanfattning av det övergripande läget.
- **Historisk** – visar mönster och trender under en viss tidsperiod.
- **Specialist** – låter dig använda rådata för att skapa dina egna anpassade rapporter.

Den första uppsättningen nya rapporter fokuserar på enhetsefterlevnad. Mer information finns i [Blogg – Rapporteringsramverk i Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) och [Intune-rapporter](reports.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Rollbaserad åtkomstkontroll

#### <a name="duplicate-custom-or-built-in-roles----1081938-----"></a>Duplicera anpassade eller inbyggda roller <!-- 1081938   -->
Du kan nu kopiera de inbyggda och de anpassade rollerna. För mer information, se [Kopiera en roll](../fundamentals/create-custom-role.md#copy-a-role).

#### <a name="new-permissions-for-school-administrator-role----5621805----"></a>Nya behörigheter för skoladministratörsrollen <!-- 5621805  -->  
Två nya behörigheter, **Tilldela profil** och **Synkronisera enhet**, har lagts till i skoladministratörsrollen > **Behörigheter** > **Registreringsprogram**. Med behörigheten synkroniseraprofil kan gruppadministratörer synkronisera Windows Autopilot-enheter. Med behörigheten tilldela profil kan de ta bort användarinitierade Apple-registreringsprofiler. De har också behörighet att hantera tilldelningar av Autopilot-enheter och distributionsprofiler för Autopilot. En lista över alla behörigheter för skoladministratör/gruppadministratör finns i [Tilldela gruppadministratörer](https://docs.microsoft.com/intune-education/group-admin-delegate).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Säkerhet

#### <a name="bitlocker-key-rotation---2564951----"></a>BitLocker-nyckel-ID<!-- 2564951  -->
Du kan använda en enhetsåtgärd i Intune för att [fjärrrotera återställningsnycklar för BitLocker](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) för hanterade enheter som kör Windows-version 1909 eller senare. För att kunna rotera återställningsnycklar måste enheterna konfigureras för att stödja rotation av återställningsnycklar.  

#### <a name="updates-to-dedicated-device-enrollment-to-support-scep-device-certificate-deployment----5198878----"></a>Uppdateringar av dedikerad enhetsregistrering för att stödja distribution av SCEP-enhetscertifikat <!-- 5198878  -->
Intune har nu stöd för distribution av SCEP-enhetscertifikat till dedikerade Android Enterprise-enheter för att möjliggöra certifikatbaserad åtkomst till Wi-Fi-profiler. Microsoft Intune appen måste finnas på enheten för att distributionen ska fungera. Därför har vi uppdaterat registreringsupplevelsen för dedikerade Android Enterprise-enheter. Nya registreringar är fortfarande samma (med QR, NFC, Zero-Touch eller Device Identifier) men har nu ett steg som kräver att användare installerar Intune-appen. På befintliga enheter kommer appen att installeras på löpande basis.

#### <a name="intune-audit-logs-for-business-to-business-collaboration--5670211---"></a>Granskningsloggar i Intune för samarbete mellan företag<!--5670211 -->
Samarbete mellan företag (B2B) gör att du på ett säkert sätt kan dela ditt företags program och tjänster med gästanvändare från en annan organisation, samtidigt som du behåller kontrollen över dina egna företagsdata. Intune stöder nu granskningsloggar för B2B-gästanvändare. Till exempel, när gästanvändare gör ändringar kommer Intune att kunna fånga dessa data via granskningsloggar. Mer information finns i [Vad är gästanvändaråtkomst i Azure Active Directory B2B?](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)

<!-- ########################## -->
## <a name="week-of-november-11-2019"></a>Veckan som börjar den 11 november 2019  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Apphantering  

#### <a name="improved-macos-enrollment-experience-in-company-portal----5074349----"></a>Förbättrad macOS-registrering i företagsportalen <!-- 5074349  -->  
Företagsportalen för macOS-registrering har en enklare registreringsprocess som stämmer bättre överens med företagsportalen för iOS-registrering. Enhetsanvändarna ser nu följande:  

- Ett mer elegant användargränssnitt.  
- En förbättrad checklista för registrering.  
- Tydligare instruktioner för hur man registrerar sina enheter.  
- Förbättrade felsökningsalternativ.  

#### <a name="web-apps-launched-from-the-windows-company-portal-app---5030972---"></a>Webbappar som startas från Windows företagsportalapp<!-- 5030972 -->
Slutanvändare kan nu starta webbappar direkt från Windows företagsportalapp. Slutanvändare kan välja webbappen och sedan välja alternativet **Öppna i webbläsare**. Den publicerade webbadressen öppnas direkt i webbläsaren. Den här funktionen kommer att distribueras under nästa vecka. Mer information om hur du lägger till webbappar finns i [Lägga till webbappar i Microsoft Intune](../apps/web-app.md).  

#### <a name="new-assignment-type-column-in-company-portal-for-windows-10----5459950----"></a>Tilldelningstyp – ny kolumn i Företagsportal för Windows 10 <!-- 5459950  -->
Kolumnen Företagsportal > **Installerade appar** > **Tilldelningstyp** har bytt namn till **Krävs av din organisation**.  I denna kolumn visas värdet **Ja** eller **Nej** för att indikera om organisationen klassat en app som obligatorisk eller valfri. Förändringarna föranleddes av att många enhetsanvändare uttryckte förvirring kring apparnas natur. Dina användare hittar mer information om hur man installerar appar från företagsportalen i [Installera och dela appar på din enhet](../user-help/install-apps-cpapp-windows.md). Mer information om hur du konfigurerar företagsportalappen för dina användare finns i [Så här konfigurerar du Microsoft Intune-företagsportalappen](../apps/company-portal-app.md).  

<!-- ########################## -->
## <a name="week-of-november-4-2019"></a>Veckan som börjar den 4 november 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Enhetssäkerhet

#### <a name="security-baselines-are-supported-on-microsoft-azure-government---4062552---"></a>Microsoft Azure Government stöder säkerhetsbaslinjer<!-- 4062552 -->

Nu kan instanser av Intune som finns i *Microsoft Azure Government* använda [säkerhetsbaslinjer](../protect/security-baselines.md) för att skydda användare och enheter.

## <a name="whats-new-archive"></a>Nyhetsarkiv
Information om tidigare månader finns i [Nyhetsarkiv](whats-new-archive.md).

## <a name="notices"></a>Meddelanden

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


