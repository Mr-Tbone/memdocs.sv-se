---
title: Använd multicast för att distribuera Windows via nätverket
titleSuffix: Configuration Manager
description: Använd multicast i Configuration Managers miljö så att flera datorer samtidigt kan hämta operativ system avbildningen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f580467ccb26209ed20666733e30959bbf50128
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124713"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Använd multicast för att distribuera Windows via nätverket med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Multicast är en nätverks optimerings metod som du kan använda när flera klienter sannolikt kommer att ladda ned samma OS-avbildning på samma gång. När du använder multicast hämtar flera datorer samtidigt operativ system avbildningen som den är multicast av distributions platsen. Det här beteendet är i stället för varje klient som laddar ned en kopia av avbildningen över en separat anslutning från distributions platsen.

Distribuera operativ system över nätverket med hjälp av multicast i följande scenarier för operativ Systems distribution:

- [Uppdatera en befintlig dator med en ny version av Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Installera en ny version av Windows på en ny dator (utan operativsystem)](install-new-windows-version-new-computer-bare-metal.md)

Slutför stegen i något av de här distributions scenarierna för operativ systemet. Använd sedan följande avsnitt för att stöda multicast.

## <a name="configure-distribution-points-for-multicast"></a><a name="BKMK_Configure"></a>Konfigurera distributions platser för multicast

Om du vill använda multicast måste du konfigurera minst en distributions plats som stöder multicast. Mer information finns i [Installera och konfigurera distributions platser](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).

En lista över portar som krävs för att stödja multicast finns i [portar](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).

## <a name="prepare-an-os-image-for-multicast"></a>Förbereda en OS-avbildning för multicast

Du måste konfigurera operativ system avbildningen så att den stöder multicast. Mer information finns i [förbereda operativ Systems avbildningen för multicast-distributioner](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Distribuera aktivitetssekvensen

Distribuera operativ systemet till en mål samling. Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md).

## <a name="next-steps"></a>Nästa steg

[Användarupplevelser för distribution av operativsystem](../understand/user-experience.md)
