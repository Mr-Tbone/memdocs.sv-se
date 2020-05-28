---
title: Distribuera virtuella App-V-program
titleSuffix: Configuration Manager
description: Se vilka överväganden du måste tänka på när du skapar och distribuerar virtuella program.
ms.date: 03/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df6f550b21523e365055f6a4cdafadca7603c4bf
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906376"
---
# <a name="deploy-app-v-virtual-applications-with-configuration-manager"></a>Distribuera virtuella App-V-program med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du använder Configuration Manager för att hantera virtuella program får du följande fördelar:  

-   En enda hanterings infrastruktur  

-   Funktioner för skalbarhet, distribution och innehålls distribution, t. ex. samlingar och mappning mellan användare och enhet  

-   Avancerade program hanterings funktioner  

-   Distribution av operativ system, program vara och maskin varu inventering, avläsning av program vara och till gångs information för att stödja virtuella program  

Mer information om hur du skapar och sekvenserar program med Microsoft Application Virtualization (App-V) finns i [Application Virtualization 4-dokumentationen](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v4/).  

Förutom de andra Configuration Manager krav och procedurer för att skapa ett program måste du tänka på följande när du skapar och distribuerar virtuella program:

-   Om du vill distribuera virtuella program till datorer måste du ha Configuration Manager klienten och App-V-klienten installerad på datorerna. Stationära och bärbara datorer samt VDI-klienter (Virtual Desktop Infrastructure) kan vara klientenheter. Configuration Manager-och App-V-klientprogramvaran arbetar tillsammans för att leverera, lokalisera och starta paket med virtuella program. Den Configuration Manager klienten hanterar leveransen av virtuella programpaket till App-V-klienten. App-V-klienten kör det virtuella programmet på klienten.  

-   Om du vill distribuera ett virtuellt program måste du först skapa det virtuella programmet genom att använda App-V Application Virtualization Sequencer. Sekvenseraren övervakar installationsprocessen för ett program och registrerar den information som krävs för att applikationen ska köras i en virtuell miljö. Du kan också använda sekvenseraren för att ange vilka filer och konfigurationer som gäller för alla användare och vilka konfigurationer som användare kan anpassa.  

-   När du sekvenserar ett program måste du spara paketet på en plats som Configuration Manager har åtkomst till. Du kan sedan skapa en programdistribution som innehåller det här virtuella programmet.  

-   Configuration Manager stöder inte användning av den delade skrivskyddade cache-funktionen i App-V 4,6.  

-   Configuration Manager stöder funktionen Shared Content Store i App-V 5.  

-   När du skapar en distributions typ för ett virtuellt program skapar Configuration Manager distributions typen genom att använda innehållet i program manifest filen. Det här är en XML-fil som innehåller information om det virtuella programmet. Dessutom skapar Configuration Manager krav för distributions typen baserat på innehållet i OSD-filen i App-V som innehåller information om de operativ system som stöds för det virtuella programmet.  

-   För att distribuera virtuella program i Configuration Manager måste klient datorerna ha minst App-V 4,6 SP1 eller en senare version av-klienten installerad.  

