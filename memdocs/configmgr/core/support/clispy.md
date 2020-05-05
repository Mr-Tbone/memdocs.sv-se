---
title: Klientspion
titleSuffix: Configuration Manager
description: Använd klient-spion för att felsöka program varu distribution, inventering och avläsning av program vara på Configuration Manager klienter.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43c3d0f25cf9a71bf07189315ee5f11eba47de1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723434"
---
# <a name="client-spy"></a>Klientspion

*Gäller för: Configuration Manager (aktuell gren)*

Klientens spion är ett av de [Configuration Manager verktygen](tools.md). Det är ett verktyg för fel sökning av program varu distribution, inventering och avläsning av program vara på Configuration Manager klienter. 

Merparten av den information som hämtas av verktyget gäller program distributioner:
- Alla aktuella program distributioner 
- Historik för program varu distribution
- Konfiguration av klientcachen
- Cachelagrade objekt
- Väntande nödvändiga distributioner
- Tillgängliga distributioner  

Den visar även följande inventerings information
- Senaste inventerings cykel datum
- Senaste rapport datum
- Huvud-och del versioner av program varu inventering
- Fil insamling
- Maskinvaruinventering
- IDMIF-samling
- Identifierings data poster (DDR) 

Regler för avläsning av program vara visas också. 

> [!Note]   
> För att förbättra prestanda samlar verktyget bara in information för varje flik när du väljer den. När du klickar på **Uppdatera**uppdateras bara informationen för den aktuella fliken som visas.



## <a name="usage"></a>Användning


### <a name="tools-menu"></a>Verktyg-menyn

Följande åtgärder är tillgängliga på **verktyg** -menyn:  

#### <a name="connect"></a>Anslut
Hämta information från en annan dator.  

- Som standard visar verktyget information från den aktuella datorn. 

- Anslut med fjärrdatorns namn, användar namn och lösen ord för kontot. Verktyget skapar en anslutning till resursen IPC $ på fjärrdatorn. Anslutningen tas bort när verktyget avslutas eller om du ansluter till en annan dator.  

- Det krävs ett konto med tillräcklig behörighet för att hämta informationen.  

- Om du inte anger ett användar namn och lösen ord använder klient-spion säkerhets kontexten för den aktuella inloggade användaren för att försöka upprätta anslutningen.  

- När du ansluter till en fjärran sluten dator visas alla flikar som visas information från fjärrdatorn.

