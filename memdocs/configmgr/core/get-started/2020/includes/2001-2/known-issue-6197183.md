---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: fca1d884b75380f90a2e2e3cdc2fb0cac357b6b5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703123"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> Det går inte att skapa eller redigera samlingar

<!--6197183-->
I den här versionen av Technical Preview-grenen kan du inte skapa en ny samling. Du kan inte heller redigera egenskaperna för en befintlig användar samling.

Undvik det här problemet genom att använda Configuration Manager PowerShell-cmdletar för att skapa nya samlingar och redigera befintliga användar samlingar. Några av de tillgängliga cmdletarna för att hantera samlingar är:

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)