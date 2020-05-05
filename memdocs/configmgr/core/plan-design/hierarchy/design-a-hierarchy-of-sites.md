---
title: Utforma en platshierarki
titleSuffix: Configuration Manager
description: Förstå tillgängliga topologier och hanterings alternativ för Configuration Manager att planera din platshierarki.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e14cf57e962d7bc90cc39db9ecfea68d9c5b00e
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073355"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>Skapa en hierarki med webbplatser för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du installerar den första platsen i en ny Configuration Manager-hierarki, är det en bra idé att förstå:  

- Tillgängliga topologier för Configuration Manager  

- Typerna av tillgängliga platser och deras relationer med varandra  

- Hanterings området som varje typ av plats tillhandahåller  

- Alternativ för innehålls hantering som kan minska antalet platser som du behöver installera  

Planera sedan en topologi som effektivt hanterar dina nuvarande affärs behov och kan senare expandera för att hantera framtida tillväxt.  

När du planerar bör du tänka på begränsningar för att lägga till ytterligare platser i en hierarki eller en fristående plats:  

- Installera en ny primär plats under en central administrations plats, upp till det [Antal primära platser som stöds](../configs/size-and-scale-numbers.md) för hierarkin.  

- [Expandera en fristående primär plats för att installera en ny central administrations plats](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)och installera sedan ytterligare primära platser.  

- Installera nya sekundära platser under en primär plats, upp till den [gräns som stöds för den primära platsen](../configs/size-and-scale-numbers.md) och den övergripande hierarkin.  

- Du kan inte lägga till en tidigare installerad plats i en befintlig hierarki för att slå samman två fristående platser. Configuration Manager stöder endast installation av nya platser i en befintlig hierarki av webbplatser.  


> [!NOTE]  
> När du planerar en ny installation av Configuration Manager bör du vara medveten om [viktig information](../../servers/deploy/install/release-notes.md), som detaljerade aktuella problem i de aktiva versionerna. Viktig information gäller för alla grenar av Configuration Manager. När du använder den [tekniska förhands gransknings grenen](../../get-started/technical-preview.md)hittar du problem som är specifika för den grenen i dokumentationen för varje version av den tekniska för hands versionen.  



##  <a name="hierarchy-topology"></a><a name="bkmk_topology"></a>Topologi för hierarki  

Hierarkins topologier sträcker sig från:  

- Enklaste: en enda fristående primär plats  

- Mest komplexa: en grupp anslutna primära och sekundära platser med en central administrations plats på den översta nivån i hierarkin  

Nyckel driv rutinen för typen och antalet webbplatser som du använder i en hierarki är vanligt vis antalet och typen av enheter som du måste ha stöd för.   

### <a name="standalone-primary-site"></a>Fristående primär plats

Använd en fristående primär plats när den har stöd för hantering av alla enheter och användare. Mer information finns i [storleks ändring och skalnings nummer](../configs/size-and-scale-numbers.md). Den här topologin lyckas också när ditt företags geografiska platser kan hanteras av en enda primär plats. Du kan hantera nätverks trafik genom att använda flera hanterings platser i gränser grupper och en noggrant planerad innehålls infrastruktur. Mer information finns i [Konfigurera gränser grupper](../../servers/deploy/configure/boundary-groups.md) och [grundläggande begrepp för innehålls hantering](fundamental-concepts-for-content-management.md).  

Den här topologin ger följande fördelar:  

- Förenklar det administrativa arbetet  

- Förenklar klientplatstilldelningen och identifieringen av tillgängliga resurser och tjänster  

- Eli minering av möjliga fördröjningar införd av databasreplikering mellan platser  

- Alternativ för att expandera en fristående primär plats till en större hierarki med en central administrations plats. Med det här alternativet kan du installera nya primära platser för att utöka skalan för din distribution.  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>Central administrations plats med en eller flera underordnade primära platser 

Använd den här topologin om du behöver mer än en primär plats för att stödja hantering av alla enheter och användare. Det krävs när du behöver använda mer än en primär plats. 

