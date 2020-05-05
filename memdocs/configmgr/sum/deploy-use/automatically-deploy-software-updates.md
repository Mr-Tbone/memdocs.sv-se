---
title: Distribuera programuppdateringar automatiskt
titleSuffix: Configuration Manager
description: Distribuera program uppdateringar automatiskt med hjälp av regler för automatisk distribution (ADR).
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: eca3227a023561a099804ef0928bfee7a7aff2c6
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110448"
---
#  <a name="automatically-deploy-software-updates"></a>Distribuera programuppdateringar automatiskt  

*Gäller för: Configuration Manager (aktuell gren)*

Använd en automatisk distributions regel (ADR) i stället för att lägga till nya uppdateringar i en befintlig program uppdaterings grupp. Normalt använder du automatisk distribution för att distribuera månads Visa program uppdateringar (även kallade "korrigerings tisdag") och för att hantera Endpoint Protection definitions uppdateringar. Om du behöver hjälp med att avgöra vilken distributions metod som passar dig, se [distribuera program uppdateringar](deploy-software-updates.md).


##  <a name="create-an-automatic-deployment-rule-adr"></a><a name="BKMK_CreateAutomaticDeploymentRule"></a> Skapa en automatisk distributionsregel  
Godkänn och distribuera program uppdateringar automatiskt med hjälp av en ADR. Regeln kan lägga till program uppdateringar till en ny program uppdaterings grupp varje gången regeln körs eller lägga till program uppdateringar till en befintlig grupp. När en regel körs och lägger till program uppdateringar till en befintlig grupp, tar regeln bort alla uppdateringar från gruppen. Den lägger sedan till i gruppen de uppdateringar som uppfyller de kriterier som du definierar. 

> [!WARNING]  
>  Innan du skapar en ADR för första gången kontrollerar du att platsen har slutfört synkroniseringen av program uppdateringar. Det här steget är viktigt när du kör Configuration Manager med ett annat språk än engelska. Program uppdaterings klassificeringar visas på engelska före den första synkroniseringen och visas sedan i de lokaliserade språken när synkroniseringen av program uppdateringen har slutförts. Regler som du skapar innan du synkroniserar program uppdateringar kanske inte fungerar korrekt efter synkroniseringen eftersom text strängen kanske inte matchar.  


### <a name="process-to-create-an-adr"></a><a name="bkmk_adr-process"></a>Process för att skapa en ADR  

1.  I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **program uppdateringar**och väljer noden **regler för automatisk distribution** .  

2.  I menyfliksområdet klickar du på **Skapa regel för automatisk distribution**.  

