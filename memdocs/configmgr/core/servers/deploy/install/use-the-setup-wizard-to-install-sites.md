---
title: Installations guide
titleSuffix: Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8325102e9a818191eae5061b7adf60dbbb7269b5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700709"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>Använd installations guiden för att installera Configuration Manager-platser

*Gäller för: Configuration Manager (aktuell gren)*

Om du vill installera en ny Configuration Manager webbplats med hjälp av ett guidat användar gränssnitt använder du installations guiden för Configuration Manager (setup.exe). Guiden stöder installation av en primär plats eller en central administrations plats. Du kan också använda guiden för att [uppgradera en utvärderings installation](upgrade-an-evaluation-install-to-a-full-install.md) av Configuration Manager till en fullt licensierad installation. När du inte vill använda guiden kan du i stället använda ett [installations skript](use-a-command-line-to-install-sites.md) och köra en obevakad kommando rads installation.

Installera en sekundär plats inifrån Configuration Manager-konsolen. Sekundära platser har inte stöd för en kommando rads installation med skript.

> [!Note]  
> Från och med version 1906 finns inte längre filen **Start. HTA** i roten på installations mediet. Den tillhandahöll länkar till följande information:<!--SCCMDocs-pr#3545-->
>
> - **Installera webbplats**: `smssetup\bin\x64\setup.exe` . Mer information finns i [installera en central administration eller en primär plats](#bkmk_primary).
> - **Innan du börjar**: [utforma en hierarki med platser](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626543 -->
> - **Utvärdera Server beredskap**: [krav kontroll](prerequisite-checker.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626546 -->
> - **Hämta nödvändiga nödvändiga filer**: `smssetup\bin\x64\setupdl.exe` . Mer information finns i [installations hämtaren](setup-downloader.md).
> - **Installera Configuration Manager-konsolen**: `smssetup\bin\i386\consolesetup.exe` . Mer information finns i [Installera konsoler](install-consoles.md).
> - [**Ladda ned System Center Updates Publisher**](../../../../sum/tools/updates-publisher.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626548 -->
> - **Ladda ned klienter för ytterligare operativ system**: <!-- https://go.microsoft.com/fwlink/p/?LinkId=626550 -->
>   - [Microsoft Endpoint Configuration Manager-macOS-klient (64-bitars)](https://www.microsoft.com/download/details.aspx?id=100850)
>   - [Klienter för UNIX och Linux](https://www.microsoft.com/download/details.aspx?id=47719)
> - [**Viktig information**](release-notes.md) <!-- https://go.microsoft.com/fwlink/?LinkID=626571 -->
> - [**Läs dokumentation**](/sccm)<!-- https://go.microsoft.com/fwlink/p/?LinkId=626547 -->
> - **Få installations hjälp**: [TechNet-forum: Configuration Manager (Current Branch) – plats-och klient distribution](https://social.technet.microsoft.com/Forums/en-us/home?forum=ConfigMgrDeployment) <!--NOTE: this link requires en-us locale to work-->   <!-- https://go.microsoft.com/fwlink/p/?LinkId=626549 -->
> - **Configuration Manager community**: [System Center-community: hur man deltar](https://social.technet.microsoft.com/wiki/contents/articles/11504.system-center-community-how-to-participate.aspx) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626544 -->
> - [**Configuration Manager start**](https://www.microsoft.com/cloud-platform/system-center-configuration-manager) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626545 -->


## <a name="install-a-central-administration-or-primary-site"></a><a name="bkmk_primary"></a> Installera en central administrations plats eller en primär plats

Använd följande procedur för att installera en central administrations plats eller en primär plats. Du kan också använda den för att uppgradera en utvärderings plats till en fullständigt licensierad Configuration Manager webbplats.

Innan du startar plats installationen bör du vara bekant med informationen i följande artiklar:

- [Förbereda för att installera platser](prepare-to-install-sites.md)
- [Förutsättningar för att installera platser](prerequisites-for-installing-sites.md)

Om du installerar en central administrations plats som en del av scenariot för plats expansion bör du granska utökningen av [en fristående primär plats](use-the-setup-wizard-to-install-sites.md#bkmk_expand) innan du använder följande procedur.

### <a name="process-to-install-a-primary-or-central-administration-site"></a><a name="bkmk_installpri"></a> Process för att installera en primär eller Central administrations plats

1. På den dator där du vill installera platsen kör `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` du för att starta **installations guiden för Configuration Manager**.  

    > [!NOTE]  
    > När du installerar en central administrations plats för att expandera på en fristående primär plats, eller installerar en ny underordnad primär plats i en befintlig hierarki, använder du installationsmedia (källfiler) som matchar versionen av den befintliga platsen eller platserna. Om du har installerat uppdateringar i konsolen som har ändrat versionen av de tidigare installerade platserna ska du inte använda det ursprungliga installations mediet. Använd i stället källfiler från [CD-skivan. Den senaste mappen](../../manage/the-cd.latest-folder.md) på en uppdaterad webbplats. Configuration Manager kräver att du använder källfiler som matchar versionen av den befintliga platsen som den nya platsen kommer att ansluta till.  

2. Välj **Nästa**på sidan **innan du börjar** .  

3. På sidan **komma igång** väljer du den typ av plats som du vill installera:  

    - **Central administrations plats**, som den första platsen i en ny hierarki, eller när du utökar en fristående primär plats:  

        Välj **installera en Configuration Manager Central administrations plats**.  

        Under ett senare steg i den här proceduren kan du välja att installera en central administrations plats som den första platsen i en ny hierarki eller installera en central administrations plats för att expandera på en fristående primär plats.  

    - **Primär plats**, som en fristående primär plats som är den första platsen i en ny hierarki eller som en underordnad primär plats:  

        Välj **installera en Configuration Manager primär plats**.  

        > [!TIP]  
        > Normalt väljer du bara alternativet **Använd vanliga installations alternativ för en fristående primär plats** när du vill installera en fristående primär plats i en test miljö. När du väljer det här alternativet gör installations programmet följande åtgärder:  
        >
        > - Konfigurerar automatiskt platsen som en fristående primär plats.  
        > - Använder en standard installations Sök väg.  
        > - Använder en lokal installation av standard instansen av SQL Server för plats databasen.  
        > - Installerar en hanterings plats och en distributions plats på plats serverdatorn.  
        > - Konfigurerar platsen med engelska och visnings språket för operativ systemet på den primära plats servern om den matchar något av de språk som Configuration Manager stöder.  

4. På sidan **produkt nyckel** :  

    - Välj om du vill installera Configuration Manager som utvärderings version eller licensierad version.  

        - Om du väljer en licensierad utgåva anger du produkt nyckeln och väljer **Nästa**.  

        - Om du väljer en utvärderings version väljer du **Nästa**. (Du kan uppgradera en utvärderings installation till en fullständig installation senare.)  

    - Du kan också ange **utgångs datumet för Software Assurance** för ditt licens avtal. Det är en praktisk påminnelse om detta datum. Om du inte anger det här datumet under installationen kan du ange det senare i Configuration Manager-konsolen.  

        > [!NOTE]  
        > Microsoft validerar inte det förfallo datum som du har angett och använder inte det här datumet för licens validering. Du kan använda den som en påminnelse om ditt förfallo datum. Det här datumet är användbart eftersom Configuration Manager regelbundet söker efter nya program uppdateringar som erbjuds online. Licens statusen för Software Assurance bör vara aktuell så att du är berättigad till att använda de här ytterligare uppdateringarna.  

    Mer information finns i [licensiering och grenar](../../../understand/learn-more-editions.md).  

5. På sidan **licens villkor för program vara från Microsoft** läser du igenom och godkänner licens villkoren.  

6. På sidan **nödvändiga licenser** läser du igenom och godkänner licens villkoren för den nödvändiga program varan. Installations programmet laddar ned och installerar automatiskt program varan på plats system eller klienter när det behövs. Acceptera alla villkor innan du fortsätter till nästa sida.  

7. På sidan **nödvändiga hämtningar** anger du om installations programmet måste ladda ned de senaste nödvändiga distribuerbara filerna från Internet eller använda tidigare hämtade filer:  

    - Om du vill att installations programmet ska hämta filerna nu väljer du **Hämta filer som krävs**. Ange sedan en plats där filerna ska lagras.  

    - Om du tidigare har laddat ned filerna med hjälp av [installations hämtaren](setup-downloader.md)väljer du **Använd tidigare hämtade filer**. Ange sedan Download-mappen.  

        > [!TIP]  
        > Om du använder tidigare hämtade filer bör du kontrol lera att sökvägen till mappen Download innehåller den senaste versionen av filerna.  

8. På sidan **Val av Server språk** väljer du de språk som är tillgängliga för Configuration Manager-konsolen och för-rapporter. (Engelska är markerat som standard och kan inte tas bort.) Mer information finns i [språk paket](language-packs.md).  

9. På sidan **Val av klient språk** väljer du de språk som är tillgängliga för klient datorer. Ange även om du vill aktivera alla klient språk för mobila enhets klienter. (Engelska är markerat som standard och kan inte tas bort.)  

    > [!IMPORTANT]  
    > När du använder en central administrations plats måste du kontrol lera att de klient språk som du konfigurerar på den centrala administrations platsen innehåller alla klient språk som du konfigurerar på varje underordnad primär plats. Klienter som installeras från en distributions plats har åtkomst till klient språken från platsen på den översta nivån, medan klienter som installerar från en hanterings plats har åtkomst till klient språken från den tilldelade primära platsen.  

10. På sidan **plats-och installations inställningar** anger du följande inställningar för den nya plats som du installerar:  

    - **Platskod**: [Varje platskod i en hierarki måste vara unik](prepare-to-install-sites.md#bkmk_sitecodes). Använd tre alfanumeriska siffror: A till Z och 0 till 9. Eftersom plats koden används i mappnamn ska du inte använda Windows-reserverade namn, inklusive:  
        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

        > [!NOTE]  
        > Installations programmet verifierar inte om den platskod som du anger redan används eller om det är ett reserverat namn.  

    - **Plats namn**: varje plats kräver detta egna namn som kan hjälpa dig att identifiera platsen.  

    - **Installationsmapp**: den här mappen är sökvägen till Configuration Manager installationen. Du kan inte ändra platsen när platsen har installerats. Sökvägen får inte innehålla Unicode-tecken eller avslutande blank steg.  

        > [!NOTE]  
        > Överväg om du vill använda standardmappen för installation. Om du använder standard operativ systemets partition i en produktions miljö kan följande problem uppstå i framtiden:  
        >
        > - Om Configuration Manager använder ytterligare ledigt disk utrymme på operativ systemets partition fungerar varken Windows eller Configuration Manager korrekt. Om du installerar Configuration Manager på en separat partition påverkar disk användningen inte operativ systemet.
        > - Configuration Manager prestanda är bättre med en snabb disk. Vissa Server design optimerar inte operativ system disken för snabbare.
        > - Du kan underhålla, återställa eller installera om operativ systemet utan att påverka Configuration Manager-installationen.  

11. På sidan **plats installation** använder du följande alternativ som matchar ditt scenario:  

    - **Jag installerar en central administrations plats:**  

        På sidan **installation av central administrations plats** väljer du **Installera som första plats i en ny hierarki**och väljer sedan **Nästa** för att fortsätta.  

    - **Jag expanderar en fristående primär plats till en hierarki med en central administrations plats:**  

        På sidan **installation av central administrations plats** väljer du **expandera en befintlig fristående primär till en hierarki**. Ange sedan det fullständiga domän namnet för den fristående primära plats servern och välj **Nästa** för att fortsätta.  

        De media som du använder för att installera den nya centrala administrations platsen måste matcha den primära platsens version.  

    - **Jag installerar en fristående primär plats:**  

        På sidan **installation av primär plats** väljer du **installera den primära platsen som en fristående plats**och väljer sedan **Nästa**.  

    - **Jag installerar en underordnad primär plats:**  

        På sidan **installation av primär plats** väljer du **Anslut den primära platsen till en befintlig hierarki**. Ange sedan det fullständiga domän namnet för den centrala administrations platsen och välj **Nästa**.  

12. Ange följande information på sidan **databas information** :  

    - **SQL Server namn (FQDN)**: som standard är det här värdet inställt på plats serverdatorn.  

        Om du använder en anpassad port lägger du till den porten i det fullständiga domän namnet för SQL Server. Följ det fullständiga domän namnet för SQL Server med ett kommatecken och sedan port numret. För Server *SQLServer1.fabrikam.com*använder du till exempel följande för att ange port *1551*: `SQLServer1.fabrikam.com,1551`  

    - **Instans namn**: som standard är det här värdet tomt. Den använder standard instansen av SQL på plats serverdatorn.  

    - **Databas namn**: som standard är det här värdet inställt på `CM_<Sitecode>` . Du kan anpassa det här värdet.  

    - **Service Broker port**: som standard är det här värdet inställt på att använda standard porten för SQL Server Service BROKER (SSB) på 4022. SQL använder den för att kommunicera direkt med plats databasen på andra platser.  

13. På den andra sidan med **databas information** kan du ange anpassade platser för SQL Server data filen och logg filen för SQL Server för plats databasen:  

    - Som standard används standard Sök vägarna för SQL Server.  

    - När du använder ett SQL Server kluster är alternativet för att ange anpassade fil platser inte tillgängligt.  

    - Krav kontrollen kontrollerar inte ledigt disk utrymme för anpassade fil platser.  

14. På sidan **Inställningar för SMS-provider** anger du FQDN för den server där du vill installera SMS-providern.  

    - Som standard anger den plats servern.  

    - När platsen har installerats kan du konfigurera ytterligare SMS-providers. Mer information finns i [Planera för SMS-providern](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

15. På sidan **kommunikations inställningar för klient** väljer du om du vill konfigurera alla plats system så att de bara accepterar HTTPS-kommunikation från klienter eller att kommunikations metoden ska konfigureras för varje plats system roll.  

    När du väljer **alla roller för plats system accepterar endast HTTPS-kommunikation från klienter**, måste klient datorn ha ett giltigt PKI-certifikat för klientautentisering. Mer information finns i [krav för PKI-certifikat](../../../plan-design/network/pki-certificate-requirements.md).  

    > [!NOTE]  
    > Det här steget gäller bara när du installerar en primär plats. Om du installerar en central administrations plats hoppar du över det här steget.  

16. På sidan **plats system roller** väljer du om du vill installera en hanterings plats eller en distributions plats. För varje roll som du väljer att installera genom att konfigurera:  

    - Ange **FQDN** för den server som ska vara värd för rollen. Välj sedan den klient anslutnings metod som servern ska stödja: HTTP eller HTTPS.  

    - Om du har valt **alla roller för plats system accepterar endast HTTPS-kommunikation från klienter** på föregående sida konfigureras klient anslutnings inställningarna automatiskt för https. Du kan inte ändra den här inställningen om du inte går tillbaka till föregående sida.  

    > [!NOTE]  
    > Det här steget gäller bara när du installerar en primär plats. Om du installerar en central administrations plats hoppar du över det här steget.  

    > [!NOTE]  
    > För att installera plats system roller använder installations programmet installations **kontot för plats system**. Som standard används den primära platsens dator konto. Det här kontot måste vara en lokal administratör på en fjärrdator för att plats system rollen ska kunna installeras. Om det här kontot saknar de behörigheter som krävs avmarkerar du plats system rollerna och installerar dem senare i Configuration Manager-konsolen, efter att du har konfigurerat ytterligare konton som ska användas som installations konton för plats system. Mer information finns i [konton](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  

17. På sidan **användnings data** granskar du informationen om data som Microsoft samlar in och väljer sedan **Nästa**. Mer information finns i [diagnostik-och användnings data](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

18. Sidan **konfiguration av tjänst anslutnings punkt** är bara tillgänglig i följande scenarier:  

    - När du installerar en fristående primär plats.  

    - När du installerar en central administrations plats.  

    > [!NOTE]  
    > Om du installerar en underordnad primär plats hoppar du över det här steget.  

     Om du installerar en central administrations plats som en del av scenariot för plats expansion och den här rollen redan är installerad på den fristående primära platsen måste du först avinstallera den här rollen från den fristående primära platsen. Endast en instans av den här rollen tillåts i en hierarki och stöds endast på platsen på den översta nivån i hierarkin.  

     När du har valt en konfiguration för **tjänst anslutnings punkten**väljer du **Nästa**. När installationen är klar kan du ändra den här konfigurationen i Configuration Manager-konsolen. Mer information finns i [om tjänst anslutnings punkten](../configure/about-the-service-connection-point.md).  

19. På sidan **Sammanfattning av inställningar** granskar du den inställning som du har valt. När du är klar väljer du **Nästa** för att starta krav kontrollen.  

20. På sidan **kontroll av installations krav** visas alla problem som granskaren kan identifiera.  

    - När krav kontrollen hittar ett problem väljer du ett objekt i listan för information om hur du löser problemet.  

    - Lös **misslyckade** objekt innan du kan fortsätta att installera platsen. Försök också att lösa objekt med statusen **Varning**, men de blockerar inte installationen av platsen.  

    - När du har löst problemet väljer du **kör kontroll** för att köra krav kontrollen igen.  

        När krav kontrollen körs, och inga kontroller får statusen **misslyckad** , kan du välja **starta installationen** för att starta plats installationen.  

    > [!TIP]  
    > Förutom feedback som guiden tillhandahåller kan du hitta ytterligare information om nödvändiga problem i filen **ConfigMgrPrereq. log** . Den finns i roten på system enheten på den dator där du installerar platsen. Mer information finns i [lista över krav kontroller](list-of-prerequisite-checks.md).  

21. På sidan **installation** visar installations status. När den grundläggande plats Server installationen är klar kan du **stänga** installations guiden. När du stänger guiden fortsätter installationen och de ursprungliga plats konfigurationerna i bakgrunden.  

    - Du kan ansluta en Configuration Manager-konsol till platsen innan installationen är klar. Den här konsolen ansluter som skrivskyddad och låter dig Visa objekt och inställningar, men du kan inte ändra något.  

    - När installationen är klar kan du ansluta en konsol som kan redigera objekt och inställningar.  


## <a name="expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Expandera en fristående primär plats

När du har installerat en fristående primär plats som din första plats kan du välja att utöka platsen till en större hierarki genom att installera en central administrations plats.

När du expanderar en fristående primär plats installerar du en ny central administrations plats som använder den befintliga fristående primära plats databasen som referens. När den nya centrala administrations platsen har installerats fungerar den fristående primära platsen som en underordnad primär plats.

- Du kan bara expandera en fristående primär plats till en ny hierarki.  

- Du kan bara expandera en fristående primär plats till en speciell hierarki. Du kan inte använda det här alternativet för att ansluta ytterligare fristående primära platser till samma hierarki. Använd i stället migreringsguiden för att migrera data från en hierarki till en annan. Mer information finns i [migrera data mellan hierarkier](../../../migration/migrate-data-between-hierarchies.md).  

- När du har expanderat en fristående plats till en hierarki med en central administrations plats kan du lägga till ytterligare underordnade primära underordnade platser.  

- Om du vill ta bort en primär plats från en hierarki med en central administrations plats måste du först avinstallera den primära platsen.  

Om du vill expandera platsen använder du installations guiden för Configuration Manager för att installera en ny central administrations webbplats med följande varningar:  

- Installera den centrala administrations platsen med samma version av Configuration Manager som den fristående primära platsen.  

- På sidan **komma igång** i installations guiden väljer du alternativet för att installera en central administrations plats. I ett senare steg i installationen väljer du ett alternativ för att expandera en befintlig fristående primär plats.  

- När du konfigurerar sidan **Val av klient språk** för den nya centrala administrations platsen väljer du samma klient språk som har kon figurer ATS för den fristående primära plats som du expanderar.  

- På sidan **plats installation** väljer du alternativet för att expandera den fristående primära platsen.  

För att expandera en fristående primär plats måste du först se för [förutsättningarna för att expandera en plats](prerequisites-for-installing-sites.md#bkmk_expand). Använd sedan proceduren [för att installera en primär eller Central administrations plats](use-the-setup-wizard-to-install-sites.md#bkmk_installpri) tidigare i den här artikeln.


## <a name="install-a-secondary-site"></a><a name="bkmk_secondary"></a> Installera en sekundär plats

Använd Configuration Manager-konsolen för att installera en sekundär plats.  

- Om konsolen som du använder inte är ansluten till den primära platsen som ska vara den överordnade platsen till den nya sekundära platsen replikeras kommandot för att installera platsen till rätt primär plats.  

- Innan du startar plats installationen måste du kontrol lera att ditt användar konto har de nödvändiga behörigheterna. Se också till att den server som ska vara värd för den nya sekundära platsen uppfyller alla krav för användning som sekundär plats Server.  

- När du installerar den sekundära platsen Configuration Manager konfigurerar den nya platsen att använda klient kommunikations portarna som har kon figurer ATS på den överordnade primära platsen.  

### <a name="process-to-install-a-secondary-site"></a><a name="bkmk_installsecondary"></a> Process för att installera en sekundär plats  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** . Välj den plats som ska vara den överordnade primära platsen för den nya sekundära platsen.  

2. Starta **guiden skapa sekundär plats**genom att välja **skapa sekundär plats** i menyfliksområdet.  

3. På sidan **innan du börjar kontrollerar du** att den primära platsen som visas är den plats som du vill ska vara överordnad den nya sekundära platsen. Välj sedan **Nästa**.  

4. På sidan **Allmänt** anger du följande inställningar:  

    - **Platskod**: Varje platskod i en hierarki måste vara unik. Använd tre alfanumeriska siffror: A till Z och 0 till 9. Eftersom plats koden används i mappnamn ska du inte använda Windows-reserverade namn, inklusive:  

        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

    > [!NOTE]  
    > Installations programmet verifierar inte om den platskod som du anger redan används eller om det är ett reserverat namn.  

    - **Plats Server namn**: det här värdet är det fullständiga domän namnet för den server där den nya sekundära platsen ska installeras.  

    - **Plats namn**: varje plats kräver detta egna namn som kan hjälpa dig att identifiera platsen.  

    - **Installationsmapp**: den här mappen är sökvägen till Configuration Manager installationen. Du kan inte ändra platsen när platsen har installerats. Sökvägen får inte innehålla Unicode-tecken eller avslutande blank steg.  

    > [!IMPORTANT]  
    > När du har angett information på den här sidan kan du välja **Sammanfattning** för att gå direkt till sidan **Sammanfattning** i guiden. Den här åtgärden använder standardinställningarna för resten av alternativen för den sekundära platsen.  
    > 
    > - Använd bara det här alternativet när du är bekant med standardinställningarna i guiden och de är de inställningar som du vill använda.  
    > - När du använder standardinställningarna är inga gränser kopplade till distributions platsen. Innan du konfigurerar gränser grupper som inkluderar den sekundära plats servern använder klienterna inte den distributions plats som är installerad på den sekundära platsen som en innehålls käll plats.  

5. På sidan **installations källfiler** väljer du hur den sekundära platsens dator hämtar källfiler för att installera platsen.  

    När du använder CD. De senaste källfilerna som delas i nätverket eller som kopieras lokalt till den sekundära plats servern:  

    - **Version 1802 och tidigare**

        - CD: n. Den senaste käll fils platsen innehåller en mapp med namnet **Redist**. Flytta den här **Redist** -mappen som en undermapp under mappen **SMSSETUP**  

            > [!Note]  
            > Om det uppstår ett fel med hash-matchningsfel under installationen uppdaterar du mappen **Redist** . Använd [installations hämtaren](setup-downloader.md) för att hämta de senaste filerna. För filer som orsakar ett hash-matchningsfel kan du även kopiera dem från den uppdaterade **Redist** -mappen till mappen **SMSSETUP\BIN\X64** .

    - **Version 1806 och senare**<!-- SCCMDocs-pr issue 3164 -->

        - CD: n. Den senaste käll fils platsen innehåller en mapp med namnet **Redist**. Flytta den här **Redist** -mappen som en undermapp under mappen **SMSSETUP**  

        - Kopiera följande filer från **Redist** -mappen till mappen **SMSSETUP\BIN\X64** :  
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - Om någon av filerna från **Redist** inte är tillgänglig, kan inte installations programmet installera den sekundära platsen.  

    - Dator kontot för den sekundära plats servern måste ha **Läs** behörighet till käll fils katalogen och resursen.  

6. På sidan **SQL Server inställningar** anger du vilken version av SQL Server som ska användas och konfigurerar sedan relaterade inställningar.  

    > [!NOTE]  
    > Installations programmet validerar inte den information som du anger på den här sidan förrän installationen påbörjas. Verifiera inställningarna innan du fortsätter.  

    - **Installera och konfigurera en lokal kopia av SQL Express på den sekundära platsens dator**  

        - **SQL Server tjänst port**: Ange SQL Server Service-port för SQL Server Express som ska användas. Tjänst porten är vanligt vis konfigurerad för att använda TCP-port 1433, men du kan konfigurera en annan port.  

        - **SQL Server Broker-port**: Ange SQL Server Service BROKER (SSB) för SQL Server Express som ska användas. Service Broker är vanligt vis konfigurerat för att använda TCP-port 4022, men du kan konfigurera en annan port. Ange en giltig port som inte används av någon annan plats eller tjänst, och som inte blockerar några brand Väggs begränsningar.  

    - **Använd en befintlig SQL Server instans**  

        - **SQL Server FQDN**: granska FQDN för datorn som kör SQL Server. Du måste använda en lokal server som kör SQL Server som värd för den sekundära plats databasen och du kan inte ändra den här inställningen.  

        - **SQL Server instans**: Ange den instans av SQL Server som ska användas som sekundär plats databas. Lämna det här alternativet tomt om du vill använda standard instansen.  

        - **Databas namn för ConfigMgr-plats**: Ange det namn som ska användas för den sekundära plats databasen.  

        - **SQL Server Broker-port**: Ange SQL Server Service BROKER (SSB) för SQL Server som ska användas. Ange en giltig port som inte används av någon annan plats eller tjänst och som inte blockerar brand Väggs begränsningar.  

    > [!TIP]  
    > En lista över de SQL Server-versioner som Configuration Manager stöder finns i [SQL Server versioner som stöds](../../../plan-design/configs/support-for-sql-server-versions.md).  

7. På sidan **distributions plats** konfigurerar du inställningarna för den distributions plats som ska installeras på den sekundära plats servern.  

    - **Inställningar som krävs:**  

        - **Ange hur klient enheter ska kommunicera med distributions platsen**: Välj mellan http och https.  

        - **Skapa ett självsignerat certifikat eller importera ett PKI-klientcertifikat**: Välj mellan att använda ett självsignerat certifikat eller importera ett certifikat från PKI: n. Med ett självsignerat certifikat kan du också tillåta anonyma anslutningar från Configuration Manager klienter till innehålls biblioteket. Certifikatet används för att autentisera distributions platsen till en hanterings plats innan distributions platsen skickar status meddelanden. Mer information finns i [krav för PKI-certifikat](../../../plan-design/network/pki-certificate-requirements.md).  

    - **Valfria inställningar:**  

        - **Installera och konfigurera IIS om det krävs av Configuration Manager**: Välj den här inställningen om du vill att Configuration Manager installera och konfigurera Internet Information Services (IIS) på servern, om det inte redan är installerat. IIS krävs på alla distributions platser.  

            > [!NOTE]  
            > Även om den här inställningen är valfri måste IIS installeras på servern innan en distributions plats kan installeras.  

        - **Aktivera och konfigurera BranchCache för den här distributions platsen**  

        - **Beskrivning**: det här värdet är en egen beskrivning för distributions platsen som hjälper dig att identifiera den.  

        - **Aktivera den här distributions platsen för förinstallerat innehåll**  

8. På sidan **enhets inställningar** anger du enhets inställningarna för distributions platsen för den sekundära platsen.  

    Du kan konfigurera upp till två disk enheter för innehålls biblioteket och två disk enheter för paket resursen. Configuration Manager kan dock använda ytterligare enheter när de första två når den konfigurerade enhets utrymmes reserven. På sidan **enhets inställningar** kan du konfigurera prioriteten för disk enheterna och mängden ledigt disk utrymme som ska finnas kvar på varje disk enhet.  

    - **Reserverat enhets utrymme (MB)**: det värde som du konfigurerar för den här inställningen avgör mängden ledigt utrymme på en enhet innan Configuration Manager väljer en annan enhet och fortsätter med kopierings processen till den enheten. Innehållsfiler kan omfatta flera enheter.  

    - **Innehålls platser**: Ange innehålls platserna för innehålls biblioteket och paket resursen. Configuration Manager kopierar innehåll till den primära innehålls platsen tills mängden ledigt utrymme når det värde som anges för **reserverat enhets utrymme (MB)**.  

    Som standard är innehålls platserna inställda på **Automatisk**. Den primära innehålls platsen har angetts till den disk enhet som har mest disk utrymme vid installationen. Den sekundära platsen har angetts till den disk enhet som har mest ledigt disk utrymme efter den primära enheten. När de primära och sekundära enheterna når enhets utrymmes reserven, Configuration Manager väljer en annan tillgänglig enhet med mest ledigt disk utrymme och fortsätter kopierings processen.  

9. På sidan **innehålls validering** anger du om du vill verifiera integriteten för innehållsfiler på distributions platsen.  

    - När du aktiverar innehålls validering enligt ett schema startar Configuration Manager processen vid den schemalagda tiden. Allt innehåll på distributions platsen verifieras.  

    - Du kan också konfigurera **prioritet för innehålls validering**.  

    - Om du vill visa resultatet av innehålls validerings processen går du till arbets ytan **övervakning** i Configuration Manager-konsolen, expanderar **distributions status**och väljer noden **innehålls status** . Den visar innehållet för varje paket typ. Dessa typer omfattar program, program uppdaterings paket och start avbildningar.  

10. På sidan **gränser grupper** hanterar du de gränser grupper som den här distributions platsen är tilldelad till:  

    - Vid innehålls distribution måste klienterna finnas i en gränser grupp som är associerad med distributions platsen för att använda den som en käll plats för innehåll.  

    - Du kan välja alternativet **Tillåt återställnings käll plats för innehåll** för att tillåta att klienter utanför dessa begränsnings grupper går tillbaka och använder distributions platsen som en käll plats för innehåll när inga prioriterade distributions platser är tillgängliga.  

        Mer information finns i [grundläggande begrepp för innehålls hantering](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

11. På sidan **Sammanfattning** kontrollerar du inställningarna och väljer sedan **Nästa** för att installera den sekundära platsen. När sidan **slut för ande** visas i guiden kan du stänga guiden. Installationen av den sekundära platsen fortsätter i bakgrunden.  

### <a name="how-to-verify-the-secondary-site-installation-status"></a><a name="bkmk_verify"></a> Verifiera installations status för den sekundära platsen  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2. Välj den sekundära plats som du vill installera och välj sedan **Visa installations status** i menyfliksområdet.  

    > [!TIP]  
    > När du installerar fler än en sekundär plats i taget körs krav kontrollen mot en enskild plats i taget. Du måste slutföra en plats innan den börjar kontrol lera nästa plats.