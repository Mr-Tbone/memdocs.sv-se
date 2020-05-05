---
title: Dataöverföringar mellan platser
titleSuffix: Configuration Manager
description: Lär dig hur Configuration Manager flyttar data mellan platser och hur du kan hantera överföringen av data i nätverket.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6b6d4eab77d0543f9001cef2c1e2b618ba3e4328
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720214"
---
# <a name="data-transfers-between-sites"></a>Dataöverföringar mellan platser

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager använder *filbaserad replikering* och *databasreplikering* för att överföra olika typer av information mellan platser. Lär dig mer om hur Configuration Manager flyttar data mellan platser och hur du kan hantera överföringen av data i nätverket.  

## <a name="types-of-replication"></a>Typer av replikering

### <a name="file-based-replication"></a><a name="bkmk_fileroute" />Filbaserad replikering

Configuration Manager använder filbaserad replikering för att överföra filbaserade data mellan platser i hierarkin. Dessa data omfattar program och paket som du vill distribuera till distributions platser på underordnade platser. Den hanterar också obearbetade identifierings data poster som platsen överför till dess överordnade plats och sedan processer.  

Mer information finns i [filbaserad replikering](file-based-replication.md).

### <a name="database-replication"></a><a name="bkmk_dbrep" />Databasreplikering

Configuration Manager databasreplikering använder SQL Server för att överföra data. Den här metoden använder den här metoden för att slå samman ändringar i dess plats databas med informationen från databasen på andra platser i hierarkin.

Mer information finns i [databasreplikering](database-replication.md).

Information om hur du felsöker SQL-replikering finns i [FELSÖKA SQL-replikering](../../servers/manage/replication/overview.md).

## <a name="see-also"></a>Se även

[Övervaka replikering](../../servers/manage/monitor-replication.md)
