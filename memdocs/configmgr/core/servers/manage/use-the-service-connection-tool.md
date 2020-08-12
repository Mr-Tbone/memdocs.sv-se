---
title: Tjänst anslutnings verktyg
titleSuffix: Configuration Manager
description: Lär dig mer om det här verktyget som gör att du kan ansluta till Configuration Manager moln tjänsten för manuell uppladdning av användnings information.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b56b849be6abd2634e29d35e58494d4d3215857
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126094"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Använd tjänst anslutnings verktyget för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd **tjänst anslutnings verktyget** när tjänst anslutnings punkten är i offline-läge. Du kan också använda den när din Configuration Manager plats system servrar inte är anslutna till Internet. Verktyget kan hjälpa dig att hålla din webbplats uppdaterad med de senaste uppdateringarna för Configuration Manager.

När du kör verktyget ansluter det till Configuration Manager moln tjänsten, laddar upp användnings information för hierarkin och hämtar uppdateringar. Överföring av användnings data krävs för att moln tjänsten ska kunna tillhandahålla rätt uppdateringar för din miljö.

## <a name="prerequisites"></a>Krav

- Platsen har en tjänst anslutnings punkt och du konfigurerar den för en offline- **anslutning på begäran**.

- Kör verktyget från en kommando tolk som administratör. Det finns inget användar gränssnitt.

- Du kör verktyget från tjänst anslutnings punkten och en dator som kan ansluta till Internet. Var och en av dessa datorer måste ha ett x64-bitars operativ system och ha följande komponenter:

  - Filer för både **Visual C++ Redistributable** x86 och x64. Som standard installerar Configuration Manager x64-versionen på datorn som är värd för tjänst anslutnings punkten. Information om hur du hämtar den här komponenten finns i [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784).

  - **.NET Framework 4.5.2** eller senare

- Det konto som du använder för att köra verktyget måste ha följande behörigheter:

  - **Lokal administratör** på den dator som är värd för tjänst anslutnings punkten

  - **Läs** behörighet till plats databasen

- Du behöver en metod för att överföra filerna mellan datorn med Internet åtkomst och tjänst anslutnings punkten. Till exempel en USB-enhet med tillräckligt mycket ledigt utrymme för att lagra filer och uppdateringar.

## <a name="overview"></a>Översikt

1. **Förbered**: kör verktyget på tjänst anslutnings punkten. Den placerar dina användnings data i en CAB-fil på den plats du anger. Kopiera data filen till datorn med en Internet anslutning.

2. **Anslut**: kör verktyget på datorn med en Internet anslutning. Den laddar upp dina användnings data och hämtar sedan Configuration Manager uppdateringar. Kopiera hämtade uppdateringar till tjänst anslutnings punkten.

    Du kan ladda upp flera datafiler i taget, var och en från en annan hierarki. Du kan också ange en proxyserver och en användare för proxyservern.

3. **Importera**: kör verktyget på tjänst anslutnings punkten. Uppdateringarna importeras och läggs till på din webbplats. Du kan sedan Visa och [installera uppdateringarna](install-in-console-updates.md) i Configuration Manager-konsolen.

### <a name="upload-multiple-data-files"></a>Ladda upp flera datafiler

- Lägg till alla exporterade datafiler från separata hierarkier i samma mapp. Ge varje fil ett unikt namn. Om det behövs kan du byta namn på dem manuellt.

- När du kör verktyget för att ladda upp data till Microsoft anger du den mapp som innehåller datafilerna.

- När du kör verktyget för att importera data importerar verktyget bara data för den hierarkin.

### <a name="specify-a-proxy-server"></a>Ange en proxyserver

