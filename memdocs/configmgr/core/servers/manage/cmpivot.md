---
title: CMPivot för real tids data
titleSuffix: Configuration Manager
description: Lär dig hur du använder CMPivot i Configuration Manager för att fråga klienter i real tid.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dcd441c7f35748f42adc8824c68ec703291a13e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719143"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>CMPivot för real tids data i Configuration Manager

<!--1358456-->

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager har alltid tillhandahållit en stor centraliserad lagring av enhets data, som kunder använder för rapporterings syfte. Webbplatsen samlar vanligt vis in dessa data varje vecka. Från och med version 1806 är CMPivot ett nytt konsol verktyg som nu ger till gång till real tids status för enheter i din miljö. Den kör omedelbart en fråga på alla aktuella anslutna enheter i mål samlingen och returnerar resultatet. Filtrera sedan och gruppera dessa data i verktyget. Genom att tillhandahålla real tids data från online-klienter kan du snabbare besvara affärs frågor, felsöka problem och reagera på säkerhets incidenter.

Till exempel, vid [minskning av problem med spekulativ körnings sidans kanal](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974), är ett av kraven att uppdatera systemets BIOS. Du kan använda CMPivot för att snabbt fråga efter systemets BIOS-information och hitta klienter som inte uppfyller kraven.

 > [!IMPORTANT]  
 > - Vissa säkerhets program kan blockera skript som körs från c:\windows\ccm\scriptstore. Detta kan förhindra lyckad körning av CMPivot-frågor. Vissa säkerhets program kan också generera gransknings händelser eller aviseringar när du kör CMPivot PowerShell.
 > - Vissa program mot skadlig kod kan oavsiktligt utlösa händelser mot Configuration Manager köra skript eller CMPivot-funktioner. Vi rekommenderar att du undantar%windir%\CCM\ScriptStore så att program mot skadlig kod tillåter dessa funktioner att köras utan störningar.


## <a name="prerequisites"></a>Krav

Följande komponenter krävs för att använda CMPivot:

- Uppgradera mål enheterna till den senaste versionen av Configuration Manager-klienten.  

- Mål klienter kräver minst PowerShell version 4.

- För att kunna samla in data för följande entiteter kräver mål klienterna PowerShell version 5,0:  
  - Administratörer
  - Anslutning
  - Config
  - SMBConfig


- Behörigheter för CMPivot:
  - **Läs** behörighet för objektet **SMS-skript**
  - **Kör skript** behörighet för **samlingen**
    - Du kan också starta i version 1906 med hjälp av **Kör CMPivot** för **samling**.
  - **Läs** behörighet för **inventerings rapporter**
  - Standard omfånget.

>[!NOTE]
> **Kör skript** är en super-uppsättning som **Kör CMPivot** -behörighet.
 
## <a name="limitations"></a>Begränsningar