#### <a name="software-distribution"></a>Programvarudistribution
Visar flikarna för [program varu distribution](#software-distribution) och döljer de andra flikarna. Som standard visar client Spy flikarna för program varu distribution.

#### <a name="inventory"></a>Inventering
Visar fliken lager och döljer de andra flikarna.

#### <a name="software-metering"></a>Avläsning av programvara
Visar fliken avläsning av program vara och döljer de andra flikarna.

#### <a name="save-current-tab-to-file"></a>Spara aktuell flik till fil
Sparar informationen på fliken som visas i den aktuella text filen som du anger. 

#### <a name="save-all-tabs-to-file"></a>Spara alla flikar i filen
Sparar informationen i alla flikar i en textfil som du anger. Det sparar bara information som ditt konto kan se.



## <a name="software-distribution-tab"></a>Fliken program varu distribution

Konfigurera inställningar på följande fyra flikar:
- [Körnings begär Anden för program varu distribution](#bkmk_exec-requests)
- [Historik för program varu distribution](#bkmk_history)
- [Cachelagrad information om program varu distribution](#bkmk_cache-info)
- [Väntande körningar av program varu distribution](#bkmk_pending-exec)


### <a name="software-distribution-execution-requests"></a><a name="bkmk_exec-requests"></a>Körnings begär Anden för program varu distribution

På den här fliken visas alla befintliga distributioner, inklusive både enhets-och användar mål distributioner.

Varje träd objekt på fliken körnings begär Anden för program distribution innehåller följande fyra attribut:
- Annons-ID. Det här värdet kan vara tomt om det är en tillgänglig distribution. 
- Paket-ID 
- Programnamn 
- Användarvänlig. Detta kan vara mål användar-SID eller SID för den användare som initierade begäran. Om båda är system begär Anden, är den visade användaren system. 

För varje körnings förfrågan visas även följande information i en under träd struktur:
- Programnamn 
- Paket-ID 
- Paketnamn 
- Tid för att skapa begäran 
- Status 
- Kör tillstånd, om tillstånd körs 
- Körnings kontext (användare eller administratör) 
- Historik tillstånd (lyckades, misslyckades eller NotRun) 
- LastRunTime (aldrig om programmet inte har körts tidigare) 
- RetryCount, om tillstånd är WaitingRetry 
- ContentAccess (antal återförsök, om tillstånd är WaitingRetry) 
- FailureCode, om tillstånd är WaitingRetry 
- FailureReason, om tillstånd är WaitingRetry 

Om begäran kräver innehåll är statusen WaitingContent. På fliken cache-information för program distribution visas information om den här nedladdnings förfrågan.

Om körnings förfrågan är en nedladdnings förfrågan visar den också antalet hämtade byte.

> [!Note]   
> Den använder olika ikoner för olika tillstånd för en körnings förfrågan.


### <a name="software-distribution-history"></a><a name="bkmk_history"></a>Historik för program varu distribution

Den här fliken innehåller information om alla program som körs tidigare. Den här informationen lagras i registret.

De huvudsakliga grenarna i det här trädet är de olika användar historiken, inklusive system. Det visar ett under träd som innehåller listan över paket från vilka program har körts för varje användare. 

Paket-ID och paket namn för varje paket under träd visar en lista över program som har körts. Följande attribut visas för varje: 
- Program namn
- Körnings tillstånd
- Senaste körnings tid
- Felkod
- Felorsak  

Felkoden och fel orsaken är tomma när ett program har körts.


### <a name="software-distribution-cache-information"></a><a name="bkmk_cache-info"></a>Cachelagrad information om program varu distribution

#### <a name="cache-config"></a>Cache-konfiguration
Innehåller information om cachen för Configuration Manager-klienten. Den här informationen omfattar cache-platsen, cache-storleken och om den används för närvarande. 

#### <a name="cached-items"></a>Cachelagrade objekt
Innehåller ett under träd för alla objekt som för närvarande finns i cacheminnet. Varje träd objekt innehåller följande information om varje objekt: 
- Objektets plats (mapp) i cachen
- Nuvarande tillstånd
- Paket-ID
- Paketnamn
- Paketversion
- Paket storlek
- Aktuellt referens antal
- Senaste refererade tid (UTC)  

#### <a name="downloading-items"></a>Laddar ned objekt
Detta är de objekt som klienten hämtar för tillfället. Var och en av dem visar samma information som visas av de cachelagrade objekten och antalet hämtade kilobyte. 


### <a name="software-distribution-pending-executions"></a><a name="bkmk_pending-exec"></a>Väntande körningar av program varu distribution

Den här fliken innehåller information som beskriver tidigare och framtida nödvändiga distributioner och en lista över tillgängliga distributioner.

Varje träd gren är för varje användar konto med tillgängliga distributioner, inklusive system.

För varje användare innehåller ett under träd följande tre objekt:  

#### <a name="mandatory-advertisements-with-future-executions"></a>Obligatoriska annonser med framtida körningar
Dessa är obligatoriska annonser som fortfarande har program kvar att köras. Detta kan vara antingen återkommande, eng ång slö eller flera schema annonser. Varje visar annons-ID, nästa körnings tillfälle och det schema som annonsen körs på. 

#### <a name="optional-advertisements"></a>Valfria annonser
Visar en lista över alla annonser som har publicerats. Den visar även information som annonserings-ID, program namn och paket namn för var och en. 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Tidigare obligatoriska annonser utan framtida schemalagda körningar
Det här är en lista över annonser som finns på klienten och som inte har några program som är schemalagda att köras. Annonserings-ID, paket namn och program namn visas. Ett under träds objekt visas för alla annonser som är valfria.

> [!Note]  
> Paket namns information är bara tillgänglig för paket som har annonserade principer kopplade till den dator som visas. Paket som inte längre har tillgängliga principer som är kopplade till dem visar meddelandet "paket namnet är inte längre tillgängligt".  



## <a name="inventory-tab"></a>Fliken inventering

Det finns bara en flik som innehåller inventerings information. Huvud trädet innehåller följande fem objekt:  

- **Program varu inventering**: innehåller det datum då den senaste cykeln startade, datumet för den senaste rapporten och de lägre och större versionerna av den senaste rapporten.  

- **Fil insamling**: innehåller det datum då den senaste cykeln startade, datumet för den senaste rapporten och de lägre och större versionerna av den senaste rapporten.  

- **Maskin varu inventering**: innehåller datumet då den senaste cykeln startade, datumet för den senaste rapporten och de lägre och större versionerna av den senaste rapporten.  

- **IDMIF-samling**: innehåller datumet då den senaste cykeln startade, datumet för den senaste rapporten och de lägre och större versionerna av den senaste rapporten.  

- **DDR**: innehåller det datum då den senaste cykeln startade, datumet för den senaste rapporten och de lägre och större versionerna av den senaste rapporten. DDR-informationen visas också i ett under träd.



## <a name="software-metering-tab"></a>Fliken avläsning av program vara

Den här fliken visar information som ett under träd och innehåller alla regler för avläsning av program vara. Varje regel visas som en nod som identifieras av fil namnet och regel-ID: t. Expandera varje nod i trädet och visa följande information:
- Explorer-filnamn 
- Ursprungligt fil namn
- Regel-ID
- Filversion
- Språk


