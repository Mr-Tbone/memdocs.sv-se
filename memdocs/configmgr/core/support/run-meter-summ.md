---
title: Verktyget körningsmätarsammanfattning
titleSuffix: Configuration Manager
description: Använd verktyget kör mätare för sammanfattning för att utlösa sammanfattnings aktiviteter för program varu avläsning i Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 599cc2f552b975fa9b40c94ea413f6b80b04a1a3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723175"
---
# <a name="run-meter-summarization-tool"></a>Verktyget körningsmätarsammanfattning

*Gäller för: Configuration Manager (aktuell gren)*

Verktyget kör mätare sammandrag är ett av de [Configuration Manager verktygen](tools.md). Använd den för att omedelbart utlösa underhålls aktiviteter för sammanfattning av avläsning av program vara på primära platser. Som standard körs dessa aktiviteter enligt schemat vid **plats underhålls** aktiviteter som startar efter 12:00 varje dag. 

Dessa uppgifter sammanfattar data i SQL-tabellen **MeterData** och skriver sammanfattnings resultatet i tabellerna **FileUsageSummary** och **MonthlyUsageSummary** . Sedan visas det sammanfattade resultatet i rapporter om avläsning av program vara. Alla Configuration Manager administrativa användare som kan ansluta till den primära plats databasen kan använda det här verktyget för att köra Sammanfattning. 

Det här verktyget kör **Sammanfattning av fil användnings Sammanfattning** och **månatlig användning Sammanfattning** av data Sammanfattning för program mätning. Den sammanfattar alla befintliga mätnings data utan den vanliga svars tiden på 12 timmar. Kör den på den SQL Server som är värd för plats databasen. Om sammanfattningen lyckas anges avslutnings koden till `0`. Om det uppstod ett fel är `1`slut koden.



## <a name="usage"></a>Användning

### <a name="command-line"></a>Kommandorad

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>Alternativ

#### <a name="database-name"></a>Databasnamn
Namnet på plats databasen på SQL-servern.

#### <a name="delay-in-hours-for-summarization"></a>Fördröjning i timmar för sammanfattning
Verktyget sammanfattar användningen av program varu avläsning som genereras före fördröjningen. Som standard är den här fördröjningen noll.


### <a name="example"></a>Exempel

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>Sammanfatta användningen av avläsning av program vara som genererats för 12 timmar sedan

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>Se även

- [Underhållsaktiviteter](../servers/manage/maintenance-tasks.md)
- [Övervaka appanvändningen med avläsning av programvara](../../apps/deploy-use/monitor-app-usage-with-software-metering.md)
