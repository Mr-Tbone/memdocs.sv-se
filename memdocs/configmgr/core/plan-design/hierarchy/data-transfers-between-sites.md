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
ms.openlocfilehash: c3b74ceab892c67abbd56e8cb2a5c123374a92be
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663319"
---
# <a name="data-transfers-between-sites"></a>Dataöverföringar mellan platser

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager använder *filbaserad replikering* och *databasreplikering* för att överföra olika typer av information mellan platser. Lär dig mer om hur Configuration Manager flyttar data mellan platser och hur du kan hantera överföringen av data i nätverket.  

## <a name="types-of-replication"></a>Typer av replikering

### <a name="file-based-replication"></a><a name="bkmk_fileroute" /></a> File-based replication

Configuration Manager använder filbaserad replikering för att överföra filbaserade data mellan platser i hierarkin. Dessa data omfattar program och paket som du vill distribuera till distributions platser på underordnade platser. Den hanterar också obearbetade identifierings data poster som platsen överför till dess överordnade plats och sedan processer.  

Mer information finns i [filbaserad replikering](file-based-replication.md).

### <a name="database-replication"></a><a name="bkmk_dbrep" /></a> Database replication

Configuration Manager databasreplikering använder SQL Server för att överföra data. Den här metoden använder den här metoden för att slå samman ändringar i dess plats databas med informationen från databasen på andra platser i hierarkin.

Mer information finns i [databasreplikering](database-replication.md).

Information om hur du felsöker SQL-replikering finns i [FELSÖKA SQL-replikering](../../servers/manage/replication/overview.md).

## <a name="see-also"></a>Se även

[Övervaka replikering](../../servers/manage/monitor-replication.md)
