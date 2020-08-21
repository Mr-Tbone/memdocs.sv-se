---
title: Ständig aktivering av SQL Server
titleSuffix: Configuration Manager
description: Planera att använda en SQL Server Always on-tillgänglighets grupp med Configuration Manager
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9cf8e74793213e47dd503de1fdf1284bdc7d6a9
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699236"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Förbered för användning SQL Server Always on-tillgänglighetsgrupper med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd den här artikeln för att förbereda Configuration Manager för att använda SQL Server Always on-tillgänglighetsgrupper. Den här funktionen ger en lösning för hög tillgänglighet och katastrof återställning för plats databasen.  

Configuration Manager stöder användning av tillgänglighets grupper:

- På primära platser och den centrala administrations platsen.
- Lokalt eller i Microsoft Azure.

När du använder tillgänglighets grupper i Microsoft Azure kan du öka tillgängligheten för plats databasen med hjälp av *Azures tillgänglighets uppsättningar*. Mer information om Azure tillgänglighetsuppsättningar finns i [Hantera tillgängligheten för virtuella datorer](/azure/virtual-machines/windows/manage-availability).

> [!Important]
> Innan du fortsätter bör du vara bekant med att konfigurera SQL Server och SQL Server tillgänglighets grupper. Informationen som följer hänvisar till SQL Server dokumentations bibliotek och procedurer.


## <a name="supported-scenarios"></a>Scenarier som stöds

Följande scenarier stöds för att använda tillgänglighets grupper med Configuration Manager. Mer information och procedurer för varje scenario finns i [Konfigurera tillgänglighets grupper för Configuration Manager](configure-aoag.md).

