---
title: Ominitiering av globala data
titleSuffix: Configuration Manager
description: Använd det här diagrammet för att starta fel sökning av ominitiering av SQL-replikering för globala data i en Configuration Manager-hierarki
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fed8a5b257591aa95fcd53b4e12a82249fce762
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713634"
---
# <a name="troubleshoot-global-data-reinit"></a>Felsöka globala data ominitieringar

I en hierarki med flera platser använder Configuration Manager SQL-replikering för att överföra data mellan platser. Mer information finns i [databasreplikering](../../../plan-design/hierarchy/database-replication.md).

Använd följande diagram för att starta fel sökning av ominitiering av SQL-replikering (ominitiering) för globala data i en Configuration Manager-hierarki:

![Diagram för att felsöka globala data ominitieringar](media/global-data-reinit.svg)

## <a name="queries"></a>Frågor

I det här diagrammet används följande frågor:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Kontrol lera om plats replikeringen inte har avinitierats

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Hämta TrackingGuid & status från den primära platsen

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>Hämta TrackingGuid & status från CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>Kontrol lera status för begäran för spårnings-ID

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Nästa steg

- [Saknat ominiteringsmeddelande](reinit-missing-message.md)
