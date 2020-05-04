---
title: Övervaka databasreplikering
titleSuffix: Configuration Manager
description: Lär dig hur du övervakar SQL Server replikering i din Configuration Manager-hierarki.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69550b35-bcdb-4b47-bbec-b3c8bc92bb7b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 96cce5d4aaa352177b1c24ff78cf15e90ea6e823
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713711"
---
# <a name="monitor-database-replication"></a>Övervaka databasreplikering

*Gäller för: Configuration Manager (aktuell gren)*

Övervaka information om databasreplikering med noden **databasreplikering** i arbets ytan **övervakning** i Configuration Manager-konsolen. Du kan övervaka statusen för replikering av länkar mellan platser. Den visar även initiering och replikering av replikeringsgrupper för den plats som du ansluter till.  

> [!TIP]  
> Även om **noden databasreplikering** också visas under noden **hierarki-konfiguration** i arbets ytan **Administration** kan du inte visa replikeringsstatus för länkar från den platsen.  

## <a name="replication-link-status"></a><a name="BKMK_MonitorReplicationLinks"></a> Replikeringslänkstatus  

Databasreplikering mellan platser omfattar replikering av flera uppsättningar med information, som kallas *replikeringsgrupper*. Varje replikeringsgrupp skickar och tar emot data med olika prioriteter. Som standard kan du inte ändra de data som finns i en replikeringsgrupp och hur ofta replikeringen ska vara.  

När en replikeringslänk är aktiv och dess status inte är misslyckad eller försämrad, replikeras alla grupper snabbt. Om en eller flera grupper inte kan slutföra replikeringen inom den förväntade tids perioden visas länken som *försämrad*. Försämrade länkar kan fortfarande fungera, men du bör övervaka dem för att se till att de återgår till aktiv status. Undersök dem för att se till att ytterligare försämrings fel eller replikeringsfel inte inträffar.  

Ange hur många gånger en misslyckad grupp försök ska göras för varje replikeringslänk. Efter det här antalet återförsök anger platsen status för länken till försämrad eller misslyckad. Även om alla utom en grupp replikeras, anger platsen status för länken till försämrad eller misslyckad. Den anger den här statusen eftersom den enda replikeringsgruppen inte kan slutföra replikeringen inom det angivna antalet försök. Mer information finns i [tröskelvärden för databasreplikering](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds).  

Använd följande information för att förstå status för de replikeringslänk som kan kräva ytterligare undersökning:  

### <a name="link-is-active"></a>Länk är aktiv

Inga problem har identifierats, och kommunikationen på länken pågår.

Medan en överordnad plats uppdateras till en ny version och du visar länk status från den underordnade platsen visas länk status som aktiv. Efter uppdateringen visas länk status som aktiv när den visas från den överordnade platsen, tills den underordnade platsen har samma version som den överordnade platsen. När den visas från den underordnade platsen visas den som konfigurerad.  

### <a name="link-is-degraded"></a>Länken är försämrad

Replikeringen fungerar, men minst ett replikeringsobjekt eller en replikeringsgrupp har råkat ut för en fördröjning. Övervaka länkar som är i det här läget. Granska informationen från båda platserna på länken för att visa information om att länken kan Miss förväntas.

En länk kan även vara försämrad om platsen som tar emot de replikerade data inte kan spara informationen i databasen tillräckligt snabbt. Det här problemet uppstår när stora volymer av data replikeras. Du kan till exempel distribuera en program uppdatering till ett stort antal datorer. Den överordnade platsen på länken kan ta en stund att bearbeta den här volymen av replikerade data. En bearbetnings fördröjning på den överordnade platsen resulterar i att länkens status anges till nedgraderad tills den kan bearbeta efter släpning av data.

### <a name="link-has-failed"></a>Länken fungerar inte

Replikering fungerar inte. Det är möjligt att en replikeringslänk kan återställas utan ytterligare åtgärder. Använd Replikeringslänkanalys (RLA) för att undersöka och hjälpa att reparera replikeringen på den här länken.

Den här statusen kan även tyda på ett problem med det fysiska nätverket mellan den över- och underordnade platsen på replikeringslänken.


## <a name="monitor-replication-status"></a><a name="BKMK_MonitorReplicationStatus"></a>Övervaka replikeringsstatus

Använd noden **databasreplikering** på arbets ytan **övervakning** för att visa status för en replikeringslänk. Visa information om databasen på varje plats på replikeringslänken. Du kan även visa information om replikeringsgrupper. Om du vill visa den här informationen väljer du en replikeringslänk och väljer sedan lämplig flik för den replikeringsstatus som du vill visa.

I följande avsnitt får du information om de olika flikarna för replikeringsstatus:

### <a name="summary"></a>Sammanfattning

Visa information på hög nivå om replikeringen av plats data och globala data mellan de två platserna på en länk.  

Välj **Visa rapporter för historisk trafik information** om du vill visa en rapport som visar information om den nätverks bandbredd som används vid replikering över länken.  

### <a name="parent-site"></a>Överordnad plats

Visa detaljer om databasen för den överordnade platsen på en replikeringslänk. Detta omfattar:  

- Brandväggsportar för SQL Server  

- Ledigt diskutrymme  

- Databasfilsökvägar  

- Certifikat  

### <a name="child-site"></a>Underordnad plats

