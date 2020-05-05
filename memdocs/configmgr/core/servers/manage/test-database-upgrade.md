---
title: Testa databas uppdatering
titleSuffix: Configuration Manager
description: Testa att uppgradera plats databasen när du installerar uppdateringar för Configuration Manager.
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 56c1422f4157b255f4f7a8624e36d10e01f28fc0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719983"
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>Testa databas uppgraderingen när du installerar en uppdatering

*Gäller för: Configuration Manager (aktuell gren)*

Informationen i det här avsnittet kan hjälpa dig att köra en test databas uppgradering innan du installerar en uppdatering i konsolen för den aktuella grenen av Configuration Manager. Test uppgraderingen är dock inte längre ett obligatoriskt eller rekommenderat steg om inte databasen är misstänkt eller ändras av anpassningar som inte uttryckligen stöds av Configuration Manager.

## <a name="do-i-need-to-run-a-test-upgrade"></a>Måste jag köra en test uppgradering?
Utfasningen av det här uppgraderings testet görs möjlig på grund av ändringar som introduceras med Configuration Manager aktuella grenen. Dessa ändringar fören klar processen och hastigheten som en produktions miljö kan uppdateras till senare versioner. Den här omdesignen har gjorts för att hjälpa kunder att hålla sig uppdaterade med mindre risk och mindre drifts kostnader när de installerar varje ny uppdatering.

Ändringarna är till för att installera uppdateringar, inklusive logik som automatiskt återställer en misslyckad uppdatering utan att behöva köra en plats återställning. Dessa ändringar gör det möjligt att använda-konsolen för att hantera uppdaterings installationer och innehåller ett alternativ för att göra [om installationen av en misslyckad uppdatering](install-in-console-updates.md#bkmk_retry).

> [!TIP]
> När du uppgraderar till Configuration Manager aktuella grenen från en äldre produkt, som System Center 2012 Configuration Manager, [är test av databas uppgraderingar ett rekommenderat steg](../deploy/install/upgrade-to-configuration-manager.md#bkmk_test).

Om du fortfarande planerar att testa uppgraderingen av en plats databas när du installerar en uppdatering i konsolen, kompletterar följande information om hur du [installerar en uppdatering i konsolen](install-in-console-updates.md#bkmk_install).

## <a name="prepare-to-run-a-test-database-upgrade"></a>Förbered för att köra en uppgradering av test databasen  
Innan du installerar en ny uppdatering i hierarkin, t. ex. uppdatering 1702, kan du testa uppgraderingen av plats databasen.

Om du vill köra uppgraderings testet använder du installations programmet för Configuration Manager från källfilerna från [CD: n. Den senaste mappen](the-cd.latest-folder.md) på en plats som kör den version av Configuration Manager som du uppdaterar till. Detta krav innebär att du kan testa databas uppdateringen för uppdatering till 1702:
-   Du måste ha minst en plats som kör version 1702 från vilken du kan hämta CD: n. Senaste mappen.
-   Om du inte har en plats som kör den version som krävs, kan du överväga att installera en plats i en labb miljö och sedan uppdatera platsen till den nya versionen. Detta skapar CD: n. Senaste mappen med rätt version av källfiler.

Uppgraderings testet körs mot en säkerhets kopia av plats databasen som du återställde till en separat instans av SQL Server.  Du kör installations programmet från **CD: n. Den senaste** mappen med kommando rads växeln **TESTDBUPGRADE** för att testa uppgraderingen som återställde kopia av databasen. När test uppgraderingen har slutförts tas den uppgraderade databasen bort. Den kan inte användas av en Configuration Manager webbplats.

Om en uppdaterings installation Miss lyckas behöver du inte återställa platsen. I stället kan du försöka att installera uppdateringen igen från-konsolen.

##  <a name="run-the-test-upgrade"></a>Kör test uppgraderingen    
1. Använd Configuration Manager-installationen och källfilerna från **CD: n. Den senaste** mappen på en plats som kör den version som du planerar att uppdatera till.  

2. Kopiera **CD: n. Den senaste** mappen till en plats på SQL Server-instansen som du ska använda för att köra test databas uppgraderingen.

3. Skapa en säkerhets kopia av plats databasen som du vill testa uppgraderingen för. Sedan återställer du en kopia av databasen till en instans av SQL Server som inte är värd för en Configuration Manager webbplats. SQL Server-instansen måste använda samma utgåva av SQL Server som plats databasen.  

4. När du har återställt databas kopian kör du **installationen** från CD: n. Den senaste mappen som innehåller källfilerna från den version som du uppdaterar till. Använd kommandotolksalternativet **/TESTDBUPGRADE** för installationen. Om SQL Server-instansen som är värd för databas kopian inte är standard instansen anger du kommando rads argumenten för att identifiera den instans som är värd för plats databasens kopia.   

   Du kan till exempel ha en plats databas med databas namnet *SMS_ABC*. Du återställer en kopia av plats databasen till en instans som stöds av SQL Server med instans namnet *dbtest*. Använd följande kommando rad för att testa en uppgradering av den här kopian av plats databasen: **Setup. exe/TESTDBUPGRADE DBtest \ CM_ABC**.  

   Setup. exe finns på följande plats på käll mediet för Configuration Manager: **SMSSETUP\BIN\X64**.  

5. På instansen av SQL Server där du kör uppgraderings testet ska du övervaka *ConfigMgrSetup. log* i roten på system enheten för att se om det går att följa förloppet.  

    Om test uppgraderingen Miss lyckas åtgärdar du eventuella problem som rör uppgraderings felet för plats databasen. Skapa sedan en ny säkerhets kopia av plats databasen och testa uppgraderingen av den nya kopian av databasen.  



## <a name="next-steps"></a>Nästa steg
När test databasen har uppdaterats tar du bort den uppdaterade databasen. Den kan inte användas av en Configuration Manager webbplats. Du kan sedan återgå till den aktiva platsen och [påbörja installationen av uppdateringen](install-in-console-updates.md).
