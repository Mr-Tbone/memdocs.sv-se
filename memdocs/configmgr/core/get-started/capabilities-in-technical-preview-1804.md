---
title: Teknisk för hands version 1804
titleSuffix: Configuration Manager
description: Lär dig mer om nya funktioner som är tillgängliga i Configuration Manager Technical Preview version 1804.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b30386745244900e7f525f8f45b25a598628bf43
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078744"
---
# <a name="capabilities-in-technical-preview-1804-for-configuration-manager"></a>Funktioner i Technical Preview 1804 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1804. Du kan installera den här versionen om du vill uppdatera och lägga till nya funktioner på din tekniska för hands versions webbplats. 

Läs artikeln om [teknisk för hands version](technical-preview.md) innan du installerar den här uppdateringen. Den artikeln är bekant med de allmänna kraven och begränsningarna för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Kända problem i den här tekniska för hands versionen

### <a name="setup-link-to-download-updates-not-working"></a><a name="bkmk_ki-prereqs"></a>Installations länk för att ladda ned uppdateringar fungerar inte
<!--514334-->
Om du kör installations programmet från mediet innehåller den första sidan en länk med rubriken **Hämta de senaste Configuration Manager uppdateringarna**, som inte fungerar i den här versionen. Den här länken används för att ladda ned de filer som krävs för installationen.

#### <a name="workaround"></a>Lösning
Kör installations guiden för att ladda ned de filer som krävs för installationen. På sidan nödvändiga hämtningar använder du alternativet för att **Ladda ned nödvändiga filer**. 


### <a name="the-application-catalog-web-service-point-cant-be-https-enabled"></a><a name="bkmk_appcathttps"></a>Webb tjänst platsen för program katalogen kan inte vara HTTPS-aktiverad
<!--512637-->
Om program katalogens webb tjänst punkt är HTTPS-aktiverad:

- Program som distribueras som tillgängliga för användare visas inte i Software Center  

- Följande fel visas i awebsctl. log:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Lösning
Konfigurera om program katalogens webb tjänst plats för att kommunicera med HTTP-anslutningar.  




</br>

**Följande är nya funktioner som du kan prova med den här versionen.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Konfigurera ett fjärrinnehålls bibliotek för plats servern  
<!--1357525-->
Frigör hård disk utrymme på den primära plats servern genom att flytta dess [innehålls bibliotek](../plan-design/hierarchy/the-content-library.md) till en annan lagrings plats. Du kan flytta innehålls biblioteket till en annan enhet på plats servern, en separat server eller feltoleranta diskar i en storage area network (SAN). Vi rekommenderar en SAN eftersom det ger elastisk lagring som växer eller minskar med tiden för att möta dina föränderliga innehålls krav. 

