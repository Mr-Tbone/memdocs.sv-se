---
title: Check lista för 1606
titleSuffix: Configuration Manager
description: Lär dig mer om åtgärder som ska vidtas innan du uppdaterar från Configuration Manager version 1511 eller 1602 till version 1606.
ms.date: 06/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 95da730a6978c235fcae6a1d05b7984486abdaeb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723084"
---
# <a name="checklist-for-installing-update-1606-for-configuration-manager"></a>Check lista för att installera uppdatering 1606 för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Version 1606 för Configuration Manager aktuella grenen är en uppdatering som du kan använda för att uppdatera från version 1511 eller 1602.

Innan du installerar version 1606 som en uppdatering bör du gå igenom följande information och check lista för åtgärder som ska vidtas innan du startar uppdateringen.

Information om bas linje versioner finns i [bas linje-och uppdaterings versioner](../../../core/servers/manage/updates.md#bkmk_Baselines) i [uppdateringar för Configuration Manager](../../../core/servers/manage/updates.md).

## <a name="about-installing-update-1606"></a>Om hur du installerar uppdatering 1606

Som en *uppdatering*kan 1606 bara installeras på platsen på den översta nivån i hierarkin. Det innebär att du startar installationen från den centrala administrations platsen om du har en, eller från din fristående primära plats.  

- Underordnade primära platser installerar uppdateringen automatiskt när den centrala administrations platsen har slutfört installationen av uppdateringen. Du kan använda Service Windows för att styra när en plats installerar uppdateringar. Före version 1606 kallades Service Windows för underhålls fönster. Mer information finns i [Service Windows for Site servers](service-windows.md).  

- Du måste manuellt uppdatera sekundära platser inifrån Configuration Manager-konsolen när den primära överordnade platsen har slutfört installationen av uppdateringen. Automatisk uppdatering av sekundära platsservrar stöds inte.  

När plats servern installerar uppdateringen uppdateras plats system roller som är installerade på plats servern och de som är installerade på fjärrdatorer automatiskt. Innan du installerar uppdateringen måste du därför kontrol lera att varje plats system Server uppfyller eventuella nya krav för åtgärder med den nya uppdaterings versionen.  

Första gången du använder en Configuration Manager-konsol efter att uppdateringen har installerats uppmanas du att uppdatera konsolen.  Om du vill göra det måste du köra Configuration Manager-installationen på den dator som är värd för-konsolen och sedan välja alternativet för att uppdatera konsolen. Vi rekommenderar att du inte väntar med att installera uppdateringen av konsolen.

**Kända problem för den här uppdateringen**   
Följande problem gäller när du visar installations status för uppdaterings paketet:
- När du uppdaterar från version 1602 till 1606 visar steget **extrahera uppdaterings paket** en status som **inte har startats**, även om nedladdningen har slutförts.
- När du uppdaterar från version 1511 till 1606 visar vissa steg statusen **slutförd** men visar inte ett värde för **senaste uppdaterings tid**.


## <a name="checklist"></a>Checklista  

**Se till att alla platser kör en version av Configuration Manager som stöds:**  Innan du påbörjar installationen av uppdatering 1606 måste varje plats server i hierarkin köra samma version av Configuration Manager: antingen version 1511 eller 1602.

**Granska installerade Microsoft.net-versioner på plats system servrar:** När en plats installerar uppdatering 1606 installeras Configuration Manager automatiskt .NET Framework 4.5.2 på varje dator som är värd för någon av följande plats system roller (om .NET Framework 4,5 eller senare inte redan är installerad):  

- Registreringsproxyplats  

- Registreringsplats  

- Hanteringsplats  

- Tjänstanslutningspunkt  

Den här installationen kan försätta plats system servern i ett väntande tillstånd för omstart och rapportera fel till visnings programmet för Configuration Manager komponent status. .NET-program på servern kan dessutom ha slumpmässiga fel innan servern startas om.  

Mer information finns i [krav för plats och plats system](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

**Granska statusen för platsen och hierarkin och kontrollera om det finns några fel som inte har åtgärdats:** Innan du uppdaterar en plats löser du alla operativa problem som finns på platsservern, platsdatabasservern och i platssystemrollerna som är installerade på fjärrdatorer. En platsuppgradering kan misslyckas på grund av befintliga operativa problem.

Mer information finns i [använda aviseringar och status systemet för Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

**Granska fil- och datareplikeringen mellan platser:**  Se till att fil- och databasreplikeringen mellan platser fungerar och är aktuell. Fördröjningar eller efter släpning i kan antingen förhindra en smidig och lyckad uppdatering.    

För databasreplikering kan du använda funktionen för replikeringslänkanalys för att lösa eventuella fel innan du startar uppdateringen. Mer information finns i [om Replikeringslänkanalys](monitor-replication.md#BKMK_RLA).  


**Installera alla tillämpliga viktiga uppdateringar för operativ system på datorer som är värdar för platsen, plats databas servern och fjärrplatsens system roller:** Innan du installerar en uppdatering för Configuration Manager bör du installera eventuella kritiska uppdateringar för varje tillämpligt plats system. Om en uppdatering som du installerar kräver en omstart, startar du om de tillämpliga datorerna innan du påbörjar uppgraderingen.  

**Inaktivera databas repliker för hanterings platser på primära platser:** Configuration Manager kan inte uppdatera en primär plats som har en databas replik för hanterings platser aktive rad. Inaktivera databasreplikering innan du installerar en uppdatering för Configuration Manager.  

Mer information finns i [databas repliker för hanterings platser för Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Ange SQL Server AlwaysOn-tillgänglighetsgrupper till manuell redundans:**  
Innan du installerar uppdateringar, till exempel version 1606, kontrollerar du att tillgänglighets gruppen är inställd på manuell redundans. När platsen har uppdaterats kan du återställa redundansen till automatisk. Mer information finns i [SQL Server AlwaysOn för en plats databas](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

**Konfigurera om program uppdaterings platser som använder NLB:** Configuration Manager kan inte uppdatera en plats som använder ett NLB-kluster (utjämning av nätverks belastning) som värd för program uppdaterings platser.  

Om du använder NLB-kluster för program uppdaterings platser kan du använda Windows PowerShell för att ta bort NLB-klustret.    

Mer information finns i [Planera för program uppdateringar](../../../sum/plan-design/plan-for-software-updates.md).  

**Inaktivera alla plats underhålls aktiviteter på varje plats under installationen av uppdateringen på platsen:** Innan du installerar uppdateringen inaktiverar du alla plats underhålls aktiviteter som kan köras under den tid som uppdaterings processen är aktiv. Detta omfattar men är inte begränsat till följande:  

- Platsserver för säkerhetskopiering  

- Ta bort föråldrade klientåtgärder  

- Ta bort föråldrade identifieringsdata  

Om en underhållsaktivitet för platsdatabasen körs under installationen av uppdateringen kan installationen av uppdateringen misslyckas. Innan du inaktiverar en aktivitet registrerar du schemat för aktiviteten så att du kan återställa dess konfiguration när uppdateringen har installerats.  

Mer information finns i [underhålls aktiviteter för Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) och [referens för underhålls aktiviteter för Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Stoppa tillfälligt antivirus program på Configuration Manager servrar:** Innan du uppdaterar en plats kontrollerar du att du har stoppat antivirus program på Configuration Manager-servrarna. <!--SMS.503481--> 

**Skapa en säkerhetskopia av platsdatabasen på den centrala administrationswebbplatsen och de primära platserna:** Innan du uppdaterar en plats säkerhetskopierar du platsdatabasen för att säkerställa att du har en säkerhetskopia som du kan använda vid katastrofåterställning.   

Mer information finns i [säkerhets kopiering och återställning för Configuration Manager](backup-and-recovery.md).  

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** Before you update a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

- You should test the site database upgrade process because when you upgrade a site, the site database might be modified.  

- Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.  

- A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.  

- Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.  

- If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.  

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.   

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, For more information, see [Step 2: Test the database upgrade before installing an update](install-in-console-updates.md#bkmk_step2) from **Before you install an in-console update**.
-->

**Planera för klient pilot:** När du installerar en uppdatering som uppdaterar klienten kan du testa den nya klient uppdateringen i för produktion innan den distribueras och uppgraderar alla dina aktiva klienter.   

Om du vill utnyttja det här alternativet innan du påbörjar installationen av uppdateringen måste du konfigurera platsen så att den stöder automatiska uppgraderingar för för produktion. Mer information finns i [Uppgradera klienter](../../../core/clients/manage/upgrade/upgrade-clients.md) och   
[Testa klient uppgraderingar i en för produktions samling](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**Planera att använda service fönster för att styra när plats servrar installerar uppdateringar:** Du kan använda Service Windows för att definiera en period under vilken uppdateringar av en plats Server kan installeras.

Detta kan hjälpa dig att styra när platser i hierarkin installerar uppdateringen.
Före version 1606 kallades Service Windows för underhålls fönster. Mer information finns i [Service Windows for Site servers](service-windows.md).  

**Kör krav kontrollen för installation:**  Innan du installerar uppdatering 1606 kan du köra krav kontrollen oberoende av installationen av uppdateringen. När du installerar uppdateringen på platsen körs krav kontrollen igen.  

Mer information finns i **steg 3: kör krav kontrollen innan du installerar en uppdatering** i avsnittet [uppdateringar för Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) .  

> [!IMPORTANT]  
> När krav kontrollen körs fristående eller som en del av en uppdaterings installation uppdaterar processen vissa produkt käll filer som används för plats underhålls aktiviteter. När du har kört krav kontrollen men innan du installerar 1606-uppdateringen måste du därför köra **setupwpf. exe** (Configuration Manager installationen) från CD: n för att utföra en plats underhålls uppgift. Den senaste mappen på plats servern.  

**Uppdatera platser:** Du är nu redo att starta installationen av uppdateringen för hierarkin.  
Vi rekommenderar att du planerar att installera uppdateringen utanför normal kontors tid för varje plats, när processen för att installera uppdateringen och dess åtgärder för att installera om plats komponenter och plats system roller har minst påverkan på din affärs verksamhet.

Mer information finns i [uppdateringar för Configuration Manager](../../../core/servers/manage/updates.md).  
