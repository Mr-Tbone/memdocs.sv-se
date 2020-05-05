---
title: Service fönster
titleSuffix: Configuration Manager
description: Använd Service Windows för att styra när Configuration Manager platser installerar uppdateringar.
ms.date: 01/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 669da2a04fe4e94b08fc426c32e0dbcc804a21d1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719115"
---
#  <a name="service-windows-for-site-servers"></a>Servicefönster för platsservrar

*Gäller för: Configuration Manager (aktuell gren)*

Du kan konfigurera service fönster på centrala administrations platser och primära platser för att styra när uppdateringar i konsolen kan installeras.  Du kan konfigurera flera fönster, med det fönster som tillåts för att installera uppdateringar som bestäms av en kombination av alla service fönster för den plats servern.

När inget service fönster har kon figurer ATS:
- **På platsen på den översta nivån** (en central administrations plats eller en fristående primär plats) väljer du när du vill starta installationen av uppdateringen.
- **På en underordnad primär plats**installeras uppdateringen automatiskt när uppdateringen har slutfört installationen på den centrala administrations platsen.
- **På en sekundär plats**startar uppdateringar aldrig automatiskt. I stället måste du starta installationen av uppdateringen från-konsolen manuellt när den överordnade primära platsen har installerat uppdateringen.

När ett service fönster konfigureras:
- **På platsen på den översta nivån**kan du inte starta installationen av en ny uppdatering från Configuration Manager-konsolen. Även om ett tjänst fönster har kon figurer ATS laddar platsen automatiskt ned uppdateringar så att de är redo att installeras.  
- **På en underordnad primär plats**kommer uppdateringar som har installerats på en central administrations plats att laddas ned till den primära platsen, men startar inte automatiskt. Du kan inte starta installationen av en uppdatering manuellt under en tid som blockeras med hjälp av ett service fönster. Vid en tidpunkt då tjänsten Windows inte längre blockerar uppdaterings installationen startar uppdateringen automatiskt.
- **Sekundära platser** har inte stöd för service fönster och installerar inte automatiskt uppdateringar. När den primära överordnade platsen för en sekundär plats installerar en uppdatering kan du starta uppdateringen av den sekundära platsen från-konsolen.

## <a name="to-configure-a-service-window"></a>Konfigurera ett service fönster

1.  I Configuration Manager-konsolen öppnar du **Administration** > **plats konfiguration** > **platser**och väljer sedan den plats server där du vill konfigurera ett service fönster.  

2.  Sedan redigerar du platsservrarnas **Egenskaper** och markerar fliken **Servicefönster**, där du sedan kan ange ett eller flera servicefönster för den aktuella platsservern.  
