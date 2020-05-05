---
title: Välj vad du vill migrera
titleSuffix: Configuration Manager
description: Lär dig vilka data du kan migrera och vilka data du inte kan migrera till Configuration Manager aktuella grenen.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b697df41490d1709782561cc59b43684fb60d16
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718919"
---
# <a name="determine-whether-to-migrate-data-to-configuration-manager-current-branch"></a>Avgöra om data ska migreras till Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

I Configuration Manager aktuella grenen ger migrering en process för att överföra data och konfigurationer som du har skapat från versioner av Configuration Manager som stöds till din nya hierarki.  Du kan använda detta för att:  

-   Kombinera flera hierarkier till en.  

-   Flytta data och konfigurationer från en labb distribution till produktions distributionen.

-   Flytta data och konfiguration från en tidigare version av Configuration Manager, t. ex. Configuration Manager 2007, som inte har någon uppgraderings väg till Configuration Manager aktuella grenen eller från System Center 2012 Configuration Manager (som stöder en uppgraderings väg till Configuration Manager aktuella grenen).  

Med undantag för distributionsplatsens platssystemroll och de datorer som är värdar för distributionsplatser kan ingen infrastruktur (vilket innefattar webbplatser, platssystemroller eller datorer som är värdar för platssystemroller) migreras, överföras eller delas mellan hierarkier.  

 Även om du inte kan migrera Server infrastruktur kan du migrera Configuration Manager klienter mellan hierarkier. Klientmigrering innefattar migrering av data som klienterna använder från källhierarkin till målhierarkin och därefter installation eller omtilldelning av klientprogramvaran så att klienten därefter rapporterar till den nya hierarkin.

När du har installerat en klient i den nya hierarkin och klienten skickar sina data hjälper dess unika Configuration Manager-ID Configuration Manager associera data som du tidigare migrerat med varje klient dator.  

 De funktioner som tillhandahålls av migreringen hjälper dig att underhålla investeringar som du har gjort i konfigurationer och distributioner samtidigt som du kan dra full nytta av grundläggande ändringar i produkten först (som först introducerades i System Center 2012 Configuration Manager och sedan fortsatte i Configuration Manager). Dessa ändringar omfattar en förenklad Configuration Manager-hierarki som använder färre platser och resurser och den förbättrade bearbetningen som kommer från att använda ursprunglig 64-bitars kod som körs på 64-bitars maskin vara.  

 Information om vilka versioner av Configuration Manager som migreringen stöder finns i [krav för migrering](../../core/migration/prerequisites-for-migration.md).  

## <a name="data-that-you-can-migrate-to-configuration-manager-current-branch"></a><a name="Can_Migrate"></a>Data som du kan migrera till Configuration Manager aktuella grenen

Migrering kan migrera de flesta objekt mellan Configuration Manager hierarkier som stöds. De migrerade instanserna av vissa objekt från en version av Configuration Manager 2007 som stöds måste ändras så att de överensstämmer med System Center 2012 Configuration Manager schemat och objekt formatet.

De här ändringarna påverkar inte data i käll platsens databas. Objekt som migreras från en version av System Center 2012 som stöds Configuration Manager eller Configuration Manager aktuella grenen behöver inte ändras.  

Följande objekt kan migreras baserat på den version av Configuration Manager som finns i källhierarkin. Vissa objekt, som t.ex. frågor, migreras inte. Om du vill fortsätta att använda dessa objekt som inte migreras måste du återskapa dem i den nya hierarkin. Andra objekt, inklusive vissa klient data, återskapas automatiskt i den nya hierarkin när du hanterar klienter i den hierarkin.  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-configuration-manager-current-branch"></a>Objekt som du kan migrera från System Center 2012 Configuration Manager eller Configuration Manager aktuella grenen

-   Program för System Center 2012 Configuration Manager och senare versioner  

-   Virtuell App-V-miljö från System Center 2012 Configuration Manager och senare versioner  

-   Anpassningar av tillgångsinformation  

-   Gränser  

-   Samlingar: om du vill migrera samlingar från en version av System Center 2012 Configuration Manager eller Configuration Manager aktuella grenen använder du ett objekt migrerings jobb.  

-   Kompatibilitetsinställningar:  

    -   Konfigurationsbaslinjer  

    -   Konfigurationsobjekt  

-   Distributioner  

-   Distribution av operativsystem:  

    -   Startavbildningar  

    -   Drivrutinspaket  

    -   Drivrutiner  

    -   Avbildningar  

    -   Paket  

    -   Aktivitetssekvenser  

-   Sök Resultat: sparade Sök villkor  

-   Programuppdateringar:  

    -   Distributioner  

    -   Distributionspaket  

    -   Mallar  

    -   Programuppdateringslistor  

-   Programdistributionspaket  

-   Regler för avläsning av programvara  

-   Virtuella programpaket  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Objekt som du kan migrera från Configuration Manager 2007 SP2

-   Annonser  

-   Program för System Center 2012 Configuration Manager och senare versioner  

-   Virtuell App-V-miljö från System Center 2012 Configuration Manager och senare versioner  

-   Anpassningar av tillgångsinformation  

-   Gränser  

-   Samlingar: du migrerar samlingar från en version av Configuration Manager 2007 som stöds genom att använda ett jobb för migrering av samlingar.  

-   Kompatibilitetsinställningar (kallas önskad konfigurationshantering i Configuration Manager 2007)  

    -   Konfigurationsbaslinjer  

    -   Konfigurationsobjekt  

-   Distribution av operativsystem:  

    -   Startavbildningar  

    -   Drivrutinspaket  

    -   Drivrutiner  

    -   Avbildningar  

    -   Paket  

    -   Aktivitetssekvenser  

-   Sök Resultat: sökmappar  

-   Programuppdateringar:  

    -   Distributioner  

    -   Distributionspaket  

    -   Mallar  

    -   Programuppdateringslistor  

-   Programdistributionspaket  

-   Regler för avläsning av programvara  

-   Virtuella programpaket  

## <a name="data-that-you-cant-migrate-to-configuration-manager-current-branch"></a><a name="Cannot_migrate"></a>Data som du inte kan migrera till Configuration Manager aktuella grenen

Du kan inte migrera följande typer av objekt:  

-   Information om AMT-klientetablering  

-   Filer på klienter, inklusive:  

    -   Klientens inventerings- och historikdata  

    -   Filer i klientcachen  

-   Frågor  

-   Configuration Manager 2007 säkerhets rättigheter och-instanser för platsen och objekten  

-   Configuration Manager 2007-rapporter från SQL Server Reporting Services  

-   Configuration Manager 2007 webb rapporter  

-   System Center 2012 Configuration Manager och Configuration Manager aktuella gren rapporter  

-   System Center 2012 Configuration Manager och Configuration Manager aktuell gren rollbaserad administration:  

    -   Säkerhetsroller  

    -   Säkerhetsomfattningar  
