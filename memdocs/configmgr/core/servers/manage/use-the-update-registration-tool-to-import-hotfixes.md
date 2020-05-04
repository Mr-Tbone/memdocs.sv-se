---
title: Verktyget uppdatera registrering
titleSuffix: Configuration Manager
description: Ta reda på när och hur du använder verktyget uppdatera registrering för att manuellt importera en uppdatering till Configuration Manager-konsolen.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 420b13005e8f9ac3d79f7d94398e6aa0ddcc190c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711240"
---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-configuration-manager"></a>Använd verktyget uppdatera registrering för att importera snabb korrigeringar till Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Vissa uppdateringar för Configuration Manager är inte tillgängliga från Microsofts moln tjänst och hämtas endast out-of-band. Ett exempel är en begränsad version av en snabbkorrigering för att lösa ett specifikt problem.   
När du måste installera en out-of-band-version och fil namnet för uppdateringen eller snabb korrigeringen slutar med tillägget **Update. exe**, kan du använda **verktyget uppdatera registrering** för att manuellt importera uppdateringen till Configuration Manager-konsolen. Med verktyget kan du extrahera och överföra uppdateringspaketet till platsservern och registrera uppdateringen med Configuration Manager-konsolen.  

 Om snabb korrigerings filen har fil namns tillägget **. exe** (inte **Update. exe**) kan [du läsa Använd installations programmet för snabb korrigeringar för att installera uppdateringar för Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  Det här avsnittet innehåller allmän vägledning om hur du installerar snabb korrigeringar som uppdaterar Configuration Manager. Mer information om en speciell snabb korrigering eller uppdatering finns i motsvarande Knowledge Base-artikel (KB) på Microsoft Support.  

 **Krav för att använda verktyget Uppdatera registrering:**  

-   Endast out-of-band-uppdateringar som slutar med tillägget **. Update. exe** kan installeras med det här verktyget  

-   Verktyget är självständigt med de enskilda uppdateringar du får direkt från Microsoft  

-   Verktyget har inte något beroende för läget för tjänstanslutningspunkten  

-   Verktyget måste köras på datorn som är värd för tjänstanslutningspunkten  

-   Datorn där verktyget körs (tjänst anslutnings punktens dator) måste ha .NET Framework 4,52 installerat  

-   Kontot som du använder för att köra verktyget måste ha **lokal administratörs** behörighet på datorn som är värd för tjänst anslutnings punkten (där verktyget körs)  

-   Det konto som du använder för att köra verktyget måste ha **Skriv** behörighet till följande mapp på den dator som är värd för tjänst anslutnings punkten: ** &lt;ConfigMgr installations\>katalog \EasySetupPayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>Använda verktyget Uppdatera registrering  

1. På datorn som är värd för tjänstanslutningspunkten:  

   -   Öppna en kommando tolk med administrativ behörighet och ändra sedan katalogerna till den plats som innehåller ** &lt;\>-&lt;produkt\>-&lt;produkt version KB-artikel-\>ID ConfigMgr. Update. exe**  

2. Kör följande kommando för att starta verktyget Uppdatera registrering:  

   -   **&lt;\>-Produkt&lt;\>produkt version-KB-artikel\>-ID ConfigMgr. Update. exe&lt;**  

   När snabbkorrigeringen har registrerats visas den som en ny uppdatering i konsolen inom 24 timmar.  Du kan påskynda processen:

   - Öppna Configuration Manager-konsolen och gå till **Administration** > **uppdateringar och underhåll**och klicka sedan på **Sök efter uppdateringar**. (Före version 1702 har uppdateringar och underhåll under **administrations** > **Cloud Services**.) 

   De åtgärder som utförs med verktyget Uppdatera registrering loggas i en loggfil på den lokala datorn. Logg filen har samma namn som filen Hotfix. exe och sparas i mappen **% systemroot%/Temp** .  

    När uppdateringen har registrerats kan du stänga verktyget Uppdatera registrering.  

3. Öppna Configuration Manager-konsolen och gå till **Administration** > **uppdateringar och underhåll**. Snabbkorrigeringarna som importerades är nu tillgängliga för installation. (Före version 1702 har uppdateringar och underhåll under **administrations** > **Cloud Services**.)

   Information om hur du installerar uppdateringar finns [i installera uppdateringar i konsolen för Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  
