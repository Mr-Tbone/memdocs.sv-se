---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: 0db30a8fdc96bc1e1d2d1ff2a059eca8d454d48e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712094"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a>Det går inte att skapa eller redigera samlingar

<!--6197183-->
I den här versionen av Technical Preview-grenen kan du inte skapa en ny samling. Du kan inte heller redigera egenskaperna för en befintlig användar samling.

Undvik det här problemet genom att använda Configuration Manager PowerShell-cmdletar för att skapa nya samlingar och redigera befintliga användar samlingar. Några av de tillgängliga cmdletarna för att hantera samlingar är:

- [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)
