---
title: Planera för migrering
titleSuffix: Configuration Manager
description: Lär dig mer om platser och hierarkier innan du migrerar data till en Configuration Manager aktuella Branch-målhierarkin.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b514e2bb0843801cfa6f0f307af8a5013fc3f9e6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719661"
---
# <a name="plan-for-migration-to-configuration-manager-current-branch"></a>Planera för migrering till Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Innan du migrerar data till en Configuration Manager aktuella gren måls hierarki, se till att du är bekant med platser och hierarkier i Configuration Manager. Mer information om platser och hierarkier finns i [grunderna i Configuration Manager](../../core/understand/fundamentals.md).  

Installera en Configuration Manager aktuella Branch-hierarkin som målhierarkin innan du migrerar data från en källhierarki som stöds.  

När du har installerat målhierarkin ställer du in de hanterings funktioner och funktioner som du vill använda i målhierarkin innan du börjar migrera data.  

Dessutom kan du behöva planera för överlappande mellan källhierarkin och målhierarkin. Du kan till exempel ställa in källhierarkin så att den använder samma nätverks platser eller gränser som målhierarkin, och sedan installerar du nya klienter i målhierarkin och använder automatisk platstilldelning. I det här scenariot, eftersom en nyinstallerad Configuration Manager-klient kan välja en plats för att ansluta från någon av hierarkierna, kan klienten felaktigt tilldela till källhierarkin. Därför bör du planera att tilldela varje ny klient i målhierarkin till en speciell plats i hierarkin i stället för att använda automatisk platstilldelning.  

Mer information om platstilldelning finns i [överväganden för klient platstilldelning](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) i [samverkan mellan olika versioner av Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

Använd följande artiklar för att få hjälp att planera hur du migrerar en källhierarki som stöds till en Configuration Manager målhierarkin:

-   [Krav för migrering](../../core/migration/prerequisites-for-migration.md)  

-   [Administratörschecklista för migreringsplanering](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Avgöra om data ska migreras till Configuration Manager aktuella grenen](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Planera en käll hierarkis strategi](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Administratörschecklista för migreringsplanering](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Planera en strategi för klient migrering](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Planera en strategi för migrering av innehålls distribution](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Planera för migrering av Configuration Manager objekt till Configuration Manager aktuella grenen](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Planera att övervaka migrerings aktivitet](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Planera för att slutföra migreringen](../../core/migration/planning-to-complete-migration.md)  
