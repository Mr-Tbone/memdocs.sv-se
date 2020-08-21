---
title: Underhåll för programuppdatering
titleSuffix: Configuration Manager
description: Om du vill underhålla uppdateringar i Configuration Manager kan du schemalägga rensnings uppgiften i WSUS, eller så kan du köra den manuellt.
author: mestew
ms.date: 12/17/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: a327d50a2743f81407530355b6fd5101ce6a8b02
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696913"
---
# <a name="software-updates-maintenance"></a>Underhåll för programuppdatering

*Gäller för: Configuration Manager (aktuell gren)*

Du kan schemalägga och köra rensnings uppgifter för WSUS från Configuration Manager-konsolen från egenskaperna för komponenten för program uppdaterings platsen. När du först väljer att köra rensnings uppgiften i WSUS körs den efter nästa synkronisering av program uppdateringar.  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Schemalägga och köra rensningsuppgiften i WSUS

Schemalägg rensnings jobbet för WSUS genom att köra följande steg:

1. I Configuration Manager-konsolen navigerar du till **Administration**  >  **Översikt**  >  **plats konfiguration**  >  **platser**.
2. Välj platsen överst i Configuration Manager hierarkin.

3. Klicka på **Konfigurera platskomponenter** i gruppen **Inställningar** och klicka sedan på **Plats för programuppdatering** för att öppna Egenskaper för platskomponent för programuppdatering.  

4. Granska **ersättnings beteendet**. Ändra beteendet om det behövs.

   ![skärm bild för ersättnings beteende](media/supersedence-behavior.png)

5. Klicka på fliken **ersättnings regler** , Välj **guiden kör WSUS-rensning**. I version 1806 byter alternativet namn till att **köra WSUS-rensning efter synkronisering**.

6. Klicka på **OK** (klicka på **Stäng** om du kör version 1806).

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>Beteende för WSUS-rensning i version 1802 och tidigare

Innan Configuration Manager version 1806 kör rensnings alternativet för WSUS följande objekt:

- Alternativet **utgångna uppdateringar** från rensnings guiden för WSUS på toppnivå PLATSens WSUS-server.

  ![Skärm bild av WSUS-utgången uppdaterings rensning](media/wsus-cleanup-expired.PNG)

- En rensning för konfigurations objekt för program uppdatering i Configuration Managers databasen sker var sjunde dag och tar bort onödiga uppdateringar från-konsolen.
  - Den här rensningen tar inte bort inaktuella uppdateringar från Configuration Manager-konsolen om de för närvarande har distribuerats.

Ytterligare underhåll krävs fortfarande på den översta WSUS-databasen och alla andra WSUS-databaser i miljön. Mer information och instruktioner finns i blogg inlägget [Microsoft WSUS och Configuration Manager SUP Maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) .

## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>Rensnings beteende för WSUS från och med version 1806

Från och med version 1806 sker rensnings alternativet för WSUS efter varje synkronisering och följande rensnings objekt:
<!--1357898 -->

- Alternativet **inaktuella uppdateringar** för WSUS-servrar på ca: er och primära platser.
  - WSUS-servrar för sekundära platser kör inte WSUS-rensning för utgångna uppdateringar.
- Configuration Manager skapar en lista över ersatta uppdateringar från databasen. Listan baseras på ersättnings beteendet i egenskaperna för komponenten för program uppdaterings plats.
  - De uppdaterings konfigurations objekt som uppfyller ersättnings beteende villkoren har upphört att gälla i Configuration Manager-konsolen.
  - Uppdateringarna nekas i WSUS för ca: er och primära platser, men inte för sekundära platser.
- En rensning för konfigurations objekt för program uppdatering i Configuration Managers databasen sker var sjunde dag och tar bort onödiga uppdateringar från-konsolen.
  - Den här rensningen tar inte bort inaktuella uppdateringar från Configuration Manager-konsolen om de för närvarande har distribuerats.

> [!NOTE]
> Antalet månader innan en ersatt uppdatering har upphört att gälla baseras på det datum då den ersatta uppdateringen skapades. Om du till exempel använder 2 månader för den här inställningen nekas uppdateringar som har ersatts i WSUS och upphör att gälla i Configuration Manager när superceding-uppdateringen är 2 månader gammal.

Alla WSUS-underhåll måste köras manuellt på sekundär platsens WSUS-databaser. Följande alternativ i **guiden Rensa WSUS-Server** körs inte på CAS och primära platser:

- Oanvända uppdateringar och uppdaterings revisioner
- Datorer som inte kontaktar servern
- Uppdateringsfiler som inte behövs

  Mer information och instruktioner finns i blogg inlägget [Microsoft WSUS och Configuration Manager SUP Maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) .

## <a name="wsus-cleanup-behavior-starting-in-version-1810"></a>Rensnings beteende för WSUS från och med version 1810

Från och med version 1810 kan du ange ersättnings regler för funktions uppdateringar separat från uppdateringar som inte är funktions uppdateringar i egenskaperna för komponenten för program uppdaterings platsen. Rensnings alternativet för WSUS inträffar efter varje synkronisering och gör följande rensnings objekt:
<!--2839349,3098809, 2977644-->

