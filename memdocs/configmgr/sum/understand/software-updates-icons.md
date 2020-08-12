---
title: Ikoner som används för programuppdateringar
titleSuffix: Configuration Manager
description: Configuration Manager-konsolen innehåller ikoner som anger ett tillstånd för den synkroniserade uppdateringen eller program uppdaterings gruppen.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 63c5ef72-5715-4d86-85a2-71beba469fab
author: mestew
ms.author: mstewart
ms.openlocfilehash: ff616c9ee61e85e4e77aeef6254ca9922427270c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129431"
---
# <a name="icons-used-for-software-updates-in-configuration-manager"></a>Ikoner som används för program uppdateringar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Synkroniserade program uppdateringar visas i Configuration Manager-konsolen och den första kolumnen för varje program uppdatering innehåller en ikon som anger ett särskilt tillstånd. Programuppdateringsgrupper visas också med en symbol som ger information om tillståndet för de programuppdateringar som ingår i gruppen. Det här avsnittet innehåller information om programuppdateringsikonerna och vad varje ikon motsvarar.  

## <a name="icons-for-software-updates"></a>Ikoner för programuppdateringar  
 Synkroniserade programuppdateringar visas med någon av följande ikoner.  

### <a name="normal-icon"></a>Normal ikon  
 ![ikonen](../media/Normal.jpg "Normal ikon") Ikonen med en grön pil visar en normal program uppdatering.  

 **Beskrivning:**  

 Normala programuppdateringar har synkroniserats och är tillgängliga för programvarudistribution.  

 **Driftproblem:**  

 Det finns inga driftproblem.  

### <a name="expired-icon"></a>Ikon för inaktuell  
 ![ikonen](../media/Expired.jpg "Utgången ikon") Ikonen med ett svart X visar en program uppdatering som har upphört att gälla. Du kan också identifiera program uppdateringar som har upphört att gälla genom att visa den **Utgångna** kolumnen för program uppdateringen när den visas i Configuration Manager-konsolen.  

 **Beskrivning:**  

 Programuppdateringar som har upphört att gälla kunde tidigare distribueras till klientdatorer, men när en programuppdatering har upphört att gälla kan nya distributioner inte längre skapas för programuppdateringarna. Program uppdateringar som har upphört att gälla tas bort från aktiva distributioner och kommer inte längre att göras tillgängliga för klienter.  

 **Driftproblem:**  

 Det finns inga driftproblem.

### <a name="superseded-icon"></a>Ikon för ersatt  
 ![ikonen](../media/Superseded.jpg "Ersatt ikon") Ikonen med en gul stjärna representerar en ersatt program uppdatering. Du kan också identifiera ersatta program uppdateringar genom att visa kolumnen **ersatt** för program uppdateringen när den visas i Configuration Manager-konsolen.  

 **Beskrivning:**  

 Ersatta programuppdateringar har bytts ut mot nyare versioner av programuppdateringen. En program uppdatering som ersätter en annan program uppdatering gör vanligt vis en eller flera av följande saker:  

- Förstärker, förbättrar eller lägger till i korrigeringen som fanns i en eller flera tidigare programuppdateringar.  

- Förbättrar effektiviteten för det ersatta uppdateringsfilpaketet, som klienten installerar om programuppdateringen godkänns för installation. Till exempel kan den ersatta program uppdateringen innehålla filer som inte längre är relevanta för korrigeringen eller för de operativ system som nu stöds av den nya program uppdateringen, så dessa filer ingår inte i den ersättande program uppdateringens fil paket.  

