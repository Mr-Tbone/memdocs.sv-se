---
title: Webbplats återställning
titleSuffix: Configuration Manager
description: Lär dig hur du återställer dina platser i Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b17c8c9ed0c1f6f9a5aeb487e07ad3d3dc66cbae
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82903964"
---
# <a name="recover-a-configuration-manager-site"></a>Återställa en Configuration Manager-plats

*Gäller för: Configuration Manager (aktuell gren)*

Kör en Configuration Manager webbplats återställning när en plats har misslyckats eller data förlust sker i plats databasen. Reparation och omsynkronisering av data är nyckeluppgifter vid en platsåterställning och krävs för att förhindra aktivitetsstörningar.

Avsnitten i den här artikeln kan hjälpa dig att återställa en Configuration Manager webbplats. Information om hur du skapar en säkerhets kopia finns i [säkerhets kopiering för Configuration Manager](backup-and-recovery.md).

## <a name="considerations-before-recovering-a-site"></a>Att tänka på innan du återställer en plats

> [!Important]  
> Den här informationen gäller endast för Site Recovery-scenarier. När du uppgraderar den lokala infrastrukturen och inte aktivt återställer en misslyckad plats kan du läsa informationen i följande artiklar:
>
> - [Uppgradera den lokala infrastrukturen](upgrade-on-premises-infrastructure.md)
> - [Ändra infrastrukturen](modify-your-infrastructure.md)

### <a name="prepare-the-server-hardware"></a>Förbered server maskin varan

<!-- 2841893 -->

Se till att befintliga konfigurationer inte finns på plats servern. Alla tidigare konfigurationer kan orsaka konflikter under webbplats återställnings processen. Använd något av följande alternativ för server maskin varan:

- Använd en ny server som uppfyller de allmänna och återställnings kraven.

- Formatera diskarna och installera om operativ systemet på den befintliga servern. Kontrol lera att det uppfyller de allmänna och återställnings kraven.

- Återanvänd en befintlig server som du har rensat

Använd någon av följande procedurer för att rensa en befintlig server:

#### <a name="clean-an-existing-server-for-site-server-recovery-only"></a>Rensa en befintlig server för återställning av plats Server

1. Ta bort SMS-registernycklar:`HKLM\Software\Microsoft\SMS`
2. Ta bort alla register poster som börjar med `SMS` från `HKLM\System\CurrentControlSet\Services` . Ett exempel:
    - SMS_DISCOVERY_DATA_MANAGER
    - SMS_EXECUTIVE
    - SMS_INBOX_MONITOR
    - SMS_INVENTORY_DATA_LOADER
    - SMS_LAN_SENDER
    - SMS_MP_FILE_DISPATCH_MANAGER
    - SMS_SCHEDULER
    - SMS_SITE_BACKUP
    - SMS_SITE_COMPONENT_MANAGER
    - SMS_SITE_SQL_BACKUP
    - SMS_SITE_VSS_WRITER
    - SMS_SOFTWARE_METERING_PROCESSOR
    - SMS_STATE_SYSTEM
    - SMS_STATUS_MANAGER
    - SMS_WSUS_SYNC_MANAGER
    - SMSvcHost 3.0.0.0
    - SMSvcHost 4.0.0.0
3. Avinstallera Configuration Manager-konsolen
4. Starta om servern
5. Bekräfta att alla ovanstående register nycklar har tagits bort.

Servern är nu klar för återställnings proceduren Configuration Manager.

#### <a name="clean-an-existing-server-for-site-database-recovery-only"></a>Rensa en befintlig server för plats databas återställning endast

1. Säkerhetskopiera plats databasen. Säkerhetskopiera även andra stödda databaser, som WSUS.
2. Glöm inte att anteckna SQL Server-namnet och instans namnet
3. Ta bort plats databasen manuellt från SQL Server
4. Starta om SQL Server

Servern är nu klar för återställnings proceduren Configuration Manager.

#### <a name="clean-an-existing-server-for-full-recovery"></a>Rensa en befintlig server för fullständig återställning

1. Säkerhetskopiera plats databasen. Säkerhetskopiera även andra stödda databaser, som WSUS.
2. Skapa en kopia av innehålls biblioteket
3. Ta bort plats databasen manuellt från SQL Server
4. Avinstallera Configuration Manager-platsen
5. Ta bort installationsmappen för Configuration Manager manuellt och andra Configuration Manager mappar
6. Starta om servern
7. Återställa innehålls biblioteket och andra databaser som WSUS

