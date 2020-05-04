---
title: Övervaka Linux/UNIX-klienter
titleSuffix: Configuration Manager
description: Övervaka klienter på Linux-och UNIX-servrar i Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2ea3a0b630e1710aeaf74a4349f202806d45039
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715363"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Övervaka klienter för Linux-och UNIX-servrar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]  
> Från och med version 1902 stöder Configuration Manager inte Linux-eller UNIX-klienter. 
> 
> Överväg Microsoft Azure hantering för hantering av Linux-servrar. Azure-lösningar har omfattande Linux-support som i de flesta fall överskrider Configuration Manager-funktioner, inklusive slut punkt till slut punkt för korrigerings hantering för Linux.

Du kan visa information från Linux-och UNIX-servrar i Configuration Manager-konsolen på samma sätt som du använder för att visa information från Windows-baserade klienter.  

 Informationen du kan visa omfattar:  

- Statusinformation från klienter, i Configuration Manager-konsolens instrument paneler  

- Information om klienter i standard Configuration Managers rapporter  

- Inventeringsinformation i Resursläsaren  

  I följande avsnitt beskrivs hur du hämtar dessa uppgifter från resurs Utforskaren och rapporter.  

##  <a name="use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a>Använda resurs läsaren för att Visa inventering för Linux-och UNIX-servrar  

 När en Configuration Manager klienten har skickat maskin varu inventeringen till Configuration Managers plats kan du använda Resursläsaren för att visa den här informationen. Configuration Manager-klienten för Linux och UNIX lägger inte till nya klasser eller vyer för inventering i Resursläsaren. Inventeringsdata för Linux och UNIX mappas till befintliga WMI-klasser. Du kan visa inventeringsinformation för Linux- och UNIX-servrar i Windows-baserade klassificeringar med Resursläsaren.  

 Du kan till exempel samla in listan med alla internt installerade program som finns på Linux- och UNIX-servrarna. Exempel på internt installerade program är **.rpms** i Linux eller **.pkgs** i Solaris. När inventeringen har skickats av en Linux-eller UNIX-klient kan du Visa en lista över alla internt installerade Linux-eller UNIX-program i Resursläsaren i Configuration Manager-konsolen.  

 Information om hur du använder Resursläsaren finns i [så här använder du Resursläsaren för att Visa maskin varu inventering](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> Använda rapporter för att visa information för Linux- och UNIX-servrar  
 Rapporter för Configuration Manager innehåller information från Linux-och UNIX-servrar tillsammans med information från Windows-baserade datorer. Ingen ytterligare konfiguration krävs för att integrera Linux- och UNIX-data i rapporterna.  

 Om du till exempel kör rapporten med namnet Antal operativsystemversioner visas listan med olika operativsystem och antalet klienter som kör varje operativsystem. Rapporten bygger på informationen om maskin varu inventering som skickades av de olika Configuration Manager-klienter som körs på de olika operativ systemen.  

 Det är också möjligt att skapa anpassade rapporter som är speciella för data från Linux-och UNIX-servrar. Egenskapen **Beskrivning** för maskinvaruinventeringsklassen **Operativsystem** är ett användbart attribut som du kan använda för att identifiera specifika operativsystem i rapportfrågan.  

 Information om rapporter i Configuration Manager finns i [Introduktion till rapportering](../../servers/manage/introduction-to-reporting.md).  
