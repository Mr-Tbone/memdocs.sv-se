---
title: Nivåer av diagnostikens användnings data
titleSuffix: Configuration Manager
description: Lär dig mer om de nivåer av diagnostik-och användnings data som Configuration Manager samlar in
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3c46bdb2-5bda-47c8-b5f4-9365a4b3521c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9de63280786d620229c7d408f09ef2fe583e231d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720340"
---
# <a name="levels-of-diagnostic-usage-data"></a>Nivåer av diagnostikens användnings data

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager samlar in tre nivåer av diagnostik-och användnings data: **grundläggande**, **utökad**och **fullständig**. Standardnivån för den här funktionen är Utökad.

> [!IMPORTANT]
> Configuration Manager samlar inte in plats koder, plats namn, IP-adresser, användar namn, dator namn, fysiska adresser eller e-postadresser på nivåerna Basic eller Enhanced. En samling av den här informationen på nivån fullständig är inte ändamålsenlig. Den kan inkluderas i avancerad diagnostisk information som loggfiler eller minnes ögonblicks bilder. Microsoft använder inte den här informationen för att identifiera dig, kontakta dig eller utveckla annonser.

## <a name="levels"></a>Nivåer

### <a name="basic"></a>Basic

Nivån Basic innehåller data om hierarkin. Det krävs för att hjälpa till att förbättra installations-och uppgraderings upplevelsen. Med den här informationen kan du också avgöra vilka Configuration Manager uppdateringar som är tillämpliga för hierarkin.

### <a name="enhanced"></a>Optimerad

Den förbättrade nivån är standard när installationen är klar. Den här nivån omfattar data som samlas in på grundläggande nivå och funktions-/regionsspecifika data. Den visar frekvens och varaktighet för användning av olika funktioner. Den innehåller också Configuration Manager klient inställnings data: komponent namn, tillstånd och vissa inställningar som avsöknings intervall. Information om program uppdateringar är grundläggande vid användning av funktioner, det innehåller inte data om att uppdatera kompatibilitet på den här nivån.

Microsoft rekommenderar den här nivån eftersom den ger minsta möjliga data för att förbättra förbättringarna av produkter och tjänster.

Några exempel på data som den här nivån inte samlar in är:

- Namn på platser, användare, dator eller andra objekt

- Information om säkerhetsrelaterade objekt

- Sårbarheter som antalet system som kräver program uppdateringar

### <a name="full"></a>Fullständig

Den fullständiga nivån omfattar alla data i nivåerna Basic och Enhanced. Den innehåller också ytterligare information om Endpoint Protection, procentandel uppdateringskompatibilitet och information om programvaruuppdateringar. Den här nivån kan även innehålla avancerad diagnostikinformation, t. ex. systemfiler och ögonblicks bilder av minnet. Den här avancerade informationen kan innehålla personlig information som finns i minnet eller loggfiler vid hämtnings tillfället.

## <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Ändra nivån

Om du vill ändra data insamlings nivån måste du **ändra** behörigheter för **plats** objekt klassen.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .
1. Välj **Inställningar för hierarki** i menyfliksområdet.
1. Växla till fliken **diagnostik-och användnings data** och välj sedan data nivån.

## <a name="version-specific-details"></a><a name="bkmk_versions"></a>Versions information

Följande artiklar innehåller information om vilka data som Configuration Manager samlas in på varje nivå med varje version som stöds:

- [Diagnostik-och användnings data för 2002](levels-of-diagnostic-usage-data-collection-2002.md)
- [Diagnostik-och användnings data för 1910](levels-of-diagnostic-usage-data-collection-1910.md)
- [Diagnostik-och användnings data för 1906](levels-of-diagnostic-usage-data-collection-1906.md)
- [Diagnostik-och användnings data för 1902](levels-of-diagnostic-usage-data-collection-1902.md)
- [Diagnostik-och användnings data för 1810](levels-of-diagnostic-usage-data-collection-1810.md)

## <a name="next-steps"></a>Nästa steg

> [!div class="nextstepaction"]
> [Vanliga frågor och svar](frequently-asked-questions.md)