- Uppdateringar för nyare versioner av en produkt kan alltså inte längre användas för äldre versioner eller konfigurationer av en produkt. Programuppdateringar kan även ersätta andra programuppdateringar om det har gjorts ändringar för utökat språkstöd. Till exempel kan en senare revision av en produkt uppdatering för Microsoft 365 appar ta bort stöd för ett äldre operativ system, men lägga till ytterligare stöd för nya språk i den ursprungliga program uppdaterings versionen.  

  På fliken Ersättningsregler i egenskaperna för Komponent för programuppdateringsplats kan du ange hur ersatta programuppdateringar ska hanteras. Mer information finns i [Ersättningsregler](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

  **Driftproblem:**  

  Distribuera den ersättande programuppdateringen till klientdatorer i stället för den ersatta programuppdateringen, när så är möjligt. Du kan visa en lista över de programuppdateringar som ersätter programuppdateringen på fliken **Ersättningsinformation** i egenskaperna för programuppdateringen.  

### <a name="invalid-icon"></a>Ikon för ogiltig  
 ![ikonen](../media/Invalid.jpg "Ogiltig ikon") Ikonen med ett rött X visar en ogiltig program uppdatering.  

 **Beskrivning:**  

 Ogiltiga program uppdateringar finns i en aktiv distribution, men av någon anledning är innehållet (program uppdaterings fil) inte tillgängligt. Följande är några scenarier där det här tillståndet kan uppstå:  

- Du distribuerar programuppdateringen, men programuppdateringsfilen tas bort från distributionspaketet och är inte längre tillgänglig.  

- Du skapar en program uppdaterings distribution på en plats och distributions objekt replikeras till en underordnad plats, men distributions paketet har inte repliker ATS till den underordnade platsen.  

  **Driftproblem:**  

  Klienter kan inte installera uppdateringen förrän innehållet blir tillgängligt på en distributionsplats när innehållet saknas för en programuppdatering. Du kan distribuera om innehållet till distributionsplatser med hjälp av åtgärden **Distribuera om** . När innehåll saknas för en programuppdatering i en distribution som har skapats på en överordnad plats måste programuppdateringen replikeras eller distribueras om till den underordnade platsen. Mer information om omdistribution av innehåll finns i [hantera det innehåll som du har distribuerat](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="metadata-only-icon"></a>Ikon för endast metadata
 ![ikonen](../media/MetadataOnly.png "Ikon för endast metadata") Ikonen med en blå pil representerar en program uppdatering med endast metadata.

 **Beskrivning:**  

 Program uppdateringar med endast metadata är tillgängliga i Configuration Manager-konsolen för rapportering. Du kan inte distribuera eller hämta program uppdateringar med endast metadata eftersom en program uppdaterings fil inte är associerad med metadata för program uppdateringarna.  

 **Driftproblem:**  

 Program uppdateringar med endast metadata är tillgängliga för rapporterings ändamål och är inte avsedda för distribution av program uppdateringar.  

## <a name="icons-for-software-update-groups"></a>Ikoner för programuppdateringsgrupper  
 Programuppdateringsgrupper visas med någon av följande ikoner.  

### <a name="normal-icon"></a>Normal ikon  
 ![ikonen](../media/Normal.jpg "Normal ikon") Ikonen med en grön pil visar en program uppdaterings grupp som endast innehåller normala program uppdateringar.  

 **Driftproblem:**  

 Det finns inga driftproblem.  

### <a name="expired-icon"></a>Ikon för inaktuell  
 ![ikonen](../media/Expired.jpg "Utgången ikon") Ikonen med ett svart X visar en program uppdaterings grupp som innehåller en eller flera program uppdateringar som har upphört att gälla.  

 **Driftproblem:**  

 Ta bort eller ersätt programuppdateringar som har upphört att gälla i programuppdateringsgruppen när det är möjligt.  

### <a name="superseded-icon"></a>Ikon för ersatt  
 ![ikonen](../media/Superseded.jpg "Ersatt ikon") Ikonen med en gul stjärna visar en program uppdaterings grupp som innehåller en eller flera ersatta program uppdateringar.  

 **Driftproblem:**  

 Byt ut den ersatta programuppdateringen i programuppdateringsgruppen med den ersättande programuppdateringen när så är möjligt.  

### <a name="invalid-icon"></a>Ikon för ogiltig  
 ![ikonen](../media/Invalid.jpg "Ogiltig ikon") Ikonen med ett rött X visar en program uppdaterings grupp som innehåller en eller flera ogiltiga program uppdateringar.  

 **Driftproblem:**  

 Klienter kan inte installera uppdateringen förrän innehållet blir tillgängligt på en distributionsplats när innehållet saknas för en programuppdatering. Du kan distribuera om innehållet till distributionsplatser med hjälp av åtgärden **Distribuera om** . När innehåll saknas för en program uppdatering i en distribution som skapats på en överordnad plats måste program uppdateringen replikeras eller distribueras om till den underordnade platsen. Mer information om omdistribution av innehåll finns i [hantera det innehåll som du har distribuerat](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  


## <a name="next-steps"></a>Nästa steg 

[Planera programuppdateringar](../plan-design/plan-for-software-updates.md)