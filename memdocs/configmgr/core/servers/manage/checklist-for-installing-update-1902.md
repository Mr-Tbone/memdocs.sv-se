---
title: Check lista för 1902
titleSuffix: Configuration Manager
description: Lär dig mer om åtgärder som ska vidtas innan du uppdaterar till Configuration Manager version 1902.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b87ac054-9b37-4725-a3f3-2340cfb10bff
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 150194be4d7d2fa07fb868e9a5f65f52f3bdd768
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723266"
---
# <a name="checklist-for-installing-update-1902-for-configuration-manager"></a>Check lista för att installera uppdatering 1902 för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du använder den aktuella grenen av Configuration Manager kan du installera uppdatering i konsolen för version 1902 för att uppdatera din hierarki från en tidigare version. <!-- baseline only statement:-->(Eftersom version 1902 också är tillgängligt som [bas linje medium](updates.md#bkmk_Baselines)kan du använda installations mediet för att installera den första platsen i en ny hierarki.)

För att hämta uppdateringen för version 1902 måste du använda en tjänst anslutnings punkt på platsen på den översta nivån i hierarkin. Den här plats system rollen kan vara i läget online eller offline. När hierarkin har laddat ned uppdaterings paketet från Microsoft kan du hitta det i-konsolen. I arbets ytan **Administration** väljer du noden **uppdateringar och underhåll** .

