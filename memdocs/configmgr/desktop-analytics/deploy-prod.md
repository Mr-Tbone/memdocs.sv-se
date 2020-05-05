---
title: Så här distribuerar du till produktion
titleSuffix: Configuration Manager
description: En instruktions guide för att distribuera till en produktions grupp för en stationär analys.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c7a14da1505e89dfd61a3dc4f13385fbf5c21d41
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723658"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Så här distribuerar du till produktion med Desktop Analytics

När du har [distribuerat till pilot](deploy-pilot.md) och har granskat statusen för dina till gångar är du redo att uppdatera resten av din produktions miljö.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

Det finns tre huvud delar för att slutföra distributionen av uppdateringar till produktions enheter:

1. [Granska till gångar som behöver ett uppgraderings beslut](#bkmk_review): om du vill göra enheter redo för produktions distribution måste deras uppgraderings beslut vara **klart** eller **klart, och reparationer krävs**.  

2. [Distribuera till enheter som är klara](#bkmk_deploy): Använd Configuration Manager för att uppdatera enheter som är klara. Skriv bords analys innehåller en lista över enheter som är klara för produktions distribution och rapporter för att övervaka lyckad distribution.  

3. [Övervaka hälsan för uppdaterade enheter](#bkmk_monitor): när uppdaterings distributionen fortskrider övervakas hälsan hos viktiga till gångar. Felsök och åtgärda problemen om det behövs. Om du bestämmer att problemen inte kan åtgärdas stoppar du distributionen till de berörda enheterna genom att ställa in ett uppgraderings beslut till att **inte**fungera.  

> [!NOTE]  
> När som helst kan du när som helst starta produktions distributionen när du är säker på att pilot distributionen lyckas. Det finns inget krav på att alla pilot enheter når "slutfört" tillstånd först.  



## <a name="review-assets-that-need-an-upgrade-decision"></a><a name="bkmk_review"></a>Granska till gångar som behöver ett uppgraderings beslut

Skriv bords analys vägleder dig genom processen för att granska dina till gångar för produktions distribution. I Azure Portal går du till **distributions planer**, väljer en distributions plan och väljer sedan **Förbered produktion** på den vänstra menyn.

![Skärm bild av förbereda produktions visning i Desktop Analytics](media/prepare-production.png)

Granska appens tillstånd. Använd den informationen för att ange uppgraderings beslutet för var och en av dessa till gångar.

Använd var och en av flikarna för att granska status för apparna. I varje tabbad vy kan du filtrera resultaten för att visa enheter som håller på att uppgraderas, kräva din uppmärksamhet, enheter med blandade resultat och dessa enheter i ett förutbestämt tillstånd.

Välj **Mötes mål** för att filtrera vyn till till gångar som troligen är klara för produktions distribution baserat på följande kriterier:

- Risk: en utvärdering före uppgradering av kända risker vid uppdatering av enheter som har den här till gången installerad  

- Hälso status: en utvärdering efter uppgradering av enheter i andra distributioner och om de fick problem efter att uppdateringen har installerats. Mer information om hälso tillstånd finns i [övervaka hälsan för uppdaterade enheter](#bkmk_monitor).  

Om du vill godkänna en till gång för uppgradering väljer du namnet i listan och väljer sedan något av följande alternativ i listan **uppgraderings beslut** :

- Granskning pågår
- Redo
- Redo (med reparation)
- Det gick inte
- Ej granskad

Om du vill ange det här värdet för flera appar samtidigt, använder du den första kolumnen för att **välja det här objektet**och väljer sedan **Ange uppgraderings beslut**.

![Ange alternativet för uppgraderings beslut på flera appar](media/prep-prod-set-upgrade-decision.png)

Välj **inga data** för att visa till gångar som inte kunde klassificeras. Dessa till gångar är vanligt vis till gångar som inte har tillräckligt med täckning för Skriv bords analys för att utföra en analys av risk-eller hälso status. Du kan förbättra täckningen genom att lägga till ytterligare enheter med dessa till gångar i piloten eller be pilot användare att testa dessa till gångar.

Det kan också finnas till gångar i den **uppmärksamhet som krävs** eller **blandade resultat** tillstånd. Dessa till gångar kan kräva ytterligare granskning innan du fattar ett uppgraderings beslut för dem.

Granska alla appar. När en bestämd enhet har ett positivt uppgraderings beslut för alla till gångar ändras dess tillstånd till "redo för produktion". Se det aktuella antalet på huvud sidan för distributions planen genom att välja det tredje distributions steget, **distribuera**.


## <a name="deploy-to-devices-that-are-ready"></a><a name="bkmk_deploy"></a>Distribuera till enheter som är klara

Configuration Manager använder data från Desktop Analytics för att skapa en samling för produktions distributionen. Distribuera inte aktivitetssekvensen med en traditionell distribution. Använd följande procedur för att skapa en stationär Analytics-integrerad distribution:

Om du har följt den rekommenderade processen för att [distribuera till pilot enheter](deploy-pilot.md#deploy-to-pilot-devices)är den Configuration Manager fasen distribution klar. När du markerar till gångar som *färdiga*synkroniserar Desktop Analytics automatiskt enheterna med Configuration Manager. Dessa enheter läggs sedan till i produktions samlingen. När den stegvisa distributionen flyttas till den andra fasen får dessa produktions enheter uppgraderings distributionen.

Om du konfigurerade den stegvisa distributionen för att **manuellt påbörja distributionen av den andra fasen**måste du flytta den manuellt till nästa fas. Mer information finns i [Hantera och övervaka stegvisa distributioner](../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_move).

Om du har skapat en stationär Analytics-integrerad enskild distribution till pilot samlingen måste du upprepa processen för att distribuera till produktions samlingen.


### <a name="address-deployment-alerts"></a>Aviseringar om adress distribution

Precis som med pilot distributionen får du en varning från Desktop Analytics om eventuella problem som behöver åtgärdas under produktions distributionen. Gå till distributions planen i Skriv bords analys och välj **distributions status** på den vänstra menyn. I vyn distributions status visas enheter i följande kategorier:  

- Inte startad
- Pågår
- Slutfört
- Kräver åtgärd – enheter (sorterat efter enhets namn)
- Kräver åtgärds problem (sorteras efter typ av ärende)

![Skärm bild av status för produktions distribution i Desktop Analytics](media/prod-deployment-status.png)


## <a name="monitor-the-health-of-updated-devices"></a><a name="bkmk_monitor"></a>Övervaka hälsan för uppdaterade enheter

Sidan **Förbered produktion** fokuserar på att hjälpa dig att fatta uppgraderings beslut för dina till gångar. Sidan som standard visar bara de till gångar som ännu inte har statusen **klar** . Sidan **övervaka hälso** tillstånd visar hälso problem på alla slags till gångar, även de till gångar som marker ATS som **färdiga**. Om det upptäcks kan du felsöka och åtgärda problemet eller ändra uppgraderings beslutet till att **inte göra det**. När du ändrar uppgraderings beslutet förhindrar den här åtgärden framtida uppgraderingar på enheter med denna till gång.

Filtrera den här sidan efter till gångar med följande hälso tillstånd:

| Hälso status filter | Beskrivning |
|----------------------|-------------|
| **Åtgärd krävs** | (Standard filter) Skriv bords analys identifierar statistiskt betydelsefull regression till viss hälso mått för denna till gång
| **Mötes mål** | Desktop Analytics identifierar ingen regression i beteendet |
| **Otillräckliga data** | Skriv bords analys har inte tillräckligt med data om den här till gången för att göra några rekommendationer |
| **Inga data** | Det finns inga användnings data ännu tillgängliga för den här till gången |

Om du vill visa en ofiltrerad vy över alla till gångar väljer du det aktuella filtret. Den här åtgärden tar bort filtret.

> [!NOTE]  
> För att minska antalet till gångar med otillräckliga data övervakar Desktop Analytics resurserna på alla enheter som har uppgraderats till den mål Windows-version som anges i din distributions plan. Dessa enheter innehåller de som inte ingår i den angivna distributions planen.  

Standard sorterings ordningen är antalet enheter som har haft en incident med en viss till gång, så att du snabbt kan se vilka som orsakar flest problem. Om du till exempel visar **appar**sorteras de efter **enheter med app kraschar de senaste två veckorna**.

Om du vill titta på hälsan för alla till gångar, även de till gångarna med otillräckliga data för Skriv bords analys för att göra statistiska inferences, använder du följande process:

1. Välj List rutan i kolumnen **enheter med incidenter under de senaste två veckorna** . Lägg till ett filter till endast de till gångar som har haft incidenter på ett minimalt antal enheter som är intressanta. Du kan till exempel Visa objekt med värden som är **större än** 100.  

2. Välj List rutan på sidan **% enheter med incidenter under de senaste två veckorna** och välj att sortera efter **fallande**.  

    I den resulterande vyn visas till gångar med högsta möjliga frekvens av incidenter till ett minsta antal incidenter.  

3. Välj en till gång för att få mer information eller ändra uppgraderings beslutet.  

Mer information finns i [övervakning av hälso tillstånd](health-status-monitoring.md).
