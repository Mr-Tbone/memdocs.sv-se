---
title: Configuration Manager på Azure
titleSuffix: Configuration Manager
description: Information om hur du använder Configuration Manager i en Azure-miljö.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c12372325573c6795396ff0832ca60cba68b8c29
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078506"
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Configuration Manager på Azure – vanliga frågor och svar

*Gäller för: Configuration Manager (aktuell gren)*

Följande frågor och svar kan hjälpa dig att förstå när du ska använda och hur du konfigurerar Configuration Manager på Microsoft Azure.

## <a name="general-questions"></a>Allmänna frågor
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>Mitt företag försöker flytta så många fysiska servrar som möjligt att Microsoft Azure, kan jag flytta Configuration Manager servrar till Azure?
Det här är ett scenario som stöds.  Se [stöd för virtualiseringslösningar för Configuration Manager](../plan-design/configs/support-for-virtualization-environments.md).

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Bra! Min miljö kräver flera-platser. Bör alla underordnade primära platser finnas i Azure med den centrala administrations platsen eller lokalt? Vad gäller sekundära platser?
Plats-till-plats-kommunikation (filbaserad och databasreplikering) fördelar från närhet av att vara värd i Azure. All klient relaterad trafik kan dock vara fjärran sluten till plats servrar och plats system. Om du använder en snabb och tillförlitlig nätverks anslutning mellan Azure och intranätet med ett obegränsat data abonnemang är det ett alternativ som är värd för all infrastruktur i Azure.

Men om du använder en mätnings data plan och tillgänglig bandbredd eller kostnad är ett problem, eller om nätverks anslutningen mellan Azure och intranätet inte är fast eller är otillförlitlig, kan du överväga att placera vissa platser (och plats system) lokalt och sedan använda de inbyggda bandbredds kontrollerna i Configuration Manager.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Har Configuration Manager i Azure ett SaaS-scenario (program vara som en tjänst)?
Nej, det är en IaaS (infrastruktur som en tjänst) eftersom du är värd för dina Configuration Manager infrastruktur servrar i Azure Virtual Machines.

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>Vilka områden bör jag tänka på när jag funderar på att flytta Configuration Manager-infrastrukturen till Azure?
Bra fråga här är de områden som är viktigast när du fattar det här beslutet, och de visas i ett separat avsnitt i det här avsnittet:
1. Nätverk
2. Tillgänglighet
3. Prestanda
4. Kostnad
5. Användarupplevelse

## <a name="networking"></a>Nätverk
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>Vad gäller nätverks krav, ska jag använda ExpressRoute eller en Azure-VPN Gateway?
Nätverk är ett mycket viktigt beslut. Nätverks hastigheter och svars tider kan påverka funktionaliteten mellan plats servern och fjärrplatssystem och all klient kommunikation till plats systemen. Vi rekommenderar att du använder ExpressRoute. Men det finns ingen Configuration Manager begränsning för att hindra dig från att använda Azure VPN Gateway. Du bör noggrant granska dina krav (prestanda, korrigeringar, program varu distribution, distribution av operativ system) från den här infrastrukturen och sedan fatta ditt beslut. Några saker att tänka på för varje lösning är:

- **ExpressRoute** (rekommenderas)
  - Naturligt tillägg till ditt data Center (kan knytas samman flera data Center)
  - Privata anslutningar mellan Azure-datacenter och din infrastruktur
  - Går inte via det offentliga Internet
  - Erbjuder tillförlitlighet, snabba hastigheter, lägre latens, hög säkerhet
  - Ger upp till 10Gbps hastigheter och obegränsade data abonnemangs alternativ