Den här topologin ger följande fördelar:  

- Den har stöd för upp till 25 primära platser som gör att du kan utöka skalan i hierarkin.    

- Du använder alltid den centrala administrations platsen, såvida du inte installerar om dina platser. Det här alternativet är permanent. Du kan inte koppla från en underordnad primär plats så att den blir en fristående primär plats.  



##  <a name="determine-when-to-use-a-central-administration-site"></a><a name="BKMK_ChooseCAS"></a>Avgöra när en central administrations plats ska användas  

Använd en central administrations plats för att konfigurera inställningar för hela hierarkin och för att övervaka alla platser och objekt i hierarkin. Den här plats typen hanterar inte klienter direkt. Den koordinerar replikering mellan plats-till-plats, som innehåller konfigurationen av platser och klienter inom hela hierarkin.  

Följande information kan hjälpa dig att planera för en central administrationswebbplats:  

- Den centrala administrations platsen är platsen på den översta nivån i en hierarki.  

- När du konfigurerar en hierarki som har fler än en primär plats installerar du en central administrations plats.  

     - Om du omedelbart behöver två eller flera primära platser installerar du den centrala administrations platsen först.  

     - Om du redan har en primär plats och vill installera en central administrations plats [expanderar du den fristående primära platsen](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) för att installera den centrala administrations platsen.  

- Den centrala administrations platsen stöder endast primära platser som underordnade platser.  

- Den centrala administrations platsen kan inte ha tilldelade klienter.  

- Den centrala administrations platsen har inte stöd för plats system roller som direkt stöder klienter, till exempel hanterings platser och distributions platser.  

- Hantera alla klienter i hierarkin och utför alla plats hanterings aktiviteter från Configuration Manager-konsolen som är ansluten till den centrala administrations platsen. De här uppgifterna omfattar installation av hanterings platser eller andra plats system roller på underordnade primära eller sekundära platser.  

- När du använder en central administrations plats är det bara den plats där du ser plats data från alla platser i hierarkin. Dessa data omfattar information som inventerings data och status meddelanden.  

- Konfigurera identifierings åtgärder inom hela hierarkin från den centrala administrations platsen. På den centrala administrations platsen tilldelar du identifierings metoder som ska köras på enskilda primära platser.  

- Hantera säkerhet i hela hierarkin genom att tilldela olika säkerhets roller, säkerhets omfattningar och samlingar till olika administrativa användare. Dessa konfigurationer gäller för varje plats i hierarkin.  

- Konfigurera replikering för att styra kommunikationen mellan platser i hierarkin. Schemalägg databasreplikering för plats data och hantera bandbredden för överföring av filbaserade data mellan platser.  



##  <a name="determine-when-to-use-a-primary-site"></a><a name="BKMK_ChoosePriimary"></a>Avgöra när en primär plats ska användas  

Använd primära platser för att hantera klienter. Installera en primär plats som en underordnad plats under en central administrations plats, eller som den första platsen i en ny hierarki. En primär plats som är den första platsen i en hierarki skapar en fristående primär plats. Både underordnade primära platser och fristående primära platser stöder sekundära platser.  

Överväg att lägga till ytterligare primära platser av följande orsaker:  

- Om du vill öka antalet enheter kan du hantera med en enda hierarki.  

- För att möta hanteringskraven inom din organisation. Du kan till exempel installera en primär plats på en fjärrplats för att hantera överföringen av distributions innehåll över ett nätverk med låg bandbredd.  

     - Överväg att i stället använda alternativ för att begränsa nätverks bandbredden när du överför data till en distributions plats. Den innehålls hanterings funktionen kan ersätta behovet av att installera ytterligare platser.  


Följande information kan hjälpa dig att avgöra när du ska installera en primär plats:  

- En primär plats kan vara en fristående primär plats eller en underordnad primär plats i en större hierarki. När en primär plats ingår i en hierarki med en central administrationsplats använder platserna databasreplikering för att replikera data mellan platserna. Om du inte behöver stöd för fler klienter och enheter än vad en enda primär plats stöder kan du överväga att installera en fristående primär plats. När du har installerat en fristående primär plats expanderar du den om det behövs i framtiden för att rapportera till en ny central administrations webbplats för att skala upp din distribution.  

