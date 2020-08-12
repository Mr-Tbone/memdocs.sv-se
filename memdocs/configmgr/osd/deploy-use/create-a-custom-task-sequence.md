---
title: Skapa en anpassad aktivitetssekvens
titleSuffix: Configuration Manager
description: Redigera en anpassad aktivitetssekvens i Configuration Manager för att lägga till steg i aktivitetssekvensen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f390c3857ad5a277002839c4c14ab1307d9ab281
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125584"
---
# <a name="create-a-custom-task-sequence-with-configuration-manager"></a>Skapa en anpassad aktivitetssekvens med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du skapar en anpassad aktivitetssekvens i Configuration Manager innehåller den inga steg i aktivitetssekvensen. När du har skapat aktivitetssekvensen redigerar du den och lägger till de steg du behöver för att kunna lägga till aktivitetssekvensen.  

## <a name="create-a-custom-task-sequence"></a><a name="BKMK_CustomTS"></a>Skapa en anpassad aktivitetssekvens

Använd följande procedur för att skapa en anpassad aktivitetssekvens:

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj noden **aktivitetssekvenser** .  

1. Välj **skapa**aktivitetssekvens i gruppen **skapa** på fliken **Start** i menyfliksområdet. Den här åtgärden startar guiden skapa aktivitetssekvens.  

1. På sidan **Skapa en ny aktivitetssekvens** väljer du **Skapa en ny anpassad aktivitetssekvens**.  

1. På sidan **information om aktivitetssekvens** anger du:

    - Ett namn på aktivitetssekvensen
    - En beskrivning av aktivitetssekvensen
    - En valfri start avbildning för aktivitetssekvensen som ska användas

När du har slutfört guiden skapa aktivitetssekvens lägger Configuration Manager till den anpassade aktivitetssekvensen i noden **aktivitetssekvenser** . Du kan nu redigera den här aktivitetssekvensen om du vill lägga till aktivitetssekvenssteg i den.  

## <a name="see-also"></a>Se även

En lista över tillgängliga steg i aktivitetssekvensen finns i [stegen i aktivitetssekvensen](../understand/task-sequence-steps.md).  

Mer information om hur du redigerar en aktivitetssekvens finns i [använda redigeraren för aktivitetssekvens](../understand/task-sequence-editor.md).  

Oftast använder du aktivitetssekvenser för att automatisera uppgifter för operativ Systems distribution, men du kan skapa en anpassad aktivitetssekvens för att automatisera olika typer av aktiviteter. Mer information finns i [skapa en aktivitetssekvens för distributioner som inte är operativ system](create-a-task-sequence-for-non-operating-system-deployments.md).

Från och med version 2002 installerar du komplexa program med hjälp av aktivitetssekvenser via program modellen. Lägg till en distributions typ till en app som är en aktivitetssekvens, antingen för att installera eller avinstallera appen. Mer information finns i [skapa Windows-program](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

## <a name="next-steps"></a>Nästa steg

[Distribuera aktivitetssekvensen](deploy-a-task-sequence.md)