3.  Konfigurera följande inställningar på sidan **Allmänt** i guiden Skapa regel för automatisk distribution:  

    -   **Namn**: Ange ett namn för den automatiska distributionsregeln. Namnet måste vara unikt, hjälpa till att beskriva syftet med regeln och identifiera den från andra på den Configuration Manager webbplatsen.  

    -   **Beskrivning**: Ange en beskrivning av den automatiska distributionsregeln. Beskrivningen bör ge en översikt av distributions regeln och annan relevant information som hjälper till att särskilja regeln från andra. Beskrivningsfältet är valfritt, har en begränsning på 256 tecken och har ett tomt värde som standard.  

    -   **Mall**: Välj en Distributionsmall för att ange om du vill tillämpa tidigare sparade ADR-konfigurationer. Konfigurera en distributionsmall som innehåller flera vanliga distributions egenskaper för uppdateringar som du kan använda när du skapar ytterligare automatisk distribution. De här mallarna sparar tid och hjälper till att säkerställa konsekvensen mellan liknande distributioner. Välj någon av följande inbyggda mallar för distribution av program uppdatering:  

         - I mallen **Korrigeringstisdag** finns vanliga inställningar du kan använda när du distribuerar programuppdateringar månadsvis.  

         - **Office 365-klientens uppdaterings** mall innehåller vanliga inställningar som används när du distribuerar uppdateringar för Office 365 Pro plus-klienter.
             > [!Note]
             > Från och med den 21 april 2020 kommer Office 365 ProPlus att byta namn till **Microsoft 365 appar för företag**. Om din automatisk distribution förlitar sig på egenskapen "title" måste du redigera den från den 9 juni 2020. `Microsoft 365 Apps Update - Semi-annual Channel Version 1908 for x64 based Edition (Build 11929.50000)`är ett exempel på den nya titeln. Mer information finns i [namn ändring för Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change).

         - **Uppdaterings mal len SCEP och Windows Defender Antivirus** innehåller vanliga inställningar som används när du distribuerar Endpoint Protection definitions uppdateringar.  

    -   **Samling**: Anger vilken målsamling som ska användas för distributionen. Medlemmar i kollektionen får programuppdateringar som är definierade i distributionen.  

    -   Bestäm om du ska lägga till programuppdateringar till en ny eller befintlig programuppdateringsgrupp. I de flesta fall väljer du att skapa en ny program uppdaterings grupp när ADR körs. Om regeln körs enligt ett mer aggressivt schema kan du välja att använda en befintlig grupp. Om du till exempel kör regeln dagligen för definitions uppdateringar kan du lägga till program uppdateringarna till en befintlig program uppdaterings grupp.  

    -   **Aktivera distributionen när regeln har körts**: Ange om programuppdateringsdistributionen ska distribueras när regeln för automatisk distribution har körts. Överväg följande alternativ för den här inställningen:  

        -   När du aktiverar distributionen läggs de uppdateringar som uppfyller regelns definierade kriterier till i en program uppdaterings grupp. Innehållet i program uppdateringen laddas ned vid behov. Innehållet kopieras till de angivna distributions platserna och uppdateringarna distribueras till klienterna i mål samlingen.  

        -   När du inte aktiverar distributionen läggs de uppdateringar som uppfyller regelns definierade villkor till i en program uppdaterings grupp. Innehållet för program uppdaterings distributionen laddas ned vid behov och distribueras till de angivna distributions platserna. Platsen skapar en inaktive rad distribution i program uppdaterings gruppen för att förhindra att uppdateringarna distribueras till klienter. Det här alternativet ger dig tid att förbereda för att distribuera uppdateringarna, verifiera de uppdateringar som uppfyller kriterierna är tillräckliga och aktivera sedan distributionen.  

