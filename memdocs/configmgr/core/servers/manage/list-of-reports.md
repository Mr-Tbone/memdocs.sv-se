---
title: Lista över rapporter
titleSuffix: Configuration Manager
description: Granska en lista med rapporter som medföljer Configuration Manager. Rapporterna visas i olika kategorier.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b7332ed3-8003-454b-bb12-1fdf8721425c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49fe5b5b94b29d93d29108660e2b76db2f87ddf9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713767"
---
# <a name="list-of-reports-in-configuration-manager"></a>Lista över rapporter i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager tillhandahåller många inbyggda rapporter som täcker många av de rapporterings uppgifter som du kanske vill göra. Du kan också använda SQL-uttrycken i dessa rapporter som en hjälp för att skapa egna rapporter.   

Följande rapporter ingår i Configuration Manager. Rapporterna visas i olika kategorier.  



## <a name="administrative-security"></a>Administrativ säkerhet  

Följande sex rapporter visas under kategorin **administrativ säkerhet** .  

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Logg för administrationsaktivitet**|Visar en post med administrativa ändringar gjorda för administrativa användare, säkerhets roller, säkerhets omfattningar och samlingar.|  
|**Säkerhetstilldelningar för administrativa användare**|Visar administrativa användare, deras associerade säkerhetsroller och de säkerhetsomfattningar som är associerade till varje säkerhetsroll för varje användare.|  
|**Objekt skyddade i ett visst säkerhetsområde**|Visar objekt som en administratör har tilldelat till den angivna säkerhets omfattningen. Den här rapporten visar inte objekt som en administratör associerar med mer än en säkerhets omfattning.|  
|**Säkerhet för ett eller flera specifika Configuration Manager-objekt**|Visar skyddsbara objekt, de säkerhetsområden som är associerade med objekten och vilka administrativa användare som har behörighet för objekten.|  
|**Översikt över säkerhetsroller**|Visar säkerhets roller och de Configuration Managers administratörer som är associerade med varje roll.|  
|**Sammanfattning av säkerhetsområden**|Visar säkerhets omfattningar och de Configuration Manager administrativa användare och säkerhets grupper som är kopplade till varje definitions område.|  



## <a name="alerts"></a>Aviseringar  

Följande två rapporter visas under kategorin **aviseringar** .  

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Bedömning av aviseringarna**|Visar en sammanfattning av alla senarelagda aviseringar som genererades mellan angivna start- och slutdatum.|  
|**Aviseringar som har genererats oftast**|Visar en sammanfattning av de aviseringar som har genererats oftast från idag och bakåt till angivet datum och för angivet funktionsområde.|  



## <a name="asset-intelligence"></a>Tillgångsinformation  

Följande 67-rapporter visas under kategorin **tillgångsinformation** .  

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Maskinvara 01A – översikt över datorer i en specifik samling**|Visar en tillgångsinformationssammanfattning för datorer i en samling som du anger.|  
|**Maskinvara 03A – primära datoranvändare**|Visar användare och antalet datorer där de är den primära användaren.|  
|**Maskinvara 03B – datorer för en specifik primär konsolanvändare**|Visar alla datorer där en specifik användare är den primära konsolanvändaren.|  
|**Maskinvara 04A – datorer med flera användare (delad)**|Visar datorer som inte har någon primär användare eftersom ingen användare har en inloggad tid som är större än 66%.|  
|**Maskinvara 05A – konsolanvändare på en specifik dator**|Visar alla konsolanvändare på en specifik dator.|  
|**Maskinvara 06A – datorer som det inte gick att fastställa konsolanvändare för**|Hjälper administrativa användare att identifiera datorer där säkerhetsloggning behöver aktiveras.|  
|**Maskinvara 07A – USB-enheter per tillverkare**|Visar USB-enheter, grupperat efter tillverkare.|  
|**Maskinvara 07B – USB-enheter per tillverkare och beskrivning**|Visar USB-enheter, grupperat efter tillverkare och beskrivning.|  
|**Maskinvara 07C – datorer med en specifik USB-enhet**|Visar alla datorer med en angiven USB-enhet.|  
|**Maskinvara 07D – USB-enheter på en specifik dator**|Visar alla USB-enheter på en angiven dator.|  
|**Maskinvara 08A – maskinvara som inte är klar för programuppdatering**|Visar maskin vara som inte uppfyller minimi kraven för maskin vara.|  
|**Maskinvara 09A – sök efter datorer**|Visar en sammanfattning av datorer som matchar nyckelords filter. Dessa filter är dator namn, Configuration Manager plats, domän, främsta konsol användare, operativ system, tillverkare eller modell.|  
|**Maskinvara 10A – datorer i en angiven samling som har ändrats under ett angivet tidsintervall**|Visar en lista över datorer i en angiven samling där en maskinvaruklass har ändrats under en angiven tidsperiod.|  
|**Maskinvara 10B – ändringar på en angiven dator inom ett angivet tidsintervall**|Visar de klasser som har ändrats på en viss dator inom en angiven tidsperiod.|  
|**Licens 01A – Microsoft Volume License-huvudbok för Microsoft-licensrapporter**|Visar en förteckning över alla Microsoft-program som är tillgängliga från Microsofts volymlicensieringsprogram.|  
|**Licens 01B – Microsoft Volume License Ledger-objekt efter försäljningskanal**|Identifierar och visar försäljningskanal för inventerad Microsoft-volymlicensieringsprogramvara.|  
|**Licens 01C – datorer med ett specifikt Microsoft Volume License-huvudboksobjekt och en specifik försäljningskanal**|Identifierar och visar datorer som har ett angivet objekt från Microsoft Volume License-huvudboken.|  
|**Licens 01D – Microsoft Volume License-huvudboksprodukter på en specifik dator**|Identifierar och visar alla Microsoft Volume License-huvudboksobjekt på en angiven dator.|  
|**Licens 02A – antal licenser som snart upphör att gälla enligt tidsintervall**|Visar det antal licenser som snart upphör att gälla enligt ett angivet tidsintervall. De produkter som visas har licenser som hanteras av Software Licensing Service.|  
|**Licens 02B – datorer med licenser som snart upphör att gälla**|Visar de angivna datorerna med licenser som snart upphör att gälla.|  
|**Licensavtal 02C – licensinformation på en specifik dator**|Visar produkter på en angiven dator vars licenser hanteras av Software Licensing Service.|  
|**Licens 03A – antal licenser utifrån licensstatus**|Visar produkter, efter licensstatus, vars licenser hanteras av Software Licensing Service.|  
|**Licens 03B – datorer med en specifik licensstatus**|Visar produkter med en angiven licensstatus vars licenser hanteras av Software Licensing Service.|  
|**Licens 04A – antal produkter som hanteras med programvarulicensiering**|Visar det antal produkter vars licenser hanteras av Software Licensing Service.|  
|**Licens 04B – datorer med en specifik produkt som hanteras av Software Licensing Service**|Visar datorer, som hanteras av Software Licensing Service, som innehåller en angiven produkt.|  
|**Licens 05A – datorer med nyckelhanteringstjänst**|Visar datorer som fungerar som nyckelhanteringsservrar.|  
|**Licens 06A – antal processorer för produkter som licensieras per processor**|Visar det antal processorer på datorer som använder Microsoft-produkter med stöd för licensiering per processor.|  
|**Licens 06B – datorer med en specifik produkt som stöder licensiering per processor**|Visar en lista över datorer där en angiven Microsoft-produkt med stöd för licensiering per processor är installerad.|  
|**Licens 14 – rapport om Microsoft Volume Licensing-avstämning**|Visar avstämningen för program varu licenser som har köpts via Microsofts volym licens avtal och det faktiska antalet lager.|  
|**Licens 14B – lista med inventerade Microsoft-program som inte hittas i MVLS**|I den här rapporten visas Microsofts program varu titlar som inte finns i Microsofts volym licens avtal.|  
|**Licens 15A – generell licensavstämningsrapport**|Visar avstämningen för program varu licenser som har köpts och det faktiska antalet lager.|  
|**Licens 15B – generell licensavstämningsrapport efter dator**|Visar datorer som har installerat den licensierade produkten med en angiven version.|  
|**Programvara 01A – översikt över installerad programvara i en specifik samling**|Visar en sammanfattning av installerad programvara, ordnat efter antalet instanser som hittades i lagret.|  
|**Programvara 02A – produktfamiljer för en specifik samling**|Visar produktfamiljerna och mängden programvara i familjen för en angiven samling.|  
|**Programvara 02B – produktkategorier för en specifik produktfamilj**|Visar produktkategorierna i en angiven produktfamilj och mängden programvara i kategorin.|  
|**Programvara 02C – programvara i en specifik produktfamilj och kategori**|Visar alla program som finns i den angivna produktfamiljen och kategorin.|  
|**Programvara 02D – datorer med specifik programvara installerad**|Visar alla datorer med angiven programvara installerad.|  
|**Programvara 02E – programvara installerad på en specifik dator**|Visar all programvara som är installerad på en angiven dator.|  
|**Programvara 03A – okategoriserad programvara**|Visar den programvara som antingen är kategoriserad som okänd eller som inte har någon kategorisering.|  
|**Programvara 04A – programvara konfigurerad för automatisk körning på datorer**|Visar en lista med programvara som är konfigurerad för automatisk körning på datorer.|  
|**Programvara 04B – datorer med specifik programvara konfigurerad för automatisk körning**|Visar alla datorer där specifik programvara är konfigurerad för automatisk körning.|  
|**Programvara 04C – programvara konfigurerad för automatisk körning på en specifik dator**|Visar installerad programvara som är konfigurerad för automatisk körning på en angiven dator.|  
|**Programvara 05A – webbläsartillägg**|Visar webb läsar tillägg som är installerade på datorer i en angiven samling.|  
|**Programvara 05B – datorer med ett specifikt webbläsartillägg**|Visar alla datorer med ett angivet webb läsar tillägg.|  
|**Programvara 05C – webbläsartillägg på en specifik dator**|Visar alla webb läsar tillägg på den angivna datorn.|  
|**Programvara 06A – sök efter installerad programvara**|Den här rapporten innehåller en sammanfattning av installerad program vara. Den söker efter följande kriterier: produkt namn, utgivare eller version.|  
|**Programvara 06B – programvara per produktnamn**|Visar en sammanfattning av installerad program vara baserat på ett angivet produkt namn.|  
|**Programvara 07A – nyligen använda körbara program enligt antal datorer**|Visar körbara program som användare nyligen har använt. Den innehåller också antalet datorer där användare använde programmet. Avläsning av programvara måste vara aktiverat för att den här platsen ska visa den här rapporten.|  
|**Programvara 07B – datorer där ett angivet körbart program har använts nyligen**|Visar de datorer där användare nyligen har använt ett angivet körbart program. Den här rapporten kräver att du aktiverar klient inställningen för program varu avläsning.|  
|**Programvara 07C – nyligen använda körbara program på en angiven dator**|Visar körbara filer som användare nyligen har använt på en angiven dator. Den här rapporten kräver att du aktiverar klient inställningen för program varu avläsning.|  
|**Programvara 08A – nyligen använda körbara program och antal användare**|Visar körbara program som användare nyligen har använt. Det innehåller också ett antal användare som senast har använt programmet. Den här rapporten kräver att du aktiverar klient inställningen för program varu avläsning.|  
|**Programvara 08B – användare som nyligen har använt ett angivet körbart program**|Visar de användare som senast har använt ett angivet körbart program. Den här rapporten kräver att du aktiverar klient inställningen för program varu avläsning.|  
|**Programvara 08C – nyligen använda körbara program för en angiven användare**|Visar körbara program som den angivna användaren nyligen använt. Den här rapporten kräver att du aktiverar klient inställningen för program varu avläsning.|  
|**Programvara 09A – programvara som används sällan**|Visar program varu titlar som användare inte har använt under en angiven tids period.|  
|**Programvara 09B – datorer med installerad programvara som används sällan**|Visar datorer med installerad program vara som användare inte har använt under en angiven tids period. Den angivna tidsperioden baseras på värdet som anges i rapporten ”Programvara 09A – programvara som används sällan”.|  
|**Programvara 10A – programtitlar med specifika egna etiketter**|Visar programtitlar baserat på matchning av alla angivna egna etikettvillkor. Upp till tre egna etiketter kan väljas för att begränsa en sökning efter programtitlar.|  
|**Programvara 10B – datorer med en specifik installerad programtitel med egna etiketter**|Visar alla datorer i den här samlingen med angivna programtitlar med egna etiketter installerade.|  
|**Programvara 11A – programtitlar med en specifik egen etikett**|Visar programtitlar baserat på matchning av minst ett angivet eget etikettvillkor.|  
|**Programvara 12A – programtitlar utan en egen etikett**|Visar alla program varu titlar som inte har en egen etikett definierad.|  
|**Programvara 14A – sökning efter program med aktiverade taggar för programvaruidentifiering**|Visar antalet installerade program med en aktiverad tagg för programvaruidentifiering.|  
|**Programvara 14B – datorer med specifika program med aktiverade taggar för programvaruidentifiering installerade**|Visar alla datorer som har programvara installerad med en angiven aktiverad tagg för programvaruidentifiering.|  
|**Programvara 14C – program med aktiverade taggar för programvaruidentifiering som är installerade på en viss dator**|Visar all installerad programvara med en angiven aktiverad tagg för programvaruidentifiering på en angiven dator.|  
|**Livs cykel 01A – datorer med en speciell program varu produkt**|Visa en lista med datorer där en angiven produkt har identifierats.|
|**Livs cykel 02A – lista över datorer med utgångna produkter i organisationen**|Visa datorer som har förfallit produkter på dem. Du kan filtrera den här rapporten efter produkt namn.|
|**Livs cykel 03A – lista över utgångna produkter som finns i organisationen**|Visa information om produkter i din miljö som har utgångna livs cykel datum.|
|**Livs cykel 04A – översikt över generell produkt livs cykel**|Visa en lista med livscykler för produkter. Filtrera listan efter produkt namn och dagar som ska upphöra att gälla.|
|**Livs cykel 05A – instrument panel för produkt livs cykel**|Från och med version 1810 innehåller den här rapporten liknande information som instrument panelen i konsolen.|



