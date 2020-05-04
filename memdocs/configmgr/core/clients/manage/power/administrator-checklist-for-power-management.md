---
title: Checklista för energisparfunktioner för administratörer
titleSuffix: Configuration Manager
description: Använd check lista för administratörer för att hjälpa dig att planera för och implementera energispar funktioner i Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 94e42cbe-9df8-4228-a04e-0ad7626180ca
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 039ebf73fba9850b8479bfabab6ab928b7d6f2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715286"
---
# <a name="administrator-checklist-for-power-management-in-configuration-manager"></a>Administratörs check lista för energispar funktioner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här check listan för administratörer innehåller rekommenderade steg för att använda Configuration Manager energispar funktioner i din organisation.  

## <a name="configuring-power-management"></a>Konfigurera energisparfunktioner  
 Följ stegen nedan när du ska konfigurera hierarkin för insamling av information om energisparfunktioner från klientdatorer.  

> [!IMPORTANT]  
>  Tillämpa inte energischeman på datorer i hierarkin förrän du har samlat in och analyserat informationen om energisparfunktioner från klientdatorerna. Om du anger nya energisparinställningar på datorerna utan att först ha undersökt de redan inställda, kan det leda till ökad energiförbrukning.  

|Uppgift|Information|  
|----------|-------------|  
|Granska energispar funktionerna i dokumentations biblioteket för Configuration Manager.|Se [Introduktion till energispar funktioner](introduction-to-power-management.md).|  
|Granska kraven för energispar funktioner i dokumentations biblioteket för Configuration Manager.|Se [krav för energispar funktioner](prerequisites-for-power-management.md).|  
|Gå igenom metodtipsen för energisparfunktioner.|Se [metod tips för energispar funktioner](best-practices-for-power-management.md).|  
|Konfigurera samlingarna för att hantera energi förbrukning från datorer i din miljö.|Använd **samlingen för rapportering av bas linje data**, **insamling för rapportering av bas linje data**, **insamling av datorer som inte kan hantera energispar**funktioner, **samlingar med datorer som energi scheman ska tillämpas**på, **samlingar med datorer som energi scheman ska tillämpas**på och **samlingar med datorer som kör Windows Server** för att hjälpa dig att hantera energi inställningar för datorer i hierarkin. Du kan skapa flera samlingar och använda olika energischeman för varje samling.|  
|Aktivera energisparfunktioner.|Innan du kan börja använda energisparfunktioner måste du aktivera dem och konfigurera nödvändiga klientinställningar. Mer information finns i [Konfigurera energispar funktioner](configuring-power-management.md).|  
|Samla in information om energisparfunktioner från klientdatorer.|Energispar funktioner rapporteras av klienter via Configuration Manager maskin varu inventering. Beroende på maskinvaruinventeringsschemat som du har konfigurerat kan det ta lite tid att hämta inventeringen från alla klientdatorer.|  

## <a name="monitoring-and-planning-phase"></a>Övervaknings- och planeringsfas  

|Uppgift|Information|  
|----------|-------------|  
|Kör rapporten **Datoraktivitet**.|Rapporten **Datoraktivitet** innehåller ett diagram över övervaknings-, dator- och användaraktiviteten för en angiven samling under en angiven tidsperiod. Den här rapporten länkar till rapporten **Information om datoraktivitet** som visar viloläges- och väckningsfunktioner för datorer i den angivna samlingen. Mer information finns i [övervaka och planera för energispar funktioner](monitor-and-plan-for-power-management.md).|  
|Kör rapporten **Energiförbrukning** eller **Energiförbrukning per dag**.|Rapporterna **Energiförbrukning** och **Energiförbrukning per dag** visar den totala månatliga strömförbrukningen i kilowatt per timme (kWh) för en angiven samling under en angiven tidsperiod. Mer information finns i [övervaka och planera för energispar funktioner](monitor-and-plan-for-power-management.md).|  
|Kör rapporten **miljö påverkan** eller **miljö påverkan per dag**.|Rapporterna **Miljöpåverkan** och **Miljöpåverkan per dag** visar ett diagram över koldioxidutsläpp (CO2) som sparats av en angiven samling datorer under en angiven tidsperiod. Mer information finns i [övervaka och planera för energispar funktioner](monitor-and-plan-for-power-management.md).|  
|Kör rapporten **Energikostnad** eller **Energikostnad per dag**.|Rapporterna **Energikostnad** och **Energikostnad per dag** visar den totala energiförbrukningskostnaden under en angiven tidsperiod. Mer information finns i [övervaka och planera för energispar funktioner](monitor-and-plan-for-power-management.md).|  
|Kör rapporten **Energifunktioner**.|Rapporten **Energifunktioner** visar energisparfunktionerna för datorer i den angivna samlingen. Mer information finns i [övervaka och planera för energispar funktioner](monitor-and-plan-for-power-management.md).|  
|Kör rapporten **Energiinställningar**.|Rapporten **Energiinställningar** visar en lista med de aktuella energiinställningar som används av datorer i en angiven samling. Mer information finns i [övervaka och planera för energispar funktioner](monitor-and-plan-for-power-management.md).|  
|Undanta samlingar med datorer från energisparfunktioner om det behövs.|Se [Konfigurera energispar funktioner](configuring-power-management.md).|  

