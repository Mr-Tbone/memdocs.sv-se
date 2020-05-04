---
title: Slutföra migrering
titleSuffix: Configuration Manager
description: Lär dig hur du Slutför migreringen till en Configuration Manager aktuella Branch-målhierarkin efter att en källhierarki inte längre innehåller data.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76cf6b57a4bc1439f2aa9c2e0484271987f85748
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713011"
---
# <a name="plan-to-complete-migration-in-configuration-manager"></a>Planera för att slutföra migreringen i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med Configuration Manager kan du slutföra processen för migrering när en källhierarki inte längre innehåller data som du vill migrera till målhierarkin. Att slutföra migreringen omfattar följande allmänna steg:  

-   Se till att de data du behöver har migrerats. Innan du Slutför migreringen från en-källhierarki ser du till att du har migrerat alla resurser från källhierarkin som du behöver i målhierarkin. Detta kan omfatta data och klienter.  

-   Sluta samla in data från käll platser. Om du vill slutföra migreringen från en-källhierarki måste du först sluta samla in data från käll platser.  

-   Rensar data för migrering. När du har slutat samla in data från alla käll platser i en-källhierarki kan du ta bort data om migreringsprocessen och källhierarkin från databasen i målhierarkin.  

-   Inaktivera källhierarkin. När du har slutfört migreringen från en-källhierarki och hierarkin inte längre har resurser som du hanterar, kan du inaktivera platserna i källhierarkin och ta bort den relaterade infrastrukturen från din miljö. Information om hur du inaktiverar platser och käll-hierarkier finns i dokumentationen för den versionen av Configuration Manager.  

Använd följande avsnitt när du planerar att slutföra migreringen från en-källhierarki genom att stoppa data insamlingen och rensa migreringen:  

-   [Planera att sluta samla in data](#Plan_to_Stop_Data_Gath)  

-   [Planera att rensa data i migreringen](#Plan_to_clean_up)  

##  <a name="plan-to-stop-gathering-data"></a><a name="Plan_to_Stop_Data_Gath"></a>Planera att sluta samla in data  
 Innan du Slutför migreringen och rensar data från migreringen måste du sluta samla in data från varje käll plats i källhierarkin. Om du vill sluta samla in data från varje käll plats måste du utföra kommandot **Avbryt data insamling** på käll platserna på den nedre nivån och upprepa sedan processen på varje överordnad plats. Platsen på den översta nivån i källhierarkin måste vara den sista du slutar samla in data på. Du måste stoppa data insamlingen på varje underordnad plats innan du kan utföra kommandot på en överordnad plats. Normalt slutar du bara att samla in data när du är redo att slutföra migreringsprocessen.  

 När du har slutat samla in data från en käll plats är delade distributions platser från den platsen inte längre tillgängliga som innehålls platser för klienter i målhierarkin. Därför bör du se till att alla migrerade innehåll som klienterna i målhierarkin behöver åtkomst till förblir tillgängliga genom att använda något av följande alternativ:  

-   Distribuera innehållet till minst en distributions plats i målhierarkin.  

-   Innan du slutar samla in data från en käll plats måste du uppgradera eller omtilldela delade distributions platser som har det innehåll som krävs. Mer information om att uppgradera eller omtilldela delade distributions platser finns i tillämpliga avsnitt i [Planera en strategi för migrering av innehålls distribution](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

När du har slutat samla in data från varje käll plats i källhierarkin kan du rensa data i migreringen. Innan du rensar data i migreringen fortsätter varje migreringsjobb som körs eller som är schemalagt att köras att vara tillgängligt i Configuration Manager-konsolen.  

Mer information om käll platser och data insamling finns i [Planera en käll-hierarki-strategi](../../core/migration/planning-a-source-hierarchy-strategy.md).  

##  <a name="plan-to-clean-up-migration-data"></a><a name="Plan_to_clean_up"></a>Planera att rensa data i migreringen  
 Det sista steget som krävs för att slutföra migreringen är att rensa data i migreringen. Du kan använda kommandot **Rensa migrering av data** när du har slutat samla in data för varje käll plats i källhierarkin. Den här valfria åtgärden tar bort data om den aktuella källhierarkin från databasen i målhierarkin.  

 När du rensar data i migreringen tas de flesta data om migreringen bort från databasen i målhierarkin. Information om migrerade objekt bevaras dock. Med den här informationen kan du använda arbets ytan **migrering** för att konfigurera om källhierarkin som har de data som migrerades för att återuppta migreringen från källhierarkin, eller granska objekt och plats ägarskap för de objekt som migrerades tidigare.  
