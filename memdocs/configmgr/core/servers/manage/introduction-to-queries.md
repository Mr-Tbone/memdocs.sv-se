---
title: Introduktion till frågor
titleSuffix: Configuration Manager
description: Skapa och kör frågor för att hitta objekt i en Configuration Manager-hierarki som matchar dina frågevillkor.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff98645c7892192f2f914a25102454b5e9415fee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713823"
---
# <a name="introduction-to-queries-in-configuration-manager"></a>Introduktion till frågor i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan skapa och köra frågor för att hitta objekt i en Configuration Manager-hierarki som matchar dina frågevillkor. Dessa objekt omfattar objekt som vissa typer av datorer eller användar grupper. Frågor kan returnera de flesta typer av Configuration Manager objekt, som omfattar platser, samlingar, program och inventerings data.  

## <a name="query-creation-overview"></a>Översikt över att skapa frågor

 När du skapar en fråga måste du ange minst två parametrar: var du vill söka och vad du vill söka efter. Om du till exempel vill hitta mängden hårddisk utrymme som är tillgängligt på alla datorer på en Configuration Manager webbplats, kan du skapa en fråga för att söka efter tillgängligt hårddisk utrymme i attributet för den **logiska diskens** attribut och attributet **ledigt utrymme (MB)** .  

 När du har skapat en första fråga kan du ange ytterligare frågevillkor. Du kan till exempel ange att frågeresultatet bara ska innehålla datorer som tilldelats en angiven plats. Du kan också ändra hur resultatet visas så att du kan visa resultaten i en ordning som är meningsfull för dig. Du kan till exempel ange att resultatet sorteras efter mängden ledigt hårddisk utrymme, i stigande eller fallande ordning.  

 När du skapar en fråga lagras den av Configuration Manager och visas i noden **frågor** på arbets ytan **övervakning** . Från den här platsen kan du skapa nya frågor och köra, uppdatera och hantera befintliga frågor.  

 Du kan också importera en fråga till en frågeregel i en Configuration Manager-samling. Mer information finns i [så här skapar du samlingar](../../../core/clients/manage/collections/create-collections.md).  

## <a name="next-steps"></a>Nästa steg

 [Skapa frågor](../../../core/servers/manage/create-queries.md)
