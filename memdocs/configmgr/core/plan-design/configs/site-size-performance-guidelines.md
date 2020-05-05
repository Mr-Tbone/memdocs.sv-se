---
title: Riktlinjer för platsstorlek och -prestanda
titleSuffix: Configuration Manager
description: Platsens storlek – relaterade prestanda test resultat, metodik och vägledning.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/23/2019
ms.openlocfilehash: 9e5cc21e4fef60f64576a7b578b3616a7e37756d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073508"
---
# <a name="configuration-manager-site-size-and-performance-guidelines"></a>Rikt linjer för Configuration Manager webbplats storlek och prestanda

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager leder branschen i skalbarhet och prestanda. Annan dokumentation täcker de [maximala skalbarhets gränserna](size-and-scale-numbers.md) och [maskin varu rikt linjerna](recommended-hardware.md) för att köra platser i de största miljö storlekarna. Den här artikeln ger kompletterande prestanda vägledning för miljöer i alla storlekar. Den här vägledningen kan hjälpa dig att korrekt beräkna den maskin vara du behöver för att distribuera Configuration Manager.

Den här artikeln fokuserar på den största bidrags givaren för att Configuration Manager prestanda Flask halsar: disk-/utdata-undersystemet eller IOPS. Artikeln:

- Visar information och test resultat som fokuserar på IOPS
- Dokument som återger testerna med dina egna miljöer och maskin vara
- Föreslår disk-IOPS-krav för olika storleks miljöer 

## <a name="performance-test-methodology"></a>Prestandatest metod

Du kan distribuera Configuration Manager på många unika sätt, men det är viktigt att förstå några få variabler i alla storleks diskussioner. En variabel är *funktions intervall*, till exempel en inventerings cykel. En annan variabel är antalet användare, program distributioner eller andra *objekt* som systemet refererar till eller distribuerar. Prestanda testningen använder dessa variabler som en del av en *belastning*. Belastningen genererar objekt i ett typiskt pris för företags kunder som använder produktions distributioner i olika storleks miljöer.

> [!NOTE] 
> Kundtelemetri-data gör det möjligt att testa den aktuella grenen bygger på de vanligaste scenarierna, konfigurationerna och inställningarna för de flesta kunder. Rekommendationerna i den här artikeln baseras på dessa genomsnitt. Dina upplevelser kan variera beroende på din miljö storlek och konfiguration. I allmänhet kräver Configuration Manager Common Sense när den kommer till objekt och intervall. Bara för att du ska kunna samla in varje fil på ett system, eller ställa in intervallet för en cykel på en minut, betyder inte det.

I följande avsnitt beskrivs några viktiga inställningar och konfigurationer som du kan använda vid testning och modellering av bearbetnings behov för stora företag. Dessa rikt linjer hjälper dig att ställa in grundläggande förväntningar för system prestanda för de föreslagna maskin varu storlekarna.

### <a name="feature-intervals-settings"></a>Inställningar för funktions intervall 
De flesta tester bör använda standard intervall för de viktigaste cyklerna i systemet. Testning av maskin varu inventering sker till exempel en gång per vecka med en större än standard- *MOF* -fil. Vissa återkommande funktions intervall, särskilt maskinvaru-och program varu inventering, kan ha betydande effekter på miljöns prestanda egenskaper. Miljöer som möjliggör aggressiva standard intervall för data insamling behöver överordnad maskin vara i direkt proportion till ökningen av aktiviteten. Anta till exempel att du har 25 000 Desktop-klienter och vill samla in maskin varu inventering två gånger snabbare än standard intervallet. Du bör börja genom att ändra platsens maskin vara på samma sätt som om du hade 50 000-klienter.

### <a name="objects"></a>Objekt 
Testerna bör använda det *övre genomsnittet* av de objekt som stora företag brukar använda med systemet. Vanliga värden är tusentals samlingar och program, som distribueras till hundratals tusen användare eller system. Testerna bör köras samtidigt på *alla* objekt i systemet vid dessa gränser. Många kunder använder flera funktioner, men använder vanligt vis inte alla funktioner i produkten i dessa övre gränser. Testning med alla produkt funktioner hjälper till att säkerställa bästa möjliga prestanda i hela systemet och tillåter en buffert för funktioner som vissa kunder kan använda över genomsnittet. 

