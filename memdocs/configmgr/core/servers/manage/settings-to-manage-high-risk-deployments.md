---
title: Hantera högriskdistributioner
titleSuffix: Configuration Manager
description: Konfigurera inställningarna för distributions verifierings platsen i Configuration Manager för att varna administratörer om de skapar en högrisk distribution.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f1498c383f9b02f7f322de3ba5708351e84c3b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719990"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>Inställningar för att hantera högrisk distributioner för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med Configuration Manager kan du konfigurera plats inställningar för *distributions verifiering* . De här inställningarna varnar administratörer om de skapar en högrisk distribution av aktivitetssekvensdistribution. En högriskdistribution:  

- En distribution som installeras automatiskt  

- kan orsaka oönskade resultat.  

En aktivitetssekvens som till exempel är **obligatorisk** och som distribuerar ett operativ system betraktas som högrisk.  

> [!WARNING]
> Om du använder PXE-distributioner och konfigurerar enhets maskin vara med nätverkskortet som den första startenheten kan de här enheterna automatiskt starta en aktivitetssekvens för operativ system distribution utan användar interaktion. Distributions verifiering hanterar inte den här konfigurationen. Även om den här konfigurationen kan förenkla processen och minska användar interaktionen, medför enheten större risk för oavsiktlig återavbildning.

## <a name="deployment-verification-settings"></a><a name="bkmk_settings"></a>Verifierings inställningar för distribution

För att minska risken för en oönskad högrisk distribution kan du konfigurera storleks gränser i dessa inställningar för distributions verifiering:  

- **Storleks gränser för samlingar**: när du skapar en distribution döljer du samlingar som innehåller fler klienter än din gräns.  

  - **Standard storlek**: när du skapar en distribution döljer den här inställningen samlingar som standard som innehåller fler klienter än den här gränsen. Du kan fortfarande se dessa samlingar när du skapar distributionen, men de är dolda som standard. Standardvärdet är **100**. Om du vill ignorera den här inställningen anger du värdet **0**.  

  - **Maximal storlek**: när du skapar en distribution döljer den här inställningen alltid samlingar med fler klienter än den här gränsen. Standardvärdet är **0**, vilket ignorerar den här inställningen. Värdet **Maximal storlek** måste vara större än värdet **Standardstorlek** .  

    Till exempel ställer du in **standard storleken** på 100 och **maximal storlek** till 1000. När du skapar en distribution med hög risk visar fönstret **Välj samling** endast samlingar som innehåller färre än 100 klienter. Om du avmarkerar inställningen för att **dölja samlingar med ett större antal medlemmar än platsens minsta storleks konfiguration**, visar fönstret samlingar som innehåller färre än 1000 klienter.  

- **Samlingar med plats system servrar**: när mål samlingen innehåller en dator med en plats system roll, blockera distributioner eller Kräv verifiering innan du skapar distributionen. När en distribution blockeras väljer du en annan samling som uppfyller kriterierna för distributions verifiering för att fortsätta att skapa distributionen.  

> [!NOTE]
> Distributioner med hög risk är alltid begränsade till anpassade samlingar, samlingar som du skapar och den inbyggda samlingen **Okända datorer** . När du skapar en distribution med hög risk kan du inte välja en inbyggd samling, till exempel **alla system**.  

## <a name="configure-deployment-verification"></a>Konfigurera distributions verifiering

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**, Välj **platser**och välj sedan den primära plats som ska konfigureras.

2. I menyfliksområdet väljer du **Egenskaper**och växlar sedan till fliken **distributions verifiering** .

3. Konfigurera de [Inställningar](#bkmk_settings) som du vill använda och välj sedan **OK** för att spara konfigurationen och stänga egenskaperna.

## <a name="next-steps"></a>Nästa steg

[Hantera aktivitetssekvenser – inställningar med hög effekt](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#high-impact-settings)

[Konfigurera platser och hierarkier](../deploy/configure/configure-sites-and-hierarchies.md)
