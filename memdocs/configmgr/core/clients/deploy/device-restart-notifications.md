---
title: Meddelanden om omstart av enhet
titleSuffix: Configuration Manager
description: Starta om aviserings beteende för olika klient inställningar i Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b6d383b2d5904f4d31fff5f549127dc21c39f29
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713396"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Meddelanden om omstart av enhet i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

De meddelanden som en användare får för en väntande enhets omstart kan variera beroende på [dator inställningar för omstart](about-client-settings.md#computer-restart) och vilken version av Configuration Manager som används. Den här artikeln hjälper administratörer att avgöra vad användar upplevelsen är för att vänta på meddelanden om omstart av enheten.

>[!NOTE]
> - Den här artikeln fokuserar på klient inställningar som finns i Configuration Manager version 1902 och version 1906.


## <a name="deployment-types-for-restart-notifications"></a>Distributions typer för meddelanden om omstart

[Klient inställningarna för omstart av datorn](about-client-settings.md#computer-restart) ändrar användar upplevelsen för alla nödvändiga distributioner som kräver en omstart av följande typer:

- [Program](../../../apps/deploy-use/deploy-applications.md)
- [Aktivitetssekvens](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Program uppdatering](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Starta om meddelande typer

När en omstart krävs får slutanvändaren ett meddelande om den kommande omstarten. Det finns fyra allmänna aviseringar som användare kan ta emot:

**Popup-meddelande** som informerar dig om att en omstart krävs. Informationen i popup-meddelandet kan vara olika beroende på vilken version av Configuration Manager du kör. Den här typen av meddelande är inbyggd i Windows OS och du kan också se program vara från tredje part med den här typen av avisering.

![Popup-meddelande om väntande omstart](media/3555947-restart-toast.png)

Software Center-meddelande med alternativet vilo läge visar återstående tid innan en omstart tillämpas. Meddelandet kan variera beroende på din version av Configuration Manager.

![Väntar på att starta om Software Center-meddelanden med knappen vilo läge](media/3976435-snooze-restart-countdown.png)

Meddelande Center slutlig tids nedräkning som inte kan stängas av användaren. Knappen vilo läge är nedtonad.

![Meddelande om slutlig nedräkning i Software Center](media/3976435-final-restart-countdown.png)

Om användaren proaktivt installerar nödvändig program vara som behöver startas om innan tids gränsen inträffar visas ett annat meddelande. Följande meddelande visas när inställningen för användar upplevelsen tillåter meddelanden och du inte använder popup-meddelanden för distributionen. Mer information om hur du konfigurerar dessa inställningar finns i [Inställningar för distribution av **användar upplevelser** ](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) och [användar meddelanden för nödvändiga distributioner](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

![Meddelande om proaktivt installerad program vara](media/3976435-proactive-user-restart-notification.png)

- När du inte använder popup-meddelanden liknar dialog rutan för program vara som är markerad som **tillgänglig** samma som proaktivt installerad program vara.

  - För **tillgänglig** program vara har meddelandet ingen tids gräns för omstarten och användaren kan välja deras egna intervall för vilo läge. Mer information finns i [godkännande inställningar](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

    ![Program vara som marker ATS som "tillgänglig" har ingen tids gräns för omstart i meddelandet.](media/3555947-deployment-marked-available-restart.png)

## <a name="device-restart-notifications-in-version-1902"></a>Meddelanden om omstart av enhet i version 1902

<!--3555947-->
Användare ser ibland inte Windows popup-meddelanden om en omstart eller en nödvändig distribution. Sedan visas inte upplevelsen för att försätta påminnelsen i vilo läge. Det här beteendet kan leda till en låg användar upplevelse när klienten når en tids gräns.

Från och med version 1902, när program varu ändringar krävs eller distributioner behöver startas om, kan du välja att använda en mer påträngande dialog ruta.

I gruppen [dator omstart](about-client-settings.md#computer-restart) av klient inställningar aktiverar du följande alternativ: **när en distribution kräver en omstart visar du ett dialog fönster för användaren i stället för ett popup-meddelande**.  

Om du konfigurerar den här klient inställningen ändras användar upplevelsen för alla nödvändiga distributioner som kräver en omstart från popup-meddelanden:

![Popup-meddelande som startas om krävs](media/3555947-restart-toast-initial.png)  

Till dialog fönstret mer påträngande Software Center:

![Dialog ruta för att starta om datorn](media/3976435-proactive-user-restart-notification.png)

Om användaren inte startade om enheten efter installationen får de ett meddelande som en påminnelse. Den här tillfälliga påminnelsen kommer att visas för användaren baserat på klient inställningen: **Visa ett tillfälligt meddelande till användaren som anger intervallet innan användaren loggas ut eller datorn startas om (minuter)**. Den här inställningen är den övergripande tiden som användaren måste starta om datorn innan en omstart framtvingas.

- Tillfälligt meddelande när du använder popup-meddelanden:

  ![Popup-meddelande om väntande omstart](media/3555947-restart-toast.png)

- Tillfälligt meddelande när du använder Software Center-dialogrutan, inte popup:

  ![Väntar på att starta om Software Center-meddelanden med knappen vilo läge](media/3555947-1902-hide-notification.png)

Om användaren inte startar om efter det tillfälliga meddelandet kommer de att få den slutgiltiga nedräknings aviseringen att de inte kan stängas. Tiden för när det slutliga meddelandet visas baseras på klient inställningen: **Visa en dialog ruta som användaren inte kan stänga, vilket visar nedräknings intervallet innan användaren loggas ut eller datorn startas om (minuter)**. Om inställningen till exempel är 60 visas en timme innan en omstart framtvingas, det slutliga meddelandet visas för användaren:

![Meddelande om slutlig nedräkning i Software Center](media/3555947-1902-final-countdown.png)

Följande inställningar måste vara kortare i varaktighet än det kortaste [underhålls fönstret](../manage/collections/use-maintenance-windows.md) som tillämpas på datorn:

- **Visa ett tillfälligt meddelande till användaren som anger intervallet innan användaren loggas ut eller omstart av datorn (minuter)**
- **Visa en dialog ruta som användaren inte kan stänga, som visar nedräknings intervallet innan användaren loggas ut eller datorn startas om (minuter)**

> [!IMPORTANT]
> I Configuration Manager 1902, under vissa omständigheter, ersätter dialog rutan inte popup-meddelanden. Lös problemet genom att installera Samlad [uppdatering för Configuration Manager version 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="device-restart-notifications-starting-in-version-1906"></a>Meddelanden om omstart av enhet från version 1906
<!--3976435-->
Vissa administratörer föredrar regelbundna omstart-meddelanden och en kort tidsram för att tillåta att omstarter ska skjutas upp. Andra administratörer låter användare skjuta upp en omstart under längre tids perioder och vill att användarna ska meddelas om den väntande omstarten sällan. Configuration Manager version 1906 ger en administratör ytterligare kontroll över tiden och frekvensen för meddelanden om omstart. Följande objekt introducerades i 1906 för att ge administratören större kontroll:

- **Ange varaktighet för vilo läge för omstart av datorn (minuter) för** [omstart av datorn.](about-client-settings.md#computer-restart)
- Det maximala värdet för att **Visa ett tillfälligt meddelande till användaren som anger intervallet innan användaren loggas ut eller datorn startas om (minuter)** , ökad från 1440 minuter (24 timmar) till 20160 minuter (två veckor).
- Användaren ser ingen förlopps indikator i meddelandet om att den väntande omstarten är mindre än 24 timmar.

### <a name="notifications-when-required-software-is-installed-at-or-after-the-deadline"></a>Meddelanden när nödvändig program vara installeras vid eller efter tids gränsen

När nödvändig program vara installeras vid eller efter tids gränsen, kommer användarna att se aviseringar beroende på vilka klient inställningar du har valt.

Om inställningen **när en distribution kräver en omstart, visar du ett dialog fönster för användaren i stället för ett popup-meddelande** är inställt på:

- **Inga** popup-meddelanden används förrän det slutliga nedräknings meddelandet har nåtts.
- **Ja** – ett meddelande om Software Center visas.
  - Om omstarten är längre än 24 timmar visas en uppskattad start tid. Tiden för det här meddelandet baseras på inställningen: **Visa ett tillfälligt meddelande till användaren som anger intervallet innan användaren loggas ut eller datorn startas om (minuter)**.

     ![Tiden för omstart är längre än 24 timmar](media/3976435-notification-greater-than-24-hours.png)

  - Om omstarten är mindre än 24 timmar visas en förlopps indikator. Tiden för det här meddelandet baseras på inställningen: **Visa ett tillfälligt meddelande till användaren som anger intervallet innan användaren loggas ut eller omstart av datorn (minuter)**

     ![Tiden för omstart är mindre än 24 timmar](media/3976435-notification-less-than-24-hours.png)

Om användaren väljer knappen för **vilo läge** inträffar ett annat tillfälligt meddelande när vilo perioden har löpt ut, förutsatt att de inte har nått den slutliga nedräkningen ännu. Tids inställningen för nästa meddelande baseras på inställningen: **ange varaktighet för vilo läge för omstart av datorns meddelanden (timmar)**. Om användaren väljer **vilo läge** och intervallet för vilo läge är en timme, kommer användaren att meddelas igen om 60 minuter förutsatt att de inte har nått den slutgiltiga nedräkningen.

När den slutliga nedräkningen uppnås får användaren ett meddelande om att de inte kan stängas. Förlopps indikatorn är i rött och användaren kan inte trycka på **vilo läge**.

![Slut punkts meddelande i program varu Center i version 1906](media/3976435-1906-final-restart-countdown.png)

### <a name="the-user-proactively-installs-before-the-deadline"></a>Användaren installerar proaktivt före tids gränsen

Om användaren proaktivt installerar nödvändig program vara som behöver startas om innan tids gränsen inträffar visas ett annat meddelande. Mer information om hur du konfigurerar dessa inställningar finns i [Inställningar för distribution av **användar upplevelser** ](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) och [användar meddelanden för nödvändiga distributioner](../../../apps/deploy-use/deploy-applications.md#bkmk_notify). 

Följande meddelande visas när inställningen för användar upplevelsen tillåter meddelanden och du inte använder popup-meddelanden för distributionen:

![Meddelande om proaktivt installerad program vara](media/3976435-proactive-user-restart-notification.png)

När tids gränsen för program varan har nåtts [installeras meddelandena när den nödvändiga program varan installeras vid eller efter att tids gränsen](#notifications-when-required-software-is-installed-at-or-after-the-deadline) har använts.

## <a name="log-files"></a>Loggfiler

Använd filen **RebootCoordinator. log** och **SCNotify. log** för fel sökning av enhets omstarter. Du kan också behöva använda ytterligare klient [logg fil](../../plan-design/hierarchy/log-files.md) baserat på vilken typ av distribution som används.

## <a name="next-steps"></a>Nästa steg

- [Introduktion till program hantering](../../../apps/understand/introduction-to-application-management.md)
- [Introduktion till operativsystemdistribution](../../../osd/understand/introduction-to-operating-system-deployment.md)
- [Introduktion till hantering av programuppdateringar](../../../sum/understand/software-updates-introduction.md)