### <a name="loads"></a>Övriga 
Testerna bör också köras på mer än *genomsnittlig genomsnittlig* inläsnings dag, genom att utföra simuleringar som genererar högsta användnings krav i systemet. Ett exempel är en simulering av korrigerings tisdags distributioner, för att se till att systemet kan returnera uppdateringens efterlevnadsprinciper vid behov under dessa dagar av topp aktivitet. Ett annat exempel är att simulera webbplats aktivitet under ett omfattande utbrott av skadlig kod, för att säkerställa att aviseringar och svar går att få så länge som möjligt. Även om distribuerade datorer av den rekommenderade storleken kan underutnyttjas under en viss dag, kräver mer extrema situationer en del bearbetnings buffert.

### <a name="configurations"></a>Konfigurationer
Kör testning på en mängd fysiska, Hyper-V-och Azure-maskinvara, med en blandning av operativ system som stöds och SQL Server versioner. Validera alltid värsta fall för den konfiguration som stöds. I allmänhet kommer Hyper-V och Azure att returnera jämförbara prestanda resultat till likvärdig fysisk maskin vara när det kon figurer ATS på liknande sätt. Nyare serveroperativ system brukar utföras på samma eller bättre sätt än äldre operativ system som stöds. Alla plattformar som stöds uppfyller minimi kraven, vanligt vis de senaste versionerna av stöd produkter som Windows och SQL ger ännu bättre prestanda. 

