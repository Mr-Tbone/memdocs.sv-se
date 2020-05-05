---
title: Informationslager
titleSuffix: Configuration Manager
description: Informations lager service punkt och databas för Configuration Manager
ms.date: 05/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: abe6b05d24955959e1d08defc2c5054c4499d756
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075599"
---
#  <a name="the-data-warehouse-service-point-for-configuration-manager"></a>Informations lager service punkten för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

<!--1277922-->
Använd informations lager service platsen för att lagra och rapportera långsiktiga historiska data för din Configuration Manager-distribution.

> [!Note]  
> Configuration Manager aktiverar den här funktionen som standard i version 1910. I version 1906 eller tidigare aktiverar Configuration Manager inte den här valfria funktionen som standard. Du måste aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](install-in-console-updates.md#bkmk_options).<!--505213-->  


Informations lagret har stöd för upp till 2 TB data, med tidsstämplar för ändrings spårning. Informations lagret lagrar data genom att automatiskt synkronisera data från Configuration Manager plats databasen till informations lager databasen. Den här informationen är sedan tillgänglig från rapporterings tjänst platsen. Data som synkroniseras med data lager databasen sparas i tre år. Med jämna mellanrum tar en inbyggd uppgift bort data som är äldre än tre år.

Data som synkroniseras innehåller följande från grupperna globala data och plats data:
- Infrastruktur hälsa
- Säkerhet
- Efterlevnad
- Skadlig kod   
- Programdistributioner
- Inventerings information (men inventerings historiken är inte synkroniserad)

När plats system rollen installeras, installeras och konfigureras informations lager databasen. Det installerar också flera rapporter så att du enkelt kan söka efter och rapportera om dessa data.

Från och med version 1810 kan du synkronisera fler tabeller från plats databasen till data lagret. Med den här ändringen kan du skapa fler rapporter utifrån dina affärs behov.<!--1358870--> 



## <a name="prerequisites"></a>Krav

- Data lagrets plats system roll stöds bara på platsen på den översta nivån i hierarkin. Till exempel en central administrations plats eller en fristående primär plats.  

- Datorn där du installerar plats system rollen kräver .NET Framework 4.5.2 eller senare.  

- Bevilja **repor ting Services-plats kontot** **db_datareader** behörighet för informations lager databasen.  

- Om du vill synkronisera data med data lager databasen använder Configuration Manager dator kontot för plats system rollen. Detta konto kräver följande behörigheter:  

    - **Administratör** på den dator som är värd för informations lager databasen.  

    - **DB_Creator** behörighet för informations lager databasen.  

    - Antingen **DB_owner** eller **DB_reader** med behörigheterna **Kör** till platsen på den översta nivån i databasen.  

- Data lager databasen kräver användning av SQL Server 2012 eller senare. Versionen kan vara standard, Enterprise eller data Center. Den SQL Server versionen för data lagret behöver inte vara samma som plats databas servern.<!--SCCMDocs issue 662-->  

- Lager databasen har stöd för följande SQL Server konfigurationer:  

    - En standard-eller namngiven instans  

    - SQL Server Always on-tillgänglighetsgrupper  

    - SQL Server redundanskluster  

- Om du använder [distribuerade vyer](../../plan-design/hierarchy/database-replication.md#bkmk_distviews)måste informations lager service platsen installeras på samma server som är värd för den centrala administrations platsens databas.  

Mer information om SQL Server-licensiering finns i [vanliga frågor och svar om produkt och licensiering](../../understand/product-and-licensing-faq.md). <!-- sms500967 -->

Ändra storlek på informations lager databasen på samma sätt som plats databasen. Även om informations lagret är mindre, kommer det att växa över tid. <!--SCCMDocs issue 756-->



## <a name="install"></a>Installera

Varje hierarki har stöd för en enda instans av den här rollen, på alla plats system på platsen på den översta nivån. SQL Server som är värd för-databasen för lagret kan vara lokalt för plats system rollen, eller fjärran sluten. Informations lagret fungerar med repor ting Services-platsen som är installerad på samma plats. Du behöver inte installera de två plats system rollerna på samma server.   

Installera rollen med hjälp av **guiden Lägg till plats system roller** eller **guiden skapa plats system Server**. Mer information finns i [Installera plats system roller](../deploy/configure/install-site-system-roles.md). På sidan **urval för system roll** i guiden väljer du rollen **data lager service punkt** . 

När du installerar rollen skapar Configuration Manager informations lager databasen åt dig på den instans av SQL Server som du anger. Om du anger namnet på en befintlig databas skapas inte en ny databas i Configuration Manager. I stället används den som du anger. Den här processen är samma som när du [flyttar data lager databasen till en ny SQL Server](#move-the-database).


### <a name="configure-properties"></a>Konfigurera egenskaper

#### <a name="general-page"></a>Sidan allmänt

- **SQL Server fullständigt kvalificerat domän namn**: Ange det fullständiga domän namnet (FQDN) för den server som är värd för informations lager tjänst punktens databas.  

- **SQL Server instans namn, om tillämpligt**: om du inte använder en standard instans av SQL Server anger du den namngivna instansen.  

- **Databas namn**: Ange ett namn för data lager databasen. Configuration Manager skapar data lager databasen med det här namnet. Om du anger ett databas namn som redan finns på SQL Server-instansen använder Configuration Manager databasen.  

- **SQL Server port som används för anslutning**: Ange TCP/IP-portnumret som används av SQL Server som är värd för informations lager databasen. Tjänsten för synkronisering av data lager använder den här porten för att ansluta till data lager databasen. Som standard använder den SQL Server Port **1433** för kommunikation.  

- **Konto för informations lager service punkt**: från och med version 1802, anger du det **användar namn** som SQL Server Reporting Services använder när det ansluter till databasen för data lagret.  


#### <a name="synchronization-schedule-page"></a>Schema sidan för synkronisering
*Gäller för version 1806 och tidigare*

- **Start tid**: Ange den tid som du vill att data lagrets synkronisering ska starta.  

- **Upprepnings mönster**

    - **Varje**dag: ange att synkroniseringen körs varje dag.  

    - **Varje vecka: Ange**en dag varje vecka och veckovis upprepning för synkronisering.


#### <a name="synchronization-settings-page"></a>Sidan Inställningar för synkronisering
*Gäller för version 1810 och senare*

- **Anpassad inställning för datasynkronisering**: Välj alternativet för att **välja tabeller**. I fönstret databas tabeller väljer du de tabell namn som ska synkroniseras till databasen för data lagret. Använd filtret för att söka efter namn eller Välj den nedrullningsbara listan för att välja vissa grupper. Välj **OK** när du är klar för att spara.  

    > [!Note]  
    > Du kan inte ta bort tabeller som rollen väljer som standard.  

- **Start tid**: Ange den tid som du vill att data lagrets synkronisering ska starta.  

- **Upprepnings mönster**

    - **Varje**dag: ange att synkroniseringen körs varje dag.  

    - **Varje vecka: Ange**en dag varje vecka och veckovis upprepning för synkronisering.



## <a name="reporting"></a>Rapportering

När du har installerat en informations lager service punkt blir flera rapporter tillgängliga på platsen för repor ting Services för webbplatsen. Om du installerar data lagrets service punkt innan du installerar en repor ting Services-plats läggs rapporterna automatiskt till när du installerar repor ting Services-platsen senare.

> [!WARNING]  
> Från och med version 1802 stöder data lager platsen alternativa autentiseringsuppgifter.<!--507334--> Om du har uppgraderat från en tidigare version av Configuration Manager måste du ange autentiseringsuppgifter som SQL Server Reporting Services använder för att ansluta till informations lager databasen. Informations lager rapporter öppnas inte förrän du har lagt till autentiseringsuppgifter. 
> 
> Om du vill ange ett konto anger du **användar namnet** för kontot för informations lager service punkt i roll egenskaperna. Mer information finns i [Konfigurera egenskaper](#configure-properties). 

Data lagrets plats system roll innehåller följande rapporter under kategorin **data lager** :  

- **Program distribution – historik**: Visa information om program distribution för ett särskilt program och en specifik dator.  

- **Endpoint Protection-och program uppdateringsefterlevnad – historik**: Visa datorer som saknar program uppdateringar.  

- **Allmän maskin varu inventering – historik**: Visa all maskin varu inventering för en angiven dator.  

- **Allmän program varu inventering – historik**: Visa all program varu inventering för en angiven dator.  

- **Översikt över infrastruktur hälsa – historik**: visar en översikt över hälso tillståndet för din Configuration Manager-infrastruktur.  

- **Lista över skadlig kod upptäckt – historisk**: Visa skadlig kod som har identifierats i organisationen.  

- **Sammanfattning av program varu distribution – historik**: en sammanfattning av program varu distributionen för en speciell annons och dator.  



## <a name="site-expansion"></a>Plats expansion

Innan du kan installera en central administrations plats för att expandera en befintlig fristående primär plats måste du först avinstallera rollen för data lager service punkt. När du har installerat den centrala administrations platsen kan du installera plats system rollen på den centrala administrations platsen.  

Till skillnad från en flyttning av informations lager databasen leder den här ändringen till förlust av historiska data som du tidigare har synkroniserat på den primära platsen. Det finns inte stöd för att säkerhetskopiera databasen från den primära platsen och återställa den på den centrala administrations platsen.



## <a name="move-the-database"></a>Flytta databasen

Använd följande steg för att flytta informations lager databasen till en ny SQL Server:  

1. Använd SQL Server Management Studio för att säkerhetskopiera informations lager databasen. Återställ sedan databasen till en SQL Server på den nya datorn som är värd för data lagret.  

    > [!NOTE]  
    > När du har återställt databasen till den nya servern kontrollerar du att databas åtkomst behörigheterna är samma i den nya informations lager databasen som i den ursprungliga informations lager databasen.  

2. Använd Configuration Manager-konsolen för att ta bort rollen för data lager service punkten från den aktuella servern.  

3. Installera om informations lager tjänst platsen. Ange namnet på den nya SQL Server och instansen som är värd för den återställda informations lager databasen.  

4. När plats system rollen har installerats slutförs flyttningen.  



## <a name="troubleshooting"></a>Felsökning 

### <a name="log-files"></a>Loggfiler 

Använd följande loggar för att undersöka problem med installationen av informations lager service punkten eller synkronisering av data:

- **DWSSMSI. log** och **DWSSSetup. log**: Använd dessa loggar för att undersöka fel när du installerar informations lager service punkten.  

- **Microsoft. ConfigMgrDataWarehouse. log**: Använd den här loggen för att undersöka datasynkronisering mellan plats databasen och informations lager databasen.  


### <a name="set-up-failure"></a>Konfigurations problem 

När rollen data lager service punkt är den första som du installerar på en fjärrserver, Miss lyckas installationen för data lagret.  

#### <a name="workaround"></a>Lösning 
Kontrol lera att datorn där du installerar data lager tjänst platsen redan är värd för minst en annan roll.  


### <a name="synchronization-failed-to-populate-schema-objects"></a>Det gick inte att fylla schema objekt med synkronisering 

Det går inte att synkronisera med följande meddelande i **Microsoft. ConfigMgrDataWarehouse. log**:`failed to populate schema objects`

#### <a name="workaround"></a>Lösning 
Kontrol lera att plats system rollens dator konto är en **db_owner** på informations lager databasen.


### <a name="reports-fail-to-open"></a>Rapporter kan inte öppnas

Informations lager rapporter kan inte öppnas när informations lager databasen och rapport tjänst platsen finns på olika plats system.  

#### <a name="workaround"></a>Lösning
Bevilja **repor ting Services-plats kontot** **db_datareader** behörighet för informations lager databasen.


### <a name="error-opening-reports"></a>Fel vid öppning av rapporter

När du öppnar en data lager rapport returneras följande fel:

``` Output
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

#### <a name="workaround"></a>Lösning 
Använd följande steg för att konfigurera certifikat:

1. På den dator som är värd för informations lager databasen:  

    1. Öppna IIS, Välj **Server certifikat**och högerklicka sedan på **Skapa självsignerat certifikat**. Ange sedan det egna namnet på certifikat namnet som **informations lager SQL Server identifierings certifikat**. Välj certifikat arkivet som **personligt**.  

    2. Öppna **SQL Server Configuration Manager**. Under **SQL Server nätverks konfiguration**högerklickar du på **Egenskaper** under **protokoll för MSSQLSERVER**. Växla till fliken **certifikat** , Välj **informations lager SQL Server identifierings certifikat** som certifikat och spara sedan ändringarna.  

    3. I **Konfigurationshanteraren för SQL Server**, under **SQL Server tjänster**, startar du om **SQL Server tjänsten**. Om SQL Reporting Services också är installerat på den server som är värd för informations lager databasen kan du även starta om **repor ting service** Services.  

    4. Öppna Microsoft Management Console (MMC) och Lägg till snapin-modulen **certifikat** . Välj **dator konto** för den lokala datorn. Expandera mappen **personligt** och välj **certifikat**. Exportera **data lagret SQL Server identifierings certifikat** som en **der-kodad binär X. 509 (. CER-** fil.  

2. På den dator som är värd för SQL Server Reporting Services öppnar du MMC och lägger till snapin-modulen **certifikat** . Välj **dator konto**. Under mappen **betrodda rot certifikat utfärdare** importerar du **SQL Server identifierings certifikat för informations lagret**.  



## <a name="data-flow"></a>Dataflöde   

![Diagram som visar det logiska data flödet mellan plats komponenter för informations lagret](./media/datawarehouse.png)

#### <a name="data-storage-and-synchronization"></a>Data lagring och synkronisering

| Steg   | Information  |
|--------|----------|  
| **1**  | Plats servern överför och lagrar data i plats databasen. |  
| **2**  | Baserat på schema och konfiguration hämtar data lager service punkten data från plats databasen. |  
| **3**  | Informations lager service punkten överför och lagrar en kopia av de synkroniserade data i informations lager databasen. |  


#### <a name="reporting"></a>Rapportering

| Steg   | Information  |
|--------|----------|  
| **A**  | Med hjälp av inbyggda rapporter begär en användare data. Den här begäran skickas till repor ting service-platsen med hjälp av SQL Server Reporting Services. |  
| **T**  | De flesta rapporter är för aktuell information och dessa begär Anden körs mot plats databasen. |  
| **C**  | När en rapport begär historiska data med hjälp av en av rapporterna med en *kategori* av **informations lager**, körs begäran mot informations lager databasen. |  
