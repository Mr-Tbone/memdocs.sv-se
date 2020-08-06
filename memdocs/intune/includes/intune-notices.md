---
title: inkludera fil
description: inkludera fil
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 79e2694cfd34f1db8bf11969506ec3d8cbc453d4
ms.sourcegitcommit: 8a9b85d1c879060ea541f7c8ad1ae34a4ed33ed0
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/31/2020
ms.locfileid: "87507658"
---
Dessa meddelanden innehåller viktig information som kan hjälpa dig att förbereda dig för framtida ändringar och funktioner i Intune.

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Microsoft Intunes support för Windows 10 Mobile upphör<!--3544938-->
Microsofts mainstream-support för Windows 10 Mobile upphörde i december 2019. Som vi har nämnt i den här supportinstruktionen kommer Windows 10 Mobile-användare inte längre att kunna ta emot nya säkerhetsuppdateringar, snabbkorrigeringar som inte är av säkerhetstyp, kostnadsfria supportalternativ eller onlineuppdateringar av tekniskt innehåll från Microsoft. Microsoft Intune kommer nu även att upphöra med all support för både företagsportalen för Windows 10 Mobile-appen och Windows 10 Mobile-operativsystemet den 10 augusti 2020.

#### <a name="how-does-this-affect-me"></a>Hur påverkar det här mig?
Om du har Windows 10 Mobile-enheter distribuerade i din organisation kan du mellan nu och den 10 augusti 2020 registrera nya enheter, lägga till eller ta bort principer och appar eller uppdatera eventuella hanteringsinställningar. Efter den 10 augusti kommer vi att stoppa nya registreringar och slutligen ta bort hanteringen av Windows 10 Mobile från Intune-användargränssnittet. Enheter kommer inte längre att checka in till Intune-tjänsten och vi kommer att ta bort enhets- och principdata.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Vad kan jag göra för att förbereda mig för den här ändringen?
Du kan kontrollera din Intune-rapportering för att se vilka enheter eller användare som kan påverkas. Gå till **Enheter** > **Alla enheter** och filtrera efter operativsystem. Du kan lägga till fler kolumner för att hjälpa till att identifiera vilka i din organisation som har enheter som kör Windows 10 Mobile. Begär att dina slutanvändare uppgraderar sina enheter eller slutar att använda enheterna för företagsåtkomst.


### <a name="end-of-support-for-legacy-pc-management"></a>Stöd för hantering av äldre datorer upphör

Stöd för hantering av äldre datorer upphör den 15 oktober 2020. Uppgradera dina enheter till Windows 10 och registrera dem igen som MDM-enheter (hanterade mobila enheter) så att de fortsätter att hanteras av Intune.