## <a name="client-push"></a>Klient-push  

Följande fyra rapporter visas under kategorin klient- **push** .  

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Information om statusen för klient-push-installationen**|Visar information om processen för klient-push-installation för alla platser.|  
|**Information om statusen för klient-push-installationen för en viss plats**|Visar information om processen för klient-push-installation för en angiven plats.|  
|**Översikt över statusen för klient-push-installationen**|Visar en sammanfattning av status för klient-push-installation för alla platser.|  
|**Översikt över statusen för klient-push-installationen för en viss plats**|Visar en sammanfattning av status för klient-push-installation för en angiven plats.|  



## <a name="client-status"></a>Klientstatus  

Följande sju rapporter visas under kategorin **klient status** .  

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Information om reparationer av klienter**|Visar information om klientreparationsåtgärder för en samling som du anger.|  
|**Sammanfattning av reparationer av klient**|Visar en sammanfattning av klientreparationsåtgärder för en angiven samling.|  
|**Klientens statushistorik**|Visar en historisk bild av övergripande klientstatus på platsen.|  
|**Sammanfattning av klientens status**|Visar resultat av klientkontroll för aktiva klienter i en viss samling.|  
|**Tid för klienter att begära en princip**|Visar procent andelen klienter som begärde principen minst en gång under de senaste 30 dagarna. Varje dag motsvarar en procent andel av totalt antal klienter som begärde principen sedan den första dagen i cykeln.|  
|**Klienter som inte godkändes i klientkontrollen**|Visar information om klienter där klientkontrollen misslyckades för en angiven samling.|  
|**Information om inaktiva klienter**|Visar en detaljerad lista med inaktiva klienter för en viss samling.|  



## <a name="company-resource-access"></a>Åtkomst till företagsresurser  

Följande tre rapporter visas under kategorin **företags resurs åtkomst** . 

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Historik för certifikat som utfärdats**|Visar historiken för certifikat som utfärdats av certifikat registrerings platsen till användare och enheter för det angivna datum intervallet.|  
|**Visar en lista över tillgångar efter status för certifikatutfärdande**|Visar de enheter eller användare med en angiven certifikatutfärdandestatus efter utvärdering av en angiven certifikatprofil.|  
|**Lista över tillgångar med certifikat som snart slutar att gälla**|Visar de enheter eller användare med certifikat som upphör att gälla på eller före det angivna datumet.|  



## <a name="compliance-and-settings-management"></a>Hantering av efterlevnad och inställningar  

Följande 22 rapporter visas under kategorin för **hantering av efterlevnad och inställningar** . 

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Kompatibilitetshistorik för en konfigurationsbaslinje**|Visar historiken för ändringar av kompatibilitet för en konfigurationsbaslinje för det angivna datumintervallet.|  
|**Kompatibilitetshistorik för ett konfigurationsobjekt**|Visar historik för ändringar av kompatibilitet för ett konfigurationsobjekt för det angivna datumintervallet.|  
|**Information om kompatibla regler för konfigurationsobjekt i en konfigurationsbaslinje för en tillgång**|Visar information om regler som har utvärderats som kompatibla för ett angivet konfigurations objekt för en angiven enhet eller användare.|  
|**Detaljerad information om regler i konflikt för konfigurationsobjekt i en konfigurationsbaslinje för en tillgång**|Visar information om regler i ett distribuerat konfigurations objekt som står i konflikt med andra regler. Ta med de andra reglerna i samma eller ett annat distribuerat konfigurations objekt.|  
|**Detaljerad information om fel för konfigurationsobjekt i en konfigurationsbaslinje för en tillgång**|Visar information om fel som har genererats av ett angivet konfigurationsobjekt för en angiven enhet eller användare.|  
|**Detaljerad information om icke-kompatibla regler för konfigurationsobjekt i en konfigurationsbaslinje för en tillgång**|Visar information om regler som har utvärderats som icke-kompatibla för ett angivet konfigurationsobjekt för en angiven enhet eller användare.|  
|**Detaljerad information om reparerade regler för konfigurationsobjekt i en konfigurationsbaslinje för en tillgång**|Visar information om regler som har åtgärdats av ett angivet konfigurationsobjekt för en angiven enhet eller användare.|  
|**Listar tillgångar efter kompatibilitetstillstånd för en konfigurationsbaslinje**|Visar de enheter eller användare som har ett angivet kompatibilitetstillstånd efter utvärdering av en angiven konfigurationsbaslinje.|  
|**Lista med tillgångar utifrån kompatibilitetstillstånd för ett konfigurationsobjekt i en konfigurationsbaslinje**|Visar de enheter eller användare som har ett angivet kompatibilitetstillstånd efter utvärdering av ett angivet konfigurationsobjekt.|  
|**Lista över icke-kompatibla appar och enheter för en viss användare**|Visar information om användare och enheter som har installerade appar som inte är kompatibla med en princip du har angett.|  
|**Lista med regler i konflikt med en angiven regel för en tillgång**|Visar en lista över regler som står i konflikt med en angiven regel för ett distribuerat konfigurations objekt.|  
|**Lista med okända tillgångar för en konfigurationsbaslinje**|Visar en lista över enheter eller användare som ännu inte har rapporterat några kompatibilitetsinformation för en angiven konfigurations bas linje.|  
|**Lista med okända tillgångar för ett konfigurationsobjekt**|Visar en lista över enheter eller användare som ännu inte har rapporterat några efterlevnadsprinciper för ett angivet konfigurations objekt.|  
|**Översikt över regler och fel för konfigurationsobjekt i en konfigurationsobjektbaslinje för en tillgång**|Visar en sammanfattning av reglerna för kompatibilitetstillstånd och eventuella inställnings fel för ett angivet konfigurations objekt. Konfigurationsobjektet måste distribueras till en enhet eller användare.|  
|**Översikt över kompatibilitet för konfigurationsbaslinje**|Visar en sammanfattning av övergripande kompatibilitet för distribuerade konfigurationsbaslinjer i hierarkin.|  
|**Översikt över kompatibilitet per konfigurationsobjekt för en konfigurationsbaslinje**|Visar en sammanfattning av kompatibilitet för konfigurationsobjekt i en angiven konfigurationsbaslinje.|  
|**Översikt över hur konfigurationsprinciperna följs**|Visar en sammanfattning av kompatibilitet för konfigurationsprinciper.|  
|**Översikt över kompatibilitet för en konfigurationsbaslinje för en samling**|Visar en översikt över övergripande kompatibilitet för en angiven konfigurations bas linje. Konfigurationsobjektet måste distribueras till den angivna samlingen.|  
|**Sammanfattning av användare som har icke-kompatibla appar**|Visar information om användare som har installerat appar som inte är kompatibla med en princip du har angett.|  
|**Godkännande av villkor**|Visar villkorsobjekt och vilken version varje användare har godkänt.|  



## <a name="data-warehouse"></a>Informationslager  

Följande sju rapporter visas under kategorin **data lager** . 

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Programdistribution**|Historisk: Visa information om program distribution för ett särskilt program och en specifik dator.|
|**Endpoint Protection-och program varu Uppdateringsefterlevnad**|Historisk: Visa datorer som saknar program uppdateringar.|
|**Allmän maskin varu inventering**|Historisk: Visa all maskin varu inventering för en angiven dator.|
|**Allmän program varu inventering**|Historisk: Visa all program varu inventering för en angiven dator.|
|**Översikt över infrastruktur hälsa**|Historisk: visar en översikt över hälso tillståndet för din Configuration Manager-infrastruktur.|
|**Lista över identifierad skadlig kod**|Historisk: Visa skadlig kod som har identifierats i organisationen.|
|**Sammanfattning av program varu distribution**|Historisk: en sammanfattning av program varu distributionen för en speciell annons och dator.|


