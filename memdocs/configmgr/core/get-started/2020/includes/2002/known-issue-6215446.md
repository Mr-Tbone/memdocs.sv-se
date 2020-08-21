---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: d887f842b789b41260a49b149b61f28741937613
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703030"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a> Det går inte att ta bort samlingar

<!--6245446-->
I den här versionen av Technical Preview-grenen kan du inte ta bort samlingar.

Undvik det här problemet genom att använda följande Configuration Manager PowerShell-cmdlet för att ta bort samlingar:

- [Remove-CMCollection](/powershell/module/configurationmanager/remove-cmcollection?view=sccm-ps)