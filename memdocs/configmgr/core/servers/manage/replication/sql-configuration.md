---
title: SQL-konfiguration
titleSuffix: Configuration Manager
description: Använd det här diagrammet för att starta fel sökning av SQL-konfiguration för Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b909d992dc16b6e786c62143347ed420d913dbc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723231"
---
# <a name="sql-configuration"></a>SQL-konfiguration

I en hierarki med flera platser använder Configuration Manager SQL-replikering för att överföra data mellan platser. Mer information finns i [databasreplikering](../../../plan-design/hierarchy/database-replication.md).

Använd följande diagram för att starta fel sökning av SQL-konfiguration som är relaterad till SQL Service Broker:

![Diagram för att felsöka SQL-konfiguration](media/sql-configuration.svg)

## <a name="queries"></a>Frågor

Det här diagrammet innehåller följande frågor och åtgärder:

### <a name="check-if-sql-can-deliver-ssb-messages"></a>Kontrol lera om SQL kan leverera SSB-meddelanden

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## <a name="remediation-actions"></a>Åtgärder

### <a name="remediate-the-issues-reported-from-transmission_status"></a>Åtgärda problemen som rapporter ATS från transmission_status

Vanliga problem:

- Konfigurering av brandvägg
- Konfiguration av nätverk
- SSB-certifikatet är felkonfigurerat

### <a name="run-sql-profiler-to-trace-ssb-events"></a>Kör SQL profileraren för att spåra SSB-händelser

Kör SQL profileraren på certifikat utfärdaren och den primära plats databasen för att spåra händelser relaterade till SQL-Service Broker:

- **Audit Broker-inloggning**
- **Gransknings service konversation**
- Händelser i **service** kategori