Det här fjärrinnehålls biblioteket är en ny förutsättning för att [plats Server rollen ska ha hög tillgänglighet](capabilities-in-technical-preview-1706.md#site-server-role-high-availability). 

> [!Note]  
> Den här åtgärden flyttar bara innehålls biblioteket på plats servern. Innehålls bibliotekets placering påverkas inte av distributions platserna. 

### <a name="prerequisites"></a>Krav  
- Plats serverns dator konto behöver **Läs** -och **Skriv** behörighet till nätverks Sök vägen som du flyttar innehålls biblioteket till. Inga komponenter är installerade på fjärrdatorn. 

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Skicka sedan [feedback](#bkmk_feedback) för att berätta hur det fungerade.

1. Växla till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration** och välj **platser**. Lägg märke till en ny kolumn för **innehålls biblioteket**på fliken **Sammanfattning** längst ned i informations fönstret.  

2. Klicka på **Hantera innehålls bibliotek** i menyfliksområdet.  

3. Välj **en nätverks resurs** och ange en giltig nätverks Sök väg. Den här sökvägen är den plats där platsen flyttar innehålls biblioteket. Klicka på **OK**.  

4. Observera egenskapen **status** i kolumnen innehålls bibliotek i informations fönstret. Den uppdaterar för att visa platsens förlopp när innehålls biblioteket flyttas. När pågår visas procent andelen slutförd. Om det finns ett fel tillstånd visas fel meddelandet. Vanliga fel är `access denied` eller `disk full`. När du är klar `OK`visas den. Mer information finns i **Distmgr. log** . Mer information finns i [loggarna plats Server och plats system Server](../plan-design/hierarchy/log-files.md#BKMK_SiteSiteServerLog).  

Om du behöver flytta innehålls biblioteket tillbaka till plats servern upprepar du den här processen men väljer alternativet **lokalt på plats servern**.  

> [!Tip]  
> Om du vill flytta innehållet till en annan enhet på plats servern använder du verktyget för **överföring av innehålls bibliotek** . Mer information finns i [Configuration Manager Toolkit](#configuration-manager-toolkit).  



## <a name="submit-feedback-from-the-configuration-manager-console"></a><a name="bkmk_feedback"></a>Skicka feedback från Configuration Manager-konsolen  
<!--1357542-->

Skicka ett leende! Nu kan du direkt tala om för Configuration Manager teamet om dina upplevelser. Det är enkelt att skicka feedback från Configuration Manager-konsolen. Vi vill gärna höra all feedback: Praise, problem och förslag.  

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Skicka sedan **feedback** för att berätta hur det fungerade.  

1. I Configuration Manager-konsolen klickar du på knappen leende i det övre högra hörnet ovanför menyfliksområdet.  

2. Välj något av de tillgängliga alternativen i list rutan:  

   - **Skicka ett leende**: du gillade något! För det här alternativet anger du information om din feedback. Du kan också ta med en skärm bild och din e-postadress.  

   - **Skicka en bister min**: du har råkat ut för ett problem i konsolen, eller så fungerade inte något som förväntat. För det här alternativet anger du information om det potentiella produkt problemet. Du kan också ta med en skärm bild, din e-postadress och diagnostikdata.  

   - **Skicka ett förslag**: du har en idé att ändra och förbättra Configuration Manager. Det här alternativet öppnar vår [UserVoice](https://configurationmanager.uservoice.com) -webbplats i webbläsaren.  

Den här feedbacken går direkt till Microsofts produkt team för Configuration Manager. När du använder Windows 10 feedback Hub, rekommenderar vi att du använder återkopplings funktionen i konsolen.  

Följande anonyma information ingår alltid i feedback för kontexten:  

- Configuration Manager konsol version och språk  

- Configuration Manager plats version  

- Support-ID, även kallat hierarki-ID  

- OS-version och språk version för systemet som-konsolen körs på  

- Den exakta platsen i konsolen där du klickade på leende  

Dessa data är konsekventa med insamlingen av våra diagnostik-och användnings data. Mer information finns i [diagnostik-och användnings data](../plan-design/diagnostics/diagnostics-and-usage-data.md).

### <a name="known-issues"></a>Kända problem

Om du försöker skicka feedback från en enhet som inte har åtkomst till Internet kan programmet avslutas. Om du vill skicka ett leende eller bister min kontrollerar du att enheten har åtkomst till petrol.office.microsoft.com.



## <a name="support-center"></a>Support Center
<!--1357489-->

Använd Support Center för klient fel sökning, real tids logg visning eller för att hämta statusen för en Configuration Manager klient dator för senare analys. Support Center är ett enda verktyg för att konsolidera många administratörs fel söknings verktyg. En för hands version av den senaste versionen av Support Center med fel korrigeringar, förbättringar och en förhands granskning av vårt nya logg visnings program finns i den tekniska för hands versionen. Hitta installations programmet för Support Center på plats servern i mappen **CD. latest\SMSSETUP\Tools\SupportCenter** .

 > [!Tip]  
 > Äldre dokumentation för de befintliga funktionerna i Support Center finns på [TechNet](https://technet.microsoft.com/library/dn688621.aspx). Relevant information finns i processen för att migrera till docs.microsoft.com-biblioteket.  

### <a name="new-support-center-features"></a>Nya Support Center-funktioner  

- Ett nytt logg visnings program, OneTrace. Det fungerar ungefär som CMTrace och innehåller förbättringar som till exempel en flikad vy och docknings bara Windows.  

- En ny data insamlings funktion samlar in diagnostikloggar från den lokala eller en fjärran sluten Configuration Manager klient. Det tillhandahåller real tids diagnostik för inventering (ersätter klientens spion), princip (ersätter princip-spion) och klientcachen.  



## <a name="configuration-manager-toolkit"></a>Configuration Manager Toolkit
<!--1357145-->

Configuration Manager Server-och klient verktyg ingår nu i den tekniska för hands versionen. Hitta dem i mappen **CD. latest\SMSSETUP\Tools** på plats servern. Ingen ytterligare installation krävs.

#### <a name="server-tools"></a>Server verktyg  

- **DP Job Manager**: fel sökning av innehålls distributions jobb till distributions platser  

- **Visnings program för samlings utvärdering**: Visa utvärderings information för samlingen  

- **Innehålls biblioteks Utforskaren**: Visa innehåll i det enskilda instans arkivet för innehålls bibliotek  

- **Innehålls biblioteks överföring**: överför innehålls bibliotek mellan enheter  

- **Verktyget för innehålls ägarskap**: ändrar ägarskap för överblivna paket. Dessa paket finns på platsen utan en ägande plats Server.  

- **Rollbaserad administration och gransknings verktyg**: hjälper administratörer att granska konfigurationen av roller  

#### <a name="client-tools"></a>Klient verktyg

- **CMTrace**: Visa loggar  

- **Verktyg för distributions övervakning**: felsöka program, uppdateringar och bas linje distributioner  

- **Princip spion**: Visa princip tilldelningar  

- **Power Viewer-verktyg**: Visa status för energispar funktioner  

- **Verktyget Skicka schema**: utlöser scheman och utvärderingar av DCM-bas linjer  

> [!Important]  
> [Support Center](#support-center) rekommenderas för de flesta användnings fall, eftersom det innehåller samma eller förbättrade funktioner för följande verktyg:  
> - Klientspion
> - CMTrace<sup>1</sup> 
> - Distributionsövervakningsverktyget
> - Principspion
> - Skicka schema-verktyget
> 
> <sup>1</sup> CMTrace är inte beroende av .net eller Windows Presentation Foundation (WPF), så används fortfarande i Windows PE-startavbildningar.

### <a name="known-issues"></a>Kända problem
Vissa klient-och Server verktyg kan avslutas oväntat vid start. Det här problemet beror på en fil som saknas på mediet. Som en lösning kopierar du filen **Microsoft. Diagnostics. tracing. EventSource. dll** från katalogen AdminConsole\bin till både SMSSETUP\Tools\ClientTools och ServerTools kataloger. Den här filen måste vara samma version som används av Configuration Manager-konsolen. Andra versioner kanske inte fungerar. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Avinstallera program för åter kallelse av godkännande
<!--1357891-->

Beteendet har ändrats när du återkallar godkännande för ett program. Nu när du nekar begäran för programmet, avinstallerar klienten programmet från användarens enhet. 

### <a name="prerequisites"></a>Krav
- Aktivera funktionen **Godkänn program begär Anden för användare per enhet**.

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Skicka sedan [feedback](#bkmk_feedback) för att berätta hur det fungerade.

1. I Configuration Manager-konsolen distribuerar du till en användare ett program som kräver godkännande. På fliken **distributions inställningar** i distributionen aktiverar du alternativet **en administratör måste godkänna en begäran för programmet på enheten**.  

2. På Configuration Manager-klienten i Software Center begär användaren godkännande för att installera programmet.  

3. I Configuration Manager-konsolen godkänner du begäran för den här användaren att installera programmet på enheten. Begär Anden om program godkännande visas i arbets ytan **program varu bibliotek** under **program hantering**i noden **godkännande begär Anden** .  

4. Användaren installerar programmet på klienten i Software Center.  

5. I Configuration Manager-konsolen nekar du användarens begäran om programmet på enheten.  

### <a name="known-issues"></a>Kända problem
- När användaren har installerat programmet på klienten uppdaterar du användar principen. Växla till fliken **alternativ** i Software Center, expandera **dator underhåll** och klicka på **Synkronisera princip**.<!--480609-->  

- Webb tjänst platsen för program katalogen måste vara HTTP. Mer information finns [i kända problem i den här tekniska för hands versionen](#bkmk_appcathttps).<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Uteslut Active Directory behållare från identifiering
<!--1358143-->
Om du vill minska antalet identifierade objekt kan du nu utesluta vissa behållare från Active Directory system identifiering. Den här funktionen är resultatet av din [UserVoice-feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery).

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Skicka sedan [feedback](#bkmk_feedback) för att berätta hur det fungerade.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **konfiguration av hierarki** och välj **identifierings metoder**. Välj **Active Directory system identifiering** och klicka på **Egenskaper** i menyfliksområdet.  

2. Klicka på ikonen Ny om du vill ange en ny Active Directory behållare.   

3. I dialog rutan Active Directory behållare bläddrar du till eller anger **sökvägen** i avsnittet plats för att starta identifieringen.  

4. I avsnittet sökalternativ aktiverar du alternativet att **rekursivt söka Active Directory underordnade behållare**. Klicka sedan på **Lägg till** och välj under behållare som ska undantas från den här identifieringen.  

5. I dialog rutan Välj ny behållare väljer du en underordnad behållare att undanta. Stäng dialog rutan Välj ny behållare genom att klicka på **OK** .  

6. Stäng dialog rutan Active Directory container genom att klicka på **OK** .  

7. I Active Directory system identifiering Fönstret Egenskaper, se sökvägen till den Active Directory behållare där identifieringen startar. Den **rekursiva** kolumnen visar **Ja**, och kolumnen ny **har exkluderingar** visar också **Ja**. Stäng Active Directory system identifiering Fönstret Egenskaper genom att klicka på **OK** .  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Ange synligheten för länken Programkatalog webbplats i Software Center
<!--1358214-->

Nu kan du kontrol lera om länken för att **öppna programkatalog webbplats** visas i noden **installations status** i Software Center.  

> [!Note]  
> Stöd för användar upplevelsen för Programkatalog webbplats slutar med den första uppdateringen som lanseras efter den 1 juni 2018. Mer information finns i [borttagna och föråldrade funktioner](../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).  

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Skicka sedan [feedback](#bkmk_feedback) för att berätta hur det fungerade.

1. I Configuration Manager-konsolen, arbets ytan **Administration** , noden **klient inställningar** , skapar du en anpassad princip för klient enhets inställningar.  

2. Välj **Software Center** -gruppen.  

3. Klicka på **Anpassa**för **Software Center-inställningar**.  

4. Aktivera alternativet för att **dölja länken programkatalog webbplats i Software Center**.   

Mer information om klient inställningar finns i [Konfigurera klient inställningar](../clients/deploy/configure-client-settings.md).




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrera regler för automatisk distribution efter program uppdaterings arkitektur
 <!--1322266-->
Nu kan du filtrera regler för automatisk distribution för att utesluta arkitekturer som Itanium och ARM64.

### <a name="try-it-out"></a>prova!
Försök att slutföra uppgifterna. Skicka sedan [feedback](#bkmk_feedback) för att berätta hur det fungerade.

1. I Configuration Manager-konsolen växlar du till arbets ytan **program varu bibliotek** . Expandera **program uppdateringar** och välj **regler för automatisk distribution**. I menyfliksområdet väljer du **Skapa regel för automatisk distribution**.  

2. Fyll i lämpliga inställningar för fliken **Allmänt** och fliken **distributions inställningar** .  

3. På fliken **program uppdateringar** väljer du **arkitektur** och klickar sedan på **objekt som du vill söka efter** i **Sök kriterierna**.  

4. Välj de arkitekturer som du vill ska ingå i regeln för automatisk distribution.  

5. Klicka på **Nästa** och fortsätt med att skapa en regel för automatisk distribution.  

> [!IMPORTANT]  
> Kom ihåg att det finns 32-bitars (x86) program och komponenter som körs på 64-bitars (x64) system. Om du inte är säker på att du inte behöver x86 kan du aktivera det även när du väljer x64.  

### <a name="known-issues"></a>Kända problem
När du har lagt till arkitektur villkoren visar sidan Egenskaper för automatisk distributions regel **rubrik** i Sök kriterierna. Den automatiska distributions regeln fungerar fortfarande som förväntat och väljer rätt program uppdateringar. Du kan dock inte inkludera både **arkitektur** -och **rubrik** kriterier för tillfället. <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>Förbättringar av OS-distribution
Vi har gjort följande förbättringar av operativ Systems distributionen, varav vissa var resultatet av din röst feedback från användaren.  

- [Maskera känsliga data som lagras i variabler i aktivitetssekvensen](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): i [variabel steget Ange aktivitetssekvens](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) väljer du det nya alternativet för att **inte Visa det här värdet**. Till exempel när du anger ett lösen ord.<!--1358330--> Följande beteenden gäller när du aktiverar det här alternativet:
  - Värdet för variabeln visas inte i Smsts. log.
  - Configuration Manager-konsolen och SMS-providern hanterar det här värdet på samma sätt som för andra hemligheter, till exempel lösen ord.
  - Värdet ingår inte när du exporterar aktivitetssekvensen.
  - Redigeraren för aktivitetssekvens läser inte det här värdet när du redigerar steget. Skriv om hela värdet för att göra ändringar.

  > [!Important]  
  > Variabler och deras värden sparas med aktivitetssekvensen som XML och fördunklade i databasen. När klienten begär en aktivitetssekvens från hanterings platsen krypteras den under överföring och lagras på klienten. Alla variabel värden är dock oformaterad text i aktivitetssekvensen i minnet under körning på klienten. Om aktivitetssekvensen innehåller ett steg för att mata ut värdet för variabeln, är den här utmatningen oformaterad text. Det här beteendet kräver en uttrycklig åtgärd av administratören att inkludera ett sådant steg i aktivitetssekvensen. 


- [Maskera program namn under körnings kommando steget i en aktivitetssekvens](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): om du vill förhindra att potentiellt känsliga data visas eller loggas anger du variabeln **OSDDoNotLogCommand** till `TRUE`. Den här variabeln maskerar program namnet i Smsts. log under [körningen av kommando rads steget Kör kommando rad](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) . <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Förbättringar av Configuration Manager-konsolen
- Den primära användar informationen visas nu när du visar medlemmarna i en samling under **till gångar och efterlevnad**, **enhets samlingar**.<!--510252-->  



## <a name="next-steps"></a>Nästa steg
Information om hur du installerar eller uppdaterar den tekniska för hands versionen finns i [teknisk för hands version för Configuration Manager](technical-preview.md).    