Om datorn med en Internet anslutning kräver en proxyserver stöder verktyget en grundläggande proxykonfiguration. Använd de valfria parametrarna **-proxyserveruri** och **-proxyusername**. Mer information finns i [kommando rads parametrar](#bkmk_cmd).

### <a name="specify-the-type-of-updates-to-download"></a>Ange vilken typ av uppdateringar som ska hämtas

Verktyget stöder alternativ för att styra vilka filer som du hämtar. Som standard hämtar verktyget bara den senaste tillgängliga uppdateringen som gäller för din webbplats version. Snabb korrigeringar laddas inte ned.

Ändra det här beteendet genom att använda någon av följande parametrar för att ändra vilka filer som hämtas:

- **-DownloadAll**: Ladda ned alla uppdateringar, inklusive uppdateringar och snabb korrigeringar, oavsett vilken version av webbplatsen som används.
- **-downloadhotfix**: Ladda ned alla snabb korrigeringar oavsett vilken version av webbplatsen du har.
- **-downloadsiteversion**: hämtar uppdateringar och snabb korrigeringar med en senare version än din webbplats version.

    > [!IMPORTANT]
    > På grund av ett känt problem i Configuration Manager version 2002 fungerar inte standard beteendet som förväntat. Uppdatera till version 2006 eller Använd parametern **-downloadsiteversion** för att hämta nödvändiga uppdateringar för version 2002.<!-- 7594517 -->

Mer information finns i [kommando rads parametrar](#bkmk_cmd).

> [!TIP]
> Verktyget fastställer versionen för din webbplats från data filen. Kontrol lera versionen genom att titta i CAB-filen för text filen med plats versionen.

## <a name="use-the-tool"></a>Använda verktyget  

Tjänst anslutnings verktyget finns på Configuration Manager installations medium på följande sökväg: `SMSSETUP\TOOLS\ServiceConnectionTool\ServiceConnectionTool.exe` . Använd alltid tjänst anslutnings verktyget som matchar den version av Configuration Manager som du använder. Alla dessa filer måste finnas i samma mapp för att tjänst anslutnings verktyget ska fungera.

Kopiera mappen **ServiceConnectionTool** med dess innehåll till datorn med en Internet anslutning.

I den här proceduren använder kommando rads exemplen följande fil namn och platser för mappar. Du behöver inte använda dessa sökvägar och fil namn. Du kan använda alternativ som matchar din miljö och dina inställningar.

- Sökvägen till källfilerna för Configuration Manager-installationsmedia på tjänst anslutnings punkten:`C:\Source`

- Sökvägen till en USB-enhet där du lagrar data som ska överföras mellan datorer:`D:\USB\`

- Namnet på den datafil som du exporterar från webbplatsen:`UsageData.cab`

- Namnet på den tomma mappen där verktyget lagrar hämtade uppdateringar för Configuration Manager:`UpdatePacks`

### <a name="prepare"></a>Förbereda

1. På den dator som är värd för tjänst anslutnings punkten öppnar du en kommando tolk som administratör och ändrar katalogen till verktygs platsen. Till exempel:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Kör följande kommando för att förbereda data filen:

    `ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

    > [!NOTE]
    > Om du överför datafiler från fler än en hierarki samtidigt, ger du varje datafil ett unikt namn. Om det behövs kan du byta namn på filer senare.

    Data i filen baseras på den nivå av diagnostik-och användnings data som du konfigurerar för platsen. Mer information finns i [Översikt över diagnostik-och användnings data](../../plan-design/diagnostics/diagnostics-and-usage-data.md). Du kan använda verktyget för att exportera data till en CSV-fil för att visa innehållet. Mer information finns i [-export](#-export).

1. När verktyget har slutfört exporten av användnings data kopierar du data filen till en dator som har åtkomst till Internet.

### <a name="connect"></a>Ansluta

1. På datorn med Internet åtkomst öppnar du en kommando tolk som administratör och ändrar katalogen till verktygets plats. Den här platsen är en kopia av hela **ServiceConnectionTool** -mappen. Till exempel:

    `cd D:\USB\ServiceConnectionTool\`

1. Kör följande kommando för att ladda upp data filen och ladda ned Configuration Manager uppdateringarna:

    `ServiceConnectionTool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

    Fler exempel finns i [kommando rads parametrar](#bkmk_cmd).

    > [!NOTE]  
    > När du kör den här kommando raden kan du se följande fel:
    >
    > **Ohanterat undantag: system. UnauthorizedAccessException: åtkomst till sökvägen ' C:\Users\jqpublic\AppData\Local\Temp\extractmanifestcab\95F8A562.sql ' nekas.**
    >
    > Du kan ignorera det här felet på ett säkert sätt. Stäng fel fönstret om du vill fortsätta.

1. När verktyget har slutfört hämtningen av uppdateringarna kopierar du dem till tjänst anslutnings punkten.

### <a name="import"></a>Importera

1. På den dator som är värd för tjänst anslutnings punkten öppnar du en kommando tolk som administratör och ändrar katalogen till verktygs platsen. Till exempel:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Kör följande kommando för att importera uppdateringarna:

    `ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

1. När importen är klar stänger du kommando tolken. Endast uppdateringar för den aktuella hierarkin importeras.

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **uppdateringar och underhåll** . Importerade uppdateringar är nu tillgängliga för installation. Mer information finns i [Installera uppdateringar i konsolen](install-in-console-updates.md).

## <a name="log-files"></a>Loggfiler

- **ServiceConnectionTool. log**: varje gången du kör tjänst anslutnings verktyget skrivs den till logg filen. Sökvägen till logg filen är alltid samma plats som verktyget. Den här logg filen innehåller enkla uppgifter om verktygs användningen baserat på de parametrar som du använder. Varje gången du kör verktyget ersätter verktyget eventuella befintliga loggfiler.

- **ConfigMgrSetup. log**: under [anslutnings](#connect) fasen skriver verktyget till den här logg filen i roten på system enheten. Den här logg filen innehåller mer detaljerad information. Till exempel vilka filer som hämtas av verktyget och om hash-kontrollerna lyckas.

## <a name="command-line-parameters"></a><a name="bkmk_cmd"></a>Kommando rads parametrar

Det här avsnittet innehåller en lista över alla tillgängliga parametrar för tjänst anslutnings verktyget i alfabetisk ordning.

### <a name="-connect"></a>– Anslut

Använd under [anslutnings](#connect) fasen på datorn med Internet åtkomst. Den ansluter till Configuration Manager moln tjänst för att överföra data filen och hämta uppdateringar.

Den kräver följande parametrar:

- **-usagedatasrc**: platsen för data filen som ska överföras
- **-updatepackdest**: en sökväg för hämtade uppdateringar

Du kan också använda följande valfria parametrar:

- **-proxyserveruri**: FQDN för proxyservern
- **-proxyusername**: ett användar namn för proxyservern
- **-DownloadAll**: Ladda ned allt, inklusive uppdateringar och snabb korrigeringar, oavsett vilken version av webbplatsen som används.
- **-downloadhotfix**: Hämta alla snabb korrigeringar, oavsett vilken version av webbplatsen som används.
- **-downloadsiteversion**: Hämta uppdateringar och snabb korrigeringar som har en senare version än din webbplats version.

#### <a name="example-of-connect-without-a-proxy-server"></a>Exempel på anslutning utan proxyserver

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks`

#### <a name="example-of-connect-with-a-proxy-server"></a>Exempel på anslutning med en proxyserver

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itproxy.contoso.com -proxyusername jqpublic`

#### <a name="example-of-connect-to-download-only-site-version-applicable-updates"></a>Exempel på Anslut för att endast hämta uppdateringar av plats version som är tillämpliga

`ServiceConnectionTool.exe -connect -downloadsiteversion -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

### <a name="-dest"></a>-mål

En obligatorisk parameter med parametern **-export** för att ange sökväg och fil namn för den CSV-fil som ska exporteras. Mer information finns i [-export](#-export).

### <a name="-downloadall"></a>-downloadall

En valfri parameter med parametern **-Connect** för att ladda ned allt, inklusive uppdateringar och snabb korrigeringar, oavsett vilken version av webbplatsen som används. Mer information finns i [-Connect](#connect).

### <a name="-downloadhotfix"></a>-downloadhotfix

En valfri parameter med parametern **-Connect** för att bara hämta alla snabb korrigeringar, oavsett vilken version av webbplatsen som används. Mer information finns i [-Connect](#-connect).

### <a name="-downloadsiteversion"></a>-downloadsiteversion

En valfri parameter med parametern **-Connect** för att bara hämta uppdateringar och snabb korrigeringar som har en senare version än din webbplats version. Mer information finns i [-Connect](#-connect).

### <a name="-export"></a>– Exportera

Använd under [förberedelse](#prepare) fasen för att exportera användnings data till en CSV-fil. Kör den som administratör på tjänst anslutnings punkten. Med den här åtgärden kan du granska innehållet i användnings data innan du överför till Microsoft. Den kräver parametern **-mål** för att ange platsen för CSV-filen.

#### <a name="example-of-export"></a>Exempel på export

`-export -dest D:\USB\usagedata.csv`

### <a name="-import"></a>– Importera

Använd under [import](#import) fasen av tjänst anslutnings punkten för att importera uppdateringarna till platsen. Den kräver parametern **-updatepacksrc** för att ange platsen för de hämtade uppdateringarna.

#### <a name="example-of-import"></a>Exempel på import

`ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

### <a name="-prepare"></a>– Förbered

Använd under [förberedelse](#prepare) fasen av tjänst anslutnings punkten för att exportera användnings data från-platsen. Parametern **-usagedatadest** måste anges för att ange platsen för den exporterade data filen.

#### <a name="example-of-prepare"></a>Exempel på förberedelse

`ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

### <a name="-proxyserveruri"></a>– proxyserveruri

En valfri parameter med parametern **-Connect** för att ange det fullständiga domän namnet för proxyservern. Mer information finns i [-Connect](#-connect).

### <a name="-proxyusername"></a>– proxyusername

En valfri parameter med parametern **-Connect** för att ange användar namnet som ska autentiseras med proxyservern. Mer information finns i [-Connect](#-connect).

### <a name="-updatepackdest"></a>– updatepackdest

En obligatorisk parameter med parametern **-Connect** för att ange en sökväg för de hämtade uppdateringarna. Mer information finns i [-Connect](#-connect).

### <a name="-updatepacksrc"></a>– updatepacksrc

En obligatorisk parameter med parametern **-import** för att ange en sökväg till de hämtade uppdateringarna. Mer information finns i [-import](#-import).

### <a name="-usagedatadest"></a>– usagedatadest

En obligatorisk parameter med parametern **-preping** för att ange en sökväg och ett fil namn för den exporterade data filen. Mer information finns i [-förbereda](#-prepare).

## <a name="next-steps"></a>Nästa steg

[Installera uppdatering i konsolen](install-in-console-updates.md)

[Visa diagnostik- och användningsdata](../../plan-design/diagnostics/view-diagnostics-and-usage-data.md)
