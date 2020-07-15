---
title: Grunder i innehållshantering
titleSuffix: Configuration Manager
description: Använd verktyg och alternativ i Configuration Manager för att hantera det innehåll som du distribuerar.
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8f29ed1e3201da139daeaa1fadca739ff44dc8e
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384952"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Grundläggande begrepp för innehålls hantering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager stöder ett robust system med verktyg och alternativ för att hantera program varu innehåll. Program varu distributioner som program, paket, program uppdateringar och OS-distributioner behöver innehåll. Configuration Manager lagrar innehållet på både plats servrar och distributions platser. Det här innehållet kräver en stor mängd nätverks bandbredd när den överförs mellan platser. För att planera och använda infrastrukturen för innehålls hantering effektivt bör du först förstå de tillgängliga alternativen och konfigurationerna. Överväg sedan att använda dem för att anpassa din nätverks miljö och dina behov av innehålls distribution.  

> [!TIP]  
> Mer information om innehålls distributions processen och om hur du hittar hjälp vid diagnostisering och lösning av allmänna problem med innehålls distribution finns [i förstå och felsöka innehålls distribution i Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Följande avsnitt är viktiga begrepp för innehålls hantering. Om ett begrepp kräver mer eller komplex information visas länkar som leder dig direkt till denna information.


## <a name="accounts-used-for-content-management"></a>Konton som används för innehållshantering

Följande konton kan användas med innehållshantering:  

### <a name="network-access-account"></a>Nätverksåtkomstkonto

Används av klienter för att ansluta till en distributions plats och åtkomst till innehåll. Som standard provas dator kontot först.  

Det här kontot används också av mottagar distributions platser för att ladda ned innehåll från en käll distributions plats i en fjärran sluten skog.  

Från och med version 1806 kräver vissa scenarier inte längre ett konto för nätverks åtkomst. Du kan aktivera platsen för att använda utökad HTTP med Azure Active Directory autentisering.<!--1358228-->

Mer information finns i [konto för nätverks åtkomst](accounts.md#network-access-account).

### <a name="package-access-account"></a>Paket åtkomst konto

Som standard beviljar Configuration Manager åtkomst till innehåll på en distributions plats till de allmänna åtkomst kontona användare och administratörer. Du kan dock konfigurera ytterligare behörigheter om du vill begränsa åtkomsten.

Mer information finns i [paket åtkomst konto](accounts.md#package-access-account).


## <a name="bandwidth-throttling-and-scheduling"></a>Begränsning och schemaläggning av bandbredd

Både begränsning och schemaläggning är alternativ som hjälper dig att bestämma när innehållet ska distribueras från en platsserver till distributionsplatser. Dessa funktioner liknar, men inte direkt relaterade till bandbredds kontroller för filbaserad replikering från plats till plats.  

Mer information finns i [Hantera nätverks bandbredd](manage-network-bandwidth.md).


## <a name="binary-differential-replication"></a>Binär differentiell replikering

Configuration Manager använder binär differentiell replikering (BDR) för att uppdatera innehåll som du tidigare har distribuerat till andra platser eller till fjärrdistributions platser. Om du vill ha stöd för BDR minskar du bandbredds användningen genom att installera funktionen för **fjärrstyrd differential komprimering** på distributions platser. Mer information finns i [krav för distributions plats](../configs/site-and-site-system-prerequisites.md#bkmk_2012dppreq).

BDR minimerar den nätverks bandbredd som används för att skicka uppdateringar av distribuerat innehåll. Den skickar bara det nya eller ändrade innehållet i stället för att skicka hela uppsättningen innehålls källfiler varje gången du ändrar filerna.  

När BDR används identifierar Configuration Manager de ändringar som inträffar i källfilerna för varje uppsättning innehåll som du har distribuerat tidigare.  

- När filer i käll innehållet ändras, skapar platsen en ny stegvis version av innehållet. Den replikerar sedan bara de ändrade filerna till mål platser och distributions platser. En fil anses vara ändrad om du har bytt namn på eller flyttat den, eller om du har ändrat filens innehåll. Om du till exempel ersätter en enskild driv rutins fil för ett driv rutins paket som du tidigare har distribuerat till flera platser replikeras bara den ändrade driv rutins filen.  

- Configuration Manager stöder upp till fem stegvisa versioner av en innehålls uppsättning innan hela innehålls uppsättningen skickas igen. Efter den femte uppdateringen gör nästa ändring av innehålls uppsättningen att webbplatsen skapar en ny version av innehålls uppsättningen. Configuration Manager distribuerar sedan den nya versionen av innehålls uppsättningen för att ersätta den tidigare uppsättningen och alla dess stegvisa versioner. När den nya innehålls uppsättningen har distribuerats kommer senare stegvisa ändringar av källfilerna att replikeras igen av BDR.  

BDR stöds mellan varje över- och underordnad plats i en hierarki. BDR stöds inom en plats mellan plats servern och dess vanliga distributions platser. Mottagar distributions platser och moln distributions platser stöder dock inte BDR för överföring av innehåll. Mottagar distributions platser stöder delta på fil nivå, överföring av nya filer, men inte block i en fil.

Program använder alltid binär differentiell replikering. BDR är valfritt för paket och är inte aktiverat som standard. Aktivera den här funktionen för varje paket om du vill använda BDR för paket. Välj alternativet **Aktivera binär differentiell replikering** när du skapar eller redigerar ett paket.


### <a name="bdr-or-delta-replication"></a>BDR eller delta-replikering

<!-- SCCMDocs#1209 -->
I följande listor sammanfattas skillnaderna mellan BDR ( *Binary differential Replication* ) och *delta-replikering*.

#### <a name="summary-of-binary-differential-replication"></a>Översikt över binär differentiell replikering

- Configuration Managers period för Windows **Remote Differential-komprimering**
- Skillnader på *block*nivå
- Alltid aktive rad för appar
- Valfritt på äldre paket
- Om en fil redan finns på distributions platsen och det finns en ändring, använder platsen BDR för att replikera block nivå ändringen i stället för hela filen. Detta beteende gäller endast när du aktiverar objektet att använda BDR.<!-- SCCMDocs#2026 -->

#### <a name="summary-of-delta-replication"></a>Översikt över delta-replikering

- *File*Skillnader på filnivå
- Aktiverat som standard, kan inte konfigureras
- När ett paket ändras söker platsen efter ändringar i de enskilda filerna i stället för hela paketet.
    - Om en fil ändras använder du BDR för att utföra arbetet
    - Om det finns en ny fil, kopierar du den nya filen


## <a name="peer-caching-technologies"></a>Peer caching-teknik

<!-- SCCMDocs#1044 -->

Configuration Manager stöder flera alternativ för att hantera innehåll mellan peer-enheter i samma nätverk:

- [BranchCache](#branchcache)
- [Leverans optimering](#delivery-optimization)
- [Configuration Manager peer-cache](#peer-cache)

Använd följande tabell för att jämföra huvud funktionerna i dessa tekniker:

| Funktion  | Peer- &nbsp; cache  | Leverans &nbsp; optimering  | BranchCache  |
|---------|---------|---------|---------|
| Över undernät | Ja | Ja | Nej |
| Begränsa bandbredden | Ja (bitar) | Ja (inbyggt) | Ja (bitar) |
| Partiellt innehåll | Ja | Ja | Ja |
| Kontrol lera cachestorlek på disk | Ja | Ja | Ja |
| Identifiering av peer-källa | Manuell (klient inställning) | Automatiskt | Automatiskt |
| Peer-identifiering | Via hanterings platsen med hjälp av gränser grupper | GÖR moln tjänst | Sändning |
| Rapportering | Instrument panel för klient data källor | Instrument panel för klient data källor | Instrument panel för klient data källor |
| WAN-användnings kontroll | Gränsgrupper | GÖR så här | Endast undernät |
| Innehåll som stöds | Allt ConfigMgr-innehåll | Windows-uppdateringar, driv rutiner, Store-appar | Allt ConfigMgr-innehåll |
| Principkontroll | Inställningar för klient agent | Inställningar för klient agent (delvis) | Inställningar för klient agent |

### <a name="recommendations"></a>Rekommendationer

- Modern hantering: om du redan använder moderna verktyg som Intune, implementera leverans optimering

- Configuration Manager och samhantering: Använd en kombination av peer-cache och leverans optimering. Använd peer-cache med lokala distributions platser och Använd leverans optimering för moln scenarier.

- Befintlig BranchCache implementerad: Använd alla tre tekniker parallellt. Använd peer-cache och leverans optimering för scenarier som inte stöds av BranchCache.


## <a name="branchcache"></a>BranchCache

[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) är en Windows-teknik. Klienter som har stöd för BranchCache och har hämtat en distribution som du konfigurerar för BranchCache och som sedan fungerar som en innehålls källa till andra BranchCache-aktiverade klienter.  

Du kan till exempel ha en distributions plats som kör Windows Server 2012 eller senare och som har kon figurer ATS som en BranchCache-server. När den första BranchCache-aktiverade klienten begär innehåll från den här servern laddar klienten ned innehållet och cachelagrar det.  

- Klienten gör sedan innehållet tillgängligt för ytterligare BranchCache-aktiverade klienter i samma undernät som också cachelagrar innehållet.  
- Andra klienter i samma undernät behöver inte hämta innehåll från distributions platsen.  
- Innehållet distribueras över flera klienter för framtida överföringar.  

Mer information finns i [stöd för Windows BranchCache](../configs/support-for-windows-features-and-networks.md#bkmk_branchcache).

## <a name="delivery-optimization"></a>Leveransoptimering

<!-- 1324696 -->
Du använder Configuration Manager gränser grupper för att definiera och reglera innehålls distribution i företags nätverket och på fjärranslutna kontor. [Windows-leverans optimering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) är en molnbaserad, peer-to-peer-teknik för att dela innehåll mellan Windows 10-enheter. Konfigurera leverans optimeringen så att den använder dina gränser när du delar innehåll mellan peer-datorer. Klient inställningar tillämpar gränserna för den begränsade gruppen som ID för leverans optimerings grupp på klienten. När klienten kommunicerar med moln tjänsten för leverans optimering används den här identifieraren för att hitta peer-datorer med innehållet. Mer information finns i klient inställningar för [leverans optimering](../../clients/deploy/about-client-settings.md#delivery-optimization) .

Leverans optimering är den rekommenderade tekniken för att optimera Windows 10-uppdateringen av Express-installationsfiler för Windows 10-kvalitets uppdateringar. Från och med Configuration Manager version 1910 är Internet åtkomst till moln tjänsten för leverans optimering ett krav för att använda peer-to-peer-funktioner. Information om vilka Internet-slutpunkter som behövs finns i [vanliga frågor och svar om leverans optimering](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). Optimering kan användas för alla Windows-uppdateringar. Mer information finns i [optimera leverans av Windows 10-uppdateringar](../../../sum/deploy-use/optimize-windows-10-update-delivery.md).


## <a name="microsoft-connected-cache"></a>Microsoft Connected Cache

<!--3555764-->
Från och med version 1906 kan du installera en Microsoft-ansluten cache-server på dina distributions platser. Genom att cachelagra det här innehållet lokalt kan dina klienter dra nytta av leverans optimerings funktionen, men du kan skydda WAN-länkar.

> [!NOTE]
> Från och med version 1910 heter funktionen nu **Microsoft Connected cache**. Det kallades tidigare för leverans optimering i nätverket.

Den här cache-servern fungerar som en transparent cache på begäran för innehåll som hämtas av leverans optimering. Använd klient inställningar för att kontrol lera att den här servern endast erbjuds till medlemmar i den lokala Configuration Managers gränser gruppen.

Den här cachen är separat från Configuration Manager distributions plats innehåll. Om du väljer samma enhet som distributions plats rollen lagrar den innehåll separat.

Mer information finns [i Microsoft Connected cache i Configuration Manager](microsoft-connected-cache.md).


## <a name="peer-cache"></a>Peer-cache

Med klient-peer-cache kan du hantera distribution av innehåll till klienter på fjärrplatser. Peer-cache är en inbyggd Configuration Manager-lösning som gör det möjligt för klienter att dela innehåll med andra klienter direkt från deras lokala cacheminne.

Distribuera först klient inställningar som aktiverar peer-cache till en samling. Medlemmar i samlingen kan sedan fungera som peer-innehålls källa för andra klienter i samma avgränsnings grupp.

Från och med version 1806 kan klient-peer cache-källor dela upp innehåll i delar. Dessa delar minimerar nätverks överföringen för att minska WAN-användningen. Hanterings platsen ger en mer detaljerad spårning av innehålls delarna. Det försöker eliminera mer än en hämtning av samma innehåll per gränser grupp.<!--1357346-->

Mer information finns i [peer-cache för Configuration Manager klienter](client-peer-cache.md).


## <a name="windows-pe-peer-cache"></a>Peer-cache i Windows PE

När du distribuerar ett nytt operativ system med Configuration Manager kan datorer som kör aktivitetssekvensen använda peer-cache i Windows PE. De hämtar innehåll från en peer-cache-källa i stället för från en distributions plats. Den här funktionen bidrar till att minimera WAN-trafik i scenarier där det inte finns någon lokal distributions plats.

Mer information finns i [peer-cache i Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="windows-ledbat"></a>Windows-LEDBAT

<!--1358112-->
Windows-LEDBAT (låg extra fördröjning) är en funktion för nätverks överbelastning i Windows Server som hjälper dig att hantera nätverks överföringar i bakgrunden. För distributions platser som körs på versioner av Windows Server som stöds aktiverar du ett alternativ för att justera nätverks trafiken. Klienterna använder sedan bara nätverks bandbredd när de är tillgängliga.

Mer information om Windows-LEDBAT i allmänhet finns i blogg inlägget [nya transport förskott](https://techcommunity.microsoft.com/t5/Networking-Blog/Announcing-Transport-Features-and-Performance-Advancements-in/ba-p/339726) .

Mer information om hur du använder Windows-LEDBAT med Configuration Manager distributions platser finns i inställningen för att **Justera nedladdnings hastigheten så att den använder oanvänd nätverks bandbredd (Windows LEDBAT)** när du [konfigurerar de allmänna inställningarna för en distributions plats](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-general).


## <a name="client-locations"></a>Klientplatser

Följande är platser som klienten har åtkomst till innehåll från:  

- **Intranät** (lokalt):  

    - Distributions platser kan använda HTTP eller HTTPs.  

    - Använd bara en moln distributions plats för återställning när lokala distributions platser inte är tillgängliga.  

- **Internet**:  

    - Kräver att Internet-riktade distributions platser accepterar HTTPS.  

    - Kan använda en moln distributions plats eller en CMG (Cloud Management Gateway).  

        Från och med version 1806 kan en CMG också hantera innehåll till klienter. Den här funktionen minskar de nödvändiga certifikaten och kostnaden för virtuella Azure-datorer. Mer information finns i [ändra en CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md).

- **Arbets grupp**:  

    - Kräver att distributions platser accepterar HTTPS.  

    - Kan använda en moln distributions plats eller en CMG.  


## <a name="content-source-priority"></a>Innehålls källans prioritet

När en klient behöver innehåll, gör den en innehålls plats förfrågan till hanterings platsen. Hanterings platsen returnerar en lista med käll platser som är giltiga för det begärda innehållet. Den här listan varierar beroende på vilket scenario, vilka tekniker som används, webbplats design, gräns grupper och distributions inställningar. Till exempel när en aktivitetssekvens körs, körs inte den fullständiga Configuration Manager klienten alltid, så beteendena kan skilja sig åt.<!-- SCCMDocs#1960 -->

Följande lista innehåller alla tänkbara innehålls käll platser som Configuration Manager-klienten kan använda, i den ordning som den prioriterar dem:  

1. Distributions platsen på samma dator som klienten
2. En peer-källa i samma undernät i nätverket
3. En distributions plats i samma undernät i nätverket
4. En peer-källa i samma ram grupp
5. En distributions plats i den aktuella gränser gruppen
6. En distributions plats i en intilliggande avgränsnings grupp som kon figurer ATS för återställning
7. En distributions plats i standard platsens gränser grupp
8. Windows Update moln tjänsten
9. En distributions plats mot Internet
10. En moln distributions plats i Azure

> [!Note]  
> <!-- SCCMDocs#1607 -->Leverans optimeringen gäller inte för den här käll prioriteringen. Den här listan visar hur Configuration Manager klienten hittar innehåll. Windows Update Agent laddar ned innehåll för leverans optimering. Om Windows Update-agenten inte kan hitta innehållet, använder Configuration Manager klienten den här listan för att söka efter den.

## <a name="content-library"></a>Innehålls bibliotek

Innehålls biblioteket är ett lagrat innehåll i en instans i Configuration Manager. Det här biblioteket minskar den totala storleken på det innehåll som du distribuerar.  

- Läs mer om [innehålls biblioteket](the-content-library.md).
- Använd [rensnings verktyget för innehålls bibliotek](content-library-cleanup-tool.md) för att ta bort innehåll som inte längre är kopplat till ett program.  


## <a name="distribution-points"></a>Distributionsplatser

Configuration Manager använder distributions platser för att lagra filer som krävs för att program ska kunna köras på klient datorer. Klienter måste ha åtkomst till minst en distributions plats från vilken de kan ladda ned filerna för det innehåll som du distribuerar.  

Den grundläggande (icke-specialiserade) distributions platsen kallas ofta för en standard distributions plats. Det finns två varianter på standard standarddistributionsplatsen som får särskild uppmärksamhet:  

- **Mottagar distributions plats**: en variant av en distributions plats där distributions platsen hämtar innehåll från en annan distributions plats (en käll distributions plats). Den här processen liknar hur klienter laddar ned innehåll från distributions platser. Mottagar distributions platser kan hjälpa dig att undvika Flask halsar i nätverks bandbredd som inträffar när plats servern måste distribuera innehåll direkt till varje distributions plats. [Använd en mottagar distributions plats](use-a-pull-distribution-point.md).

- **Moln distributions plats**: en variant av en distributions plats som är installerad på Microsoft Azure. [Lär dig hur du använder en moln distributions plats](use-a-cloud-based-distribution-point.md).  

Standard distributions platser har stöd för en mängd konfigurationer och funktioner:  

- Använd kontroller som **scheman** eller **bandbredds begränsning** för att kontrol lera överföringen.  

- Använd andra alternativ, inklusive **förinstallerat innehåll**och **mottagar distributions platser** för att minimera och kontrol lera nätverks förbrukningen.  

- **BranchCache**, **peer-cache**och **leverans optimering** är peer-to-peer-tekniker för att minska den nätverks bandbredd som används när du distribuerar innehåll.  

- Det finns olika konfigurationer för distributioner av operativ system, till exempel **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** och **[multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**  

- Alternativ för **mobila enheter**  
  
Moln-och mottagar distributions platser stöder många av dessa konfigurationer, men har begränsningar som är begränsade till varje distributions plats variation.  


## <a name="distribution-point-groups"></a>Distributions plats grupper

Distributions plats grupper är logiska grupperingar av distributions platser som kan förenkla innehålls distributionen.  

Mer information finns i [Hantera distributions plats grupper](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).


## <a name="distribution-point-priority"></a>Distributionsplatsprioritet

Distributionsplatsprioriteten baseras på hur lång tid det tog att överföra tidigare distributioner till distributionsplatsen.  

- Det här värdet är själv justering. Den ställs in på varje distributions plats för att hjälpa Configuration Manager snabbare överföra innehåll till fler distributions platser.  

- När du distribuerar innehåll till flera distributions platser samtidigt, eller till en distributions plats grupp, skickar platsen först innehållet till servern med högst prioritet. Sedan skickar den samma innehåll till en distributions plats med lägre prioritet.  

- Distributions plats prioritet ersätter inte distributions prioriteten för paket. Paket prioriteten är fortfarande den avgörande faktorn för när platsen skickar annat innehåll.  

Du kan till exempel ha ett paket som har en hög paket prioritet. Du distribuerar den till en server med en låg distributions plats prioritet. Det här paketet med hög prioritet överförs alltid före ett paket med lägre prioritet. Paket prioriteten gäller även om platsen distribuerar paket med lägre prioritet till servrar med högre distributions plats prioriteter.

Paketets höga prioritet säkerställer att Configuration Manager distribuerar innehållet till distributions platser innan det skickar några paket med lägre prioritet.  

> [!NOTE]  
> Pull-distributionsplatser använder också prioritet för att ordna källdistributionsplatsernas ordningsföljd.  
>
> - Distributions plats prioriteten för innehålls överföringar till servern skiljer sig från den prioritet som mottagar distributions platser använder. Mottagar distributions platser använder sin prioritet när de söker efter innehåll från en käll distributions plats.  
> - Mer information finns i [använda en mottagar distributions plats](use-a-pull-distribution-point.md).  


## <a name="fallback"></a>Återställning

Flera saker har ändrats med Configuration Manager aktuella grenen på det sätt som klienter hittar en distributions plats som har innehåll, inklusive fallback.

Klienter som inte kan hitta innehåll från en distributions plats som är associerat med den aktuella gränser gruppen går tillbaka till användning av innehålls käll platser kopplade till närliggande gränser grupper. En intilliggande gräns grupp måste ha en definierad relation med klientens aktuella gräns grupp för att kunna användas för återställningen. Den här relationen innehåller en konfigurerad tid som måste passera innan en klient som inte kan hitta innehåll lokalt innehåller innehålls källor från intilliggande gräns grupp som en del av dess sökning.

Begreppen för prioriterade distributions platser används inte längre, och inställningarna för **Tillåt återställnings käll platser för innehåll** är inte längre tillgängliga eller framtvingas.

Mer information finns i [gränser grupper](../../servers/deploy/configure/boundary-groups.md).


## <a name="network-bandwidth"></a>Nätverksbandbredd

För att hjälpa till att hantera mängden nätverks bandbredd som används när du distribuerar innehåll kan du använda följande alternativ:  

- **Förinstallerat innehåll**: överför innehåll till en distributions plats utan att distribuera innehållet i nätverket.  

- **Schemaläggning och begränsning**: konfigurationer som hjälper dig att styra när och hur innehållet distribueras till distributions platser.  

Mer information finns i [Hantera nätverks bandbredd](manage-network-bandwidth.md).


## <a name="network-connection-speed-to-content-source"></a>Nätverksanslutningshastigheten till innehållskällan

Flera saker har ändrats med Configuration Manager aktuella grenen på det sätt som klienter hittar en distributions plats som har innehåll. Dessa ändringar omfattar nätverks hastigheten i en innehålls källa.

Nätverks anslutnings hastigheter som definierar en distributions plats som **snabb** eller **långsam** används inte längre. I stället behandlas alla plats system som är kopplade till en avgränsnings grupp.

Mer information finns i [gränser grupper](../../servers/deploy/configure/boundary-groups.md).


## <a name="on-demand-content-distribution"></a>Innehållsdistribution på begäran

Innehålls distribution på begäran är ett alternativ för enskilda program-och paket distributioner. Det här alternativet möjliggör innehålls distribution på begäran till prioriterade servrar.  

- Aktivera den här inställningen för en distribution genom att aktivera: **distribuera det här paketets innehåll till prioriterade distributions platser**.  

- När du aktiverar det här alternativet för en distribution och en klient begär innehåll, men innehållet inte är tillgängligt på någon av klientens primära distributions platser, Configuration Manager automatiskt distribuera innehållet till klientens primära distributions platser.  

- Även om detta utlöser Configuration Manager automatiskt distribuerar innehållet till klientens primära distributions platser kan klienten hämta innehållet från andra distributions platser innan de primära distributions platserna för klienten får distributionen. När detta inträffar kommer innehållet att finnas på den distributions platsen för användning av nästa klient som söker efter distributionen.  

Mer information finns i [gränser grupper](../../servers/deploy/configure/boundary-groups.md).


## <a name="package-transfer-manager"></a>Package Transfer Manager

Package Transfer Manager är den plats Server komponent som överför innehåll till distributions platser på andra datorer.  

Mer information finns i [Package Transfer Manager](package-transfer-manager.md).  


## <a name="prestage-content"></a>Förinstallera innehåll

Att förinstallera innehåll är en process för att överföra innehåll till en distributions plats utan att distribuera innehållet i nätverket.  

Mer information finns i [Hantera nätverks bandbredd](manage-network-bandwidth.md).