Den största variationen kommer från de SQL Server versioner som används. Mer information om SQL Server-versioner finns i [vilken version av SQL ska jag köra?](../../understand/site-size-performance-faq.md#what-version-of-sql-should-i-run). 

## <a name="key-performance-determinants"></a>Faktorer för nyckeltal

Du kan testa och mäta Configuration Manager prestanda med olika inställningar, på olika sätt och på olika plats storlekar. Följande inställningar och objekt kan kraftigt påverka prestandan. Var noga med att tänka på dem när du testar och modellerar prestanda i din miljö.

> [!CAUTION]
> Även om några aspekter av Configuration Manager har officiella gränser eller användar gränssnitts gränser som förhindrar alltför stor användning, kan rikt linjerna ha betydande negativa effekter på platsens prestanda. Att överskrida rekommenderade nivåer eller att ignorera storleks vägledningen kräver vanligt vis större maskin vara, och kan leda till att miljön blir försämrad tills du minskar frekvensen eller antalet olika objekt.

### <a name="hardware-inventory"></a>Maskinvaruinventering
Om du vill testa bas linje prestanda ställer du in maskin varu inventerings samlingen på en gång per vecka, med standard storleken *. MOF* -fil och cirka 20% ytterligare egenskaper. Aktivera inte alla egenskaper och samla bara in de egenskaper som du verkligen behöver. Beakta särskilt uppmärksamhet när du samlar in egenskaper, till exempel tillgängligt virtuellt minne, som *alltid* kommer att ändras med *varje* inventerings cykel. Insamling av dessa egenskaper kan orsaka överdriven omsättning på varje inventerings cykel från varje klient.

### <a name="software-inventory"></a>Programvaruinventering
Om du vill testa bas linje prestanda ställer du in program varu inventeringen på en gång per vecka, med *enbart produkt* information. Insamling av många filer kan vara en betydande belastning på inventerings under systemet. Undvik att ange filter som kan sluta samla in tusentals filer över flera klienter, till exempel * \*. exe* eller * \*. dll*.

### <a name="collections"></a>Samlingar
Grundläggande prestanda testning kan innehålla flera tusen samlingar med olika omfång, storlek, komplexitet och uppdaterings inställningar. Plats prestanda är inte en direkt funktion i Sheer antal samlingar på en plats. Prestanda är också en kors produkt av samlingars fråga om komplexitet, fullständiga och stegvisa uppdateringar och ändrings frekvens, beroenden mellan samlingar och antalet klienter i samlingarna.

Minimera om möjligt de samlingar som har dyra eller komplicerade dynamiska regel frågor. För samlingar som kräver dessa typer av regler anger du lämpliga uppdaterings intervall och uppdaterings tider för att minimera effekten av omvärdering av samlingar på systemet. Uppdatera till exempel i midnatt i stället för 8:00.

Om du aktiverar stegvisa uppdateringar av samlingar säkerställer det snabba och fort löp ande uppdateringar av samlings medlemskap. Men även om stegvisa uppdateringar är effektiva är de fortfarande belastningen på systemet. Balansera den ändrings frekvens som du förväntar dig med behovet av att uppdatera medlemskap i nära real tid. Anta till exempel att du förväntar dig tung omsättning i samlings medlemmar, men du behöver inte vänta på medlemskaps uppdateringar i nära real tid. Det är mer effektivt och ger mindre belastning på systemet för att uppdatera samlingen med en schemalagd fullständig uppdatering vid ett visst intervall, än att aktivera stegvisa uppdateringar. 

När du aktiverar stegvisa uppdateringar bör du minska schemalagda fullständiga uppdateringar på samma samlingar. De är bara en metod för säkerhets kopiering, eftersom stegvisa uppdateringar bör hålla ditt samlings medlemskap uppdaterat i nära real tid. [Metod tips för samlingar](../../clients/manage/collections/best-practices-for-collections.md#bkmk_incremental) rekommenderar maximalt antal samlingar för stegvisa uppdateringar, men när artikeln pekar ut kan din upplevelse variera beroende på många faktorer.

Samlingar med endast direkta medlemskaps regler och med en begränsande samling som inte utför stegvisa uppdateringar behöver inte schemalagda fullständiga uppdateringar. Inaktivera uppdaterings scheman för dessa typer av samlingar för att förhindra onödig belastning på systemet. Om den begränsande samlingen använder stegvisa uppdateringar kanske samlingar med endast direkta medlemskaps regler inte återspeglar medlemskaps uppdateringar i upp till 24 timmar eller tills en schemalagd uppdatering sker.

Vi rekommenderar inte att vissa organisationer skapar hundratals eller till och med tusentals samlingar som en del av olika affärs processer. Om du använder Automation för att skapa samlingar är det viktigt att du aktiverar alla nödvändiga stegvisa uppdateringar på rätt sätt. Minimera och Sprid ut alla fullständiga uppdaterings scheman för att undvika frekventa fläckar för samlings utvärdering under en och samma tids period. Upprätta en vanlig rensnings process för att ta bort oanvända samlingar, särskilt om du automatiskt skapar samlingar som du inte längre behöver efter en stund.

Kom ihåg att Configuration Manager skapar principer för alla objekt i samlingarna när du riktar in aktiviteter som distributioner till dem. Medlemskaps ändringar, antingen genom schemalagd uppdatering eller stegvisa uppdateringar, kan skapa mycket annat arbete för hela systemet. Den senaste aktuella grenen bygger har särskilda princip optimeringar för samlingarna alla system och alla användare. Använd de inbyggda samlingarna i stället för en klon av de här inbyggda samlingarna när du riktar in hela företaget.

Om du vill undersöka insamlings prestanda ännu djupare kan du använda samlings utvärderings visaren (CEViewer) i [Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012).

### <a name="discovery-methods"></a>Identifierings metoder
Vid testning av bas linje prestanda kan du köra serverbaserade identifierings metoder en gång i veckan, så att delta identifieringen är lämplig för att hålla data uppdaterade under veckan. Testerna bör upptäcka en objekt mängd som är proportionell till den simulerade företags storleken. Prestanda bas test för pulsslags identifiering bör också köras en gång i veckan.

Identifierings data är globala data. Ett vanligt problem med prestanda är att felaktigt konfigurera serverbaserade identifierings metoder i en hierarki, vilket leder till dubbla identifieringar av samma resurser från flera primära platser. Konfigurera identifierings metoder noggrant för att optimera kommunikationen med mål tjänsten, till exempel Active Directory domänkontrollanter, samtidigt som du undviker duplicering av samma identifierings omfång på flera primära platser.

## <a name="general-sizing-guidelines"></a>Rikt linjer för allmän storlek 

Enligt föregående metod för [prestandatest](#performance-test-methodology)ger följande *tabell allmänna rikt* linjer för maskin varu krav för ett visst antal hanterade klienter. De här värdena bör tillåta de flesta kunder med det angivna antalet klienter att bearbeta objekt tillräckligt snabbt för att administrera den angivna platsen. Dator kraft fortsätter att minska i priset varje år och några av kraven nedan är små vad gäller moderna maskinvarukonfigurationer för Server. Maskin vara som överskrider följande rikt linjer proportionellt ökar prestanda för platser som kräver ytterligare processor kraft eller har särskilda produkt användnings mönster. 

| Skriv bords klienter  | Typ av webbplats/roll  | Kärnor<sup>1</sup>   | Minne (GB)   | SQL-minnesallokering  | IOPS: inkorgar<sup>2</sup>  | IOPS: SQL<sup>2</sup>   | Nödvändigt lagrings utrymme (GB)<sup>3</sup>   |
|------|-------------------------------------------------------------|-----|-----|-----|------|------|------|
| 25k  | Primär-eller ca med databas plats roll på samma server   | 6   | 24  | 65% | 600  | 1700 | 350  |
| 25k  | Primär eller CAS                                              | 4   | 8   |     | 600  |      | 100  |
|      | Fjärr-SQL                                                  | 4   | 16  | 70 % |      | 1700 | 250  |
|      |                                                             |     |     |     |      |      |      |
| 50 000  | Primär-eller ca med databas plats roll på samma server   | 8   | 32  | 70 % | 1200 | 2800 | 600  |
| 50 000  | Primär eller CAS                                              | 4   | 8   |     | 1200 |      | 200  |
|      | Fjärr-SQL                                                  | 8   | 24  | 70 % |      | 2800 | 400  |
|      |                                                             |     |     |     |      |      |      |
| 100 000 | Primär-eller ca med databas plats roll på samma server   | 12  | 64  | 70 % | 1200 | 5000 | 1100 |
| 100 000 | Primär eller CAS                                              | 6   | 12  |     | 1200 |      | 300  |
|      | Fjärr-SQL                                                  | 12  | 48  | 80 % |      | 5000 | 800  |
|      |                                                             |     |     |     |      |      |      |
| 150k | Primär-eller ca med databas plats roll på samma server   | 16  | 96  | 70 % | 1800 | 7400 | 1600 |
| 150k | Primär eller CAS                                   | 8   | 16   |     | 1800  |         | 400   |
|      | Fjärr-SQL                                       | 16  | 72   | 90 % |       | 7400    | 1200  |
|      |                                                             |     |     |     |      |      |      |
| 700k | Certifikat utfärdare med databas plats roll på samma server   | 20+ | 128 + | 80 % | 1800 + | 9000 +   | 5000 + |
| 700k | CERTIFIKAT UTFÄRDARE                                              | 8 +  | 16+  |     | 1800 + |         | 500 +  |
|      | Fjärr-SQL                                       | 16+ | 96 +  | 90 % |       | 9000 +   | 4500 + |
|      |                                                             |     |     |     |      |      |      |
| 5 k   | Sekundär plats                                   | 4   | 8    |     | 500   | -       | 200   |
| k  | Sekundär plats                                   | 8   | 16   |     | 500   | -       | 300   |

**Obs!**

1. **Kärnor**: Configuration Manager utför många samtidiga processer, så behöver ett visst minsta antal processor kärnor för olika plats storlekar. Kärnan blir snabbare varje år, men det är viktigt att se till att ett visst minsta antal kärnor fungerar parallellt. I allmänhet uppfyller alla server nivå CPU: n som producerats efter 2015 grundläggande prestanda krav för de kärnor som anges i tabellen. Configuration Manager drar nytta av ytterligare kärnor utöver rekommendationerna, men vanligt vis när du har minst de föreslagna kärnorna bör du prioritera processor resurs investeringen för att öka hastigheten på befintliga kärnor, inte lägga till fler, långsammare kärnor. Configuration Manager kommer till exempel att fungera bättre för viktiga bearbetnings uppgifter med 16 snabba kärnor än med 24 långsamma kärnor, förutsatt att det finns tillräckligt med andra system resurser som disk-IOPS.
   
   Förhållandet mellan kärnor och minne är också viktigt. I allmänhet minskar den totala bearbetnings kapaciteten på SQL-servrarna med mindre än 3-4 GB RAM-minne per kärna. Du behöver mer RAM-minne per kärna när SQL är Samplacerat med plats Server komponenterna.
   
   > [!NOTE]
   > Alla tester anger maskin energi scheman för att tillåta maximal CPU-strömförbrukning och prestanda.
   
2. **IOPS: inkorgar och IOPS: SQL** avser IOPS-behoven för de Configuration Manager och logiska SQL-enheterna. I kolumnen **IOPS: inkorgar** visas IOPS-kraven för den logiska enhet där Configuration Manager-kataloger finns. I kolumnen **IOPS: SQL** visas de totala IOPS-behoven för de logiska enheter som olika SQL-filer använder. Dessa kolumner är olika eftersom de två enheterna ska ha olika format. Mer information och exempel på rekommenderade SQL-diskkonfigurationer och metod tips för filer, inklusive information om hur du delar upp filer över flera volymer finns i [vanliga frågor och svar om plats storlek och prestanda](../../understand/site-size-performance-faq.md).
   
   Båda dessa IOPS-kolumner använder data från standard verktyget *Diskspd*. Se [hur du mäter disk prestanda](#how-to-measure-disk-performance) för instruktioner om hur du duplicerar dessa mått. När du uppfyller grundläggande processor-och minnes krav har underlag rings systemet störst inverkan på plats prestanda och förbättringar här ger flest Payback på investeringen.
   
3.  **Nödvändigt lagrings utrymme:** Dessa verkliga värden kan skilja sig från andra dokumenterade rekommendationer. Vi tillhandahåller bara dessa siffror som en allmän rikt linje. enskilda krav kan variera mycket. Planera noggrant om disk utrymme måste vara före plats installationen. Anta att en del av lagrings utrymmet fortfarande är det lediga disk utrymmet i största delen av tiden. Du kan använda detta buffertutrymme i ett återställnings scenario, eller för uppgraderings scenarier som behöver ledigt disk utrymme för att utöka installations paketet. Din plats kan kräva ytterligare lagrings utrymme för stora mängder data insamling, längre perioder av datakvarhållning och stora mängder program varu distributions innehåll. Du kan också lagra dessa objekt på separata volymer med lägre data flöde.

## <a name="how-to-measure-disk-performance"></a>Hur man mäter disk prestanda 

Du kan använda *Diskspd* för bransch standard för att tillhandahålla standardiserade förslag för de IOPS som krävs för olika Configuration Manager miljöer. När du inte är uttömmande ger följande test steg och kommando rader ett enkelt och reproducerbart sätt att uppskatta dina servrars data flöde för disk under system. Du kan jämföra resultaten med minsta möjliga IOPS i [rikt linjerna för allmän storleks](#general-sizing-guidelines) kontroll. 

Se [exempel på diskkonfigurationer](#example-disk-configurations) för test resultat från olika maskinvarukonfigurationer i labb miljöer. Du kan använda data för en grov Start punkt när du utformar underlag rings systemet för en ny miljö från grunden.

### <a name="to-test-disk-iops"></a>För att testa disk-IOPS  
1. Hämta verktyget *Diskspd* här: [https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62](https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62).
   
1. Se till att du har minst 100 GB ledigt disk utrymme. Inaktivera alla appar som kan störa eller orsaka extra belastning på disken, till exempel aktiva virus genomsökningar av katalogen, SQL eller SMSExec.
   
1. Kör *Diskspd* från en upphöjd kommando tolk. 
   
   Utför två körningar av verktyget i tur och ordning för den volym som du vill testa. Det första testet utför 64K-storlek, slumpmässig Skriv åtgärder i en minut. Det här testet garanterar att inläsning av styrenhets-cache och disk utrymme tilldelas, om volymen expanderas dynamiskt. Ignorera resultatet från det första testet. Det andra testet bör *omedelbart* följa det första testet och utföra samma belastning i fem minuter.
   
   Använd till exempel följande kommando rader för att testa G:\\ -volymen.
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d60 -h -L G:\\test\testfile.dat` 
   
   `del G:\\test\testfile.dat`
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d300 -h -L G:\\test\testfile.dat`
   
1. Granska resultatet från det andra testet för att hitta total IOPS i kolumnen **i/O per s** . I följande exempel är total IOPS **3929,18**.

   ``` Output
   Total IO
   | thread |  bytes      |  I/Os   |  MB/s  | I/O per s | AvgLat | LatStdDev |
   |--------|-------------|---------|--------|-----------|--------|-----------|
   |   1    |  9651814400 |  147275 |  30.68 |    490.92 | 16.294 | 10.210    |
   |   2    |  9676652544 |  147654 |  30.76 |    492.18 | 16.252 |  9.998    |
   |   3    |  9638248448 |  147068 |  30.64 |    490.23 | 16.317 | 10.295    |
   |   4    |  9686089728 |  147798 |  30.79 |    492.66 | 16.236 | 10.072    |
   |   5    |  9590931456 |  146346 |  30.49 |    487.82 | 16.398 | 10.384    |
   |   6    |  9677242368 |  147663 |  30.76 |    492.21 | 16.251 | 10.067    |
   |   7    |  9637330944 |  147054 |  30.64 |    490.18 | 16.319 | 10.249    |
   |   8    |  9692577792 |  147897 |  30.81 |    492.99 | 16.225 | 10.125    |
   | Total: | 77250887680 | 1178755 | 245.57 |   3929.18 | 16.286 | 10.176    |
   ```

## <a name="example-disk-configurations"></a>Exempel på diskkonfigurationer

Följande tabeller visar resultat från att köra test stegen i [hur man mäter disk prestanda](#how-to-measure-disk-performance) med olika Test Lab-konfigurationer. Använd dessa data för en *grov* start punkt när du utformar underlag rings systemet för en ny miljö från grunden. 

### <a name="physical-machines-and-hyper-v"></a>Fysiska datorer och Hyper-V 
Maskin varan förbättras alltid. Vänta på nyare generationens maskin vara och olika maskin varu kombinationer, som SSD och San, för att överskrida de prestanda som anges nedan. De här resultaten är en grundläggande start punkt som du bör tänka på när du utformar en server eller diskuterar med maskin varu leverantören.

I följande tabell visas test resultaten mellan olika disk under system, inklusive disk-och SSD-baserade hård diskar, i olika testlabb-konfigurationer. Alla konfigurationer formaterar diskarna med 64 KB kluster och kopplar dem till en disk styrenhet för företags klass. Förutom disk antalet för RAID-matriser har de minst en reserv disk.

| Disktyp   | Disk antal, inte inklusive + 1 reserv disk | RAID     | IOPS mätt  |
|------------------|----------------------------------------------------|---------------|---------------|
| 15 000 SAS          | 2                                                  |           1   | 620           |
| 15 000 SAS          | 4                                                  |           10  | 1206          |
| 15 000 SAS          | 6                                                  |           10  | 1751          |
| 15 000 SAS          | 8                                                  |           10  | 2322          |
| 15 000 SAS          | 10                                                 |           10  | 2882          |
| 15 000 SAS          | 12                                                 |           10  | 3476          |
| 15 000 SAS          | 16                                                 |           10  | 4236          |
| 15 000 SAS          | 20                                                 |           10  | 5148          |
| 15 000 SAS          | 30                                                 |           10  | 7398          |
| 15 000 SAS          | 40                                                 |           10  | 9913          |
| SSD SATA         | 2                                                  |           1   | 3300          |
| SSD SATA         | 4                                                  |           10  | 5542          |
| SSD SATA         | 6                                                  |           10  | 7201          |
| SSD SAS          | 2                                                  |           1   | 7539          |
| SSD SAS          | 4                                                  |           10  | 14346         |
| SSD SAS          | 6                                                  |           10  | 15607         |

Detta är de enheter som exemplet använde. Den här informationen är inte en rekommendation för någon speciell maskin varu modell eller tillverkare. 

| Disktyp    | Modell      | RAID-styrenhet | Cache-minne och konfiguration |
|-------------------|-----------------|----------------------|-------------------------------------|
| 15 000 RPM SAS HD    | HP-EH0300JDYTH  | P822 för smart matris     | 2 GB, 20% Läs/80% skrivning           |
| SSD SATA          | ATA-MK0200GCTYV | P420i för smart matris    | 1 GB, 20% Läs/80% skrivning           |
| SSD SAS           | HP MO0800-JEFPB | P420i för smart matris    | 1 GB, 20% Läs/80% skrivning           |

### <a name="azure-machine-and-disk-performance"></a>Prestanda för Azure-datorer och diskar 
Azure disk Performance är beroende av flera faktorer, till exempel storleken på den virtuella Azure-datorn och antalet och typen av diskar som används. Azure lägger också ständigt till nya maskin typer och disk hastigheter som skiljer sig från följande diagram. Mer information om Configuration Manager som körs på Azure och ytterligare information om hur du kan förstå disk-I/O på Azure finns i [Configuration Manager på vanliga frågor och svar om Azure](../../understand/configuration-manager-on-azure.md).

Alla diskar är formaterade som NTFS 64 KB kluster storlek och rader med mer än en disk konfigureras som stripe-volymer via Windows disk hanterings verktyg.

| Azure VM| Azure-disk| Antal diskar | Tillgängligt utrymme | IOPS mätt   | Begränsa faktor   |
|--------------------------------------------|-------------------------|---------------------|---------------------------|-------|-----------------|
| **DS2/DS11**                              | P20                     | 1                   | 512 MB                    | 965   | Storlek på Azure-VM   |
| **DS2/DS11**                              | P20                     | 2                   | 1024 MB                   | 996   | Storlek på Azure-VM   |
| **DS2/DS11**                              | P30                     | 1                   | 1024 MB                   | 996   | Storlek på Azure-VM   |
| **DS2/DS11**                              | P30                     | 2                   | 2048 MB                   | 996   | Storlek på Azure-VM   |
| **DS3/DS12/F4-ENHETER**                          | P20                     | 1                   | 512 MB                    | 1994  | Storlek på Azure-VM   |
| **DS3/DS12/F4-ENHETER**                          | P20                     | 2                   | 1024 MB                   | 1992  | Storlek på Azure-VM   |
| **DS3/DS12/F4-ENHETER**                          | P30                     | 1                   | 1024 MB                   | 1993  | Storlek på Azure-VM   |
| **DS3/DS12/F4-ENHETER**                          | P30                     | 2                   | 2048 MB                   | 1992  | Storlek på Azure-VM   |
| **DS4/DS13/F8-ENHETER**                          | P20                     | 1                   | 512 MB                    | 2334  | P20 disk        |
| **DS4/DS13/F8-ENHETER**                          | P20                     | 2                   | 1024 MB                   | 3984  | Storlek på Azure-VM   |
| **DS4/DS13/F8-ENHETER**                          | P20                     | 3                   | 1536 MB                   | 3984  | Storlek på Azure-VM   |
| **DS4/DS13/F8-ENHETER**                          | P30                     | 1                   | 1024 MB                   | 3112  | P30 disk        |
| **DS4/DS13/F8-ENHETER**                          | P30                     | 2                   | 2048 MB                   | 3984  | Storlek på Azure-VM   |
| **DS4/DS13/F8-ENHETER**                          | P30                     | 3                   | 3072 MB                   | 3996  | Storlek på Azure-VM   |
| **DS5/DS14/F16-ENHETER**                         | P20                     | 1                   | 512 MB                    | 2335  | P20 disk        |
| **DS5/DS14/F16-ENHETER**                         | P20                     | 2                   | 1024 MB                   | 4639  | P20 disk        |
| **DS5/DS14/F16-ENHETER**                         | P20                     | 3                   | 1536 MB                   | 6913  | P20 disk        |
| **DS5/DS14/F16-ENHETER**                         | P20                     | 4                   | 2048 MB                   | 7966  | Storlek på Azure-VM   |
| **DS5/DS14/F16-ENHETER**                         | P30                     | 1                   | 1024 MB                   | 3112  | P30 disk        |
| **DS5/DS14/F16-ENHETER**                         | P30                     | 2                   | 2048 MB                   | 6182  | P30 disk        |
| **DS5/DS14/F16-ENHETER**                         | P30                     | 3                   | 3072 MB                   | 7963  | Storlek på Azure-VM   |
| **DS5/DS14/F16-ENHETER**                         | P30                     | 4                   | 4096 MB                   | 7968  | Storlek på Azure-VM   |
| **DS15**                                  | P30                     | 1                   | 1024 MB                   | 3113  | P30 disk        |
| **DS15**                                  | P30                     | 2                   | 2048 MB                   | 6184  | P30 disk        |
| **DS15**                                  | P30                     | 3                   | 3072 MB                   | 9225  | P30 disk        |
| **DS15**                                  | P30                     | 4                   | 4096 MB                   | 10200 | Storlek på Azure-VM   |

## <a name="see-also"></a>Se även

- [Vanliga frågor och svar om webbplats storlek och prestanda](../../understand/site-size-performance-faq.md)
- [Configuration Manager vanliga frågor och svar om Azure](../../understand/configuration-manager-on-azure.md)
- [Antal och gränsvärden](size-and-scale-numbers.md)
- [Rekommenderad maskinvara](recommended-hardware.md)

