---
title: Variabelreferens för aktivitetssekvens
titleSuffix: Configuration Manager
description: Lär dig mer om variablerna för att styra och anpassa en Configuration Manager aktivitetssekvens.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: reference
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 667d7451f467592bd0645b54d7068a20628ec98e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124149"
---
# <a name="task-sequence-variables"></a>Aktivitetssekvensvariabler

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln är en referens för alla tillgängliga variabler i alfabetisk ordning. Använd webbläsaren **Sök** funktion (vanligt vis **CTRL**  +  **F**) för att hitta en speciell variabel. Variabeln noterar om den är specifik för särskilda steg. Artikeln om [stegen i aktivitetssekvensen](task-sequence-steps.md) innehåller en lista över variabler som är speciella för varje steg.

Mer information finns i [använda variabler för aktivitetssekvens](using-task-sequence-variables.md).

## <a name="task-sequence-variable-reference"></a><a name="bkmk_tsvar"></a>Variabel referens för aktivitetssekvens

### <a name="_osddetectedwindir"></a><a name="OSDDetectedWinDir"></a>_OSDDetectedWinDir

Aktivitetssekvensen söker igenom datorns hård diskar efter en tidigare installation av operativ systemet när Windows PE startar. Mappen Windows lagras i den här variabeln. Du kan konfigurera aktivitetssekvensen så att den hämtar värdet från miljön och använda det för att ange samma plats för Windows-mappen för den nya installationen av operativsystemet.

### <a name="_osddetectedwindrive"></a><a name="OSDDetectedWinDrive"></a>_OSDDetectedWinDrive

Aktivitetssekvensen söker igenom datorns hård diskar efter en tidigare installation av operativ systemet när Windows PE startar. Platsen på hårddisken där operativsystemet är installerat lagras i den här variabeln. Du kan konfigurera aktivitetssekvensen för att hämta det här värdet från miljön och använda det för att ange samma plats på hårddisken för att använda det nya operativsystemet.

### <a name="_osdmigrateusmtpackageid"></a><a name="OSDMigrateUsmtPackageID"></a>_OSDMigrateUsmtPackageID

