---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 668db6aa10fbee0a078eef04f0560973e5ed9454
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81716119"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a>Aktivitetssekvenser är inte tillgängliga för PXE eller media

<!--5578298-->
Om du distribuerar en aktivitetssekvens för PXE eller media (USB eller DVD) får klienten ingen princip. Följande meddelande är i **Smsts. log**:

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>Lösning

Starta aktivitetssekvensen från Software Center.
