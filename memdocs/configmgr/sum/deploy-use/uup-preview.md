---
title: UUP för hands version
titleSuffix: Configuration Manager
description: Instruktioner för för hands versionen av UUP-integrering
ms.date: 11/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c37fab775cdb90667ff1bc9f77dbbcaa1864b6f0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696794"
---
# <a name="uup-private-preview-instructions"></a>UUP privata för hands versions instruktioner

> [!Note]  
> Den här informationen är relaterad till en förhands gransknings funktion som kan ändras avsevärt innan den släpps kommersiellt. Microsoft lämnar inga garantier, uttryckliga eller underförstådda, avseende informationen som visas här.  

## <a name="introduction"></a>Introduktion

Den enhetliga uppdaterings plattformen (UUP) är den paket-och publicerings plattform som konsumenter och företags enheter använder för att ta emot uppdateringar från Windows Update för företag. Det privata för hands versions programmet UUP är för kunder som har kommit överens om att hjälpa Microsoft att validera användningen av UUP-uppdateringar i Configuration Manager för att lösa problem som kunder rapporterar med service perioder i dag. De här uppdateringarna är inte offentligt tillgängliga för närvarande.

Mer information om UUP finns i följande Windows blogg inlägg: [en uppdatering på vår Unified Update Platform (UUP)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/).

## <a name="benefits"></a>Fördelar

Windows 10 UUP-funktionen och kumulativa uppdateringar hjälper till att lösa flera problem som kunder rapporterar med service perioder i dag.

### <a name="feature-updates"></a>Funktionsuppdateringar

- Med en UUP funktions uppdatering bevarar Windows Update-processen funktioner på begäran (franska) och språk paket.

- Uppdatera direkt till den senaste nivån för säkerhets efterlevnad. Du behöver inte installera säkerhets uppdateringar direkt efter en funktions uppdatering. Microsoft publicerar en ny funktions uppdatering varje månad med den senaste kumulativa säkerhets uppdateringen. Du behöver inte hämta eller distribuera merparten av funktions uppdaterings innehållet varje månad. Du hämtar bara säkerhets uppdateringen som UUP delar med den kumulativa uppdateringen.

### <a name="cumulative-updates"></a>Kumulativa uppdateringar

- Kumulativa uppdateringar med UUP inkluderar service stack-uppdateringar (SJÄLVBETJÄNINGS) med kumulativa säkerhets uppdateringar per månad. Detta löser problem med att dirigera dessa två uppdateringar. Det ser till att underhålls stackens uppdateringar är på plats för att installera ackumulerade uppdateringar. Du behöver inte hantera och dirigera dessa relationer.

- Kumulativa uppdateringar med UUP gör att du kan distribuera franska och språk paket innehåll offline. Med det här beteendet kan användarna lägga till dem på begäran. Användarna behöver inte ladda ned från Internet, och du behöver inte ta reda på hur du förbereder det här innehållet.

## <a name="set-up"></a>Konfigurera

### <a name="1-send-your-wsus-id-to-microsoft"></a>1. skicka ditt WSUS-ID till Microsoft

Om du vill delta i UUP privata för hands version delar du ditt WSUS-ID med din UUP Preview-kontakt. Microsoft godkänner din WSUS-miljö i UUP Preview-programmet. Utan det här ID: t kan du inte se några UUP-uppdateringar förrän för hands versionen är offentlig.

Kör följande PowerShell-skript för att hämta ditt WSUS-ID:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

Egenskapen **MUUrl** ska vara `https://sws.update.microsoft.com` . Information om hur du ändrar det finns i lösningen i följande Support artikel: [WSUS-synkroniseringen Miss lyckas med SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception).

### <a name="2-update-configuration-manager"></a>2. uppdatera Configuration Manager

Gör följande ändringar i Configuration Managers platsen för att stödja för hands versionen av UUP:

