---
title: Innehålls käll plats
titleSuffix: Configuration Manager
description: Läs om de Configuration Manager inställningar som gör det möjligt för klienter att hitta innehåll i ett långsamt nätverk.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9d58138380263a7e7c3305ab2ad663a5246098b4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720242"
---
# <a name="content-source-location-scenarios-in-configuration-manager"></a>Scenarier för innehålls käll platser i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Före version 1610 har Configuration Manager stöd för flera inställningar som kombineras för att definiera hur och var klienterna ska hitta innehåll när de är i ett långsamt nätverk. Möjliga kombinationer påverkar den innehålls plats klienter som använder och om de kan använda en återställnings plats när en önskad källa för innehåll inte är tillgänglig.  

> [!IMPORTANT]  
> **Om dina webbplatser kör version 1511, 1602 eller 1606**, gäller informationen i det här avsnittet för din infrastruktur. Se även [gränser grupper för versionerna 1511, 1602 och 1606](../../servers/deploy/configure/boundary-groups-for-1511-1602-and-1606.md) för information som är speciell för gränser grupper med dessa versioner av Configuration Manager.
>
> **Om dina webbplatser kör version 1610 eller senare**kan du använda informationen i [definiera plats gränser och gräns grupper för Configuration Manager](../../servers/deploy/configure/define-site-boundaries-and-boundary-groups.md) för att förstå hur klienter hittar distributions platser som har tillgängligt innehåll.





**Följande tre inställningar definierar beteendet när klienter begär innehåll:**

- **Tillåt återställnings käll plats för innehåll** (aktiverat eller inte aktiverat): det här är ett alternativ som du kan aktivera på fliken **begränsnings grupper** för en distributions plats. Detta gör att klienten kan använda en distributions plats som har kon figurer ATS som en återställnings plats när innehållet inte är tillgängligt på en prioriterad distributions plats.  

  - **Distributions beteende för nätverks anslutnings hastighet**: varje distribution konfigureras med en av följande beteenden som ska användas när anslutningen till distributions platsen är långsam:  

    -   **Hämta innehåll från distributions platsen och kör det lokalt**  

    -   **Hämta inte innehåll**: det här alternativet används bara när en klient använder en återställnings plats för att hämta innehåll.  

    Anslutnings hastigheten för en distributions plats konfigureras på fliken **referenser** i en avgränsnings grupp och är den som är unik för den begränsande gruppen.  

  - **Paket distribution på begäran** (till prioriterade distributions platser): det här alternativet aktive ras när du väljer alternativet **distribuera innehållet för det här paketet till prioriterade distributions platser** på fliken **distributions inställningar** i ett pakets eller programmets egenskaper. När det här alternativet är aktiverat dirigeras Configuration Manager för att automatiskt kopiera innehållet till en prioriterad distributions plats som ännu inte har innehållet efter att klienten begär innehåll från den distributions platsen.  


 **Följande krav gäller för alla scenarier:**


-   Innehållet är tillgängligt på en återställnings distributions plats  

-   Distributions platser är online och tillgängliga  


## <a name="scenario-1"></a>Scenario 1  
 Gäller när följande konfigurationer finns:  

-   **Innehållet är tillgängligt på en prioriterad distributions plats**  

-   **Tillåt reserv**: inte aktiverat  

-   **Distributions beteende för långsamma nätverk**: alla konfigurationer  


**Information:** (konfigurationen för paket distribution på begäran är inte relevant i det här scenariot.)  

1.  Klienten skickar en innehålls förfrågan till hanterings platsen.  

2.  En innehålls plats lista skickas tillbaka till klienten från hanterings platsen med de primära distributions platser som innehåller innehållet.  

3.  Klienten laddar ned innehållet från en primär distributions plats på listan.  

## <a name="scenario-2"></a>Scenario 2  
 Följande konfigurationer finns:  

-   **Innehållet är tillgängligt på en prioriterad distributions plats**  

-   **Tillåt reserv**: aktiverat  

-   **Distributions beteende för ett långsamt nätverk**: Hämta inte innehåll  


**Information:** (konfigurationen för paket distribution på begäran är inte relevant i det här scenariot.)  

1.  Klienten skickar en innehålls förfrågan till hanterings platsen. Klienten innehåller en flagga med begäran som anger att återställnings distributions platser är tillåtna.  

2.  En innehålls plats lista skickas tillbaka till klienten från hanterings platsen med de primära distributions platser och återställnings distributions platser som innehåller innehållet.  