Visa detaljer om databasen för den underordnade platsen på en replikeringslänk. Detta omfattar:  

- Brandväggsportar för SQL Server  

- Ledigt diskutrymme  

- Databasfilsökvägar  

- Certifikat  

### <a name="initialization-detail"></a>Initieringsinformation

Visa initierings status för grupper som replikerar över länken. Med denna information kan du se när initieringen av replikeringsdata pågår eller har misslyckats.  

Använd den här informationen för att identifiera när en plats kan vara i *Interoperabilitets läge*. Samverkans läge är när den underordnade platsen inte kör samma version av Configuration Manager som den överordnade platsen.  

### <a name="replication-detail"></a>Replikeringsinformation

Visa replikeringsstatus för varje grupp som replikerar över länken. Använd den här informationen för att identifiera problem eller fördröjningar vid replikering av vissa data. Det kan hjälpa dig att avgöra lämpliga tröskelvärden för databasreplikering för den här länken. Mer information finns i [tröskelvärden för databasreplikering](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds).  

> [!TIP]  
> Replikeringsgrupper för platsdata skickas endast från den underordnade platsen till den överordnade platsen. Replikeringsgrupper för globala data replikerar åt båda hållen.  


## <a name="replication-link-analyzer"></a><a name="BKMK_RLA"></a>Replikeringslänkanalys

Configuration Manager innehåller **Replikeringslänkanalys** (RLA) som du använder för att analysera och reparera problem med replikeringen. Använd RLA för att reparera länkfel när replikeringen Miss lyckas. Det är också användbart när replikeringen slutar fungera men platsen ännu inte har rapporterat den som misslyckad.

Använd RLA för att åtgärda replikeringsfel mellan följande datorer i hierarkin:  

- Mellan en plats Server och plats databas servern  

- Mellan en plats databas server och en annan plats databas server, annars kallat replikering mellan platser  

> [!Note]  
> Det spelar ingen roll om replikeringens haveri riktning.

Kör RLA antingen i Configuration Manager-konsolen eller i en kommando tolk:  

- För att köra i Configuration Manager-konsolen: gå till arbets ytan **övervakning** och välj noden **databasreplikering** . Välj den replikeringslänk som du vill analysera och välj sedan i menyfliksområdet **Replikeringslänkanalys**.  

- Skriv följande kommando för att köra i en kommando tolk:`%ProgramFiles(x86)%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe <source site server FQDN> <destination site server FQDN>`  

När du kör RLA upptäcks problem med hjälp av en serie diagnostiska regler och kontroller. Du ser de problem som verktyget identifierar. När det finns instruktioner för att lösa ett problem visas dessa. Om RLA kan åtgärda ett problem automatiskt, visas ett sådant alternativ.

När RLA är klar sparas resultaten i följande XML-baserade rapport och i en loggfil på Skriv bordet för den användare som kör verktyget:  

- ReplicationAnalysis.xml  

- ReplicationLinkAnalysis.log  

RLA stoppar följande tjänster medan de åtgärdar vissa problem. De här tjänsterna startas om när reparationen är klar:  

- SMS_SITE_COMPONENT_MANAGER  

- SMS_EXECUTIVE  

Om RLA inte kan slutföra reparationen startar du om dessa tjänster på plats servern om det behövs.  

RLA loggar alla undersöknings-och reparations åtgärder för att ge ytterligare information som inte visas i guiden.  

### <a name="rla-prerequisites"></a>RLA-krav

Det konto som du använder för att köra RLA måste ha följande behörigheter:

- Lokal administratörs behörighet på varje dator som är involverad i replikeringslänken.

- Sysadmin-behörighet för varje SQL Server databas som är involverad i replikeringslänken.  

> [!Note]  
> Kontot kräver inte en speciell Configuration Manager roll-baserad administrations säkerhets roll. En administrativ användare med åtkomst till noden **databasreplikering** kan köra verktyget i Configuration Manager-konsolen. En system administratör med tillräcklig behörighet till varje dator kan köra verktyget i en kommando tolk.  

### <a name="rla-known-issue"></a>RLA-känt problem

RLA genererar SQL Server Service Broker (SSB) certifikat fel för primära platser som har uppgraderats från System Center 2012 Configuration Manager. Det här problemet beror på ändringar i namnen på certifikaten i Configuration Manager aktuella grenen. Du kan ignorera dessa fel utan att oroa dig.  


## <a name="monitoring-database-replication"></a><a name="BKMK_ProcsforMonitoringReplication"></a>Övervaka databasreplikering  

### <a name="monitor-high-level-site-to-site-database-replication-status"></a>Övervaka replikeringsstatus för plats-till-plats-databas på hög nivå

1. Gå till arbets ytan **övervakning** i Configuration Manager-konsolen.  

2. Välj noden **platshierarki för att** öppna vyn **Hierarkidiagram** .  

3. Hovra med mus pekaren på linjen mellan de två platserna. Visa status för global replikering och plats data replikering för dessa platser.  

### <a name="monitor-the-status-of-a-replication-link"></a>Övervaka status för en replikeringslänk

1. Gå till arbets ytan **övervakning** i Configuration Manager-konsolen.  

2. Välj noden **databasreplikering** och välj sedan den replikeringslänk som du vill övervaka. Välj sedan lämplig flik för att visa olika detaljer om replikeringsstatus för länken.  
