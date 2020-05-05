---
title: Vanliga frågor och svar om plats storlek och prestanda
titleSuffix: Configuration Manager
description: Svar på vanliga Configuration Manager frågor om plats storlek och prestanda.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 3e7b9f6bc861ef5a60e4c0857dc253e3c806a851
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073270"
---
# <a name="configuration-manager-site-sizing-and-performance-faq"></a>Vanliga frågor och svar om Configuration Manager webbplats storlek och prestanda

*Gäller för: Configuration Manager (aktuell gren)*

Det här dokumentet behandlar vanliga frågor om Configuration Manager webbplats storleks vägledning och vanliga prestanda problem.

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>Vanliga frågor och svar om dator-och disk konfiguration

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>Hur ska jag formatera diskarna på min plats Server och SQL Server?

Avgränsa Configuration Manager inkorgar och SQL-filer på minst två olika volymer. Med den här separationen kan du optimera kluster tilldelnings storlekarna för de olika typerna av I/O som de utför. 

För den volym som är värd för plats serverns inkorgar använder du NTFS med 4K-eller 8K-allokeringsenheter. ReFS skriver 64 KB även för små filer. Configuration Manager har många små filer kan ReFS skapa onödig disk belastning.

För diskar som innehåller SQL Database-filer använder du NTFS-eller ReFS-formatering med 64 KB-allokeringsenheter.

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>Hur och var ska jag placera mina SQL Database-filer?

Moderna matriser av solid state-hårddiskar (SSD) och Azure Premium Storage kan ge hög IOPS på en enda volym, med få diskar. Du lägger normalt till fler enheter i en matris för ytterligare lagring, inte ytterligare data flöde. Om du använder fysiska diskbaserade diskar kan du behöva fler IOPS än du kan generera på en enskild volym. Du bör allokera 60% av den totala rekommenderade IOPS och disk utrymme för *. mdf* -filen, 20% för *. ldf* -filen och 20% för logg-och data temporära filer. *LDF* -och temp-filerna kan alla finnas på en enda volym med 40% (20% + 20%) av din allokerade IOPS.

SQL-servrar som är tidigare än SQL Server 2016 skapas som standard bara en temporär data fil. Du bör skapa mer för att undvika SQL-lås och vänta på åtkomst till en enskild fil. Community-åsikter varierar med det bästa antalet temporära datafiler att skapa, från fyra till åtta. Testningen visar en liten skillnad mellan fyra och åtta, så du kan skapa fyra *lika stora* Temp-datafiler. Dina tempdb-datafiler bör vara upp till 20-25% av storleken på din fullständiga databas.

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>Finns det några andra rekommendationer för disk installationen?

Vid konfigurering kan du ställa in RAID-styrenhetens minne på 70% allokering för Skriv åtgärder och 30% för Läs åtgärder. I allmänhet använder du en RAID 10 mat ris konfiguration för plats databasen. RAID 1 är också acceptabelt för små platser med låga I/O-krav, eller om du använder snabb SSD. Med större disk mat ris konfigurerar du reserv diskar för att automatiskt ersätta misslyckade diskar.

**Exempel: fysisk dator med fysiska diskar** 

[Storleks rikt linjer](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) för en samplacerad plats Server och SQL server med **100 000** -klienter är 1200 IOPS för plats Server inkorgar och 5000 IOPS för SQL Server filer.

Den resulterande disk konfigurationen kan se ut så här:

| Enheter<sup>1</sup> | RAID | Format | Volym innehåll | Lägsta IOPS som behövs| Ca. IOPS angavs<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10k          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | NTFS-8k     | ConfigMgr-inkorgar    |     1700            | 1751             |
| 12x15k         | 10        | 64K-referenser    | SQL. mdf             | 60% * 5000 = 3000     | 3476             |
| 8x15k          | 10        | 64K-referenser    | SQL. ldf, temporära filer | 40% * 5000 = 2000     | 2322             |

