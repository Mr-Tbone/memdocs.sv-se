---
title: Tekniska för hands versioner
titleSuffix: Configuration Manager
description: Lär dig mer om den tekniska för hands versionen för att testa nya funktioner och funktioner i Configuration Manager.
ms.date: 06/25/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5dfa3b33a46166cfa4e1233eb71125696f5aa39d
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383146"
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

Installera en bas linje version i upp till ett år efter lanseringen. Använd den senaste bas linje versionen när du installerar en ny Technical Preview-webbplats.

- **Teknisk för hands version 2002**: Configuration Manager Technical Preview branch version 2002 är tillgänglig som både en uppdatering i konsolen och som en ny bas linje version.

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
<!-- - [title](2020/technical-preview-2006.md) <!--ID-->

Följande funktioner är tillgängliga med den senaste Configuration Manager Technical Preview-versionen:

### <a name="technical-preview-version-2006"></a>Teknisk för hands version 2006

- [Använd Företagsportal-appen på samhanterade enheter](2020/technical-preview-2006.md#bkmk_portal) <!--3601237-->
- [Förbättringar av tillgängliga appar via CMG](2020/technical-preview-2006.md#bkmk_availapp) <!--7033501-->
- [Intranät klienter kan använda en CMG program uppdaterings plats](2020/technical-preview-2006.md#bkmk_cmg-sup) <!--7102873-->
- [Förbättringar av aktivitetssekvenser via CMG](2020/technical-preview-2006.md#bkmk_osdcmg) <!--6983320-->
- [Hanterings insikter för att optimera för fjärranslutna arbetare](2020/technical-preview-2006.md#bkmk_wfhmi) <!--6982226-->
- [Förbättringar av VPN-gränser](2020/technical-preview-2006.md#bkmk_vpn) <!--7020519-->
- [Klient koppling: förbättringar av Configuration Manager åtgärder i administrations Center för Microsoft Endpoint Manager](2020/technical-preview-2006.md#bkmk_apps) <!--7518897-->
- [CMG-stöd för Endpoint Protection-principer](2020/technical-preview-2006.md#bkmk_epcmg) <!--4773948-->
- [Importera tidigare skapade Azure AD-program under klient kopplings registrering](2020/technical-preview-2006.md#bkmk_aad-app) <!--6479246-->
- [Förbättringar av klient uppgradering på en avgiftsbelagd anslutning](2020/technical-preview-2006.md#bkmk_meter) <!--6976145-->
- [Förbättringar av hantering av omstarter av enheter](2020/technical-preview-2006.md#bkmk_restart) <!--3601213-->
- [Förbättrat stöd för virtuella Windows-datorer](2020/technical-preview-2006.md#bkmk_wvd) <!--6527576-->
- [Direkt länkar till Configuration Manager community Hub-objekt](2020/technical-preview-2006.md#bkmk_deeplink) <!--4224406-->

> [!NOTE]
> Funktioner som var tillgängliga i en tidigare version av den tekniska för hands versionen är fortfarande tillgängliga i senare versioner. På samma sätt är funktioner som läggs till i Configuration Manager aktuella grenen tillgängliga i den tekniska förhands gransknings grenen.

## <a name="features-in-recent-technical-previews"></a>Funktioner i senaste tekniska för hands versionen

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

Följande funktioner släpptes med tidigare versioner av Configuration Manager Technical Preview-grenen eftersom aktuell gren version 2002:

> [!TIP]
> När en ny aktuell gren version är tillgänglig visas funktioner som är tillgängliga i den versionen i *den senaste artikeln om nyheter.* Mer information finns i [Nyheter i stegvisa versioner](../plan-design/changes/whats-new-incremental-versions.md#supported-versions).

### <a name="technical-preview-version-2005"></a>Teknisk för hands version 2005

- [Klientkoppling: Enhetstidslinje i administrationscentret](2020/technical-preview-2005.md#bkmk_timeline) <!--7141381-->
- [Klientkoppling: Installera ett program från administrationscentret](2020/technical-preview-2005.md#bkmk_apps) <!--6024389-->
- [Klientkoppling: CMPivot från administrationscentret](2020/technical-preview-2005.md#bkmk_cmpivot) <!--6024392-->
- [Klientkoppling: Kör skript från administrationscentret](2020/technical-preview-2005.md#bkmk_scripts) <!--6234688-->
- [VPN-avgränsnings typ](2020/technical-preview-2005.md#bkmk_vpn) <!--7020519-->
- [Azure AD-autentisering i Software Center](2020/technical-preview-2005.md#bkmk_availapp) <!--6935376-->
- [Installera och uppgradera klienten på en avgiftsbelagd anslutning](2020/technical-preview-2005.md#bkmk_meter) <!--6976145-->
- [Medie stöd för aktivitetssekvens för molnbaserad innehåll](2020/technical-preview-2005.md#bkmk_tsmedia) <!--6209223-->
- [Förbättringar av Cloud Management Gateway-cmdletar](2020/technical-preview-2005.md#bkmk_pwshcmg) <!--6978300-->
- [Community Hub och GitHub](2020/technical-preview-2005.md#community-hub-and-github) <!--3555935-->
- [Microsoft 365-appar för företag](2020/technical-preview-2005.md#bkmk_365_apps) <!--6298093-->
- [Rapportera installations-och uppgraderings problem till Microsoft](2020/technical-preview-2005.md#report-setup-and-upgrade-failures-to-microsoft) <!--5622909-->
- [Meddelande om förfallo datum för Azure AD-appens hemliga nyckel](2020/technical-preview-2005.md#bkmk_alertkey) <!--6386392-->
- [Förbättringar av stegen i BitLocker-aktivitetssekvensen](2020/technical-preview-2005.md#bkmk_tsbitlocker) <!--6995601-->
- [Förbättringar av rensnings verktyget för innehålls bibliotek](2020/technical-preview-2005.md#bkmk_content) <!--6887878-->
- [Ta bort kommando tolken under uppgraderingen av Windows 10 på plats](2020/technical-preview-2005.md#bkmk_ipucmd) <!--2837795-->

### <a name="technical-preview-version-2004"></a>Teknisk för hands version 2004

- [Microsoft Endpoint Manager-klient ansluter: information om ConfigMgr-klient](2020/technical-preview-2004.md#bkmk_mem) <!--6374854-->
- [Meddelanden från Microsoft](2020/technical-preview-2004.md#notifications-from-microsoft) <!--3953121-->
- [Kopiera identifierings data från-konsolen](2020/technical-preview-2004.md#bkmk_copydisco) <!--6890051-->
- [Förbättringar av CMPivot](2020/technical-preview-2004.md#improvements-to-cmpivot) <!--6518631-->
- [Stöd för PowerShell version 7](2020/technical-preview-2004.md#bkmk_pwsh7) <!--6023299-->
- [Förbättra för att formatera och partitionera disk steg för aktivitetssekvens](2020/technical-preview-2004.md#bkmk_osdpart) <!--6610288-->
- [Regler för insikter för operativ system distribution](2020/technical-preview-2004.md#bkmk_osdmi) <!--6982275-->
- [PowerShell-cmdletar för distributions typer för aktivitetssekvens](2020/technical-preview-2004.md#bkmk_osdpwsh) <!--7019342-->

### <a name="technical-preview-version-2003"></a>Teknisk för hands version 2003

- [Publicera Configuration Manager klienter till Microsoft Defender ATP via Microsoft Endpoint Manager-konsolen](2020/technical-preview-2003.md#bkmk_atp) <!--5691658-->
- [Spåra reparationer av konfigurations objekt](2020/technical-preview-2003.md#bkmk_track) <!--4261411 in 2002-->
- [Visa gränser grupper för enheter](2020/technical-preview-2003.md#bkmk_boundary) <!--6521835 in 2002-->
- [Ny feedback-guide](2020/technical-preview-2003.md#bkmk_feedback) <!--3180826-->
- [Förbättringar av Microsoft Edge Management-instrumentpanelen](2020/technical-preview-2003.md#bkmk_edge) <!--5907383-->
- [Förbättringar av CMPivot](2020/technical-preview-2003.md#bkmk_cmpivot) <!--6518631-->
- [Fråga efter feedback som skickats till Microsoft](2020/technical-preview-2003.md#bkmk_smile) <!--6488450-->
- [Ny SDK-metod för aktivitetssekvens](2020/technical-preview-2003.md#bkmk_tsapi) <!--6448458-->
- [Förbättringar av OS-distribution](2020/technical-preview-2003.md#bkmk_osd) <!--6452769-->

## <a name="features-in-previous-technical-previews"></a>Funktioner i föregående tekniska för hands versionerna

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

Följande funktioner släpptes med tidigare versioner av Configuration Manager Technical Preview-grenen. Dessa funktioner är tillgängliga i senare versioner, men är ännu inte tillgängliga i den aktuella grenen.

| Funktion        | Teknisk för hands version |
|----------------|---------------------------|
| Bifoga filer till feedback <!--3556011--> | [Teknisk för hands version 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Förbättringar av multicast-aktiverade distributions platser <!--3785535--> | [Teknisk för hands version 1908,2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Mallar för stegvis distribution <!--4961086--> | [Teknisk för hands version 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Fjärr styrning var som helst med hjälp av Cloud Management Gateway <!--4575930--> | [Teknisk för hands version 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Förbättringar av Community-hubb <!--3555935--> | [Teknisk för hands version 1906](2019/technical-preview-1906.md#bkmk_hub) |
| Förbättringar av Community-hubb <!--4224401--> | [Teknisk för hands version 1905](2019/technical-preview-1905.md#bkmk_hub) |
| Community-hubb och GitHub <!--3555935--> | [Teknisk för hands version 1904](2019/technical-preview-1904.md#community-hub-and-github) |
| Moln tjänster kostnads uppskattning <!--3555774--> | [Teknisk för hands version 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| Hämta rapporter från Community-hubb <!--3555936--> | [Teknisk för hands version 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Community-hubb <!--3556020, fka 1357766--> | [Teknisk för hands version 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
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
