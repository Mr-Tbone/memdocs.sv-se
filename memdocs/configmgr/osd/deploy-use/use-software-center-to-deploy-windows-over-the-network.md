---
title: Använda Software Center för att distribuera Windows via nätverket
titleSuffix: Configuration Manager
description: Distribuera ett operativ system från Software Center för att uppdatera en befintlig dator med en ny version av Windows eller uppgradera Windows till den senaste versionen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6bd10240ebc7ec478efe122bf7f8a45d3afe9f10
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124609"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Använd Software Center för att distribuera Windows via nätverket med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan göra en aktivitetssekvens som installerar ett operativ system som är tillgängligt i Software Center. En användare kan köra en aktivitetssekvens från Software Center för följande distributions scenarier för operativ system:

- [Uppdatera en befintlig dator med en ny version av Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Uppgradera Windows till den senaste versionen](upgrade-windows-to-the-latest-version.md)

- [Skapa en aktivitetssekvens för annat än distributioner av operativsystem](create-a-task-sequence-for-non-operating-system-deployments.md)

Slutför stegen i ett av de här distributions scenarierna för operativ systemet. Använd sedan följande avsnitt för att förbereda för distributioner som är tillgängliga i Software Center.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Distribuera aktivitetssekvensen

Distribuera aktivitetssekvensen till en mål samling. Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md).

På sidan **distributions inställningar** i distributionen väljer du något av följande alternativ för inställningen **gör tillgängligt för följande** :

- Endast Configuration Manager klienter

- Configuration Manager-klienter, media och PXE

Konfigurera även om distributionen är obligatorisk eller tillgänglig:

- Nödvändig distribution: nödvändiga distributioner gör aktivitetssekvensen tillgänglig i Software Center. Den startas automatiskt vid den konfigurerade tids gränsen.

- Tillgänglig distribution: aktivitetssekvensen är tillgänglig i Software Center och en användare kan installera den på begäran.

När du har skapat distributionen kommer klienter i mål samlingen att Visa aktivitetssekvensen i Software Center.

## <a name="next-steps"></a>Nästa steg

[Användarupplevelser för distribution av operativsystem](../understand/user-experience.md#software-center)
