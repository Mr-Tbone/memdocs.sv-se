---
title: Uppgradera till aktuell gren
titleSuffix: Configuration Manager
description: Lär dig hur du kör en lyckad uppgradering på plats från en plats och hierarki som kör System Center 2012 Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a2a803a62f2b42c3b62a09e710a3ca74110a4257
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717967"
---
# <a name="upgrade-to-configuration-manager-current-branch"></a>Uppgradera till Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Gör en uppgradering på plats för att Configuration Manager aktuella grenen från en plats och hierarki som kör System Center 2012 Configuration Manager. Innan du uppgraderar från System Center 2012 Configuration Manager måste du förbereda platserna. För det här förberedelse testet krävs att du tar bort vissa konfigurationer som kan förhindra uppgraderingen. Följ sedan uppgraderings ordningen när mer än en plats är involverad.  

> [!TIP]  
> När du hanterar Configuration Manager plats-och hierarki-infrastruktur används villkoren *Uppgradera*, *Uppdatera*och *Installera* för att beskriva tre olika begrepp. Information om hur varje term används finns i [om uppgradering, uppdatering och installation](../../../understand/upgrade-update-install.md).

## <a name="in-place-upgrade-paths"></a><a name="bkmk_path"></a>Sökvägar för uppgradering på plats  

Följande alternativ är de nuvarande uppgraderings vägarna på plats som stöds:

### <a name="upgrade-to-version-2002"></a>Uppgradera till version 2002

Du kan uppgradera följande produkter till en *fullständigt licensierad* version av Configuration Manager, aktuell gren version 2002:

- En *utvärderings* installation av Configuration Manager, aktuell gren version 2002
- System Center 2012 Configuration Manager med Service Pack 1
- System Center 2012 Configuration Manager med Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager med Service Pack 1

Mer information finns i [vanliga frågor och svar om Configuration Manager grenar och licensiering](../../../understand/product-and-licensing-faq.md).