#### <a name="diagnostics-and-usage-data-level"></a>Nivå för diagnostik-och användnings data

Överväg att öka Configuration Manager diagnostik-och data användnings nivå under för hands versionen. Med **fullständig** nivå kan Microsoft bättre analysera och felsöka problem med den här nya funktionen. Mer information finns i [nivåer för insamling av diagnostikdata för version 1906](../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906.md).

#### <a name="install-the-latest-update"></a>Installera den senaste uppdateringen

1. Uppdatera platsen med någon av följande uppdateringar:

    - Version 1902 med [Samlad uppdatering](https://support.microsoft.com/help/4500571)
    - [Version 1906](../../core/servers/manage/checklist-for-installing-update-1906.md)

    Mer information finns i [Installera uppdateringar i konsolen](../../core/servers/manage/install-in-console-updates.md).

2. Uppdatera klienter.  

    - Överväg att använda automatisk klient uppgradering för att förenkla den här processen. Mer information finns i [Uppgradera klienter](../../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

    - För att förhindra *onödigt nedladdning runt 6 GB* oanvänt innehåll till klienten uppdaterar du alla klienter som du riktar UUP uppdateringar till.

### <a name="3-update-windows-clients-to-a-supported-version"></a>3. uppdatera Windows-klienter till en version som stöds

För att UUP-uppdateringar ska installeras installerar du båda följande uppdateringar:

1. En speciell minimi nivå för ackumulerad månatlig.

2. En detaljerad icke-kumulativ, icke-säkerhetsuppdatering från Microsoft Update katalogen. Om du vill importera uppdateringen till Configuration Manager för distribution, se [Importera uppdateringar från Microsoft Update-katalogen](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog).

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>Versioner av Windows 10 och nödvändiga uppdateringar som stöds

| Windows 10-version | Lägsta kompatibilitetsnivå | Ytterligare katalog uppdatering |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10, version 1903** | RTM | 7 november 2019 [KB4529943](https://www.catalog.update.microsoft.com/search.aspx?q=4529943) |
| **Windows 10, version 1809** | 2019 augusti, [KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | 7 november 2019 [KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10, version 1803** | 2019 april, [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | 7 november 2019 [KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10, version 1709** | 2019 april, [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | 7 november 2019 [KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

> [!IMPORTANT]
> - Om du använder 12 november 2019-uppdateringar på klienten innan du tillämpar den 7 november 2019 ytterligare katalog uppdatering, kommer de Windows Update Agent ändringar som krävs för att stödja UUP att skrivas över. Om du vill reparera klienter i det scenariot installerar du den ytterligare katalog uppdateringen efter de 12 november 2019 uppdateringarna installeras.
> - Om du använder en funktions uppdatering för klienten måste du installera om den ytterligare katalog uppdateringen när uppgraderingen är klar.
> - För att göra det enklare att testa funktions uppdateringar importerar du uppdateringarna till Configuration Manager. Mer information finns i [Importera uppdateringar från Microsoft Update katalogen](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog). När funktions uppdateringen är klar visas den ytterligare katalog uppdateringen som **krävs**, vilket möjliggör automatisk distribution till operativ systemets version på högre nivå.

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4. Tillåt att klienter laddar ned delta innehåll när det är tillgängligt

Om du vill att UUP-uppdateringar ska laddas ned korrekt aktiverar du klient inställningen så att **klienter kan ladda ned delta innehåll när det är tillgängligt**. Med den här inställningen kan Configuration Manager låta Windows Update Agent (WUA) avgöra vilket innehåll som krävs för att ladda ned till klienter. Detta är i stället för standardvärdet där Configuration Manager-klienten laddar ned allt innehåll som är associerat med UUP-uppdateringen. När du aktiverar den här inställningen fastställer WUA det ytterligare innehåll som krävs från varje UUP uppdatering. Till exempel är endast de obligatoriska franska och språk paketen.

När du aktiverar den här inställningen påverkas inte hämtning av Server innehåll från Internet. Den gäller endast för klient hämtningar. Innan du distribuerar UUP-uppdateringar till klienter ska du använda den här inställningen för klienter som uppfyller de versioner som stöds för UUP. De nödvändiga klient uppdateringarna åtgärdar kompatibilitetsproblem för UUP-uppdateringar i WSUS och Configuration Manager.

Mer information om den här klient inställningen finns i [om klient inställningar-program uppdateringar](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)

### <a name="5-review-your-software-update-infrastructure"></a>5. granska din infrastruktur för program uppdatering

Innan du synkroniserar UUP-uppdateringar bör du gå igenom reglerna för automatisk distribution (ADR) och service planer. Om du inte vill att dessa uppdateringar ska distribueras automatiskt kan du ändra automatisk distribution för att filtrera ut dem. Mer information finns i [så här hittar du synkroniserade UUP-uppdateringar](#how-to-find-synced-uup-updates). Som standard distribuerar befintliga Service planer endast icke-UUP uppdateringar. Du kan ändra service planerna för att ändra det här beteendet.

Granska dina rapporter om efterlevnad och ändra vid behov. Om du till exempel mäter kompatibilitet för alla produkter ser du nu både UUP och kumulativa uppdateringar som inte är UUP. Enheterna rapporterar efterlevnad mot båda typerna av uppdateringar. Se till att dina Compliance-rapporter löser den här ändringen.

## <a name="enable-uup-and-start-testing"></a>Aktivera UUP och starta testning

### <a name="select-products-and-classifications-to-sync"></a>Välj de produkter och klassificeringar som ska synkroniseras

När du är redo att börja synkronisera UUP-uppdateringar och Microsoft har godkänt ditt WSUS-ID aktiverar du de nya produkterna:

1. [Synkronisera program uppdateringar](../get-started/synchronize-software-updates.md) för att fylla de nya produkterna.  

2. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .

3. Välj platsen på den högsta nivån, som är antingen en central administrations plats (ca) eller en fristående primär plats.

4. I menyfliksområdet väljer du **Konfigurera plats komponenter**och sedan **program uppdaterings plats**.

5. Växla till fliken **produkter** och välj en eller flera av följande produkter: 

    - **Windows 10 UUP Preview**
    - **Windows Server UUP Preview**

6. Växla till fliken **klassificeringar** och välj följande alternativ:  

    - **Säkerhets uppdateringar**: om du vill se KUMULATIVa UUP-uppdateringar  
    - **Uppgraderingar**: om du vill se UUP funktions uppdateringar  

7. Synkronisera program uppdateringar igen för att se de nya UUP-uppdateringarna.

### <a name="how-to-find-synced-uup-updates"></a>Så här hittar du synkroniserade UUP-uppdateringar

När du har synkroniserat UUP-uppdateringar i din miljö kan du söka efter dem i Configuration Manager-konsolen för att testa. Det finns två sätt att hitta för hands versions uppdateringar:

- Eftersom de här för hands versions uppdateringarna finns i en separat produkt använder du produkten för att filtrera för att hitta uppdateringarna. Använd service planens produkt filter för att distribuera antingen UUP eller icke-UUP funktions uppdateringar.  

- I noden **alla uppdateringar av program uppdateringar** och **alla Windows 10-uppdateringar** i **program varu biblioteket**finns det en ny valfri kolumn- **tagg**. Den här egenskapen är även tillgänglig som ett filter i automatisk distribution. Sök i det här fältet för UUP-uppdateringar `UUP` . Det är tomt för icke-UUP uppdateringar.  

### <a name="updates-available-during-preview"></a>Uppdateringar som är tillgängliga under för hands versionen

Mer information om alla Windows 10-uppdateringar som publicerats av Microsoft finns i [Windows 10 versions information](/windows/release-information/).

#### <a name="cumulative-updates-to-test"></a>Kumulativa uppdateringar som ska testas

Även om du kan se flera UUP-märkta uppdateringar som är tillgängliga, börjar du med uppdateringen **September 2019** (2019-09) eller en senare version. Exempel:

- 2019-09 kumulativ uppdatering för Windows 10 version 1809 för x64-baserade system (KB4512578)
- 2019-09 kumulativ uppdatering för Windows 10 version 1803 för x64-baserade system (KB4516058)
- 2019-09 kumulativ uppdatering för Windows 10 version 1709 för x64-baserade system (KB4516066)

#### <a name="feature-updates-to-test"></a>Funktions uppdateringar som ska testas

Även om du kan se flera UUP-märkta uppdateringar som är tillgängliga, börjar du med uppdateringen **September 2019** (2019-vara 09B) eller en senare version. Exempel:

- Funktions uppdatering för Windows 10, version 1809 x64 2019-vara 09B
- Funktions uppdatering för Windows 10, version 1803 x64 2019-vara 09B

## <a name="scenarios-to-test"></a>Scenarier som ska testas

### <a name="test-feature-updates"></a>Testa funktions uppdateringar

- Uppdatera direkt till din valda säkerhets kompatibilitetsnivå  

- Installera FODs och språk paket före uppdateringen. Se till att uppdateringen bevarar dessa komponenter.  

### <a name="test-cumulative-updates"></a>Testa ackumulerade uppdateringar

Under förhands granskningen ska klienterna vara kompatibla med UUP-typ uppdateringen för flera efterföljande uppdateringar. Det här testet hjälper dig att förstå det pågående beteendet.

### <a name="test-content"></a>Testa innehåll

Den första uppdateringen för varje huvud version (1809, 1803, 1709), arkitektur och språk kombination ser ut att vara stor. Den här storleken är både i antal filer och disk utrymme, jämfört med vad du tidigare såg med icke-UUP uppdateringar. Det extra innehållet är främst avsett för alla franska och språk paketen för kumulativa uppdateringar. För funktions uppdateringar finns det ytterligare mycket innehåll för den första uppdateringen.

För framtida kumulativa uppdateringar och funktions uppdateringar är mängden nytt innehåll som platsen laddar ned och distribuerar mycket mindre. UUP delar intelligentt alla franska och språk paket innehåll mellan uppdateringar. Det behöver inte ladda ned eller distribuera om det delade innehållet. Under för hands versionen är den här månatliga nedladdningen ungefär samma som storleken på de ackumulerade uppdateringarna i UUP-scenarier i Windows 10-versionerna 1709 och 1803. I Windows 10 version 1809 och senare är den stegvisa nedladdningen av den kumulativa uppdateringen mycket mindre varje månad.

När du tittar på det totala innehållet som hämtas och distribueras under en 12-månaders period för *icke-Express*bör Windows 10 version 1803 utan UUP vara ungefär samma som version 1809 med UUP. Det totala innehållet som hämtats och distribuerats över hela livs längd i versionen är mindre i version 1809 med UUP.

### <a name="supported-content-channels"></a>Innehålls kanaler som stöds

För för hands versionen testar du dina typiska verkliga scenarier. UUP stöder alla innehålls kanaler, inklusive:

- Windows-leverans optimering (göra)
  - När du använder det kontrollerar du att den är korrekt konfigurerad. Mer information finns i [optimera leverans av Windows 10-uppdateringar](optimize-windows-10-update-delivery.md).
- Configuration Manager peer-cache
- Windows BranchCache
- Använd alternativet **inget distributions paket** och klienterna Ladda ned direkt från Microsoft Update. Använd det här alternativet med leverans optimering.
- Alternativa innehålls leverantörer från tredje part

Mer information om innehålls kanaler finns i [optimera leverans av Windows 10-uppdateringar](optimize-windows-10-update-delivery.md).

<!-- TODO: Addlink to WSUS Perf documentation-->