3.  Klienten laddar ned innehållet från en primär distributions plats på listan.  

## <a name="scenario-3"></a>Scenario 3  
 Följande konfigurationer finns:  

-   **Innehållet är tillgängligt på en prioriterad distributions plats**  

-   **Tillåt reserv**: aktiverat  

-   **Distributions beteende för ett långsamt nätverk**: Hämta och installera innehåll  


**Information:** (konfigurationen för paket distribution på begäran är inte relevant i det här scenariot.)  

1.  Klienten skickar en innehålls förfrågan till hanterings platsen. Klienten innehåller en flagga med begäran som anger att återställnings distributions platser är tillåtna.  

2.  En innehålls plats lista skickas tillbaka till klienten från hanterings platsen med de primära distributions platser och återställnings distributions platser som innehåller innehållet.  

3.  Klienten laddar ned innehållet från en primär distributions plats på listan.  

## <a name="scenario-4"></a>Scenario 4  
 Följande konfigurationer finns:  

-   **Innehållet är inte tillgängligt på en prioriterad distributions plats**  

-   **Distribuera det här paketets innehåll till prioriterade distributions platser** har inte Aktiver ATS  

-   **Tillåt reserv**: inte aktiverat  

-   **Distributions beteende för långsamma nätverk**: alla konfigurationer  


**Information**  

1.  Klienten skickar en innehålls förfrågan till hanterings platsen.  

2.  En innehålls plats lista skickas tillbaka till klienten från hanterings platsen med de primära distributions platser som har innehållet. Det finns inga prioriterade distributions platser i listan.  

3.  Klienten Miss lyckas med att meddelande **innehållet inte är tillgängligt** och går in i återförsöks läge. En ny innehålls förfrågan startas varje timme.  

## <a name="scenario-5"></a>Scenario 5  
 Följande konfigurationer finns:  

-   **Innehållet är inte tillgängligt på en prioriterad distributions plats**  

-   **Distribuera det här paketets innehåll till prioriterade distributions platser** har inte Aktiver ATS  

-   **Tillåt reserv**: aktiverat  

-   **Distributions beteende för ett långsamt nätverk**: Hämta inte innehåll  


**Information**  

1.  Klienten skickar en innehålls förfrågan till hanterings platsen. Klienten innehåller en flagga med begäran som anger att återställnings distributions platser är tillåtna.  

2.  En innehålls plats lista skickas tillbaka till klienten från hanterings platsen med de primära distributions platser och återställnings distributions platser som har innehållet. Det finns inga prioriterade distributions platser som har innehållet, men minst en återställnings distributions plats har innehållet.  

3.  Innehållet laddas inte ned eftersom distributions egenskapen för när klienten använder en återställnings distributions plats har angetts till **Hämta inte innehåll** (som används när klienterna återgår till att hämta innehållet). Klienten Miss lyckas med att meddelande **innehållet inte är tillgängligt** och går in i återförsöks läge. Klienten gör en ny innehålls förfrågan varje timme.  

## <a name="scenario-6"></a>Scenario 6  
 Följande konfigurationer finns:  

-   **Innehållet är inte tillgängligt på en prioriterad distributions plats**  

-   **Distribuera det här paketets innehåll till prioriterade distributions platser** har inte Aktiver ATS  

-   **Tillåt reserv**: aktiverat  

-   **Distributions beteende för ett långsamt nätverk**: Hämta och installera innehåll  


**Information**  

1.  Klienten skickar en innehålls förfrågan till hanterings platsen. Klienten innehåller en flagga med begäran som anger att återställnings distributions platser är aktiverade.  

2.  En innehålls plats lista skickas tillbaka till klienten från hanterings platsen med de primära distributions platser och återställnings distributions platser som har innehållet. Det finns inga prioriterade distributions platser som har innehållet, men minst en återställnings distributions plats med innehållet.  

3.  Innehållet hämtas från en återställnings distributions plats i listan eftersom distributions egenskapen för när klienten använder en återställnings distributions plats har kon figurer ATS för att **Ladda ned och installera innehållet**.  

## <a name="scenario-7"></a>Scenario 7  
 Följande konfigurationer finns:  

-   **Innehållet är inte tillgängligt på en prioriterad distributions plats**  

-   **Distribuera det här paketets innehåll till prioriterade distributions platser** är aktiverat  

-   **Tillåt reserv**: inte aktiverat  

-   **Distributions beteende för långsamma nätverk**: alla konfigurationer  


