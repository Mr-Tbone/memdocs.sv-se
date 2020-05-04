---
title: DP jobbköhanteraren
titleSuffix: Configuration Manager
description: Använd tjänsten DP job queue Manager för att felsöka och hantera innehålls distributions jobb för att Configuration Manager distributions platser.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9f6269d559bbcb192b1189419a8450a860d70058
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713662"
---
# <a name="dp-job-queue-manager"></a>DP jobbköhanteraren

*Gäller för: Configuration Manager (aktuell gren)*

Jobb Queue Manager för distributions platsen (DP) är ett av de [Configuration Manager verktygen](tools.md). Använd den för att felsöka och hantera pågående innehålls distributions jobb till Configuration Manager distributions platser. 

Verktyget visar en lista över jobb som Package Transfer Manager-komponenten har i kön. Den visar också status för jobben: redo att köras, köras eller försöker igen. Med den kan du manipulera jobben i kön, flytta jobb högre upp i listan, avbryta ett jobb eller manuellt starta ett jobb.

Den hämtar också information från den plats Server på vilken distributions platsen kör ett jobb. Verktyget ansluter via providern till plats servern. Den ansluter inte till varje fjärrdistributions plats för att samla in den här informationen. Eftersom den utlöser åtgärder och hämtar information via providern, finns det en fördröjning i att avspegla ändringar från fjärrdistributions platser.



## <a name="usage"></a>Användning

Kör **DPJobMgr. exe**. Verktygets huvud meny innehåller följande flikar: 

