---
title: Uppdateringsverktyg för återställning
titleSuffix: Configuration Manager
description: Använd verktyget uppdatera återställning för uppdateringar i konsolen för Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b4aa67280c879d6f7feaf549ac7f13ba0136ca91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720753"
---
# <a name="update-reset-tool"></a>Uppdateringsverktyg för återställning

*Gäller för: Configuration Manager (aktuell gren)*  


Från och med version 1706 innehåller Configuration Manager primära platser och centrala administrations platser verktyget Configuration Manager uppdaterings återställning, **CMUpdateReset. exe**. Använd verktyget för att åtgärda problem när uppdateringar i konsolen har problem med att hämta eller replikera. Verktyget finns i mappen ***\CD.latest\SMSSETUP\TOOLS*** på plats servern.

Du kan använda det här verktyget med alla versioner av den aktuella grenen som finns kvar i supporten.

Använd det här verktyget när en [uppdatering i konsolen](install-in-console-updates.md) ännu inte har installerats och är i ett felaktigt tillstånd. Ett felaktigt tillstånd innebär att uppdaterings nedladdningen pågår men fastnar eller tar lång tid. Lång tid anses vara timmar som är längre än dina historiska förväntningar för uppdaterings paket av liknande storlek. Det kan också vara ett haveri att replikera uppdateringen till underordnade primära platser.  

När du kör verktyget körs det mot den uppdatering som du anger. Som standard tar verktyget inte bort installerade eller nedladdade uppdateringar.  

### <a name="prerequisites"></a>Förutsättningar
Det konto som du använder för att köra verktyget kräver följande behörigheter:
- **Läs** -och **Skriv** behörighet till plats databasen för den centrala administrations platsen och till varje primär plats i hierarkin. Om du vill ange dessa behörigheter kan du lägga till användar kontot som medlem i **db_datawriter** och **db_datareader** [fasta databas roller](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) i Configuration Manager databasen för varje plats. Verktyget samverkar inte med sekundära platser.
- **Lokal administratör** på platsen på den översta nivån i hierarkin.
- **Lokal administratör** på den dator som är värd för tjänst anslutnings punkten.

Du behöver GUID för det uppdaterings paket som du vill återställa. Hämta GUID:
  1.   I-konsolen går du till **Administration**  >  **uppdateringar och underhåll**.
  2.   I visningsfönstret högerklickar du på rubriken för en av kolumnerna (t. ex. **tillstånd**) och väljer sedan **paket-GUID** för att lägga till kolumnen i visningen.
  3.   Kolumnen visar nu GUID för uppdaterings paketet.

> [!TIP]  
> Om du vill kopiera GUID väljer du raden för det uppdaterings paket som du vill återställa och använder sedan CTRL + C för att kopiera raden. Om du klistrar in det kopierade valet i en text redigerare kan du sedan kopiera bara GUID för användning som en kommando rads parameter när du kör verktyget.

### <a name="run-the-tool"></a>Kör verktyget    
Verktyget måste köras på platsen på den översta nivån i hierarkin.

När du kör verktyget använder du kommando rads parametrar för att ange:
- SQL Server på platsen på den översta nivån i hierarkin.
- Plats databasens namn på platsen på den översta nivån.
- GUID för det uppdaterings paket som du vill återställa.

Baserat på uppdateringens status identifierar verktyget de ytterligare servrar som krävs för åtkomst.   

Om uppdaterings paketet är i ett *post hämtnings* tillstånd rensar verktyget inte paketet. Som ett alternativ kan du tvinga borttagning av en nedladdnings bara uppdatering med hjälp av parametern framtvinga borttagning (se kommando rads parametrarna senare i det här avsnittet).

När verktyget har körts:
- Om ett paket har tagits bort startar du om SMS_Executive-tjänsten på platsen på den översta nivån. Sök sedan efter uppdateringar så att du kan ladda ned paketet igen.
- Om ett paket inte har tagits bort behöver du inte vidta några åtgärder. Uppdateringen initieras om och startar sedan om replikering eller installation.

**Kommando rads parametrar:**  


|                        Parameter                         |                                                       Beskrivning                                                        |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **-S &lt; FQDN för SQL Server på platsen på den översta nivån>** | *Obligatoriskt* <br> Ange det fullständiga domän namnet för SQL Server som är värd för plats databasen för platsen på den översta nivån i hierarkin. |
|                **-D &lt; databas namn>**                 |                          *Obligatoriskt* <br> Ange namnet på databasen på platsen på den översta nivån.                          |
|                 **-P &lt; paket-GUID>**                 |                        *Obligatoriskt* <br> Ange GUID för det uppdaterings paket som du vill återställa.                        |
|           **-I &lt; SQL Server instans namn>**           |                    *Valfritt* <br> Identifiera instansen av SQL Server som är värd för plats databasen.                     |
|                       **-FDELETE**                       |                       *Valfritt* <br> Framtvinga borttagning av ett uppdaterings paket som har hämtats.                        |

**Exempel:**  
I ett typiskt scenario vill du återställa en uppdatering som har hämtnings problem. Dina SQL Server-FQDN är *server1.fabrikam.com*, plats databasen är *CM_XYZ*och paketets GUID är *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Du kör: ***CMUpdateReset. exe-S server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

I ett mer extrema scenario vill du framtvinga borttagning av problem med uppdaterings paketet. Dina SQL Server-FQDN är *server1.fabrikam.com*, plats databasen är *CM_XYZ*och paketets GUID är *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Du kör: ***CMUpdateReset. exe-FDELETE-S server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***
