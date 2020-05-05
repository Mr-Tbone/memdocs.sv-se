---
title: Förbereda för distribution av operativsystem
titleSuffix: Configuration Manager
description: Lär dig mer om hur du förbereder operativ Systems distributioner i Configuration Manager
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bdd8cd61aedb06fe35a4ba268806f64cc18bf85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724085"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>Förbered för distribution av operativ system i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det finns flera saker du måste göra i Configuration Manager innan du kan distribuera operativ system. Använd följande artiklar för att förbereda för distribution av operativ system:  

-   [Hantera startavbildningar](manage-boot-images.md)  

-   [Hantera avbildningar av operativsystem](manage-operating-system-images.md)  

-   [Hantera uppgraderingspaket för operativsystem](manage-operating-system-upgrade-packages.md)  

-   [Hantera drivrutiner](manage-drivers.md)  

-   [Hantera användartillstånd](manage-user-state.md)  

-   [Förbereda distributioner till okända datorer](prepare-for-unknown-computer-deployments.md)  

-   [Koppla användare till en måldator](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>Storlek på operativ system avbildning  

OS-avbildningar är stora i storlek. Bild storleken för Windows 7 är till exempel 3 GB eller mer. Storleken på avbildningen och antalet datorer som du distribuerar operativ systemet till påverkar nätverkets prestanda och den tillgängliga bandbredden. Se till att testa nätverkets prestanda. Testning av påverkan bättre mätar effekten som avbildnings distributionen kan ha och den tid det tar att slutföra distributionen. Configuration Manager aktiviteter som påverkar nätverks prestanda inkluderar att distribuera avbildningen till en distributions plats, distribuera avbildningen från en plats till en annan och ladda ned avbildningen till klienten.  

Kontrol lera också att du planerar för tillräckligt med disk utrymme på de distributions platser som är värdar för OS-avbildningarna.  

Mer information finns i [ytterligare planerings överväganden för distributions platser](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_AdditionalPlanning).


### <a name="client-cache-size"></a>Storlek på klientens cacheminne  

När Configuration Manager klienter laddar ned innehåll använder de automatiskt Background Intelligent Transfer Service (BITS), om det är tillgängligt. När du distribuerar en aktivitetssekvens som installerar ett operativ system kan du ange ett alternativ för distributionen så att Configuration Manager klienter laddar ned hela avbildningen till ett lokalt cacheminne innan aktivitetssekvensen körs.  

När en Configuration Manager-klient måste ladda ned en operativ system avbildning, men det inte finns tillräckligt med utrymme i cacheminnet, kan klienten rensa utrymme i cacheminnet. Det kontrollerar de andra paketen i cacheminnet för att avgöra om det finns tillräckligt med disk utrymme för att ta reda på om de äldsta paketen tas bort. Om det inte finns tillräckligt med utrymme för att ta bort paket laddar inte klienten ned avbildningen och distributionen Miss lyckas. Detta kan inträffa om cachen har ett stort paket som du konfigurerar för att kvarhålla i cacheminnet. Om det går att frigöra tillräckligt med diskutrymme i cacheminnet genom att paket tas bort tar klienten bort dem och laddar sedan ned avbildningen till cacheminnet.  

Standardvärdet för cachestorlek på Configuration Manager-klienter kanske inte är tillräckligt stort för de flesta distributioner av operativ system avbildningar. Om du planerar att ladda ned hela avbildningen till klientens cacheminne justerar du storleken på klientens cacheminne på mål datorerna för att hantera storleken på avbildningen som du distribuerar.  

Mer information finns i [Konfigurera klientens cacheminne](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  