-   Innan du kan distribuera virtuella program uppdaterar du App-V-klienten med den senaste snabb korrigeringen. Mer information finns i [aktuell lista över app-v 4,5-och app-v 4,6-fil versioner](https://support.microsoft.com/help/2950945/current-list-of-app-v-4-5-and-app-v-4-6-file-versions).

-   När du använder anslutnings grupper i App-V 5,0 kan de distribuerade virtuella programmen dela samma fil system och register på klient datorerna. Till skillnad från virtuella program kan dessa program dela data med varandra. Dessutom behåller anslutningsgrupper användarinställningarna för de program som de innehåller. Virtuella App-V-miljöer i Configuration Manager används för att konfigurera anslutnings grupper på klient datorer. Virtuella miljöer skapas eller ändras på klientdatorer när programmet installeras eller när klienter sedan utvärderar de installerade programmen. Du kan prioritera dessa program så att när flera program försöker att ändra ett filsystem eller ett registervärde så har programmet med den högsta prioriteten företräde. Mer information finns i [skapa virtuella App-V-miljöer](../../apps/deploy-use/create-app-v-virtual-environments.md).  

##  <a name="supported-app-v-versions"></a> App-V-versioner som stöds  
 Configuration Manager stöder följande versioner av App-V:  

-   **App-v 4,6**: om du vill använda virtuella program i Configuration Manager måste app-v 4,6 SP1, app-v 4,6 SP2 eller app-v 4,6 SP3-klienten vara installerad på klient datorerna.  

     Innan du kan distribuera virtuella program uppdaterar du App-V 4,6-klienten med den senaste snabb korrigeringen. Mer information finns i [aktuell lista över app-v 4,5-och app-v 4,6-fil versioner](https://support.microsoft.com/help/2950945/current-list-of-app-v-4-5-and-app-v-4-6-file-versions).  

-   **App-v 5, app-v 5,0 SP1, App-V 5,0 SP2, app-v 5,0 SP3 och app-v 5,1**: för app-v 5,0 SP2 måste du installera [Hotfix Package 5](https://support.microsoft.com/help/2963211) eller använda app-v 5,0 SP3.  
-   **App-V 5,2**: Detta är inbyggt i Windows 10 Education (1607 och senare), Windows 10 Enterprise (1607 och senare) och windows Server 2016.

Mer information om App-V i Windows 10 finns i följande avsnitt:

- [Vad är nytt i App-V](https://docs.microsoft.com/windows/application-management/app-v/appv-about-appv)
- [Komma igång med App-V för Windows 10](https://docs.microsoft.com/windows/application-management/app-v/appv-getting-started)
- [Uppgradera till App-V för Windows 10 från en befintlig installation](https://docs.microsoft.com/windows/application-management/app-v/appv-upgrading-to-app-v-for-windows-10-from-an-existing-installation)

##  <a name="steps-to-manage-app-v-virtual-applications"></a>Steg för att hantera virtuella App-V-program  
 Följ dessa steg om du vill hantera virtuella App-V-program:  

1.   **Sekvens**: sekvensering är en process där ett program konverteras till ett virtuellt program med hjälp av App-V-sekvenseraren.

2.   **Skapa**: Använd guiden skapa distributions typ för att importera det sekvenserade programmet till en Configuration Manager distributions typ som du sedan kan lägga till i ett program. Du kan även skapa virtuella miljöer där flera virtuella program tillåts dela inställningar.

3.   **Distribuera**: distribution är en process som gör App-V-program tillgängliga på Configuration Manager distributions platser.

4.   **Distribuera**: distribution är en process som gör programmet tillgängligt på klient datorer. Detta kallas för publicering och strömning i en fullständig App-V-infrastruktur.  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Metoder för att leverera virtuella program med Configuration Manager  
Configuration Manager stöder två metoder för leverans av virtuella program till klienter: strömmande leverans och lokal leverans (Hämta och kör).

När du bestämmer vilken leverans metod som ska användas jämför du det reducerade disk utrymmes kravet för strömnings leverans mot garanterad tillgänglighet för App-V-program i lokal leverans. Det utökade diskutrymmet på klienten som krävs för lokal leverans kan vara att föredra framför strömmande leverans, eftersom användarna då alltid har programmet tillgängligt, var de än är.  

###  <a name="streaming-delivery"></a>Strömmande leverans
När du använder Configuration Manager för att hantera App-V-klienten, stöds strömning av virtuella program via HTTP eller HTTPS från en distributions plats. Strömning via HTTP eller HTTPS är aktiverat som standard och har kon figurer ATS i dialog rutan för distributions plats egenskaper. När du distribuerar ett virtuellt program till klient datorer och en användare kör det virtuella programmet, kontaktar Configuration Manager-klienten en hanterings plats för att avgöra vilken distributions plats som ska användas. Sedan strömmas programmet från distributions platsen.  

Använd informationen i den här tabellen för att få hjälp att avgöra om streaming Delivery är den bästa leverans metoden för dig:

|Fördelar|Nackdelar|  
|----------------|-------------------|  
|Med den här metoden används standardnätverksprotokoll för att strömma paketinnehåll från distributionsplatser.<br /><br /> Programgenvägar till virtuella program anropar en anslutning till distributionsplatsen, så det virtuella programmet levereras på begäran.<br /><br /> Den här metoden fungerar bra för klienter med snabba anslutningar till distributionsplatserna.<br /><br /> Uppdaterade virtuella program som distribueras i företaget är tillgängliga eftersom klienterna tar emot en princip som informerar dem om att den aktuella versionen har ersatts. Bara ändringarna jämfört med den tidigare versionen laddas ned.<br /><br /> Åtkomstbehörigheter som definieras på distributionsplatsen förhindrar användare från att komma åt program eller paket de inte har behörighet till.|Virtuella program strömmas inte förrän användaren kör programmet för första gången. I det här scenariot kan en användare erhålla programgenvägar till virtuella program och sedan koppla ned anslutningen från nätverket innan de virtuella programmen körs för första gången. Om användaren försöker köra det virtuella programmet medan klienten är offline ser användaren ett fel och kan inte köra det virtualiserade programmet eftersom en Configuration Manager distributions plats inte är tillgänglig för att strömma programmet. Programmet blir inte tillgängligt förrän användaren återansluter till nätverket och kör det.<br /><br /> Du kan undvika detta genom att använda den lokala leveransmetoden för leverans av virtuella program till klienter, eller så kan du aktivera internetbaserad klienthantering för strömmande leverans.|  

###  <a name="local-delivery-download-and-execute"></a>Lokal leverans (hämta och kör)  
Att ladda ned och köra är den vanligaste metoden när du använder Configuration Manager eftersom den här metoden liknar hur andra program format levereras med Configuration Manager. När du använder den lokala leverans metoden laddar den Configuration Manager klienten först ned hela det virtuella programpaketet i Configuration Manager-klientcachen. Configuration Manager instruerar App-V-klienten att strömma programmet från Configuration Manager cacheminne till App-V-cachen. Om du distribuerar ett virtuellt program till klient datorer och dess innehåll inte finns i App-V-cachen, strömmar App-V-klienten program innehållet från Configuration Manager klientcachen till App-V-cachen och kör sedan programmet. När programmet har körts kan du ange Configuration Manager-klienten för att ta bort alla äldre versioner av paketet vid nästa borttagnings cykel, eller för att spara dem i Configuration Manager klientcachen. Att spara innehåll lokalt kan dra nytta av innehålls optimerings metoder för paket innehåll som BranchCache och PeerCache.

Använd informationen i den här tabellen för att avgöra om lokal leverans är den bästa leverans metoden för dig:   

|Fördelar|Nackdelar|  
|----------------|-------------------|  
|Standarddistributionsplatsens funktion används för att ladda ned paketet med hjälp av BITS (Background Intelligent Transfer Service).<br /><br /> Innehållet i virtuella programpaket levereras lokalt till klienten. Det innebär att användarna kan köra dem när datorn inte är ansluten till nätverket.<br /><br /> Den här metoden lämpar sig för långsamma eller otillförlitliga nätverksanslutningar och för datorer som bara ansluter till nätverket ibland.<br /><br /> Configuration Manager använder RDC (Remote Differential Compression) för att skicka till klienter enbart de byte i filerna som har ändrats när innehållet i det virtuella programpaketet uppdateras. Configuration Manager-klienten använder RDC för att bygga en ny version av ett virtuellt applikations paket baserat på den aktuella versionen av paketet och eventuella ändringar som skickas till klienten.<br /><br /> Den här metoden ger mobila och nedkopplade användare möjlighet att använda programmet. Administratörer kan välja att spara paketet i Configuration Manager cache efter leverans om det virtuella programmet distribuerades med en installations åtgärd. Paketet i Configuration Manager-klientcachen fungerar som en lokal, tillförlitlig strömnings källa för App-V-klienten för att hämta paketet till dess cacheminne.|Disk utrymme som motsvarar upp till två gånger det virtuella programpaketets storlek krävs på klienten när det virtuella programmet sparas i Configuration Manager cache.|  

###  <a name="deployment-from-an-image"></a>Distribution från en avbildning

Du kan även förinstallera virtuella program på en dator och sedan skapa en avbildning av datorn för distribution till andra datorer. Men om det virtuella programpaketet har skapats på en annan plats kommer den binära delta-replikeringen inte att användas för att hämta uppdateringar till programmet. Detta alternativ kan vara bra att ta till i en infrastruktur med virtuella datorer om man vill att program ska bli tillgängliga omedelbart i stället för att programmen hämtas efter det att användaren har loggat in.    

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a> Migrera från en App-V-infrastruktur till en infrastruktur med Configuration Manager och App-V  
Använd följande tabell som hjälp för att planera en migrering från en befintlig App-V-infrastruktur till hantering av virtuella program med Configuration Manager.  

|Steg|Mer information|  
|----------|----------------------|  
|Undersök dina befintliga virtuella program och välj de program som du vill migrera till din Configuration Manager-infrastruktur.|Ingen ytterligare information.|  
|Gå igenom användarna och enheterna till vilka de virtuella programmen ska distribueras.|Skapa Configuration Manager samlingar för att gruppera samman de användare och enheter som du vill distribuera de virtuella programmen till. Se [Introduktion till samlingar](../../core/clients/manage/collections/introduction-to-collections.md).|  
|Migrera anslutnings grupper i App-V 5 till Configuration Manager virtuella miljöer.|Se avsnittet [migrera App-V 5-anslutnings grupper till Configuration Manager virtuella miljöer](deploying-app-v-virtual-applications.md#migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments) i det här avsnittet.|  
|Undersök för att ta reda på om något av dina virtuella program finns som fullständiga program i Configuration Manager-infrastrukturen.|Hanteringen förenklas om du lägger till virtuella program som en ny distributionstyp i det befintliga, fullständiga programmet. Se [skapa program](../../apps/deploy-use/create-applications.md).|  
|Skapa program för att ersätta befintliga App-V-paket.|Se [Introduktion till program hantering](../understand/introduction-to-application-management.md) och [skapa program](../../apps/deploy-use/create-applications.md).|  
|Configuration Manager börjar hantera virtuella program på en klient efter den första distributionen av ett virtuellt program. Efter detta måste Configuration Manager hantera alla App-V-program på datorn.|Ingen ytterligare information.|  
|Distribuera innehållet till de lämpliga distributionsplatserna så aktiveras lokal leverans av program.|Se [Hantera innehåll och innehålls infrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Distribuera programmet till Configuration Manager-klienter.<br /><br /> Om App-V-programmet skapades med en tidigare version av sekvenseraren som inte skapar en manifest-XML-fil, kan du öppna det och spara det i en senare version av sekvenseraren för att skapa filen. Den här filen krävs för att distribuera virtuella program med Configuration Manager.<br /><br /> App-V stöder de virtuella programpaket som skapas med SoftGrid 4,1 SP1 eller 4,2-versioner av sekvenseraren.<br /><br /> Om programmen tidigare installerades lokalt, måste du avinstallera dem innan du distribuerar en virtuell version av dem.|Se [distribuera program](../../apps/deploy-use/deploy-applications.md).|  
|Configuration Manager kan inte längre använda paket och program som innehåller virtuella program. När du migrerar från Configuration Manager 2007 till Configuration Manager nuvarande gren konverterar Configuration Manager dessa paket till program.<br /><br /> Configuration Manager 2007-annonser omvandlas till följande distributions typer:<br /><br /> – Migrera App-V-paket utan annons: en distributions typ som använder standardinställningarna för distributions typen.<br /><br /> – Migrera App-V-paket med en annons: en distributions typ som använder samma inställningar som <br />                Configuration Manager 2007-annonsering.<br /><br /> – Migrera App-V-paket med flera annonser: en distributions typ för varje <br />                Configuration Manager 2007-annonsering som använder inställningarna för den annonsen.|Se [Planera för migrering av objekt till Configuration Manager aktuella grenen](../../core/migration/planning-for-the-migration-of-objects.md).|  

##  <a name="migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Migrating App-V 5 connection groups to Configuration Manager virtual environments  
Virtuella App-V-miljöer i Configuration Manager tillåta virtuella program som du har distribuerat för att dela samma fil system och register på klient datorer. Detta innebär att dessa program kan dela data med varandra, till skillnad från vanliga virtuella program. Virtuella miljöer skapas eller ändras på klientdatorer när programmet installeras eller när klienter sedan utvärderar de installerade programmen. Virtuella miljöer liknar anslutnings grupper i fristående App-V 5.  

När du migrerar anslutnings grupper från fristående App-V 5 till Configuration Manager virtuella miljöer, måste du se till att Configuration Manager korrekt hanterar de anslutnings grupper som redan finns på klient datorer och att användarens miljö i dessa anslutnings grupper bevaras.  

Så här konverterar du anslutnings grupper i App-V 5 till Configuration Manager virtuella miljöer:  

1.  Skapa Configuration Manager-program för alla program som fanns i App-V.  

2.  Distribuera programmen till användare och enheter med distributionssyftet **Obligatorisk**. Distributioner till användare måste distribueras till samma användare som använde programmet i App-V. Distributioner till datorer måste distribueras till samma datorer som hade programmet i App-V.  

3.  När distributionen är färdig skapar du virtuella miljöer som matchar de anslutnings grupper som publiceras i fristående App-V. Den virtuella miljön måste ha samma paket (särskilt App-V 5-distributions typer) i samma ordning.  

Information om hur du skapar en virtuell App-V-miljö finns i [så här skapar du virtuella app-v-miljöer](../../apps/deploy-use/create-app-v-virtual-environments.md).  

Du kan också ta bort alla anslutnings grupper från App-V-klienten innan du börjar distribuera program med Configuration Manager. Men alla inställningar som användare kan ha sparat i App-V-anslutningssträngar går förlorade.  

##  <a name="dynamic-suite-composition-in-app-v-46"></a>Dynamic Suite Composition i App-V 4.6  
Dynamisk Suite-komposition är en funktion som gör att du kan definiera ett virtuellt programpaket som ett beroende av ett annat virtuellt programpaket. När programmet körs är App-V-klienten värd för det primära paketet och beroendepaketet i samma virtuella miljö för programmet.  

För att du ska kunna använda den här funktionen med Configuration Manager måste båda paketen distribueras och registreras med App-V-klienten. För att säkerställa att det beroende paket innehållet finns lokalt på klient datorn konfigurerar du program distributionen för lokal leverans (Hämta och kör).  

Mer information om App-V Dynamic Suite Composition finns i dokumentationen till App-V.  

##  <a name="converting-app-v-46-applications-to-app-v-5-applications"></a>Konvertera App-V 4.6-program till App-V 5-program  
Programpaketsformatet har ändrats mellan App-V 4.6 och App-V 5. Program som har sekvenserats med App-V 4.6 stöds inte längre. Men App-V 5 har ett paket konverterings verktyg som du kan använda för att konvertera program. Mer information finns i [så här konverterar du ett paket som skapats i en tidigare version av App-V](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/how-to-convert-a-package-created-in-a-previous-version-of-app-v).  

Följ dessa anvisningar när du konverterar App-V 4.6-program till App-V 5-program:  

1.  Konvertera eller sekvensera om App-V 4,6-paketen till App-V 5-formatet.  

2.  Distribuera App-V 5-klienten till datorer i din hierarki.  

3.  Skapa nya program som innehåller distributionstyper för dina App-V 5-program, och skapa ersättningsregler så att App-V 4.6-programmen kan ersättas.  

4.  Skapa virtuella miljöer efter behov.  

5.  Distribuera de nya App-V 5-programmen till datorerna.  

##  <a name="user-and-deployment-configuration-files"></a> Konfigurationsfiler för användare och distribution  
Konfigurationsfiler för användare och distribution har inställningar som styr hur ett program fungerar. Du kan använda dessa filer om du vill ändra program inställningar utan att ändra ordningsföljd för programmet.  

Ett typiskt App-V 5-program skulle kunna innehålla följande filer:  

-   En Programpakets fil (. AppV)  

-   En användar konfigurations fil  

-   En distributions konfigurations fil  

Användar konfigurations filen innehåller inställningar som bara gäller den inloggade användaren. Du kan till exempel redigera konfigurationsfilerna för att ändra informationen om den program gen väg som ska distribueras till användarna. Du kan också skapa ett Configuration Manager program med flera distributions typer. Varje distributions typ kan innehålla en annan användar konfigurations fil och använda krav regler för att säkerställa att dessa installeras för relevanta användare.  

Distributions konfigurations filen innehåller inställningar som gäller för datorn, till exempel register inställningar. Filen kan även innehålla användar inställningar som tillämpas på alla användare.  

Om du vill distribuera virtuella App-V 5-program med Configuration Manager måste alla tre filerna finnas i samma mapp när du skapar distributions typen App-V 5. Om det finns flera filer i mappen kommer Configuration Manager använda den senaste.  

Mer information finns i om den [dynamiska konfigurationen av App-V 5,0](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/about-app-v-50-dynamic-configuration).  

##  <a name="app-v-local-interaction"></a> Local Interaction i App-V  
I vissa program distributions scenarier installeras program lokalt på klient datorerna och andra program distribueras som virtuella program till samma klient dator. Som standard kan inte program som installeras lokalt se eller kommunicera direkt med virtualiserade program. Detta är det avsedda beteendet för program isoleringen som App-V tillhandahåller. Lokal interaktion är en funktion i App-V-klienten som du kan aktivera för varje program så att lokalt installerade program som körs på en klient dator kan se och kommunicera med virtualiserade program. Configuration Manager och App-V har fullt stöd för lokal interaktion.  

Mer information om funktionen App-V Local Interaction finns i dokumentationen till App-V.  

##  <a name="app-v-5-shared-content-store"></a>Shared Content Store i App-V 5  
Configuration Manager stöder den delade innehålls lagrings funktionen i App-V 5. Mer information finns i [Planera för App-V 5.0 Shared Content Store (SCS)](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/planning-for-the-app-v-50-sequencer-and-client-deployment#planning-for-the-app-v-50-shared-content-store-scs).  

##  <a name="monitoring-virtual-applications"></a>Övervaka virtuella program  

### <a name="virtual-application-reports"></a>Rapporter över virtuella program  
Du kan använda följande rapporter för att övervaka App-V i din Configuration Manager-miljö:  

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|Resultat för virtuella App-V-miljöer|Visar information om en vald virtuell miljö som är i ett angivet tillstånd för en vald samling (endast App-V 5).|  
|Resultat för resurs i den virtuella App-V-miljön|Visar information om en vald virtuell miljö för en angiven till gång och alla distributions typer för den valda virtuella miljön (endast App-V 5).|  
|Status för den virtuella App-V-miljön|Visar kompatibilitetsinformation för en vald virtuell miljö för en vald samling. Kolumnen **kvarhållen** i den här rapporten visar de till gångar där en virtuell miljö som tidigare har kon figurer ATS inte längre är tillämplig, men den behålls för att bevara användar inställningar i program som körs i den virtuella miljön (endast App-V 5).|  
|Datorer med ett specifikt virtuellt program|Visar en översikt över datorer som har den angivna App-V-genvägen att Application Virtualization Management Sequencer skapas (endast App-V 4,6).|  
|Datorer med ett specifikt virtuellt programpaket|Visar en lista med datorer som har det angivna App-V-programpaketet installerat (endast App-V 4,6).|  
|Antalet instanser av alla programpaket|Visar antalet identifierade App-V-programpaket (endast App-V 4,6).|  
|Antalet instanser av alla program|Visar antalet identifierade App-V-program (endast App-V 4,6).|  

### <a name="log-files"></a>Loggfiler  
Configuration Manager registrerar information om virtuella program distributioner i loggfiler. Information om loggfiler som virtuella program och Configuration Manager program hantering använder finns i [loggfiler](../../core/plan-design/hierarchy/log-files.md).  

För Windows 8,1 hittar du loggar för App-V-klienten i C:\ProgramData\Microsoft\Application Virtualization-klienten.  