- **VPN Gateway**
  - VPN för plats-till-plats/punkt-till-plats
  - Trafiken går via det offentliga Internet
  - Använder Internet Protocol säkerhet (IPsec) och Internet Key Exchange (IKE)

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>ExpressRoute har många olika alternativ som obegränsade kontra förkortade, olika hastighets alternativ och Premium-tillägg. Vad ska jag välja?
Vilka alternativ du väljer beror på vilket scenario du implementerar och hur mycket data du planerar att distribuera. Överföringen av Configuration Manager data kan styras mellan plats servrar och distributions platser, men kommunikationen mellan plats Server och plats Server kan inte styras.   När du använder en dataplan med datapriser kan du styra kostnaden för att använda Azure genom att placera vissa platser (och plats system) lokalt och använda [Configuration Manager inbyggda bandbredds kontroller](../plan-design/hierarchy/fundamental-concepts-for-content-management.md) .

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>Vad gäller installations krav som Active Directory domäner? Behöver jag fortfarande ansluta mina plats servrar till en Active Directory domän?
Ja. När du flyttar till Azure förblir de [konfigurationer som stöds](../plan-design/configs/supported-configurations.md) detsamma, inklusive Active Directory krav för att installera Configuration Manager.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Jag är införstådd med att behöva ansluta till mina plats servrar till en Active Directory domän, men kan jag använda Azure Active Directory?
Nej, Azure Active Directory stöds inte för tillfället. Plats servrarna måste fortfarande vara medlemmar i en [Windows Active Directory-domän](../plan-design/configs/support-for-active-directory-domains.md).



## <a name="availability"></a>Tillgänglighet
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>En av orsakerna till att vi flyttar infrastruktur till Azure är ett löfte om hög tillgänglighet. Kan jag dra nytta av alternativ för hög tillgänglighet, t. ex. tillgänglighets uppsättningar för Azure VM för virtuella datorer som jag ska använda för Configuration Manager?
Ja! Tillgänglighets uppsättningar för Azure VM kan användas för redundanta plats system roller som distributions platser eller hanterings platser.

Du kan också använda dem för Configuration Manager plats servrar. Centrala administrations platser och primära platser kan till exempel vara i samma tillgänglighets uppsättning som kan hjälpa dig att se till att de inte startas om på samma gång.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>Hur kan jag göra databasen hög tillgänglig? Kan jag använda Azure SQL Database? Eller behöver jag använda Microsoft SQL Server på en virtuell dator?
Du måste använda Microsoft SQL Server i en virtuell dator. Configuration Manager stöder inte Azure SQL Server för tillfället. Men du kan använda funktioner som AlwaysOn-tillgänglighetsgrupper för din SQL Server. [AlwaysOn-tillgänglighetsgrupper](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) rekommenderas och stöds officiellt från och med version 1602 av Configuration Manager.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>Kan jag använda Azure Load Balancer med plats system roller som hanterings platser eller program uppdaterings platser?
Medan Configuration Manager inte testas med Azure Load Balancer, om funktionen är transparent för programmet, bör den inte ha några negativa effekter på normala åtgärder.


## <a name="performance"></a>Prestanda
### <a name="what-factors-affect-performance-in-this-scenario"></a>Vilka faktorer påverkar prestanda i det här scenariot?
[Azure VM-storlek och-typ](https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs), Azure VM-diskar (Premium Storage rekommenderas, särskilt för SQL Server), nätverks fördröjning och hastighet är de viktigaste områdena.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Så berätta mer om virtuella datorer i Azure. vilken storlek ska jag använda för virtuella datorer?
I allmänhet måste din beräknings kraft (CPU och minne) uppfylla den [rekommenderade maskin varan för Configuration Manager](../plan-design/configs/recommended-hardware.md). Men det finns vissa skillnader mellan vanliga dator maskin vara och virtuella Azure-datorer, särskilt när de kommer till de diskar som de virtuella datorerna använder.  Vilken storlek som de virtuella datorer du använder beror på storleken på din miljö, men här är några rekommendationer:
- För produktions distributioner av en betydande storlek rekommenderar vi att du är "**S**" klass för Azure-virtuella datorer. Detta beror på att de kan utnyttja Premium Storage diskar.  Icke-klassens virtuella datorer använder Blob Storage och i allmänhet uppfyller inte de prestanda krav som krävs för en acceptabel produktions upplevelse.
- Flera Premium Storage diskar bör användas för högre skala och stripas i Windows Disk Management-konsolen för högsta IOPS.  
- Vi rekommenderar att du använder bättre eller flera Premium diskar under den första distributions platsen (t. ex. P30 i stället för P20 och 2xP30 i en stripe-volym i stället för 1xP30). Om din webbplats senare behöver öka storleken på den virtuella dator storleken på grund av ytterligare belastning, kan du dra nytta av den ytterligare processor och det minne som en större VM-storlek erbjuder. Det finns även diskar som redan är på plats som kan dra nytta av det ytterligare IOPS-dataflöde som tillåter den större virtuella dator storleken.



