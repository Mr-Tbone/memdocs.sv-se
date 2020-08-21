---
title: Funktioner i Technical Preview 1511
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1511.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 59d343d09f827edec5db0dd5302c75c00a0c8455
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694516"
---
# <a name="capabilities-in-technical-preview-1511-for-configuration-manager"></a>Funktioner i Technical Preview 1511 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1511. Den här versionen är en bas linje installation för den tekniska för hands versionen som du kan använda för att installera en ny Technical Preview-webbplats eller uppgradera från en tidigare version av Technical Preview.   Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.  

Följande är nya funktioner som du kan prova med den här versionen.  

##  <a name="integration-with-windows-update-for-business-in-windows-10"></a><a name="BKMK_WUfB"></a> Integrering med Windows Update för företag i Windows 10  
 Configuration Manager kan nu skilja en Windows 10-dator som är direkt ansluten via Windows Update for Business (WUfB) jämfört med de som är anslutna till WSUS för att hämta uppdateringar och uppgraderingar för Windows 10.  För datorer som är anslutna via WUfB kan uppdateringar och uppgraderingar hanteras på takt som anges av en administrativ användare via grup principer eller MDM-principer och dessa uppdateringar/uppgraderingar kan installeras direkt från WUfB.    
För datorer som är anslutna via WUfB kommer Configuration Manager inte att kunna rapportera om kompatibilitetsstatus (inklusive Windows-uppdateringar eller definitions uppdateringar). Configuration Manager kommer heller inte att kunna distribuera Microsoft-uppdateringar eller uppdateringar från tredje part till dessa datorer.  

 **Krav för det här scenariot:**  

-   Windows 10 Desktop Pro eller Windows 10 Enterprise Edition version 1511 eller senare  

-   Datorer som ska hanteras via [Windows Update för företag](/windows/deployment/update/waas-manage-updates-wufb).  

### <a name="try-it-out"></a>prova!  
 Försök att utföra följande uppgift och Använd sedan feedback-informationen nära överst i det här avsnittet för att berätta för oss hur det fungerade:  

1.  Inaktivera Windows Update-agenten så att den inte genomsöker mot WSUS, om den har aktiverats tidigare.   
    Register nyckeln **HKEY_LOCAL_MACHINE \software\policies\microsoft\windows\windowsupdate\au\usewsusserver** kan anges för att indikera om datorn genomsöks mot WSUS eller Windows Update.  När värdet är 2 genomsöker den inte mot WSUS.  

2.  Anteckna det nya attributet **UseWUServer**under noden **Windows Update** i Configuration Manager Resursläsaren.  

3.  Skapa en samling som bygger på attributet **UseWUServer** för alla datorer som är anslutna via WUfB för uppdateringar och uppgraderingar.  

4.  Skapa en klientagentinställning för att inaktivera arbetsflödet för programvaruuppdatering och distribuera inställningen till den samling med datorer som är anslutna direkt till WUfB.  

5.  De datorer som hanteras via WUfB visas som **okända** i kompatibilitetsstatus och räknas inte som en del av den övergripande kompatibiliteten i procent.  

##  <a name="managing-office-365-proplus-client-update-through-configuration-manager"></a><a name="BKMK_Office365ProPlus"></a> Hantera Office 365 ProPlus-klient uppdatering via Configuration Manager  
 Configuration Manager har nu möjlighet att hantera uppdateringar för Office 365 Desktop-klienter med hjälp av Configuration Manager hantering av programuppdateringar-arbetsflöde.    
När Microsoft publicerar en ny uppdatering för Office 365-skrivbordet till WSUS (Windows Server Update Services), kommer Configuration Manager att kunna synkronisera uppdateringen till sin katalog om Office 365-uppdateringen har kon figurer ATS att ingå i katalog synkroniseringen.  Plats servern för Configuration Manager hämtar Office 365-klient uppdateringarna och distribuerar paketet till Configuration Manager distributions platser.  Den Configuration Manager klienten informerar sedan Office 365 Desktop-klienter där uppdateringarna ska hämtas och när installations processen för uppdateringen startas.  

**Krav för det här scenariot:**  

### <a name="try-it-out"></a>prova!  
 Försök att utföra följande uppgift och Använd sedan feedback-informationen nära överst i det här avsnittet för att berätta för oss hur det fungerade:  

1. Du kan synkronisera Office 365-uppdateringar till Configuration Manager plats Server och visa dem från Configuration Manager-konsolen.  