4.  Konfigurera följande inställningar på sidan **distributions inställningar** :  

    -   **Använd Wake on LAN för att väcka klienter för nödvändiga distributioner**: anger om Wake on LAN ska aktive ras vid tids gränsen. Wake On LAN skickar aktiverings paket till datorer som kräver en eller flera program uppdateringar i distributionen. Platsen aktiverar alla datorer som är i vilo läge vid installationens tids gräns så att installationen kan initieras. Klienter som är i vilo läge och som inte behöver några program uppdateringar i distributionen startas inte. Som standard är den här inställningen inte aktive rad. Konfigurera datorer och nätverk för Wake On LAN innan du använder det här alternativet. Mer information finns i [så här konfigurerar du Wake on LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

    -   **Detalj nivå**: Ange detalj nivån för meddelanden om uppdatering av tvångs tillstånd som rapporteras av klienter.  

        > [!IMPORTANT]  
        >  När du distribuerar definitions uppdateringar anger du detalj nivån till **endast fel** om du endast vill att klienten ska rapportera ett tillstånds meddelande när en definitions uppdatering Miss lyckas. Annars rapporterar klienten ett stort antal tillstånds meddelanden som kan påverka plats serverns prestanda.  
        
        > [!NOTE]  
        > Informations nivån **fel** skickar inte de tvingande status meddelanden som krävs för spårning av väntande omstarter.

    -   **Inställning för licensvillkor**: Ange om programuppdateringar ska distribueras automatiskt med associerade licensvillkor. Vissa program uppdateringar inkluderar licens villkor. När du distribuerar program uppdateringar automatiskt visas inte licens villkoren och det finns inget alternativ för att acceptera licens villkoren. Välj att automatiskt distribuera alla program uppdateringar oberoende av associerade licens villkor eller distribuera bara uppdateringar som inte har några associerade licens villkor.  

         - Om du vill granska licens villkoren för en program uppdatering väljer du program uppdateringen i noden **alla program uppdateringar** i arbets ytan **program varu bibliotek** . Klicka på **Granska licens**i menyfliksområdet.    

         - Om du vill hitta program uppdateringar med associerade licens villkor lägger du till kolumnen **licens villkor** i resultat fönstret i noden **alla program uppdateringar** . Klicka på rubriken för kolumnen för att sortera efter program uppdateringar med licens villkor.  

5.  På sidan **program uppdateringar** konfigurerar du kriterier för program uppdateringar som ADR hämtar och lägger till i program uppdaterings gruppen.  

     - Gränsen för programuppdateringar i den automatiska distributionsregeln är 1000 programuppdateringar.  

     - Vid behov filtrerar du på innehålls storleken för program uppdateringar i regler för automatisk distribution. Mer information finns i [Configuration Manager och förenklad Windows-underhåll på äldre operativ system](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).  

     - Från och med version 1910 kan du använda **distribuerat** som ett uppdaterings filter för de automatiska distributions reglerna. Med det här filtret kan du identifiera nya uppdateringar som kan behöva distribueras till pilot-eller test samlingar. Filtret för program uppdatering kan också undvika att distribuera om äldre uppdateringar. 
         - När du använder **distribuerad** som ett filter måste du vara mindful att du redan har distribuerat uppdateringen till en annan samling, till exempel en pilot-eller test samling. <!--4852033-->
     - Från och med version 1806 är ett egenskaps filter för **arkitektur** nu tillgängligt. Använd det här filtret för att utesluta arkitekturer som Itanium och ARM64 som är mindre vanliga. Kom ihåg att det finns 32-bitars (x86) program och komponenter som körs på 64-bitars (x64) system. Om du inte är säker på att du inte behöver x86 kan du aktivera det även när du väljer x64.<!--1322266-->  

    > [!NOTE]  
    > **Windows 10, version 1903 och senare** har lagts till i Microsoft Update som sin egen produkt, i stället för att vara en del av **Windows 10** -produkten som tidigare versioner. Den här ändringen gjorde att du utför ett antal manuella åtgärder för att se till att dina klienter ser dessa uppdateringar. Vi har hjälpt till att minska antalet manuella åtgärder som du behöver vidta för den nya produkten i Configuration Manager version 1906. Mer information finns i [Konfigurera produkter för versioner av Windows 10](../get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later) <!--4682946-->


6. På sidan **utvärderings schema** anger du om du vill aktivera ADR för att köras enligt ett schema. När detta är aktivt klickar du på **Anpassa** för att ange det återkommande schemat.  

    - Start tids konfigurationen för schemat baseras på den lokala tiden på den dator som kör Configuration Manager-konsolen.  

    - Den automatiska utvärderingen av distributionsregeln kan köras så ofta som tre gånger per dag.  

    - Ange aldrig utvärderings schema med en frekvens som överskrider schemat för synkronisering av program uppdateringar. Den här sidan visar synkroniseringsschemat för program uppdaterings platsen som hjälper dig att avgöra frekvensen för utvärderings schema.  

    - Om du vill köra ADR manuellt väljer du regeln i noden **regel för automatisk distribution** i-konsolen och klickar sedan på **Kör nu** i menyfliksområdet.  

    - Från och med version 1802 kan automatisk distribution schemaläggas för att utvärdera förskjutningen från en bas dag. Till exempel, om korrigerings tisdag faktiskt är onsdag för dig, anger du utvärderings schema för den andra tisdagen i månaden med en dag.<!--1357133-->  
        - När du planerar utvärderingen med en förskjutning under den sista veckan i månaden, och om du väljer en förskjutning som fortsätter till nästa månad, schemaläggs platsen för den sista dagen i månaden.<!--506731-->  
        ![ADR anpassad utvärderings schema förskjutning från bas dag](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Konfigurera följande inställningar på sidan **distributions schema** :  

    -   **Schema utvärdering**: Ange den tid som Configuration Manager utvärderar den tillgängliga tid-och installations tids gränsen. Välj att använda UTC (Coordinated Universal Time) eller lokal tid för den dator som kör Configuration Manager-konsolen.  

          - När du väljer **lokal tid för klient** här och sedan väljer **så snart som möjligt** för **tillgänglig tid för program vara**, används den aktuella tiden på datorn som kör Configuration Manager-konsolen för att utvärdera när uppdateringar är tillgängliga. Detta är samma sak som **installations tids gränsen** och den tid då uppdateringar installeras på en klient. Om klienten finns i en annan tidszon inträffar de här åtgärderna när klientens tid når utvärderings tiden.  

    -   **Tillgänglig tid för programvara**: Välj en av följande inställningar för att ange när programuppdateringarna är tillgängliga för klienter:  

        -   **Så snart som möjligt**: gör program uppdateringarna i distributionen tillgängliga för klienter så snart som möjligt. När du skapar distributionen med den här inställningen aktive ras Configuration Manager uppdaterar klient principen. Vid nästa avsöknings cykel för klient principen blir klienter medvetna om distributionen och program uppdateringarna är tillgängliga för installation.  

        -   **Angiven tid**: gör program uppdateringar som ingår i distributionen tillgängliga för klienter vid ett visst datum och en angiven tidpunkt. När du skapar distributionen med den här inställningen aktive rad uppdaterar Configuration Manager klient principen. Vid nästa avsöknings cykel för klient principen blir klienter medvetna om distributionen. Program uppdateringarna i distributionen är dock inte tillgängliga för installation förrän efter det konfigurerade datumet och den angivna tiden.  

    -   **Tidsgräns för installation**: Välj någon av följande inställningar för att ange installationstidsgränsen för programuppdateringar i distributionen:  

        -   **Så snart som möjligt**: Välj den här inställningen om du vill installera programuppdateringarna automatiskt i distributionen så snart som möjligt.  

        -   **Angiven tid**: Välj den här inställningen om du vill installera programuppdateringar automatiskt i distributionen vid ett specifikt datum och en specifik tidpunkt. Configuration Manager **bestämmer tids gränsen** för att installera program uppdateringar genom att lägga till det konfigurerade tidsintervallet till **tillgänglig tid för program vara**.  

             - Den faktiska tids gräns tiden för installationen är den tids gräns tid som visas plus en slumpmässig tids period på upp till två timmar. Slumpmässigheten minskar den potentiella påverkan av klienter i samlingen som installerar uppdateringar i distributionen på samma tidpunkt.  

             - Om du vill inaktivera slumpmässig fördröjning för installationen av obligatoriska program uppdateringar konfigurerar du klient inställningen för att **Inaktivera slumpmässig tids gräns** i **dator agent** gruppen. Mer information finns i [klient inställningar för dator agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

    -  **Fördröj verk ställning av distributionen enligt användar inställningar, upp till den Respitperiod som definierats i klient inställningarna**: Aktivera den här inställningen för att ge användare mer tid att installera nödvändiga program uppdateringar utanför tids gränsen.  

        - Det här beteendet krävs vanligt vis när en dator stängs av under lång tid och måste installera många program uppdateringar eller program. Till exempel, när en användare returnerar från semestern, måste de vänta en stund när klienten installerar förfallna distributioner.  

        - Konfigurera den här Grace-perioden med egenskapen **respitperiod för tillämpning efter distributionens tids gräns (timmar)** i klient inställningar. Mer information finns i avsnittet [dator agent](../../core/clients/deploy/about-client-settings.md#computer-agent) . Den tvingande Grace-perioden gäller alla distributioner med det här alternativet aktiverat och riktas mot enheter som du också distribuerar klient inställningen till.  

        - Efter tids gränsen installerar klienten program uppdateringarna i det första fönstret, som användaren har konfigurerat, upp till den här Grace-perioden. Användaren kan dock fortfarande öppna Software Center och installera program uppdateringarna när som helst. När Grace-perioden går ut återgår tvång till det normala beteendet för förfallna distributioner.  

8. Konfigurera följande inställningar på sidan **användar upplevelse** :  

    -   **Användar meddelanden**: Ange om du vill visa ett meddelande i Software Center vid den konfigurerade **tillgänglig tid för program vara**. Den här inställningen styr även om användarna ska meddelas om klienterna.  

    -   **Beteende för tids gräns**: Ange beteenden när program uppdaterings distributionen når deadline utanför eventuella definierade underhålls fönster. Alternativen inkluderar om program uppdateringarna ska installeras och om en omstart ska utföras efter installationen. Mer information om underhålls perioder finns i [använda underhålls](../../core/clients/manage/collections/use-maintenance-windows.md)perioder.  
        
        > [!Note]
        > Detta gäller endast när underhålls perioden har kon figurer ATS för klient enheten. Om inget underhålls fönster har definierats på enheten sker uppdatering av installationen och omstarten sker alltid efter tids gränsen.

    -   **Beteende för omstart av enhet**: Ange om du vill ignorera en omstart av systemet på servrar och arbets stationer om det krävs en omstart för att slutföra installationen av uppdateringen.  

        > [!WARNING]  
        >  Att förhindra omstarter av systemet kan vara användbart i Server miljöer eller när du inte vill att mål datorerna ska starta om som standard. Det kan dock medföra att datorer är i ett osäkert tillstånd. Att tillåta en framtvingad omstart hjälper till att säkerställa att installationen av program uppdateringen slutförs omedelbart.  

    -   **Skriv filter hantering för Windows Embedded-enheter**: den här inställningen styr installations beteendet på Windows Embedded-enheter som är aktiverade med ett Skriv filter. Välj alternativet för att genomföra ändringar vid installationens tids gräns eller under en underhålls period. När du väljer det här alternativet krävs en omstart och ändringarna sparas på enheten. Annars installeras uppdateringen, tillämpas på det tillfälliga överlägget och genomförs senare.  

           -  När du distribuerar en program uppdatering till en Windows Embedded-enhet ser du till att enheten är medlem i en samling som har en konfigurerad underhålls period.  

    - **Distributions omvärdering för distribution av program uppdateringar vid omstart**: Välj den här inställningen om du vill konfigurera distributioner av program uppdateringar så att klienterna kör en sökning efter program uppdateringar omedelbart efter att en klient har installerat program uppdateringar och startar om. Den här inställningen gör att klienten kan söka efter ytterligare uppdateringar som blir tillämpliga när klienten startas om, och sedan installera dem i samma underhålls period.  

9. På sidan **aviseringar** konfigurerar du hur Configuration Manager genererar aviseringar för den här distributionen. Granska de senaste program uppdaterings aviseringarna från Configuration Manager i noden **program uppdateringar** i arbets ytan **program varu bibliotek** . Om du också använder System Center Operations Manager konfigurerar du även aviseringarna.  

10. Konfigurera följande inställningar på sidan **hämtnings inställningar** :  

    - Ange om klienter ska hämta och installera uppdateringarna när de använder en distributions plats från en granne eller standard platsens gränser grupper.  

    - Ange om klienter ska hämta och installera uppdateringarna från en distributions plats i platsens standard gränser grupp, när innehållet för program uppdateringarna inte är tillgängligt från en distributions plats i den aktuella eller intilliggande gränser grupperna.  

    - **Tillåt att klienter delar innehåll med andra klienter i samma undernät**: Ange om användning av BranchCache ska aktiveras för nedladdning av innehåll. Mer information finns i [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). Från och med version 1802 är BranchCache alltid aktiverat på klienter. Den här inställningen tas bort eftersom klienterna använder BranchCache om distributions platsen stöder det.  

    - **Om program uppdateringar inte är tillgängliga på distributions platsen i aktuella, intilliggande eller plats gränser grupper laddar du ned innehåll från Microsoft Updates**: Välj den här inställningen om du vill att intranät anslutna klienter ska kunna hämta program uppdateringar från Microsoft Update om uppdateringar inte är tillgängliga på distributions platser. Internetbaserade klienter går alltid till Microsoft Update för program uppdaterings innehåll.  

    - Ange om du vill tillåta att klienter kan ladda ned efter en installations tids gräns när de använder avgiftsbelagda Internet anslutningar. Internet leverantörer debiteras ibland av den mängd data som du skickar och tar emot när du använder en anslutning med datapriser.  

    > [!NOTE]  
    >  Klienter begär installationsplatsen från en hanteringsplats för programuppdateringarna i en distribution. Hämtnings beteendet beror på hur du har konfigurerat distributions platsen, distributions paketet och inställningarna på den här sidan.   

11. Välj något av följande alternativ på sidan **distributions paket** :  

    - **Välj ett distributions paket**: Lägg till dessa uppdateringar i ett befintligt distributions paket.  

    - **Skapa ett nytt distributions paket**: Lägg till dessa uppdateringar i ett nytt distributions paket. Konfigurera följande ytterligare inställningar:  

        -  **Namn**: Ange namnet på distributionspaketet. Använd ett unikt namn som beskriver paket innehållet. Den är begränsad till 50 tecken.  

        -  **Beskrivning**: Ange en beskrivning som ger information om distributionspaketet. Den valfria beskrivningen är begränsad till 127 tecken.  

        -  **Paketkälla**: Anger platsen för källfilerna för programuppdateringen. Ange en nätverks Sök väg för käll platsen, till exempel `\\server\sharename\path`eller klicka på **Bläddra** för att hitta nätverks platsen. Skapa en delad mapp för distributions paketets källfiler innan du fortsätter till nästa sida.  

            - Du kan inte använda den angivna platsen som källa till ett annat program distributions paket.  

            - Du kan ändra paketets käll plats i egenskaperna för distributions paketet när Configuration Manager skapar distributions paketet. Om du gör det kopierar du först innehållet från den ursprungliga paket källan till den nya paket käll platsen.  

            -  Dator kontot för SMS-providern och användaren som kör guiden för att ladda ned program uppdateringarna måste båda ha **Skriv** behörighet till nedladdnings platsen. Begränsa åtkomsten till nedladdnings platsen. Den här begränsningen minskar risken för angripare som manipulerar källfilerna för program uppdatering.  

        -  **Sändningsprioritet**: Ange sändningsprioriteten för distributionspaketet. Configuration Manager använder den här prioriteten när paketet skickas till distributions platser. Distributions paketen skickas i prioritetsordning: hög, medel eller låg. Paket med identisk prioritering skickas i den ordning de skapades. Om det inte finns någon efter släpning bearbetas paketet omedelbart oavsett prioritet.  

        - **Aktivera binär differentiell replikering**: Aktivera den här inställningen för att minimera nätverks trafiken mellan platser. Binär differentiell replikering (BDR) uppdaterar endast det innehåll som har ändrats i paketet, i stället för att uppdatera hela paket innehållet. Mer information finns i [binär differentiell replikering](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

    - **Inget distributions paket**: från och med version 1806, distribuera program uppdateringar till enheter utan att först hämta och distribuera innehåll till distributions platser. Den här inställningen är fördelaktig vid hantering av mycket stor uppdaterings innehåll. Använd den även när du alltid vill att klienter ska hämta innehåll från Microsoft Update moln tjänsten. Klienter i det här scenariot kan också hämta innehåll från peer-datorer som redan har det innehåll som krävs. Den Configuration Manager klienten fortsätter att hantera innehålls hämtningen och kan därför använda funktionen Configuration Manager peer-cache eller andra tekniker som leverans optimering. Den här funktionen stöder alla uppdaterings typer som stöds av Configuration Manager hantering av program uppdateringar, inklusive Windows-och Office-uppdateringar.<!--1357933-->  

        > [!Note]  
        > När du har valt det här alternativet och tillämpar inställningarna kan du inte längre ändra det. De andra alternativen är nedtonade.<!--SCCMDocs-pr issue 3003-->  

12. På sidan **distributions platser** anger du de distributions platser eller distributions plats grupper som ska vara värdar för program uppdaterings filerna. Mer information om distributionsplatser finns i [Konfigurationer av distributionsplatser](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Den här sidan är bara tillgänglig när du skapar ett nytt distributionspaket för programuppdatering.  
  

13. På sidan **hämtnings plats** anger du om du vill ladda ned program uppdaterings filerna från Internet eller från ditt lokala nätverk. Konfigurera följande inställningar:  

    -   **Hämta program uppdateringar från Internet**: Välj den här inställningen för att ladda ned program uppdateringar från en angiven plats på Internet. Den här inställningen är aktiverad som standard.  

    -   **Hämta programuppdateringar från en plats i det lokala nätverket**: Välj den här inställningen för att ladda ned programuppdateringarna från en lokal katalog eller delad mapp. Den här inställningen är användbar när den dator som kör guiden inte har Internet åtkomst. Alla datorer med Internet åtkomst kan preliminärt ladda ned program uppdateringarna. Lagra dem sedan på en plats i det lokala nätverket som är tillgängligt från den dator där guiden körs.  

14. På sidan **Val av språk** väljer du de språk för vilka platsen hämtar de valda program uppdateringarna. Platsen hämtar bara de här uppdateringarna om de är tillgängliga på de valda språken. Program uppdateringar som inte är språkspecifika laddas alltid ned. Som standard väljer guiden de språk som du har konfigurerat i egenskaperna för program uppdaterings platsen. Minst ett språk måste väljas innan du fortsätter till nästa sida. Om du bara väljer språk som en program uppdatering inte stöder, Miss lyckas nedladdningen för uppdateringen.  

15. Granska inställningarna på sidan **Sammanfattning** . Om du vill spara inställningarna till en distributionsmall klickar du på **Spara som mall**. Ange ett namn och välj de inställningar som du vill inkludera i mallen och klicka sedan på **Spara**. Om du vill ändra en konfigurerad inställning klickar du på den associerade guidesidan och ändrar inställningen.  

    -  Mallnamnet kan bestå av alfanumeriska ASCII-tecken och `\` (omvänt snedstreck) eller `'` (enkelt citat tecken).  

16. Skapa den automatiska distributionsregeln genom att klicka på **Nästa** .  

När du har slutfört guiden körs ADR. Den lägger till de program uppdateringar som uppfyller de angivna villkoren för en program uppdaterings grupp. Därefter laddar ADR uppdateringarna till innehålls biblioteket på plats servern och distribuerar dem till de konfigurerade distributions platserna. Därefter distribuerar ADR program uppdaterings gruppen till klienter i mål samlingen.  



##  <a name="add-a-new-deployment-to-an-existing-adr"></a><a name="BKMK_AddDeploymentToADR"></a>Lägg till en ny distribution i en befintlig ADR  

När du har skapat en ADR lägger du till ytterligare distributioner till regeln. Den här åtgärden hjälper dig att hantera komplexiteten vid distribution av olika uppdateringar till olika samlingar. Varje ny distribution har en fullständig uppsättning funktioner och distributionsövervakning.  


### <a name="process-to-add-a-new-deployment-to-an-existing-adr"></a>Process för att lägga till en ny distribution i en befintlig ADR  

1.  I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **program uppdateringar**, väljer noden **regler för automatisk distribution** och väljer sedan önskad regel.  

2.  Klicka på **Lägg till distribution**i menyfliksområdet.   

3.  På sidan **samling** i guiden Lägg till distribution konfigurerar du de tillgängliga inställningarna på samma sätt som sidan **Allmänt** i guiden Skapa regel för automatisk distribution. Mer information finns i föregående avsnitt om [processen för att skapa en ADR](#bkmk_adr-process). Resten av guiden Lägg till distribution innehåller följande sidor, som också matchar detaljerade beskrivningar ovan:  

     - Distributions inställningar
     - Distributions schema
     - Användarupplevelse
     - Aviseringar
     - Hämtningsinställningar  

Distributioner kan också läggas till program mässigt med Windows PowerShell-cmdlets. En fullständig beskrivning av hur du använder den här metoden finns i [New-CMSoftwareUpdateDeployment](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsoftwareupdatedeployment) .

Mer information om distributionsprocessen finns i avsnittet [Distributionsprocess för programuppdatering](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).


## <a name="next-steps"></a>Nästa steg
[Övervaka programuppdateringar](monitor-software-updates.md)
