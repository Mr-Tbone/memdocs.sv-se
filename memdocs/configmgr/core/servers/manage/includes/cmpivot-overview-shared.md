---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 07/13/2020
ms.openlocfilehash: 80302a1c369c36a08cc1a55e20cf339dbc8d2883
ms.sourcegitcommit: 6d987bb69d0eb9955a3003202864f58d6aaa426a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/14/2020
ms.locfileid: "86381057"
---
<!--This file is shared by the CMPivot overview articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->

## <a name="queries"></a>Frågor

Frågor kan användas för att söka efter termer, identifiera trender, analysera mönster och tillhandahålla många andra insikter baserade på dina data. CMPivot använder en delmängd av [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query) Data Flow-modellen för tabell uttrycks instruktionen. Den typiska strukturen i en tabell uttrycks instruktion är en sammansättning av klient enheter och tabell data operatörer (till exempel filter och projektioner). Sammansättningen representeras av vertikalstreck (|), vilket ger instruktionen ett vanligt formulär som visuellt representerar flödet av tabell data från vänster till höger. Varje operator accepterar en tabell data uppsättning från pipe och ytterligare indata (inklusive andra tabell data uppsättningar) från huvud delen av operatorn och genererar sedan en tabell data uppsättning till nästa operator som följer:`entity | operator1 | operator2 | ...`

I följande exempel är entiteten `CCMRecentlyUsedApplications` (en referens till de senast använda programmen) och operatorn är där (som filtrerar poster från indata enligt vissa predikat per post):

```
CCMRecentlyUsedApplications | where CompanyName like '%Microsoft%' | project CompanyName, ExplorerFileName, LastUsedTime, LaunchCount, FolderPath
```

## <a name="entities"></a>Entiteter

Entiteter är objekt som kan frågas från klienten. Vi stöder för närvarande följande entiteter:


