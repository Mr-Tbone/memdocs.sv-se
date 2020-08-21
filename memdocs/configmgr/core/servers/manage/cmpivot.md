---
title: CMPivot för real tids data
titleSuffix: Configuration Manager
description: Lär dig hur du använder CMPivot i Configuration Manager för att fråga klienter i real tid.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 11b5a58a6d9501b0368fcb0b47bf31df1bd8a6af
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700590"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>CMPivot för real tids data i Configuration Manager

<!--1358456-->

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager har alltid tillhandahållit en stor centraliserad lagring av enhets data, som kunder använder för rapporterings syfte. Webbplatsen samlar vanligt vis in dessa data varje vecka. Från och med version 1806 är CMPivot ett nytt konsol verktyg som nu ger till gång till real tids status för enheter i din miljö. Den kör omedelbart en fråga på alla aktuella anslutna enheter i mål samlingen och returnerar resultatet. Filtrera sedan och gruppera dessa data i verktyget. Genom att tillhandahålla real tids data från online-klienter kan du snabbare besvara affärs frågor, felsöka problem och reagera på säkerhets incidenter.

Till exempel, vid [minskning av problem med spekulativ körnings sidans kanal](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974), är ett av kraven att uppdatera systemets BIOS. Du kan använda CMPivot för att snabbt fråga efter systemets BIOS-information och hitta klienter som inte uppfyller kraven.

 > [!IMPORTANT]  
 > - Vissa säkerhets program kan blockera skript som körs från c:\windows\ccm\scriptstore. Detta kan förhindra lyckad körning av CMPivot-frågor. Vissa säkerhets program kan också generera gransknings händelser eller aviseringar när du kör CMPivot PowerShell.
 > - Vissa program mot skadlig kod kan oavsiktligt utlösa händelser mot Configuration Manager köra skript eller CMPivot-funktioner. Vi rekommenderar att du undantar%windir%\CCM\ScriptStore så att program mot skadlig kod tillåter dessa funktioner att köras utan störningar.


## <a name="prerequisites"></a>Förutsättningar

Följande komponenter krävs för att använda CMPivot:

- Uppgradera mål enheterna till den senaste versionen av Configuration Manager-klienten.  

- Mål klienter kräver minst PowerShell version 4.

- För att kunna samla in data för följande entiteter kräver mål klienterna PowerShell version 5,0:  
  - Administratörer
  - Anslutning
  - Config
  - SMBConfig

- CMPivot och [Microsoft Edge](../../../apps/deploy-use/deploy-edge.md) -installationsprogrammet är signerade med **Microsofts kod signerings** certifikat. Om certifikatet inte visas i arkivet **Betrodda utgivare** måste du lägga till det. Annars körs inte CMPivot och Microsoft Edge-installationsprogrammet när PowerShell-körnings principen är inställd på **AllSigned**. <!--7585106-->

## <a name="permissions"></a>Behörigheter

Följande behörigheter krävs för CMPivot:

- **Läs** behörighet för objektet **SMS-skript**
- **Kör skript** behörighet för **samlingen**
   - Du kan också starta i version 1906 med hjälp av **Kör CMPivot** för **samling**.
- **Läs** behörighet för **inventerings rapporter**
- Standard omfånget.