-   När uppdateringen är listad som **tillgänglig**är uppdateringen klar att installeras. Innan du installerar version 1902 bör du läsa följande information [om hur du installerar uppdatering 1902](#about-installing-update-1902) och [Check listan](#checklist) för konfigurationer som ska göras innan du startar uppdateringen.

-   Om uppdateringen visas som **hämtning** och inte ändras granskar du **hman. log** och **dmpdownloader. log** för fel.

    -   Dmpdownloader. log kan indikera att dmpdownloader-processen väntar i ett intervall innan den söker efter uppdateringar. Starta om den **SMS_EXECUTIVE** tjänsten på plats servern för att starta om nedladdningen av uppdateringens omdistributions filer.

    -   En annan vanlig hämtnings fråga inträffar när proxyserverinställningar förhindrar nedladdning från `silverlight.dlservice.microsoft.com`, `download.microsoft.com`och `go.microsoft.com`.

Mer information om hur du installerar uppdateringar finns [i uppdateringar och underhåll i konsolen](updates.md#bkmk_inconsole).

Mer information om aktuella gren versioner finns i [bas linje-och uppdaterings versioner](updates.md#bkmk_Baselines).



## <a name="about-installing-update-1902"></a>Om hur du installerar uppdatering 1902

#### <a name="sites"></a>Webbplatser
Du installerar uppdatering 1902 på platsen på den översta nivån i hierarkin. Starta installationen från den centrala administrations platsen eller från den fristående primära platsen. När uppdateringen har installerats på platsen på den översta nivån har de underordnade platserna följande uppdaterings beteende:

-   Underordnade primära platser installerar uppdateringen automatiskt när den centrala administrations platsen har slutfört installationen av uppdateringen. Du kan använda Service Windows för att styra när en plats installerar uppdateringen. Mer information finns i [Service Windows for Site servers](service-windows.md).

-   Uppdatera manuellt varje sekundär plats i Configuration Manager-konsolen när den primära överordnade platsen har slutfört installationen av uppdateringen. Automatisk uppdatering av sekundära plats servrar stöds inte.

#### <a name="site-system-roles"></a>Platssystemroller
När en plats Server installerar uppdateringen uppdaterar den automatiskt alla plats system roller. Dessa roller finns på plats servern eller installeras på fjärrservrar. Innan du installerar uppdateringen måste du kontrol lera att varje plats system Server uppfyller de aktuella kraven för den nya uppdaterings versionen.

#### <a name="configuration-manager-consoles"></a>Configuration Manager-konsoler   
Första gången du använder en Configuration Manager-konsol när uppdateringen är klar uppmanas du att uppdatera konsolen. Du kan också köra installations programmet för Configuration Manager på den dator som är värd för konsolen och välja alternativet för att uppdatera konsolen. Installera uppdateringen till-konsolen så snart som möjligt. Mer information finns i [installera Configuration Manager-konsolen](../deploy/install/install-consoles.md).

> [!IMPORTANT]  
> När du installerar en uppdatering på den centrala administrations platsen bör du vara medveten om följande begränsningar och fördröjningar som finns tills alla underordnade primära platser också Slutför installationen av uppdateringen:    
> - **Klient uppgraderingar** startar inte. Detta inkluderar automatiska uppdateringar av klienter och för produktions klienter. Dessutom kan du inte befordra för produktions klienter till produktion förrän den sista platsen har slutfört installationen av uppdateringen. När den sista platsen har slutfört installationen av uppdateringen börjar klient uppgraderingar utifrån dina konfigurations alternativ.   
> - **Nya funktioner** som du aktiverar med uppdateringen är inte tillgängliga. Detta är att förhindra att data som är relaterade till den funktionen skickas till en plats som ännu inte har installerat stöd för den funktionen. När alla primära platser har installerat uppdateringen kommer funktionen att vara tillgänglig för användning.   
> - **Länkar** mellan den centrala administrations platsen och underordnade primära platser visas som ej uppgraderade. Detta visas i installations status för uppdaterings paketet som status slutförd med varning vid övervakning av replikering av replikering. I noden övervakning i-konsolen visas detta när *länken konfigureras*.


## <a name="checklist"></a>Checklista

#### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>Alla platser kör en version av Configuration Manager som stöds  
Varje plats server i hierarkin måste köra samma version av Configuration Manager innan du kan starta installationen av uppdatering 1902. Om du vill uppdatera till 1902 måste du använda version 1802, 1806 eller 1810.

#### <a name="review-the-status-of-your-product-licensing"></a>Granska statusen för produkt licensen 
Du måste ha ett aktivt Software Assurance-avtal (SA) eller motsvarande prenumerations rättigheter för att installera den här uppdateringen. När du uppdaterar platsen visar **licensierings** sidan alternativet att bekräfta **utgångs datumet för Software Assurance**.

Det här värdet är valfritt. Du kan ange som en bekväm påminnelse om licensens förfallo datum. Datumet visas när du installerar framtida uppdateringar. Du kan ha angett det här värdet tidigare under installationen eller installationen av en uppdatering. Du kan också ange det här värdet i Configuration Manager-konsolen. I arbets ytan **Administration** expanderar du **plats konfiguration**och väljer **platser**. Välj **Inställningar för hierarki** i menyfliksområdet och växla till fliken **licensiering** .

Mer information finns i [licensiering och grenar](../../understand/learn-more-editions.md).

#### <a name="review-microsoft-net-versions"></a>Granska Microsoft .NET versioner 
När en plats installerar den här uppdateringen, om minimi kravet för .NET Framework 4,5 inte är installerad, Configuration Manager installeras automatiskt .NET Framework 4.5.2. När den här förutsättningen inte redan är installerad installerar platsen den på varje server som är värd för någon av följande plats system roller:

-   Hanteringsplats
-   Tjänstanslutningspunkt
-   Registreringsproxyplats
-   Registreringsplats

Den här installationen kan försätta plats system servern i ett väntande tillstånd för omstart och rapportera fel till visnings programmet för Configuration Manager komponent status. Dessutom kan .NET-program på servern uppleva slumpmässiga problem innan servern startas om.

Mer information finns i [krav för plats och plats system](../../plan-design/configs/site-and-site-system-prerequisites.md).

#### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Granska versionen av Windows ADK för Windows 10
Versionen av Windows 10 Assessment and Deployment Kit (ADK) bör stödjas för Configuration Manager version 1902. Mer information om Windows ADK-versioner som stöds finns i [Windows 10 ADK](../../plan-design/configs/support-for-windows-10.md#windows-10-adk). Om du behöver uppdatera Windows ADK måste du göra det innan du påbörjar uppdateringen av Configuration Manager. Den här ordningen ser till att standard start avbildningarna uppdateras automatiskt till den senaste versionen av Windows PE. Uppdatera manuellt anpassade Start avbildningar efter att platsen har uppdaterats.

Om du uppdaterar platsen innan du uppdaterar Windows ADK, se [Uppdatera distributions platser med start avbildningen](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

#### <a name="review-sql-server-native-client-version"></a>Granska SQL Server Native Client version
En lägsta version av SQL Server 2012 Native Client som innehåller stöd för TLS 1,2 måste vara installerad. Mer information finns i [listan över krav kontroller](../deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

#### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>Granska plats-och hierarki status för olösta problem 
En platsuppgradering kan misslyckas på grund av befintliga operativa problem. Innan du uppdaterar en plats löser du alla operativa problem för följande system:  
- Plats servern  
- Plats databas servern  
- Fjärrplatsens system roller på andra servrar   

Mer information finns i [använda aviseringar och status systemet](use-alerts-and-the-status-system.md).

#### <a name="review-file-and-data-replication-between-sites"></a>Granska fil-och datareplikering mellan platser   
Se till att fil-och databasreplikering mellan platser fungerar och är aktuella. Fördröjningar eller efter släpning i kan antingen förhindra en smidig och lyckad uppdatering. För databasreplikering kan du använda funktionen för replikeringslänkanalys för att lösa eventuella fel innan du startar uppdateringen.

Mer information finns i [om Replikeringslänkanalys](monitor-replication.md#BKMK_RLA).

#### <a name="install-all-applicable-critical-windows-updates"></a>Installera alla tillämpliga viktiga Windows-uppdateringar
Innan du installerar en uppdatering för Configuration Manager bör du installera eventuella kritiska uppdateringar för operativ systemet för varje tillämpligt plats system. Dessa servrar omfattar plats servern, plats databas servern och fjärrplatsens system roller. Om en uppdatering som du installerar kräver en omstart måste du starta om de aktuella servrarna innan du påbörjar uppgraderingen.

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Inaktivera databas repliker för hanterings platser på primära platser   
Configuration Manager kan inte uppdatera en primär plats som har en databas replik för hanterings platser aktive rad. Innan du installerar en uppdatering för Configuration Manager inaktiverar du databasreplikering.

Mer information finns i [databas repliker för hanterings platser](../deploy/configure/database-replicas-for-management-points.md).

#### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>Ange SQL Server AlwaysOn-tillgänglighetsgrupper till manuell redundans   
Om du använder en tillgänglighets grupp ser du till att tillgänglighets gruppen är inställd på manuell redundans innan du startar installationen av uppdateringen. När platsen har uppdaterats kan du återställa redundansen till automatisk. Mer information finns i [SQL Server AlwaysOn för en plats databas](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

#### <a name="disable-site-maintenance-tasks-at-each-site"></a>Inaktivera plats underhålls aktiviteter på varje plats
Innan du installerar uppdateringen inaktiverar du alla plats underhålls aktiviteter som kan köras under den tid då uppdaterings processen är aktiv. Till exempel, men inte begränsat till:

-   Platsserver för säkerhetskopiering
-   Ta bort föråldrade klientåtgärder
-   Ta bort föråldrade identifieringsdata

Om en underhållsaktivitet för platsdatabasen körs under installationen av uppdateringen kan installationen av uppdateringen misslyckas. Innan du inaktiverar en aktivitet registrerar du schemat för aktiviteten så att du kan återställa dess konfiguration när uppdateringen har installerats.

Mer information finns i [underhålls aktiviteter](maintenance-tasks.md) och [referens för underhålls aktiviteter](reference-for-maintenance-tasks.md).

#### <a name="temporarily-stop-any-antivirus-software"></a>Stoppa alla antivirus program tillfälligt 
Innan du uppdaterar en plats måste du stoppa antivirus programmet på Configuration Manager-servrarna. Antivirus programmet kan låsa filer som behöver uppdateras vilket gör att vår uppdatering Miss söker. <!--SMS.503481--> 

#### <a name="create-a-backup-of-the-site-database"></a>Skapa en säkerhets kopia av plats databasen 
Innan du uppdaterar en plats säkerhetskopierar du plats databasen på den centrala administrations platsen och de primära platserna. Den här säkerhets kopian säkerställer att du har en lyckad säkerhets kopia som kan användas för haveri beredskap.

Mer information finns i [säkerhets kopiering och återställning](backup-and-recovery.md).

#### <a name="plan-for-client-piloting"></a>Planera för klient pilot   
När du installerar en uppdatering som uppdaterar klienten kan du testa den nya klient uppdateringen i för produktion innan den distribueras och uppgraderar alla dina aktiva klienter. Om du vill utnyttja det här alternativet måste du konfigurera platsen så att den stöder automatiska uppgraderingar för för produktion innan du påbörjar installationen av uppdateringen.

Mer information finns i [Uppgradera klienter](../../clients/manage/upgrade/upgrade-clients.md) och [testa klient uppgraderingar i en för produktions samling](../../clients/manage/upgrade/test-client-upgrades.md).

#### <a name="plan-to-use-service-windows"></a>Planera att använda service fönster   
Om du vill definiera en period under vilken uppdateringar till en plats Server kan installeras använder du Service Windows. De kan hjälpa dig att styra när platser i hierarkin installerar uppdateringen. Mer information finns i [Service Windows for Site servers](service-windows.md).

#### <a name="review-supported-extensions"></a>Granska stödda tillägg
<!--SCCMdocs#587-->
Om du utökar Configuration Manager med andra produkter från Microsoft eller Microsoft-partner, kontrollerar du att produkterna stöder version 1902. Fråga produkt leverantören om den här informationen. Se till exempel [versions information](../../../mdt/release-notes.md)för Microsoft Deployment Toolkit.

#### <a name="run-the-setup-prerequisite-checker"></a>Kör krav kontrollen för installation   
När uppdateringen visas i-konsolen som **tillgänglig** kan du oberoende köra krav kontrollen innan du installerar uppdateringen. (När du installerar uppdateringen på platsen körs krav kontrollen igen.)

Om du vill köra en krav kontroll från konsolen går du till arbets ytan **Administration** och väljer **uppdateringar och underhåll**. Välj uppdaterings paketet **Configuration Manager 1902** och välj **Kör krav kontroll** i menyfliksområdet.

Mer information finns i avsnittet **köra krav kontrollen innan du installerar en uppdatering** i [innan du installerar en uppdatering i konsolen](install-in-console-updates.md#bkmk_beforeinstall).

> [!IMPORTANT]  
> När krav kontrollen körs uppdaterar processen vissa produkt käll filer som används för plats underhålls aktiviteter. När du har kört krav kontrollen men innan du installerar uppdateringen måste du därför köra **setupwpf. exe** (Configuration Manager installationen) från CD: n för att utföra en plats underhålls uppgift. Den senaste mappen på plats servern.

#### <a name="update-sites"></a>Uppdatera platser   
Du är nu redo att starta installationen av uppdateringen för hierarkin. Mer information om hur du installerar uppdateringen finns [i installera uppdateringar i konsolen](install-in-console-updates.md#bkmk_install).

Du kan planera att installera uppdateringen utanför normal kontors tid. Fastställ när processen har minst påverkan på din affärs verksamhet. Installera uppdateringen och dess åtgärder installera om plats komponenter och plats system roller.

Mer information finns i [uppdateringar för Configuration Manager](updates.md).



## <a name="post-update-checklist"></a>Check lista för efter uppdatering

När platsen har uppdaterats använder du följande check lista för att slutföra vanliga uppgifter och konfigurationer.


#### <a name="confirm-version-and-restart-if-necessary"></a>Bekräfta version och omstart (om det behövs)
Kontrol lera att varje plats Server och plats system roll har uppdaterats till version 1902. I-konsolen lägger du till kolumnen **version** i noderna **platser** och **distributions platser** på arbets ytan **Administration** . Vid behov installeras en plats system roll automatiskt om för att uppdatera till den nya versionen. 

Överväg att starta om fjärrplatssystem som inte har uppdaterats först. Granska plats infrastrukturen och kontrol lera att tillämpliga plats servrar och fjärrplatssystem har startats om. Normalt startar plats servrar bara när Configuration Manager installerar .NET som ett krav för en plats system roll.


#### <a name="confirm-site-to-site-replication-is-active"></a>Bekräfta att plats-till-plats-replikering är aktiv
Gå till följande platser i Configuration Manager-konsolen för att visa statusen och se till att replikering är aktiv:  

-   **Monitoring** Arbets ytan övervakning **, noden platshierarki**  

-   Arbets ytan **övervakning** , noden **databasreplikering**  

Mer information finns i följande artiklar:  

- [Övervaka hierarki](monitor-hierarchy.md)
- [Övervaka replikering](monitor-replication.md)
- [Om Replikeringslänkanalys](monitor-replication.md#BKMK_RLA)  


#### <a name="update-configuration-manager-consoles"></a>Uppdatera Configuration Manager-konsoler
Uppdatera alla fjärranslutna Configuration Manager-konsoler till samma version. Du uppmanas att uppdatera konsolen när:  

-   Du öppnar-konsolen.  

-   Du går till en ny nod i-konsolen.  


#### <a name="reconfigure-database-replicas-for-management-points"></a>Konfigurera om databas repliker för hanterings platser
När du har uppdaterat en primär plats kan du konfigurera om databas repliken för hanterings platser som du har avinstallerat innan du uppdaterade platsen. Mer information finns i [databas repliker för hanterings platser](../deploy/configure/database-replicas-for-management-points.md).  


#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Konfigurera om inaktiverade underhålls aktiviteter
Om du har inaktiverat databas [underhålls aktiviteter](maintenance-tasks.md) på en plats innan du installerade uppdateringen konfigurerar du om dessa uppgifter. Använd samma inställningar som på plats före uppdateringen.  


#### <a name="update-clients"></a>Uppdatera klienter
Uppdatera klienter per plan som du har skapat, särskilt om du har konfigurerat klientens pilotering innan du installerade uppdateringen. Mer information finns i [Uppgradera klienter för Windows-datorer](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  


#### <a name="third-party-extensions"></a>Tillägg från tredje part
Om du använder några tillägg för att Configuration Manager måste du uppdatera dem till den senaste versionen för att stödja Configuration Manager version 1902. 


#### <a name="update-custom-boot-images-and-media"></a>Uppdatera anpassade Start avbildningar och media
<!--SCCMDocs issue 775-->

Använd åtgärden **Uppdatera distributions platser** för alla start avbildningar som du använder, oavsett om det är en standard-eller anpassad start avbildning. Den här åtgärden ser till att klienterna kan använda den senaste versionen. Även om det inte finns en ny version av Windows ADK kan Configuration Manager klient komponenterna ändras med en uppdatering. Om du inte uppdaterar start avbildningar och media kan det hända att distributioner av aktivitetssekvensdistributioner Miss lyckas på enheter. 

När du uppdaterar platsen uppdaterar Configuration Manager automatiskt *standard* start avbildningarna. Det uppdaterade innehållet distribueras inte automatiskt till distributions platser. Använd åtgärden **Uppdatera distributions platser** för vissa start avbildningar när du är redo att distribuera det här innehållet i nätverket. 

Uppdatera eventuella *anpassade* start avbildningar manuellt när du har uppdaterat platsen. Den här åtgärden uppdaterar start avbildningen med de senaste klient komponenterna vid behov, laddar om den med den aktuella Windows PE-versionen och distribuerar om innehållet till distributions platserna. 

Mer information finns i [Uppdatera distributions platser med start avbildningen](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image). 
