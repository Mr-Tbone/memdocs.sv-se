---
title: Felsöka ansluten cache
titleSuffix: Configuration Manager
description: Teknisk information för Microsoft Connected cache för att hjälpa dig att felsöka problem.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 121e0341-4f51-4d54-a357-732c26caf7c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a08b74552d5d17a737ec9e1802e10c87621f5b97
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126366"
---
# <a name="troubleshoot-microsoft-connected-cache-in-configuration-manager"></a>Felsök Microsoft Connected cache i Configuration Manager

Den här artikeln innehåller teknisk information om Microsoft Connected cache i Configuration Manager. Använd den för att felsöka problem som du kan ha i din miljö. Mer information om hur det fungerar och hur du använder det finns i [Microsoft Connected cache i Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).

> [!NOTE]
> Från och med version 1910 heter funktionen nu **Microsoft Connected cache**. Det kallades tidigare för leverans optimering i nätverket.

## <a name="verify"></a>Verifiera

När du installerar cache-servern för leverans optimering korrekt och konfigurerar klienterna på rätt sätt, hämtas de från den cache-server som är installerad på distributions platsen i stället för Internet.

Verifiera detta beteende [på en klient](#bkmk_verify-client) eller [på servern](#bkmk_verify-server).

### <a name="verify-on-a-client"></a><a name="bkmk_verify-client"></a>Verifiera på en klient

1. På klienten som kör Windows 10, version 1809 eller senare, laddar du ned moln hanterat innehåll. Mer information om vilka typer av innehåll som anslöt till cacheminnet finns i [Verifiera ansluten cache](../../../plan-design/hierarchy/microsoft-connected-cache.md#verify).

2. Öppna PowerShell och kör följande kommando:`Get-DeliveryOptimizationStatus`

Till exempel:

```PowerShell
PS C:\> Get-DeliveryOptimizationStatus

FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
FileSize                    : 549064
TotalBytesDownloaded        : 549064
PercentPeerCaching          : 0
BytesFromPeers              : 0
BytesFromHttp               : 0
Status                      : Caching
Priority                    : Background
BytesFromCacheServer        : 549064
BytesFromLanPeers           : 0
BytesFromGroupPeers         : 0
BytesFromInternetPeers      : 0
BytesToLanPeers             : 0
BytesToGroupPeers           : 0
BytesToInternetPeers        : 0
DownloadDuration            : 00:00:00.0780000
HttpConnectionCount         : 2
LanConnectionCount          : 0
GroupConnectionCount        : 0
InternetConnectionCount     : 0
DownloadMode                : 99
SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                              atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
NumPeers                    : 0
PredefinedCallerApplication : WU Client Download
ExpireOn                    : 9/6/2019 8:36:19 AM
IsPinned                    : False
```

Observera att `BytesFromCacheServer` attributet inte är noll.

Om klienten inte har kon figurer ATS korrekt, eller om cache-servern inte är korrekt installerad, kommer leverans optimerings klienten tillbaka till den ursprungliga moln källan. Sedan kommer BytesFromCacheServer-attributet att vara noll.

### <a name="verify-on-the-server"></a><a name="bkmk_verify-server"></a>Verifiera på servern

Kontrol lera först att register egenskaperna är korrekt konfigurerade: `HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache` . Till exempel är enhetens cache-plats `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294` , där `PrimaryDrivesInput` kan vara flera enheter, till exempel `C,D,E` .

Använd sedan följande metod för att simulera en begäran om klient hämtning till servern med de obligatoriska rubrikerna.

1. Öppna ett 64-bitars PowerShell-fönster som administratör.
2. Kör följande kommando och ersätt namnet eller IP-adressen för servern för `<DoincServer>` :

```PowerShell
Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
```

Utdata ser ut ungefär som i följande exempel:

```PowerShell
PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


StatusCode        : 200
StatusDescription : OK
Content           : {71, 73, 70, 56...}
RawContent        : HTTP/1.1 200 OK
                    X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                    .p,1567797125.cds058.se2.p
                    X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                    t2.p,1567797125.cds058.se2.p], [X-CCC,
                    cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                    [X-CID, 100], [Accept-Ranges, bytes]...}
RawContentLength  : 969710
```

Följande attribut indikerar att det är klart:

- `StatusCode : 200`
- `StatusDescription : OK`

## <a name="log-files"></a>Loggfiler

- Installations logg för ARR:`%temp%\arr_setup.log`

- Server installations logg för cachelagring: `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` på distributions platsen och `DistMgr.log` på plats servern

- Drift loggar i IIS: som standard`%SystemDrive%\inetpub\logs\LogFiles`

- Kör cache-serverns operativa logg:`C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > I den här loggen kan du använda den här loggen för att identifiera anslutnings problem med Microsoft-molnet.

## <a name="setup-error-codes"></a>Installations fel koder

När Configuration Manager installerar den anslutna cache-komponenten på distributions platsen, visas de möjliga fel koder som kan uppstå i följande tabell:

| Felkod | Felbeskrivning |
|------------|-------------------|
| 0x00000000 | Klart |
| 0x00000BC2 | Lyckades, omstart krävs |
| 0x00000643 | Allmänt installations problem |
| 0x00D00001 | Det går bara att köra installations programmet för anslutna cacheminnen om Internet Information Services (IIS) har installerats |
| 0x00D00002 | Det går bara att köra installations programmet för anslutna cacheminnen om en "standard webbplats" finns på servern |
| 0x00D00003 | Du kan inte installera den anslutna cachen om du redan har installerat programbegärans dirigering (ARR) |
| 0x00D00004 | Det går bara att köra installations programmet för anslutna cache om ARR (Application Request routing) har installerats av Install.ps1-skriptet |
| 0x00D00005 | Installationen av den anslutna cachen kräver en PowerShell-session som körs som administratör |
| 0x00D00006 | Det går bara att köra installations programmet för anslutna cacheminnen från en 64-bitars PowerShell-miljö |
| 0x00D00007 | Det går bara att köra installations programmet för anslutna cacheminnen på en Windows Server |
| 0x00D00008 | Fel: antalet angivna cache-enheter måste matcha antalet angivna procent andelar för cache-enheten |
| 0x00D00009 | Failure: ett giltigt ID för cache-nod måste anges |
| 0x00D0000A | Failure: en giltig cache-enhet måste anges |
| 0x00D0000B | Det gick inte att ange en giltig storlek procent för cache-enhet måste anges |
| 0x00D0000C | Ett problem: en giltig cachestorlek i procent eller cache-hårddisk storlek i GB måste anges |
| 0x00D0000D | Det gick inte att ange en giltig storlek för cache-enheten och cache-enhetens storlek i GB kan inte båda anges |
| 0x00D0000E | Fel: antalet angivna cache-enheter måste matcha antalet cache-enheter i GB som anges |
| 0x00D0000F | Problem: det gick inte att säkerhetskopiera applicationhost.config filen från $AppHostConfig till $AppHostConfigDestinationName |
| 0x00D00010 | Problem: det gick inte att säkerhetskopiera standard webbplatsen web.config filen från $WebsiteConfigFilePath till $WebConfigDestinationName |
| 0x00D00011 | Fel: ett undantag inträffade i SetupARRWebFarm.ps1 |
| 0x00D00012 | Fel: ett undantag inträffade i SetupARRWebFarmRewriteRules.ps1 |
| 0x00D00013 | Fel: ett undantag inträffade i SetupARRWebFarmProperties.ps1 |
| 0x00D00014 | Fel: ett undantag inträffade i SetupAllowableServerVariables.ps1 |
| 0x00D00015 | Fel: ett undantag inträffade i SetupFirewallRules.ps1 |
| 0x00D00016 | Fel: ett undantag inträffade i SetupAppPoolProperties.ps1 |
| 0x00D00017 | Fel: ett undantag inträffade i SetupARROutboundRules.ps1 |
| 0x00D00018 | Fel: ett undantag inträffade i SetupARRDiskCache.ps1 |
| 0x00D00019 | Fel: ett undantag inträffade i SetupARRProperties.ps1 |
| 0x00D0001A | Fel: ett undantag inträffade i SetupARRHealthProbes.ps1 |
| 0x00D0001B | Fel: ett undantag inträffade i VerifyIISSItesStarted.ps1 |
| 0x00D0001C | Fel: ett undantag inträffade i SetDrivesToHealthy.ps1 |
| 0x00D0001D | Fel: ett undantag inträffade i VerifyCacheNodeSetup.ps1 |
| 0x00D0001E | Du kan inte installera den anslutna cachen om standard webbplatsen inte finns på port 80 |
| 0x00D0001F | Problem: allokeringen av cache-enheten i procent får inte överstiga 100 |
| 0x00D00020 | Failure: allokeringen av cache-enheten i GB får inte överskrida enhetens lediga utrymme |
| 0x00D00021 | Failure: allokeringen av cache-enheten i procent måste vara större än 0 |
| 0x00D00022 | Failure: allokeringen av cache-enheten i GB måste vara större än 0 |
| 0x00D00023 | Fel: ett undantag inträffade i RegisterScheduledTask_CacheNodeKeepAlive |
| 0x00D00024 | Fel: ett undantag inträffade i RegisterScheduledTask_Maintenance |
| 0x00D00025 | Fel: ett undantag uppstod vid inställning av reglerna för omskrivning för HTTPS-servergrupp: $FarmName |
| 0x00D00026 | Fel: ett undantag uppstod vid inställning av omskrivnings reglerna för HTTP-servergruppen: $FarmName |
| 0x00D00027 | Du kan inte installera den anslutna cachen eftersom det inte gick att installera den beroende program varan för programbegäran (ARR). Se logg filen som finns på% Temp% \ arr_setup. log |

## <a name="iis-configurations"></a>IIS-konfigurationer

Installationen av gör cache-servern gör flera ändringar i IIS-konfigurationen på distributions platsen.

### <a name="application-request-routing"></a>Routning av programbegäran

Kör cache-servern installerar och konfigurerar IIS [-programbegäran routning (arr)](https://www.iis.net/downloads/microsoft/application-request-routing). För att undvika potentiella konflikter kan distributions platsen inte redan ha den här komponenten installerad.

### <a name="allowed-server-variables"></a>Tillåtna servervariabler

När du har installerat kör cache-servern har standard webbplatsen följande *lokala* servervariabler:

- HTTP_HOST
- QUERY_STRING
- X-KOPIA
- X-CID
- X-DOINC-UTGÅENDE

### <a name="rewrite-rules"></a>Skriv om regler

Den gör cache-servern lägger till följande omskrivnings regler:

#### <a name="inbound-rewrite-rules"></a>Regler för inkommande omskrivning

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### <a name="outbound-rewrite-rules"></a>Regler för utgående omskrivning

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

## <a name="manage-server-resources"></a>Hantera Server resurser

Disk utrymme som krävs för varje server-cache kan variera beroende på organisationens uppdaterings krav. 100 GB ska vara tillräckligt med utrymme för att cachelagra följande innehåll:

- En funktions uppdatering
- Två till tre månaders kvalitet och Microsoft 365 uppdateringar av appar
- Microsoft Intune appar och appar för Windows-Inkorgen

Server-cachen ska inte förbruka mycket system minne eller processor tid. När du har installerat kör cache-servern kan du analysera loggfilerna för IIS och ARR om du upptäcker betydande process-eller minnes resursförbrukning.

Om IIS-och ARR-loggfilerna tar upp för mycket utrymme på servern finns det flera metoder som du kan använda för att hantera loggfilerna. Mer information finns i [Hantera IIS-logg File Storage](https://docs.microsoft.com/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview).

## <a name="see-also"></a>Se även

[Microsoft Connected cache i Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md)
