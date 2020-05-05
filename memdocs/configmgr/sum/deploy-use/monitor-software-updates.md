---
title: Övervaka programuppdateringar
titleSuffix: Configuration Manager
description: Configuration Manager-konsolen innehåller aviseringar och statusar för att övervaka uppdateringar och efterlevnad.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: aa17e58f2687a48895502d1062a22d0c8630aea3
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110380"
---
# <a name="monitor-software-updates-in-configuration-manager"></a>Övervaka program uppdateringar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager innehåller många olika sätt att övervaka program uppdaterings objekt, processer och kompatibilitetsinformation. Använd följande avsnitt för att övervaka program uppdateringar.

## <a name="software-updates-dashboard"></a>Instrument panel för program uppdateringar

*(Lanseras i version 1610)*

Från och med Configuration Manager version 1610 kan du använda instrument panelen för program uppdateringar för att visa aktuella kompatibilitetsstatus för enheter i din organisation och snabbt analysera data för att se vilka enheter som är utsatta för risk. Om du vill visa instrument panelen navigerar du till **övervaknings** > **Översikt** > **säkerhets** > **instrument panel för säkerhets program uppdateringar**.

## <a name="drill-through-required-updates"></a>Granska nödvändiga uppdateringar
<!--4224414-->
*(Lanseras i version 1906)*

Du kan gå igenom efterlevnads statistik för att se vilka enheter som kräver en speciell Microsoft 365 program uppdatering av program vara. Om du vill visa enhets listan måste du ha behörighet att visa uppdateringar och de samlingar som enheterna tillhör. Så här ökar du detalj nivån i enhets listan:

1. Gå till **program varu bibliotek** > **program uppdateringar** > **alla program uppdateringar**.
1. Välj en uppdatering som krävs av minst en enhet.
1. Titta på fliken **Sammanfattning** och hitta cirkel diagrammet under **statistik**.
1. Välj hyperlänken **vy som krävs** bredvid cirkel diagrammet för att öka detalj nivån i enhets listan.
1. Den här åtgärden tar dig till en tillfällig nod under **enheter** där du kan se vilka enheter som kräver uppdateringen. Du kan också utföra åtgärder för noden, till exempel skapa en ny samling från listan.


##  <a name="alerts-for-software-updates"></a><a name="BKMK_SUAlerts"></a> Aviseringar om programuppdateringar  
 Du kan konfigurera aviseringar för programuppdateringar för att avisera administrativa användare när kompatibilitetsnivåer för programuppdateringsdistributioner ligger under den konfigurerade procentsatsen. Du kan konfigurera aviseringar för programuppdateringsdistributioner på följande platser:  

-   Inställning för automatisk distributionsregel: Du kan ange aviseringsinställningarna i guiden Skapa regel för automatisk distribution och i egenskaperna för den automatiska distributionsregeln.  

-   Distributionsinställning: Du kan ange aviseringsinställningarna i guiden Distribuera programuppdateringar och i distributionsegenskaperna.  

När du har konfigurerat aviserings inställningarna, om de angivna villkoren inträffar, genererar Configuration Manager en avisering. Du kan granska programuppdateringsaviseringarna på följande platser:  

1.  Granska de senaste aviseringarna i noden **Programuppdateringar** i arbetsytan **Programvarubibliotek** .  

2.  Hantera de konfigurerade aviseringarna i noden **Aviseringar** i arbetsytan **Övervakning** .  

##  <a name="software-updates-synchronization-status"></a><a name="BKMK_SUSyncStatus"></a>Synkroniseringsstatus för program uppdateringar  
 När du har startat synkroniseringsprocessen kan du övervaka synkroniseringsprocessen från Configuration Manager-konsolen för alla program uppdaterings platser i hierarkin. Använd följande procedur för att övervaka synkroniseringsprocessen för programuppdatering.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Övervaka processen för synkronisering av programuppdateringar  

- I Configuration Manager-konsolen navigerar du till **övervakning** > **Översikt** > **program uppdaterings punktens synkroniseringsstatus**.  

    Program uppdaterings platserna i Configuration Manager hierarkin visas i resultat fönstret. Från den här vyn kan du övervaka synkroniseringsstatusen för alla programuppdateringsplatser. Om du vill visa mer detaljerad information om synkroniseringsprocessen kan du granska filen wsyncmgr. log som finns i <*ConfigMgrInstallationPath*> \Logs på varje plats Server.  

##  <a name="software-update-deployment-status"></a><a name="BKMK_SUDeployStatus"></a> Distributionsstatus för programuppdatering  
 När du har distribuerat programuppdateringarna i en programuppdateringsgrupp eller distribuerar en enskild programuppdatering kan du övervaka distributionsstatusen. Använd följande procedur för att övervaka distributionsstatusen för en programuppdateringsgrupp eller programuppdatering.  

#### <a name="to-monitor-deployment-status"></a>Övervaka distributionsstatus  

1.  I Configuration Manager-konsolen går du till **övervakning** > **Översikt** > **distributioner**.  

2.  Klicka på programuppdateringsgruppen eller programuppdateringen för vilken du vill övervaka distributionsstatus.  

3.  Klicka på **Visa status** på fliken **Start** i gruppen **Distribution**.  

