---
title: Om loggfiler
titleSuffix: Configuration Manager
description: Använd loggfiler för att felsöka problem med Configuration Manager-klienter och-plats system.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b1751e3c-a60c-4ab7-a943-2595df1eb612
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d6be23adc7ac082545bffeef59ed52d3455d9931
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720305"
---
# <a name="about-log-files-in-configuration-manager"></a>Om loggfiler i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I Configuration Manager registrerar klient-och plats Server komponenter process information i individuella loggfiler. Du kan använda informationen i dessa loggfiler för att felsöka problem som kan uppstå. Som standard aktiverar Configuration Manager loggning för klient-och Server komponenter.

Den här artikeln innehåller allmän information om Configuration Manager loggfiler. Den innehåller verktyg som du kan använda, hur du konfigurerar loggarna och var du hittar dem. Mer information om vissa loggfiler finns i [logg filens referens](log-files.md).


## <a name="how-it-works"></a><a name="BKMK_AboutLogs"></a>Så här fungerar det

De flesta processer i Configuration Manager Skriv drifts information till en loggfil som är dedikerad för den processen. Loggfilerna identifieras av **. log** eller **. LO_** fil namns tillägg. Configuration Manager skriver till en. log-fil tills loggen når sin maximala storlek. När loggen är full kopieras. log-filen till en fil med samma namn men med fil namns tillägget. lo_ och processen eller komponenten fortsätter att skriva till. log-filen. När. log-filen når maximal storlek, skrivs filen. lo_ över och processen upprepas. Vissa komponenter upprättar en logg fils historik genom att lägga till en datum-och tidsstämpel till logg filens namn och genom att behålla fil namns tillägget. log.


## <a name="log-viewer-tools"></a><a name="bkmk_tools"></a>Verktyg för logg visning

Alla Configuration Manager loggfiler är oformaterad text så att du kan visa dem med valfri text läsare som anteckningar. Loggarna använder unik formatering som visas bäst med något av följande specialiserade verktyg:

