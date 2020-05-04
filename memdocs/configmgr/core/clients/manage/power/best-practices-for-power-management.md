---
title: Rekommendationer för energispar funktioner
titleSuffix: Configuration Manager
description: Lär dig mer om Microsoft-rekommendationer för energispar funktioner i Configuration Manager.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 02cfb32f9187ca5a0ae0ad70ffcb4b85db8afb1b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715265"
---
# <a name="recommendations-for-power-management-in-configuration-manager"></a>Rekommendationer för energispar funktioner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd följande rekommendationer för energispar funktioner i Configuration Manager.  

## <a name="monitor-at-a-representative-time"></a>Övervaka vid en representativ tid

I övervaknings fasen av energispar funktionerna får du följande information från datorerna i din organisation:

- Strömförbrukning
- Aktivitet
- Energispar funktioner
- Miljö påverkan

Välj en representativ tid för att övervaka enheterna. Övervakning under en offentlig helgdag ger till exempel inte en realistisk rapport om datorns energi förbrukning.

## <a name="create-a-control-collection"></a>Skapa en kontroll samling

Skapa två grupper med datorer för att kontrollera hur energischeman påverkar förbrukningen. Den första samlingen ska innehålla majoriteten av de datorer som du vill tillämpa energi inställningar på. *Kontroll samlingen* ska innehålla återstående datorer. Använd den nödvändiga energi hanterings planen för den första samlingen. Kör sedan rapporter för att jämföra påverkan mellan de två samlingarna.  

## <a name="run-reports-before-you-apply-a-plan"></a>Köra rapporter innan du använder en plan

Innan du använder en Energis par plan på en samling datorer kör du rapporten **energi inställningar** . Använd den här rapporten för att hjälpa dig att förstå de energispar funktioner som redan har kon figurer ATS på datorer i samlingen. Om du använder nya inställningar för energispar funktioner på datorer utan att först undersöka de befintliga inställningarna kan det öka strömförbrukningen.  

## <a name="exclude-servers"></a>Uteslut servrar

Energispar funktioner för datorer som kör Windows Server stöds inte. Lägg till servrar i en samling och exkludera den från energispar funktioner.  

> [!NOTE]
> Även om Configuration Manager inte har stöd för energispar funktioner i Windows Server, samlar den fortfarande in energi förbruknings data för analys och rapportering.

## <a name="exclude-other-computers"></a>Undanta andra datorer

Om du har datorer som du inte vill hantera med energispar funktioner lägger du till dessa datorer i en undantags samling.  

Du kanske vill utesluta från energispar funktioner på följande typer av datorer:

- Datorer som måste vara påslagna.  

- Datorer som användarna behöver för att fjärrans luta.  

- Datorer som inte kan använda energispar funktioner.  

- Datorer som har platssystemrollen för distributionsplats.  

- Offentliga datorer, till exempel kiosk datorer, informations skärmar eller övervaknings konsoler där datorn och övervakaren alltid måste vara påslagna.  

Mer information finns i [Konfigurera energispar funktioner](configuring-power-management.md).  

## <a name="apply-power-plans-to-a-test-collection"></a>Använda energi scheman i en test samling

Testa alltid först energischemat på en testgrupp datorer innan du använder schemat på en större datorgrupp.  

När du undantar en dator från energispar funktioner återgår alla energi inställningar till sina ursprungliga värden. Du kan inte återställa enskilda energi inställningar till sina ursprungliga värden.  

## <a name="apply-power-plan-settings-individually"></a>Använd individuella energischemainställningar

Övervaka effekten av att tillämpa varje energi inställning innan du tillämpar nästa. Den här processen ser till att varje inställning har den nödvändiga inverkan. Mer information om energi schema inställningar finns i [tillgängliga inställningar för energispar funktioner](create-and-apply-power-plans.md#BKMK_Plans).  

## <a name="regularly-monitor-computers-for-multiple-power-plans"></a>Övervaka datorer regelbundet för flera energi scheman

Energispar funktioner innehåller en rapport som visar datorer som har mer än ett energi schema installerat: **datorer med flera energi scheman**.

Om en dator är medlem i flera samlingar, var och en använder olika energi scheman, gäller följande beteenden:  

- **Energi schema**: om du använder flera värden för energi inställningar till en dator används det minst restriktiva värdet.  

- **Väcknings tid**: om du använder flera Väcknings tider på en stationär dator, används tiden närmast midnatt.  

Mer information finns i [datorer med flera energi scheman](monitor-and-plan-for-power-management.md#BKMK_Multiple).  

## <a name="save-or-export-power-management-information"></a>Spara eller exportera information om energispar funktioner

Spara eller exportera resultaten när du kör rapporter under övervaknings-och efterlevnadsprinciper. Behåll data för senare jämförelse om Configuration Manager senare tar bort data.  

Configuration Manager sparas i plats databasen följande information om energispar funktioner:

- Information om energispar funktioner som används av dagliga rapporter: 31 dagar

- Information om energispar funktioner som används av månads rapporter: 13 månader
