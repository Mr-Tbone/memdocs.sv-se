---
title: Tekniska för hands versioner
titleSuffix: Configuration Manager
description: Lär dig mer om den tekniska för hands versionen för att testa nya funktioner och funktioner i Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76d1edf8598e1abd71b6fd1db7faffa1750110d4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129128"
---
# <a name="technical-preview-for-configuration-manager"></a>Teknisk för hands version för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln innehåller information om den månatliga Technical Preview-grenen för Configuration Manager. Den tekniska för hands versionen introducerar nya funktioner som Microsoft arbetar med. Den introducerar nya funktioner som ännu inte ingår i den aktuella grenen av Configuration Manager. Dessa funktioner kan slutligen tas med i en uppdatering av den aktuella grenen. Innan vi slutför funktionerna vill du testa dem och ge oss feedback.

Eftersom den här versionen är en teknisk för hands version kan detaljer och funktioner komma att ändras.

Den här informationen gäller för alla versioner av Configuration Manager Technical Preview-grenen. Den här artikeln innehåller en lista över alla nya funktioner tillsammans med den tekniska för hands versionen som den först visas i. Till exempel version **2001** för januari ( `01` ) av 2020 ( `20` ). Separata-artiklar som är dedikerade till varje för hands versions information.

Information om vad som är nytt i den *aktuella grenen* av Configuration Manager finns i [Nyheter i Configuration Manager stegvisa versioner](../plan-design/changes/whats-new-incremental-versions.md).

