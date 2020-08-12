---
title: Hantera nätverks bandbredd för innehåll
titleSuffix: Configuration Manager
description: Konfigurera schemaläggning, begränsning och förinstallerat innehåll för Configuration Manager.
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df3188e827623db8faa0b27be2fe282031e9fa50
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126400"
---
# <a name="manage-network-bandwidth-for-content"></a>Hantera nätverks bandbredd för innehåll
Du kan använda inbyggda kontroller för schemaläggning och begränsning för att hjälpa dig att hantera nätverks bandbredd som används för innehålls hanterings processen för Configuration Manager. Du kan också använda förinstallerat innehåll. I följande avsnitt beskrivs dessa alternativ mer utförligt.

##  <a name="scheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>Schemaläggning och begränsning  

 När du skapar ett paket, ändrar käll Sök vägen för innehållet eller uppdaterar innehållet på distributions platsen kopieras filerna från käll Sök vägen till innehålls biblioteket på plats servern. Sedan kopieras innehållet från innehålls biblioteket på plats servern till innehålls biblioteket på distributions platserna. När källfiler för innehållet uppdateras och källfilerna redan har distribuerats, hämtar Configuration Manager bara de nya eller uppdaterade filerna och skickar dem sedan till distributions platsen.

 Du kan använda schemaläggnings-och begränsnings kontroller för plats-till-plats-kommunikation och för kommunikation mellan en plats Server och en fjärrdistributions plats. Om nätverks bandbredden är begränsad även efter att du ställt in schemaläggnings-och begränsnings kontrollerna kan du överväga att förinstallera innehållet på distributions platsen.  

 I Configuration Manager kan du ställa in ett schema och ange begränsnings inställningar på de fjärranslutna distributions platser som avgör när och hur innehålls distribution utförs. Varje fjärrdistributions plats kan ha olika konfigurationer som hjälper dig att hantera begränsningar för nätverks bandbredd från plats servern till den fjärranslutna distributions platsen. Kontrollerna för schemaläggning och begränsning till den fjärranslutna distributions platsen liknar inställningarna för en standard avsändar adress. I det här fallet används inställningarna av en ny komponent som kallas Package Transfer Manager.

 Package Transfer Manager distribuerar innehåll från en plats Server, som en primär plats eller sekundär plats, till en distributions plats som är installerad på ett plats system. Inställningarna för begränsning anges på fliken **hastighets begränsningar** och schemaläggnings inställningarna anges på fliken **schema** för en distributions plats som inte finns på en plats Server. Tids inställningarna baseras på tids zonen från den sändande platsen, inte på distributions platsen.  

> [!IMPORTANT]  
>  Flikarna **hastighets gränser** och **schema** visas endast i egenskaperna för distributions platser som inte är installerade på en plats Server.  

Mer information finns i [Installera och konfigurera distributions platser för Configuration Manager](../../servers/deploy/configure/install-and-configure-distribution-points.md).  

##  <a name="prestaged-content"></a><a name="BKMK_PrestagingContent"></a>Förinstallerat innehåll  
 Du kan förinstallera innehåll för att lägga till innehållsfilerna i innehålls biblioteket på en plats Server eller distributions plats innan du distribuerar innehållet. Eftersom innehållsfilerna redan finns i innehålls biblioteket överförs de inte över nätverket när du distribuerar innehållet. Du kan förinstallera innehållsfiler för program och paket.  

I Configuration Manager-konsolen väljer du det innehåll som du vill förinstallera och använder sedan **guiden Skapa förinstallerad innehålls fil**. Detta skapar en komprimerad, förinstallerad innehålls fil som innehåller filerna och associerade metadata för innehållet. Sedan kan du manuellt importera innehållet på en plats Server eller distributions plats. Observera följande punkter:  

-   När du importerar den förinstallerade innehålls filen på en plats server läggs innehållsfilerna till i innehålls biblioteket på plats servern och registreras sedan i plats Server databasen.  