|Entitet|Description|
|---|---|
|AadStatus|Status för Azure Active Directory|
|Administratörer|Medlemmar i den lokala administratörs gruppen|
|AppCrash|Senaste program krasch rapporter|
|AppVClientApplication|AppV-klientprogram|
|AppVClientPackage|AppV-klient paket|
|AutoStartSoftware|Program vara som startar automatiskt med, eller omedelbart efter, operativ systemet|
|BaseBoard|BaseBoard|
|Batteri|Batteri|
|BIOS|Systemets BIOS-information|
|BitLocker|BitLocker|
|BitLockerEncryptionDetails|Information om BitLocker-kryptering|
|BitLockerPolicy|BitLocker-princip|
|BootConfiguration|Start konfiguration|
|BrowserHelperObject|Webb läsar hjälp objekt|
|BrowserUsage|Webb läsar användning|
|CcmLog()|Rader inom 24 timmar (som standard) från en CCM-loggfil|
|CCMRAX|CCM_RAX|
|CCMRecentlyUsedApplications|Nyligen använda program|
|CCMWebAppInstallInfo|Webb program|
|ENHETEN|CDROM-enhet|
|ClientEvents|Klient händelser|
|Computer|Datorsystem|
|ComputerSystemEx|Dator system ex|
|ComputerSystemProduct|Dator System produkt|
|ConnectedDevice|Ansluten enhet|
|Anslutning|En aktiv TCP-anslutning in eller ut från enheten|
|Skrivbord|Skrivbord|
|DesktopMonitor|Skriv bords skärm|
|Enhet|Grundläggande information om enheten|
|Disk|Information om lokal lagrings enhet på ett dator system som kör Windows|
|DMA|DMA|
|DMAChannel|DMA-kanal|
|DriverVxD|Driv rutin-VxD|
|EmbeddedDeviceInformation|Inbäddad enhets information|
|Miljö|Miljö|
|EPStatus|Status för program mot skadlig kod på datorn|
|EventLog ()|Händelser inom 24 timmar (som standard) från en händelse logg|
|Fil ()|Information om en enskild fil|
|FileShare|Information om aktiv fil resurs|
|Inbyggd programvara|Inbyggd programvara|
|IDEController|IDE-styrenhet|
|InstalledExecutable|Installerad körbar fil|
|InstalledSoftware|Ett program som är installerat på enheten|
|Config|Hämtar nätverks konfiguration, inklusive användbara gränssnitt, IP-adresser och DNS-servrar|
|IRQTable|IRQ-tabell|
|Tangentbord|Tangentbord|
|LoadOrderGroup|Läs in beställnings grupp|
|Logisk disk|Logisk disk|
|MDMDevDetail|Enhets information|
|Minne|Minne|
|/Faxmodem|/Faxmodem|
|Kort|Kort|
|NetworkAdapter|Nätverkskort|
|NetworkAdapterConfiguration|Konfiguration av nätverkskort|
|NetworkClient|Nätverks klient|
|NetworkLoginProfile|Nätverks inloggnings profil|
|NTEventlogFile|NT EventLog-fil|
|Office365ProPlusConfigurations|Office 365 ProPlus-konfigurationer|
|OfficeAddin|Office-tillägg|
|OfficeClientMetric|Office-klientens mått|
|OfficeDeviceSummary|Sammanfattning av Office-enhet|
|OfficeDocumentMetric|Mått för Office-dokument|
|OfficeDocumentSolution|Office-dokument lösning|
|OfficeMacroError|Fel i Office-makro|
|OfficeProductInfo|Office-produkt information|
|OfficeVbaRuleViolation|Överträdelse av Office VBA-regel|
|OfficeVbaSummary|Sammanfattning av Office VBA-genomsökning|
|OperatingSystem|Operativsystem|
|OperatingSystemEx|Operativ system ex|
|OperatingSystemRecoveryConfiguration|Konfiguration av operativ system återställning|
|OptionalFeature|Valfri funktion|
|Operativsystem|Grundläggande information om operativ systemet|
|PageFileSetting|Inställning av sid fil|
|ParallelPort|Parallell port|
|Partition|Diskpartitioner|
|PCMCIAController|PCMCIA-styrenhet|
|Fysisk|Fysisk|
|PhysicalMemory|Fysiskt minne|
|PNPDEVICEDRIVER|Driv rutin för PNP-enhet|
|PointingDevice|Pekdon|
|PortableBattery|Bärbart batteri|
|Portar|Portar|
|PowerCapabilities|Energispar funktioner|
|PowerClientOptOutSettings|Undantags inställningar för energispar funktioner|
|PowerConfigurations|Energi konfiguration|
|PowerManagementDaily|Dagliga data för energispar funktioner|
|PowerManagementInsomniaReasons|Orsaker till strömförsörjnings sömnlöshet|
|PowerManagementMonthly|Månatliga data för energispar funktioner|
|PowerSettings|Energi inställningar|
|PrinterConfiguration|Skrivar konfiguration|
|PrinterDevice|Skrivar enhet|
|PrintJobs|Utskrifts jobb|
|Process|En process på ett operativ system|
|ProcessModule()|Moduler som lästs in av angivna processer|
|Processor|Processor|
|ProtectedVolumeInformation|Information om skyddad volym|
|Protokoll|Protokoll|
|QuickFixEngineering|Snabb korrigerings teknik|
|SCSIController|SCSI-styrenhet|
|SerialPortConfiguration|Konfiguration av seriell port|
|SerialPorts|Serie portar|
|ServerFeature|Serverfunktion|
|Tjänst|En tjänst på ett dator system som kör Windows|
|Tjänster|Tjänster|
|Resurser|Resurser|
|SMBConfig|SMB-konfiguration för en enhet|
|SMSAdvancedClientPorts|Configuration Manager klient portar|
|SMSAdvancedClientSSLConfigurations|Configuration Manager SSL-konfigurationer för klienter|
|SMSAdvancedClientState|Configuration Manager klient tillstånd|
|SMSDefaultBrowser|Standard webbläsare|
|SMSSoftwareTag|Program varu tagg|
|SMSWindows8Application|Windows-app|
|SMSWindows8ApplicationUserInfo|Användar information för Windows-app|
|SoftwareShortcut|Program gen väg|
|SoftwareUpdate|En program uppdatering som är tillämplig men inte installerad på enheten|
|SoundDevices|Ljud enheter|
|SWLicensingProduct|Program varu licensierings produkt|
|SWLicensingService|Software Licensing Service|
|SystemAccount|Systemkonto|
|SystemBootData|System starts data|
|SystemBootSummary|System starts Sammanfattning|
|SystemConsoleUsage|Användning av system konsol|
|SystemConsoleUser|System konsol användare|
|SystemDevices|System enheter|
|Systemdrives|System driv rutiner|
|SystemEnclosure|Systeminneslutning|
|TapeDrive|Band enhet|
|TimeZone|Tidszon|
|TPM|TPM|
|TPMStatus|TPM-status|
|TSIssuedLicense|TS-utfärdad licens|
|TSLicenseKeyPack|Nyckel paket för TS-licens|
|UninterruptiblePowerSupply|Avbrotts fri ström källa|
|USBController|USB-styrenhet|
|USBDevice|USB-enhet|
|Användare|Ett användar konto med en aktiv anslutning till enheten|
|USMFolderRedirectionHealth|Hälso tillstånd för mappomdirigering|
|USMUserProfile|Hälsa för användar profil|
|VideoController|Video styrenhet|
|VirtualMachine|Virtuell dator|
|VirtualMachine64|Virtuell dator (64)|
|Volym|Volym|
|WindowsUpdate|Windows Update|
|WindowsUpdateAgentVersion|Windows Update Agent version|
|WinEvent ()|Händelser inom 24 timmar (som standard) från en händelse logg i Windows|
|WriteFilterState|Skriv filter status|

