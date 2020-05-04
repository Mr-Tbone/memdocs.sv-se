---
title: Hantera Windows som en tjänst
titleSuffix: Configuration Manager
description: Visa statusen för Windows som en tjänst (WaaS) med Configuration Manager, skapa Service planer för att skapa distributions ringar och visa aviseringar när Windows 10-klienter närmar sig slutet av supporten.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9a682ec0b3d438a26429486f119d641fd150404f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710841"
---
# <a name="manage-windows-as-a-service-using-configuration-manager"></a>Hantera Windows som en tjänst med hjälp av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I Configuration Manager kan du Visa status för Windows som en tjänst (WaaS) i din miljö. Skapa Service planer för att skapa distributions ringar och se till att Windows 10-system hålls uppdaterade när nya versioner släpps. Du kan också visa aviseringar när Windows 10-klienter närmar sig slutet på supporten för den halvårs Visa versionen.

Mer information om underhålls alternativ för Windows 10 finns i [Översikt över Windows som en tjänst](/windows/deployment/update/waas-overview#servicing-channels).

Använd följande avsnitt för att hantera Windows som en tjänst.

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a>Krav

Om du vill se data i service instrument panelen för Windows 10 måste du göra följande:

- Windows 10-datorer måste använda Configuration Manager program uppdateringar med Windows Server Update Services (WSUS) för hantering av program uppdateringar. När datorer använder Windows Update för företag (eller Windows Insiders) för hantering av program uppdateringar utvärderas inte datorn i Service planer för Windows 10. Mer information finns i [Integrering med Windows Update för företag i Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).

- Använd en WSUS-version som stöds:
  - WSUS-10.0.14393 (roll i Windows Server 2016)
  - WSUS-10.0.17763 (roll i Windows Server 2019) (kräver Configuration Manager 1810 eller senare)
  - WSUS 6,2 och 6,3 (roll i Windows Server 2012 och Windows Server 2012 R2)
    - [Kb 3095113 och KB 3159706 (eller motsvarande uppdatering) måste installeras](../../sum/plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012) på WSUS 6,2 och 6,3.

- Aktivera pulsslagsidentifiering. Data som visas i serviceinstrumentpanelen för Windows 10 hittas genom identifiering. Mer information finns i [Konfigurera pulsslagsidentifiering](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc).

    Följande Windows 10-kanal och build-information identifieras och lagras i följande attribut:  

    - **Beredskaps gren för operativ system**: anger operativ systemets kanal. Till exempel **0** = halvårs kanal-mål (Skjut inte upp uppdateringar), **1** = halvårs kanal (Skjut upp uppdateringar), **2** = långsiktig service kanal (LTSC)

    - **Operativ system version**: anger operativ systemets version. Till exempel **10.0.10240** (RTM) eller **10.0.10586** (version 1511)

- Tjänst anslutnings punkten måste vara installerad och konfigurerad för läget **online, permanent anslutning** för att se data på service instrument panelen för Windows 10. När du arbetar i offlineläge ser du inte data uppdateringar i instrument panelen förrän du har Configuration Manager underhålls uppdateringar. Mer information finns i [om tjänst anslutnings punkten](../../core/servers/deploy/configure/about-the-service-connection-point.md).

- Internet Explorer 9 eller senare måste vara installerat på datorn som kör Configuration Manager-konsolen.

- Programuppdateringar måste konfigureras och synkroniseras. Välj klassificeringen **uppgraderingar** och synkronisera program uppdateringar innan du kan uppgradera Windows 10-funktioner i Configuration Manager-konsolen. Mer information finns i [förbereda för hantering av program uppdateringar](../../sum/get-started/prepare-for-software-updates-management.md).

- Från och med Configuration Manager version 1902 kontrollerar du [klient inställningen](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority) **Ange tråd prioritet för funktions uppdateringar för** att säkerställa att den är lämplig för din miljö.

- Från och med Configuration Manager version 1906, verifiera [klient inställningen](../../core/clients/deploy/about-client-settings.md#bkmk_du) **aktivera dynamisk uppdatering för funktions uppdateringar** för att säkerställa att den är lämplig för din miljö. <!--4062619-->

## <a name="windows-10-servicing-dashboard"></a><a name="BKMK_ServicingDashboard"></a> Serviceinstrumentpanel för Windows 10

Serviceinstrumentpanelen för Windows 10 ger dig information om Windows 10-datorer i din miljö, aktiva serviceplaner, kompatibilitetsinformation osv. Data i serviceinstrumentpanelen för Windows 10 är beroende av att tjänstanslutningspunkten är installerad. Instrumentpanelen innehåller följande ikoner:

- **Panelen användning i Windows 10**: ger en uppdelning av offentliga versioner av Windows 10. Windows Insiders build-versioner visas som **andra** samt alla versioner som ännu inte är kända för din plats. Tjänst anslutnings punkten hämtar metadata som informerar den om Windows-versionerna och sedan jämförs dessa data med identifierings data.

- **Panel för Windows 10-ringar**: tillhandahåller en uppdelning av Windows 10 efter kanal och beredskaps tillstånd. LTSC-segmentet innehåller alla LTSC-versioner. Den första panelen delar ned de olika versionerna, till exempel Windows 10 LTSC 2015.

- **Panelen skapa service plan**: ger ett snabbt sätt att skapa en service plan. Du anger namnet, samling (visar endast de 10 viktigaste samlingarna efter storlek, minsta först), distributions paket (visar bara de 10 högsta paketen efter det som senast ändrades) och beredskaps tillstånd. Standardvärden används för de andra inställningarna. Klicka på **Avancerade inställningar** för att starta guiden Skapa service plan där du kan konfigurera alla inställningar för service planen.

- **Ikonen Har gått ut**: Visar procentandelen enheter som har en version av Windows 10 som har förfallit. Configuration Manager anger procent andelen av de metadata som tjänst anslutnings punkten laddar ned och jämför den med identifierings data. En version som har varit i slutet av livet tar inte längre upp månads vis ackumulerade uppdateringar, som innehåller säkerhets uppdateringar. Datorerna i den här kategorin bör uppgraderas till nästa version. Configuration Manager avrundar uppåt till närmaste heltal. Om du till exempel har 10 000 datorer och bara en på en utgången version visar panelen 1%.

- **Ikonen Upphör snart att gälla**: Visar hur många procent av datorerna som är på en version som håller på att förfalla (inom ca fyra månader), på samma sätt som ikonen **Har gått ut** . Configuration Manager avrundar uppåt till närmaste heltal.

- **Ikonen Aviseringar**: Visar aktiva aviseringar.

- **Övervaknings panel för service plan**: Visa Service planer som du har skapat och ett diagram över kompatibiliteten för varje. Den här panelen ger dig en snabb överblick över det aktuella läget för distributioner av Service planer. Om en tidigare distributionsring uppfyller dina förväntningar för kompatibilitet kan du sedan välja en senare serviceplan (distributionsring) och klicka på **Distribuera nu** istället för att vänta på att reglerna för serviceplanen ska utlösas automatiskt.

- **Panelen Windows 10-versioner**: Visa är en fast tids linje för bilder som ger dig en översikt över de Windows 10-versioner som för närvarande är publicerade och ger dig en allmän uppfattning om när du skapar en över gång till olika tillstånd. Den här panelen togs bort från och med Configuration Manager version 1902 eftersom mer detaljerad information finns på [instrument panelen för produktens livs cykel](../../core/clients/manage/asset-intelligence/product-lifecycle-dashboard.md). <!--3446861-->

> [!IMPORTANT]
> Informationen som visas i serviceinstrumentpanelen för Windows 10 (till exempel livscykeln för support för Windows 10-versioner) har angetts för att underlätta för dig och ska enbart användas internt på företaget. Du bör inte lita enbart på den här informationen för att säkerställa uppdateringskompatibiliteten. Se till att kontrollera att den information som du har fått stämmer.

## <a name="drill-through-required-updates"></a>Granska nödvändiga uppdateringar
<!--4224414-->
*(Lanseras i version 1906)*

Du kan gå igenom efterlevnads statistik för att se vilka enheter som kräver en speciell uppdatering av Windows 10-funktionen. Om du vill visa enhets listan måste du ha behörighet att visa uppdateringar och de samlingar som enheterna tillhör. Så här ökar du detalj nivån i enhets listan:

1. Gå till **program varu biblioteket** > **Windows 10-Underhåll** > **alla Windows 10-uppdateringar**.
1. Välj en uppdatering som krävs av minst en enhet.
1. Titta på fliken **Sammanfattning** och hitta cirkel diagrammet under **statistik**.
1. Välj hyperlänken **vy som krävs** bredvid cirkel diagrammet för att öka detalj nivån i enhets listan.
1. Den här åtgärden tar dig till en tillfällig nod under **enheter** där du kan se vilka enheter som kräver uppdateringen. Du kan också utföra åtgärder för noden, till exempel skapa en ny samling från listan.

## <a name="servicing-plan-workflow"></a>Arbetsflöde för serviceplan

Service planer för Windows 10 i Configuration Manager är ungefär som automatiska distributions regler för program uppdateringar. Du skapar en service plan med följande kriterier som Configuration Manager utvärderar:

- **Klassificeringen Uppgraderingar**: Endast uppdateringar med klassificeringen **Uppgraderingar** utvärderas.

- **Beredskapstillstånd**: Beredskapstillståndet som definierats i serviceplanen jämförs med beredskapstillståndet för uppgraderingen. Metadata för uppgraderingen hämtas när tjänstanslutningspunkten söker efter uppdateringar.

- **Tidsfördröjning**: Antalet dagar som du anger för **Hur många dagar efter att Microsoft har publicerat en ny uppgradering vill du vänta innan du distribuerar den i din miljö** i serviceplanen. Om det aktuella datumet infaller efter lanserings datumet plus det konfigurerade antalet dagar, Configuration Manager utvärderas om du vill inkludera en uppgradering i distributionen.

  När en uppgradering uppfyller kriterierna lägger serviceplanen till uppgraderingen i distributionspaketet, distribuerar paketet till distributionsplatser och distribuerar uppgraderingen till samlingen baserat på de inställningar som du konfigurerar i serviceplanen. Du kan övervaka distributioner i panelen Service Plan Monitoring (Övervakning av serviceplan) på serviceinstrumentpanelen för Windows 10. Mer information finns i [övervaka program uppdateringar](../../sum/deploy-use/monitor-software-updates.md).

> [!NOTE]
> **Windows 10, version 1903 och senare** har lagts till i Microsoft Update som sin egen produkt, i stället för att vara en del av **Windows 10** -produkten som tidigare versioner. Den här ändringen gjorde att du utför ett antal manuella åtgärder för att se till att dina klienter ser dessa uppdateringar. Vi har hjälpt till att minska antalet manuella åtgärder som du behöver vidta för den nya produkten i Configuration Manager version 1906. Mer information finns i [Konfigurera produkter för versioner av Windows 10](../../sum/get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later).<!--4682946-->

## <a name="windows-10-servicing-plan"></a><a name="BKMK_ServicingPlan"></a> Serviceplan för Windows 10

När du distribuerar Windows 10-halvårs kanal kan du skapa en eller flera Service planer för att definiera de distributions ringar som du vill ha i din miljö och sedan övervaka dem i service instrument panelen för Windows 10. Serviceplaner använder bara programuppdateringar med klassificeringen **Uppgraderingar** , inte kumulativa uppdateringar för Windows 10. För dessa uppdateringar måste du fortfarande distribuera med hjälp av arbets flödet för program uppdateringar. Slutanvändarens upplevelse av en serviceplan är densamma som med programuppdateringar, inklusive inställningarna som du konfigurerar i serviceplanen.  

> [!NOTE]
> Du kan använda en aktivitetssekvens för att distribuera en uppgradering för varje Windows 10-version, men det krävs mer manuellt arbete. Du skulle behöva importera de uppdaterade källfilerna som ett uppgraderingspaket för operativsystemet och sedan skapa och distribuera aktivitetssekvensen till rätt datorer. I en aktivitetssekvens finns dock fler anpassade alternativ, till exempel för- och efterdistributionsåtgärder.

Du kan skapa en grundläggande serviceplan från serviceinstrumentpanelen för Windows 10. När du har angett namnet, samling (visar endast de 10 viktigaste samlingarna efter storlek, minsta först), distributions paket (visar bara de 10 högsta paketen efter det som senast ändrades) och beredskaps tillstånd. Configuration Manager skapar service planen med standardvärden för de andra inställningarna. Du kan också starta guiden Skapa serviceplan för att konfigurera alla inställningarna. Följa stegen nedan om du vill skapa en serviceplan med hjälp av guiden Skapa serviceplan.  

> [!NOTE]  
> Du kan hantera beteendet för distributioner med hög risk. En distribution med hög risk är en distribution som installeras automatiskt och kan orsaka oönskade resultat. Exempel: En aktivitetssekvens som har syftet **Obligatoriskt** och som distribuerar Windows 10 anses vara en högriskdistribution. Mer information finns i [Inställningar för att hantera distributioner med hög risk](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

### <a name="to-create-a-windows-10-servicing-plan"></a>Skapa en serviceplan i Windows 10

1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.

1. I arbetsytan Programbibliotek expanderar du **Windows 10-underhåll**och klickar sedan på **Serviceplaner**.

1. På fliken **Start** går du till gruppen **Skapa** och klickar på **Skapa serviceplan**. Guiden Skapa serviceplan öppnas.

1. På sidan **Allmänt** konfigurerar du följande inställningar:

    - **Namn**: Ange namnet på serviceplanen. Namnet måste vara unikt, hjälpa till att beskriva målet med regeln och identifiera det från andra på den Configuration Manager webbplatsen.

    - **Beskrivning**: Ange en beskrivning av serviceplanen. Beskrivningen bör ge en översikt över service planen och annan relevant information som hjälper till att identifiera och särskilja planen bland andra på den Configuration Manager webbplatsen. Beskrivningsfältet är valfritt, har en begränsning på 256 tecken och har ett tomt värde som standard.

1. På sidan service plan anger du **mål samlingen**. Medlemmar i samlingen får Windows 10-uppgraderingar som är definierade i serviceplanen.

    - När du distribuerar en högrisk distribution, till exempel service plan, visar fönstret **Välj samling** bara de anpassade samlingar som uppfyller de verifierings inställningar för distribution som kon figurer ATS i platsens egenskaper.

    - Distributioner med hög risk är alltid begränsade till anpassade samlingar, samlingar som du skapar och den inbyggda samlingen **Okända datorer** . När du skapar en distribution med hög risk kan du inte välja en inbyggd samling, till exempel **alla system**. Avmarkera **Dölj samlingar med ett större antal medlemmar än platsens minsta storleks konfiguration** för att se alla anpassade samlingar som innehåller färre klienter än den konfigurerade maximala storleken. Mer information finns i [Inställningar för att hantera distributioner med hög risk](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

    - Verifieringsinställningarna för distribution baseras på samlingens aktuella medlemskap. När du har distribuerat service planen utvärderas inte samlings medlemskapet igen för distributions inställningarna med hög risk.

      - Anta till exempel att du ställer in **standard storleken** på 100 och den **maximala storleken** till 1000. När du skapar en distribution med hög risk visar fönstret **Välj samling** endast samlingar som innehåller färre än 100 klienter. Om du avmarkerar inställningen **Dölj samlingar med ett större antal medlemmar än platsens minsta storleks konfiguration** visas samlingar som innehåller färre än 1000 klienter.  
      När du väljer en samling som innehåller en plats roll gäller följande kriterier:
        - Om samlingen innehåller en plats system Server och i verifierings inställningarna för distributionen som du konfigurerar för att blockera samlingar med plats system servrar, uppstår ett fel och du kan inte fortsätta.
        - Om samlingen innehåller en platssystemserver och du i verifieringsinställningarna för distribution konfigurerar att varna dig om samlingar har platssystemservrar, om samlingen överstiger standardvärdet för storlek eller om samlingen innehåller en server, visas en varning om hög risk i guiden Distribuera programvara. Du måste acceptera att skapa en distribution med hög risk och ett revisionsstatusmeddelande skapas.

1. Konfigurera följande inställningar på sidan Distributionsring:

   - **Ange det beredskaps tillstånd för Windows som underhålls planen ska gälla**: Välj något av följande alternativ:

      - **Halvårs kanal (riktad)**: i den här underhålls modellen är funktions uppdateringar tillgängliga så fort Microsoft publicerar dem.

      - **Halvårs kanal**: den här underhålls kanalen används vanligt vis för bred distribution. Windows 10-klienter i halvårs kanal får samma version av Windows 10 som enheterna i mål kanalen, precis vid ett senare tillfälle.

        Mer information om underhålls kanaler och vilka alternativ som passar dig bäst finns i [underhålls kanaler](/windows/deployment/update/waas-overview#servicing-channels).

   - **Hur många dagar efter att Microsoft har publicerat en ny uppgradering vill du vänta innan du distribuerar i din miljö**: om det aktuella datumet infaller efter lanserings datumet plus antalet dagar som du konfigurerar för den här inställningen, kan Configuration Manager utvärdera om en uppgradering ska inkluderas i distributionen.

1. På sidan uppgraderingar konfigurerar du Sök kriterierna för att filtrera uppgraderingarna som läggs till i tjänste planen. Endast uppgraderingar som uppfyller de angivna villkoren läggs till i den associerade distributionen. Följande egenskaps filter är tillgängliga: <!--3098809, 3113836, 3204570 -->

   - **Arkitektur** (från och med version 1810)
   - **Språk**
   - **Produkt kategori** (från och med version 1810)
   - **Obligatoriskt**
      > [!IMPORTANT]
      > Vi rekommenderar att du som en del av Sök villkoren ställer in det **obligatoriska** fältet med värdet **>= 1**. Genom att använda det här kriteriet ser du till att endast tillämpliga uppdateringar läggs till i tjänste planen.
   - **Ersatt** (startar i version 1810)
   - **Avdelning**

    Klicka på **Förhandsgranska** för att visa uppgraderingarna som uppfyller de angivna kriterierna.

1. Konfigurera följande inställningar på sidan Distributionsschema:

   - **Schema utvärdering**: ange om Configuration Manager utvärderar den tillgängliga tid-och installations tids gränsen genom att använda UTC eller lokal tid för den dator som kör Configuration Manager-konsolen.

       > [!NOTE]
       > När du väljer lokal tid och väljer **så snart som möjligt** för **tillgänglig tid för program vara** eller tids **gräns för installation**, används den aktuella tiden på datorn som kör Configuration Manager-konsolen för att utvärdera när uppdateringar är tillgängliga eller när de installeras på en klient. Om klienten finns i en annan tidszon inträffar åtgärderna när klientens tid når utvärderingstiden.

   - **Tillgänglig tid för programvara**: Välj en av följande inställningar för att ange när programuppdateringarna är tillgängliga för klienter:

        - **Så snart som möjligt**: Välj den här inställningen för att göra programuppdateringar som ingår i distributionen tillgängliga för klientdatorer så snart som möjligt. När du skapar distributionen med den här inställningen aktive ras Configuration Manager uppdaterar klient principen. Vid nästa avsöknings cykel för klient princip blir klienterna medvetna om distributionen och kan hämta de uppdateringar som är tillgängliga för installation.

        - **Angiven tid**: Välj den här inställningen för att göra programuppdateringar som ingår i distributionen tillgängliga för klientdatorer vid ett specifikt datum och en specifik tidpunkt. När du skapar distributionen med den här inställningen aktive rad uppdaterar Configuration Manager klient principen. Vid nästa avsökningscykel informeras klienterna om distributionen. Program uppdateringarna i distributionen är dock inte tillgängliga för installation förrän efter det konfigurerade datumet och den angivna tiden.

   - **Tidsgräns för installation**: Välj någon av följande inställningar för att ange installationstidsgränsen för programuppdateringar i distributionen:

        - **Så snart som möjligt**: Välj den här inställningen om du vill installera programuppdateringarna automatiskt i distributionen så snart som möjligt.

        - **Angiven tid**: Välj den här inställningen om du vill installera programuppdateringar automatiskt i distributionen vid ett specifikt datum och en specifik tidpunkt. Configuration Manager **bestämmer tids gränsen** för att installera program uppdateringar genom att lägga till det konfigurerade tidsintervallet till **tillgänglig tid för program vara**.

           > [!NOTE]
           > Den faktiska tidsgränstiden för installationen är den tidsgränstid som visas plus en slumpmässig tidsperiod på upp till 2 timmar. Detta reducerar den potentiella påverkan på alla klientdatorer i den målsamling som installerar uppdateringarna i distributionen samtidigt.
           >
           > Du kan konfigurera **Datoragent** -klientinställningen **Inaktivera slumpmässig tidsgräns** för att inaktivera slumpmässig fördröjning för installationen av obligatoriska uppdateringar. Mer information finns i [Datoragent](../../core/clients/deploy/about-client-settings.md#computer-agent).

        - **Fördröj verk ställandet av den här distributionen enligt användar inställningar, upp till den Respitperiod som definierats på klienten**: Välj det här alternativet om du vill respektera [ **respitperioden för tvång efter distributionens tids gräns (timmar) för** klient inställningen](../../core/clients/deploy/about-client-settings.md#grace-period-for-enforcement-after-deployment-deadline-hours).

1. Konfigurera följande inställningar på sidan Användarupplevelse:  

    - **Användarmeddelanden**: Ange om du vill visa meddelandet om uppdateringar i Software Center på klientdatorn vid den konfigurerade **Tillgänglig tid för programvara** och om du vill visa användarmeddelanden på klientdatorerna.

    - **Beteende för tidsgräns**: Ange det beteende som ska uppvisas när tidsgränsen nås för distributionen av uppdateringen. Ange om uppdateringarna ska installeras i distributionen. Ange också om en systemomstart ska utföras efter installationen av uppdateringen oberoende av den konfigurerade underhållsperioden. Mer information om underhålls perioder finns i [använda underhålls](../../core/clients/manage/collections/use-maintenance-windows.md)perioder.  

    - **Beteende för enhetsomstart**: Ange om en systemomstart ska förhindras på servrar och arbetsstationer efter att uppdateringar har installerats och en systemomstart krävs för att slutföra installationen.

    - **Skrivfilterhantering för Windows Embedded-enheter**: När du distribuerar uppdateringar till Windows Embedded-enheter som är skrivfilteraktiverade kan du ange att uppdateringen ska installeras på det tillfälliga överlägget och antingen att ändringar ska utföras senare eller att ändringarna ska utföras vid installationens tidsgräns eller under underhållsperioden. När du gör ändringar vid installationens tidsgräns eller under en underhållsperiod krävs en omstart och ändringarna är kvar på enheten.
        - När du distribuerar en uppdatering på en Windows Embedded-enhet bör du se till att enheten tillhör en samling som har en konfigurerad underhållsperiod.

    - **Distributions omvärdering för distribution av program uppdateringar vid omstart**: om du vill tvinga en annan utvärderings cykel för uppdaterings distribution efter omstart väljer du alternativet **om någon uppdatering i distributionen kräver en systemomstart kör du utvärderings cykeln för uppdaterings distribution efter omstart**.

1. På sidan distributions paket väljer du ett befintligt distributions paket, inget distributions paket eller konfigurerar följande inställningar för att skapa ett nytt distributions paket:

    1. **Namn**: Ange namnet på distributionspaketet. Det här namnet måste vara unikt och beskriver paket innehållet. Den är begränsad till 50 tecken.

    1. **Beskrivning**: Ange en beskrivning som ger information om distributionspaketet. Använd högst 127 tecken.

    1. **Paketkälla**: Anger platsen för källfilerna för programuppdateringen. Ange en nätverks Sök väg för käll platsen, till exempel ** \\\Server\\\\ShareName sökväg**eller klicka på **Bläddra** för att hitta nätverks platsen. Skapa en delad mapp för distributions paketets källfiler innan du fortsätter till nästa sida.
        - Den källplats för distributionspaketet som du anger får inte användas av något annat programdistributionspaket.
        - Både SMS-providerns datorkonto och användaren som kör guiden för att ladda ned programuppdateringarna måste ha NTFS-behörigheten **Skriva** för nedladdningsplatsen. Du bör noggrant begränsa åtkomsten till nedladdnings platsen för att minska risken för att angripare manipulerar källfilerna för program uppdatering.
        - Du kan ändra paketets käll plats i egenskaperna för distributions paketet när Configuration Manager skapar distributions paketet. Men om du gör det måste du först kopiera innehållet från originalpaketkällan till den nya paketkällan.

    1. **Sändningsprioritet**: Ange sändningsprioriteten för distributionspaketet. Configuration Manager använder sändnings prioriteten för distributions paketet när paketet skickas till distributions platser. Distributions paketen skickas i prioritetsordning: hög, medel eller låg. Paket med identisk prioritering skickas i den ordning de skapades. Om det inte finns någon efter släpning bearbetas paketet omedelbart oavsett prioritet.

    1. **Aktivera binär differentiell replikering**: aktivera det här alternativet om du vill använda binär differentiell replikering.

1. På sidan distributions platser anger du de distributions platser eller distributions plats grupper som är värdar för uppdateringsfilerna. Mer information om distributions platser finns i [Konfigurera en distributions plats](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).

    > [!NOTE]
    > Den här sidan är bara tillgänglig när du skapar ett nytt distributionspaket för programuppdatering.  

1. På sidan Hämtningsplats anger du om du vill ladda ned uppdateringsfiler från Internet eller från ditt lokala nätverk. Konfigurera följande inställningar:

    - **Hämta programuppdateringar från Internet**: Välj den här inställningen för att ladda ned uppdateringar från en angiven plats på Internet. Den här inställningen är aktiverad som standard.

    - **Hämta programuppdateringar från en plats i det lokala nätverket**: Välj den här inställningen för att ladda ned uppdateringarna från en lokal katalog eller delad mapp. Den här inställningen är användbar när den dator som kör guiden inte har Internet åtkomst. Vilken dator som helst med Internetåtkomst kan preliminärt ladda ned uppdateringar och lagra dem på en plats på det lokala nätverket som kan kommas åt från den dator där guiden körs.

1. På sidan Val av språk väljer du de språk för vilka de valda uppdateringarna laddas ned. Uppdateringarna laddas bara ned om de är tillgängliga på de valda språken. Uppdateringar som inte är språkspecifika laddas alltid ned. Som standard väljer guiden de språk som du har konfigurerat i egenskaperna för program uppdaterings platsen. Minst ett språk måste väljas innan du fortsätter till nästa sida. Om du bara väljer språk som inte stöds av en uppdatering Miss lyckas nedladdningen för uppdateringen.

1. Granska inställningarna på sidan Sammanfattning och klicka sedan på **Nästa** för att skapa serviceplanen.  

När du har slutfört guiden körs service planen. Den lägger till uppdateringar som uppfyller de angivna villkoren för en program uppdaterings grupp, laddar ned uppdateringarna till innehålls biblioteket på plats servern, distribuerar uppdateringarna till de konfigurerade distributions platserna och distribuerar sedan program uppdaterings gruppen till klienter i mål samlingen.

## <a name="modify-a-servicing-plan"></a><a name="BKMK_ModifyServicingPlan"></a> Ändra en serviceplan

När du har skapat en grundläggande service plan från service instrument panelen för Windows 10 eller om du behöver ändra inställningarna för en befintlig service plan kan du gå till egenskaperna för service planen.

> [!NOTE]
> Du kan konfigurera inställningar i egenskaperna för service planen som inte är tillgängliga i guiden när du skapar service planen. Guiden använder standardinställningarna för inställningarna för följande: hämtnings inställningar, distributions inställningar och aviseringar.  

Följ stegen nedan för att ändra egenskaperna för en serviceplan. 

### <a name="to-modify-the-properties-of-a-servicing-plan"></a>Ändra egenskaperna för en serviceplan

1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.

1. I arbets ytan program Bibliotek expanderar du **Windows 10-Underhåll**, klickar på **Service planer**och väljer sedan den service plan som du vill ändra.

1. På fliken **Start** klickar du på **Egenskaper** för att öppna egenskaper för den valda serviceplanen.

    Följande inställningar är tillgängliga i egenskaperna för underhålls planen som inte har kon figurer ATS i guiden:

    **Distributions inställningar**: Konfigurera följande inställningar på fliken distributions inställningar:

    - **Använd Wake-on-LAN för att väcka klienter för nödvändiga distributioner**: Ange om Wake-on-LAN ska aktiveras vid tidsgränsen för att skicka aktiveringspaket till datorer som kräver en eller flera uppdateringar i distributionen. Alla datorer som är i vilo läge vid installationens tids gräns är aktive ras så att program uppdaterings installationen kan initieras. Klienter som är i vilo läge och som inte behöver några program uppdateringar i distributionen startas inte. Som standard är den här inställningen inte aktive rad.

        > [!WARNING]
        > Innan du kan använda det här alternativet måste datorer och nätverk har konfigurerats för Wake On LAN.

    - **Detaljnivån**: Ange detaljnivån för tillståndsmeddelanden som rapporteras av klientdatorer.

    **Hämtnings inställningar**: Konfigurera följande inställningar på fliken hämtnings inställningar:

    - Ange om klienten ska ladda ned och installera program uppdateringar när en klient är ansluten till ett långsamt nätverk eller använder en plats för återställnings innehåll.

    - Ange om klienten ska laddas ned och installera program uppdateringar från en återställnings distributions plats när innehållet för program uppdateringarna inte är tillgängligt på en prioriterad distributions plats.

    - **Tillåt att klienter delar innehåll med andra klienter i samma undernät**: Ange om användning av BranchCache ska aktiveras för nedladdning av innehåll. Mer information om BranchCache finns i [grundläggande begrepp för innehålls hantering](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).

    - Ange om du vill att klienter ska kunna ladda ned program uppdateringar från Microsoft Update om program uppdateringar inte är tillgängliga på distributions platser.
        > [!IMPORTANT]
        > Använd inte den här inställningen för service uppdateringar i Windows 10. Configuration Manager (minst till och med version 1610) kan inte hämta Service uppdateringar för Windows 10 från Microsoft Update.

    - Ange om klienter ska kunna ladda ned efter en installationstidsgräns när avgiftsbelagda Internetanslutningar används. Ibland tar Internetleverantören betalt för den mängd data du skickar och tar emot när du använder en Internetanslutning med datapriser.

    **Aviseringar**: på fliken aviseringar konfigurerar du hur Configuration Manager och System Center Operations Manager genererar aviseringar för den här distributionen.
    - Du kan granska tidigare programuppdateringsaviseringar från noden **Programuppdateringar** i arbetsytan **Programvarubibliotek** .

## <a name="next-steps"></a>Nästa steg

Mer information finns i [grunderna i Configuration Manager som en tjänst och Windows som en tjänst](../../core/understand/configuration-manager-and-windows-as-service.md).
