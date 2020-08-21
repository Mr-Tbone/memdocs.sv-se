---
title: Teknisk för hands version 1706
titleSuffix: Configuration Manager
description: Lär dig mer om de funktioner som finns i teknisk för hands version 1706 för Configuration Manager.
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 8c3624f9fc903395b36846170ff3552f32db59dd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692952"
---
# <a name="capabilities-in-technical-preview-1706-for-configuration-manager"></a>Funktioner i Technical Preview 1706 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1706. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa [Technical Preview för Configuration Manager](../../core/get-started/technical-preview.md) för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
- **Issue Name**. Details
    Workaround details.
-->
**Kända problem i den här tekniska för hands versionen:**

- **Flytta distributions plats** – alternativen i-konsolen för att flytta en distributions plats mellan platser kan inte användas med den här versionen på grund av den tekniska för hands versionen av en enda primär plats.

- **Inställningar** för enhetskompatibilitet – du kan uppleva motsatt beteende när du använder de två nya inställningarna för enhetskompatibilitet:
  - **Blockera USB-felsökning på enheten**
  - **Blockera appar från okända källor**

    Om t. ex. administratörer ställer in **blockera USB-felsökning på enheten** till **True**markeras alla enheter som inte har aktiverat USB-felsökning som icke-kompatibla.

**Följande är nya funktioner som du kan prova med den här versionen.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Förbättrade avgränsnings grupper för program uppdaterings platser
<!-- 1324591 -->
Den här versionen innehåller förbättringar för hur program uppdaterings platser fungerar med gränser grupper. Följande sammanfattar det nya återställnings beteendet:
- Återställningen för program uppdaterings platser använder nu en konfigurerbar tid för att återgå till intilliggande gräns grupper, med en minsta tid på 120 minuter.

- Oberoende av återställnings konfigurationen försöker en klient komma åt den senaste program uppdaterings platsen som den använde i 120 minuter. Efter att ha misslyckats med att kontakta servern i 120 minuter, kontrollerar klienten sin pool med tillgängliga program uppdaterings platser så att den kan hitta en ny.

  - Alla program uppdaterings platser i klientens aktuella gränser grupp läggs till i klientens pool omedelbart.

  - Eftersom en klient försöker använda sin ursprungliga server i 120 minuter innan den söker efter en ny, kontaktas inte några ytterligare servrar förrän två timmar har förflutit.

  - Om återställningen till en grann grupp har kon figurer ATS för minst 120 minuter, kommer program uppdaterings platser från den intilliggande gräns gruppen att ingå i klientens pool med tillgängliga servrar.

- Efter att ha misslyckats med att komma åt den ursprungliga servern i två timmar växlar klienten till en kortare cykel för att kontakta en ny program uppdaterings plats.

  Det innebär att om en klient inte kan ansluta till en ny server, väljer den snabbt nästa server från poolen med tillgängliga servrar och försöker kontakta den.

  - Den här cykeln fortsätter tills klienten ansluter till en program uppdaterings plats som den kan använda.
  - Tills klienten hittar en program uppdaterings plats läggs ytterligare servrar till i poolen med tillgängliga servrar när återställnings tiden för varje intilliggande gräns grupp uppfylls.

