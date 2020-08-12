---
title: Ändringar i CMPivot
titleSuffix: Configuration Manager
description: Lär dig mer om ändringar som gjorts i CMPivot mellan Configuration Manager-versioner.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: a49a9564-0863-44c3-991e-a8e271fed586
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 20b23cec74ae3d201bc81fe1834e87e7eb8fcc13
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129694"
---
# <a name="changes-to-cmpivot"></a>Ändringar i CMPivot

Använd följande information för att lära dig om ändringar som gjorts i [CMPivot](cmpivot.md) mellan Configuration Manager-versioner:

## <a name="cmpivot-changes-for-version-2006"></a><a name="bkmk_2006"></a>CMPivot ändringar för version 2006
<!--6518631-->

Från och med version 2006 har följande förbättringar gjorts för CMPivot:

- [CMPivot fristående](cmpivot.md#bkmk_standalone) och CMPivot som startas från administratörs konsolen har konvergerat. När du startar CMPivot från administratörs konsolen, används samma underliggande teknik som CMPivot fristående för att ge dig scenario paritet.

- Förbättringar för tangent bords navigering i CMPivot.

- Du kan köra CMPivot från en enskild enhet eller flera enheter från noden enheter utan att behöva välja en enhets samling. Den här förbättringen gör det enklare för människor, till exempel de som arbetar som supportavdelningen, att skapa CMPivot-frågor för vissa enheter utanför en i förväg skapad samling.
   - Välj en enskild enhet eller flera enheter i en enhets samling eller Välj **Starta CMPivot**.

- När du returnerar enheter i en listvy kan du välja **enhets Pivot** på en eller flera enheter och sedan pivotera och fråga på bara enheterna för att gå vidare. Med den här ändringen kan du öka detalj nivån utan att fråga den större uppsättningen enheter från den ursprungliga samlingen. **Enheten Pivot** ersatte **Pivot to**.
   - I en befintlig CMPivot-åtgärd väljer du en enskild enhet eller flera enheter från utdata. Högerklicka och Pivotera med alternativet **enhets Pivot** . Den här åtgärden startar en separat CMPivot-instans som omfattas av bara de enheter som du har valt. Detta gör det enklare att pivotera och bara fråga på enheter som önskas utan att du behöver skapa en samling för dem.

- När du kör CMPivot för en enskild enhet visas enhetens namn längst upp i fönstret. För flera enheter visas antalet valda enheter överst i fönstret.
- Alternativet **skapa samling** på fliken fråga Sammanfattning togs bort eftersom CMPivot inte längre kräver frågor mot en samling. Utföra en **enhets Pivot** för att öppna en ny instans av CMPivot som är begränsad till enbart de enheter som du vill fråga på. **Skapa samling** är fortfarande tillgängligt i huvud menyn.

![Enhets pivotering för flera enheter med CMPivot](./media/6518631-cmpivot-multi-select.png)


## <a name="cmpivot-changes-for-version-2002"></a><a name="bkmk_2002"></a>CMPivot ändringar för version 2002
<!--5870934-->
Vi har gjort det enklare att navigera i CMPivot-entiteter. Från och med Configuration Manager version 2002 kan du söka i CMPivot-entiteter. Nya ikoner har också lagts till för att enkelt särskilja entiteter och objekt typer för entiteten.

![Söker i CMPivot-entiteter](./media/5870934-search-cmpivot-entities.png)


## <a name="cmpivot-changes-for-version-1910"></a><a name="bkmk_cmpivot1910"></a>CMPivot ändringar för version 1910
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

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a>WinEvent ( \<logname> , [ \<timespan> ])

Den här entiteten används för att hämta händelser från händelse loggar och loggfiler för händelse spårning. Entiteten hämtar data från händelse loggar som genereras av Windows händelse logg teknik. Entiteten hämtar också händelser i loggfiler som genereras av ETW (Event Tracing for Windows) (ETW). WinEvent tittar på händelser som har inträffat under de senaste 24 timmarna som standard. Standardvärdet för 24 timmar kan dock åsidosättas genom att inkludera ett TimeSpan.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a>FileContent ( \<filename> )

FileContent används för att hämta innehållet i en textfil.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a>ProcessModule ( \<processname> )  

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
När du använder CMPivot utanför Configuration Managers konsolen, kan du fråga bara den lokala enheten utan att behöva Configuration Manager infrastrukturen. Nu kan du använda CMPivot Azure Log Analytics-frågor för att snabbt Visa WMI-information på den lokala enheten. Detta möjliggör även validering och förfining av CMPivot-frågor innan du kör dem i en större miljö. CMPivot standalone finns bara på engelska. Mer information om fristående CMPivot finns i [CMPivot standalone](#bkmk_standalone).

#### <a name="known-issues-for-local-device-query-evaluation"></a>Kända problem för den lokala utvärderingen av enhets frågan

 - Om du frågar på **den här datorn** för en WMI-entitet som du inte har åtkomst till, till exempel en låst WMI-klass, kan det hända att du ser en krasch i CMPivot. Kör CMPivot med ett konto med utökade behörigheter för att fråga dessa entiteter. <!--5753242-->
- Om du frågar icke-WMI-entiteter på **den här datorn**visas ett **ogiltigt namn område** eller ett tvetydigt undantag.
- Kör CMPivot fristående från Start-menyns genväg, inte direkt från sökvägen till den körbara filen. <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a>Andra förbättringar

- Du kan göra vanliga uttryck typ frågor med den nya `like` operatorn. Till exempel:<!--3056858-->
  
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

- Du kan lägga till kommentarer i frågor.<!-- 5431463 --> Det här beteendet är användbart när du delar frågor. Till exempel:

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- CMPivot ansluter automatiskt till den sista platsen.<!-- 5420395 --> När du har startat CMPivot kan du ansluta till en ny plats om det behövs.

- Från menyn **Exportera** väljer du det nya alternativet för att **fråga länkar till Urklipp**.<!-- 5431577 --> Den här åtgärden kopierar en länk till Urklipp som du kan dela med andra. Till exempel:

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
    > För att den här länken ska fungera [installerar du CMPivot standalone](#bkmk_standalone).

- I frågeresultat, om enheten har registrerats i Microsoft Defender Avancerat skydd (ATP), högerklickar du på enheten för att starta **Microsoft defender Security Center** online-portalen.

### <a name="known-issues-for-cmpivot-in-version-1910"></a>Kända problem för CMPivot i version 1910

- Banderollen för maximalt antal resultat kan inte visas när gränsen har uppnåtts. <!--5431427-->
  - Varje klient är begränsad till 128 KB data per fråga.
  - Resultaten kan trunkeras om resultatet av frågan överskrider 128 KB.

## <a name="cmpivot-changes-for-version-1906"></a><a name="bkmk_cmpivot1906"></a>CMPivot ändringar för version 1906

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

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)] 

## <a name="cmpivot-changes-for-version-1902"></a><a name="bkmk_cmpivot1902"></a>CMPivot ändringar för version 1902
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


## <a name="cmpivot-changes-for-version-1810"></a><a name="bkmk_cmpivot"></a>CMPivot ändringar för version 1810
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
   - Det här alternativet har tagits bort i version 2006 eftersom CMPivot inte längre kräver frågor mot en samling.
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
|==|Lika med|`"aBc" == "aBc"`|
|!=|Inte lika med|`"abc" != "ABC"`|
|likadan|LHS innehåller en matchning för RHS|`"FabriKam" like "%Brik%"`|
|! like|LHS innehåller ingen matchning för RHS|`"Fabrikam" !like "%xyz%"`|
|contains|RHS inträffar som en under serie av LHS|`"FabriKam" contains "BRik"`|
|! innehåller|RHS inträffar inte i LHS|`"Fabrikam" !contains "xyz"`|
|StartsWith|RHS är en inledande delsekvens av LHS|`"Fabrikam" startswith "fab"`|
|! StartsWith|RHS är inte en inledande delsekvens av LHS|`"Fabrikam" !startswith "kam"`|
|EndsWith|RHS är en avslutande delsekvens av LHS|`"Fabrikam" endswith "Kam"`|
|! EndsWith|RHS är inte en avslutande delsekvens av LHS|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a>Fråga Sammanfattning

Välj fliken **fråga Sammanfattning** längst ned i fönstret CMPivot. Med den här statusen kan du identifiera klienter som är offline eller Felsöka fel som kan uppstå. Välj ett värde i kolumnen antal för att öppna en lista över vissa enheter med denna status. 

Välj till exempel antal enheter med statusen status. Se det detaljerade fel meddelandet och exportera en lista över dessa enheter. Om felet är att en speciell cmdlet inte känns igen skapar du en samling från den exporterade enhets listan för att distribuera en Windows PowerShell-uppdatering.  

### <a name="cmpivot-audit-status-messages"></a>CMPivot gransknings status meddelanden

Från och med version 1810 skapas ett gransknings status meddelande med **MessageID 40805**när du kör CMPivot. Du kan visa status meddelanden genom att gå till **övervaka**  >  **system status**  >  **status meddelande frågor**. Du kan köra **alla gransknings status meddelanden för en enskild användare**, **alla gransknings status meddelanden för en enskild plats**eller skapa en egen status meddelande fråga.

Följande format används för meddelandet:

MessageId 40805: användar &lt; namn> körde skript &lt; skript-GUID> med hash &lt; -skript-hash> för samlings- &lt; ID>.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 är skript-GUID för CMPivot.
- Skriptet-hash kan visas i klientens scripts. log-fil.
- Du kan också se hash-värdet som lagras i klientens skript arkiv. Namnet på klienten är &lt; skript-Guid>_ &lt; skriptet-hash>.
    - Exempel på fil namn: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123. PS
   

![Exempel på CMPivot gransknings status meddelande](media/cmpivot-audit-status-message.png)

## <a name="next-steps"></a>Nästa steg
 
[Felsöka CMPivot](cmpivot-tsg.md)