> [!TIP]  
> När du uppgraderar från System Center 2012 Configuration Manager-versionen till den aktuella grenen kan du förenkla uppgraderings processen. Mer information finns i följande:  
>
> - [Bas linje-och uppdaterings versioner](../../manage/updates.md#bkmk_Baselines)  
> - [Mappen CD.Latest](../../manage/the-cd.latest-folder.md)  

### <a name="unsupported-paths"></a>Sökvägar som inte stöds

Följande sökvägar stöds inte:

- Det finns inte stöd för att uppgradera en Technical Preview-gren till en fullt licensierad installation. En teknisk för hands version kan endast uppgradera till en senare version av den tekniska för hands versionen.  

- Migrering från en teknisk för hands version till en fullt licensierad version stöds inte.  

## <a name="upgrade-checklists"></a><a name="bkmk_checklist"></a>Check listor för uppgradering  

Följande check listor kan hjälpa dig att planera en lyckad uppgradering till Configuration Manager.  

### <a name="before-you-upgrade"></a>Innan du uppgraderar  

Granska de här stegen innan du uppgraderar till Configuration Manager.

#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>Granska System Center 2012 Configuration Managers miljö

Lösa problem som beskrivs i följande Microsoft Support artikel: [Configuration Manager-klienter installerar om var femte timme på grund av en återkommande återförsöks aktivitet och kan orsaka en oavsiktlig klient uppgradering](https://support.microsoft.com/help/4018655).

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>Kontrol lera att din miljö uppfyller de konfigurationer som stöds

- Granska serverns OS-version som används som värd för plats system roller:  

  - Vissa äldre operativ system som stöds av System Center 2012 Configuration Manager stöds inte av Configuration Manager aktuella grenen. Ta bort plats system roller på dessa operativ system versioner före uppgraderingen. Mer information finns i [operativ system som stöds för plats system servrar](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

  - Krav kontrollen för Configuration Manager verifierar inte kraven för plats system roller på plats servern eller på fjärrplatssystem  

- Granska nödvändiga komponenter för varje dator som är värd för en plats system roll. Om du till exempel vill distribuera ett operativ system använder Configuration Manager Windows 10 Assessment and Deployment Kit (Windows ADK). Innan du kör installationsprogrammet måste du hämta och installera Windows 10 ADK på platsservern och på varje dator som kör en instans av SMS-providern.  

Mer information om plattformar som stöds och nödvändiga konfigurationer finns i [konfigurationer som stöds](../../../plan-design/configs/supported-configurations.md).  

Mer information om hur du använder Windows ADK med Configuration Manager finns i [infrastruktur krav för distribution av operativ system](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>Granska platsens och hierarkins status och kontrol lera att det inte finns några olösta problem

Innan du uppgraderar en plats måste du lösa alla operativa problem som finns på platsservern, platsdatabasservern och platssystemsrollerna som är installerade på fjärrdatorer. En plats uppgradering kan inte utföras på grund av befintliga drift problem.  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>Installera alla tillämpliga viktiga uppdateringar för operativ system på datorer som är värdar för platsen, plats databas servern och fjärrplatsens system roller

Innan du uppgraderar en plats installerar du eventuelle viktiga uppdateringar för varje tillämpligt platssystem. Om en uppdatering som du installerar kräver att datorn startas om, ska du starta om de aktuella datorerna innan du installerar service packet.  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>Avinstallera plats system rollerna som inte stöds av Configuration Manager

Följande plats system roller används inte längre i Configuration Manager. Avinstallera dem innan du uppgraderar från System Center 2012 Configuration Manager:  

- Out-of-band-hanteringsplats  

- Systemhälsoverifierarpunkt  

- Webbplats punkt för program katalog och webb tjänst punkt

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Inaktivera databas repliker för hanterings platser på primära platser

Configuration Manager kan inte uppgradera en primär plats som har en databas replik för hanterings platser. Inaktivera databasreplikering innan du:  

- Skapar en säkerhetskopia av platsdatabasen för att testa databasuppgraderingen  

- Uppgradera produktions platsen till Configuration Manager aktuella grenen  

Mer information finns i följande artiklar:  

- System Center 2012 Configuration Manager: [Konfigurera databas repliker för hanterings platser](../configure/database-replicas-for-management-points.md#BKMK_DBReplica_Config)  

- Configuration Manager, aktuell gren: [databas repliker för hanterings platser](../configure/database-replicas-for-management-points.md)  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>Konfigurera om program uppdaterings platser som använder NLB

Configuration Manager kan inte uppgradera en plats som använder ett NLB-kluster (utjämning av nätverks belastning) som värd för program uppdaterings platser.  

Om du använder NLB-kluster för programuppdateringsplatser använder du PowerShell för att ta bort NLB-klustret. (Från och med System Center 2012 Configuration Manager SP1 finns det inget alternativ i Configuration Manager-konsolen för att konfigurera ett NLB-kluster.)  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>Inaktivera alla plats underhålls aktiviteter på varje plats under hela den tid då platsen uppgraderas

Innan du uppgraderar till Configuration Manager inaktiverar du alla plats underhålls aktiviteter som kan köras under den tid då uppgraderings processen är aktiv. Den här listan omfattar men är inte begränsad till följande uppgifter:  

- Platsserver för säkerhetskopiering  
- Ta bort föråldrade klientåtgärder  
- Ta bort föråldrade identifieringsdata  

Om en plats databas underhålls aktivitet körs under uppgraderings processen kan plats uppgraderingen inte utföras.  

Innan du inaktiverar en aktivitet registrerar du schemat för aktiviteten så att du kan återställa dess konfiguration när platsuppgraderingen har slutförts.

Mer information om plats underhålls aktiviteter finns i följande artiklar:  

- System Center 2012 Configuration Manager: [Planera för plats åtgärder](../../../plan-design/hierarchy/plan-for-the-site-database.md)  

- Configuration Manager, aktuell gren: [referens för underhålls aktiviteter](../../manage/reference-for-maintenance-tasks.md)  

#### <a name="run-setup-prerequisite-checker"></a>Kör krav kontrollen för installation

Innan du uppgraderar en plats måste du köra **krav kontrollen** oberoende av installations programmet för att kontrol lera att platsen uppfyller kraven. När du senare uppgraderar platsen körs krav kontrollen igen.  

Den oberoende krav kontrollen utvärderar platsen för uppgradering till både den aktuella grenen och LTSB (Long term Servicing Branch) för Configuration Manager. Eftersom vissa funktioner inte stöds av LTSB kan du se poster i **ConfigMgrPrereq. log** som liknar följande exempel:

- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

Om du planerar att uppgradera till den aktuella grenen kan fel för LTSB-versionen ignoreras. De gäller endast om du planerar att uppgradera till LTSB.

Senare, när du kör Configuration Manager installations programmet för att uppgradera, körs krav kontrollen igen. Den utvärderar din webbplats baserat på den gren av Configuration Manager du väljer att installera (aktuell gren eller LTSB). Om du väljer att uppgradera till den aktuella grenen så körs inte kontrollen av de funktioner som inte stöds av LTSB.

Mer information finns i [krav kontrollen](prerequisite-checker.md) och [listan över krav kontroller](list-of-prerequisite-checks.md).  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>Hämta nödvändiga filer och distribuerbara filer för Configuration Manager

Använd **installations hämtaren** för att ladda ned nödvändiga omdistribuerbara filer, språk paket och de senaste produkt uppdateringarna för Configuration Manager.  

Mer information finns i [installations hämtaren](setup-downloader.md).  

#### <a name="plan-to-manage-server-and-client-languages"></a>Planera för hantering av Server-och klient språk

När du uppgraderar en plats installeras endast de språkpaketversioner som du väljer under uppgraderingen.  

- Installations programmet granskar den aktuella språk konfigurationen för platsen. Den identifierar sedan de språk paket som är tillgängliga i den mapp där du lagrar tidigare hämtade nödvändiga filer.  

- Du kan bekräfta valet av aktuella Server-och klient språk paket, eller ändra valen för att lägga till eller ta bort stöd för språk.  

- Endast språk paket som är tillgängliga när du kör installations programmet kan väljas.  

> [!NOTE]  
> Du kan inte använda språk paketen från System Center 2012 Configuration Manager för att aktivera språk för en Configuration Manager aktuella gren platsen.  

Mer information om språk paket finns i [språk paket](language-packs.md).  

#### <a name="review-considerations-for-site-upgrades"></a>Läs överväganden för plats uppgraderingar

När du uppgraderar en plats, återställs vissa funktioner och konfigurationer till standardkonfigurationen. Information om hur du förbereder för dessa och relaterade ändringar finns i [överväganden för uppgradering](#bkmk_considerations).  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>Skapa en säkerhets kopia av plats databasen på den centrala administrations platsen och de primära platserna

Innan du uppgraderar en plats säkerhetskopierar du plats databasen för att kontrol lera att du har en lyckad säkerhets kopia som du kan använda för haveri beredskap.  

Mer information finns i [säkerhets kopiering och återställning](../../manage/backup-and-recovery.md).  

#### <a name="back-up-a-customized-configurationmof-file"></a>Säkerhetskopiera en anpassad Configuration. MOF-fil

Om du använder en anpassad Configuration. MOF-fil för att definiera data klasser som du använder med maskin varu inventering, skapar du en säkerhets kopia av den här filen. Efter uppgraderingen återställer du filen till din plats. Mer information finns i [så här utökar du maskin varu inventering](../../../clients/manage/inventory/extend-hardware-inventory.md).  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>Testa databas uppgraderingen på en kopia av den senaste säkerhets kopian av plats databasen

Innan du uppgraderar en central administrationswebbplats eller primär plats med Configuration Manager bör du testa uppgraderingen av platsdatabasen på en kopia av platsdatabasen.  

- Testa uppgraderings processen för plats databasen. När du uppgraderar en plats kan plats databasen ändras.  

- Även om det inte krävs att testa databas uppgraderingen, kan det identifiera problem för uppgraderingen innan produktions databasen påverkas  

- Om uppgraderingen av platsdatabasen misslyckas kanske den inte går att använda, och platsen kanske måste återställas till fungerande skick  

- Även om platserna i en hierarki använder samma platsdatabas, bör du planera att testa databasen på varje aktuell plats innan du uppgraderar den platsen  

- Om du använder databasreplikeringar för hanteringsplatser på en primär plats, ska du inaktivera replikeringen innan du skapar säkerhetskopian av platsdatabasen  

Configuration Manager stöder inte säkerhets kopiering av sekundära platser eller test uppgradering av en sekundär plats databas.  

Det går inte att köra en uppgradering av test databasen på produktions plats databasen. Då uppdateras platsdatabasen vilket kan göra att platsen inte fungerar alls.  

Mer information finns i [Testa uppgraderingen av databasen](#bkmk_test).  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>Starta om plats servern och varje dator som är värd för en plats system roll

Gör så här för att se till att det inte finns några väntande åtgärder från en senaste installation av uppdateringar eller krav.  

#### <a name="upgrade-sites"></a>Uppgradera platser

Starta på platsen på den översta nivån i hierarkin och kör setup. exe från Configuration Manager-käll mediet.  

När platsen på den översta nivån har uppgraderats kan du börja uppgradera varje underordnad plats. Slutför uppgraderingen av varje plats innan du börjar uppgradera nästa plats.  

Hierarkin körs i ett läge för blandade versioner tills alla platser i hierarkin har uppgraderats till Configuration Manager.  

Information om hur du kör uppgraderingen finns i [Uppgradera platser](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Efter att du har uppgraderat  

Granska de här stegen när du har uppgraderat till Configuration Manager.

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>Uppgradera fristående Configuration Manager-konsoler

När du uppgraderar en central administrations plats eller en primär plats, uppgraderas som standard Configuration Managers konsolen som är installerad på plats servern. Uppgradera manuellt varje-konsol som är installerad på en annan dator än plats servern.  

> [!TIP]  
> Innan du börjar uppgradera ska du stänga varje konsol som är öppen.  

Mer information finns i [installera Configuration Manager-konsoler](install-consoles.md).  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>Konfigurera om databas repliker för hanterings platser på primära platser

Om du använder databas repliker för hanterings platser på primära platser måste du avinstallera databas replikerna innan du uppgraderar platsen. Konfigurera databasreplikeringen för hanteringsplatser när du har uppgraderat en primär plats.

Mer information finns i [databas repliker för hanterings platser](../configure/database-replicas-for-management-points.md).  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>Konfigurera om alla databas underhålls aktiviteter som du inaktiverade före uppgraderingen

Om du har inaktiverat databas [underhålls aktiviteter](../../manage/reference-for-maintenance-tasks.md) på en plats före uppgraderingen konfigurerar du om dessa aktiviteter på platsen med samma inställningar som fanns före uppgraderingen.  

#### <a name="upgrade-clients"></a>Uppgradera klienter

När alla platser har uppgraderats till Configuration Manager, planera att uppgradera klienter.  

När du uppgraderar en klient, avinstalleras den befintliga klientprogramvaran och sedan installeras den nya klientprogramversionen. Du kan använda valfri metod som Configuration Manager stöder för att uppgradera klienter.  

> [!TIP]  
> När platsen på den översta nivån i hierarkin uppdateras, uppdateras även klientinstallationspaketet på varje distributionsplats i hierarkin. När du uppgraderar en primär plats uppdateras klient uppgraderings paketet som är tillgängligt från den primära platsen.  

Mer information finns i [Uppgradera klienter för Windows-datorer](../../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="considerations-for-upgrading"></a><a name="bkmk_considerations"></a>Att tänka på vid uppgradering  

### <a name="automatic-actions"></a>Automatiska åtgärder

När du uppgraderar till Configuration Manager sker följande åtgärder automatiskt:  

- En plats återställning. Den här åtgärden inkluderar ominstallation av alla plats system roller.  

- Om platsen är på den översta nivån i hierarkin, uppdateras klientinstallationspaketet på varje distributionsplats i hierarkin. Platsen uppdaterar också standard start avbildningarna för att använda den nya Windows PE-versionen som ingår i Windows Assessment and Deployment Kit 10. Uppgraderingen uppgraderar dock inte befintliga media för användning med avbildnings distribution.  

- Om platsen är primär, uppdateras klientuppgraderingspaketet för platsen.  

### <a name="manual-actions-after-an-upgrade"></a>Manuella åtgärder efter en uppgradering

När du har uppgraderat en plats ser du till att du utför följande åtgärder:  

- Kontrol lera att klienterna har tilldelats varje primär plats uppgradering och installera den nya klient versionen  

- Uppgradera varje Configuration Manager-konsol som ansluts till platsen och som körs på en dator som är fjärran sluten från plats servern  

- På primära platser där databasreplikeringar används för hanteringsplatser, måste du konfigurera om databasreplikeringarna  

- Uppgradera fysiska media som ISO-filer för CD-skivor, DVD-skivor eller USB-flashminnen manuellt när platsen har uppgraderats. Den innehåller också förinstallerade medier som tillhandahålls av maskin varu leverantörer. Plats uppgraderingen uppdaterar standard start avbildningarna, det går inte att uppgradera de här mediefilerna eller enheterna som används externa för att Configuration Manager.  

- Planera för att uppdatera anpassade Start avbildningar när du inte behöver den äldre versionen av Windows PE.  

### <a name="actions-that-affect-configurations-and-settings"></a>Åtgärder som påverkar konfigurationer och inställningar

När en plats uppgraderas till Configuration Manager sparas inte vissa konfigurationer och inställningar efter uppgraderingen. Vissa konfigurationer är inställda på en ny standard. I följande lista finns några inställningar som inte finns kvar eller som ändras:  

- **Software Center**  
    Följande Software Center-inställningar återställs till sina standardvärden:  

  - **Arbets information** återställs till kontors tid från **5:10:00** till **10:12:00** måndag till fredag.  

  - Värdet för **Datorunderhåll** sätts till **Pausa Software Center-aktiviteter när min dator är i presentationsläge**.  

  - Värdet för **Fjärrstyrning** sätts till det klientinställningsvärde som har tilldelats datorn.  

- **Scheman för sammanfattning av program uppdatering**: anpassade sammanfattnings scheman för program uppdateringar eller program uppdaterings grupper återställs till standardvärdet 1 timme. Återställ de anpassade sammanfattningsinställningarna till önskade värden när uppgraderingen har slutförts.  

## <a name="test-the-site-database-upgrade"></a><a name="bkmk_test"></a>Testa uppgraderingen av plats databasen  

Följande information gäller endast när du uppgraderar en tidigare version som System Center 2012 Configuration Manager för att Configuration Manager aktuella grenen.

Innan du uppgraderar en plats testar du en kopia av platsens databas för uppgraderingen.  

Om du vill testa databasen för en uppgradering återställer du först en kopia av plats databasen till en instans av SQL Server som inte är värd för en Configuration Manager plats. Den version av SQL Server som du använder som värd för databas kopian måste vara en version av SQL Server som Configuration Manager stöder.  

När du har återställt plats databasen kör du Configuration Manager installations programmet från källmappen för Configuration Manager på SQL Server dator. Använd `/TESTDBUPGRADE` kommando rads alternativet.  

Mer information finns i följande artiklar:

- [Säkerhetskopiera en Configuration Manager-plats](../../manage/backup-and-recovery.md)  

- [Kommando rads alternativ för installation](command-line-options-for-setup.md#bkmk_setup)  

- [Stöd för SQL Server-versioner](../../../plan-design/configs/support-for-sql-server-versions.md)  

> [!TIP]  
> Om du integrerar Microsoft Intune med Configuration Manager:  
>
> När du kör ett test för databasuppgradering på en kopia av platsdatabasen som är 5 dagar eller mer, kan det hända att något av följande meddelanden visas:  
>
> - VARNING: Uppgraderingen tvingar full synkronisering till moln.  
> - FEL: Databasuppgraderingen tvingar full synkronisering till moln.  
>
> Båda kan ignoreras på ett säkert sätt vid testning av en databas uppgradering. De tyder inte på ett fel eller problem med test uppgraderingen. De anger i stället att under den faktiska uppgraderingen kan data från **moln** databasens replikeringsgrupp synkroniseras med Microsoft Intune.  

### <a name="test-a-site-database-for-upgrade"></a>Testa en plats databas för uppgradering  

Använd följande procedur på varje central administrations webbplats och primär plats som du planerar att uppgradera:  

1. Gör en kopia av plats databasen. Återställ sedan kopian till en instans av SQL Server som använder samma version som plats databasen och som inte är värd för en Configuration Manager webbplats. Exempel: Om platsdatabasen kör en instans av Enterprise-versionen av SQL Server måste databasen återställas till en SQL Server-instans som också kör Enterprise-versionen.  

2. När du har återställt databas kopian kör du installationen från käll mediet för Configuration Manager aktuella grenen. Använd `/TESTDBUPGRADE` kommando rads alternativet när du kör installations programmet. Om SQL Server-instansen som är värd för databas kopian inte är standard instansen anger du även kommando rads argumenten för att identifiera den instans som är värd för plats databas kopian.  

    Anta till exempel att du tänker uppgradera en platsdatabas med databasnamnet SMS_ABC. Du återställer en kopia av platsdatabasen till en kompatibel SQL Server-instans med instansnamnet DBTest. Använd följande kommando rad för att testa en uppgradering av den här kopian av plats databasen:`Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`  

    Setup. exe finns på följande plats på Configuration Manager-käll mediet:`SMSSETUP\BIN\X64`  

3. På den SQL Server-instans där databasuppgraderingstestet utförs kontrollerar du förloppet genom att bevaka ConfigMgrSetup.log i systemenhetsroten:  

    - Om test uppgraderingen Miss lyckas löser du eventuella problem som rör uppgraderings fel för plats databasen. Skapa sedan en ny säkerhets kopia av plats databasen och testa uppgraderingen av den nya kopian av plats databasen.  

    - När uppgraderingen har lyckats kan du radera databaskopian.  

        > [!NOTE]  
        > Det finns inte stöd för att återställa den kopia av plats databasen som du använder för test uppgraderingen för användning som plats databas på en plats.  

När du har uppgraderat en kopia av plats databasen fortsätter du med uppgraderingen av Configuration Manager-platsen och dess plats databas.  

## <a name="upgrade-sites"></a><a name="bkmk_upgrade"></a>Uppgradera platser  

Du är redo att uppgradera Configuration Manager-platsen när du har slutfört följande aktiviteter:

- Konfigurationer före uppgradering för din plats
- Testa uppgraderingen av plats databasen på en databas kopia
- Hämta nödvändiga filer och språk paket för den version som du planerar att installera

När du uppgraderar en plats i en hierarki börjar du med att uppgradera platsen på den översta nivån i hierarkin. Platsen på den översta nivån är antingen en central administrationsplats eller en fristående primär plats. När du har slutfört uppgraderingen av en central administrations plats kan du uppgradera underordnade primära platser i valfri ordning. När du har uppgraderat en primär plats kan du uppgradera platsens underordnade sekundära platser eller uppgradera ytterligare primära platser innan du uppgraderar några sekundära platser.  

Uppgradera en central administrations plats eller primär plats genom att köra installations programmet från Configuration Manager-käll mediet. Kör inte installations programmet för att uppgradera sekundära platser. I stället använder du Configuration Manager-konsolen för att uppgradera en sekundär plats när du har slutfört uppgraderingen av den primära överordnade platsen.  

Innan du uppgraderar en plats stänger du Configuration Manager-konsolen på plats servern tills platsen uppgraderingen har slutförts. Stäng också varje Configuration Manager-konsol som körs på andra datorer än plats servern. Du kan öppna konsolen igen när platsuppgraderingen har slutförts. Men tills du uppgraderar en Configuration Manager-konsol till den nya versionen av Configuration Manager kan den konsolen inte visa vissa objekt och information som är tillgängliga i den nya versionen av Configuration Manager.  

### <a name="upgrade-a-central-administration-site-or-primary-site"></a>Uppgradera en central administrations plats eller en primär plats  

1. Kontrollera att den användare som kör installationsprogrammet har följande säkerhetsbehörigheter:  

    - Lokal **Administratörs** behörighet på plats servern  

    - Om plats databas servern är fjärr från plats servern, lokal **Administratörs** behörighet på den.  

2. Öppna följande program på plats servern: `<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe`. Den här åtgärden öppnar installations guiden för Configuration Manager.  

3. Läs informationen på sidan **innan du börjar** och välj sedan **Nästa**.  

4. På sidan **komma igång** väljer du **uppgradera den här Configuration Manager platsen**och väljer sedan **Nästa**.  

5. På sidan **produkt nyckel** :  

    Om du tidigare har installerat Configuration Manager utvärdering kan du välja **installera den licensierade versionen av den här produkten**. Ange sedan produkt nyckeln för en fullständig installation av Configuration Manager. Den här åtgärden konverterar platsen till en fullständig version.  

    Du kan också ange **utgångs datumet för Software Assurance** för ditt licens avtal som en bekväm påminnelse till dig om det datumet. Om du inte anger det här värdet under installationen kan du ange det senare i Configuration Manager-konsolen.  

    > [!NOTE]  
    > Microsoft validerar inte det utgångs datum du angav och kommer inte att använda det här datumet för licens validering. Du kan använda den som en påminnelse om ditt förfallo datum. Configuration Manager regelbundet söker efter nya program uppdateringar som erbjuds online och din licens status för Software Assurance måste vara aktuell för att kunna använda dessa ytterligare uppdateringar.

    Mer information finns i [licensiering och grenar](../../../understand/learn-more-editions.md).

6. På sidan **licens villkor för program vara från Microsoft** läser du igenom och godkänner licens villkoren och väljer sedan **Nästa**.  

7. På sidan **nödvändiga licenser** läser du igenom och godkänner licens villkoren för den nödvändiga program varan och väljer sedan **Nästa**. Installations programmet laddar ned och installerar automatiskt program varan på plats system eller klienter när det behövs. Innan du kan fortsätta till nästa sida godkänner du alla villkor.  

8. På sidan **nödvändiga hämtningar** anger du om installations programmet ska hämta det senaste innehållet från Internet eller om tidigare nedladdade filer ska användas. Det här innehållet inkluderar nödvändiga omdistribuerbara filer, språk paket och de senaste produkt uppdateringarna. Om du tidigare har hämtat filer med installationshämtaren markerar du **Använd tidigare hämtade filer** och anger en hämtningsmapp. Mer information finns i [installations hämtaren](setup-downloader.md).  

    > [!NOTE]  
    > Om du använder tidigare hämtade filer bör du kontrollera att sökvägen till hämtningsmappen innehåller den senaste versionen av filerna.  

9. På sidan **Val av serverspråk** visas en lista med språk som är installerade för platsen. Välj ytterligare språk som är tillgängliga på den här platsen för Configuration Manager-konsolen och för-rapporter. Du kan också ta bort språk som du inte längre vill ha stöd för på den här platsen. Som standard är engelska markerat och kan inte tas bort.  

    > [!IMPORTANT]  
    > Varje version av Configuration Manager kan inte använda språk paket från en tidigare version av Configuration Manager. Om du vill aktivera stöd för ett språk på en Configuration Manager plats som du uppgraderar, måste du använda språk paketets version för den nya versionen. Till exempel, vid uppgradering från System Center 2012 Configuration Manager till Configuration Manager aktuell gren, om den aktuella gren versionen av ett språk paket inte är tillgänglig med de nödvändiga filer som du hämtar, kan du inte installera stöd för språket.  

10. På sidan **Val av klientspråk** visas en lista med språk som är installerade för platsen. Välj fler språk som ska vara tillgängliga för platsens klientdatorer, eller välj bort språk som du inte längre vill ge stöd för på platsen. Ange om alla klientspråk ska aktiveras för mobilenhetsklienter och klicka sedan på **Nästa**. Som standard är engelska markerat och kan inte tas bort.  

11. På sidan **Sammanfattning av inställningar** granskar du konfigurationen. När du är klar väljer du **Nästa** för att starta krav kontrollen för att verifiera Server beredskap för uppgraderingen av platsen.  

12. Om inga problem visas på sidan **kontroll av installations krav** väljer du **Nästa** för att uppgradera plats-och plats system rollerna.

    Om ett problem upptäcks under krav kontrollen kan du välja ett objekt i listan för information om hur du löser problemet. Om problem visas i listan, dvs. om det finns poster med statusen **Fel** , måste du åtgärda problem innan du fortsätter med installationen. När du har löst problemet klickar du på **Kör kontroll** för att starta om kravkontrollen. Du kan även öppna filen ConfigMgrPrereq.log i systemenhetens rot och granska resultatet från kravkontrollen. Logg filen kan innehålla ytterligare information som inte visas i användar gränssnittet. En lista över nödvändiga regler och beskrivningar för installationen finns i [krav kontroll](list-of-prerequisite-checks.md).

På sidan **Uppgradera** visas övergripande installationsstatus. När huvudplatsserver- och platssysteminstallationen är klar kan du stänga guiden. Platskonfigurationen fortsätter i bakgrunden.  

### <a name="upgrade-a-secondary-site"></a>Uppgradera en sekundär plats  

1. Kontrollera att den administrativa användaren som kör installationsprogrammet har följande säkerhetsbehörigheter:  

    - Lokal **Administratörs** behörighet på den sekundära plats servern  

    - **Infrastruktur administratör** eller säkerhets rollen **Fullständig administratör** på den överordnade primära platsen  

    - System administratörs rättigheter (**sa**) på plats databasen för den sekundära platsen  

2. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

3. Välj den sekundära plats som du vill uppgradera. På fliken **Start** i menyfliksområdet väljer du **Uppgradera**i gruppen **plats** .  

4. Välj **Ja** för att bekräfta beslutet och starta uppgraderingen av den sekundära platsen.  

Uppgraderingen av den sekundära platsen körs i bakgrunden. När uppgraderingen är klar bekräftar du statusen i Configuration Manager-konsolen. Välj den sekundära plats servern och välj **Visa installations status**i gruppen **plats** på fliken **Start** i menyfliksområdet.  

## <a name="post-upgrade-tasks"></a><a name="BKMK_PostUpgrade"></a>Uppgifter efter uppgraderingen  

När du har uppgraderat en plats kan du behöva utföra ytterligare åtgärder för att slutföra uppgraderingen eller konfigurera om platsen. Dessa uppgifter kan omfatta följande objekt:

- Uppgradera Configuration Manager-klienter
- Uppgradera Configuration Manager-konsoler
- Återaktivera databas repliker för hanterings platser
- Återställa inställningar för Configuration Manager funktioner som du använder och som inte behålls efter uppgraderingen  
