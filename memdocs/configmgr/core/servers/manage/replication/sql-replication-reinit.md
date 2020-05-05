---
title: Ominitiering av SQL-replikering
titleSuffix: Configuration Manager
description: Använd det här diagrammet för att börja felsöka ominitiering av SQL-replikering mellan Configuration Manager-platser
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ce4a1ca8-6433-4447-819f-19dd5faa6f46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6207ed4eeeef892de38c85096d2cc80189214d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078572"
---
# <a name="sql-replication-reinit"></a>Ominitiering av SQL-replikering

I en hierarki med flera platser använder Configuration Manager SQL-replikering för att överföra data mellan platser. Mer information finns i [databasreplikering](../../../plan-design/hierarchy/database-replication.md).

Använd följande diagram för att börja felsöka ominitiering av SQL-replikering (ominitiering):

![Diagram för att felsöka ominitiering av SQL-replikering](media/sql-replication-reinit.svg)

## <a name="queries"></a>Frågor

I det här diagrammet används följande frågor:

### <a name="check-if-site-is-in-maintenance-mode"></a>Kontrol lera om webbplatsen är i underhålls läge

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>Kontrol lera vilken replikeringsgrupp som inte har slutförts ominitiering

```sql
SELECT * FROM RCM_DrsInitializationTracking
WHERE InitializationStatus NOT IN (6,7)
```

### <a name="check-global-data"></a>Kontrol lera globala data

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'GLOBAL'
```

### <a name="check-site-data"></a>Kontrol lera plats data

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

## <a name="next-steps"></a>Nästa steg

- [Ominitiering av globala data](global-data-reinit.md)
- [Ominitiering av webbplatsdata](site-data-reinit.md)
- [SQL-konfiguration](sql-configuration.md)
