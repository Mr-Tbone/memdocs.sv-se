---
title: Power Viewer-verktyget
titleSuffix: Configuration Manager
description: Använd verktyget Power Viewer för att visa status för energispar funktioner på en Configuration Manager-klient.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcab26abe2e2a9062eda5ff80ea958010e8a7f62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723196"
---
# <a name="power-viewer-tool"></a>Power Viewer-verktyget

*Gäller för: Configuration Manager (aktuell gren)*

Verktyget Power Viewer är ett av de [Configuration Manager verktygen](tools.md). Använd den för att visa status för energispar funktioner på en Configuration Manager-klient.

Kör **PowerVwr. exe** som administratör. När verktyget startas visas energispar funktioner och energi inställningar på den lokala datorn på fliken **energi konfiguration** . 

Så här visar du energispar funktioner för en fjärrdator:  

1. Gå till **Arkiv** -menyn och klicka på **Anslut**. 

2. Ange **dator** namnet och ett **användar** namn och **lösen ord**om det behövs. 

Det finns tre flikar i Power Viewer:  

- **Energi konfiguration**: Visa energispar funktioner och energi inställningar för mål datorn.  

- **Daglig aktivitet**: Visa de dagliga aktivitets diagrammen i klienten, som innehåller följande information:  

    - **Dator på**: datorns energi status på en dag. Vilo läge anses vara avstängt.  

    - **Övervaka på**: på eller av övervakas status på en dag.  

    - **Användaren är aktiv**: information om användar aktiviteter på en dag.  

- **Power events**: Visa alla dagliga energi händelser. Klienten sammanfattar dessa händelser vid 12:00. Den här sammanfattningen genererar data för diagrammet för daglig aktivitet.  
