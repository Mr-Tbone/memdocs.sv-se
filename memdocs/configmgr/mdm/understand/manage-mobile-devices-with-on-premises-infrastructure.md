---
title: Lokal MDM
titleSuffix: Configuration Manager
description: Lär dig mer om lokal hantering av mobila enheter (MDM) i Configuration Manager
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38d68447093d098f1a8157a2e18e19a6c4f88364
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721838"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>Lokal MDM i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager lokal hantering av mobila enheter (MDM) är en lösning för enhets hantering som förlitar sig på de inbyggda hanterings funktionerna i Windows. Den här funktionen baseras på standarden för enhets hantering i Open Mobile Alliance (OMA). Den använder organisationens Configuration Manager-infrastruktur för att hantera och underhålla enheterna. Din organisation kräver Microsoft Intune licenser för att använda den här funktionen, men den kräver ingen moln anslutning. Configuration Manager lagrar all information om dina enheter i din lokala plats databas.

Lokal MDM skiljer sig från Microsoft Intune, som också förlitar sig på inbyggda OMA DM-funktioner. Alla hanterings funktioner i Intune levereras via Cloud Services. Lokal MDM skiljer sig också från den klientbaserade hanterings lösningen som traditionellt erbjuds av Configuration Manager. Den förlitar sig på liknande infrastruktur, men använder inte separat installerad klient program vara på de enheter som hanteras.  

## <a name="comparison"></a>Jämförelse

I följande avsnitt listas fördelarna och nack delarna med lokal MDM jämfört med traditionell klientbaserad hantering:  

### <a name="advantages"></a>Fördelar

- **Förenklad infrastruktur**: färre plats system roller krävs.

- **Enklare att underhålla**: eftersom hanterings funktionerna är inbyggda i enhetens operativ system krävs inga nya versioner av den Configuration Manager klienten när nya hanterings funktioner introduceras på platsen.

- **Lokalt**:-all hantering och data lagras lokalt.

### <a name="disadvantages"></a>Nackdelar

**Färre klient hanterings funktioner**: ingen dirigering, avläsning av program vara, integration från tredje part, aktivitetssekvenser eller support för Software Center.

- **Begränsat stöd för enheter**: lokalt MDM stöder inte lika många operativ system versioner som Configuration Manager-klienten. Mer information finns i [operativ system versioner som stöds för klienter och enheter](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

## <a name="next-step"></a>Nästa steg

Lär dig mer om vad du bör tänka på när du konfigurerar Configuration Manager-infrastrukturen och planerar för enhets registrering i lokal MDM.

> [!div class="nextstepaction"]
> [Planera för lokal MDM](../plan-design/plan-on-premises-mdm.md)  