**Information**  

1.  Klienten skickar en innehålls förfrågan till hanterings platsen.  

2.  En innehålls plats lista skickas tillbaka till klienten från hanterings platsen med de primära distributions platser som har innehållet. Det finns inga prioriterade distributions platser som har innehållet.  

3.  Klienten Miss lyckas med att meddelande **innehållet inte är tillgängligt** och går in i återförsöks läge. En ny innehålls förfrågan görs varje timma.  

4.  Hanterings platsen skapar en utlösare för distributions hanteraren för distribution av innehållet till alla prioriterade distributions platser för den klient som gjorde innehålls förfrågan.  

5.  Distribution Manager distribuerar innehållet till alla prioriterade distributions platser. I de flesta fall distribueras innehållet till de prioriterade distributions platserna inom en timme.  

6.  En ny innehålls förfrågan initieras av klienten till hanterings platsen.  

7.  En innehålls plats lista skickas tillbaka till klienten från hanterings platsen med de primära distributions platser som har innehållet. Klienten laddar ned innehållet från en primär distributions plats på listan.  

## <a name="scenario-8"></a>Scenario 8  
 Följande konfigurationer finns:  

-   **Innehållet är inte tillgängligt på en prioriterad distributions plats**  

-   **Distribuera det här paketets innehåll till prioriterade distributions platser** är aktiverat  

-   **Tillåt reserv**: aktiverat  

-   **Distributions beteende för ett långsamt nätverk**: Hämta inte innehåll  


**Information**  

1.  Klienten skickar en innehålls förfrågan till hanterings platsen. Klienten innehåller en flagga med begäran som anger att återställnings distributions platser är tillåtna.  

2.  En innehålls plats lista skickas tillbaka till klienten från hanterings platsen med de primära distributions platser och återställnings distributions platser som har innehållet. Det finns inga prioriterade distributions platser som har innehållet, men minst en återställnings distributions plats har innehållet.  

3.  Innehållet laddas inte ned eftersom distributions egenskapen för när klienten använder en återställnings distributions plats har angetts till **Hämta inte**. Klienten Miss lyckas med att meddelande **innehållet inte är tillgängligt** och går in i återförsöks läge. Klienten gör en ny innehålls förfrågan varje timme.  

4.  Hanterings platsen skapar en utlösare för distributions hanteraren för distribution av innehållet till alla prioriterade distributions platser för den klient som gjorde innehålls förfrågan.  

5.  Distribution Manager distribuerar innehållet till alla prioriterade distributions platser. I de flesta fall distribueras innehållet till de prioriterade distributions platserna inom en timme.  

6.  En ny innehålls förfrågan initieras av klienten till hanterings platsen.  

7.  En innehålls plats lista skickas tillbaka till klienten från hanterings platsen med de primära distributions platser som har innehållet.  

8.  Klienten laddar ned innehållet från en primär distributions plats på listan.  

## <a name="scenario-9"></a>Scenario 9  
 Följande konfigurationer finns:  

-   **Innehållet är inte tillgängligt på en prioriterad distributions plats**  

-   **Distribuera det här paketets innehåll till prioriterade distributions platser** är aktiverat  

-   **Tillåt reserv**: aktiverat  

-   **Distributions beteende för ett långsamt nätverk**: Hämta och installera innehåll  


**Information**  

1.  Klienten skickar en innehålls förfrågan till hanterings platsen. Klienten innehåller en flagga med begäran som anger att återställnings distributions platser är tillåtna.  

2.  En innehålls plats lista skickas tillbaka till klienten från hanterings platsen med de primära distributions platser och återställnings distributions platser som har innehållet. Det finns inga prioriterade distributions platser som har innehållet, men minst en återställnings distributions plats har innehållet.  

3.  Innehållet hämtas från en återställnings distributions plats i listan eftersom distributions egenskapen för när klienten använder en återställnings distributions plats har kon figurer ATS för att **Ladda ned och installera innehållet**. Den här distributions inställningen gör det möjligt för en klient som måste använda en återställnings innehålls plats för att hämta innehållet från den platsen.  

4.  Hanterings platsen skapar en utlösare för distributions hanteraren för distribution av innehållet till alla prioriterade distributions platser för den klient som gjorde innehålls förfrågan.  

5.  Distributions hanteraren distribuerar innehållet till alla prioriterade distributions platser, vilket gör att ytterligare klienter kan hämta innehållet utan att använda en återställnings distributions plats.  
