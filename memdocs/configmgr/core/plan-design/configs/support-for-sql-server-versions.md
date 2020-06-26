---
title: SQL Server-versioner som stöds
titleSuffix: Configuration Manager
description: Hämta SQL Server versions-och konfigurations krav för att vara värd för en Configuration Manager plats databas.
ms.date: 06/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b30380f4e272050b7224b52d092f39aa8ab5bad4
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383180"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>SQL Server-versioner som stöds för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Varje Configuration Manager-plats kräver en SQL Server version och konfiguration som stöds som värd för plats databasen.  

## <a name="sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> SQL Server-instanser och platser

### <a name="central-administration-site-and-primary-sites"></a>Central administrations plats och primära platser

Plats databasen måste ha en fullständig installation av SQL Server.  

SQL Server kan finnas på:  

- Plats serverdatorn.  
- En dator som är fjärran sluten till plats servern.  

Följande instanser stöds:  

- Standard-eller namngiven instans av SQL Server.  
- Konfigurationer med flera instanser.  
- Ett SQL Server kluster. Se [Använd ett SQL Server-kluster som värd för plats databasen](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
- En SQL Server AlwaysOn-tillgänglighetsgruppen. Mer information finns i [SQL Server AlwaysOn för en plats databas med hög](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)tillgänglighet.

### <a name="secondary-sites"></a>Sekundära platser

Plats databasen kan använda standard instansen av en fullständig installation av SQL Server eller SQL Server Express.  

SQL Server måste finnas på plats serverdatorn.  

### <a name="limitations-to-support"></a>Begränsningar för support

Följande konfigurationer stöds inte:

- Ett SQL Server kluster i en kluster konfiguration för Utjämning av nätverks belastning (NLB)
- Ett SQL Server-kluster på en klusterdelad volym (CSV)
- SQL Server databas speglings teknik och peer-to-peer-replikering

SQL Server transaktionell replikering stöds endast för replikering av objekt till hanterings platser som är konfigurerade att använda [databas repliker](../../servers/deploy/configure/database-replicas-for-management-points.md).  

## <a name="supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> Versioner av SQL Server som stöds

I en hierarki med flera platser kan olika platser använda olika versioner av SQL Server som värd för plats databasen. Så länge som följande objekt är sanna:

- Configuration Manager stöder de versioner av SQL Server som du använder.
- De SQL Server-versioner som du använder finns kvar i supporten av Microsoft.
- SQL Server stöder replikering mellan de två versionerna av SQL Server. Mer information finns i [SQL Server replikering bakåt](https://docs.microsoft.com/sql/relational-databases/replication/replication-backward-compatibility).

För SQL Server 2016 och tidigare, stöd för varje SQL-version och service pack följer [Microsofts livs cykel princip](https://aka.ms/sqllifecycle). Stöd för en speciell SQL Server service pack innehåller ackumulerade uppdateringar om de inte bryter mot den grundläggande service pack versionen. Från och med SQL Server 2017 frigörs inte service packs eftersom det följer en [modern underhålls modell](https://docs.microsoft.com/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server). SQL Servers teamet rekommenderar kontinuerlig, [proaktiv installation av ackumulerade uppdateringar](https://docs.microsoft.com/archive/blogs/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism) när de blir tillgängliga.

Om inget annat anges stöds följande versioner av SQL Server med alla aktiva versioner av Configuration Manager. Om stöd för en ny SQL Server-version läggs till, anges Configuration Manager-versionen som lägger till det stödet. Om stödet är inaktuellt kan du se mer information om berörda versioner av Configuration Manager.

> [!IMPORTANT]  
> När du använder SQL Server Standard för databasen på den centrala administrations platsen begränsar du det totala antalet klienter som en hierarki har stöd för. Se [Antal och gränsvärden](size-and-scale-numbers.md).

### <a name="sql-server-2019-standard-enterprise"></a>SQL Server 2019: standard, Enterprise

Från och med Configuration Manager version 1910 kan du använda den här versionen med Cumulative Update 5 (CU5) eller senare, så länge din kumulativa uppdaterings version stöds av SQL-livscykeln. CU5 är minimi kravet för SQL Server 2019 eftersom det löser ett problem med [SKALÄR UDF](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining)-inskalning.

Den här versionen av SQL kan användas för följande platser:

- En central administrations plats
- En primär plats
- En sekundär plats

<!--
#### Known issue with SQL Server 2019

There's a known issue<!--6436234 with the new [scalar UDF inlining](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining) feature in SQL 2019. To work around this issue and disable UDF lining, run the following script on the SQL 2019 server:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF  
```

While not always necessary, you may need to restart the SQL server after you run this script. For more information, see [Disabling Scalar UDF Inlining without changing the compatibility level](https://docs.microsoft.com/sql/relational-databases/user-defined-functions/scalar-udf-inlining?view=sql-server-ver15#disabling-scalar-udf-inlining-without-changing-the-compatibility-level).

You can safely disable this SQL feature for the site database server because Configuration Manager doesn't use it.

If you don't disable scalar UDF inlining in SQL 2019, the site server will randomly fail to query the site database. For example, you'll see the following errors in **hman.log**:

```hman.log
*** [HY000][0][Microsoft][SQL Server Native Client 11.0]Unspecified error occurred on SQL Server. Connection may have been terminated by the server.
*** select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
*** [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.
Failed to execute SQL command select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
```

You may see similar errors in other logs, such as **SmsAdminUI.log**.

SQL Server version 2019 logs the following error:

`Microsoft SQL Server reported SQL message 596, severity 21: [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.`

You'll also see crash dumps (`.mdump` files) from SQL in its log directory, which by default is `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log`.
-->

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: standard, Enterprise

Du kan använda den här versionen med [kumulativ uppdatering version 2](https://support.microsoft.com/help/4052574) eller högre, så länge din kumulativa uppdaterings version stöds av SQL-livscykeln. Den här versionen av SQL kan användas för följande platser:

- En central administrations plats  
- En primär plats  
- En sekundär plats  
  <!--SMS.498506-->

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: standard, Enterprise  
<!--514985-->
Du kan använda den här versionen med minst service pack och ackumulerad uppdatering som stöds av SQL-livscykeln. Den här versionen av SQL kan användas för följande platser:

- En central administrations plats  
- En primär plats  
- En sekundär plats  

### <a name="sql-server-2014-standard-enterprise"></a>SQL Server 2014: standard, Enterprise

Du kan använda den här versionen med minst service pack och ackumulerad uppdatering som stöds av SQL-livscykeln. Den här versionen av SQL kan användas för följande platser:

- En central administrations plats  
- En primär plats  
- En sekundär plats

### <a name="sql-server-2012-standard-enterprise"></a>SQL Server 2012: standard, Enterprise

Du kan använda den här versionen med minst service pack och ackumulerad uppdatering som stöds av SQL-livscykeln. Den här versionen av SQL kan användas för följande platser:

- En central administrations plats  
- En primär plats  
- En sekundär plats  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express

Du kan använda den här versionen med [kumulativ uppdatering version 2](https://support.microsoft.com/help/4052574) eller högre, så länge din kumulativa uppdaterings version stöds av SQL-livscykeln. Den här versionen av SQL kan användas för följande platser:

- En sekundär plats
<!--SMS.498506-->

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express

Du kan använda den här versionen med minst service pack och ackumulerad uppdatering som stöds av SQL-livscykeln. Den här versionen av SQL kan användas för följande platser:

- En sekundär plats

### <a name="sql-server-2014-express"></a>SQL Server 2014 Express

Du kan använda den här versionen med minst service pack och ackumulerad uppdatering som stöds av SQL-livscykeln. Den här versionen av SQL kan användas för följande platser:

- En sekundär plats  

### <a name="sql-server-2012-express"></a>SQL Server 2012 Express

Du kan använda den här versionen med minst service pack och ackumulerad uppdatering som stöds av SQL-livscykeln. Den här versionen av SQL kan användas för följande platser:

- En sekundär plats  

## <a name="required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> Konfigurationer som krävs för SQL Server

Följande konfigurationer krävs av alla installationer av SQL Server som du använder för en plats databas, inklusive SQL Server Express. När Configuration Manager installerar SQL Server Express som en del av installationen av en sekundär plats skapas dessa konfigurationer automatiskt.  

### <a name="sql-server-architecture-version"></a>SQL Server arkitektur version

Configuration Manager kräver en 64-bitars version av SQL Server som värd för plats databasen.  

### <a name="database-collation"></a>Databas sortering

På varje plats måste både den instans av SQL Server som används för platsen och plats databasen använda följande sortering: **SQL_Latin1_General_CP1_CI_AS**.  

Configuration Manager stöder två undantag till den här sorteringen för Kina GB18030 standard. Mer information finns i [internationell support](../hierarchy/international-support.md).  

### <a name="database-compatibility-level"></a>Kompatibilitetsnivå för databas

Configuration Manager kräver att plats databasens kompatibilitetsnivå är mindre än den lägsta SQL Server versionen som stöds för din Configuration Manager version. Till exempel, från och med version 1702, måste du ha en kompatibilitetsnivå för [databas](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) som är större än eller lika med 110. <!-- SMS.506266-->

### <a name="sql-server-features"></a>SQL Server funktioner

Endast funktionen **Database Engine Services** krävs för varje platsserver.  

Configuration Manager databasreplikering kräver inte funktionen **SQL Server replikering** . Detta SQL Server konfiguration krävs dock när du använder [databas repliker för hanterings platser](../../servers/deploy/configure/database-replicas-for-management-points.md).  

### <a name="windows-authentication"></a>Windows-autentisering

Configuration Manager kräver **Windows-autentisering** för att verifiera anslutningar till databasen.  

### <a name="sql-server-instance"></a>SQL Server instans

Använd en dedikerad instans av SQL Server för varje plats. Instansen kan vara en **namngiven instans** eller **standard instansen**.  

### <a name="sql-server-memory"></a>SQL Server minne

Reservera minne för SQL Server med SQL Server Management Studio. Ange minimi inställningen för **Server minne** under **alternativ för server minne**. Mer information om hur du konfigurerar den här inställningen finns [SQL Server konfigurations alternativ för minnes Server](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options).  

- **För en databas server som du installerar på samma dator som plats servern**: begränsa minnet för SQL Server till 50 till 80 procent av det tillgängliga, adresser bara system minnet.  

- **För en dedikerad databas server som är fjärran sluten till plats servern**: begränsa minnet för SQL Server till 80 till 90 procent av det tillgängliga, adresser bara system minnet.  

- **För en minnes reserv för bufferten för varje SQL Server instans som används**:  

  - För en central administrations plats: ange minst 8 GB.  
  - För en primär plats: ange minst 8 GB.  
  - För en sekundär plats: ange minst 4 GB.  

### <a name="sql-nested-triggers"></a>SQL-kapslade utlösare

Kapslade SQL-utlösare måste vara aktiverat. Mer information finns i [Konfigurera Server konfigurations alternativet kapslade utlösare](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option)

### <a name="sql-server-clr-integration"></a>CLR-integrering i SQL Server

Platsdatabasen kräver att CLR (Common Language Runtime) är aktiverat i SQL Server. Det här alternativet aktive ras automatiskt när Configuration Manager installeras. Mer information om CLR finns i [Introduktion till SQL Server CLR-integrering](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).  

### <a name="sql-server-service-broker-ssb"></a>SQL Server Service Broker (SSB)

SQL Server Service Broker krävs både för replikering mellan platser och för en enda primär plats.

### <a name="trustworthy-setting"></a>BETRODD inställning

Configuration Manager aktiverar automatiskt SQL- [betrodd databas egenskap](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property). Den här egenskapen krävs för att Configuration Manager ska vara **på**.

## <a name="optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> Valfria konfigurationer för SQL Server

Följande konfigurationer är valfria för varje databas som använder en fullständig SQL Server-installation.  

### <a name="sql-server-service"></a>SQL Server tjänst

Du kan konfigurera SQL Server-tjänsten att köras med:  

- Ett *användar konto med låg rättighets domän* :  

  - Den här konfigurationen är en bästa praxis och du kan behöva registrera tjänstens huvud namn (SPN) manuellt för kontot.  

- Det **lokala system** kontot för datorn som kör SQL Server:  

  - Använd det lokala systemkontot för att förenkla konfigurationsprocessen.  
  - När du använder kontot Lokalt system registrerar Configuration Manager automatiskt SPN för tjänsten SQL Server.  
  - Att använda det lokala system kontot för tjänsten SQL Server är inte ett SQL Server bästa praxis.  

När datorn som kör SQL Server inte använder det lokala system kontot för att köra SQL Server-tjänsten konfigurerar du tjänstens huvud namn för det konto som kör SQL Servers tjänsten i Active Directory Domain Services. (När system kontot används registreras SPN automatiskt åt dig.)

Information om SPN för plats databasen finns i [Hantera SPN för plats databas servern](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN).  

Information om hur du ändrar det konto som används av SQL Server-tjänsten finns i [SCM-tjänster-ändra tjänstens start konto](https://docs.microsoft.com/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services krävs för att installera en repor ting Services-plats där du kan köra rapporter. Configuration Manager stöder samma versioner av SQL Server för rapportering som för plats databasen.

Mer information finns i [krav för rapportering i Configuration Manager](../../servers/manage/prerequisites-for-reporting.md).

> [!IMPORTANT]  
> När du har uppgraderat SQL Server från en tidigare version kan du se följande fel: *Report Builder finns inte*.  
> För att lösa det här felet måste du installera om repor ting Services-platsens plats system roll.  

### <a name="data-warehouse-service-point"></a>Informations lager service punkt

Data lagret använder en separat databas. Du kan vara värd för den på plats databas servern eller en separat SQL Server. Mer information finns i [informations lager service punkten för Configuration Manager](../../servers/manage/data-warehouse.md).

### <a name="sql-server-ports"></a>SQL Server portar

För kommunikation till SQL Server databas motor och för replikering mellan platser kan du använda standardvärdena för SQL Server-port eller ange anpassade portar:  

- **Kommunikation mellan platser** använder SQL Server Service Broker, som använder TCP-port 4022 som standard.  
- **Kommunikation mellan platser** mellan SQL Server databas motor och olika Configuration Manager plats system roller använder TCP 1433 som standard port. Följande platssystemsroller kommunicerar direkt med SQL Server-databasen:  

  - Hanteringsplats  
  - SMS-providerdator  
  - Rapporteringstjänstpunkt  
  - Platsserver  

När en dator som kör SQL Server är värd för en databas från mer än en plats måste varje databas använda en separat instans av SQL Server. Dessutom måste varje instans konfigureras för att använda en unik uppsättning portar.  

> [!WARNING]  
> Configuration Manager stöder inte dynamiska portar. Eftersom namngivna SQL Server-instanser normalt använder dynamiska portar för anslutningar till databasmotorn, måste du när du använder en namngiven instans manuellt konfigurera den statiska port som du vill använda för kommunikation mellan platser.  

Om du har en brand vägg aktive rad på den dator som kör SQL Server, kontrollerar du att den har kon figurer ATS för att tillåta portarna som används av distributionen och på alla platser i nätverket mellan datorer som kommunicerar med SQL Server.  

Ett exempel på hur du konfigurerar SQL Server att använda en speciell port finns i [Konfigurera en server för att lyssna på en angiven TCP-port](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  

## <a name="upgrade-options-for-sql-server"></a>Uppgraderings alternativ för SQL Server

Om du behöver uppgradera din version av SQL Server kan du använda någon av följande metoder, från enkel till mer komplex:  

- [Uppgradera SQL Server på plats](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server) (rekommenderas)  

- Installera en ny version av SQL Server på en ny dator och Använd sedan [alternativet för databas flyttning](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) i Configuration Manager installations programmet för att peka plats servern mot den nya SQL Server  

- Använd [säkerhets kopiering och återställning](../../servers/manage/backup-and-recovery.md). Det finns stöd för att använda säkerhets kopiering och återställning för ett SQL-uppgraderings scenario. Du kan ignorera kraven för SQL-versioner när du går igenom [överväganden innan du återställer en plats](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site).
