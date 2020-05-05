---
title: inkludera fil
description: inkludera fil
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: fbf352c3bccfb17efc35e34a2a822b6bbbcc215d
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/28/2020
ms.locfileid: "82183064"
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


### <a name="decreasing-support-for-android-device-administrator--5857738--"></a>Minskat stöd för Android-enhetsadministratör<!--5857738-->
Android-enhetsadministratören (kallas ibland för ”äldre” Android-hantering och lanserades med Android 2.2) är ett sätt att hantera Android-enheter. Det finns dock en bättre hanteringsfunktion med [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (lanseras med Android 5.0). För att kunna flytta till en modern, mer omfattande och säkrare enhetshantering,minskar Google stödet för enhetsadministration i nya versioner av Android.

#### <a name="how-does-this-affect-me"></a>Hur påverkar det här mig?
På grund av dessa ändringar av Google kommer Intune-användare att påverkas på följande sätt:  
- Intune kommer bara att kunna erbjuda fullt stöd för enhetsadministratörshanterade Android-enheter som kör Android 10 och senare till och med andra kvartalet 2020. Enheter med Android 10 eller senare som hanteras av enhetsadministratörer efter denna tidpunkt kommer inte längre att kunna hanteras fullt ut. Det innebär exempelvis att berörda enheter inte får de nya lösenordskraven.
    - Samsung KNOX-enheter påverkas inte av denna tidsram, eftersom utökad support tillhandahålls via Intunes integrering med KNOX-plattformen. Detta ger dig mer tid att planera övergången från enhetsadministratörernas hantering.    
- Android-enheter som hanteras av en enhetsadministratör som blir kvar på tidigare versioner av Android än Android 10 påverkas inte och kan fortfarande hanteras av en enhetsadministratör.    
- För alla enheter med Android 10 och senare har Google begränsat möjligheten för hanteringsagenter för enhetsadministratören, t.ex. företagsportalen, att komma åt information om enhetsidentifierare. Den här begränsningen påverkar följande Intune-funktioner när enheten uppdateras till Android 10 eller senare:  
    - Nätverksåtkomstkontroll för VPN fungerar inte längre.   
    - Om enheter identifieras som företagsägda med IMEI eller serienummer markeras de inte automatiskt som företagsägda.  
    - IMEI och serienumret kommer inte längre att vara synligt för IT-administratörer i Intune. 
        > [!NOTE]
        > Detta påverkar endast enheter som hanteras av enhetsadministratören på Android 10 och senare och påverkar inte enheter som hanteras som Android Enterprise. 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Vad kan jag göra för att förbereda mig för den här ändringen?
För att undvika den minskade funktionaliteten i tredje kvartalet 2020, rekommenderar vi följande:
- Publicera inte nya enheter för hantering av enhetsadministratören.
- Om en enhet väntar på en Android 10-uppdatering kan du migrera den från enhetsadministratörshantering till Android Enterprise-hantering och/eller appskyddsprinciper.

#### <a name="additional-information"></a>Ytterligare information
- [Googles vägledning för migrering från enhetsadministratören till Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Googles dokumentation om tillbakadragningen av API:et för enhetsadministratören](https://developers.google.com/android/work/device-admin-deprecation)