Servern är nu klar för återställnings proceduren Configuration Manager.

### <a name="use-a-supported-version-and-same-edition-of-sql-server"></a>Använd en version som stöds och samma version av SQL Server

<!-- SCCMDocs#751 -->

Använd om möjligt samma version av SQL Server. Det finns dock stöd för att återställa en databas till en nyare version.

Ändra inte SQL Server versionen. Det finns inte stöd för att återställa en plats databas från Standard Edition till Enterprise Edition.

Ytterligare SQL Server konfigurations krav:

- SQL Server kan inte ställas **in på enanvändarläge**.
- Kontrol lera att MDF-och LDF-filerna är giltiga. När du återställer en plats finns det ingen kontroll över filens tillstånd.  

### <a name="sql-server-always-on-availability-groups"></a>SQL Server AlwaysOn-tillgänglighetsgrupper

Om du använder SQL Server Always on-tillgänglighetsgrupper för att vara värd för plats databasen ändrar du återställnings planerna enligt beskrivningen i [förbereda för att använda SQL Server Always on](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-recovery).

### <a name="database-replicas"></a>Databas repliker

När du har återställt en plats databas som du har konfigurerat för databas repliker kan du konfigurera om varje replik. Innan du kan använda databas replikerna återskapar du både publikationer och prenumerationer.

## <a name="determine-your-recovery-options"></a>Avgör dina återställningsalternativ

Det finns två huvud områden att tänka på för Configuration Manager primär plats Server och återställning av central administrations plats (CAS): **plats servern** och **plats databasen**.
I följande avsnitt får du hjälp att välja de bästa alternativen för ditt återställnings scenario.

> [!NOTE]  
> När Configuration Manager installations programmet identifierar en befintlig-plats på servern kan du starta en plats återställning, men återställnings alternativen för plats servern är begränsade. Om du exempelvis kör installationen på en befintlig platsserver och väljer återställning kan du återställa platsdatabasservern, men alternativet för återställning av platsservern är inaktiverat.

### <a name="site-server-recovery-options"></a>Återställningsalternativ för platsservern

Starta Configuration Manager installations programmet från en kopia av **CD-skivan. Den senaste** mappen som du skapade utanför installations-mappen för Configuration Manager.  

- Om du kör installations programmet från **Start** -menyn på plats servern är alternativet **Återställ en plats** inte tillgängligt.  

- Om du har installerat några uppdateringar inifrån Configuration Manager-konsolen innan du gjorde säkerhets kopieringen kan du inte installera om platsen med hjälp av installations programmet från följande platser:

  - Installations medium
  - Configuration Manager installations Sök väg

Välj sedan alternativet **Återställ en plats** . Du har följande återställnings alternativ för den misslyckade plats servern:  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>Återställa plats servern med en befintlig säkerhets kopia

Använd det här alternativet om du har en Configuration Manager säkerhets kopia av plats servern från före plats felet. Platsen skapar säkerhets kopian som en del av underhålls uppgiften **plats Server för säkerhets kopiering** . Platsen installeras om och plats inställningarna konfigureras baserat på den plats som säkerhetskopierades.  

#### <a name="reinstall-the-site-server"></a>Installera om plats servern

Använd det här alternativet om du inte har någon säkerhets kopia av plats servern. Plats servern installeras om och du måste ange plats inställningarna på samma sätt som vid en första installation.  

- Använd samma platskod och plats databas namn som du använde när den felande platsen först installerades.  

- Du kan installera om platsen på en ny dator som kör en ny operativ system version.  

- Servern måste använda samma värdnamn och fullständigt kvalificerat domän namn (FQDN) för den ursprungliga plats servern.

### <a name="site-database-recovery-options"></a>Återställningsalternativ för platsdatabasen

När du kör Configuration Manager installations programmet har du följande återställnings alternativ för plats databasen:  

#### <a name="recover-the-site-database-using-a-backup-set"></a>Återställa plats databasen med en säkerhets kopia

Använd det här alternativet om du har en Configuration Manager säkerhets kopia av plats databasen från före databas felet. Platsen skapar säkerhets kopian som en del av underhålls uppgiften **plats Server för säkerhets kopiering** . Vid återställning av en primär plats i en-hierarki hämtas återställnings processen från CAS till alla ändringar som görs i plats databasen efter den senaste säkerhets kopieringen. När du återställer CAS hämtar återställnings processen dessa ändringar från en primär referens plats. När du återställer plats databasen för en fristående primär plats förlorar du plats ändringarna efter den senaste säkerhets kopieringen.  