> [!IMPORTANT]  
>  Se till att du sparar informationen från energisparrapporter som genereras under övervaknings- och planeringsfasen. Du kan jämföra dessa data med informationen om energisparfunktioner som genereras under tvångsåtgärds- och efterlevnadsfaserna för att utvärdera besparingarna av energiförbrukning, energikostnader och miljöpåverkan tack vare användningen av ett energisparschema för datorer i hierarkin.  

## <a name="enforcement-phase"></a>Tvångsåtgärdsfas  

|Uppgift|Information|  
|----------|-------------|  
|Välj befintliga energischeman eller skapa nya energischeman för samlingar av datorer i din organisation.|Se [hur du skapar och använder energi scheman](create-and-apply-power-plans.md).|  
|Använd dessa energischeman på datorer.|Se [hur du skapar och använder energi scheman](create-and-apply-power-plans.md).|  

## <a name="compliance-phase"></a>Kompatibilitetsfas  

|Uppgift|Information|  
|----------|-------------|  
|Kör rapporten **Datoraktivitet**.|Rapporten **Datoraktivitet** innehåller ett diagram över övervaknings-, dator- och användaraktiviteten för en angiven samling under en angiven tidsperiod. Den här rapporten länkar till rapporten **Energisparfunktioner - information om datoraktivitet** som visar viloläges- och väckningsfunktioner för datorer i den angivna samlingen. Mer information finns i [övervaka och planera för energispar funktioner](monitor-and-plan-for-power-management.md).|  
|Kör rapporten **Energiförbrukning** eller **Energiförbrukning per dag**.|Rapporterna **Energiförbrukning** och **Energiförbrukning per dag** visar den totala månatliga strömförbrukningen i kilowatt per timme (kWh) för en angiven samling under en angiven tidsperiod. Mer information finns i [övervaka och planera för energispar funktioner](monitor-and-plan-for-power-management.md).|  
|Kör rapporten **Miljöpåverkan** eller **Miljöpåverkan per dag**.|Rapporterna **Miljöpåverkan** och **Miljöpåverkan per dag** visar ett diagram över koldioxidutsläpp (CO2) som sparats av en angiven samling datorer under en angiven tidsperiod. Mer information finns i [övervaka och planera för energispar funktioner](monitor-and-plan-for-power-management.md).|  
|Kör rapporten **Energikostnad** eller **Energikostnad per dag**.|Rapporterna **Energikostnad** och **Energikostnad per dag** visar den totala energiförbrukningskostnaden under en angiven tidsperiod. Mer information finns i [övervaka och planera för energispar funktioner](monitor-and-plan-for-power-management.md).|  

## <a name="troubleshooting"></a>Felsökning  

|Uppgift|Information|  
|----------|-------------|  
|Om datorer i hierarkin inte har försatts i strömsparläge eller viloläge kör du en **rapport om enheter som inte använder viloläge** som visar möjliga orsaker.|**Rapporten om enheter som inte använder viloläge** innehåller en lista över vanliga orsaker som har förhindrat datorer från att gå in i strömsparläge eller viloläge och antalet datorer som har påverkats av respektive orsak under en angiven tidsperiod. Mer information finns i [övervaka och planera för energispar funktioner](monitor-and-plan-for-power-management.md).|  
|Om flera energischeman tillämpas på en dator används det minst restriktiva energischemat. Kör rapporten **Datorer med flera scheman** som visar datorer som har flera energischeman.|Se **datorer med flera energi scheman** för [att övervaka och planera för](monitor-and-plan-for-power-management.md)energispar funktioner.|  
