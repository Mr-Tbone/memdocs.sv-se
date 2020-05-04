---
title: Instrument panel för Surface-enheter
titleSuffix: Configuration Manager
description: Granska information om Surface-enheter med hjälp av instrument panelen.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: 08baf595199bdda121f897d507de97cb7e93e620
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715069"
---
# <a name="surface-device-dashboard-in-configuration-manager"></a>Instrument panel för Surface-enhet i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Från och med version 1802 ger instrument panelen för Surface-enheter information om Surface-enheter som finns i din miljö snabbt och enkelt. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Öppna instrument panelen för Surface-enheter

Använd följande steg för att öppna instrument panelen för Surface-enheter: 

1. Öppna Configuration Manager-konsolen. 
2. Klicka på noden **övervakning** . 
3. Om du vill läsa in instrument panelen klickar du på **Surface-enheter**.

**Instrument panel för Surface Device-instrumentpanelens**
![yta](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Granska informationen på instrument panelen för Surface-enheter

På instrument panelen för Surface-enheter visas tre grafer för din miljö. 

- **Procent av Surface-enheter** – ger dig procent andelen av Surface-enheter i din miljö.

    ![Diagram över procent av Surface-enheter](media/Percent-Surface-Devices.PNG)
- **Surface-modeller** – visar antalet enheter per Surface-modell. 
  - Om du hovrar över ett diagram avsnitt får du procent andelen av de Surface-enheter som är markerade med modellen. 

       ![Diagram över ytdiagram](media/Surface-Models-Hover.PNG)
  - Om du klickar på ett Graph-avsnitt tas du till en enhets lista för modellen. 
      ![Enhets lista för funktions modell](media/Surface-Model-Device-List.PNG)

- De **fem översta versionerna av inbyggd program vara**– visar ett diagram med de fem främsta inbyggda program varu modellerna i din miljö. 
  - Om du hovrar över ett diagram avsnitt får du det antal Surface-enheter som är valda för den inbyggda program varan. Från och med Configuration Manager version 1806 visas en lista över relevanta enheter när du klickar på ett diagram avsnitt. <!--1358654-->
     ![Enhets lista för funktions modell](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Mer information

Mer information om Surface-enheter finns i:
- [Ytans]( https://go.microsoft.com/fwlink/?linkid=861998) webbplats.

Mer information om hur du distribuerar uppdateringar av inbyggd Surface-programvara i Configuration Manager finns i:
- [Hantera uppdateringar av Surface-drivrutiner i Configuration Manager]( https://support.microsoft.com/help/4098906).




