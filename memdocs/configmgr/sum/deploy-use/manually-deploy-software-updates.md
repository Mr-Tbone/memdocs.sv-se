---
title: Distribuera programuppdateringar manuellt
titleSuffix: Configuration Manager
description: Skapa program varu distributioner manuellt för att få dina klienter uppdaterade med nödvändiga program uppdateringar eller för att distribuera out-of-band-uppdateringar.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: b7d6640beb9353d5c613cf38e3f880e7fd76b393
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717092"
---
# <a name="manually-deploy-software-updates"></a>Distribuera programuppdateringar manuellt  

*Gäller för: Configuration Manager (aktuell gren)*

En manuell program uppdaterings distribution är en process där du väljer program uppdateringar från Configuration Manager-konsolen och startar distributions processen manuellt. Eller Lägg till valda program uppdateringar i en uppdaterings grupp och distribuera sedan uppdaterings gruppen manuellt. Du använder vanligt vis manuella distributioner för att få dina klienter uppdaterade med nödvändiga program uppdateringar. Du använder sedan automatiska distributions regler (ADR) för att hantera pågående månatliga program uppdaterings distributioner. Använd även den här manuella metoden för att distribuera out-of-band-programuppdateringar. Mer information om vilka distributions metoder som passar dig bäst finns i [distribuera program uppdateringar](deploy-software-updates.md).



##  <a name="step-1-specify-search-criteria-for-software-updates"></a><a name="BKMK_1SearchCriteria"></a>Steg 1: Ange Sök villkor för program uppdateringar  

Beroende på de kombinationer av produkter och klassificeringar som platsen synkroniserar finns det potentiellt tusentals program uppdateringar som visas i Configuration Manager-konsolen. Det första steget i arbetsflödet för manuell distribution av programuppdateringar är att identifiera de programuppdateringar som du vill distribuera. Du kan till exempel Visa alla program uppdateringar som krävs på över 50 klient enheter med en **säkerhet** eller **kritisk** klassificering.  

> [!IMPORTANT]  
>  En enda program uppdaterings distribution har en gräns på 1000 program uppdateringar.  

### <a name="process-to-specify-search-criteria-for-software-updates"></a>Process för att ange Sök villkor för program uppdateringar  

1.  I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **program uppdateringar**och klickar på **alla program uppdateringar**. Den här noden visar alla synkroniserade program uppdateringar.  

    > [!NOTE]  
    >  I noden **alla program uppdateringar** visas endast program uppdateringar med en **kritisk** och **säkerhets** klassificering som har släppts under de senaste 30 dagarna.  

2.  I Sök-fönstret filtrerar du för att identifiera de program uppdateringar som du behöver. Använd ett eller båda av följande alternativ:  

    -   Skriv en Sök sträng som filtrerar program uppdateringarna i rutan Sök text. Skriv till exempel artikeln eller Bulletin-ID: t för en speciell program uppdatering. Eller ange en sträng som visas i rubriken för flera program uppdateringar.  

    -   Klicka på **Lägg till kriterier**och välj kriterier för att filtrera program uppdateringar. Klicka på **Lägg till**och ange sedan värdena för villkoret.  

3.  Filtrera programuppdateringarna genom att klicka på **Sök** .  

    > [!TIP]  
    >  Spara filter villkor som används ofta. Klicka på alternativet för att **Spara aktuell sökning**i menyfliksområdet. Hämta tidigare sökningar genom att klicka på **sparade sökningar**.   



##  <a name="step-2-create-a-software-update-group-that-contains-the-software-updates"></a><a name="BKMK_2UpdateGroup"></a> Steg 2: Skapa en programuppdateringsgrupp som innehåller programuppdateringarna   

Med program uppdaterings grupper kan du organisera program uppdateringar i förberedelser inför distribution. Följ stegen nedan om du vill lägga till program uppdateringar i en ny program uppdaterings grupp manuellt.  

### <a name="process-to-manually-add-software-updates-to-a-new-software-update-group"></a>Process för att lägga till program uppdateringar i en ny program uppdaterings grupp manuellt  

1.  Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen och välj **program uppdateringar**. Välj önskade program uppdateringar.  

2.  Klicka på **skapa program uppdaterings grupp** i menyfliksområdet.  