- En primär plats har endast stöd för en central administrations plats som överordnad plats.  

- En primär plats har endast stöd för sekundära platser som underordnade platser och har stöd för flera sekundära platser.  

- Primära platser ansvarar för att behandla alla klient data från de tilldelade klienterna.  

- Primära platser använder databasreplikering för att kommunicera direkt med den centrala administrations platsen. Detta beteende konfigureras automatiskt när en ny plats installeras.  



##  <a name="determine-when-to-use-a-secondary-site"></a><a name="BKMK_ChooseSecondary"></a>Avgöra när du ska använda en sekundär plats  

Använd sekundära platser för att hantera överföringen av distributions innehåll och klient data över nätverk med liten bandbredd.  

Du hanterar en sekundär plats från en central administrations plats eller den sekundära platsens direkt överordnade primära plats. Sekundära platser är kopplade till en primär plats. Du kan inte flytta dem till en annan överordnad plats utan att avinstallera dem och sedan installera om dem som en underordnad plats under den nya primära platsen.

Du kan dock dirigera innehåll mellan två sekundära peer-platser för att hjälpa till att hantera den filbaserade replikeringen av distributions innehåll. Den sekundära platsen använder filbaserad replikering för att överföra klient data till en primär plats. En sekundär plats använder även databasreplikering för att kommunicera med den överordnade primära platsen.  

Överväg att installera en sekundär plats om något av följande villkor gäller:  

- Du behöver inte en lokal anslutnings punkt för en administrativ användare.  

- Du måste hantera överföringen av distributions innehåll till platser som finns lägre i hierarkin.  

- Du måste hantera klient information som skickas till platser som finns högre upp i hierarkin.  

Om du inte vill installera en sekundär plats och du har klienter på fjärrplatser, bör du överväga följande alternativ:  

- Använda peer-to-peer-tekniker som Windows BranchCache  

- Aktivera distributions platser för bandbredds kontroll och schemaläggning   

