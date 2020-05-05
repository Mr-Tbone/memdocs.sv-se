---
title: Logginsamlaren
titleSuffix: Configuration Manager
description: Använd loggar insamlings verktyget för att felsöka Desktop Analytics
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c101e45eb794ff73599e9612a5aec991be01ae6c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718884"
---
# <a name="desktop-analytics-log-collector"></a>Logg insamlare för Skriv bords analys

Från och med Configuration Manager version 1906 använder du verktyget **DesktopAnalyticsLogsCollector. ps1** från installations katalogen Configuration Manager för att felsöka problem med enhets registrering för Station ära datorer. Den kör vissa grundläggande fel söknings steg och samlar in relevanta loggar i en enda arbets katalog. Du kan dela det här innehållet med Microsoft support.


## <a name="prerequisites"></a>Krav

- En stationär Analytics-klient som kör Windows 10, Windows 8,1 eller Windows 7 med Service Pack 1

- Kör skriptet på enheten som en administrativ användare och **Kör som administratör**.

    > [!Tip]
    > Du kan använda funktionen Configuration Manager **skript** med det här verktyget. Mer information finns i [exempel 5: Distribuera skript via Configuration Manager **skript**](#bkmk_ex5).

- För Windows 7 med Service Pack 1, PowerShell version 4,0 eller senare
    - [.NET Framework version 4,6 eller senare](https://dotnet.microsoft.com/download/dotnet-framework)

    - Windows Management Framework [version 4,0](https://support.microsoft.com/help/2819745) (aka.MS/wmf4download) eller [version 5,1](https://www.microsoft.com/download/details.aspx?id=54616) (aka.MS/wmf5download)

## <a name="usage"></a>Användning

Hämta skriptet från installations innehållet för Configuration Manager:`SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>Parametrar

### `-LogPath`

Anger en lokal sökväg eller UNC-sökväg för att lagra loggen och andra utdatafiler.

**Värden**:

- Lokal sökväg (maximal längd = 130), till exempel:`c:\myfolder`

- UNC-sökväg (maximal längd = 130), till exempel:`\\myserver\myfolder`

**Typ**: sträng

**Position**: 1

**Standardvärde**: `$Env:SystemDrive\M365AnalyticsLogs` (när den här parametern är null, tom eller blank steg skapar skriptet mappen M365AnalyticsLogs under systemen het.)

### `-LogMode`

Anger utförlig nivå för loggarna.

**Värden**:

- `0`: Endast kommando fönstret Logga skript meddelanden till PowerShell-kommando.

- `1`: Logga skript meddelanden till både logg filen under mappen utdata och PowerShell-kommando.

- `2`: Logga skript meddelanden till logg filen under mappen utdata.

**Typ**: Int16

**Position**: 2

**Standardvärde**: `1` (logga skript meddelanden till både logg filen och PowerShell-Kommandotolken.)

### `-CollectNetTrace`

Anger om skriptet samlar in nätverks spårningen.

**Värden**:

- `0`: Aktivera inte nätverks spårningen.

- `1`(ett heltal som inte är noll): Aktivera nätverks spårning och samla in resultat.

**Typ**: Int16

**Position**: 3

**Standardvärde**: `0` (Aktivera inte nätverks spårning)

### `-CollectUTCTrace`

Anger om skriptet samlar in Windows UTC-spårning och kör anslutnings diagnos.

**Värden**:

- `0`: Aktivera inte UTC-spårning eller kör anslutnings diagnos.

- `1`(ett heltal som inte är noll): Aktivera UTC-spårning, köra anslutnings diagnos och samla in resultat.

**Typ**: Int16

**Position**: 4

**Standardvärde**: `0` (Aktivera inte UTC-spårning eller diagnostik för att köra anslutning)


## <a name="output"></a>Utdata

Skriptet skapar en *arbetsmapp* under den angivna sökvägen. Till exempel **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**. Alla utdatafiler placeras i den här arbetsmappen.

Om du aktiverar skriptet att skriva till en *loggfil*genereras ett i arbetsmappen. Till exempel **M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss. txt**.

Skriptet genererar också andra *diagnostiska filer* i arbetsmappen. Ett exempel:

- `installedKBs.txt`: en lista över Windows-uppdateringar som är installerade på enheten
- `appcompat`: data för programkompatibilitet
- `Reg*.txt`: en serie filer med exporterade data från Windows-registret


## <a name="examples"></a>Exempel

### <a name="example-1-run-script-via-powershell-command-window-with-default-values"></a><a name="bkmk_ex1"></a>Exempel 1: kör skript via PowerShell kommando fönstret med standardvärden

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="example-2-run-script-via-powershell-command-window-with-specified-parameters"></a><a name="bkmk_ex2"></a>Exempel 2: kör skript via PowerShell-kommando fönstret med angivna parametrar

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="example-3-run-script-via-powershell-command-window-with-specified-parameters-in-position"></a><a name="bkmk_ex3"></a>Exempel 3: kör skript via PowerShell-kommando fönstret med angivna parametrar i position

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="example-4-run-script-via-powershell-command-window-with-specified-parameter-and-verbose-messages"></a><a name="bkmk_ex4"></a>Exempel 4: kör skript via PowerShell-kommando fönstret med den angivna parametern och utförliga meddelanden

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="example-5-deploy-script-via-configuration-manager-scripts"></a><a name="bkmk_ex5"></a>Exempel 5: Distribuera skript via Configuration Manager **skript**

Mer information finns i [skapa och köra PowerShell-skript från Configuration Manager-konsolen](../apps/deploy-use/create-deploy-scripts.md).

DesktopAnalyticsLogsCollector. ps1 har signerats digitalt av Microsoft. Du kan behöva lägga till dess Microsoft kod signerings certifikat som en betrodd utgivare på mål enheten.

1. Öppna egenskaperna för skriptet i Utforskaren i Windows. Växla till fliken **digitala signaturer** och välj **information**.

2. På fliken **Allmänt** väljer du **Visa certifikat**.

    > [!Note]
    > Om du vill distribuera certifikatet via andra metoder måste du först exportera certifikatet till en fil. Gå till fliken **information** och välj **Kopiera till fil**.

3. Välj **Installera certifikat**. Importera certifikatet och placera det i arkivet **Betrodda utgivare** .


## <a name="see-also"></a>Se även

- [Felsöka Desktop Analytics](troubleshooting.md)

- [Skapa och kör PowerShell-skript från Configuration Manager-konsolen](../apps/deploy-use/create-deploy-scripts.md)