3.  Ange ett namn på programuppdateringsgruppen och tillhandahåll eventuellt en beskrivning. Använd ett namn och en beskrivning som ger tillräckligt med information för att du ska kunna avgöra vilken typ av uppdateringar som finns i program uppdaterings gruppen. Klicka på **Skapa**.  

4.  Välj noden **program uppdaterings grupper** och välj den nya program uppdaterings gruppen. Om du vill visa listan över uppdateringar i gruppen klickar du på **Visa medlemmar** i menyfliksområdet.  



##  <a name="step-3-download-the-content-for-the-software-update-group"></a><a name="BKMK_3DownloadContent"></a> Steg 3: Ladda ned innehållet för programuppdateringsgruppen  

Innan du distribuerar program uppdateringarna ska du ladda ned innehållet för program uppdateringarna i program uppdaterings gruppen. I det här steget kan du kontrol lera att innehållet är tillgängligt på distributions platser innan du distribuerar program uppdateringarna. Det hjälper dig också att undvika oväntade problem med innehålls distribution. Om du hoppar över det här steget, som en del av distributions processen, laddar platsen ned innehållet och distribuerar dem till distributions platserna. Använd följande procedur för att ladda ned innehållet till programuppdateringarna i programuppdateringsgruppen.  


### <a name="process-to-download-content-for-the-software-update-group"></a>Process för att ladda ned innehåll för program uppdaterings gruppen
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

### <a name="process-to-monitor-content-status"></a>Process för att övervaka innehålls status
1. Om du vill övervaka innehålls status för program uppdateringarna går du till arbets ytan **övervakning** i Configuration Manager-konsolen. Expandera **distributions status**och välj sedan noden **innehålls status** .  

2. Välj det programuppdateringspaket som du tidigare har identifierat för att ladda ned programuppdateringar i programuppdateringsgruppen.  

3. Klicka på **Visa status** i menyfliksområdet.  



##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_4DeployUpdateGroup"></a>Steg 4: distribuera program uppdaterings gruppen  

När du har fastställt vilka uppdateringar du vill distribuera och lägger till dem i en program uppdaterings grupp distribuerar du program uppdaterings gruppen manuellt.  

### <a name="process-to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Process för att manuellt distribuera program uppdateringar i en program uppdaterings grupp  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **program uppdateringar**och väljer noden **program uppdaterings grupper** .  

2. Välj den program uppdaterings grupp som du vill distribuera. Klicka på **distribuera** i menyfliksområdet.   

3. Konfigurera följande inställningar på sidan **Allmänt** i guiden distribuera program uppdateringar:  

   -   **Namn**: Ange namnet på distributionen. Distributionen måste ha ett unikt namn som beskriver syftet och särskiljer den från andra distributioner på-platsen. Det här namn fältet innehåller en gräns på 256 tecken. Som standard tillhandahåller Configuration Manager automatiskt ett namn för distributionen i följande format:`Microsoft Software Updates - YYYY-MM-DD <time>`  

   -   **Beskrivning**: Ange en beskrivning av distributionen. Beskrivningen är valfri, men ger en översikt över distributionen. Ta med annan relevant information som hjälper dig att identifiera och särskilja den bland andra på-platsen. Beskrivnings fältet innehåller en gräns på 256 tecken och har ett tomt värde som standard.  

   -   **Program uppdatering/program uppdaterings grupp**: verifiera att den program uppdaterings grupp eller program uppdatering som visas är korrekt.  

   -   **Välj distributionsmall**: Ange om du ska tillämpa en tidigare sparad distributionsmall. Konfigurera en Distributionsmall för att spara vanliga egenskaper för program uppdaterings distribution. Tillämpa sedan mallen när du distribuerar program uppdateringar i framtiden. De här mallarna sparar tid och hjälper till att säkerställa konsekvensen mellan liknande distributioner.  

   -   **Samling**: Ange samlingen för distributionen. Enheter i samlingen får program uppdateringar i den här distributionen.  