När du återställer plats databasen för en plats i en hierarki skiljer sig återställnings beteendet för en certifikat utfärdare och en primär plats. Beteendet är också detsamma när den senaste säkerhets kopieringen ligger innanför eller utanför SQL Server kvarhållningsperioden för ändrings spårning. Mer information finns i avsnittet om [återställnings scenarier för plats databas](#site-database-recovery-scenarios) i den här artikeln.  

> [!NOTE]  
> Om du väljer att återställa plats databasen med hjälp av en säkerhets kopia, men plats databasen redan finns, Miss lyckas återställningen.  

#### <a name="create-a-new-database-for-this-site"></a>Skapa en ny databas för den här platsen

Använd det här alternativet om du inte har en säkerhets kopia av plats databasen. I en hierarki skapar återställnings processen en ny plats databas. När du återställer en underordnad primär plats återställs data genom att replikeras från certifikat utfärdarna. När du återställer CAS replikeras data från en primär referens plats. Det här alternativet är inte tillgängligt när du återställer en fristående primär plats eller en certifikat utfärdare som inte har några primära platser.  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>Använd en plats databas som har återställts manuellt

Använd det här alternativet om du redan har återställt Configuration Manager plats databasen men måste slutföra återställnings processen.  

- Configuration Manager kan återställa plats databasen från någon av följande processer:  

  - Åtgärden Configuration Manager säkerhets kopierings underhåll  
  - Säkerhets kopiering av en plats databas med Data Protection Manager (DPM)  
  - En annan säkerhets kopierings process  

    När du har återställt plats databasen med hjälp av en metod utanför Configuration Manager kör du installations programmet och väljer det här alternativet för att slutföra återställningen av plats databasen.  

    > [!NOTE]  
    > När du använder DPM för att säkerhetskopiera plats databasen använder du DPM-procedurerna för att återställa plats databasen till en angiven plats innan du fortsätter med återställnings processen i Configuration Manager. Mer information om DPM finns i dokumentations biblioteket för [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) .  

- När du återställer en primär plats databas i en-hierarki, hämtas återställnings processen från CAS till alla ändringar som görs i plats databasen efter den senaste säkerhets kopieringen. När du återställer CAS hämtar återställnings processen dessa ändringar från en primär referens plats. När du återställer plats databasen för en fristående primär plats förlorar du plats ändringarna efter den senaste säkerhets kopieringen.  

#### <a name="skip-database-recovery"></a>Hoppa över databas återställning

Använd det här alternativet om ingen data förlust har inträffat på Configuration Manager plats databas servern. Det här alternativet är bara giltigt när plats databasen finns på en annan dator än den plats server som du återställer.  

### <a name="sql-server-change-tracking-retention-period"></a>Kvarhållningsperioden för spårning av ändringar för SQL Server

Configuration Manager aktiverar ändrings spårning för plats databasen i SQL Server. Med ändrings spårning kan Configuration Manager fråga efter information om de ändringar som gjorts i databas tabellerna efter en tidigare tidpunkt. Kvarhållningsperioden anger hur länge informationen om ändrings spårningen ska behållas. Som standard är plats databasen konfigurerad för att ha en kvarhållningsperiod på fem dagar. När du återställer en platsdatabas fortsätter återställningsprocessen på olika sätt beroende på om din säkerhetskopia görs inom kvarhållningsperioden eller inte. Om din SQL Server till exempel Miss lyckas och den senaste säkerhets kopieringen är sju dagar gammal, är den utanför kvarhållningsperioden.

Mer information om SQL Server ändrings spårning av intern information finns i följande blogg inlägg från SQL Server-teamet: [ändringsspårning rensa-del 1](https://docs.microsoft.com/archive/blogs/sql_server_team/change-tracking-cleanup-part-1) och [ändringsspårning rensning-del 2](https://docs.microsoft.com/archive/blogs/sql_server_team/change-tracking-cleanup-part-2).

### <a name="reinitialization-of-site-or-global-data"></a>Initiera om plats-eller globala data

Den process där platsdata eller globala data ominiteras och befintliga data i platsdatabasen ersätts med data från en annan platsdatabas. Om platsen ABC exempelvis initierar om data från plats XYZ genomförs följande steg:

- Data kopieras från plats XYZ till plats ABC.
- Befintliga data för plats XYZ tas bort från platsdatabasen på plats ABC.
- Kopierade data från plats XYZ förs in i platsdatabasen för plats ABC.

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-cas"></a>Exempel scenario 1: den primära platsen initierar om globala data från CAS

Vid återställnings processen tas befintliga globala data för den primära platsen i den primära plats databasen bort och data ersätts med de globala data som kopieras från certifikat utfärdarna.

#### <a name="example-scenario-2-the-cas-reinitializes-the-site-data-from-a-primary-site"></a>Exempel scenario 2: CAS initierar om plats data från en primär plats

Vid återställnings processen tas befintliga plats data för den primära platsen i CAS-databasen bort. Data ersätts med de plats data som kopieras från den primära platsen. Plats data för andra primära platser påverkas inte.

### <a name="site-database-recovery-scenarios"></a>Scenarion för återställning av platsdatabas

När en plats databas har återställts från en säkerhets kopia försöker Configuration Manager återställa ändringarna på platsen och globala data efter den senaste säkerhets kopieringen av databasen. Configuration Manager startar följande åtgärder när en plats databas har återställts från säkerhets kopian:  

#### <a name="recovered-site-is-a-cas"></a>Den återställda platsen är en certifikat utfärdare

- Databassäkerhetskopian gjordes inom kvarhållningsperioden för ändringsspårning  

  - **Globala data**: ändringarna i globala data efter säkerhets kopieringen replikeras från alla primära platser.  

  - **Plats data**: ändringarna i plats data efter säkerhets kopieringen replikeras från alla primära platser.  

- Databassäkerhetskopian gjordes inte inom kvarhållningsperioden för ändringsspårning  

  - **Globala data**: CAS initierar om globala data från den primära referens platsen om du anger den. Sedan initierar alla andra primära platser om globala data från certifikat utfärdarna. Om du inte anger en referens plats initierar alla primära platser om globala data från certifikat utfärdarna. Den här informationen är det du återställde från säkerhets kopian.  

  - **Plats data**: CAS initierar om plats data från varje primär plats.  

#### <a name="recovered-site-is-a-primary-site"></a>Den återställda platsen är en primär plats

- Databassäkerhetskopian gjordes inom kvarhållningsperioden för ändringsspårning  

  - **Globala data**: ändringarna i globala data efter säkerhets kopieringen replikeras från CAS.  

  - **Plats data**: CAS initierar om plats data från den primära platsen. Ändringar efter att säkerhets kopian förlorats. Klienter återskapar de flesta data när de skickar information till den primära platsen.  

- Databassäkerhetskopian gjordes inte inom kvarhållningsperioden för ändringsspårning  

  - **Globala data**: den primära platsen initierar om globala data från certifikat utfärdarna.  

  - **Plats data**: CAS initierar om plats data från den primära platsen. Ändringar efter att säkerhets kopian förlorats. Klienter återskapar de flesta data när de skickar information till den primära platsen.  

## <a name="site-recovery-procedures"></a>Procedurer för platsåterställning

Använd någon av följande procedurer för att få hjälp att återställa plats servern och plats databasen:

### <a name="start-a-site-recovery-in-the-setup-wizard"></a>Starta en webbplats återställning i installations guiden

1. Kopiera [CD: n. Den senaste mappen](the-cd.latest-folder.md) till en plats utanför mappen Configuration Manager-installation. Från kopian av CD: n. Senaste mappen, kör installations guiden för Configuration Manager.  

2. På sidan **komma igång** väljer du **Återställ en plats**och väljer sedan **Nästa**.  

3. Slutför guiden med hjälp av de alternativ som är lämpliga för din platsåterställning.  

     - Under återställningen identifierar installations programmet den SQL Server Service Broker-port (SSB) som används av SQL Server. Ändra inte den här port inställningen under återställningen eller datareplikeringen fungerar inte korrekt när återställningen har slutförts.  

     - Du kan ange den ursprungliga eller en ny sökväg som ska användas för Configuration Manager installationen i installations guiden.  

### <a name="start-an-unattended-site-recovery"></a>Starta en obevakad webbplats återställning

1. Förbered det obevakade installationsskriptet för de alternativ som du behöver för platsåterställningen. Mer information finns i [obevakad plats återställning](unattended-recovery.md).  

2. Kör Configuration Manager-installationen med hjälp av `/script` kommando rads alternativet. Du kan till exempel skapa en initierings fil för installations programmet **namnet ConfigMgrUnattend. ini**. Du sparar den i `C:\Temp` katalogen på den dator där du kör installations programmet. Ange följande kommando:  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  

> [!NOTE]  
> När du har återställt en certifikat utfärdare kan replikering av vissa plats data från underordnade platser inte upprättas. Dessa data kan omfatta maskin varu inventering, program varu inventering och status meddelanden.
>
> Om det här problemet uppstår initierar du om **ConfigMgrDRSSiteQueue** för databasreplikering. Använd **SQL Server Manager** för att köra följande fråga mot plats databasen för CAS:
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```

## <a name="post-recovery-tasks"></a>Aktiviteter efter återställning

När du har återställt platsen finns det flera uppgifter efter återställningen att tänka på innan plats återställningen är klar. Använd följande avsnitt för att få hjälp att slutföra platsåterställningsprocessen.

### <a name="reenter-user-account-passwords"></a>Ange användar konto lösen orden igen

Ange lösen orden för alla användar konton på platsen efter återställning av plats Server. Dessa lösen ord återställs under plats återställningen. Kontona visas på sidan **slutfört** i installations guiden när plats återställningen har slutförts. Listan sparas också `C:\ConfigMgrPostRecoveryActions.html` på den återställda plats servern.

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>Ange lösen ord för användar kontot igen efter plats återställningen

1. Öppna Configuration Manager-konsolen och Anslut till den återställda platsen.  

2. Gå till arbets ytan **Administration** , expandera **säkerhet**och välj sedan **konton**.  

3. För varje konto utför du följande steg för att ange lösen ordet igen:  

     1. Välj kontot från listan som identifieras efter Site Recovery.  

     2. Välj **Egenskaper** i menyfliksområdet.  

     3. På fliken **Allmänt** väljer du **Ange ange**, och ange sedan lösen ordet för kontot igen.  

     4. Välj **Verifiera**, Välj lämplig data källa för det valda användar kontot och välj sedan **Testa anslutning**. Det här steget testar att användar kontot kan ansluta till data källan och verifierar autentiseringsuppgifterna.  

     5. Välj **OK** för att spara lösen ords ändringarna och välj sedan **OK** för att stänga sidan konto egenskaper.  

#### <a name="reenter-pxe-passwords"></a>Ange PXE-lösenord igen

<!-- SCCMDocs#1683 -->

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **distributions platser** . Alla lokala distributions platser med **Ja** i **PXE** -kolumnen är aktiverade för PXE och kan ha ett lösen ord att ange.

1. Välj en PXE-aktiverad distributions plats och välj **Egenskaper** i menyfliksområdet.

1. Växla till **PXE** -fliken.

1. Om alternativet för att **kräva ett lösen ord när datorer använder PXE** är aktiverat, ange och bekräfta lösen ordet.

1. Välj **OK** för att spara och stänga egenskaperna.

Upprepa processen för alla andra PXE-aktiverade distributions platser.

#### <a name="reenter-task-sequence-passwords"></a>Ange lösen ord för aktivitetssekvens igen

<!-- SCCMDocs#1683 -->

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **operativ system**och väljer noden **aktivitetssekvenser** .

1. Välj en aktivitetssekvens och välj sedan **Redigera**i menyfliksområdet.

1. Granska följande steg för att ange lösen ord för att ange följande:

    - **Använd Windows-inställningar**: om du aktiverar och anger det lokala administratörs lösen ordet måste du ange och bekräfta lösen ordet.

    - **Använd Nätverks inställningar**: för det konto som har behörighet att ansluta till domänen väljer du **Ange**. Ange och bekräfta lösen ordet och välj sedan **Verifiera**.

    - **Avbilda operativ Systems avbildning**: för kontot som används för att komma åt målet väljer du **Ange**. Ange och bekräfta lösen ordet och välj sedan **Verifiera**.

    - **Anslut till nätverksmappen**: Välj **Ange**för kontot som används för att ansluta en nätverksmapp. Ange och bekräfta lösen ordet och välj sedan **Verifiera**.

    - **Aktivera BitLocker**: om du använder alternativet **TPM och PIN-kod**för nyckel hantering anger du PIN-koden igen.

    - **Anslut till domän eller arbets grupp**: för det konto som har behörighet att ansluta till domänen väljer du **Ange**. Ange och bekräfta lösen ordet och välj sedan **Verifiera**.

    - **Kör kommando rad**: om du använder alternativet för att **köra det här steget som följande konto**väljer du **Ange**. Ange och bekräfta lösen ordet och välj sedan **Verifiera**.

    - **Kör PowerShell-skript**: om du använder alternativet för att **köra det här steget som följande konto**väljer du **Ange**. Ange och bekräfta lösen ordet och välj sedan **Verifiera**.

Upprepa processen för alla aktivitetssekvenser.

### <a name="reenter-sideloading-keys"></a>Ange nycklar för separat inläsning

Efter en plats Server återställning anger du de Windows-nycklar för separat inläsning som angetts för platsen. Nycklarna återställs under plats återställningen. När du har angett nycklarna för separat inläsning återställer platsen antalet i kolumnen **aktiveringar som används** för Windows-nycklar för separat inläsning.

Innan plats haveriet till exempel visas **Totalt antal aktiveringar** som **100**. Antalet nycklar som enheterna har använt, eller **aktiveringar som används**, är **90**. Efter plats återställningen visar värdet för **Totalt antal aktiveringar** fortfarande **100**, men kolumnen **använda aktiveringar** visar felaktigt **0**. När 10 nya enheter använder en nyckel för separat inläsning finns det inga fler nycklar för separat inläsning och den elfte enheten kan inte använda en nyckel för separat inläsning.

### <a name="recreate-azure-services"></a>Återskapa Azure-tjänster

<!-- SCCMDocs#1022 -->

Efter webbplats återställning i Configuration Manager version 1806 visas följande fel meddelande i CloudMgr. log:

`Index (zero-based) must be greater than or equal to zero`

Lös detta genom att [förnya den hemliga nyckeln](../deploy/configure/azure-services-wizard.md#bkmk_renew) för varje Azure-klient anslutning.

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Konfigurera SSL för platssystemroller som använder IIS

När du återställer plats system som kör IIS och du har konfigurerat för HTTPS kan du konfigurera om IIS att använda webb Server certifikatet.

### <a name="reinstall-hotfixes"></a>Installera om snabb korrigeringar

Efter en plats återställning måste du installera om eventuella [out-of-band-snabbkorrigeringar](updates.md#bkmk_outofband) som har tillämpats på plats servern. Efter plats återställningen visar du listan över de tidigare installerade snabb korrigeringarna på sidan **slutfört** i installations guiden. Den här listan sparas också `C:\ConfigMgrPostRecoveryActions.html` på den återställda plats servern.

### <a name="recover-custom-reports"></a>Återställa anpassade rapporter

Vissa kunder skapar anpassade rapporter i SQL Server Reporting Services. När den här komponenten Miss lyckas återställer du rapporterna från en säkerhets kopia av rapport servern. Mer information om hur du återställer dina anpassade rapporter i repor ting Services finns i [säkerhets kopierings-och återställnings åtgärder för repor ting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).

### <a name="recover-content-files"></a>Återställa innehållsfiler

Plats databasen spårar var innehållsfilerna lagras på plats servern. Själva innehållsfilerna säkerhets kopie ras eller återställs inte som en del av säkerhets kopierings-och återställnings processen. Om du vill återställa innehållsfiler fullständigt återställer du innehålls biblioteket och paketets källfiler till den ursprungliga platsen. Det finns flera metoder för att återskapa innehållsfilerna. Den enklaste metoden är att återställa filerna från en fil system säkerhets kopia av plats servern.

Om du inte har en fil system säkerhets kopia för paketets källfiler, kopierar eller hämtar du dem manuellt. Den här processen liknar när du ursprungligen skapade paketet. Kör följande fråga i SQL Server för att hitta paketets käll plats för alla paket och program: `SELECT * FROM v_Package` . Identifiera paketets käll plats genom att titta på de första tre tecknen i paket-ID: t. Om paketets ID exempelvis är CEN00001 är platskoden för källplatsen CEN. När du ska återställa paketkällfiler måste de återställas till den plats där de fanns innan felet inträffade.

Om du inte har en fil system säkerhets kopia som innehåller innehålls biblioteket har du följande återställnings alternativ:  

- **Importera en förinstallerad innehålls fil**: i en Configuration Manager-hierarki kan du skapa en förinstallerad innehålls fil med alla paket och program från en annan plats. Importera sedan den förinstallerade innehålls filen för att återställa innehålls biblioteket på plats servern.  

- **Uppdatera innehåll**: Configuration Manager kopierar innehållet från paket källan till innehålls biblioteket. För att den här åtgärden ska slutföras måste källfilerna för paketet vara tillgängliga på den ursprungliga platsen. Gör den här åtgärden för varje paket och program.

### <a name="recover-custom-software-updates"></a>Återställa anpassade program uppdateringar

När du har inkluderat System Center Updates Publisher databasfiler i din säkerhets kopierings plan kan du återställa databaserna om uppdaterings utgivarens dator Miss lyckas. Mer information om Updates Publisher finns [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).

#### <a name="restore-the-updates-publisher-database"></a>Återställa Updates Publisher-databasen

1. Installera om Updates Publisher på den återställda datorn.  

2. Kopiera databas filen **Scupdb. SDF** från säkerhets kopierings målet till `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` på den dator som kör Updates Publisher.  

3. När fler än en användare kör Updates Publisher på datorn kopierar du varje databas fil till rätt plats för användar profiler.  

### <a name="user-state-migration-data"></a>Migreringsdata för användartillstånd

Som en del av egenskaperna för tillståndsmigrering anger du de mappar som lagrar användar tillstånds data. När du har återställt en plats för tillståndsmigrering återställer du manuellt användar tillstånds data på servern. Återställ den till samma mappar som lagrade data före felen.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Återskapa certifikatet för distributionsplatser

När du har återställt en plats kan **Distmgr. log** ange följande post för en eller flera distributions platser: `Failed to decrypt cert PFX data` . Den här posten anger att distributions platsens certifikat data inte kan dekrypteras av platsen. Lös problemet genom att återskapa eller importera certifikatet för berörda distributions platser igen. Använd cmdleten [set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint) PowerShell.

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Uppdatera certifikat som används för molnbaserade distributions platser

Configuration Manager kräver ett Azure-hanterings certifikat för plats servern för att kommunicera med molnbaserade distributions platser. Efter en plats återställning uppdaterar du certifikaten för molnbaserade distributions platser.

## <a name="recover-a-secondary-site"></a>Återställa en sekundär plats

Configuration Manager har inte stöd för säkerhets kopiering av databasen på en sekundär plats, men stöder återställning genom att installera om den sekundära platsen. Återställning av sekundär plats krävs när en Configuration Manager sekundär plats Miss lyckas.

### <a name="requirements"></a>Krav

- Servern måste uppfylla alla krav för sekundär plats och ha rätt behörighet.  

- Använd samma installations Sök väg som användes för den misslyckade platsen.  

- Använd en server med samma konfiguration som den felande servern. Den här konfigurationen omfattar det fullständigt kvalificerade domän namnet (FQDN).  

- Servern måste ha samma SQL Server konfiguration som den felande platsen.  

  - Under en sekundär webbplats återställning installerar Configuration Manager inte SQL Server Express om den inte redan är installerad på datorn.  

  - Använd samma version av SQL Server och samma instans av SQL Server som du använde för den sekundära plats databasen före problemet.  

### <a name="procedure"></a>Procedur

Använd åtgärden **Återställ sekundär plats** från noden **platser** i Configuration Manager-konsolen. Till skillnad från andra typer av platser, använder inte återställning för en sekundär plats en säkerhets kopia. Den här processen installerar om de sekundära platsens filer på den felande servern. När platsen har installerats om initieras de sekundära plats data från den överordnade primära platsen.

Under återställnings processen verifierar Configuration Manager om innehålls biblioteket finns på den sekundära plats servern. Det kontrollerar också att rätt innehåll är tillgängligt. Den sekundära platsen använder det befintliga innehålls biblioteket, om det innehåller lämpligt innehåll. Annars kan du återställa innehålls biblioteket för en sekundär plats, distribuera om eller förinstallera innehållet till servern.

Om du har en distributions plats som inte finns på den sekundära plats servern, behöver du inte installera om distributions platsen under en återställning av den sekundära platsen. När den sekundära platsen har återställts, synkroniseras den automatiskt med distributionsplatsen.

Du kan kontrol lera statusen för den sekundära plats återställningen genom att använda åtgärden **Visa installations status** från noden **platser** i Configuration Manager-konsolen.
