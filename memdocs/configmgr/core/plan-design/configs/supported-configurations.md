---
title: Konfigurationer som stöds
titleSuffix: Configuration Manager
description: Identifiera viktiga konfigurationer och krav så att du kan planera, distribuera och underhålla en fungerande Configuration Manager distribution.
ms.date: 10/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 66770ea14c3ae53bad8e6df61b54c7c5e2d2aaa0
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904563"
---
# <a name="supported-configurations-for-configuration-manager"></a>Konfigurationer som stöds för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Som en lokal lösning gör Configuration Manager använda dina servrar, klienter, nätverkskonfigurationer och ytterligare produkter som Microsoft Intune, SQL Server och Azure.

Informationen i det här och följande avsnitt är nödvändig för att hjälpa dig att identifiera viktiga konfigurationer, krav och begränsningar, så att du kan planera, distribuera och underhålla en fungerande Configuration Manager distribution.  Den här informationen är unik för infrastrukturen för Configuration Manager platser, hierarkier och hanterade enheter.

När en Configuration Manager funktion eller funktion kräver mer detaljerade konfigurationer, ingår informationen i den användarspecifika dokumentationen och kompletterar mer allmän konfigurations information.  

 De produkter och tekniker som beskrivs i följande avsnitt stöds av Configuration Manager. Deras införande i det här innehållet innebär dock inte en förlängning av stöd för någon produkt utöver produktens enskilda support livs cykel. Produkter som är bortom deras support livs cykel stöds inte för användning med Configuration Manager, inklusive produkter som omfattas av [ESU-programmet (Extended Security updates)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) . Mer information om Microsofts supportlivscykler finns på webbplatsen [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle) . Mer information om utökade säkerhets uppdateringar i Configuration Manager finns i [operativ system versioner som stöds för klienter och enheter för Configuration Manager](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU).

> [!NOTE]  
>  Om du vill ha mer information om Microsofts support livs cykel policy går du till webbplatsen vanliga frågor och svar om support policy för Microsoft Support Lifecycle på [Microsoft Support livs cykel princip](https://support.microsoft.com/lifecycle).  

 Dessutom stöds inte produkter och produkt versioner som inte listas i följande avsnitt med Configuration Manager om de inte har meddelats på bloggen för [Enterprise Mobility and Security](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/bg-p/enterprisemobilityandsecurity).  I så fall föregås innehållet på den här bloggen av en uppdatering av den här delen av dokumentationen.


-  [Antal och gränsvärden](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Lär dig mer om hur många platser, plats system roller per plats och klienter eller enheter som stöds i olika hierarkier för Configuration Manager.

-  [Plats och krav för platssystem](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Lär dig mer om konfigurationer som krävs på en Windows-Server för att stödja olika plats typer och plats system roller.

-  [Operativsystem som stöds för platssystemservrar](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Lär dig mer om vilka operativ system som du kan använda som plats Server eller plats system Server.

-  [Operativsystem som stöds för klienter och enheter](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Lär dig mer om vilka operativ system du kan hantera med Configuration Manager, inklusive Windows, Windows Embedded, Linux och UNIX, Mac och mobila enheter.

-  [Operativ system som stöds för-konsolen](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Lär dig mer om vilka operativ system som kan vara värdar för Configuration Manager-konsolen för att ge en åtkomst punkt för att hantera distributionen.  

-  [Stöd för SQL Server-versioner](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Lär dig mer om vilka versioner av SQL Server kan vara värd för plats databasen och rapporterings databasen, samt om obligatoriska konfigurationer och valfria konfigurationer som du kan använda.

-  [Alternativ för hög tillgänglighet](../../servers/deploy/configure/high-availability-options.md)  
Lär dig mer om de alternativ som du kan implementera när du utformar din miljö för att underhålla en hög nivå av tillgänglig tjänst för din Configuration Manager-distribution.

-  [Rekommenderad maskinvara](../../../core/plan-design/configs/recommended-hardware.md)  
Lär dig mer om rikt linjer som kan hjälpa dig att identifiera rätt maskin vara och konfigurationer som är värdar för dina Configuration Manager-platser och nyckel tjänster.

-  [Stöd för Active Directory-domäner](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Läs om de Active Directory-domänautentiseringsuppgifter som stöds och som Configuration Manager kräver och stöder.

-  [Stöd för Windows-funktioner och nätverk](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Lär dig mer om Windows-tekniker som stöds (till exempel BranchCache och datadeduplicering) och begränsningar för deras användning med Configuration Manager.

-  [Stöd för virtualiseringsmiljöer](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Lär dig mer om hur du använder virtuella dator tekniker som stöds.