2. Du kan godkänna och distribuera Office 365-uppdateringar.  

3. Du kan hämta och installera Office 365-uppdateringar till klienter.  

4. Du kan kontrol lera efterlevnaden för Office 365-uppdateringar med hjälp av övervakning eller rapporter i konsolen.  

   Detaljerade anvisningar finns i [Hantera Office 365-klient uppdateringar med Configuration Manager Technical Preview](/deployoffice/manage-microsoft-365-apps-updates-configuration-manager).  

##  <a name="support-for-sql-server-alwayson-for-highly-available-databases"></a><a name="BKMK_AlwasyOn"></a> Stöd för SQL Server AlwaysOn för databaser med hög tillgänglighet  
 Configuration Manager har nu stöd för att använda en SQL Server AlwaysOn-tillgänglighetsgrupper som värd för plats databasen.  När du installerar en ny plats kan du direkt konfigurera installationen att använda tillgänglighets gruppen i stället för en normal instans av SQL Server.  

> [!NOTE]  
>  Lyckad konfiguration och användning av tillgänglighets grupper kräver att du är van att konfigurera SQL Server tillgänglighets grupper och förlitar sig på dokumentation och procedurer som finns i SQL Server-dokumentations biblioteket.  

Hög nivå processen för att konfigurera och använda tillgänglighets grupper innehåller:  

1.  Konfigurera tillgänglighets gruppen i SQL Server.  

2.  Installera en ny Configuration Manager plats och under installationen dirigerar du platsen till att använda tillgänglighets gruppen genom att ange gruppens slut punkt.  

**Krav för det här scenariot:**  

-   Kräver en version av SQL Server som stöds av Configuration Manager Technical Preview  

-   Du måste skapa och konfigurera SQL Server tillgänglighets grupp innan du installerar Configuration Manager  

-   Tillgänglighetsgruppen måste ha en primär replik och kan ha upp till två samtidiga sekundära repliker  

-   Tillgänglighets gruppen måste ha minst en slut punkt  

-   Du måste ha en nätverks plats som varje SQL Server i tillgänglighets gruppen har åtkomst till. Den här platsen används av installations programmet när du konfigurerar tillgänglighets gruppen och kan tas bort när installationen är klar.  

**Kända problem för den här versionen:**  

-   Det går inte att lägga till en ny replik medlem i en tillgänglighets grupp som redan används som plats databas. I stället måste du installera om platsen när den nya replik medlemmen har lagts till.  