## <a name="table-operators"></a>Tabell operatörer

Tabell operatörer kan använda filter, sammanfatta och transformera data strömmar. För närvarande stöds följande operatorer:

|Tabell operatörer|Description|
|---|---|
|count|Returnerar en tabell med en enda post som innehåller antalet poster|
|distinct|Skapar en tabell med en distinkt kombination av de angivna kolumnerna i indata-tabellen|
|join|Sammanfoga raderna i två tabeller för att skapa en ny tabell genom att matcha raden för samma enhet|
|Sortera efter|Sortera raderna i indatalistnen i ordning efter en eller flera kolumner|
|projekt|Markera de kolumner som du vill inkludera, byta namn på eller släppa och infoga nya beräknade kolumner|
|sammanfatta|Skapar en tabell som sammanställer innehållet i Indataporten|
|take|Returnera upp till det angivna antalet rader|
|top|Returnerar de första N posterna sorterade efter de angivna kolumnerna|
|var|Filtrerar en tabell till delmängd av rader som uppfyller ett predikat|

## <a name="scalar-operators"></a>Skalära operatorer

I följande tabell sammanfattas operatörer:

|Operatorer|Beskrivning|Exempel
|---|---|---|
|==|Lika med|`1 == 1, 'aBc' == 'AbC'`|
|!=|Inte lika med|`1 != 2, 'abc' != 'abcd'`|
|< |Minskad|`1 < 2, 'abc' < 'DEF'`|
|> |Störst|`2 > 1, 'xyz' > 'XYZ'`|
|<=|Mindre än eller lika med|`1 <= 2, 'abc' <= 'abc'`|
|>=|Större än eller lika med|`2 >= 1, 'abc' >= 'ABC'`|
|+|Lägg till|`2 + 1, now() + 1d`|
|-|Subtrahera|`2 - 1, now() - 1h`|
|*|Multiplicera|`2 * 2`|
|/|Dividera|`2 / 1`|
|%|Modulo|`2 % 1`|
|likadan|Vänster sida (LHS) innehåller en matchning för höger sida (RHS)|`'abc' like '%B%'`|
|! like|LHS innehåller ingen matchning för RHS|`'abc' !like '_d_'`|
|contains|RHS inträffar som en under serie av LHS|`'abc' contains 'b'`|
|! innehåller|RHS inträffar inte i LHS|`'team' !contains 'i'`|
|StartsWith|RHS är en inledande delsekvens av LHS|`'team' startswith 'tea'`|
|! StartsWith|RHS är inte en inledande delsekvens av LHS|`'abc' !startswith 'bc'`|
|EndsWith|RHS är en avslutande delsekvens av LHS|`'abc' endswith 'bc'`|
|! EndsWith|RHS är inte en avslutande delsekvens av LHS|`'abc' !endswith 'a'`|
|och|Sant om och endast om RHS och LHS är sanna|`(1 == 1) and (2 == 2)`|
|eller|Sant om och endast om RHS eller LHS är sant|`(1 == 1) or (1 == 2)`|

