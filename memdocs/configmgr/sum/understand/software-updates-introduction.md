---
title: Introduktion till programuppdateringar
titleSuffix: Configuration Manager
description: Lär dig grunderna i program uppdateringar i Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 10/30/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9778b13-c8a3-40eb-8655-34ac8ce9cdaa
ms.openlocfilehash: bd384edafd6464073b33a593a56bc88ba2fb0b87
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906769"
---
# <a name="introduction-to-software-updates-in-configuration-manager"></a>Introduktion till program uppdateringar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Program uppdateringar i Configuration Manager innehåller en uppsättning verktyg och resurser som kan hjälpa dig att hantera den komplexa uppgiften att spåra och tillämpa program uppdateringar på klient datorer i företaget. En effektiv process för hantering av programuppdateringar är nödvändig för att upprätthålla effektiv drift, klara av säkerhetsproblem och hålla nätverksinfrastrukturen stabil. Men på grund av teknikens föränderliga natur och den kontinuerliga framväxten av nya säkerhetshot, kräver effektiv hantering av programuppdateringar konsekvent, kontinuerlig uppmärksamhet.  

Ett exempel scenario som visar hur du kan distribuera program uppdateringar i din miljö finns i [exempel scenario för att distribuera säkerhets program uppdateringar](../deploy-use/example-scenario-deploy-monitor-monthly-security-updates.md).  

##  <a name="software-updates-synchronization"></a><a name="BKMK_Synchronization"></a>Synkronisering av program uppdateringar  
 Synkronisering av program uppdateringar i Configuration Manager ansluter till Microsoft Update för att hämta metadata för program uppdateringar. Platsen på den översta nivån (den centrala administrations platsen eller en fristående primär plats) synkroniseras med Microsoft Update enligt ett schema eller när du startar synkroniseringen manuellt från Configuration Manager-konsolen. När Configuration Manager Slutför synkroniseringen av program uppdateringar på platsen på den översta nivån, börjar synkroniseringen av program uppdateringar på underordnade platser, om de finns. När synkroniseringen är klar på alla primära eller sekundära platser skapas en platsomfattande princip som tillhandahåller placeringen för programuppdateringsplatserna till klientdatorerna.  

