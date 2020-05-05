---
title: Package Transfer Manager
titleSuffix: Configuration Manager
description: Förstå hur Package Transfer Manager i Configuration Manager överför innehåll från en plats Server till fjärrdistributions platser.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b450c45342793b89d41a2d96b8a7340939899093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722454"
---
# <a name="package-transfer-manager-in-configuration-manager"></a>Package Transfer Manager i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

På en Configuration Manager plats är paket överförings hanteraren en komponent i den SMS_Executive tjänst som hanterar överföringen av innehåll från en plats serverdator till fjärrdistributions platser på en plats. (En fjärrdistributions plats är en plats som inte finns på plats serverdatorn.) Paket överförings hanteraren har inte stöd för konfigurationer av administratören, men förståelse för hur den fungerar kan hjälpa dig att planera din infrastruktur för innehålls hantering. Det kan också hjälpa dig att lösa problem med innehålls distribution.


När du distribuerar innehåll till en eller flera fjärranslutna distributions platser på en plats, skapar **distributions hanteraren** ett innehålls överförings jobb. Den meddelar sedan paket överförings hanteraren på primära och sekundära plats servrar att överföra innehållet till distributions platserna.

 Package Transfer Manager loggar sina åtgärder i filen **pkgxfermgr. log** på plats servern. Logg filen är den enda plats där du kan visa aktiviteter för Package Transfer Manager.  

> [!NOTE]  
>  I tidigare versioner av Configuration Manager hanterar distributions hanteraren överföringen av innehåll till en annan distributions plats. Distribution Manager hanterar även överföring av innehåll mellan platser. Med Configuration Manager fortsätter distributions hanteraren att hantera överföringen av innehåll mellan två platser. Paket överförings hanteraren hanterar dock nu överföringen av innehåll till ett stort antal distributions platser. Detta hjälper till att öka den övergripande prestandan för innehålls distribution mellan platser och distributions platser inom en plats.  

För att överföra innehåll till en standard distributions plats fungerar Package Transfer Manager på samma sätt som distributions hanteraren fungerar i tidigare versioner av Configuration Manager. Det innebär att den aktivt hanterar överföringen av filer till varje distributions plats. Men för att distribuera innehåll till en mottagar distributions plats meddelar Package Transfer Manager den mottagar distributions plats som innehållet är tillgängligt. Mottagar distributions platsen tar sedan över överförings processen.  

Följande information beskriver hur Package Transfer Manager hanterar överföringen av innehåll till standard distributions platser och till distributions platser som är konfigurerade som mottagar distributions platser:
1.  **Admin distribuerar innehåll till en eller flera distributions platser på en plats.**  

    -   **Standard distributions plats:** Distribution Manager skapar ett innehålls överförings jobb för innehållet.  

    -   **Mottagar distributions plats:** Distribution Manager skapar ett innehålls överförings jobb för innehållet.  

2.  **Distribution Manager kör preliminära kontroller.**  

    -   **Standard distributions plats:** Distribution Manager kör en grundläggande kontroll för att bekräfta att varje distributions plats är redo att ta emot innehållet. Efter den här kontrollen meddelar distributions hanteraren paket överförings hanteraren att starta överföringen av innehållet till distributions platsen.  

    -   **Mottagar distributions plats:** Distribution Manager startar Package Transfer Manager, som sedan meddelar mottagar distributions platsen att det finns ett nytt innehålls överförings jobb. Distribution Manager kontrollerar inte statusen för de fjärranslutna distributions platser som är mottagar distributions platser, eftersom varje mottagar distributions plats hanterar sina egna innehålls överföringar.  