## <a name="aggregation-functions"></a>Aggregeringsfunktioner

Agg regerings funktioner kan användas med operatorn sammanfatta tabell till beräknade sammanfattade värden. För närvarande stöds följande agg regerings funktioner:

|Funktion|Beskrivning|
|---|---|
|avg()|Returnerar medelvärdet för värdena i gruppen|
|count()|Returnerar ett antal poster per sammanfattnings grupp|
|countif()|Returnerar ett antal rader för vilka predikatet utvärderas till true|
|dcount()|Returnerar antalet distinkta värden i gruppen|
|max()|Returnerar det maximala värdet över gruppen|
|min()|Returnerar det minsta värdet över gruppen|
|percentil ()|Returnerar en uppskattning för den angivna percentilen från närmaste rang för populationen som definieras av expr|
|sum()|Returnerar summan av värdena i gruppen|
|sumif()|Returnerar en summa av uttryck för vilka predikatet utvärderas till true|

## <a name="scalar-functions"></a>Skalärfunktioner

Skalära funktioner kan användas i uttryck. För närvarande stöds följande skalära funktioner:

|Funktion|Beskrivning|
|---|---|
|ago()|Subtraherar angivet TimeSpan från aktuell tid för UTC-klockan|
|bin()|Avrundar värden nedåt till ett antal datetime-multiplar av en specifik lager plats storlek|
|case()|Utvärderar en lista med predikat och returnerar det första resultat uttryck vars predikat är uppfyllt|
|datetime_add()|Beräknar ett nytt datetime-värde från en angiven DatumDel multiplicerat med en angiven mängd, tillagt i angivet datetime|
|datetime_diff()|Beräknar skillnaden mellan två datum/tid-värden|
|iif()|Utvärderar det första argumentet och returnerar värdet för antingen det andra eller tredje argumentet beroende på om predikatet utvärderas till sant (sekund) eller falskt (tredje)|
|indexof()|Funktionen rapporterar det nollbaserade indexet för den första förekomsten av en angiven sträng i Indatasträngen|
|isnotnull()|Utvärderar dess enda argument och returnerar ett booleskt värde som anger om argumentet utvärderas till ett värde som inte är null|
|isnull()|Utvärderar dess enda argument och returnerar ett booleskt värde som anger om argumentet utvärderas till ett null-värde|
|now()|Returnerar aktuell UTC-Klock tid|
|strcat()|Sammanfogar mellan 1 och 64 argument|
|strlen()|Returnerar längden, i tecken, för Indatasträngen|
|substring()|Extraherar en under sträng från en käll sträng som börjar från ett index till slutet av strängen|
|tostring()|Konverterar inmatad till en sträng representation|

## <a name="additional-entities-operators-and-functions-for-cmpivot-from-configuration-manager"></a><a name="bkmk_onprem_only"></a>Ytterligare entiteter, operatorer och funktioner för CMPivot från Configuration Manager

> [!Important]
> Dessa objekt stöds inte när du kör CMPivot från Microsoft Endpoint Manager administrations Center.

|Typ|Objekt|Beskrivning|
|--|--|---|
|Entitet|AccountSID|Konto-SID|
|Entitet|FileContent()|Innehåll i en enskild fil|
|Entitet|NAPClient|NAP-klient|
|Entitet|NAPSystemHealthAgent|Hälso agent för NAP-system|
|Entitet|Register ()|Alla värden för en enskild register nyckel<!--7371183-->|
|Tabell operator|återge|Återger resultat som grafiska utdata|
