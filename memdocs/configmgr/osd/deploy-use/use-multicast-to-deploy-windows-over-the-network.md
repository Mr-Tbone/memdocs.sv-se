---
title: Använd multicast för att distribuera Windows via nätverket
titleSuffix: Configuration Manager
description: Använd multicast i Configuration Managers miljö så att flera datorer samtidigt kan hämta operativ system avbildningen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f81b23d3783d397d83a3925b98c0c8f601fa4012
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720123"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Använd multicast för att distribuera Windows via nätverket med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Multicast är en nätverks optimerings metod som du kan använda i din Configuration Manager-miljö där flera klienter sannolikt kommer att hämta samma operativ system avbildning på samma tidpunkt. När multicast används hämtar flera datorer operativsystemavbildningen samtidigt när den skickas med multicast av distributionsplatsen istället för att distributionspunkten skickar en kopia av data till varje klient via en separat anslutning.  

 Du kan distribuera operativsystem via nätverket genom att använda multicast i följande scenarier vid operativsystemsdistribution:  

- [Uppdatera en befintlig dator med en ny version av Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Installera en ny version av Windows på en ny dator (utan operativsystem)](install-new-windows-version-new-computer-bare-metal.md)  

  Utför stegen i ett av scenarierna för operativsystemsdistribution och använd sedan följande avsnitt för att skapa stöd för multicast.  

##  <a name="configure-a-distribution-point-to-support-multicast"></a><a name="BKMK_Configure"></a> Konfigurera en distributionsplats för att stöda multicast  
 Innan du använder multicast för att distribuera operativsystem måste du konfigurera en distributionsplats som har stöd för multicast. Mer information finns i [Installera och konfigurera distributions platser](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast). En lista över portar som krävs för att stödja multicast finns i [portar](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Förbereda en operativsystemavbildning för multicastdistributioner  
 Information om hur du konfigurerar operativsystemavbildningspaketet för att ha stöd för multicast finns i [Prepare the operating system image for multicast deployments](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Distribuera aktivitetssekvensen  
 Distribuera operativsystemet till en målsamling. Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md).  
