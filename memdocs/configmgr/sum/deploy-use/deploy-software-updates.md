---
title: Distribuera programuppdateringar
titleSuffix: Configuration Manager
description: Lär dig hur du manuellt eller automatiskt distribuerar program uppdateringar i Configuration Manager-konsolen.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 2adf22fd9c17863d7c29e2a29d2125d22f2d944f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127679"
---
# <a name="deploy-software-updates"></a>Distribuera programuppdateringar  

*Gäller för: Configuration Manager (aktuell gren)*

Distributions fasen för program uppdateringar är en process för att distribuera program uppdateringar. Oavsett hur du distribuerar program uppdateringar, platsen:
- Lägger till uppdateringar i en program uppdaterings grupp
- Distribuerar uppdaterings innehållet till distributions platser
- Distribuerar uppdaterings gruppen till klienter  

När du har skapat distributionen skickar platsen en associerad program uppdaterings princip till riktade klienter. Klienterna laddar ned innehålls filerna för program uppdateringen från en innehålls källa till sin lokala cache. Klienter på Internet laddar alltid ned innehåll från Microsoft Update moln tjänsten. Program uppdateringarna är sedan tillgängliga för installation av-klienten.   

> [!Tip]  
>  Om en distributions plats inte är tillgänglig kan klienter på intranätet även hämta program uppdateringar från Microsoft Update.  

> [!NOTE]  
>  Till skillnad från andra distributions typer laddas alla program uppdateringar ned till klientens cacheminne. Detta gäller oavsett inställningen för maximal cachestorlek på klienten. Mer information om inställningen för klientcachen finns i [Konfigurera klientens cacheminne för Configuration Manager klienter](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Om du konfigurerar en nödvändig programuppdateringsdistribution, installeras programuppdateringarna automatiskt vid den schemalagda tidsgränsen. Alternativt kan användaren på klientdatorn schemalägga eller initiera programuppdateringsinstallationen före tidsgränsen. Efter installationsförsöket skickar klientdatorerna tillståndsmeddelanden tillbaka till platsservern för att rapportera om programuppdateringsinstallationen har lyckats. Mer information om programuppdateringsdistributioner finns i [Arbetsflöden vid programuppdateringsdistributioner](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Det finns tre huvud scenarier för distribution av program uppdateringar: 
- [Manuell distribution](#BKMK_ManualDeployment)  
- [Automatisk distribution](#bkmk_auto)  
- [Stegvis distribution](#bkmk_phased)  

Normalt börjar du med att distribuera program uppdateringar manuellt för att skapa en bas linje för dina klienter, och sedan hanterar du program uppdateringar på klienter med hjälp av en automatisk eller stegvis distribution.  

> [!Note]  
> Du kan inte använda en automatisk distributions regel med en stegvis distribution.



## <a name="manually-deploy-software-updates"></a><a name="BKMK_ManualDeployment"></a>Distribuera program uppdateringar manuellt
Välj program uppdateringar i Configuration Manager-konsolen och starta distributions processen manuellt. Du använder vanligt vis den här distributions metoden för att:  

- Hämta klienterna uppdaterade med nödvändiga program uppdateringar innan du skapar regler för automatisk distribution som hanterar månatliga distributioner  

- Distribuera out-of-band-programuppdateringar  


Följande lista visar det allmänna arbetsflödet för manuell distribution av programuppdateringar:  

1. Filtrera fram programuppdateringar där särskilda krav används. Du kan till exempel ange villkor som hämtar alla säkerhets uppdateringar eller kritiska program uppdateringar som krävs på över 50 klienter.  

2. Skapa en programuppdateringsgrupp som innehåller programuppdateringarna.  

3. Ladda ned innehållet för programuppdateringarna i programuppdateringsgruppen.  

4. Distribuera programuppdateringsgruppen manuellt.  

Mer information och detaljerade anvisningar finns i [distribuera program uppdateringar manuellt](manually-deploy-software-updates.md).

> [!Note]
> - Från och med den 21 april 2020 kommer Office 365 ProPlus att byta namn till **Microsoft 365 appar för företag**. Mer information finns i [namn ändring för Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Du kan fortfarande se referenser till det gamla namnet i Configuration Manager-konsolen och stöd dokumentationen medan-konsolen uppdateras.
> - När du distribuerar uppdateringar för Microsoft 365-appar manuellt hittar du dem i noden **office 365-uppdateringar** under **Office 365-klient hantering** av arbets ytan **program varu bibliotek** . 

## <a name="automatically-deploy-software-updates"></a><a name="bkmk_auto"></a>Distribuera program uppdateringar automatiskt

Konfigurera automatisk distribution av program uppdateringar med hjälp av en regel för automatisk distribution (ADR). Den här distributions metoden är vanlig för månatliga program uppdateringar (kallas vanligt vis "korrigerings tisdag") och för att hantera definitions uppdateringar. Du definierar villkoren för en ADR för att automatisera distributions processen. I följande lista visas det allmänna arbets flödet för automatisk distribution av program uppdateringar:  

1.  Skapa en ADR som anger distributions inställningar.  

2.  Platsen lägger till program uppdateringar till en program uppdaterings grupp.  

3.  Platsen distribuerar program uppdaterings gruppen till klienterna i mål samlingen.  

Börja med att fastställa en strategi för automatisk distribution av program uppdateringar. Skapa till exempel ADR till att börja med att ange en samling test klienter som mål. När du har kontrollerat att test gruppen har installerat program uppdateringarna lägger du till en ny distribution i regeln. Du kan också ändra mål samlingen i den befintliga distributionen till en som innehåller en större uppsättning klienter. Tänk på följande när du bestämmer vilken strategi som ska användas:  

- Du kan ändra egenskaperna för de program uppdaterings objekt som skapas av ADR.   

- I ADR distribueras automatiskt program uppdateringar till klienter när du lägger till dem i mål samlingen.  

- När du eller ADR lägger till nya program uppdateringar i program uppdaterings gruppen, distribuerar platsen automatiskt dem till klienterna i mål samlingen.  

- Aktivera eller inaktivera distributioner när som helst för ADR.  


När du har skapat en ADR lägger du till ytterligare distributioner till regeln. Den här åtgärden hjälper dig att hantera komplexiteten vid distribution av olika uppdateringar till olika samlingar. Varje ny distribution har en fullständig uppsättning funktioner och distributionsövervakning.  

Varje ny distribution som du lägger till:  

- Använder samma uppdaterings grupp och paket, som ADR skapar första gången den körs  
- Kan rikta en annan samling  
- Stöder unika distributionsegenskaper, t.ex.:  
  -   Aktiveringstid  
  -   Tidsgräns  
  -   Användarupplevelse  
  -   Separata aviseringar för varje distribution  


Mer information och detaljerade anvisningar finns i [distribuera program uppdateringar automatiskt](automatically-deploy-software-updates.md)



## <a name="deploy-software-updates-in-phases"></a><a name="bkmk_phased"></a>Distribuera program uppdateringar i faser

<!--1358146-->
Från och med version 1810 skapar du stegvisa distributioner för program uppdateringar. Med stegvisa distributioner kan du dirigera en samordnad, sekvenserad distribution av program vara utifrån anpassningsbara kriterier och grupper.

Mer information finns i skapa stegvisa [distributioner](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