## <a name="device-management"></a>Enhetshantering  

Följande 37-rapporter visas under kategorin **enhets hantering** . 

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla företagsägda mobila enheter**|Visar alla företagsägda mobila enheter.|
|**Alla klienter för mobila enheter**|Visar information om alla klienter för mobila enheter. Enheter som hanteras av Exchange Server-anslutningen ingår inte.|  
|**Certifikat problem på mobila enheter som hanteras av Configuration Manager-klienten för Windows CE och som inte är felfria**|Visar detaljerad information om certifikat problem på mobila enheter som hanteras av Configuration Manager-klienten för Windows CE.|  
|**Klient distributions problem för mobila enheter som hanteras av Configuration Manager-klienten för Windows CE**|Visar detaljerad information om distributions problem för mobila enheter som hanteras av Configuration Manager-klienten för Windows CE.|  
|**Information om klient distributions status för mobila enheter som hanteras av Configuration Manager-klienten för Windows CE**|Visar information om statusen för mobila enheter som hanteras av Configuration Manager-klienten för Windows CE.|  
|**Slutförd distribution för mobila enheter som administreras av Configuration Manager-klienten för Windows CE**|Visar detaljerad information om lyckade distributioner för mobila enheter som hanteras av Configuration Manager-klienten för Windows CE.|  
|**Kommunikationsproblem på mobila enheter som administreras av Configuration Manager-klienten för Windows CE och inte är felfria**|Den här rapporten innehåller detaljerad information om kommunikations problem på mobila enheter som administreras av Configuration Manager-klienten för Windows CE.|  
|**Kompatibilitetsstatus för standard princip för ActiveSync-postlåda för mobila enheter som hanteras av Exchange Server-anslutningen**|Visar en sammanfattning av kompatibilitetsstatus med standard principen för Exchange ActiveSync-postlådan för de mobila enheter som hanteras av Exchange Server-anslutningen.|  
|**Antal mobila enheter utifrån visningskonfigurationer**|Den här rapporten visar antalet mobila enheter efter visningsinställningar.|  
|**Antal mobila enheter per operativsystem**|Visar antalet mobila enheter efter operativsystem.|  
|**Antal mobila enheter utifrån programminne**|Visar antalet mobila enheter efter programminne.|  
|**Antal mobila enheter efter lagringsminneskonfigurationer**|Antal mobila enheter efter lagringsminneskonfigurationer|  
|**Hälsoinformation för mobila enheter som administreras av Configuration Manager-klienten för Windows CE**|Visar detaljerad hälso information för mobila enheter som hanteras av Configuration Manager-klienten för Windows CE.|  
|**Hälsoöversikt för mobila enheter som administreras av Configuration Manager-klienten för Windows CE**|Visar hälso översikts information för mobila enheter som hanteras av Configuration Manager-klienten för Windows CE.|  
|**Inaktiva mobila enheter som hanteras av Exchange Server-anslutningsappen**|Visar de mobila enheter som hanteras av Exchange Server-anslutningen som inte är ansluten till en Exchange-Server under ett angivet antal dagar.|  
|**Lista över enheter efter tillstånd för hälsoattestering**|Visar en lista över enheter med attribut som rapporter ATS av tjänsten hälsoattestering|
|**Lista över registrerade enheter per användare i Microsoft Intune**|Visar alla enheter som en användare har registrerat med Microsoft Intune.|  
|**Lista över enheter i en viss enhets kategori**|Visar information för alla enheter inom en viss enhets kategori.|
|**Lokala klientproblem på mobila enheter som administreras av Configuration Manager-klienten för Windows CE och inte är felfria**|Den här rapporten innehåller detaljerad information om lokala klient problem på mobila enheter som administreras av Configuration Manager-klienten för Windows CE.|  
|**Information om klient för mobil enhet**|Visar information om de mobila enheter som har Configuration Manager-klienten installerad. Du kan använda den här rapporten för att verifiera vilka mobila enheter som kan kommunicera med en hanteringsplats.|  
|**Information om kompatibilitet för mobila enheter för Exchange Server-anslutare**|Visar kompatibilitetsinformation om mobil enhet för en Exchange ActiveSync-standardbrevlådeprincip som konfigureras med Exchange Server-anslutningen.|  
|**Mobila enheter efter operativsystem**|Visar de mobila enheterna efter operativsystem.|  
|**Mobila enheter som är jailbrokade eller rotade**|Visar de mobila enheter som är jailbrokade eller rotade enheter.|  
|**Mobila enheter som inte hanteras eftersom platstilldelning misslyckades efter registreringen**|Visar de mobila enheter som har slutfört registreringen med Configuration Manager, har ett certifikat, men det gick inte att slutföra platstilldelning.|  
|**Mobila enheter med en viss mängd ledigt programminne**|Visar alla mobila enheter med en angiven mängd ledigt programminne.|  
|**Mobila enheter med en angiven mängd ledigt borttagbart lagringsminne**|Visar alla mobila enheter med en angiven mängd ledigt borttagbart minne.|  
|**Mobila enheter med certifikatförnyelseproblem**|Visar de registrerade mobila enheter som kunde inte förnya sina certifikat. Om du inte förnyar certifikatet innan giltighets perioden upphör att gälla, blir de mobila enheterna ohanterade.|  
|**Mobila enheter med endast lite ledigt programminne (mindre ledigt utrymme än angivet värde i KB)**|Visar de mobila enheter där programminnet har mindre utrymme än en angiven storlek i KB.|  
|**Mobila enheter med endast lite ledigt utrymme i borttagbart lagringsminne (mindre ledigt utrymme än angivet värde i KB)**|Visar de mobila enheter där det borttagbara lagringsminnet har mindre utrymme än en angiven storlek i KB.|  
|**Antal registrerade enheter per användare i Microsoft Intune**|Visar de användare som är aktiverade för Microsoft Intune prenumerationen. Det visar även det totala antalet enheter som har registrerats för varje användare.|  
|**Väntar på att ta ur bruk och rensa begäran om mobila enheter**|Visar de rensningsbegäranden som väntar för mobila enheter.|  
|**Nyligen registrerade och platstilldelade mobila enheter**|Visar mobila enheter som nyligen har registrerats med Configuration Manager och som har tilldelats till en plats.|  
|**Mobila enheter som nyligen har rensats**|Visar en lista med mobila enheter som nyligen har rensas.|  
|**Inställningsöversikt för mobilenheter som hanteras av Exchange Server-anslutningsappen**|Visar antalet mobila enheter som använder inställningarna för varje standard princip för Exchange ActiveSync-postlådan som hanteras av Exchange Server-anslutningen.|  
|**Status för Windows RT-nycklar för separat inläsning**|Visar detaljerad statusinformation för en specifik Windows RT-nyckel för separat inläsning.|  
|**Sammanfattning av Windows RT-nycklar för separat inläsning**|Visar status för Windows RT-nycklar för separat inläsning.|  



## <a name="driver-management"></a>Driv rutins hantering  

Följande 13 rapporter visas under kategorin **driv rutins hantering** . 

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla drivrutiner**|Visar en lista över alla drivrutiner.|  
|**Alla drivrutiner för en viss plattform**|Visar alla drivrutiner för en angiven plattform.|  
|**Alla drivrutiner i en viss startavbildning**|Visar alla drivrutiner i en angiven startavbildning.|  
|**Alla drivrutiner i en viss kategori**|Visar alla drivrutiner i en angiven kategori.|  
|**Alla drivrutiner i ett visst paket**|Visar alla drivrutiner i ett angivet paket.|  
|**Kategorier för en specifik drivrutin**|Visar kategorier för en angiven drivrutin.|  
|**Datorer där installation av drivrutiner misslyckades för en specifik samling**|Visar datorer där installation av drivrutiner misslyckades för en angiven samling.|  
|**Matchningsrapport för drivrutinskatalog för en specifik samling**|Visar en matchningsrapport för drivrutinskatalog för en angiven samling.|  
|**Matchningsrapport för drivrutinskatalog för en specifik dator**|Visar en matchningsrapport för drivrutinskatalog för en angiven dator.|  
|**Matchningsrapport för drivrutinskatalog för en specifik enhet på en specifik dator**|Visar en matchningsrapport för drivrutinskatalog för en specifik enhet på en angiven dator.|  
|**Matchningsrapport för drivrutinskatalog för datorer i en specifik samling med en specifik enhet**|Visar en matchningsrapport för drivrutinskatalog för datorer i en angiven samling med en angiven enhet.|  
|**Drivrutiner som inte gick att installera på en specifik dator**|Visar drivrutiner som inte gick att installera på en angiven dator.|  
|**Plattformar som stöds för en specifik drivrutin**|Visar plattformar som stöds för en angiven drivrutin.|  



## <a name="endpoint-protection"></a>Slutpunktsskydd  

Följande sex rapporter visas under kategorin **Endpoint Protection** . 

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Rapport – aktivitet för program mot skadlig kod**|Visar en översikt över aktivitet för program mot skadlig kod.|  
|**Allmän status och historik för program mot skadlig kod**|Visar allmän status och historik för program mot skadlig kod.|  
|**Information om program med skadlig kod på datorn**|Visar information om en angiven dator och listan över skadlig kod som har hittats på den.|  
|**Infekterade datorer**|Visar en lista över datorer där ett angivet hot har hittats.|  
|**Användare med flest hot**|Visar en lista med användarna som har flest upptäckta hot.|  
|**Hotlista för användare**|Visar listan över hot som har hittats för ett angivet användarkonto.|  



## <a name="hardware---cd-rom"></a>Maskin vara-CD-ROM  

Följande fyra rapporter visas under kategorin **maskin vara-CD-ROM** . 

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**CD-ROM-information för en specifik dator**|Visar information om CD-ROM-enheter på en angiven dator.|  
|**Datorer för en specifik CD-ROM-tillverkare**|Visar en lista över datorer med en CD-ROM-enhet som tillverkats av en tillverkare som du anger.|  
|**Räkna CD-ROM-enheter per tillverkare**|Visar antalet CD-ROM-enheter som har inventerats per tillverkare.|  
|**Historik-CD-ROM-historik för en speciell dator**|Visar inventeringshistoriken för CD-ROM-enheter på en angiven dator.|  



## <a name="hardware---disk"></a>Maskin vara-disk  