1. Innehåller inte rekommenderade reserv diskar. 
2. Det här värdet är [exempel på diskkonfigurationer](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>Jag använder Hyper-V på Windows Server. Hur konfigurerar jag diskarna för mina Configuration Manager virtuella datorer för bästa prestanda?

Hyper-V levererar liknande prestanda till en fysisk server, om maskin varu resurser (processor kärnor och direkt lagring) är 100% dedikerade till den virtuella datorn (VM). Om du använder *VHD* -eller *VHDX* -filer med fast storlek får du en minimal prestanda på 1-5% I/O. Om du använder dynamiskt expanderande *. VHD* -eller *. vhdx* -diskpartitioner får du upp till 25% i/O prestanda påverkan för Configuration Manager arbets belastningen. Om du behöver expandera diskar dynamiskt kan du kompensera genom att lägga till ytterligare 25% IOPS-prestanda i matrisen.

När du kör din Configuration Manager plats Server eller SQL inuti en virtuell dator isolerar du Hyper-V-värdens OS-enheter från VM-OS och data enheter.

Mer information om hur du optimerar virtuella datorer finns i [prestanda justering Hyper-V-servrar](/windows-server/administration/performance-tuning/role/hyper-v-server/).

**Exempel: plats Server för virtuell Hyper-V-baserad plats** 

[Storleks rikt linjer](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) för en samplacerad plats Server och SQL server med **150 000** -klienter är 1800 IOPS för plats Server inkorgar och 7400 IOPS för SQL Server filer.

Den resulterande disk konfigurationen kan se ut så här:

| Enheter<sup>1</sup> | RAID | Format<sup>2</sup> | Volym innehåll | Lägsta IOPS som behövs| Ca. IOPS angavs<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10k          | 1         | -              | Hyper-V-värd-OS           | -                    | -                |
| 2x10k          | 1         | -              | (VM) plats serverns operativ system       | -                    | -                |
| 2xSSD SAS      | 1         | NTFS-8k        | (VM) ConfigMgr-inkorgar    | 1800                 | 7539             |
| 4xSSD SAS      | 10        | 64K-referenser       | (VM) värd-SQL (alla filer) | 7400                 | 14346            |

1. Innehåller inte rekommenderade reserv diskar. 
2. Fast storlek, vidarekoppling *. vhdx* för den virtuella dator enhet som är dedikerad till den underliggande volymen. 
3. Det här värdet är [exempel på diskkonfigurationer](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>Finns det några förslag på Configuration Manager miljöer i Microsoft Azure?

Börja med att läsa [Configuration Manager på vanliga frågor och svar om Azure](configuration-manager-on-azure.md).

Azure Infrastructure as a Service (IaaS) virtuella datorer som använder Premium Storage-baserade diskar kan ha höga IOPS. På de här virtuella datorerna konfigurerar du ytterligare diskar för förväntade disk utrymmes behov, i stället för ytterligare IOPS.

Azure Storage är i själva fall redundant och kräver inte flera diskar för tillgänglighet. Du kan lägga till stripe-diskar i Disk Manager eller lagrings utrymmen för att ge ytterligare utrymme och prestanda.

Mer information och rekommendationer om hur du maximerar Premium Storage prestanda och kör SQL-servrar i virtuella Azure IaaS-datorer finns i:

- [Optimera program prestanda](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [Vägledning för diskar](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**Exempel: Azure-baserad plats Server** 

[Storleks rikt linjer](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) för en samplacerad plats Server och SQL server med **50 000** -klienter är åtta kärnor, 32 GB och 1200 IOPS för plats Server inkorgar och 2800 IOPS för SQL Server filer.

Den resulterande Azure-datorn kan vara en DS13v2 (åtta kärnor, 56 GB) med följande disk konfiguration:

| Enheter | Format | Innehåller | Lägsta IOPS som behövs| Ca. IOPS angavs<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standard&gt; | -             | OS för plats Server     | -                    | -                |
| 1xP20 (512 GB)    | NTFS-8k       | ConfigMgr-inkorgar  | 1200                 | 2334             |
| 1xP30 (1024 GB)   | 64K-referenser      | SQL (alla filer<sup>2</sup>) | 2800                 | 3112             |

1. Det här värdet är [exempel på diskkonfigurationer](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations).
2. Med [Azures vägledning](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) kan du placera tempdb på den lokala SSD-baserade *D:* -enheten, eftersom den inte överskrider det tillgängliga utrymmet och ger ytterligare disk-I/O-distribution.

**Exempel: Azure-baserad plats Server (för omedelbar prestanda ökning)** 

Azure disk data flöde begränsas av storleken på den virtuella datorn. Konfigurationen i föregående Azure-exempel kan begränsa framtida expansion eller ytterligare prestanda. Om du lägger till ytterligare diskar under den första distributionen av din virtuella Azure-dator kan du utvidga din virtuella Azure-dator för ökad bearbetnings kraft i framtiden, med minsta möjliga start investering. Det är mycket enklare att planera framåt för att öka platsens prestanda när kraven ändras, i stället för att senare behöver göra en mer komplicerad migrering.

Ändra diskarna i föregående Azure-exempel för att se hur IOPS förändras.

**DS13v2** 

| Enheter<sup>1</sup> | Format | Innehåller | Lägsta IOPS som behövs| Ca. IOPS angavs<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standard&gt; | -             | OS för plats Server     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS-8k       | ConfigMgr-inkorgar  | 1200                 | 3984             |
| 2xP30 (2048 GB)   | 64K-referenser      | SQL (alla filer<sup>3</sup>) | 2800                 | 3984             |

1. Diskar stripas med lagrings utrymmen.
2. Det här värdet är [exempel på diskkonfigurationer](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). Prestanda för VM-storlek begränsar.
3. Med [Azures vägledning](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) kan du placera tempdb på den lokala SSD-baserade *D:* -enheten, eftersom den inte överskrider det tillgängliga utrymmet och ger ytterligare disk-I/O-distribution.

Om du behöver mer prestanda i framtiden kan du utvidga den virtuella datorn till en DS14v2, vilket kommer att ha dubbla CPU och minne. Den ytterligare disk bandbredden som tillåts av den virtuella dator storleken kommer också att öka den tillgängliga disk-IOPS omedelbart på dina tidigare konfigurerade diskar.

**DS14v2**

| Enheter<sup>1</sup> | RAID | Format | Innehåller | Lägsta IOPS som behövs| Ca. IOPS angavs<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standard&gt; | -             | OS för plats Server     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS-8k       | ConfigMgr-inkorgar  | 1200                 | 4639             |
| 2xP30 (2048 GB)   | 64K-referenser      | SQL (alla filer<sup>3</sup>) | 2800                 | 6182             |

1. Diskar stripas med lagrings utrymmen.
2. Det här värdet är [exempel på diskkonfigurationer](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). Prestanda för VM-storlek begränsar.
3. Med [Azures vägledning](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) kan du placera tempdb på den lokala SSD-baserade *D:* -enheten, eftersom den inte överskrider det tillgängliga utrymmet och ger ytterligare disk-I/O-distribution.

## <a name="other-common-sql-server-related-performance-questions"></a>Andra vanliga SQL Server-relaterade prestanda frågor 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>Är det bättre att köra med SQL som finns på plats servern eller att köra den på en fjärrserver?

Båda kan utföras på rätt sätt, förutsatt att den enskilda servern har rätt storlek, eller om nätverks anslutningen räcker mellan de två servrarna.

SQL fjärr-SQL kräver en ytterligare servers drifts-och drift kostnad, men det är vanligt i stor skala kunder. Fördelarna med den här konfigurationen är:

- Förbättrade alternativ för webbplats tillgänglighet, till exempel SQL Always on
- Möjlighet att köra tung rapportering med mindre överbelastade plats bearbetning
- Enklare katastrof återställning i vissa situationer
- Enklare säkerhets hantering
- Separering av roller för SQL-hantering, t. ex. med ett separat DBA-team

Samplacerad SQL kräver en enskild server och är vanligt för de flesta små och stora kunder. Fördelarna med den här konfigurationen är:

- Lägre kostnader för datorer, licenser och underhåll
- Färre felplatser på platsen
- Bättre kontroll för planerings stillestånd

### <a name="how-much-ram-should-i-allocate-for-sql"></a>Hur mycket minne ska jag allokera för SQL?

Som standard använder SQL allt tillgängligt minne på servern, vilket kan svälter operativ systemet och andra processer på datorn. För att undvika potentiella prestanda problem är det viktigt att allokera minne till SQL explicit. På plats servrar som samplaceras med SQL-servrar kontrollerar du att operativ systemet har tillräckligt med RAM-minne för cachelagring av filer och andra åtgärder. Se till att det finns tillräckligt med RAM-minne för SMSExec och andra Configuration Managers processer. När du kör SQL på en fjärrserver kan du allokera *merparten* av minnet till SQL, men inte alla. Läs igenom [storleks rikt linjerna](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) för inledande vägledning. 

SQL Server minnes tilldelningen ska avrundas till hela GB. När RAM-minnet ökar till stora mängder kan du dessutom låta SQL ha en högre procent andel. Om till exempel 256 GB eller mer RAM-minne är tillgängligt kan du konfigurera SQL för upp till 95%, eftersom det fortfarande bevarar tillräckligt med minne för operativ systemet. Att övervaka växlings filen är ett bra sätt att se till att det finns tillräckligt med minne för operativ systemet och Configuration Manager processer.

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>Kärnor är billiga i dessa dagar. Bör jag bara lägga till en massa av dem till min SQL Server?

Du kan stöta på problem med minnes konkurrens om det finns fler än 16 fysiska kärnor och inte tillräckligt med RAM-minne på SQL-servern. Configuration Manager-arbetsbelastningen fungerar bättre när minst 3-4 GB RAM-minne per kärna är tillgängligt för SQL. När du lägger till kärnor till dina SQL-servrar måste du öka RAM-minnet i proportionella mängder.

### <a name="will-sql-always-on-impact-my-performance"></a>Kommer SQL alltid att påverka min prestanda?

I allmänhet har SQL Always on en försumbar effekt på systemets prestanda när tillräckligt många nätverk är tillgängliga mellan SQL-replik servrarna. Du kan ha snabb databas logg *. ldf* -Filtillväxt i en upptaget SQL Always on-miljö. Logg fils utrymmet släpps dock automatiskt efter en lyckad säkerhets kopiering av databasen. Lägg till ett SQL-jobb för Configuration Manager databasen för att utföra en säkerhets kopiering, till exempel var 24: e timme och en *. ldf* -säkerhetskopiering var sjätte timme. Mer information om SQL Always on och Configuration Manager, inklusive mer om strategier för SQL-säkerhetskopiering, finns i [SQL Server Always on för en plats databas med hög](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)tillgänglighet.

### <a name="should-i-enable-sql-compression-on-my-database"></a>Ska jag aktivera SQL-komprimering på databasen?

SQL-komprimering rekommenderas inte för den Configuration Manager databasen. Även om det inte finns några funktionella problem med att aktivera komprimering på en Configuration Manager-databas, visar test resultaten inte mycket storleks besparingar jämfört med de potentiella skalbara prestanda som påverkar systemet.

### <a name="should-i-enable-sql-encryption-on-my-database"></a>Ska jag aktivera SQL-kryptering i min databas?

Alla hemligheter i Configuration Manager-databasen lagras redan på ett säkert sätt, men om du lägger till SQL-kryptering kan du lägga till ännu ett säkerhets lager. Det finns inga funktions problem med att aktivera kryptering i databasen, men det kan vara upp till 25% prestanda försämring, beroende på vilka tabeller du väljer att kryptera och vilken version av SQL du använder. Därför bör du kryptera med försiktighet, särskilt i storskaliga miljöer. Kom även ihåg att uppdatera dina säkerhets kopierings-och återställnings planer så att du kan återställa krypterade data.

### <a name="what-version-of-sql-should-i-run"></a>Vilken version av SQL ska jag köra?

Information om vilka SQL-versioner som stöds finns i [stöd för SQL Server-versioner](../plan-design/configs/support-for-sql-server-versions.md). Från en prestanda synpunkt uppfyller alla versioner av SQL som stöds de nödvändiga prestanda villkoren. SQL 2012 och SQL 2016 eller nyare tenderar att avsevärt SQL 2014 i vissa delar av Configuration Manager arbets belastningen. Att köra SQL 2014 på kompatibilitetsnivån för SQL 2012 (110) förbättrar dessutom prestanda i allmänhet. Vid installationen ställs Configuration Manager-databaser som körs på SQL 2012 och SQL 2014 in på kompatibilitetsnivån 110. SQL 2016 eller senare har angetts till SQL-versionens standard kompatibilitetsnivå, till exempel 130 för SQL 2016. Om du uppgraderar SQL på plats uppdateras inte kompatibilitetsnivån förrän du installerar nästa större Configuration Manager aktuella gren versionen. 

Om du ser ovanliga tids gränser eller långsamma på vissa SQL-frågor på SQL 2016 eller senare, till exempel när du använder RBAC i administratörs konsolen, kan du försöka ändra SQL-kompatibilitetsnivån på Configuration Manager databasen till 110. Att köra på SQL-kompatibilitetsnivån 110 på SQL 2014 och senare versioner av SQL stöds fullt ut. Mer information finns i [tids gränsen för SQL-frågor eller konsolen är långsam på vissa Configuration Manager databas frågor](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d).

Från och med januari 2018 bör du *undvika* följande SQL-versioner, på grund av olika kända prestanda eller andra potentiella problem:

- SQL 2012 SP3-CU1 till CU5
- SQL 2014 SP1 CU6 till SP2 CU2
- SQL 2016 RTM till CU3, SP1 CU3 till CU5

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>Bör jag implementera eventuella ytterligare SQL-indexerings uppgifter?

Ja, uppdatera indexen så ofta som en gång i veckan och statistiken så ofta som en gång om dagen för att förbättra SQL-prestanda. Skript från tredje part och ytterligare information som är tillgänglig från Configuration Manager och SQL-communities kan hjälpa till att optimera dessa uppgifter.

På stora platser kan vissa SQL-tabeller, till exempel\_CI CurrentComplianceStatusDetails, HinvChangeLog, vara stora, beroende på dina användnings mönster. Du kan behöva minska eller ändra underhålls metoden för dem en i taget.

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>När ska jag använda fullständig SQL Server i stället för SQL Express på mina sekundära platser?

SQL Express har inga betydande prestanda effekter på sekundära platser och det räcker för de flesta kunder. Det är också enkelt att distribuera och hantera och är den rekommenderade konfigurationen för nästan alla kunder i valfri storlek.

Det finns en situation där en fullständig SQL Server installation kan behövas. Om du har ett stort antal distributions platser och paket eller källor i din miljö, är det möjligt att överskrida storleks gränsen på 10 GB för SQL Express. Om antalet paket gånger som antalet distributions platser är mer än 4 000 000, till exempel 2 000 DPs med 2 000 innehålls delar, bör du överväga att använda fullständig SQL Server på dina sekundära platser. 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>Bör jag ändra MaxDOP-inställningar på databasen?

Om du lämnar inställningen 0 (Använd alla tillgängliga processorer) är den optimala för övergripande bearbetnings prestanda i de flesta fall.

Många Configuration Manager-administratörer följer rikt linjerna [för rekommendationer och rikt linjer för konfigurations alternativet "Max grad av parallellitet" i SQL Server](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi). I den flesta moderna stora maskin vara leder den här vägledningen till en föreslagen högsta inställning på åtta. Men om du kör många mindre frågor jämfört med ditt antal processorer kan det vara bättre att ange ett högre antal. Att begränsa dig till åtta är inte nödvändigt vis den bästa inställningen på större platser när fler kärnor är tillgängliga. 

På SQL-servrar med fler än åtta kärnor börjar du med inställningen 0 och gör bara ändringar om det uppstår prestanda problem eller överdriven låsning. Om du behöver ändra MaxDOP eftersom du påträffar prestanda problem vid 0 börjar du med ett nytt värde som är minst större än eller lika med det minsta rekommenderade antalet kärnor för den platsens SQL Server-storlek. Lägre än det här värdet har nästan alltid negativa prestanda effekter. Till exempel måste en fjärran sluten SQL Server för en 100 000-klient plats minst 12 kärnor. Om SQL-servern har 16 kärnor börjar du testa din MaxDOP-inställning med värdet 12.

## <a name="other-common-performance-related-questions"></a>Andra vanliga frågor om prestandarelaterade prestanda

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>Vilka mappar på plats servern (eller andra roller) ska jag undanta för antivirus program?

Var försiktig när du inaktiverar Antivirus skydd på alla system. I stora volymer och säkra miljöer rekommenderar vi att du inaktiverar *aktiv övervakning* för optimala prestanda.

Mer information om rekommenderade Antivirus undantag finns i [rekommenderade Antivirus undantag för Configuration Manager 2012 och Current Branch plats servrar, plats system och klienter](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu).

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>Vad kan jag göra för att utföra WSUS bättre när den används med Configuration Manager?

Att ändra några viktiga IIS-inställningar, t. ex. WsusPool Kölängd och WsusPool privat minnes gräns, kan förbättra WSUS-prestanda, även vid mindre installationer. Mer information finns i [Rekommenderad maskin vara](../plan-design/configs/recommended-hardware.md).

Kontrol lera också att du har de senaste uppdateringarna installerade för operativ systemet som kör WSUS:

- Windows Server 2012: alla icke-säkerhetssamlade uppdateringar som inte är "säkerhet", som lanserades den 2017 eller senare. ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2: alla icke-säkerhetssamlade uppdateringar som inte är "säkerhet" lanserades 2017 eller senare. ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Window Server 2016: alla icke-säkerhetssamlade uppdateringar som inte är "säkerhet" lanserades 2017 eller senare. ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>Vilken typ av underhåll ska jag köra på mina WSUS-servrar?

Se [den fullständiga guiden för Microsoft WSUS och Configuration Manager SUP-underhåll](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint).

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>Jag vill konfigurera grundläggande prestanda övervakning för min webbplats. Vad ska jag titta på?

Traditionell övervakning av Server prestanda fungerar effektivt för allmänna Configuration Manager. Du kan också använda de olika System Center Operations Manager hanterings paketen för Configuration Manager, SQL Server och Windows Server för att övervaka serverns grundläggande hälso tillstånd. Du kan också direkt övervaka prestanda räknare för Windows Performance Monitor (PerfMon) Configuration Manager tillhandahåller. Övervaka de olika inkorgarna i de olika inkorgarna för tidiga varnings tecken på potentiella problem med plats prestanda eller efter släpning.

## <a name="see-also"></a>Se även

- [Rikt linjer för webbplats storlek och prestanda](../plan-design/configs/site-size-performance-guidelines.md)
- [Configuration Manager vanliga frågor och svar om Azure](configuration-manager-on-azure.md)
