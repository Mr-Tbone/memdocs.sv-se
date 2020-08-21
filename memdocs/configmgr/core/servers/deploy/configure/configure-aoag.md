---
title: Konfigurera tillgänglighets grupper
titleSuffix: Configuration Manager
description: Konfigurera och hantera SQL Server Always on-tillgänglighetsgrupper med Configuration Manager
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e85b36d0caeb6ceb99f56220e271774dc0db0f6
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699253"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Konfigurera SQL Server Always on-tillgänglighetsgrupper för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd informationen i den här artikeln för att konfigurera och hantera de tillgänglighets grupper som du använder med Configuration Manager.

Innan du börjar:  

- Var bekant med informationen från [att förbereda för att använda SQL Server Always on-tillgänglighetsgrupper med Configuration Manager](sql-server-alwayson-for-a-highly-available-site-database.md).
- Var bekant med SQL Server-dokumentationen som täcker användningen av tillgänglighets grupper och relaterade procedurer. Den informationen krävs för att slutföra följande scenarier.


## <a name="create-and-configure-an-availability-group"></a><a name="bkmk_create"></a> Skapa och konfigurera en tillgänglighets grupp

Använd följande procedur för att skapa en tillgänglighets grupp och sedan flytta en kopia av plats databasen till den tillgänglighets gruppen.

