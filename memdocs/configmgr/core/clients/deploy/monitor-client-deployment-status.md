---
title: Övervaka klient distributions status
titleSuffix: Configuration Manager
description: Övervaka klient distributions status i Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 80cfa1576ae2cc4505147aee07a247e035b07ada
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713319"
---
# <a name="how-to-monitor-client-deployment-status-in-configuration-manager"></a>Övervaka klient distributions status i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det tar tid att distribuera klienter på din plats och vissa installationer kanske inte lyckas första gången. Configuration Manager-konsolen är ett sätt att hålla ett öga på klient distributioner i en samling genom att rapportera klient distributions status i real tid.  

> [!NOTE]  
>  Det bästa och mest pålitliga sättet att övervaka klient distributionen är med Configuration Manager-konsolen (som beskrivs i den här artikeln). Avsnittet **Klientstatus** i arbetsytan **Övervakning** i konsolen anger klientdistributionens status korrekt och i realtid. Du kan övervaka klientdistributioner med andra verktyg, till exempel Server Manager i Windows Server eller System Center Operations Manager, men du kan få larm från normala klientinstallationsaktiviteter. På grund av sättet som klientinstallationsprogrammet (CCMSetup.exe) körs på i olika miljöer kan dessa andra verktyg generera falsklarm och varningar som inte korrekt speglar statusen för klientdistributioner.  

 I arbetsytan **Övervakning** i konsolen kan du övervaka följande status för klientdistributioner som sker i en samling som du anger:  

- Kompatibel  

- Pågår  

- Ej kompatibel  

- Misslyckades  

- Okänt  

  Configuration Manager rapporterar om distributioner för produktionsklienter eller förproduktionsklienter. Configuration Manager-konsolen innehåller också ett diagram över misslyckade klientdistributioner under en angiven tidsperiod för att hjälpa dig att avgöra om åtgärder som du vidtar för att felsöka distributioner förbättrar antalet lyckade distributioner över tid.  

## <a name="to-monitor-client-deployments"></a>Övervaka klientdistributioner  

- Klicka på **övervaka** > **klient status**i Configuration Manager-konsolen.  

- Klicka på **Klientdistribution för produktion** eller **Klientdistribution till förproduktion** beroende på vilken version av klienten du vill övervaka.  

- Granska diagrammen för status för klientdistribution och misslyckade klientdistributioner.  

- Om du vill ändra omfattningen för rapporten klickar du på **Bläddra...** och väljer en annan samling.  

  Mer information om klient distributioner för för produktion finns i [så här testar du klient uppgraderingar i en för produktions samling](../../../core/clients/manage/upgrade/test-client-upgrades.md).

  > [!NOTE]
  > Distributions status på datorer som är värdar för plats system roller i en för produktions samling kan rapporteras som **icke-kompatibla** även när klienten har distribuerats. När du uppgraderar klienten till produktion rapporteras distributionens status korrekt.   

  Information om hur du övervakar status för distribuerade klienter finns i [övervaka klienter](../../../core/clients/manage/monitor-clients.md)  

  Du kan använda Configuration Manager-rapporter för att få mer information om statusen för klienterna på din plats. Mer information om hur du kör rapporter finns i [Introduktion till rapportering](../../servers/manage/introduction-to-reporting.md).  