Följande åtta rapporter visas under kategorin **maskin varu disk** . 

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Datorer med en specifik hårddiskstorlek**|Visar en lista över datorer som har hårddiskar med en angiven storlek.|  
|**Datorer med ont om ledigt diskutrymme (mindre än det angivna %-värdet är ledigt)**|Visar en lista över datorer i en angiven samling med ett ledigt diskutrymme som är mindre än det angivna värdet.|  
|**Datorer med ont om ledigt diskutrymme (mindre ledigt utrymme än det angivna MB-värdet)**|Visar en lista över datorer och diskar där det är ont om utrymme. Mängden ledigt utrymme som gäller för kontrollen anges i MB.|  
|**Räkna fysiska diskkonfigurationer**|Visar antalet hårddiskar som har inventerats efter diskkapacitet.|  
|**Disk information för en speciell dator – logiska diskar**|Visar sammanfattningsinformation om de logiska diskarna på en angiven dator.|  
|**Diskinformation för en specifik dator – partitioner**|Visar sammanfattningsinformation om diskpartitionerna på en angiven dator.|  
|**Diskinformation för en specifik dator – fysiska diskar**|Visar sammanfattningsinformation om de fysiska diskarna på en angiven dator.|  
|**Historik – historik för logiskt diskutrymme för en specifik dator**|Visar inventeringshistoriken för logiska diskenheter på en angiven dator.|  



## <a name="hardware---general"></a>Maskin vara-allmänt  

Följande fem rapporter visas under kategorin **maskin vara – allmänt** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Datorinformation för en specifik dator**|Visar sammanfattningsinformation för en angiven dator.|  
|**Datorer i en specifik arbetsgrupp eller domän**|Visar en lista över datorer i en angiven arbetsgrupp eller domän.|  
|**Inventeringklasser tilldelade en specifik samling**|Visar inventeringsklasser som har tilldelats en angiven samling.|  
|**Aktiverade inventeringklasser på en viss dator**|Visar de inventeringsklasser som har aktiverats på en angiven dator.|  
|**Enhets information för Windows autopilot**|Visar information om klient enheter som behövs för Windows autopilot-registrering.|



## <a name="hardware---memory"></a>Maskin vara-minne  

Följande fem rapporter visas under kategorin **maskin vara – minne** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Datorer där det fysiska minnet har ändrats**|Visar en lista över datorer där mängden RAM-minne har ändrats sedan den senaste inventeringscykeln.|  
|**Datorer med en viss mängd minne**|Visar en lista med datorer som har en angiven mängd RAM-minne (totalt fysiskt minne avrundat till närmaste MB).|  
|**Datorer med ont om minne (mindre än eller lika med angivet MB-värde)**|Visar en lista över datorer med ont om minne. Mängden minne som gäller för kontrollen anges i MB.|  
|**Räkna minneskonfigurationer**|Visar antalet inventerade datorer efter mängden RAM-minne.|  
|**Minnesinformation för en specifik dator**|Visar sammanfattningsinformation om minnet på en angiven dator.|  



## <a name="hardware---modem"></a>Maskin vara-modem  

Följande tre rapporter visas under kategorin **maskin vara – modem** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Datorer med specifik modemtillverkare**|Visar en lista över datorer med modem som har tillverkats av en angiven tillverkare.|  
|**Räkna modem per tillverkare**|Visar antalet inventerade modem för varje modemtillverkare.|  
|**Modeminformation för en specifik dator**|Visar sammanfattningsinformation om modemet på en angiven dator.|  



## <a name="hardware---network-adapter"></a>Maskin vara-nätverkskort  

Följande tre rapporter visas under kategorin **maskin vara –** nätverkskort.

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Datorer med ett specifikt nätverkskort**|Visar en lista över datorer som har ett angivet nätverkskort.|  
|**Räkna nätverkskort per typ**|Visar antalet inventerade nätverkskort för varje typ.|  
|**Nätverkskortinformation för en specifik dator**|Visar information om de nätverkskort som är installerade på en angiven dator.|  



## <a name="hardware---processor"></a>Maskin vara-processor  

Följande fem rapporter visas under kategorin **maskin varu processor** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Datorer för en specifik processorhastighet**|Visar en lista över datorer som har processorer med en angiven hastighet.|  
|**Datorer med snabba processorer (klockfrekvens lika med eller högre än angivet värde)**|Visar en lista över datorer som har processorer med en hastighet som är högre än den angivna hastigheten.|  
|**Datorer med långsamma processorer (klockfrekvens lika med eller lägre än angivet värde)**|Visar en lista över datorer som har processorer med en hastighet som är lägre än den angivna hastigheten.|  
|**Räkna processorhastigheter**|Visar antalet inventerade datorer efter processorhastighet.|  
|**Processorinformation för en specifik dator**|Visar information om de processorer som är installerade på en angiven dator.|  



## <a name="hardware---scsi"></a>Maskin vara-SCSI  

Följande fem rapporter visas under kategorin **maskin vara – SCSI** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Datorer med en specifik SCSI-korttyp**|Visar en lista över datorer som har ett angivet SCSI-kort installerat.|  
|**Räkna SCSI-korttyper**|Visar antalet inventerade SCSI-kort efter korttyp.|  
|**SCSI-kortinformation för en specifik dator**|Visar information om de SCSI-kort som är installerade på en angiven dator.|  



## <a name="hardware---security"></a>Maskin vara-säkerhet

Följande rapport visas under kategorin **maskin vara – säkerhet** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Information om tillstånd för inbyggd program vara på enheter**|Visar information om tillstånden för UEFI, SecureBoot och TPM. **Obs!** den här rapporten finns inte i version 1810.<!--SCCMDocs issue #1189-->|  



## <a name="hardware---sound-card"></a>Maskin vara-ljudkort  

Följande tre rapporter visas under kategorin **maskin vara – SCSI** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Datorer med ett specifikt ljudkort**|Visar en lista över datorer som har ett angivet ljudkort.|  
|**Räkna ljudkort**|Visar antalet inventerade datorer efter varje ljudkortstyp.|  
|**Ljudkortsinformation för en specifik dator**|Visar sammanfattningsinformation om ljudkorten på en angiven dator.|  



## <a name="hardware---video-card"></a>Maskin vara-grafik kort  

Följande tre rapporter visas under kategorin **maskin vara – video kort** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Datorer med ett specifikt grafikkort**|Visar en lista över datorer som har ett angivet grafikkort.|  
|**Räkna grafikkort enligt typ**|Visar en lista över alla grafik kort som är installerade på datorerna. Det visar även numret för varje typ av grafik kort.|  
|**Grafikkortsinformation för en specifik dator**|Visar information om de grafikkort som är installerade på en angiven dator.|  



## <a name="migration"></a>Migrering  

Följande fem rapporter visas under kategorin **migrering** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Klienter i exkluderingslista**|Visar klienter som undantas från migrering.|  
|**Beroende av en Configuration Manager-samling**|Visar de objekt som är beroende av en samling för källhierarkin.|  
|**Egenskaper för migreringsjobb**|Rapporten visar innehållet i det angivna migreringsjobbet.|  
|**Migreringsjobb**|Denna rapport visar listan med migreringsjobb.|  
|**Objekt som inte gick att migrera**|Visar en lista med objekt som inte gick att migrera under det senaste försöket.|  



## <a name="network"></a>Nätverk  

Följande sex rapporter visas under kategorin **nätverk** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Räkna IP-adresser per undernät**|Visar antalet IP-adresser som har inventerats för varje IP-undernät.|  
|**IP-alla undernät per nätmask**|Visar en lista över IP-undernät och nätmasker.|  
|**IP-datorer i ett särskilt undernät**|Visar en lista över datorer och IP-information för ett angivet IP-undernät.|  
|**IP-information för en speciell dator**|Visar sammanfattningsinformation om IP på en angiven dator.|  
|**IP-information för en speciell IP-adress**|Visar sammanfattningsinformation om en angiven IP-adress.|  
|**MAC-datorer för en angiven MAC-adress**|Visar datornamn och IP-adress för datorer som har den angivna MAC-adressen.|  



## <a name="operating-system"></a>Operativsystem  

Följande 10 rapporter visas under kategorin **operativ system** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Versionshistorik för datorns operativsystem**|Visar inventeringshistoriken för operativsystemet på en angiven dator.|  
|**Datorer med ett specifikt operativsystem**|Visar datorer med ett angivet operativsystem.|  
|**Datorer med ett specifikt operativsystem och Service Pack**|Visar datorer med ett specifikt operativsystem och Service Pack.|  
|**Räkna operativsystemsversioner**|Visar antalet inventerade datorer efter operativsystem.|  
|**Räkna operativsystem och Service Pack**|Visar antalet inventerade datorer efter kombinationer av operativsystem och Service Pack.|  
|**Tjänster – datorer där en specifik tjänst körs**|Visar en lista över datorer som kör en specifik tjänst.|  
|**Tjänster – datorer där RAS (fjärråtkomstserver) körs**|Visar en lista med datorer där RAS (fjärråtkomstserver) körs.|  
|**Tjänster – tjänstinformation för en specifik dator**|Visar sammanfattningsinformation om tjänsterna på en angiven dator.|  
|**Service information för Windows 10 för en speciell samling**|Visar allmän information om Windows 10-underhåll för en speciell samling.|
|**Windows Server-datorer**|Visar en lista över datorer som kör Windows Server-operativsystemen.|  


## <a name="power-management"></a>Energisparfunktioner  

Följande 18 rapporter visas under kategorin **energispar funktioner** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Energispar funktioner-dator aktivitet**|Visar ett diagram över skärm-, dator-och användar aktivitet för en angiven samling under en angiven tids period.|  
|**Energispar funktioner-dator aktivitet efter dator**|Visar ett diagram över skärm-, dator-och användar aktivitet för en angiven dator på ett angivet datum.|  
|**Energispar funktioner-information om dator aktivitet**|Visar en lista med vilo- och väckningsfunktioner för datorer i den angivna samlingen för angivet datum och tid.|  
|**Energispar funktioner-dator information**|Visar detaljerad information om energispar funktioner, energi inställningar och energi scheman som tillämpas på en angiven dator.|  
|**Energispar funktioner-datorn rapporterar inte information**|Visar en lista över datorer som inte rapporterar någon energiaktivitet för angivet datum och tid.|  
|**Energispar funktioner-undantagna datorer**|Visar en lista över datorer som undantas från energischemat.|  
|**Energispar funktioner-datorer med flera energi scheman**|Visar en lista över datorer som har flera motstridiga energiinställningar.|  
|**Energispar funktioner-energi förbrukning**|Visar den totala månatliga energiförbrukningen (i kWh) för en angiven samling under en angiven tidsperiod.|  
|**Energispar funktioner-energi förbrukning per dag**|Visar den totala energiförbrukningen (i kWh) för en angiven samling under de senaste 31 dagarna.|  
|**Energispar funktioner-energi kostnad**|Visar den totala månatliga energiförbrukningskostnaden för en angiven samling under en angiven tidsperiod.|  
|**Energispar funktioner – energi kostnad per dag**|Visar den totala energiförbrukningskostnaden för en angiven samling under de senaste 31 dagarna.|  
|**Energispar funktioner-miljö påverkan**|Visar ett diagram över koldioxidutsläpp (CO2) som har genererats av en angiven samling under en angiven tidsperiod.|  
|**Energispar funktioner-miljö påverkan per dag**|Visar ett diagram över CO2-utsläpp som har genererats av en angiven samling under de senaste 31 dagarna.|  
|**Energispar funktioner-sömnlöshet dator information**|Visar detaljerad information om datorer som inte försätts i vilo läge eller vilo läge inom en angiven tids period.|  
|**Energispar funktioner – sömnlöshet-rapport**|Visar en lista över vanliga orsaker som förhindrar att datorer försätts i ström spar läge eller vilo läge. Det visar också antalet datorer som påverkas av varje orsak under en angiven tids period.|  
|**Energispar funktioner-energi funktioner**|Visar energisparfunktioner för datorer i den angivna samlingen.|  
|**Energispar funktioner-energi inställningar**|Visar en sammansatt lista med energiinställningarna som används av datorer i en angiven samling.|  
|**Energispar funktioner-information om energi inställningar**|Används för att visa ytterligare information om datorer som har angetts i rapporten **energispar funktioner-energi inställningar** .|  



