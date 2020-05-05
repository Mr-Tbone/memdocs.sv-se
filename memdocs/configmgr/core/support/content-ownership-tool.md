---
title: Innehållsägarskapsverktyget
titleSuffix: Configuration Manager
description: Använd verktyget för innehålls ägarskap för att ändra ägarskap för överblivna paket i Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1a24a93bb71178af3a4cfbba2a406bdd958d19
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723392"
---
# <a name="content-ownership-tool"></a>Innehållsägarskapsverktyget

*Gäller för: Configuration Manager (aktuell gren)*

Verktyget för innehålls ägarskap är ett av de [Configuration Manager verktygen](tools.md). Den ändrar ägarskap för överblivna paket i Configuration Manager. Överblivna paket har ingen ägande plats Server. Paket kan bli överblivna genom att plats servern tas bort medan den fortfarande ägs av den här plats servern.

Kör verktyget för innehålls ägarskap på alla plats servrar i Configuration Manager hierarkin. Logga in som en administrativ användare med tillräckliga paket behörigheter.  

> [!Tip]  
> Använd **ContentLibraryCleanup. exe** i `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` om du vill *ta bort* överblivna innehåll från en distributions plats. Mer information finns i [rensnings verktyget för innehålls bibliotek](../plan-design/hierarchy/content-library-cleanup-tool.md).  



## <a name="features"></a>Funktioner

- Visa alla överblivna paket  

- Visa alla paket, även om de inte är överblivna  

- Visa status för anslutningen till en plats  

- Filtrera paket efter namn, platskod eller pakettyp  

- Sortera efter valfri kolumn som visas  

- Ändra tilldelningen av ett eller flera paket med en enda åtgärd  

- Visa förloppet för aktiviteten för ägarskaps överföring  



## <a name="usage"></a>Användning

Kör **ContentOwnershipTool. exe** för att starta verktyget. Lokal administratörs behörighet på datorn krävs inte för att köra verktyget.

Det finns inga kommando rads parametrar.

> [!Important]   
> Det här verktyget ändrar ägarskapet för ett överblivna paket. Själva paketet flyttas inte från den distributions plats som den lagras på. Den här ägarskaps ändringen innebär inte att paketet uppdateras på distributions platser. Det gör också att klienterna inte kan utvärdera om principen för distribution av paketet. När ägarskapet ändras kontrollerar du att den nya plats servern har åtkomst till källfilerna. Det måste ha minst **Läs** behörighet till källfilerna för varje paket. 



## <a name="see-also"></a>Se även

- [Grundläggande begrepp för innehållshantering](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Innehållsbibliotek](../plan-design/hierarchy/the-content-library.md)