- I en-hierarki ansluter du Configuration Manager-konsolen till en *primär plats* för att köra CMPivot. Åtgärden **Starta CMPivot** visas inte i konsolen när den är ansluten till en central administrations plats (ca).
  - Från och med Configuration Manager version 1902 kan du köra CMPivot från en certifikat utfärdare. I vissa miljöer krävs ytterligare behörigheter. Mer information finns i [CMPivot från och med version 1902](#bkmk_cmpivot1902).

- CMPivot returnerar endast data för klienter som är anslutna till den aktuella platsen.  

- Om en samling innehåller enheter från en annan plats, är CMPivot-resultaten endast från enheter på den aktuella platsen.  

- Du kan inte anpassa egenskaper för entiteter, kolumner för resultat eller åtgärder på enheter.  

- Endast en instans av CMPivot kan köras samtidigt på en dator som kör Configuration Manager-konsolen.  

- I version 1806 fungerar frågan för entiteten **Administratörer** endast om gruppen heter "administratörer". Det fungerar inte om grupp namnet är lokaliserat. Till exempel "Administrateurs" på franska.<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>Starta CMPivot

1. I Configuration Manager-konsolen ansluter du till den primära platsen. Gå till arbets ytan **till gångar och efterlevnad** och välj noden **enhets samlingar** . Välj en mål samling och klicka på **Starta CMPivot** i menyfliksområdet för att starta verktyget.  

    > [!Tip]  
    > Om du inte ser det här alternativet kontrollerar du följande konfigurationer:  
    > 
    > - Bekräfta med en plats administratör att ditt konto har de behörigheter som krävs. Mer information finns i [krav](#prerequisites).  
    > 
    > - Anslut-konsolen till en *primär plats*.  

2. Gränssnittet innehåller ytterligare information om hur du använder verktyget.  

     - Ange frågesträngarna manuellt överst eller klicka på länkarna i den infogade dokumentationen.  

     - Klicka på en av **entiteterna** för att lägga till den i frågesträngen.  

     - Länkarna för **tabell operatorer**, **agg regerings funktioner**och **skalära funktioner** öppnar språk referens dokumentation i webbläsaren. CMPivot använder [KQL (Kusto Query Language)](https://docs.microsoft.com/azure/kusto/query/).  

3. Låt fönstret CMPivot vara öppet för att visa resultat från klienter. När du stänger fönstret CMPivot slutförs sessionen.  

    > [!Note]  
    > Om frågan har skickats skickar klienterna fortfarande ett tillstånds meddelande svar till servern.  



## <a name="how-to-use-cmpivot"></a>Använda CMPivot

![Exempel på CMPivot-fönster](media/1358456-cmpivot-sample.png)

Fönstret CMPivot innehåller följande element:  

1. Den samling som CMPivot för närvarande är i namn listen längst upp och statusfältet längst ned i fönstret. Till exempel "PM_Team_Machines" i skärm bilden ovan.  

2. I rutan till vänster visas de **entiteter** som är tillgängliga på-klienter. Vissa entiteter förlitar sig på WMI medan andra använder PowerShell för att hämta data från klienter.   

    - Högerklicka på en entitet för följande åtgärder:  

       - **Infoga**: Lägg till entiteten i frågan vid den aktuella pekar positionen. Frågan körs inte automatiskt. Den här åtgärden är standard när du dubbelklickar på en entitet. Använd den här åtgärden när du skapar en fråga.  

       - **Fråga alla**: kör en fråga för den här entiteten inklusive alla egenskaper. Använd den här åtgärden för att snabbt fråga efter en enskild entitet.  

       - **Fråga efter enhet**: kör en fråga för den här entiteten och gruppera resultatet. Till exempel, `Disk | summarize dcount( Device ) by Name`  

    - Expandera en entitet för att se vilka egenskaper som är tillgängliga för varje entitet. Dubbelklicka på en egenskap för att lägga till den i frågan vid den aktuella pekar positionen.  

3. På fliken **Start** visas allmän information om CMPivot, inklusive länkar till exempel frågor och support dokumentation.  

4. På fliken **fråga** visas frågefönstret, resultat fönstret och statusfältet. Fliken fråga är markerad i skärm bilds exemplet ovan.  

5. I fönstret fråga kan du skapa eller ange en fråga som ska köras på klienter i samlingen.  

    - CMPivot använder en delmängd av [KQL (Kusto Query Language)](https://docs.microsoft.com/azure/kusto/query/).  

    - Klipp ut, kopiera eller klistra in innehåll i frågefönstret.  
    <!-- markdownlint-disable MD038 -->
    - Som standard används IntelliSense i det här fönstret. Om du exempelvis börjar skriva `D`, föreslår IntelliSense alla entiteter som börjar med den bokstaven. Välj ett alternativ och tryck på TABB för att infoga det. Ange ett vertikalstreck och ett blank steg `| `. sedan föreslår IntelliSense alla tabell operatorer. Infoga `summarize` och skriv ett blank steg, och IntelliSense föreslår alla agg regerings funktioner. Om du vill ha mer information om dessa operatörer och funktioner klickar du på fliken **Start** i CMPivot.  

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

      - **Kör skript**: starta guiden kör skript för att köra ett befintligt PowerShell-skript på den här enheten. Mer information finns i [köra ett skript](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script).  

      - **Fjärr styrning**: starta en Configuration Manager fjärrstyrningssession på den här enheten. Mer information finns i [så här fjärradministrerar du en Windows-klientdator](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

      - **Resursläsaren**: starta Configuration Manager Resursläsaren för den här enheten. Mer information finns i [Visa maskin varu inventering](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) eller [Visa program varu inventering](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

   - Högerklicka på valfri cell som inte är enhet för att vidta följande ytterligare åtgärder:  

     - **Kopiera**: texten i cellen kopieras till Urklipp.  

     - **Visa enheter med**: fråga efter enheter med det här värdet för den här egenskapen. Du kan till exempel välja det här alternativet `OS` i en cell på versions raden från resultatet av frågan:`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Visa enheter utan**: fråga efter enheter utan detta värde för den här egenskapen. Du kan till exempel välja det här alternativet `OS` i en cell på versions raden från resultatet av frågan:`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Bing IT**: starta standard webbläsaren https://www.bing.com med det här värdet som frågesträng.  

   - Klicka på valfri hyperlänkad text om du vill pivotera vyn med denna information.  

   - Resultat fönstret visar inte fler än 20 000 rader. Ändra antingen frågan för att ytterligare filtrera data eller starta om CMPivot på en mindre samling.  

7. Statusfältet visar följande information (från vänster till höger):  

   - Status för den aktuella frågan till mål samlingen. Denna status omfattar:  
     - Antalet aktiva klienter som slutförde frågan (3)  
     - Antalet totalt antal klienter (5)  
     - Antalet offline-klienter (2)  
     - Klienter som returnerade felet (0)  

       Exempelvis: `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - ID för klient åtgärden. Exempelvis: `id(16780221)`  

   - Den aktuella samlingen. Exempelvis: `PM_Team_Machines`  

   - Det totala antalet rader i resultat fönstret. Till exempel, `1 objects`  



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

En gång i veckan köra CMPivot mot en samling av servrar som du hanterar och välj **fråga alla** på **AppCrash** entiteten. Du högerklickar på kolumnen **fil namn** och väljer **Sortera stigande**. En enhet returnerar sju resultat för sqlsm. exe med en tidsstämpel om 03:00 varje dag. Du väljer fil namnet på en av raderna, högerklickar på det och väljer **Bing**. Genom att bläddra bland Sök resultaten i webbläsaren hittar du en Support artikel från Microsoft för det här problemet med mer information och lösning. 


### <a name="example-3-bios-version"></a>Exempel 3: BIOS-version

Ett av kraven är att uppdatera systemets BIOS för att [undvika spekulativ körnings problem på sidans kanal](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974). Du börjar med en fråga för **BIOS** -entiteten. Sedan kan du **Gruppera efter** **version** -egenskapen. Högerklicka sedan på ett särskilt värde, till exempel "LENOVO-1140" och välj **Visa enheter med**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Exempel 4: ledigt disk utrymme

Du måste tillfälligt lagra en stor fil på en nätverks fil server, men är inte säker på vilken som har tillräckligt med kapacitet. Starta CMPivot mot en samling fil servrar och fråga **disk** entiteten. Ändra frågan för CMPivot snabbt för att snabbt returnera en lista över aktiva servrar med lagrings data i real tid:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-starting-in-version-1810"></a><a name="bkmk_cmpivot"></a>CMPivot från och med version 1810
<!--1359068, 3607759-->

CMPivot innehåller följande förbättringar som börjar i Configuration Manager version 1810:

- [CMPivot-verktyg och prestanda](#bkmk_cmpivot-perf)
- [Skalärfunktioner](#bkmk_cmpivot-functions)  
- [Återge visualiseringar](#bkmk_cmpivot-charts)  
- [Maskinvaruinventering](#bkmk_cmpivot-hinv)  
- [Skaläroperatorer](#bkmk_cmpivot-operators)  
- [Fråga Sammanfattning](#bkmk_cmpivot-summary)  
- [Granska status meddelanden](#cmpivot-audit-status-messages)

### <a name="cmpivot-utility-and-performance"></a><a name="bkmk_cmpivot-perf"></a>CMPivot-verktyg och prestanda

- CMPivot kommer att returnera upp till 100 000 celler i stället för 20 000 rader.
  - Om entiteten har 5 egenskaper, betyder 5 kolumner, upp till 20 000 rader visas.
  - För en entitet med 10 egenskaper visas upp till 10 000 rader.
  - De totala data som visas är mindre än eller lika med 100 000 celler.
- På fliken fråga Sammanfattning väljer du antalet misslyckade eller frånkopplade enheter och väljer sedan alternativet för att **skapa samlingen**. Det här alternativet gör det enkelt att rikta in enheterna med en reparations distribution.
- Spara **favorit** frågor genom att klicka på mappikonen.
   ![Exempel på att spara en favorit fråga i CMPivot](media/cmpivot-favorite.png)

- Klienter som uppdaterats till 1810-versionen returnerade utdata som är mindre än 80 KB till platsen via en snabb kommunikations kanal.
  - Den här ändringen ökar prestanda för visning av skript eller frågor om utdata.
  - Om skriptet eller frågans utdata är större än 80 KB skickar klienten data via ett tillstånds meddelande.
  - Om klienten inte har uppdaterats till 1810-klient versionen fortsätter den att använda tillstånds meddelanden.

- Följande fel kan visas när du startar CMPivot: **du kan inte använda CMPivot just nu på grund av en inkompatibel skript version. Det här problemet kan bero på att hierarkin håller på att uppgradera en plats. Vänta tills uppgraderingen är klar och försök sedan igen.**

  - Om det här meddelandet visas kan det betyda:
    - Säkerhets omfattningen har inte ställts in korrekt.
    - Det finns problem med uppgraderingen i processen.
    - Det underliggande CMPivot-skriptet är inte kompatibelt.


### <a name="scalar-functions"></a><a name="bkmk_cmpivot-functions"></a>Skalära funktioner
CMPivot stöder följande skalära funktioner:
- **sedan ()**: subtraherar angivet TimeSpan från aktuell tid för UTC-klockan  
- **datetime_diff ()**: beräknar kalender skillnaden mellan två datum/tid-värden  
- **Now ()**: returnerar aktuell tid för UTC-klockan  
- **bin ()**: avrundar värden nedåt till ett heltals multipel av en specifik lager plats storlek  

> [!Note]  
> Data typen datetime representerar en omedelbar tid, vanligt vis uttryckt som datum och tid på dagen. Tids värden mäts i 1 – 2 enheter. Ett datetime-värde är alltid i UTC-tidszonen. Alltid exakta litteraler för datum och tid i ISO 8601-format, till exempel`yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>Exempel
- `datetime(2015-12-31 23:59:59.9)`: En angiven datum/tid-literal   
- `now()`: Aktuell tid  
- `ago(1d)`: Aktuell tid minus en dag  


### <a name="rendering-visualizations"></a><a name="bkmk_cmpivot-charts"></a>Återge visualiseringar

CMPivot innehåller nu grundläggande stöd för KQL [Render-operatorn](https://docs.microsoft.com/azure/kusto/query/renderoperator). Det här stödet omfattar följande typer:  
- **Barchart**: första kolumnen är x-axel och kan vara text, DateTime eller numeric. De andra kolumnerna måste vara numeriska och visas som en vågrät remsa.  
- **columnchart**: t. ex. Barchart, med lodräta ränder i stället för vågräta ränder.  
- **piechart**: den första kolumnen är färg axel, den andra kolumnen är numerisk.  
- **timechart**: linje diagram. Den första kolumnen är x-axel och ska vara DateTime. Andra kolumnen är y-axeln.  

#### <a name="example-bar-chart"></a>Exempel: stapeldiagram
Följande fråga återger de senast använda programmen som ett stapeldiagram:

``` Kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

![Exempel på visualisering av CMPivot-stapeldiagram](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>Exempel: tids diagram
Om du vill återge tids diagram använder du operatorn New **bin ()** för att gruppera händelser i tid. Följande fråga visar när enheter har startats under de senaste sju dagarna:

``` Kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

![Exempel på visualisering av CMPivot tids diagram](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>Exempel: cirkel diagram
Följande fråga visar alla OS-versioner i ett cirkel diagram:

``` Kusto
OperatingSystem
| summarize count() by Caption
| render piechart
```

![Exempel på visualisering av CMPivot cirkel diagram](media/1359068-cmpivot-piechart.png)


### <a name="hardware-inventory"></a><a name="bkmk_cmpivot-hinv"></a>Maskin varu inventering
Använd CMPivot för att fråga efter maskin varu inventerings klass. Dessa klasser inkluderar eventuella anpassade tillägg som du gör i maskin varu inventeringen. CMPivot returnerar omedelbart cachelagrade resultat från den senaste genomsökningen av maskin varu inventeringen som lagras i plats databasen. Samtidigt uppdaterar den resultatet om det behövs med real tids data från alla online-klienter.

Färgmättnad för data i resultat tabellen eller diagrammet anger om datan är Live eller cachelagrat. Till exempel är mörk blå data i real tid från en online-klient. Ljusblå är cachelagrade data.

#### <a name="example"></a>Exempel

``` Kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

![Exempel på CMPivot inventerings fråga med visualisering av stapeldiagram](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>Begränsningar
- Följande enheter för maskin varu inventering stöds inte:  
    - Mat ris egenskaper, till exempel IP-adress  
    - Real32/Real64 <!--example?-->  
    - Egenskaper för inbäddat objekt <!--example?-->  
- Lager enhets namn måste börja med ett blank steg
- Du kan inte skriva över de inbyggda entiteterna genom att skapa en lager enhet med samma namn  


### <a name="scalar-operators"></a><a name="bkmk_cmpivot-operators"></a>Skalära operatorer
CMPivot innehåller följande skalära operatorer:  

> [!Note]  
> - LHS: sträng till vänster om operatorn  
> - RHS: sträng till höger om operatorn  


|Operator|Beskrivning|Exempel (ger sant)|
|--------|-----------|---------------------|
|==|Är lika med|`"aBc" == "aBc"`|
|!=|Inte lika med|`"abc" != "ABC"`|
|likadan|LHS innehåller en matchning för RHS|`"FabriKam" like "%Brik%"`|
|! like|LHS innehåller ingen matchning för RHS|`"Fabrikam" !like "%xyz%"`|
|innehåller|RHS inträffar som en under serie av LHS|`"FabriKam" contains "BRik"`|
|! innehåller|RHS inträffar inte i LHS|`"Fabrikam" !contains "xyz"`|
|StartsWith|RHS är en inledande delsekvens av LHS|`"Fabrikam" startswith "fab"`|
|! StartsWith|RHS är inte en inledande delsekvens av LHS|`"Fabrikam" !startswith "kam"`|
|EndsWith|RHS är en avslutande delsekvens av LHS|`"Fabrikam" endswith "Kam"`|
|! EndsWith|RHS är inte en avslutande delsekvens av LHS|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a>Fråga Sammanfattning

Välj fliken **fråga Sammanfattning** längst ned i fönstret CMPivot. Med den här statusen kan du identifiera klienter som är offline eller Felsöka fel som kan uppstå. Välj ett värde i kolumnen antal för att öppna en lista över vissa enheter med denna status. 

Välj till exempel antal enheter med statusen status. Se det detaljerade fel meddelandet och exportera en lista över dessa enheter. Om felet är att en speciell cmdlet inte känns igen skapar du en samling från den exporterade enhets listan för att distribuera en Windows PowerShell-uppdatering.  

### <a name="cmpivot-audit-status-messages"></a>CMPivot gransknings status meddelanden

Från och med version 1810 skapas ett gransknings status meddelande med **MessageID 40805**när du kör CMPivot. Du kan visa status meddelanden genom att gå till **övervaka** > **system status** > **status meddelande frågor**. Du kan köra **alla gransknings status meddelanden för en enskild användare**, **alla gransknings status meddelanden för en enskild plats**eller skapa en egen status meddelande fråga.

Följande format används för meddelandet:

MessageId 40805: användar &lt;namn> körde skript &lt;skript-GUID> med hash &lt;-skript-hash> för &lt;samlings-ID>.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 är skript-GUID för CMPivot.
- Skriptet-hash kan visas i klientens scripts. log-fil.
- Du kan också se hash-värdet som lagras i klientens skript arkiv. Namnet på klienten är &lt;skript-GUID>_&lt;skriptet-hash>.
    - Exempel på fil namn: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123. PS
   

![Exempel på CMPivot gransknings status meddelande](media/cmpivot-audit-status-message.png)

## <a name="cmpivot-starting-in-version-1902"></a><a name="bkmk_cmpivot1902"></a>CMPivot från och med version 1902
<!--3610960-->
Från och med Configuration Manager version 1902 kan du köra CMPivot från den centrala administrations platsen (CAS) i en hierarki. Den primära platsen hanterar fortfarande kommunikationen till klienten. När du kör CMPivot från den centrala administrations platsen kommunicerar den med den primära platsen via prenumerations kanalen för snabb meddelanden. Den här kommunikationen är inte beroende av standard-SQL-replikering mellan platser.

Om du kör CMPivot på certifikat utfärdarna krävs ytterligare behörigheter när SQL eller providern inte finns på samma dator eller när det gäller SQL Always on Configuration. Med dessa fjärrkonfigurationer har du ett "dubbel hopp"-scenario för CMPivot.

För att CMPivot ska fungera på certifikat utfärdarna i ett sådant "dubbel hopp"-scenario kan du definiera begränsad delegering. Om du vill förstå säkerhets konsekvenserna för den här konfigurationen läser du artikeln [Kerberos-begränsad delegering](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) . Kerberos måste fungera genom alla hopp mellan datorerna.<!--5746133--> Om du har mer än en fjärrkonfiguration, till exempel en SQL-eller SMS-provider som samplaceras med certifikat utfärdare eller inte, eller flera betrodda skogar, kan du behöva en kombination av behörighets inställningar. Nedan visas de steg som du kan behöva utföra:

### <a name="cas-has-a-remote-sql-server"></a>CA: er har en fjärran sluten SQL Server

1. Gå till varje primär plats SQL Server.
   1. Lägg till CAS-fjärrinstansen av SQL Server och CAS-platsservern i [Configmgr_DviewAccesss](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) gruppen.
   ![Configmgr_DviewAccess grupp på en primär platss SQL Server](media/cmpivot-dviewaccess-group.png)
1. Gå till Active Directory användare och datorer.
   1. Högerklicka på varje primär plats Server och välj **Egenskaper**.
      1. På fliken delegering väljer du det tredje alternativet och **litar endast på den här datorn för delegering till angivna tjänster**. 
      1. Välj **Använd endast Kerberos**.
      1. Lägg till CAS: s SQL Server-tjänst med port och instans.
      1. Se till att dessa ändringar överensstämmer med företagets säkerhets princip!
   1. Högerklicka på CAS-platsen och välj **Egenskaper**.
      1. På fliken delegering väljer du det tredje alternativet och **litar endast på den här datorn för delegering till angivna tjänster**. 
      1. Välj **Använd endast Kerberos**.
      1. Lägg till varje primär plats SQL Server-tjänst med port och instans.
      1. Se till att dessa ändringar överensstämmer med företagets säkerhets princip!

   ![CMPivot AD Delegerings exempel för dubbla hopp](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>CA: er har en fjärran sluten Provider

1. Gå till varje primär plats SQL Server.
   1. Lägg till CAS-providerns dator konto och CAS-platsservern i [Configmgr_DviewAccesss](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) gruppen.
1. Gå till Active Directory användare och datorer.
   1. Välj datorn för CAS-providern, högerklicka och välj **Egenskaper**.
      1. På fliken delegering väljer du det tredje alternativet och **litar endast på den här datorn för delegering till angivna tjänster**. 
      1. Välj **Använd endast Kerberos**.
      1. Lägg till varje primär plats SQL Server-tjänst med port och instans.
      1. Se till att dessa ändringar överensstämmer med företagets säkerhets princip!
   1. Välj plats servern för certifikat utfärdare, högerklicka och välj **Egenskaper**.
      1. På fliken delegering väljer du det tredje alternativet och **litar endast på den här datorn för delegering till angivna tjänster**. 
      1. Välj **Använd endast Kerberos**.
      1. Lägg till varje primär plats SQL Server-tjänst med port och instans.
      1. Se till att dessa ändringar överensstämmer med företagets säkerhets princip!
1. Starta om CAS-fjärrprovidern.

### <a name="sql-always-on"></a>SQL Always on

1. Gå till varje primär plats SQL Server.
   1. Lägg till plats servern för CAS i [Configmgr_DviewAccesss](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) gruppen.
1. Gå till Active Directory användare och datorer.
   1. Högerklicka på varje primär plats Server och välj **Egenskaper**.
      1. På fliken delegering väljer du det tredje alternativet och **litar endast på den här datorn för delegering till angivna tjänster**. 
      1. Välj **Använd endast Kerberos**.
      1. Lägg till CAS: s SQL Server-användarkonton för SQL-noderna med port och instans.
      1. Se till att dessa ändringar överensstämmer med företagets säkerhets princip!
   1. Välj plats servern för certifikat utfärdare, högerklicka och välj **Egenskaper**.
      1. På fliken delegering väljer du det tredje alternativet och **litar endast på den här datorn för delegering till angivna tjänster**. 
      1. Välj **Använd endast Kerberos**.
      1. Lägg till varje primär plats SQL Server-tjänst med port och instans.
      1. Se till att dessa ändringar överensstämmer med företagets säkerhets princip!
1. Kontrol lera att [SPN har publicerats](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs) för CAS-namnet för SQL-lyssning och varje primär SQL-lyssnings namn.
1. Starta om de primära SQL-servrarna.
1. Starta om CAS plats Server och CAS SQL-servrar.

## <a name="cmpivot-starting-in-version-1906"></a><a name="bkmk_cmpivot1906"></a>CMPivot från och med version 1906

Från och med version 1906 lades följande objekt till i CMPivot:

- [Kopplingar, ytterligare operatorer och agg regeringar](#bkmk_cmpivot_joins)
- [CMPivot-behörigheter har lagts till i rollen säkerhets administratör](#bkmk_cmpivot_secadmin1906)
- [Fristående CMPivot](#bkmk_standalone)

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a><a name="bkmk_cmpivot_joins"></a>Lägg till kopplingar, ytterligare operatorer och agg regeringar i CMPivot
<!--4054074-->
Nu har du ytterligare aritmetiska operatorer, agg regeringar och möjlighet att lägga till frågor, till exempel att använda register och filer tillsammans. Följande objekt har lagts till:

#### <a name="table-operators"></a>Tabell operatörer

|Tabell operatörer| Beskrivning|
|-----|-----|
| [ansluta](https://docs.microsoft.com/azure/kusto/query/joinoperator)| Sammanfoga raderna i två tabeller för att skapa en ny tabell genom att matcha raden för samma enhet|
|återge|Återger resultat som grafiska utdata|

Render-operatorn finns redan i CMPivot. Stöd för flera serier och **with** -satsen har lagts till. Mer information finns i avsnittet [exempel](#bkmk_cmpivot_examples1906) avsnitt och Kusto join- [operator](https://docs.microsoft.com/azure/kusto/query/joinoperator) .

#### <a name="limitations-for-joins"></a>Begränsningar för kopplingar

1. Kopplings kolumnen utförs alltid i fältet **enhet** .
1. Du kan använda högst 5 kopplingar per fråga.
1. Du kan använda högst 64 kombinerade kolumner.

#### <a name="scalar-operators"></a>Skaläroperatorer

|Operator| Beskrivning|Exempel|
|-----|-----|-----|
| + | Lägg till| `2 + 1, now() + 1d`|
| - |  Subtrahera| `2 - 1, now() - 1d`|
| * | Multiplicera| `2 * 2`|
| / | Dividera | `2 / 1`|
| % | Modulo | `2 % 1`

#### <a name="aggregation-functions"></a>Aggregeringsfunktioner

|Funktion| Beskrivning|
|-----|-----|
| percentil ()| Returnerar en uppskattning för den angivna percentilen från närmaste rang för populationen som definieras av expr|
| sumif() | Returnerar en summa av uttryck för vilka predikatet utvärderas till true|

#### <a name="scalar-functions"></a>Skalärfunktioner

|Funktion| Beskrivning|
|-----|-----|
| case()| Utvärderar en lista med predikat och returnerar det första resultat uttryck vars predikat är uppfyllt |
| iff() | Utvärderar det första argumentet och returnerar värdet för antingen det andra eller tredje argumentet beroende på om predikatet utvärderas till sant (sekund) eller falskt (tredje)|
 | indexof() | Funktionen rapporterar det nollbaserade indexet för den första förekomsten av en angiven sträng i Indatasträngen|
| strcat() | Sammanfogar mellan 1 och 64 argument |
| strlen()| Returnerar längden, i tecken, för Indatasträngen|
| substring() | Extraherar en under sträng från en käll sträng som börjar från ett index till slutet av strängen |
| tostring() | Konverterar inmatad till en sträng åtgärd |

#### <a name="examples"></a><a name="bkmk_cmpivot_examples1906"></a>Fler

- Visa enhet, tillverkare, modell och OSVersion:

   ``` Kusto
   ComputerSystem
   | project Device, Manufacturer, Model
   | join (OperatingSystem | project Device, OSVersion=Caption)
   ```

- Visa diagram över start tider för en enhet:

   ``` Kusto
   SystemBootData
   | where Device == 'MyDevice'
   | project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
   | order by SystemStartTime desc
   | render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
   ```

   ![Liggande stapeldiagram som visar start tider för en enhet i MS](./media/4054074-render-using-with-statement.png)

### <a name="added-cmpivot-permissions-to-the-security-administrator-role"></a><a name="bkmk_cmpivot_secadmin1906"></a>CMPivot-behörigheter har lagts till i rollen säkerhets administratör
<!--4683130-->

Från och med version 1906 har följande behörigheter lagts till i Configuration Manager den inbyggda rollen **säkerhets administratör** :

 - **Läs** vidare på SMS-skript
 - **Kör CMPivot** för samling
 - **Läs** vidare på inventerings rapport

>[!NOTE]
> **Kör skript** är en super-uppsättning som **Kör CMPivot** -behörighet.
 

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a>Fristående CMPivot
<!--3555890, 4619340, 4683130 -->

Från och med version 1906 kan du använda CMPivot som en fristående app. CMPivot standalone finns bara på engelska. Kör CMPivot utanför Configuration Manager-konsolen för att Visa real tids status för enheter i din miljö. Den här ändringen gör att du kan använda CMPivot på en enhet utan att först installera-konsolen.

> [!Tip]  
> Den här funktionen introducerades först i version 1906 som en [för hands versions funktion](pre-release-features.md). Från och med version 2002 är det inte längre en för hands versions funktion.  

Du kan dela kraften i CMPivot med andra personer, till exempel supportavdelningen eller säkerhets administratörer, som inte har konsolen installerad på datorn. Dessa andra personer kan använda CMPivot för att fråga Configuration Manager tillsammans med andra verktyg som de traditionellt använder. Genom att dela dessa omfattande hanterings data kan du samar beta för att proaktivt lösa affärs problem som uppstår mellan roller.

#### <a name="install-cmpivot-standalone"></a>Installera fristående CMPivot

1. Ställ in de behörigheter som krävs för att köra CMPivot. Mer information finns i [krav](#prerequisites). Du kan också använda [rollen säkerhets administratör](#bkmk_cmpivot_secadmin1906) om behörigheterna är lämpliga för användaren.
2. Hitta installations programmet CMPivot på följande sökväg: `<site install path>\tools\CMPivot\CMPivot.msi`. Du kan köra den från den sökvägen eller kopiera den till en annan plats.
3. När du kör den fristående CMPivot-appen uppmanas du att ansluta till en-plats. Ange det fullständigt kvalificerade domän namnet eller dator namnet för antingen den centrala administrations servern eller den primära plats servern.
   - Varje gången du öppnar CMPivot fristående uppmanas du att ansluta till en plats Server.
4. Bläddra till den samling som du vill köra CMPivot på och kör sedan frågan.

   ![Bläddra till den samling som du vill köra frågan mot](./media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> Högerklicka på åtgärder, till exempel **köra skript**, **Resursläsaren**och Webbs ökning inte är tillgängligt i CMPivot fristående. Den primära användningen av CMPivot-fristående frågor görs oberoende av den Configuration Manager infrastrukturen. För att hjälpa säkerhets administratörerna, innehåller CMpivot fristående möjlighet att ansluta till Microsoft Defender Security Center. <!--5605358-->

## <a name="cmpivot-starting-in-version-1910"></a><a name="bkmk_cmpivot1910"></a>CMPivot från och med version 1910
<!--5410930, 3197353-->
Från och med version 1910 var CMPivot avsevärt optimerad för att minska nätverks trafiken och belastningen på dina servrar. Dessutom har ett antal entiteter och förbättringar av enheten lagts till för att under lätta fel sökning och jakt. Följande ändringar infördes för CMPivot i version 1910:

- [Optimeringar till CMPivot-motorn](#bkmk_optimization)
- Ytterligare förbättringar av entiteter och entiteter:
  - Windows-händelseloggar ([WinEvent](#bkmk_WinEvent))
  - Fil innehåll ([FileContent](#bkmk_File))
  - DLL-filer som lästs in av processer ([ProcessModule](#bkmk_ProcessModule))
  - Azure Active Directory information ([AADStatus](#bkmk_AadStatus))
  - Endpoint Protection-status ([EPStatus](#bkmk_EPStatus))
- [Utvärdering av lokal enhets fråga med fristående CMPivot](#bkmk_local-eval)
- [Andra förbättringar av CMPivot](#bkmk_Other)


### <a name="optimizations-to-the-cmpivot-engine"></a><a name="bkmk_optimization"></a>Optimeringar till CMPivot-motorn
<!--3197353-->
För att minska nätverks trafiken och belastningen på dina servrar optimerades CMPivot i 1910. Många fråge åtgärder utförs nu direkt på klienten i stället för på servrarna. Den här ändringen innebär också att vissa CMPivot-åtgärder returnerar minimala data från den första frågan. Om du bestämmer dig för att öka detalj nivån för data för mer information kan en ny fråga köras för att hämta ytterligare data från klienten. Tidigare returnerade en stor data uppsättning till servern när du körde frågan "sammanfattade antal".  Vid retur av en stor data uppsättning erbjöds direkt detalj nivån, många gånger då bara det sammanfattade antalet krävdes. I 1910 när du väljer att detaljgranska i en speciell klient sker en annan insamling av data för att returnera ytterligare data som du har begärt. Den här ändringen ger bättre prestanda och skalbarhet för frågor mot ett stort antal klienter. <!--3197353, 5458337-->

#### <a name="examples"></a>Exempel

CMPivot-Optimeringarna minskar drastiskt den nätverks-och Server processor belastning som krävs för att köra CMPivot-frågor. Med dessa optimeringar kan vi nu gå igenom flera gigabyte av klient data i real tid. Följande frågor illustrerar Optimeringarna:

- Sök i alla händelse loggar på alla klienter i företaget efter autentiseringsfel.

   ``` Kusto
   EventLog('Security')
   | where  EventID == 4673
   | summarize count() by Device
   | order by count_ desc
   ```

- Sök efter en fil med hash.

   ``` Kusto
   Device
   | join kind=leftouter ( File('%windir%\\system32\\*.exe')
   | where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
   | project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
   ```

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a>WinEvent (\<logname>, [\<TimeSpan>])

Den här entiteten används för att hämta händelser från händelse loggar och loggfiler för händelse spårning. Entiteten hämtar data från händelse loggar som genereras av Windows händelse logg teknik. Entiteten hämtar också händelser i loggfiler som genereras av ETW (Event Tracing for Windows) (ETW). WinEvent tittar på händelser som har inträffat under de senaste 24 timmarna som standard. Standardvärdet för 24 timmar kan dock åsidosättas genom att inkludera ett TimeSpan.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a>FileContent (\<filename>)

FileContent används för att hämta innehållet i en textfil.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a>ProcessModule (\<processname>)  

Den här entiteten används för att räkna upp de moduler (dll) som läses in av en specifik process. ProcessModule är användbart när det gäller skadlig kod som döljer i legitima processer.  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="aadstatus"></a><a name="bkmk_AadStatus"></a>AadStatus

Den här entiteten kan användas för att hämta aktuell Azure Active Directory identitets information från en enhet.

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="epstatus"></a><a name="bkmk_EPStatus"></a>EPStatus

EPStatus används för att hämta status för program mot skadlig kod som är installerad på datorn.

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="local-device-query-evaluation-using-cmpivot-standalone"></a><a name="bkmk_local-eval"></a>Utvärdering av lokal enhets fråga med fristående CMPivot
<!--3197353-->
När du använder CMPivot utanför Configuration Managers konsolen, kan du fråga bara den lokala enheten utan att behöva Configuration Manager infrastrukturen. Nu kan du använda CMPivot Azure Log Analytics-frågor för att snabbt Visa WMI-information på den lokala enheten. Detta möjliggör även validering och förfining av CMPivot-frågor innan du kör dem i en större miljö. CMPivot standalone finns bara på engelska. Mer information om hur du installerar fristående CMPivot finns i [Installera CMPivot standalone](#install-cmpivot-standalone).

#### <a name="known-issues-for-local-device-query-evaluation"></a>Kända problem för den lokala utvärderingen av enhets frågan

 - Om du frågar på **den här datorn** för en WMI-entitet som du inte har åtkomst till, till exempel en låst WMI-klass, kan det hända att du ser en krasch i CMPivot. Kör CMPivot med ett konto med utökade behörigheter för att fråga dessa entiteter. <!--5753242-->
- Om du frågar icke-WMI-entiteter på **den här datorn**visas ett **ogiltigt namn område** eller ett tvetydigt undantag.
- Kör CMPivot fristående från Start-menyns genväg, inte direkt från sökvägen till den körbara filen. <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a>Andra förbättringar

- Du kan göra vanliga uttryck typ frågor med den nya `like` operatorn. Ett exempel:<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- Vi har uppdaterat entiteterna **CcmLog ()** och **EventLog ()** så att de bara kan titta på meddelanden under de senaste 24 timmarna som standard. Detta beteende kan åsidosättas genom att skicka i ett valfritt TimeSpan. Följande fråga kommer till exempel att titta på händelser under de senaste 1 timmarna:

   ```kusto
   CcmLog('Scripts',1h)
   ```

- Entiteten **()** har uppdaterats för att samla in information om dolda filer och systemfiler och inkludera MD5-hash. Även om en MD5-hash inte är lika korrekt som SHA256-hashvärdet, är det sannolikt att det är den vanligaste rapporterade hashen i de flesta bulletiner för skadlig kod.  

- Du kan lägga till kommentarer i frågor.<!-- 5431463 --> Det här beteendet är användbart när du delar frågor. Ett exempel:

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- CMPivot ansluter automatiskt till den sista platsen.<!-- 5420395 --> När du har startat CMPivot kan du ansluta till en ny plats om det behövs.

- Från menyn **Exportera** väljer du det nya alternativet för att **fråga länkar till Urklipp**.<!-- 5431577 --> Den här åtgärden kopierar en länk till Urklipp som du kan dela med andra. Ett exempel:

    `cmpivot:Ly8gU2FtcGxlIHF1ZXJ5DQpPcGVyYXRpbmdTeXN0ZW0NCnwgc3VtbWFyaXplIGNvdW50KCkgYnkgQ2FwdGlvbg0KfCBvcmRlciBieSBjb3VudF8gYXNjDQp8IHJlbmRlciBiYXJjaGFydA==`

    Den här länken öppnar CMPivot fristående med följande fråga:

    ``` Kusto
    // Sample query
    OperatingSystem
    | summarize count() by Caption
    | order by count_ asc
    | render barchart
    ```

    > [!TIP]
    > För att den här länken ska fungera [installerar du CMPivot standalone](#install-cmpivot-standalone).

- I frågeresultat, om enheten har registrerats i Microsoft Defender Avancerat skydd (ATP), högerklickar du på enheten för att starta **Microsoft defender Security Center** online-portalen.

### <a name="known-issues-for-cmpivot-in-version-1910"></a>Kända problem för CMPivot i version 1910

- Banderollen för maximalt antal resultat kan inte visas när gränsen har uppnåtts. <!--5431427-->
  - Varje klient är begränsad till 128 KB data per fråga.
  - Resultaten kan trunkeras om resultatet av frågan överskrider 128 KB.
  
## <a name="cmpivot-starting-in-version-2002"></a><a name="bkmk_2002"></a>CMPivot från och med version 2002
<!--5870934-->
Vi har gjort det enklare att navigera i CMPivot-entiteter. Från och med Configuration Manager version 2002 kan du söka i CMPivot-entiteter. Nya ikoner har också lagts till för att enkelt särskilja entiteter och objekt typer för entiteten.

![Söker i CMPivot-entiteter](./media/5870934-search-cmpivot-entities.png)

 
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
 
[Felsöka CMPivot](cmpivot-tsg.md)

[Skapa och kör PowerShell-skript](../../../apps/deploy-use/create-deploy-scripts.md)


