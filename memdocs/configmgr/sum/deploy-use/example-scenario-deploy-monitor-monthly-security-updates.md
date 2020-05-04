---
title: Exempel scenario för att distribuera och övervaka uppdateringar
titleSuffix: Configuration Manager
description: Så här använder du program uppdateringar i Configuration Manager för att distribuera och övervaka månatliga program uppdateringar.
ms.date: 10/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ea654c4ec13b95b78a65c85d9d36ce576619854e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714915"
---
# <a name="example-scenario-to-deploy-and-monitor-monthly-software-updates"></a>Exempel scenario för att distribuera och övervaka månatliga program uppdateringar

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller ett exempel scenario för hur du kan använda program uppdateringar i Configuration Manager för att distribuera och övervaka de säkerhets program uppdateringar som Microsoft lanserar varje månad.  

 I det här scenariot följer vi åtgärderna i Configuration Manager-administratören på Sparbanken. Administratören måste skapa en strategi för distribution av program uppdateringar med följande villkor och krav:  

- Aktiv programuppdateringsdistribution sker en vecka efter att Microsoft släpper säkerhetsprogramuppdateringarna den andra tisdagen varje månad. Den här händelsen kallas ofta korrigeringstisdagen.  

- Programuppdateringar laddas ned och mellanlagras på distributionsplatser. Sedan testas en distribution till en delmängd av klienterna innan ConfigMgr-administratören distribuerar program uppdateringarna i sin produktions miljö fullständigt.  

- Administratören måste kunna övervaka program uppdateringarnas kompatibilitet per månad eller per år.  

  Det här scenariot förutsätter att programuppdateringsplatsens infrastruktur redan har implementerats. Använd följande information för att planera för och konfigurera program uppdateringar i Configuration Manager.  

|Process|Referens|  
|-------------|---------------|  
|Gå igenom nyckelkoncepten för programuppdateringar.|[Introduktion till programuppdateringar](../understand/software-updates-introduction.md)|  
|Planera programuppdateringar Den här informationen hjälper dig att planera för kapacitetsöverväganden, bestämma programuppdateringsplatsens infrastruktur, programuppdateringsplatsens installation, synkroniseringsinställningar och klientinställningar för programuppdateringar.|[Planera programuppdateringar](../plan-design/plan-for-software-updates.md)|  
|Konfigurera programuppdateringar. Den här informationen hjälper dig att installera och konfigurera programuppdateringsplatser i din hierarki och hjälper till att konfigurera och synkronisera programuppdateringar.<br /><br /> I det här scenariot konfigurerar vår ConfigMgr-administratör schemaläggningen av program uppdateringar till att ske den andra onsdagen varje månad för att säkerställa att de hämtar de senaste säkerhets program uppdateringarna från Microsoft.|[Synkronisera programuppdateringar](../get-started/synchronize-software-updates.md)|  

 Följande avsnitt i det här avsnittet innehåller exempel steg som hjälper dig att distribuera och övervaka Configuration Manager säkerhets program uppdateringar i din organisation.

##  <a name="step-1-create-a-software-update-group-for-yearly-compliance"></a><a name="BKMK_Step1"></a>Steg 1: skapa en program uppdaterings grupp för årlig kompatibilitet  
 Configuration Manager-administratören skapar en program uppdaterings grupp som kan användas för att övervaka kompatibilitet för alla säkerhets program uppdateringar som de släpper i 2016. Administratören utför stegen i följande tabell.  

|Process|Referens|  
|-------------|---------------|  
|Från noden **alla program uppdateringar** i Configuration Manager-konsolen lägger Configuration Manager administratören till kriterier för att endast Visa säkerhets program uppdateringar som släpps eller revideras under år 2015 som uppfyller följande kriterier:<br /><br /><ul><li>**Kriterier**: Datum för släpp eller ändring</li><li>**Villkor**: Är större än eller lika med det angivna datumet<br />**Värde**: 1/1/2015</li><li>**Kriterier**: Klassificering av uppdateringar<br />**Värde**: Säkerhetsuppdateringar</li><li>**Kriterier**: Inaktuell <br />**Värde**: Nej</li></ul>|Ingen ytterligare information|
|ConfigMgr-administratören lägger till alla filtrerade program uppdateringar till en ny program uppdaterings grupp med följande krav:<br /><br /><ul><li>**Namn**: Kompatibilitetsgrupp – Microsofts säkerhetsuppdateringar 2015</li><li>**Beskrivning**: Programuppdateringar|[Lägga till programuppdateringar i en uppdateringsgrupp](add-software-updates-to-an-update-group.md)|  

##  <a name="step-2-create-an-automatic-deployment-rule-for-the-current-month"></a><a name="BKMK_Step2"></a>Steg 2: skapa en automatisk distributions regel för den aktuella månaden  
 Configuration Manager-administratören skapar en regel för automatisk distribution för säkerhets program uppdateringar som lanseras av Microsoft under den aktuella månaden. Administratören utför stegen i följande tabell.  

