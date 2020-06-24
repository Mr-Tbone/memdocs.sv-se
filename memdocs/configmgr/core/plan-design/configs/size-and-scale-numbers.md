---
title: Storlek och skala
titleSuffix: Configuration Manager
description: Fastställ antalet plats system roller och platser som du behöver för att stödja enheterna i din miljö.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5109ababd00011784618f9c989e1d2b756a322d9
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715636"
---
# <a name="size-and-scale-numbers-for-configuration-manager"></a>Antal och gränsvärden för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Varje Configuration Manager-distribution har ett maximalt antal platser, plats system roller och enheter som den kan stödja. De här talen varierar beroende på hierarkins struktur, vilka typer och antalet platser du använder samt de plats system roller som du distribuerar. Informationen i den här artikeln kan hjälpa dig att avgöra hur många plats system roller och platser som du behöver stöd för de enheter som du förväntar dig att hantera.

Mer information finns i följande artiklar:

- [Rekommenderad maskinvara](recommended-hardware.md)
- [Operativsystem som stöds för platssystemservrar](supported-operating-systems-for-site-system-servers.md)  
- [Operativsystem som stöds för klienter och enheter](supported-operating-systems-for-clients-and-devices.md)
- [Plats och krav för platssystem](site-and-site-system-prerequisites.md)

Dessa support nummer baseras på användning av den rekommenderade maskin varan för Configuration Manager. De är också baserade på standardinställningarna för alla tillgängliga Configuration Manager-funktioner. När du inte använder den rekommenderade maskin varan eller använder mer aggressiva anpassade inställningar kan prestandan för plats system försämras. Plats systemen kanske inte uppfyller de angivna support nivåerna. (Ett exempel på mer aggressiva klient inställningar är att köra maskin-eller program varu inventering oftare än standardvärdena var sjunde dag.)

## <a name="site-types"></a><a name="bkmk_SiteSystemScale"></a>Plats typer  

### <a name="central-administration-site"></a>Central administrationsplats  

- En central administrations plats har stöd för upp till 25 underordnade primära platser.  

### <a name="primary-site"></a>Primär plats  

- Varje primär plats har stöd för upp till 250 sekundära platser.  

