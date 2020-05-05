---
title: Hög tillgänglighet
titleSuffix: Configuration Manager
description: Lär dig hur du distribuerar Configuration Manager med hjälp av alternativ som upprätthåller en hög nivå av tillgänglig tjänst.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cf8714aff7235736628d44238561eea82b896698
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073321"
---
# <a name="high-availability-options-for-configuration-manager"></a>Alternativ för hög tillgänglighet för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln beskriver hur du distribuerar Configuration Manager med hjälp av alternativ som upprätthåller en hög nivå av tillgänglig tjänst.

Följande Configuration Manager alternativ stöder hög tillgänglighet:

- Konfigurera en fristående primär plats med ytterligare en plats server i passivt läge.  

- Konfigurera en SQL Server Always on-tillgänglighetsgrupper för plats databasen på primära platser och den centrala administrations platsen.

- -Platser har stöd för flera instanser av plats system roller som ger viktiga tjänster till klienter. Till exempel hanterings platser och distributions platser.  

- Centrala administrations platser och primära platser har stöd för säkerhets kopiering av plats databasen. Plats databasen lagrar alla konfigurationer för platser och klienter. Platserna i en hierarki delar konfigurations data.  

- Inbyggda alternativ för plats återställning kan minska serverns stillestånds tid. Dessa avancerade alternativ fören klar återställning när du har en hierarki med en central administrations plats.  

- Klienter kan automatiskt åtgärda vanliga problem utan administrativ åtgärd.  

- Platser genererar aviseringar om klienter som inte kan skicka senaste data, vilket varnar administratörer till potentiella problem.  

- Configuration Manager innehåller flera inbyggda rapporter och instrument paneler. Använd dessa för att identifiera problem och trender innan de blir problem med Server-eller klient åtgärder.  

Configuration Manager innehåller flera funktioner som ger nära real tids tjänst. Om de här funktionerna är kritiska för att uppfylla dina affärs behov kan du planera och konfigurera dina platser och hierarkier för hög tillgänglighet. Ett exempel:  

- [Åtgärder för klient meddelanden](../../../clients/manage/manage-clients.md), till exempel starta om, starta Windows Defender-genomsökningar eller fjärr skrivbord.  

- Tillstånds meddelanden för att övervaka funktioner, t. ex. program uppdateringar och Endpoint Protection.

- [Skript](../../../../apps/deploy-use/create-deploy-scripts.md)

- [CMPivot](../../manage/cmpivot.md)

Andra funktioner i Configuration Manager tillhandahåller inte real tids service. Dessa funktioner omfattar, men är inte begränsade till, klient inställningar, maskin-och program varu inventering, program distributioner och kompatibilitetsinställningar. Vänta på att de ska fungera med viss data svars tid. Det är ovanligt för de flesta scenarier som innefattar ett tillfälligt avbrott i tjänsten för att bli ett kritiskt problem. För att minimera drift stopp, upprätthålla självständighet i driften och tillhandahålla en hög service nivå kan du konfigurera dina platser och hierarkier med hög tillgänglighet i åtanke.  

Configuration Manager-klienter fungerar till exempel vanligt vis självständigt genom att använda kända scheman och konfigurationer för åtgärder och scheman för att skicka data till platsen för bearbetning.  

- Om klienterna inte kan kontakta platsen cachelagrar de data som ska skickas tills de kan kontakta platsen.  

- Klienter som inte kan kontakta platsen fortsätter att arbeta. De använder senast kända scheman och cachelagrad information, tills de kan kontakta platsen och få nya principer. En-klient kan till exempel behålla ett tidigare nedladdat program som de måste köra eller installera.

- Platsen övervakar sina plats system och klienter för regelbundna status uppdateringar. Den kan generera aviseringar när dessa komponenter inte kan registreras.  

- Inbyggda rapporter ger insikter om pågående åtgärder, historiska åtgärder och aktuella trender. Configuration Manager också stöd för tillstånds meddelanden som ger nära real tids information för pågående åtgärder.  


