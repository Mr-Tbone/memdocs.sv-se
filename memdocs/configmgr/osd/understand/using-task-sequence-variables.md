---
title: Använda aktivitetssekvensvariabler
titleSuffix: Configuration Manager
description: Lär dig mer om hur du använder variablerna i en Configuration Manager aktivitetssekvens.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c043cfabc411dbd5ae4984110fc2904d37669300
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717827"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Så här använder du variabler för aktivitetssekvenser i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

 Motorn för aktivitetssekvenser i operativ system distributions funktionen i Configuration Manager använder många variabler för att styra dess beteenden. Använd följande variabler för att:

- Ange villkor för steg  
- Ändra beteenden för vissa steg  
- Använd i skript för mer komplexa åtgärder  

En referens för alla tillgängliga variabler för aktivitetssekvenser finns i [variabler](task-sequence-variables.md)för aktivitetssekvens.

## <a name="types-of-variables"></a><a name="bkmk_types"></a>Typer av variabler

Det finns flera typer av variabler:  

- [Inbyggd](#bkmk_built-in)  
- [Åtgärd](#bkmk_action)  
- [Anpassad](#bkmk_custom)  
- [Skrivskyddad](#bkmk_read-only)  
- [Matris](#bkmk_array)  

### <a name="built-in-variables"></a><a name="bkmk_built-in"></a>Inbyggda variabler

Inbyggda variabler ger information om miljön där aktivitetssekvensen körs. Deras värden är tillgängliga i hela aktivitetssekvensen. Vanligt vis initierar modulen för aktivitetssekvenser de inbyggda variablerna innan du kör några steg.

Till exempel `_SMSTSLogPath` är en miljö variabel som anger den sökväg som Configuration Manager-komponenter skriver loggfiler till. Alla steg i aktivitetssekvensen kan komma åt den här miljövariabeln.

Aktivitetssekvensen utvärderar vissa variabler före varje steg. `_SMSTSCurrentActionName` Visar till exempel namnet på det aktuella steget.

### <a name="action-variables"></a><a name="bkmk_action"></a>Action-variabler

Variabler för aktivitetssekvenser anger konfigurations inställningar som används i ett enda steg i en aktivitetssekvens. Som standard initierar steget sina inställningar innan det körs. De här inställningarna är bara tillgängliga när det associerade steget körs. Aktivitetssekvensen lägger till variabeln åtgärds värde i miljön innan steget körs. Den tar sedan bort värdet från miljön när steget har körts.

Du kan till exempel lägga till steget **Kör kommando rad** i en aktivitetssekvens. Det här steget innehåller en **Start i** -egenskap. Aktivitetssekvensen lagrar ett standardvärde för den här egenskapen som `WorkingDirectory` variabeln. Aktivitetssekvensen initierar det här värdet innan **körnings kommando rads** steget körs. När det här steget körs får du åtkomst till **Start i** egenskap svärdet från `WorkingDirectory` värdet. När steget har slutförts tar aktivitetssekvensen bort värdet för `WorkingDirectory` variabeln från miljön. Om aktivitetssekvensen innehåller ett annat **kommando rads** steg för körning initieras en ny `WorkingDirectory` variabel. Vid detta tillfälle ställer aktivitetssekvensen variabeln till startvärdet för det aktuella steget. Mer information finns i [WorkingDirectory](task-sequence-variables.md#WorkingDirectory).  

*Standardvärdet* för en åtgärds variabel finns när steget körs. Om du anger ett *nytt* värde är det tillgängligt för flera steg i aktivitetssekvensen. Om du åsidosätter ett standardvärde förblir det nya värdet i miljön. Detta nya värde åsidosätter standardvärdet för andra steg i aktivitetssekvensen. Du kan till exempel lägga till **variabel steget Ange aktivitetssekvens** som det första steget i aktivitetssekvensen. Det här steget anger `WorkingDirectory` variabeln `C:\`till. Alla **körnings kommando rads** steg i aktivitetssekvensen använder det nya Start Katalog svärdet.  

Vissa steg i aktivitetssekvensen markerar vissa åtgärds variabler som *utdata*. Steg senare i aktivitetssekvensen läser dessa utdata-variabler.

> [!Note]  
> Inte alla steg i aktivitetssekvensen har åtgärds variabler. Även om det till exempel finns variabler som är associerade med åtgärden **Aktivera BitLocker** , finns det inga variabler som är kopplade till åtgärden **inaktivera BitLocker** .  

### <a name="custom-variables"></a><a name="bkmk_custom"></a>Anpassade variabler

Dessa variabler är de som Configuration Manager inte skapar. Initiera dina egna variabler för användning som villkor, i kommando rader eller i skript.

Följ dessa rikt linjer när du anger ett namn på en ny aktivitetssekvens:  

- Variabel namnet för aktivitetssekvensen får innehålla bokstäver, siffror, under streck (`_`) och ett bindestreck (`-`).  

- Variabel namn för aktivitetssekvenser får innehålla minst en tecken längd och högst 256 tecken.  

- Användardefinierade variabler måste börja med en bokstav (`A-Z` eller `a-z`).  

- Användardefinierade variabel namn får inte inledas med under strecks tecknet. Endast skrivskyddade variabler för aktivitetssekvens föregås av under strecks tecknet.  

- Variabel namn för aktivitetssekvens är inte Skift läges känsliga. Till exempel `OSDVAR` och `osdvar` är samma variabel i aktivitetssekvensen.  

- Variabel namn för aktivitetssekvens får inte börja eller sluta med ett blank steg. De får inte heller innehålla inbäddade blank steg. Aktivitetssekvensen ignorerar blank steg i början eller slutet av ett variabel namn.  

Det finns ingen angiven gräns för hur många variabler för aktivitetssekvens som du kan skapa. Men antalet variabler är begränsat av storleken på aktivitetssekvensmiljön. Den totala storleksgränsen för aktivitetssekvensmiljön är 32 MB.  

### <a name="read-only-variables"></a><a name="bkmk_read-only"></a>Skrivskyddade variabler

Du kan inte ändra värdet för vissa variabler, som är skrivskyddade. Vanligt vis börjar namnet med ett under streck (`_`). Aktivitetssekvensen använder dem för driften. Skrivskyddade variabler visas i aktivitetssekvensen.

Dessa variabler är användbara i skript eller kommando rader. Du kan till exempel köra en kommando rad och skicka utdata till en loggfil i `_SMSTSLogPath` med de andra loggfilerna.

> [!NOTE]  
> Skrivskyddade variabler för aktivitetssekvens kan läsas av steg i en aktivitetssekvens, men de kan inte anges. Använd till exempel en skrivskyddad variabel som en del av kommando raden för steget **Kör kommando rad** . Du kan inte ange en skrivskyddad variabel med hjälp av **variabel steget Ange aktivitetssekvens** .  

### <a name="array-variables"></a><a name="bkmk_array"></a>Mat ris variabler

Aktivitetssekvensen lagrar vissa variabler som en matris. Varje element i matrisen representerar inställningarna för ett enskilt objekt. Använd de här variablerna när en enhet har fler än ett objekt att konfigurera. Följande steg i aktivitetssekvensen använder array-variabler:

- [Använd nätverksinställningar](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

- [Formatera och partitionera disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  

## <a name="how-to-set-variables"></a><a name="bkmk_set"></a>Ange variabler

För anpassade variabler eller variabler som inte är skrivskyddade finns det flera metoder för att initiera och ange värdet för variabeln:  

- [Variabel steget Ange aktivitetssekvens](#bkmk_set-ts-step)
- Steg för att [Ange dynamiska variabler](#bkmk_set-dyn-step)
- [Kör PowerShell-skript](#bkmk_run-ps) steg
- [Samlings-och enhets variabler](#bkmk_set-coll-var)  
- [TSEnvironment COM-objekt](#bkmk_set-com)  
- [För inläsnings kommando](#bkmk_set-prestart)  
- [Guiden aktivitetssekvens](#bkmk_set-tswiz)
- [Guiden media för aktivitetssekvens](#bkmk_set-media)  

Ta bort en variabel från miljön med samma metoder som när du skapar en variabel. Om du vill ta bort en variabel anger du variabeln värde till en tom sträng.  

Du kan kombinera metoder för att ställa in en aktivitetssekvens-variabel till olika värden för samma sekvens. Ange till exempel standardvärdena med hjälp av redigeraren för aktivitetssekvens och ange sedan anpassade värden med hjälp av ett skript.

Om du ställer in samma variabel med olika metoder, använder modulen för aktivitetssekvenser följande ordning:  

1. Den utvärderar först Collection-variabler.  

2. Enhetsspecifika variabler åsidosätter samma variabel uppsättning i en samling.  

3. Variabler som anges med någon av metoderna under aktivitetssekvensen prioriteras över samlings-eller enhets variabler.  

### <a name="general-limitations-for-task-sequence-variable-values"></a>Allmänna begränsningar för variabla värden i aktivitetssekvensen

- Variabla värden i aktivitetssekvens får innehålla högst 4 000 tecken.  

- Du kan inte ändra en variabel för skrivskyddad aktivitetssekvens. Skrivskyddade variabler har namn som börjar med ett under streck (`_`).  

- Variabla värden i aktivitetssekvensen kan vara Skift läges känsliga beroende på användningen av värdet. I de flesta fall är variabel värden för aktivitetssekvens inte Skift läges känsliga. En variabel som innehåller ett lösen ord är Skift läges känslig.  

### <a name="set-task-sequence-variable"></a><a name="bkmk_set-ts-step"></a>Ange variabel för aktivitetssekvens

Använd det här steget i aktivitetssekvensen för att ange en enskild variabel till ett enda värde.

Mer information finns i [ange variabel](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)för aktivitetssekvens.

### <a name="set-dynamic-variables"></a><a name="bkmk_set-dyn-step"></a>Ange dynamiska variabler

Använd det här steget i aktivitetssekvensen för att ange en eller flera variabler för aktivitetssekvens. Du definierar regler i det här steget för att avgöra vilka variabler och värden som ska användas.

Mer information finns i [Ange dynamiska variabler](task-sequence-steps.md#BKMK_SetDynamicVariables).

### <a name="run-powershell-script"></a><a name="bkmk_run-ps"></a>Kör PowerShell-skript

<!-- 6315548 -->

Använd det här steget i aktivitetssekvensen om du vill använda ett PowerShell-skript för att ange en variabel för en aktivitetssekvens.

Du kan ange ett skript namn från ett paket eller ange ett PowerShell-skript direkt i steget. Använd sedan egenskapen steg för att **skriva utdata till variabeln** aktivitetssekvens för att spara skript resultatet till en anpassad aktivitetssekvens.

Mer information om det här steget finns i [kör PowerShell-skript](task-sequence-steps.md#BKMK_RunPowerShellScript).

> [!NOTE]
> Du kan också använda ett PowerShell-skript för att ange en eller flera variabler med **TSEnvironment** -objektet. Mer information finns i [så här använder du variabler i en](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) aktivitetssekvens som körs i Configuration Manager SDK.

#### <a name="example-scenario-with-run-powershell-script-step"></a>Exempel scenario med kör PowerShell-skript steg

Din miljö har användare i flera länder, så du vill ställa frågor om OS-språket så att det är ett villkor för flera språkspecifika **Apply OS** -steg.

1. Lägg till en instans av **Run PowerShell-skriptet** i aktivitetssekvensen innan du **installerar operativ Systems** stegen.

1. Använd alternativet för att **Ange ett PowerShell-skript** för att ange följande kommando:

    ```powershell
    (Get-Culture).TwoLetterISOLanguageName
    ```

    Mer information om cmdleten finns i [Get-Culture](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/get-culture). Mer information om ISO-Språknamnen med två bokstäver finns i [lista över iso 639-1-koder](https://wikipedia.org/wiki/List_of_ISO_639-1_codes).

1. Ange `CurrentOSLanguage`som alternativ för att skriva **utdata till en aktivitetssekvens**.

    ![Skärm bild av exempel på kör PowerShell-skript steg](media/run-powershell-script-example-language.png)

1. Skapa följande villkor i steget **Använd operativ system** för den engelska språk bilden:`Task Sequence Variable CurrentOSLanguage equals "en"`

    ![Skärm bild av ett exempel på villkor för att tillämpa OS-steg](media/condition-custom-task-sequence-variable.png)

    > [!TIP]
    > Mer information om hur du skapar ett villkor i ett steg finns i [så här får du åtkomst till variabler – steg villkor](#bkmk_access-condition).

1. Spara och distribuera aktivitetssekvensen.

När steget **kör PowerShell-skript** körs på en enhet med den engelska språk versionen av Windows, returnerar kommandot värdet `en`. Sedan sparas värdet i den anpassade variabeln. När steget **Använd OS** -steget för den engelska språk avbildningen körs på samma enhet, utvärderas villkoret som sant. Om du har flera instanser av **Apply OS** -steget för olika språk, kör aktivitetssekvensen dynamiskt det steg som matchar OS-språket.

### <a name="collection-and-device-variables"></a><a name="bkmk_set-coll-var"></a>Samlings-och enhets variabler

Du kan definiera anpassade variabler för aktivitetssekvens för enheter och samlingar. Variabler som du definierar för en enhet kallas för variabler för aktivitetssekvens för enheter. Variabler som definieras för en samling kallas aktivitetssekvensvariabler per samling. Om det finns en konflikt prioriteras variabler per enhet framför variabler per samling. Detta innebär att aktivitetssekvenser som tilldelas en speciell enhet automatiskt har högre prioritet än variabler som har tilldelats den samling som innehåller enheten.  

Till exempel är enhet XYZ medlem i samlingen ABC. Du tilldelar en variabel till samling ABC med värdet 1. Du tilldelar också en variabel till enhet XYZ med värdet 2. Variabeln som är tilldelad XYZ har högre prioritet än variabeln som har tilldelats till samlingen ABC. När en aktivitetssekvens med denna variabel körs på XYZ, har variabeln värdet 2.

Du kan dölja variabler per enhet och per samling så att de inte visas i Configuration Manager-konsolen. Om du använder alternativet **Visa inte det här värdet i Configuration Manager-konsolen**, visas inte värdet för variabeln i-konsolen. Variabeln kan fortfarande användas av aktivitetssekvensen när den körs. Om du inte längre vill att dessa variabler ska vara dolda tar du bort dem först. Definiera sedan om variablerna utan att välja alternativet att dölja dem.  

> [!WARNING]  
> Inställningen för att **inte Visa det här värdet i Configuration Manager-konsolen** gäller bara för Configuration Manager-konsolen. Värdena för variablerna visas fortfarande i logg filen för aktivitetssekvensen (**Smsts. log**).

Du kan hantera variabler per enhet på en primär plats eller på en central administrations plats. Configuration Manager stöder inte fler än 1 000 tilldelade variabler för en enhet.  

> [!IMPORTANT]  
> När du använder variabler per samling för aktivitetssekvenser bör du tänka på följande:  
>
> - Ändringar i samlingar replikeras alltid i hela hierarkin. Eventuella ändringar som du gör i Collection-variablerna gäller inte bara medlemmar av den aktuella platsen, utan till alla medlemmar i samlingen i hela hierarkin.  
>  
> - När du tar bort en samling tar den här åtgärden även bort de variabler för aktivitetssekvens som du har konfigurerat för samlingen.  

#### <a name="create-task-sequence-variables-for-a-device"></a>Skapa variabler för aktivitetssekvens för en *enhet*

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enheter** .  

2. Välj mål enheten och välj **Egenskaper**.  

3. I dialog rutan **Egenskaper** växlar du till fliken **variabler** .  

4. Välj ikonen **ny** för varje variabel som du vill skapa. Ange **namn** och **värde** för variabeln aktivitetssekvens. Om du vill dölja variabeln så att den inte visas i Configuration Manager-konsolen väljer du alternativet **Visa inte det här värdet i Configuration Manager-konsolen**.  

5. När du har lagt till alla variabler i enhets egenskaperna väljer du **OK**.  

#### <a name="create-task-sequence-variables-for-a-collection"></a>Skapa variabler för aktivitetssekvens för en *samling*

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enhets samlingar** . Välj mål samlingen och välj **Egenskaper**.  

2. I dialog rutan **Egenskaper** växlar du till fliken **Collection-variabler** .  

3. Välj ikonen **ny** för varje variabel som du vill skapa. Ange **namn** och **värde** för variabeln aktivitetssekvens. Om du vill dölja variabeln så att den inte visas i Configuration Manager-konsolen väljer du alternativet **Visa inte det här värdet i Configuration Manager-konsolen**.  

4. Du kan också ange prioriteten för Configuration Manager som ska användas när variablerna för aktivitetssekvensen utvärderas.  

5. När du har lagt till alla variabler i samlings egenskaperna väljer du **OK**.  

### <a name="tsenvironment-com-object"></a><a name="bkmk_set-com"></a>TSEnvironment COM-objekt

Använd **TSEnvironment** -objektet om du vill arbeta med variabler från ett skript.

Mer information finns i [så här använder du variabler i en](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) aktivitetssekvens som körs i Configuration Manager SDK.

### <a name="prestart-command"></a><a name="bkmk_set-prestart"></a>För inläsnings kommando

För inläsnings kommandot är ett skript eller en körbar fil som körs i Windows PE innan användaren väljer aktivitetssekvensen. För inläsnings kommandot kan fråga en variabel eller fråga användaren om information och sedan spara den i-miljön. Använd [TSEnvironment](#bkmk_set-com) com-objekt för att läsa och skriva variabler från för inläsnings kommandot.

Mer information finns i [för inläsnings kommandon för media i aktivitetssekvensen](prestart-commands-for-task-sequence-media.md).

### <a name="task-sequence-wizard"></a><a name="bkmk_set-tswiz"></a>Guiden aktivitetssekvens

Från och med version 1906, när du har valt en aktivitetssekvens i fönstret aktivitetssekvens, innehåller sidan för att redigera variabler för aktivitetssekvens en **redigerings** knapp. Du kan använda tillgängliga kortkommandon för att redigera variablerna. Den här ändringen hjälper i fall där musen inte är tillgänglig.<!-- 4668846 -->

### <a name="task-sequence-media-wizard"></a><a name="bkmk_set-media"></a>Guiden media för aktivitetssekvens

Ange variabler för aktivitetssekvenser som körs från media. När du använder medier för att distribuera operativ systemet lägger du till variablerna för aktivitetssekvens och anger deras värden när du skapar mediet. Variablerna och deras värden lagras på mediet.  

> [!NOTE]  
> Aktivitetssekvenser lagras på fristående media. Men alla andra typer av medier, till exempel för beredda medier, hämtar aktivitetssekvensen från en hanterings plats.  

När du kör en aktivitetssekvens från media kan du lägga till en variabel på sidan **anpassning** i guiden.

Använd medievariablerna som finns för variabler per samling eller per dator. Om aktivitetssekvensen körs från media, gäller inte variabler per dator och per samling och används inte.  

> [!TIP]  
> Aktivitetssekvensen skriver paket-ID: t och för inläsnings kommando raden till filen **CreateTSMedia. log** på den dator som kör Configuration Manager-konsolen. Den här logg filen innehåller värdet för alla variabler i en aktivitetssekvens. Granska logg filen för att kontrol lera värdet för variablerna för aktivitetssekvensen.  

Mer information finns i [skapa media för aktivitetssekvens](../deploy-use/create-task-sequence-media.md).

## <a name="how-to-access-variables"></a><a name="bkmk_access"></a>Så här använder du variabler

När du har angett variabeln och dess värde genom att använda någon av metoderna från föregående avsnitt, använder du den i dina aktivitetssekvenser. Du kan till exempel få åtkomst till standardvärden för inbyggda variabler i aktivitetssekvensen eller göra ett steg beroende av värdet för en variabel.  

Använd följande metoder för att få åtkomst till variabel värden i aktivitetssekvensen:

- [Använd i ett steg](#bkmk_access-step)  
- [Steg villkor](#bkmk_access-condition)  
- [Anpassat skript](#bkmk_access-script)  
- [Svarsfil för installations programmet för Windows](#bkmk_access-answer)  
  
### <a name="use-in-a-step"></a><a name="bkmk_access-step"></a>Använd i ett steg

Ange ett variabel värde för en inställning i ett steg i en aktivitetssekvens. I redigeraren för aktivitetssekvens redigerar du steget och anger variabel namnet som fält värde. Omge variabelns namn i procent tecken (`%`).

Du kan till exempel använda variabel namnet som en del av **kommando rads** fältet i steget **Kör kommando rad** . Följande kommando rad skriver dator namnet till en textfil.

`cmd.exe /c %_SMSTSMachineName% > C:\File.txt`

### <a name="step-condition"></a><a name="bkmk_access-condition"></a>Steg villkor

Använd inbyggda eller anpassade variabler för aktivitetssekvens som en del av ett villkor i ett steg eller en grupp. Aktivitetssekvensen utvärderar variabelvärdet innan det kör steget eller gruppen.

Gör så här om du vill lägga till ett villkor som utvärderar ett variabel värde:  

1. I redigeraren för aktivitetssekvens väljer du det steg eller den grupp som du vill lägga till villkoret i.  

2. Växla till fliken **alternativ** för steget eller gruppen. Klicka på **Lägg till villkor**och välj **variabeln**aktivitetssekvens.  

3. I dialog rutan **variabel** för aktivitetssekvens anger du följande inställningar:  

    - **Variabel**: namnet på variabeln. Till exempel `_SMSTSInWinPE`.  

    - **Villkor**: villkoret för att utvärdera variabelvärdet. Till exempel **är lika med**.  

    - **Värde**: värdet för den variabel som ska kontrol leras. Till exempel `false`.  

De tre exemplen ovan utgör ett vanligt villkor för att testa om aktivitetssekvensen körs från en start avbildning i Windows PE:

> **Variabel för aktivitetssekvens**`_SMSTSInWinPE equals "false"`

Se det här tillståndet i gruppen **avbilda filer och inställningar** i standardmallen för aktivitetssekvens för att installera en befintlig operativ system avbildning.

Mer information om villkor finns i [Redigeraren för aktivitetssekvens-villkor](task-sequence-editor.md#bkmk_conditions).

### <a name="custom-script"></a><a name="bkmk_access-script"></a>Anpassat skript

Läs och skriv variabler genom att använda **Microsoft. SMS. TSEnvironment** com-objektet medan aktivitetssekvensen körs.

Följande Windows PowerShell-exempel frågar **_SMSTSLogPath** -variabeln för att hämta den aktuella logg platsen. Skriptet konfigurerar också en anpassad variabel.

```PowerShell
# Create an object to access the task sequence environment
$tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment

# Query the environment to get an existing variable
# Set a variable for the task sequence log path
$LogPath = $tsenv.Value("_SMSTSLogPath")

# Or, convert all of the variables currently in the environment to PowerShell variables
$tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

# Write a message to a log file
Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append

# Set a custom variable "startTime" to the current time
$tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
```

### <a name="windows-setup-answer-file"></a><a name="bkmk_access-answer"></a>Svarsfil för installations programmet för Windows

Svars filen för Windows-installationen som du anger kan ha inbäddade variabler för aktivitetssekvens. Använd formuläret `%varname%`där *varname* är namnet på variabeln. Steget **Installera Windows och ConfigMgr** ersätter variabel namn strängen för det faktiska variabel värdet. Dessa inbäddade variabler för aktivitetssekvens kan inte användas i ett numeriskt fält i svars filen Unattend. xml.

Mer information finns i avsnittet [Setup Windows and ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).

## <a name="see-also"></a>Se även

- [Aktivitetssekvenssteg](task-sequence-steps.md)

- [Aktivitetssekvensvariabler](task-sequence-variables.md)

- [Att tänka på när du planerar automatiseringsuppgifter](../plan-design/planning-considerations-for-automating-tasks.md)

- [Redigeraren för aktivitetssekvens](task-sequence-editor.md)