- Alternativet **inaktuella uppdateringar** för WSUS-servrar på ca: er, primära och sekundära platser.
- Configuration Manager skapar en lista över ersatta uppdateringar från databasen. Listan baseras på ersättnings beteendet i egenskaperna för komponenten för program uppdaterings plats.
  - De uppdaterings konfigurations objekt som uppfyller ersättnings beteende villkoren har upphört att gälla i Configuration Manager-konsolen.
  - Uppdateringarna nekas i WSUS för ca: er, primära och sekundära platser.
- En rensning för konfigurations objekt för program uppdatering i Configuration Managers databasen sker var sjunde dag och tar bort onödiga uppdateringar från-konsolen.
  - Den här rensningen tar inte bort inaktuella uppdateringar från Configuration Manager-konsolen om de för närvarande har distribuerats.

> [!NOTE]
> Antalet månader innan en ersatt uppdatering har upphört att gälla baseras på det datum då den ersatta uppdateringen skapades. Om du till exempel använder 2 månader för den här inställningen nekas uppdateringar som har ersatts i WSUS och upphör att gälla i Configuration Manager när superceding-uppdateringen är 2 månader gammal.

Följande alternativ i **guiden Rensa WSUS-Server** körs inte på CAS-, primär-och sekundära platser:

- Oanvända uppdateringar och uppdaterings revisioner
- Datorer som inte kontaktar servern
- Uppdateringsfiler som inte behövs

  Mer information och instruktioner finns i blogg inlägget [Microsoft WSUS och Configuration Manager SUP Maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) .

## <a name="wsus-cleanup-starting-in-version-1906"></a>WSUS-rensning startar i version 1906
<!--41101009-->

 Du har ytterligare WSUS underhålls aktiviteter som Configuration Manager kan köra för att upprätthålla felfria program uppdaterings platser. Förutom att de nekade uppdateringar som har gått ut i WSUS kan Configuration Manager lägga till icke-grupperade index i WSUS-databaserna och ta bort föråldrade uppdateringar från WSUS-databaserna. WSUS-underhållet sker efter varje synkronisering.

### <a name="decline-expired-updates-in-wsus-according-to-supersedence-rules"></a>Neka utgångna uppdateringar i WSUS enligt ersättnings regler

Om du avböjer uppdateringar i WSUS förbättras prestanda genom att de uppdateringarna tas bort från katalogerna som skickas till klienter. Att minimera uppdateringar som Configuration Manager markerar som ersatta minimerar ytterligare kataloger och förbättrar prestandan.

1. I Configuration Manager-konsolen navigerar du till **Administration**  >  **Översikt**  >  **plats konfiguration**  >  **platser**.
2. Välj platsen överst i Configuration Manager hierarkin.
3. Klicka på **Konfigurera platskomponenter** i gruppen Inställningar och klicka sedan på **Plats för programuppdatering** för att öppna Egenskaper för platskomponent för programuppdatering.
4. På fliken **WSUS-underhåll** väljer du **neka utgångna uppdateringar i WSUS enligt ersättnings regler**.

### <a name="add-non-clustered-indexes-to-the-wsus-database-to-improve-wsus-cleanup-performance"></a>Lägg till icke-grupperade index i WSUS-databasen för att förbättra prestanda för rensning av WSUS

Om du lägger till icke-grupperade index förbättras prestanda för WSUS-rensning som Configuration Manager gör.

1. I Configuration Manager-konsolen navigerar du till **Administration**  >  **Översikt**  >  **plats konfiguration**  >  **platser**.
2. Välj platsen överst i Configuration Manager hierarkin.
3. Klicka på **Konfigurera platskomponenter** i gruppen Inställningar och klicka sedan på **Plats för programuppdatering** för att öppna Egenskaper för platskomponent för programuppdatering.
4. På fliken **WSUS-underhåll** väljer du **Lägg till icke-grupperade index i WSUS-databasen**.
5. På varje SUSDB som används av Configuration Manager läggs index till i följande tabeller:
   - tbLocalizedPropertyForRevision
   - tbRevisionSupersedesUpdate

#### <a name="sql-permissions-for-creating-indexes"></a>SQL-behörigheter för att skapa index