## <a name="high-availability-for-sites-and-hierarchies"></a><a name="bkmk_snh"></a>Hög tillgänglighet för platser och hierarkier  

### <a name="use-a-site-server-in-passive-mode"></a>Använda en plats server i passivt läge

Installera ytterligare en plats server i *passivt* läge för en fristående primär plats. Plats servern i passivt läge är utöver den befintliga plats servern i *aktivt* läge. En plats server i passivt läge är tillgänglig för omedelbar användning vid behov. Mer information finns i [hög tillgänglighet för plats Server](site-server-high-availability.md).  

### <a name="use-a-remote-content-library"></a>Använd ett fjärrinnehålls bibliotek

Flytta platsens innehålls bibliotek till en annan plats som tillhandahåller lagring med hög tillgänglighet. Den här funktionen är ett krav för hög tillgänglighet för plats Server. Mer information finns i [innehålls biblioteket](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote).

### <a name="centralize-content-sources"></a>Centralisera innehålls källor

Alla program varu innehåll i Configuration Manager kräver en paket käll plats i nätverket. Använd centraliserad lagring med hög tillgänglighet för att vara värd för en vanlig paket käll plats för allt innehåll.

### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>Använd en SQL Server Always on-tillgänglighetsgruppen som värd för plats databasen

Vara värd för plats databasen på primära platser och den centrala administrations webbplatsen på SQL Server Always on-tillgänglighetsgrupper. Mer information finns i [SQL Server Always on för en plats databas med hög](sql-server-alwayson-for-a-highly-available-site-database.md)tillgänglighet.  

### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>Använd ett SQL Server-kluster som värd för plats databasen

När du använder ett SQL Server-kluster för databasen på en central administrations plats eller en primär plats, använder du fel stödet som är inbyggt i SQL Server.  

Sekundära platser kan inte använda ett SQL Server kluster och har inte stöd för säkerhets kopiering eller återställning av plats databasen. Återställ en sekundär plats genom att installera om den sekundära platsen från den överordnade primära platsen.  

### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>Distribuera en hierarki med platser med en central administrations plats och en eller flera underordnade primära platser

Den här konfigurationen kan ge fel tolerans när platserna hanterar överlappande segment i nätverket. Det finns också ett ytterligare återställnings alternativ för att använda informationen i den delade databasen som är tillgänglig på en annan plats, för att återskapa plats databasen på den återställda platsen. Använd det här alternativet om du vill ersätta en misslyckad eller otillgänglig säkerhets kopia av den felande platsens databas.  

### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>Skapa regelbundna säkerhets kopieringar på centrala administrations platser och primära platser

När du skapar och testar en vanlig säkerhets kopiering av platsen ser du till att du har de data som krävs för att återställa en plats. Du bör också öva på att återskapa en webbplats på den minimala tiden.  

### <a name="install-multiple-instances-of-site-system-roles"></a>Installera flera instanser av plats system roller

När du installerar flera instanser av kritiska plats system roller ger du redundanta kontakt punkter för klienter. Till exempel ger flera hanterings platser och distributions platser redundanta tjänster i händelse av att en enskild server är offline.  

### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>Installera flera instanser av SMS-providern på en plats

SMS-providern tillhandahåller den administrativa kontakt punkten för en eller flera Configuration Manager-konsoler. Om du vill tillhandahålla redundans för kontakt punkter för att administrera din plats och hierarki, installerar du flera SMS-providers.  


## <a name="high-availability-for-site-system-roles"></a><a name="bkmk_ssr"></a>Hög tillgänglighet för plats system roller

På varje plats distribuerar du plats system roller för att tillhandahålla de tjänster som du vill att klienter ska använda på den platsen. Plats databasen innehåller konfigurations information för platsen och för alla klienter. Använd ett eller flera av de tillgängliga alternativen för att tillhandahålla hög tillgänglighet för plats databasen och återställningen av platsen och plats databasen om det behövs.  

### <a name="redundancy-for-important-site-system-roles"></a>Redundans för viktiga plats system roller

- Webb service punkt för program katalog  

- Plats för program katalog  

- Distributionsplats  

