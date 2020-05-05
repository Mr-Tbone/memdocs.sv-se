---
title: Migrera åtgärder
titleSuffix: Configuration Manager
description: Skapa och Kör jobb för att migrera data och klienter till Configuration Manager aktuella grenen.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a93269fc50c7bb39cd47f10e448d30742fc8ab22
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720921"
---
# <a name="operations-for-migrating-to-configuration-manager-current-branch"></a>Åtgärder för att migrera till Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Vid migrering i Configuration Manager kan du migrera data och klienter när du har samlat in data från en käll plats i en källhierarki som stöds. Använd informationen i följande avsnitt för att skapa och köra migreringsjobb för att migrera data och klienter och slutför sedan migreringsprocessen.  

-   [Skapa och redigera migreringsjobb](#Create_Edit_migration_Jobs)  

-   [Köra migreringsjobb](#Run_Migration_Jobs)  

-   [Uppgradera eller omtilldela en delad distributionsplats](#BKMK_ProcUpgrdSS)  

-   [Övervaka migreringsaktiviteten på arbetsytan Migrering](#Monitor_MIgration)  

-   [Migrera klienter](#BKMK_MigrateClients)  

-   [Slutför migrering](#Complete_Migration)  

##  <a name="create-and-edit-migration-jobs"></a><a name="Create_Edit_migration_Jobs"></a>Skapa och redigera migreringsjobb  
 Använd följande procedurer för att skapa jobb för datamigrering, redigera undantags listan för samlings jobbbaserade migreringsjobb, konfigurera delade distributions platser och redigera scheman för migreringsjobb.  

> [!NOTE]  
>  Följande procedur för att skapa ett migrerings jobb som migreras av samlingar gäller endast för käll-hierarkier som kör en version av Configuration Manager 2007 som stöds. Den samlings migreringen är inte tillgänglig när du migrerar från en System Center 2012 Configuration Manager eller Configuration Manager aktuella gren källhierarkin.  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>Skapa ett migreringsjobb för att migrera utifrån samlingar  

1.  Välj **Administration**i Configuration Manager-konsolen.  

2.  I arbets ytan **Administration** expanderar du **migrering**och väljer sedan **migreringsjobb**.  

3.  På fliken **Start** går du till gruppen **skapa** och väljer **Skapa migreringsjobb**.  

4.  På sidan **Allmänt** i guiden Skapa migreringsjobb ställer du in följande och väljer sedan **OK**:  

    -   Ange ett namn på migreringsjobbet.  

    -   Välj **Migrering av samling** i listrutan **Typ av utskriftsjobb**.  

5.  På sidan **Välj samlingar** ställer du in följande och väljer sedan **Nästa**:  

    -   Välj de samlingar som ska migreras.  

    -   Om du endast vill migrera samlingar och inte de objekt som är associerade med dessa samlingar avmarkerar **du migrera objekt som är associerade med de angivna samlingarna**. Om du avmarkerar det här alternativet migreras inga associerade objekt i det här jobbet och du kan hoppa över steg 6 och 7.  

6.  På sidan **Välj objekt** avmarkerar du alla objekt typer eller vissa tillgängliga objekt som du inte vill migrera. Som standard är alla associerade objekttyper och tillgängliga objekt markerade. Välj **Nästa**.  

7.  På sidan **innehålls ägarskap** tilldelar du ägarskapet för innehållet från varje listad käll plats till en plats i målhierarkin och väljer sedan **Nästa**.  

8.  På sidan **säkerhets omfattning** väljer du en eller flera rollbaserade administrations säkerhets omfattningar som ska tilldelas objekten som ska migreras i det här migreringsjobbet. Välj sedan **Nästa**.  

9. På sidan **samlings begränsning** ställer du in en samling från målhierarkin för att begränsa omfånget för varje listad samling och väljer sedan **Nästa**. Om inga samlingar visas väljer du **Nästa**.  

10. På sidan för att ersätta **plats koder** tilldelar du en platskod från målhierarkin för att ersätta Configuration Manager 2007-plats koden för varje listad samling och väljer sedan **Nästa**. Om inga samlingar visas väljer du **Nästa**.  

11. På sidan **Granska information** väljer du **Spara till fil** för att spara den information som visas för senare visning. När du är redo att fortsätta väljer du **Nästa**.  

12. På sidan **Inställningar** ställer du in när migreringsjobbet ska köras, väljer eventuella ytterligare inställningar som du behöver för migreringsjobbet och väljer sedan **Nästa**.  

13. Bekräfta inställningarna och slutför guiden.  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>Skapa ett migreringsjobb för att migrera med objekt  

1.  Välj **Administration**i Configuration Manager-konsolen.  

2.  I arbets ytan **Administration** expanderar du **migrering**och väljer sedan **migreringsjobb**.  

3.  På fliken **Start** går du till gruppen **skapa** och väljer **Skapa migreringsjobb**.  

4.  På sidan **Allmänt** i guiden Skapa migreringsjobb ställer du in följande och väljer sedan **Nästa**:  

    -   Ange ett namn på migreringsjobbet.  

    -   Välj **Objektmigrering** i listan **Typ av utskriftsjobb**.  

5.  På sidan **Markera objekt** väljer du de objekttyper som ska migreras. Som standard markeras alla tillgängliga objekt för den objekttyp som du väljer.  

6.  På sidan **innehålls ägarskap** tilldelar du ägarskapet för innehållet från varje listad käll plats till en plats i målhierarkin och väljer sedan **Nästa**. Om inga käll platser visas väljer du **Nästa**.  

7.  På sidan **säkerhets omfattning** väljer du en eller flera rollbaserade administrations säkerhets omfattningar som ska tilldelas objekten i det här migreringsjobbet. Välj sedan **Nästa**.  

8.  På sidan **Granska information** väljer du **Spara till fil** för att spara den information som visas för senare visning. När du är redo att fortsätta väljer du **Nästa**.  

9. På sidan **Inställningar** ställer du in när migreringsjobbet ska köras och väljer eventuella ytterligare inställningar som du behöver för migreringsjobbet. Välj sedan **Nästa**.  

10. Bekräfta inställningarna och slutför guiden.  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>Skapa ett migreringsjobb för att migrera ändrade objekt  

1.  Välj **Administration**i Configuration Manager-konsolen.  

2.  I arbets ytan **Administration** expanderar du **migrering**och väljer sedan **migreringsjobb**.  

3.  På fliken **Start** går du till gruppen **skapa** och väljer **Skapa migreringsjobb**.  

4.  På sidan **Allmänt** i guiden Skapa migreringsjobb ställer du in följande och väljer sedan **Nästa**:  

    -   Ange ett namn på migreringsjobbet.  

    -   I list rutan **Jobbtyp** väljer du objekt som har **ändrats efter migreringen**.  

5.  På sidan **Markera objekt** väljer du de objekttyper som ska migreras. Som standard markeras alla tillgängliga objekt för den objekttyp som du väljer.  

6.  På sidan **innehålls ägarskap** tilldelar du ägarskapet för innehållet från varje listad käll plats till en plats i målhierarkin och väljer sedan **Nästa**. Om inga käll platser visas väljer du **Nästa**.  

7.  På sidan **säkerhets omfattning** väljer du en eller flera rollbaserade administrations säkerhets omfattningar som ska tilldelas objekten i det här migreringsjobbet. Välj sedan **Nästa**.  

8.  På sidan **Granska information** väljer du **Spara till fil** för att spara den information som visas för senare visning. När du är redo att fortsätta väljer du **Nästa**.  

9. På sidan **Inställningar** ställer du in när migreringsjobbet ska köras och väljer eventuella ytterligare inställningar som krävs för det här migreringsjobbet. Till skillnad från andra typer av migreringsjobb, måste det här migreringsjobbet skriva över de tidigare migrerade objekten i Configuration Manager databasen. Välj **Nästa**.  

10. Bekräfta inställningarna och slutför sedan guiden.  

###  <a name="modify-the-exclusion-list-for-migration"></a><a name="BKMK_Modify_Exclusion_List"></a>Ändra undantags listan för migrering  

1.  Välj **Administration**i Configuration Manager-konsolen.  

2.  I arbets ytan **Administration** väljer du **migrering** för att få åtkomst till undantags listan. Du kan också komma åt undantagslistan via noden **Källhierarki** eller noden **Migreringsjobb** .  

3.  Välj **Redigera undantags lista**i gruppen **migrering** på fliken **Start** .  

4.  I dialog rutan **Redigera undantags lista** markerar du det exkluderade objekt som du vill ta bort från undantags listan och väljer sedan **ta bort**.  

5.  Spara ändringarna och slutför redigeringen genom att välja **OK** . Om du vill avbryta aktuella ändringar och återställa alla objekt som du har tagit bort, väljer du **Avbryt**och väljer sedan **Nej**. Därmed avbryts borttagningen av objekten och sedan stängs dialogrutan **Redigera undantagslista** .  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>Dela distributions platser från källhierarkin  

1.  Välj **Administration**i Configuration Manager-konsolen.  

2.  I arbets ytan **Administration** expanderar du **migrering**, väljer **källhierarki**och väljer sedan den käll plats som du vill konfigurera.  

3.  På fliken **Start** går du till gruppen **käll plats** och väljer **Konfigurera**.  

4.  I dialog rutan **käll platsens autentiseringsuppgifter** väljer du **Aktivera delning av distributions platser för käll plats servern**och välj sedan **OK**.  

5.  När data insamlingen är klar väljer du **Stäng**.  

#### <a name="change-the-schedule-of-a-migration-job"></a>Ändra schemat för ett migreringsjobb  

1.  Välj **Administration**i Configuration Manager-konsolen.  

2.  I arbets ytan **Administration** expanderar du **migrering**och väljer sedan **migreringsjobb**.  

3.  Välj det migreringsjobb som du vill ändra. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

4.  I egenskaperna för migreringsjobbet väljer du fliken **Inställningar** , ändrar körnings tiden för migreringsjobbet och väljer sedan **OK**.  

##  <a name="run-migration-jobs"></a><a name="Run_Migration_Jobs"></a> Köra migreringsjobb  
 Följ instruktionerna nedan om du vill köra ett migreringsjobb som inte har startats.  


1.  Välj **Administration**i Configuration Manager-konsolen.  

2.  I arbets ytan **Administration** expanderar du **migrering**och väljer sedan **migreringsjobb**.  

3.  Välj det migreringsjobb som du vill köra. Välj **Start**i gruppen **migreringsjobb** på fliken **Start** .  

4.  Välj **Ja** för att starta migreringsjobbet.  

##  <a name="upgrade-or-reassign-a-shared-distribution-point"></a><a name="BKMK_ProcUpgrdSS"></a>Uppgradera eller omtilldela en delad distributions plats  
 Du kan uppgradera en distributions plats som stöds och delas från en Configuration Manager 2007-käll plats (eller omtilldela en distributions plats som stöds och delas från en Configuration Manager käll plats) som en distributions plats i målhierarkin.  

> [!IMPORTANT]  
>  Innan du uppgraderar en Configuration Manager 2007 gren distributions plats måste du avinstallera Configuration Manager 2007-klient program varan från gren distributions plats datorn. Om Configuration Manager 2007-klientprogramvaran installeras när du försöker uppgradera distributions platsen, Miss lyckas uppgraderingen och innehåll som tidigare har distribuerats till gren distributions platsen tas bort från datorn.  

> [!CAUTION]  
>  När du uppgraderar eller omtilldelar en delad distributions plats tas distributions plats system rollen och plats system datorn bort från käll platsen och läggs till som en distributions plats på platsen i målhierarkin som du väljer.  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a>Uppgradera eller omtilldela en delad distributionsplats  

1.  Välj **Administration**i Configuration Manager-konsolen.  

2.  I arbets ytan **Administration** expanderar du **migrering**och väljer sedan **källhierarki**.  

3.  Välj den plats som äger den distributions plats som du vill uppgradera, Välj fliken **delade distributions platser** och välj sedan den tillgängliga distributions plats som du vill uppgradera eller omtilldela.  

4.  På fliken **distributions plats** går du till gruppen **distributions plats** och väljer **omtilldela**.  

5.  Ange inställningar i guiden Omtilldela delad distributions plats som du installerar en ny distributions plats för målhierarkin, med följande tillägg:  

    -   På sidan **innehålls konvertering** granskar du vägledningen om utrymmet som krävs för att konvertera det befintliga innehållet. På sidan **enhets inställningar** i guiden kontrollerar du sedan att den valda distributions plats datorns enhet har tillräckligt mycket ledigt disk utrymme.  

6.  Bekräfta inställningarna och slutför sedan guiden.  

##  <a name="monitor-migration-activity-in-the-migration-workspace"></a><a name="Monitor_MIgration"></a>Övervaka migrerings aktivitet på arbets ytan migrering  
 Använd Configuration Manager-konsolen för att övervaka migreringen.  

1.  Välj **Administration**i Configuration Manager-konsolen.  

2.  I arbets ytan **Administration** expanderar du **migrering**och väljer sedan **migreringsjobb**.  

3.  Välj det migreringsjobb som du vill övervaka.  

4.  Granska detalj- och statusinformation om det valda migreringsjobbet på flikarna **Sammanfattning** och **Objekt i ett jobb**.  

##  <a name="migrate-clients"></a><a name="BKMK_MigrateClients"></a> Migrera klienter  
 När du har migrerat data för klienter mellan hierarkier, men innan du Slutför migreringen, planerar du att migrera klienter till målhierarkin. Migreringen av klienter mellan hierarkier innebär att avinstallera Configuration Manager klient program varan från datorer som är tilldelade till källhierarkin och sedan installera Configuration Manager-klientprogramvaran från målhierarkin. När du installerar klienten från målhierarkin kopplar du även klienten till en primär plats i målhierarkin. Mer information om att migrera klienter finns i [Planera en strategi för klient migrering](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="finish-migration"></a><a name="Complete_Migration"></a>Slutför migrering  
 Använd den här proceduren för att slutföra migreringen från källhierarkin.  

1.  Välj **Administration**i Configuration Manager-konsolen.  

2.  I arbets ytan **Administration** expanderar du **migrering**och väljer sedan **källhierarki**.  

3.  För en Configuration Manager 2007-källhierarki väljer du en käll plats som finns på den nedre nivån i källhierarkin. Välj den tillgängliga käll platsen för en System Center 2012 Configuration Manager eller Configuration Manager aktuell Branch-källhierarki.  

4.  På fliken **Start** går du till gruppen **Rensa** och väljer **sluta samla in data**.  

5.  Bekräfta genom att klicka på **Ja** .  

6.  För en Configuration Manager 2007-källhierarki, innan du fortsätter till nästa steg, upprepar du steg 3, 4 och 5. Gå igenom de här stegen på varje plats i hierarkin, från längst ned i hierarkin till överst. Fortsätt till nästa steg för en System Center 2012 Configuration Manager eller Configuration Manager aktuella gren källhierarkin.  

7.  På fliken **Start** går du till gruppen **Rensa** och väljer **Rensa migrations data**.  

8.  I dialog rutan **Rensa migrerings data** i list rutan **källhierarki** väljer du platskod och plats Server för platsen på den översta nivån i källhierarkin och väljer sedan **OK**.  

9. Välj **Ja** om du vill slutföra migreringsprocessen för källhierarkin.  