> [!Tip]
> Om du vill få ett meddelande när den här sidan uppdateras kopierar du och klistrar in följande URL i din RSS-feed läsare:`https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a>Krav och begränsningar

> [!IMPORTANT]
> Den tekniska för hands versionen är endast licensierad för användning i en labb miljö. Microsoft erbjuder kanske inte support tjänster och vissa funktioner kanske inte är tillgängliga i tekniska för hands versionerna. Dessutom kan tekniska för hands versions program ha minskat eller andra säkerhets-, sekretess-, tillgänglighets-, tillgänglighets-och Tillförlitlighets standarder i förhållande till kommersiellt tillhandahållen program vara.

För de flesta produkt krav använder du informationen i de konfigurationer som [stöds](../plan-design/configs/supported-configurations.md). Följande undantag gäller för den Technical Preview-grenen:

- Varje installation är aktiv i 90 dagar innan den blir inaktiv.

- Engelska är det enda språk som stöds.

- Det stöder endast följande kommando rads parametrar för installationen:

  - `/silent`
  - `/testdbupgrade`

- Tjänst anslutnings punkten installeras i onlineläge. Den har inte stöd för offline-läge.

- De separata artiklarna för varje version av den tekniska för hands versionen innehåller ytterligare begränsningar eller krav, efter vad som är tillämpligt.

- Följande funktioner stöds inte i grenen Technical Preview:

  - [Migrering](../migration/migrate-data-between-hierarchies.md) till eller från den här förhands gransknings grenen.

  - [Uppgradera](../servers/deploy/install/upgrade-to-configuration-manager.md) till den här förhands gransknings grenen.

  - [Site Recovery](../servers/manage/recover-sites.md) från CD. senaste mappen.<!--507106-->

- Det finns inget stöd för att uppdatera till aktuell gren från den här förhands gransknings grenen.

    > [!Note]
    > När uppdateringar är tillgängliga för en för hands version kan du fortfarande hitta och installera dem från noden **uppdateringar och underhåll** i Configuration Manager-konsolen. En video om uppgraderings processen i konsolen finns i [installera Configuration Manager uppdaterings paket](https://www.youtube.com/embed/KBd_EGFbUT8) på YouTube.com.

- Den har endast stöd för en fristående primär plats. Det finns inget stöd för en central administrations plats, flera primära platser eller sekundära platser.

Den tekniska för hands versionen av Configuration Manager stöder följande produkter och tekniker:

- Om inget annat anges stöder den Technical Preview-grenen samma versioner av SQL Server som den aktuella grenen. Mer information finns i [SQL Server-versioner som stöds](../plan-design/configs/support-for-sql-server-versions.md).

- -Platsen har stöd för upp till 10 klienter, vilket kan köra en [version som stöds av klienten](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).<!-- SCCMDocs#1656 -->

> [!Note]
> Inkludering av dessa produkter i det här innehållet innebär inte en förlängning av stöd för en version som ligger utanför support livs cykeln. Configuration Manager stöder inte produkter som ligger utanför support livs cykeln. Mer information finns i [Microsofts livs cykel princip](https://support.microsoft.com/lifecycle).

## <a name="install-and-update"></a><a name="bkmk_install"></a>Installera och uppdatera

Configuration Manager Technical Preview-grenen för labb användning skiljer sig från den Configuration Manager aktuella grenen för produktions användning.

Installera först en bas linje version av Technical Preview-grenen. När du har installerat en bas linje version använder du uppdateringar i konsolen för att uppdatera installationen med den senaste för hands versionen. Nya versioner av den tekniska för hands versionen är vanligt vis tillgängliga varje månad.

Microsoft stöder varje teknisk för hands version fram till tre efterföljande versioner. Till exempel när version 1908 lanserades, stöds inte längre version 1904. Versionerna 1905, 1906 och 1907 låg i stöd. När en bas linje faller utanför supporten stöds den fortfarande för att installera en ny Technical Preview-webbplats, förutsatt att du omedelbart uppdaterar till en version som stöds. Den äldre bas linjen stöds tills en ny bas linje version är tillgänglig. Uppdatera till den senaste tillgängliga versionen från bas linjen och upprepa sedan uppdaterings processen tills du har installerat den senaste tekniska för hands versionen.

> [!TIP]
> När du installerar en uppdatering för den tekniska för hands versionen uppdaterar du installationen av för hands versionen till den nya tekniska för hands versionen. En teknisk för hands installation har aldrig möjlighet att uppgradera till en aktuell gren installation. Den tar heller aldrig emot uppdateringar från den aktuella gren versionen.
>
> Det finns flera gånger under året, men det finns teknisk för hands versions gren och aktuella gren versioner med samma versions nummer. Det finns till exempel en teknisk för hands version 1910 och en aktuell gren version 1910.

### <a name="active-baseline-versions"></a>Aktiva bas linje versioner

Installera en bas linje version i upp till ett år efter lanseringen. Använd den senaste bas linje versionen när du installerar en ny Technical Preview-webbplats. Följande Configuration Manager-versioner av teknisk för hands version är tillgängliga som både uppdateringar i konsolen och nya bas linje versioner:

- **Teknisk för hands version 2007**

Hämta en bas linje version från [utvärderings centret](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a>Lämna feedback

Vi älskar att höra dina synpunkter om de nya funktionerna i den tekniska för hands versionen. Mer information finns i [produkt feedback](../understand/find-help.md#product-feedback).

Om du har idéer om nya funktioner som du vill se kan du berätta för oss! Skicka in nya idéer och rösta på idéerna av andra: [Configuration Manager UserVoice](https://configurationmanager.uservoice.com).

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a>Funktioner i den senaste versionen

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2007.md) <!--ID-->

Följande funktioner är tillgängliga med den senaste Configuration Manager Technical Preview-versionen:

### <a name="technical-preview-version-2008"></a>Teknisk för hands version 2008

- [Förhands granskning av samlings fråga](2020/technical-preview-2008.md#collection-query-preview) <!--7380401-->
- [Analysera SetupDiag-fel för funktions uppdateringar](2020/technical-preview-2008.md#bkmk_setupdiag) <!--4385028-->
- [Övervaka hälso tillstånd för hälsa](2020/technical-preview-2008.md#bkmk_health) <!--7699463-->
- [Vy för samlings utvärdering](2020/technical-preview-2008.md#bkmk_colleval) <!--6251274-->
- [Se storlek på aktivitetssekvens i-konsolen](2020/technical-preview-2008.md#bkmk_tssize) <!--7645732-->
- [Ta bort föråldrade diagnostikdata](2020/technical-preview-2008.md#bkmk_logs) <!--6503308-->
- [Importera objekt till aktuell mapp](2020/technical-preview-2008.md#bkmk_folder) <!--6601203-->

> [!NOTE]
> Funktioner som var tillgängliga i en tidigare version av den tekniska för hands versionen är fortfarande tillgängliga i senare versioner. På samma sätt är funktioner som läggs till i Configuration Manager aktuella grenen tillgängliga i den tekniska förhands gransknings grenen.

## <a name="features-in-recent-technical-previews"></a>Funktioner i senaste tekniska för hands versionen

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

Följande funktioner släpptes med tidigare versioner av Configuration Manager Technical Preview-grenen eftersom aktuell gren version 2006:

> [!TIP]
> När en ny aktuell gren version är tillgänglig visas funktioner som är tillgängliga i den versionen i *den senaste artikeln om nyheter.* Mer information finns i [Nyheter i stegvisa versioner](../plan-design/changes/whats-new-incremental-versions.md#supported-versions).

### <a name="technical-preview-version-2007"></a>Teknisk för hands version 2007

- [Klient anslutning: Visa maskin varu inventering i administrations Center för Microsoft Endpoint Manager](2020/technical-preview-2007.md#bkmk_mem) <!--6479284-->
- [Förbättringar av instrument panelen för klient data källor](2020/technical-preview-2007.md#bkmk_content) <!--7102084-->
- [Teckensnitt med fast bredd som nu används i vissa konsol områden](2020/technical-preview-2007.md#bkmk_font) <!--7632637-->
- [Hantera princip storlek för aktivitetssekvens](2020/technical-preview-2007.md#bkmk_tspol) <!--6888853-->
- [Förbättringar av enhets tids linjen i administrations centret](2020/technical-preview-2007.md#bkmk_timeline)<!--7141381-->

## <a name="features-in-previous-technical-previews"></a>Funktioner i föregående tekniska för hands versionerna

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

Följande funktioner släpptes med tidigare versioner av Configuration Manager Technical Preview-grenen. Dessa funktioner är tillgängliga i senare versioner, men är ännu inte tillgängliga i den aktuella grenen.

| Funktion        | Teknisk för hands version |
|----------------|---------------------------|
| Använd Företagsportal-appen på samhanterade enheter <!--3601237--> | [Teknisk för hands version 2006](2020/technical-preview-2006.md#bkmk_portal) |
| Förbättringar av tillgängliga appar via CMG <!--7033501--> | [Teknisk för hands version 2006](2020/technical-preview-2006.md#bkmk_availapp) |
| Klient koppling: förbättringar av Configuration Manager åtgärder i administrations Center för Microsoft Endpoint Manager <!--7518897--> | [Teknisk för hands version 2006](2020/technical-preview-2006.md#bkmk_apps) |
| Klientkoppling: Enhetstidslinje i administrationscentret <!--7141381--> | [Teknisk för hands version 2005](2020/technical-preview-2005.md#bkmk_timeline) |
| Klientkoppling: Installera ett program från administrationscentret <!--6024389--> | [Teknisk för hands version 2005](2020/technical-preview-2005.md#bkmk_apps) |
| Klientkoppling: CMPivot från administrationscentret <!--6024392--> | [Teknisk för hands version 2005](2020/technical-preview-2005.md#bkmk_cmpivot) |
| Klientkoppling: Kör skript från administrationscentret <!--6234688--> | [Teknisk för hands version 2005](2020/technical-preview-2005.md#bkmk_scripts) |
| Förbättringar av Cloud Management Gateway-cmdletar <!--6978300--> | [Teknisk för hands version 2005](2020/technical-preview-2005.md#bkmk_pwshcmg) |
| Rapportera installations-och uppgraderings problem till Microsoft <!--5622909--> | [Teknisk för hands version 2005](2020/technical-preview-2005.md#report-setup-and-upgrade-failures-to-microsoft) |
| Förbättringar av rensnings verktyget för innehålls bibliotek <!--6887878--> | [Teknisk för hands version 2005](2020/technical-preview-2005.md#bkmk_content) |
| Kopiera identifierings data från-konsolen <!--6890051--> | [Teknisk för hands version 2004](2020/technical-preview-2004.md#bkmk_copydisco) |
| Stöd för PowerShell version 7 <!--6023299--> | [Teknisk för hands version 2004](2020/technical-preview-2004.md#bkmk_pwsh7) |
| Ny feedback-guide <!--3180826--> | [Teknisk för hands version 2003](2020/technical-preview-2003.md#bkmk_feedback) |
| Fråga efter feedback som skickats till Microsoft <!--6488450--> | [Teknisk för hands version 2003](2020/technical-preview-2003.md#bkmk_smile) |
| Bifoga filer till feedback <!--3556011--> | [Teknisk för hands version 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Förbättringar av multicast-aktiverade distributions platser <!--3785535--> | [Teknisk för hands version 1908,2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Mallar för stegvis distribution <!--4961086--> | [Teknisk för hands version 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Fjärr styrning var som helst med hjälp av Cloud Management Gateway <!--4575930--> | [Teknisk för hands version 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Moln tjänster kostnads uppskattning <!--3555774--> | [Teknisk för hands version 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| Klient-based PXE responder service <!--3556018, fka 1357148--> | [Teknisk för hands version 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| PXE-nätverkets start stöd för IPv6 <!--3601254, fka 1269793--> |[Teknisk för hands version 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Använda Azure Active Directory <!--3607315, fka 1322145--> | [Teknisk för hands version 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Förbättringar av Tillgångsinformation <!--3601024, fka 1307390--> | [Teknisk för hands version 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>Se även

Mer information finns i följande artiklar:

- [Utvärdera Configuration Manager i ett labb](evaluate-with-lab-environment.md)
- [Nyheter i Configuration Manager inkrementella versioner](../plan-design/changes/whats-new-incremental-versions.md)
- [Introduktion till Configuration Manager](../understand/introduction.md)

> [!Tip]
> Mer information om aktuella gren funktioner som kräver medgivande för att aktivera finns i [för hands versions funktioner](../servers/manage/pre-release-features.md).
>
> Mer information om aktuella gren funktioner som du måste aktivera först finns i [Aktivera valfria funktioner från uppdateringar](../servers/manage/install-in-console-updates.md#bkmk_options).
