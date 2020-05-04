---
title: Diagnostik och användningsdata
titleSuffix: Configuration Manager
description: Lär dig mer om diagnostik-och användnings data som Configuration Manager samlar in om sig själv.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6fff68eaad52f753d27971562a4bbfaa47a6cf6e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711569"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Diagnostik-och användnings data för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager samlar in diagnostik-och användnings data om sig själv, som används av Microsoft för att förbättra installations upplevelsen, kvaliteten och säkerheten i framtida versioner.  

Varje Configuration Manager hierarki möjliggör diagnostik-och användnings data. Den består av SQL Server frågor som körs veckovis på varje primär plats och på den centrala administrations platsen (CAS). När hierarkin använder en certifikat utfärdare replikeras underordnade primära platser sina data till certifikat utfärdarna. På platsen på den översta nivån i hierarkin skickar [tjänst anslutnings punkten](../../servers/deploy/configure/about-the-service-connection-point.md) den här informationen när den söker efter uppdateringar. Om tjänst anslutnings punkten är i offlineläge överför du informationen med hjälp av [tjänst anslutnings verktyget](../../servers/manage/use-the-service-connection-tool.md).

> [!NOTE]  
> Configuration Manager samlar endast in data från platsens SQL Server-databas och samlar inte in data direkt från klienter eller plats servrar.  

Mer information finns i [Microsofts sekretess policy](https://go.microsoft.com/fwlink/?LinkID=626527).  

> [!div class="nextstepaction"]
> [Så använder Microsoft diagnostik och användningsdata](how-diagnostics-and-usage-data-is-used.md)