> [!NOTE]  
>  Som standard är programuppdateringar aktiverade i klientinställningarna. Men om du anger klientinställningen **Aktivera programvaruuppdateringar på klienter** till **Nej** för att inaktivera programuppdateringar för en samling eller i standardinställningarna, skickas placeringen för programuppdateringsplatserna inte till de associerade klienterna. Mer information finns i [klient inställningar för program uppdateringar](../../core/clients/deploy/about-client-settings.md#software-updates).  

 När klienten har hämtat principen startar klienten en genomsökning för kompatibilitet med programuppdateringarna och skriver informationen till WMI (Windows Management Instrumentation). Kompatibilitetsinformationen skickas sedan till hanteringsplatsen, som sedan skickar informationen till platsservern. Mer information om kompatibilitetsutvärdering finns i [Software updates compliance assessment](#BKMK_SUMCompliance) i det här ämnet.  

 Du kan installera flera programuppdateringsplatser på en primär plats. Den första programuppdateringsplatsen du installerar konfigureras som synkroniseringskälla. Detta synkroniseras från Microsoft Update eller en WSUS-server som inte är i din Configuration Manager-hierarki. De övriga programuppdateringsplatserna på platsen använder den första programuppdateringsplatsen som synkroniseringskälla.  

> [!NOTE]  
>  När synkroniseringen av programuppdateringar är klar på platsen på den högsta nivån, replikeras metadata för programuppdateringar till underordnade platser med databasreplikering. När du ansluter en Configuration Manager-konsol till den underordnade platsen Configuration Manager visar metadata för program uppdateringar. Men tills du har installerat och konfigurerat en program uppdaterings plats på platsen kommer klienterna inte att söka efter kompatibilitet med program uppdateringar, klienter rapporterar inte kompatibilitetsinformation till Configuration Manager och du kan inte distribuera program uppdateringar.  

### <a name="synchronization-on-the-top-level-site"></a>Synkronisering på platsen på den högsta nivån  
 Synkroniseringen av programuppdateringar på platsen på den högsta nivån hämtar de metadata för programuppdateringar från Microsoft Update som uppfyller de villkor du angett i egenskaperna för komponenten programuppdatering. Du konfigurerar bara villkoren på platsen på den högsta nivån.  

> [!NOTE]  
>  Du kan ange en befintlig WSUS-server som inte finns i Configuration Manager-hierarkin i stället för Microsoft Updates som synkroniserings källa.  

 Följande lista beskriver de grundläggande stegen i synkroniseringsprocessen på platsen på den högsta nivån.  

1.  Synkroniseringen av programuppdateringar startar.  

2.  Synkroniseringshanteraren för WSUS skickar en begäran till WSUS som körs på programuppdateringsplatsen om att starta synkroniseringen med Microsoft Update.  

3.  Metadata för programuppdateringarna synkroniseras från Microsoft Update, och eventuella ändringar infogas eller uppdateras i WSUS-databasen.  

4.  När synkroniseringen är färdig synkroniserar WSUS Synchronization Manager program uppdateringarnas metadata från WSUS-databasen till Configuration Manager databasen, och eventuella ändringar efter den senaste synkroniseringen infogas eller uppdateras i plats databasen. Metadata för programuppdateringen lagras i platsdatabasen som ett konfigurationsobjekt.  

5.  Konfigurationsobjekten för programuppdateringen skickas till underordnade platser med databasreplikering.  

6.  När synkroniseringen är klar skapas statusmeddelandet 6702 i WSUS Synkroniseringshanteraren.  

7.  Synkroniseringshanteraren för WSUS skickar en synkroniseringsbegäran till alla underordnade platser.  

8.  Synkroniseringshanteraren för WSUS skickar en begäran i taget till WSUS som körs på andra programuppdateringsplatser på platsen. WSUS-servrarna på de andra programuppdateringsplatserna har konfigurerats att vara repliker av WSUS som körs på platsens standardprogramuppdateringsplats.  

### <a name="synchronization-on-child-primary-and-secondary-sites"></a>Synkronisering för underordnade primära och sekundära platser  
 Under synkroniseringen av programuppdateringar på platsen på den högsta nivån, replikeras konfigurationsobjekt för programuppdateringar till underordnade platser med databasreplikering. I slutet av processen skickar platsen på den högsta nivån en synkroniseringsbegäran till den underordnade platsen, och den underordnade platsen startar WSUS-synkroniseringen. Följande lista beskriver de grundläggande stegen i synkroniseringsprocessen på en underordnad primär eller sekundär plats.  

1.  Synkroniseringshanteraren för WSUS tar emot en synkroniseringsbegäran från platsen på den högsta nivån.  

2.  Synkroniseringen av programuppdateringar startar.  

3.  Synkroniseringshanteraren för WSUS skickar en begäran till WSUS som körs på programuppdateringsplatsen om att starta synkroniseringen.  

4.  WSUS som körs på programuppdateringsplatsen på den underordnade platsen uppdaterar metadata från WSUS som körs på programuppdateringsplatsen på den överordnade platsen.  

5.  När synkroniseringen är klar skapas statusmeddelandet 6702 i WSUS Synkroniseringshanteraren.  

6.  Från en primär plats skickar Synkroniseringshanteraren för WSUS en synkroniseringsbegäran till eventuella underordnade sekundära platser. Den sekundära platsen startar synkroniseringen för programuppdateringar med den överordnade primära platsen. Den sekundära platsen är konfigurerad som en replik av WSUS som körs på den överordnade platsen.  

7.  Synkroniseringshanteraren för WSUS skickar en begäran i taget till WSUS som körs på andra programuppdateringsplatser på platsen. WSUS-servrarna på de andra programuppdateringsplatserna har konfigurerats att vara repliker av WSUS som körs på platsens standardprogramuppdateringsplats.  

##  <a name="software-updates-compliance-assessment"></a><a name="BKMK_SUMCompliance"></a>Utvärdering av kompatibilitet för program uppdateringar  
 Innan du distribuerar program uppdateringar till klient datorer i Configuration Manager startar du en sökning efter program uppdateringarnas kompatibilitet på klient datorer. För varje programuppdatering skapas ett tillståndsmeddelande som innehåller kompatibilitetsstatus för uppdateringen. Tillståndsmeddelandena skickas i grupp till hanteringsplatsen och sedan till platsservern, där kompatibilitetstillståndet lagras i platsdatabasen. Kompatibilitetstillstånd för program uppdateringar visas i Configuration Manager-konsolen. Du kan distribuera och installera programuppdateringar på datorer som kräver uppdateringarna. I följande stycken finns information om kompatibilitetstillstånden och en beskrivning av processen för att söka efter kompatibilitet för programuppdateringar.  

### <a name="software-updates-compliance-states"></a>Tillstånd för programuppdateringskompatibilitet  
 I följande listor och beskrivs varje kompatibilitetstillstånd som visas i Configuration Manager-konsolen för program uppdateringar.  

-   **Obligatoriskt**  

     Anger att programuppdateringen är tillämplig och obligatorisk på klientdatorn. Vilket som helst av följande villkor kan vara uppfyllt när programuppdateringens tillstånd är **Obligatoriskt**:  

    -   Programuppdateringen distribuerades inte till klientdatorn.  

    -   Programuppdateringen installerades på klientdatorn. Men det senaste tillståndsmeddelandet har ännu inte lagts in i databasen på platsservern. Klientdatorn söker efter uppdateringen igen när installationen är klar. Det kan uppstå en fördröjning på upp till två minuter innan klienten skickar det uppdaterade tillståndet till hanteringsplatsen, som sedan vidarebefordrar det uppdaterade tillståndet till platsservern.  

    -   Programuppdateringen installerades på klientdatorn. Men installationen av programuppdateringen kräver att datorn startas om innan uppdateringen är slutförd.  

    -   Programuppdateringen distribuerades till klientdatorn, men har ännu inte installerats.  

-   **Krävs inte**  

     Anger att programuppdateringen inte är tillämplig på klientdatorn. Därför är programuppdateringen inte obligatorisk.  

-   **Installerad**  

     Anger att programuppdateringen är tillämplig på klientdatorn, och att klientdatorn redan har programuppdateringen installerad.  

-   **Okänt**  

     Anger att platsservern inte har tagit emot något tillståndsmeddelande från klientdatorn, normalt beroende på något av följande:  

    -   Klientdatorn har inte genomfört en genomsökning för kompatibilitet med programuppdateringarna.  

    -   Genomsökningen genomfördes på klientdatorn. Däremot har tillståndsmeddelandet ännu inte behandlats på platsservern, möjligen beroende på en eftersläpning för tillståndsmeddelanden.  

    -   Genomsökningen genomfördes på klientdatorn, men tillståndsmeddelandet har inte tagits emot från den underordnade platsen.  

    -   Genomsökningen genomfördes på klientdatorn, men tillståndsmeddelandefilen var skadad på något sätt och kunde inte behandlas.  

### <a name="scan-for-software-updates-compliance-process"></a>Processen för att söka efter kompatibilitet för programuppdateringar  
 När program uppdaterings platsen har installerats och synkroniserats skapas en princip för hela platsen som informerar klient datorer som Configuration Manager program uppdateringar har Aktiver ATS för platsen. När en klient tar emot datorprincipen schemaläggs en genomsökning för utvärdering av kompatibilitet för start vid en slumpmässig tidpunkt inom de närmaste två timmarna. När genomsökningen startas rensar en klientagent för programuppdateringar genomsökningshistoriken, varefter den skickar en begäran om att hitta den WSUS-server som ska användas för genomsökningen och uppdaterar den lokala grupprincipen med WSUS-serverns placering.  

> [!NOTE]  
>  Internetbaserade klienter måste ansluta till WSUS-servern med SSL.  

 En förfrågan om genomsökning skickas till Windows Update-agenten. Windows Update-agenten ansluter då till WSUS-serverplatsen som står på listan i den lokala principen, hämtar de programuppdateringsmetadata som har synkroniserats på WSUS-servern, och genomsöker klientdatorn efter uppdateringarna. En klientagentprocess för programuppdateringar identifierar att kompatibilitetsgenomsökningen har slutförts och skapar tillståndsmeddelanden för varje programuppdatering vars kompatibilitetsstatus har ändrats sedan den senaste genomsökningen. Tillståndsmeddelandena skickas till gruppvis till hanteringsplatsen var 15:e minut. Hanteringsplatsen vidarebefordrar sedan tillståndsmeddelandena till platsservern där de läggs till i platsserverdatabasen.  

 Efter den första genomsökningen efter programuppdateringar, startas genomsökningen enligt det inställda genomsökningsschemat. Men om klienten har sökt efter programuppdateringskompatibilitet under den tidsperiod som anges av TTL-värdet (time to live) använder klienten de programuppdateringsmetadata som är sparade lokalt. Om den senaste genomsökningen gjordes utanför TTL-perioden måste klienten ansluta till den WSUS som körs på programuppdateringsplatsen och uppdatera de programuppdateringsmetadata som är sparade på klienten.  

 Du kan starta genomsökningen efter programuppdateringskompatibilitet, inklusive genomsökningsschemat, på följande sätt:  

-   **Schema för genomsökning av programuppdateringar**: Genomsökningen efter programuppdateringskompatibilitet startar enligt det förinställda schemat som konfigureras i inställningarna för klientagenten för programuppdateringar. Mer information om hur du konfigurerar klient inställningarna för program uppdateringar finns i [klient inställningar för program uppdateringar](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Åtgärden Egenskaper för Configuration Manager**: Användaren kan starta åtgärden **Sökcykel för programuppdateringar** eller **Utvärderingscykel för distribution av programuppdateringar** på fliken **Åtgärd** i dialogrutan **Egenskaper för Configuration Manager** på klientdatorn.  

-   **Schema för ny distributionsutvärdering**: Distributionsutvärderingen och genomsökningen efter programuppdateringskompatibilitet startar enligt det förinställda schemat för ny distributionsutvärdering som konfigureras i inställningarna för klientagenten för programuppdateringar. Mer information om klient inställningarna för program uppdateringar finns i [klient inställningar för program uppdateringar](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Innan uppdateringsfilerna laddas ned**: När en klientdator får en tilldelningsprincip för en ny nödvändig distribution, laddar programuppdateringsklientagenten ned programuppdateringsfilerna till den lokala klientcachen. Innan programuppdateringsfilerna laddas ned startar klientagenten en genomsökning för att kontrollera att programuppdateringen fortfarande är nödvändig.  

-   **Innan programuppdateringen installeras**: Innan programuppdateringen installeras startar programuppdateringsklientagenten en genomsökning för att kontrollera att programuppdateringarna fortfarande är nödvändiga.  

-   **När programuppdateringen har installerats**: Efter att programuppdateringen har installerats startar programuppdateringsklientagenten en genomsökning för att kontrollera att programuppdateringarna inte längre är nödvändiga, och skapar ett nytt tillståndsmeddelande om att programuppdateringen har installerats. När installationen är klar men en omstart krävs, visar tillståndsmeddelandet att klientdatorn väntar på att startas om.  

-   **När systemet har startats om**: Om en klientdator väntar på att systemet ska startas om för att programuppdateringsinstallationen ska slutföras, startar programuppdateringsklientagenten en genomsökning efter omstarten för att kontrollera att programuppdateringen inte längre behövs, och skapar ett tillståndsmeddelande om att programuppdateringen har installerats.  

#### <a name="time-to-live-value"></a>TTL-värde  
 Programuppdateringens metadata som behövs för genomsökningen efter programuppdateringskompatibilitet lagras på den lokala klientdatorn och är som standard giltiga i upp till 24 timmar. Värdet kallas TTL-värde (time to live).  

#### <a name="scan-for-software-updates-compliance-types"></a>Typer av genomsökning av programuppdateringskompatibilitet  
 Klienten utför genomsökningen genom att använda en online- eller offlinegenomsökning och en framtvingad eller icke-framtvingad genomsökning, beroende på hur genomsökningen startades. Här följer en beskrivning av vilka metoder för att starta genomsökningen online eller offline och om genomsökningen tvingas eller inte.  

-   **Schema för genomsökning av program uppdateringar** (ej Tvingad online-genomsökning)  

     Enligt det konfigurerade genomsökningsschemat ansluter bara klienten till den WSUS som körs på programuppdateringsplatsen för att hämta programuppdateringsmetadata om den senaste genomsökningen utfördes utanför TTL-perioden.  

-   **Utvärderings cykel** för **genomsökning av program uppdateringar** eller distribution av program uppdateringar (Tvingad online-genomsökning)  

     Klientdatorn ansluter alltid till WSUS som körs på programuppdateringsplatsen för att hämta programuppdateringsmetadata innan en genomsökning görs. När genomsökningen är klar återställs TTL-räknaren. Om TTL-perioden exempelvis är 24 timmar och en användare startar en genomsökning efter programuppdateringskompatibilitet, återställs värdet till 24 timmar när genomsökningen är klar.  

-   **Schema för ny distributions utvärdering** (ej Tvingad online-genomsökning)  

     Enligt det konfigurerade schemat för ny distributionsutvärdering ansluter klienten till WSUS som körs på programuppdateringsplatsen för att hämta programuppdateringsmetadata bara om den senaste genomsökningen utfördes utanför TTL-perioden.  

-   **Innan du hämtar uppdateringsfiler** (ej Tvingad online-genomsökning)  

     Innan klienten kan ladda ned uppdateringsfilerna ansluter klienten till WSUS som körs på programuppdateringsplatsen för att hämta programuppdateringsmetadata bara om den senaste genomsökningen utfördes utanför TTL-perioden.  

-   **Före installationen av program uppdateringen** (ej Tvingad online-genomsökning)  

     Innan klienten installerar programuppdateringarna, ansluter klienten till WSUS som körs på programuppdateringsplatsen för att hämta programuppdateringsmetadata bara om den senaste genomsökningen utfördes utanför TTL-perioden.  

-   **Efter installation av program uppdatering** (Tvingad offline-genomsökning)  

     När en programuppdatering har installerats startar klientagenten för programuppdateringar en genomsökning genom att använda lokala metadata. Klienten ansluter aldrig till WSUS som körs på programuppdateringsplatsen för att hämta programuppdateringsmetadata.  

-   **Efter omstart av systemet** (Tvingad offline-genomsökning)  

     När en programuppdatering har installerats och datorn startats om, startar klientagenten för programuppdateringar en genomsökning genom att använda lokala metadata. Klienten ansluter aldrig till WSUS som körs på programuppdateringsplatsen för att hämta programuppdateringsmetadata.  

##  <a name="software-update-deployment-packages"></a><a name="BKMK_DeploymentPackages"></a> Distributionspaket för programvaruuppdateringar  
 Ett distributionspaket för programuppdatering används för att ladda ned programuppdateringar till en delad nätverksmapp och kopiera programuppdateringskällfilerna till innehållsbiblioteket på platsservrar och distributionsplatser som definierats i distributionen. Du kan använda guiden för att hämta uppdateringar för att ladda ned programuppdateringar och lägga till dem i distributionspaket innan du distribuerar dem. Med den här guiden kan du etablera programuppdateringar på distributionsplatser och kontrollera att den här delen av distributionsprocessen fungerar innan du distribuerar programuppdateringarna till klienter.  

 När du distribuerar nedladdade programuppdateringar med guiden, används automatiskt det distributionspaket som innehåller programuppdateringarna. Om programuppdateringar som inte har laddats ned distribueras, måste du ange ett nytt eller befintligt distributionspaket i guiden så att programuppdateringarna laddas ned när guiden har slutförts.  

> [!IMPORTANT]  
>  Du måste skapa den delade nätverksmappen manuellt för distributionspaketets källfiler innan du anger den i guiden. Alla distributionspaket måste använda olika delade nätverksmappar.  

> [!IMPORTANT]  
>  SMS-providerkontot och den administrativa användare som laddar ned programuppdateringarna, måste båda ha **skriv** -behörighet för paketkällan. Begränsa åtkomsten till paketkällan för att minska risken för att en angripare manipulerar programuppdateringskällfilerna där.  

 När ett nytt distributionspaket skapas ställs innehållsversionen in på 1 innan några programuppdateringar laddas ned. När filerna för programuppdateringen laddas ned via paketet ökar innehållsversionen till 2. Därför börjar alla nya distributionspaket med innehållsversion 2. Varje gång innehållet ändras i ett distributionspaket ökar innehållsversionen med 1. Mer information finns i [grundläggande begrepp för innehålls hantering](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

 Klienter installerar programuppdateringar i en distribution genom att använda en distributionsplats där de tillgängliga programuppdateringarna finns, oavsett distributionspaket. Även om ett distributionspaket har tagits bort för en aktiv distribution, kan klienterna fortfarande installera programuppdateringarna i distributionen så länge varje uppdatering har laddats ned till minst ett annat distributionspaket och är tillgängligt på en distributionsplats som kan nås från klienten. När det sista distributionspaketet som innehåller en programuppdatering har tagits bort, kan klientdatorerna inte hämta programuppdateringar förrän uppdateringen laddas ned igen till ett distributionspaket. Program uppdateringar visas med en röd pil i Configuration Manager-konsolen när uppdateringsfilerna inte finns i några distributions paket. Distributioner visas med en röd dubbelpil om de innehåller några uppdateringar i det här tillståndet.  

##  <a name="software-update-deployment-workflows"></a><a name="BKMK_DeploymentWorkflows"></a> Arbetsflöden för distribution av programuppdatering  
 Det finns två huvudscenarier för distribution av programuppdateringar i miljön: manuell distribution och automatisk distribution. Det vanligaste är att distribuera programuppdateringar manuellt för att skapa en baslinje för klientdatorer, och sedan hantera programuppdateringarna på klienter med automatisk distribution. I följande avsnitt visas en sammanfattning av arbetsflödet vid manuell och automatisk distribution av programuppdateringar.  

###  <a name="manual-deployment-of-software-updates"></a><a name="BKMK_ManualDeployment"></a> Manuell distribution av programuppdateringar  
 Manuell distribution av program uppdateringar är processen att välja program uppdateringar i Configuration Manager-konsolen och manuellt starta distributions processen. Den här metoden kan du använda för att uppdatera klientdatorerna med nödvändiga programuppdateringar innan du skapar regler för automatisk uppdatering som hanterar pågående månadsvisa programuppdateringsdistributioner, och för att distribuera krav för out-of-band-programuppdateringar. Följande lista visar det allmänna arbetsflödet för manuell distribution av programuppdateringar:  

1.  Filtrera fram programuppdateringar där särskilda krav används. Du kan till exempel ange villkor som hämtar alla säkerhetsprogramuppdateringar eller kritiska programuppdateringar som krävs för över 50 klientdatorer.  

2.  Skapa en programuppdateringsgrupp som innehåller programuppdateringarna.  

3.  Ladda ned innehållet för programuppdateringarna i programuppdateringsgruppen.  

4.  Distribuera programuppdateringsgruppen manuellt.  

###  <a name="automatic-deployment-of-software-updates"></a><a name="BKMK_AutomaticDeployment"></a> Automatisk distribution av programuppdateringar  
 Automatisk distribution av programuppdateringar konfigureras med regler för automatisk distribution (ADR). Du kan använda den här metoden för månadsvisa programuppdateringar (vanligtvis kallat korrigeringstisdag) och för att hantera definitionsuppdateringar. När regeln körs tas uppdateringar bort från programuppdateringsgruppen (om en befintlig grupp används), programuppdateringar som uppfyller ett angivet villkor (till exempel alla säkerhetsprogramuppdateringar som släpptes föregående vecka) läggs till i en programuppdateringsgrupp, innehållsfilerna för programuppdateringar hämtas och kopieras till distributionsplatser och programuppdateringar distribueras till klientdatorer i målsamlingen. Följande lista visar det allmänna arbetsflödet för automatisk distribution av programuppdateringar:  

1. Skapa en regel för automatisk distribution som anger distributionsinställningar enligt följande:  

   -   Målsamling  

   -   Bestäm om du ska aktivera distributionen eller rapportera programuppdateringskompatibilitet för klientdatorerna i målsamlingen.  

   -   Villkor för programuppdateringar  

   -   Scheman för utvärdering och distribution  

   -   Användarupplevelse  

   -   Nedladdningsegenskaper  

2. Programuppdateringarna läggs till i en programuppdateringsgrupp.  

3. Programuppdateringsgruppen distribueras till klientdatorerna i målsamlingen, om den har angetts.  

   Du måste bestämma vilken distributionsstrategi som ska användas i miljön. Du kan till exempel skapa en regel för automatisk distribution och använda testklienter som målsamling. När du har kontrollerat att programuppdateringarna har installerats i testgruppen kan du lägga till en ny distribution i regeln eller ändra samlingen i den befintliga distributionen till en samling som omfattar en större grupp klienter. Programuppdateringsobjekten som skapas via regeln för automatisk distribution är interaktiva.  

- Programuppdateringar som har distribuerats med en regel för automatisk distribution, distribueras automatiskt på nya klienter som läggs till i målsamlingen.  

- Nya programuppdateringar som läggs till i en programuppdateringsgrupp distribueras automatiskt till klienterna i målsamlingen.  

- Du kan aktivera eller inaktivera distributioner när som helst för en regel för automatisk distribution.  

  När du har skapat en regel för automatisk distribution kan du lägga till ytterligare distributioner för regeln. Detta kan hjälpa dig att hantera komplex distribution av olika uppdateringar till olika samlingar. Varje ny distribution har en fullständig uppsättning funktioner och distributionsövervakning, och varje ny distribution som du lägger till:  

- De använder den uppdateringsgrupp och det paket som skapades när ADR kördes första gången  

- De kan ange en annan samling  

- Stöder unika distributionsegenskaper, t.ex.:  

  -   Aktiveringstid  

  -   Tidsgräns  

  -   Visa eller dölj slutanvändarens upplevelse  

  -   Separata aviseringar för den här distributionen  

##  <a name="software-update-deployment-process"></a><a name="BKMK_DeploymentProcess"></a>Distributions process för program uppdatering  
 När du har distribuerat programuppdateringar eller när en regel för automatisk distribution körs och distribuerar programuppdateringar, läggs en distributionstilldelningsprincip till i platsens datorprincip. Programuppdateringarna laddas ned från nedladdningsplatsen, Internet eller en delad nätverksmapp, till paketkällan. Programuppdateringarna kopieras från paketkällan till innehållsbiblioteket på platsservern och kopieras sedan till innehållsbiblioteket på distributionsplatsen.  

 När en klientdator i målsamlingen för distributionen tar emot datorprincipen startar klientagenten för programuppdateringen en utvärderingssökning. Klient agenten laddar ned innehållet för obligatoriska program uppdateringar från en distributions plats till den lokala klientcachen vid inställningen **tillgänglig tid för program vara** för distributionen och sedan är program uppdateringarna tillgängliga för installation. Programuppdateringarna i valfria distributioner (distributioner som inte har någon installationstidsgräns) laddas inte ned förrän en användare startar installationen manuellt.  

 När den konfigurerade tidsgränsen har passerat utför klientagenten för programuppdateringar en sökning för att verifiera att programuppdateringar fortfarande krävs. Sedan kontrolleras den lokala cachen på klientdatorn för att verifiera att källfilerna för programuppdateringen fortfarande är tillgänglig. Slutligen installerar klienten programuppdateringarna. Om innehållet har tagits bort från klientcachen, till exempel för att ge plats åt en annan distribution, laddas programuppdateringarna ned på nytt till klientcachen från distributionsplatsen. Programuppdateringar laddas alltid ned till klientcacheutrymmet, oavsett den konfigurerade största storleken för klientcacheutrymmet. När installationen har slutförts verifierar klientcachen att programuppdateringar inte längre krävs och skickar sedan ett statusmeddelande till hanteringsplatsen för att indikera att programuppdateringar nu har installerats på klienten.  

### <a name="required-system-restart"></a>Obligatorisk omstart  
 En omstart av systemet startas som standard när programuppdateringar från en obligatorisk distribution installeras på en klientdator och en systemstart krävs för att installationen ska slutföras. För programuppdateringar som har installerats före tidsgränsen skjuts omstarten av det automatiska systemet upp tills tidgränsen uppnås, om inte datorn startas om innan dess av någon annan orsak. Omstarten av systemet kan förhindras för servrar och arbetsstationer. Dessa inställningar konfigureras på sidan **Användarupplevelse** i guiden Distribuera programuppdateringar eller guiden Skapa automatiska uppdateringar.  

### <a name="deployment-reevaluation-cycle"></a>Omvärderingscykel för distribution  
 Som standard startar klientdatorer en omvärderingscykel för distribution var 7:e dag. Under den här omvärderingscykeln söker klientdatorn efter programuppdateringar som tidigare har distribuerats och installerats. Om några programuppdateringar saknas installeras programuppdateringarna om från den lokala cachen. Om en programuppdatering inte längre är tillgänglig i den lokala cachen laddas den ned från en distributionsplats och installeras sedan om. Du kan konfigurera omvärderingsschemat på sidan **Programuppdateringar** i klientinställningar för platsen.  

##  <a name="support-for-windows-embedded-devices-that-use-write-filters"></a><a name="BKMK_EmbeddedDevices"></a>Stöd för Windows Embedded-enheter som använder Skriv filter  
 När du distribuerar programuppdateringar till Windows Embedded-enheter med aktiverat skrivfilter, kan du ange om skrivfiltret ska inaktiveras på enheten under distributionen och sedan starta om enheten efter distributionen. Om skrivfiltret inte är inaktiverat distribueras programvaran till ett tillfälligt överlägg och programvaran kommer inte längre att installeras när enheten startas om, om inte en annan distribution framtvingar att ändringar ska sparas.  

> [!NOTE]  
>  När du distribuerar en programuppdatering på en Windows Embedded-enhet bör du se till att enheten tillhör en samling som har en konfigurerad underhållsperiod. På så vis kan du hantera när skrivfiltret ska inaktiveras och aktiveras och när enheten ska startas om.  

 Den inställning för användarupplevelse som styr skrivfilterbeteendet är en kryssruta med namnet **Genomför ändringar efter deadline eller under ett underhållsfönster (omstart krävs)**.  

 Mer information om hur Configuration Manager hanterar inbäddade enheter som använder Skriv filter, finns i [Planera för klient distribution till Windows Embedded-enheter](../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

##  <a name="extend-software-updates-in-configuration-manager"></a><a name="BKMK_ExtendSoftwareUpdates"></a>Utöka program uppdateringar i Configuration Manager  
 Använd System Center Updates Publisher för att hantera program uppdateringar som inte är tillgängliga från Microsoft Update. När du har publicerat program uppdateringar till uppdaterings servern och synkroniserar program uppdateringarna i Configuration Manager kan du distribuera program uppdateringarna till Configuration Manager klienter. Mer information om Updates Publisher finns i [updates publisher 2011](https://docs.microsoft.com/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

## <a name="next-steps"></a>Nästa steg
[Planera programuppdateringar](../plan-design/plan-for-software-updates.md)