- Antalet sekundära platser per primär plats baseras på kontinuerligt anslutna och tillförlitliga Wide Area Network WAN-anslutningar. För platser som har färre än 500 klienter bör du överväga en distributions plats i stället för en sekundär plats.  

  Information om hur många klienter och enheter en primär plats har stöd för finns i [klient nummer för platser och hierarkier](#bkmk_clientnumbers).  

### <a name="secondary-site"></a>Sekundär plats  

- Sekundära platser har inte stöd för underordnade platser.  

## <a name="site-system-roles"></a><a name="bkmk_roles"></a>Plats system roller

### <a name="application-catalog-web-service-point"></a>Webb service punkt för program katalog  

> [!Important]
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- Du kan installera flera instanser av Programkatalog-webbtjänstens plats på primära platser.  

### <a name="application-catalog-website-point"></a>Plats för program katalog  

> [!Important]
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- Du kan installera flera instanser av Programkatalog webbplats på primära platser.  

### <a name="cloud-management-gateway"></a><a name="bkmk_cmg"></a>Cloud Management Gateway

- Du kan installera flera instanser av CMG (Cloud Management Gateway) på primära platser eller på den centrala administrations platsen.  

    > [!Tip]  
    > Skapa CMG på den centrala administrations webbplatsen i en hierarki.  

  - En CMG stöder en till 16 virtuella dator instanser (VM) i Azure-molnet.  

  - Varje CMG VM-instans stöder 6 000 samtidiga klient anslutningar. När CMG är under hög belastning på grund av mer än det antal klienter som stöds, hanterar den fortfarande begär Anden, men det kan uppstå en fördröjning.  

Mer information finns i CMG- [prestanda och skalning](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale)

### <a name="cloud-management-gateway-connection-point"></a>Anslutning punkt för moln hanterings-Gateway

- Du kan installera flera instanser av CMG-anslutnings punkten på primära platser.  

- En CMG-anslutnings punkt har stöd för en CMG med upp till fyra VM-instanser. Om CMG har fler än fyra VM-instanser lägger du till en andra CMG-kopplings punkt för belastnings utjämning. En CMG med 16 VM-instanser ska länkas med fyra CMG-anslutnings punkter.

Mer information finns i CMG- [prestanda och skalning](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale)

> [!NOTE]
> När du överväger maskin varu kraven för CMG-anslutnings punkten, se [Rekommenderad maskin vara för fjärrplatsens system servrar](recommended-hardware.md#bkmk_RemoteSiteSystem).<!-- SCCMDocs#2276 -->

### <a name="distribution-point"></a>Distributionsplats  

- Distributions platser per plats:  

  - Varje primär och sekundär plats har stöd för upp till 250 distributions platser.  

  - Varje primär och sekundär plats har stöd för upp till 2000 ytterligare distributions platser som är konfigurerade som mottagar distributions platser. En enda primär plats stöder **till exempel**2250 distributions platser när 2000 av dessa distributions platser är konfigurerade som mottagar distributions platser.  

  - Varje distributions plats stöder anslutningar från upp till 4 000 klienter.  

  - En mottagar distributions plats fungerar som en klient när den kommer åt innehåll från en käll distributions plats.  

- Varje primär plats har stöd för en kombinerad summa på upp till 5 000 distributions platser. Den här summan omfattar alla distributions platser på den primära platsen och alla distributions platser som tillhör den primära platsens underordnade sekundära platser.  

- Varje distributions plats har stöd för en kombinerad summa på upp till 10 000 paket och program.  

> [!WARNING]  
> Det faktiska antalet klienter som en distributions plats har stöd för beror på nätverkets hastighet och maskin varu konfigurationen på servern.  
>
> Antalet mottagar distributions platser som en käll distributions plats har stöd för beror på nätverks hastigheten och maskin varu konfigurationen på käll distributions platsen. Men det här antalet påverkas också av mängden innehåll som du har distribuerat. Detta beror på att, till skillnad från klienter som normalt kommer åt innehåll vid olika tidpunkter under en distribution, så begär alla mottagar distributions platser på samma gång. Mottagar distributions platser kan begära allt tillgängligt innehåll, inte bara det innehåll som är tillämpligt för dem. När du placerar en hög bearbetnings belastning på en käll distributions plats kan det uppstå oväntade fördröjningar när innehållet distribueras till mål distributions platserna.  

### <a name="fallback-status-point"></a>Status för återställningsplats  

- Varje återställnings status plats har stöd för upp till 100 000 klienter.  

### <a name="management-point"></a>Hanteringsplats  

- Varje primär plats har stöd för upp till 15 hanterings platser.  

    > [!TIP]  
    > Installera inte hanterings platser på servrar som finns i en långsam länk från den primära plats servern eller plats databas servern.  

- Varje sekundär plats har stöd för en enda hanterings plats som måste installeras på den sekundära plats servern.  

Information om hur många klienter och enheter som en hanterings plats har stöd för finns i avsnittet [hanterings platser](#bkmk_mp) .  

> [!NOTE]
> Om du aktiverar hanterings platsen så att den har stöd för en [Gateway för moln hantering](../../clients/manage/cmg/plan-cloud-management-gateway.md), är det Internetbaserade klient förfrågningar per normal. Storleks vägledningen för en hanterings plats påverkar inte om den fungerar lokalt eller på Internetbaserade klienter.

### <a name="software-update-point"></a>Programuppdateringsplats  

Använd följande rekommendationer som bas linje. Den här bas linjen hjälper dig att fastställa information för den kapacitets planering för program uppdateringar som är lämpligt för din organisation. De faktiska kapacitets kraven kan skilja sig från rekommendationerna som anges i den här artikeln beroende på följande kriterier:

- Din speciella nätverks miljö
- Den maskin vara som du använder som värd för program uppdaterings platsens plats system
- Antalet hanterade klienter
- De andra plats system rollerna som är installerade på servern  

> [!NOTE]
> Om du aktiverar program uppdaterings platsen för att ha stöd för en [Gateway för moln hantering](../../clients/manage/cmg/plan-cloud-management-gateway.md), är det Internetbaserade klient förfrågningar per normal. Storleks vägledningen för en program uppdaterings plats ändrar inte om den fungerar lokalt eller på Internetbaserade klienter.

#### <a name="capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> Kapacitetsplanering för programuppdateringsplatsen  

Antalet klienter som stöds beror på vilken version av Windows Server Update Services (WSUS) som körs på program uppdaterings platsen. Det beror också på om program uppdaterings platsens plats system roll finns i en annan plats system roll:  

- Program uppdaterings platsen har stöd för upp till 25 000 klienter när WSUS körs på program uppdaterings plats servern och program uppdaterings platsen samexisterar med en annan plats system roll.  

- Program uppdaterings platsen har stöd för upp till 150 000 klienter när en fjärrserver uppfyller WSUS-kraven, men WSUS används med Configuration Manager och du konfigurerar följande inställningar:

  IIS-programpooler:

  - Öka WsusPool Queue Length till 2000
  - Öka WsusPool privata minnes gräns gånger eller ange 0 (obegränsat). Om standard gränsen till exempel är 1 843 200 KB, ökar du den till 7 372 800. Mer information finns i det här [blogg inlägget för Configuration Manager Support Team](https://www.phoenixtekk.com/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    Mer information om maskin varu krav för program uppdaterings platsen finns i [Rekommenderad maskin vara för plats system](recommended-hardware.md#bkmk_ScaleSieSystems).  

#### <a name="capacity-planning-for-software-updates-objects"></a><a name="bkmk_sum-capacity-obj"></a>Kapacitets planering för program uppdaterings objekt  

Använd följande kapacitets information för att planera för program uppdaterings objekt:  

- **Gränsen på 1000 program uppdateringar i en distribution** – begränsa antalet program uppdateringar till 1000 för varje program uppdaterings distribution. När du skapar en automatisk distributions regel (ADR) anger du ett villkor som begränsar antalet program uppdateringar. ADR Miss lyckas när de angivna kriterierna returnerar fler än 1000 program uppdateringar. Kontrol lera status för ADR från noden **regler för automatisk distribution** i Configuration Manager-konsolen. När du distribuerar program uppdateringar manuellt ska du inte välja fler än 1000 uppdateringar att distribuera.  

  Begränsa också antalet program uppdateringar till 1000 i en konfigurations bas linje. Mer information finns i [skapa konfigurations bas linjer](../../../compliance/deploy-use/create-configuration-baselines.md).

- **Gräns för 580 säkerhets omfattningar för regler för automatisk distribution** -<!--ado 4962928-->
Begränsa antalet säkerhets omfattningar i regler för automatisk distribution (automatisk distribution) till mindre än 580. När du skapar en ADR läggs de säkerhets omfattningar som har åtkomst till den automatiskt. Om du har angett fler än 580 säkerhets omfattningar kommer inte ADR att köras och ett fel loggas i RuleEngine. log.

### <a name="sms-provider"></a>SMS-provider

<!-- SCCMDocs#1958 -->

Varje instans av SMS-providern stöder samtidiga anslutningar från flera begär Anden. De enda begränsningarna för dessa anslutningar är antalet Server anslutningar som är tillgängliga för Windows och de tillgängliga resurserna på servern för att betjäna anslutnings begär Anden.

Mer information finns i [Planera för SMS-providern](../hierarchy/plan-for-the-sms-provider.md).

## <a name="client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a>Klient nummer för platser och hierarkier

Använd följande information för att avgöra hur många klienter och vilka typer av klienter du kan stödja på en plats eller i en hierarki.  

### <a name="hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a>Hierarki med en central administrations plats

En central administrations plats har stöd för ett totalt antal enheter som innehåller upp till antalet enheter som listas för följande tre grupper:  

- 700 000 Windows-datorer. Se även stöd för [inbäddade enheter](#embedded).

- 25 000 enheter som kör Mac och Windows CE 7,0  

- 100 000 enheter som du hanterar med lokal hantering av mobila enheter (MDM)

I en hierarki kan du till exempel stödja 700 000 Station ära datorer, upp till 25 000 Mac och Windows CE 7,0-enheter och upp till 100 000 enheter som hanteras av lokal MDM. Den här hierarkin stöder totalt 825 000 enheter.

> [!IMPORTANT]  
> I en-hierarki där den centrala administrations platsen använder en standard version av SQL Server, stöder hierarkin högst 50 000 Station ära datorer och enheter. Om du vill ha stöd för fler än 50 000 Station ära datorer och enheter måste du använda en Enterprise-version av SQL Server. Detta krav gäller endast för en central administrations plats. Den gäller inte för en fristående primär plats eller en underordnad primär plats. Den version av SQL Server som du använder för en primär plats begränsar inte dess kapacitet att stödja det angivna antalet klienter.

Den version av SQL Server som används på en fristående primär plats begränsar inte platsens kapacitet att stödja upp till det angivna antalet klienter.  

### <a name="child-primary-site"></a><a name="bkmk_chipri"></a>Underordnad primär plats

Varje underordnad primär plats i en hierarki med en central administrations plats har stöd för följande antal klienter:  

- 150 000 totalt antal klienter och enheter som inte är begränsade till en viss grupp eller typ, förutsatt att stödet inte överskrider det antal som stöds för hierarkin. Se även stöd för [inbäddade enheter](#embedded).

En primär plats stöder till exempel 25 000 Mac-och Windows CE 7,0-enheter. Talet är gränsen för en hierarki. Den här primära platsen kan sedan stödja ytterligare 125 000 Station ära datorer. Det totala antalet enheter som stöds för den underordnade primära platsen är den maximala gränsen på 150 000 som stöds.

### <a name="stand-alone-primary-site"></a><a name="bkmk_pri"></a>Fristående primär plats

En fristående primär plats har stöd för följande antal enheter:  

- 175 000 totalt antal klienter och enheter, inte större än:  

  - 150 000 datorer (datorer som kör Windows, Linux och UNIX). Se även stöd för [inbäddade enheter](#embedded).

  - 25 000 enheter som kör Mac och Windows CE 7,0

  - 50 000 enheter som du hanterar med lokal MDM  

Till exempel kan en fristående primär plats som har stöd för 150 000 Station ära datorer och 10 000 Mac-datorer bara stödja ytterligare 15 000-mobila enheter som hanteras av lokal MDM.

### <a name="primary-sites-and-windows-embedded-devices"></a><a name="embedded"></a>Primära platser och Windows Embedded-enheter

Primära platser har stöd för Windows Embedded-enheter som har filbaserade Skriv filter (FBWF) aktiverade. När inbyggda enheter inte har Skriv filter aktiverade kan en primär plats stödja ett antal inbäddade enheter upp till det tillåtna antalet enheter för den platsen. När inbäddade enheter har FBWF eller UWF (Unified Write filters) aktiverade kan en primär plats stödja högst 10 000 Windows Embedded-enheter. De här enheterna måste konfigureras med undantagen som anges i den viktiga kommentaren som finns i [Planera för klient distribution till Windows Embedded-enheter](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md). En primär plats stöder endast 3 000 Windows Embedded-enheter som har EWF aktiverat och som inte har kon figurer ATS för undantagen.

### <a name="secondary-sites"></a><a name="bkmk_sec"></a>Sekundära platser

Sekundära platser har stöd för följande antal enheter:  

- 15 000 datorer (datorer som kör Windows, Linux och UNIX)  

### <a name="management-points"></a><a name="bkmk_mp"></a>Hanterings platser

Varje hanterings plats har stöd för följande antal enheter:  

- 25 000 totalt antal klienter och enheter, inte större än:  

  - 25 000 datorer (datorer som kör Windows, Linux och UNIX)  

  - Något av följande (inte båda):  

    - 10 000 enheter som hanteras med lokal MDM  

    - 10 000 enheter som kör Mac-och Windows CE 7,0-klienter
