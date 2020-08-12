---
title: Skapa en avbildning för en OEM-tillverkare i fabriken eller lokal anläggning
titleSuffix: Configuration Manager
description: Använd förinstallerade medie distributioner för att minska nätverks trafiken medan du distribuerar ett operativ system till en dator som inte är helt etablerad.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15145cccf73e517d0e49444fbdaf834de342865e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125448"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Skapa en avbildning för en OEM-tillverkare i fabriken eller ett lokalt lager med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med förinstallerade medie distributioner i Configuration Manager kan du distribuera ett operativ system till en dator som inte är helt etablerad. Det förinstallerade mediet är en WIM-fil (Windows Image). Tillverkaren (OEM) kan installera den på en dator utan operativ system, eller så kan du använda den i ett fristående Center som är separat från produktions miljön.

Den här distributions metoden kan minska nätverks trafiken, eftersom start avbildningen och operativ system avbildningen redan finns på mål datorn. Du kan ange program, paket och driv rutins paket så att de också ingår i det för beredda mediet. När operativ systemet har installerats på datorn kontrollerar aktivitetssekvensen först det förinstallerade cacheminnet för program, paket eller driv rutins paket. Om det inte går att hitta det nödvändiga innehållet, eller om det finns en nyare revision tillgänglig online, laddar aktivitetssekvensen ned innehållet från en distributions plats.

Använd förinstallerade medier i följande distributions scenarier för operativ system:

- [Installera en ny version av Windows på en ny dator (utan operativsystem)](install-new-windows-version-new-computer-bare-metal.md)

- [Ersätta en befintlig dator och överföra inställningar](replace-an-existing-computer-and-transfer-settings.md)

Slutför stegen i något av de här distributions scenarierna för operativ systemet. Använd sedan följande avsnitt för att förbereda för och skapa de förinstallerade medierna.

## <a name="configure-deployment-settings"></a>Konfigurera distributionsinställningar

På sidan **distributions inställningar** i distributionen väljer du något av följande alternativ för inställningen **gör tillgängligt för följande** :

- Configuration Manager klienter, media och PXE

- Endast media och PXE

- Endast media och PXE (dolt)

## <a name="create-the-prestaged-media"></a>Skapa förinstallerade medier

Skapa den förinstallerade mediefilen som ska skickas till OEM eller den lokala anläggningen. Mer information finns i [Skapa förinstallerade media med Configuration Manager](create-prestaged-media.md).

## <a name="send-the-prestaged-media-file"></a>Skicka den förinstallerade medie filen

Skicka mediet till OEM-tillverkaren eller ditt lokala lager för att förinstallera på datorerna. De tillämpar avbildnings filen på en formaterad hård disk på datorn.

## <a name="deliver-the-computer"></a>Leverera datorn

När du levererar datorn till en användare och aktiverar den för första gången:

1. Datorn startar med den förinstallerade start avbildningen.

1. Den kontrollerar en hash på det förinstallerade mediet för att kontrol lera att den är giltig.

1. Datorn ansluter till hanterings platsen för att de tillgängliga aktivitetssekvenserna ska kunna slutföra processen.

## <a name="next-steps"></a>Nästa steg

[Användarupplevelser för distribution av operativsystem](../understand/user-experience.md)