|Process|Referens|  
|-------------|---------------|  
|ConfigMgr-administratören skapar en automatisk distributions regel med följande krav:<br /><br /><ol><li>På fliken **Allmänt** konfigurerar ConfigMgr-administratören följande:<br /> <ul><li>Anger **månatliga säkerhets uppdateringar** för namnet.</li><li>Väljer en test samling med begränsade klienter.</li><li>Väljer **skapa en ny program uppdaterings grupp**.</li><li>Kontrollerar att **Aktivera distributionen när regeln har körts** inte har valts.</li></ul></li><li>På fliken **distributions inställningar** väljer ConfigMgr-administratören standardinställningarna.</li><li>På sidan **program uppdateringar** konfigurerar ConfigMgr-administratören följande egenskaps filter och Sök kriterier:<br /><ul><li>Datum för släpp eller ändring **Senaste månaden**.</li><li>Uppdatera klassifikationen **Säkerhetsuppdateringar**.</li></ul></li><li>På sidan **utvärdering** aktiverar ConfigMgr-administratören att regeln körs enligt ett schema för den **andra torsdagen** varje **månad**.  ConfigMgr-administratören kontrollerar också att synkroniseringsschemat är inställt på att köras den **andra onsdagen** varje **månad**.</li><li>ConfigMgr-administratören använder standardinställningarna på sidorna distributions schema, användar upplevelse, aviseringar och hämtnings inställningar.</li><li>På sidan **distributions paket** anger ConfigMgr-administratören ett nytt distributions paket.</li><li>ConfigMgr-administratören använder standardinställningarna på sidorna hämtnings plats och val av språk.</li></ol>|[Distribuera programuppdateringar automatiskt](automatically-deploy-software-updates.md)|  

##  <a name="step-3-verify-that-software-updates-are-ready-to-deploy"></a><a name="BKMK_Step3"></a>Steg 3: kontrol lera att program uppdateringarna är klara att distribueras  
 Den andra torsdagen varje månad verifierar ConfigMgr-administratören att program uppdateringarna är klara att distribueras. Administratören utför följande steg.  

|Process|Referens|  
|-------------|---------------|  
|ConfigMgr-administratören kontrollerar att synkroniseringen av program uppdateringarna har slutförts.|[Synkroniseringsstatus för programuppdateringar](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_Step4"></a>Steg 4: distribuera program uppdaterings gruppen  
 När ConfigMgr-administratören har kontrollerat att program uppdateringarna är klara att distribueras, distribuerar de program uppdateringarna. Administratören utför stegen i följande tabell.  

|Process|Referens|  
|-------------|---------------|  
|ConfigMgr-administratören skapar två test distributioner för den nya program uppdaterings gruppen. Administratören förväntar sig följande miljöer för varje distribution:<br /><br /> **Test distribution av arbets Station**: ConfigMgr-administratören ska beakta följande för test distributionen av arbets stationer:<br /><br /><ul><li>Anger en distributions samling som innehåller en delmängd av arbets Stations klienter för att verifiera distributionen.</li><li>Konfigurerar de distributions inställningar som är lämpliga för arbets Stations klienterna i miljön.</li></ul><br />**Server test distribution**: ConfigMgr-administratören ska beakta följande för Server test distributionen:<br /><br /><ul><li>Anger en distributions samling som innehåller en delmängd av Server klienter för att verifiera distributionen.</li><li>Konfigurerar de distributions inställningar som är lämpliga för Server klienterna i miljön.</li></ul>|[Distribuera programuppdateringar](deploy-software-updates.md)|  
|ConfigMgr-administratören kontrollerar att test distributionerna har distribuerats.|[Distributions status för program uppdateringar](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|ConfigMgr-administratören uppdaterar de två distributionerna med nya samlingar som innefattar hans produktions arbets stationer och servrar.|Ingen ytterligare information|  

##  <a name="step-5-monitor-compliance-for-deployed-software-updates"></a><a name="BKMK_Step5"></a>Steg 5: övervaka kompatibilitet för distribuerade program uppdateringar  
 ConfigMgr-administratören övervakar kompatibilitet för sina program uppdaterings distributioner. Administratören utför steget i följande tabell.  

|Process|Referens|  
|-------------|---------------|  
|ConfigMgr-administratören övervakar distributions statusen för program uppdateringar i Configuration Manager-konsolen och kontrollerar distributions rapporterna för program uppdatering som är tillgängliga i-konsolen.|[Övervaka programuppdateringar](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="step-6-add-monthly-software-updates-to-the-yearly-update-group"></a><a name="BKMK_Step6"></a>Steg 6: Lägg till månads program uppdateringar till års uppdaterings gruppen  
 ConfigMgr-administratören lägger till program uppdateringarna från gruppen för månatlig program uppdatering i den årliga program uppdaterings gruppen. Administratören utför steget i följande tabell.  

|Process|Referens|  
|-------------|---------------|  
|ConfigMgr-administratören väljer program uppdateringar från gruppen för månads program uppdateringar och lägger till program uppdateringarna i program uppdaterings gruppen som har skapats för årlig kompatibilitet. Administratören spårar program uppdateringens kompatibilitet och skapar olika rapporter för sin hantering.|[Lägga till programuppdateringar till en distribuerad uppdateringsgrupp.](add-software-updates-to-an-update-group.md)|  

ConfigMgr-administratören har slutfört sin månads distribution för säkerhets program uppdateringar. Administratören fortsätter att övervaka och rapportera om program varu uppdateringarnas kompatibilitet för att säkerställa att klienterna i sin miljö är inom godtagbara nivåer för efterlevnad.  

##  <a name="recurring-monthly-process-to-deploy-software-updates"></a><a name="BKMK_MonthlyProcess"></a>Återkommande månads process för att distribuera program uppdateringar  
 Efter den första månaden som vår ConfigMgr-administratör distribuerar program uppdateringar utför administratören steg tre till sex för att distribuera de månatliga säkerhets program uppdateringar som Microsoft tillhandahåller.  
