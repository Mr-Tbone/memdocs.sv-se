---
title: Inaktuell för plats servrar
titleSuffix: Configuration Manager
description: Lär dig mer om de produkter och operativ system som Configuration Manager inte längre stöder för plats servrar.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2b6f9dfae2eaa4e7fac4cc9b059b608de3c1386a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719479"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Borttaget och inaktuellt för Configuration Manager plats servrar

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln beskrivs produkter och operativ system som tas bort från stöd för Configuration Manager plats servrar, eller som kommer att tas bort i en kommande uppdatering (föråldrad). Det ger ett tidigt meddelande om framtida ändringar som kan påverka din användning av Configuration Manager.  

Den här informationen kan ändras i framtiden. Det kanske inte omfattar varje föråldrad funktion, produkt eller operativ system.  

## <a name="server-os"></a>Server-OS  

|Operativsystem|Första meddelande om utfasning|Support indragen|
|-|-|-|
|Windows Server 2008 R2 med SP1|10 juli 2015| Version 1702|
|Windows Server 2008 med SP2|10 juli 2015|Version 1511|

## <a name="sql-server"></a>SQL Server

|SQL Server-versioner|Första meddelande om utfasning|Support indragen|
|-|-|-|
|SQL Server 2008 R2|10 juli 2015|Version 1702|
|SQL Server 2008|10 juli 2015|Version 1511|

Om du behöver uppgradera din version av SQL Server rekommenderar vi följande metoder från enkla till mer komplexa:

1. [Uppgradera SQL Server på plats](../../../servers/manage/upgrade-on-premises-infrastructure.md#BKMK_SupConfigUpgradeDBSrv) (rekommenderas).  

2. Installera en ny version av SQL Server på en ny dator. Om du sedan vill peka plats servern på den nya SQL Server [använder du alternativet för databas flyttning](../../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) i Configuration Manager installationen.  

3. Använd [säkerhets kopiering och återställning](../../../servers/manage/backup-and-recovery.md).  

## <a name="next-steps"></a>Nästa steg

Mer information finns i följande artiklar:

- [Borttaget och inaktuellt](removed-and-deprecated.md)  

- [Microsoft Support livs cykel](https://support.microsoft.com/lifecycle)  

- [Stöd för aktuella gren versioner av Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)  