I följande tabeller visas de första föreslagna disk antal som används på primära och centrala administrations platser för olika storleks installationer:

**Samplacerad plats databas** – primär eller Central administrations plats med plats databasen på plats servern:

| Skriv bords klienter    |Rekommenderad storlek på virtuell dator|Rekommenderade diskar|
|--------------------|-------------------|-----------------|
|**Upp till 25k**       |   DS4_V2          |2xP30 (randigt)  |
|**25k till 50 000**      |   DS13_V2         |2xP30 (randigt)  |
|**50 000 till 100 000**     |   DS14_V2         |3xP30 (randigt)  |


**Fjärrplatsens databas** – primär eller Central administrations plats med plats databasen på en fjärrserver:

| Skriv bords klienter    |Rekommenderad storlek på virtuell dator|Rekommenderade diskar |
|--------------------|-------------------|------------------|
|**Upp till 25k**       | Plats Server: F4-enheter </br>Databas server: DS12_V2 | Plats Server: 1xP30 </br>Databas server: 2xP30 (Striped)  |
|**25k till 50 000**      | Plats Server: F4-enheter </br>Databas server: DS13_V2 | Plats Server: 1xP30 </br>Databas server: 2xP30 (Striped)   |
|**50 000 till 100 000**     | Plats Server: F8-enheter </br>Databas server: DS14_V2 | Plats Server: 2xP30 (Striped)   </br>Databas server: 3xP30 (Striped)   |

Följande visar en exempel konfiguration för 50 000 till 100 000-klienter på DS14_V2 med 3xP30-diskar i en stripe-volym med separata logiska volymer för Configuration Manager installations-och databasfiler ![: VM-diskar](media/vm_disks.png)  



## <a name="user-experience"></a>Användarupplevelse
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>Du säger att användar upplevelsen är ett av de viktigaste områdena, varför är det?
De beslut du fattar för nätverk, tillgänglighet, prestanda och var du placerar dina Configuration Manager-plats servrar kan påverka dina användare direkt. Vi tror att en flytt till Azure bör vara transparent för dina användare så att de inte upplever en ändring i den dagliga interaktionen med Configuration Manager.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>OK, jag får det. Jag planerar att installera en enda fristående primär plats på en virtuell Azure-dator och jag vill se till att mina kostnader är låga. Ska jag placera (fjärrplatssystem) (till exempel hanterings platser, distributions platser och program uppdaterings platser) på virtuella Azure-datorer eller lokalt?
Förutom kommunikation från plats servern till en distributions plats kan dessa server-till-server-kommunikation på en plats ske när som helst och inte använda mekanismer för att styra användningen av nätverks bandbredd. Eftersom du inte kan styra kommunikationen mellan plats systemen bör alla kostnader som är kopplade till dessa meddelanden beaktas.

Nätverks hastigheter och svars tider är andra faktorer att tänka på. Långsamma eller otillförlitliga nätverk kan påverka funktionaliteten mellan plats servern och fjärrplatssystem samt all klient kommunikation till plats systemen. Antalet hanterade klienter som använder ett angivet plats system samt de funktioner som du använder aktivt bör också beaktas.
I allmänhet kan du utnyttja den normala vägledningen när den är relaterad till WAN-länkar och-plats system som utgångs punkt. Det bästa är att det data flöde som du väljer och tar emot mellan Azure och intranätet kommer att vara konsekvent med ett WAN-nätverk som är väl anslutet till ett snabbt nätverk.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>Vad gäller innehålls distribution och innehålls hantering? Ska standard distributions platser vara i Azure eller lokalt, och bör jag använda BranchCache eller mottagar distributions platser lokalt? Eller bör jag göra exklusiv användning av moln distributions platser?
Metoden för innehålls hantering är ungefär samma som för plats servrar och plats system.
- Om du använder en snabb och tillförlitlig nätverks anslutning mellan Azure och intranätet med ett obegränsat data abonnemang kan det vara ett alternativ som är värd för standard distributions platser i Azure.
- Om du använder en dataplan med datapriser och bandbredds kostnaden är ett problem, eller om nätverks anslutningen mellan Azure och intranätet inte är hög eller kan vara otillförlitlig, kan du överväga andra metoder. Dessa omfattar att lokalisera standard-eller mottagar distributions platser både lokalt och med BranchCache. Användningen av molnbaserade distributions platser är också ett alternativ, men det finns vissa begränsningar för de innehålls typer som stöds (till exempel inget stöd för program uppdaterings paket).

