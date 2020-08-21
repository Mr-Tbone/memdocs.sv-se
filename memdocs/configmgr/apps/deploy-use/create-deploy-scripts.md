---
title: Skapa och köra skript
titleSuffix: Configuration Manager
description: Skapa och kör PowerShell-skript på klient enheter.
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: db3a673d99efc40bd6fa0da7930c66c648136e03
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695375"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Skapa och kör PowerShell-skript från Configuration Manager-konsolen

*Gäller för: Configuration Manager (aktuell gren)*

<!--1236459-->
Configuration Manager har en integrerad möjlighet att köra PowerShell-skript. PowerShell har fördelen att skapa avancerade, automatiserade skript som förstås och delas med en större community. Skripten fören klar skapandet av anpassade verktyg för att administrera program vara och gör att du snabbt kan utföra rutinmässiga-uppgifter, så att du kan få stora jobb snabbare och mer konsekvent.  

> [!Note]  
> Configuration Manager aktiverar inte den här valfria funktionen som standard. Du måste aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  


Med den här integreringen i Configuration Manager kan du använda funktionen *Kör skript* för att göra följande:

- Skapa och redigera skript som ska användas med Configuration Manager.
- Hantera skript användning via roller och säkerhets omfattningar. 
- Kör skript på samlingar eller enskilda lokala hanterade Windows-datorer.
- Få snabba, aggregerade skript resultat från klient enheter.
- Övervaka skript körning och Visa rapporterings resultat från utdata från skript.

> [!WARNING]
> - Med tanke på kraften i skript, påminner vi om att du är avsiktlig och försiktig med deras användning. Vi har byggt ytterligare skydd för att hjälpa dig. åtskiljda roller och omfång. Kontrol lera att skripten är korrekta innan du kör dem och bekräfta att de kommer från en betrodd källa, för att förhindra oavsiktlig skript körning. Var mindful utökade tecken eller andra döljande och lär dig mer om att skydda skript. [Läs mer om PowerShell-skript säkerhet](learn-script-security.md)
> - Vissa program mot skadlig kod kan oavsiktligt utlösa händelser mot Configuration Manager köra skript eller CMPivot-funktioner. Vi rekommenderar att du undantar%windir%\CCM\ScriptStore så att program mot skadlig kod tillåter dessa funktioner att köras utan störningar.

## <a name="prerequisites"></a>Förutsättningar

- För att köra PowerShell-skript måste klienten köra PowerShell version 3,0 eller senare. Men om ett skript som du kör innehåller funktioner från en senare version av PowerShell måste klienten som kör skriptet köra den versionen av PowerShell.
- Configuration Manager klienter måste köra-klienten från 1706-versionen eller senare för att kunna köra skript.
- Om du vill använda skript måste du vara medlem i lämplig Configuration Manager säkerhets roll.
- För att importera och redigera skript – ditt konto måste ha behörighet att **skapa** för **SMS-skript**.
- För att godkänna eller neka skript – ditt konto måste ha behörigheten **Godkänn** för **SMS-skript**.
- För att köra skript – ditt konto måste ha **Kör skript** behörigheter för **samlingar**.

