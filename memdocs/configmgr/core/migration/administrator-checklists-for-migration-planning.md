---
title: Check listor för migrering
titleSuffix: Configuration Manager
description: Använd administratörs check listor för att hjälpa dig att planera en migrerings strategi till Configuration Manager aktuella grenen.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e406a2b7674815bb3313200ba850baa249f17ebc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718947"
---
# <a name="administrator-checklists-for-migration-planning-in-configuration-manager"></a>Administratörs check listor för planering av migrering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd följande check lista för administratörer för att hjälpa dig att planera din strategi för migrering för att Configuration Manager aktuella grenen.

##  <a name="administrator-checklist-for-migration-planning"></a><a name="Checklist_Migraiton_Planning"></a>Administratörs check lista för migrerings planering  
 Använd följande check lista för planerings stegen före migreringen.  

-   **Bedöm den aktuella miljön:**  

     Identifiera befintliga affärskrav som möts av källhierarkin och utveckla planer för att fortsätta att uppfylla kraven i målhierarkin.  

-   **Granska de funktioner och ändringar som är tillgängliga med den version av Configuration Manager som du använder och Använd den här informationen för att hjälpa dig att utforma målhierarkin:**  

    Mer information finns i [grunderna i Configuration Manager](../../core/understand/fundamentals.md) och vad som [är nytt](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).  


