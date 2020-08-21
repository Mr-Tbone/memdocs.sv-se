---
title: Planera plats databasen
titleSuffix: Configuration Manager
description: Överväg plats databasen och plats databasens server roll när du planerar din Configuration Manager-hierarki.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 068511c5b3b0c15eb355c484b241a76d9dd512e2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700188"
---
# <a name="plan-for-the-site-database-for-configuration-manager"></a>Planera för plats databasen för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Plats databas servern är en dator som kör en version av Microsoft SQL Server som stöds. SQL Server används för att lagra information för Configuration Manager-platser. Varje plats i en Configuration Manager-hierarki innehåller en plats databas och en server som har tilldelats plats databasens server roll.  

-   För centrala administrations platser och primära platser kan du installera SQL Server på plats servern, eller så kan du installera SQL Server på en annan dator än plats servern.  

-   För sekundära platser kan du använda SQL Server Express i stället för en fullständig SQL Server-installation. Databas servern måste dock köras på den sekundära plats servern.  

-  För användning av SQL-tillgänglighetsgruppen måste databas återställnings modellen vara FULL  

-  För användnings gruppen för icke-SQL-tillgänglighet måste databas återställnings modellen vara inställd på enkel  

Mer information om SQL-återställnings läge finns i [återställnings modeller (SQL Server)](/sql/relational-databases/backup-restore/recovery-models-sql-server).

Du kan använda följande SQL Server-konfigurationer för platsdatabasen:  

-   Standardinstansen av SQL Server.  

-   En namngiven instans på en enskild dator som kör SQL Server.  

-   En namngiven instans på en klustrad instans av SQL Server.  

-   En SQL Server AlwaysOn-tillgänglighetsgruppen (från och med version 1602 av Configuration Manager)


För att vara värd för plats databasen måste SQL Server uppfylla kraven som beskrivs i [stöd för SQL Server versioner för Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  



## <a name="remote-database-server-location-considerations"></a>Överväganden för fjärrdatabasernas plats  

Om du använder en fjärran sluten databas serverdator måste du se till att den mellanliggande nätverks anslutningen är en nätverks anslutning med hög bandbredd och hög tillgänglighet. Plats servern och vissa plats system roller måste ständigt kommunicera med den fjärrserver som är värd för plats databasen.

-   Mängden bandbredd som krävs för kommunikation till databas servern beror på en kombination av många olika plats-och klientkonfigurationer. Den faktiska bandbredd som krävs kan därför inte förutsägas på ett korrekt sätt.  

-   Varje dator som kör SMS-providern och som ansluter till platsdatabasen ökar kraven på nätverksbandbredd.  

-   Datorn som kör SQL Server måste finnas i en domän som har dubbelriktat förtroende för plats servern och alla datorer som kör SMS-providern.  

-   Du kan inte använda en grupperad SQL Server för platsdatabaservern när platsdatabasen är samordnad med platsservern.  


Normalt har en plats system server bara stöd för plats system roller från en enda Configuration Manager plats. Du kan dock använda olika instanser av SQL Server på klustrade eller icke-klustrade servrar som kör SQL Server, som värd för en databas från olika Configuration Manager-platser. Om du vill stödja databaser från olika platser måste du konfigurera varje instans av SQL Server att använda unika portar förkommunikation.