Mer information om Configuration Manager säkerhets roller:</br>
[Säkerhets omfattningar för körning av skript](#security-scopes)</br>
[Säkerhets roller för körning av skript](#bkmk_ScriptRoles)</br>
[Grunderna i rollbaserad administration](../../core/understand/fundamentals-of-role-based-administration.md).

## <a name="limitations"></a>Begränsningar

Kör skript stöder för närvarande:

- Skript språk: PowerShell
- Parameter typer: heltal, sträng och lista.


>[!WARNING]
>Tänk på att när du använder parametrar öppnas ett Surface-utrymme för potentiell risk för PowerShell-injektering. Det finns olika sätt att åtgärda och kringgå, till exempel att använda reguljära uttryck för att validera parameter Indatatyp eller använda fördefinierade parametrar. Vanliga rekommenderade metoder är att inte inkludera hemligheter i dina PowerShell-skript (inga lösen ord osv.). [Läs mer om PowerShell-skript säkerhet](learn-script-security.md) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Kör skript författare och god kännare

Kör skript använder begreppet *skript författare* och *skript god kännare* som separata roller för implementering och körning av ett skript. Om du har rollen författare och god kännare kan en viktig process kontroll utföras för det kraftfulla verktyget som kör skript. Det finns ytterligare en *skript utlöpares* -roll som tillåter körning av skript, men inte skapa eller godkänna skript. Se [skapa säkerhets roller för skript](#bkmk_ScriptRoles).

### <a name="scripts-roles-control"></a>Skript roller-kontroll

Som standard kan användare inte godkänna ett skript som de har skapat. Eftersom skript är kraftfulla, mångsidiga och potentiellt distribuerade till många enheter, kan du skilja rollerna mellan den person som skapar skriptet och den person som godkänner skriptet. Dessa roller ger ytterligare en säkerhets nivå för att köra ett skript utan överblick. Du kan inaktivera sekundärt godkännande för enklare testning.

### <a name="approve-or-deny-a-script"></a>Godkänn eller neka ett skript

Skripten måste godkännas av *skript god kännare* -rollen innan de kan köras. Så här godkänner du ett skript:

1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.
2. I arbets ytan **program bibliotek** klickar du på **skript**.
3. Välj det skript som du vill godkänna eller neka i listan **skript** och klicka sedan på **Godkänn/neka**i gruppen **skript** på fliken **Start** .
4. I dialog rutan **Godkänn eller neka skript** väljer du **Godkänn**eller **neka** för skriptet. Du kan också ange en kommentar om ditt beslut.  Om du nekar ett skript kan det inte köras på klient enheter. <br>
![Skript godkännande](./media/run-scripts/RS-approval.png)
1. Slutför guiden. I listan **skript** ser du kolumnen **godkännande tillstånd** ändrad beroende på vilken åtgärd du vidtog.

### <a name="allow-users-to-approve-their-own-scripts"></a>Tillåt användare att godkänna sina egna skript

Detta godkännande används främst för test fasen vid skript utveckling.

1. Klicka på **Administration**i Configuration Manager-konsolen.
2. I arbetsytan **Administration** expanderar du **Platskonfiguration**och klickar sedan på **Platser**.
3. Välj din plats i listan över platser och klicka sedan på **Inställningar för hierarki**i gruppen **platser** på fliken **Start** .
4. På fliken **Allmänt** i dialog rutan **Egenskaper för hierarkiskt egenskaper** avmarkerar du kryss rutan **skript författare kräver ytterligare skript god kännare**.

>[!IMPORTANT]
>Som bästa praxis bör du inte tillåta en skript författare att godkänna sina egna skript. Det bör endast tillåtas i en labb inställning. Överväg noga den potentiella effekten av att ändra den här inställningen i en produktions miljö.

## <a name="security-scopes"></a>Säkerhetsomfattningar
  
Kör skript använder säkerhets omfattningar, en befintlig funktion i Configuration Manager, för att styra skript redigering och körning genom att tilldela taggar som representerar användar grupper. Mer information om hur du använder säkerhets omfattningar finns i [Konfigurera rollbaserad administration för Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="create-security-roles-for-scripts"></a><a name="bkmk_ScriptRoles"></a> Skapa säkerhets roller för skript
De tre säkerhets rollerna som används för att köra skript skapas inte som standard i Configuration Manager. Följ stegen nedan om du vill skapa skript utlöpare, skript författare och roller för god kännare av skript.

1. I Configuration Manager-konsolen går du till **Administration**  > **säkerhets**  > **säkerhets roller**
2. Högerklicka på en roll och klicka på **Kopiera**. Rollen som du kopierar har redan tilldelats behörigheter. Se till att du bara tar med de behörigheter som du vill använda. 
3. Ge den anpassade rollen ett **namn** och en **Beskrivning**. 
4. Tilldela säkerhets rollen behörigheterna som beskrivs nedan.  

### <a name="security-role-permissions"></a>Säkerhets roll behörigheter  

**Roll namn**: skript utlöpare  
- **Beskrivning**: de här behörigheterna gör det möjligt för den här rollen att endast köra skript som tidigare har skapats och godkänts av andra roller.  
- **Behörigheter:** Se till att följande är inställt på **Ja**.  

|Kategori|Behörighet|Status|
|---|---|---|
|Samling|Kör skript|Ja|
|Webbplats|Läsa|Ja|
|SMS-skript|Läsa|Ja|


**Roll namn**: skript författare  
- **Beskrivning**: de här behörigheterna gör att den här rollen kan skapa skript, men de kan inte godkänna eller köra dem.  
- **Behörigheter**: se till att följande behörigheter är inställda.
 
|Kategori|Behörighet|Status|
|---|---|---|
|Samling|Kör skript|Nej|
|Webbplats|Läsa|Ja|
|SMS-skript|Skapa|Ja|
|SMS-skript|Läsa|Ja|
|SMS-skript|Ta bort|Ja|
|SMS-skript|Ändra|Ja|


**Rollnamn**: skript god kännare  
- **Beskrivning**: de här behörigheterna gör det möjligt för den här rollen att godkänna skript, men de kan inte skapa eller köra dem.  
- **Behörigheter:** Se till att följande behörigheter är inställda.  

|Kategori|Behörighet|Status|
|---|---|---|
|Samling|Kör skript|Nej|
|Webbplats|Läsa|Ja|
|SMS-skript|Läsa|Ja|
|SMS-skript|Godkänn|Ja|
|SMS-skript|Ändra|Ja|

     
**Exempel på behörigheter för SMS-skript för rollen skript författare**  

 ![Exempel på behörigheter för SMS-skript för rollen skript författare](./media/run-scripts/script_authors_permissions.png)


## <a name="create-a-script"></a>Skapa ett skript

1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.
2. I arbets ytan **program bibliotek** klickar du på **skript**.
3. På fliken **Start** går du till gruppen **skapa** och klickar på **skapa skript**.
4. Konfigurera följande inställningar på sidan **skript** i guiden skapa **skript** :
    - **Skript namn** – ange ett namn för skriptet. Även om du kan skapa flera skript med samma namn blir det svårare för dig att hitta det skript som du behöver i Configuration Manager-konsolen med hjälp av dubblettnamn.
    - **Skript språk** – för närvarande stöds endast PowerShell-skript.
    - **Importera** – importera ett PowerShell-skript till-konsolen. Skriptet visas i fältet **skript** .
    - **Rensa** – tar bort det aktuella skriptet från skript fältet.
    - **Skript** – visar det aktuella importerade skriptet. Du kan redigera skriptet i det här fältet vid behov.
5. Slutför guiden. Det nya skriptet visas i **skript** listan med statusen **väntar på godkännande**. Innan du kan köra det här skriptet på klient enheter måste du godkänna det. 

> [!IMPORTANT]
> Undvik att köra skript a omstart av enheten eller starta om Configuration Manager agenten när du använder funktionen kör skript. Om du gör det kan det leda till ett tillstånd för kontinuerlig omstart. Vid behov, finns det funktioner för klient avisering som aktiverar omstarter av enheter. [Kolumnen för väntande omstart](../../core/clients/manage/manage-clients.md#restart-clients) kan hjälpa dig att identifiera enheter som behöver startas om. 
> <!--SMS503978  -->

## <a name="script-parameters"></a>Skriptparametrar

Genom att lägga till parametrar i ett skript får du ökad flexibilitet för ditt arbete. Du kan inkludera upp till 10 parametrar. I följande avsnitt beskrivs funktionen kör skript funktionens aktuella funktion med skript parametrar för; *Sträng*, *heltals* data typer. Listor med förinställda värden är också tillgängliga. Om skriptet innehåller data typer som inte stöds får du en varning.

I dialog rutan **skapa skript** klickar du på **skript parametrar** under **skript**.

Var och en av dina skripts parametrar har en egen dialog ruta för att lägga till mer information och verifiering. Om det finns en standard parameter i skriptet räknas den in i parameter gränssnittet och du kan ange den. Configuration Manager skriver inte över standardvärdet eftersom det aldrig kommer att ändra skriptet direkt. Du kan tänka på detta som "förifyllda föreslagna värden" i användar gränssnittet, men Configuration Manager ger inte till gång till "default"-värden i körnings läge. Detta kan du arbeta runt genom att redigera skriptet så att det har rätt standardinställningar. <!--17694323-->

>[!IMPORTANT]
> Parameter värden får inte innehålla ett enkelt citat tecken. </br></br>
> Det finns ett känt problem där parameter värden som innehåller eller omges av enkla citat tecken inte skickas till skriptet korrekt. Använd dubbla citat tecken i stället när du anger standard parameter värden som innehåller ett blank steg i ett skript. När du anger standard parameter värden när du skapar eller kör ett **skript**, är det inte nödvändigt att omge standardvärdet i dubbla eller enkla citat tecken oavsett om värdet innehåller ett blank steg eller inte.

### <a name="parameter-validation"></a>Parameter validering

Varje parameter i skriptet har en dialog ruta för **skript parameter egenskaper** där du kan lägga till verifiering för den parametern. När du har lagt till verifieringen bör du få fel om du anger ett värde för en parameter som inte uppfyller dess verifiering.

#### <a name="example-firstname"></a>Exempel: *FirstName*

I det här exemplet kan du ange egenskaperna för parametern String, *FirstName*.

![Skript parametrar-sträng](./media/run-scripts/RS-parameters-string.png)


Avsnittet validering i dialog rutan **Egenskaper för skript parameter** innehåller följande fält som du använder:

- **Minsta längd** – minsta antal tecken i fältet *FirstName* .
- **Maximal längd**-maximalt antal tecken i fältet *förnamn*
- **Regex** -kort för *reguljärt uttryck*. Mer information om hur du använder det reguljära uttrycket finns i nästa avsnitt *med verifiering av reguljära uttryck*.
- **Anpassat fel** – användbart för att lägga till ett eget anpassat fel meddelande som ersätter eventuella fel meddelanden i system verifieringen.

#### <a name="using-regular-expression-validation"></a>Använda verifiering av reguljära uttryck

Ett reguljärt uttryck är en kompakt form av programmering för att kontrol lera en sträng med tecken mot en kodad verifiering. Du kan till exempel kontrol lera att det inte finns något versalt alfabetiskt tecken i fältet *FirstName* genom `[^A-Z]` att placera i fältet *regex* .

Den reguljära uttrycks bearbetningen för den här dialog rutan stöds av .NET Framework. Vägledning om hur du använder reguljära uttryck finns i [reguljära uttryck för .net](/dotnet/standard/base-types/regular-expressions) och [reguljära uttryck](/dotnet/standard/base-types/regular-expression-language-quick-reference).


## <a name="script-examples"></a>Skriptexempel

Här följer några exempel som illustrerar skript som du kanske vill använda med den här funktionen.

### <a name="create-a-new-folder-and-file"></a>Skapa en ny mapp och fil

Det här skriptet skapar en ny mapp och en fil i mappen, med tanke på dina namngivnings indata.

``` PowerShell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Hämta OS-version

Det här skriptet använder WMI för att fråga datorn om dess OS-version.

``` PowerShell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="edit-or-copy-powershell-scripts"></a><a name="bkmk_psedit"></a> Redigera eller kopiera PowerShell-skript
<!--3705507-->
*(Lanserades med version 1902)*  
Du kan **redigera** eller **Kopiera** ett befintligt PowerShell-skript som används med funktionen **Kör skript** . I stället för att skapa ett skript som du behöver ändra direkt redigerar du det nu. Båda åtgärderna använder samma guide upplevelse som när du skapar ett nytt skript. När du redigerar eller kopierar ett skript behåller Configuration Manager inte godkännande statusen.

> [!Tip]  
> Redigera inte ett skript som körs aktivt på klienter. Det ursprungliga skriptet slutförs inte och du kanske inte får de avsedda resultaten från dessa klienter.  

### <a name="edit-a-script"></a>Redigera ett skript

1. Gå till noden **skript** under arbets ytan **program varu bibliotek** .
1. Välj det skript som du vill redigera och klicka sedan på **Redigera** i menyfliksområdet. 
1. Ändra eller importera ditt skript på sidan **skript information** .
1. Klicka på **Nästa** för att visa **sammanfattningen** och **Stäng** när du är klar med redigeringen.

### <a name="copy-a-script"></a>Kopiera ett skript

1. Gå till noden **skript** under arbets ytan **program varu bibliotek** .
1. Markera skriptet som ska kopieras och klicka sedan på **Kopiera** i menyfliksområdet.
1. Byt namn på skriptet i fältet **skript namn** och gör ytterligare ändringar som du kan behöva.
1. Klicka på **Nästa** för att visa **sammanfattningen** och **Stäng** när du är klar med redigeringen.


## <a name="run-a-script"></a>Kör ett skript

När ett skript har godkänts kan det köras mot en enskild enhet eller en samling. När körningen av skriptet har påbörjats, lanseras det snabbt via ett system med hög prioritet och tids gränsen på en timme. Resultatet av skriptet returneras sedan med ett tillstånds meddelande system.

Så här väljer du en samling mål för skriptet:

1. Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.
2. I arbetsytan Tillgångar och efterlevnad klickar du på **Enhetssamlingar**.
3. I listan **enhets samlingar** klickar du på den samling enheter som du vill köra skriptet på.
4. Välj en samling som du vill välja och klicka på **Kör skript**.
5. På sidan **skript** i guiden **Kör skript** väljer du ett skript i listan. Endast godkända skript visas.
6. Klicka på **Nästa**och slutför sedan guiden.

> [!IMPORTANT]
> Om ett skript inte körs, till exempel eftersom en målenhet har inaktiverats under en timmes tids period, måste du köra den igen.

### <a name="target-machine-execution"></a>Körning av mål dator

Skriptet körs som *system* -eller *dator* konto på mål klienterna. Det här kontot har begränsad nätverks åtkomst. All åtkomst till fjärranslutna system och platser med skriptet måste tillhandahållas i enlighet med detta.

## <a name="script-monitoring"></a>Skript övervakning

När du har initierat körningen av ett skript på en samling av enheter kan du använda följande procedur för att övervaka åtgärden. Du kan övervaka ett skript i real tid när det körs och senare återgå till status och resultat för en specifik körning av skript körningen. Skript status data rensas som en del av [underhålls aktiviteten Ta bort föråldrade klient åtgärder](../../core/servers/manage/reference-for-maintenance-tasks.md) eller borttagning av skriptet.<br>

![Skript övervakare – skript körnings status](./media/run-scripts/RS-monitoring-three-bar.png)

1. Klicka på **övervakning**i Configuration Manager-konsolen.
2. I arbets ytan **övervakning** klickar du på **skript status**.
3. I listan **skript status** visar du resultaten för varje skript som du körde på klient enheter. En avslutnings kod på skriptet **0** visar vanligt vis att skriptet har körts.

 
   ![Skript övervakaren – trunkerat skript](./media/run-scripts/Script-monitoring-truncated.png)

## <a name="script-output"></a>Skriptets utdata

Klientens retur skript utdata med JSON-formatering genom att skicka in skript resultatet till [ConvertTo-JSON-](/powershell/module/microsoft.powershell.utility/convertto-json) cmdleten. JSON-formatet returnerar konsekvent läsbara utdata från skriptet. För skript som inte returnerar objekt som utdata konverterar cmdleten ConvertTo-JSON utdata till en enkel sträng som klienten returnerar i stället för JSON.  

- Skript som får ett okänt resultat eller där klienten var offline visas inte i diagrammen eller data uppsättningen. <!--507179-->
- Undvik att returnera stora utdata i skriptet eftersom det trunkeras till 4 KB. <!--508488-->
- Konvertera ett Enum-objekt till ett sträng värde i skript så att de visas korrekt i JSON-format. <!--508377-->

   ![Omvandla Enum-objekt till ett sting-värde](./media/run-scripts/enum-tostring-JSON.png)

Du kan visa detaljerad skript utmatning i oformaterat eller strukturerat JSON-format. Den här formateringen gör det lättare att läsa och analysera utdata. Om skriptet returnerar en giltig JSON-formaterad text eller om utdata kan konverteras till JSON med PowerShell [-cmdleten ConvertTo-JSON](/powershell/module/microsoft.powershell.utility/convertto-json) , visar du de detaljerade utdata som antingen **JSON-utdata** eller **rå utdata**. I annat fall är det enda alternativet **skript-utdata**.

### <a name="example-script-output-is-convertible-to-valid-json"></a>Exempel: skriptets utdata kan konverteras till giltig JSON

Kommandoprompt `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

### <a name="example-script-output-isnt-valid-json"></a>Exempel: skriptets utdata är inte giltig JSON

Kommandoprompt `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```

## <a name="log-files"></a>Loggfiler

- Som standard på klienten i C:\Windows\CCM\logs:  
  - **Scripts. log**  
  - **CcmMessaging.log**  

- I hanterings paketet, som standard i C:\ SMS_CCM \Logs:
  - **MP_RelayMsgMgr. log**  

- På plats servern som standard i C:\Program Files\Configuration Manager\Logs:
  - **SMS_Message_Processing_Engine. log**

## <a name="see-also"></a>Se även

- [Konfigurera rollbaserad administration för Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Grunderna i rollbaserad administration](../../core/understand/fundamentals-of-role-based-administration.md)