4. Konfigurera följande inställningar på sidan **distributions inställningar** :  

   -   **Typ av distribution**: Ange distributionstypen för programuppdateringsdistributionen.  

       > [!IMPORTANT]  
       >  När du har skapat program uppdaterings distributionen kan du inte ändra distributions typen.  

        - Välj **krävs** för att skapa en obligatorisk program uppdaterings distribution. Program uppdateringarna installeras automatiskt på klienterna innan tids gränsen för installationen konfigureras.  

        - Välj **tillgänglig** för att skapa en valfri program uppdaterings distribution. Den här distributionen är tillgänglig för användare att installera från Software Center.  

       > [!NOTE]  
       >  När du distribuerar en program uppdaterings grupp efter **behov**laddar klienterna ned innehållet i bakgrunden och ser till att BITS-inställningarna är konfigurerade.  
       > 
       > För program uppdaterings grupper som distribueras som **tillgängliga**laddar klienterna ned innehållet i förgrunden och IGNORERAr BITS-inställningar.  

   -   **Använd Wake-on-LAN för att väcka klienter för nödvändiga distributioner**: anger om Wake on LAN ska aktive ras vid tids gränsen. Wake On LAN skickar aktiverings paket till datorer som kräver en eller flera program uppdateringar i distributionen. Platsen aktiverar alla datorer som är i vilo läge vid installationens tids gräns så att installationen kan initieras. Klienter som är i vilo läge och som inte behöver några program uppdateringar i distributionen startas inte. Som standard är den här inställningen inte aktive rad. Den är endast tillgänglig för **nödvändiga** distributioner. Konfigurera datorer och nätverk för Wake On LAN innan du använder det här alternativet. Mer information finns i [så här konfigurerar du Wake on LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

   -   **Detalj nivå**: Ange detalj nivån för de tillstånds meddelanden som klienter rapporterar till platsen.  

5. Konfigurera följande inställningar på sidan **Schemaläggning** :  

   -   **Schema utvärdering**: Ange den tid som Configuration Manager utvärderar den tillgängliga tid-och installations tids gränsen. Välj att använda UTC (Coordinated Universal Time) eller lokal tid för den dator som kör Configuration Manager-konsolen.  

       - När du väljer **lokal tid för klient** här och sedan väljer **så snart som möjligt** för **tillgänglig tid för program vara**, används den aktuella tiden på datorn som kör Configuration Manager-konsolen för att utvärdera när uppdateringar är tillgängliga. Detta är samma sak som **installations tids gränsen** och den tid då uppdateringar installeras på en klient. Om klienten finns i en annan tidszon inträffar de här åtgärderna när klientens tid når utvärderings tiden.  

   -   **Tillgänglig tid för programvara**: Välj en av följande inställningar för att ange när programuppdateringarna är tillgängliga för klienter:  

       -   **Så snart som möjligt**: gör program uppdateringarna i distributionen tillgängliga för klienter så snart som möjligt. När du skapar distributionen med den här inställningen aktive ras Configuration Manager uppdaterar klient principen. Vid nästa avsöknings cykel för klient principen blir klienter medvetna om distributionen och program uppdateringarna är tillgängliga för installation.  

       -   **Angiven tid**: gör program uppdateringar som ingår i distributionen tillgängliga för klienter vid ett visst datum och en angiven tidpunkt. När du skapar distributionen med den här inställningen aktive rad uppdaterar Configuration Manager klient principen. Vid nästa avsöknings cykel för klient principen blir klienter medvetna om distributionen. Program uppdateringarna i distributionen är dock inte tillgängliga för installation förrän efter det konfigurerade datumet och den angivna tiden.  

   -   **Installations tids gräns**: de här alternativen är bara tillgängliga för **nödvändiga** distributioner. Välj en av följande inställningar för att ange installations tids gränsen för program uppdateringar i distributionen  

       -   **Så snart som möjligt**: Välj den här inställningen om du vill installera programuppdateringarna automatiskt i distributionen så snart som möjligt.  

       -   **Angiven tid**: Välj den här inställningen om du vill installera programuppdateringar automatiskt i distributionen vid ett specifikt datum och en specifik tidpunkt.  

           - Den faktiska tids gräns tiden för installationen är den tids gräns tid som visas plus en slumpmässig tids period på upp till två timmar. Slumpmässigheten minskar den potentiella påverkan av klienter i samlingen som installerar uppdateringar i distributionen på samma tidpunkt.   

           - Om du vill inaktivera slumpmässig fördröjning för installationen av obligatoriska program uppdateringar konfigurerar du klient inställningen för att **Inaktivera slumpmässig tids gräns** i **dator agent** gruppen. Mer information finns i [klient inställningar för dator agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

   -  **Fördröj verk ställning av distributionen enligt användar inställningar, upp till den Respitperiod som definierats i klient inställningarna**: Aktivera den här inställningen för att ge användare mer tid att installera nödvändiga program uppdateringar utanför tids gränsen.  

       - Det här beteendet krävs vanligt vis när en dator stängs av under lång tid och måste installera många program uppdateringar eller program. Till exempel, när en användare returnerar från semestern, måste de vänta en stund när klienten installerar förfallna distributioner.  

       - Konfigurera den här Grace-perioden med egenskapen **respitperiod för tillämpning efter distributionens tids gräns (timmar)** i klient inställningar. Mer information finns i avsnittet [dator agent](../../core/clients/deploy/about-client-settings.md#computer-agent) . Den tvingande Grace-perioden gäller alla distributioner med det här alternativet aktiverat och riktas mot enheter som du också distribuerar klient inställningen till.  

       - Efter tids gränsen installerar klienten program uppdateringarna i det första fönstret, som användaren har konfigurerat, upp till den här Grace-perioden. Användaren kan dock fortfarande öppna Software Center och installera program uppdateringarna när som helst. När Grace-perioden går ut återgår tvång till det normala beteendet för förfallna distributioner.  

6. Konfigurera följande inställningar på sidan **användar upplevelse** :  

   -   **Användar meddelanden**: Ange om du vill visa ett meddelande i Software Center vid den konfigurerade **tillgänglig tid för program vara**. Den här inställningen styr även om användarna ska meddelas på klient datorerna. För **tillgängliga** distributioner kan du inte välja alternativet att **dölja i Software Center och alla meddelanden**.  

   -   **Beteende för tids gräns**: den här inställningen kan bara konfigureras för **nödvändiga** distributioner. Ange beteenden när program uppdaterings distributionen når deadline utanför eventuella definierade underhålls fönster. Alternativen inkluderar om program uppdateringarna ska installeras och om en omstart ska utföras efter installationen. Mer information om underhålls perioder finns i [använda underhålls](../../core/clients/manage/collections/use-maintenance-windows.md)perioder. 
  
       > [!Note]
       > Detta gäller endast när underhålls perioden har kon figurer ATS för klient enheten. Om inget underhålls fönster har definierats på enheten sker uppdatering av installationen och omstarten sker alltid efter tids gränsen.

   -   **Beteende för omstart av enhet**: den här inställningen kan bara konfigureras för **nödvändiga** distributioner. Ange om du vill förhindra omstart av systemet på servrar och arbets stationer om det krävs en omstart för att slutföra installationen av uppdateringen.  

       > [!WARNING]  
       >  Att förhindra omstarter av systemet kan vara användbart i Server miljöer eller när du inte vill att mål datorerna ska starta om som standard. Det kan dock medföra att datorer är i ett osäkert tillstånd. Att tillåta en framtvingad omstart hjälper till att säkerställa att installationen av program uppdateringen slutförs omedelbart.  

   -   **Skriv filter hantering för Windows Embedded-enheter**: den här inställningen styr installations beteendet på Windows Embedded-enheter som är aktiverade med ett Skriv filter. Välj alternativet för att genomföra ändringar vid installationens tids gräns eller under en underhålls period. När du väljer det här alternativet krävs en omstart och ändringarna sparas på enheten. Annars installeras uppdateringen, tillämpas på det tillfälliga överlägget och genomförs senare.  

       -  När du distribuerar en program uppdatering till en Windows Embedded-enhet ser du till att enheten är medlem i en samling som har en konfigurerad underhålls period.  

   - **Distributions omvärdering för distribution av program uppdateringar vid omstart**: Välj den här inställningen om du vill konfigurera distributioner av program uppdateringar så att klienterna kör en sökning efter program uppdateringar omedelbart efter att en klient har installerat program uppdateringar och startar om. Den här inställningen gör att klienten kan söka efter ytterligare uppdateringar som blir tillämpliga när klienten startas om, och sedan installera dem i samma underhålls period.  

7. På sidan **aviseringar** konfigurerar du hur Configuration Manager genererar aviseringar för den här distributionen. Granska de senaste program uppdaterings aviseringarna från Configuration Manager i noden **program uppdateringar** i arbets ytan **program varu bibliotek** . Om du också använder System Center Operations Manager konfigurerar du även aviseringarna. Konfigurera endast aviseringar för **nödvändiga** distributioner.  

8. Konfigurera följande inställningar på sidan **hämtnings inställningar** :  

    > [!NOTE]  
    >  Klienter begär installationsplatsen från en hanteringsplats för programuppdateringarna i en distribution. Hämtnings beteendet beror på hur du har konfigurerat distributions platsen, distributions paketet och inställningarna på den här sidan.  

    - Ange om klienter ska hämta och installera uppdateringarna när de använder en distributions plats från en granne eller standard platsens gränser grupper.  

    - Ange om klienter ska hämta och installera uppdateringarna från en distributions plats i platsens standard gränser grupp, när innehållet för program uppdateringarna inte är tillgängligt från en distributions plats i den aktuella eller intilliggande gränser grupperna.  

    - **Tillåt att klienter delar innehåll med andra klienter i samma undernät**: Ange om användning av BranchCache ska aktiveras för nedladdning av innehåll. Mer information finns i [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). Från och med version 1802 är BranchCache alltid aktiverat på klienter. Den här inställningen tas bort eftersom klienterna använder BranchCache om distributions platsen stöder det.  

    - **Om program uppdateringar inte är tillgängliga på distributions platsen i aktuella, intilliggande eller plats gränser grupper laddar du ned innehåll från Microsoft Updates**: Välj den här inställningen om du vill att intranät anslutna klienter ska kunna hämta program uppdateringar från Microsoft Update om uppdateringar inte är tillgängliga på distributions platser. Internetbaserade klienter går alltid till Microsoft Update för program uppdaterings innehåll.

    - Ange om du vill tillåta att klienter kan ladda ned efter en installations tids gräns när de använder avgiftsbelagda Internet anslutningar. Internet leverantörer debiteras ibland av den mängd data som du skickar och tar emot när du använder en anslutning med datapriser.  

9. Välj något av följande alternativ på sidan **distributions paket** :  

    > [!Note]  
    > Om du redan utför [steg 3: Ladda ned innehållet för program uppdaterings gruppen](#BKMK_3DownloadContent)visas inte sidorna **distributions paket**, **distributions platser**och **Val av språk** i guiden. Gå till sidan [Sammanfattning](#bkmk_summary) i guiden.  
    > 
    >  Program uppdateringar som tidigare har laddats ned till innehålls biblioteket på plats servern laddas inte ned igen. Det här beteendet gäller även när du skapar ett nytt distributions paket för program uppdateringarna. Om alla program uppdateringar redan har hämtats hoppar guiden över sidan [Sammanfattning](#bkmk_summary) .  

    - **Välj ett distributions paket**: Lägg till dessa uppdateringar i ett befintligt distributions paket.  

    - **Skapa ett nytt distributions paket**: Lägg till dessa uppdateringar i ett nytt distributions paket. Konfigurera följande ytterligare inställningar:  

        -  **Namn**: Ange namnet på distributionspaketet. Använd ett unikt namn som beskriver paket innehållet. Den är begränsad till 50 tecken.  

        -  **Beskrivning**: Ange en beskrivning som ger information om distributionspaketet. Den valfria beskrivningen är begränsad till 127 tecken.  

        -  **Paketkälla**: Ange platsen för programuppdateringskällfilerna. Ange en nätverks Sök väg för käll platsen, till exempel `\\server\sharename\path`eller klicka på **Bläddra** för att hitta nätverks platsen. Skapa en delad mapp för distributions paketets källfiler innan du fortsätter till nästa sida.  

            - Du kan inte använda den angivna platsen som källa till ett annat program distributions paket.  

            - Du kan ändra paketets käll plats i egenskaperna för distributions paketet när Configuration Manager skapar distributions paketet. Om du gör det kopierar du först innehållet från den ursprungliga paket källan till den nya paket käll platsen.  

            -  Dator kontot för SMS-providern och användaren som kör guiden för att ladda ned program uppdateringarna måste båda ha **Skriv** behörighet till nedladdnings platsen. Begränsa åtkomsten till nedladdnings platsen. Den här begränsningen minskar risken för angripare som manipulerar källfilerna för program uppdatering.  

        -  **Sändningsprioritet**: Ange sändningsprioriteten för distributionspaketet. Configuration Manager använder den här prioriteten när paketet skickas till distributions platser. Distributions paketen skickas i prioritetsordning: hög, medel eller låg. Paket med identisk prioritering skickas i den ordning de skapades. Om det inte finns någon efter släpning bearbetas paketet omedelbart oavsett prioritet.  

        - **Aktivera binär differentiell replikering**: Aktivera den här inställningen för att minimera nätverks trafiken mellan platser. Binär differentiell replikering (BDR) uppdaterar endast det innehåll som har ändrats i paketet, i stället för att uppdatera hela paket innehållet. Mer information finns i [binär differentiell replikering](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Inget distributions paket**: från och med version 1806, distribuera program uppdateringar till enheter utan att först hämta och distribuera innehåll till distributions platser. Den här inställningen är fördelaktig vid hantering av mycket stor uppdaterings innehåll. Använd den även när du alltid vill att klienter ska hämta innehåll från Microsoft Update moln tjänsten. Klienter i det här scenariot kan också hämta innehåll från peer-datorer som redan har det innehåll som krävs. Den Configuration Manager klienten fortsätter att hantera innehålls hämtningen och kan därför använda funktionen Configuration Manager peer-cache eller andra tekniker som leverans optimering. Den här funktionen stöder alla uppdaterings typer som stöds av Configuration Manager hantering av program uppdateringar, inklusive Windows-och Office-uppdateringar.<!--1357933-->  

10. På sidan **distributions platser** anger du de distributions platser eller distributions plats grupper som ska vara värdar för program uppdaterings filerna. Mer information om distributionsplatser finns i [Konfigurationer av distributionsplatser](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!Note]  
    > Om du redan utför [steg 3: Ladda ned innehållet för program uppdaterings gruppen](#BKMK_3DownloadContent)visas inte sidorna **distributions paket**, **distributions platser**och **Val av språk** i guiden. Gå till sidan [Sammanfattning](#bkmk_summary) i guiden.  

11. På sidan **hämtnings plats** anger du om du vill ladda ned program uppdaterings filerna från Internet eller från ditt lokala nätverk. Konfigurera följande inställningar:  

    -   **Hämta program uppdateringar från Internet**: Välj den här inställningen för att ladda ned program uppdateringar från en angiven plats på Internet. Den här inställningen är aktiverad som standard.  

    -   **Hämta programuppdateringar från en plats i det lokala nätverket**: Välj den här inställningen för att ladda ned programuppdateringarna från en lokal katalog eller delad mapp. Den här inställningen är användbar när den dator som kör guiden inte har Internet åtkomst. Alla datorer med Internet åtkomst kan preliminärt ladda ned program uppdateringarna. Lagra dem sedan på en plats i det lokala nätverket som är tillgängligt från den dator där guiden körs.  

12. På sidan **Val av språk** väljer du de språk för vilka platsen hämtar de valda program uppdateringarna. Platsen hämtar bara de här uppdateringarna om de är tillgängliga på de valda språken. Program uppdateringar som inte är språkspecifika laddas alltid ned. Som standard väljer guiden de språk som du har konfigurerat i egenskaperna för program uppdaterings platsen. Minst ett språk måste väljas innan du fortsätter till nästa sida. Om du bara väljer språk som en program uppdatering inte stöder, Miss lyckas nedladdningen för uppdateringen.  

    > [!Note]  
    > Om du redan utför [steg 3: Ladda ned innehållet för program uppdaterings gruppen](#BKMK_3DownloadContent)visas inte sidorna **distributions paket**, **distributions platser**och **Val av språk** i guiden. Gå till sidan [Sammanfattning](#bkmk_summary) i guiden.  

13. <a name="bkmk_summary"></a>På sidan **Sammanfattning** granskar du inställningarna. Om du vill spara inställningarna till en distributionsmall klickar du på **Spara som mall**. Ange ett namn och välj de inställningar som du vill inkludera i mallen och klicka sedan på **Spara**. Om du vill ändra en konfigurerad inställning klickar du på den associerade guidesidan och ändrar inställningen.  

    -  Mallnamnet kan bestå av alfanumeriska ASCII-tecken och `\` (omvänt snedstreck) eller `'` (enkelt citat tecken).  

14. Klicka på **Nästa** för att distribuera programuppdateringen.  

    När du har slutfört guiden Configuration Manager Ladda ned program uppdateringarna till innehålls biblioteket på plats servern. Sedan distribueras innehållet till de konfigurerade distributions platserna och program uppdaterings gruppen distribueras till klienter i mål samlingen. Mer information om distributionsprocessen finns i avsnittet [Distributionsprocess för programuppdatering](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).  



## <a name="next-steps"></a>Nästa steg
[Övervaka programuppdateringar](monitor-software-updates.md)