Använd dessa alternativ för innehålls hantering med eller utan sekundära platser. De hjälper till att minska storleken på din Configuration Manager-infrastruktur. Mer information om alternativ för innehålls hantering i Configuration Manager finns i [avgöra när du ska använda alternativ för innehålls hantering](#BKMK_ChooseSecondaryorDP).  


Följande information kan hjälpa dig att avgöra när du ska installera en sekundär plats:  

- Om en lokal instans av SQL Server inte är tillgänglig installeras sekundära plats servrar automatiskt SQL Server Express under plats installationen.  

- Installation av sekundär plats initieras från Configuration Manager-konsolen, i stället för att köra installations programmet direkt på en dator.  

- Sekundära platser använder en delmängd av informationen i plats databasen. Det här beteendet minskar mängden data som SQL replikerar mellan den överordnade primära platsen och den sekundära platsen.  

- Sekundära platser stöder routning av filbaserat innehåll till andra sekundära platser som har en gemensam överordnad primär plats.  

- Sekundära plats installationer installerar automatiskt hanterings platsen och plats system rollerna för distributions platsen på den sekundära plats servern.  



##  <a name="determine-when-to-use-content-management-options"></a><a name="BKMK_ChooseSecondaryorDP"></a>Avgöra när du ska använda alternativ för innehålls hantering  

Om du har klienter på fjärrnätverksplatser bör du överväga att använda ett eller flera alternativ för innehållshantering i stället för en primär eller sekundär plats. Följande alternativ tar ofta bort behovet av att installera en plats:  

- Leverans optimering för Windows 10  

- Configuration Manager peer-cache  

- Windows BranchCache  

- Konfigurera distributions platser för bandbredds kontroll  

- Kopiera innehåll till distributions platser manuellt (Förinstallera innehåll)  


Om något av följande villkor gäller, bör du överväga att distribuera en distributions plats i stället för att installera en annan plats:  

- Nätverks bandbredden räcker för att klient datorer på fjärrplatsen ska kunna kommunicera med en hanterings plats på den primära platsen. Klienterna kommunicerar med en hanterings plats för att ladda ned klient principer, skicka inventering, skicka rapporterings status och skicka identifierings information.  

- Background Intelligent Transfer Service (BITS) ger inte tillräckligt med bandbredds kontroll för dina nätverks krav.  

Mer information om alternativ för innehålls hantering i Configuration Manager finns i [grundläggande begrepp för innehålls hantering](fundamental-concepts-for-content-management.md).  



##  <a name="beyond-hierarchy-topology"></a><a name="bkmk_beyond"></a>Bortom hierarkins topologi  

Förutom den inledande topologin för hierarkin bör du även tänka på följande frågor:  

- Vilka plats system roller tillhandahåller tjänster eller funktioner från olika platser i hierarkin?  

- Hur hanterar du konfigurationer och funktioner i hela hierarkin i din infrastruktur?  


Följande vanliga överväganden beskrivs i separata artiklar. Den här informationen är viktig för att påverka eller påverkas av hierarkin:  

- När du förbereder för att [hantera datorer och enheter](../../clients/manage/manage-clients.md)bör du fundera över om enheterna är lokala, i molnet eller inkludera användar ägda enheter (BYOD). Tänk också på hur du hanterar enheter som stöder flera hanterings alternativ. Du kan till exempel hantera Windows 10-enheter med Configuration Manager eller integrera med Microsoft Intune. Mer information finns i [Välj en lösning för enhets hantering](../choose-a-device-management-solution.md).  

- Förstå hur din tillgängliga nätverks infrastruktur kan påverka flödet av data mellan fjärranslutna platser. Mer information finns i [förbereda din nätverks miljö](../network/configure-firewalls-ports-domains.md). Överväg också den geografiska platsen för dina användare och enheter och om de får åtkomst till din infrastruktur via ditt lokala nätverk eller Internet.  

- Planera för en innehålls infrastruktur för att effektivt distribuera det innehåll som du distribuerar till enheter som du hanterar. Det här innehållet kan vara program, program uppdateringar eller operativ system. Mer information finns i [Hantera innehåll och innehålls infrastruktur](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

- Ta reda [på vilka funktioner och funktioner i Configuration Manager](../changes/features-and-capabilities.md) du planerar att använda. Olika funktioner kräver olika plats system roller eller Windows-infrastruktur. I en hierarki med flera platser bestämmer du var du vill distribuera dem för den mest effektiva användningen av dina nätverks-och server resurser.  

- Överväg säkerheten för data och enheter, inklusive användning av en PKI (Public Key Infrastructure). Mer information finns i [krav för PKI-certifikat](../network/pki-certificate-requirements.md).  


Läs följande artiklar om sitespecifika konfigurationer:  

- [Planera för SMS-providern](plan-for-the-sms-provider.md)  

- [Planera för platsdatabasen](plan-for-the-site-database.md)  

- [Planera för platssystemservrar och platssystemroller](plan-for-site-system-servers-and-site-system-roles.md)  

- [Planera för säkerhet](../security/plan-for-security.md)  

- [Hantera nätverkets bandbredd](manage-network-bandwidth.md) vid distribution av innehåll inom en plats  


Överväg konfigurationer som sträcker sig över platser och hierarkier  

- [Alternativ för hög tillgänglighet](../../servers/deploy/configure/high-availability-options.md) för platser och hierarkier

- [Utöka Active Directory-schemat](../network/extend-the-active-directory-schema.md) och konfigurera platser för att [publicera plats data](../../servers/deploy/configure/publish-site-data.md)  

- [Dataöverföringar mellan platser](data-transfers-between-sites.md)  

- [Grunderna i rollbaserad administration](../../understand/fundamentals-of-role-based-administration.md)  

- [Hantera klienter på Internet](../../clients/manage/manage-clients-internet.md)  