## <a name="replication-traffic"></a>Replikeringstrafik  

Följande 10 rapporter visas under kategorin **replikeringstrafik** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Trafik per länk för global datareplikering (linjediagram)**|Visar total trafik för global datareplikering på en angiven länk under ett angivet antal dagar.|  
|**Trafik per länk för global datareplikering (cirkeldiagram)**|Visar total trafik för global datareplikering på en angiven länk under ett angivet antal dagar.|  
|**Replikeringstrafik per länk i hierarkin**|Visar total replikeringstrafik för varje länk i hierarkin för ett angivet antal dagar.|  
|**Trafik för de tio främsta replikgrupperna per länk i hierarkin (cirkeldiagram)**|Visar replikeringstrafiken för de tio främsta replik grupperna i hela hierarkin som identifieras av länken.|  
|**Länkreplikeringstrafik**|Visar total replikeringstrafik för alla data för ett angivet antal dagar.|  
|**Trafik per länk för replikgruppen**|Visar nätverkstrafik för replikgruppen på en angiven databasreplikeringslänk för ett angivet antal dagar.|  
|**Trafik per länk för platsdatareplikering (linjediagram)**|Visar total trafik för platsdatareplikering på en angiven länk under ett angivet antal dagar.|  
|**Trafik per länk för platsdatareplikering (cirkeldiagram)**|Visar total trafik för platsdatareplikering på en angiven länk under ett angivet antal dagar.|  
|**Total replikeringstrafik i hierarkin (linjediagram)**|Visar hierarkins sammanställda globala och platsdatareplikering för varje riktning för varje länk under ett angivet antal dagar.|  
|**Total replikeringstrafik i hierarkin (cirkeldiagram)**|Visar hierarkins sammanställda globala och platsdatareplikering för varje riktning för varje länk under ett angivet antal dagar.|  



## <a name="site---client-information"></a>Plats-klient information  

Följande 19 rapporter visas under kategorin **plats-klient information** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Statusrapport om klienttilldelningar**|Visar detaljerad information om status för klienttilldelning.|  
|**Information om misslyckade klienttilldelningar**|Visar detaljerad information om misslyckade klienttilldelningar.|  
|**Statusinformation om klienttilldelningar**|Visar översiktsinformation om status för klienttilldelningar.|  
|**Information om lyckade klienttilldelningar**|Visar detaljerad information om tilldelade klienter.|  
|**Rapport om misslyckade klientdistributioner**|Visar detaljerad information för klienter som inte har distribuerats.|  
|**Statusinformation om klientdistributioner**|Visar sammanfattningsinformation om status för klientinstallationer.|  
|**Rapport om lyckade klientdistributioner**|Visar detaljerad information för klienter som har distribuerats.|  
|**Klienter som inte klarar HTTPS-kommunikation**|Visar detaljerad information om varje klient som kör verktyget HTTPS Communication readiness och rapporter som inte kan kommunicera via HTTPS.|  
|**Datorer tilldelade men inte installerade för en viss plats**|Visar en lista över datorer som har tilldelats en angiven plats, men som inte rapporterar till den platsen.|  
|**Datorer med en viss Configuration Manager-klientversion**|Visar en lista med datorer som kör en angiven version av Configuration Manager-klient program varan.|  
|**Antal klienter och protokoll som används för kommunikation**|Visar en sammanfattning av de kommunikationsmetoder som används av klienterna (HTTP eller HTTPS).|  
|**Antal klienter tilldelade och installerade för varje webbplats**|Visar antalet datorer som tilldelats och installeras för varje plats. Klienter med en nätverks plats som är kopplad till flera platser räknas endast som installerade om de rapporterar till den platsen.|  
|**Antal klienter som klarar HTTPS-kommunikation**|Visar detaljerad information om varje klient som kör verktyget HTTPS Communication readiness och rapporter som antingen kan vara kompatibla eller kan kommunicera via HTTPS.|  
|**Antal klienter per plats**|Visar antalet Configuration Manager-klienter som har installerats med Platskod.|  
|**Antal Configuration Manager-klienter enligt klientversion**|Visar antalet datorer som identifierats av Configuration Manager klient versionen.|  
|**Probleminformation rapporterad till återställningsstatusplatsen för en viss samling**|Visar detaljerad information om problem som har rapporter ATS av klienter i en angiven samling. Dessa klienter måste ha en tilldelad återställnings status plats.|  
|**Probleminformation rapporterad till återställningsstatusplatsen för en viss webbplats**|Visar detaljerad information om problem som har rapporter ATS av klienter på en angiven plats. Dessa klienter måste ha en tilldelad återställnings status plats.|  
|**Översikt över problem rapporterade till återställningsstatusplatsen**|Visar information om alla problem som har rapporter ATS av klienter. Dessa klienter måste ha en tilldelad återställnings status plats.|  
|**Översikt över problem rapporterade till återställningsstatusplatsen för en viss samling**|Visar sammanfattnings information om problem som har rapporter ATS av klienter i en angiven samling. Dessa klienter måste ha en tilldelad återställnings status plats.|  



## <a name="site---discovery-and-inventory-information"></a>Plats-identifierings-och inventerings information  

Följande 10 rapporter visas under kategorin **plats identifiering och inventerings information** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Klienter som inte har rapporterat nyligen (inom ett angivet antal dagar)**|Visar en lista över klienter som inte har rapporterat identifierings data, maskin varu inventering eller program varu inventering under ett angivet antal dagar.|  
|**Identifierade datorer för en specifik plats**|Visar en lista över alla datorer som den angivna platsen har identifierat. Det visar även datumet för den senaste identifieringen.|  
|**Nyligen identifierade datorer enligt identifieringsmetod**|Visar en lista med datorer där platsen identifierats inom det angivna antalet dagar. Den visar även de agenter som identifierade dem. Om flera agenter har identifierat en dator kan det visas mer än en gång i listan.|  
|**Datorer som inte nyligen har identifierats (sedan det angivna antalet dagar)**|Visar en lista med datorer där platsen inte nyligen har identifierats. Det visar också antalet dagar sedan platsen upptäckte att datorn har identifierat datorn.|  
|**Datorer som inte nyligen har inventerats (sedan det angivna antalet dagar)**|Visar en lista med datorer där platsen inte nyligen har inventerats. Den visar också senaste gånger som klienten inventerade datorn.|  
|**Datorer som kanske delar samma unika identifierare för Configuration Manager**|Visar en lista över datorer vars namn har ändrats. En namn ändring är ett möjligt symtom på att en dator delar en Configuration Manager unik identifierare med en annan dator.|  
|**Datorer med dubbla MAC-adresser**|Visar datorer som delar MAC-adress.|  
|**Räkna datorer i resursdomäner eller arbetsgrupper**|Visar antalet datorer i varje resursdomän eller arbetsgrupp.|  
|**Identifieringsinformation för en specifik dator**|Visar en lista över de agenter och platser som har identifierat en angiven dator.|  
|**Inventeringsdatum för en specifik dator**|Visar datum och tid då inventering senast kördes på en angiven dator.|  



## <a name="site---general"></a>Plats – allmänt  

Följande tre rapporter visas under kategorin **plats – allmänt** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Datorer på en viss plats**|Visar en lista över klientdatorer på en angiven plats.|  
|**Platsstatus för hierarkin**|Visar listan över platser i hierarkin med platsversion och information om platsstatus.|  
|**Status för Configuration Manager-uppdatering i hierarki**|Visar information om Configuration Manager plats uppdateringar för hierarkin.|  



## <a name="site---server-information"></a>Plats-Server information  

Följande en rapport visas under kategorin **plats-Server information** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Platssystemroller och platssystemservrar för en specifik plats**|Visar en lista över platssystemservrar och deras platssystemroller för en angiven plats.|  



## <a name="software---companies-and-products"></a>Program vara – företag och produkter  

Följande 15 rapporter visas under kategorin **program vara – företag och produkter** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla inventerade produkter för ett specifikt programvaruföretag**|Visar en lista över inventerade programvaruprodukter och versioner från ett angivet programvaruföretag.|  
|**Alla programvaruföretag**|Visar en lista över alla företag som tillverkar inventerad programvara.|  
|**Alla Windows-appar**|Visar en sammanfattning av installerade Windows-appar. Den söker efter följande kriterier: program namn, arkitektur eller utgivare.|  
|**Datorer med en specifik produkt**|Visar en lista med datorer där en angiven produkt har inventerats och versioner av produkten.|  
|**Datorer med specifik produkt och specifik produktversion**|Visar en lista över de datorer där en angiven version av en produkt har inventerats.|  
|**Datorer med specifik programvara registrerad i Lägg till/ta bort program**|Visar en sammanfattning av alla datorer där angiven programvara har registrerats i Lägg till/ta bort program eller Program och funktioner.|  
|**Räkna alla inventerade produkter och versioner**|Visar en lista över inventerade programvaruprodukter och versioner och antalet datorer som var och en är installerad på.|  
|**Räkna inventerade produkter och versioner för en specifik produkt**|Visar en lista över inventerade versioner av en angiven produkt och antalet datorer som var och en är installerad på.|  
|**Antal instanser av programvaror som är registrerade i Lägg till/ta bort program**|Visar en sammanfattning av alla instanser av programvara som har installerats och registrerats med Lägg till eller ta bort program eller Program och funktioner på datorer i den angivna samlingen.|  
|**Antal instanser av specifik programvara registrerad i Lägg till/ta bort program**|Visar antalet instanser för angivna programvarupaket som har installerats och registrerats i Lägg till eller ta bort program eller Program och funktioner.|  
|**Antal standard webbläsare**|Visar antalet klienter med en speciell webbläsare som Windows standard. <br>Använd följande referens för vanliga BrowserProgIDs:<br> -AppXq0fevzme2pys62n3e0fbqa7peapykr8v: Microsoft Edge<br> IE. HTTP: Microsoft Internet Explorer<br> -ChromeHTML: Google Chrome<br> -OperaStable: Opera program vara<br> -FirefoxURL-308046B0AF4A39CB: Mozilla Firefox<br> – Okänd: klientens OS stöder inte frågan, frågan har inte körts eller också har användaren inte loggat in|
|**Installationer av angivna Windows-appar**|Den här rapporten visar en lista över alla datorer med en angiven Windows-app.|  
|**Produkter på en specifik dator**|Visar en sammanfattning av inventerade programvaruprodukter och deras tillverkare på en angiven dator.|  
|**Programvara registrerad i Lägg till/ta bort program på en specifik dator**|Visar en sammanfattning av programvara som är installerad på en angiven dator som har registrerats i Lägg till/ta bort program eller Program och funktioner.|  
|**Windows-appar som har installerats för den angivna användaren**|Visar alla Windows-appar som har installerats för den angivna användaren|  



