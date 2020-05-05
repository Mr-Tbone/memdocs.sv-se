---
title: Saknat ominiteringsmeddelande
titleSuffix: Configuration Manager
description: Använd det här diagrammet för att starta fel sökning av ett saknat meddelande med ominitiering av SQL-replikering i Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e640c3dd756d96a58e8b54d6056d2adbb7bb99c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720466"
---
# <a name="reinit-missing-message"></a>Saknat ominiteringsmeddelande

I en hierarki med flera platser använder Configuration Manager SQL-replikering för att överföra data mellan platser. Mer information finns i [databasreplikering](../../../plan-design/hierarchy/database-replication.md).

Använd följande diagram för att starta fel sökning av ett saknat meddelande med ominitiering av SQL-replikering (ominitiering):

![Diagram för att felsöka meddelande om att ominitiering saknas](media/reinit-missing-message.svg)

## <a name="queries"></a>Frågor

I det här diagrammet används följande frågor:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Kontrol lera om plats replikeringen inte har avinitierats

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-subscriber-site"></a>Hämta TrackingGuid & status från prenumerantens webbplats

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-the-publishing-site"></a>Hämta TrackingGuid & status från publicerings platsen

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## <a name="remediation-actions"></a>Åtgärder

### <a name="version-1902-and-later"></a>Version 1902 och senare

Kör [Replikeringslänkanalys](../monitor-replication.md#BKMK_RLA)för att identifiera problemet och ominitieringen.

### <a name="version-1810-and-earlier"></a>Version 1810 och tidigare

Kör följande SQL-fråga för att hämta `ReplicationGroupID`:

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

Använd sedan `InitializeData` metoden i `SMS_ReplicationGroup` WMI-klassen med följande värden:

- ReplicationGroupID: från SQL-frågan ovan
- SiteCode1: överordnad plats
- SiteCode2: underordnad plats

Mer information finns [i InitializeData-metoden i klass SMS_ReplicationGroup](../../../../develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup.md).

#### <a name="example"></a>Exempel

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## <a name="next-steps"></a>Nästa steg

- [Ominitiering av SQL-replikering (ominitiering)](sql-replication-reinit.md)
