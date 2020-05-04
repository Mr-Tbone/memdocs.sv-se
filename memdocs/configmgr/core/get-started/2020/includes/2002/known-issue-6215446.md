---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: 54e00688c1375f9ec54ada86d2b2c4b9347d5405
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711919"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a>Det går inte att ta bort samlingar

<!--6245446-->
I den här versionen av Technical Preview-grenen kan du inte ta bort samlingar.

Undvik det här problemet genom att använda följande Configuration Manager PowerShell-cmdlet för att ta bort samlingar:

- [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection?view=sccm-ps)
