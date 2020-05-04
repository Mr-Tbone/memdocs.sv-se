---
title: Användning av diagnostikdata
titleSuffix: Configuration Manager
description: Lär dig mer om hur Microsoft använder diagnostik-och användnings data som Configuration Manager samlar in.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6a014d60c49b0ff7e10cd74c101294dd002266d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715615"
---
# <a name="how-microsoft-uses-configuration-manager-diagnostics-and-usage-data"></a>Hur Microsoft använder Configuration Manager diagnostik-och användnings data

*Gäller för: Configuration Manager (aktuell gren)*

Diagnostik-och användnings data som Configuration Manager samlar in ger Microsoft nästan omedelbar feedback om hur produkten fungerar och används för att justera framtida uppdateringar. Microsoft kan också se konfigurations data som hjälper dem att teknikern och testa de konfigurationer som du använder i produktionen. Ett exempel:

- Windows Server-versioner som används på plats servrar

- Installerade språk paket

- Skillnaden i SQL-schemat jämfört med produktstandard

Dessa data hjälper teknik teamet att planera framtida tester för att se till att du har den bästa upplevelsen med de vanligaste konfigurationerna. Dessa data är viktiga för att snabbt justera och anpassa med en frekvent versions cykel.

Lika viktigt är hur diagnostik-och användnings data inte används. Microsoft använder inte dessa data för:

- Licensieringsgranskningar, som att till exempel jämföra kundens användning med vad som anges i licensavtalet

- Granskning av produkter som inte längre stöds

- Annonsering baserad på tillgängliga data, till exempel användning av funktioner eller geolokalisering (tidszon)

Microsoft använder tillgängliga data för att förbättra produkten. Ett exempel:

- Det första support som erbjuds av den aktuella grenen av Configuration Manager begränsad support tids linjen för Windows Server 2008 R2. Microsoft undersökte användnings data från kunder som hade uppgraderat till Configuration Manager aktuella grenen. De identifierade sedan behovet av att ändra och utöka tids linjen för att stödja kunder som fortfarande använder detta operativ system.

- Microsoft har förbättrat de nödvändiga kontrollerna för att installera en uppdatering. De tog bort föråldrade regler, redovisat ytterligare fall och automatiskt reparerat vissa problem.  

> [!div class="nextstepaction"]
> [Så samlar Configuration Manager in data](how-diagnostics-and-usage-data-is-collected.md)