-   **Bestäm vilken administrativ säkerhets modell som ska användas för rollbaserad administration:**  

    Mer information finns i [grunderna i rollbaserad administration för Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   **Utvärdera din nätverks-och Active Directory topologi:** Granska din befintliga domän struktur och nätverkstopologi och Överväg hur detta påverkar hierarkins design-och migreringsåtgärder.  

-   **Slutför din målhierarkiutformning:**  

    Bestäm placeringen av en central administrationsplats, primära platser, sekundära platser och distributionsalternativ för innehåll.  

-   **Mappa hierarkin till de datorer som du ska använda för platser och platsservrar i målhierarkin:**  

    Identifiera de datorer som platser och plats system servrar ska använda i målhierarkin och se till att de har tillräcklig kapacitet för att uppfylla befintliga och framtida drift krav.  

-   **Planera din objektmigreringsstrategi:**  

    Planera att använda tillgängliga migreringsjobb för att migrera olika objekt, inklusive plats gränser, samlingar, annonser och distributioner. Mer information finns i [typer av migreringsjobb](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration) i [Planera en jobb strategi för migrering](../../core/migration/planning-a-migration-job-strategy.md)  

    Configuration Manager migrerar endast de objekt som du väljer. Alla objekt som inte migreras och som krävs i målhierarkin måste återskapas i målhierarkin.  

    Objekt som kan migreras visas när du konfigurerar migreringsjobb.  

-   **Planera din klientmigreringsstrategi:**  

    Planera att migrera klienter genom att använda en styrd metod som begränsar nätverksbandbredden och serverns bearbetningskrav när du migrerar klienter till målhierarkin. Mer information om hur du planerar en strategi för klientmigrering finns i [Planera en strategi för klient migrering](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Planera för inventerings- och efterlevnadsdata:**  

    Configuration Manager stöder inte migrering av maskin varu inventering, program varu inventering eller Desired Configuration Management-kompatibilitetsstatus för program uppdateringar eller klienter.  

    Istället skickar klienten den här informationen till den tilldelade platsen efter att klienten har migrerat till sin nya plats i målhierarkin och har tagit emot principen för de här konfigurationerna. Den här åtgärden fyller i aktuella inventerings- och efterlevnadsdata i målplatsdatabasen.  

-   **Planera för att slutföra migreringen från källhierarkin:**  

    Besluta när objekt och klienter ska migreras. När migreringen har slutförts kan du planera att ställa av platsservrarna i källhierarkin.  

##  <a name="administrator-checklist-for-hierarchy-migration"></a><a name="Checklist_Hierarchy_for_migration"></a>Administratörs check lista för Hierarchy-migrering  
Använd följande checklista för att planera en målhierarki innan du påbörjar migreringen.  

-   **Identifiera vilka datorer som ska användas i målhierarkin:**  

    Configuration Manager har inte stöd för en uppgradering på plats från Configuration Manager 2007-infrastruktur. I stället använder du migrering för att flytta data från Configuration Manager 2007 till Configuration Manager aktuella grenen. Detta kräver att du använder en sida vid sida-distribution och installerar Configuration Manager på nya datorer.  

    När du migrerar från en annan Configuration Manager-hierarki måste du också installera en ny målnod som är en sida-vid-sida-distribution till källhierarkin.  

-   **Skapa målhierarkin:**  

    För att förbereda för migrering installerar och konfigurerar du en Configuration Manager målhierarkin som innehåller en primär plats. Ett exempel:  

    -   Installera en central administrations plats och installera minst en underordnad primär.  

    -   Installera en fristående primär plats om du inte planerar att använda en central administrations plats.  

-   **Om du vill migrera information som är relaterad till programuppdateringar konfigurerar du en programuppdateringsplats i målhierarkin och synkroniserar programuppdateringarna:**  

    Du måste konfigurera och synkronisera programuppdateringar i målhierarkin innan du kan migrera programuppdateringsinformation från källhierarkin.  


-   **Installera och konfigurera ytterligare platssystemroller i målhierarkin:**  

    Konfigurera ytterligare plats system roller och plats system som du behöver.  

-   **Kontrol lera operativa funktioner i målhierarkin:**  

    Kontrollera följande:  

    -   Om målhierarkin innefattar flera platser, bekräfta att databasreplikeringen fungerar mellan platserna. Databasreplikering gäller inte för fristående primära platser.  

    -   Kontrol lera att alla installerade plats system roller fungerar.  

    -   Kontrol lera att de Configuration Manager-klienter som du installerar i målhierarkin kan kommunicera med sin tilldelade plats.  


##  <a name="administrator-checklist-for-migration"></a><a name="Checklisit_Migration"></a>Administratörs check lista för migrering  
Använd följande checklista för att migrera data från källhierarkin till målhierarkin.  

-   **Aktivera migrering i målhierarkin:**  

    Konfigurera en källhierarki genom att ange platsen på den översta nivån i källhierarkin. Mer information om hur du anger käll platsen finns i [Planera en käll-hierarki-strategi](../../core/migration/planning-a-source-hierarchy-strategy.md).  

-   **När källhierarkin kör Configuration Manager 2007 SP2 väljer du och konfigurerar ytterligare platser i källhierarkin:**  

    För varje ytterligare plats i den Configuration Manager 2007 SP2-källhierarkin som du vill samla in data från måste du konfigurera autentiseringsuppgifter för data insamling. När du konfigurerar varje käll plats börjar data insamlings processen omedelbart och fortsätter under migreringen tills du avslutar data insamlingen för platsen. Data insamling säkerställer att du kan migrera objekt från källhierarkin som uppdateras eller läggs till efter en tidigare data insamlings process.

    > [!NOTE]  
    >  När källhierarkin kör System Center 2012 Configuration Manager eller senare behöver du inte konfigurera ytterligare käll platser.  

-   **Konfigurera distributionsplatsresurser:**  

    Du kan dela distributionsplatser mellan de båda hierarkierna för att göra innehåll för objekt som du vill migrera tillgängligt för klienter i målhierarkin. Detta säkerställer att samma innehåll är tillgängligt för klienter i båda hierarkierna och att du kan underhålla det här innehållet tills du slutar att samla in data och Slutför migreringen.  

    Information om delade distributions platser finns i [dela distributions platser mellan käll-och målhierarkin](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) i [Planera en strategi för migrering av innehålls distributioner](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Skapa och kör migreringsjobb för att migrera objekt som är förknippade med klienterna i källhierarkin:**  

    Skapa migreringsjobb för att migrera objekt mellan hierarkierna. De nödvändiga konfigurationerna för varje migreringsjobb kan variera beroende på vilka data som jobbet migrerar.  

    När du migrerar innehåll måste du till exempel, oavsett vilket migreringsjobb du använder, tilldela en plats i målhierarkin för egen hantering av innehållet. Den tilldelade platsen öppnar den ursprungliga källfilplatsen för innehållet och ansvarar för att distribuera innehållet till distributionsplatser i målhierarkin.  

    Mer information finns i [skapa och redigera migreringsjobb för Configuration Manager](../../core/migration/operations-for-migration.md#Create_Edit_migration_Jobs) i [åtgärder för att migrera till Configuration Manager aktuella grenen](../../core/migration/operations-for-migration.md).  

-   **Migrera klienter till målhierarkin:**  

    Processen för klientmigrering beror på ditt migreringsscenario:  

    -   När du migrerar klienter som har en klient version som inte är samma som målhierarkin, måste du uppgradera klient programmet. Uppgraderingen kräver att den aktuella Configuration Manager klienten tas bort, följt av installationen av den nya klient versionen som matchar mål platsen.  

    -   När du migrerar klienter som har en annan klientversion som matchar versionen i målhierarkin måste uppgraderas eller ominstalleras inte klienten. Klienter omtilldelas istället till en primär plats i målhierarkin.  

    När du migrerar en klient till målhierarkin förknippas klienten med dess data som du tidigare migrerade till den aktuella målhierarkin.  

    Mer information finns i [Planera en strategi för klient migrering](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Uppgradera eller omtilldela delade distributionsplatser:**  

    När du inte längre behöver ha stöd för klienter i källhierarkin kan du uppgradera delade distributions platser från en Configuration Manager 2007-käll plats eller omtilldela delade distributions platser från ett System Center 2012 Configuration Manager eller Configuration Manager aktuella gren käll platsen. När du uppgraderar eller omtilldelar en distributionsplats överförs platssystemrollen till en primär plats i målhierarkin och distributionsplatsen avlägsnas från källplatsen i källhierarkin. När du uppgraderar eller omtilldelar en delad distributions plats kvarstår innehållet på distributions plats datorn och du behöver inte omdistribuera innehållet till nya distributions platser i målhierarkin.  

    Du kan också uppgradera en distributions plats som är samordnad på en Configuration Manager 2007 sekundär plats Server. Detta tar bort den sekundära platsen och leder till endast en distributionsplats i målhierarkin.  

    Information om delade distributions platser finns i [dela distributions platser mellan käll-och målhierarkin](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) i [Planera en strategi för migrering av innehålls distributioner](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Slutför migreringen:**  

    När du har migrerat data och klienter från alla platser i källhierarkin och du har uppgraderat tillämpliga distributions platser kan du slutföra migreringen. För att slutföra migreringen slutar du att samla in data för varje käll plats i källhierarkin. Du kan därefter ta bort migreringsinformation som du inte behöver och ställa av din källhierarkis infrastruktur. Mer information finns i [Planera för att slutföra migreringen](../../core/migration/planning-to-complete-migration.md).  
