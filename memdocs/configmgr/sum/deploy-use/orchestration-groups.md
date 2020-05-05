---
title: Orchestration-grupper
titleSuffix: Configuration Manager
description: Skapa Orchestration-grupper och distribuera uppdateringar till dem.
ms.date: 04/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cddbebea-b418-4839-b0a8-7809486c8a4c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9a307df23900abb985535b2ab59a5ff172cafb7
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254919"
---
# <a name="orchestration-groups-in-configuration-manager"></a>Orchestration-grupper i Configuration Manager
<!--3098816-->
*Gäller för: Configuration Manager (aktuell gren)*

Från och med Configuration Manager version 2002 kan du skapa Orchestration-grupper. Skapa en Orchestration-grupp för att få bättre kontroll över distributionen av program uppdateringar till enheter. Många Server administratörer måste noggrant hantera uppdateringar för vissa arbets belastningar och automatisera beteenden mellan.

En Orchestration-grupp ger dig flexibiliteten att uppdatera enheter baserat på en procents ATS, ett bestämt nummer eller en explicit ordning. Du kan också köra ett PowerShell-skript före och efter att enheterna har kört uppdaterings distributionen.

Medlemmar i en Orchestration-grupp kan vara alla Configuration Manager-klienter, inte bara servrar. Reglerna för Dirigerings grupper gäller för enheterna för alla program uppdaterings distributioner till en samling som innehåller en medlem i en Orchestration-grupp. Andra distributions beteenden gäller fortfarande. Du kan till exempel underhålla Windows-och distributions scheman.

> [!NOTE]
> I den här versionen av Configuration Manager är Orchestration-grupper en för hands versions funktion. För att aktivera den, se [för hands versions funktioner](../../core/servers/manage/pre-release-features.md).  
>
> **Orchestration Groups** -funktionen är utvecklingen av funktionen [Server grupper](service-a-server-group.md) . En Orchestration-grupp är ett objekt i Configuration Manager.

## <a name="orchestration-group-usage-example"></a>Exempel på dirigerings grupp användning

- Som administratör för program uppdateringar hanterar du alla uppdateringar för din organisation.
- Du har en stor samling för alla servrar och en stor samling för alla klienter. Du distribuerar alla uppdateringar av de här samlingarna.
- SQL-administratörer vill kontrol lera all program vara som är installerad på SQL-servrarna. De vill korrigera fem servrar i en speciell ordning. Den aktuella processen är att manuellt stoppa vissa tjänster innan du installerar uppdateringar, och sedan startar om tjänsterna efteråt.
- Du skapar en Orchestration-grupp och lägger till alla fem SQL-servrar. Du lägger också till för-och efter-skript med hjälp av de PowerShell-skript som tillhandahålls av SQL-administratörerna.
- Under nästa uppdaterings cykel skapar du och distribuerar program uppdateringarna som vanligt till en stor samling servrar. SQL-administratörerna kör distributionen och Orchestration-gruppen automatiserar order och tjänster.

## <a name="prerequisites"></a>Krav

### <a name="site-server-and-permission-prerequisites"></a>Krav för plats Server och behörighet
- Ditt konto måste vara en **Fullständig administratör**för att se alla Orchestration-grupper och uppdateringar för dessa grupper.
   - Rollbaserad administration för Orchestration-grupper är inte tillgänglig.
