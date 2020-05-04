---
title: Paketdefinitionsfiler
titleSuffix: Configuration Manager
description: Lär dig mer om att använda paket definitions filer för att skapa paket och program i Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d2d0dcad06c18b13b337185ae1feb768a7ee323
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710141"
---
# <a name="package-definition-files"></a>Paketdefinitionsfiler

*Gäller för: Configuration Manager (aktuell gren)*

Paket definitions filer är skript som hjälper dig att automatisera skapandet av [paket och program](packages-and-programs.md) i Configuration Manager. De tillhandahåller all information som Configuration Manager behöver för att skapa ett paket och program, förutom platsen för paketets källfiler.

## <a name="about-the-package-definition-file-format"></a>Om paket definitions fil formatet

Varje paket definitions fil är en ASCII-eller UTF-8-textfil som använder fil formatet. ini. Den innehåller följande avsnitt:  

### <a name="pdf"></a>[PDF]

Det här avsnittet identifierar filen som en paketdefinitionsfil. Det innehåller följande information:  

- **Version**: ange versionen för det paket definitions fil format som filen använder. Den här versionen motsvarar den version av Configuration Manager som den skrevs för. Den här posten måste anges.  

### <a name="package-definition"></a>[Package Definition]

Ange egenskaperna för paketet och programmet. Den innehåller följande information:  

- **Name**: Namnet på paketet, högst 50 tecken.  

- **Version** (valfritt): versionen av paketet, upp till 32 tecken.  

- **Ikon** (valfritt): filen som innehåller den ikon som ska användas för det här paketet. Om den här ikonen anges ersätter den här ikonen standard paket ikonen i Configuration Manager-konsolen.

- **Publisher**: Paketets utgivare, högst 32 tecken.

- **Language**: Språkversion för paketet, högst 32 tecken.

- **Kommentar** (valfritt): en kommentar om paketet, upp till 127 tecken.

- **ContainsNoFiles**: den här posten anger om paketet innehåller källfiler.  

- **Program**: de program som du definierar för det här paketet. Varje programnamn motsvarar ett **[Program]**-avsnitt i den här paketdefinitionsfilen.  

    Exempel:  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**: Namnet på den MIF-fil (Management Information Format) som innehåller paketstatus, högst 50 tecken.  

- **MIFName**: namnet på paketet för MIF-matchning, upp till 50 tecken.  

- **MIF version**: paketets versions nummer för MIF-matchning, upp till 32 tecken.  

- **MIFPublisher**: program varu utgivaren för paketet för MIF-matchning, upp till 32 tecken.  

### <a name="program"></a>[Program]

Ta med avsnittet [program] för varje program som du anger i posten **program** i avsnittet **[Package Definition]** . I det här avsnittet definieras varje program. Varje program avsnitt innehåller följande information:  

- **Name**: Namnet på programmet, högst 50 tecken. Den här posten måste vara unikt i ett paket.  

- **Ikon** (valfritt): Ange den fil som innehåller den ikon som ska användas för programmet. Den här ikonen ersätter standard program ikonen i Configuration Manager-konsolen. Klienten visar även den här ikonen när du distribuerar programmet till en samling.

- **Kommentar** (valfritt): en kommentar om programmet, upp till 127 tecken.

- **Kommando rad: Ange**kommando raden för programmet, upp till 127 tecken. Kommandot avser paketkällmappen.

- **Starta**: Ange arbetsmappen för programmet, upp till 127 tecken. Posten kan vara en absolut sökväg på klient datorn eller en sökväg som är relativ till paketets källmapp.

- **Kör**: Ange i vilket läge programmet ska köras. Du kan ange **Minimerat**, **Maximerat** eller **Dolt**. Om du inte tar med den här posten körs programmet i normalt läge.  

- **AfterRunning**: Ange eventuella särskilda åtgärder som inträffar när programmet har slutförts. Alternativen är **SMSRestart**, **ProgramRestart** eller **SMSLogoff**. Om du inte tar med den här posten körs inte en särskild åtgärd i programmet.  

- **EstimatedDiskSpace**: Ange hur mycket disk utrymme som krävs för att köra programmet på datorn. Standardvärdet är **Okänt**. Du kan ange värdet som ett heltal som är större än eller lika med noll. Om du anger ett värde inkluderar du även enhetens värden.  

    Exempel:  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime**: Ange den uppskattade varaktigheten i minuter som du förväntar dig att programmet ska köras på klient datorn. Standardvärdet är **120**. Du kan ange värdet som ett heltal som är större än noll eller **Okänt**.  

    Exempel:  

    `EstimatedRunTime=25`  

