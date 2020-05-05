---
title: Säkerhets kopierings platser
titleSuffix: Configuration Manager
description: Lär dig hur du säkerhetskopierar dina platser före händelse av avbrott eller data förlust i Configuration Manager.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 824eaeb939249e1bcc2ed21d5815a0a72dc54797
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717869"
---
# <a name="back-up-a-configuration-manager-site"></a>Säkerhetskopiera en Configuration Manager-plats

*Gäller för: Configuration Manager (aktuell gren)*

Förbered säkerhets kopierings-och återställnings metoder för att undvika data förlust. För Configuration Manager-platser kan en säkerhets kopierings-och återställnings metod hjälpa dig att återställa platser och hierarkier snabbare, och med minsta möjliga data förlust.  

Avsnitten i den här artikeln kan hjälpa dig att säkerhetskopiera dina webbplatser. Information om hur du återställer en plats finns i [återställningen av Configuration Manager](recover-sites.md).  

<!--/SCCMdocs/issues/2108-->
>[!WARNING]
> De två säkerhets kopierings metoder som stöds för Configuration Manager Site Recovery är:
>
> - En lyckad säkerhets kopiering från underhålls uppgiften **plats Server för säkerhets kopiering**
> - En manuellt återställd säkerhets kopia av plats databasen


## <a name="considerations-before-creating-a-backup"></a>Att tänka på innan du skapar en säkerhets kopia  

-   Om du använder en SQL Server Always on-tillgänglighetsgrupper som värd för plats databasen: ändra säkerhets kopierings-och återställnings planerna enligt beskrivningen i [förbereda för att använda SQL Server Always on](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup).  

-   Configuration Manager kan återställa plats databasen från aktiviteten Configuration Manager säkerhets kopiering. Den kan också använda en säkerhets kopia av plats databasen som du skapar med en annan process.   

     Du kan till exempel återställa plats databasen från en säkerhets kopia som skapats som en del av en Microsoft SQL Server underhålls plan. Du kan också använda en säkerhets kopia som skapats med hjälp av Data Protection Manager för att säkerhetskopiera plats databasen.  

-   Från och med version 1806 installerar du ytterligare en plats server i *passivt* läge. Plats servern i passivt läge är utöver den befintliga plats servern i *aktivt* läge. En plats server i passivt läge är tillgänglig för omedelbar användning vid behov. Mer information finns i [hög tillgänglighet för plats Server](../deploy/configure/site-server-high-availability.md). Även om den här rollen inte tar bort behovet av att planera för och öva på säkerhets kopierings-och återställnings åtgärder, minskar det avsevärt arbetet för att återställa en plats vid behov.  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Säkerhetskopiera platsdatabasen med Data Protection Manager
Du kan använda System Center-Data Protection Manager (DPM) för att säkerhetskopiera Configuration Manager-platsdatabasen.

Skapa en ny skydds grupp i DPM för plats databasens dator. På sidan **Välj grupp medlemmar** i fönstret Skapa guiden Ny skyddsgrupp väljer du tjänsten SMS Writer från listan data källa. Välj sedan plats databasen som en lämplig medlem. Mer information om hur du använder DPM finns i dokumentations biblioteket för [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) .  

> [!IMPORTANT]  
>  Configuration Manager har inte stöd för DPM-säkerhetskopiering för ett SQL Server-kluster som använder en namngiven instans. Det stöder DPM-säkerhetskopiering på ett SQL Server kluster som använder standard instansen av SQL Server.  

När du har återställt plats databasen följer du stegen i installations programmet för att återställa platsen. Om du vill använda plats databasen som du säkerhetskopierade med Data Protection Manager väljer du återställnings alternativet för att **använda en plats databas som har återställts manuellt**.  



## <a name="backup-maintenance-task"></a>Säkerhetskopiera underhållsåtgärder
Du kan automatisera säkerhets kopieringen för Configuration Manager platser genom att schemalägga den fördefinierade underhålls uppgiften plats Server för säkerhets kopiering. Den här uppgiften har följande funktioner:

-   Körs enligt ett schema
-   Säkerhetskopierar platsdatabasen
-   Säkerhetskopierar särskilda registernycklar
-   Säkerhetskopierar vissa mappar och filer
-   Säkerhetskopierar [CD: n. Senaste mappen](the-cd.latest-folder.md)   

Planera att köra standard aktiviteten för säkerhets kopiering av plats minst var femte dag. Det här schemat beror på att Configuration Manager använder en *SQL Server kvarhållningsperiod för ändrings spårning* på fem dagar. Mer information finns i [SQL Server kvarhållningsperiod för ändrings spårning](recover-sites.md#sql-server-change-tracking-retention-period).

För att förenkla säkerhets kopierings processen kan du skapa en **AfterBackup. bat** -fil. Det här skriptet kör automatiskt åtgärder efter säkerhets kopiering när säkerhets kopierings åtgärden har slutförts. Använd filen AfterBackup. bat för att arkivera ögonblicks bilden av säkerhets kopian på en säker plats. Du kan också använda filen AfterBackup. bat för att kopiera filer till säkerhetskopieringsmappen eller starta andra säkerhets kopierings aktiviteter.  

Du kan säkerhetskopiera en central administrations plats och en primär plats. Sekundära platser eller plats system servrar har inte säkerhets kopierings aktiviteter.

När Configuration Manager säkerhets kopierings tjänsten körs följer den instruktionerna som definierats i säkerhets kopierings kontroll `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl`filen:. Du kan redigera säkerhetskopieringskontrollfilen och därmed ändra säkerhetskopieringstjänstens beteende.  
> [!NOTE]
> Ändringar av **Smsbkup. CTL** kommer att gälla efter att tjänsten SMS_SITE_VSS_WRITER på plats servern har startats om.

Statusinformation för platssäkerhetskopieringen skrivs till filen **Smsbkup.log** . Den här filen skapas i målmappen som du anger i egenskaperna för underhålls åtgärden plats Server för säkerhets kopiering.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Aktivera underhållsåtgärden för platssäkerhetskopiering  
1.  Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2.  Välj den plats som du vill aktivera underhålls åtgärden för säkerhets kopiering av plats för.  

3.  Klicka på **plats underhålls aktiviteter** i menyfliksområdet.  

4.  Välj aktiviteten **säkerhetskopiera plats Server** och klicka på **Redigera**.  

5.  Välj alternativet för att **Aktivera den här uppgiften**. Klicka på **Ange sökvägar** för att ange mål för säkerhets kopieringen. Du har följande alternativ:  

    > [!IMPORTANT]  
    >  Förhindra ändring av säkerhetskopian genom att lagra filerna på en säker plats. Den mest säkra sökvägen till säkerhets kopiering är till en lokal enhet, så du kan ange NTFS-filbehörighet för mappen. Configuration Manager krypterar inte de säkerhets kopierings data som lagras i sökvägen för säkerhets kopiering.  

    -   **Lokal enhet på plats servern för plats data och databasen**: anger att säkerhets kopiorna för platsen och plats databasen ska lagras på den angivna sökvägen på den lokala disk enheten på plats servern. Skapa den lokala mappen innan säkerhets kopierings åtgärden körs. Det lokala system kontot på plats servern måste ha **Skriv** behörighet för NTFS-fil till den lokala mappen för plats serverns säkerhets kopiering. Det lokala system kontot på datorn som kör SQL Server måste ha NTFS-behörigheten **Skriv** till mappen för säkerhets kopian av plats databasen.  

    -   **Nätverks Sök väg (UNC-namn) för plats data och databasen**: anger att säkerhets kopiorna för platsen och plats databasen ska lagras i den angivna nätverks Sök vägen. Skapa resursen innan säkerhets kopierings åtgärden körs. Plats serverns dator konto måste ha **Skriv** -NTFS-och resurs behörigheter till mappen delade nätverk. Om SQL Server är installerat på en annan dator, måste dator kontot för SQL Server ha samma behörigheter.  

    -   **Lokala enheter på plats servern och SQL Server**: anger att säkerhets kopiorna för platsen ska lagras på den angivna sökvägen på plats serverns lokala enhet. Uppgiften lagrar säkerhetskopieringsfilerna för plats databasen på den angivna sökvägen på plats databas serverns lokala enhet. Skapa de lokala mapparna innan säkerhets kopierings åtgärden körs. Platsserverns datorkonto måste ha NTFS-filsystembehörigheten **Skriva** till mappen som du skapar på platsservern. SQL Servers datorkonto måste ha NTFS-filsystembehörigheten **Skriva** till mappen som du skapar på platsdatabasservern. Det här alternativet är bara tillgängligt om plats databasen inte är installerad på plats servern.  

    > [!NOTE]  
    > Alternativet att bläddra till säkerhets kopierings målet är bara tillgängligt när du anger nätverks Sök vägen för säkerhets kopierings målet.  
    >  
    > Mappnamnet eller resurs namnet som används för säkerhets kopierings målet stöder inte användning av Unicode-tecken.  

6.  Konfigurera ett schema för plats säkerhets kopierings åtgärden. Överväg ett schema för säkerhets kopiering utanför aktiva arbets timmar. Om du har en-hierarki bör du tänka på ett schema som körs minst två gånger per vecka. Om platsen kraschar säkerställer det här schemat maximal kvarhållning av data.  

    När du kör Configuration Manager-konsolen på samma plats server som du konfigurerar för säkerhets kopiering, använder säkerhets kopierings aktiviteten lokal tid för schemat. När du kör Configuration Manager-konsolen från en annan dator använder säkerhets kopieringen UTC-tid (Coordinated Universal Time) för schemat.  

7.  Välj om du vill skapa en avisering om plats säkerhets kopierings åtgärden Miss lyckas. När det här alternativet är markerat skapar Configuration Manager en kritisk avisering för säkerhets kopierings problemet. Du kan granska dessa aviseringar i noden **aviseringar** på arbets ytan **övervakning** .  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>Kontrol lera att underhålls uppgiften plats Server för säkerhets kopiering körs  

-   Kontrol lera tidsstämpeln på filerna i målmappen för säkerhets kopieringen som uppgiften skapades. Kontrol lera att tidsstämpeln uppdateras till den tidpunkt då uppgiften senast schemalades att köras.  

-   Gå till noden **komponent status** i arbets ytan **övervakning** . Granska status meddelanden för **SMS_SITE_BACKUP**. När säkerhets kopieringen av platsen har slutförts visas meddelande-ID **5035**. Det här meddelandet anger att platsens säkerhets kopiering slutfördes utan fel.  

-   När du konfigurerar säkerhets kopierings aktiviteten för att skapa en avisering när den Miss lyckas kan du leta efter fel aviseringar om säkerhets kopiering i noden **aviseringar** på arbets ytan **övervakning** .  

-   Öppna Utforskaren på plats servern och bläddra till `<ConfigMgrInstallationFolder>\Logs`. Granska **Smsbkup. log** för varningar och fel. När säkerhets kopieringen av platsen har slutförts visas `Backup completed` loggen med `STATMSG: ID=5035`meddelande-ID.  

    > [!TIP]  
    >  Starta om säkerhets kopierings åtgärden genom att stoppa och starta om tjänsten **SMS_SITE_BACKUP** Windows när underhålls åtgärden för säkerhets kopieringen Miss lyckas.  



## <a name="archive-the-backup-snapshot"></a>Arkivera ögonblicks bilden av säkerhets kopian  
Säkerhets kopierings åtgärden skapar en ögonblicks bild av säkerhets kopian första gången den körs. Du kan använda den här ögonblicks bilden för att återställa plats servern om den Miss lyckas. När säkerhets kopierings åtgärden körs igen enligt schemat, skapas en ny ögonblicks bild som skriver över den tidigare ögonblicks bilden. Därför har platsen bara en ögonblicks bild av säkerhets kopian och du har inte möjlighet att hämta en tidigare ögonblicks bild av säkerhets kopian.  

Behåll flera Arkiv av ögonblicks bilden av säkerhets kopian av följande anledningar:  

-   Det är vanligt att säkerhets kopierings medier inte fungerar, får felplacerats eller bara innehåller en partiell säkerhets kopia. Att återställa en misslyckad fristående primär plats från en äldre säkerhetskopia är bättre än att återställa utan någon säkerhetskopia. För en plats server i en hierarki måste säkerhets kopian finnas i SQL Server kvarhållningsperioden för ändrings spårning, eller så krävs inte säkerhets kopieringen.  

-   Ett fel på platsen kan förbli oupptäckt under flera säkerhetskopieringscykler. Du kan behöva använda en ögonblicks bild av en säkerhets kopia från innan platsen skadades. Den här orsaken gäller för en fristående primär plats och till platser i en hierarki där säkerhets kopian finns i SQL Server kvarhållningsperioden för ändrings spårning.  

-   Platsen kanske inte har någon säkerhets kopierings ögonblicks bild alls. Om det till exempel inte går att utföra underhålls åtgärden plats Server för säkerhets kopiering. Eftersom säkerhets kopierings aktiviteten tar bort den tidigare ögonblicks bilden av säkerhets kopian innan den börjar säkerhetskopiera aktuella data kommer det inte att finnas någon giltig ögonblicks bild.  



## <a name="using-the-afterbackupbat-file"></a>Använda filen AfterBackup.bat  
När platsen har säkerhetskopierats försöker säkerhets kopierings aktiviteten automatiskt att köra ett skript med namnet **AfterBackup. bat**. Skapa filen AfterBackup. bat manuellt på plats servern i `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box`. Om det finns en AfterBackup. bat-fil i rätt mapp, körs den automatiskt när säkerhets kopierings åtgärden har slutförts.

AfterBackup. bat-filen låter dig arkivera ögonblicks bilden av säkerhets kopian i slutet av varje säkerhets kopierings åtgärd. Den kan utföra andra uppgifter efter säkerhets kopieringen som inte är en del av underhålls uppgiften plats Server för säkerhets kopiering. AfterBackup.bat-filen integrerar arkivet och säkerhetskopieringsåtgärderna, och säkerställer härigenom att varje ny ögonblicksbild av säkerhetskopian arkiveras.

Om AfterBackup. bat-filen inte finns hoppar säkerhets kopierings åtgärden över den utan att det påverkar säkerhets kopieringen. Kontrol lera att säkerhets kopierings uppgiften har kört det här skriptet genom att gå till noden **komponent status** i arbets ytan **övervakning** och granska status meddelanden för **SMS_SITE_BACKUP**. När du har startat kommando filen AfterBackup. bat visas meddelande-ID **5040**.  

> [!TIP]  
>  Om du vill arkivera säkerhets kopiorna av plats servern med AfterBackup. bat måste du använda ett kopierings kommando verktyg i kommando filen. Ett sådant verktyg är [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) i Windows Server. Skapa till exempel filen AfterBackup. bat med följande kommando:`Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

Även om den avsedda användningen av AfterBackup. bat är att arkivera ögonblicks bilder av säkerhets kopior kan du skapa en AfterBackup. bat-fil för att köra ytterligare aktiviteter i slutet av varje säkerhets kopierings åtgärd.  



##  <a name="supplemental-backup-tasks"></a>Kompletterande säkerhetskopieringsaktiviteter  
Underhålls uppgiften plats Server för säkerhets kopiering innehåller en ögonblicks bild av plats serverns filer och plats databasen. Det finns andra objekt som inte säkerhets kopie ras som du måste tänka på när du skapar din strategi för säkerhets kopiering. Använd de här avsnitten som hjälp när du slutför din strategi för Configuration Manager säkerhets kopiering.  

### <a name="back-up-custom-reports"></a>Säkerhetskopiera anpassade rapporter   
Om du ändrar fördefinierade eller skapade anpassade rapporter i SQL Server Reporting Services skapar du en säkerhets kopia av databasfilerna för rapport servern. Säkerhets kopian av rapport servern måste innehålla följande komponenter:
- Källfilerna för rapporter och modeller
- Krypteringsnycklar
- Anpassade sammansättningar eller tillägg
- Konfigurationsfiler
- Anpassade SQL Server vyer som används i anpassade rapporter
- Anpassade lagrade procedurer  

> [!IMPORTANT]  
>  När Configuration Manager uppdateringar till en nyare version kan de fördefinierade rapporterna skrivas över av nya rapporter. Om du ändrar en fördefinierad rapport, se till att säkerhetskopiera rapporten och sedan återställa den i repor ting Services.  

Mer information om hur du säkerhetskopierar dina anpassade rapporter i repor ting Services finns i [säkerhets kopierings-och återställnings åtgärder för repor ting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).  

### <a name="back-up-content-files"></a>Säkerhetskopiera innehållsfiler  
Innehålls biblioteket i Configuration Manager är den plats där alla innehållsfiler lagras för alla program distributioner. Innehålls biblioteket finns på plats servern och på varje distributions plats. Underhålls uppgiften plats Server för säkerhets kopiering säkerhetskopierar inte innehålls biblioteket eller paketets källfiler. När en plats server kraschar återställs informationen om innehålls biblioteket till plats databasen, men du måste återställa innehålls biblioteket och paketets källfiler.  

-   Innehålls biblioteket måste återställas innan du kan distribuera om innehållet till distributions platser. När du startar omdistribution av innehåll Configuration Manager kopieras filerna från plats serverns innehålls bibliotek till distributions platserna. Mer information finns i [innehålls biblioteket](../../plan-design/hierarchy/the-content-library.md).  

-   Paketets källfiler måste återställas innan du kan uppdatera innehåll på distributions platser. När du startar en innehålls uppdatering Configuration Manager kopierar nya eller ändrade filer från paket källan till innehålls biblioteket. Sedan kopieras filerna till associerade distributions platser. Kör följande SQL Server fråga mot plats databasen för att hitta paketets käll plats för alla paket och program: `SELECT * FROM v_Package`. Du kan identifiera paketets källplats genom att titta på de första tre tecknen i paketets ID. Om paketets ID exempelvis är CEN00001 är platskoden för källplatsen CEN. När du återställer paketets källfiler måste de återställas till samma plats som innan det uppstod.  

Kontrol lera att du inkluderar både innehålls biblioteket och paketets källfiler i fil systemets säkerhets kopia för plats servern.  

### <a name="back-up-custom-software-updates"></a>Säkerhetskopiera anpassade programuppdateringar  
System Center Updates Publisher är ett fristående verktyg som låter dig hantera anpassade program uppdateringar. Updates Publisher använder en lokal databas för sin program uppdaterings lagring. När du använder Updates Publisher för att hantera anpassade program uppdateringar avgör du om du ska ta med Updates Publisher-databasen i din säkerhets kopierings plan. Mer information finns i [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).  

Använd följande procedur för att säkerhetskopiera Updates Publisher-databasen.  

#### <a name="back-up-the-updates-publisher-database"></a>Säkerhetskopiera Updates Publisher-databasen  

1.  På den dator som kör Updates Publisher bläddrar du till uppdaterings utgivarens databas fil **Scupdb. SDF** i `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\`. Det finns en annan databas fil för varje användare som kör Updates Publisher.  

2.  Kopiera databasfilen till ditt mål för säkerhetskopian. Om ditt mål för säkerhets kopiering till exempel `E:\ConfigMgr_Backup`är, kan du kopiera uppdateringens publicerings databas `E:\ConfigMgr_Backup\SCUP`fil till.  

    > [!TIP]  
    >  Om det finns mer än en databas fil på en dator bör du överväga att lagra filen i en undermapp som anger den användar profil som är kopplad till databas filen. Du kan till exempel ha en databas fil i `E:\ConfigMgr_Backup\SCUP\User1` och en annan databas fil i `E:\ConfigMgr_Backup\SCUP\User2`.  



## <a name="user-state-migration-data"></a>Migreringsdata för användartillstånd  
Du kan använda Configuration Manager aktivitetssekvenser för att avbilda och återställa användar tillstånds data i distributions scenarier för operativ system. Egenskaperna för platsen för tillståndsmigrering listar de mappar som lagrar användar tillstånds data. Dessa data säkerhets kopie ras inte som en del av underhålls åtgärden för säkerhets kopiering av plats Server. Som en del av din säkerhetskopieringsplan måste du säkerhetskopiera de mappar som du anger för att spara migreringsdata om användartillstånd manuellt.   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>Bestäm vilka mappar som används för att lagra data för migrering av användar tillstånd  

1.  Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **servrar och plats system roller** .  

2.  Välj det plats system som är värd för tillståndsmigrering. Välj sedan **plats för tillståndsmigrering** i fönstret **plats system roller** .  

3.  Klicka på **Egenskaper** i menyfliksområdet.  

4.  De mappar där migreringsdata om användartillstånd sparas finns angivna i avsnittet **Mappdetaljer** på fliken **Allmänt**.  



## <a name="about-the-sms-writer-service"></a>Om tjänsten SMS Writer  
SMS Writer är en tjänst som interagerar med Windows-tjänsten Volume Shadow Copy (VSS) under säkerhets kopierings processen. Tjänsten SMS Writer måste vara igång för att den Configuration Manager platsen ska kunna slutföras.  

### <a name="process"></a>Process  
1. SMS Writer registreras hos VSS-tjänsten och binds till dess gränssnitt och händelser. 
2. När VSS sänder ut information om händelser, eller om tjänsten skickar specifika meddelanden till SMS Writer, svarar SMS Writer på meddelandet och vidtar lämpliga åtgärder. 
3. SMS Writer läser säkerhets kopierings kontroll filen **Smsbkup. CTL** som finns `<ConfigMgrInstallationPath>\inboxes\smsbkup.box`i och avgör vilka filer och data som ska säkerhets kopie ras. 
4. SMS Writer bygger metadata, som består av olika komponenter, inklusive specifika data från SMS-registernyckeln och under nycklar. 
    a. Den skickar metadata till VSS när den begärs. 
    b. VSS skickar sedan metadata till det begärda programmet, Configuration Manager backup Manager. 
5. Backup Manager väljer vilka data som ska säkerhets kopie ras och skickar dessa data till SMS Writer via VSS. 
6. SMS Writer vidtar de åtgärder som krävs som förberedelse inför säkerhetskopieringen. 
7. Senare, när VSS är redo att ta ögonblicks bilden: a. Den skickar en händelse b. SMS Writer stoppar alla Configuration Manager Services c. Det säkerställer att Configuration Manager aktiviteter är låsta medan ögonblicks bilden skapas. 
8. När ögonblicksbilden har tagits startar SMS Writer om tjänsterna och aktiviteterna.

Tjänsten SMS Writer installeras automatiskt. Den måste vara igång när VSS begär en säkerhetskopiering eller återställning.  

### <a name="writer-id"></a>Id-nummer för Writer  
Skrivar-ID: t för SMS Writer är **03ba67dd-dc6d-4729-A038-251f7018463b**.  

### <a name="permissions"></a>Behörigheter  
Tjänsten SMS Writer måste köras med kontot Lokalt system.  

### <a name="volume-shadow-copy-service"></a>Tjänsten Volume Shadow Copy  
VSS är ett antal COM API:er som implementerar ett ramverk som gör det möjligt att ta säkerhetskopior av volymer medan programmen på systemet fortsätter att skriva till volymerna. VSS erbjuder ett konsekvent gränssnitt som möjliggör samordning mellan användarprogram som ändrar data på hårddisken (tjänsten SMS Writer) och dem som säkerhetskopierar program (tjänsten Backup Manager). Mer information finns i [tjänsten Volume Shadow Copy](https://go.microsoft.com/fwlink/p/?LinkId=241968).  



## <a name="next-steps"></a>Nästa steg
När du har skapat en säkerhets kopia kan du öva [webbplats återställning](recover-sites.md) med säkerhets kopian. Den här metoden kan hjälpa dig att bekanta dig med återställnings processen innan du måste förlita dig på den. Det kan också hjälpa att bekräfta att säkerhets kopieringen lyckades för det avsedda syftet.  
