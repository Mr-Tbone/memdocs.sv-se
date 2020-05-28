---
title: Övervaka anslutningsstatus
titleSuffix: Configuration Manager
description: Information om hur du övervakar anslutnings hälsa och enhets tillstånd för Skriv bords analys i Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: fdc15860f2d093a4c9c61b787ba0b780051d3f3d
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864879"
---
# <a name="monitor-connection-health"></a>Övervaka anslutningsstatus

Använd instrument panelen för **anslutningens hälso tillstånd** i Configuration Manager för att öka detalj nivån i kategorier efter enhets hälsa. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera noden **Skriv bords analys** och välj instrument panelen för **hälso tillstånd för anslutning** .  

[![Skärm bild av instrument panelen för Configuration Manager anslutningens hälso tillstånd](media/connection-health-dashboard.png)](media/connection-health-dashboard.png#lightbox)

När du först konfigurerar Desktop Analytics kanske dessa diagram inte visar fullständiga data. Det kan ta 2-3 dagar för aktiva enheter att skicka diagnostikdata till tjänsten Desktop Analytics, tjänsten för att bearbeta data och sedan synkronisera med Configuration Manager-platsen.<!-- 4098037 -->

## <a name="connection-details"></a>Anslutningsinformation

Den här panelen visar följande grundläggande information om anslutningen från Configuration Manager till Skriv bords analys:

- **Klient**organisations namn: namnet på Skriv bords analys anslutningen i noden **Azure-tjänster**

- **Mål samling**: samma *mål samling* som du angav när du anslöt Configuration Manager till Skriv bords analys. Den här samlingen innehåller alla enheter som Configuration Manager konfigurerar med inställningarna för ditt handels-ID och diagnostikdata. Det är en fullständig uppsättning enheter som Configuration Manager ansluter till Skriv bords analys tjänsten.

- **Riktade enheter**: alla enheter i mål samlingen, minus följande typer av enheter:

  - Inaktiverade
  - Ersatt
  - Inaktiv
  - Ohanterade
  - Enheter som kör LTSC-versioner (Long term Servicing Channel) av Windows 10
  - Enheter som kör Windows Server

    Mer information om dessa enhets tillstånd finns i [om klient status](../core/clients/manage/monitor-clients.md#bkmk_about).

    > [!Note]  
    > Configuration Manager uppladdningar till Desktop Analytics alla enheter i mål samlingen minus inaktive rad och föråldrade klienter.

- **Enheter som är berättigade till da**: antalet enheter som är mål minus enheter som inte är berättigade till Skriv bords analys. Till exempel enheter i mål samlingen som kör Windows Server eller Windows 10 långsiktig service Channel (LTSC).

## <a name="last-sync-details"></a>Senaste synkroniseringsinformation

Den här panelen visar när Configuration Manager synkroniseras med moln tjänsten för Skriv bords analys och hur många enheter som synkroniseras.

- **Synkroniserade enheter**: antalet kvalificerade enheter som Configuration Manager skickas till Skriv bords analys. Tjänsten innehåller enheterna i den just nu synliga ögonblicks bilden.

- **Senaste synkronisering av tjänst**: samma som den **senaste uppdaterade** tiden i Skriv bords analys portalen.

- **Nästa tjänst-synkronisering**: när du kan förväntar dig nästa dagliga ögonblicks bild i Skriv bords analys.

> [!Note]  
> När du först registrerar enheter i Desktop Analytics kan det ta flera dagar innan data laddas upp och bearbetas. Under den här tiden kan den **senaste synkroniserade informations** panelen visas som tom.
> Dessutom uppdateras inget av värdena i den här panelen automatiskt när du begär en ögonblicks bild på begäran. Mer information finns i [data svars tid](troubleshooting.md#data-latency).

Om du tycker att vissa enheter inte visas i Desktop Analytics kontrollerar du att enheterna stöds av Desktop Analytics. Mer information finns i [krav](overview.md#prerequisites).

## <a name="connection-health"></a>Anslutnings hälsa

I **anslutnings hälso** diagrammet visas antalet enheter i följande hälso tillstånd:  

- [Korrekt registrerad](#properly-enrolled): enheten visas i Skriv bords analys med en fullständig inventering
- [Det går inte att registrera](#unable-to-enroll): det finns ett spärr problem som förhindrar enhets registrering
- [Konfigurations varning](#configuration-alert): enheten visas inte i Skriv bords analys eller så visas en ofullständig inventering. Configuration Manager även identifierat ett problem med enhets registreringen.
- [Väntar på registrering](#awaiting-enrollment): Configuration Manager konfigurerade enheten, men den visas ännu inte i Skriv bords analys
- [Status väntar](#status-pending): Configuration Manager konfigurerar enheten fortfarande, eller så har den inte tillräckligt med data från enheten för att fastställa dess tillstånd
- [Data som saknas](#missing-data): Configuration Manager konfigurerade enheten, men Desktop Analytics har bara delar av data

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

Det totala antalet enheter i det här diagrammet ska vara detsamma som de enheter som är **berättigade till da** -värdet på panelen anslutnings information.

Välj sektorn i diagrammet för att öka detalj nivån till en lista över enheter med det aktuella läget. Mer information finns i [enhets lista](#device-list).

Välj kategori namnet i förklaringen för att ta bort eller lägga till det i diagrammet. Den här åtgärden hjälper till att zooma diagrammet så att du kan se de relativa storlekarna för mindre segment.

### <a name="properly-enrolled"></a>Korrekt registrerad

Enheten har följande attribut:

- En Configuration Manager-klient version 1902 eller senare  
- Det finns inga konfigurations fel  
- Skriv bords analys fick fullständiga diagnostikdata från enheten under de senaste 28 dagarna  
- Skriv bords analys har en fullständig inventering av enhetens konfiguration och installerade appar  

### <a name="unable-to-enroll"></a>Det gick inte att registrera

Configuration Manager identifierar ett eller flera blockerande problem som förhindrar enhets registrering. Mer information finns i listan över [enhets egenskaper för Skriv bords analys i Configuration Manager](#bkmk_config-issues).  

Configuration Manager-klienten är till exempel inte minst version 1902 (5.0.8790). Uppdatera klienten till den senaste versionen. Överväg att aktivera automatisk klient uppgradering för Configuration Managers platsen. Mer information finns i [Uppgradera klienter](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

> [!TIP]
> Det finns ett känt problem med den utökade säkerhets uppdateringen från april 2020 (ESU) för Windows 7 som orsakar att enheter rapporterar felet. Mer information finns i [versions anteckningar](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack).<!-- 7283186 -->

Från och med version 2002 kan du enklare identifiera konfigurations problem för klientens proxyserver på två områden:

- **Kontroll av slut punkts anslutning**: om klienterna inte kan komma åt en obligatorisk slut punkt visas en konfigurations avisering på instrument panelen. Öka detalj nivån för klienter som inte kan registrera sig för att se slut punkterna som klienterna inte kan ansluta till på grund av konfigurations problem. Mer information finns i [anslutnings kontroller för slut punkter](#endpoint-connectivity-checks).<!-- 4963230 -->

- **Anslutnings status**: om klienterna använder en proxyserver för att få åtkomst till Desktop Analytics visar Configuration Manager problem med proxyautentisering från klienter. Öka detalj nivån för att se klienter som inte kan registreras på grund av problem med proxyautentisering. Mer information finns i [anslutnings status](#connectivity-status).<!-- 4963383 -->

### <a name="configuration-alert"></a>Konfigurations avisering

Enheten visas inte i Skriv bords analys eller så visas en ofullständig inventering. Configuration Manager även identifierat ett problem med enhets registreringen. Mer information finns i listan över [enhets egenskaper för Skriv bords analys i Configuration Manager](#bkmk_config-issues).

Enheten har till exempel inte någon anslutning till tjänsten. Mer information finns i [Windows diagnostisk slut punkts anslutning](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>Väntar på registrering

Det finns inga diagnostikdata för den här enheten i Skriv bords analys. Det här problemet kan bero på att du nyligen har lagt till enheten i mål samlingen och att den ännu inte har skickat data. Det kan också betyda att enheten inte kommunicerar korrekt med tjänsten och att de senaste diagnostikdata är mer än 28 dagar gamla.

Kontrol lera att enheten kan kommunicera med tjänsten. Mer information finns i [slut punkter](enable-data-sharing.md#endpoints).  

### <a name="status-pending"></a>Status väntar

Configuration Manager konfigurerar fortfarande enheten, eller så har den inte tillräckligt med data från enheten för att fastställa dess tillstånd.

### <a name="missing-data"></a>Data som saknas

Configuration Manager har konfigurerat enheten, men det går inte att skapa en kompatibilitetskontroll med Desktop Analytics. Den har ingen fullständig data uppsättning för enhetens konfiguration (inventering) eller installerade appar (inventering).

Det här problemet åtgärdas ofta automatiskt när enheten försöker igen. Om den finns kvar ser du till att enheten kan kommunicera med tjänsten. Mer information finns i [slut punkter](enable-data-sharing.md#endpoints).  

## <a name="device-list"></a>Enhetslista

Om du vill se en detaljerad lista över enheter efter status börjar du med instrument panelen för **hälso tillstånd för anslutning** . Välj ett av segmenten på panelen **anslutnings hälsa** och gå nedåt till en lista över enheter i det här tillståndet. I den här vyn för anpassad enhet visas följande Skriv bords analys kolumner som standard:

- Konfiguration av kommersiellt ID
- Lägsta kompatibilitets uppdatering
- Deltagande i Windows-diagnostikdata
- Deltagande i Windows kommersiella data
- Anslutning till Windows diagnostisk slut punkt
- Anslutnings status (från och med version 2002)
- Kontroll av slut punkts anslutningar (från och med version 2002)

Dessa kolumner motsvarar de viktiga [kraven](overview.md#prerequisites) för att enheter ska kunna kommunicera med Desktop Analytics.

[![Skärm bild av det går inte att registrera enhets listan](media/device-list-unable-to-enroll.png)](media/device-list-unable-to-enroll.png#lightbox)

Välj en enhet om du vill se en fullständig lista över tillgängliga egenskaper i informations fönstret. Du kan också lägga till någon av dessa egenskaper som kolumner i enhets listan.

## <a name="device-properties"></a><a name="bkmk_config-issues"></a>Enhets egenskaper

Följande enhets egenskaper för Desktop Analytics är tillgängliga som kolumner i listan Configuration Manager enhet:

- [Kontroll av slut punkts anslutningar](#endpoint-connectivity-checks) (från och med version 2002)
- [Anslutnings status](#connectivity-status) (från och med version 2002)
- [Bedömnings konfiguration](#appraiser-configuration)  
- [Lägsta kompatibilitets uppdatering](#minimum-compatibility-update)  
- [Utbedömnings version](#appraiser-version)  
- [Senaste lyckade körning av bedömare](#last-successful-full-run-of-appraiser)  
- [Data insamling för bedömning](#appraiser-data-collection)  
- [Senaste lyckade körning av inventering](#last-successful-full-run-of-census)  
- [Insamling av inventerings data](#census-data-collection)  
- [Anslutning till Windows diagnostisk slut punkt](#windows-diagnostic-endpoint-connectivity)  
- [Kontrol lera diagnostikdata för slutanvändare](#check-end-user-diagnostic-data)  
- [Kontrol lera användar proxy](#check-user-proxy)  
- [Konfiguration av kommersiellt ID](#commercial-id-configuration)  
- [Deltagande i Windows kommersiella data](#windows-commercial-data-opt-in)  
- [Kontrol lera enhets namnet i diagnostikdata](#check-device-name-in-diagnostic-data)  
- [Konfiguration av DiagTrack-tjänsten](#diagtrack-service-configuration)  
- [DiagTrack-version](#diagtrack-version)  
- [Hämtning av SQM-ID](#sqm-id-retrieval)  
- [Unikt hämtning av enhets identifierare](#unique-device-identifier-retrieval)  
- [Deltagande i Windows-diagnostikdata](#windows-diagnostic-data-opt-in)  

Den vanligaste rutan för **registrerings blockerare och konfigurations aviseringar** på instrument panelen för anslutningens hälso tillstånd visar de egenskaper som enheterna oftast rapporterar som ett problem.

### <a name="endpoint-connectivity-checks"></a>Kontroll av slut punkts anslutning

Från och med version 2002,<!-- 4963230 --> för att identifiera problem med proxyautentisering utför klienterna anslutnings kontroller mot obligatoriska slut punkter. Om en klient inte kan komma åt en obligatorisk slut punkt visar den här egenskapen en numrerad lista över slut punkter som den inte kan ansluta till på grund av konfigurations problem med proxyservern. Jämför den här listan med den publicerade listan över [obligatoriska slut punkter](enable-data-sharing.md#endpoints).

### <a name="connectivity-status"></a>Anslutnings status

Från och med version 2002,<!-- 4963383 --> Om klienterna använder en proxyserver för att komma åt Desktop Analytics visar den här egenskapen problem med proxyautentisering. Den innehåller följande information som rör proxyautentisering:

- Statuskod
- Returkod

Du ser fel som liknar följande i logg filen:

`Error 407: Can't connect to Microsoft %s. Check your network/proxy settings`

Där `%s` är URL: en för en obligatorisk slut punkt.

Du kan också se icke-deterministiska fel meddelanden som inte behöver åtgärdas förrän enheterna har problem med registreringen. Ett exempel:

`This status is not related to proxy configuration, consider to investigate only if you are experiencing device enrollment or configuration alert issues.`

Mer information om hur du konfigurerar proxyservrar för användning med Desktop Analytics finns i [Proxy Server-autentisering](enable-data-sharing.md#proxy-server-authentication).

### <a name="appraiser-configuration"></a>Bedömnings konfiguration

<!--20,21-->
En bedömning är den Windows-komponent som motsvarar [kompatibilitetsinställningarna](enroll-devices.md#update-devices). Den bedömer appar och driv rutiner på enheten för kompatibilitet med den senaste versionen av Windows.

Om den här kontrollen lyckas konfigureras uppräknings komponenten korrekt på enheten.

Annars kan det Visa något av följande fel:

- Det går inte att konfigurera SetRequestAllAppraiserVersions (Device app Compatibility data insamling). Kontrol lera loggen för undantags informationen  

- Det går inte att konfigurera SetRequestAllAppraiserVersions (Device app Compatibility data insamling). Kontrol lera loggen för undantags informationen  

- Det går inte att skriva RequestAllAppraiserVersions till register nyckeln `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser` . Kontrol lera behörigheter  

Kontrol lera behörigheterna för den här register nyckeln. Kontrol lera att det lokala system kontot har åtkomst till den här nyckeln för att Configuration Manager-klienten ska ställas in.  

Mer information hittar du i M365AHandler. log på klienten.  

### <a name="minimum-compatibility-update"></a>Lägsta kompatibilitets uppdatering

<!--18,19,32-->
Kompatibilitetsrapporten (bedömare. dll) är inte installerad eller inaktuell på enheten. Den är äldre än minimi kravet för Skriv bords analys, 10.0.17763.

Installera den senaste kompatibilitetsrapporten. Mer information finns i [Compatibility updates](enroll-devices.md#update-devices).

### <a name="appraiser-version"></a>Utbedömnings version

Den här egenskapen visar den aktuella versionen av komponenten för bedömning på enheten. Den visar fil versionen på `%windir%\System32\appraiser.dll` , utan decimal tecken. Fil version 10.0.17763 visas till exempel som 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Senaste lyckade körning av bedömare

Den här egenskapen visar datum och tid då enheten senast körde en bedömning.

### <a name="appraiser-data-collection"></a>Data insamling för bedömning

<!--Appraiser run status-->
<!--22,33-->
Den här egenskapen visar det senaste resultatet från Windows som kör komponenten för bedömning.

Om det inte lyckas kan det Visa något av följande fel:

- Det går inte att samla in RunAppraiser (app Compatibility data). Mer information finns i loggarna  

- Data insamling för programkompatibilitet (CompatTelRunner. exe) avslutades med en felkod  

Mer information hittar du i M365AHandler. log på klienten.

Sök efter följande fil: `%windir%\System32\CompatTelRunner.exe` . Om den inte finns installerar du om de [uppdateringar](enroll-devices.md#update-devices)som krävs. Kontrol lera att ingen annan system komponent tar bort den här filen, till exempel en grup princip eller en tjänst för program mot skadlig kod.

Om filen M365AHandler. log på klienten innehåller något av följande fel:

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Du kan åtgärda felen genom att köra följande kommandon från en upphöjd Windows PowerShell-konsol på den berörda klienten:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Senaste lyckade körning av inventering

Den här egenskapen visar datum och tid då enheten senast körde inventering.

### <a name="census-data-collection"></a>Insamling av inventerings data

<!-- Census run status -->
<!--51,52-->
Inventering är den Windows-komponent som inventerar enheten. Dessa lager data används för att förstå enheten och dess konfiguration.

Den här egenskapen visar det senaste resultatet från Windows som kör inventerings komponenten.

Om det inte lyckas kan det Visa något av följande fel:

- Det går inte att samla in data om enheten och dess konfiguration (RunCensus). Kontrol lera loggen för undantags informationen  

- Det gick inte att hitta data insamlings verktyget för enheter och konfiguration (devicecensus. exe)  

Mer information hittar du i M365AHandler. log på klienten.

Sök efter följande fil: `%windir%\System32\DeviceCensus.exe` . Om den inte finns installerar du om de [uppdateringar](enroll-devices.md#update-devices)som krävs. Kontrol lera att ingen annan system komponent tar bort den här filen, till exempel en grup princip eller en tjänst för program mot skadlig kod.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Anslutning till Windows diagnostisk slut punkt

<!--12,15-->
Om den här kontrollen lyckas kan enheten ansluta till den anslutna användar upplevelsen och telemetri-slutpunkten (Vortex).

Annars kan det Visa något av följande fel:  

- Det går inte att ansluta till den anslutna användar upplevelsen och telemetri-slutpunkten (Vortex). Kontrol lera inställningarna för nätverk/proxy  

- Det går inte att kontrol lera anslutningen till den anslutna användar upplevelsen och telemetri-slutpunkten (CheckVortexConnectivity). Kontrol lera loggen för undantags informationen  

Enheter verifierar anslutningen med en GET-begäran till följande slut punkt baserat på operativ system version:

| OS-version | Slutpunkt |
|------------|----------|
| – Windows 10, version 1809 eller senare<br/>– Windows 10, version 1803 med den kumulativa uppdateringen för 2018-09 eller senare | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10, version 1803 *utan* ackumulerad uppdatering för 2018-09 eller senare | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, version 1709 eller tidigare | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 eller Windows 8,1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Kontrol lera att enheten kan kommunicera med tjänsten. Den här kontrollen validerar vissa men inte alla obligatoriska slut punkter. Mer information finns i [slut punkter](enable-data-sharing.md#endpoints).  

Mer information hittar du i M365AHandler. log på klienten.  

### <a name="check-end-user-diagnostic-data"></a>Kontrol lera diagnostikdata för slutanvändare

<!--1004-->
Om den här kontrollen inte lyckas har en användare valt en lägre Windows-diagnostikdata på enheten. Det kan också orsakas av ett grup princip objekt som står i konflikt. Mer information finns i [Windows-inställningar](enroll-devices.md#windows-settings).

Beroende på dina affärs behov kan du inaktivera användar val via grup principer. Använd inställningen för att **Konfigurera inställningar för att välja användar gränssnitt i telemetri**. Mer information finns i [Konfigurera Windows-diagnostikdata i din organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

### <a name="check-user-proxy"></a>Kontrol lera användar proxy

<!--30,35-->
Inställningen DisableEnterpriseAuthProxy är aktive rad som standard för Windows 7. För Windows 8,1-datorer anger Configuration Manager inställningen DisableEnterpriseAuthProxy till 0 (inte inaktive rad).

Den här egenskapen kan visa följande fel:

- Proxyautentisering är aktive rad. Ange DisableEnterpriseAuthProxy till 0 i`HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- Det går inte att söka efter status för proxyautentisering. Kontrol lera loggen för undantags informationen

Mer information hittar du i M365AHandler. log på klienten.  

Kontrol lera behörigheterna för den här register nyckeln. Kontrol lera att det lokala system kontot har åtkomst till den här nyckeln för att Configuration Manager-klienten ska ställas in. Det kan också orsakas av ett grup princip objekt som står i konflikt. Mer information finns i [Windows-inställningar](enroll-devices.md#windows-settings).  

### <a name="commercial-id-configuration"></a>Konfiguration av kommersiellt ID

<!--9, 11, 53-->
Microsoft använder ett unikt kommersiellt ID för att mappa information från enheter till din arbets yta i Desktop Analytics. När du integrerar Configuration Manager med Desktop Analytics frågar den automatiskt om det här ID: t för tjänsten. Configuration Manager ska automatiskt använda detta ID för klienter som du har angett för Skriv bords analys inställningar.

Om den här kontrollen lyckas konfigureras enheten korrekt med ett kommersiellt ID.

Annars kan det Visa något av följande fel:

- Det går inte att skriva CommercialId till register nyckeln `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` . Kontrol lera behörigheter  

- Det går inte att uppdatera CommercialId i register nyckeln `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection` . Kontrol lera loggen för undantags informationen  

- Ange rätt CommercialId-värde vid`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Mer information hittar du i M365AHandler. log på klienten.  

Kontrol lera behörigheterna för den här register nyckeln. Kontrol lera att det lokala system kontot har åtkomst till den här nyckeln för att Configuration Manager-klienten ska ställas in. Det kan också orsakas av ett grup princip objekt som står i konflikt. Mer information finns i [Windows-inställningar](enroll-devices.md#windows-settings).  

Det finns ett annat ID för enheten. Den här register nyckeln används av en grup princip. Det har företräde framför det ID som tillhandahålls av Configuration Manager.  

<a name="bkmk_ViewCommercialID"></a>Gör så här om du vill visa det kommersiella ID: t i Skriv bords analys portalen:

1. Gå till Skriv bords analys portalen och välj **anslutna tjänster** i den globala inställnings gruppen.  

2. I fönstret **anslutna tjänster** är fönstret **registrera enheter** valt som standard. I fönstret registrera enheter visar informations avsnittet din kommersiella ID-nyckel.  

[![Skärm bild av handels-ID i Skriv bords analys Portal](media/commercial-id.png)](media/commercial-id.png#lightbox)

> [!Important]  
> Hämta bara en **ny ID-nyckel** när du inte kan använda den aktuella. Om du återskapar det kommersiella ID: t [registrerar du dina enheter på nytt med det nya ID: t](enroll-devices.md#device-enrollment). Den här processen kan leda till förlust av diagnostikdata under över gången.  

### <a name="windows-commercial-data-opt-in"></a>Deltagande i Windows kommersiella data

<!--64-->
Den här egenskapen är speciell för enheter som kör Windows 7 eller Windows 8,1. Den kör liknande tester som [Windows-diagnostikdata](#windows-diagnostic-data-opt-in), förutom värdet CommercialDataOptIn.

### <a name="check-device-name-in-diagnostic-data"></a>Kontrol lera enhets namnet i diagnostikdata

<!--56,58-->
Om den här kontrollen lyckas konfigureras enheten korrekt för att dela enhets namnet.

Annars kan det Visa något av följande fel:

- Det går inte att söka efter enhets namnet som ska skickas till Microsoft som en del av Windows-diagnostikdata. Kontrol lera loggen för undantags informationen  

- Det går inte att skriva AllowDeviceNameInTelemetry till register nyckeln `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection` . Kontrol lera behörigheter  

Mer information hittar du i M365AHandler. log på klienten.  

Kontrol lera behörigheterna för den här register nyckeln. Kontrol lera att det lokala system kontot har åtkomst till den här nyckeln för att Configuration Manager-klienten ska ställas in. Det kan också orsakas av ett grup princip objekt som står i konflikt. Mer information finns i [Windows-inställningar](enroll-devices.md#windows-settings).  

Se till att en annan princip mekanism, till exempel grup princip, inte inaktiverar den här inställningen.

### <a name="diagtrack-service-configuration"></a>Konfiguration av DiagTrack-tjänsten

<!--44,45,50-->
Om den här kontrollen lyckas konfigureras DiagTrack-komponenten korrekt på enheten. Den lägsta version som krävs av Desktop Analytics är 10010586 (10.0.10586).

Annars kan det Visa något av följande fel:

- Komponenten för anslutna användar upplevelser och telemetri (DiagTrack. dll) är inaktuell. Kontrol lera krav  

    > [!TIP]
    > Det finns ett känt problem med den utökade säkerhets uppdateringen från april 2020 (ESU) för Windows 7 som orsakar att enheter rapporterar felet. Mer information finns i [versions anteckningar](../core/servers/deploy/install/release-notes.md#dawin7-diagtrack).<!-- 7283186 -->

- Det går inte att hitta komponenten för anslutna användar upplevelser och telemetri (DiagTrack. dll). Kontrol lera krav  

- Aktivera och starta tjänsten anslutna användar upplevelser och telemetri för att skicka data till Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Installera de senaste uppdateringarna. Mer information finns i [enhets uppdateringar](enroll-devices.md#update-devices).

Kontrol lera att tjänsten för **anslutna användar upplevelser och telemetri** på enheten körs.

### <a name="diagtrack-version"></a>DiagTrack-version

Den här egenskapen visar den aktuella versionen av komponenten ansluten användar upplevelse och telemetri på enheten. Den visar fil versionen på `%windir%\System32\diagtrack.dll` , utan decimal tecken. Fil version 10.0.10586 visas till exempel som 10010586.

### <a name="sqm-id-retrieval"></a>Hämtning av SQM-ID

<!--38-->
Den här egenskapen är främst avsedd för Windows 7-enheter. Den kan användas av senare OS-versioner som reserv identifierare för enheten.

Om åtgärden Miss lyckas kan följande fel visas:

- Det går inte att hämta Legacy-identifieraren för enhets telemetri (SQM-ID)

Mer information hittar du i M365AHandler. log på klienten.  

Se till att du inte har dubbletter av ID: n i din miljö. Till exempel om enheter har distribuerats med en OS-avbildning som inte är generaliserad.

### <a name="unique-device-identifier-retrieval"></a>Unikt hämtning av enhets identifierare

<!--54-->
Skriv bords analys använder Microsoft-konto tjänsten för en mer tillförlitlig enhets identitet.

Kontrol lera att tjänsten **inloggnings assistent för Microsoft-konto** inte är inaktive rad. Start typen ska vara **Manuell (utlösare start)**.

Om du vill inaktivera slut användar Microsoft-konto åtkomst använder du princip inställningar i stället för att blockera slut punkten. Mer information finns i [Microsoft-konto i företaget](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Deltagande i Windows-diagnostikdata

<!--8,40,55,62-->
Den här egenskapen kontrollerar att Windows är korrekt konfigurerat för att tillåta diagnostikdata. Den kontrollerar AllowTelemetry-värdet i följande register nycklar:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Kontrol lera behörigheterna för dessa register nycklar. Kontrol lera att det lokala system kontot har åtkomst till nycklarna för att den Configuration Manager klienten ska kunna ställas in. Det kan också orsakas av ett grup princip objekt som står i konflikt. Mer information finns i [Windows-inställningar](enroll-devices.md#windows-settings).  

Mer information hittar du i M365AHandler. log på klienten.  

## <a name="see-also"></a>Se även

[Felsöka Desktop Analytics](troubleshooting.md)
