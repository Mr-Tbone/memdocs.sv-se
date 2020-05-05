---
title: SQL-replikering
titleSuffix: Configuration Manager
description: Använd det här diagrammet för att starta fel sökning av SQL-replikering mellan Configuration Manager-platser
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a25218e53313b7a8c3192959b54b65d2a32fae7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717526"
---
# <a name="sql-replication"></a>SQL-replikering

I en hierarki med flera platser använder Configuration Manager SQL-replikering för att överföra data mellan platser. Mer information finns i [databasreplikering](../../../plan-design/hierarchy/database-replication.md).

Använd följande diagram för att starta fel sökning av SQL-replikering när en länk Miss lyckas:

![Diagram för att felsöka SQL-replikering](media/sql-replication.svg)

## <a name="queries"></a>Frågor

I det här diagrammet används följande frågor:

### <a name="check-if-the-replication-group-link-is-in-degraded-or-failed-state"></a>Kontrol lera att länken för replikeringsgruppen är i ett försämrat tillstånd eller felaktigt tillstånd

```sql
SELECT * FROM RCM_ReplicationLinkStatus
WHERE Status IN (8, 9)
```

### <a name="check-if-replication-group-link-is-recently-calculated"></a>Kontrol lera om replikeringslänk har beräknats nyligen

```sql
DECLARE @cutoffTime DATETIME
SELECT @cutoffTime = DATEADD(minute, -30, GETUTCDATE())
SELECT * FROM RCM_ReplicationLinkStatus
WHERE UpdateTime >@cutoffTime
```

### <a name="check-sql-maintenance-mode"></a>Kontrol lera underhålls läge för SQL

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

## <a name="next-steps"></a>Nästa steg

- [Ominitiering av SQL-replikering (ominitiering)](sql-replication-reinit.md)
- [SQL-prestanda](sql-performance.md)
- [SQL-konfiguration](sql-configuration.md)
