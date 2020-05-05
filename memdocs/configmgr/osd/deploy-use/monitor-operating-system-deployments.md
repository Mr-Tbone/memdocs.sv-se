---
title: Övervaka distribution av operativsystem
titleSuffix: Configuration Manager
description: För att hjälpa dig att övervaka objekt för operativ Systems distribution tillhandahåller Configuration Manager-konsolen aviseringar, rapporter och olika status indikatorer.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 08085d94-295c-432f-b5e3-9736bce0193b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9d0a430a1010611bc6a7e0871e8c59ca3d1f8de7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723833"
---
# <a name="monitor-operating-system-deployments-in-configuration-manager"></a>Övervaka operativ Systems distributioner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager-konsolen innehåller följande metoder som hjälper dig att övervaka objekt för operativ Systems distribution.  


##  <a name="alerts-for-operating-system-deployments"></a><a name="BKMK_OSDAlerts"></a> Varningar för operativsystemsdistribution  
 Du kan konfigurera en avisering i aktivitetssekvensens distributionsinställningar för att meddela administrativa användare när kompatibilitetsnivåer för distributionen ligger under den konfigurerade procentsatsen.  

 När du har konfigurerat aviserings inställningarna, om de angivna villkoren inträffar, genererar Configuration Manager en avisering. Du kan granska distributionsaviseringar för aktivitetssekvensen på följande platser:  

1.  Granska de senaste aviseringarna i noden **Operativsystem** på arbetsytan **Programvarubibliotek** .  

2.  Hantera de konfigurerade aviseringarna i noden **Aviseringar** i arbetsytan **Övervakning** .  

##  <a name="task-sequence-deployment-status"></a><a name="BKMK_TSDeployStatus"></a>Distributions status för aktivitetssekvens  
 När du har distribuerat en aktivitetssekvens kan du övervaka distributionsstatus. Använd följande procedur för att övervaka distributionsstatusen för en aktivitetssekvens.  

#### <a name="to-monitor-deployment-status"></a>Övervaka distributionsstatus  

1.  Klicka på **övervakning**i Configuration Manager-konsolen.  

2.  I arbetsytan Övervakning klickar du på **Distributioner**.  

3.  Klicka på den aktivitetssekvens som du vill övervaka distributionsstatus för.  

4.  Klicka på **Visa status** på fliken **Start** i gruppen **Distribution**.  

##  <a name="operating-system-deployment-reports"></a><a name="BKMK_TSReports"></a> Rapporter för operativsystemsdistribution  
 Det finns många fördefinierade rapporter för operativsystemsdistribution. De ordnas i flera kategorier och kan användas för att rapportera om specifik information om tillståndsmigrering och aktivitetssekvensdistribution. Förutom att använda förkonfigurerade rapporter kan du också skapa anpassade programuppdateringsrapporter i enlighet med företagets behov. Mer information finns i [åtgärder och underhåll för rapportering](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a>Övervaka innehåll  
 Du kan övervaka innehållet i Configuration Manager-konsolen för att granska status för alla paket typer i förhållande till associerade distributions platser. Detta kan inkludera innehållsvalideringsstatus för innehållet i paketet, status för innehåll som har tilldelats till en specifik distributionsplatsgrupp, tillståndet för innehåll som har tilldelats till en distributionsplats och statusen för valfria funktioner för varje distributionsplats (innehållsvalidering, PXE och multicast).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Övervakning av innehållsstatus  
 Noden **Innehållsstatus** i arbetsytan **Övervakning** innehåller information om innehållspaket. Du kan granska allmän information om paketet, distributionsstatus för paketet och detaljerad statusinformation om paketet. Använd följande procedur för att visa innehållsstatus.  

#### <a name="to-monitor-content-status"></a>Övervaka innehållsstatus  

1.  Klicka på **övervakning**i Configuration Manager-konsolen.  

2.  I arbetsytan Övervakning expanderar du **Distributionsstatus**och klickar sedan på **Innehållsstatus**. Paketen visas.  

3.  Välj det paket som du vill visa detaljerad statusinformation om.  

4.  På fliken **Start** klickar du på **Visa status**. Detaljerad statusinformation om det paket som visas.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a>Status för distributions plats grupp  
 Noden **Gruppstatus för distributionsplatser** på arbetsytan **Övervakning** innehåller information om distributionsplatsgrupper. Du kan granska allmän information om distributionsplatsgruppen, till exempel status för distributionsplatsgruppen och kompatibilitetsnivån, såväl som detaljerad statusinformation för distributionsplatsgruppen. Använd följande procedur om du vill visa distributionsplatsgruppens status.  

#### <a name="to-monitor-distribution-point-group-status"></a>Övervaka distributionsplatsgruppens status  

1.  Klicka på **övervakning**i Configuration Manager-konsolen.  

2.  I arbetsytan Övervakning expanderar du **Distributionsstatus**och klickar sedan på **Status för distributionsgrupp**. Distributionsplatsens grupper visas.  

3.  Välj den distributionsplatsgrupp som du vill visa detaljerad statusinformation om.  

4.  På fliken **Start** klickar du på **Visa status**. Detaljerad statusinformation för distributionsplatsgruppen visas.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a>Konfigurations status för distributions plats  
 Noden **Konfigurationsstatus för distributionsplatser** på arbetsytan **Övervakning** innehåller information om distributionsplatsen. Du kan granska vilka attribut som är aktiva för distributionsplatsen, till exempel PXE, multicast och innehållsvalidering. Du kan även visa detaljerad statusinformation för distributionsplatsen. Använd följande procedur om du vill visa distributionsplatsens konfigurationsstatus.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Övervaka distributionsplatsens konfigurationsstatus  

1.  Klicka på **övervakning**i Configuration Manager-konsolen.  

2.  I arbetsytan Övervakning expanderar du **Distributionsstatus**och klickar sedan på **Konfigurationsstatus för distributionsplatser**. Distributionsplatserna visas.  

3.  Välj den distributionsplats för vilken du vill visa statusinformation för distributionsplatser.  

4.  Klicka på fliken **information** i resultat fönstret. information om den här distributions platsens status visas.  
