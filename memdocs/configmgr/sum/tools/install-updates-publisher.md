---
title: Installera Updates Publisher
titleSuffix: Configuration Manager
description: Installera System Center Updates Publisher i din miljö
ms.date: 08/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f83e7207207496d69342a2322909e972ada5676
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720375"
---
# <a name="install-updates-publisher"></a>Installera Updates Publisher

*Gäller för: System Center Updates Publisher*

Informationen i de här artiklarna kan hjälpa dig att ladda ned, installera och konfigurera Updates Publisher för användning med din Configuration Managers miljö.

## <a name="prerequisites-and-limitations"></a>Krav och begränsningar
System Center Updates Publisher kan bara användas med Configuration Manager. Den är inte avsedd att användas med fristående WSUS-hierarkier.

I följande avsnitt beskrivs kraven för att installera och använda Updates Publisher, samt begränsningar och kända problem för användning.  

### <a name="operating-systems"></a>Operativsystem
Installera och kör Updates Publisher på en 64-bitars utgåva av följande operativ system. Det finns inga minimi krav för ackumulerad uppdatering eller service pack.

-   Windows Server 2016 (standard, data Center)
-   Windows Server 2012 R2 (standard, data Center)
-   Windows 10 (Pro, Education, Pro Education, Enterprise)
-   Windows 8,1 (Professional, Enterprise)

### <a name="prerequisites"></a>Krav
Följande krävs på den dator som kör Updates Publisher.

-   **64-bitars operativ system**: datorn där du installerar Updates Publisher måste köra ett 64-bitars operativ system.
-   **WSUS 6,2 eller senare**:
    -   På Windows Server installerar du standard administrations konsolen för att uppfylla det här kravet.
    -   För Windows 10 och Windows 8,1 installerar du [verktyg för fjärrserveradministration (RSAT) för Windows-operativsystem](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). Detta installerar det nödvändiga stödet för att använda Updates Publisher (*API-och PowerShell-cmdletar*och *hanterings konsolen för användar gränssnitt*).
-   **Behörigheter**:
    -   Installation: lokal administratör
    -   De flesta åtgärder: lokal användare
    -   Publicering eller åtgärder som inbegriper WSUS: medlem i gruppen WSUS-administratörer på WSUS-servern.

### <a name="supported-languages"></a>Språk som stöds
Updates Publisher är bara tillgängligt på engelska men kan hantera uppdateringar för andra språk. Språk stödet är beroende av uppgiften, till exempel att publicera, skapa eller redigera uppdateringar.

När du exporterar eller publicerar uppdateringar visar Updates Publisher titeln och beskrivningen av program uppdateringen baserat på språkvarianten för datorn där Updates Publisher är installerat.

Du kan till exempel skapa en program uppdatering som har en engelsk och spansk rubrik.

-   Om du skapar uppdateringen på en dator vars språk är engelska, visas rubriken och beskrivningen på engelska som standard.
-   Om du sedan exporterar eller publicerar uppdateringen till en dator vars språk är spanska på den datorn visas rubriken och beskrivningen på spanska.

### <a name="publishing"></a>Publicera
När du publicerar program uppdateringar kan du ange språket för den binära filen för program uppdatering. Du kan också ange att binärfilen är språk oberoende. Följande språk stöds:

-   Arabiska
-   Kinesiska (Hongkong SAR)
-   Kinesiska (traditionell)
-   Kinesiska (förenklad)
-   Tjeckiska
-   Danska
-   Nederländska
-   Svenska
-   Finska
-   Franska
-   Tyska
-   Grekiska
-   Hebreiska
-   Ungerska
-   Italienska
-   Japanska
-   Koreansk
-   Norska
-   Polska
-   Portugisiska
-   Portugisiska (Brasilien)
-   Ryska
-   Spanska
-   Svenska
-   Turkiska

### <a name="software-update-titles-and-descriptions"></a>Program uppdaterings titlar och beskrivningar
Följande språk stöds för program uppdaterings titlar och beskrivningar.

-   Kinesiska (traditionell)
-   Kinesiska (förenklad)
-   Svenska
-   Franska
-   Tyska
-   Italienska
-   Japanska
-   Koreansk
-   Portugisiska (Brasilien)
-   Ryska
-   Spanska

## <a name="install-updates-publisher"></a>Installera Updates Publisher
Hämta **UpdatesPubliser. msi** för att installera System Center Updates Publisher från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55543).

Installera Updates Publisher genom att köra **UpdatesPublisher. msi** på en dator som uppfyller *kraven*. Följande mapp skapas i installations programmet som innehåller de filer som krävs för att köra Updates Publisher:%PROGRAMFILES%\Microsoft\UpdatesPublisher *.

Eftersom den här mappen innehåller alla filer som krävs för att använda Updates Publisher, kan du kopiera mappen och dess innehåll till en ny plats eller dator och sedan använda Updates Publisher från den platsen. Den nya platsen eller datorn måste dock uppfylla kraven för att köra Updates Publisher.

När installationen har slutförts kör du **UpdatesPublisher. exe** från mappen *UpdatesPublisher* för att starta Updates Publisher.

## <a name="next-steps"></a>Nästa steg
 När du har installerat Updates Publisher rekommenderar vi att du [konfigurerar alternativen](updates-publisher-options.md) för Updates Publisher. Du måste konfigurera vissa alternativ innan du kan använda vissa funktioner i Updates Publisher.

 Men om du vill använda standardvärdena och inte planerar att distribuera uppdateringar till en uppdaterings Server eller till hanterade enheter, kan du gå direkt till att [hantera program uppdaterings kataloger](updates-publisher-catalogs.md)eller [skapa program uppdateringar](create-updates-with-updates-publisher.md) och skapa uppdaterings kataloger.
