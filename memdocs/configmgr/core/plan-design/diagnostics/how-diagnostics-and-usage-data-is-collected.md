---
title: Data insamling för diagnostik
titleSuffix: Configuration Manager
description: Lär dig mer om hur Configuration Manager samlar in diagnostik-och användnings data om sig själv.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca40891c840e954f2828833c179f01bcbc6e7448
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709539"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Hur Configuration Manager samlar in diagnostik-och användnings data

*Gäller för: Configuration Manager (aktuell gren)*

För att samla in diagnostik-och användnings data för Configuration Manager kör varje primär plats SQL Server frågor varje vecka. Data replikeras till den centrala administrationswebbplatsen i en hierarki med flera platser.  

På platsen på den översta nivån i en hierarki skickar tjänst anslutnings punkten den här informationen när den söker efter uppdateringar. Tjänst anslutnings punktens läge avgör hur data överförs:

- **Online**: en gång i veckan skickar tjänst anslutnings punkten automatiskt diagnostik-och användnings data till moln tjänsten.

- **Offline**: du överför diagnostik-och användnings data manuellt med [tjänst anslutnings verktyget](../../servers/manage/use-the-service-connection-tool.md).

Mer information finns i [om tjänst anslutnings punkten](../../servers/deploy/configure/about-the-service-connection-point.md).

> [!div class="nextstepaction"]
> [Visa diagnostik- och användningsdata](view-diagnostics-and-usage-data.md)
