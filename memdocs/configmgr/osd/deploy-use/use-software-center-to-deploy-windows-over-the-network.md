---
title: Använda Software Center för att distribuera Windows via nätverket
titleSuffix: Configuration Manager
description: Du kan distribuera ett operativ system till Software Center för att uppdatera en befintlig dator med en ny version av Windows eller uppgradera Windows till den senaste versionen.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b9946f6204c2e95645c932cd4e9aab691f1d95d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724218"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Använd Software Center för att distribuera Windows via nätverket med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan göra en aktivitetssekvens som installerar ett operativ system i Configuration Manager tillgängligt i Software Center. Du kan distribuera ett operativ system till Software Center med följande distributions scenarier för operativ system:

-   [Uppdatera en befintlig dator med en ny version av Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Uppgradera Windows till den senaste versionen](upgrade-windows-to-the-latest-version.md)

Slutför stegen i ett av scenarierna för operativ Systems distribution. Använd sedan följande avsnitt för att förbereda för distributioner som är tillgängliga i Software Center.

## <a name="configure-deployment-settings"></a>Konfigurera distributionsinställningar  
Konfigurera distributionen för att göra operativ Systems distributionen tillgänglig i Software Center. Du kan konfigurera distributionen på sidan **distributions inställningar** i guiden distribuera program vara eller på fliken **distributions inställningar** i egenskaperna för distributionen. För inställningen **Gör tillgängligt för följande** konfigurerar du antingen **Endast Configuration Manager-klienter** eller **Configuration Manager-klienter, media och PXE**. Efter att systemet har distribuerat operativ systemet visas operativ systemet i Software Center för medlemmar i mål samlingen.

##  <a name="deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a>Distribuera aktivitetssekvensen till datorer  
Distribuera operativsystemet till en målsamling. Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md). När du distribuerar operativ system för Software Center kan du konfigurera om distributionen är obligatorisk eller tillgänglig.

-   **Obligatorisk distribution**: Krävs för distributioner som gör operativsystemet tillgängligt i Software Center, men det startas automatiskt enligt det konfigurerade tilldelningsschemat.

-   **Tillgänglig distribution**: Operativsystemet blir tillgängligt i Software Center och användaren kan installera det på begäran.
