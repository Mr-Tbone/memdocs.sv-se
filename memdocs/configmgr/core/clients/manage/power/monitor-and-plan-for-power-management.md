---
title: Övervaka och planera för energispar funktioner
titleSuffix: Configuration Manager
description: Lär dig att övervaka och planera för energispar funktioner i Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 507bf676-2679-4e4d-8831-3ffc9cf8557e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a4e5ee9c35dd96f79ea1a88ab09200d4386a7535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715216"
---
# <a name="how-to-monitor-and-plan-for-power-management-in-configuration-manager"></a>Övervaka och planera för energispar funktioner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd följande information som hjälp för att övervaka och planera för energispar funktioner i Configuration Manager.  

##  <a name="how-to-use-reports-for-power-management"></a><a name="BKMK_How_to_use_reports"></a> Använda rapporter för energisparfunktioner  
 Energispar funktioner i Configuration Manager innehåller flera rapporter som hjälper dig att analysera energi förbrukning och energi inställningar för datorer i din organisation. Rapporterna kan även användas för att felsöka problem.  

 Innan du kan använda rapporterna måste du konfigurera rapportering för hierarkin. Mer information om rapportering i Configuration Manager finns i [Introduktion till rapportering](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  Information om energispar funktioner som används av dagliga rapporter behålls i Configuration Manager plats databasen i 31 dagar.  
>           Information om energispar funktioner som används av månads rapporter sparas i Configuration Manager plats databasen i 13 månader.  
>   
>  När du kör rapporter under övervaknings-och planerings-och Compliance-faserna i energispar funktioner, sparar eller exporterar du resultaten från alla rapporter som du vill behålla data för senare jämförelse om de senare tas bort av Configuration Manager.  

## <a name="list-of-power-management-reports"></a>Lista över rapporter för energisparfunktioner  
 I följande lista beskrivs de energispar funktioner som är tillgängliga i Configuration Manager.  

> [!NOTE]  
>  Rapporterna visar antalet fysiska datorer och antalet virtuella datorer i en viss samling. Dock visas endast information om energisparfunktioner från fysiska datorer i rapporterna för energisparfunktioner.  

###  <a name="computer-activity-report"></a><a name="BKMK_Activity"></a> Rapport över datoraktivitet  
 Rapporten **Datoraktivitet** innehåller ett diagram som visar följande aktivitet för en angiven samling under en angiven period:  

- **Dator på** – Datorn har slagits på.  

- **Skärm på** – Skärmen har slagits på.  

- **Användaren är aktiv** – aktivitet har upptäckts från dator musen, dator tangent bordet eller från en fjärr skrivbords anslutning till datorn  

  Den här rapporten används under övervaknings-, planerings- och tvångsåtgärdsfaserna och hjälper dig att förstå sambandet mellan dator-, övervaknings- och användaraktivitet under en 24-timmarsperiod. Om du kör rapporten över ett antal dagar slås informationen under perioden ihop. Den här rapporten hjälper dig att fastställa typiska kontorstimmar (hög belastning) och tider utanför kontorstid (låg belastning) för en vald samling så att det blir lättare att bestämma när konfigurerade energischeman ska tillämpas.  

  Diagrammet visar tidsperioder då en dator kan vara påslagen, men utan användaraktivitet. Överväg att använda mer restriktiva inställningar under dessa tider för att spara på energikostnaderna för datorer som är igång, men som inte används. En dator räknas som aktiv om det har förekommit dator-, användar- eller övervakningsaktivitet minst en minut under en timme som återges i diagrammet. Om en dator inte rapporterar data för energisparfunktioner tas den inte med i rapporten **Datoraktivitet** .  

  Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Startdatum**|Välj startdatum för rapporten i listrutan.|  
|**Slutdatum (valfritt)**|Välj ett valfritt slutdatum för rapporten i listrutan.|  
|**Samlingsnamn**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Enhets typ**|Välj den typ av dator som du vill köra en rapport för i listrutan. Giltiga värden är **alla** (både Station ära och bärbara datorer), **Skriv bord** (endast Station ära datorer) och **bärbar dator** (endast bärbara datorer).|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Den här rapporten har inga dolda parametrar som du kan ange.  

#### <a name="report-links"></a>Rapportlänkar  
 Om inget värde anges för **Slutdatum (valfritt)** innehåller den här rapporten en länk till följande rapport som innehåller ytterligare information.  

|Rapportnamn|Information|  
|-----------------|-------------|  
|**Information om datoraktivitet**|Klicka på länken **Klicka för att visa detaljerad information** om du vill visa en lista över aktiva, inaktiva och icke-rapporterande datorer för det angivna datumet.<br /><br /> Mer information finns i [Computer Activity Details Report](#BKMK_Activity_Details) i det här ämnet.|  

###  <a name="computer-activity-by-computer-report"></a><a name="BKMK_Comp_Activity_by_computer"></a> Rapporten Energifunktionsaktivitet per dator  
 Rapporten **Energifunktionsaktivitet per dator** innehåller ett diagram som visar följande aktivitet för en angiven dator på ett angivet datum:  

- **Dator på** – Datorn har slagits på.  

- **Skärm på** – Skärmen har slagits på.  

- **Användaren är aktiv** – Aktivitet har upptäckts från datormusen, tangentbordet eller från en fjärrskrivbordsanslutning till datorn.  

  Den här rapporten kan köras separat eller anropas av rapporten **Information om datoraktivitet** .  

> [!NOTE]  
>  Information om datoraktivitet samlas in från klientdatorer under en maskinvaruinventering. Beroende på när maskinvaruinventeringen körs kan information samlas in då ett energischema för hög eller låg belastning tillämpas.  

 Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Rapportdatum**|Välj ett datum för rapporten i listrutan.|  
|**Dator namn**|Ange namnet på en dator som du vill köra en rapport för.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Den här rapporten har inga dolda parametrar som du kan ange.  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten innehåller länkar till följande rapport som innehåller ytterligare information om det valda objektet.  

|Rapportnamn|Information|  
|-----------------|-------------|  
|**Information om dator**|Klicka på länken **Klicka för att visa detaljerad information** om du vill visa energisparfunktioner, energiinställningar och energischeman som används för den valda datorn.|  

###  <a name="computer-activity-details-report"></a><a name="BKMK_Activity_Details"></a> Computer Activity Details report  
 Rapporten **Information om datoraktivitet** visar en lista över aktiva eller inaktiva datorer med deras viloläges- och väckningsfunktioner. Den här rapporten anropas av [Computer Activity Report](#BKMK_Activity) och är inte avsedd att köras direkt av platsadministratören.  

 Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Samlingsnamn**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Rapportdatum**|Välj ett datum för rapporten i listrutan.|  
|**Rapportera tid**|Välj en tid i listrutan för det angivna datumet då du vill köra rapporten. Giltiga värden är mellan **00:00** och **23:00**.|  
|**Datortillstånd**|Välj det datortillstånd i listrutan som du vill köra rapporten för. Giltiga värden är **alla** (datorer som har Aktiver ATS eller inaktiverats), **på** (datorer som var aktiverade) och **av** (datorer som var inaktiverade, i ström spar läge eller i vilo läge). Dessa värden returneras bara för den valda rapporterings perioden.|  
|**Enhets typ**|Välj den typ av dator som du vill köra en rapport för i listrutan. Giltiga värden är **alla** (både Station ära och bärbara datorer), **Skriv bord** (endast Station ära datorer) och **bärbar dator** (endast bärbara datorer). Dessa värden returneras bara för den valda rapporterings perioden.|  
|**Sparlägeskapabel**|Välj i listrutan om du vill visa datorer som kan försättas i strömsparläge i rapporten. Giltiga värden är **alla** (datorer som stöder och är inkompatibla med vilo läge), **Nej** (datorer som inte är kompatibla med vilo läge) och **Ja** (datorer som kan vila).|  
|**Klarar väckning från strömsparläge**|Välj i listrutan om du vill visa datorer som kan väckas från strömsparläge i rapporten. Giltiga värden är **alla** (datorer som stöder och inte kan väckas från vilo läge), **Nej** (datorer som inte kan väckas från vilo läge) och **Ja** (datorer som kan väckas från vilo läge).|  
|**Energischema**|Välj vilka energischematyper i listrutan som du vill visa i rapporten. Giltiga värden är **alla** (datorer som inte har några energi hanterings planer tillämpade. datorer som har en energi hanterings plan tillämpad. datorer som undantas från energispar funktioner), har **inte angetts** (datorer som inte har någon energi hanterings plan tillämpad), **definierat** (datorer som har en energispar funktioner) och **exkluderas** (datorer som har uteslutits från energispar funktioner)|  
|**Operativsystem**|Välj de operativsystem i listrutan som du vill visa i rapporten eller välj **Alla** om du vill visa alla operativsystem.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Den här rapporten har inga dolda parametrar som du kan ange.  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten innehåller länkar till följande rapport som innehåller ytterligare information om det valda objektet.  

|Rapportnamn|Information|  
|-----------------|-------------|  
|**Energifunktionsaktivitet per dator**|Klicka på ett dator namn om du vill se en viss aktivitet för datorn under en vald rapporterings period. Följande aktiviteter inkluderar **dator på** (har datorn Aktiver ATS?), **övervaka på** (har övervakaren aktive rad?) och **användaren är aktiv** (aktivitet har upptäckts från datorns mus, tangent bord eller fjärr skrivbords anslutning).<br /><br /> Mer information finns i [Computer Activity by Computer Report](#BKMK_Comp_Activity_by_computer) i det här ämnet.|  

###  <a name="computer-details-report"></a><a name="BKMK_Computer_Details"></a> Rapporten Datorinformation  
 Rapporten **Datorinformation** visar detaljerad information om energisparfunktioner, energiinställningar och energischeman som tillämpas på en angiven dator. Rapporten anropas av rapporten **Energifunktionsaktivitet per dator** , rapporten **Datorer med flera scheman** , rapporten **Energisparfunktioner** och rapporten **Information om energiinställningar** . Den är inte avsedd att köras direkt av platsadministratören.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Dator namn**|Ange namnet på en dator som du vill köra en rapport för.|  
|**Energi spar läge**|Välj den typ av energisparinställningar i listrutan som du vill visa i rapportresultatet. Välj **Ansluten** om du vill visa energiinställningarna som konfigurerats för när datorn är ansluten och **Vid batteridrift** om du vill visa energiinställningarna för när datorn körs med batteridrift.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Den här rapporten har inga dolda parametrar som du kan ange.  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten länkar inte till några andra rapporter om energisparfunktioner.  

###  <a name="computer-not-reporting-details-report"></a><a name="BKMK_Not_Reporting"></a> Rapporten Datorer som inte skickar någon information  
 Rapporten **Datorer som inte skickar någon information** visar en lista med datorer i en angiven samling som inte har rapporterat någon energiaktivitet vid ett angivet datum och en angiven tid. Den här rapporten anropas av **Computer Activity Report** och är inte avsedd att köras direkt av platsadministratören.  

> [!NOTE]  
>  Datorer rapporterar information om energisparfunktioner som en del av deras maskinvaruinventeringsschema. Innan du betraktar en dator som icke-rapporterande kontrollerar du att den har rapporterat maskinvaruinventering.  

 Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Samlingsnamn**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Rapportdatum**|Välj ett datum för rapporten i listrutan.|  
|**Rapportera tid**|Välj en tid i listrutan för det angivna datumet då du vill köra rapporten. Giltiga värden är mellan **00:00** och **23:00**.|  
|**Enhets typ**|Välj den typ av dator som du vill köra en rapport för i listrutan. Giltiga värden är **alla** (både Station ära och bärbara datorer), **Skriv bord** (endast Station ära datorer) och **bärbar dator** (endast bärbara datorer). Dessa värden returneras bara för den valda rapporterings perioden.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Den här rapporten har inga dolda parametrar som du kan ange.  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten länkar inte till några andra rapporter om energisparfunktioner.  

###  <a name="computers-excluded"></a><a name="BKMK_Excluded"></a> Undantagna datorer  
 Rapporten **undantagna datorer** visar en lista med datorer i en angiven samling som har uteslutits från Configuration Manager energispar funktioner.  

 Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Samling**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Orsak**|Välj en orsak i listrutan som förklarar varför datorerna undantagits från energisparfunktionerna. Du kan visa **alla** (alla undantagna datorer) som **uteslutits av administratören** (endast datorer som uteslutits av en administrativ användare) och **exkluderas av användaren** (endast datorer som uteslutits av en användare i Software Center).|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Den här rapporten har inga dolda parametrar som du kan ange.  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten innehåller länkar till följande rapport som innehåller ytterligare information om det valda objektet.  

|Rapportnamn|Information|  
|-----------------|-------------|  
|**Information om energisparfunktioner för dator**|Klicka på ett datornamn om du vill visa energisparfunktioner, energiinställningar och energischeman för den valda datorn.<br /><br /> Mer information finns i [Computer Details Report](#BKMK_Computer_Details) i det här ämnet.|  

###  <a name="computers-with-multiple-power-plans"></a><a name="BKMK_Multiple"></a> Datorer med flera scheman  
 Rapporten **Datorer med flera scheman** visar en lista med datorer som är medlemmar i flera samlingar, och som alla har olika energischeman. För varje dator med energiinställningar som potentiellt är i konflikt med varandra visar rapporten datornamnet och de energischeman som tillämpas för varje samling som datorn är medlem i.  

> [!IMPORTANT]  
>  Om en dator är medlem i flera samlingar, där varje samling har olika energi scheman, används minst restriktivt energi schema.  
>   
>  Om en dator är medlem i flera samlingar, där varje samling har olika Väcknings tider, kommer tiden närmast midnatt att användas.  

 Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Samlingsnamn**|Välj den samling i listrutan som du vill använda för rapporten.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Den här rapporten har inga dolda parametrar som du kan ange.  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten innehåller länkar till följande rapport som innehåller ytterligare information om det valda objektet.  

|Rapportnamn|Information|  
|-----------------|-------------|  
|**Information om energisparfunktioner för dator**|Klicka på ett datornamn om du vill visa energisparfunktioner, energiinställningar och energischeman för den valda datorn.<br /><br /> Mer information finns i [Computer Details Report](#BKMK_Computer_Details) i det här ämnet.|  

###  <a name="energy-consumption-report"></a><a name="BKMK_Consumption"></a> Rapporten Energiförbrukning  
 Rapporten **Energiförbrukning** visar följande information:  

- Ett diagram som visar den totala månatliga energiförbrukningen för datorer i kilowatt per timme (kWh) i den angivna samlingen under den angivna tidsperioden.  

- Ett diagram som visar den genomsnittliga energiförbrukningen i kilowatt per timme (kWh) för varje dator i den angivna samlingen under den angivna tidsperioden.  

- En tabell som visar den totala månatliga energiförbrukningen i kilowatt per timme (kWh) och den genomsnittliga energiförbrukningen för datorer i den angivna samlingen under den angivna tidsperioden.  

  Den här informationen hjälper dig att förstå energiförbrukningen i din miljö. När du har tillämpat ett energischema på datorer i den valda samlingen bör datorernas energiförbrukning minska.  

> [!NOTE]  
>  Om du lägger till eller tar bort medlemmar i samlingen när du har tillämpat ett energischema kommer detta att påverka resultatet i rapporten **Energiförbrukning** och kan göra det svårare att jämföra resultatet från övervaknings-, planerings- och tvångsåtgärdsfasen.  

 Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Startdatum**|Välj ett startdatum för rapporten i listrutan.|  
|**Slutdatum**|Välj ett slutdatum för rapporten i listrutan.|  
|**Samlingsnamn**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Enhets typ**|Välj den typ av dator som du vill köra en rapport för i listrutan. Giltiga värden är **alla** (både Station ära och bärbara datorer), **Skriv bord** (endast Station ära datorer) och **bärbar dator** (endast bärbara datorer). Dessa värden returneras bara för den valda rapporterings perioden.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Om du vill kan du ange följande dolda parametrar som ändrar rapportens beteende.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Stationär dator på**|Ange energiförbrukningen för en stationär dator när den är påslagen. Standardvärdet är **0,07** kW per timme.|  
|**Bärbar dator på**|Ange energiförbrukningen för en bärbar dator när den är påslagen. Standardvärdet är **0,02** kW per timme.|  
|**Stationär dator i strömsparläge**|Ange energiförbrukningen för en stationär dator som har försatts i strömsparläge. Standardvärdet är **0,003** kW per timme.|  
|**Bärbar dator viloläge**|Ange energiförbrukningen för en bärbar dator som har försatts i viloläge. Standardvärdet är **0,001** kW per timme.|  
|**Stationär dator av**|Ange energiförbrukningen för en stationär dator när den är avstängd. Standardvärdet är **0** kW per timme.|  
|**Bärbar dator av**|Ange energiförbrukningen för en bärbar dator när den är avstängd. Standardvärdet är **0** kW per timme.|  
|**Stationär bildskärm på**|Ange energiförbrukningen för bildskärmen på en stationär dator när den är påslagen. Standardvärdet är **0,028** kW per timme.|  
|**Bärbar dators skärm på**|Ange energiförbrukningen för bildskärmen på en bärbar dator när den är påslagen. Standardvärdet är **0** kW per timme.|  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten länkar inte till några andra rapporter om energisparfunktioner.  

###  <a name="energy-consumption-by-day-report"></a><a name="BKMK_Consumption_by_Day"></a> Rapporten Energiförbrukning per dag  
 Rapporten **Energiförbrukning per dag** visar följande information:  

- Ett diagram som visar den totala dagliga energiförbrukningen för datorer i kilowatt per timme (kWh) i den angivna samlingen under de senaste 31 dagarna.  

- Ett diagram som visar den genomsnittliga dagliga energiförbrukningen i kilowatt per timme (kWh) för varje dator i den angivna samlingen under de senaste 31 dagarna.  

- En tabell som visar den totala dagliga energiförbrukningen i kilowatt per timme (kWh) och den genomsnittliga dagliga energiförbrukningen för datorer i den angivna samlingen under de senaste 31 dagarna.  

  Den här informationen hjälper dig att förstå energiförbrukningen i din miljö. När du har tillämpat ett energischema på datorer i den valda samlingen bör datorernas energiförbrukning minska.  

> [!NOTE]  
>  Om du lägger till eller tar bort medlemmar i samlingen när du har tillämpat ett energischema kommer detta att påverka resultatet i rapporten **Energiförbrukning** och kan göra det svårare att jämföra resultatet från övervaknings-, planerings- och tvångsåtgärdsfasen.  

 Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Samling**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Enhetstyp**|Välj den typ av dator i listrutan som du vill köra en rapport för. Giltiga värden är **alla** (både Station ära och bärbara datorer), **Skriv bord** (endast Station ära datorer) och **bärbar dator** (endast bärbara datorer). Dessa värden returneras bara för den valda rapporterings perioden.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Om du vill kan du ange följande dolda parametrar som ändrar rapportens beteende.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Stationär dator på**|Ange energiförbrukningen för en stationär dator när den är påslagen. Standardvärdet är **0,07** kW per timme.|  
|**Bärbar dator på**|Ange energiförbrukningen för en bärbar dator när den är påslagen. Standardvärdet är **0,02** kW per timme.|  
|**Stationär dator i strömsparläge**|Ange energiförbrukningen för en stationär dator som har försatts i strömsparläge. Standardvärdet är **0,003** kW per timme.|  
|**Bärbar dator viloläge**|Ange energiförbrukningen för en bärbar dator som har försatts i viloläge. Standardvärdet är **0,001** kW per timme.|  
|**Stationär dator av**|Ange energiförbrukningen för en stationär dator när den är avstängd. Standardvärdet är **0** kW per timme.|  
|**Bärbar dator av**|Ange energiförbrukningen för en bärbar dator när den är avstängd. Standardvärdet är **0** kW per timme.|  
|**Stationär bildskärm på**|Ange energiförbrukningen för bildskärmen på en stationär dator när den är påslagen. Standardvärdet är **0,028** kW per timme.|  
|**Bärbar dators skärm på**|Ange energiförbrukningen för bildskärmen på en bärbar dator när den är påslagen. Standardvärdet är **0** kW per timme.|  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten länkar inte till några andra rapporter om energisparfunktioner.  

###  <a name="energy-cost-report"></a><a name="BKMK_Cost"></a> Rapporten Energikostnader  
 Rapporten **Energikostnader** visar följande information:  

- Ett diagram som visar den totala månatliga energikostnaden för datorer i den angivna samlingen under den angivna tidsperioden.  

- Ett diagram som visar den genomsnittliga månatliga energikostnaden för varje dator i den angivna samlingen under den angivna tidsperioden.  

- En tabell som visar den totala månatliga energikostnaden och den genomsnittliga månatliga energikostnaden för datorer i den angivna samlingen under de senaste 31 dagarna.  

  Den här informationen hjälper dig att förstå energikostnaderna i din miljö. När du har tillämpat ett energischema på datorer i den valda samlingen bör datorernas energikostnad minska.  

  Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Startdatum**|Välj ett startdatum för rapporten i listrutan.|  
|**Slutdatum**|Välj ett slutdatum för rapporten i listrutan.|  
|**Kostnad för kWh**|Ange kostnaden per kWh elektricitet. Standardvärdet är **0,09**.<br /><br /> Du kan ändra valutan som används i den här rapporten i avsnittet för dolda parametrar.|  
|**Samlingsnamn**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Enhets typ**|Välj den typ av dator i listrutan som du vill köra en rapport för. Giltiga värden är **alla** (både Station ära och bärbara datorer), **Skriv bord** (endast Station ära datorer) och **bärbar dator** (endast bärbara datorer). Dessa värden returneras bara för den valda rapporterings perioden.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Om du vill kan du ange följande dolda parametrar som ändrar rapportens beteende.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Stationär dator på**|Ange energiförbrukningen för en stationär dator när den är påslagen. Standardvärdet är **0,07** kW per timme.|  
|**Bärbar dator på**|Ange energiförbrukningen för en bärbar dator när den är påslagen. Standardvärdet är **0,02** kW per timme.|  
|**Stationär dator i strömsparläge**|Ange energiförbrukningen för en stationär dator som har försatts i strömsparläge. Standardvärdet är **0,003** kW per timme.|  
|**Bärbar dator viloläge**|Ange energiförbrukningen för en bärbar dator som har försatts i viloläge. Standardvärdet är **0,001** kW per timme.|  
|**Stationär dator av**|Ange energiförbrukningen för en stationär dator när den är avstängd. Standardvärdet är **0** kW per timme.|  
|**Bärbar dator av**|Ange energiförbrukningen för en bärbar dator när den är avstängd. Standardvärdet är **0** kW per timme.|  
|**Stationär bildskärm på**|Ange energiförbrukningen för bildskärmen på en stationär dator när den är påslagen. Standardvärdet är **0,028** kW per timme.|  
|**Bärbar dators skärm på**|Ange energiförbrukningen för bildskärmen på en bärbar dator när den är påslagen. Standardvärdet är **0** kW per timme.|  
|**Valuta**|Ange valutan som ska användas för den här rapporten. Standardvärdet är **USD ($)**.|  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten länkar inte till några andra rapporter om energisparfunktioner.  

###  <a name="energy-cost-by-day-report"></a><a name="BKMK_Cost_by_Day"></a> Rapporten Energikostnad per dag  
 Rapporten **Energikostnad per dag** visar följande information:  

- Ett diagram som visar den totala dagliga energikostnaden för datorer i den angivna samlingen under de senaste 31 dagarna.  

- Ett diagram som visar den genomsnittliga dagliga energikostnaden för varje dator i den angivna samlingen under de senaste 31 dagarna.  

- En tabell som visar den totala dagliga energikostnaden och den genomsnittliga dagliga energikostnaden för datorer i den angivna samlingen under de senaste 31 dagarna.  

  Den här informationen hjälper dig att förstå energikostnaderna i din miljö. När du har tillämpat ett energischema på datorer i den valda samlingen bör datorernas energikostnad minska.  

  Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Samlingsnamn**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Enhets typ**|Välj den typ av dator i listrutan som du vill köra en rapport för. Giltiga värden är **alla** (både Station ära och bärbara datorer), **Skriv bord** (endast Station ära datorer) och **bärbar dator** (endast bärbara datorer). Dessa värden returneras bara för den valda rapporterings perioden.|  
|**Kostnad för kWh**|Ange kostnaden per kWh elektricitet. Standardvärdet är **0,09**.<br /><br /> Du kan ändra valutan som används i den här rapporten i avsnittet för dolda parametrar.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Om du vill kan du ange följande dolda parametrar som ändrar rapportens beteende.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Stationär dator på**|Ange energiförbrukningen för en stationär dator när den är påslagen. Standardvärdet är **0,07** kW per timme.|  
|**Bärbar dator på**|Ange energiförbrukningen för en bärbar dator när den är påslagen. Standardvärdet är **0,02** kW per timme.|  
|**Stationär dator i strömsparläge**|Ange energiförbrukningen för en stationär dator som har försatts i strömsparläge. Standardvärdet är **0,003** kW per timme.|  
|**Bärbar dator viloläge**|Ange energiförbrukningen för en bärbar dator som har försatts i viloläge. Standardvärdet är **0,001** kW per timme.|  
|**Stationär dator av**|Ange energiförbrukningen för en stationär dator när den är avstängd. Standardvärdet är **0** kW per timme.|  
|**Bärbar dator av**|Ange energiförbrukningen för en bärbar dator när den är avstängd. Standardvärdet är **0** kW per timme.|  
|**Stationär bildskärm på**|Ange energiförbrukningen för bildskärmen på en stationär dator när den är påslagen. Standardvärdet är **0,028** kW per timme.|  
|**Bärbar dators skärm på**|Ange energiförbrukningen för bildskärmen på en bärbar dator när den är påslagen. Standardvärdet är **0** kW per timme.|  
|**Valuta**|Ange valutan som ska användas för den här rapporten. Standardvärdet är **USD ($)**.|  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten länkar inte till några andra rapporter om energisparfunktioner.  

###  <a name="environmental-impact-report"></a><a name="BKMK_Environmental_Impact"></a> Rapporten Miljöpåverkan  
 Rapporten **Miljöpåverkan** visar följande information:  

- Ett diagram som visar den totala månatliga koldioxid som genererats (i ton) för datorer i den angivna samlingen under den angivna tids perioden.  

- Ett diagram som visar den genomsnittliga månatliga koldioxid som genererats (i ton) för varje dator i den angivna samlingen under den angivna tids perioden.  

- En tabell som visar den totala månatliga koldioxid som genereras och den genomsnittliga månatliga CO2 som genereras för datorer i den angivna samlingen under den angivna tids perioden.  

  Rapporten **miljö påverkan** beräknar den mängd koldioxid som genereras (i ton) genom att använda den tid som en dator eller Övervakare var aktive rad under en 24-timmarsperiod.  

  Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Rapportstartdatum**|Välj ett startdatum för rapporten i listrutan.|  
|**Rapportslutdatum**|Välj ett slutdatum för rapporten i listrutan.|  
|**Samlingsnamn**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Enhets typ**|Välj den typ av dator som du vill köra en rapport för i listrutan. Giltiga värden är **alla** (både Station ära och bärbara datorer), **Skriv bord** (endast Station ära datorer) och **bärbar dator** (endast bärbara datorer). Dessa värden returneras bara för den valda rapporterings perioden.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Om du vill kan du ange följande dolda parametrar som ändrar rapportens beteende.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Stationär dator på**|Ange energiförbrukningen för en stationär dator när den är påslagen. Standardvärdet är **0,07** kW per timme.|  
|**Bärbar dator på**|Ange energiförbrukningen för en bärbar dator när den är påslagen. Standardvärdet är **0,02** kW per timme.|  
|**Stationär dator i strömsparläge**|Ange energiförbrukningen för en stationär dator som har försatts i strömsparläge. Standardvärdet är **0,003** kW per timme.|  
|**Bärbar dator viloläge**|Ange energiförbrukningen för en bärbar dator som har försatts i viloläge. Standardvärdet är **0,001** kW per timme.|  
|**Stationär dator av**|Ange energiförbrukningen för en stationär dator när den är avstängd. Standardvärdet är **0** kW per timme.|  
|**Bärbar dator av**|Ange energiförbrukningen för en bärbar dator när den är avstängd. Standardvärdet är **0** kW per timme.|  
|**Stationär bildskärm på**|Ange energiförbrukningen för bildskärmen på en stationär dator när den är påslagen. Standardvärdet är **0,028** kW per timme.|  
|**Bärbar dators skärm på**|Ange energiförbrukningen för bildskärmen på en bärbar dator när den är påslagen. Standardvärdet är **0** kW per timme.|  
|**Kolfaktor (ton/kWh)** (CO2Mix)|Ange värdet för kolfaktor (i ton per kWh) som du normalt kan få från ditt elbolag. Standardvärdet är **0,0015** ton per kWh.|  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten länkar inte till några andra rapporter om energisparfunktioner.  

###  <a name="environmental-impact-by-day-report"></a><a name="BKMK_Environmental_Impact_by_Day"></a> Rapporten Miljöpåverkan per dag  
 Rapporten **Miljöpåverkan per dag** visar följande information:  

- Ett diagram som visar den totala dagliga koldioxid som genererats (i ton) för datorer i den angivna samlingen under de senaste 31 dagarna.  

- Ett diagram som visar den genomsnittliga dagliga koldioxid som genererats (i ton) för varje dator i den angivna samlingen under de senaste 31 dagarna.  

- En tabell som visar den totala dagliga koldioxid som genererats och den genomsnittliga dagliga koldioxid som genereras för datorer i den angivna samlingen under de senaste 31 dagarna.  

  Rapporten **miljö påverkan per dag** BERÄKNAR mängden koldioxid som genereras (i ton) genom att använda den tid som en dator eller Övervakare var aktiv under en 24-timmarsperiod.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Samlingsnamn**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Enhets typ**|Välj den typ av dator i listrutan som du vill köra en rapport för. Giltiga värden är **alla** (både Station ära och bärbara datorer), **Skriv bord** (endast Station ära datorer) och **bärbar dator** (endast bärbara datorer). Dessa värden returneras bara för den valda rapporterings perioden.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Om du vill kan du ange följande dolda parametrar som ändrar rapportens beteende.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Stationär dator på**|Ange energiförbrukningen för en stationär dator när den är påslagen. Standardvärdet är **0,07** kWh.|  
|**Bärbar dator på**|Ange energiförbrukningen för en bärbar dator när den är påslagen. Standardvärdet är **0,02** kWh.|  
|**Stationär dator av**|Ange energiförbrukningen för en stationär dator när den är avstängd. Standardvärdet är **0** kWh.|  
|**Bärbar dator av**|Ange energiförbrukningen för en bärbar dator när den är avstängd. Standardvärdet är **0** kWh.|  
|**Stationär dator i strömsparläge**|Ange energiförbrukningen för en stationär dator som har försatts i strömsparläge. Standardvärdet är **0,003** kWh.|  
|**Bärbar dator viloläge**|Ange energiförbrukningen för en bärbar dator som har försatts i viloläge. Standardvärdet är **0,001** kWh.|  
|**Stationär bildskärm på**|Ange energiförbrukningen för bildskärmen på en stationär dator när den är påslagen. Standardvärdet är **0,028** kWh.|  
|**Bärbar dators skärm på**|Ange energiförbrukningen för bildskärmen på en bärbar dator när den är påslagen. Standardvärdet är **0** kWh.|  
|**Kolfaktor (ton/kWh)** (CO2Mix)|Ange ett värde för kolfaktorn (i ton per kWh) som du normalt kan få från ditt elbolag. Standardvärdet är **0,0015** ton per kWh.|  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten länkar inte till några andra rapporter om energisparfunktioner.  

###  <a name="insomnia-computer-details-report"></a><a name="BKMK_Insomnia_Computer_Details"></a> Rapporten Information om datorer som inte använder viloläge  
 Rapporten **Information om datorer som inte använder viloläge** visar en lista med datorer som inte försattes i viloläge eller strömsparläge av en viss anledning inom en angiven tidsperiod. Den här rapporten anropas av **rapporten om enheter som inte använder viloläge** och är inte avsedd att köras direkt av platsadministratören.  

 **Rapporten om enheter som inte använder viloläge** visar datorer som **Inte strömsparlägeskapabel** om de inte stöder strömsparläge och har varit påslagna under hela det angivna rapportintervallet. Rapporten visar datorer som **Inte vilolägeskapabel** om de inte stöder viloläge och har varit påslagna under hela det angivna rapportintervallet.  

> [!NOTE]  
>  Energisparfunktioner kan endast samla in orsaker som förhindrat att datorer försatts i strömsparläge eller viloläge för datorer som kör Windows 7 eller Windows Server 2008 R2.  

 Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Samlingsnamn**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Rapportintervall (dagar)**|Ange antalet dagar som du vill rapportera. Standardvärdet är **7** dagar.|  
|**Orsaken till sömnlöshet**|Välj en av orsakerna i listrutan som kan förhindra att datorer försätts i strömsparläge eller viloläge.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Den här rapporten har inga dolda parametrar som du kan ange.  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten innehåller länkar till följande rapport som innehåller ytterligare information om det valda objektet.  

|Rapportnamn|Information|  
|-----------------|-------------|  
|**Information om dator**|Klicka på länken **Klicka för att visa detaljerad information** om du vill visa energisparfunktioner, energiinställningar och energischeman som används för den valda datorn.<br /><br /> Mer information finns i [Computer Details Report](#BKMK_Computer_Details) i det här ämnet.|  

###  <a name="insomnia-report"></a><a name="BKMK_Insomnia"></a> Insomnia report  
 **Rapporten om enheter som inte använder viloläge** innehåller en lista över vanliga orsaker som har förhindrat datorer från att gå in i strömsparläge eller viloläge och antalet datorer som har påverkats av respektive orsak under en angiven tidsperiod. Det finns ett antal orsaker som kan förhindra att en dator försätts i strömsparläge eller viloläge, till exempel en process som körs på datorn, en öppen fjärrskrivbordssession eller att datorn inte stöder strömsparläge eller viloläge. I den här rapporten kan du öppna rapporten **Information om datorer som inte använder viloläge** som visar en lista med datorer som påverkas av respektive orsak till att datorer inte försätts i strömsparläge eller viloläge.  

 Rapporten om enheter som inte använder viloläge visar datorer som **Inte strömsparlägeskapabel** om de inte stöder strömsparläge och har varit påslagna under hela det angivna rapportintervallet. Rapporten visar datorer som **Inte vilolägeskapabel** om de inte stöder viloläge och har varit påslagna under hela det angivna rapportintervallet.  

> [!NOTE]  
>  Energisparfunktioner kan endast samla in orsaker som förhindrat att datorer försatts i strömsparläge eller viloläge för datorer som kör Windows 7 eller Windows Server 2008 R2.  

 Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Samlingsnamn**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Rapportintervall (dagar)**|Ange antalet dagar som du vill rapportera. Standardvärdet är **7** dagar. Det högsta värdet är **365** dagar. Ange **0** om du vill köra rapporten för i dag.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Den här rapporten har inga dolda parametrar som du kan ange.  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten innehåller länkar till följande rapport som innehåller ytterligare information om det valda objektet.  

|Rapportnamn|Information|  
|-----------------|-------------|  
|**Information om datorer som inte använder viloläge**|Klicka på ett nummer i kolumnen **Berörda datorer** om du vill visa en lista med datorer som inte kunde försättas i strömsparläge eller viloläge på grund av den valda orsaken.<br /><br /> Mer information finns i [Insomnia Computer Details Report](#BKMK_Insomnia_Computer_Details) i det här ämnet.|  

###  <a name="power-capabilities-report"></a><a name="BKMK_Capabilites"></a> Rapporten Energisparfunktioner  
 Rapporten **Energifunktioner** visar maskinvarubaserade energisparfunktioner för datorer i den angivna samlingen. Den här rapporten används vanligtvis i övervakningsfasen för att fastställa energisparfunktionerna för datorer i organisationen. Informationen som visas i rapporten kan sedan användas för att skapa samlingar med datorer som energischeman ska tillämpas på, eller som ska undantas från energisparfunktioner. Energisparfunktionerna som visas i den här rapporten är:  

- **Sparlägeskapabel** – Anger om datorn kan försättas i sparläge om den har konfigurerats att göra det.  

- **Vilolägeskapabel** – Anger om datorn kan försättas i viloläge om den har konfigurerats att göra det.  

- **Väckning från strömsparläge** – Anger om datorn kan väckas från strömsparläge om den har konfigurerats att göra det.  

- **Väckning från viloläge** – Anger om datorn kan väckas från viloläge om den har konfigurerats att göra det.  

  Värdena som rapporteras i rapporten **Energisparfunktioner** anger viloläges- och strömsparfunktionerna för datorer så som de rapporteras i Windows. Rapportvärdena återger dock inte fall där Windows- eller BIOS-inställningar hindrar dessa funktioner från att fungera.  

  Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Samling**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**Visa filter**|I list rutan väljer du **stöds inte** för att endast visa datorer i den angivna samlingen som inte kan vila, vilo läge, väckning från vilo läge eller väckning från vilo läge. Välj **Visa alla** för att visa alla datorer i den angivna samlingen.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Den här rapporten har inga dolda parametrar som du kan ange.  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten innehåller länkar till följande rapport som innehåller ytterligare information om det valda objektet.  

|Rapportnamn|Information|  
|-----------------|-------------|  
|**Information om dator**|Klicka på ett datornamn om du vill visa energisparfunktioner, energiinställningar och energischeman för den valda datorn.<br /><br /> Mer information finns i [Computer Details Report](#BKMK_Computer_Details) i det här ämnet.|  

###  <a name="power-settings-report"></a><a name="BKMK_Settings"></a> Rapporten Energiinställningar  
 Rapporten **Energiinställningar** visar en lista med energiinställningar som används av datorer i den angivna samlingen. För varje energiinställning visas möjliga energisparlägen, värden och enheter, tillsammans med antalet datorer som använder dessa värden. Den här rapporten kan användas under övervakningsfasen och hjälper administratören att se vilka befintliga energiinställningar som används av datorerna på platsen samt att planera för optimala energisparinställningar som ska tillämpas med hjälp av ett energischema. Rapporten är också användbar vid felsökning för att kontrollera att energiinställningarna har tillämpats korrekt.  

> [!NOTE]  
>  Inställningarna som visas samlas in från klientdatorer under maskinvaruinventeringen. Beroende på när maskinvaruinventeringen körs kan inställningar samlas in från aktiva energischeman för hög eller låg belastning.  

 Du kan använda följande parametrar för att konfigurera den här rapporten.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Samlingsnamn**|Välj den samling i listrutan som du vill använda för rapporten.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Om du vill kan du ange följande dolda parametrar som ändrar rapportens beteende.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Ange på hur många språk du vill visa namnen på energiinställningarna som rapporteras av klientdatorerna. Om du bara vill visa det populäraste språket lämnar du standardinställningen **1**. Om du vill visa alla språk ange du värdet till **0**.|  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten innehåller länkar till följande rapport som innehåller ytterligare information om det valda objektet.  

|Rapportnamn|Information|  
|-----------------|-------------|  
|**Information om energiinställningar**|Klicka på antalet datorer i kolumnen **Datorer** om du vill visa en lista med alla datorer som använder energiinställningarna på den raden.<br /><br /> Mer information finns i [Power Settings Details Report](#BKMK_Settings_Details) i det här ämnet.|  

###  <a name="power-settings-details-report"></a><a name="BKMK_Settings_Details"></a> Power Settings Details report  
 Rapporten **Information om energiinställningar** visar ytterligare information om datorer som valts i rapporten **Energisparinställningar** . Den här rapporten anropas av rapporten **Energiinställningar** och är inte avsedd att köras direkt av platsadministratören.  

#### <a name="required-report-parameters"></a>Obligatoriska rapportparametrar  
 Följande parametrar måste anges för att du ska kunna köra den här rapporten.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**Samling**|Välj den samling i listrutan som du vill använda för rapporten.|  
|**GUID för energiinställning**|Välj det GUID för energiinställningar i listrutan som du vill köra rapporten för. En lista över alla energi inställningar och deras användning finns i de [tillgängliga inställningarna för energispar](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) funktioner i avsnittet [skapa och tillämpa energi scheman](../../../../core/clients/manage/power/create-and-apply-power-plans.md).|  
|**Power Mode**|Välj den typ av energisparinställningar i listrutan som du vill visa i rapportresultatet. Välj **Ansluten** om du vill visa energiinställningarna som konfigurerats för när datorn är ansluten och **Vid batteridrift** om du vill visa energiinställningarna för när datorn körs med batteridrift.|  
|**Inställningsindex**|Välj värdet för den valda energiinställning som du vill köra rapporten för i listrutan. Om du till exempel vill visa alla datorer där inställningen **Stäng av hårddisken efter** har värdet **10** minuter väljer du **Stäng av hårddisken efter** för **Namn för energiinställning** och **10** för **Inställningsindex**.|  

#### <a name="hidden-report-parameters"></a>Dolda rapportparametrar  
 Om du vill kan du ange följande dolda parametrar som ändrar rapportens beteende.  

|Parameternamn|Beskrivning|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Ange på hur många språk du vill visa namnen på energiinställningarna som rapporteras av klientdatorerna. Om du bara vill visa det populäraste språket lämnar du standardinställningen **1**. Om du vill visa alla språk ange du värdet till **0**.|  

#### <a name="report-links"></a>Rapportlänkar  
 Den här rapporten innehåller länkar till följande rapport som innehåller ytterligare information om det valda objektet.  

|Rapportnamn|Information|  
|-----------------|-------------|  
|**Information om dator**|Klicka på ett datornamn om du vill visa energisparfunktioner, energiinställningar och energischeman för den valda datorn.<br /><br /> Mer information finns i [Computer Details Report](#BKMK_Computer_Details) i det här ämnet.|  