-   När du importerar den förinstallerade innehålls filen på en distributions plats läggs innehållsfilerna till i innehålls biblioteket på distributions platsen. Ett status meddelande skickas till plats servern som informerar webbplatsen om att innehållet är tillgängligt på distributions platsen.  

Du kan också konfigurera distributions platsen som **förinstallerad** för att under lätta hanteringen av innehålls distribution. När du sedan distribuerar innehåll kan du välja om du vill:  

-   Förinstallera alltid innehållet på distributions platsen.  

-   Förinstallera det ursprungliga innehållet för paketet och Använd sedan standard processen för innehålls distribution när det finns uppdateringar av innehållet.  

-   Använd alltid standard innehålls distributions processen för innehållet i paketet.  

###  <a name="determine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>Ta reda på om du ska förinstallera innehåll  
 Överväg att förinstallera innehåll för program och paket i följande scenarier:  

-   **För att åtgärda problemet med begränsad nätverks bandbredd från plats servern till en distributions plats.** Om schemaläggning och begränsning inte räcker för att uppfylla dina problem om bandbredd, bör du överväga att förinstallera innehållet på distributions platsen. Varje distributions plats har inställningen **Aktivera distributions platsen för förinstallerat innehåll** som du kan välja i egenskaperna för distributions platsen. När du aktiverar det här alternativet identifieras distributions platsen som en förinstallerad distributions plats, och du kan välja hur du vill hantera innehållet för en per paket-basis.  

    Följande inställningar är tillgängliga i egenskaperna för ett program, paket, driv rutins paket, start avbildning, installations program för operativ system och avbildning. Med de här inställningarna kan du välja hur innehålls distribution hanteras på fjärranslutna distributions platser som identifieras som förinstallerade:  

    -   **Hämta innehåll automatiskt när paket tilldelas distributions platser**: Använd det här alternativet om du har mindre paket och inställningarna för schemaläggning och begränsning ger tillräckligt med kontroll för innehålls distribution.  

    -   **Hämta endast innehålls ändringar till distributions platsen**: Använd det här alternativet om du förväntar dig att framtida uppdateringar av innehållet i paketet ska vara allmänt mindre än det ursprungliga paketet. Du kan till exempel förinstallera ett program som Microsoft 365 appar, eftersom den ursprungliga paket storleken är över 700 MB och är för stor för att skickas över nätverket. Innehålls uppdateringar av det här paketet kan dock vara mindre än 10 MB och kan användas för att distribuera över nätverket. Ett annat exempel kan vara driv rutins paket, där den ursprungliga paket storleken är stor, men stegvisa driv rutins tillägg till paketet kan vara små.  

    -   **Kopiera innehållet i det här paketet manuellt till distributions platsen**: Använd det här alternativet när du har stora paket, med innehåll, till exempel ett operativ system, och du aldrig vill använda nätverket för att distribuera innehållet till distributions platsen. När du väljer det här alternativet måste du förinstallera innehållet på distributions platsen.  

    > [!IMPORTANT]  
    >  Föregående alternativ gäller för varje paket och används bara när en distributions plats identifieras som förinstallerad. Distributions platser som inte har identifierats som förinstallerade ignorerar de här inställningarna. I det här fallet distribueras alltid innehållet över nätverket från plats servern till distributions platserna.  

-   **För att återställa innehålls biblioteket på en plats Server.** När en plats server kraschar återställs information om paket och program som finns i innehålls biblioteket till plats databasen som en del av återställnings processen, men innehålls biblioteks filen återställs inte som en del av processen. Om du inte har en fil system säkerhets kopia för att återställa innehålls biblioteket kan du skapa en förinstallerad innehålls fil från en annan plats som innehåller de paket och program som du måste ha. Sedan kan du extrahera den förinstallerade innehålls filen på den återställda plats servern. Mer information om säkerhets kopiering och återställning av plats servrar finns i [säkerhets kopiering och återställning för Configuration Manager](../../servers/manage/backup-and-recovery.md).  