## <a name="software---files"></a>Programvara – filer  

Följande fem rapporter visas under kategorin **program vara – filer** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla inventerade filer för en specifik produkt**|Visar en sammanfattning av de inventerade filer som är kopplade till en angiven programvaruprodukt.|  
|**Alla inventerade filer på en specifik dator**|Visar en sammanfattning av alla filer som har inventerats på en angiven dator.|  
|**Jämför programvaruinventering för två datorer**|Visar skillnaderna mellan programvaruinventeringar som har rapporterats för två angivna datorer.|  
|**Datorer med en specifik fil**|Visar en lista över datorer som har samlat in programvaruinventering för ett angivet filnamn. Om en dator innehåller flera kopior av filen kan den visas mer än en gång i listan.|  
|**Antal datorer med ett specifikt filnamn**|Visar antalet datorer som har samlat in programvaruinventering för en angiven fil.|  



## <a name="software-distribution---application-monitoring"></a>Program varu distribution-program övervakning  

Följande 10 rapporter visas under kategorin **program distribution – program övervakning** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla programdistributioner (avancerat)**|Visar detaljerad sammanfattningsinformation för alla programdistributioner.|  
|**Alla programdistributioner (grundläggande)**|Visar sammanfattningsinformation för alla programdistributioner.|  
|**Programkompatibilitet**|Visar kompatibilitetsinformation för det angivna programmet i den angivna samlingen.|  
|**Programdistributioner per tillgång**|Visar program som har distribuerats till en angiven enhet eller användare.|  
|**Fel i programinfrastrukturen**|Visar fel i programinfrastrukturen. Felen omfattar interna infrastruktur problem eller fel som orsakas av ogiltiga krav regler.|  
|**Detaljerad status för programanvändning**|Visar användningsinformation för installerade program.|  
|**Statusöversikt för programanvändning**|Visar en användningssammanfattning för installerade program.|  
|**Aktivitetssekvensdistributioner som innehåller programmet**|Visar aktivitetssekvensdistributioner som installerar ett angivet program.|  


## <a name="software-distribution---collections"></a>Program distribution – samlingar  

Följande tre rapporter visas under kategorin **program distribution – samlingar** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla samlingar**|Visar alla samlingar i hierarkin.|  
|**Alla resurser i en specifik samling**|Visar alla resurser i en angiven samling.|  
|**Tillgängliga underhållsfönster för en angiven klient**|Visar alla underhållsfönster som kan användas på den angivna klienten.|  



## <a name="software-distribution---content"></a>Program varu distribution-innehåll  

Följande 16 rapporter visas under kategorin **program distribution – innehåll** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla aktiva innehållsdistributioner**|Visar alla distributionplatser där innehåll för närvarande installeras eller tas bort.|  
|**Allt innehåll**|Visar alla program och paket på en plats.|  
|**Allt innehåll på en specifik distributionsplats**|Visar allt innehåll som för närvarande är installerat på en angiven distributionsplats.|  
|**Alla distributionsplatser**|Visar information om distributionsplatserna för varje plats.|  
|**Alla statusmeddelanden för ett specifikt paket på en specifik distributionsplats**|Visar alla statusmeddelanden för ett angivet paket på en angiven distributionsplats.|  
|**Distributionsstatus för programinnehåll**|Visar information om distributionsstatus för programinnehåll.|  
|**Program riktade till en distributionsplatsgrupp**|Visar information om programinnehåll som har distribuerats till en angiven distributionsplatsgrupp.|  
|**Program som inte är synkroniserade i en angiven distributionsplatsgrupp**|Visar de program för vilka de associerade innehållsfilerna inte har uppdaterats med den senaste versionen på en angiven distributions plats grupp.|  
|**Distributionsplatsgrupp**|Visar information om en angiven distributionsplatsgrupp.|  
|**Sammanfattning av distributionsplatsanvändning**|Visar användningssammanfattning för varje distributionsplats.|  
|**Distributionsstatus för angivet paket**|Visar distributionsstatus för angivet paketinnehåll på varje distributionsplats.|  
|**Paket riktade till distributionsplatsgrupp**|Visar information om paket som är riktade till en angiven distributionsplatsgrupp.|  
|**Paket som inte är synkroniserade i en angiven distributionsplatsgrupp**|Visar paket med associerade innehållsfiler som inte har uppdaterats med den senaste versionen på en angiven distributions plats grupp.|  
|**Avvisning av käll innehåll i peer-cache**|Visar antalet avvisningar av peer-cache-källan per avgränsnings grupp.|
|**Avvisning av käll innehåll i peer-cache efter villkor**|Visar de peer-cache-källor som avvisade att betjäna innehåll baserat på ett villkor.|
|**Information om avvisning av käll innehåll i peer-cache**|Visar namnet på det innehåll som avvisats av en peer-källa.|



## <a name="software-distribution---package-and-program-deployment"></a>Program varu distribution – paket-och program distribution 

Följande fem rapporter visas under kategorin **program distribution – paket-och program distribution** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla distributioner för ett angivet paket och program**|Visar information om alla distributioner av ett angivet paket och program.|  
|**Alla paket- och programdistributioner**|Visar alla paket- och programdistributioner på den här platsen.|  
|**Alla paket- och programdistributioner till en angiven samling**|Visar alla paket- och programdistributioner till en angiven samling.|  
|**Alla paket- och programdistributioner till en angiven dator**|Visar alla paket- och programdistributioner som gäller för en angiven dator.|  
|**Alla paket- och programdistributioner till en angiven användare**|Visar alla paket- och programdistributioner till en angiven användare.|  



## <a name="software-distribution---package-and-program-deployment-status"></a>Program distribution-status för paket-och program distribution  

Följande fem rapporter visas under kategorin **program distribution – status för paket-och program distribution** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla systemresurspaket- och programdistributioner med status**|Visar alla paket- och programdistributioner för platsen med en sammanfattningsstatus för varje distribution.|  
|**Alla systemresurser för en angiven paket- och programdistribution i ett visst tillstånd**|Visar en lista med resurser som har ett angivet tillstånd för en angiven paket- och programdistribution.|  
|**Diagram-slut för ande status för paket-och program distribution per timme**|Visar procent andelen datorer som har installerat paketet. Listan organiseras för varje timme eftersom en administratör skapar paket-och program distributionen. Det kan användas för att spåra genomsnittlig tid för en paket- och programdistribution.|  
|**Status för paket- och programdistributionsstatus för en angiven klient och distribution**|Visar statusmeddelanden som har rapporterats för en angiven dator och paket- och programdistribution.|  
|**Status för en angiven paket- och programdistribution**|Visar statussammanfattning för en angiven paket- och programdistribution.|  



## <a name="software-metering"></a>Avläsning av programvara  

Följande 13 rapporter visas under kategorin avläsning av **program vara** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla programmätregler som används för webbplatsen**|Visar en lista över alla programmätregler på platsen.|  
|**Datorer där ett bevakat program är installerat men inte har körts sedan det angivna datumet**|Visar alla datorer med angivet bevakat program, men ingen användare har kört programmet sedan det angivna datumet.|  
|**Datorer där ett angivet bevakat program har körts**|Visar en lista över datorer som har kört program som överensstämmer med den angivna regeln för avläsning av programvara under den angivna månaden och året.|  
|**Samtidig användning för alla bevakade program**|Visar det högsta antalet användare som samtidigt körde varje bevakat program under angiven månad och år.|  
|**Trendanalys för samtidig användning av ett specifikt bevakat program**|Visar det högsta antalet användare som samtidigt körde varje det angivna bevakade programmet under varje månad det senaste året.|  
|**Installationsbas för alla bevakade programvaror**|Visar antalet datorer som har bevakade programvaror installerade enligt rapporter från programvaruinventering. Den här rapporten kräver att datorn samlar in program varu inventering.|  
|**Förlopp för sammanfattning av programavläsning**|Visar den tid då senaste sammanfattade avläsningsdata bearbetades på platsservern. Rapporter om avläsning av program vara visar bara mätnings data som bearbetats före dessa datum.|  
|**Översikt över daglig användning för ett specifikt bevakat program**|Visar det genomsnittliga antalet användningar för ett visst program under de senaste 90 dagarna, fördelat på timme och dag.|  
|**Total användning för alla program som bevakas**|Visar antalet användare som körde program under angiven månad och år och som matchar varje regel för avläsning av program vara. Dessa regler gäller lokalt installerad program vara eller med Terminal Services.|  
|**Total användning för alla program som bevakas på Windows Terminal-servrar**|Visar hur många användare som körde program som överensstämmer med varje regel för avläsning av programvara som använder Terminal Services under angiven månad och år.|  
|**Trendanalys för total användning för ett specifikt program som bevakas**|Visar antalet användare som körde program under varje månad under det senaste året, och som matchar den angivna regeln för avläsning av program vara. Dessa regler gäller lokalt installerad program vara eller med Terminal Services.|  
|**Trendanalys för total användning för ett angivet program som bevakas på Windows Terminal-servrar**|Visar antalet användare som körde program under varje månad under det senaste året, och som matchar den angivna regeln för avläsning av program vara. Dessa regler gäller för användning av Terminal Services.|  
|**Användare som har kört ett specifikt program som bevakas**|Visar en lista över användare som har kört program under den angivna månaden och det angivna året, och som matchar den angivna regeln för avläsning av program vara.|  



## <a name="software-updates---a-compliance"></a>Program uppdateringar-A kompatibilitet  

