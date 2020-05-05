---
title: Obevakad återställning
titleSuffix: Configuration Manager
description: Använd ett skript för att återställa dina webbplatser i Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a12de673776817330a80cb68588faf225922e241
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720802"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Obevakad webbplats återställning för Configuration Manager   

*Gäller för: Configuration Manager (aktuell gren)*

 Om du vill utföra en [obevakad återställning](recover-sites.md#site-recovery-procedures) av en Configuration Manager Central administrations plats eller primär plats kan du skapa ett obevakat installations skript och sedan använda installations programmet med kommando alternativet **/script** . Skriptet innehåller samma typ av information som installations guiden efterfrågar, förutom att det inte finns några standardinställningar. Alla värden måste anges för de installationsnycklar som gäller för den typ av återställning som du använder.

 Om du vill använda kommando rads alternativet/script setup måste du skapa en initierings fil. Ange sedan det här fil namnet efter alternativet/script. Filens namn är inte viktigt så länge den har fil namns tillägget **. ini** . När du hänvisar till initeringsfilen från kommandoraden måste du uppge den fullständiga sökvägen till filen. Om installations initierings filen till exempel heter *Setup. ini*och lagras i *mappen C:\setup*skulle kommando raden bli:

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  Du måste ha administratörs behörighet för att köra installations programmet. När du kör installations programmet med det obevakade skriptet startar du kommando tolken i en administratörs kontext med hjälp av **Kör som administratör**.

 Skriptet innehåller avsnittsnamnen, nyckelnamn och värden. De nödvändiga nyckelnamnet på avsnitten varierar beroende på vilken återställningstyp som du skriptar. Ordningen på nycklarna i avsnitt och ordningen på avsnitt i filen är inte viktigt. Nycklarna är inte Skift läges känsliga. När du anger värden för nycklarna måste namnet på nycklarna följas av ett likhetstecken (=) och värdet för nyckeln.

 Använd följande avsnitt för att få hjälp med att skapa ditt skript för obevakad platsåterställning. I tabellen anges de tillgängliga installationsskriptnycklarna, motsvarande värden, om de är obligatoriska eller ej, vilken typ av installation de används för samt en kort beskrivning av nyckeln.

## <a name="recover-a-central-administration-site-unattended"></a>Återställa en central administrationsplats obevakat
 Använd följande information för att konfigurera en obevakad installations skript fil för att återställa en central administrations plats.

 **Fastställa**

-   **Nyckelnamn:** Action

    -   **Krävs:** Ja
    -   **Värden:** RecoverCCAR
    -   **Information:** Återställer en central administrationsplats


-   **Nyckel namn:** CDLatest

    -   **Krävs:** Ja – endast när du använder media från CD: n. Senaste mappen.
    -   **Värden:** 1 andra värden än 1 anses inte använda CD. Nya.
    -   **Information:** Skriptet måste innehålla den här nyckeln och värdet när du kör installations programmet från media i en CD. Den senaste mappen för att installera en primär eller Central administrations plats eller återställning av en primär eller Central administrations plats. Det här värdet informerar installations programmet om medie formulärets CD. Den senaste används.

**RecoveryOptions**   
-   **Nyckelnamn:** ServerRecoveryOptions   

    -   **Krävs:** Ja
    -   **Värden:** 1, 2 eller 4  
         1 = Återställ platsserver och SQL Server.   
         2 = Återställ endast platsserver.  
         4 = Återställ endast SQL Server.
    -   **Information:** Anger om installations programmet återställer plats servern, SQL Server eller båda. De tillhörande nycklarna är obligatoriska när du anger följande värde för inställningen ServerRecoveryOptions:  
        -   **Värde = 1** Du kan ange ett värde för nyckeln **SiteServerBackupLocation** för att återställa platsen med hjälp av en säkerhetskopia. Om du inte anger något värde ominstalleras platsen utan återställning från en säkerhetskopia.

             Nyckeln **BackupLocation** är obligatorisk när du anger värdet **10** för nyckeln **DatabaseRecoveryOptions** för att återställa platsdatabasen från en säkerhetskopia.

        -   **Värde = 2** Du kan ange ett värde för nyckeln **SiteServerBackupLocation** för att återställa platsen med hjälp av en säkerhetskopia. Om du inte anger något värde ominstalleras platsen utan återställning från en säkerhetskopia.

        -   **Värde = 4** Nyckeln **BackupLocation** är obligatorisk när du anger värdet **10** för nyckeln **DatabaseRecoveryOptions** för att återställa platsdatabasen från en säkerhetskopia.

-   **Nyckelnamn:** DatabaseRecoveryOptions

    -   **Krävs:** Kanske
    -   **Parametervärden**   
         - **10** = Återställ plats databasen från en säkerhets kopia.  
         - **20** = Använd en plats databas som har återställts manuellt med hjälp av en annan metod.   
         - **40** = skapa en ny databas för platsen. Använd det här alternativet om det inte finns någon säkerhetskopia av platsdatabasen. Globala data och platsdata återställs via replikering från andra platser.  
         - **80** = hoppa över databas återställning.
    -   **Information:** Anger hur installations programmet återställer plats databasen i SQL Server. Den här nyckeln är obligatorisk när inställningen **ServerRecoveryOptions** har värdet **1** eller **4**.


-   **Nyckelnamn:** ReferenceSite  

    -   **Krävs:** Kanske
    -   **Värden:** &lt;ReferenceSiteFQDN\>
    -   **Information:** Anger den primära referens platsen. Om säkerhets kopian av databasen är äldre än bevarande perioden för ändrings spårning, eller om du återställer platsen utan en säkerhets kopia, använder den centrala administrations platsen referens platsen för att återställa globala data.

         Om du inte anger en referens plats och säkerhets kopian är äldre än bevarande perioden för ändrings spårning, initieras alla primära platser om med återställda data från den centrala administrations platsen.

         Om du inte anger en referens plats och säkerhets kopian finns inom kvarhållningsperioden för ändrings spårning replikeras endast ändringar sedan säkerhets kopieringen replikeras från primära platser. När det finns ändringar från primära platser som står i konflikt med varandra så används den först mottagna ändringen.

         Den här nyckeln är obligatorisk när inställningen **DatabaseRecoveryOptions** har värdet **40**.

-   **Nyckelnamn:** SiteServerBackupLocation

    -   **Krävs:** Nej
    -   **Värden:** &lt;PathToSiteServerBackupSet\>
    -   **Information:** Anger sökvägen till den säkerhetskopierade platsservern. Den här nyckeln är valfri när inställningen **ServerRecoveryOptions** har värdet **1** eller **2**. Ange ett värde för nyckeln **SiteServerBackupLocation** för att återställa platsen med hjälp av en säkerhetskopia. Om du inte anger något värde ominstalleras platsen utan återställning från en säkerhetskopia.


-   **Nyckelnamn:** BackupLocation

    -   **Krävs:** Kanske
    -   **Värden:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Information:** Anger sökvägen till den säkerhetskopierade platsdatabasen. Nyckeln **BackupLocation** är obligatorisk när du anger värdet **1** eller **4** för nyckeln **ServerRecoveryOptions** och värdet **10** för nyckeln **DatabaseRecoveryOptions** .


**Alternativ**

- **Nyckelnamn:** ProductID
  -   **Krävs:** Ja
  -   **Parametervärden**   
       - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
       - Eval
  -   **Information:** Produkt nyckeln för Configuration Manager installationen, inklusive strecken. I **utvärderingen kan du installera utvärderings** versionen av Configuration Manager.  


- **Nyckelnamn:** SiteCode

  -   **Krävs:** Ja
  -   **Värden:** &lt;platskod\>
  -   **Information:** Tre alfanumeriska tecken som unikt identifierar platsen i hierarkin. Ange den platskod som användes av platsen före åtgärden.


- **Nyckelnamn:** SiteName

  -   **Krävs:** Ja
  -   **Värden:** Platsnamn
  -   **Information:** Beskrivning av platsen.


- **Nyckelnamn:** SMSInstallDir

  - **Krävs:** Ja
  - **Värden:** &lt;*ConfigMgrInstallationPath*>
  - **Information:** Anger installationsmappen för Configuration Manager program-filerna.
    > [!NOTE]   
    >  Du kan ange den ursprungliga sökvägen eller en ny sökväg som ska användas för den Configuration Manager installationen.

- **Nyckelnamn:** SDKServer

  -   **Krävs:** Ja
  -   **Värden:** &lt;*FQDN för SMS-provider*>
  -   **Information:** Anger FQDN för den server som är värd för SMS-providern. Ange den server som är värd för SMS-providern före det här problemet.

       Du kan konfigurera ytterligare SMS-providrar för platsen efter den första installationen.

- **Nyckelnamn:** PrerequisiteComp

  -   **Krävs:** Ja
  -   **Värden:** 0 eller 1  
       0 = ladda ned   
       1 = redan nedladdat
  -   **Information:** Anger om nödvändiga filer för installations programmet redan har laddats ned. Om du till exempel använder värdet 0 laddar installations programmet ned filerna.  


- **Nyckelnamn:** PrerequisitePath

  -   **Krävs:** Ja
  -   **Värden:** &lt;*PathToSetupPrerequisiteFiles*>
  -   **Information:** Anger sökvägen till de nödvändiga filerna för installationen. Beroende på **PrerequisiteComp** -värdet använder installations programmet den här sökvägen för att lagra hämtade filer eller för att hitta tidigare hämtade filer.

- **Nyckelnamn:** AdminConsole

  -   **Krävs:** Kanske
  -   **Värden:** 0 eller 1 0 = installera inte   
       1 = installera
  -   **Information:** Anger om Configuration Manager-konsolen ska installeras eller inte. Den här nyckeln är obligatorisk förutom när inställningen **ServerRecoveryOptions** har värdet **4**.


- **Nyckelnamn:** JoinCEIP   
  > [!Note]  
  > Från och med Configuration Manager version 1802, tas CEIP-funktionen bort från produkten.

  -   **Krävs:** Ja
  -   **Värden:** 0 eller 1  
       0 = delta inte  
       1 = delta
  -   **Information:** Anger om du ska delta eller inte i Customer Experience Improvement Program.

**SQLConfigOptions**

-   **Nyckelnamn:** SQLServerName

    -   **Krävs:** Ja
    -   **Värden:** * &lt;SQLServerName\>*
    -   **Information:** Namnet på servern eller namnet på den klustrade instansen som kör SQL Server som är värd för plats databasen. Ange samma server som är värd för plats databasen före felen.


-   **Nyckelnamn:** DatabaseName

    -   **Krävs:** Ja
    -   **Värden:** * &lt;SiteDatabaseName\> * \\eller * &lt;instancename\>**SiteDatabaseName&lt;\> *
    -   **Information:** Anger namnet på SQL Server-databasen som ska skapas eller användas för att installera databasen för den centrala administrationsplatsen. Ange samma databas namn som användes före det här problemet.

        > [!IMPORTANT]  
        >  Om du inte använder standard instansen måste du ange instans namn och plats databasens namn.

-   **Nyckelnamn:** SQLSSBPort

    -   **Krävs:** Nej
    -   **Värden:** &lt;*SSBPortNumber*>
    -   **Information:** Ange den SQL SBB-port (Server Service Broker) som används av SQL Server. SSB är vanligtvis konfigurerat för användning av TCP-porten 4022, men även andra portar kan användas. Ange samma SSB-port som användes före det här problemet.

## <a name="recover-a-primary-site-unattended"></a>Återställa en primär obevakad platsserver
 Använd följande information för att konfigurera en obevakad installations skript fil för att återställa en central administrations plats.

 **Fastställa**

-   **Nyckelnamn:** Action

    -   **Krävs:** Ja
    -   **Värden:** RecoverPrimarySite
    -   **Information:** Återställer en primär plats


-   **Nyckel namn:** CDLatest

    -   **Krävs:** Ja – endast när du använder media från CD: n. Senaste mappen.
    -   **Värden:** 1 andra värden än 1 anses inte använda CD. Nya.
    -   **Information:** Skriptet måste innehålla den här nyckeln och värdet när du kör installations programmet från media i en CD. Den senaste mappen för att installera en primär eller Central administrations plats eller återställning av en primär eller Central administrations plats. Det här värdet informerar installations programmet om medie formulärets CD. Den senaste används.

**RecoveryOptions**

-   **Nyckelnamn:** ServerRecoveryOptions

    -   **Krävs:** Ja
    -   **Värden:** 1, 2 eller 4    
         1 = Återställ platsserver och SQL Server.   
         2 = Återställ endast platsserver.  
         4 = Återställ endast SQL Server.
    -   **Information:** Anger om installations programmet återställer plats servern, SQL Server eller båda. De tillhörande nycklarna är obligatoriska när du anger följande värde för inställningen ServerRecoveryOptions:

        -   **Värde = 1** Du kan ange ett värde för nyckeln **SiteServerBackupLocation** för att återställa platsen med hjälp av en säkerhetskopia. Om du inte anger något värde ominstalleras platsen utan återställning från en säkerhetskopia.

             Nyckeln **BackupLocation** är obligatorisk när du anger värdet **10** för nyckeln **DatabaseRecoveryOptions** för att återställa platsdatabasen från en säkerhetskopia.

        -   **Värde = 2** Du kan ange ett värde för nyckeln **SiteServerBackupLocation** för att återställa platsen med hjälp av en säkerhetskopia. Om du inte anger något värde ominstalleras platsen utan återställning från en säkerhetskopia.

        -   **Värde = 4** Nyckeln **BackupLocation** är obligatorisk när du anger värdet **10** för nyckeln **DatabaseRecoveryOptions** för att återställa platsdatabasen från en säkerhetskopia.

-   **Nyckelnamn:** DatabaseRecoveryOptions

    -   **Krävs:** Kanske
    -   **Parametervärden**   
         - **10** = Återställ plats databasen från en säkerhets kopia.  
         - **20** = Använd en plats databas som har återställts manuellt med hjälp av en annan metod.     
         - **40** = skapa en ny databas för platsen. Använd det här alternativet om det inte finns någon säkerhetskopia av platsdatabasen. Globala data och platsdata återställs via replikering från andra platser.  
         - **80** = hoppa över databas återställning.
    -   **Information:** Anger hur installations programmet återställer plats databasen i SQL Server. Den här nyckeln är obligatorisk när inställningen **ServerRecoveryOptions** har värdet **1** eller **4**.


-   **Nyckelnamn:** SiteServerBackupLocation

    -   **Krävs:** Nej
    -   **Värden:** &lt;PathToSiteServerBackupSet\>
    -   **Information:** Anger sökvägen till den säkerhetskopierade platsservern. Den här nyckeln är valfri när inställningen **ServerRecoveryOptions** har värdet **1** eller **2**. Ange ett värde för nyckeln **SiteServerBackupLocation** för att återställa platsen med hjälp av en säkerhetskopia. Om du inte anger något värde ominstalleras platsen utan återställning från en säkerhetskopia.     


-   **Nyckelnamn:** BackupLocation

    -   **Krävs:** Kanske
    -   **Värden:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Information:** Anger sökvägen till den säkerhetskopierade platsdatabasen. Nyckeln **BackupLocation** är obligatorisk när du anger värdet **1** eller **4** för nyckeln **ServerRecoveryOptions** och värdet **10** för nyckeln **DatabaseRecoveryOptions** .

**Alternativ**

-   **Nyckelnamn:** ProductID

    -   **Krävs:** Ja
    -   **Parametervärden**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - Eval     
    -   **Information:** Produkt nyckeln för Configuration Manager installationen, inklusive strecken. I **utvärderingen kan du installera utvärderings** versionen av Configuration Manager.  


-   **Nyckelnamn:** SiteCode

    -   **Krävs:** Ja
    -   **Värden:** &lt;platskod\>
    -   **Information:** Tre alfanumeriska tecken som unikt identifierar platsen i hierarkin. Ange den platskod som användes av platsen före åtgärden.


-   **Nyckelnamn:** SiteName

    -   **Krävs:** Ja
    -   **Värden:** Platsnamn
    -   **Information:** Beskrivning av platsen.


-   **Nyckelnamn:** SMSInstallDir

    -   **Krävs:** Ja
    -   **Värden:** &lt;*ConfigMgrInstallationPath*>
    -   **Information:** Anger installationsmappen för Configuration Manager program-filerna.

        > [!NOTE]   
        >  Du kan ange den ursprungliga sökvägen eller en ny sökväg som ska användas för den Configuration Manager installationen.

-   **Nyckelnamn:** SDKServer

    -   **Krävs:** Ja
    -   **Värden:** &lt;*FQDN för SMS-provider*>
    -   **Information:** Anger FQDN för den server som är värd för SMS-providern. Ange den server som är värd för SMS-providern före det här problemet.

         Du kan konfigurera ytterligare SMS-providrar för platsen efter den första installationen.

-   **Nyckelnamn:** PrerequisiteComp

    -   **Krävs:** Ja
    -   **Värden:** 0 eller 1    
         0 = ladda ned   
         1 = redan nedladdat   
    -   **Information:** Anger om nödvändiga filer för installations programmet redan har laddats ned. Om du till exempel använder värdet 0 laddar installations programmet ned filerna.


-   **Nyckelnamn:** PrerequisitePath

    -   **Krävs:** Ja
    -   **Värden:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Information:** Anger sökvägen till de nödvändiga filerna för installationen. Beroende på **PrerequisiteComp** -värdet använder installations programmet den här sökvägen för att lagra hämtade filer eller för att hitta tidigare hämtade filer.


-   **Nyckelnamn:** AdminConsole

    -   **Krävs:** Kanske
    -   **Värden:** 0 eller 1  
         0 = installera inte   
         1 = installera  
    -   **Information:** Anger om Configuration Manager-konsolen ska installeras eller inte. Den här nyckeln är obligatorisk förutom när inställningen **ServerRecoveryOptions** har värdet **4**.

-   **Nyckelnamn:** JoinCEIP  
    > [!Note]  
    > Från och med Configuration Manager version 1802, tas CEIP-funktionen bort från produkten.

    -   **Krävs:** Ja
    -   **Värden:** 0 eller 1    
         0 = delta inte  
         1 = delta
    -   **Information:** Anger om du ska delta eller inte i Customer Experience Improvement Program.


**SQLConfigOptions**

-   **Nyckelnamn:** SQLServerName

    -   **Krävs:** Ja
    -   **Värden:** * &lt;SQLServerName\>*
    -   **Information:** Namnet på servern eller namnet på den klustrade instansen som kör SQL Server som är värd för plats databasen. Ange samma server som är värd för plats databasen före felen.


-   **Nyckelnamn:** DatabaseName

    -   **Krävs:** Ja
    -   **Värden:** * &lt;SiteDatabaseName\> * \\eller * &lt;instancename\>**SiteDatabaseName&lt;\> *
    -   **Information:** Anger namnet på SQL Server-databasen som ska skapas eller användas för att installera databasen för den centrala administrationsplatsen. Ange samma databas namn som användes före det här problemet.

        > [!IMPORTANT]    
        >  Om du inte använder standard instansen måste du ange instans namn och plats databasens namn.

-   **Nyckelnamn:** SQLSSBPort

    -   **Krävs:** Nej
    -   **Värden:** &lt;*SSBPortNumber*>
    -   **Information:** Ange den SQL SBB-port (Server Service Broker) som används av SQL Server. SSB är vanligtvis konfigurerat för användning av TCP-porten 4022, men även andra portar kan användas. Ange samma SSB-port som användes före det här problemet.

**Expansionsalternativ för hierarkin**

-   **Nyckelnamn:** CCARSiteServer

    -   **Krävs:** Kanske
    -   **Värden:** &lt; *SiteCodeForCentralAdministrationSite*>
    -   **Information:** Anger den centrala administrations platsen som en primär plats kopplas till när den ansluter till Configuration Manager-hierarkin. Den här inställningen är obligatorisk om den primära platsen har kopplats till en central administrationsplats före felet. Ange den platskod som användes för den centrala administrations platsen före problemet.

-   **Nyckelnamn:** CASRetryInterval

    -   **Krävs:** Nej
    -   **Värden:** &lt; *Interval*>
    -   **Information:** Anger intervallet (i minuter) för nya försök att ansluta till den centrala administrationswebbplatsen om anslutningen misslyckas. Om det till exempel inte går att ansluta till den centrala administrations platsen, väntar den primära platsen det antal minuter som du anger för CASRetryInterval och försöker sedan ansluta igen.


-   **Nyckelnamn:** WaitForCASTimeout

    -   **Krävs:** Nej
    -   **Värden:** &lt;*Timeout*>
    -   **Information:** Anger det maximala värdet för tidsgränsen (i minuter) för en primär platsanslutning till den centrala administrationswebbplatsen. Om en primär plats exempelvis misslyckas med att ansluta till en central administrationsplats, försöker den primära platsen upprätta anslutningen till den centrala administrationsplatsen igen baserat på CASRetryInterval tills WaitForCASTimeout-perioden har uppnåtts. Ange ett värde mellan 0 och 100.
