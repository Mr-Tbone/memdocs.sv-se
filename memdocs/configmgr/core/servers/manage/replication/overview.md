---
title: Felsöka SQL-replikering
titleSuffix: Configuration Manager
description: Använd de här diagrammen för att förstå och felsöka SQL-replikering mellan Configuration Manager-platser
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 202a3360b5e04d66ada0d3b47ddd4638c2197167
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720473"
---
# <a name="troubleshoot-sql-replication"></a>Felsöka SQL-replikering

I en hierarki med flera platser använder Configuration Manager SQL-replikering för att överföra data mellan platser. Mer information finns i [databasreplikering](../../../plan-design/hierarchy/database-replication.md).

Använd de här diagrammen för att få bättre förståelse och felsöka problem med SQL-replikering.

- [SQL-replikering](sql-replication.md)
- [SQL-konfiguration](sql-configuration.md)
- [SQL-prestanda](sql-performance.md)
- [Ominitiering av SQL-replikering (ominitiering)](sql-replication-reinit.md)
- [Ominitiering av globala data](global-data-reinit.md)
- [Ominitiering av webbplatsdata](site-data-reinit.md)
- [Saknat ominiteringsmeddelande](reinit-missing-message.md)

Dessa fel söknings diagram är sammankopplade. Använd följande diagram för att förstå deras relationer:

![Översikts diagram över processen för fel sökning av SQL-replikering](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

Mer information finns i följande blogg serier från Microsoft Support:

- [Intern synkronisering av ConfigMgr-DRS](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317)
- [ConfigMgr 2012 tjänsten Datareplikering (DRS) friutnyttjas](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916)
- [ConfigMgr 2012 DRS – felsöka vanliga frågor och svar](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934)
- [Inbyggda ConfigMgr 2012 DRS-initieringar](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948)
- [ConfigMgr 2012: problem med DRS och SQL Service Broker-certifikat](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910)