##  <a name="software-updates-reports"></a><a name="BKMK_SUReports"></a> Programuppdateringsrapporter  
 Tillståndsmeddelandena för programuppdateringar innehåller information om kompatibiliteten för programuppdateringar och om utvärderingen och tvångsåtgärdstillståndet för programuppdateringsdistributioner. Du kan köra programuppdateringsrapporter för att visa dessa tillståndsmeddelanden. Det finns fler än 30 fördefinierade programuppdateringsrapporter tillgängliga. De är ordnade i flera kategorier och kan användas för att rapportera om detaljerad information om program uppdateringar och distributioner. Förutom att använda förkonfigurerade rapporter kan du också skapa anpassade programuppdateringsrapporter i enlighet med företagets behov. Mer information finns i [åtgärder och underhåll för rapportering](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

### <a name="recommended-software-updates-reports"></a>Rekommenderade program uppdaterings rapporter
Följande är några av de rapporter som är användbara när du identifierar potentiella problem: 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>Kompatibilitet 9 – övergripande hälso tillstånd och efterlevnad (från och med version 1806)
Rapporten innehåller följande delar:

- **Felfria klienter jämfört med totalt antal klienter**: det här stapeldiagrammet jämför de "friska" klienter som har kommunicerat med platsen under den angivna tids perioden mot det totala antalet klienter i den angivna samlingen.
- **Översikt över efterlevnad**: det här cirkel diagrammet visar det övergripande kompatibilitetstillstånd för den specifika program uppdaterings gruppen på aktiva klienter i den angivna samlingen.
- **5 främsta icke-kompatibla enligt artikel-ID**: det här stapeldiagrammet visar de fem främsta program varu uppdateringarna i den angivna gruppen som inte är kompatibla med aktiva klienter i den angivna samlingen.
- Längst ned i rapporten finns en tabell med ytterligare information som visar program uppdateringar i den angivna gruppen.

#### <a name="management-2---updates-required-but-not-deployed"></a>Hantering 2 – nödvändiga uppdateringar som inte har distribuerats

I den här rapporten visas leverantörsspecifika program uppdateringar i en bestämd uppdaterings klassificering som har identifierats som krävs på klienter, men som inte har distribuerats till en angiven samling. 

#### <a name="troubleshooting-2---deployment-errors"></a>Fel sökning 2 – distributions fel

Den här rapporten returnerar distributions fel på platsen och antalet datorer där varje fel uppstår. 


##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a>Övervaka innehåll  
 Du kan övervaka innehållet i Configuration Manager-konsolen för att granska status för alla paket typer i förhållande till associerade distributions platser. Detta kan inkludera innehållsvalideringsstatus för innehållet i paketet, status för innehåll som har tilldelats till en specifik distributionsplatsgrupp, tillståndet för innehåll som har tilldelats till en distributionsplats och statusen för valfria funktioner för varje distributionsplats (innehållsvalidering, PXE och multicast).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Övervakning av innehållsstatus  
 Noden **Innehållsstatus** i arbetsytan **Övervakning** innehåller information om innehållspaket. Du kan granska allmän information om paketet, distributionsstatus för paketet och detaljerad statusinformation om paketet. Använd följande procedur för att visa innehållsstatus.  

#### <a name="to-monitor-content-status"></a>Övervaka innehållsstatus  

1.  I Configuration Manager-konsolen navigerar du till **övervakning** > **Översikt** > **distribution status** > **innehålls status**. Paketen visas.  

2.  Välj det paket som du vill visa detaljerad statusinformation om.  

3.  På fliken **Start** klickar du på **Visa status**. Detaljerad statusinformation om det paket som visas.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a>Status för distributions plats grupp  
 Noden **Gruppstatus för distributionsplatser** på arbetsytan **Övervakning** innehåller information om distributionsplatsgrupper. Du kan granska allmän information om distributionsplatsgruppen, till exempel status för distributionsplatsgruppen och kompatibilitetsnivån, såväl som detaljerad statusinformation för distributionsplatsgruppen. Använd följande procedur om du vill visa distributionsplatsgruppens status.  

#### <a name="to-monitor-distribution-point-group-status"></a>Övervaka distributionsplatsgruppens status  

1.  I Configuration Manager-konsolen navigerar du till **övervakning** > **Översikt** > **distribution status** > **distribution plats grupp status**. Distributionsplatsens grupper visas.  

2.  Välj den distributionsplatsgrupp som du vill visa detaljerad statusinformation om.  

3.  På fliken **Start** klickar du på **Visa status**. Detaljerad statusinformation för distributionsplatsgruppen visas.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a>Konfigurations status för distributions plats  
 Noden **Konfigurationsstatus för distributionsplatser** på arbetsytan **Övervakning** innehåller information om distributionsplatsen. Du kan granska vilka attribut som är aktiva för distributionsplatsen, till exempel PXE, multicast och innehållsvalidering. Du kan även visa detaljerad statusinformation för distributionsplatsen. Använd följande procedur om du vill visa distributionsplatsens konfigurationsstatus.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Övervaka distributionsplatsens konfigurationsstatus  

1.  I Configuration Manager-konsolen navigerar du till **övervakning** > **Översikt** > **distribution status** > **distribution plats konfigurations status**. Distributionsplatserna visas.  

2.  Välj den distributionsplats för vilken du vill visa statusinformation för distributionsplatser.  

3.  Klicka på fliken **information** i resultat fönstret. information om den här distributions platsens status visas.  

## <a name="next-steps"></a>Nästa steg

- [Loggfiler för program uppdateringar](../../core/plan-design/hierarchy/log-files.md#BKMK_SU_NAPLog)

- [Whitepaper om hantering av program uppdateringar](https://www.microsoft.com/download/confirmation.aspx?id=44578)