*Gäller steget [avbilda användar tillstånd](task-sequence-steps.md#BKMK_CaptureUserState) .*

(indata)

Anger paket-ID: t för det Configuration Manager-paket som innehåller USMT-filerna. Den här variabeln är obligatorisk.

### <a name="_osdmigrateusmtrestorepackageid"></a><a name="OSDMigrateUsmtRestorePackageID"></a>_OSDMigrateUsmtRestorePackageID

*Gäller steget [Återställ användar tillstånd](task-sequence-steps.md#BKMK_RestoreUserState) .*

(indata)

Anger paket-ID: t för det Configuration Manager-paket som innehåller USMT-filerna. Den här variabeln är obligatorisk.

### <a name="_smstsadvertid"></a><a name="SMSTSAdvertID"></a>_SMSTSAdvertID

Lagrar det unika ID:t för den aktuella aktivitetssekvensdistributionen som körs. Samma format används som Configuration Manager distributions-ID för program distribution. Om aktivitetssekvensen körs via fristående media anges inte den här variabeln.

#### <a name="example"></a>Exempel

`ABC20001`

### <a name="_smstsassettag"></a><a name="SMSTSAssetTag"></a>_SMSTSAssetTag

*Gäller steget [Ställ in dynamiska variabler](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Anger datorns tillgångstagg.

### <a name="_smstsbootimageid"></a><a name="SMSTSBootImageID"></a>_SMSTSBootImageID

Om den aktuella aktiva aktivitetssekvensen refererar till ett start avbildnings paket lagrar den här variabeln start avbildningens paket-ID. Om aktivitetssekvensen inte refererar till ett start avbildnings paket anges inte den här variabeln.

#### <a name="example"></a>Exempel

`ABC00001`  

### <a name="_smstsbootuefi"></a><a name="SMSTSBootUEFI"></a>_SMSTSBootUEFI

Aktivitetssekvensen anger den här variabeln när den identifierar en dator som är i UEFI-läge.

### <a name="_smstsclientcache"></a><a name="SMSTSClientCache"></a>_SMSTSClientCache

<!-- SCCMDocs issue 1400 -->
Aktivitetssekvensen anger den här variabeln när innehållet i cacheminnet på den lokala enheten cachelagras. Variabeln innehåller sökvägen till cachen. Om den här variabeln inte finns finns det inget cacheminne.

### <a name="_smstsclientguid"></a><a name="SMSTSClientGUID"></a>_SMSTSClientGUID

Lagrar värdet för Configuration Manager klient-GUID. Om aktivitetssekvensen körs från fristående media anges inte den här variabeln.

#### <a name="example"></a>Exempel

`0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`

### <a name="_smstscurrentactionname"></a><a name="SMSTSCurrentActionName"></a>_SMSTSCurrentActionName

Anger namnet på det sekvenssteg som körs. Den här variabeln anges innan aktivitetssekvenshanteraren kör varje enskilt steg.

#### <a name="example"></a>Exempel

`run command line`

### <a name="_smstsdefaultgateways"></a><a name="SMSTSDefaultGateways"></a>_SMSTSDefaultGateways

*Gäller steget [Ställ in dynamiska variabler](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Anger standardgateways som används av datorn.

### <a name="_smstsdownloadondemand"></a><a name="SMSTSDownloadOnDemand"></a>_SMSTSDownloadOnDemand

Om den aktuella aktivitetssekvensen körs i läget Hämta på begäran är den här variabeln `true` . Ladda ned-i-demand-läge innebär att Task Sequence Manager laddar ned innehåll lokalt endast när det måste ha åtkomst till innehållet.

### <a name="_smstsinwinpe"></a><a name="SMSTSInWinPE"></a>_SMSTSInWinPE

När det aktuella steget i aktivitetssekvensen körs i Windows PE är den här variabeln `true` . Testa den här aktivitetssekvensen för att fastställa den aktuella operativ system miljön.

### <a name="_smstsipaddresses"></a><a name="SMSTSIPAddresses"></a>_SMSTSIPAddresses

*Gäller steget [Ställ in dynamiska variabler](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Anger de IP-adresser som används av datorn.

### <a name="_smstslastactionname"></a><a name="SMSTSLastActionName"></a>_SMSTSLastActionName

Lagrar namnet på den senaste åtgärden som kördes. Den här variabeln relaterar till **_SMSTSLastActionRetCode**. Aktivitetssekvensen loggar dessa värden till filen Smsts. log. Den här variabeln är fördelaktig när en aktivitetssekvens felsöks. Om ett steg Miss lyckas kan ett anpassat skript inkludera steg namnet tillsammans med retur koden.

### <a name="_smstslastactionretcode"></a><a name="SMSTSLastActionRetCode"></a>_SMSTSLastActionRetCode

Lagrar retur koden från den senaste åtgärden som kördes. Den här variabeln kan användas som ett villkor för att avgöra om nästa steg ska köras.

#### <a name="example"></a>Exempel

`0`

### <a name="_smstslastactionsucceeded"></a><a name="SMSTSLastActionSucceeded"></a>_SMSTSLastActionSucceeded

- Om det sista steget lyckades är den här variabeln `true` .  

- Om det sista steget misslyckades, är det `false` .  

- Om aktivitetssekvensen hoppade över den senaste åtgärden, eftersom steget har inaktiverats eller det associerade villkoret utvärderas till **false**återställs inte den här variabeln. Den innehåller fortfarande värdet för föregående åtgärd.  

### <a name="_smstslastcontentdownloadlocation"></a><a name="SMSTSLastContentDownloadLocation"></a>_SMSTSLastContentDownloadLocation

<!-- 2840337 -->
Från och med version 1906 innehåller den här variabeln den sista platsen där aktivitetssekvensen hämtades eller försökte hämta innehåll. Kontrol lera den här variabeln i stället för att parsa klient loggarna för den här innehålls platsen.

### <a name="_smstslaunchmode"></a><a name="SMSTSLaunchMode"></a>_SMSTSLaunchMode

Anger att aktivitetssekvensen har startats via någon av följande metoder:  

- **SMS**: Configuration Manager-klienten, t. ex. När en användare startar den från Software Center
- **USB-minne**: äldre USB-media
- **USB-minne och format**: nyare USB-media
- **CD**: en startbar CD
- **DVD**: en startbar DVD
- **PXE**: nätverks start med PXE
- **HD**: förinstallerade media på en hård disk

### <a name="_smstslogpath"></a><a name="SMSTSLogPath"></a>_SMSTSLogPath

Lagrar den fullständiga sökvägen till loggkatalogen. Använd det här värdet för att avgöra var stegen i aktivitetssekvensen ska loggas. Värdet anges inte när en hård disk inte är tillgänglig.

### <a name="_smstsmacaddresses"></a><a name="SMSTSMacAddresses"></a>_SMSTSMacAddresses

*Gäller steget [Ställ in dynamiska variabler](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Anger de MAC-adresser som används av datorn.

### <a name="_smstsmachinename"></a><a name="SMSTSMachineName"></a>_SMSTSMachineName

Lagrar och anger datornamnet. Lagrar namnet på datorn som aktivitetssekvensen använder för att logga alla status meddelanden. Om du vill ändra dator namnet i det nya operativ systemet använder du variabeln [OSDComputerName](#OSDComputerName-input) .

### <a name="_smstsmake"></a><a name="SMSTSMake"></a>_SMSTSMake

*Gäller steget [Ställ in dynamiska variabler](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Anger datorns märke.

### <a name="_smstsmdatapath"></a><a name="SMSTSMDataPath"></a>_SMSTSMDataPath

Anger den sökväg som definieras av [SMSTSLocalDataDrive](#SMSTSLocalDataDrive) -variabeln. Den här sökvägen anger var aktivitetssekvensen lagrar temporära cachefiler på mål datorn när den körs. När du definierar SMSTSLocalDataDrive innan aktivitetssekvensen startar, t. ex. genom att ange en samlings variabel, definierar Configuration Manager _SMSTSMDataPath variabeln när aktivitetssekvensen startar.

### <a name="_smstsmediatype"></a><a name="SMSTSMediaType"></a>_SMSTSMediaType

Anger vilken typ av media som används för att initiera installationen. Exempel på typer av media är startmedia, fullständiga media, PXE och förberedda media.

### <a name="_smstsmodel"></a><a name="SMSTSModel"></a>_SMSTSModel

*Gäller steget [Ställ in dynamiska variabler](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Anger datorns modell.

### <a name="_smstsmp"></a><a name="SMSTSMP"></a>_SMSTSMP

Lagrar URL-adressen eller IP-adressen för en Configuration Manager hanterings plats.

### <a name="_smstsmpport"></a><a name="SMSTSMPPort"></a>_SMSTSMPPort

Lagrar port numret för en Configuration Manager hanterings plats.

### <a name="_smstsorgname"></a><a name="SMSTSOrgName"></a>_SMSTSOrgName

Lagrar namnet på anpassnings titeln som aktivitetssekvensen visas i dialog rutan förlopp.

### <a name="_smstsosupgradeactionreturncode"></a><a name="SMSTSOSUpgradeActionReturnCode"></a>_SMSTSOSUpgradeActionReturnCode

*Gäller steget [Uppgradera operativ system](task-sequence-steps.md#BKMK_UpgradeOS) .*

Lagrar det slutkod som Installationsprogrammet för Windows returnerar för att indikera lyckade eller misslyckade. Den här variabeln är användbar med `/Compat` kommando rads alternativet.

#### <a name="example"></a>Exempel

När du har slutfört en sökning efter en kompatibilitet, vidta åtgärder i senare steg, beroende på den misslyckade eller slut för ande avslutnings koden. Starta uppgraderingen om den lyckas. Eller ange en markör i miljön som ska samlas in med maskin varu inventering. Du kan till exempel lägga till en fil eller ange en register nyckel. Använd den här markören för att skapa en samling datorer som är redo att uppgraderas eller som kräver åtgärd före uppgraderingen.

### <a name="_smstspackageid"></a><a name="SMSTSPackageID"></a>_SMSTSPackageID

Lagrar aktuellt aktivitetssekvens-ID som körs. Detta ID använder samma format som Configuration Manager-paket-ID.

#### <a name="example"></a>Exempel

`HJT00001`

### <a name="_smstspackagename"></a><a name="SMSTSPackageName"></a>_SMSTSPackageName

Lagrar det aktuella namnet på aktivitetssekvensen som körs. En Configuration Manager administratör anger det här namnet när du skapar aktivitetssekvensen.

#### <a name="example"></a>Exempel

`Deploy Windows 10 task sequence`

### <a name="_smstsrunfromdp"></a><a name="SMSTSRunFromDP"></a>_SMSTSRunFromDP

Ange till `true` om den aktuella aktivitetssekvensen körs i läget Kör-från-distribution-punkt. Det här läget innebär att aktivitetssekvensen hämtar nödvändiga paket resurser från distributions platsen.

### <a name="_smstsserialnumber"></a><a name="SMSTSSerialNumber"></a>_SMSTSSerialNumber

*Gäller steget [Ställ in dynamiska variabler](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Anger datorns serienummer.

### <a name="_smstssetuprollback"></a><a name="SMSTSSetupRollback"></a>_SMSTSSetupRollback

Anger om Installationsprogrammet för Windows utförde en återställnings åtgärd under en uppgradering på plats. De variabla värdena kan vara `true` eller `false` .

### <a name="_smstssitecode"></a><a name="SMSTSSiteCode"></a>_SMSTSSiteCode

Lagrar plats koden för den Configuration Manager webbplatsen.

#### <a name="example"></a>Exempel

`ABC`

### <a name="_smststimezone"></a><a name="SMSTSTimezone"></a>_SMSTSTimezone

Den här variabeln lagrar tids zons informationen i följande format:

`Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName`

#### <a name="example"></a>Exempel

För tids zonens **Eastern-tid (USA och Kanada)**:

`300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time`

### <a name="_smststype"></a><a name="SMSTSType"></a>_SMSTSType

Anger vilken typ av aktivitetssekvens som körs. Det kan ha ett av följande värden:  

- **1**: en allmän aktivitetssekvens
- **2**: aktivitetssekvens för operativ system distribution

### <a name="_smstsusecrl"></a><a name="SMSTSUseCRL"></a>_SMSTSUseCRL

När aktivitetssekvensen använder HTTPS för att kommunicera med hanterings platsen anger den här variabeln om den använder listan över återkallade certifikat (CRL).

### <a name="_smstsuserstarted"></a><a name="SMSTSUserStarted"></a>_SMSTSUserStarted

Anger om en användare startade aktivitetssekvensen. Den här variabeln anges endast om aktivitetssekvensen startas från Software Center. Om [_SMSTSLaunchMode](#SMSTSLaunchMode) exempelvis är inställt på `SMS` .

Den här variabeln kan ha följande värden:  

- `true`: Anger att aktivitetssekvensen startas manuellt av en användare från Software Center.  

- `false`: Anger att aktivitetssekvensen initieras automatiskt av Configuration Manager Scheduler.

### <a name="_smstsusessl"></a><a name="SMSTSUseSSL"></a>_SMSTSUseSSL

Anger om aktivitetssekvensen använder SSL för att kommunicera med Configuration Manager hanterings platsen. Om du konfigurerar dina plats system för HTTPS anges värdet till `true` .

### <a name="_smstsuuid"></a><a name="SMSTSUUID"></a>_SMSTSUUID

*Gäller steget [Ställ in dynamiska variabler](task-sequence-steps.md#BKMK_SetDynamicVariables) .*

Anger datorns UUID.

### <a name="_smstswtg"></a><a name="SMSTSWTG"></a>_SMSTSWTG

Anger om datorn körs som en Windows To Go-enhet.

### <a name="_ts_crmemory"></a><a name="TSCRMEMORY"></a>_TS_CRMEMORY

*Från och med version 2002* <!--6005561-->  
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för om kontroll av **minsta minne (MB)** returnerade sant ( `1` ) eller falskt ( `0` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_ts_crspeed"></a><a name="TSCRSPEED"></a>_TS_CRSPEED

*Från och med version 2002* <!--6005561-->  
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för huruvida kontroll av **lägsta processorhastighet (MHz)** returnerade sant ( `1` ) eller falskt ( `0` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_ts_crdisk"></a><a name="TSCRDISK"></a>_TS_CRDISK

*Från och med version 2002* <!--6005561-->  
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för om kontroll av **minsta ledigt disk utrymme (MB)** returnerade sant ( `1` ) eller falskt ( `0` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_ts_crostype"></a><a name="TSCROSTYPE"></a>_TS_CROSTYPE

*Från och med version 2002* <!--6005561-->  
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för om det **aktuella operativ systemet som ska uppdateras är** kontrollen returnerade sant ( `1` ) eller falskt ( `0` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_ts_crarch"></a><a name="TSCRARCH"></a>_TS_CRARCH

*Från och med version 2002* <!--6005561-->  
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för om **arkitekturen för aktuell OS** -kontroll returnerade true ( `1` ) eller false ( `0` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_ts_crminosver"></a><a name="TSCRMINOSVER"></a>_TS_CRMINOSVER

*Från och med version 2002* <!--6005561-->  
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för om den **lägsta versions kontrollen för operativ systemet** returnerade true ( `1` ) eller false ( `0` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_ts_crmaxosver"></a><a name="TSCRMAXOSVER"></a>_TS_CRMAXOSVER

*Från och med version 2002* <!--6005561-->  
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för om den **högsta versions kontrollen för operativ systemet** returnerar true ( `1` ) eller false ( `0` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_ts_crclientminver"></a><a name="TSCRCLIENTMINVER"></a>_TS_CRCLIENTMINVER

*Från och med version 2002* <!--6005561-->  
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för om den **lägsta klient versions** kontrollen returnerade true ( `1` ) eller false ( `0` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_ts_croslanguage"></a><a name="TSCROSLANGUAGE"></a>_TS_CROSLANGUAGE

*Från och med version 2002* <!--6005561-->  
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för om **språket för den aktuella OS** -kontrollen returnerade true ( `1` ) eller false ( `0` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_ts_cracpower"></a><a name="TSCRACPOWER"></a>_TS_CRACPOWER

*Från och med version 2002* <!--6005561-->  
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för om den **nätström** som är ansluten check returnerade true ( `1` ) eller false ( `0` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_ts_crnetwork"></a><a name="TSCRNETWORK"></a>_TS_CRNETWORK

*Från och med version 2002* <!--6005561-->  
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för om kontrollen nätverkskort **anslutet** returnerade true ( `1` ) eller false ( `0` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_ts_cruefi"></a><a name="TSCRUEFI"></a>_TS_CRUEFI

*Från och med version 2006* <!--6452769-->
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för om **datorn är i UEFI-läge** som returnerar BIOS ( `0` ) eller UEFI ( `1` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_ts_crwired"></a><a name="TSCRWIRED"></a>_TS_CRWIRED

*Från och med version 2002* <!--6005561-->  
*Gäller för steget [kontrol lera beredskap](task-sequence-steps.md#BKMK_CheckReadiness) .*

En skrivskyddad variabel för om **nätverkskortet inte är trådlös** kontroll returnerade värdet true ( `1` ) eller false ( `0` ). Om du inte aktiverar kontrollen är värdet för den här skrivskyddade variabeln tomt.

### <a name="_tsappinstallstatus"></a><a name="TSAppInstallStatus"></a>_TSAppInstallStatus

Aktivitetssekvensen anger den här variabeln med installations status för programmet under steget [installera program](task-sequence-steps.md#BKMK_InstallApplication) . Den anger något av följande värden:  

- **Odefinierad**: steget installera program körs inte.  

- **Fel**: minst ett program misslyckades på grund av ett fel under steget installera program.  

- **Varning**: inga fel inträffade under steget installera program. Ett eller flera program, eller ett nödvändigt beroende, installerades inte på grund av att ett krav inte uppfylldes.  

- **Lyckades**: inga fel eller varningar upptäcktes under steget installera program.  

### <a name="_tssecureboot"></a><a name="TSSecureBoot"></a>_TSSecureBoot

*Från och med version 2002* <!--5842295-->  

Använd den här variabeln för att fastställa statusen för säker start på en UEFI-aktiverad enhet. Variabeln kan ha ett av följande värden:

- `NA`: Det associerade registervärdet finns inte, vilket innebär att enheten inte stöder säker start.
- `Enabled`: Enheten har säker start aktiverat.
- `Disabled`: Enheten har säker start inaktiverat.

### <a name="osdadapter"></a><a name="OSDAdapter"></a>OSDAdapter

*Gäller för steget [tillämpa nätverks inställningar](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(indata)

Variabeln aktivitetssekvens är en *mat ris* variabel. Varje element i matrisen representerar inställningarna för ett enskilt nätverkskort på datorn. Få åtkomst till inställningarna för varje nätverkskort genom att kombinera mat ris variabelns namn med det nollbaserade nätverkskort indexet och egenskaps namnet.

Om steget tillämpa nätverks inställningar konfigurerar flera nätverkskort definierar det egenskaperna för det *andra* nätverkskortet med hjälp av index **1** i variabel namnet. Till exempel: OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList och OSDAdapter1DNSDomain.

Använd följande variabel namn för att definiera egenskaperna för det *första* nätverkskortet för steget att konfigurera:

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP

Denna inställning är obligatorisk. Möjliga värden är `True` eller `False`. Till exempel:

`true`: Aktivera Dynamic Host Configuration Protocol (DHCP) för kortet

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList

Kommaavgränsad lista med IP-adresser för nätverkskortet. Den här egenskapen ignoreras om inte **EnableDHCP** har angetts till `false` . Denna inställning är obligatorisk.

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask

Kommaavgränsad lista med nätmasker. Den här egenskapen ignoreras om inte **EnableDHCP** har angetts till `false` . Denna inställning är obligatorisk.

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways

Kommaavgränsad lista över IP-gateway-adresser. Den här egenskapen ignoreras om inte **EnableDHCP** har angetts till `false` . Denna inställning är obligatorisk.

#### <a name="osdadapter0dnsdomain"></a>OSDAdapter0DNSDomain

Domain Name System DNS-domän (DNS) för kortet.

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList

Kommaavgränsad lista över DNS-servrar för kortet. Denna inställning är obligatorisk.

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration

Ange att `true` IP-adressen för kortet ska registreras i DNS.

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration

Ange till `true` att registrera IP-adressen för kortet i DNS under det fullständiga DNS-namnet för datorn.

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering

Ange till `true` för att aktivera filtrering av IP-protokoll på kortet.

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList

Kommaavgränsad lista över protokoll som tillåts att köra över IP. Den här egenskapen ignoreras om **EnableIPProtocolFiltering** har värdet `false` .

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering

Ange till för `true` att aktivera TCP-port filtrering för nätverkskortet.

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList

Kommaavgränsad lista över portar som ska beviljas åtkomst behörighet för TCP. Den här egenskapen ignoreras om **EnableTCPFiltering** har värdet `false` .

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions

Alternativ för NetBIOS över TCP/IP. Möjliga värden är:  

- `0`: Använd NetBIOS-inställningar från DHCP-servern  
- `1`: Aktivera NetBIOS över TCP/IP  
- `2`: Inaktivera NetBIOS över TCP/IP  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS

Ange till `true` att använda WINS för namn matchning.

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList

Kommaavgränsad lista med IP-adresser för WINS-server. Den här egenskapen ignoreras om inte **EnableWINS** har angetts till `true` .

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress

MAC-adress som används för att matcha inställningar med det fysiska nätverkskortet.

#### <a name="osdadapter0name"></a>OSDAdapter0Name

Namnet på nätverks anslutningen som det visas i programmet för nätverks anslutningar på kontroll panelen. Namnet är mellan 0 och 255 tecken långt.

#### <a name="osdadapter0index"></a>OSDAdapter0Index

Index för nätverkskort inställningarna i matrisen med inställningar.

#### <a name="example"></a>Exempel

- **Värdet OSDAdapterCount** = `1`  
- **OSDAdapter0EnableDHCP** = `FALSE`  
- **OSDAdapter0IPAddressList** = `192.168.0.40`  
- **OSDAdapter0SubnetMask** = `255.255.255.0`  
- **OSDAdapter0Gateways** = `192.168.0.1`  
- **OSDAdapter0DNSSuffix** = `contoso.com`  

### <a name="osdadaptercount"></a><a name="OSDAdapterCount"></a>Värdet OSDAdapterCount

*Gäller för steget [tillämpa nätverks inställningar](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(indata)

Anger antalet installerade nätverkskort på måldatorn. När du ställer in värdet **värdet OSDAdapterCount** anger du även alla konfigurations alternativ för varje kort.

Om du till exempel ställer in värdet **OSDAdapter0TCPIPNetbiosOptions** för det första nätverkskortet måste du konfigurera alla värden för det kortet.

Om du inte anger det här värdet ignorerar aktivitetssekvensen alla **OSDAdapter** -värden.

### <a name="osdapplydriverbootcriticalcontentuniqueid"></a><a name="OSDApplyDriverBootCriticalContentUniqueID"></a>OSDApplyDriverBootCriticalContentUniqueID

*Gäller steget [Använd driv rutins paket](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(indata)

Anger innehålls-ID:t för drivrutinen för masslagringsenheter som ska installeras från drivrutinspaketet. Om den här variabeln inte anges installeras ingen driv rutin för Mass lagring.

### <a name="osdapplydriverbootcriticalhardwarecomponent"></a><a name="OSDApplyDriverBootCriticalHardwareComponent"></a>OSDApplyDriverBootCriticalHardwareComponent

*Gäller steget [Använd driv rutins paket](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(indata)

Anger om en driv rutin för Mass lagrings enhet är installerad, den här variabeln måste vara **SCSI**.

Om [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) har angetts krävs den här variabeln.

### <a name="osdapplydriverbootcriticalid"></a><a name="OSDApplyDriverBootCriticalID"></a>OSDApplyDriverBootCriticalID

*Gäller steget [Använd driv rutins paket](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(indata)

Anger det startkritiska ID:t för drivrutinen för masslagringsenheter som ska installeras. Detta ID anges i **SCSI-** avsnittet i enhets driv Rutinens Txtsetup. OEM-fil.

Om [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) har angetts krävs den här variabeln.

### <a name="osdapplydriverbootcriticalinffile"></a><a name="OSDApplyDriverBootCriticalINFFile"></a>OSDApplyDriverBootCriticalINFFile

*Gäller steget [Använd driv rutins paket](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(indata)

Anger INF-filen för drivrutinen för masslagringsenheter som ska installeras.

Om [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) har angetts krävs den här variabeln.

### <a name="osdautoapplydriverbestmatch"></a><a name="OSDAutoApplyDriverBestMatch"></a>OSDAutoApplyDriverBestMatch

*Gäller för steget [Använd driv rutiner automatiskt](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

(indata)

Om det finns flera enhets driv rutiner i driv rutins katalogen som är kompatibla med en maskin varu enhet avgör den här variabeln stegets åtgärd.

#### <a name="valid-values"></a>Giltiga värden

- `true`(standard): installera bara den bästa enhets driv rutinen  

- `false`: Installerar alla kompatibla enhets driv rutiner och Windows väljer den bästa driv rutinen som ska användas  

### <a name="osdautoapplydrivercategorylist"></a><a name="OSDAutoApplyDriverCategoryList"></a>OSDAutoApplyDriverCategoryList

*Gäller för steget [Använd driv rutiner automatiskt](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

(indata)

En kommaavgränsad lista över unika ID:n för kategorier i drivrutinskatalogen. Med steget **Använd driv rutin automatiskt** beaktas driv rutinerna i minst en av de angivna kategorierna. Det här värdet är valfritt och anges inte som standard. Hämta tillgängliga kategori-ID: n genom att räkna upp listan med **SMS_CategoryInstance** objekt på webbplatsen.

### <a name="osdbitlockerrebootcount"></a><a name="OSDBitLockerRebootCount"></a>OSDBitLockerRebootCount

*Gäller för steget [inaktivera BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker) .*

<!-- 4512937 -->
Från och med version 1906 använder du den här variabeln för att ange hur många omstarter du vill återuppta skyddet för.

#### <a name="valid-values"></a>Giltiga värden

Ett heltal från `1` till `15` .

### <a name="osdbitlockerrebootcountoverride"></a><a name="OSDBitLockerRebootCountOverride"></a>OSDBitLockerRebootCountOverride

*Gäller för steget [inaktivera BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker) .*

<!-- 4512937 -->
Från och med version 1906 anger du det här värdet för att åsidosätta antalet som anges i steget eller [OSDBitLockerRebootCount](#OSDBitLockerRebootCount) -variabeln. De andra metoderna accepterar bara värdena 1 till 15, om du anger den här variabeln till 0, förblir BitLocker inaktive rad under obestämd tid. Den här variabeln är användbar när aktivitetssekvensen anger ett värde, men du vill ange ett separat värde för per enhet eller per samling.

#### <a name="valid-values"></a>Giltiga värden

Ett heltal från `0` till `15` .

### <a name="osdbitlockerrecoverypassword"></a><a name="OSDBitLockerRecoveryPassword"></a>OSDBitLockerRecoveryPassword

*Gäller för steget [Aktivera BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker) .*

(indata)

I stället för att skapa ett slumpmässigt återställnings lösen ord använder steget **Aktivera BitLocker** det angivna värdet som återställnings lösen ord. Värdet måste vara ett giltigt numeriskt BitLocker-återställningslösenord.

### <a name="osdbitlockerstartupkey"></a><a name="OSDBitLockerStartupKey"></a>OSDBitLockerStartupKey

*Gäller för steget [Aktivera BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker) .*

(indata)

I stället för att skapa en slumpmässig start nyckel för nyckel hanterings alternativet **Start nyckel på endast USB,** använder **BitLocker** -steget Trusted Platform Module (TPM) som start nyckel. Värdet måste vara en giltig, 256-bitars Base64-kodad BitLocker-startnyckel.

### <a name="osdcaptureaccount"></a><a name="OSDCaptureAccount"></a>OSDCaptureAccount

*Gäller för steget [avbilda operativ system avbildning](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(indata)

Anger ett Windows-kontonamn som har behörighet att lagra avbildningen på en nätverks resurs ([OSDCaptureDestination](#OSDCaptureDestination)). Ange även [aktivitetssekvensvariabeln OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

Mer information om avbildnings kontot för avbildnings operativ system finns i [konton](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account).

### <a name="osdcaptureaccountpassword"></a><a name="OSDCaptureAccountPassword"></a>Aktivitetssekvensvariabeln OSDCaptureAccountPassword

*Gäller för steget [avbilda operativ system avbildning](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(indata)

Anger lösen ordet för Windows-kontot ([OSDCaptureAccount](#OSDCaptureAccount)) som används för att lagra den insamlade avbildningen på en nätverks resurs ([OSDCaptureDestination](#OSDCaptureDestination)).

### <a name="osdcapturedestination"></a><a name="OSDCaptureDestination"></a>OSDCaptureDestination

*Gäller för steget [avbilda operativ system avbildning](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(indata)

Anger den plats där aktivitetssekvensen sparar den fångade OS-avbildningen. Katalognamnet får innehålla högst 255 tecken. Om nätverks resursen kräver autentisering anger du variablerna [OSDCaptureAccount](#OSDCaptureAccount) och [aktivitetssekvensvariabeln OSDCaptureAccountPassword](#OSDCaptureAccountPassword) .

### <a name="osdcomputername-input"></a><a name="OSDComputerName-input"></a>OSDComputerName (Indatatyp)

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Anger namnet på måldatorn.

#### <a name="example"></a>Exempel

`%_SMSTSMachineName%`objekt

### <a name="osdcomputername-output"></a><a name="OSDComputerName-output"></a>OSDComputerName (utdata)

*Gäller för steget [avbilda Windows-inställningar](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

Ange datorns NetBIOS-namn. Värdet anges bara om variabeln [OSDMigrateComputerName](#OSDMigrateComputerName) har värdet `true` .

### <a name="osdconfigfilename"></a><a name="OSDConfigFileName"></a>OSDConfigFileName

*Gäller för steget [Använd operativ Systems avbildning](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) .*

(indata)

Anger fil namnet för distributions svars filen för operativ systemet som är kopplad till avbildnings paketet för operativ system distribution.  

### <a name="osddataimageindex"></a><a name="OSDDataImageIndex"></a>OSDDataImageIndex

*Gäller för steget [Använd data avbildning](task-sequence-steps.md#BKMK_ApplyDataImage) .*

(indata)

Anger indexvärdet för den avbildning som används på mål datorn.

### <a name="osddiskindex"></a><a name="OSDDiskIndex"></a>OSDDiskIndex

*Gäller för [disk steget formatera och partition](task-sequence-steps.md#BKMK_FormatandPartitionDisk) .*

(indata)

Anger numret på den fysiska disk som ska partitioneras.

### <a name="osddnsdomain"></a><a name="OSDDNSDomain"></a>OSDDNSDomain

*Gäller för steget [tillämpa nätverks inställningar](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(indata)

Anger den primära DNS-server som mål datorn använder.

### <a name="osddnssuffixsearchorder"></a><a name="OSDDNSSuffixSearchOrder"></a>OSDDNSSuffixSearchOrder

*Gäller för steget [tillämpa nätverks inställningar](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(indata)

Anger DNS-sökordningen för måldatorn.

### <a name="osddomainname"></a><a name="OSDDomainName"></a>OSDDomainName

*Gäller för steget [tillämpa nätverks inställningar](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(indata)

Anger namnet på den Active Directory domän som mål datorn ansluter till. Det angivna värdet måste vara ett giltigt Active Directory Domain Services-domännamn.

### <a name="osddomainouname"></a><a name="OSDDomainOUName"></a>OSDDomainOUName

*Gäller för steget [tillämpa nätverks inställningar](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(indata)

Anger RFC 1779-formatnamnet för organisationsenheten (OU) som måldatorn ansluter till. Om värdet anges måste det innehålla den fullständiga sökvägen.

#### <a name="example"></a>Exempel

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`

### <a name="osddonotlogcommand"></a><a name="OSDDoNotLogCommand"></a>OSDDoNotLogCommand

<!--1358493-->
*Gäller steget [installera paket](task-sequence-steps.md#BKMK_InstallPackage) .*

*Från och med version 1902*  
*Gäller för steget [Kör kommando rad](task-sequence-steps.md#BKMK_RunCommandLine) .*

(indata)

Ange variabeln till om du vill förhindra att potentiellt känsliga data visas eller loggas `TRUE` . Den här variabeln maskerar program namnet i steget **Smsts. log** under ett **installations paket** .

Från och med version 1902 `TRUE` döljer den också kommando raden från steget **Kör kommando rad** i logg filen.<!--3654172-->

### <a name="osdenabletcpipfiltering"></a><a name="OSDEnableTCPIPFiltering"></a>OSDEnableTCPIPFiltering

*Gäller för steget [tillämpa nätverks inställningar](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(indata)

Anger om TCP/IP-filtrering är aktiverat.

#### <a name="valid-values"></a>Giltiga värden

- `true`  
- `false`objekt  

### <a name="osdgptbootdisk"></a><a name="OSDGPTBootDisk"></a>OSDGPTBootDisk

*Gäller för [disk steget formatera och partition](task-sequence-steps.md#BKMK_FormatandPartitionDisk) .*

(indata)

Anger om en EFI-partition ska skapas på en GPT-hårddisk. EFI-baserade datorer använder den här partitionen som start disk.

#### <a name="valid-values"></a>Giltiga värden

- `true`  
- `false`objekt

### <a name="osdimagecreator"></a><a name="OSDImageCreator"></a>OSDImageCreator

*Gäller för steget [avbilda operativ system avbildning](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(indata)

Ett valfritt namn för användaren som skapade avbildningen. Det här namnet lagras i WIM-filen. Användarnamnet får innehålla högst 255 tecken.

### <a name="osdimagedescription"></a><a name="OSDImageDescription"></a>OSDImageDescription

*Gäller för steget [avbilda operativ system avbildning](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(indata)

En valfri användardefinierad Beskrivning av den fångade OS-avbildningen. Den här beskrivningen lagras i WIM-filen. Beskrivningen får innehålla högst 255 tecken.

### <a name="osdimageindex"></a><a name="OSDImageIndex"></a>OSDImageIndex

*Gäller för steget [Använd operativ Systems avbildning](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) .*

(indata)

Anger bild indexets värde för WIM-filen som tillämpas på mål datorn.

### <a name="osdimageversion"></a><a name="OSDImageVersion"></a>OSDImageVersion

*Gäller för steget [avbilda operativ system avbildning](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

(indata)

Ett valfritt användardefinierat versions nummer som ska tilldelas avbildningen av den insamlade operativ systemet. Versionsnumret lagras i WIM-filen. Det här värdet kan vara en valfri kombination av alfanumeriska tecken med en maximal längd på 32.

### <a name="osdinstalldriversadditionaloptions"></a><a name="OSDInstallDriversAdditionalOptions"></a>OSDInstallDriversAdditionalOptions

<!--516679/2840016-->
*Gäller steget [Använd driv rutins paket](task-sequence-steps.md#BKMK_ApplyDriverPackage) .*

(indata)

Anger ytterligare alternativ som ska läggas till i DISM-kommandoraden vid tillämpning av ett driv rutins paket. Aktivitetssekvensen verifierar inte kommando rads alternativen.

Om du vill använda den här variabeln aktiverar du inställningen **Installera driv rutins paket genom att köra DISM med alternativet rekursivt**i steget **Använd driv rutins paket** .

Mer information finns i [kommando rads alternativ för Windows 10 DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).

### <a name="osdjoinaccount"></a><a name="OSDJoinAccount"></a>OSDJoinAccount

*Gäller för följande steg:*  

- [Använd nätverksinställningar](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Anslut till domän eller arbetsgrupp](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(indata)

Anger det domän användar konto som används för att lägga till mål datorn i domänen. Den här variabeln är obligatorisk vid anslutning till en domän.

Mer information om konto för aktivitetssekvens domän anslutning finns i [konton](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

### <a name="osdjoindomainname"></a><a name="OSDJoinDomainName"></a>OSDJoinDomainName

*Gäller för steget [Anslut till domän eller arbets grupp](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(indata)

Anger namnet på en Active Directory domän som mål datorn ansluter till. Domän namnets längd måste vara mellan 1 och 255 tecken.

### <a name="osdjoindomainouname"></a><a name="OSDJoinDomainOUName"></a>OSDJoinDomainOUName

*Gäller för steget [Anslut till domän eller arbets grupp](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(indata)

Anger RFC 1779-formatnamnet för organisationsenheten (OU) som måldatorn ansluter till. Om värdet anges måste det innehålla den fullständiga sökvägen. Längden på ORGANISATIONSENHETens namn måste vara mellan 0 och 32 767 tecken. Värdet anges inte om variabeln [osdjointype tilldelas värdet](#OSDJoinType) har angetts till `1` (Anslut till arbets grupp).

#### <a name="example"></a>Exempel

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

### <a name="osdjoinpassword"></a><a name="OSDJoinPassword"></a>OSDJoinPassword

*Gäller för följande steg:*  

- [Använd nätverksinställningar](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Anslut till domän eller arbetsgrupp](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(indata)

Anger lösen ordet för den [OSDJoinAccount](#OSDJoinAccount) som mål datorn använder för att ansluta till Active Directorys domänen. Om den här variabeln inte innehåller den här variabeln försöker Installationsprogrammet för Windows ett tomt lösen ord. Om variabeln [osdjointype tilldelas värdet](#OSDJoinType) -variabeln har angetts till `0` (Anslut till domän), krävs det här värdet.

### <a name="osdjoinskipreboot"></a><a name="OSDJoinSkipReboot"></a>OSDJoinSkipReboot

*Gäller för steget [Anslut till domän eller arbets grupp](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(indata)

Anger om du vill hoppa över omstarten när måldatorn har anslutit till domänen eller arbetsgruppen.

#### <a name="valid-values"></a>Giltiga värden

- `true`  
- `false`  

### <a name="osdjointype"></a><a name="OSDJoinType"></a>Osdjointype tilldelas värdet

*Gäller för steget [Anslut till domän eller arbets grupp](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(indata)

Anger om måldatorn ansluter till en Windows-domän eller arbetsgrupp.

#### <a name="valid-values"></a>Giltiga värden

- `0`: Ansluta mål datorn till en Windows-domän  
- `1`: Ansluta mål datorn till en arbets grupp  

### <a name="osdjoinworkgroupname"></a><a name="OSDJoinWorkgroupName"></a>OSDJoinWorkgroupName

*Gäller för steget [Anslut till domän eller arbets grupp](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) .*

(indata)

Anger namnet på en arbetsgrupp som måldatorn ansluter till. Längden på arbetsgruppens namn måste vara mellan 1 och 32 tecken.

### <a name="osdkeepactivation"></a><a name="OSDKeepActivation"></a>OSDKeepActivation

*Gäller för steget [Förbered Windows för avbildning](task-sequence-steps.md#BKMK_PrepareWindowsforCapture) .*

(indata)

Anger om Sysprep behåller eller återställer produkt aktiverings flaggan.

#### <a name="valid-values"></a>Giltiga värden

- `true`: Behåll aktiverings flaggan
- `false`(standard): Återställ aktiverings flaggan

### <a name="osdlocaladminpassword"></a><a name="OSDLocalAdminPassword"></a>OSDLocalAdminPassword

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(indata)

Anger lösen ordet för det lokala administratörs kontot. Om du aktiverar alternativet att **slumpmässigt generera det lokala administratörs lösen ordet och inaktivera kontot för alla plattformar som stöds**, ignorerar steget den här variabeln. Det angivna värdet måste vara mellan 1 och 255 tecken.

### <a name="osdlogpowershellparameters"></a><a name="OSDLogPowerShellParameters"></a>OSDLogPowerShellParameters

<!--3556028-->
*Från och med version 1902*  
*Gäller skript steget [kör PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript) .*

(indata)

För att förhindra att potentiellt känsliga data loggas loggar inte steget **kör PowerShell-skript** skript parametrar i filen **Smsts. log** . Ange den här variabeln till **Sant**om du vill inkludera skript parametrarna i aktivitetssekvensen.

### <a name="osdmigrateadaptersettings"></a><a name="OSDMigrateAdapterSettings"></a>OSDMigrateAdapterSettings

*Gäller för steget [avbilda nätverks inställningar](task-sequence-steps.md#BKMK_CaptureNetworkSettings) .*

(indata)

Anger om aktivitetssekvensen fångar information om nätverkskortet. Den här informationen omfattar konfigurations inställningar för TCP/IP, DNS och WINS.

#### <a name="valid-values"></a>Giltiga värden

- `true`objekt
- `false`

### <a name="osdmigrateadditionalcaptureoptions"></a><a name="OSDMigrateAdditionalCaptureOptions"></a>Aktivitetssekvensvariabeln OSDMigrateAdditionalCaptureOptions

*Gäller steget [avbilda användar tillstånd](task-sequence-steps.md#BKMK_CaptureUserState) .*

(indata)

Ange ytterligare kommando rads alternativ för USMT-verktyget (User State Migration Tool) som aktivitetssekvensen använder för att avbilda användar tillstånd. Steget visar inte inställningarna i redigeraren för aktivitetssekvens. Ange de här alternativen som en sträng, som aktivitetssekvensen lägger till i den automatiskt genererade USMT-kommandoraden för ScanState.

De USMT-alternativ som anges med denna aktivitetssekvens är inte validerade för noggrannhet innan aktivitetssekvensen körs.

Mer information om tillgängliga alternativ finns i [ScanState syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax).

### <a name="osdmigrateadditionalrestoreoptions"></a><a name="OSDMigrateAdditionalRestoreOptions"></a>Aktivitetssekvensvariabeln OSDMigrateAdditionalRestoreOptions

*Gäller steget [Återställ användar tillstånd](task-sequence-steps.md#BKMK_RestoreUserState) .*

(indata)

Anger ytterligare kommando rads alternativ för USMT-verktyget (User State Migration Tool) som aktivitetssekvensen använder vid återställning av användar tillstånd. Ange ytterligare alternativ som en sträng, som aktivitetssekvensen lägger till i den automatiskt genererade USMT-kommandoraden för LoadState.

De USMT-alternativ som anges med denna aktivitetssekvens är inte validerade för noggrannhet innan aktivitetssekvensen körs.

Mer information om tillgängliga alternativ finns i [LoadState syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).

### <a name="osdmigratecomputername"></a><a name="OSDMigrateComputerName"></a>OSDMigrateComputerName

*Gäller för steget [avbilda Windows-inställningar](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

(indata)

Anger om datornamnet migrerats.

#### <a name="valid-values"></a>Giltiga värden

- `true`(standard). [OSDComputerName (output)](#OSDComputerName-output) -variabeln anges till datorns NetBIOS-namn.  
- `false`  

### <a name="osdmigrateconfigfiles"></a><a name="OSDMigrateConfigFiles"></a>OSDMigrateConfigFiles

*Gäller steget [avbilda användar tillstånd](task-sequence-steps.md#BKMK_CaptureUserState) .*

(indata)

Anger konfigurationsfilerna som används för att kontrollera avbildningen av användarprofiler. Den här variabeln används bara om [OSDMigrateMode](#OSDMigrateMode) har värdet `Advanced` . Det här kommaavgränsade listvärdet anges för att utföra anpassad migrering av användarprofiler.

#### <a name="example"></a>Exempel

`miguser.xml,migsys.xml,migapps.xml`  

### <a name="osdmigratecontinueonlockedfiles"></a><a name="OSDMigrateContinueOnLockedFiles"></a>OSDMigrateContinueOnLockedFiles

*Gäller steget [avbilda användar tillstånd](task-sequence-steps.md#BKMK_CaptureUserState) .*

(indata)

Om USMT inte kan avbilda vissa filer tillåter den här variabeln att inspelningen av användar tillstånd fortsätter.

#### <a name="valid-values"></a>Giltiga värden

- `true`objekt  
- `false`  

### <a name="osdmigratecontinueonrestore"></a><a name="OSDMigrateContinueOnRestore"></a>OSDMigrateContinueOnRestore

*Gäller steget [Återställ användar tillstånd](task-sequence-steps.md#BKMK_RestoreUserState) .*

(indata)

Fortsätt processen även om USMT inte kan återställa vissa filer.

#### <a name="valid-values"></a>Giltiga värden

- `true`objekt  
- `false`  

### <a name="osdmigrateenableverboselogging"></a><a name="OSDMigrateEnableVerboseLogging"></a>OSDMigrateEnableVerboseLogging

*Gäller för följande steg:*  

- [Avbilda användartillstånd](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Återställ användartillstånd](task-sequence-steps.md#BKMK_RestoreUserState)  

(indata)

Aktiverar utförlig loggning för USMT. Steget kräver det här värdet.

#### <a name="valid-values"></a>Giltiga värden

- `true`  
- `false`objekt  

### <a name="osdmigratelocalaccounts"></a><a name="OSDMigrateLocalAccounts"></a>OSDMigrateLocalAccounts

*Gäller steget [Återställ användar tillstånd](task-sequence-steps.md#BKMK_RestoreUserState) .*

(indata)

Anger om det lokala datorkontot återställs.

#### <a name="valid-values"></a>Giltiga värden

- `true`  
- `false`objekt  

### <a name="osdmigratelocalaccountpassword"></a><a name="OSDMigrateLocalAccountPassword"></a>OSDMigrateLocalAccountPassword

*Gäller steget [Återställ användar tillstånd](task-sequence-steps.md#BKMK_RestoreUserState) .*

(indata)

Om variabeln [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) är `true` måste den här variabeln innehålla lösen ordet som tilldelats till *alla* migrerade lokala konton. USMT tilldelar samma lösen ord till alla migrerade lokala konton. Överväg det här lösen ordet som temporärt och ändra det senare med någon annan metod.

### <a name="osdmigratemode"></a><a name="OSDMigrateMode"></a>OSDMigrateMode

*Gäller steget [avbilda användar tillstånd](task-sequence-steps.md#BKMK_CaptureUserState) .*

(indata)

Gör att du kan anpassa de filer som USMT samlar in.

#### <a name="valid-values"></a>Giltiga värden

- `Simple`: Aktivitetssekvensen använder bara standardkonfigurations filerna för USMT  

- `Advanced`: Variabeln [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) anger KONFIGURATIONSFILER som USMT använder  

### <a name="osdmigratenetworkmembership"></a><a name="OSDMigrateNetworkMembership"></a>OSDMigrateNetworkMembership

*Gäller för steget [avbilda nätverks inställningar](task-sequence-steps.md#BKMK_CaptureNetworkSettings) .*

(indata)

Anger om aktivitetssekvensen migrerar information om arbets grupp eller domän medlemskap.

#### <a name="valid-values"></a>Giltiga värden

- `true`objekt
- `false`

### <a name="osdmigrateregistrationinfo"></a><a name="OSDMigrateRegistrationInfo"></a>OSDMigrateRegistrationInfo

*Gäller för steget [avbilda Windows-inställningar](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

(indata)

Anger om steget migrerar information om användare och organisationer.

#### <a name="valid-values"></a>Giltiga värden

- `true`(standard). Variabeln [tilldelas osdregisteredorgname (output)](#OSDRegisteredOrgName-output) anges till datorns registrerade organisations namn.  
- `false`  

### <a name="osdmigrateskipencryptedfiles"></a><a name="OSDMigrateSkipEncryptedFiles"></a>OSDMigrateSkipEncryptedFiles

*Gäller steget [avbilda användar tillstånd](task-sequence-steps.md#BKMK_CaptureUserState) .*

(indata)

Anger om krypterade filer avbildas.

#### <a name="valid-values"></a>Giltiga värden

- `true`  
- `false`objekt  

### <a name="osdmigratetimezone"></a><a name="OSDMigrateTimeZone"></a>OSDMigrateTimeZone

*Gäller för steget [avbilda Windows-inställningar](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

(indata)

Anger om datorns tidszon migreras.

#### <a name="valid-values"></a>Giltiga värden

- `true`(standard). Variabeln [tilldelas osdtimezone (output)](#OSDTimeZone-output) har angetts till datorns tidszon.  
- `false`  

### <a name="osdnetworkjointype"></a><a name="OSDNetworkJoinType"></a>OSDNetworkJoinType

*Gäller för steget [tillämpa nätverks inställningar](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(indata)

Anger om mål datorn ansluter till en Active Directory domän eller en arbets grupp.

#### <a name="value-values"></a>Värde värden

- `0`: Anslut en Active Directory domän  
- `1`: Anslut till en arbets grupp

### <a name="osdpartitions"></a><a name="OSDPartitions"></a>OSDPartitions

*Gäller för [disk steget formatera och partition](task-sequence-steps.md#BKMK_FormatandPartitionDisk) .*

(indata)

Variabeln aktivitetssekvens är en mat ris variabel av partitionsalternativ. Varje element i matrisen representerar inställningarna för en enskild partition på hårddisken. Få åtkomst till inställningarna som definierats för varje partition genom att kombinera mat ris variabelns namn med det nollbaserade disk partitionerings numret och egenskaps namnet.

Använd följande variabel namn för att definiera egenskaperna för den *första* partition som det här steget skapar på hård disken:

#### <a name="osdpartitions0type"></a>OSDPartitions0Type

Anger typen av partition. Den här egenskapen är obligatorisk. Giltiga värden är `Primary` , `Extended` , `Logical` och `Hidden` .

#### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem

Anger vilken typ av fil system som ska användas för att formatera partitionen. Den här egenskapen är valfri. Om du inte anger något fil system formateras inte partitionen av steget. Giltiga värden är `FAT32` och `NTFS` .

#### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable

Anger om partitionen är startbar. Den här egenskapen är obligatorisk. Om det här värdet är inställt på `TRUE` för MBR-diskar markerar steget den här partitionen som aktiv.

#### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat

Anger vilken typ av format som används. Den här egenskapen är obligatorisk. Om det här värdet är inställt på `TRUE` , utför steget ett Snabbformatering. Annars utför steget ett fullständigt format.

#### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName

Anger det namn som har tilldelats volymen när den formateras. Den här egenskapen är valfri.

#### <a name="osdpartitions0size"></a>OSDPartitions0Size

Anger partitionens storlek. Den här egenskapen är valfri. Om den här egenskapen inte anges skapas partitionen med allt återstående ledigt utrymme. Enheter anges med variabeln **OSDPartitions0SizeUnits** .

#### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits

I steget används dessa enheter för att tolka variabeln **OSDPartitions0Size** . Den här egenskapen är valfri. Giltiga värden är `MB` (standard), `GB` och `Percent` .

#### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable

När det här steget skapar partitioner, använder den alltid nästa tillgängliga enhets beteckning i Windows PE. Använd denna valfria egenskap för att ange namnet på en annan aktivitetssekvens variabel. I steget används den här variabeln för att spara den nya enhets beteckningen för framtida bruk.

Om du definierar flera partitioner med det här steget definieras egenskaperna för den *andra* partitionen med hjälp av **1** -indexet i variabel namnet. Till exempel: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**och **OSDPartitions1VolumeName**.

### <a name="osdpartitionstyle"></a><a name="OSDPartitionStyle"></a>OSDPartitionStyle

*Gäller för [disk steget formatera och partition](task-sequence-steps.md#BKMK_FormatandPartitionDisk) .*

(indata)

Anger partitionstypen som ska användas när disken partitioneras.

#### <a name="valid-values"></a>Giltiga värden

- `GPT`: Använd formatet GUID partition table
- `MBR`: Använd Master Boot Record partitionstyp

### <a name="osdproductkey"></a><a name="OSDProductKey"></a>OSDProductKey

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(indata)

Anger produktnyckeln för Windows. Det angivna värdet måste vara mellan 1 och 255 tecken.

### <a name="osdrandomadminpassword"></a><a name="OSDRandomAdminPassword"></a>OSDRandomAdminPassword

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(indata)

Anger ett slumpmässigt genererat lösen ord för det lokala administratörs kontot i det nya operativ systemet.

#### <a name="valid-values"></a>Giltiga värden

- `true`(standard): Installationsprogrammet för Windows inaktiverar det lokala administratörs kontot på mål datorn  

- `false`: Installationsprogrammet för Windows aktiverar det lokala administratörs kontot på mål datorn och anger konto lösen ordet till värdet för [OSDLocalAdminPassword](#OSDLocalAdminPassword)  

### <a name="osdregisteredorgname-input"></a><a name="OSDRegisteredOrgName-input"></a>Tilldelas osdregisteredorgname (Indatatyp)

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Anger det registrerade standard organisations namnet i det nya operativ systemet. Det angivna värdet måste vara mellan 1 och 255 tecken.

### <a name="osdregisteredorgname-output"></a><a name="OSDRegisteredOrgName-output"></a>Tilldelas osdregisteredorgname (utdata)

*Gäller för steget [avbilda Windows-inställningar](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

Inställt på datorns registrerade organisationsnamn. Värdet anges bara om variabeln [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) har värdet `true` .

### <a name="osdregisteredusername"></a><a name="OSDRegisteredUserName"></a>OSDRegisteredUserName

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(indata)

Anger det registrerade standard användar namnet i det nya operativ systemet. Det angivna värdet måste vara mellan 1 och 255 tecken.

### <a name="osdserverlicenseconnectionlimit"></a><a name="OSDServerLicenseConnectionLimit"></a>OSDServerLicenseConnectionLimit

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(indata)

Anger högsta antal tillåtna anslutningar. Det angivna värdet måste ligga i intervallet mellan 5 och 9 999 anslutningar.

### <a name="osdserverlicensemode"></a><a name="OSDServerLicenseMode"></a>OSDServerLicenseMode

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

(indata)

Anger licens läget för Windows Server som används.

#### <a name="valid-values"></a>Giltiga värden

- `PerSeat`
- `PerServer`

### <a name="osdsetupadditionalupgradeoptions"></a><a name="OSDSetupAdditionalUpgradeOptions"></a>OSDSetupAdditionalUpgradeOptions

*Gäller steget [Uppgradera operativ system](task-sequence-steps.md#BKMK_UpgradeOS) .*

(indata)

Anger ytterligare kommando rads alternativ som läggs till i Installationsprogrammet för Windows under en Windows 10-uppgradering. Aktivitetssekvensen verifierar inte kommando rads alternativen.

Mer information finns i [Kommandoradsalternativ för Windows-installationsprogrammet](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

### <a name="osdstatefallbacktonaa"></a><a name="OSDStateFallbackToNAA"></a>OSDStateFallbackToNAA

*Gäller för steget [begär tillstånds lager](task-sequence-steps.md#BKMK_RequestStateStore) .*

(indata)

Om dator kontot inte kan ansluta till platsen för tillståndsmigrering anger den här variabeln om aktivitetssekvensen går tillbaka till att använda kontot för nätverks åtkomst (PEERCACHELAGRING).

Mer information om kontot för nätverks åtkomst finns i [konton](../../core/plan-design/hierarchy/accounts.md#network-access-account).

#### <a name="valid-values"></a>Giltiga värden

- `true`  
- `false`objekt  

### <a name="osdstatesmpretrycount"></a><a name="OSDStateSMPRetryCount"></a>OSDStateSMPRetryCount

*Gäller för steget [begär tillstånds lager](task-sequence-steps.md#BKMK_RequestStateStore) .*

(indata)

Anger hur många gånger aktivitetssekvenssteget försöker hitta en plats för tillståndsmigrering innan steget misslyckas. Det angivna antalet måste vara mellan 0 och 600.

### <a name="osdstatesmpretrytime"></a><a name="OSDStateSMPRetryTime"></a>OSDStateSMPRetryTime

*Gäller för steget [begär tillstånds lager](task-sequence-steps.md#BKMK_RequestStateStore) .*

(indata)

Anger hur många sekunder aktivitetssekvenssteget ska vänta innan ett nytt försök görs. Antalet sekunder får bestå av högst 30 tecken.

### <a name="osdstatestorepath"></a><a name="OSDStateStorePath"></a>Aktivitetssekvensvariabeln OSDStateStorePath

*Gäller för följande steg:*  

- [Avbilda användartillstånd](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Frisläpp tillståndslager](task-sequence-steps.md#BKMK_ReleaseStateStore)  
- [Begär tillståndslager](task-sequence-steps.md#BKMK_RequestStateStore)  
- [Återställ användartillstånd](task-sequence-steps.md#BKMK_RestoreUserState)  

(indata)

Nätverks resursen eller namnet på den lokala sökvägen till den mapp där aktivitetssekvensen sparar eller återställer användar tillstånd. Det finns inget standardvärde.

### <a name="osdtargetsystemdrive"></a><a name="OSDTargetSystemDrive"></a>OSDTargetSystemDrive

*Gäller för steget [Använd operativ Systems avbildning](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage) .*

(utdata)

Anger enhets beteckningen för den partition som innehåller OS-filerna när avbildningen har tillämpats.

### <a name="osdtargetsystemroot-input"></a><a name="OSDTargetSystemRoot-input"></a>OSDTargetSystemRoot (Indatatyp)

*Gäller för steget [avbilda operativ system avbildning](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage) .*

Anger sökvägen till Windows-katalogen för det installerade operativ systemet på referens datorn. Aktivitetssekvensen verifierar att ett operativ system som stöds för avbildning av Configuration Manager.

### <a name="osdtargetsystemroot-output"></a><a name="OSDTargetSystemRoot-output"></a>OSDTargetSystemRoot (utdata)

*Gäller för steget [Förbered Windows för avbildning](task-sequence-steps.md#BKMK_PrepareWindowsforCapture) .*

Anger sökvägen till Windows-katalogen för det installerade operativ systemet på referens datorn. Aktivitetssekvensen verifierar att ett operativ system som stöds för avbildning av Configuration Manager.

### <a name="osdtimezone-input"></a><a name="OSDTimeZone-input"></a>Tilldelas osdtimezone (Indatatyp)

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Anger standard tids zons inställningen som används i det nya operativ systemet.

Ange värdet för den här variabeln till språkets invariant-namn för tids zonen. Använd till exempel strängen i `Std` värdet för en tidszon under följande register nyckel: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones` .

### <a name="osdtimezone-output"></a><a name="OSDTimeZone-output"></a>Tilldelas osdtimezone (utdata)

*Gäller för steget [avbilda Windows-inställningar](task-sequence-steps.md#BKMK_CaptureWindowsSettings) .*

Anger datorns tidszon. Värdet anges bara om variabeln [OSDMigrateTimeZone](#OSDMigrateTimeZone) har värdet `true` .

### <a name="osdwindowssettingsinputlocale"></a><a name="OSDWindowsSettingsInputLocale"></a>OSDWindowsSettingsInputLocale

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Anger standard språk inställningen för inmatningar som används i det nya operativ systemet.

Mer information om värdet för svars filen för Windows-installationen finns i [Microsoft-Windows-International-Core-InputLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-inputlocale).

### <a name="osdwindowssettingssystemlocale"></a><a name="OSDWindowsSettingsSystemLocale"></a>OSDWindowsSettingsSystemLocale

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Anger standard språk inställningen som används i det nya operativ systemet.

Mer information om värdet för svars filen för Windows-installationen finns i [Microsoft-Windows-International-Core-SystemLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-systemlocale).

### <a name="osdwindowssettingsuilanguage"></a><a name="OSDWindowsSettingsUILanguage"></a>OSDWindowsSettingsUILanguage

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Anger standard språk inställningen för användar gränssnittet som används i det nya operativ systemet.

Mer information om värdet för svars filen för Windows-installationen finns i [Microsoft-Windows-International-Core-UILanguage](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguage).

### <a name="osdwindowssettingsuilanguagefallback"></a><a name="OSDWindowsSettingsUILanguageFallback"></a>OSDWindowsSettingsUILanguageFallback

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Anger språk inställningen för återställnings användar gränssnittet som används i det nya operativ systemet.

Mer information om värdet för svars filen för Windows-installationen finns i [Microsoft-Windows-International-Core-UILanguageFallback](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-uilanguagefallback).

### <a name="osdwindowssettingsuserlocale"></a><a name="OSDWindowsSettingsUserLocale"></a>OSDWindowsSettingsUserLocale

*Gäller steget [Använd Windows-inställningar](task-sequence-steps.md#BKMK_ApplyWindowsSettings) .*

Anger standard språk inställningen för användare som används i det nya operativ systemet.

Mer information om värdet för svars filen för Windows-installationen finns i [Microsoft-Windows-International-Core-UserLocale](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core-userlocale).

### <a name="osdwipedestinationpartition"></a><a name="OSDWipeDestinationPartition"></a>OSDWipeDestinationPartition

*Gäller för steget [Använd data avbildning](task-sequence-steps.md#BKMK_ApplyDataImage) .*

(indata)

Anger om filerna på målpartitionen ska tas bort.

#### <a name="valid-values"></a>Giltiga värden

- `true`objekt
- `false`

### <a name="osdworkgroupname"></a><a name="OSDWorkgroupName"></a>OSDWorkgroupName

*Gäller för steget [tillämpa nätverks inställningar](task-sequence-steps.md#BKMK_ApplyNetworkSettings) .*

(indata)

Anger namnet på arbetsgruppen som måldatorn ansluter till.

Ange antingen den här variabeln eller [OSDDomainName](#OSDDomainName) -variabeln. Namnet på arbetsgruppen får innehålla högst 32 tecken.

### <a name="setupcompletepause"></a><a name="SetupCompletePause"></a>SetupCompletePause

*Gäller steget [Uppgradera operativ system](task-sequence-steps.md#BKMK_UpgradeOS) .*

<!-- 4680263 -->

Från och med version 1910 använder du den här variabeln för att åtgärda tids problem med Windows 10 på plats-uppgradering för hög prestanda när Windows-installationen är klar. När du tilldelar ett värde i sekunder till den här variabeln, förskjuter Windows-installationsprogrammet den tiden innan aktivitetssekvensen startas. Denna timeout ger Configuration Manager klienten ytterligare tid att initiera.

Följande logg poster är vanliga exempel på det här problemet som du kan åtgärda med den här variabeln:

- TSManager-komponenten registrerar poster som liknar följande fel i **Smsts. log**:

    ``` log
    Failed to initate policy evaluation for namespace 'root\ccm\policy\machine', hr=0x80041010
    Error compiling client config policies. code 80041010
    Task Sequence Manager could not initialize Task Sequence Environment. code 80041010
    ```

- Installations programmet för Windows registrerar poster som liknar följande fel i **Setupcomplete. log**:

    ``` log
    Running C:\windows\CCM\\TSMBootstrap.exe to resume task sequence
    ERRORLEVEL = -1073741701
    TSMBootstrap did not request reboot, resetting registry
    Exiting setupcomplete.cmd
    ```

### <a name="smsclientinstallproperties"></a><a name="SMSClientInstallProperties"></a>SMSClientInstallProperties

*Gäller för steget [Installera Windows och ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) .*

(indata)

Anger de klient installations egenskaper som aktivitetssekvensen använder för att installera Configuration Manager-klienten.

Mer information finns i [om klient installations parametrar och egenskaper](../../core/clients/deploy/about-client-installation-properties.md).

### <a name="smsconnectnetworkfolderaccount"></a><a name="SMSConnectNetworkFolderAccount"></a>SMSConnectNetworkFolderAccount

*Gäller steget [Anslut till nätverksmapp](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) .*

(indata)

Anger det användar konto som används för att ansluta till nätverks resursen i [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). Ange konto lösen ordet med värdet [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword) .

Mer information om anslutnings kontot för en nätverksmapp finns i [konton](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account).

### <a name="smsconnectnetworkfolderdriveletter"></a><a name="SMSConnectNetworkFolderDriveLetter"></a>SMSConnectNetworkFolderDriveLetter

*Gäller steget [Anslut till nätverksmapp](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) .*

(indata)

Anger enhetsbeteckningen för nätverksanslutningen. Det här värdet är valfritt. Om den inte anges mappas inte nätverks anslutningen till en enhets beteckning. Om det här värdet anges måste värdet vara i intervallet från D till Z. Använd inte X, det är enhets beteckningen som används av Windows PE under Windows PE-fasen.

#### <a name="examples"></a>Exempel

- `D:`  
- `E:`  

### <a name="smsconnectnetworkfolderpassword"></a><a name="SMSConnectNetworkFolderPassword"></a>SMSConnectNetworkFolderPassword

*Gäller steget [Anslut till nätverksmapp](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) .*

(indata)

Anger lösen ordet för den [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) som används för att ansluta till nätverks resursen i [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath).

### <a name="smsconnectnetworkfolderpath"></a><a name="SMSConnectNetworkFolderPath"></a>SMSConnectNetworkFolderPath

*Gäller steget [Anslut till nätverksmapp](task-sequence-steps.md#BKMK_ConnectToNetworkFolder) .*

(indata)

Anger nätverkssökvägen för anslutningen. Om du behöver mappa sökvägen till en enhets beteckning använder du [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter) -värdet.

#### <a name="example"></a>Exempel

`\\server\share`

### <a name="smsinstallupdatetarget"></a><a name="SMSInstallUpdateTarget"></a>SMSInstallUpdateTarget

*Gäller steget [installera program uppdateringar](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) .*

(indata)

Anger om alla uppdateringar ska installeras eller endast obligatoriska uppdateringar.

#### <a name="valid-values"></a>Giltiga värden

- `All`  
- `Mandatory`  

### <a name="smsrebootmessage"></a><a name="SMSRebootMessage"></a>SMSRebootMessage

*Gäller steget [starta om datorn](task-sequence-steps.md#BKMK_RestartComputer) .*

(indata)

Anger vilket meddelande som ska visas för användarna innan måldatorn startas om. Om den här variabeln inte anges visas standard meddelande texten. Det angivna meddelandet får inte överstiga 512 tecken.

#### <a name="example"></a>Exempel

`Save your work before the computer restarts.`  

### <a name="smsreboottimeout"></a><a name="SMSRebootTimeout"></a>SMSRebootTimeout

*Gäller steget [starta om datorn](task-sequence-steps.md#BKMK_RestartComputer) .*

(indata)

Anger hur många sekunder varningen visas för användaren innan datorn startas om.

#### <a name="examples"></a>Exempel

- `0`(standard): Visa inte ett omstarts meddelande  
- `60`: Visa varningen i en minut  

### <a name="smstsassignmentsdownloadinterval"></a><a name="SMSTSAssignmentsDownloadInterval"></a>SMSTSAssignmentsDownloadInterval

Antalet sekunder att vänta innan klienten försöker hämta principen sedan det senaste försöket som inte returnerade några principer. Som standard väntar klienten **0** sekunder innan den försöker igen.

Du kan ange den här variabeln genom att använda ett förinläsningskommando från medier eller PXE.

### <a name="smstsassignmentsdownloadretry"></a><a name="SMSTSAssignmentsDownloadRetry"></a>SMSTSAssignmentsDownloadRetry

Antalet gånger som en klient försöker hämta principen när inga principer har hittats vid det första försöket. Som standard försöker klienten igen **0** gånger.

Du kan ange den här variabeln genom att använda ett förinläsningskommando från medier eller PXE.

### <a name="smstsassignusersmode"></a><a name="SMSTSAssignUsersMode"></a>SMSTSAssignUsersMode

Anger hur en aktivitetssekvensen associerar användare med måldatorn. Ställ in variabeln på ett av följande värden:  

- **Auto**: När aktivitetssekvensen distribuerar operativ systemet till mål datorn skapas en relation mellan de angivna användarna och mål datorn.  

- **Väntar**: Aktivitetssekvensen skapar en relation mellan de angivna användarna och mål datorn. En administratör måste godkänna relationen för att ställa in den.  

- **Inaktive rad**: aktivitetssekvensen kopplar inte användare till mål datorn när operativ systemet distribueras.

### <a name="smstsdisablestatusretry"></a><a name="SMSTSDisableStatusRetry"></a>SMSTSDisableStatusRetry

<!--512358-->
I frånkopplade scenarier försöker aktivitetssekvensen upprepade gånger att skicka status meddelanden till hanterings platsen. Detta beteende i det här scenariot orsakar fördröjningar vid bearbetning av aktivitetssekvensen.

Ange den här variabeln till så `true` försöker motorn för aktivitetssekvenser inte att skicka status meddelanden när det första meddelandet inte har skickats. Det första försöket innehåller flera återförsök.

När aktivitetssekvensen startas om kvarstår värdet för den här variabeln. Aktivitetssekvensen försöker dock skicka ett första status meddelande. Det första försöket innehåller flera återförsök. Om det lyckas fortsätter aktivitetssekvensen att skicka status oavsett värdet för den här variabeln. Om det inte går att skicka status använder aktivitetssekvensen värdet för den här variabeln.

> [!NOTE]  
> [Status rapportering för aktivitetssekvens](../../core/servers/manage/list-of-reports.md#task-sequence---deployment-status) förlitar sig på dessa status meddelanden för att visa förloppet, historiken och information om varje steg. Om status meddelanden inte kan skickas är de inte i kö. När anslutningen återställs till hanterings platsen skickas de inte vid ett senare tillfälle. Detta leder till att status rapporter för aktivitetssekvens inte är fullständiga och saknade objekt.

### <a name="smstsdisablewow64redirection"></a><a name="SMSTSDisableWow64Redirection"></a>SMSTSDisableWow64Redirection

*Gäller för steget [Kör kommando rad](task-sequence-steps.md#BKMK_RunCommandLine) .*

(indata)

Som standard i ett 64-bitars operativ system hittar aktivitetssekvensen och kör programmet på kommando raden med hjälp av WOW64-fil systemets omdirigerare. Detta gör att kommandot kan hitta 32-bitars versioner av OS-program och DLL-filer. Om du anger den här variabeln `true` inaktive ras användningen av WOW64-fil systemets omdirigerare. Kommandot hittar inbyggda 64-bitars versioner av OS-program och DLL-filer. Den här variabeln har ingen påverkan när den körs på ett 32-bitars operativ system.

### <a name="smstsdownloadabortcode"></a><a name="SMSTSDownloadAbortCode"></a>SMSTSDownloadAbortCode

Den här variabeln innehåller värdet för abort-koden för det externa program hämtaren. Det här programmet anges i variabeln [SMSTSDownloadProgram](#SMSTSDownloadProgram) . Om programmet returnerar en felkod som är lika med värdet för variabeln SMSTSDownloadAbortCode Miss lyckas hämtningen av innehållet och ingen annan nedladdnings metod görs.

### <a name="smstsdownloadprogram"></a><a name="SMSTSDownloadProgram"></a>SMSTSDownloadProgram

Använd den här variabeln för att ange en alternativ innehålls leverantör (ACP). En AVS är ett hämta program som används för att ladda ned innehåll. Aktivitetssekvensen använder ACP i stället för standard Configuration Manager hämtaren. Som en del av processen för innehålls hämtning kontrollerar aktivitetssekvensen den här variabeln. Om det här alternativet anges kör aktivitetssekvensen programmet för att ladda ned innehållet.

### <a name="smstsdownloadretrycount"></a><a name="SMSTSDownloadRetryCount"></a>SMSTSDownloadRetryCount

Antalet gånger Configuration Manager försöker ladda ned innehåll från en distributions plats. Som standard försöker klienten igen **2** gånger.

### <a name="smstsdownloadretrydelay"></a><a name="SMSTSDownloadRetryDelay"></a>SMSTSDownloadRetryDelay

Antalet sekunder som Configuration Manager väntar innan det försöker ladda ned innehåll från en distributions plats igen. Som standard väntar klienten **15** sekunder innan den försöker igen.

### <a name="smstsdriverrequestconnecttimeout"></a><a name="SMSTSDriverRequestConnectTimeOut"></a>SMSTSDriverRequestConnectTimeOut

*Gäller för steget [Använd driv rutiner automatiskt](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

När du begär driv rutins katalogen är den här variabeln antalet sekunder som aktivitetssekvensen väntar på HTTP-servern. Om anslutningen tar längre tid än timeout-inställningen avbryter aktivitetssekvensen begäran. Som standard är tids gränsen inställd på **60** sekunder.

### <a name="smstsdriverrequestreceivetimeout"></a><a name="SMSTSDriverRequestReceiveTimeOut"></a>SMSTSDriverRequestReceiveTimeOut

*Gäller för steget [Använd driv rutiner automatiskt](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

När du begär driv rutins katalogen är den här variabeln antalet sekunder som aktivitetssekvensen väntar på ett svar. Om anslutningen tar längre tid än timeout-inställningen avbryter aktivitetssekvensen begäran. Som standard är tids gränsen inställd på **480** sekunder.

### <a name="smstsdriverrequestresolvetimeout"></a><a name="SMSTSDriverRequestResolveTimeOut"></a>SMSTSDriverRequestResolveTimeOut

*Gäller för steget [Använd driv rutiner automatiskt](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

När du begär driv rutins katalogen är den här variabeln antalet sekunder som aktivitetssekvensen väntar på HTTP-namnmatchning. Om anslutningen tar längre tid än timeout-inställningen avbryter aktivitetssekvensen begäran. Som standard är tids gränsen inställd på **60** sekunder.

### <a name="smstsdriverrequestsendtimeout"></a><a name="SMSTSDriverRequestSendTimeOut"></a>SMSTSDriverRequestSendTimeOut

*Gäller för steget [Använd driv rutiner automatiskt](task-sequence-steps.md#BKMK_AutoApplyDrivers) .*

När du skickar en begäran för driv rutins katalogen är den här variabeln antalet sekunder som aktivitetssekvensen väntar på att skicka begäran. Om begäran tar längre tid än timeout-inställningen avbryter aktivitetssekvensen begäran. Som standard är tids gränsen inställd på **60** sekunder.

### <a name="smstserrordialogtimeout"></a><a name="SMSTSErrorDialogTimeout"></a>SMSTSErrorDialogTimeout

När ett fel uppstår i en aktivitetssekvens visas en dialog ruta med felet. Aktivitetssekvensen ignorerar automatiskt den efter antalet sekunder som anges av den här variabeln. Som standard är det här värdet **900** sekunder (15 minuter).

### <a name="smstslanguagefolder"></a><a name="SMSTSLanguageFolder"></a>SMSTSLanguageFolder

Använd den här variabeln för att ändra visningsspråk för en språkneutral startavbildning.

### <a name="smstslocaldatadrive"></a><a name="SMSTSLocalDataDrive"></a>SMSTSLocalDataDrive

Anger var aktivitetssekvensen lagrar temporära cachefiler på mål datorn när den körs.

Ange den här variabeln innan aktivitetssekvensen startar, t. ex. genom att ange en samlings variabel. När aktivitetssekvensen startar definierar Configuration Manager [_SMSTSMDataPath](#SMSTSMDataPath) variabeln baserat på vad variabeln SMSTSLocalDataDrive har definierats för.

### <a name="smstsmp"></a><a name="SMSTSMP"></a>SMSTSMP

Använd den här variabeln för att ange URL: en eller IP-adressen för Configuration Manager hanterings platsen.

### <a name="smstsmplistrequesttimeoutenabled"></a><a name="SMSTSMPListRequestTimeoutEnabled"></a>SMSTSMPListRequestTimeoutEnabled

*Gäller för följande steg:*  

- [Installera program](task-sequence-steps.md#BKMK_InstallApplication)  
- [Installera programuppdateringar](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(indata)

Om klienten inte finns på intranätet använder du den här variabeln för att aktivera upprepade MPList-begäranden för att uppdatera klienten. Som standard är den här variabeln inställd på `True` .

När klienterna är på Internet anger du den här variabeln för `False` att undvika onödiga fördröjningar.

### <a name="smstsmplistrequesttimeout"></a><a name="SMSTSMPListRequestTimeout"></a>SMSTSMPListRequestTimeout

*Gäller för följande steg:*  

- [Installera program](task-sequence-steps.md#BKMK_InstallApplication)  
- [Installera programuppdateringar](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(indata)

Om aktivitetssekvensen inte kan hämta listan över hanterings platser (MPList) från plats tjänster anger den här variabeln hur många millisekunder den väntar innan den försöker igen. Som standard väntar aktivitetssekvensen i `60000` millisekunder (60 sekunder) innan den försöker igen. Det försöker igen upp till tre gånger.

### <a name="smstspeerdownload"></a><a name="SMSTSPeerDownload"></a>SMSTSPeerDownload

Använd den här variabeln om du vill att klienten ska kunna använda peer-cache i Windows PE. Om du anger den här variabeln `true` aktive ras den här funktionen.

### <a name="smstspeerrequestport"></a><a name="SMSTSPeerRequestPort"></a>SMSTSPeerRequestPort

En anpassad nätverks port som används av peer-cache i Windows PE för den första sändningen. Standard porten som kon figurer ATS i klient inställningarna är **8004**.

### <a name="smstspersistcontent"></a><a name="SMSTSPersistContent"></a>SMSTSPersistContent

Använd den här variabeln för att tillfälligt bevara innehåll i aktivitetssekvenscachen. Den här variabeln skiljer sig från [SMSTSPreserveContent](#SMSTSPreserveContent), som behåller innehåll i Configuration Manager-klientcachen efter att aktivitetssekvensen har slutförts. SMSTSPersistContent använder cachen för aktivitetssekvenser, SMSTSPreserveContent använder Configuration Manager-klientcachen.

### <a name="smstspostaction"></a><a name="SMSTSPostAction"></a>SMSTSPostAction

Anger ett kommando som körs när aktivitetssekvensen har slutförts. Ange till exempel `shutdown.exe /r /t 30 /f` att datorn ska starta om 30 sekunder efter att aktivitetssekvensen har slutförts.

### <a name="smstspreferredadvertid"></a><a name="SMSTSPreferredAdvertID"></a>SMSTSPreferredAdvertID

Tvingar aktivitetssekvensen att köra en viss riktad distribution på mål datorn. Ange den här variabeln genom ett för inläsnings kommando från media eller PXE. Om den här variabeln anges åsidosätter aktivitetssekvensen alla nödvändiga distributioner.

### <a name="smstspreservecontent"></a><a name="SMSTSPreserveContent"></a>SMSTSPreserveContent

Den här variabeln flaggar innehållet i aktivitetssekvensen som ska behållas i Configuration Manager-klientcachen efter distributionen. Den här variabeln skiljer sig från [SMSTSPersistContent](#SMSTSPersistContent), som endast behåller innehållet under aktivitetssekvensen. SMSTSPersistContent använder cachen för aktivitetssekvenser, SMSTSPreserveContent använder Configuration Manager-klientcachen. Aktivera den här funktionen genom att ange SMSTSPreserveContent till `true` .

### <a name="smstsrebootdelay"></a><a name="SMSTSRebootDelay"></a>SMSTSRebootDelay

Anger hur många sekunder du måste vänta innan datorn startas om. Om den här variabeln är noll (0) visas inte en meddelande dialog ruta innan du startar om den här aktivitetssekvensen.

#### <a name="example"></a>Exempel

- `0`: Visa inte ett meddelande  

- `60`: Visa ett meddelande i en minut  

### <a name="smstsrebootdelaynext"></a><a name="SMSTSRebootDelayNext"></a>SMSTSRebootDelayNext

<!--4447680-->
Från och med version 1906 använder du den här variabeln med den befintliga [SMSTSRebootDelay](task-sequence-variables.md#SMSTSRebootDelay) -variabeln. Om du vill att senare omstarter ska ske under en annan tids gräns än den första, anger du SMSTSRebootDelayNext till ett annat värde på några sekunder.

#### <a name="example"></a>Exempel

Du vill ge användarna ett meddelande om att starta om 60-minuters omstart i början av en aktivitetssekvens för Windows 10-uppgradering på plats. Efter den första långa tids gränsen vill du att ytterligare tids gränser bara är 60 sekunder. Ange SMSTSRebootDelay till `3600` och SMSTSRebootDelayNext till `60` .  


### <a name="smstsrebootmessage"></a><a name="SMSTSRebootMessage"></a>SMSTSRebootMessage

Anger meddelandet som ska visas i dialog rutan Starta om meddelande. Om den här variabeln inte anges visas ett standard meddelande.

#### <a name="example"></a>Exempel

`The task sequence is restarting this computer`

### <a name="smstsrebootrequested"></a><a name="SMSTSRebootRequested"></a>SMSTSRebootRequested

Anger att en omstart krävs när det aktuella aktivitetssekvenssteget har slutförts. Om steget i aktivitetssekvensen kräver en omstart för att slutföra åtgärden, anger du den här variabeln. När datorn har startats om fortsätter aktivitetssekvensen att köras från nästa steg i aktivitetssekvensen.

- `HD`: Starta om till det installerade operativ systemet
- `WinPE`: Starta om till den associerade start avbildningen

### <a name="smstsretryrequested"></a><a name="SMSTSRetryRequested"></a>SMSTSRetryRequested

Begär ett nytt försök efter att det aktuella aktivitetssekvenssteget har slutförts. Om variabeln för aktivitetssekvensen har angetts anger du även variabeln [SMSTSRebootRequested](#SMSTSRebootRequested) `true` . När datorn har startats om kör aktivitetssekvensen om samma steg i aktivitetssekvensen.

### <a name="smstsruncommandlineasuser"></a><a name="SMSTSRunCommandLineAsUser"></a>SMSTSRunCommandLineAsUser

*Från och med version 2002* <!-- 5573175 -->  
*Gäller för steget [Kör kommando rad](task-sequence-steps.md#BKMK_RunCommandLine) .*

Använd variabler för aktivitetssekvens för att konfigurera användar kontexten för steget **Kör kommando rad** . Du behöver inte konfigurera steget **Kör kommando rad** med ett plats hållare för att använda variablerna [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName) och [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword) .

Konfigurera `SMSTSRunCommandLineAsUser` med något av följande värden:

- `true`: Alla ytterligare **körnings kommando rads** steg körs i kontexten för den användare som anges i `SMSTSRunCommandLineUserName` .

- `false`: Alla ytterligare **körnings kommando rads** steg körs i den kontext som du konfigurerade i steget.

### <a name="smstsruncommandlineusername"></a><a name="SMSTSRunCommandLineUserName"></a>SMSTSRunCommandLineUserName

*Gäller för steget [Kör kommando rad](task-sequence-steps.md#BKMK_RunCommandLine) .*

(indata)

Anger det konto som kommandoraden körs med. Värdet är en sträng med formatet användarnamn eller domän\användarnamn. Ange konto lösen ordet med variabeln [SMSTSRunCommandLineUserPassword](#SMSTSRunCommandLineUserPassword) .

> [!NOTE]
> Från och med version 2002 använder du variabeln [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) med den här variabeln för att konfigurera användar kontexten för det här steget.
>
> I version 1910 och tidigare konfigurerar du steget **Kör kommando rad** med inställningen för att **köra det här steget som följande konto**. Om du aktiverar det här alternativet anger du ett värde för kontot om du anger användar namn och lösen ord med variabler.

Mer information om kör som-kontot för aktivitetssekvens finns i [konton](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

### <a name="smstsruncommandlineuserpassword"></a><a name="SMSTSRunCommandLineUserPassword"></a>SMSTSRunCommandLineUserPassword

*Gäller för steget [Kör kommando rad](task-sequence-steps.md#BKMK_RunCommandLine) .*

(indata)

Anger lösen ordet för kontot som anges av [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName) -variabeln.

### <a name="smstsrunpowershellasuser"></a><a name="SMSTSRunPowerShellAsUser"></a>SMSTSRunPowerShellAsUser

*Från och med version 2002* <!-- 5573175 -->  
*Gäller skript steget [kör PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript) .*

Använd variabler för aktivitetssekvens för att konfigurera användar kontexten för steget **kör PowerShell-skript** . Du behöver inte konfigurera steget **kör PowerShell-skript** med ett plats hållare för att använda variablerna [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName) och [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword) .

Konfigurera `SMSTSRunPowerShellAsUser` med något av följande värden:

- `true`: Alla **kör PowerShell-skript** körs i kontexten för den användare som anges i `SMSTSRunPowerShellUserName` .

- `false`: Alla **kör PowerShell-skript** körs i den kontext som du konfigurerade i steget.

### <a name="smstsrunpowershellusername"></a><a name="SMSTSRunPowerShellUserName"></a>SMSTSRunPowerShellUserName

*Gäller skript steget [kör PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript) .*

(indata)

Anger det konto som används för att köra PowerShell-skriptet. Värdet är en sträng med formatet användarnamn eller domän\användarnamn. Ange konto lösen ordet med variabeln [SMSTSRunPowerShellUserPassword](#SMSTSRunPowerShellUserPassword) .

> [!NOTE]
> Om du vill använda dessa variabler konfigurerar du steget **kör PowerShell-skript** med inställningen för att **köra det här steget som följande konto**. Om du aktiverar det här alternativet anger du ett värde för kontot om du anger användar namn och lösen ord med variabler.

Mer information om kör som-kontot för aktivitetssekvens finns i [konton](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account).

### <a name="smstsrunpowershelluserpassword"></a><a name="SMSTSRunPowerShellUserPassword"></a>SMSTSRunPowerShellUserPassword

*Gäller skript steget [kör PowerShell](task-sequence-steps.md#BKMK_RunPowerShellScript) .*

(indata)

Anger lösen ordet för kontot som anges av [SMSTSRunPowerShellUserName](#SMSTSRunPowerShellUserName) -variabeln.

### <a name="smstssoftwareupdatescantimeout"></a><a name="SMSTSSoftwareUpdateScanTimeout"></a>SMSTSSoftwareUpdateScanTimeout

*Gäller steget [installera program uppdateringar](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) .*

(indata)

Kontrol lera timeout för genomsökning av program uppdateringar under det här steget. Om du till exempel förväntar dig flera uppdateringar under genomsökningen ska du öka värdet. Standardvärdet är `3600` sekunder (60 minuter). Värdet för variabeln anges i sekunder.

### <a name="smstsudausers"></a><a name="SMSTSUDAUsers"></a>SMSTSUDAUsers

Anger de primära användarna av mål datorn med hjälp av följande format: `<DomainName>\<UserName>` . Avgränsa flera användare med kommatecken ( `,` ). Mer information finns i [associera användare med en måldator](../get-started/associate-users-with-a-destination-computer.md).

#### <a name="example"></a>Exempel

`contoso\jqpublic, contoso\megb, contoso\janedoh`

### <a name="smstswaitforsecondreboot"></a><a name="SMSTSWaitForSecondReboot"></a>SMSTSWaitForSecondReboot

*Gäller steget [installera program uppdateringar](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) .*

(indata)

Den här valfria variabeln aktivitetssekvens styr klient beteendet när en program uppdaterings installation kräver två omstarter. Ange den här variabeln före det här steget för att förhindra att en aktivitetssekvens Miss Miss Missing på grund av en andra omstart från installationen av program uppdateringen.

Ange värdet för SMSTSWaitForSecondReboot i sekunder för att ange hur länge aktivitetssekvensen pausas i det här steget när datorn startas om. Tillåt tillräckligt med tid om det finns en andra omstart.

Om du till exempel ställer in SMSTSWaitForSecondReboot på `600` pausar en aktivitetssekvens i 10 minuter efter en omstart innan ytterligare steg körs. Den här variabeln är användbar när steget installera program uppdateringar i en enskild installation installerar hundratals program uppdateringar.

> [!Note]
> Den här variabeln gäller bara för en aktivitetssekvens som distribuerar ett operativ system. Den fungerar inte i en anpassad aktivitetssekvens. <!-- 2839998 -->

### <a name="tsdebugmode"></a><a name="TSDebugMode"></a>TSDebugMode

<!--3612274-->
Från och med version 1906 ställer du in den här variabeln `TRUE` på en samling eller ett dator objekt som aktivitetssekvensen distribueras till. Alla enheter som har denna variabel uppsättning kommer att placera en aktivitetssekvens som distribueras i fel söknings läge.

Mer information finns i [fel sökning av en aktivitetssekvens](../deploy-use/debug-task-sequence.md).

### <a name="tsdebugonerror"></a><a name="TSDebugOnError"></a>TSDebugOnError

<!-- 5012536 -->
Från och med version 1910 ställer du in den här variabeln för `TRUE` att automatiskt starta [fel sökning av aktivitetssekvensen](../deploy-use/debug-task-sequence.md) när aktivitetssekvensen returnerar ett fel.

Ange den här variabeln med:

- [Variabel steget Ange aktivitetssekvens](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)

- En samlings variabel. Mer information finns i [så här ställer du in variabler](using-task-sequence-variables.md#bkmk_set).

### <a name="tsdisableprogressui"></a><a name="TSDisableProgressUI"></a>TSDisableProgressUI

<!-- 1354291 -->
Använd den här variabeln för att styra när aktivitetssekvensen visar förloppet till slutanvändarna. Om du vill dölja eller Visa förloppet vid olika tidpunkter anger du den här variabeln flera gånger i en aktivitetssekvens.  

- `true`: Dölj förlopp för aktivitetssekvens  

- `false`: Visa förlopp för aktivitetssekvens  

### <a name="tserroronwarning"></a><a name="TSErrorOnWarning"></a>TSErrorOnWarning

*Gäller steget [installera program](task-sequence-steps.md#BKMK_InstallApplication) .*

(indata)

Ange om motorn för aktivitetssekvenser ser en identifierad varning som ett fel under det här steget. Aktivitetssekvensen ställer in [_TSAppInstallStatus](#TSAppInstallStatus) variabeln till `Warning` när ett eller flera program, eller ett obligatoriskt beroende, inte installerades eftersom det inte uppfyller ett krav. När du ställer in den här variabeln på `True` och aktivitetssekvensen anger **_TSAppInstallStatus** till `Warning` , är resultatet ett fel. Värdet `False` är standard beteendet.

### <a name="tsprogressinfolevel"></a><a name="TSProgressInfoLevel"></a>TSProgressInfoLevel

*Från och med version 2002*<!--5932692-->  

Ange den här variabeln för att styra vilken typ av information som ska visas i fönstret för aktivitetssekvens. Använd följande värden för den här variabeln:

- `1`: Inkludera det aktuella steget och de totala stegen för förlopps texten. Till exempel **2 av 10**.
- `2`: Inkludera det aktuella steget, totalt antal steg och slutförda procent. Till exempel **2 av 10 (20% slutförd)**.
- `3`: Inkludera procent andelen slutförd. Till exempel **(20% slutförd)**.

### <a name="tsuefidrive"></a><a name="TSUEFIDrive"></a>TSUEFIDrive

Använd i egenskaperna för en FAT32-partition i **variabel** fältet. När aktivitetssekvensen identifierar den här variabeln förbereder den disken för över gång till UEFI innan datorn startas om. Mer information finns i avsnittet [om aktivitetssekvenser för att hantera BIOS till UEFI-konvertering](../deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

### <a name="workingdirectory"></a><a name="WorkingDirectory"></a>WorkingDirectory

*Gäller för steget [Kör kommando rad](task-sequence-steps.md#BKMK_RunCommandLine) .*

(indata)

Anger startkatalogen för en kommandoradsåtgärd. Det angivna katalog namnet får inte överskrida 255 tecken.

#### <a name="examples"></a>Exempel

- `C:\`  
- `%SystemRoot%`  


## <a name="deprecated-variables"></a>Föråldrade variabler

Följande variabler är föråldrade:

- **OSDAllowUnsignedDriver**: används inte när du distribuerar Windows Vista och senare operativ system
- **OSDBuildStorageDriverList**: gäller endast för Windows XP och windows Server 2003
- **OSDDiskpartBiosCompatibilityMode**: behövs bara när du distribuerar Windows XP eller windows Server 2003
- **OSDInstallEditionIndex**: krävs inte post-Windows Vista
- **OSDPreserveDriveLetter**: Mer information finns i [OSDPreserveDriveLetter](#osdpreservedriveletter)

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

> [!Important]
> Den här variabeln för aktivitetssekvensen är inaktuell.
>
> Under en operativ Systems distribution bestämmer Installationsprogrammet för Windows som standard den bästa enhets beteckningen (vanligt vis C:).

*Föregående beteende*: OSDPreverveDriveLetter-variabeln avgör om aktivitetssekvensen använder enhets beteckningen som registrerats i avbildnings filen (WIM) när en avbildning används. Ange värdet för den här variabeln till `false` att använda den plats som du anger för **mål** inställningen i steget **Använd operativ systemets** aktivitetssekvens. Mer information finns i [Använd OS-avbildning](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).


## <a name="see-also"></a>Se även

- [Aktivitetssekvenssteg](task-sequence-steps.md)
- [Använda variabler för aktivitetssekvens](using-task-sequence-variables.md)
- [Att tänka på när du planerar automatiseringsuppgifter](../plan-design/planning-considerations-for-automating-tasks.md)
