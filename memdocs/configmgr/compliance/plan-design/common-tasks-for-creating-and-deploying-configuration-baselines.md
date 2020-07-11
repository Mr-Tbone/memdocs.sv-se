---
title: 'Vanliga aktiviteter för konfigurations bas linjer '
titleSuffix: Configuration Manager
description: Lär dig mer om hur du skapar och distribuerar Configuration Manager konfigurations bas linjer.
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 40f0fe1adc723587316dcc5f03d710ae4b31b78b
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240702"
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-configuration-manager"></a>Vanliga åtgärder för att skapa och distribuera konfigurations bas linjer med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller vanliga scenarier som hjälper dig att lära dig hur du skapar och distribuerar Configuration Manager konfigurations bas linjer.  

 Om du redan är bekant med kompatibilitetsinställningar kan du hitta detaljerad dokumentation om alla funktioner som du använder i avsnitten [skapa konfigurations bas linjer](../../compliance/deploy-use/create-configuration-baselines.md) och [distribuera konfigurations bas linjer](../../compliance/deploy-use/deploy-configuration-baselines.md) .  

 Innan du börjar läser du [komma igång med](../../compliance/get-started/get-started-with-compliance-settings.md) kompatibilitetsinställningar för att lära dig grunderna om kompatibilitetsinställningar och även läsa [Planera för och konfigurera kompatibilitetsinställningar](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) för att implementera nödvändiga komponenter.  

## <a name="create-a-configuration-baseline"></a>Skapa en konfigurationsbaslinje  
 I det här exemplet har du skapat ett konfigurations objekt för endast Windows 10-datorer som kör Configuration Manager-klienten.  

 Det här konfigurationsobjektet kräver ett lösenord på minst sex tecken på Windows 10-datorer. Konfigurationsobjektet heter **Tvingande Windows 10-lösenord**.  

Använd följande procedur för att lära dig hur du lägger till det här konfigurationsobjektet i en konfigurations bas linje för att förbereda det för distribution.  

1. I Configuration Manager-konsolen klickar du på **till gångar och efterlevnad**  >  **kompatibilitetsinställningar**  >  **konfigurations bas linjer**.  

2. Klicka på **Skapa konfigurationsbaslinje** i gruppen **Skapa** på fliken **Start**.  

3. Konfigurera följande inställningar i dialog rutan **skapa konfigurations bas linje** :  

   -   **Namn** – Ange **Windows 10-lösenord** (eller ett annat valfritt namn)  

4. Klicka på **Lägg till**  >  **konfigurations objekt**.  

5. I dialogrutan **Lägg till konfigurationsobjekt** väljer du konfigurationsobjektet för **Tvingande Windows 10-lösenord** som du skapade tidigare och klickar på **Lägg till**.  

6. Klicka på OK för att stänga dialog rutan **Lägg till konfigurations objekt** och gå tillbaka till dialog rutan **skapa konfigurations bas linje** .

7. Stäng dialogrutan **Skapa konfigurationsbaslinje** genom att klicka på **OK** .  

   Nu kan du se konfigurations bas linjen i noden **konfigurations bas linjer** i Configuration Manager-konsolen.  

## <a name="deploy-the-configuration-baseline"></a>Distribuera konfigurations bas linjen  
 I det här exemplet distribuerar du konfigurations bas linjen som du skapade i föregående procedur till en samling datorer.  

1. I Configuration Manager-konsolen klickar du på **till gångar och efterlevnad**  >  **kompatibilitetsinställningar**  >  **konfigurations bas linjer**.  

2. Välj **Windows 10-lösenord**i listan med konfigurationsbaslinjer.  

3. På fliken **Start** går du till gruppen **Distribution** och klickar på **Distribuera**.  

4. Konfigurera följande inställningar i dialog rutan **distribuera konfigurations bas linjer** :  

   -   **Markerade konfigurationsbaslinjer** – Kontrollera att konfigurationsbaslinjen **Windows 10-lösenord** lades till automatiskt i listan.  

   -   **Reparera inkompatibla regler när stöd** finns – Markera den här kryss rutan om du vill se till att om rätt inställningar inte finns på mål enheterna, åtgärdas de av Configuration Manager.  

   -   **Samling** – Klicka på **Bläddra** och välj den samling datorer där konfigurations bas linjen utvärderas och åtgärdas för efterlevnad. I det här exemplet distribuerades konfigurationsbaslinjen till den inbyggda samlingen **Alla skrivbords- och serverklienter** .  

       > [!TIP]  
       >  Oroa dig inte om den samling som du väljer innehåller datorer eller enheter som inte kör Windows 10. Så länge som du konfigurerade plattformar som stöds i konfigurationsobjektet som du skapade, utvärderas endast Windows 10-datorer för efterlevnad.  

   -   Vid behov konfigurerar du det schema enligt vilket konfigurations bas linjen utvärderas. Annars behåller du standardvärdet **7 dagar**.  

5. Stäng dialogrutan **Distribuera konfigurationsbaslinjer** och skapa distributionen genom att klicka på **OK** .  

   Om du vill titta på kompatibilitetsstatistiken för distributionen klickar du på **Distributioner** på arbetsytan **Övervakning**. Längst ned på skärmen visas ett diagram **över Kompatibilitetsrapport** .  

## <a name="next-steps"></a>Nästa steg 

Mer detaljerad information om hur du övervakar konfigurations bas linjer finns i [övervaka kompatibilitetsinställningar](../../compliance/deploy-use/monitor-compliance-settings.md).  