- [CMTrace](#cmtrace)
- [OneTrace](#onetrace)
- [Logg visaren för Support Center](#support-center-log-viewer)

### <a name="cmtrace"></a>CMTrace

Om du vill visa loggarna använder du Configuration Manager logg visnings verktyget **CMTrace**. Den finns i `\SMSSetup\Tools` mappen för Configuration Manager-käll mediet. Verktyget CMTrace läggs till i alla start avbildningar som läggs till i program varu biblioteket. CMTrace logga visnings verktyg installeras automatiskt tillsammans med Configuration Manager-klienten.<!--1357971--> Mer information finns i [CMTrace](../../support/cmtrace.md).

### <a name="onetrace"></a>OneTrace

Från och med version 1906 är **OneTrace** ett nytt logg visnings program med Support Center. Det fungerar ungefär som CMTrace, med förbättringar. Mer information finns i [Support Center OneTrace](../../support/support-center-onetrace.md).

### <a name="support-center-log-viewer"></a>Logg visaren för Support Center

**Support Center** innehåller ett modernt logg visnings program. Det här verktyget ersätter CMTrace och ger ett anpassningsbart gränssnitt med stöd för flikar och docknings bara fönster. Det har ett snabb presentations lager och kan läsa in stora loggfiler på några sekunder. Mer information finns i [logg visnings referens för Support Center](../../support/support-center-ui-reference.md#bkmk_log-viewer).

> [!Note]  
> Support Center och OneTrace använder Windows Presentation Foundation (WPF). Den här komponenten är inte tillgänglig i Windows PE. Fortsätt att använda CMTrace i Start avbildningar med aktivitetssekvensdistribution.


## <a name="configure-logging-options"></a><a name="bkmk_logoptions"></a>Konfigurera loggnings alternativ

Du kan ändra konfigurationen för loggfilerna, till exempel utförlig nivå, storlek och historik. Det finns flera sätt att ändra dessa inställningar:

- [Under klient installationen](#bkmk_logoptions-clientprop)
- [Använda Configuration Manager Service Manager](#bkmk_logoptions-sm)
- [Använda Windows-registret](#bkmk_logoptions-registry)
- [I Configuration Manager-konsolen](#bkmk_logoptions-console)

### <a name="configure-logging-options-during-client-installation"></a><a name="bkmk_logoptions-clientprop"></a>Konfigurera loggnings alternativ under klient installationen

Du kan ange konfigurationen för klient logg filen under installationen. Använd följande egenskaper:

- CCMENABLELOGGING
- CCMDEBUGLOGGING
- CCMLOGLEVEL
- CCMLOGMAXHISTORY
- CCMLOGMAXSIZE

Mer information finns i [Egenskaper för klient installation](../../clients/deploy/about-client-installation-properties.md#clientMsiProps).

### <a name="configure-logging-options-by-using-configuration-manager-service-manager"></a><a name="bkmk_logoptions-sm"></a>Konfigurera loggnings alternativ genom att använda Configuration Manager Service Manager

Du kan ändra var Configuration Manager lagrar loggfilerna och deras storlek.  

Ändra storleken på loggfilerna genom att ändra namnet och platsen för logg filen eller för att tvinga flera komponenter att skriva till en enda loggfil. gör så här:  

#### <a name="modify-logging-for-a-component"></a>Ändra loggning för en komponent  

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **system status**och väljer sedan noden **plats status** eller **komponent status** .  

2. Välj **Start**i menyfliksområdet och välj sedan **Configuration Manager Service Manager**.  

3. När Configuration Manager Service Manager öppnas ansluter du till den plats som du vill hantera. Om den plats som du vill hantera inte visas väljer du **plats**, väljer **Anslut**och anger sedan namnet på plats servern för rätt plats.  

4. Expandera platsen och gå till **komponenter** eller **servrar**, beroende på var de komponenter som du vill hantera finns.  

5. Välj en eller flera komponenter i den högra rutan.  

6. På **komponent** -menyn väljer du **loggning**.  

7. I dialogrutan **Komponentloggning för Configuration Manager** anger du de tillgängliga konfigurationsalternativen för dina val.  

8. Välj **OK** för att spara konfigurationen.  

### <a name="configure-logging-options-by-using-the-windows-registry"></a><a name="bkmk_logoptions-registry"></a>Konfigurera loggnings alternativ med hjälp av Windows-registret

<!-- SCCMDocs#992 -->
Använd Windows-registret på servrarna eller klienterna för att ändra följande loggnings alternativ:

- Utförlig nivå
- Maximal historik
- Maximal storlek

När du felsöker ett problem kan du Aktivera utförlig loggning för Configuration Manager att skriva ytterligare information i loggfilerna.

> [!Warning]
> Felaktig konfiguration av de här inställningarna kan orsaka Configuration Manager att logga stora mängder information eller ingen alls. Även om dessa data kan vara bra för fel sökning kan du vara försiktig när du ändrar dessa värden på produktions platser. Testa alltid dessa ändringar i en labb miljö först. Överdriven loggning kan inträffa, vilket kan göra det svårt att hitta relevant information i loggfilerna.

När du har gjort ändringar i register inställningarna startar du om komponenten:

- Om du ändrar klient inställningarna startar du om tjänsten **SMS agent Host** (ccmexec).
- Om du ändrar Server inställningarna startar du om **SMS Executive** tjänsten.

Register inställningarna varierar beroende på komponenten:

- [Klient-och hanterings plats](#bkmk_reg-client)
- [Platsserver](#bkmk_reg-site)
- [Platssystemroll](#bkmk_reg-role)
- [Configuration Manager-konsol](#bkmk_reg-console)

#### <a name="client-and-management-point-logging-options"></a><a name="bkmk_reg-client"></a>Loggnings alternativ för klient-och hanterings platser

Om du vill konfigurera loggnings alternativ för alla komponenter på en klient-eller hanterings plats system konfigurerar du dessa **REG_DWORD** värden under följande Windows-register nyckel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\@Global`

|Name  |Värden  |Beskrivning  |
|---------|---------|---------|
|Loggnivå|`0`: Utförlig<br>`1`: Standard<br>`2`: Varningar och fel<br>`3`: Endast fel|Den detalj nivå som ska skrivas till loggfilerna.|
|LogMaxHistory|Ett heltal som är större än eller lika med noll, till exempel:<br>`0`: Ingen historik<br>`1`: Standard|När en loggfil når den maximala storleken, byter klienten namn på den som en säkerhets kopia och skapar en ny loggfil. Ange hur många tidigare versioner som ska behållas.|
|LogMaxSize|Ett heltal som är större än eller lika med 10 000, till exempel:<br>250000|Den maximala logg fils storleken i byte. När en logg växer till den angivna storleken byter klienten namn på den som en historik fil och skapar en ny fil. Standardvärdet är 250 000 byte.|

> [!Note]  
> Ändra inte andra värden som kan finnas i den här register nyckeln.

För avancerad fel sökning kan du också lägga till detta **REG_SZ** -värde under följande Windows-register nyckel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Logging\DebugLogging`

|Name  |Värden  |Beskrivning  |
|---------|---------|---------|
|Enabled | `True`: Aktivera fel söknings loggar<br>`False`: inaktivera fel söknings loggar |Aktiverar fel söknings loggning i fel söknings syfte.|

Den här inställningen gör att klienten loggar information på låg nivå för fel sökning. Undvik att använda den här inställningen på produktions platser. Överdriven loggning kan inträffa, vilket kan göra det svårt att hitta relevant information i loggfilerna. Se till att inaktivera den här inställningen när du har löst problemet.

#### <a name="site-server-logging-options"></a><a name="bkmk_reg-site"></a>Loggnings alternativ för plats Server

Du kan konfigurera inställningar globalt eller för en enskild komponent på Configuration Manager plats Server.

Konfigurera de här värdena under följande Windows-register nyckel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing`

|Name  |Värden  |Typ  |Beskrivning
|---------|---------|---------|---------|
|SqlEnabled| `1`: Aktivera SQL-spårning<br> `0`: inaktivera SQL-spårning |REG_DWORD|Lägg till SQL trace-loggning till alla plats Server loggar.|
|ArchiveEnabled| `1`: Aktivera logg Arkiv<br> `0`: inaktivera logg Arkiv | REG_DWORD |Arkivera plats Server loggar på en annan plats för historisk bevarande.|
|ArchivePath| En giltig mappsökväg, till exempel`C:\Logs\Archive` | REG_SZ |Sökvägen för att arkivera plats Server loggar.|

Aktivera endast SQL-spårning i fel söknings syfte. Undvik att använda den på produktions platser. Överdriven loggning kan inträffa, vilket kan göra det svårt att hitta relevant information i loggfilerna. Se till att inaktivera den här inställningen när du har löst problemet.

> [!Note]  
> Ändra inte andra värden som kan finnas i den här register nyckeln.

Konfigurera loggnings alternativ för en enskild server komponent genom att konfigurera dessa **REG_DWORD** värden under följande Windows-register nyckel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\Tracing\<ComponentName>`

|Name  |Värden  |Beskrivning  |
|---------|---------|---------|
|LoggingLevel|`0`: Utförlig<br>`1`: Standard<br>`2`: Varningar och fel<br>`3`: Endast fel|Den detalj nivå som ska skrivas till loggfilerna.|
|LogMaxHistory|Ett heltal som är större än eller lika med noll, till exempel:<br>`0`: Ingen historik<br>`1`: Standard|När en loggfil når den maximala storleken, byter servern namn på den som en säkerhets kopia och skapar en ny loggfil. Ange hur många tidigare versioner som ska behållas.|
|MaxFileSize|Ett heltal som är större än eller lika med 10 000, till exempel:<br>250000|Den maximala logg fils storleken i byte. När en logg växer till den angivna storleken byter klienten namn på den som en historik fil och skapar en ny fil. Standardvärdet är 250 000 byte.|
|DebugLogging| `1`: Aktivera fel söknings loggar<br>`0`: inaktivera fel söknings loggar |Aktiverar fel söknings loggning i fel söknings syfte.|

Inställningen DebugLogging gör att servern loggar information på låg nivå för fel sökning. Undvik att använda den här inställningen på produktions platser. Överdriven loggning kan inträffa, vilket kan göra det svårt att hitta relevant information i loggfilerna. Se till att inaktivera den här inställningen när du har löst problemet.

> [!Note]  
> Ändra inte andra värden som kan finnas i den här register nyckeln.

#### <a name="site-system-role-logging-options"></a><a name="bkmk_reg-role"></a>Loggnings alternativ för plats system roll

Du kan konfigurera inställningar globalt eller för en enskild komponent på ett plats system som är värd för en Configuration Manager Server roll.

Konfigurera loggnings alternativ för en enskild server komponent genom att konfigurera dessa **REG_DWORD** värden under följande Windows-register nyckel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\<ComponentName>\Logging`

Till exempel för distributions plats rollen:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP\Logging`

|Name  |Värden  |Beskrivning  |
|---------|---------|---------|
|Loggnivå|`0`: Utförlig<br>`1`: Standard<br>`2`: Varningar och fel<br>`3`: Endast fel|Den detalj nivå som ska skrivas till loggfilerna.|
|LogMaxHistory|Ett heltal som är större än eller lika med noll, till exempel:<br>`0`: Ingen historik<br>`1`: Standard|När en loggfil når den maximala storleken, byter servern namn på den som en säkerhets kopia och skapar en ny loggfil. Ange hur många tidigare versioner som ska behållas.|
|LogMaxSize|Ett heltal som är större än eller lika med 10 000, till exempel:<br>250000|Den maximala logg fils storleken i byte. När en logg växer till den angivna storleken, byter servern namn på den som en historik fil och skapar en ny fil. Standardvärdet är 250 000 byte.|

> [!Note]  
> Ändra inte andra värden som kan finnas i den här register nyckeln.

#### <a name="configuration-manager-console-logging-options"></a><a name="bkmk_reg-console"></a>Configuration Manager konsol loggnings alternativ

Använd följande procedur för att ändra utförlig nivå för AdminUI. log för Configuration Manager-konsolen:

1. Öppna konsol konfigurations filen **Microsoft. ConfigurationManagement. exe. config**i en XML-redigerare som anteckningar. Standard konfigurations filen finns på följande plats:`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

1. Under elementet **system. Diagnostics** > **sources** > **SOURCES** , ändrar du attributet **switchValue** från `Error` till `Verbose`. Ett exempel:

    Original: `<source name="SmsAdminUISnapIn" switchValue="Error">` nytt:`<source name="SmsAdminUISnapIn" switchValue="Verbose" >`

1. Spara filen och starta om konsolen.

### <a name="configure-logging-options-in-the-configuration-manager-console"></a><a name="bkmk_logoptions-console"></a>Konfigurera loggnings alternativ i Configuration Manager-konsolen

<!-- 4433455 -->

Från och med version 1910, aktivera eller inaktivera utförlig loggning på en klient eller samling från-konsolen:

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen, välj noden **enheter** och välj en målenhet.

1. I menyfliksområdet på fliken **Start** i gruppen **enhet** väljer du **client Diagnostics**. Välj en av de tillgängliga åtgärderna.

Mer information finns i [client Diagnostics](../../clients/manage/client-notification.md#client-diagnostics).

## <a name="locating-log-files"></a><a name="BKMK_LogLocation"></a>Söker efter loggfiler

Configuration Manager och beroende komponenter lagrar loggfiler på olika platser. Dessa platser är beroende av processen som skapar logg filen och konfigurationen av din miljö.

Följande platser är standardvärdena. Om du har anpassat installations katalogerna i din miljö kan de faktiska Sök vägarna variera.

- Klientsession`C:\Windows\CCM\logs`
- Servernamn`C:\Program Files\Microsoft Configuration Manager\Logs`
- Hanterings plats:`C:\SMS_CCM\Logs`
- Configuration Manager-konsol:`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog`
- IIS`C:\inetpub\logs\logfiles\w3svc1`

### <a name="task-sequence-log-locations"></a>Platser för aktivitetssekvens

Platsen för logg filen **Smsts. log** i aktivitetssekvensen varierar beroende på fasen i aktivitetssekvensen:

- I Windows PE före [Formatera och partitionera disk](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) steg: `X:\Windows\temp\smstslog\smsts.log` (X är Windows PE RAM-enhet)
- I steget Windows PE efter **format och disk partition** : `X:\smstslog\smsts.log`, kopieras sedan till `C:\_SMSTaskSequence\Logs\smstslog\smsts.log` när enheten är klar
- I det nya Windows-operativsystemet innan klienten installeras:`C:\_SMSTaskSequence\Logs\smstslog\smsts.log`
- I Windows efter att klienten har installerats:`C:\Windows\CCM\Logs\smstslog\smsts.log`
- I Windows när aktivitetssekvensen har slutförts:`C:\Windows\CCM\Logs\smsts.log`

> [!Tip]  
> Variabeln skrivskyddad aktivitetssekvens [_SMSTSLogPath](../../../osd/understand/task-sequence-variables.md#SMSTSLogPath) innehåller alltid sökvägen till den aktuella logg filen.


## <a name="see-also"></a>Se även

- [Referens för loggfiler](log-files.md)

- [Support Center OneTrace](../../support/support-center-onetrace.md)

- [Logg fils visnings program för Support Center](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
