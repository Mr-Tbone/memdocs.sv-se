---
title: Meddelanden om omstart av enhet
titleSuffix: Configuration Manager
description: Starta om aviserings beteende för olika klient inställningar i Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feb9f4206df65ee34228577a9e589ddd1be72870
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127263"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Meddelanden om omstart av enhet i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

De meddelanden som en användare får för en väntande omstart av enheten kan variera beroende på [klient inställningarna för datorn](#client-settings) och vilken version av Configuration Manager du använder. Den här artikeln hjälper dig att konfigurera användar upplevelsen för meddelanden om väntande omstart av enheten.

## <a name="deployment-types-for-restart-notifications"></a>Distributions typer för meddelanden om omstart

[Klient inställningarna för omstart av datorn](#client-settings) ändrar användar upplevelsen för alla nödvändiga distributioner som kräver en omstart av följande typer:

- [Program](../../../apps/deploy-use/deploy-applications.md)
- [Aktivitetssekvens](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Program uppdatering](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Starta om meddelande typer

När en enhet kräver en omstart, visar klienten ett meddelande till slutanvändaren om den kommande omstarten.

### <a name="toast-notification"></a>Popup-meddelande

Ett Windows popup-meddelande informerar användaren om att enheten måste startas om. Informationen i popup-meddelandet kan vara olika beroende på vilken version av Configuration Manager du kör. Den här typen av meddelande är inbyggd i Windows OS. Du kan också se program vara från tredje part med den här typen av avisering.

:::image type="content" source="media/3555947-restart-toast.png" alt-text="Popup-meddelande om väntande omstart":::

### <a name="software-center-notification-with-snooze"></a>Software Center-meddelande med vilo läge

I Software Center visas ett meddelande med ett alternativ för vilo läge och den tid som återstår innan enheten måste startas om. Meddelandet kan variera beroende på din version av Configuration Manager.

:::image type="content" source="media/3976435-snooze-restart-countdown.png" alt-text="Väntar på att starta om Software Center-meddelanden med knappen vilo läge":::

### <a name="software-center-final-countdown-notification"></a>Meddelande om slutlig nedräkning i Software Center

Software Center visar denna slutgiltiga nedräknings avisering som användaren inte kan stänga eller i vilo läge.

:::image type="content" source="media/3976435-final-restart-countdown.png" alt-text="Meddelande om slutlig nedräkning i Software Center":::

Från och med version 1906 ser användaren ingen förlopps indikator i meddelandet om att den väntande omstarten är mindre än 24 timmar.

### <a name="software-center-notification-before-deadline"></a>Software Center-meddelande före tids gräns

Om användaren proaktivt installerar nödvändig program vara före tids gränsen, och det krävs en omstart, visas ett annat meddelande. Följande meddelande visas när inställningen för användar upplevelsen tillåter meddelanden och du inte använder popup-meddelanden för distributionen. Mer information om hur du konfigurerar dessa inställningar finns i [Inställningar för distribution av **användar upplevelser** ](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) och [användar meddelanden för nödvändiga distributioner](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Meddelande om proaktivt installerad program vara":::

#### <a name="available-apps"></a>Tillgängliga appar

När du inte använder popup-meddelanden liknar dialog rutan för program vara som är markerad som **tillgänglig** samma som proaktivt installerad program vara. För **tillgänglig** program vara har meddelandet ingen tids gräns för omstarten och användaren kan välja deras egna intervall för vilo läge. Mer information finns i [godkännande inställningar](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

:::image type="content" source="media/3555947-deployment-marked-available-restart.png" alt-text="Den tillgängliga program varan har ingen tids gräns för omstart i meddelandet":::

### <a name="software-center-notification-of-required-restart"></a>Software Center-meddelande om nödvändig omstart

<!--3601213-->

Från och med version 2006 kan du konfigurera klient inställningar för att förhindra att enheter startar om automatiskt när en distribution kräver det. När en nödvändig distribution behöver enheten för att starta om, men du inaktiverar klient inställningen **Configuration Manager kan tvinga en enhet att starta om**, visas följande meddelande:

:::image type="content" source="media/3601213-restart-your-computer.png" alt-text="Software Center-meddelande för omstart av datorn":::

Om du försätter det här meddelandet i **vilo läge** visas det igen baserat på hur du konfigurerar frekvensen för meddelanden om påminnelser om omstart. Enheten startar inte om förrän du har valt **starta om** eller startar om Windows manuellt.

> [!NOTE]
> Som standard kan Configuration Manager fortfarande tvinga enheter att starta om.

## <a name="client-settings"></a>Klientinställningar

Om du vill styra klient omstarts beteendet konfigurerar du följande enhets klient inställningar i gruppen **omstart av dator** . Mer information finns i [så här konfigurerar du klient inställningar](configure-client-settings.md).

### <a name="configuration-manager-can-force-a-device-to-restart"></a>Configuration Manager kan tvinga en enhet att starta om

<!--3601213-->

Från och med version 2006 kan du konfigurera klient inställningar för att förhindra att enheter startar om automatiskt när en distribution kräver det. Configuration Manager aktiverar den här inställningen som standard.

> [!IMPORTANT]
> Den här klient inställningen gäller för alla program, program uppdateringar och paket distributioner till enheten. Tills en användare startar om enheten manuellt:
>
> - Program uppdateringar och app-revisioner kanske inte är helt installerade
> - Ytterligare program varu installationer kanske inte sker

När du inaktiverar den här inställningen kan du inte ange efter hur lång tid enheten ska startas om, eller så visas en slutgiltig nedräknings avisering.

> [!NOTE]
> För att dra full nytta av nya Configuration Manager funktioner kan du även uppdatera klienter till den senaste versionen när du har uppdaterat platsen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.

### <a name="specify-the-amount-of-time-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Ange efter hur lång tid en enhet har startats om (minuter)

Den här inställningen måste vara kortare i varaktighet än den kortaste underhålls perioden som tillämpas på datorn. Mer information om underhålls perioder finns i [använda underhålls](../manage/collections/use-maintenance-windows.md)perioder.

Standardvärdet är 90 minuter. Från och med version 1906 ökade det maximala värdet från 1440 minuter (24 timmar) till 20160 minuter (två veckor).

> [!NOTE]
> Den här inställningen **visar tidigare ett tillfälligt meddelande till användaren som anger intervallet innan användaren loggas ut eller datorn startas om (minuter)**.

### <a name="specify-the-amount-of-time-that-a-user-is-presented-a-final-countdown-notification-before-a-device-gets-restarted-minutes"></a>Ange hur lång tid det tar för en användare att presentera en slut för tids nedräkning innan en enhet startas om (minuter)

Den här inställningen måste vara kortare i varaktighet än den kortaste underhålls perioden som tillämpas på datorn. Mer information om underhålls perioder finns i [använda underhålls](../manage/collections/use-maintenance-windows.md)perioder.

Standardvärdet är 15 minuter.

> [!NOTE]
> Den här inställningen har tidigare rubriken **Visa en dialog ruta som användaren inte kan stänga, vilket visar nedräknings intervallet innan användaren loggas ut eller datorn startas om (minuter)**.

### <a name="specify-the-frequency-of-reminder-notifications-presented-to-the-user-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Ange frekvensen för påminnelse meddelanden som visas för användaren, efter tids gränsen, innan en enhet startas om (minuter)
<!--3976435-->
_Från och med version 1906_

Värdet för frekvens varaktigheten måste vara mindre än värdet för **Ange efter hur lång tid som en enhet har startats om (minuter)** minus värdet för **Ange hur lång tid en användare har fått en slutgiltig nedräknings avisering innan en enhet startas om (minuter)**. Annars fungerar inte påminnelse meddelandena.

Standardvärdet är 240 minuter.

> [!NOTE]
> Den här inställningen har tidigare rubriken **ange varaktighet för vilo läge för omstart av datorns meddelanden (minuter)**.

### <a name="when-a-deployment-requires-a-restart-show-a-dialog-window-to-the-user-instead-of-a-toast-notification"></a>När en distribution kräver en omstart visar du ett dialog fönster för användaren i stället för ett popup-meddelande
<!--3555947-->
Från och med version 1902 kan du konfigurera den här inställningen till **Ja** för att ändra användar upplevelsen till mer påträngande. Den här inställningen gäller för alla distributioner av program, aktivitetssekvenser och program uppdateringar. Mer information finns i [Planera för Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact).

> [!IMPORTANT]
> I Configuration Manager 1902, under vissa omständigheter, ersätter dialog rutan inte popup-meddelanden. Lös problemet genom att installera Samlad [uppdatering för Configuration Manager version 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="device-restart-notifications-version-1906"></a>Meddelanden om omstart av enhet (version 1906)
<!--3976435-->
Vissa kunder föredrar vanliga omstart-meddelanden och gör det möjligt för användarna att skjuta upp en kort tids period. Andra gör det möjligt för användare att skjuta upp en omstart under längre tids perioder och meddela användare om den väntande omstarten sällan. Från och med Configuration Manager version 1906 har du ytterligare kontroll över tidpunkten och frekvensen för att starta om aviseringar.

### <a name="install-required-software-at-or-after-the-deadline"></a>Installera nödvändig program vara vid eller efter tids gränsen

När nödvändig program vara installeras vid eller efter tids gränsen, kommer användarna att se aviseringar beroende på vilka klient inställningar du har valt.

Om inställningen **när en distribution kräver en omstart, visar du ett dialog fönster för användaren i stället för ett popup-meddelande** är inställt på:

- **Nej**: Windows visar popup-meddelanden tills distributionen når den slutgiltiga nedräknings aviseringen.

- **Ja**: Software Center visar ett meddelande:

  - Om omstarten är längre än 24 timmar visas en uppskattad start tid. Tiden för det här meddelandet baseras på inställningen: **Ange efter hur lång tid som ska gå innan enheten startas om (minuter)**.

    :::image type="content" source="media/3976435-notification-greater-than-24-hours.png" alt-text="Tiden för omstart är längre än 24 timmar":::

  - Om omstarten är mindre än 24 timmar visas en förlopps indikator. Tiden för det här meddelandet baseras på inställningen: **Ange efter hur lång tid som ska gå innan enheten startas om (minuter)**.

    :::image type="content" source="media/3976435-notification-less-than-24-hours.png" alt-text="Tiden för omstart är mindre än 24 timmar":::

Om användaren väljer **vilo läge**visas ett annat tillfälligt meddelande efter att vilo perioden har löpt ut. Det här beteendet förutsätter att det inte har nått den slutgiltiga nedräkningen ännu. Tids inställningen för nästa meddelande baseras på inställningen: **Ange frekvensen för påminnelse meddelanden som visas för användaren, efter deadline, innan en enhet startas om (minuter)**. Om användaren väljer **vilo läge**och intervallet för vilo läge är en timme, meddelar Software Center användaren igen om 60 minuter. Det här beteendet förutsätter att det inte har nått den slutgiltiga nedräkningen ännu.

När den når den slutgiltiga nedräkningen visar Software Center användaren ett meddelande om att de inte kan stängas. Förlopps indikatorn är i rött och användaren kan inte försätta den i **vilo läge** .

:::image type="content" source="media/3976435-1906-final-restart-countdown.png" alt-text="Slut punkts meddelande i program varu Center i version 1906":::

### <a name="proactively-install-required-software-before-the-deadline"></a>Installera nödvändig program vara före tids gränsen

Om användaren proaktivt installerar nödvändig program vara som behöver startas om före tids gränsen, ser de ett annat meddelande. Mer information om hur du konfigurerar dessa inställningar finns i [Inställningar för distribution av **användar upplevelser** ](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) och [användar meddelanden för nödvändiga distributioner](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

Följande meddelande visas när inställningen för användar upplevelsen tillåter meddelanden och du inte använder popup-meddelanden för distributionen:

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Meddelande om proaktivt installerad program vara":::

När distributionen når sin tids gräns följer Software Center beteendet för att [installera nödvändig program vara vid eller efter tids gränsen](#install-required-software-at-or-after-the-deadline).

## <a name="example-configurations"></a>Exempel på konfigurationer

I följande exempel beskrivs hur du konfigurerar klient inställningarna för att uppnå vissa beteenden.

### <a name="reminders-are-off"></a>Påminnelser är inaktiverade

| Inställning | Värde |
|---------|---------|
|Ange efter hur lång tid en enhet har startats om (minuter)|180|
|Ange hur lång tid det tar för en användare att presentera en slut för tids nedräkning innan en enhet startas om (minuter)|60|
|Ange frekvensen för påminnelse meddelanden som visas för användaren, efter tids gränsen, innan en enhet startas om (minuter)|240|
|När en distribution kräver en omstart visar du ett dialog fönster för användaren i stället för ett popup-meddelande|No|

Enheten kommer att startas om tre timmar (**180** minuter) efter distributionens tids gräns. En timme (**60** minuter) innan den startas om ser användaren en nedräkning som inte kan stängas eller försättas i vilo läge. Det första påminnelse meddelandet är inställt på att starta fyra timmar (**240** minuter) efter tids gränsen, vilket är efter omstarten. Det innebär att användaren inte ser några påminnelser.

### <a name="low-reminder-frequency"></a>Låg påminnelse frekvens

| Inställning | Värde |
|---------|---------|
|Ange efter hur lång tid en enhet har startats om (minuter)|7200|
|Ange hur lång tid det tar för en användare att presentera en slut för tids nedräkning innan en enhet startas om (minuter)|120|
|Ange frekvensen för påminnelse meddelanden som visas för användaren, efter tids gränsen, innan en enhet startas om (minuter)|900|
|När en distribution kräver en omstart visar du ett dialog fönster för användaren i stället för ett popup-meddelande|Ja|

Enheten kommer att startas om fem dagar (**7200** minuter) efter distributionens tids gräns. Två timmar (**120** minuter) innan den startas om ser användaren en nedräkning som inte kan stängas eller försättas i vilo läge. Den här konfigurationen gör det möjligt för 118 timmar att Visa påminnelser ( `(7200 - 120) / 60` ). 15 timmar (**900** minuter) efter tids gränsen visar Software Center den första påminnelsen. Det visar högst sex ytterligare påminnelser var 15: e timme (**900 minuter**). Användaren ser påminnelsen som ett fönster på skärmen, i stället för ett meddelande som försvinner om några sekunder.

### <a name="high-reminder-frequency"></a>Hög påminnelse frekvens

| Inställning | Värde |
|---------|---------|
|Ange efter hur lång tid en enhet har startats om (minuter)|2880|
|Ange hur lång tid det tar för en användare att presentera en slut för tids nedräkning innan en enhet startas om (minuter)|60|
|Ange frekvensen för påminnelse meddelanden som visas för användaren, efter tids gränsen, innan en enhet startas om (minuter)|30|
|När en distribution kräver en omstart visar du ett dialog fönster för användaren i stället för ett popup-meddelande|Ja|

Enheten startas om två dagar (**2880** minuter) efter distributionens tids gräns. En timme (**60** minuter) innan den startas om ser användaren en nedräkning som inte kan stängas eller försättas i vilo läge. Den här konfigurationen gör det möjligt för 47 timmar att Visa påminnelser ( `(2880 - 60) / 60` ). **30** minuter efter tids gränsen visar Software Center den första påminnelsen. Det visar högst 92 ytterligare påminnelser var **30: e minut**. Användaren ser påminnelsen som ett fönster på skärmen, i stället för ett meddelande som försvinner om några sekunder.

## <a name="device-restart-notifications-version-1902"></a>Meddelanden om omstart av enhet (version 1902)

<!--3555947-->
Användare ser ibland inte Windows popup-meddelanden om en omstart eller en nödvändig distribution. Sedan visas inte upplevelsen för att försätta påminnelsen i vilo läge. Det här beteendet kan leda till en låg användar upplevelse när klienten når en tids gräns.

Från och med version 1902, när program varu ändringar krävs eller distributioner behöver startas om, kan du välja att använda en mer påträngande dialog ruta.

I gruppen [dator omstart](#client-settings) av klient inställningar aktiverar du följande alternativ: **när en distribution kräver en omstart visar du ett dialog fönster för användaren i stället för ett popup-meddelande**.  

Om du konfigurerar den här klient inställningen ändras användar upplevelsen för alla nödvändiga distributioner som kräver en omstart från popup-meddelanden:

:::image type="content" source="media/3555947-restart-toast-initial.png" alt-text="Popup-meddelande som startas om krävs":::

Till dialog fönstret mer påträngande Software Center:

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Dialog ruta för att starta om datorn":::

Om användaren inte startade om enheten efter installationen får de ett meddelande som en påminnelse. Den här tillfälliga påminnelsen kommer att visas för användaren baserat på klient inställningen: **Visa ett tillfälligt meddelande till användaren som anger intervallet innan användaren loggas ut eller datorn startas om (minuter)**. Den här inställningen är den övergripande tiden som användaren måste starta om datorn innan en omstart framtvingas.

- Tillfälligt meddelande när du använder popup-meddelanden:

    :::image type="content" source="media/3555947-restart-toast.png" alt-text="Popup-meddelande om väntande omstart":::

- Tillfälligt meddelande när du använder Software Center-dialogrutan, inte popup:

    :::image type="content" source="media/3555947-1902-hide-notification.png" alt-text="Väntar på att starta om Software Center-meddelanden med knappen vilo läge":::

Om användaren inte startar om efter det tillfälliga meddelandet kommer de att få den slutgiltiga nedräknings aviseringen att de inte kan stängas. Tiden för när det slutliga meddelandet visas baseras på klient inställningen: **Visa en dialog ruta som användaren inte kan stänga, vilket visar nedräknings intervallet innan användaren loggas ut eller datorn startas om (minuter)**. Om inställningen till exempel är 60 visas en timme innan en omstart framtvingas, det slutliga meddelandet visas för användaren:

:::image type="content" source="media/3555947-1902-final-countdown.png" alt-text="Meddelande om slutlig nedräkning i Software Center":::

Följande inställningar måste vara kortare i varaktighet än det kortaste [underhålls fönstret](../manage/collections/use-maintenance-windows.md) som tillämpas på datorn:

- **Visa ett tillfälligt meddelande till användaren som anger intervallet innan användaren loggas ut eller omstart av datorn (minuter)**
- **Visa en dialog ruta som användaren inte kan stänga, som visar nedräknings intervallet innan användaren loggas ut eller datorn startas om (minuter)**

> [!IMPORTANT]
> I Configuration Manager 1902, under vissa omständigheter, ersätter dialog rutan inte popup-meddelanden. Lös problemet genom att installera Samlad [uppdatering för Configuration Manager version 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="log-files"></a>Loggfiler

Om du vill felsöka omstarter av enheter använder du filerna **RebootCoordinator. log** och **SCNotify. log** på klienten. Utifrån en speciell typ av distribution kan du också behöva använda ytterligare klient [logg-filer](../../plan-design/hierarchy/log-files.md).

## <a name="next-steps"></a>Nästa steg

- [Konfigurera klientinställningar](configure-client-settings.md)
- [Inställningar för **användar upplevelse** för program distribution](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)
- [Användar meddelanden för obligatoriska program distributioner](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)