> [!NOTE]
>  Om PXE-eller multicast-stöd krävs måste du använda lokala distributions platser (standard eller pull) för att svara på begär Anden om start.


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>Jag är OK med begränsningarna för molnbaserade distributions platser, jag vill inte placera min hanterings plats i en DMZ trots att det behövs för att stödja mina Internetbaserade klienter. Finns det några andra alternativ?
Ja! Med Configuration Manager version 1610 introducerade vi [Cloud Management Gateway](../clients/manage/manage-clients-internet.md#cloud-management-gateway) som en för hands versions funktion. (Den här funktionen visades först i den tekniska för hands version 1606 som [Cloud proxy-tjänsten](../get-started/capabilities-in-technical-preview-1606.md#cloud_proxy)).

**Cloud Management Gateway** är ett enkelt sätt att hantera Configuration Manager-klienter på Internet. Tjänsten, som distribueras till Microsoft Azure och kräver en Azure-prenumeration, ansluter till din lokala Configuration Manager-infrastruktur med hjälp av en ny roll som kallas för Cloud Management Gateway anslutnings punkt. När den har distribuerats och kon figurer ATS kan klienter komma åt lokala Configuration Manager plats system roller oavsett om de är anslutna till det interna privata nätverket eller Internet.

Du kan börja använda Cloud Management Gateway i din miljö och ge oss feedback för att göra detta bättre. Information om för hands versions funktioner finns i [använda för hands versions funktioner från uppdateringar](../servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>Jag har också hört att du har en annan ny funktion som kallas peer-cache införd som en för hands versions funktion i version 1610. Är det något annat än BranchCache? Vilken av dem ska jag välja?
Ja, helt annorlunda. [Peer-cache](../plan-design/hierarchy/client-peer-cache.md) är 100% intern Configuration Manager teknik där BranchCache är en funktion i Windows. Båda kan vara användbara för dig. BranchCache använder en sändning för att hitta det begärda innehållet, medan peer-cache använder konfigurations hanterare regelbundna distributions arbets flöden och gränser grupp inställningar.

Du kan konfigurera valfri klient som en peer-cache-källa. När hanterings platser ger klienter information om platser för innehålls källor innehåller de dessutom information om både distributions platserna och de peer-cache-källor som har det innehåll som klienten behöver.


## <a name="cost"></a>Kostnad
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>OK och berätta lite om kostnaden. Kommer detta att vara en kostnads effektiv lösning för mig?
Svårt att säga eftersom varje miljö är annorlunda. Det bästa att göra är att kosta din miljö med hjälp av Microsoft Azure pris kalkylator:https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>Ytterligare resurser
**Grundläggande:**https://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Typer av virtuella Azure-datorer:**
- Azure-dator storlekar:https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs/  
- Prissättning för virtuella datorer:https://azure.microsoft.com/pricing/details/virtual-machines/  
- Lagrings priser:https://azure.microsoft.com/pricing/details/storage/

**Disk prestanda överväganden:**    
- Premium disk – Intro:https://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
- Information om djupare Premium disk:https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
- Praktisk samling diagram för Max storlek och prestanda mål för lagring:https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
- En annan Intro och några häftiga Uber-datanörd-data om hur Premium Storage fungerar bakom omslag:https://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Offlinetillgänglighet**
- SLA för Azure IaaS-drift tid:https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
- Förklarad tillgänglighets uppsättning:https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability/

**Koppling**
- Express Route jämfört med Azure VPN:https://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
- Priser för Express Route:https://azure.microsoft.com/pricing/details/expressroute/
- Mer om Express Route:https://azure.microsoft.com/documentation/articles/expressroute-introduction/
