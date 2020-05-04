---
title: Hantera VDI-klienter
titleSuffix: Configuration Manager
description: Hantera Configuration Manager klienter i en VDI-infrastruktur (Virtual Desktop Infrastructure).
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01348695ac5b3b64ca87a9b42aa52ac235b533d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713326"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Hantera Configuration Manager klienter i en VDI-infrastruktur (Virtual Desktop Infrastructure)

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager stöder installation av Configuration Manager-klienten i följande VDI-scenarier (Virtual Desktop Infrastructure):  

- **Personliga virtuella datorer** – personliga virtuella datorer används vanligt vis när du vill se till att användar data och inställningar upprätthålls på den virtuella datorn mellan sessioner.  

- **Fjärrskrivbordstjänster sessioner** – Fjärrskrivbordstjänster gör det möjligt för en server att vara värd för flera samtidiga klient sessioner. Användare kan ansluta till en session och sedan köra program på den servern.  

- **Poolbaserade virtuella datorer** – virtuella datorer i pooler är inte beständiga mellan sessioner. När en session stängs ignoreras alla data och inställningar. Virtuella datorer i pooler är användbara när Fjärrskrivbordstjänster inte kan användas eftersom det inte går att köra ett program som krävs på den Windows Server som är värd för klientsessioner.  

  I följande tabell visas överväganden för att hantera Configuration Manager-klienten i en infrastruktur för virtuella skriv bord.  

|Typ av virtuell dator|Överväganden|  
|--------------------------|--------------------|  
|Personliga virtuella datorer|Configuration Manager behandlar personliga virtuella datorer på samma sätt som en fysisk dator. Configuration Manager-klienten kan förinstalleras på den virtuella dator avbildningen eller distribueras efter att den virtuella datorn har tillhandahållits.|  
|Fjärrskrivbordstjänster|Den Configuration Manager klienten är inte installerad för enskilda fjärrskrivbordssessioner. Klienten installeras i stället bara en gången på Fjärrskrivbordstjänster servern. Alla Configuration Manager funktioner kan användas på Fjärrskrivbordstjänster-servern.|  
|Virtuella datorer i pooler|När en virtuell dator i poolen inaktive ras försvinner eventuella ändringar som du gör med hjälp av Configuration Manager.<br /><br /> Data som returneras från Configuration Manager funktioner som maskin varu inventering, program varu inventering och avläsning av program vara kanske inte är relevanta för dina behov eftersom den virtuella datorn kanske bara fungerar under en kort tids period. Överväg att utesluta virtuella datorer i pooler från inventerings aktiviteter.|  

 Eftersom virtualiseringen har stöd för att köra flera Configuration Manager-klienter på samma fysiska dator har många klient åtgärder en inbyggd slumpmässig fördröjning för schemalagda åtgärder, till exempel maskin-och program varu inventering, genomsökning av skadlig kod, program varu installationer och genomsökningar av program uppdateringar. Den här fördröjningen hjälper till att distribuera CPU-bearbetning och data överföring för en dator som har flera virtuella datorer som kör Configuration Manager-klienten.  

> [!NOTE]  
>  Med undantag för Windows Embedded-klienter som är i behandlings läge, kan Configuration Manager klienter som inte körs i virtualiserade miljöer även använda denna slumpmässiga fördröjning. När du har många distribuerade klienter bidrar detta till att undvika toppar i nätverks bandbredden och minskar kraven på processor bearbetning på Configuration Manager-plats system, till exempel hanterings platsen och plats servern. Fördröjnings intervallet varierar beroende på Configuration Manager funktion.  
>   
>  Slump fördröjningen inaktive ras som standard för obligatoriska program uppdateringar med hjälp av följande klient inställning: **dator agent**: **Inaktivera slumpmässig tids gräns**.