- Hanteringsplats  

- Programuppdateringsplats  

- Plats för tillståndsmigrering  

Om du vill ge redundans för rapportering på platser och klienter installerar du flera instanser av repor ting Services-platsen.

Om du vill ha stöd för redundans med program uppdaterings platsen använder du Windows PowerShell för att installera den här rollen på ett Windows-kluster för Utjämning av nätverks belastning (NLB).  

### <a name="built-in-site-backup"></a>Inbyggd plats säkerhets kopiering

Configuration Manager innehåller en inbyggd säkerhets kopierings uppgift som hjälper dig att säkerhetskopiera platsen och viktig information enligt ett regelbundet schema. Dessutom stöder installations guiden för Configuration Manager plats återställnings åtgärder som hjälper dig att återställa en plats till åtgärder.  

### <a name="publishing-to-active-directory-domain-services-and-dns"></a>Publicera till Active Directory Domain Services och DNS

Konfigurera varje plats för att publicera data om-platsen till Active Directory Domain Services och DNS. Den här publiceringen gör det möjligt för klienter att identifiera den mest tillgängliga servern i nätverket. Klienter använder också den för att identifiera när nya plats system servrar är tillgängliga för att tillhandahålla viktiga tjänster, till exempel hanterings platser.  

### <a name="sms-provider-and-configuration-manager-console"></a>SMS-provider och Configuration Manager-konsol

Configuration Manager stöder installation av flera SMS-providrar på separata servrar som flera åtkomst punkter för-konsolen. Om en SMS-provider är offline kan du fortfarande visa och hantera platser och klienter.  

När en Configuration Manager-konsol ansluter till en plats ansluter den till en instans av SMS-providern på den platsen. Instansen av SMS-providern väljs slumpmässigt. Om den valda SMS-providern inte är tillgänglig har du följande alternativ:  

- Återanslut-konsolen till-platsen. Varje ny anslutningsbegäran tilldelas slumpvis en instans av SMS-providern. Det är möjligt att den nya anslutningen tilldelas en tillgänglig instans.  

- Anslut konsolen till en annan Configuration Manager plats och hantera konfigurationen från den anslutningen. Det här alternativet ger en liten fördröjning av konfigurations ändringar på högst några minuter. När SMS-providern för platsen är online ansluter du Configuration Manager-konsolen direkt till den plats som du vill hantera.  

Installera Configuration Manager-konsolen på flera datorer för användning av administratörer. Varje SMS-provider stöder anslutningar från fler än en-konsol.  

### <a name="management-point"></a>Hanteringsplats

Installera flera hanterings platser på varje primär plats och gör det möjligt för platserna att publicera plats data till din Active Directory-infrastruktur och till DNS.  

Flera hanterings platser hjälper till att belastningsutjämna användningen av en enskild hanterings plats av flera klienter. Överväg också att installera en eller flera databas repliker för hanterings platser. Den här konfigurationen minskar hanterings platsens processor intensiva åtgärder. Det ökar också tillgängligheten för den här kritiska plats system rollen.  

Sekundära platser har endast stöd för installation av en hanterings plats, som måste finnas på den sekundära plats servern. Hanterings platser på sekundära platser anses inte ha en konfiguration med hög tillgänglighet.  

> [!NOTE]  
> Enheter som hanteras av lokal hantering av mobila enheter ansluter bara till en hanterings plats på en primär plats. Hanterings platsen tilldelas av Configuration Manager till den mobila enheten under registreringen och ändras inte. När du installerar flera hanterings platser och aktiverar mer än en för mobila enheter, är hanterings platsen som är tilldelad till en mobilen hets klient icke-deterministisk.  
>
> Om hanterings platsen som en mobilen hets klient använder blir otillgänglig måste du lösa problemet med hanterings platsen eller rensa den mobila enheten och registrera den igen så att den kan tilldelas en drift hanterings plats som är aktive rad för mobila enheter.  

### <a name="distribution-point"></a>Distributionsplats

