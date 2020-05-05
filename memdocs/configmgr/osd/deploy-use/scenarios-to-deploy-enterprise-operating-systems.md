---
title: Scenarier för att distribuera operativsystem i företag
titleSuffix: Configuration Manager
description: Lär dig mer om flera scenarier för att distribuera operativ system i företag med Configuration Manager.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07e8623928cbfe0bcd562d3d6efdf3a9ceee85ae
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723770"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Scenarier för att distribuera operativ system i företag med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Följande distributions scenarier för operativ system är tillgängliga i Configuration Manager:  

#### <a name="upgrade-windows-to-the-latest-version"></a>Uppgradera Windows till den senaste versionen
Det här scenariot uppgraderar operativ systemet på datorer som kör Windows 7, Windows 8,1 eller Windows 10. Uppgraderings processen behåller program, inställningar och användar data på datorn. Det finns inga externa beroenden, t. ex. Windows ADK. Den här processen kan vara snabbare och mer flexibel än vanliga OS-distributioner.  

Mer information finns i [uppgradera Windows till den senaste versionen](upgrade-windows-to-the-latest-version.md).


#### <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot för befintliga enheter
<!--3607717, fka 1358333-->
Från och med version 1810 finns Windows autopilot för befintliga enheter med Windows 10 version 1809 eller senare. Med den här funktionen kan du återställa avbildningen och etablera en Windows 7-enhet för Windows autopilot-användarläge med hjälp av en enda Configuration Manager-aktivitetssekvens.

Mer information finns i [Windows Autopilot för befintliga enheter](windows-autopilot-for-existing-devices.md).


#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Uppdatera en befintlig dator med en ny version av Windows
Det här scenariot partitionerar och formaterar (raderar) en befintlig dator och installerar ett nytt operativ system på datorn. Du kan migrera inställningar och användar data när operativ systemet har installerats.  

Mer information finns i [Uppdatera en befintlig dator med en ny version av Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md).


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>Installera en ny version av Windows på en ny dator (utan operativsystem)
Det här scenariot installerar ett operativ system på en ny dator. Det är en ny installation av operativ systemet och innehåller inte några inställningar eller migrering av användar data.  

Mer information finns i [installera en ny version av Windows på en ny dator (Bare Metal)](install-new-windows-version-new-computer-bare-metal.md).


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>Ersätta en befintlig dator och överföra inställningar
Det här scenariot installerar ett operativ system på en ny dator. Du kan också välja att migrera inställningar och användardata från den gamla datorn till den nya datorn.  

Mer information finns i [ersätta en befintlig dator och överföra inställningar](replace-an-existing-computer-and-transfer-settings.md).