- Aktivera funktionen **Orchestration Groups** . Mer information finns i [Aktivera valfria funktioner](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
   - När du aktiverar **Orchestration-grupper**inaktiverar platsen funktionen **Server grupper** . Det här beteendet förhindrar konflikter mellan de två funktionerna.

### <a name="client-prerequisites"></a>Klient krav

- Uppgradera mål enheterna till den senaste versionen av Configuration Manager-klienten.
- Medlemmar i en Orchestration-grupp ska tilldelas till samma plats.
- Enheter får inte finnas i fler än en Orchestration-grupp.
   - Enheter som redan finns i en Orchestration-grupp är inte tillgängliga för att väljas när nya medlemmar läggs till.


## <a name="limitations"></a>Begränsningar

- Du kan ha upp till 1000 Orchestration Group-medlemmar.
- Orchestration-grupper fungerar inte i Interoperabilitets läge. Mer information finns i [samverkan mellan olika versioner av Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#bkmk_mixed). <!--6389000-->
- Om uppdateringar initieras av användare från Software Center kringgås dirigeringen. <!--6362887-->

## <a name="server-groups-are-automatically-updated-to-orchestration-groups"></a>Server grupper uppdateras automatiskt till Orchestration-grupper

**Orchestration Groups** -funktionen är utvecklingen av funktionen [Server grupper](service-a-server-group.md) . När du installerar Configuration Manager version 2002 eller senare och du har aktiverat Server grupper flyttas Server grupperna automatiskt till Orchestration-grupper.

## <a name="create-an-orchestration-group"></a>Skapa en Orchestration-grupp

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **Orchestration Group** .

1. I menyfliksområdet väljer du **skapa Orchestration-grupp** för att öppna **guiden skapa Orchestration-grupp**.

1. På sidan **Allmänt** ger du din Orchestration-grupp ett **namn** och eventuellt en **Beskrivning**. Ange värden för följande objekt:
   - **Tids gräns för Orchestration-grupp (i minuter)**: tids gräns för alla grupp medlemmar för att slutföra installationen av uppdateringen.
   - **Tids gräns för Dirigerings grupps medlem (i minuter)**: tids gräns för en enskild enhet i gruppen för att slutföra installationen av uppdateringen.

1. På sidan **medlems val** anger du först **plats koden**. Välj sedan **Lägg till** för att lägga till enhets resurser som medlemmar i den här Orchestration-gruppen. **Sök** efter enheter efter namn och Lägg sedan **till** dem. Du kan också filtrera sökningen till en enda samling med hjälp av **Sök i samling**.  Välj **OK** när du är klar med att lägga till enheter i listan med valda resurser.
   - När du väljer resurser för gruppen visas endast giltiga klienter. Kontroller görs för att verifiera plats koden, att klienten är installerad och att resurserna inte dupliceras.

1. Välj något av följande alternativ på sidan **regel val** :

   - **Tillåt att en procent andel av datorerna uppdateras samtidigt**, Välj eller ange ett nummer för den här procent andelen. Använd den här inställningen för att möjliggöra framtida flexibilitet i storleken på Orchestration-gruppen. Din Orchestration-grupp innehåller till exempel 50 enheter och du anger värdet till 10. Vid en program uppdaterings distribution tillåter Configuration Manager att fem enheter kör distributionen samtidigt. Om du senare ökar storleken på Orchestration-gruppen till 100 enheter uppdateras 10 enheter samtidigt.

   - **Tillåt att ett antal datorer uppdateras samtidigt**, Välj eller ange ett värde för det här antalet. Använd den här inställningen om du alltid vill begränsa till ett angivet antal enheter, oavsett den övergripande storleken på Orchestration-gruppen.

   - **Ange underhålls ordningen**och sortera sedan de valda resurserna i rätt ordning. Använd den här inställningen för att uttryckligen definiera i vilken ordning enheterna ska köra program uppdaterings distributionen.

1. På sidan **före skript** anger du ett PowerShell-skript som ska köras på varje enhet *innan* distributionen körs. Skriptet ska returnera värdet `0` för lyckad eller `3010` för lyckad omstart.

1. På sidan **efter skript** anger du ett PowerShell-skript som ska köras på varje enhet *när* distributionen har körts. Beteendet är i övrigt samma som för-skriptet.

1. Slutför guiden.

> [!WARNING]
> Se till att för skript och post-skript testas innan du använder dem för Orchestration-grupper. För-skript och post-scripts är inte tids gräns och kommer att köras tills Orchestration-gruppens medlems tids gräns har nåtts.

## <a name="view-orchestration-groups-and-members"></a>Visa Orchestration-grupper och-medlemmar

I arbets ytan **till gångar och efterlevnad** väljer du noden **Orchestration Group** . Om du vill visa medlemmar väljer du en Orchestration-grupp och väljer **Visa medlemmar** i menyfliksområdet. Mer information om tillgängliga kolumner för noderna finns i [övervaka Orchestration-grupper och-medlemmar](#bkmk_orch_monitor).

## <a name="edit-or-delete-an-orchestration-group"></a>Redigera eller ta bort en Orchestration-grupp

Om du vill ta bort Orchestration-gruppen markerar du den och klickar sedan på **ta bort** i menyfliksområdet eller på snabb menyn. Om du vill redigera en Orchestration-grupp markerar du den och klickar sedan på **Egenskaper** i menyfliksområdet eller på snabb menyn. Ändra inställningarna från följande flikar:

   - **Allmänt**: 
      - **Namn**: namnet på din Orchestration-grupp
      - **Beskrivning**: Beskrivning av Orchestration-grupp (valfritt)
      - **Tids gräns för Orchestration-grupp (i minuter)**: tids gräns för alla grupp medlemmar för att slutföra installationen av uppdateringen.
      - **Tids gräns för Dirigerings grupps medlem (i minuter)**: tids gräns för en enskild enhet i gruppen för att slutföra installationen av uppdateringen.

  - **Medlems val**:
     - **Platskod**: Platskod för Orchestration-gruppen.
     - **Medlemmar**: Klicka på **Lägg till** för att välja ytterligare enheter för Orchestration-gruppen. Klicka på **ta bort** för att ta bort den valda enheten.

   - **Val av regel**:
      - **Tillåt att en procent andel av datorerna uppdateras samtidigt**, Välj eller ange ett nummer för den här procent andelen. Använd den här inställningen för att möjliggöra framtida flexibilitet i storleken på Orchestration-gruppen. Din Orchestration-grupp innehåller till exempel 50 enheter och du anger värdet till 10. Vid en program uppdaterings distribution tillåter Configuration Manager att fem enheter kör distributionen samtidigt. Om du senare ökar storleken på Orchestration-gruppen till 100 enheter uppdateras 10 enheter samtidigt.
      - **Tillåt att ett antal datorer uppdateras samtidigt**, Välj eller ange ett värde för det här antalet. Använd den här inställningen om du alltid vill begränsa till ett angivet antal enheter, oavsett den övergripande storleken på Orchestration-gruppen.
      - **Ange en underhålls ordning**: sortera de valda resurserna i rätt ordning. Använd den här inställningen för att uttryckligen definiera i vilken ordning enheterna ska köra program uppdaterings distributionen.

   - **Före skript**: 
       - Ange ett PowerShell-skript som körs på varje enhet *innan* distributionen körs. Skriptet ska returnera värdet `0` för lyckad eller `3010` för lyckad omstart.
       
   - **Efter skript**:
      - Ange ett PowerShell-skript som ska köras på varje enhet *när* distributionen har körts. Skriptet ska returnera värdet `0` för lyckad eller `3010` för lyckad omstart.
   > [!WARNING]
   > Se till att för skript och post-skript testas innan du använder dem för Orchestration-grupper. För-skript och post-scripts är inte tids gräns och kommer att köras tills Orchestration-gruppens medlems tids gräns har nåtts.


## <a name="start-orchestration"></a>Starta dirigering

1. [Distribuera program uppdateringar](deploy-software-updates.md) till en samling som innehåller medlemmarna i Orchestration-gruppen.

1. Orchestration startar när en klient i gruppen försöker installera program uppdateringar vid tids gränsen eller under en underhålls period. Den börjar för hela gruppen och kontrollerar att enheterna uppdateras genom att följa reglerna för Orchestration-gruppen.
1. Du kan starta Orchestration manuellt genom att välja den från noden **Orchestration Group** och sedan välja **Starta dirigering** från menyfliksområdet eller snabb menyn.
1. Om en Orchestration-grupp är i ett *felaktigt* tillstånd:
   1. Ta reda på varför dirigeringen misslyckades och Lös eventuella problem.
   1. [Återställ Dirigerings tillstånd för grupp medlemmar](#bkmk_reset).
   1. Från noden **Orchestration-grupp** klickar du på knappen **Starta Orchestration** för att starta om Orchestration.
   [![Starta dirigering](./media/3098816-start-orchestration.png)](./media/3098816-start-orchestration.png#lightbox)


> [!TIP]
> - Orchestration-grupper gäller endast för program uppdaterings distributioner. De gäller inte för andra distributioner.
> - Du kan högerklicka på en medlem i Orchestration-gruppen och välja **Återställ Orchestration Group-medlem**. På så sätt kan du köra Orchestration igen.


## <a name="monitor-orchestration-groups"></a><a name="bkmk_orch_monitor"></a>Övervaka Orchestration-grupper

I arbets ytan **till gångar och efterlevnad** väljer du noden **Orchestration Group** . Lägg till någon av följande kolumner för att få information om grupperna:

- **Orchestration-namn**: namnet på din Orchestration-grupp.
- **Platskod**: plats koden för gruppen.
- **Orchestration-typ**: är en av följande typer:
   - Antal
   - Procent
   - Sequence

- **Orchestration-värde**: hur många medlemmar eller procent andelen av medlemmar som kan få ett lås samtidigt. **Orchestration-värdet** är bara ifyllt när **Orchestration-typen** är antingen *nummer* eller *procent*.  
- **Dirigerings tillstånd**: pågår under dirigering. Inaktiv vid ej pågående.
- **Dirigerings start tid**: datum och tid då dirigeringen startades.
- **Aktuellt ordnings nummer**: anger för vilken medlem i grupp dirigeringen som är aktiv. Det här talet motsvarar **ordnings numret** för medlemmen.  
- **Dirigerings-timeout (i minuter)**: värdet på **tids gränsen för Orchestration-gruppen (i minuter)** som angetts på sidan **Allmänt** när gruppen skapas, eller fliken **Allmänt** när gruppen redige ras.
- **Tids gräns för Dirigerings grupps medlem (i minuter)**: värdet för **tids gräns för Orchestration-gruppmedlemmar (i minuter)** som angetts på sidan **Allmänt** när gruppen skapas, eller fliken **Allmänt** när gruppen redige ras.
- **Orchestration-grupp-ID**: ID för gruppen används ID: t i loggar och databasen.
- **Unikt ID för Orchestration-grupp**: gruppens unika ID, det unika ID: t används i loggar och databasen.

## <a name="monitor-orchestration-group-members"></a>Övervaka medlemmar i Orchestration-gruppen

Välj en Orchestration-grupp i noden **Orchestration Group** . I menyfliksområdet väljer du **Visa medlemmar**. Du kan se medlemmarna i gruppen och deras Dirigerings status. Lägg till någon av följande kolumner för att få information om medlemmarna:

- **Namn**: enhets namnet för Orchestration Group-medlemmen
- **Nuvarande tillstånd**: ger dig statusen för medlems enheten.
   - **Pågår** under dirigeringen.
   - **Väntar**: anger att klienten väntar på att låset ska kunna installera uppdateringar.
   - **Inaktiv** när dirigeringen är klar eller inte körs.
- **Tillstånds kod**: du kan högerklicka på Orchestration-gruppmedlemen och välja **Återställ Orchestration Group-medlem**. Med den här återställningen kan du köra Orchestration igen. Tillstånd är: 
   - Inaktiv
   - Väntar, väntar enheten i sin tur
   - Pågår, installerar en uppdatering
   - Misslyckades
   - Omstart väntar
- **Lås förvärvad tid**: Lås begärs av klienten baserat på principen. När klienten erhåller ett lås utlöses dirigeringen på den.  
-**Senaste status rapporterings tid**: tid då medlemmen senast rapporterade ett tillstånd.
- **Ordnings nummer**: klientens plats i kön för att installera uppdateringar.
- **Platskod**: medlemmens plats kod.
- **Klient aktivitet**: anger om klienten är aktiv eller inaktiv.
- **Primär (a) användare**: vilka användare som är primära för enheten.
- **Klient typ**: vilken typ av enhet klienten är.
- **Inloggad användare**: vilken användare som är inloggad för tillfället på enheten.
- **Og-ID**: ID för Orchestration-gruppen som medlemmen tillhör.
- **Og Unique ID**: unikt ID för Orchestration-gruppen som medlemmen tillhör.
- **Resurs-ID**: resurs-ID för enheten.

## <a name="reset-the-orchestration-state-for-a-group-member"></a><a name="bkmk_reset"></a>Återställa Dirigerings tillstånd för en grupp medlem

Om du vill köra Orchestration på en grupp medlem på nytt kan du rensa dess tillstånd, till exempel *slutfört* eller *misslyckat*. Om du vill ta bort statusen högerklickar du på medlemmar i Orchestration-gruppen och väljer **Återställ Dirigerings grupp medlem**. Du kan också klicka på **Återställ Dirigerings grupp medlem** från menyfliksområdet. Innan du återställer status bör du kontrol lera klienten för att se varför den misslyckades och korrigera eventuella problem som hittas.
   [![Återställ Orchestration Group-medlem](./media/3098816-reset-group-member.png)](./media/3098816-reset-group-member.png#lightbox)

## <a name="log-files"></a>Loggfiler

Använd följande loggfiler på plats servern för att övervaka och felsöka:

### <a name="site-server"></a>Platsserver

- **Policypv. log**: visar att platsen är riktad mot Orchestration-gruppen till klienterna.
- **SMS_OrchestrationGroup. log**: visar beteenden för Orchestration-gruppen.

### <a name="client"></a>Klient

- **MaintenanceCoordinator. log**: visar processen för att låsa hämtningen, uppdatera installationen, för-och efter-skript och låsa publicerings processen.
- **UpdateDeployment. log**: visar installations processen för uppdateringen.
- **Policy. log**: kontrollerar om klienten finns i en Orchestration-grupp.

## <a name="next-steps"></a>Nästa steg

[Distribuera programuppdateringar](deploy-software-updates.md)