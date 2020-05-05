---
title: Databasreplikering
titleSuffix: Configuration Manager
description: Lär dig hur Configuration Manager databasreplikering använder SQL Server för att överföra data i hierarkin.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b495b02-c966-4eb3-92b9-52ebbf5c38ae
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d1a2c8baa349e6499aa483f947d94f7459357be4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720200"
---
# <a name="database-replication"></a>Databasreplikering

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager databasreplikering använder SQL Server för att överföra data. Den här metoden använder den här metoden för att slå samman ändringar i dess plats databas med informationen från databasen på andra platser i hierarkin.

Observera följande saker om databasreplikering:

- Alla platser delar samma information.  

- När du installerar en plats i en hierarki etablerar Configuration Manager automatiskt databasreplikering mellan den nya platsen och dess överordnade plats.  

- När plats installationen är klar startas databasreplikering automatiskt.  

När du lägger till en ny plats i en hierarki skapar Configuration Manager en generisk databas på den nya platsen. Den överordnade platsen skapar en ögonblicks bild av relevanta data i databasen. Den överför sedan ögonblicks bilden till den nya platsen med hjälp av [filbaserad replikering](file-based-replication.md). Den nya platsen använder sedan SQL Server Mass kopierings program (BCP) för att läsa in informationen till den lokala kopian av Configuration Manager-databasen. När ögonblicksbilden har lästs in utför varje plats en databasreplikering med den andra platsen.  

För att replikera data mellan platser använder Configuration Manager sin egen databasreplikering. Tjänsten databasreplikering använder SQL Server ändrings spårning för att övervaka den lokala plats databasen för ändringar. Den replikerar sedan ändringarna till andra platser med hjälp av SQL Server Service Broker (SSB). Som standard använder den här processen TCP-port 4022.  


## <a name="replication-groups"></a>Replikeringsgrupper

Configuration Manager grupperar data som replikeras med databasreplikering i olika replikeringsgrupper. Varje replikeringsgrupp har ett separat, fast replikeringsschema. Platsen använder det här schemat för att avgöra hur ofta den replikerar ändringar till andra platser.  

Till exempel replikeras en ändring av en rollbaserad administrations konfiguration snabbt till andra platser. Det här beteendet ser till att den andra platsen snabbt kan verkställa ändringarna. En konfigurations ändring med lägre prioritet, till exempel en begäran om att installera en ny sekundär plats, replikeras med mindre angelägenhets grad. Det kan ta flera minuter för en ny plats förfrågan att komma åt den primära mål platsen.  


## <a name="settings"></a>Inställningar

Du kan ändra följande inställningar för databasreplikering:  

- **Länkar för databasreplikering**: styr när en speciell trafik passerar nätverket.  

- **Distribuerade vyer**: när en central administrations plats (CAS) begär valda plats data, kan den komma åt data direkt från databasen på en underordnad primär plats.  

- **Scheman**: Ange när en replikeringslänk används och när olika typer av plats data replikeras.  

- **Sammanfattning**: ändra inställningar för data sammanfattning om nätverks trafik som passerar replikeringslänken. Sammanfattningen sker varje kvart som standard. Den används i rapporter för databasreplikering.  

- **Tröskelvärden för databasreplikering**: definiera när platsen rapporterar länkar till en degraderad eller misslyckad. Du kan också konfigurera när Configuration Manager genererar aviseringar om replikeringslänken som har statusen degraderad eller misslyckad.  


## <a name="types-of-data"></a>Typer av data

Configuration Manager klassificerar främst de data som replikeras antingen som *globala data* eller *plats data*. När databasreplikering sker överför platsen ändringar till globala data och plats data över länken databasreplikering. Globala data replikeras till en överordnad eller underordnad plats. Plats data replikeras endast till en överordnad plats. En tredje data typen, *lokala data*, replikeras inte till andra platser. Lokala data är information som andra platser inte behöver.  

### <a name="global-data"></a>Globala data

Globala data är administratörs skapade objekt som replikeras till alla platser i hierarkin. Sekundära platser tar bara emot en delmängd globala data som globala proxy-data. Du skapar globala data på certifikat utfärdare och primära platser. Den här typen innehåller följande data:

- Programdistributioner
- Programuppdateringar
- Samlings definitioner
- Rollbaserade administrations säkerhets omfattningar

### <a name="site-data"></a>Plats data

Plats data är verksamhets information som skapats av Configuration Manager primära platser och deras tilldelade klienter. Plats data replikeras till certifikat utfärdarna, men inte till andra primära platser. Plats data kan bara visas på ca: er och på den primära plats där data har sitt ursprung. Du kan bara ändra plats data på den primära platsen där du skapade den. Den här typen innehåller följande data:

- Maskinvaruinventering
- Statusmeddelanden
- Aviseringar
- Resultatet av frågebaserade samlingar

Alla plats data replikeras till CAS. CAS gör administration och rapportering för hela platshierarki.  


## <a name="database-replication-links"></a><a name="bkmk_Dblinks"></a>Länkar för databasreplikering

När du installerar en ny plats i en hierarki skapar Configuration Manager automatiskt en länk för databasreplikering mellan den överordnade platsen och den nya platsen. Den skapar en enda länk för att ansluta de två platserna.  

Ändra inställningarna för varje länk om du vill kontrol lera överföringen av data över replikeringslänken. Varje replikeringslänk har stöd för separata konfigurationer. Varje länk till databasreplikering innehåller följande kontroller:  

- Stoppa replikeringen av valda plats data från en primär plats till certifikat utfärdarna. Den här åtgärden gör att CAS kommer åt dessa data direkt från databasen för den primära platsen.  

- Schemalägg valda plats data att överföra från en underordnad primär plats till CAS.

- Definiera de inställningar som avgör när en länk till databasreplikering har statusen degraderad eller misslyckad.

- Ange när aviseringar ska genereras för en misslyckad replikeringslänk.

- Ange hur ofta Configuration Manager sammanfattar data om replikeringstrafik som använder replikeringslänken. Den använder dessa data i rapporter.

Om du vill konfigurera en länk till databasreplikering går du till arbets ytan **övervakning** i Configuration Manager-konsolen. Välj noden **databasreplikering** och redigera egenskaperna för länken. Den här noden finns också i arbets ytan **Administration** under noden **hierarki konfiguration** . Redigera en replikeringslänk från antingen den överordnade platsen eller den underordnade platsen för replikeringslänken.  