Följande åtta rapporter visas under kategorin **program uppdateringar – en kompatibilitet** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Kompatibilitet 1 – övergripande kompatibilitet**|Visar övergripande kompatibilitetsdata för en programuppdateringsgrupp.|  
|**Kompatibilitet 2 – specifik programuppdatering**|Visar kompatibilitetsdata för en angiven programuppdateringsgrupp.|  
|**Kompatibilitet 3 – uppdateringsgrupp (per uppdatering)**|Visar kompatibilitetsdata för programuppdateringar som har definierats i en programuppdateringsgrupp.|  
|**Kompatibilitet 4 – uppdateringar per leverantör månad och år**|Visar kompatibilitetsdata för programuppdateringar som har publicerats av en leverantör under en angiven månad och år.|  
|**Kompatibilitet 5 – specifik dator**|Den här rapporten returnerar kompatibilitetsdata för programuppdateringar för en viss dator. Om du vill begränsa mängden information som returneras kan du ange leverantör och klassificering av programuppdatering.|  
|**Kompatibilitet 6 – specifika programuppdateringstillstånd (sekundär)**|Visar antalet och procentandelen datorer i varje kompatibilitetstillstånd för den angivna programuppdateringen.|  
|**Kompatibilitet 7 – datorer i ett specifikt kompatibilitetstillstånd för en uppdateringsgrupp (sekundär)**|Visar alla datorer i en samling som har ett angivet övergripande kompatibilitetstillstånd mot en programuppdateringsgrupp.|  
|**Kompatibilitet 8 – datorer i ett specifikt kompatibilitetstillstånd för en uppdatering (sekundär)**|Visar alla datorer i en samling som har ett angivet kompatibilitetstillstånd för en programuppdatering.|  
|**Efterlevnad 9 – övergripande hälso tillstånd och efterlevnad**|Visar övergripande information om hälso tillstånd och efterlevnad för en program uppdaterings grupp. (från och med version 1806)| 


## <a name="software-updates---b-deployment-management"></a>Program uppdateringar-B distributions hantering  

Följande åtta rapporter visas under kategorin **program uppdateringar-B distributions hantering** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Hantering 1 – distributioner för en uppdateringsgrupp**|Visar alla distributioner som innehåller alla program uppdateringar som definierats i en angiven program uppdaterings grupp.|  
|**Hantering 2 – nödvändiga uppdateringar som inte har distribuerats**|Visar alla leverantörsspecifika program uppdateringar som klienter identifierar vid behov, men en administratör som inte har distribuerats till en angiven samling.|  
|**Hantering 3 – uppdateringar i en distribution**|Visar de programuppdateringar som ingår i en angiven distribution.|  
|**Hantering 4 – distributioner riktade till en samling**|Visar alla programuppdateringsdistributioner som är riktade till en angiven samling.|  
|**Hantering 5 – distributioner riktade till en dator**|Visar alla programuppdateringsdistributioner som distribueras till en angiven dator.|  
|**Hantering 6 – distributioner som innehåller en specifik uppdatering 	**|Visar alla distributioner som innehåller en angiven program uppdatering och den associerade mål samlingen för distributionen.|  
|**Hantering 7 – uppdatering i en distribution som saknar innehåll**|Visar program uppdateringar i en angiven distribution som inte har allt associerat innehåll. Det här läget förhindrar klienter från att installera uppdateringen, vilket förhindrar att distributionen når 100% efterlevnad.|  
|**Hantering 8 – datorer som saknar innehåll (sekundär)**|Visar alla datorer som kräver den angivna program uppdateringen, men det tillhör ande innehållet distribueras ännu inte till en distributions plats.|  



## <a name="software-updates---c-deployment-states"></a>Program uppdateringar-C distributions tillstånd  

Följande sex rapporter visas under kategorin **program uppdateringar-C distributions tillstånd** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Tillstånd 1 – tvångsåtgärdstillstånd för en distribution**|Visar tvångsåtgärdstillstånd för en angiven programuppdateringsdistribution, som normalt är den andra fasen i en distributionsutvärdering.|  
|**Tillstånd 2 – utvärderingstillstånd för en distribution**|Visar utvärderingstillstånd för en angiven programuppdateringsdistribution, som normalt är den första fasen i en distributionsutvärdering.|  
|**Tillstånd 3 – tillstånd för en distribution och en dator**|Visar tillstånd för alla programuppdateringar i den angivna distributionen för en angiven dator.|  
|**Tillstånd 4 – datorer ett specifikt tillstånd för en distribution (sekundär)**|Visar alla datorer i ett angivet tillstånd för en programuppdateringsdistribution.|  
|**Tillstånd 5 – tillstånd för en uppdatering i en distribution (sekundär)**|Visar en sammanfattning av tillstånd för en angiven programuppdatering som är mål för en angiven distribution.|  
|**Tillstånd 6 – datorer i ett specifikt tvångsåtgärdstillstånd för en uppdatering (sekundärt)**|Visar alla datorer i ett angivet tvångsåtgärdstillstånd för en angiven programuppdatering.|  



## <a name="software-updates---d-scan"></a>Program uppdateringar-D genomsökning  

Följande fyra rapporter visas under kategorin **program uppdateringar-D genomsökning** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Genomsökning 1 – senaste genomsökningstillstånden utifrån samling**|Ange en samling för att visa antalet datorer i varje genomsöknings tillstånd för kompatibilitet. Klienterna returnerar tillstånd under den senaste genomsökningen.|  
|**Genomsökning 2 – senaste genomsökningstillstånden per plats**|Ange en plats för att visa antalet datorer i varje genomsöknings tillstånd för kompatibilitet. Klienterna returnerar tillstånd under den senaste genomsökningen.|  
|**Genomsökning 3 – klienter som i en samling rapporterar ett visst tillstånd (sekundär)**|Visar alla datorer för en angiven samling och ett angivet tillstånd för kompatibilitetsgenomsökning under den senaste kompatibilitetsgenomsökningen.|  
|**Genomsökning 4 – klienter på en plats som rapporterar ett specifikt tillstånd (sekundär)**|Ange en plats för att visa alla datorer med ett angivet tillstånd för kompatibilitetskontroll. Klienterna returnerar statusen under den senaste genomsökningen.|  



## <a name="software-updates---e-troubleshooting"></a>Program uppdateringar – E fel sökning  

Följande fyra rapporter visas under kategorin **program uppdateringar – E fel sökning** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Fel sökning 1 – genomsöknings fel**|Visar genomsökningsfel på platsen och det antal datorer som har varje fel.|  
|**Fel sökning 2 – distributions fel**|Visar distributionsfelen på platsen och det antal datorer som har varje fel.|  
|**Fel sökning 3 – datorer som inte har ett speciellt genomsöknings fel (sekundär)**|Visar en lista över de datorer där en sökning misslyckades på grund av ett angivet fel.|  
|**Felsökning 4 – datorer med specifikt distributionsfel (sekundär)**|Visar en lista över datorer där distributionen av uppdateringen misslyckas på grund av ett angivet fel.|  



## <a name="state-migration"></a>Tillståndsmigrering  

Följande tre rapporter visas under kategorin **tillståndsmigrering** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Tillståndsmigreringsinformation för en specifik källdator**|Visar tillståndsmigreringsinformation för en angiven dator.|  
|**Tillståndsmigreringsinformation för en specifik tillståndsmigreringsplats**|Visar tillståndsmigreringsinformation för en angiven tillståndsmigreringsplats.|  
|**Tillståndsmigreringsplatser för en viss webbplats**|Visar tillståndsmigreringsplatser för en angiven plats.|  



## <a name="status-messages"></a>Statusmeddelanden  

Följande 12 rapporter visas under kategorin **status meddelanden** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla meddelanden för ett visst meddelande-ID**|Visar en lista över statusmeddelanden som har ett angivet meddelande-ID.|  
|**Klienter som för en specifik plats har rapporterat fel under de senaste 12 timmarna**|Visar en lista över datorer och komponenter som har rapporterat fel under de senaste 12 timmarna och antalet fel som har rapporterats.|  
|**Komponentmeddelanden för de senaste 12 timmarna**|Visar en lista över komponentmeddelanden för de senaste 12 timmarna för en angiven platskod, dator och komponent.|  
|**Komponentmeddelanden den senaste timmen**|Visar en lista över status meddelanden som har skapats under den senaste timmen av en angiven komponent på en angiven dator på en angiven plats.|  
|**Räkna komponentmeddelanden den senaste timmen för en specifik plats**|Visar antalet statusmeddelanden per komponent och angelägenhetsgrad som har rapporterats under den senaste timmen på en angiven plats.|  
|**Räkna fel de senaste 12 timmarna**|Visar antalet statusmeddelanden för serverkomponentfel under de senaste 12 timmarna.|  
|**Allvarliga fel (utifrån komponent)**|Visar en lista över datorer som har rapporterat allvarliga fel efter komponent.|  
|**Allvarliga fel (per datornamn)**|Visar en lista över datorer som har rapporterat allvarliga fel efter datornamn.|  
|**Senaste 1 000 meddelandena för en specifik dator (fel och varningar)**|Visar en sammanfattning av de senaste 1 000 fel- och varningsmeddelandena om komponentstatus för en angiven dator.|  
|**Senaste 1 000 meddelandena för en specifik dator (fel och information)**|Visar en sammanfattning av de 1 000 senaste fel-, varnings- och informationsmeddelandena om komponentstatus för en angiven dator.|  
|**Senaste 1 000 meddelandena för en specifik dator (fel)**|Visar en sammanfattning av de senaste 1000 felmeddelandena om komponentstatus för en angiven dator.|  
|**Senaste 1 000 meddelanden för en specifik serverkomponent**|Visar en sammanfattning av de senaste 1 000 statusmeddelandena för en angiven serverkomponent.|  



## <a name="status-messages---audit"></a>Status meddelanden – granskning  

Följande tre rapporter visas under kategorin **status meddelanden – granskning** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla granskningsmeddelanden för en specifik användare**|Visar en sammanfattning av alla granskningsstatusmeddelanden för en angiven användare. Gransknings meddelanden beskriver åtgärder som vidtas i Configuration Manager-konsolen som lägger till, ändrar eller tar bort objekt i Configuration Manager.|  
|**Fjärr styrning – alla datorer som fjärrstyrs av en speciell användare**|Visar en sammanfattning av statusmeddelanden som visar fjärrstyrning av klientdatorer av en angiven användare.|  
|**Fjärr styrning-all fjärr styrnings information**|Visar en sammanfattning av statusmeddelanden som är relaterade till fjärrstyrning av klientdatorer.|  



## <a name="task-sequence---deployment-status"></a>Aktivitetssekvens-distributions status  