Installera flera distributions platser och distribuera innehåll till flera distributions platser. Lägg till fler än en distributions plats per gränser grupp för att se till att klienterna får flera alternativ i innehålls förfrågningen. Konfigurera Relations grupp relationer så att de har ett predicable-återställnings beteende till en annan avgränsnings grupp eller moln distributions plats. Mer information finns i [Konfigurera gränser grupper](boundary-groups.md).  

### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>Webb service punkt för program katalog och webbplats för program katalog

> [!Important]
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Installera mer än en instans av varje plats system roll. För bästa prestanda bör du distribuera en av var och en av dem på samma plats system Server.  

Varje plats system roll för program katalogen ger samma information som andra instanser av rollen oavsett var de finns i hierarkin. När en klient gör en begäran för program katalogen och du har konfigurerat klienter för att automatiskt identifiera standard webbplats för program katalog dirigeras klienten till en tillgänglig instans. Klienter föredrar lokala program katalog instanser, baserat på klientens aktuella nätverks plats.  

Mer information om den här klient inställningen och hur automatisk identifiering fungerar finns i klient inställningarna för [dator agent](../../../clients/deploy/about-client-settings.md#computer-agent) .  


## <a name="high-availability-for-clients"></a><a name="bkmk_client"></a>Hög tillgänglighet för klienter  

### <a name="client-operations-are-autonomous"></a>Klient åtgärder är självständiga

Configuration Manager-klientens självständighet innehåller följande beteenden:  

- Klienter kräver inte kontinuerlig kontakt med några olika plats system servrar. De använder kända konfigurationer för att utföra förkonfigurerade åtgärder enligt ett schema.  

- Klienter kan använda alla tillgängliga instanser av en plats system roll som tillhandahåller tjänster till klienter. De försöker kontakta kända servrar tills de hittar en tillgänglig server.  

- Klienter kan köra inventering, program varu distributioner och liknande schemalagda åtgärder oberoende av direkt kontakt med plats system servrar.  

- Klienter som är konfigurerade för att använda en återställnings status punkt kan skicka information till återställnings status platsen när de inte kan kommunicera med en hanterings plats.  

### <a name="clients-can-repair-themselves"></a>Klienter kan reparera sig själva

Klienterna reparerar automatiskt de vanligaste problemen utan direkt administrations åtgärder.  

- Med jämna mellanrum kan klienterna själv utvärdera sin status. De vidtar åtgärder för att åtgärda vanliga problem genom att använda ett lokalt cacheminne för reparations steg och källfiler för reparationer.  

- När en klient inte kan skicka statusinformation till platsen kan platsen generera en avisering. Administrativa användare som får dessa aviseringar kan vidta omedelbara åtgärder för att återställa klientens normala funktion.  

### <a name="clients-cache-information-to-use-in-the-future"></a>Klienter cachelagrar information som ska användas i framtiden

När en klient kommunicerar med en hanterings plats kan klienten hämta och cachelagra följande information:  

- Klientinställningar  

- Klient scheman  

- Information om program varu distributioner och en nedladdning av den program vara som klienten är schemalagd att installera, när distributionen konfigureras för den här åtgärden.  

När en klient inte kan kontakta en hanterings plats cachelagrar klienterna lokalt status-, tillstånds-och klient information som de rapporterar till platsen. Klienten överför dessa data när den upprättar kontakt med en hanterings plats.  

### <a name="client-can-submit-status-to-a-fallback-status-point"></a>Klienten kan skicka status till en återställnings status plats

När du konfigurerar en-klient för att använda en återställnings status plats ger du en ytterligare kontakt punkt för klienten för att skicka viktig information om åtgärden. Klienter som är konfigurerade för att använda en återställnings status punkt fortsätter att skicka status om sina åtgärder till plats system rollen även när klienten inte kan kommunicera med en hanterings plats.  

### <a name="central-management-of-client-data-and-client-identity"></a>Central hantering av klient data och klient identitet

Plats databasen, i stället för den enskilda klienten, behåller viktig information om varje klients identitet och kopplar dessa data till en viss dator eller användare.  

- Klientens källfiler på en dator kan avinstalleras och installeras om utan att de historiska posterna för den dator där-klienten är installerad påverkas.  

- En klient dators haveri påverkar inte integriteten för den information som lagras i-databasen. Den här informationen kan vara tillgänglig för rapportering.  


## <a name="options-for-sites-and-site-system-roles-that-arent-highly-available"></a><a name="bkmk_nonHAoptions"></a>Alternativ för platser och plats system roller som inte har hög tillgänglighet

Flera-plats system har inte stöd för flera instanser på en plats eller i hierarkin. Den här informationen kan hjälpa dig att förbereda för de här plats systemen som går offline.  

### <a name="asset-intelligence-synchronization-point-hierarchy"></a>Plats för synkronisering av till gångs information (hierarki)

Den här plats system rollen anses inte vara verksamhets kritisk och innehåller valfria funktioner i Configuration Manager. Om det här plats systemet är offline kan du använda något av följande alternativ:  

- Lös orsaken till att plats systemet är offline.  

- Avinstallera rollen från den aktuella servern och installera rollen på en ny server.  

### <a name="endpoint-protection-point-hierarchy"></a>Endpoint Protection-plats (hierarki)

Den här plats system rollen anses inte vara verksamhets kritisk och innehåller valfria funktioner i Configuration Manager. Om det här plats systemet är offline kan du använda något av följande alternativ:  

- Lös orsaken till att plats systemet är offline.  

- Avinstallera rollen från den aktuella servern och installera rollen på en ny server.  

### <a name="enrollment-point-site"></a>Registrerings plats (plats)

Den här plats system rollen anses inte vara verksamhets kritisk och innehåller valfria funktioner i Configuration Manager. Om det här plats systemet är offline kan du använda något av följande alternativ:  

- Lös orsaken till att plats systemet är offline.  

- Avinstallera rollen från den aktuella servern och installera rollen på en ny server.  

### <a name="enrollment-proxy-point-site"></a>Proxy för registrerings plats (plats)

Den här plats system rollen anses inte vara verksamhets kritisk och innehåller valfria funktioner i Configuration Manager. Du kan dock installera flera instanser av den här plats system rollen på en plats och på flera platser i hierarkin. Om det här plats systemet är offline kan du använda något av följande alternativ:  

- Lös orsaken till att plats systemet är offline.  

- Avinstallera rollen från den aktuella servern och installera rollen på en ny server.  

Om du har fler än en proxyserver för registrering på en plats använder du ett DNS-alias för Server namnet. När du använder den här konfigurationen tillhandahåller DNS Round Robin viss fel tolerans och belastnings utjämning för när användare registrerar sina mobila enheter.  

### <a name="fallback-status-point-site-or-hierarchy"></a>Återställnings status plats (plats eller hierarki)

Den här plats system rollen anses inte vara verksamhets kritisk och innehåller valfria funktioner i Configuration Manager. Om det här plats systemet är offline kan du använda något av följande alternativ:  

- Lös orsaken till att plats systemet är offline.  

- Avinstallera rollen från den aktuella servern och installera rollen på en ny server. Eftersom klienter tilldelas återställnings status platsen under klient installationen måste du ändra befintliga klienter så att de använder den nya plats system servern.  

### <a name="service-connection-point-hierarchy"></a>Tjänst anslutnings punkt (hierarki)

Även om den här plats system rollen är viktig för att hålla Configuration Manager aktuella grenen uppdaterad, används vanligt vis inte ofta. Använd något av följande alternativ om systemet är offline:

- Lös orsaken till att plats systemet är offline.  

- Avinstallera rollen från den aktuella servern och installera rollen på en ny server.  


## <a name="see-also"></a>Se även

- [Konfigurationer som stöds](../../../plan-design/configs/supported-configurations.md)  

- [Rekommenderad maskinvara](../../../plan-design/configs/recommended-hardware.md)  

- [Operativsystem som stöds för platssystemservrar](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)

- [Plats och krav för platssystem](../../../plan-design/configs/site-and-site-system-prerequisites.md)  

- [Påverkan av webbplatsfel](../../manage/site-failure-impacts.md)  