> [!TIP]  
> Du kan redigera länkar för databasreplikering från noden **Databasreplikering** på valfri arbetsyta. Men när du använder noden **databasreplikering** på arbets ytan **övervakning** kan du också se statusen för databasreplikering. Den ger också till gång till [Replikeringslänkanalys](../../servers/manage/monitor-replication.md#BKMK_RLA) -verktyget. Använd det här verktyget för att undersöka problem med databasreplikering.  

Mer information om hur du konfigurerar Länkar för replikering finns i [kontroller för plats databas replikering](#BKMK_DBRepControls). Mer information om hur du övervakar replikering finns i [övervaka databasreplikering](../../servers/manage/monitor-replication.md).  


## <a name="distributed-views"></a><a name="bkmk_distviews"></a>Distribuerade vyer  

Genom distribuerade vyer, när du gör en begäran på certifikat utfärdarna för valda plats data, kommer den direkt åt databasen på den underordnade primära platsen. Denna direkta åtkomst ersätter behovet av att replikera plats data från den primära platsen till certifikat utfärdarna. Eftersom varje replikeringslänk är oberoende av andra länkar kan du använda distribuerade vyer på de replikeringsgrupper som du väljer. Du kan inte använda distribuerade vyer mellan en primär plats och en sekundär plats.  

Distribuerade vyer ger följande fördelar:  

- Minska CPU-belastningen för att bearbeta databas ändringar på CAS och primära platser

- Minska mängden data som överförs över nätverket till CAS

- Förbättra prestanda för den SQL Server som är värd för CAS-databasen

- Minska disk utrymmet som används av CAS-databasen

Överväg att använda distribuerade vyer när en primär plats är nära befinner sig på certifikat utfärdarna i nätverket, är de två platserna alltid på och alltid anslutna. Distribuerade vyer ersätter replikeringen av valda data mellan platserna med direkta anslutningar mellan SQL-servrarna på varje plats. Certifikat utfärdarna skapar en direkt anslutning varje gången du begär dessa data.

Platsen begär distribuerade Visa data i följande exempel scenarier:

- När du kör rapporter eller frågor
- När du visar information i Resursläsaren
- Samlings utvärdering för samlingar som innehåller plats data-baserade regler

Som standard är distribuerade vyer inaktiverade för varje replikeringslänk. När du aktiverar distribuerade vyer väljer du plats data som inte kommer att replikeras till certifikat utfärdarna över länken. CAS kommer åt dessa data direkt från databasen för den underordnade primära plats som delar länken. Du kan konfigurera följande typer av platsdata för distribuerade vyer:  

- **Maskin varu inventerings** data från klienter
- **Program varu inventering och data för avläsning av program vara** från klienter
- **Status meddelanden** från klienter, den primära platsen och alla sekundära platser

När du visar data i Configuration Manager-konsolen eller i rapporter, är distribuerade vyer som är grovt osynliga för dig. När du begär data som har Aktiver ATS för distribuerade vyer, kommer CAS-platsdatabasen att komma åt den underordnade primära platsens databas för att hämta informationen.

Du kan till exempel använda en Configuration Manager-konsol som är ansluten till certifikat utfärdarna. Du begär information om maskin varu inventering från två primära platser: ABC och XYZ. Du har bara aktiverat maskin varu inventering för distribuerade vyer på plats ABC. CAS hämtar inventerings information för XYZ-klienter från den egna databasen. CAS hämtar inventerings information för ABC-klienter direkt från databasen på plats ABC. Den här informationen visas i Configuration Manager-konsolen eller i en rapport utan att identifiera källan.  

Om en replikeringslänk har en typ av data som har Aktiver ATS för distribuerade vyer, replikerar inte den underordnade primära platsen dessa data till CAS. När du inaktiverar distribuerade vyer för en typ av data återupptar den underordnade primära platsen normal datareplikering till certifikat utfärdarna. Innan dessa data är tillgängliga på CAS måste replikeringsgrupperna för dessa data initieras om mellan den primära platsen och certifikat utfärdarna. När du har avinstallerat en primär plats som har distribuerade vyer, måste certifikat utfärdaren slutföra ominitieringen av sina data innan du kan komma åt data som du har aktiverat för distribuerade vyer på certifikat utfärdarna.  

> [!IMPORTANT]  
> När du använder distribuerade vyer på en replikeringslänk i platshierarki måste du inaktivera distribuerade vyer för alla länkar innan du avinstallerar en primär plats. Mer information finns i [Avinstallera en primär plats som använder distribuerade vyer](../../servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_distviews).  

### <a name="prerequisites-and-limitations-for-distributed-views"></a>Krav och begränsningar för distribuerade vyer  

- Använd endast distribuerade vyer på länkar mellan certifikat utfärdare och en primär plats.

- CAS måste använda SQL Server Enterprise Edition. Den primära platsen har inte det här kravet.

- CAS kan bara ha en instans av SMS-providern. Installera den enskilda instansen på plats databas servern. Den här konfigurationen stöder Kerberos-autentisering. SQL Server på CAS kräver Kerberos för att få åtkomst till SQL Server på den underordnade primära platsen. Det finns inga begränsningar för SMS-providern på den underordnade primära platsen.

- Du kan bara installera en repor ting Services-plats på CAS. Installera SQL Server Reporting Services på plats databas servern. Den här konfigurationen stöder Kerberos-autentisering. SQL Server på CAS kräver Kerberos för att få åtkomst till SQL Server på den underordnade primära platsen.

- Du kan inte vara värd för plats databasen på ett [SQL Server kluster](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).

- I version 1902 och tidigare kan du inte vara värd för plats databasen på en [SQL Server Always on-tillgänglighetsgrupper](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md). För att stödja den här konfigurationen uppdaterar du till version 1906 eller senare.<!-- SCCMDocs-pr#3792 -->

- Dator kontot för CAS-databasservern kräver **Läs** behörighet för den primära plats databasen.

> [!IMPORTANT]  
> Distribuerade vyer och [scheman](#BKMK_schedules) för när data kan replikeras är ömsesidigt uteslutande inställningar för en länk till databasreplikering.  


## <a name="schedule-transfers-of-site-data"></a><a name="BKMK_schedules"></a>Schemalägga överföringar av plats data

För att hjälpa dig att styra nätverks bandbredden som används för att replikera plats data från en underordnad primär plats till CAS, Schemalägg när en replikeringslänk används. Ange sedan när olika typer av plats data ska replikeras. Du kan bestämma när den primära platsen replikerar statusmeddelanden, inventerings- och mätdata. Länkar för databasreplikering från sekundära platser stöder inte scheman för plats data. Det går inte att schemalägga överföringen av globala data.  

När du konfigurerar ett länkat schema för databasreplikering kan du begränsa överföringen av valda plats data från den primära platsen till certifikat utfärdarna. Du kan också konfigurera olika tider för att replikera olika typer av plats data.  

> [!IMPORTANT]  
> [Distribuerade vyer](#bkmk_distviews) och scheman för när data kan replikeras ömsesidigt uteslutande konfigurationer för en länk till databasreplikering.  


## <a name="summarization-of-traffic"></a><a name="BKMK_SummarizeDBReplication"></a>Sammanfattande av trafik  

Varje webbplats sammanfattar regelbundet data om nätverks trafiken som passerar Länkar för databasreplikering för platsen. Platsen använder sammanfattande data i rapporter för databasreplikering. Bägge platserna som deltar i en replikeringslänk sammanfattar nätverkstrafiken som går via replikeringslänken. Plats databas servern sammanfattar data. När den sammanfattar data replikeras informationen till andra platser som globala data.  

Sammanfattningen sker varje kvart som standard. Om du vill ändra sammanfattnings frekvensen för nätverks trafik redigerar du **sammanfattnings intervallet**i egenskaperna för länken databasreplikering. Sammanfattnings frekvensen påverkar den information som du visar i rapporter om databasreplikering. Du kan välja ett intervall mellan 5 och 60 minuter. Om du ökar sammanfattningsfrekvensen, ökar belastningen på SQL Server på varje plats som ingår i replikeringslänken.  

## <a name="database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a>Tröskelvärden för databasreplikering

Tröskelvärden för databasreplikering definierar när Configuration Manager rapporterar status för en länk till databasreplikering antingen degraderad eller misslyckad. Som standard anger den en länk som *försämrad* om en valfri replikeringsgrupp inte kan slutföra replikeringen för 12 på varandra följande försök. Den anger länken som *misslyckad* när en replikeringsgrupp inte replikeras i 24 på varandra följande försök.  

Du kan ange anpassade värden för degraderad eller misslyckad status. Om du justerar dessa värden kan du mer noggrant övervaka hälsan för databasreplikering över länkarna.  

Det går inte att replikera en eller flera replikeringsgrupper medan andra replikeringsgrupper fortsätter att replikeras. Planera för att granska replikeringsstatus för en länk när den först rapporteras vara försämrad.

Överväg att ändra värdena för återförsök för länken i följande situationer:

- Det finns återkommande fördröjningar för vissa replikeringsgrupper och deras fördröjning är inte ett problem

- Nätverks länken mellan platserna har låg tillgänglig bandbredd

När du ökar antalet nya försök innan platsen anger att länken ska försämras eller Miss lyckas kan du eliminera falska varningar om kända problem. Med den här åtgärden kan du spåra länkens status bättre.  

Om du vill förstå hur ofta replikering av gruppen sker bör du fundera över antalet replikeringsintervall för varje replikeringsgrupp. Om du vill visa **synkroniseringsfrekvensen** för replikeringsgrupper går du till arbets ytan **övervakning** i Configuration Manager-konsolen. I noden **databasreplikering** väljer du fliken **replikeringsinformation** i en replikeringslänk.  

Mer information om hur du övervakar databasreplikering, inklusive hur du visar replikeringsstatus, finns i [övervaka databasreplikering](../../servers/manage/monitor-replication.md).  


## <a name="site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a>Kontroller av plats databasens replikering  

Du kan styra den nätverks bandbredd som används för databasreplikering genom att ändra inställningarna för varje plats databas. Inställningarna gäller endast för den plats databas där du konfigurerar inställningarna. Inställningarna används alltid när platsen replikerar data genom databasreplikering till en annan plats.  

Du kan ändra följande replikeringsinställningar för varje plats databas:  

- SSB-porten  

- Vänte tiden innan replikeringsfel utlöser platsen för att initiera om sin kopia av plats databasen  

- Komprimera data som en plats replikerar. Den komprimerar bara data för överföring mellan platser och inte för lagring i plats databasen på någon av platserna.  

Om du vill ändra inställningarna för replikeringsinställningarna för en plats databas, går du till noden **databasreplikering** och redigerar plats databasens egenskaper i Configuration Manager-konsolen. Den här noden visas under noden **hierarki konfiguration** i arbets ytan **Administration** och visas också i arbets ytan **övervakning** . Om du vill redigera egenskaperna för plats databasen väljer du replikeringslänken mellan platserna och öppnar sedan Egenskaper för antingen **överordnad databas** eller **underordnad databas**.  

> [!TIP]  
> Du kan konfigurera databasreplikeringskontrollerna från noden **Databasreplikering** på båda arbetsytorna. Men när du använder noden **databasreplikering** på arbets ytan **övervakning** kan du också visa statusen för databasreplikering för en replikeringslänk och få åtkomst till Replikeringslänkanalyss verktyget för att hjälpa dig att undersöka problem med replikeringen.  


## <a name="see-also"></a>Se även

[Övervaka replikering](../../servers/manage/monitor-replication.md)

[Felsöka SQL-replikering](../../servers/manage/replication/overview.md)