Följande 11 rapporter visas under kategorin **aktivitetssekvens-distributions status** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla systemresurser för en aktivitetssekvensdistribution i ett specifikt tillstånd**|Visar en lista över måldatorerna för den angivna aktivitetssekvensdistributionen i ett angivet distributionstillstånd.|  
|**Alla systemresurser för en aktivitetssekvensdistribution som är i ett specifikt tillstånd och inte är tillgänglig för okända datorer**|Visar en lista över måldatorerna för den angivna aktivitetssekvensdistributionen som befinner sig i ett angivet distributionstillstånd.|  
|**Antal systemresurser med tilldelade aktivitetssekvensdistributioner som inte har körts**|Visar antalet datorer som har godkänt aktivitetssekvenser, men inte har kört aktivitetssekvensen.|  
|**Historik för aktivitetssekvensdistribution på en dator**|Visar status för varje steg i den angivna aktivitetssekvensdistributionen på den angivna måldatorn. Om ingen post returneras har aktivitetssekvensen inte startats på datorn.|  
|**Lista med datorer som överskred en angiven tidsgräns vid körningen av en aktivitetssekvensdistribution**|Visar en lista med måldatorer som överskred den angivna tiden för att köra en aktivitetssekvens.|  
|**Körningstid för en specifik aktivitetssekvensdistribution på en specifik måldator**|Visar den totala tid som det tog för att slutföra en aktivitetssekvensdistribution på en angiven dator.|  
|**Körningstid för varje steg i en aktivitetssekvensdistribution på en specifik måldator**|Visar den tid det tog att slutföra varje steg i den angivna aktivitetssekvensdistributionen på den angivna måldatorn.|  
|**Status för en specifik aktivitetssekvensdistribution för en specifik dator**|Visar statussammanfattningen för en angiven aktivitetssekvensdistribution på en angiven dator.|  
|**Status för en aktivitetssekvensdistribution på en okänd måldator**|Visar status för den angivna aktivitetssekvensdistributionen på den angivna okända måldatorn.|  
|**Statusöversikt för en specifik aktivitetssekvensdistribution**|Visar en statussammanfattning för alla resurser som har varit mål för en distribution.|  
|**Statusöversikt för en angiven aktivitetssekvensdistribution som är tillgänglig för okända datorer**|Visar status sammanfattning för alla resurser som är riktade till den angivna distributionen och som är tillgänglig för en samling som innehåller okända datorer.|  



## <a name="task-sequence---deployments"></a>Aktivitetssekvens-distributioner  

Följande 11 rapporter visas under kategorin **aktivitetssekvens-distributioner** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla systemresurser i en specifik grupp eller fas i en specifik aktivitetssekvensdistribution**|Visar en lista över datorer som för närvarande körs i en angiven grupp eller fas för en angiven aktivitetssekvensdistribution.|  
|**Alla systemresurser där aktivitetssekvensdistribution misslyckades inom en specifik grupp eller fas**|Visar en lista över datorer som misslyckades i en angiven grupp/fas för den angivna aktivitetssekvensdistributionen.|  
|**Alla distributioner av aktivitetssekvenser**|Visar information om alla aktivitetssekvensdistributioner som har initierats från den aktuella platsen.|  
|**Alla aktivitetssekvensdistributioner tillgängliga för okända datorer**|Visar information om alla aktivitetssekvensdistributioner som har initierats från platsen och distribuerats till samlingar som innehåller okända datorer.|  
|**Antal fel i varje fas eller grupp för en specifik aktivitetssekvens**|Visar antalet fel i varje fas eller grupp för den angivna aktivitetssekvensen.|  
|**Antalet fel i varje fas eller grupp för en specifik aktivitetssekvensdistribution**|Visar antalet fel i varje fas eller grupp för den angivna aktivitetssekvensdistributionen.|  
|**Distributionsstatus för alla aktivitetssekvensdistributioner**|Visar övegripande förlopp för alla aktivitetssekvensdistributioner.|  
|**Förlopp för pågående aktivitetssekvens**|Visar förloppet för den angivna aktivitetssekvensen.|  
|**Förlopp för pågående aktivitetssekvensdistribution**|Visar sammanfattningsinformation för den angivna aktivitetssekvensdistributionen.|  
|**Förlopp för alla distributioner för en specifik aktivitetssekvens**|Visar förloppet för alla distributioner för en specifik aktivitetssekvens.|  
|**Översiktsrapport för en aktivitetssekvensdistribution**|Visar sammanfattningsinformation för den angivna aktivitetssekvensdistributionen.|  



## <a name="task-sequence---progress"></a>Aktivitetssekvens-förlopp  

Följande fem rapporter visas under kategorin **aktivitetssekvens-förlopp** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Diagram – vecko förlopp för en aktivitetssekvens**|Visar veckoförloppet för en aktivitetssekvens, med början från distributionsdatumet.|  
|**Förlopp för en aktivitetssekvens**|Visar förloppet för den angivna aktivitetssekvensen.|  
|**Förlopp för alla aktivitetssekvenser**|Visar en sammanfattning av förloppet för alla aktivitetssekvenser.|  
|**Förlopp för aktivitetssekvenser för operativsystemdistributioner**|Visar förloppet för alla aktivitetssekvenser som distribuerar operativsystem.|  
|**Status för alla okända datorer**|Visar en lista med datorer som var okända vid den tidpunkt då de körde en aktivitetssekvensdistribution och om de nu är kända datorer.|  



## <a name="task-sequences---references"></a>Aktivitetssekvenser-referenser  

Följande rapport visas under kategorin **aktivitetssekvenser – referenser** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Innehåll som en specifik aktivitetssekvens innehåller hänvisning till**|Visar innehåll som en angiven aktivitetssekvens hänvisar till.|  



<!--
## Upgrade Assessment  
The following 11 reports are listed under the **Upgrade Assessment** category.

|Report name|Description|  
|-----------------|-----------------|  
|**Application status for a specific computer**|Displays the compatibility of applications that are installed on a computer for a specified operating system.|  
|**Application status for computers in a specific collection**|Displays the overall status for computers in a collection to let you assess them for upgrade to a specified operating system based on the applications on each computer. Use this report to determine which computers have compatible applications before you deploy an operating system.|  
|**Application status summary**|Displays a summary of the application status for a specified operating system. Use this report to determine application compatibility before you deploy an operating system.|  
|**Computers with a specific application installed**|Displays computers with a specified application installed.|  
|**Computers with a specific hardware device**|Displays computers that have a specific hardware device.|  
|**Hardware device status for a specific computer**|Displays the compatibility status of hardware devices for a specified operating system that are found on a specified computer.|  
|**Hardware device status for computers in a specific collection**|Displays the overall status for hardware devices for a specified operating system for computers in a specified collection. Use this report to determine hardware compatibility before you deploy an operating system.|  
|**Hardware device status summary**|Displays a summary of hardware device status for a specified operating system. You can use this report to determine hardware device compatibility before you deploy an operating system.|  
|**Operating system hardware requirements**|Displays the minimum and recommended hardware criteria for operating systems.|  
|**Operating system requirement status for computers in a specific collection**|Displays the status of operating system requirements for the specified operating system for computers in a specified collection. Use this report to determine if a computer meets the specified operating system requirements for CPU processor speed, memory size, and hard disk space.|  
|**Upgrade assessment summary**|Displays the upgrade assessment summary. You can use this report to assess the overall status for upgrade compatibility.|  
-->



## <a name="user---device-affinity"></a>Mappning mellan användare och enhet  

Följande två rapporter visas under kategorin mappning mellan **användare och enhet** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Väntande tillhörighetskopplingar per samling för användarenheter**|Den här rapporten visar alla väntande tillhörighetskopplingar baserat på användningsdata för medlemmar i en samling.|  
|**Tillhörighetskopplingar per samling för användarens enhet**|Visar alla mappningar mellan användare och enheter för den angivna samlingen och grupperar resultaten efter samlings typ (till exempel användare eller enhet).|  



## <a name="user-data-and-profiles-health"></a>Hälso tillstånd för användar data och profiler  

Följande fyra rapporter visas under kategorin **användar data och profiler hälso tillstånd** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Hälsorapport för mappomdirigering – information**|Visar hälso tillstånds information om Mappomdirigering för var och en av de omdirigerade mapparna för en specifik användare.|  
|**Hälsorapport om centrala användarprofiler – information**|Visar hälso tillstånds information om den centrala användar profilen för en angiven användare.|  
|**Hälsorapport om användardata och profiler – information**|Visar fel-eller varnings information om mappomdirigering eller centrala användar profiler. Den här rapporten är informations målet från sammanfattnings rapporten.|  
|**Hälsorapport om användardata och profiler – sammanfattning**|Visar en sammanfattning av hälsotillstånd för mappomdirigering och centrala användarprofiler.|  



## <a name="users"></a>Användare  

Följande tre rapporter visas under kategorin **användare** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Datorer för ett specifikt användarnamn**|Visar en lista med de datorer som användes av en angiven användare.|  
|**Räkna användare per domän**|Visar antalet användare i varje domän.|  
|**Användare i en specifik domän**|Visar en lista med användare och deras datorer i en angiven domän.|  



## <a name="virtual-applications"></a>Virtuella program  

Följande sju rapporter visas under kategorin **virtuella program** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Resultat för virtuella App-V-miljöer**|Visar information om en angiven virtuell miljö som befinner sig i ett specifikt tillstånd för en angiven samling.|  
|**Resultat för resurs i den virtuella App-V-miljön**|Visar information om en angiven virtuell miljö för en angiven till gång. Det visar även alla distributions typer för den angivna virtuella miljön.|  
|**Status för den virtuella App-V-miljön**|Visar kompatibilitetsinformation för en angiven virtuell miljö för en angiven samling.|  
|**Datorer med ett specifikt virtuellt program**|Visar en sammanfattning av datorer som har en angiven App-V-programgenväg som skapades av Application Virtualization Management Sequencer.|  
|**Datorer med ett specifikt virtuellt programpaket**|Visar en sammanfattning av datorer som har det angivna App-V-programpaketet.|  
|**Antalet instanser av virtuella programpaket**|Visar antalet upptäckta App-V-programpaket.|  
|**Antal instanser av virtuella program**|Visar antalet upptäckta App-V-program.|  



## <a name="vulnerability-assessment"></a>Sårbarhetsbedömning

Följande rapport visas under kategorin **sårbarhets bedömning** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Övergripande rapport om sårbarhets bedömning**|Identifierar säkerhets-, administrations-och efterlevnads problem för en speciell dator|  



## <a name="wake-on-lan"></a>Wake on LAN  

Följande sju rapporter visas under kategorin **Wake on LAN** .

|Rapportnamn|Beskrivning|  
|-----------------|-----------------|  
|**Alla måldatorer för Wake-On-LAN-aktivitet**|Ange typen av distribution för att visa en lista över datorer som är riktade för Wake-on-LAN-aktivitet.|  
|**Alla objekt som väntar på väckningsaktiviteter**|Visar objekt som är schemalagda för väckning.|  
|**Alla platser som har aktiverats för Wake-On-LAN**|Visar en lista över alla platser i hierarkin som har aktiverats för Wake-On-LAN.|  
|**Fel som har tagits emot vid sändning av väckningspaket för en definierad period**|Visar fel som har tagits emot vid sändning av väckningspaket för en definierad period.|  
|**Historik för Wake-On-LAN-aktivitet**|Visar en historik över väckningsaktivitet som har inträffat under en viss tid.|  
|**Information om distributionstillstånd för aktiveringsproxy**|Visar information om distributionsstatus för aktiveringsproxy för varje enhet i en angiven samling.|  
|**Sammanfattning av distributionstillståndet för aktiveringsproxy**|Visar en sammanfattning av distributionsstatus för aktiveringsproxy för en angiven samling.|  
