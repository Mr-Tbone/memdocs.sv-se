---
title: Identifiera enhets-och användar resurser
titleSuffix: Configuration Manager
description: Läs en översikt över identifierings processen och identifierings data poster.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1869c9e6de455b7086a051db91bb26bc00a91a5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718373"
---
# <a name="run-discovery-for-configuration-manager"></a>Kör identifiering för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan använda en eller flera identifierings metoder i Configuration Manager för att hitta enhets-och användar resurser som du kan hantera. Du kan också använda identifiering för att identifiera nätverks infrastrukturen i din miljö. Det finns flera olika metoder som du kan använda för att identifiera olika saker, och varje metod har egna konfigurationer och begränsningar.  

## <a name="overview-of-discovery"></a>Översikt över identifiering  
 Identifiering är den process genom vilken Configuration Manager lära sig om de saker som du kan hantera. Tillgängliga identifieringsmetoder:  

-   Identifiering av Active Directory-skogar  

-   Identifiering av Active Directory-grupper  

-   Identifiering av Active Directory-system  

-   Identifiering av Active Directory-användare  

-   Identifiering av pulsslag  

-   Nätverksidentifiering  

-   Serveridentifiering  

> [!TIP]  
>  Du kan lära dig om de enskilda identifierings metoderna i [om identifierings metoder för Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  Information om hur du väljer vilka metoder som ska användas och på vilka platser i hierarkin finns i [Välj identifierings metoder som ska användas för Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Om du vill använda de flesta identifierings metoder måste du aktivera metoden på en plats och konfigurera den så att den söker efter vissa nätverks-eller Active Directory platser. När den körs frågar den angiven plats om information om enheter eller användare som Configuration Manager kan hantera. När en identifierings metod hittar information om en resurs, placerar den informationen i en fil som kallas DDR (Discovery data Record). Filen bearbetas sedan av en primär eller Central administrations plats. Vid bearbetningen av en DDR skapas en ny post i platsdatabasen för nyidentifierade resurser eller så uppdateras befintliga poster med den nya informationen.  

 Vissa identifierings metoder kan generera en stor mängd nätverks trafik, och det DDR som de producerar kan leda till en betydande användning av processor resurserna under bearbetningen. Planera därför att bara använda de identifierings metoder som du behöver för att uppfylla dina mål. Du kan börja med att använda bara en eller två identifieringsmetoder och sedan lägga till fler metoder om du behöver utöka identifieringsnivån i miljön.  

 När identifierings informationen har lagts till i plats databasen replikeras informationen till varje plats i hierarkin, oavsett var den identifierades eller bearbetades. Det innebär att du kan konfigurera olika scheman och inställningar för identifierings metoder på olika platser, men du kan köra en viss identifierings metod på bara en enda plats. Detta minskar användningen av nätverks bandbredd genom dubbla identifierings åtgärder och minskar bearbetningen av redundanta identifierings data på flera platser.  

 Du kan använda identifierings data för att skapa anpassade samlingar och frågor som logiskt grupperar resurser för hanterings uppgifter. Ett exempel:  

-   Push-överföra klient installationer eller uppgradera.  

-   Distribuera innehåll till användare eller enheter.  

-   Distribuera klient inställningar och relaterade konfigurationer.

##  <a name="about-discovery-data-records"></a><a name="BKMK_DDRs"></a>Om identifierings data poster  
 DDR är filer som skapas av en identifierings metod. De innehåller information om en resurs som du kan hantera i Configuration Manager, till exempel datorer, användare och i vissa fall nätverks infrastruktur. De behandlas på primära platser eller på centrala administrationsplatser. När resursinformationen i DDR anges i databasen, tas DDR bort och informationen replikeras som globala data till alla platser i hierarkin.  

 Vid vilken plats identifieringsdataposten behandlas beror på vilken information den innehåller:  

-   DDR för nyligen identifierade resurser som inte finns i databasen bearbetas på platsen på den översta nivån i hierarkin. Platsen på den högsta nivån skapar en ny resurs post i databasen och tilldelar den ett unikt ID. DDR-överföring via filbaserad replikering tills de når platsen på den högsta nivån.  

-   Identifieringsdataposter för tidigare identifierade objekt behandlas på primära platser. Underordnade primära platser överför inte identifieringsdataposter till den centrala administrationsplatsen när identifieringsdataposten innehåller information om en resurs som redan finns i databasen.  

-   Sekundära platser bearbetar inte DDR och överför dem alltid genom filbaserad replikering till sin överordnade primära plats.  

Identifieringsdatapostfiler går att känna igen på tillägget .ddr. De har normalt en storlek på c:a 1 kB.  

## <a name="get-started-with-discovery"></a>Kom igång med identifiering:  
 Innan du använder Configuration Manager-konsolen för att konfigurera identifiering bör du förstå skillnaderna mellan metoderna, vad de kan göra, och i vissa fall deras begränsningar.  

I följande avsnitt kan du skapa en grund som hjälper dig att använda identifierings metoder:  

-   [Om identifierings metoder för Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Välj identifierings metoder som ska användas för Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

När du förstår de metoder som du vill använda hittar du vägledning för att ställa in varje metod i [Konfigurera identifierings metoder för Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  