1. Använd följande kommando för att stoppa Configuration Manager-platsen:

    `preinst.exe /stopsite`

    Mer information finns i [verktyget underhåll av hierarki](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Ändra säkerhets kopierings modellen för plats databasen från **enkel** till **fullständig**:

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    Tillgänglighets grupper stöder bara den fullständiga säkerhets kopierings modellen. Mer information finns i [Visa eller ändra återställnings modellen för en databas](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

3. Använd SQL Server för att skapa en fullständig säkerhets kopia av plats databasen. Välj något av följande alternativ:

    - **Blir medlem i tillgänglighets gruppen**: om du använder den här servern som första primära replik medlem i tillgänglighets gruppen behöver du inte återställa en kopia av plats databasen till den här servern eller en annan i gruppen. Databasen finns redan på den primära repliken. SQL Server replikerar databasen till de sekundära replikerna under ett senare steg.  

    - **Kommer inte att vara medlem i tillgänglighets gruppen**: Återställ en kopia av plats databasen till servern som ska vara värd för den primära repliken av gruppen.

    Mer information finns i följande artiklar i SQL Server-dokumentationen:

    - [Skapa en fullständig säkerhets kopia av databasen](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [Återställa en säkerhets kopia av databasen med SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > Om du planerar att flytta från en tillgänglighets grupp till fristående på en befintlig replik tar du först bort databasen från tillgänglighets gruppen.

4. Skapa tillgänglighets gruppen genom att använda [guiden Ny tillgänglighets grupp](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) på den server som ska vara värd för den första primära repliken i gruppen. I guiden:

    - På sidan **Välj databas** väljer du databasen för din Configuration Manager webbplats.  

    - På sidan **Ange repliker** konfigurerar du:

        - **Repliker:** Ange de servrar som ska vara värdar för sekundära repliker.

        - **Lyssnare:** Ange **lyssnings-DNS-namnet** som ett fullständigt DNS-namn, till exempel `<listener_server>.fabrikam.com` . När du konfigurerar Configuration Manager att använda databasen i tillgänglighets gruppen, används det här namnet.

    - På sidan **Välj inledande datasynkronisering** väljer du **Fullständig**. När guiden har skapat tillgänglighets gruppen säkerhets kopie ras den primära databasen och transaktions loggen. Sedan återställer guiden dem på varje server som är värd för en sekundär replik.

        > [!Note]  
        > Om du inte använder det här steget återställer du en kopia av plats databasen till varje server som är värd för en sekundär replik. Anslut sedan databasen till gruppen manuellt.

5. Kontrol lera konfigurationen på varje replik:

    1. Kontrol lera att plats serverns dator konto är medlem i den lokala gruppen **Administratörer** på varje dator som är medlem i tillgänglighets gruppen.  

    2. Kör [verifierings skriptet](sql-server-alwayson-for-a-highly-available-site-database.md#prerequisites) för att bekräfta att plats databasen på varje replik är korrekt konfigurerad.

    3. Om det är nödvändigt att ange konfigurationer på sekundära repliker, måste du manuellt växla över den primära repliken till den sekundära repliken innan du fortsätter. Du kan bara konfigurera databasen för en primär replik. Mer information finns i [utföra en planerad manuell redundansväxling av en tillgänglighets grupp](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) i SQL Server-dokumentationen.

6. När alla repliker uppfyller kraven är tillgänglighets gruppen redo att användas med Configuration Manager.


## <a name="configure-a-site-to-use-the-availability-group"></a><a name="bkmk_configure"></a> Konfigurera en plats att använda tillgänglighets gruppen

När du har [skapat och konfigurerat tillgänglighets gruppen](#bkmk_create)använder du Configuration Manager plats underhåll för att konfigurera platsen att använda databasen som tillgänglighets gruppen är värd för.

Det finns inte stöd för att installera en ny plats med dess databas i en tillgänglighets grupp. Om du till exempel använder bas linje medier installerar du platsen med en enda instans av SQL Server. När platsen har installerats flyttar du plats databasen till tillgänglighets gruppen.

1. Kör **Configuration Manager-installationen**: `\BIN\X64\setup.exe` från mappen Configuration Manager plats installation.

2. På sidan **komma igång** väljer du **utför plats underhåll eller Återställ den här platsen**och väljer sedan **Nästa**.

3. Välj **ändra SQL Server konfiguration**och välj sedan **Nästa**.

4. Konfigurera om följande inställningar för plats databasen:

    - **SQL Server namn**: Ange det virtuella namnet för tillgänglighets gruppens *lyssnare*. Du konfigurerade lyssnaren när du skapade tillgänglighets gruppen. Det virtuella namnet ska vara ett fullständigt DNS-namn, till exempel `<Listener_Server>.fabrikam.com` .  

    - **Instans:** Om du vill ange standard instansen för *lyssnaren* för tillgänglighets gruppen måste värdet vara tomt. Om den aktuella plats databasen körs på en namngiven instans rensar du den aktuella namngivna instansen.

    - **Databas:** : Lämna namnet som det är. Det här namnet är den aktuella plats databasen.

5. När du har angett informationen för den nya databas platsen slutför du installationen med din normala process och dina vanliga konfigurationer.


## <a name="synchronous-replica-members"></a><a name="bkmk_sync"></a> Synkrona replik medlemmar  

När plats databasen finns i en tillgänglighets grupp kan du använda följande procedurer för att lägga till eller ta bort synkrona replik medlemmar. Mer information om typen och antalet repliker som stöds finns i konfigurationer för [tillgänglighets grupper](sql-server-alwayson-for-a-highly-available-site-database.md#availability-group-configurations).

### <a name="add-a-new-synchronous-replica-member"></a><a name="bkmk_sync-add"></a> Lägg till en ny medlem i en synkron replik

<!--3127336-->
Från och med version 1906 kör Configuration Manager-installationen för att lägga till en ny synkron replik medlem.

1. Lägg till en sekundär replik med hjälp av SQL Server procedurer.

    1. [Lägg till en sekundär replik i en tillgänglighets grupp som alltid är tillgänglig](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

    1. Se status i SQL Management Studio. Vänta tills tillgänglighets gruppen återgår till full hälsa.

1. Kör Configuration Manager-installationen och välj alternativet för att ändra platsen.

1. Ange namnet på tillgänglighets gruppens lyssnare som databas namnet. Om lyssnaren använder en nätverks port som inte är standard, anger du även det. Den här åtgärden gör att installationen ser till att varje nod är korrekt konfigurerad. Det startar också en databas återställnings process.

Configuration Manager-installationen använder flytt åtgärden för SQL Database och ser till att noderna är korrekt konfigurerade.

Mer information om hur du utför den här processen manuellt i version 1902 eller tidigare finns i [ConfigMgr 1702: lägga till en ny nod (sekundär replik) i en befintlig SQL-Ao AG](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-1702-adding-a-new-node-secondary-replica-to-an/ba-p/339960).

### <a name="remove-a-replica-member"></a>Ta bort en replik medlem

Från och med version 1906 kan du använda Configuration Manager-installationen för att ta bort en replik medlem. Använd samma process för att [lägga till en ny medlem i en synkron replik](#bkmk_sync-add).

Mer information om hur du utför den här processen manuellt i version 1902 eller tidigare finns i [ta bort en sekundär replik från en tillgänglighets grupp](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server).  


## <a name="asynchronous-replicas"></a><a name="bkmk_async"></a> Asynkrona repliker

Du kan använda en asynkron replik i tillgänglighets gruppen som du använder med Configuration Manager. Du behöver inte köra de konfigurations skript som krävs för att konfigurera en synkron replik eftersom en asynkron replik inte stöds för plats databasen.

### <a name="configure-an-asynchronous-commit-replica"></a>Konfigurera en asynkron commit-replik

Mer information finns i [lägga till en sekundär replik i en tillgänglighets grupp](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Använd den asynkrona repliken för att återställa din webbplats

Använd den asynkrona repliken för att återställa plats databasen.

1. Stoppa den aktiva primära platsen för att förhindra ytterligare skrivningar till plats databasen. Om du vill stoppa platsen använder du [verktyget underhåll av hierarki](../../manage/hierarchy-maintenance-tool-preinst.exe.md): `preinst.exe /stopsite`

1. När du har stoppat platsen använder du den asynkrona repliken i stället för en [manuellt återställd databas](../../manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).


## <a name="stop-using-an-availability-group"></a><a name="bkmk_stop"></a> Sluta använda en tillgänglighets grupp

Följ anvisningarna nedan om du inte längre vill ha platsdatabasen i en tillgänglighetsgrupp. Med den här processen flyttar du plats databasen tillbaka till en enda instans av SQL Server.

1. Stoppa Configuration Manager-webbplatsen med hjälp av följande kommando: `preinst.exe /stopsite` . Mer information finns i [verktyget underhåll av hierarki](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Skapa en fullständig säkerhetskopia av databasen från den primära repliken med hjälp av SQL Server. Mer information finns i [skapa en fullständig säkerhets kopia av databasen](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).

3. Använd SQL Server för att återställa säkerhetskopian av platsdatabasen på den server som ska vara värd för platsdatabasen. Mer information finns i [återställa en säkerhets kopia av databasen med SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).

    > [!Note]  
    > Om den primära replik servern för tillgänglighets gruppen kommer att vara värd för den enskilda instansen av plats databasen, hoppar du över det här steget.

4. Ändra säkerhets kopierings modellen för plats databasen från **fullständig** till **enkel**på den server som ska vara värd för plats databasen. Mer information finns i [Visa eller ändra återställnings modellen för en databas](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

5. Kör **Configuration Manager-installationen**: `\BIN\X64\setup.exe` från mappen Configuration Manager plats installation.

6. På sidan **komma igång** väljer du **utför plats underhåll eller Återställ den här platsen**och väljer sedan **Nästa**.  

7. Välj **ändra SQL Server konfiguration**och välj sedan **Nästa**.  

8. Konfigurera om följande inställningar för plats databasen:

    - **SQL Server-namn:** Ange namnet på den server som nu är värd för platsdatabasen.

    - **Instans:** Ange den namngivna instans som är värd för plats databasen. Lämna fältet tomt om databasen finns på standard instansen.

    - **Databas:** : Lämna namnet som det är. Det här namnet är den aktuella plats databasen.

9. När du har angett informationen för den nya databas platsen slutför du installationen med din normala process och dina vanliga konfigurationer. När installationen är klar startas platsen om och börjar använda den nya databas platsen.

10. Om du vill rensa de servrar som var medlemmar i tillgänglighets gruppen följer du rikt linjerna i [ta bort en tillgänglighets grupp](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server).