> [!NOTE]
> - **Kör skript** är en super-uppsättning som **Kör CMPivot** -behörighet.
> - Från och med version 1906 [lades behörigheter för CMPivot](cmpivot-changes.md#bkmk_cmpivot_secadmin1906) till i Configuration Manager den inbyggda rollen **säkerhets administratör** .
 
## <a name="limitations"></a>Begränsningar

- I en-hierarki ansluter du Configuration Manager-konsolen till en *primär plats* för att köra CMPivot. Åtgärden **Starta CMPivot** visas inte i konsolen när den är ansluten till en central administrations plats (ca).
  - Från och med Configuration Manager version 1902 kan du köra CMPivot från en certifikat utfärdare. I vissa miljöer krävs ytterligare behörigheter. Mer information finns i [CMPivot-ändringar för version 1902](cmpivot-changes.md#bkmk_cmpivot1902).

- CMPivot returnerar endast data för klienter som är anslutna till den aktuella platsen.  

- Om en samling innehåller enheter från en annan plats, är CMPivot-resultaten endast från enheter på den aktuella platsen.  

- Du kan inte anpassa egenskaper för entiteter, kolumner för resultat eller åtgärder på enheter.  

- Endast en instans av CMPivot kan köras samtidigt på en dator som kör Configuration Manager-konsolen.  

- I version 1806 fungerar frågan för entiteten **Administratörer** endast om gruppen heter "administratörer". Det fungerar inte om grupp namnet är lokaliserat. Till exempel "Administrateurs" på franska.<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>Starta CMPivot

1. I Configuration Manager-konsolen ansluter du till den primära platsen. Gå till arbets ytan **till gångar och efterlevnad** och välj noden **enhets samlingar** . Välj en mål samling och klicka på **Starta CMPivot** i menyfliksområdet för att starta verktyget. Om du inte ser det här alternativet kontrollerar du följande konfigurationer:  
   - Bekräfta med en plats administratör att ditt konto har de behörigheter som krävs. Mer information finns i [krav](#prerequisites).  
   - Anslut-konsolen till en *primär plats*.  

2. Gränssnittet innehåller ytterligare information om hur du använder verktyget.  

     - Ange frågesträngarna manuellt överst eller klicka på länkarna i den infogade dokumentationen.  

     - Klicka på en av **entiteterna** för att lägga till den i frågesträngen.  

     - Länkarna för **tabell operatorer**, **agg regerings funktioner**och **skalära funktioner** öppnar språk referens dokumentation i webbläsaren. CMPivot använder [KQL (Kusto Query Language)](/azure/kusto/query/).  

3. Låt fönstret CMPivot vara öppet för att visa resultat från klienter. När du stänger fönstret CMPivot slutförs sessionen.
   - Om frågan har skickats skickar klienterna fortfarande ett tillstånds meddelande svar till servern.  



## <a name="how-to-use-cmpivot"></a>Använda CMPivot

![Exempel på CMPivot-fönster](media/1358456-cmpivot-sample.png)

Fönstret CMPivot innehåller följande element:  

1. Den samling som CMPivot för närvarande är i namn listen längst upp och statusfältet längst ned i fönstret. Till exempel "PM_Team_Machines" i skärm bilden ovan.  

2. I rutan till vänster visas de **entiteter** som är tillgängliga på-klienter. Vissa entiteter förlitar sig på WMI medan andra använder PowerShell för att hämta data från klienter.   

    - Högerklicka på en entitet för följande åtgärder:  

       - **Infoga**: Lägg till entiteten i frågan vid den aktuella pekar positionen. Frågan körs inte automatiskt. Den här åtgärden är standard när du dubbelklickar på en entitet. Använd den här åtgärden när du skapar en fråga.  

       - **Fråga alla**: kör en fråga för den här entiteten inklusive alla egenskaper. Använd den här åtgärden för att snabbt fråga efter en enskild entitet.  

       - **Fråga efter enhet**: kör en fråga för den här entiteten och gruppera resultatet. Till exempel `Disk | summarize dcount( Device ) by Name`  

    - Expandera en entitet för att se vilka egenskaper som är tillgängliga för varje entitet. Dubbelklicka på en egenskap för att lägga till den i frågan vid den aktuella pekar positionen.  

3. På fliken **Start** visas allmän information om CMPivot, inklusive länkar till exempel frågor och support dokumentation.  

4. På fliken **fråga** visas frågefönstret, resultat fönstret och statusfältet. Fliken fråga är markerad i skärm bilds exemplet ovan.  

5. I fönstret fråga kan du skapa eller ange en fråga som ska köras på klienter i samlingen.  

    - CMPivot använder en delmängd av [KQL (Kusto Query Language)](/azure/kusto/query/).  

    - Klipp ut, kopiera eller klistra in innehåll i frågefönstret.  
    <!-- markdownlint-disable MD038 -->
    - Som standard används IntelliSense i det här fönstret. Om du exempelvis börjar skriva `D` , föreslår IntelliSense alla entiteter som börjar med den bokstaven. Välj ett alternativ och tryck på TABB för att infoga det. Ange ett vertikalstreck och ett blank steg `| ` . sedan föreslår IntelliSense alla tabell operatorer. Infoga `summarize` och skriv ett blank steg, och IntelliSense föreslår alla agg regerings funktioner. Om du vill ha mer information om dessa operatörer och funktioner klickar du på fliken **Start** i CMPivot.  

    - Fönstret fråga innehåller även följande alternativ:  

        - Kör frågan.  

        - Flytta bakåt och framåt i historik listan med frågor.  

        - Skapa en samling med direkt medlemskap.  

        - Exportera frågeresultaten till CSV eller Urklipp.  

6. I resultat fönstret visas de data som returneras av aktiva klienter för frågan.  

   - Vilka kolumner som är tillgängliga beror på entiteten och frågan.  

   - Klicka på ett kolumn namn för att sortera resultaten efter den egenskapen.  

   - Högerklicka på ett kolumn namn för att gruppera resultatet efter samma information i kolumnen, eller sortera resultaten.  

   - Högerklicka på ett enhets namn om du vill göra följande ytterligare åtgärder på enheten:  

      - **Pivotera till**: fråga efter en annan entitet på den här enheten.
         - Från och med version 2006 ersattes **Pivot to till** **Device Pivot**. Mer information finns i [CMPivot-ändringar för version 2006](cmpivot-changes.md#bkmk_2006).

      - **Kör skript**: starta guiden kör skript för att köra ett befintligt PowerShell-skript på den här enheten. Mer information finns i [köra ett skript](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script).  

      - **Fjärr styrning**: starta en Configuration Manager fjärrstyrningssession på den här enheten. Mer information finns i [så här fjärradministrerar du en Windows-klientdator](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

      - **Resursläsaren**: starta Configuration Manager Resursläsaren för den här enheten. Mer information finns i [Visa maskin varu inventering](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) eller [Visa program varu inventering](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

   - Högerklicka på valfri cell som inte är enhet för att vidta följande ytterligare åtgärder:  

     - **Kopiera**: texten i cellen kopieras till Urklipp.  

     - **Visa enheter med**: fråga efter enheter med det här värdet för den här egenskapen. Du kan till exempel `OS` välja det här alternativet i en cell på versions raden från resultatet av frågan: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Visa enheter utan**: fråga efter enheter utan detta värde för den här egenskapen. Du kan till exempel `OS` välja det här alternativet i en cell på versions raden från resultatet av frågan: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Bing IT**: starta standard webbläsaren https://www.bing.com med det här värdet som frågesträng.  

   - Klicka på valfri hyperlänkad text om du vill pivotera vyn med denna information.  

   - Resultat fönstret visar inte fler än 20 000 rader. Ändra antingen frågan för att ytterligare filtrera data eller starta om CMPivot på en mindre samling.  

7. Statusfältet visar följande information (från vänster till höger):  

   - Status för den aktuella frågan till mål samlingen. Denna status omfattar:  
     - Antalet aktiva klienter som slutförde frågan (3)  
     - Antalet totalt antal klienter (5)  
     - Antalet offline-klienter (2)  
     - Klienter som returnerade felet (0)  

       Exempel: `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - ID för klient åtgärden. Exempel: `id(16780221)`  

   - Den aktuella samlingen. Exempel: `PM_Team_Machines`  

   - Det totala antalet rader i resultat fönstret. Till exempel `1 objects`  



## <a name="example-scenarios"></a>Exempelscenarier

I följande avsnitt finns exempel på hur du kan använda CMPivot i din miljö:


### <a name="example-1-stop-a-running-service"></a>Exempel 1: stoppa en tjänst som körs

Säkerhets administratören ber dig att stoppa och inaktivera tjänsten Computer Browser så snabbt som möjligt på alla enheter på ekonomi avdelningen. Du startar CMPivot på en samling för alla enheter i redovisningen och väljer **fråga alla** på entiteten **tjänst** . 

`Service`

När resultatet visas högerklickar du på kolumnen **namn** och väljer **Gruppera efter**. 

`Service | summarize dcount( Device ) by Name`

I raden för **webb läsar** tjänsten klickar du på det länkade numret i kolumnen **dcount_** . 

`Service | where (Name == 'Browser') | summarize count() by Device`

Du väljer flera enheter, högerklickar på markeringen och väljer **Kör skript**. Den här åtgärden startar guiden kör skript där du kör ett befintligt skript som du har för att stoppa och inaktivera en tjänst. Med CMPivot kan du snabbt svara på säkerhets incidenten för alla aktiva datorer och visa resultaten i guiden kör skript. Sedan kan du följa uppföljningen för att skapa en konfigurations bas linje för att reparera andra datorer i samlingen när de blir aktiva i framtiden. 

![CMPivot-exempel för webb läsar tjänsten och kör skript åtgärd](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Exempel 2: lös program felen proaktivt  

En gång i veckan köra CMPivot mot en samling av servrar som du hanterar och välj **fråga alla** på **AppCrash** entiteten. Du högerklickar på kolumnen **fil namn** och väljer **Sortera stigande**. En enhet returnerar sju resultat för sqlsqm.exe med en tidsstämpel om 03:00 varje dag. Du väljer fil namnet på en av raderna, högerklickar på det och väljer **Bing**. Genom att bläddra bland Sök resultaten i webbläsaren hittar du en Support artikel från Microsoft för det här problemet med mer information och lösning. 


### <a name="example-3-bios-version"></a>Exempel 3: BIOS-version

Ett av kraven är att uppdatera systemets BIOS för att [undvika spekulativ körnings problem på sidans kanal](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974). Du börjar med en fråga för **BIOS** -entiteten. Sedan kan du **Gruppera efter** **version** -egenskapen. Högerklicka sedan på ett särskilt värde, till exempel "LENOVO-1140" och välj **Visa enheter med**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Exempel 4: ledigt disk utrymme

Du måste tillfälligt lagra en stor fil på en nätverks fil server, men är inte säker på vilken som har tillräckligt med kapacitet. Starta CMPivot mot en samling fil servrar och fråga **disk** entiteten. Ändra frågan för CMPivot snabbt för att snabbt returnera en lista över aktiva servrar med lagrings data i real tid:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> Fristående CMPivot

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)]


 
## <a name="inside-cmpivot"></a>Inuti CMPivot

CMPivot skickar frågor till klienter med hjälp av Configuration Manager "snabb kanal". Den här kommunikations kanalen från server till klient används också av andra funktioner som klient meddelande åtgärder, klient status och Endpoint Protection. Klienter returnerar resultat via det liknande snabb tillstånds meddelande systemet. Tillstånds meddelanden lagras tillfälligt i-databasen. Mer information om portarna som används för klient meddelanden finns i artikeln [portar](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP) .

Frågorna och resultaten är bara text. Entiteterna **InstallSoftware** och **process** returnerar några av de största resultat uppsättningarna. Under prestanda testning var det största tillstånds meddelande fil storleken från en klient för dessa frågor mindre än **1 KB**. Den här engångs frågan genererar mindre än 50 MB data över nätverket, skalade till en stor miljö med 50 000 aktiva klienter. Alla objekt på Välkomst sidan som är understrukna kommer att returnera mindre än 1 KB information per klient.

![Exempel på CMPivot understrukna entiteter](media/cmpivot-underlined-entities.png)

Från och med Configuration Manager 1810 kan CMPivot fråga maskin varu inventerings data, inklusive utökade maskin varu lager klasser. Dessa nya entiteter (entiteter som inte är understrukna på Välkomst sidan) kan returnera mycket större data uppsättningar, beroende på hur mycket data som definierats för en viss maskin varu inventerings egenskap. Till exempel kan entiteten "InstalledExecutable" returnera flera MB data per klient, beroende på vilka specifika data du frågar efter. Mindful prestanda och skalbarhet på dina system när du returnerar större data uppsättningar för maskin varu inventering från större samlingar med CMPivot.

En fråga nådde sin tids gräns efter en timme. En samling har till exempel 500 enheter och 450 av klienterna är online. De aktiva enheterna tar emot frågan och returnerar resultaten nästan omedelbart. Om du lämnar fönstret CMPivot öppet, som de andra 50 klienterna är online, tar de även emot frågan och returnerar resultat. 

## <a name="log-files"></a>Loggfiler

 CMPivot-interaktioner loggas i följande loggfiler:

**På Server sidan:**
- SmsProv. log
- BgbServer. log
- Tillstånd. log

**På klient sidan:**
- CcmNotificationAgent.log
- Scripts. log
- StateMessage.log

Mer information finns i [loggfiler](../../plan-design/hierarchy/log-files.md) och [fel sökning av CMPivot](cmpivot-tsg.md).

## <a name="next-steps"></a>Nästa steg

- [Ändringar i CMPivot](cmpivot-changes.md)
- [Felsöka CMPivot](cmpivot-tsg.md)
- [Skapa och kör PowerShell-skript](../../../apps/deploy-use/create-deploy-scripts.md)