-   I det här scenariot kan du behöva installera **SQL Server 2012 Native Client** ([från SQL Server 2012 Feature Pack](https://www.microsoft.com/download/details.aspx?id=29065)) på hanterings plats servern. Detta förhindrar SQL-anslutningsfel (som loggas i **mp_getauth. log** på hanterings plats servern).  

### <a name="try-it-out"></a>prova!  
Försök att utföra följande uppgifter och Använd sedan feedback-informationen nära överst i det här avsnittet för att berätta för oss hur de fungerade:  

-   Jag kan installera en primär plats som använder en databas server som kon figurer ATS för SQL AlwaysOn-tillgänglighetsgrupper  

-   Det gick inte att redundansväxla min SQL AlwaysOn-tillgänglighetsgruppen till en ny replik i gruppen och den primära platsen fortfarande fungerar  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>Konfigurera SQL Server AlwaysOn för Configuration Manager  
 Använd följande procedurer för att först skapa och konfigurera tillgänglighets gruppen och sedan installera en ny Configuration Manager-plats som använder tillgänglighets gruppen.  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>Så här skapar du en SQL Server AlwaysOn-tillgänglighetsgruppen  
Processen för att [skapa en SQL Server tillgänglighets grupp](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-ver15) dokumenteras i SQL Server-dokumentations biblioteket.  När du skapar tillgänglighets gruppen ser du till att följande krav för användning med Configuration Manager är uppfyllda:  

-   Högst tre medlemmar:  

    -   En primär replik och upp till två sekundära repliker  

    -   Sekundära repliker måste vara synkrona.  

        > [!TIP]  
        >  Vi rekommenderar att sekundära repliker konfigureras för att vara skrivskyddade. På så sätt kan du använda en sekundär replik för funktioner som rapportering och samtidigt bibehålla prestanda för den primära repliken för plats åtgärder.  

-   Minst en slut punkt. Det virtuella namnet för den här slut punkten kommer att användas när du installerar Configuration Manager-platsen.  

    > [!TIP]  
    >  Även om gruppen kan innehålla flera slut punkter kan Configuration Manager bara använda en.  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>Installera en Configuration Manager-plats som använder tillgänglighets gruppen  
Installera en plats som använder en SQL Server tillgänglighets grupp:  

1.  Ersätt följande när du uppmanas att göra det Configuration Manager installationen:  

    -   **SQL Server namn**: Ange det virtuella namnet för den slut punkt som du konfigurerade när du skapade tillgänglighets gruppen. Det virtuella namnet ska vara ett fullständigt DNS-namn, t ** &lt; \> . ex. endpointServer. fabrikam.com**.  

    -   **Instans**: det här värdet ska vara tomt. Det finns ingen instans i den här konfigurationen.  

    -   **Databas**: Ange namnet på databasen som du skapade på den primära repliken av tillgänglighets gruppen.  

2.  Därefter måste du ange en nätverks plats som varje SQL Server i gruppen kan komma åt:  

    -   Dator kontot och tjänst kontot från varje SQL Server måste ha fullständig behörighet till den här platsen.  

    -   Den här platsen används endast under installationen och kan tas bort från delningen eller tas bort när installationen är klar och platsen har installerats.  

3.  När du har angett den här informationen slutför du installationen med din normala process och dina vanliga konfigurationer.  

##  <a name="service-a--server-cluster"></a><a name="BKMK_ClusterServerUpdates"></a> Underhålla ett Server kluster  
Nu kan du skapa en samling som innehåller servrar i ett kluster och sedan konfigurera de kluster inställningar som ska användas när du distribuerar uppdateringar till klustret. Du kan styra den procent andel av servrar som är online vid en viss tidpunkt, samt konfigurera PowerShell-skript för för distribution och efter distribution för att köra anpassade åtgärder.  

**Kända problem för den här versionen:**  

-   Det går inte att kontrol lera statusen för distribution av program uppdateringar för kluster servrar.  

-   Alternativet underhålls ordning på sidan **kluster inställningar** är inaktiverat och inte tillgängligt i den här versionen.  

### <a name="try-it-out"></a>prova!  
Försök att utföra följande uppgift och Använd sedan feedback-informationen nära överst i det här avsnittet för att berätta för oss hur det fungerade:  

-   Jag kan skapa en samling som representerar ett kluster med servrar. För det här testet kan du konfigurera insamlade medlemskaps regler så att de har två datorer i den här samlingen.  

-   Jag kan ange att endast 50% av servrar i klustret kan vara offline när som helst i kluster underhåll. Använd exempel skripten i proceduren för att ange skript för för distribution och efter distribution.  

-   Distribuera en uppdatering i den här samlingen. Granska start.txt och end.txt filer i C:\Temp och kontrol lera start-och slut tider för distributionen på servrarna i klustret. Se filen UpdatesDeployment. log för mer information.  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>Så här skapar du en samling för ett Server kluster  

1.  [Skapa en enhets samling](../clients/manage/collections/create-collections.md) som innehåller servrarna i klustret.  

2.  I arbets ytan **till gångar och efterlevnad** klickar du på **enhets samlingar**, högerklickar på den samling som innehåller servrarna i klustret och klickar sedan på **Egenskaper**.  

3.  På fliken **Allmänt** väljer du **alla enheter tillhör samma Server kluster**och klickar sedan på **Inställningar**.  

4.  På sidan **kluster inställningar** väljer du den procent andel av servrar som kan tas offline samtidigt som program uppdateringarna ska installeras. En kluster Server kan tas offline i taget, oavsett procent andelen som du anger. Configuration Manager avrundas nedåt när du väljer hur många servrar som ska betjänas på en gång. Om du till exempel väljer 51% och det finns 4 servrar i klustret, kommer 2 servrar att tas offline på samma tid.  

5.  Ange om du vill använda ett skript för för distribution (Node dränering) eller efter distribution (Node Resume).  

    > [!TIP]  
    >  Följande är exempel som du kan använda vid testning av skript för för distribution och efter distribution som skriver den aktuella tiden till en textfil:  
    >   
    >  **Före distribution**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Efter distributionen**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>Distribuera program uppdateringar till Server klustret  

1.  [Distribuera program uppdateringar](../../sum/deploy-use/deploy-software-updates.md) till Server kluster samlingen.  

2.  [Övervaka program uppdaterings distributionen](../../sum/deploy-use/monitor-software-updates.md).