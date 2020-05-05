---
title: Hantera publikationer
titleSuffix: Configuration Manager
description: Hantera grupper av program uppdateringar som en publikation med System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0b79e0ec67fa7c1d7ede0af1549c8cda4dd3ee3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717708"
---
# <a name="manage-publications-in-updates-publisher"></a>Hantera publikationer i Updates Publisher

*Gäller för: System Center Updates Publisher*

Du kan använda publikationer för att hantera grupper med uppdateringar och paket som ett enda objekt. Detta inkluderar att publicera uppdateringarna till en hanterings Server och exportera publikationen som en grupp för användning med en annan installation av Updates Publisher.

## <a name="create-publications"></a>Skapa publikationer
Publikationer skapas på två sätt:

-   När du hanterar uppdateringar och paket i **arbets ytan uppdateringar**kan du [tilldela](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication) dem till en ny publikation som skapas vid den tidpunkten.

-   På **arbets ytan publikationer** kan du använda knappen **skapa** på fliken **publikation** i menyfliksområdet. Med den här metoden kan du skapa en publikation för framtida bruk. När du senare tilldelar uppdateringar kan du använda den här publikationen.

## <a name="rename-a-publication"></a>Byta namn på en publikation
Om du vill byta namn på en publikation väljer du publikationen inifrån **arbets ytan publikationer**och väljer sedan **Redigera**på fliken **publikation** i menyfliksområdet.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Ändra publikationens typ av uppdateringar i en publikation
Du kan ändra **publikationens typ** av uppdateringar och paket som är kopplade till en publikation från **arbets ytan publicera**.

1. Välj den publikation som innehåller de uppdateringar som du vill ändra och välj sedan en eller flera uppdateringar eller paket från listan **alla &lt;publicerings namn> medlems uppdatering** .

2. Välj sedan något av följande alternativ på fliken **Start** . Vilka alternativ som är tillgängliga beror på publikationens typ av de uppdateringar som du har valt.

   -   **Automatisk**
   -   **Fullständigt innehåll**
   -   **Endast metadata**

När du har gjort en ändring kan du behöva uppdatera vyn publikation för att se de nya värdena.

Information om olika typer av publikationer finns i [tilldela uppdateringar och paket till en publikation](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication).

> [!TIP]    
> När du anger publikationens typ av paket publiceras alla program uppdateringar i paketet med publikationens Publikationstyp.

## <a name="remove-updates-from-a-publication"></a>Ta bort uppdateringar från en publikation
Om du vill ta bort uppdateringar eller paket från en publikation väljer du den publikation som du vill ändra i **arbets ytan publikationer** och väljer sedan de uppdateringar och paket som du vill ta bort. Gå sedan till fliken **Start** i menyfliksområdet och välj **ta bort**.

När uppdateringarna har tagits bort från en publikation finns de kvar i Updates Publisher-lagringsplatsen.

## <a name="publish-publications"></a>Publicera publikationer
När du publicerar uppdateringar och paket lägger uppdaterings utgivare till information om dessa uppdateringar och paket (metadata) och eventuellt binärfiler för uppdateringarna (fullständigt innehåll) till en uppdaterings Server för distribution till enheter.

Innan du kan publicera måste du konfigurera alternativet [uppdaterings Server](updates-publisher-options.md#update-server) för Updates Publisher. För att öppna det här konfigurations alternativet går du till **Översikt över** **uppdateringar arbets yta** &gt; och väljer **Konfigurera WSUS och signerings certifikat.** Du kan också gå till sidan uppdaterings server i Updates Publisher-alternativ.

> [!NOTE]   
> Updates Publisher kan bara publicera uppdateringar som är 375 megabyte (MB) eller mindre i storlek.

### <a name="to-publish-a-publication"></a>Publicera en publikation

1. Gå till **arbets ytan publikationer**och välj sedan en publikation som innehåller den grupp med uppdateringar och paket som du vill publicera eller exportera. Välj sedan **publicera** från fliken **Start** i menyfliksområdet.

2. På sidan **Välj** i **publicerings** guiden kan du välja att signera alla uppdateringar med ett nytt publicerings certifikat, men du kan inte ändra publikationens typ.

3. Slutför guiden.

   Om publiceringen Miss lyckas visas en länk till filen UpdatesPublisher. log som kan innehålla mer information.

## <a name="export-a-publication"></a>Exportera en publikation
Du kan exportera en publikation från din Updates Publisher-lagringsplats. Då exporteras uppdateringarna och paketen som har tilldelats publikationen och en uppdaterings katalog skapas. Du kan sedan [lägga till](updates-publisher-catalogs.md#add-software-update-catalogs) och [Importera](updates-publisher-catalogs.md#import-updates) katalogen till en annan instans av Updates Publisher. Du kan också [Exportera uppdateringar](manage-updates-with-updates-publisher.md#export-updates) som inte ingår i en publikation.

Om du vill exportera en publikation går du till **arbets ytan publikationer** och väljer publikationen som innehåller uppdateringar som du vill exportera. Du kan bara välja en publikation i taget.

Med publikationen markerad väljer du **Exportera** från fliken **Start** i menyfliksområdet och anger sedan en sökväg och ett fil namn för katalog exporten.

Du har också möjlighet att exportera (inkludera) beroende program uppdateringar som en del av exporten.

## <a name="rename-a-publication"></a>Byta namn på en publikation
Om du vill byta namn på en publikation väljer du publikationen i **arbets ytan publikationer**och väljer sedan **Redigera** på fliken **publikation** i menyfliksområdet.

## <a name="delete-a-publication"></a>Ta bort en publikation
Om du vill ta bort en publikation väljer du publikationen i **arbets ytan publikationer**och väljer sedan **ta bort** på fliken **publikation** i menyfliksområdet.

När publikationen har tagits bort från Updates Publisher förblir de uppdateringar som fanns i publikationen tillgängliga i publicerings platsen för uppdateringar.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Förfaller eller återaktivera uppdateringar och paket
Du kan använda **arbets ytan uppdateringar** för att välja och sedan gå ut eller återaktivera uppdateringar och paket. Du kan gå ut och återaktivera uppdateringar och paket så många gånger du väljer.

-   **Om du vill upphöra med uppdateringar eller paket**i arbets ytan uppdateringar väljer du en eller flera uppdateringar eller paket som inte har upphört att gälla, och väljer sedan **förfaller** från fliken **Start** . Innan du publicerar uppdateringen eller paketet som förfallit till Configuration Manager, kan du återaktivera den.

    Innan du kan ta bort (ta bort) en anpassad uppdatering eller paket från Configuration Manager måste du gå ut den och sedan publicera den förfallna statusen till Configuration Manager. När uppdateringar eller paket har gått ut i Configuration Manager kan du inte längre distribuera eller återaktivera uppdateringen eller paketet.

-   **Om du vill återaktivera uppdateringar eller paket**på arbets ytan uppdateringar väljer du en eller flera uppdateringar som har upphört att gälla och väljer sedan **återaktivera** från fliken **Start** i menyfliksområdet. Om den inaktuella uppdateringen tidigare publicerades som upphörde till Configuration Manager, kan du inte återaktivera den.
