---
title: Samlings utvärdering
titleSuffix: Configuration Manager
description: Lär dig mer om processen för samlings utvärdering, typer och utlösare. Förstå diagrammet och hierarkin för samlings utvärdering.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: af90154b848ddcd7cbff21917ef122ab10585098
ms.sourcegitcommit: 1d8bf691780b94a945e94945115d4d1df4242808
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663915"
---
# <a name="collection-evaluation-in-configuration-manager"></a>Samlings utvärdering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager använder *samlings utvärdering* för att uppdatera samlings medlemskap baserat på de samlings regler som du definierar. Omfattning och tids inställning för samlings utvärdering varierar beroende på plats-och samlings konfiguration och utvärderings typ. 

Det är viktigt att förstå beteendet för samlings utvärdering så att du kan fatta lämpliga beslut om samlings design. Information om vägledning och rekommendationer för samlings utvärdering finns i [metod tips för samlingar](best-practices-for-collections.md).

## <a name="evaluation-process"></a>Utvärderings process

[Colleval. log](https://docs.microsoft.com/mem/configmgr/core/plan-design/hierarchy/log-files#BKMK_ServerLogs) -posterna när samlings utvärderaren skapar, ändrar och tar bort samlingar.

Varje enskild samlings utvärdering och uppdatering följer dessa steg på hög nivå:

![Uppdaterings process för samling på hög nivå](media/high-level-collection-update-process.png)

1. Kör samlings frågan.
1. Lägg till alla system som är direkta medlemmar.
1. Utvärdera alla *Inkludera* samlingar.
   
   Om inkludera samlingar också har Frågeregler, eller om de ska innehålla eller utelämna samlingar, kan du även utvärdera dem. Om samlingarna ta med själva samlingarna är att begränsa samlingar, kan du utvärdera alla samlingar nedan. Returnera resultaten till den anropande samlingen när du har utvärderat trädet fullständigt.
   
1. Utför ett logiskt `AND` mellan de returnerade resultaten och den begränsande samlingen.
1. Utvärdera *exkluderings* samlingar.
   
   Om exkluderings samlingarna också har Frågeregler, eller om de har inkludera eller exkludera samlingar, kan du även utvärdera dem. Om dessa samlingar själva är begränsade till samlingar, kan du utvärdera alla samlingar nedan. Returnera resultaten till den anropande samlingen när du har utvärderat trädet fullständigt.
   
1. Jämför resultat uppsättningen från att utvärdera direkta medlemmar och inkludera samlingar med resultaten av utvärdering av exkluderings samlingar.
1. Skriv ändringarna i databasen och utför uppdateringar.
1. Utlös även alla beroende samlingar som ska uppdateras. Beroende samlingar är samlingar som är de aktuella samlings gränserna eller som refererar till den aktuella samlingen med hjälp av inkludera eller exkludera regler.

## <a name="collection-evaluation-types-and-triggers"></a>Samlings utvärderings typer och utlösare

De här typerna av trådar hanterar samlings utvärdering, beroende på utvärderings typ:

- **Primär** för schemalagda samlings uppdateringar
- **Hjälp** för att manuellt uppdatera samlingar med beroende samlingar
- **Enkel** att uppdatera samlingar utan beroende samlingar manuellt
- **Express** för uppdateringar av stegvis samling

I följande tabell beskrivs utlösare för samlings utvärdering och deras motsvarande utvärderings typer. 

| Utlösare | Utvärderings typ | Description |
|---------|-----------------|-------------|
|Manuell|Enkel eller extra|Manuell är den högsta prioriterings utvärderingen. När en administratör begär en manuell samlings utvärdering tilldelar samlings utvärderaren nästa tillgängliga utvärderings tråd till utvärderingen.|
|Schemalagd|Primär|Processen för schemalagd utvärdering är densamma som för manuell utvärdering, förutom att utvärderingen är tids driven i stället för händelse driven.|
|Mellanlagring|Enkel eller extra|Alla samlingar är direkt eller indirekt beroende av **alla system** eller **alla användare och användar grupper**. Båda dessa samlingar gör en fullständig samlings utvärdering vid 4:00 per dag. En ändring i någon av dessa samlingar utlöser uppdateringar av beroende samlingar baserat på ett [diagram med fullständig samling](#collection-evaluation-graph).
|Inkrementellt|Express|Stegvis utvärdering använder ett diagram för samlings utvärdering för att utvärdera och uppdatera beroende samlingar om en uppdatering av de stegvisa samlings medlemskapen ändras. Configuration Manager övervakar och uppdaterar resurs objekt i alla samlingar som är konfigurerade för stegvisa uppdateringar.<br /><br />Om en samlings fråga baseras på information som kommer att uppdateras senare, t. ex. maskin varu inventering, lägger Configuration Manager bara till eller tar bort resursen från samlingen under uppdateringen av den schemalagda samlingen.|

## <a name="collection-evaluation-graph"></a>Diagram över samlings utvärdering

Ett *diagram för samlings utvärdering* mappar alla samlingar som är relaterade till den samling som är avsedd för utvärdering. En samlings utvärdering omfattar mål samlingen och relaterade samlingar i utvärderings diagrammet för samlingar.

När samlings utvärderingen startar skapar Configuration Manager en graf som innehåller alla samlingar som kan behöva utvärderas till följd av ändringar i mål samlingen, med början från den högsta nivån i cykeln. Samlings utvärderaren går sedan igenom grafen i ordning och utvärderar varje samling medlemskap i tur och ordning. När samlingen är fullständigt utvärderad tar samlings utvärderaren bort samlingar på lägre nivå som inte påverkas av den här cykeln från diagrammet för samlings utvärdering.

Om en eller flera av de samlingar som utvärderas har en regel för inkludera eller exkludera, lägger samlings utvärderaren till den inkluderade eller exkluderade samlingen i grafen, tillsammans med alla samlingar som insamlings gränser. Om det finns några ändringar under utvärderingen av samlingarna include och exclude fortsätter grafen på den grenen innan den återgår till huvud grenen.

Configuration Manager skapar två typer av utvärderings diagram, *stegvisa* eller *fullständiga*.

### <a name="incremental-collection-evaluation"></a>Utvärdering av stegvis samling

När tabell data ändras infogar en SQL-utlösare en rad i **CollectionNotifications** -tabellen. Nästa gången en samlings utvärderings schema utlöses, är det `AND` resurs-ID: t med den befintliga samlings frågan och utlöser uppdateringar på samlingar som är aktiverade för *stegvisa* samlingar.

En stegvis samlings utvärdering kör en fråga per dator. Standard plats konfigurationen för utvärdering av stegvis samling är var femte minut.

Ett diagram över en stegvis samlings utvärdering mappar endast refererade samlingar om de är aktiverade för stegvis utvärdering. Om en stegvis utvärdering är begränsad till en samling som inte är aktive rad för stegvis utvärdering, utvärderar diagrammet samlingen baserat på det befintliga medlemskapet i den begränsande samlingen. 

Följande diagram visar till exempel nyligen identifierade resurser som är tillämpliga för alla samlingar. Samlings utvärderingen uppdaterar dock bara **alla-servrar** och **alla** domänkontrollanter-samlingar. Samlings utvärderaren utvärderar inte de andra samlingarna eftersom samlingen **alla medlems servrar** inte är aktive rad för stegvis utvärdering.

![Diagram exempel för utvärdering av stegvis samling](media/incremental-collection-evaluation-graph.png)

### <a name="full-collection-evaluation"></a>Fullständig samlings utvärdering

Utvärdering av manuella eller schemalagda insamlingar skapar ett diagram över *fullständig* samlings utvärdering av alla beroende samlingar. Diagrammet innehåller alla samlingar som refererar till samlingen som uppdateras och efterföljande samlingar. Configuration Manager fortsätter att utvärdera diagrammet så länge uppdateringar sker i samlingarna som bearbetas.

Följande diagram visar hur en schemalagd eller manuell samlings uppdaterings förfrågan för samlingen **alla servrar** skapar en fullständig graf som innehåller alla tillämpliga samlingar. De nya resurserna för DNS-servern och domänkontrollanten omfattas av medlemskaps frågorna för alla samlingar, så alla samlingar uppdateras.

![Diagram exempel för fullständig samlings utvärdering 1](media/full-collection-evaluation-graph-1.png)

En fullständig utvärdering utvärderar inte alltid alla samlingar. Diagrammet för samlings utvärdering fortsätter bara att utvärdera beroende samlingar om en uppdatering sker till den aktuella refererade samlingen. Om en stegvis uppdaterad samling uppdateras under schemalagda stegvisa utvärderingar kan det hända att referens samlingar som inte är aktiverade för stegvisa uppdateringar inte uppdateras. En fullständig utvärdering uppdaterar inte samlingen, avslutar samlings utvärderings grafen och eventuella utvärderings samlingar för den cykeln. 

I följande exempel gör installationen av DNS på den befintliga servern medlem i samlingen **DNS-servrar** , men eftersom det inte finns någon uppdatering av den begränsade samlingen av **alla medlems servrar** , utvärderas inte den fullständiga utvärderingen av samlingen med **DNS-servrar** . Nästa stegvisa utvärderings cykel kommer att utvärdera samlingen med **DNS-servrar** , eftersom det är en stegvis samling.

![Diagram exempel för fullständig samlings utvärdering 2](media/full-collection-evaluation-graph-2.png)

## <a name="next-steps"></a>Nästa steg
- [Skapa samlingar](create-collections.md)
- [Metodtips för samlingar](best-practices-for-collections.md)
- [Visningsprogrammet för mängdutvärdering](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer)
- [ConfigMgrDogs Felsök ConfigMgr 2012](https://channel9.msdn.com/Events/TechEd/Australia/2014/DCI411) -sessionen i TechEd Australien