- **SupportedClients**: Ange de processorer och operativ system som programmet körs på. Avgränsa plattformarna med kommatecken. Om du inte tar med den här posten kontrollerar klienten inte vilka plattformar som stöds för programmet.  

- **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: Ange start-till-slut-intervallet för versions nummer för de operativ system som anges i posten **SupportedClients** .  

    Exempel:  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **AdditionalProgramRequirements** (valfritt): Ange annan information eller krav för klient datorer, upp till 127 tecken.

- **CanRunWhen**: Ange den användar status som krävs för att köra programmet på klient datorn. Tillgängliga värden är **UserLoggedOn**, **NoUserLoggedOn** och **AnyUserStatus**. Standardvärdet är **UserLoggedOn**.  

- **UserInputRequired**: Ange om programmet kräver interaktion med användaren. Tillgängliga värden är **True** och **False**. Standardvärdet är **True**. Värdet är **false** om **CanRunWhen** inte är inställt på **UserLoggedOn**.  

- **AdminRightsRequired**: Ange om programmet kräver administratörs behörighet på datorn som ska köras. Tillgängliga värden är **True** och **False**. Standardvärdet är **false**. Värdet är **True** om **CanRunWhen** inte är inställt på **UserLoggedOn**.  

- **UseInstallAccount**: Ange om programmet ska använda klient program varans installations konto när det körs på klient datorer. Standardvärdet är **False**. Värdet är också **False** om **CanRunWhen** är inställt på **UserLoggedOn**.  

- **DriveLetterConnection**: Ange om programmet kräver en enhets betecknings anslutning till paketfilerna på distributions platsen. Du kan ange **True** eller **False**. Standardvärdet är **false**, vilket gör att programmet kan använda en Universal NAMING Convention (UNC-anslutning). När det här värdet är inställt på **Sant**, använder klienten nästa tillgängliga enhets beteckning, som börjar med Z: och fortsätter bakåt.  

- **SpecifyDrive** (valfritt): Ange en enhets beteckning som programmet behöver för att ansluta till paketfilerna på distributions platsen. Den här inställningen tvingar användningen av den angivna enhets beteckningen för klient anslutningar till distributions platser.

- **ReconnectDriveAtLogon**: Ange om datorn återansluter till distributions platsen när användaren loggar in. Tillgängliga värden är **True** och **False**. Standardvärdet är **false**.  

- **DependentProgram**: Ange ett program i det här paketet som måste köras före det aktuella programmet. I den här posten används `DependentProgram=<ProgramName>`formatet, `<ProgramName>` där är **namn** posten för programmet i paket definitions filen. Lämna det tomt om det inte finns några beroende program.  

    Exempel:  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **Tilldelning**: Ange hur programmet ska tilldelas användare. Det här värdet kan vara:

    - **FirstUser**: endast den första användare som loggar in på klienten kör programmet
    - **EveryUser**: varje användare som loggar in kör programmet

    När **CanRunWhen** inte är inställt på **UserLoggedOn**anges den här posten till **FirstUser**.  

- **Inaktive rad**: Ange om du kan distribuera programmet till klienter. Tillgängliga värden är **True** och **False**. Standardvärdet är **false**.  


## <a name="use-a-package-definition-file"></a>Använda en paket definitions fil  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **program hantering**och väljer noden **paket** .  

2. På fliken **Start** i menyfliksområdet väljer du **skapa paket från definition**i gruppen **skapa** .  

3. På sidan **paket definition** i **guiden Skapa paket från definition**väljer du en befintlig paket definitions fil. Om du vill öppna en ny paket definitions fil väljer du **Bläddra**. När du har angett en ny paket definitions fil markerar du den i listan **paket definition** .

4. På sidan **källfiler** anger du information om eventuella källfiler som krävs för paketet och programmet.  

5. Om paketet kräver källfiler går du till sidan **källmapp** och anger den plats från vilken platsen kan hämta källfilerna.  

6. Slutför guiden.  


## <a name="see-also"></a>Se även

[Paket och program](packages-and-programs.md)