[Läs mer](https://go.microsoft.com/fwlink/?linkid=2107122)

### <a name="move-to-the-microsoft-endpoint-manager-admin-center-for-all-your-intune-management"></a>Flytta all Intune-administration till administrationscentret för Microsoft Endpoint Manager
I MC208118 som lanserades förra mars introducerade vi en ny enkel webbadress för all administration av Microsoft Endpoint Manager och Intune: [https://endpoint.microsoft.com](https://endpoint.microsoft.com). Microsoft Endpoint Manager är en enhetlig plattform som innehåller Microsoft Intune och Configuration Manager. **Från och med 1 augusti 2020** tar vi bort Intune-administrationen på [https://portal.azure.com](https://portal.azure.com) och rekommenderar att du i stället använder [https://endpoint.microsoft.com](https://endpoint.microsoft.com) för all slutpunktshantering. 


### <a name="decreasing-support-for-android-device-administrator--7371518--"></a>Minskat stöd för Android-enhetsadministratör<!--7371518-->
Funktionen Android-enhetsadministratör lanserades i Android 2.2 som ett sätt att hantera Android-enheter. Från Android 5 lanserades det mer moderna hanteringsramverket [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (för enheter som kan ansluta till Google Mobile Services). Google uppmuntrar till att användare byter från funktionen enhetsadministratör genom att minska hanteringsstödet i nya Android-versioner.

#### <a name="how-does-this-affect-me"></a>Hur påverkar det här mig?
Eftersom Google gör de här ändringarna kommer du inte längre att ha tillgång till lika många hanteringsfunktioner på berörda enheter med funktionen enhetsadministratör från det fjärde kvartalet 2020. 

> [!NOTE]
> Det här datumet angavs tidigare som tredje kvartalet 2020, men det har flyttats fram baserat på [den senaste informationen från Google](https://www.blog.google/products/android-enterprise/da-migration/).

##### <a name="device-types-that-will-be-impacted"></a>Enhetstyper som påverkas
De enheter som påverkas av det minskade stödet för funktionen enhetsadministratör är de som alla tre villkoren nedan gäller för:
- registrerad för enhetsadministratörshantering
- kör Android 10 eller senare
- inte är en Samsung-enhet.

Enheter påverkas inte om något av följande stämmer:
- inte registrerad för enhetsadministratörshantering
- kör en tidigare Android-version än Android 10.
- är en Samsung-enhet. Samsung KNOX-enheter kommer inte att påverkas av denna tidsram, eftersom utökad support tillhandahålls via Intunes integrering med KNOX-plattformen. Det här ger dig ytterligare tid att planera övergången från enhetsadministratörshantering för Samsung-enheter.

##### <a name="settings-that-will-be-impacted"></a>Inställningar som påverkas
[Googles minskade stöd för enhetsadministratörshantering](https://developers.google.com/android/work/device-admin-deprecation) hindrar dig att tillämpa följande inställningar på enheter som påverkas.

###### <a name="configuration-profile-device-restriction-settings"></a>Inställningar för enhetsbegränsningar i konfigurationsprofiler

- Blockera **Kamera**
- Ange **Minsta längd på lösenord**
- Ange **Antal felaktiga inloggningar innan enheten rensas** (gäller inte för enheter utan något inställt lösenord utan endast enheter med lösenord)
- Ange **Lösenordets giltighetstid (dagar)**
- Ange **Lösenordstyp som krävs**
- Ange **Förhindra återanvändning av tidigare lösenord**
- Blockera **Smart Lock och andra betrodda agenter**

###### <a name="compliance-policy-settings"></a>Inställningar för efterlevnadsprinciper

- Ange **Lösenordstyp som krävs**
- Ange **Minsta längd på lösenord**
- Ange **Antal dagar tills lösenordet går ut**
- Ange **Antal tidigare lösenord för att förhindra återanvändning**


![Skärmbild av sidan Android-efterlevnadspolicy](../fundamentals/media/notices/android-compliance-settings.png)

###### <a name="additional-impacts-based-on-android-os-version"></a>Ytterligare saker som påverkas baserat på Android OS-versionen

**Android 10**: För alla enhetsadministratörshanterade enheter (inklusive Samsung) som kör Android 10 och senare har Google begränsat möjligheten för hanteringsagenter som Företagsportal att komma åt information om enhetsidentifierare. Den här begränsningen påverkar följande Intune-funktioner när enheten uppdateras till Android 10 eller senare:
- Nätverksåtkomstkontroll för VPN fungerar inte längre
- När enheter identifieras som företagsägda med IMEI eller serienummer markeras de inte automatiskt som företagsägda
- IMEI och serienummer är inte längre synliga för IT-administratörer i Intune

**Android 11**: Vi testar för närvarande stödet för Android 11 i den senaste betaversionen för att se hur enhetsadministratörshanterade enheter påverkas.

#### <a name="user-experience-of-impacted-settings-on-impacted-devices"></a>Användarupplevelsen av aktuella inställningar på enheter som påverkas

Konfigurationsinställningar som påverkas:
- För redan registrerade enheter som redan har tillämpat inställningarna fortsätter de påverkade konfigurationsinställningarna att tillämpas.
- För nyregistrerade enheter, nyligen tilldelade inställningar och uppdaterade inställningar tillämpas inte de aktuella konfigurationsinställningarna (men alla andra konfigurationsinställningar tillämpas fortfarande).

Efterlevnadsinställningar som påverkas:
- För redan registrerade enheter som redan har tillämpat inställningarna visas fortfarande de efterlevnadsinställningar som påverkas som inkompatibla på sidan ”Uppdatera enhetsinställningar”. Enheten uppfyller inte efterlevnadskraven och lösenordskrav tillämpas fortfarande i appen Inställningar.
- För nyregistrerade enheter, nyligen tilldelade inställningar och uppdaterade inställningar visas de efterlevnadsinställningar som påverkas fortfarande som orsaker till inkompatibilitet på sidan ”Uppdatera enhetsinställningar” och enheten uppfyller inte efterlevnadskraven, men striktare lösenordskrav tillämpas inte i appen Inställningar.

#### <a name="cause-of-impact"></a>Orsak till påverkan 
Enheterna börjar påverkas under det fjärde kvartalet 2020. Då släpper vi även en uppdatering till appen Företagsportal som utökar API-inriktningen för Företagsportal från nivå 28 till nivå 29 ([enligt krav från Google](https://www.blog.google/products/android-enterprise/da-migration/)). 

Enhetsadministratörshanterade enheter från andra tillverkare än Samsung påverkas då såvida inte användaren utför båda de här åtgärderna:
- Uppdaterar till Android 10 eller senare.
- Uppdaterar appen Företagsportal till den version som är inriktad på API-nivå 29.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Vad kan jag göra för att förbereda mig för den här ändringen?
För att undvika de kommande funktionsbegränsningarna under fjärde kvartalet 2020 rekommenderar vi följande:
- **Nya registreringar**: Använd [Android Enterprise](../enrollment/connect-intune-android-enterprise.md)-hantering för nya enheter (där det är tillgängligt) och/eller [appskyddspolicyer](../apps/app-protection-policies.md). Undvik att använda enhetsadministratörshantering för nya enheter. 
- **Tidigare registrerade enheter**: Om en enhetsadministratörshanterad enhet kör Android 10 eller senare, eller om den uppdateras till Android 10 eller senare (särskilt om den inte är en Samsung-enhet), så kan du flytta den från enhetsadministratörshantering till [Android Enterprise](../enrollment/connect-intune-android-enterprise.md)-hantering och/eller [appskyddspolicyer](../apps/app-protection-policies.md). Du kan använda det smidiga flödet för att [flytta Android-enheter från enhetsadministratör till arbetsprofilhantering](../enrollment/android-move-device-admin-work-profile.md).

#### <a name="additional-information"></a>Ytterligare information
- [Flytta Android-enheter från enhetsadministratör till arbetsprofilhantering](../enrollment/android-move-device-admin-work-profile.md)
- [Konfigurera registrering av Android Enterprise-arbetsprofilenheter](../enrollment/android-work-profile-enroll.md)
- [Konfigurera registrering av dedikerade Android Enterprise-enheter](../enrollment/android-kiosk-enroll.md)
- [Konfigurera Intune-registrering av helt hanterade Android Enterprise-enheter](../enrollment/android-fully-managed-enroll.md)
- [Skapa och tilldela appskyddspolicyer](../apps/app-protection-policies.md)
- [Använda Intune i miljöer utan Google Mobile Services](../apps/manage-without-gms.md)
- [Förstå appskyddspolicyer och arbetsprofiler på Android Enterprise-enheter](../apps/android-deployment-scenarios-app-protection-work-profiles.md)
- [Googles blogg om det du behöver veta om indragningen av funktionen Enhetsadministratör](https://www.blog.google/products/android-enterprise/da-migration/)
- [Googles vägledning för migrering från enhetsadministratören till Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Googles dokumentation om indragna API:er för enhetsadministratörshantering](https://developers.google.com/android/work/device-admin-deprecation)


### <a name="plan-for-change-intune-enrollment-flow-update-for-apples-automated-device-enrollment-for-iosipados"></a>Planera för förändring: Uppdaterat registreringsflöde i Intune för Apples automatiska enhetsregistrering för iOS/iPadOS
I juli-versionen av Företagsportal ändrar vi registreringsflödet för iOS/iPad-enheter i Apples automatiska enhetsregistrering (tidigare kallat DEP). Ändringen av registreringsflödet gäller endast flödet ”Registrera med användartillhörighet”. Om du tidigare angav ”Nej” för ”Installera Företagsportal” i konfigurationen kunde användarna fortfarande installera appen Företagsportal från Store. Då utlöses en registrering där användaren skulle lägga till rätt serienummer. I den nya versionen av Företagsportal tar vi bort den här bekräftelseskärmen för serienummer. Skapa i stället en motsvarande appkonfigurationspolicy som tillämpas vid sidan av Företagsportal så att användarna kan registrera sig, eller ange ”Ja” för ”Installera Företagsportal” i konfigurationen. 
 - Mer information finns i inlägget [här](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-enrollment-flow-update-for-apple-s-automated-device/ba-p/1431629).
