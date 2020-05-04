---
title: Importera och exportera program
titleSuffix: Configuration Manager
description: Lär dig hur du importerar och exporterar program i Configuration Manager att dela mellan olika hierarkier.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b4ed1c10e23b75dc4478a0409d197015c98aff8b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710218"
---
# <a name="import-and-export-applications"></a>Importera och exportera program

*Gäller för: Configuration Manager (aktuell gren)*

Använd Configuration Manager för att importera och exportera program mellan två hierarkier. Du kan till exempel kopiera ett program från en test miljö till en produktions miljö.

## <a name="export"></a>Exportera

1. I Configuration Manager-konsolen väljer du noden **program** . I gruppen Skapa i menyfliksområdet väljer du **Exportera program**.
1. På sidan **Allmänt** anger du en sökväg till en ny zip-fil att exportera till. Du kan också ange om du vill exportera *beroenden, ersättnings förhållanden, villkor och virtuella miljöer*samt *innehåll för de valda programmen och beroenden*.  Ange eventuella administratörs kommentarer, om det behövs, och välj **Nästa**.
1. Kontrol lera att programmet och eventuella beroenden visas på sidan **relaterade objekt** och välj **Nästa**.
1. På sidan Sammanfattning väljer du **Nästa**.
1. När processen har slutförts skapas ZIP-filen och du kan stänga guiden.

> [!IMPORTANT]
> Om du vill kopiera det här programmet till en annan miljö ska du ta både ZIP-filen och mappen som medföljer. ZIP-filen måste finnas i samma katalog som den skapade mappen.

## <a name="import"></a>Importera

> [!NOTE]
> Du kan bara importera program från UNC-sökvägar, det går inte att importera direkt från den lokala disken.

1. I Configuration Manager-konsolen väljer du noden **program** . I gruppen Skapa i menyfliksområdet väljer du **importera program**.
1. Välj den ZIP-fil som du vill importera och välj **Nästa**.
1. I fönstret fil innehåll visas vad som händer när du importerar programmet. Välj **Nästa**.
1. Granska sammanfattnings skärmen och välj **Nästa**.
1. Stäng guiden. Programmet är nu tillgängligt på platsen.

## <a name="see-also"></a>Se även
 
Automatisera import och export av program med hjälp av PowerShell.

* [Importera – CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication)
* [Exportera – CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmapplication)
