---
title: Migrera data
titleSuffix: Configuration Manager
description: Lär dig hur du överför data från en-källhierarki till en Configuration Manager målhierarkin.
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3771011f2822bb93a9569ec534b77259e2e8dc3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718905"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>Migrera data mellan hierarkier i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd migrering för att överföra data från en källhierarki som stöds till din Configuration Manager-målnod (aktuell gren). När du migrerar data från en-källhierarki:  

- Du kan komma åt data från plats databaserna i käll infrastrukturen och sedan överföra dessa data till din aktuella miljö.  

- Migreringen ändrar inte data i källhierarkin. I stället identifierar den data och lagrar en kopia i-databasen i målhierarkin.  

Tänk på följande när du planerar din strategi för migrering:  

- Du kan migrera en befintlig Configuration Manager 2007 SP2-infrastruktur till Configuration Manager (aktuell gren).  

- Du kan migrera vissa eller alla data som stöds från en källplats.  

- Du kan migrera data från en enda källplats till flera olika platser i målhierarkin.  

- Du kan flytta data från flera källplatser till en enda plats i målhierarkin.  


I följande video beskrivs och demonstreras två vanliga [scenarier för migrering](#BKMK_MigrationScenarios). Den innehåller också alternativ för att inkludera Microsoft Azure i migrations planer.
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="concepts"></a><a name="BKMK_MigrationConcepts"></a>Tryck  

 Configuration Manager använder följande begrepp och termer under migreringen.  

#### <a name="source-hierarchy"></a>Källhierarki
En hierarki som kör en version av Configuration Manager som stöds och innehåller data som du vill migrera. När du ställer in migreringen identifierar du källhierarkin när du anger platsen på den översta nivån i en-källhierarki. Efter att du har specificerat en källhierarki samlar toppnivåplatsen i målhierarkin in data från databasen för den angivna källplatsen för att identifiera de data som du kan migrera. 

Mer information finns i [käll-hierarkier](planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies).

#### <a name="source-sites"></a>Källplatser
Platserna i källhierarkin som har data som du kan migrera till din målhierarki. 

Mer information finns i [käll platser](planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites).

#### <a name="destination-hierarchy"></a>Målhierarki
En Configuration Manager-hierarki (aktuell gren) där migrering körs för att importera data från en-källhierarki.

#### <a name="data-gathering"></a>Datainsamling
Den fortlöpande processen med att identifiera informationen i källhierarkin som du kan migrera till målhierarkin. Configuration Manager kontrollerar källhierarkin enligt ett schema. Den här processen identifierar eventuella ändringar av informationen i källhierarkin som du migrerade tidigare och som du kan vilja uppdatera i målhierarkin.

Mer information finns i [data insamling](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### <a name="migration-jobs"></a>Migreringsjobb
Processen att konfigurera de specifika objekten som ska migreras och därefter hantera migreringen av dessa objekt till målhierarkin.

Mer information finns i [Planera en jobb strategi för migrering](planning-a-migration-job-strategy.md).

#### <a name="client-migration"></a>Klientmigrering
Processen att överföra information som klienterna använder från källplatsens databas till målhierarkins databas. Migreringen av data följs sedan av en uppgradering av klient program vara på enheter till klient program versionen från målhierarkin.

Mer information finns i [Planera en strategi för klient migrering](planning-a-client-migration-strategy.md).

#### <a name="shared-distribution-points"></a>Delade distributionsplatser
Distributions platserna i källhierarkin som Configuration Manager resurser med målhierarkin under migreringen.

Under migrerings perioden kan klienter som är tilldelade platser i målhierarkin hämta innehåll från delade distributions platser.

Mer information finns i [dela distributions platser mellan käll-och målhierarkin](planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration).

#### <a name="monitoring-migration"></a>Övervaka migrering
Processen att övervaka migreringsaktiviteter. Du övervakar migreringens förlopp och framgång från noden **migrering** på arbets ytan **Administration** .

Mer information finns i [Planera för att övervaka migrering av aktiviteter](planning-to-monitor-migration-activity.md).

#### <a name="stop-gathering-data"></a>Avbryta datainsamling
Processen att stoppa datainsamlingen från källplatser. När du inte längre har data som ska migreras från en-källhierarki, eller om du vill pausa migreringen av migrering, kan du konfigurera målhierarkin för att sluta samla in data från källhierarkin.

Mer information finns i [data insamling](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering).

#### <a name="clean-up-migration-data"></a>Rensa migreringsdata
Processen att slutföra migrering från en källhierarki genom att avlägsna information om migreringen från målhierarkiernas databas.

Mer information finns i [Planera för att slutföra migreringen](planning-to-complete-migration.md).



## <a name="typical-workflow"></a>Typiskt arbetsflöde  

Så här konfigurerar du ett arbets flöde för migrering:

1.  Ange en källhierarki som stöds.  

2.  Konfigurera data insamling. Med data insamling kan Configuration Manager samla in information om data som kan migreras från källhierarkin.  

     Configuration Manager upprepar automatiskt processen att samla in data med ett enkelt schema tills du avbryter data insamlings processen. Som standard upprepas data insamlings processen var fjärde timme så att Configuration Manager kan identifiera ändringar av data i källhierarkin. Data insamling är också nödvändigt för att dela distributions platser.  

3.  Ska migreringsjobb för att migrera data mellan käll- och målhierarkin.  

4.  Du kan stoppa data insamlings processen när som helst genom att använda åtgärden **Avbryt data insamling** . När du stoppar data insamlingen identifierar Configuration Manager inte längre ändringar av data i källhierarkin och kan inte längre dela distributions platser. Normalt använder du den här åtgärden när du inte längre planerar att migrera data eller dela distributionsplatser från källhierarkin.  

5.  Om data insamlingen har stoppats på alla platser för källhierarkin kan du rensa migreringen med åtgärden **Rensa migreringen** . Den här åtgärden tar bort historiska data om migrering från en källhierarki från databasen i målhierarkin.  

När du har migrerat data, och du inte längre behöver källhierarkin för att hantera enheter i din miljö, kan du inaktivera källhierarkin och infrastruktur.  



##  <a name="scenarios"></a><a name="BKMK_MigrationScenarios"></a>Olika  

 Configuration Manager har stöd för följande migrerings scenarier:
- [Migrering från Configuration Manager 2007-hierarkier](#bkmk_2007)  
- [Migrering från Configuration Manager 2012 eller en annan Configuration Manager-hierarki](#bkmk_2012)

> [!NOTE]  
>  Expansionen av en hierarki som har en fristående plats till en hierarki med en central administrations plats kategoriseras inte som en migrering. Information om hur du kan utöka hierarkin finns i [expandera en fristående primär plats](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).  


### <a name="migration-from-configuration-manager-2007-hierarchies"></a><a name="bkmk_2007"></a>Migrering från Configuration Manager 2007-hierarkier  

 När du använder migrering för att migrera data från Configuration Manager 2007 kan du behålla din investering i din befintliga plats infrastruktur och få följande fördelar:  

#### <a name="site-database-improvements"></a>Platsdatabasförbättringar
Configuration Manager-databasen (aktuell gren) stöder fullständig Unicode.

#### <a name="database-replication-between-sites"></a>Databasreplikering mellan platser
Replikering i Configuration Manager (aktuell gren) baseras på Microsoft SQL Server. Det här beteendet förbättrar prestandan för data överföring från plats till plats.

#### <a name="user-centric-management"></a>Användarcentrerad hantering
Användarna är fokus för hanterings uppgifter i Configuration Manager (aktuell gren). Du kan till exempel distribuera program vara till en användare även om du inte känner till enhets namnet för användaren. Dessutom ger Configuration Manager användare mycket mer kontroll över vilken program vara som installeras på deras enheter och när program varan installeras.

#### <a name="hierarchy-simplification"></a>Hierarkiförenkling
Configuration Manager (aktuell gren) gör det möjligt att bygga en enklare platshierarki. Den här förbättringen beror på introduktionen av den centrala administrations plats typen och ändringar av beteendet hos primära och sekundära platser. Configuration Manager (aktuell gren) använder mindre nätverks bandbredd och kräver färre servrar än tidigare versioner.

#### <a name="role-based-administration"></a>Rollbaserad administration
Den här centrala säkerhets modellen i Configuration Manager (aktuell gren) erbjuder säkerhet och hantering i hela hierarkin som motsvarar dina administrativa och affärs behov.

> [!NOTE]  
>  På grund av design ändringar som först introducerades i System Center 2012 Configuration Manager, kan du inte uppgradera Configuration Manager 2007 till Configuration Manager (aktuell gren). Uppgradering på plats stöds från System Center 2012 Configuration Manager till Configuration Manager (aktuell gren).  


### <a name="migration-from-configuration-manager-2012-or-another-configuration-manager-hierarchy"></a><a name="bkmk_2012"></a>Migrering från Configuration Manager 2012 eller en annan Configuration Manager-hierarki  
 Processen för att migrera data från en System Center 2012 Configuration Manager eller Configuration Manager hierarki är densamma. Den här processen omfattar migrering av data från flera käll-hierarkier till en hierarki med en enda mål. Du kan använda den här processen när företaget får ytterligare resurser som redan hanteras av Configuration Manager. Dessutom kan du migrera data från en test miljö till din Configuration Manager produktions miljö. Med den här processen kan du underhålla din investering i Configuration Manager test miljö.  



## <a name="see-also"></a>Se även  

-   [Planera för migrering till Configuration Manager](planning-for-migration.md)  

-   [Konfigurera käll-hierarkier och käll platser för migrering](configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Åtgärder för migrering](operations-for-migration.md)  

-   [Säkerhet och sekretess för migrering](security-and-privacy-for-migration.md)  

-   [Börja använda Configuration Manager](../servers/deploy/start-using.md)