3.  **Package Transfer Manager förbereder överföring av innehåll.**  

    -   **Standard distributions plats:** Package Transfer Manager undersöker innehålls lagringen för den enskilda instansen för varje angiven fjärrdistributions plats. Syftet med detta är att identifiera filer som redan finns på distributions platsen. Sedan, paketera överförings hanterarens köer bara för överföring av de filer som inte redan finns.  

        > [!NOTE]  
        >  Om du vill kopiera varje fil i distributionen till distributions platsen, även om filerna redan finns i det enskilda instans lagret på distributions platsen, använder du åtgärden **distribuera** om innehåll.  

    -   **Mottagar distributions plats:** För varje mottagar distributions plats i distributionen kontrollerar Package Transfer Manager mottagar distributions platserna käll distributions platser för att bekräfta om innehållet är tillgängligt.  

        -   När innehållet är tillgängligt på minst en käll distributions plats skickar Package Transfer Manager ett meddelande till den mottagar distributions platsen. Meddelandet dirigerar den distributions platsen för att påbörja överföringen av innehållet. Meddelandet innehåller fil namn och storlek, attribut och hash-värden.  

        -   När innehållet inte är tillgängligt än, skickar Package Transfer Manager inget meddelande till distributions platsen. I stället upprepas kontrollen var 20: e minut tills innehållet är tillgängligt. När innehållet är tillgängligt skickar Package Transfer Manager meddelandet till den mottagar distributions platsen.  

        > [!NOTE]  
        >  För att mottagar distributions platsen ska kopiera varje fil i distributionen till distributions platsen, även om filerna redan finns i det enskilda instans lagret på mottagar distributions platsen, använder du åtgärden **distribuera** om innehåll.  

4.  **Innehållet börjar överföras.**  

    -   **Standard distributions plats:** Package Transfer Manager kopierar filer till varje distributions plats. Under överföringen till en standard distributions plats:  

        -   Som standard kan Package Transfer Manager samtidigt bearbeta tre unika paket och distribuera dem till fem distributions platser parallellt. Gemensamt kallas dessa för **samtidiga distributions inställningar**. Om du vill konfigurera en samtidig distribution går du till fliken **Allmänt** i **komponent egenskaperna för program varu distribution** för varje plats.  

        -   Package Transfer Manager använder schemaläggning och konfigurationer av nätverks bandbredd för varje distributions plats vid överföring av innehåll till den distributions platsen. Om du vill konfigurera dessa inställningar går du till flikarna **schema** och **hastighets begränsningar** i **egenskaperna** för varje distributions plats. Mer information finns i [Hantera innehåll och innehålls infrastruktur för Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Mottagar distributions plats:** När en mottagar distributions plats tar emot en meddelande fil, påbörjar distributions platsen processen för att överföra innehållet. Överförings processen körs oberoende på varje mottagar distributions plats:  

        1.   Mottagar distributionen identifierar filerna i innehålls distributionen som den inte redan har i sin instans lager och förbereder för att ladda ned innehållet från en av käll distributions platserna.  

        2.   Sedan kontrollerar mottagar distributions platsen med var och en av sina käll distributions platser, i ordning, tills den hittar en käll distributions plats som har tillgängligt innehåll. När mottagar distributions platsen identifierar en käll distributions plats med innehållet börjar hämtningen av innehållet.  

        > [!NOTE]  
        >  Processen för att ladda ned innehåll från mottagar distributions platsen är samma som den som används av Configuration Manager-klienter. För överföring av innehåll av mottagar distributions platsen används inte samtidiga överförings inställningar. Schemaläggnings-och begränsnings alternativ som du konfigurerar för standard distributions platser används inte heller.  

5.  **Innehålls överföringen har slutförts.**  

    -   **Standard distributions plats:** När paket överförings hanteraren har överfört filer till varje angiven fjärrdistributions plats, verifierar den hashen för innehållet på distributions platsen. Sedan meddelar den distributions hanteraren att distributionen är klar.  

    -   **Mottagar distributions plats:** När mottagar distributions platsen slutfört innehålls hämtningen verifierar distributions platsen hash-värdet för innehållet. Sedan skickar den ett status meddelande till plats hanterings platsen för att indikera att det lyckas. Om den här statusen inte tas emot efter 60 minuter, aktive ras paket överförings hanteraren igen. Den kontrollerar om mottagar distributions platsen ska bekräfta om mottagar distributions platsen har hämtat innehållet. Om innehålls hämtningen pågår laddas paket överförings hanteraren i vilo läge i ytterligare 60 minuter innan den kontrollerar mottagar distributions platsen igen. Den här cykeln fortsätter tills pull-distributionsplatsen har hämtat innehållet.  
