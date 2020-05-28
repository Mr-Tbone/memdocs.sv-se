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
ms.openlocfilehash: ffa50d2cfb3095eb136128c09b74e9ee6a4eb501
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904405"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Diagnostik-och användnings data för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager samlar in diagnostik-och användnings data om sig själv, som används av Microsoft för att förbättra installations upplevelsen, kvaliteten och säkerheten i framtida versioner.  

Varje Configuration Manager hierarki möjliggör diagnostik-och användnings data. Den består av SQL Server frågor som körs veckovis på varje primär plats och på den centrala administrations platsen (CAS). När hierarkin använder en certifikat utfärdare replikeras underordnade primära platser sina data till certifikat utfärdarna. På platsen på den översta nivån i hierarkin skickar [tjänst anslutnings punkten](../../servers/deploy/configure/about-the-service-connection-point.md) den här informationen när den söker efter uppdateringar. Om tjänst anslutnings punkten är i offlineläge överför du informationen med hjälp av [tjänst anslutnings verktyget](../../servers/manage/use-the-service-connection-tool.md).

> [!NOTE]  
> Configuration Manager samlar endast in data från platsens SQL Server-databas och samlar inte in data direkt från klienter eller plats servrar.  

Mer information finns i [Microsofts sekretess policy](https://privacy.microsoft.com/privacystatement).  

> [!div class="nextstepaction"]
> [Så använder Microsoft diagnostik och användningsdata](how-diagnostics-and-usage-data-is-used.md)