- [Anslut](#bkmk_connect): etablera den första anslutningen till den primära plats servern  

- [Översikt](#bkmk_overview): sammanfattar alla jobb som körs på alla distributions platser i en enda vy  

- [Distributions plats information](#bkmk_dp-info): flera-Välj distributions platser för att spåra dem och hantera ett enda jobb av intresse  

- [Hantera jobb](#bkmk_manage-jobs): visar en lista över alla jobb och deras status i en platt vy. Ändra jobb, flytta dem, avbryta eller starta manuellt.  


### <a name="connect-tab"></a><a name="bkmk_connect"></a>Fliken Anslut

Använd den här fliken för att upprätta den första anslutningen till den primära plats servern. Den använder den för tillfället inloggade användarens autentiseringsuppgifter. Det går inte att ansluta till den centrala administrations platsen eller sekundära platser. Anslutningen kräver säkerhets rollen **Fullständig administratör** .

När verktyget har upprättat en anslutning, bekräftar ett meddelande längst ned i verktyget att det är anslutet till plats servern. 


### <a name="overview-tab"></a><a name="bkmk_overview"></a>Fliken Översikt

Visar en översikt över alla jobb på alla distributions platser. Se följande kolumner:  

- **Distributions plats**: visar namnen på distributions platserna  

- **Jobb som körs**: visar antalet samtidiga jobb som körs på en viss distributions plats.  

    > [!Tip]  
    > Antalet samtidiga program varu distributioner är en plats inställning. Ändrade den här inställningen i komponent egenskaperna för program varu distribution.  

- **Totalt antal jobb**: visar antalet jobb som är riktade till en viss distributions plats. Det här antalet inkluderar jobb som kör, försöker igen eller väntar på att köras.  

- **Totalt antal återförsök**: visar antalet gånger som jobb har återtestats på en viss distributions plats. En högre siffra kan representera ett allmänt problem med den specifika distributions platsen.  


> [!Tip]  
> - Om du vill sortera varje kolumn på den här fliken klickar du på kolumn namnet  
> 
> - Uppdatera informationen manuellt på den här fliken genom att klicka på **Uppdatera**  
> 
> - Uppdatera informationen i den här fliken automatiskt genom att klicka på **Starta automatisk uppdatering** och ange intervall för automatisk uppdatering. Standard intervallet för uppdatering är två minuter.  


### <a name="distribution-point-info-tab"></a><a name="bkmk_dp-info"></a>Fliken information om distributions plats

Visar en lista över alla distributions platser under den anslutna platsen. I rutan till vänster visas alla distributions platser. Klicka på **Markera alla** eller **avmarkera allt** vid behov, eller Välj flera angivna distributions platser i den här listan. I rutan till höger visas jobben för de valda distributions platserna.

Det finns åtta kolumner:  

- **Status ikon**: det finns tre möjliga status ikoner:  

    - **Klar**: indikerar att ett visst jobb har slutfört alla verifierings steg. Den är redo att läggas till i körningen av samtidiga jobb. Jobb i det här tillståndet är vanligt vis i en väntande fas. De väntar på att den aktuella processen som körs ska avslutas för att öppna upp ett utrymme för dem.  

    - **Körs**: visar att ett visst jobb för närvarande körs på en distributions plats. För långvariga jobb (stora paket) finns det vanligt vis tid att hämta förloppet (%) till slut för ande. Den visar procent andelen i kolumnen **Progress** i den här vyn. För små paket kan **förlopps** kolumnen vara tom. Jobbet kanske redan har slutförts vid den tid det tar emot status från den fjärranslutna distributions platsen.  

    - **Försök igen**: indikerar att ett visst jobb har misslyckats och nu är i ett återförsöks läge. Ett nytt försök har gjorts för det här jobbet efter återförsöksintervall. Intervallet kan konfigureras och anges till 30 minuter som standard.  

- **Program vara**: namnet på det paket som är mål för en viss distributions plats  

- **Paket-ID**: paket-ID för det paket som är mål för en viss distributions plats  

- **Storlek**: paketets storlek i KB  

- **Förlopp**: jobb slut för ande procent. Mer information finns i beskrivningen **körnings** status ikon.  

- **Tid för start/omstart**: det här värdet är start tiden för ett jobb som körs (grönt). För ett återförsöks jobb är det här värdet den tid då ett nytt försök görs i jobbet.  

- **Återförsök**: antal gånger som det här paketet har provats om.  

- **Distributions platsens namn**: det fullständigt kvalificerade domän namnet (FQDN) för distributions platsen  

> [!Tip]  
> - Om du vill sortera varje kolumn på den här fliken klickar du på kolumn namnet  
> 
> - Uppdatera informationen manuellt på den här fliken genom att klicka på **Uppdatera**  
> 
> - Uppdatera informationen i den här fliken automatiskt genom att klicka på **Starta automatisk uppdatering** och ange intervall för automatisk uppdatering. Standard intervallet för uppdatering är två minuter.  
> 
> - Om du behöver ändra ett visst jobb högerklickar du på jobbet i den här vyn och väljer **Hantera jobb**. Den här åtgärden öppnar [fliken Hantera jobb](#bkmk_manage-jobs).  


### <a name="manage-jobs-tab"></a><a name="bkmk_manage-jobs"></a>Fliken Hantera jobb

Visar en lista över alla jobb och deras status i en platt vy. Den innehåller samma åtta kolumner som [fliken information om distributions plats](#bkmk_dp-info). I den här vyn högerklickar du på jobben för följande åtgärder:  

- **Kör**: startar ett jobb som är i något annat tillstånd än att köra  

- **Flytta högst upp**: flyttar ett eller flera jobb överst i kön. Den här åtgärden kan leda till att jobben körs omedelbart. Ett jobb med lägre prioritet kan pausas på grund av den här åtgärden.  

- **Flytta upp**: flyttar ett visst jobb en rad ovanför. Ett jobb med lägre prioritet kan pausas på grund av den här åtgärden.  

- **Flytta ned**: flyttar ett visst jobb en rad nedan.  

- **Flytta längst ned**: flyttar ett eller flera jobb längst ned i kön.  

    > [!Tip]  
    > Dra och släpp jobb i listan för att flytta dem.  

- **Avbryt**: försöker avbryta ett eller flera jobb.  

    > [!Note]  
    > Du kan inte avbryta jobb nära slut för ande tiden. Om plats servern också är en distributions plats kan du inte avbryta jobb på plats servern.  



## <a name="see-also"></a>Se även

- [Grundläggande begrepp för innehållshantering](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Package Transfer Manager](../plan-design/hierarchy/package-transfer-manager.md)