När WSUS-databasen finns på en fjärran sluten SQL Server kan du behöva lägga till behörigheter i SQL för att skapa index. Det konto som används för att ansluta till WSUS-databasen och skapa index kan variera. Om du anger ett [anslutnings konto för WSUS-servern i egenskaperna för program uppdaterings platsen](../get-started/install-a-software-update-point.md#wsus-server-connection-account)kontrollerar du att anslutnings kontot har SQL-behörighet. Om du inte anger ett anslutnings konto för en WSUS-server måste plats serverns dator konto ha SQL-behörighet.

- För att skapa ett index krävs `ALTER` behörighet för tabellen eller vyn. Kontot måste vara medlem i den `sysadmin` fasta Server rollen eller de `db_ddladmin` `db_owner` fasta databas rollerna och. Mer information om att skapa och indexera och behörigheter finns i [create index (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql?view=sql-server-2017#permissions).
- `CONNECT SQL`Server behörigheten måste beviljas till kontot. Mer information finns i [Granting Server Permissions (Transact-SQL)](/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017).

> [!NOTE]  
>  Om WSUS-databasen finns på en fjärran sluten SQL Server med en annan port än standard porten, kan det hända att index inte läggs till. Du kan skapa ett [Server Ali Aset med Konfigurationshanteraren för SQL Server](/sql/database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client?view=sql-server-2017) för det här scenariot. När aliaset har lagts till och Configuration Manager kan upprätta en anslutning till WSUS-databasen, läggs indexen till.

### <a name="remove-obsolete-updates-from-the-wsus-database"></a>Ta bort föråldrade uppdateringar från WSUS-databasen

Föråldrade uppdateringar är oanvända uppdateringar och uppdaterings revisioner i WSUS-databasen. I allmänhet anses en uppdatering vara föråldrad när den inte längre finns i [Microsoft Update katalogen](https://www.catalog.update.microsoft.com/) och det behövs inga andra uppdateringar som ett krav eller beroende.

1. I Configuration Manager-konsolen navigerar du till **Administration**  >  **Översikt**  >  **plats konfiguration**  >  **platser**.
2. Välj platsen överst i Configuration Manager hierarkin.
3. Klicka på **Konfigurera platskomponenter** i gruppen Inställningar och klicka sedan på **Plats för programuppdatering** för att öppna Egenskaper för platskomponent för programuppdatering.
4. På fliken **WSUS-underhåll** väljer du **ta bort föråldrade uppdateringar från WSUS-databasen**.
   - Borttagning av föråldrad uppdatering kommer att kunna köras i högst 30 minuter innan den stoppas. Den kommer att startas igen när nästa synkronisering sker.  

#### <a name="sql-permissions-for-removing-obsolete-updates"></a>SQL-behörigheter för borttagning av föråldrade uppdateringar

När WSUS-databasen finns på en fjärran sluten SQL Server måste plats serverns dator konto ha följande SQL-behörigheter:

- De `db_datareader` `db_datawriter` fasta databas rollerna och. Mer information finns i [roller på databas nivå](/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-2017#fixed-database-roles).
- `CONNECT SQL`Server behörigheten måste beviljas till plats serverns dator konto. Mer information finns i [Granting Server Permissions (Transact-SQL)](/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017).

#### <a name="wsus-cleanup-wizard"></a>Guiden rensning av WSUS

Från och med version 1906 körs inte följande alternativ i **Guiden rensning av WSUS-Server** på certifikat utfärdare, primära och sekundära platser:

- Datorer som inte kontaktar servern
- Uppdateringsfiler som inte behövs

  Mer information och instruktioner finns i blogg inlägget [Microsoft WSUS och Configuration Manager SUP Maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) .


### <a name="known-issues-for-version-1906"></a>Kända problem för version 1906

Föreställ dig följande scenario:
<!--5418148-->
- Du använder Configuration Manager version 1906
- Du har fjärranslutna program uppdaterings platser med hjälp av en intern Windows-databas
- I **egenskaperna för komponenten för program uppdaterings plats**har du något av följande alternativ på fliken **WSUS-underhåll** :
   - Lägg till icke-grupperade index i WSUS-databasen
   - Ta bort föråldrade uppdateringar från WSUS-databasen

I det här scenariot kan Configuration Manager inte utföra ovanstående WSUS-underhåll för program uppdaterings platser med hjälp av en intern Windows-databas. Det här problemet uppstår eftersom Windows Internal Database inte tillåter fjärr anslutningar. Följande fel visas på `WSyncMgr.log` plats servern:

```text
Indexing Failed. Could not connect to SUSDB.
SqlException thrown while connect to SUSDB in Server: <SUP.CONTOSO.COM>. Error Message: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server)
...
Could not Delete Obselete Updates because ConfigManager could not connect to SUSDB: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) UpdateServer: <SUP.CONTOSO.COM>
```

Du kan lösa problemet genom att automatisera WSUS-underhållet för fjärrprogram uppdaterings platser med hjälp av en intern Windows-databas. Mer information och detaljerade anvisningar finns i [fullständig guide till Microsoft WSUS och Configuration Manager SUP-underhåll](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint).

## <a name="updates-cleanup-log-entries"></a>Uppdatera logg poster för rensning

Du kan kontrol lera den här rensningen genom att granska wsyncmgr. log för följande poster:

- Nekande av ersatta uppdateringar i WSUS är slutförd när du ser den här logg posten: `Cleanup processed <number> total updates and declined <number>`
- Rensningen av WSUS startar när du ser den här posten: `Calling WSUS Cleanup.`
- WSUS-rensningen för utgångna uppdateringar är klar när du ser den här posten: `Successfully completed WSUS Cleanup.`
- Rensningen av konfigurations objekt för Configuration Manager inaktuella uppdateringar startar när du ser den här posten: `Deleting old expired updates...`
- Rensningen av konfigurations objekt för Configuration Manager inaktuella uppdateringar är slutförd när du ser den här posten: `Deleted <number> expired updates total`