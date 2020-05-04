---
title: Introduktion till energisparfunktioner
titleSuffix: Configuration Manager
description: Få en introduktion till energispar funktioner i Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 400fe3113207217504317eeb8ef8bbce4ab6a298
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715223"
---
# <a name="introduction-to-power-management-in-configuration-manager"></a>Introduktion till energispar funktioner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Energispar funktioner i Configuration Manager hanterar behovet av att många organisationer måste övervaka och minska energi förbrukningen för sina datorer. Funktionen tillämpar relevanta och konsekventa inställningar på datorer i organisationen genom att utnyttja energisparfunktionerna som är inbyggda i Windows. Du kan tillämpa olika energiinställningar för datorer under kontorstid och utanför arbetstid. Du kanske till exempel vill tillämpa ett mer restriktivt energischema på datorer utanför arbetstid. Du kan förhindra att inställningar för energisparfunktioner används i fall då datorerna alltid måste vara aktiverade.  

 Energispar funktioner i Configuration Manager innehåller flera rapporter som hjälper dig att analysera energi förbrukning och energi inställningar för datorer i din organisation. Du kan också använda rapporterna för att felsöka problem med energisparfunktionerna.  

 Ett detaljerat arbets flöde om hur du konfigurerar och använder energispar funktioner finns i [Administratörs check lista för](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md)energispar funktioner.  

> [!IMPORTANT]  
>  Configuration Manager energispar funktioner stöds inte på virtuella datorer. Du kan inte använda energischeman på virtuella datorer och inte heller rapportera energidata från dem.  

## <a name="the-power-management-workflow"></a>Arbetsflödet för energisparfunktioner  
 Använd följande tre faser för att planera och implementera energispar funktioner i Configuration Manager.  

### <a name="monitoring-and-planning-phase"></a>Övervaknings- och planeringsfas  
 Energispar funktionerna använder Configuration Manager maskin varu inventering för att samla in data om dator användning och energi inställningar för datorer på platsen. Det finns ett antal rapporter som du kan använda för att analysera data och avgöra de optimala energisparinställningarna för datorer. Under övervaknings- och planeringsfasen i arbetsflödet för energisparfunktioner kan du exempelvis skapa samlingar som baseras på data i rapporten **Energisparfunktioner** och använda den informationen för att identifiera datorer som inte kan hantera energisparfunktioner. Sedan kan du undanta dessa datorer från konfigurationen av energisparfunktioner.  

> [!IMPORTANT]  
>  Tillämpa inte energischeman för datorer på din plats förrän du samlat in och analyserat energiinformationen från klientdatorer. Om du tillämpar nya energisparinställningar på datorerna utan att först ha undersökt de befintliga inställningarna kan det leda till ökad energiförbrukning.  

### <a name="enforcement-phase"></a>Tvångsåtgärdsfas  
 Med energisparfunktioner kan du skapa energischeman som du kan använda för samlingar med datorer på din plats. Dessa energischeman konfigurerar Windows-energisparinställningar på datorer. Du kan använda de energi scheman som ingår i Configuration Manager, eller så kan du konfigurera dina egna anpassade energi scheman. Du kan använda energiinformation som samlas in under övervaknings- och planeringsfasen som utgångspunkt för att utvärdera energisparfunktionerna när du har tillämpat ett energischema på datorer. Mer information finns i [Administratörs check lista för energispar funktioner](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

### <a name="compliance-phase"></a>Kompatibilitetsfas  
 I kompatibilitetsfasen kan du köra rapporter som hjälper dig att utvärdera besparingarna av energiförbrukning och energikostnader i organisationen. Du kan också köra rapporter som beskriver förbättringarna i mängden CO2 som genereras av datorerna. Det finns också rapporter som hjälper dig att kontrollera att energiinställningarna tillämpats korrekt på datorerna och som hjälper dig att felsöka problem med energisparfunktionerna.  
