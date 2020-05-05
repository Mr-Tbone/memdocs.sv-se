---
title: Filbaserad replikering
titleSuffix: Configuration Manager
description: Lär dig hur Configuration Manager använder filbaserad replikering för att överföra data mellan platser i hierarkin
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65fcc1a8-214e-4dd9-8093-de4cd4a00442
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b7d7f1564057a7a942fc4a32064eb54cdbfa890d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720172"
---
# <a name="file-based-replication"></a>Filbaserad replikering

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager använder filbaserad replikering för att överföra filbaserade data mellan platser i hierarkin. Dessa data omfattar program och paket som du vill distribuera till distributions platser på underordnade platser. Den hanterar också obearbetade identifierings data poster som platsen överför till dess överordnade plats och sedan processer.  

Vid filbaserad kommunikation mellan platser används SMB-protokollet ( *Server Message Block* ) på TCP/IP-port 445. Om du vill kontrol lera mängden data som platsen överför i nätverket anger du bandbredds begränsning och puls läge. Använd scheman för att styra när data ska skickas i nätverket.  

## <a name="routes"></a><a name="bkmk_routes"></a>Cirkulera

Följande information kan hjälpa dig att konfigurera och använda filreplikeringsflöde.  

### <a name="file-replication-route"></a>Filreplikeringsflöde

Varje filreplikeringsflöde identifierar en målplats som en plats överför filbaserade data till. Varje plats har stöd för ett filreplikeringsflöde till en angiven målplats.  

Om du vill hantera ett filreplikeringsflöde går du till arbets ytan **Administration** . Expandera noden **hierarki konfiguration** och välj sedan **filreplikering**.  

Du kan ändra följande inställningar för vägar för filreplikeringsflöde:  

#### <a name="file-replication-account"></a>Filreplikeringstjänsten

Det här kontot ansluter till mål platsen och skriver data till den platsens **SMS_SITE** -resurs. Den mottagande platsen bearbetar de data som skrivs till den här resursen. Som standard när du lägger till en plats i-hierarkin tilldelar Configuration Manager den nya plats serverns dator konto som konto för filreplikeringstjänsten. Den lägger sedan till det här kontot till mål platsens `SMS_SiteToSiteConnection_<sitecode>` grupp. Den här gruppen är lokal på den dator som beviljar åtkomst till SMS_Sites resursen. Du kan ändra kontot till ett Windows-användarkonto. Om du ändrar kontot ska du se till att lägga till det nya kontot i mål platsens `SMS_SiteToSiteConnection_<sitecode>` grupp.  

> [!NOTE]  
> Sekundära platser använder alltid datorkontot för den sekundära platsservern som **filreplikeringskonto**.  

#### <a name="schedule"></a>Schema

Ange schemat för varje filreplikeringsflöde. Den här åtgärden begränsar vilken typ av data och tid som data kan överföra till mål platsen.  

#### <a name="rate-limits"></a>Hastighets begränsningar

Ange hastighets begränsningar för varje filreplikeringsflöde. Den här åtgärden styr nätverks bandbredden som används av platsen vid överföring av data till mål platsen:  

- **Puls läge**: Ange storleken på de data block som platsen skickar till mål platsen. Du kan också ange en tidsfördröjning mellan varje datablock som skickas. Använd det här alternativet om du måste skicka data över en nätverks anslutning med låg bandbredd till mål platsen.

    Du har till exempel begränsningar för att skicka 1 KB data var femte sekund, men inte 1 KB var tredje sekund. Den här begränsningen gäller oavsett hastigheten på länken eller användningen vid en specifik tidpunkt.

- **Begränsad till högsta överförings hastighet per timme**: platsen skickar data till en målplats genom att bara använda den procent andel av tiden som du anger. Configuration Manager identifierar inte nätverkets tillgängliga bandbredd. Den delar upp den tid det kan skicka data till sektorer av tiden. Den skickar sedan data i ett kort tidsintervall, som följs av tids block när de inte skickar data.

    Till exempel ställer du in Max hastigheten på **50%**. Configuration Manager överför data under en viss tids period, följt av en lika lång tids period då inga data skickas. Den hanterar inte den faktiska storleken på det data block som skickas. Platsen hanterar bara den tid under vilken data skickas.  

    > [!CAUTION]  
    > Som standard kan en plats använda upp till tre **samtidiga sändningar** för att skicka data till en målplats. När du aktiverar hastighets begränsningar för ett filreplikeringsflöde begränsar det **samtidiga** sändningar till den platsen till en. Det här beteendet gäller även om den **tillgängliga bandbredden (%)** är inställd på **100%**. Om du till exempel använder standardinställningarna för avsändaren minskar överföringshastigheten till mål platsen till en tredjedel av standard kapaciteten.  

#### <a name="routes-between-secondary-sites"></a>Vägar mellan sekundära platser

Konfigurera ett filreplikeringsflöde mellan två sekundära platser för att dirigera filbaserat innehåll mellan dessa platser.  


### <a name="sender"></a>Avsändare

Varje plats har en avsändare. Avsändaren hanterar nätverks anslutningen från en plats till en målplats. Den kan upprätta anslutningar till flera platser samtidigt. För att ansluta till en plats använder avsändaren filreplikeringsflöde till platsen och identifierar det konto som används för att upprätta nätverks anslutningen. Avsändaren använder även det här kontot för att skriva data till mål platsens SMS_Site resurs.  

Som standard skriver avsändaren data till en målplats genom att använda flera **samtidiga**sändningar eller en *tråd*. Varje tråd kan överföra ett annat filbaserat objekt till mål platsen. När avsändaren börjar skicka ett objekt fortsätter den att skriva data block för objektet tills hela objektet skickas. När du har skickat alla data för objektet kan ett nytt objekt börja skickas till den tråden.  

Om du vill hantera avsändaren för en plats går du till arbets ytan **Administration** och expanderar noden **plats konfiguration** . Välj noden **platser** och välj sedan **Egenskaper** för den plats som du vill hantera. Växla till fliken **avsändare** för att ändra avsändarens inställningar.  

Du kan ändra följande inställningar för en avsändare:  

#### <a name="maximum-concurrent-sendings"></a>Maximalt antal samtidiga sändningar

Som standard använder varje plats fem samtidiga sändningar (trådar). Tre trådar är tillgängliga för användning när den skickar data till en mål plats. När du ökar det här antalet kan du öka data flödet mellan platser. Fler trådar innebär att Configuration Manager kan överföra fler filer samtidigt. Att öka det här antalet ökar även behovet av nätverksbandbredd mellan platserna.  

#### <a name="retry-settings"></a>Inställningar för nya försök

Som standard försöker varje plats med en problem anslutning två gånger, med en minuters fördröjning mellan anslutnings försöken. Du kan ändra antalet anslutnings försök som platsen gör, och hur lång tid det tar att vänta mellan försöken.  


## <a name="next-steps"></a>Nästa steg

[Databasreplikering](database-replication.md)