- [Skapa en tillgänglighets grupp för användning med Configuration Manager](configure-aoag.md#bkmk_create)  
- [Konfigurera en plats att använda tillgänglighets gruppen](configure-aoag.md#bkmk_configure)  
- [Lägga till eller ta bort synkrona replik medlemmar från en tillgänglighets grupp som är värd för en plats databas](configure-aoag.md#bkmk_sync)  
- [Konfigurera eller återställa en plats från en asynkron inchecknings repliker](configure-aoag.md#bkmk_async)  
- [Flytta en plats databas från en tillgänglighets grupp till en standard-eller namngiven instans av en fristående SQL Server](configure-aoag.md#bkmk_stop)  


## <a name="prerequisites"></a>Förutsättningar

Följande krav gäller för alla scenarier. Om det finns ytterligare krav som gäller för ett speciellt scenario, är de detaljerade med det scenariot.

### <a name="configuration-manager-accounts-and-permissions"></a>Configuration Manager konton och behörigheter

#### <a name="installation-account"></a>Installations konto

Det konto som du använder för att köra Configuration Manager-installationen måste vara:

- En medlem i den lokala gruppen **Administratörer** på varje dator som är medlem i tillgänglighets gruppen.
- En **sysadmin** på varje instans av SQL Server som är värd för plats databasen.

#### <a name="site-server-to-replica-member-access"></a>Åtkomst till plats Server till replik medlem

Plats serverns dator konto måste vara medlem i den lokala gruppen **Administratörer** på varje dator som är medlem i tillgänglighets gruppen.

### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>Version

Varje replik i tillgänglighets gruppen måste köra en version av SQL Server som stöds av din version av Configuration Manager. När det stöds av SQL Server kan olika noder i en tillgänglighets grupp köra olika versioner av SQL Server. Mer information finns i [SQL Server-versioner som stöds för Configuration Manager](../../../plan-design/configs/support-for-sql-server-versions.md).<!--SCCMDocs issue 656-->

#### <a name="edition"></a>Utgåva

Använd en *Enterprise* -version av SQL Server.

#### <a name="account"></a>Konto

Varje instans av SQL Server kan köras under ett domän användar konto (**tjänst konto**) eller ett konto som inte är ett domän konto. Varje replik i en grupp kan ha en annan konfiguration.

- Använd ett konto med lägsta möjliga behörighet. Mer information finns i [säkerhets överväganden för en SQL Server-installation](/sql/sql-server/install/security-considerations-for-a-sql-server-installation).  

- Mer information om hur du konfigurerar tjänst konton och behörigheter för SQL Server finns i [Konfigurera Windows tjänst konton och behörigheter](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).  

- Om du vill använda ett konto som inte är ett domän konto måste du använda certifikat. Mer information finns i [använda certifikat för en databas speglings slut punkt (Transact-SQL)](/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).  

- Mer information finns i [skapa en slut punkt för databas spegling för Always on Availability groups](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).  


### <a name="database"></a>Databas

#### <a name="configure-the-database-on-a-new-replica"></a>Konfigurera databasen på en ny replik

Konfigurera databasen för varje replik med följande inställningar:  

- Aktivera **CLR-integrering**:

    ``` SQL
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO
    ```

    Mer information finns i [CLR-integrering](/sql/relational-databases/clr-integration/clr-integration-enabling).  

- Ange **Max storleken för text repl** till `2147483647` :  

    ``` SQL
    EXECUTE sp_configure 'max text repl size (B)', 2147483647
    ```

- Ange databas ägaren till sa- *kontot*. Du behöver inte aktivera det här kontot.

- Aktivera **den** **betrodda** inställningen:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET TRUSTWORTHY ON;
    ```

    Mer information finns i [egenskapen betrodd databas](/sql/relational-databases/security/trustworthy-database-property).

- Aktivera **Service Broker**:  

    ``` SQL
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER
    ```

    > [!Note]  
    > Du kan inte aktivera alternativet Service Broker på en databas som redan tillhör en tillgänglighets grupp. Du måste aktivera det alternativet innan du lägger till det i tillgänglighets gruppen.<!-- SCCMDocs#1432 -->

- Konfigurera Service Broker prioritet:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET HONOR_BROKER_PRIORITY ON;
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER WITH ROLLBACK IMMEDIATE

    ```

Gör bara dessa konfigurationer på en primär replik. Om du vill konfigurera en sekundär replik måste du först redundansväxla den primära till den sekundära. Den här åtgärden gör den sekundära den nya primära repliken.

#### <a name="database-verification-script"></a>Skript för databas verifiering

Kör följande SQL-skript för att kontrol lera databas konfigurationerna för både primära och sekundära repliker. Innan du kan åtgärda ett problem på en sekundär replik bör du ändra att den sekundära repliken är den primära repliken.

``` SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targeting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```


### <a name="availability-group-configurations"></a>Konfigurationer för tillgänglighets grupp

#### <a name="replica-members"></a>Replik medlemmar

- Tillgänglighets gruppen måste ha en primär replik.  

- Använd samma antal och typ av repliker i en tillgänglighets grupp som din version av SQL Server stöder.

- Du kan använda en asynkron commit-replik för att återställa din synkrona replik. Mer information finns i [återställnings alternativ för plats databas](../../manage/recover-sites.md#site-database-recovery-options).  

    > [!Warning]  
    > Configuration Manager stöder inte *redundans* för att använda den asynkrona commit-repliken som plats databas. Mer information finns i [lägen för redundans och redundans (alltid på tillgänglighets grupper)](/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups).  

Configuration Manager validerar inte statusen för den asynkrona commit-repliken för att bekräfta att den är aktuell. Användning av en asynkron commit-replik som plats databasen kan skydda din webbplats och data på risk. Den här repliken kan vara osynkroniserade genom design. Mer information finns i [Översikt över SQL Server Always on-tillgänglighetsgrupper](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Varje replik medlem måste ha följande konfiguration:

- Använd *standard instansen* eller en *namngiven instans*  

- Inställningen **anslutningar i primär roll** är **Tillåt alla anslutningar**  

- Den **läsbara sekundära** inställningen är **Ja**  

- Aktive rad för **manuell redundans**

    > [!Note]
    > I version 1902 och tidigare måste du konfigurera alla tillgänglighets grupper på SQL Server för manuell redundansväxling. Den här konfigurationen krävs även om den inte är värd för plats databasen.
    >
    > Från och med version 1906 stöder Configuration Manager användningen av synkrona repliker för tillgänglighets gruppen när den är inställd på **Automatisk redundans**. Ange **manuell redundans** när:
    >
    > - Du kör Configuration Manager-installationen för att ange användning av plats databasen i tillgänglighets gruppen.  
    > - Du installerar en uppdatering för Configuration Manager. (Inte bara uppdateringar som gäller plats databasen).  

- Alla medlemmar behöver samma [seeding-läge](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas).<!-- SCCMDocs-pr#3899 --> Configuration Manager-installationen innehåller en krav kontroll för att verifiera konfigurationen när du skapar en databas via installation eller återställning.

    > [!Note]  
    > När installations programmet skapar-databasen och du konfigurerar **Automatisk** initiering måste tillgänglighets gruppen ha behörighet att skapa databasen. Detta krav gäller både för en ny databas eller återställning. Mer information finns i [automatisk dirigering för sekundär replik](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas#security).<!-- SCCMDocs-pr#3900 -->

#### <a name="replica-member-location"></a>Replik medlems plats

Antingen vara värd för alla repliker i en tillgänglighets grupp lokalt eller var värd för dem på Microsoft Azure. En grupp som innehåller en lokal medlem och en medlem i Azure stöds inte.

> [!NOTE]
> Om du använder en virtuell Azure-dator för SQL Server aktiverar du **flytande IP**. Mer information finns i [Konfigurera en belastningsutjämnare för en SQL Server Always on-tillgänglighetsgrupper på virtuella Azure-datorer](/azure/azure-sql/virtual-machines/windows/availability-group-load-balancer-portal-configure).<!-- SCCMDocs#1928 -->

Configuration Manager installationen måste ansluta till varje replik. När du konfigurerar en tillgänglighets grupp i Azure och gruppen ligger bakom en intern eller extern belastningsutjämnare, öppnar du följande standard portar:

- RPC-slutpunktsmappare: **TCP 135**

- SQL Server Service Broker: **TCP 4022**  

- SQL över TCP: **TCP 1433**

När installationen är klar måste dessa portar vara öppna för Configuration Manager och Replikeringslänkanalys.<!-- MEMDocs#375 -->

Du kan använda anpassade portar för dessa konfigurationer. Använd samma anpassade portar av slut punkten och alla repliker i tillgänglighets gruppen.

Skapa en belastnings Utjämnings regel för varje port i Azure Load Balancer för SQL för att replikera data mellan platser. Mer information finns i [Konfigurera portar med hög tillgänglighet för en intern belastningsutjämnare](/azure/load-balancer/load-balancer-configure-ha-ports).<!-- MEMDocs#252 -->

#### <a name="listener"></a>Lyssnare

Tillgänglighetsgruppen måste ha minst en *lyssnare i tillgänglighetsgruppen*. När du konfigurerar Configuration Manager att använda plats databasen i tillgänglighets gruppen, använder den den här lyssnaren virtuella namn. Även om en tillgänglighets grupp kan innehålla flera lyssnare kan Configuration Manager bara använda en. Mer information finns i [skapa eller konfigurera en lyssnare för en SQL Server tillgänglighets grupp](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### <a name="file-paths"></a>Fil Sök vägar

När du kör Configuration Manager installations programmet för att konfigurera en plats för att använda databasen i en tillgänglighets grupp måste varje sekundär replik Server ha en SQL Server fil Sök väg som är identisk med fil Sök vägen för plats databasens filer på den aktuella primära repliken. Om det inte finns någon identisk sökväg, kan inte installations programmet lägga till instansen för tillgänglighets gruppen som den nya platsen för plats databasen.  

Det lokala SQL Server tjänst kontot måste ha behörigheten **fullständig** behörighet för den här mappen.

De sekundära replik servrarna kräver bara denna fil Sök väg när du använder Configuration Manager-installationen för att ange databas instansen i tillgänglighets gruppen. När du har slutfört konfigurationen av plats databasen i tillgänglighets gruppen kan du ta bort den oanvända sökvägen från de sekundära replik servrarna.

Betrakta till exempel följande scenario:

- Du skapar en tillgänglighets grupp som använder tre SQL-servrar.  

- Din primära replikserver är en ny installation av SQL Server 2014. Som standard lagras databasen i databasen. MDF och. LDF-filer i `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA` .  

- Du har uppgraderat båda de sekundära replik servrarna till SQL Server 2014 från tidigare versioner. Med uppgraderingen behåller de här servrarna den ursprungliga fil Sök vägen för att lagra databasfiler: `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA` .  

- Innan du flyttar plats databasen till den här tillgänglighets gruppen skapar du följande fil Sök väg på varje sekundär replik Server: `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA` . Den här sökvägen är en dubblett av sökvägen som används på den primära repliken, även om de sekundära replikerna inte använder den här fil platsen.  

- Sedan beviljar du SQL Server tjänst kontot på varje sekundär replik fullständig behörighet till den nyligen skapade fil platsen på den servern.  

- Nu kan du köra Configuration Manager installations programmet för att konfigurera platsen att använda plats databasen i tillgänglighets gruppen.  

#### <a name="multi-subnet-failover"></a>Redundans för flera undernät

<!-- SCCMDocs-pr#3734 -->
Från och med version 1906 kan du aktivera [nyckelordet MultiSubnetFailover-anslutningssträng](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) i SQL Server. Du måste också lägga till följande värden manuellt i Windows-registret på plats servern:

``` Registry
HKLM:\SOFTWARE\Microsoft\SMS\Identification
HKLM:\SOFTWARE\Microsoft\SMS\SQL Server

MSF Enabled : 1 (DWORD)
```

> [!Warning]  
> Användning av [plats Server hög tillgänglighet](site-server-high-availability.md) och SQL Server Always on med redundans för flera undernät ger inte alla funktioner för automatisk redundans för haveri beredskap.

Om du behöver skapa en tillgänglighets grupp med en medlem på en fjärran sluten plats, prioriterar du baserat på den lägsta nätverks fördröjningen. Hög nätverks fördröjning kan orsaka replikeringsfel.<!-- SCCMDocs#1381 -->


## <a name="limitations-and-known-issues"></a>Begränsningar och kända problem

Följande begränsningar gäller för alla scenarier.

### <a name="unsupported-sql-server-options-and-configurations"></a>SQL Server alternativ och konfigurationer som inte stöds

- **Grundläggande tillgänglighets grupper**: introducerades med SQL Server 2016 Standard Edition, så stöder inte grundläggande tillgänglighets grupper Läs åtkomst till sekundära repliker. Konfigurationen kräver den här åtkomsten. Mer information finns i [grundläggande SQL Server tillgänglighets grupper](/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017).  

- **Kluster instans för växling vid fel**: det finns inte stöd för kluster instanser för replikering som du använder med Configuration Manager. Mer information finns i [SQL Server Always on Cluster instances](/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).  

- **MultiSubnetFailover**: i version 1902 och tidigare finns det inte stöd för att använda en tillgänglighets grupp med Configuration Manager i en konfiguration för flera undernät. Du kan inte heller använda anslutnings strängen [MutliSubnetFailover](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) för nyckelord.

    Om du vill ha stöd för den här konfigurationen uppdaterar du Configuration Manager till version 1906 eller senare. Mer information finns i krav för [redundans för flera undernät](sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover) .

### <a name="sql-servers-that-host-additional-availability-groups"></a>SQL-servrar som är värdar för ytterligare tillgänglighets grupper

<!--SCCMDocs issue 649-->
När SQL Server är värd för en eller flera tillgänglighets grupper förutom den grupp du använder för Configuration Manager, behöver den vissa inställningar vid den tidpunkt då du kör Configuration Manager installationen. De här inställningarna krävs också för att installera en uppdatering för Configuration Manager. Varje replik i varje tillgänglighets grupp måste ha följande konfigurationer:

- Manuell redundans  
- Tillåt alla skrivskyddade anslutningar  

> [!Note]
> I version 1902 och tidigare måste du konfigurera alla tillgänglighets grupper på SQL Server för manuell redundansväxling. Den här konfigurationen krävs även om den inte är värd för plats databasen.
>
> Från och med version 1906 stöder Configuration Manager användningen av synkrona repliker för tillgänglighets gruppen när den är inställd på **Automatisk redundans**. Ange **manuell redundans** när:
>
> - Du kör Configuration Manager-installationen för att ange användning av plats databasen i tillgänglighets gruppen.  
> - Du installerar en uppdatering för Configuration Manager. (Inte bara uppdateringar som gäller plats databasen).  

### <a name="unsupported-database-use"></a>Databas användning som inte stöds

#### <a name="configuration-manager-supports-only-the-site-database-in-an-availability-group"></a>Configuration Manager stöder endast plats databasen i en tillgänglighets grupp

Följande databaser stöds inte av Configuration Manager i en SQL Server Always on-tillgänglighets grupp:  

- Rapportdatabas  
- WSUS-databas  

#### <a name="pre-existing-database"></a>Redan befintlig databas

Du kan inte använda en ny databas som skapats på repliken. När du konfigurerar en tillgänglighets grupp återställer du en kopia av en befintlig Configuration Manager databas till den primära repliken.  

#### <a name="distributed-views"></a>Distribuerade vyer

<!-- SCCMDocs-pr#3792 -->
Om du är värd för plats databasen på en SQL Server Always on-tillgänglighetsgrupper i version 1902 och tidigare kan du inte aktivera [distribuerade vyer](../../../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) för databasreplikering. För att stödja den här konfigurationen uppdaterar du till version 1906 eller senare.


### <a name="setup-errors-in-configmgrsetuplog"></a>Installations fel i ConfigMgrSetup. log

När du kör Configuration Manager-installationen för att flytta en plats databas till en tillgänglighets grupp försöker den bearbeta databas roller på de sekundära replikerna i tillgänglighets gruppen. Filen **ConfigMgrSetup. log** visar följande fel:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

Dessa fel är säkra att ignorera.

### <a name="site-expansion"></a>Plats expansion

<!--SCCMDocs issue 568-->
Om du konfigurerar plats databasen för en fristående primär plats att använda SQL Always on kan du inte expandera platsen för att inkludera en central administrations plats. Om du försöker utföra den här processen Miss lyckas det. Om du vill expandera platsen tar du tillfälligt bort den primära platsens databas från tillgänglighets gruppen.

Du behöver inte göra några ändringar i konfigurationen när du lägger till en sekundär plats.


## <a name="changes-for-site-backup"></a>Ändringar för säkerhets kopiering av plats

### <a name="backup-database-files"></a>Säkerhetskopiera databasfiler
  
När en plats databas använder en tillgänglighets grupp kör du den inbyggda underhålls uppgiften **plats Server för säkerhets kopiering** för att säkerhetskopiera vanliga Configuration Manager inställningar och filer. Använd inte. MDF eller. LDF-filer som skapats av säkerhets kopian. Gör i stället direkta säkerhets kopior av dessa databasfiler med hjälp av SQL Server.

### <a name="transaction-log"></a>Transaktions logg  

Ange att plats databasens återställnings modell är **fullständig**. Den här konfigurationen är ett krav för Configuration Manager används i en tillgänglighets grupp. Planera för att övervaka och underhålla storleken på transaktions loggen för plats databasen. I den fullständiga återställnings modellen är transaktionerna inte skärpta förrän den gör en fullständig säkerhets kopia av databasen eller transaktions loggen. Mer information finns i [säkerhetskopiera och återställa SQL Server-databaser](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).


## <a name="changes-for-site-recovery"></a>Ändringar för webbplats återställning

Om minst en nod i tillgänglighets gruppen fortfarande fungerar använder du alternativet plats återställning för att **hoppa över databas återställning (Använd det här alternativet om plats databasen inte påverkades)**.

Från och med version 1906 kan Site Recovery återskapa databasen på en SQL Always-grupp. Den här processen fungerar med både manuell och automatisk dirigering.<!-- SCCMDocs-pr#3846 -->

I version 1902 eller tidigare, när du förlorar alla noder i en tillgänglighets grupp, måste du först återskapa tillgänglighets gruppen innan du kan återställa platsen. Configuration Manager kan inte återskapa eller återställa noden tillgänglighet. Återskapa gruppen, Återställ säkerhets kopian och konfigurera om SQL. Använd sedan alternativet plats återställning för att **hoppa över databas återställning (Använd det här alternativet om plats databasen inte påverkades)**.

Mer information finns i [säkerhets kopiering och återställning](../../manage/backup-and-recovery.md).


## <a name="changes-for-reporting"></a>Ändringar för rapportering

### <a name="install-the-reporting-service-point"></a>Installera repor ting service-platsen

Repor ting Services-platsen stöder inte användning av det virtuella namnet för lyssnaren i tillgänglighets gruppen. Den har inte heller stöd för att vara värd för databasen i en SQL Server Always on-tillgänglighetsgrupper.  

- Som standard anger installationen av repor ting Services- **platsen plats databas serverns namn** till det virtuella namn som har angetts som lyssnare. Ändra den här inställningen om du vill ange ett dator namn och en instans av en replik i tillgänglighets gruppen.  

- Om du vill avlasta rapporteringen och öka tillgängligheten när en replikerad nod är offline, bör du överväga att installera ytterligare repor ting Services-platser på varje replik Konfigurera sedan varje repor ting Services-plats så att det använder ett eget dator namn. När du installerar en rapporterings tjänst punkt på varje replik i tillgänglighets gruppen kan rapportering alltid ansluta till en aktiv rapporterings plats Server.  

### <a name="switch-the-reporting-services-point-used-by-the-console"></a>Växla den repor ting Services-plats som används av-konsolen

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **rapportering**och väljer noden **rapporter** .

1. I menyfliksområdet väljer du **rapport alternativ**.  

1. I dialog rutan rapport alternativ väljer du den repor ting Services-plats som du vill använda.  


## <a name="next-steps"></a>Nästa steg

I den här artikeln beskrivs krav, begränsningar och ändringar av vanliga uppgifter som Configuration Manager kräver när du använder tillgänglighets grupper. Procedurer för att konfigurera och konfigurera din webbplats att använda tillgänglighets grupper finns i [Konfigurera tillgänglighets grupper](configure-aoag.md).