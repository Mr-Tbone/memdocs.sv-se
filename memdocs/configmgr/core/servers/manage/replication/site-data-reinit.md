---
title: Ominitiering av webbplatsdata
titleSuffix: Configuration Manager
description: Använd det här diagrammet för att starta fel sökning av ominitiering av SQL-replikering för plats data i en Configuration Manager hierarki
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19741d45-2d42-438e-a9f3-15bb365d63ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a336bdf323fbb81a16082e9c308577763a7c104
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078606"
---
# <a name="troubleshoot-site-data-reinit"></a>Felsöka plats data ominitiering

I en hierarki med flera platser använder Configuration Manager SQL-replikering för att överföra data mellan platser. Mer information finns i [databasreplikering](../../../plan-design/hierarchy/database-replication.md).

Använd följande diagram för att starta fel sökning av ominitiering av SQL-replikering (ominitiering) för plats data i en Configuration Manager hierarki:

![Diagram för fel sökning av ominitiering av plats data](media/site-data-reinit.svg)

## <a name="queries"></a>Frågor

I det här diagrammet används följande frågor:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Kontrol lera om plats replikeringen inte har avinitierats

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Site'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>Hämta TrackingGuid & status från CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Hämta TrackingGuid & status från den primära platsen

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-primary-site-isnt-in-maintenance-mode"></a>Kontrol lera att den primära platsen inte är i underhålls läge

```sql
SELECT * FROM ServerData
WHERE SiteStatus = 125
AND SiteCode=dbo.fnGetSiteCode()
AND ServerRole=N'Peer'
```

### <a name="check-request-status-for-the-tracking-id"></a>Kontrol lera status för begäran för spårnings-ID

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Nästa steg

- [Saknat ominiteringsmeddelande](reinit-missing-message.md)
- [Ominitiering av globala data](global-data-reinit.md)