Mer information finns i [program uppdaterings platser](../servers/deploy/configure/boundary-groups.md#bkmk_sup) i avsnittet gränser grupper för Current Branch.


## <a name="site-server-role-high-availability"></a>Plats server roll hög tillgänglighet
<!-- 1128774 -->
Hög tillgänglighet för plats Server rollen är en Configuration Manager baserad lösning för att installera ytterligare en primär plats server i *passivt* läge. Plats servern för passivt läge är utöver den befintliga primära plats servern i *aktivt* läge. En plats Server för passivt läge är tillgänglig för omedelbar användning vid behov.

En primär plats server i passivt läge:
- Använder samma plats databas som din aktiva plats Server.
- Tar emot en kopia av innehålls biblioteket för aktiva plats servrar, som sedan hålls i synch.
- Skriver inte data till plats databasen, så länge den är i passivt läge.
- Stöder inte installation eller borttagning av valfria plats system roller, så länge den är i passivt läge.

Om du vill göra plats servern för passivt läge till plats servern för det passiva läget kan du befordra den manuellt. Detta växlar den aktiva plats servern till att vara den passiva plats servern. De plats system roller som är tillgängliga på den ursprungliga aktiva läges servern förblir tillgängliga så länge datorn är tillgänglig. Endast plats Server rollen växlar mellan aktivt och passivt läge.

Om du vill installera en plats Server för passivt läge använder du **guiden skapa plats system Server** för att konfigurera en ny plats server med en typ av **primär plats Server** och ett **passivt**läge. Guiden kör sedan Configuration Manager-installationen på den angivna servern för att installera den nya plats servern i passivt läge. När installationen är klar behåller den aktiva läges plats servern den passiva läges plats servern och dess innehålls bibliotek synkroniserat med ändringar eller konfigurationer som du gör till den aktiva plats servern.

### <a name="prerequisites-and-limitations"></a>Krav och begränsningar
- En enda plats server i passivt läge stöds på varje primär plats.

- Plats servern i passivt läge kan vara lokal eller molnbaserad i Azure.

- Både det aktiva läget och det passiva läges plats servrarna måste finnas i samma domän.

- Både det aktiva läget och den passiva läges plats servern måste använda samma plats databas, som måste vara fjärran sluten till datorerna för varje plats Server.

    - SQL Server som är värd för databasen kan använda en standard instans, namngiven instans, SQL Server kluster eller en tillgänglighets grupp som alltid är tillgänglig.

    - Plats servern i passivt läge har kon figurer ATS för att använda samma plats databas som plats servern för det aktiva läget. Plats servern för passivt läge använder dock inte databasen förrän den har befordrats till aktivt läge.

- Datorn som ska köra plats servern för passivt läge:

    - Måste uppfylla [kraven för att installera en primär plats](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).

    - Installerar med källfiler som matchar versionen av plats servern för det aktiva läget.

    - Det går inte att ha en plats system roll från någon plats innan den passiva läges platsen installeras.

- Plats serverns aktiva och passiva läge kan köra olika operativ system eller service pack versioner, så länge de båda fortfarande stöds av din version av Configuration Manager.

- Befordran av plats servern för passivt läge till den aktiva läges servern är manuell. Det finns ingen automatisk redundans.

- Plats system roller kan bara installeras på den plats server som är i aktivt läge.

    - En plats server i aktivt läge stöder alla plats system roller. Det går inte att installera plats system roller på servern när den är i passivt läge.

    - Plats system roller som använder en databas (t. ex. rapporterings platsen) måste ha den databasen på en server som är fjärran sluten från både aktivt läge och plats servrar för passivt läge.

    - SMS_Provider installeras inte på plats servern i passivt läge. Eftersom du måste ansluta till en SMS_Provider för att platsen ska kunna befordra plats servern för passivt läge manuellt till aktivt läge, rekommenderar vi att du [installerar minst en ytterligare instans av providern](../plan-design/hierarchy/plan-for-the-sms-provider.md) på en annan dator.

**Känt problem**:   
I den här versionen visas **status** för följande villkor i-konsolen som numeriska värden i stället för läsbar text:
- 131071 – plats Server installationen misslyckades
- 720895 – det gick inte att avinstallera plats Server rollen
- 851967 – det gick inte att redundansväxla

### <a name="add-a-site-server-in-passive-mode"></a>Lägga till en plats server i passivt läge
1. I-konsolen går du till **Administration**  >  **plats konfiguration**  >  **platser** och startar [guiden Lägg till plats system roller](../servers/deploy/configure/install-site-system-roles.md). Du kan också använda **guiden skapa plats system Server**.

2. På sidan **Allmänt** anger du den server som ska vara värd för plats servern för passivt läge. Den server du anger kan inte vara värd för några plats system roller innan du installerar en plats server i passivt läge.

3. På sidan **urval för system roll** väljer du endast **primär plats server i passivt läge**.

4. För att slutföra guiden måste du ange följande information som används för att köra installations programmet och installera plats Server rollen på den angivna servern:
    - Välj att kopiera installationsfiler från den aktiva plats servern till den nya passiva läges plats servern eller ange en sökväg till en plats som innehåller innehållet på den aktiva plats serverns **CD. Senaste** mappen.

    - Ange samma plats databas server och databas namn som används av plats servern för aktivt läge.

5. Configuration Manager installerar sedan plats servern i passivt läge på den angivna servern.

Om du vill ha en detaljerad installations status går du till **Administration**  >  **plats konfiguration**  >  **platser**.
- Status för plats servern i passivt läge visas som **installation**.

- Välj servern och klicka sedan på **Visa status** för att öppna **installations status för plats Server** för mer detaljerad information.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>Flytta upp plats servern för passivt läge till aktivt läge
När du vill ändra plats servern för passivt läge till aktivt läge gör du det från fönstret **noder** i **Administration**  >  **plats konfiguration**  >  **platser**. Så länge du kan komma åt en instans av SMS_Provider, kan du komma åt platsen för att göra den här ändringen.
1. I fönstret **noder** i Configuration Manager-konsolen väljer du plats servern i passivt läge och väljer sedan **befordra till aktiv**i menyfliksområdet.

2. Den enkla **statusen** för den server som du befordrar visas i fönstret **noder** som **befordran**.

3. När befordran är slutförd visas i kolumnen **status** **OK** för både den nya *aktiva* läges plats servern och för den nya plats servern för *passivt* läge.

4. På plats för **administrations**  >  **plats konfiguration**  >  **Sites**visar namnet på den primära plats servern nu namnet på den nya plats servern för *aktiva* läge.
För detaljerad status, gå till **övervakning**  >  **plats Server status**.
    - I kolumnen **mode** identifieras vilken server som är *aktiv* eller *passiv*.

    - När du befordrar en server från passivt läge till aktivt läge väljer du den plats server som du befordrar till aktiv och väljer sedan **Visa status** från menyfliksområdet. Då öppnas fönstret **plats Server befordran status** som visar mer information om processen.

När en plats server i aktivt läge växlar över till passivt läge görs bara plats system rollen som passiv. Alla andra plats system roller som är installerade på den datorn förblir aktiva och tillgängliga för klienter.


### <a name="daily-monitoring"></a>Daglig övervakning
När du har en primär plats i passivt läge kan du övervaka den dagligen för att säkerställa att den är synkroniserad med den aktiva läges plats servern och är redo att användas. Det gör du genom att gå till **övervakning**  >  **plats Server status**. Här kan du Visa plats servrar för både aktivt läge och passivt läge.

Fliken **Sammanfattning** :
- I kolumnen **mode** identifieras vilken server som är aktiv eller passiv.
- I kolumnen **status** visas **OK** när servern för passivt läge är synkroniserad med den aktiva läges servern.
- Om du vill visa mer information om tillståndet för synkronisering av innehåll klickar du på **Visa status** från innehållets synkroniseringstillstånd. Då öppnas fliken innehålls bibliotek där du kan försöka åtgärda problem med innehålls synkronisering.

Fliken **innehålls bibliotek** :
- Visa **status** för innehåll som synkroniseras från den aktiva plats servern till plats servern för passivt läge.
- Du kan välja innehåll med statusen **misslyckad**och sedan välja **synkronisera markerade objekt** från menyfliksområdet. Den här åtgärden försöker synkronisera om innehållet från innehållets källa till plats servern för passivt läge. Under återställningen visas status som **pågående**och när den är synkroniserad visas den som **slutförd**.

### <a name="try-it-out"></a>prova!
Försök att utföra följande uppgifter och skicka sedan oss **feedback** från fliken **Start** i menyfliksområdet så att vi kan se hur det fungerade:
- Jag kan installera en primär plats i passivt läge.
- Jag kan använda-konsolen för att befordra plats servern för passivt läge för att göra den till den aktiva läges plats servern och bekräfta ändringen av status för båda plats servrarna.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Inkludera förtroende för vissa filer och mappar i en Device Guard-princip
<!-- 1324676 -->
I den här versionen har vi lagt till ytterligare funktioner i hantering av [enhets skydds](../../protect/deploy-use/use-device-guard-with-configuration-manager.md) principer

Du kan nu välja att lägga till förtroende för vissa filer för mappar i en Device Guard-princip. På så sätt kan du:

1. Lösa problem med hanterade installations beteenden
2. Verksamhetsbaserade appar som inte kan distribueras med Configuration Manager
3. Lita på appar som ingår i en distributions avbildning för operativ system.

### <a name="try-it-out"></a>prova!

1. När du skapar en Device Guard-princip klickar du på **Lägg till**på fliken inkluderingar i guiden skapa enhets skydds princip.
2. I dialog rutan **Lägg till betrodd fil eller mapp** anger du information om filen eller mappen som du vill lita på. Du kan antingen ange en lokal fil eller mappsökväg eller ansluta till en fjärran sluten enhet som du har behörighet att ansluta till och ange en sökväg till en fil eller mapp på enheten.
3. Slutför guiden.


## <a name="hide-task-sequence-progress"></a>Dölj förlopp för aktivitetssekvens
<!-- 1354291 -->
I den här versionen kan du styra när förlopp för aktivitetssekvenser visas för slutanvändare med hjälp av en ny variabel. I aktivitetssekvensen använder du **variabel steget Ange aktivitetssekvens** för att ange värdet för variabeln **TSDisableProgressUI** för att dölja eller Visa förlopp för aktivitetssekvens. Du kan använda variabel steget Ange aktivitetssekvens flera gånger i en aktivitetssekvens för att ändra värdet för variabeln. På så sätt kan du dölja eller Visa förlopp för aktivitetssekvens i olika avsnitt i aktivitetssekvensen.

#### <a name="to-hide-task-sequence-progress"></a>Dölja förlopp för aktivitetssekvens
I redigeraren för aktivitetssekvens använder du [variabel steget Ställ in aktivitetssekvens](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) för att ange värdet för variabeln **TSDisableProgressUI** till **Sant** för att dölja förlopp för aktivitetssekvensen.

#### <a name="to-display-task-sequence-progress"></a>Visa förlopp för aktivitetssekvens
I redigeraren för aktivitetssekvens använder du [variabel steget Ställ in aktivitetssekvens](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) för att ange värdet för **TSDisableProgressUI** -variabeln till **falskt** för att Visa förlopp för aktivitetssekvens.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>Ange en annan innehålls plats för att installera innehåll och avinstallera innehåll
<!-- 1097546 -->
I Configuration Manager idag anger du den installations plats som innehåller installationsfilerna för en app. När du anger en installations plats används även detta som avinstallations plats för program innehållet.
När du vill avinstallera ett distribuerat program och appens innehåll inte finns på klient datorn, kommer klienten att ladda ned alla installationsfiler för appen igen innan programmet avinstalleras.
För att lösa det här problemet kan du nu ange både en installations innehålls plats och en valfri avinstallations innehålls plats. Dessutom kan du välja att inte ange en innehålls plats för avinstallation.

### <a name="try-it-out"></a>Prova!

1. I egenskaperna för distributions typen för ett program klickar du på fliken **innehåll** .
2. Konfigurera **installations innehålls platsen** som normal.
3. Välj något av följande för att **Avinstallera innehålls inställningar**:
   - **Samma som för att installera innehåll** – samma innehålls plats används oavsett om du installerar eller avinstallerar programmet.
   - **Ingen avinstallation av innehåll** – Välj detta om du inte vill ange en plats för avinstallation av innehåll för programmet.
   - **Skiljer sig från installera innehåll** – Välj det här om du vill ange en annan plats för avinstallation av innehåll som skiljer sig från installations innehålls platsen.
5. Om du har valt **annorlunda än installera innehåll**, bläddrar du till eller anger platsen för det program innehåll som ska användas för att avinstallera programmet.
6. Klicka på **OK** för att stänga dialog rutan Egenskaper för distributions typ.


## <a name="accessibility-improvements"></a>Förbättrad användbarhet  
<!--1253000 -->
Den här för hands versionen innehåller flera förbättringar av [hjälpmedels funktionerna](../understand/accessibility-features.md) i Configuration Manager-konsolen. Exempel på dessa är:     

**Nya kortkommandon för att flytta runt i-konsolen:**
- Ctrl + M – anger fokus i huvud fönstret (Central).
- Ctrl + T-anger fokus till den översta noden i navigerings fönstret. Om fokus redan finns i fönstret är fokus inställt på den sista noden som du besökte.
- Ctrl + I-anger fokus till fältet för dynamiska länkar under menyfliksområdet.
- CTRL + L – anger fokus till **Sök** fältet när det är tillgängligt.
- CTRL + D – anger fokus till informations fönstret när det är tillgängligt.
- Alt – ändrar fokus in och ut ur menyfliksområdet.

**Allmänna förbättringar:**
- Förbättrad navigering i navigerings fönstret när du skriver in bokstäverna i ett nodnamn.
- Tangent bords navigering via huvudvyn och menyfliksområdet är nu cirkulärt.
- Tangent bords navigering i informations fönstret är nu cirkulär. Om du vill återgå till föregående objekt eller fönster, använder du Ctrl + D och sedan Shift + TABB.
- När du har uppdaterat vyn arbets yta är fokus inställt på arbets ytans huvud fönster.
- Ett problem har åtgärd ATS att aktivera skärm läsare för att meddela namnen på list objekt.
- Du har lagt till tillgängliga namn för flera kontroller på sidan som gör att skärm läsare kan tillkännage viktig information.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Ändringar i guiden Azure-tjänster som stöder Uppgraderingsberedskap
<!-- 1353331 -->
Från och med den här versionen kan du använda guiden Azure-tjänster för att konfigurera en anslutning från Configuration Manager till Uppgraderingsberedskap. Med hjälp av guiden blir det enklare att konfigurera anslutningen genom att använda en gemensam guide för relaterade Azure-tjänster.   

Även om metoden för att konfigurera anslutningen har ändrats, måste krav för anslutningen och hur du använder Uppgraderingsberedskap förbli oförändrade.   

### <a name="prerequisites-for-upgrade-readiness"></a>Krav för Uppgraderingsberedskap
Kraven för en anslutning till Uppgraderingsberedskap är oförändrade från de som är detaljerade för Current Branch av Configuration Manager. De upprepas här för enkelhetens skull:  

**Förutsättningar**
- För att du ska kunna lägga till anslutningen måste din Configuration Managers miljö först konfigurera en [tjänst anslutnings punkt](../servers/deploy/configure/about-the-service-connection-point.md) i ett [online-läge](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes). När du lägger till anslutningen till din miljö kommer den också att installera Microsoft Monitoring Agent på den dator som kör den här plats system rollen.
- Registrera Configuration Manager som ett hanterings verktyg för webb program och/eller webb-API och hämta [klient-ID: t från den här registreringen](/azure/active-directory/develop/quickstart-register-app).
- Skapa en klient nyckel för det registrerade hanterings verktyget i Azure Active Directory.
- I Azure Portal anger du den registrerade webbappen med behörighet att komma åt OMS.

> [!IMPORTANT]       
> När du konfigurerar behörighet att komma åt OMS måste du välja **deltagar** rollen och tilldela den till resurs gruppen för den registrerade appen.

När kraven har kon figurer ATS är du redo att använda guiden för att skapa anslutningen.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Använd guiden Azure-tjänster för att konfigurera Uppgraderingsberedskap
1. I-konsolen går du till **administrations**  >  **Översikt**  >  **Cloud Services**  >  **Azure-tjänster**och väljer sedan **Konfigurera Azure-tjänster** på fliken **Start** i menyfliksområdet för att starta **guiden Azure-tjänster**.

2. På sidan **Azure-tjänster** väljer du **uppgraderingsberedskap anslutningen**och klickar sedan på **Nästa**.

3. På sidan **app** anger du din **Azure-miljö** (den tekniska för hands versionen stöder bara det offentliga molnet). Klicka sedan på **Importera** för att öppna fönstret **Importera appar** .

4. I fönstret **Importera appar** anger du information för en webbapp som redan finns i din Azure AD.
    - Ange ett eget namn för namnet på Azure AD-klienten. Ange sedan klient-ID, program namn, klient-ID, hemlig nyckel för Azure-webbappen och app-ID-URI: n.
    - Klicka på **Verifiera**, och om det är klart klickar du på **OK** för att fortsätta.

5.  På sidan **konfiguration** anger du den prenumeration, resurs grupp och Windows Analytics-arbetsyta som du vill använda med den här anslutningen för att uppgraderingsberedskap.  

6. Klicka på **Nästa** för att gå till sidan **Sammanfattning** och slutför sedan guiden för att skapa anslutningen.


## <a name="new-client-settings-for-cloud-services"></a>Nya klient inställningar för moln tjänster
<!-- 1319883 -->

I den här versionen har vi lagt till två nya klient inställningar för Configuration Manager. Du hittar dessa i avsnittet **Cloud Services** .  De här inställningarna ger dig följande funktioner:

- Styr vilka Configuration Manager-klienter som har åtkomst till en konfigurerad Cloud Management Gateway.
- Registrera automatiskt Windows 10-domänanslutna Configuration Manager-klienter med Azure Active Directory.

De här nya inställningarna hjälper dig att utföra de funktioner som beskrivs i [Configuration Manager 1705 Technical Preview](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management).

### <a name="before-you-start"></a>Innan du börjar

Du måste ha installerat och konfigurerat Azure AD Connect mellan dina lokala Active Directory och din Azure AD-klient.

Om du tar bort anslutningen avregistreras inte enheterna, men inga nya enheter registreras.

### <a name="try-it-out"></a>prova!

1. Konfigurera följande klient inställningar (finns i Cloud Services)-avsnittet med hjälp av informationen i [så här konfigurerar du klient inställningar](../clients/deploy/configure-client-settings.md).
   - **Registrera automatiskt nya Windows 10-domänanslutna enheter med Azure Active Directory** – Ställ in på **Ja** (standard) eller **Nej**.
   - **Gör det möjligt för klienter att använda en Cloud Management Gateway** – Ställ in på **Ja** (standard) eller **Nej**.
2. Distribuera klient inställningarna till den obligatoriska samlingen av enheter.

Bekräfta att enheten är ansluten till Azure AD genom att köra kommandot **dsregcmd.exe/status** i kommando tolkens fönster. I fältet **AzureAdjoined** i resultatet visas **Ja** om enheten är Azure AD-ansluten.

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Skapa och kör PowerShell-skript från Configuration Manager-konsolen
<!-- 1236459 -->

I Configuration Manager kan du distribuera skript till klient enheter med hjälp av paket och program. I den här tekniska för hands versionen har vi lagt till nya funktioner som gör att du kan vidta följande åtgärder:

- Importera PowerShell-skript till Configuration Manager
- Redigera skripten från Configuration Manager-konsolen (endast för osignerade skript)
- Markera skript som godkända eller nekade för att förbättra säkerheten
- Kör skript på samlingar av Windows-klientdatorer och lokala hanterade Windows-datorer. Du distribuerar inte skript istället körs de i nära real tid på klient enheter.
- Granska resultaten som returnerades av skriptet i Configuration Manager-konsolen.


### <a name="prerequisites"></a>Förutsättningar

Om du vill använda skript måste du vara medlem i lämplig Configuration Manager säkerhets roll.

- **För att importera och skapa skript** – ditt konto måste ha behörighet att **skapa** behörigheter för **SMS-skript** i säkerhets rollen **Fullständig administratör** .
- **För att godkänna eller neka skript** – ditt konto måste ha behörigheten **Godkänn** för **SMS-skript** i säkerhets rollen **Fullständig administratör** .
- **För att köra skript** – ditt konto måste ha behörighet att **köra skript** för **samlingar** i säkerhets rollen för **Compliance Settings Manager** .

Mer information om Configuration Manager säkerhets roller finns i [grunderna i rollbaserad administration](../understand/fundamentals-of-role-based-administration.md).

Som standard kan användare inte godkänna ett skript som de har skapat. Eftersom skript är kraftfulla, mångsidiga och kan distribueras till många enheter har vi introducerat ett nytt begrepp som ger möjlighet att separera rollerna mellan den person som skapar skriptet och den person som godkänner skriptet. Detta ger ytterligare säkerhets nivåer för att köra ett skript utan överblick. Du kan stänga av detta sekundära godkännande för enklare testning, särskilt under den tekniska för hands versionen.

För att tillåta användare att godkänna egna skript:

1. Klicka på **Administration**i Configuration Manager-konsolen.
2. I arbetsytan **Administration** expanderar du **Platskonfiguration**och klickar sedan på **Platser**.
3. Välj din plats i listan över platser och klicka sedan på **Inställningar för hierarki**i gruppen **platser** på fliken **Start** .
4. På fliken **Allmänt** i dialog rutan **Egenskaper för hierarkiskt egenskaper** avmarkerar du kryss rutan **Tillåt inte att skript författare godkänner sina egna skript**.


### <a name="try-it-out"></a>prova!

#### <a name="import-and-edit-a-script"></a>Importera och redigera ett skript

1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.
2. I arbets ytan **program bibliotek** klickar du på **skript**.
3. På fliken **Start** går du till gruppen **skapa** och klickar på **skapa skript**.
4. Konfigurera följande på sidan **skript** i guiden **skapa skript** :
   - **Skript namn** – ange ett namn för skriptet. Även om du kan skapa flera skript med samma namn, blir det svårare för dig att hitta det skript du behöver i Configuration Manager-konsolen.
   - **Skript språk** – för närvarande stöds endast **PowerShell** -skript.
   - **Importera** – importera ett PowerShell-skript till-konsolen. Skriptet visas i fältet **skript** .
   - **Rensa** – tar bort det aktuella skriptet från **skript** fältet.
   - **Skript** – visar det aktuella importerade skriptet. Du kan redigera skriptet i det här fältet vid behov.
5. Slutför guiden. Det nya skriptet visas i **skript** listan med statusen **väntar på godkännande**. Innan du kan köra det här skriptet på klient enheter måste du godkänna det.


#### <a name="approve-or-deny-a-script"></a>Godkänn eller neka ett skript



Innan du kan köra ett skript måste det godkännas. Så här godkänner du ett skript:

1. I Configuration Manage-konsolen klickar du på **Programbibliotek**.
2. I arbets ytan **program bibliotek** klickar du på **skript**.
3. Välj det skript som du vill godkänna eller neka i listan **skript** och klicka sedan på **Godkänn/neka**i gruppen **skript** på fliken **Start** .
4. I dialog rutan **Godkänn eller neka skript** , **Godkänn**eller **neka** skriptet och om du vill kan du ange en kommentar om ditt beslut. Om du nekar ett skript kan det inte köras på klient enheter.
5. Slutför guiden. I listan **skript** ser du kolumnen **godkännande tillstånd** ändrad beroende på vilken åtgärd du vidtog.

#### <a name="run-a-script"></a>Kör ett skript

När ett skript har godkänts kan det köras mot en samling som du väljer.

1. Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.
2. I arbetsytan **Tillgångar och efterlevnad** klickar du på **Enhetssamlingar**.
3. I listan **enhets samlingar** klickar du på den samling enheter som du vill köra skriptet på.
3. På fliken **Start** går du till gruppen **alla system** och klickar på **Kör skript**.
4. På sidan **skript** i guiden **Kör skript** väljer du ett skript i listan. Endast godkända skript visas. Klicka på **Nästa**och slutför sedan guiden.

#### <a name="monitor-a-script"></a>Övervaka ett skript

När du har kört ett skript på klient enheter kan du använda den här proceduren för att övervaka att åtgärden lyckades.

1. Klicka på **övervakning**i Configuration Manager-konsolen.
2. I arbets ytan **övervakning** klickar du på **skript resultat**.
3. I listan **skript resultat** kan du Visa resultaten för varje skript som du körde på klient enheter. En avslutnings kod på skriptet **0**, indikerar vanligt vis att skriptet har körts.

## <a name="pxe-network-boot-support-for-ipv6"></a>PXE-nätverkets start stöd för IPv6
<!-- 1269793 -->
Nu kan du aktivera PXE-nätverkets start stöd för IPv6 för att starta en aktivitetssekvensdistribution för operativ system. När du använder den här inställningen kommer PXE-aktiverade distributions platser stödja både IPv4 och IPv6. Det här alternativet kräver inte WDS och kommer att stoppa WDS om det finns.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>Så här aktiverar du stöd för PXE-start för IPv6
Använd följande procedur för att aktivera alternativet för IPv6-stöd för PXE.

1. I Configuration Manager-konsolen går du till **Administration**  >  **Översikt**  >  **distributions platser**och klickar på **Egenskaper** för PXE-aktiverade distributions platser.
2. På fliken **PXE** väljer du **stöd för IPv6** för att aktivera stöd för IPv6 för PXE.

## <a name="manage-microsoft-surface-driver-updates"></a>Hantera uppdateringar av Microsoft Surface-drivrutiner
<!-- 1098490 -->
Du kan nu använda Configuration Manager för att hantera uppdateringar av Microsoft Surface-drivrutiner.

### <a name="prerequisites"></a>Förutsättningar
Alla program uppdaterings platser måste köra Windows Server 2016.

### <a name="try-it-out"></a>prova!
Försök att utföra följande uppgifter och skicka sedan oss **feedback** från fliken **Start** i menyfliksområdet så att vi kan se hur det fungerade:
1. Aktivera synkronisering för Microsoft Surface-drivrutiner. Använd proceduren i [Konfigurera klassificering och produkter](../../sum/get-started/configure-classifications-and-products.md) och välj **Inkludera uppdateringar för Microsoft-Surface-drivrutiner och inbyggd program vara** på fliken **klassificeringar** för att aktivera Surface-drivrutiner.
2. [Synkronisera Microsoft Surface-drivrutiner](../../sum/get-started/synchronize-software-updates.md).
3. [Distribuera synkroniserade Microsoft Surface-drivrutiner](../../sum/deploy-use/deploy-software-updates.md)

## <a name="configure-windows-update-for-business-deferral-policies"></a>Konfigurera Windows Update för principer för avstängning av företag
<!-- 1290890 -->
Nu kan du konfigurera regler för avstängning för Windows 10-funktions uppdateringar eller kvalitets uppdateringar för Windows 10-enheter som hanteras direkt av Windows Update för företag. Du kan hantera uppskjutnings principerna i noden nya **Windows Update för affärs principer** under **program varu bibliotek**  >  **Windows 10-Underhåll**.

### <a name="prerequisites"></a>Förutsättningar
Windows 10-enheter som hanteras av Windows Update för företag måste ha Internet anslutning.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Så här skapar du en princip för avstängning av Windows Update för företag
1. I **program varu biblioteket**  >  **Windows 10 Servicing**  >  **Windows Update for Business policies**
2. På fliken **Start** går du till gruppen **skapa** och väljer **skapa Windows Update för företag** för att öppna guiden skapa Windows Update för företag-princip.
3. På sidan **Allmänt** anger du ett namn och en beskrivning för principen.
4. På sidan **regler för avstängning** anger du om du vill skjuta upp eller pausa funktions uppdateringar.    
    Funktionsuppdateringarna är för det mesta nya funktioner i Windows. När du har konfigurerat inställningen **gren beredskaps nivå** kan du definiera om, och hur länge, du vill skjuta upp att ta emot funktions uppdateringar efter deras tillgänglighet från Microsoft.
    - **Gren beredskaps nivå**: Ange den gren för vilken enheten ska ta emot Windows-uppdateringar (Current Branch eller Current Branch for Business).
    - Uppskjutnings **period (dagar)**: Ange antalet dagar som funktions uppdateringar ska skjutas upp. Du kan fördröja mottagandet av dessa funktionsuppdateringar under en period på upp till 180 dagar från det att de har släppts.
    - **Pausa funktioner uppdateringar startar**: Välj om du vill pausa enheter från att ta emot funktions uppdateringar under en period på upp till 60 dagar från den tidpunkt då du pausar uppdateringarna. Efter det att det maximala antalet pausdagar har passerat upphör funktionen automatiskt och enheten söker efter tillämpliga uppdateringar på Windows Update. Efter den här sökningen kan du pausa uppdateringarna igen. Du kan avbryta pausen av funktions uppdateringar genom att avmarkera kryss rutan.   
5. Välj om du vill skjuta upp eller pausa kvalitets uppdateringar.     
    Kvalitetsuppdateringar utgörs vanligtvis av korrigeringar och förbättringar av befintliga Windows-funktioner, och publiceras vanligtvis den första tisdagen varje månad, men Microsoft kan publicera dem när som helst. Du kan ange om, och hur länge, du vill skjuta upp mottagandet av kvalitetsuppdateringar från det att de har gjorts tillgängliga.
    - Uppskjutnings **period (dagar)**: Ange antalet dagar som funktions uppdateringar ska skjutas upp. Du kan fördröja mottagandet av dessa funktionsuppdateringar under en period på upp till 180 dagar från det att de har släppts.
    - **Pausa kvalitets uppdateringar**från: Välj om du vill pausa enheter från att ta emot kvalitets uppdateringar under en period på upp till 35 dagar från den tidpunkt då du pausar uppdateringarna. Efter det att det maximala antalet pausdagar har passerat upphör funktionen automatiskt och enheten söker efter tillämpliga uppdateringar på Windows Update. Efter den här sökningen kan du pausa uppdateringarna igen. Du kan avbryta kvalitets uppdateringar genom att avmarkera kryss rutan.
6. Välj **Installera uppdateringar från andra Microsoft-produkter** för att aktivera grup princip inställningen som gör uppskjutnings inställningar tillämpliga på Microsoft Update, samt Windows-uppdateringar.
7. Välj **Inkludera driv rutiner med Windows Update** för att automatiskt uppdatera driv rutiner från Windows-uppdateringar. Om du avmarkerar den här inställningen laddas inte driv rutins uppdateringar ned från Windows-uppdateringar.
8. Slutför guiden för att skapa den nya avstängnings principen.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Så här distribuerar du en princip för avstängning av Windows Update för företag
1. I **program varu biblioteket**  >  **Windows 10 Servicing**  >  **Windows Update for Business policies**
2. På fliken **Start** går du till gruppen **distribution** och väljer **distribuera Windows Update for Business-princip**.
3. Konfigurera följande inställningar:
    - **Konfigurations princip som ska distribueras**: välj den Windows Update för företags princip som du vill distribuera.
    - **Samling**: Klicka på **Bläddra** och välj den samling där du vill distribuera principen.
    - **Reparera inkompatibla regler när stöd**finns: Välj att automatiskt reparera regler som inte är kompatibla för Windows Management INSTRUMENTATION (WMI), registret, skript och alla inställningar för mobila enheter som har registrerats av Configuration Manager.
    - **Tillåt reparation utanför underhålls fönstret**: om en underhålls period har kon figurer ATS för den samling som du distribuerar principen till aktiverar du det här alternativet för att låta kompatibilitetsinställningar reparera värdet utanför underhålls perioden. Mer information om underhålls perioder finns i [använda underhålls](../clients/manage/collections/use-maintenance-windows.md)perioder.
    - **Generera en avisering**: konfigurerar en avisering som genereras om konfigurations bas linjens kompatibilitet är mindre än en angiven procent andel vid en angiven tidpunkt. Du kan även ange om du vill att en avisering ska skickas till System Center Operations Manager.
    - **Slumpmässig fördröjning (timmar)**: anger en fördröjnings period för att undvika överdriven bearbetning av registrerings tjänsten för nätverks enheter. Standardvärdet är 64 timmar.
    - **Schema**: Ange det schema för utvärdering av kompatibilitet som den distribuerade profilen utvärderas på klient datorer. Schemat kan vara ett enkelt eller ett anpassat schema. Profilen utvärderas av klientdatorer när användaren loggar in.
4.  Distribuera profilen genom att slutföra guiden.



## <a name="support-for-entrust-certification-authorities"></a>Stöd för Entrust certifikat utfärdare
<!-- 1350740 -->
Configuration Manager stöder nu Entrust-certifikat utfärdare; Detta möjliggör leverans av PFX-certifikat till enheter som har registrerats i Microsoft Intune.

Du kan konfigurera Entrust som certifikat utfärdare när du lägger till en certifikat registrerings plats roll i Configuration Manager. När du lägger till en ny certifikat profil som utfärdar PFX-certifikat kan du välja antingen en Microsoft-eller Entrust-certifikatutfärdare.

**Känt problem**: i 1706 Technical Preview utfärdas inte PFX-certifikat för Microsoft-certifierings myndigheter. Importerade PFX-certifikat eller SCEP-profiler påverkas inte.


## <a name="cisco-ipsec-support-for-ios-vpn-profiles"></a>Stöd för Cisco (IPsec) för iOS VPN-profiler
<!-- 1321367 -->

Du kan skapa en VPN-profil för iOS med Cisco (IPsec) som Anslutnings typ. Mer information finns i [skapa VPN-profiler](../../protect/deploy-use/create-vpn-profiles.md#create-a-vpn-profile).


## <a name="new-windows-configuration-item-settings"></a>Nya inställningar för konfigurations objekt för Windows
<!-- 1354715 -->

I den här versionen har vi lagt till följande nya inställningar som du kan använda i konfigurations objekt i Windows:

### <a name="password"></a>lösenordsinställning

- **Enhets kryptering**

### <a name="device"></a>Enhet

- **Ändring av regions inställningar (endast skriv bord)**
- **Ändra energi-och vilo läges inställningar**
- **Ändra språk inställningar**
- **Ändring av system tid**
- **Ändring av enhets namn**

### <a name="store"></a>Lagringsplats

- **Uppdatera appar automatiskt från Store**
- **Använd endast privat lagring**
- **Start av app från Store-app**

### <a name="microsoft-edge"></a>Microsoft Edge

- **Blockera åtkomst till about: Flags**
- **Åsidosätt SmartScreen-prompt**
- **Åsidosättning av SmartScreen-meddelanden för filer**
- **WebRTC localhost-IP-adress**
- **Standard sökmotor**
- **OpenSearch-XML-URL**
- **Start sidor (endast skriv bord)**

Mer information om kompatibilitetsinställningar finns i [Se till att enheten uppfyller kraven](../../compliance/understand/ensure-device-compliance.md).


## <a name="new-device-compliance-policy-rules"></a>Nya regler för efterlevnadsprinciper för enheter

* **Krav på lösen ords typ**. Ange om användaren måste skapa ett alfanumeriskt lösen ord eller ett numeriskt lösen ord. För alfanumeriska lösen ord anger du också det minsta antal teckenuppsättningar som lösen ordet måste innehålla. De fyra teckenuppsättningarna är: gemener, versaler, symboler och siffror.

  **Stöds på:**
  * Windows Phone 8+
  * Windows 8.1 +
  * iOS 6+
<br></br>
* **Blockera USB-felsökning på enheten**. Du behöver inte konfigurera de här inställningarna eftersom USB-felsökning redan har inaktiverats på Android for Work-enheter.

  **Stöds på:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Blockera appar från okända källor**. Kräv att enheter förhindrar installation av appar från okända källor. Du behöver inte konfigurera den här inställningen eftersom Android for Work-enheter alltid begränsar installationen från okända källor.

  **Stöds på:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Kräv hot genomsökning på appar**. Den här inställningen anger att funktionen Verifiera appar är aktive rad på enheten.

  **Stöds på:**
  * Android 4,2 till 4,4
  * Samsung KNOX Standard 4.0+


## <a name="new-mobile-application-management-policy-settings"></a>Nya princip inställningar för hantering av mobil program
Från och med den här versionen kan du använda tre nya princip inställningar för hantering av mobil program (MAM):

- **Blockera skärmdump (endast Android-enheter):** Anger att skärm bilds funktionerna på enheten är blockerade när du använder den här appen.

- **Inaktivera synkronisering av kontakter:** Hindrar appen från att spara data till den interna appen Kontakter på enheten.

- **Inaktivera utskrift:** Hindrar appen från att skriva ut arbets-eller skol data.

## <a name="android-and-ios-enrollment-restrictions"></a>Registrerings begränsningar för Android och iOS
<!-- 1290826 -->
Från och med den här versionen kan administratörer nu ange att användare inte kan registrera personliga Android-eller iOS-enheter i sin hybrid miljö. På så sätt kan du begränsa registrerade enheter till fördeklarerade, företagsägda enheter eller iOS-enheter som har registrerats med Programmet för enhetsregistrering bara.

### <a name="try-it-out"></a>Prova
1. Gå till **Molntjänster** Microsoft Intune-prenumeration **i arbetsytan** > **Administration**i Configuration Manager-konsolen.
2. Välj **Konfigurera plattformar** på fliken **Start** i gruppen **prenumeration** och välj sedan **Android** eller **iOS**.
3. Välj **blockera personligt ägda enheter**.

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Program hanterings princip för Android for Work för Copy-klistra in
Vi har uppdaterat inställnings beskrivningarna för konfigurations objekt för Android for Work för den **Tillåt data delning mellan arbets profilen och den personliga profilen**.

|Före 1706 teknisk för hands version | Nytt alternativ namn | Beteende|
|-|-|-|
|Förhindra all delning över gränser| Standard begränsningar för delning| Arbete till personligt: standard (förväntas vara blockerad på alla versioner) <br>Personligt arbete: standard (tillåts på 6. x +, blockeras på 5. x)|
|Inga begränsningar| Appar i den personliga profilen kan hantera delnings förfrågningar från arbets profilen| Arbets-till-personlig: tillåten  <br>Personligt arbete: tillåtet|
|Appar i arbets profilen kan hantera delnings förfrågningar från den personliga profilen |Appar i arbets profilen kan hantera delnings förfrågningar från den personliga profilen |Arbete till personligt: standard<br>Personligt arbete: tillåtet<br>(Är bara användbart på 5. x där personligt arbete blockeras)|

Inget av de här alternativen förhindrar kopiera-inklistring-beteende. Vi har lagt till en anpassad inställning för tjänsten och Företagsportal app i 1704 som kan konfigureras för att förhindra kopiera-klistra in. Detta kan ställas in via anpassad URI.

- OMA-URI:./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Värdetyp: Boolean

Genom att ange DisallowCrossProfileCopyPaste till True förhindras kopierings inklistring mellan Android for Work-profiler och arbets profiler.

### <a name="try-it-out"></a>Prova
1. I Configuration Manager-konsolen väljer du **till gångar och efterlevnad**  >  **–**  >  **Compliance settings**  >  **konfigurations objekt**för kompatibilitetsinställningar.
2. Välj **skapa** för att skapa ett nytt konfigurations objekt och ange **namn** och **Android for Work**.
3. I enhets inställnings grupperna som ska konfigureras väljer du **arbets profil**och **sedan nästa**.
4. Välj värdet för **Tillåt data delning mellan arbets profiler och personliga profiler**och slutför sedan guiden.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Hälsoattestering för enhet bedömning av efterlevnadsprinciper för villkorlig åtkomst
<!-- 1097546 -->
Från och med den här versionen kan du använda Hälsoattestering för enhet status som en regel för efterlevnadsprinciper för villkorlig åtkomst till företags resurser.

### <a name="try-it-out"></a>Prova
Välj en Hälsoattestering för enhet regel som en del av en utvärdering av efterlevnadsprinciper.