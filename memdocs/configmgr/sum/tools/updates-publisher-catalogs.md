---
title: Hantera uppdaterings kataloger
titleSuffix: Configuration Manager
description: Hantera program uppdaterings kataloger för System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1314e2b4a6adc21b876e6bdbf8b25aa9e4fd3e9a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717771"
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Hantera program uppdaterings kataloger i Updates Publisher

*Gäller för: System Center Updates Publisher*

Använd **arbets ytan** **kataloger** för att hantera program uppdaterings kataloger. Detta inkluderar tillägg av nya kataloger, hantering av befintliga katalog prenumerationer och import av information om uppdateringarna från en katalog till utgivarens uppdaterings databas.

Program uppdaterings kataloger innehåller information om relaterade uppdateringar som skapats av andra organisationer än Microsoft. Andra organisationer är en egen organisation och program leverantörer från tredje part som har registrerat sina kataloger med Microsoft. Registrerade kataloger från program varu leverantörer kallas *partner kataloger*. Kataloger som du skapar och som inte är registrerade hos Microsoft kallas *användar* kataloger.

## <a name="add-software-update-catalogs"></a>Lägg till program uppdaterings kataloger
Du måste lägga till en uppdaterings katalog i Updates Publisher innan du kan hantera de uppdateringar som den innehåller. När du lägger till en katalog uppdateras Publisher:
-   Skapar en prenumeration på katalogen, så att den kan söka efter uppdateringar av katalogen.
-   Lägger till katalogen i en lista i fönstret **Mina program uppdaterings kataloger** i **arbets ytan kataloger**.  

Information om varje prenumerations katalog är tillgänglig i-konsolen. Informationen omfattar hämtnings-URL: en eller platsen, namnet på företaget eller organisationen som skapade katalogen och när den senast importerades eller ändrades.

Updates Publisher kan automatiskt kontrol lera dina prenumerationer efter ändringar varje gången de startas. Detta är konfigurerat som ett [Avancerat alternativ](updates-publisher-options.md#advanced). När updates har kon figurer ATS refererar uppdateringar till nedladdnings-URL: en eller plats informationen för prenumerationen och varnar dig när det finns ändringar i katalogen som har gjorts sedan den senaste gången du importerade den till lagrings platsen.

Om du vill söka efter en katalog uppdatering manuellt väljer du katalogen i listan **Mina program uppdaterings kataloger** och väljer sedan **Uppdatera** från menyfliksområdet.

Förutom att lägga till kataloger och Visa information om prenumererade kataloger kan du:
-  **Redigera** information för *användar* kataloger.
-  **Ta bort** (ta bort) en katalog från Updates Publisher.
-  **Importera** uppdateringar från en katalog till utgivarens updates-lagringsplats. När du importerar uppdateringar importerar du alla uppdateringar som finns i katalogen. Du kan sedan Visa uppdateringarna på arbets ytan uppdateringar där du sedan kan välja och publicera uppdateringar till uppdaterings servern.

> [!NOTE]   
> Om du tar bort en katalog från Updates Publisher resulterar uppdateringarna i katalogen bort från lagrings platsen. Detta påverkar inte de uppdateringar som du har publicerat på uppdaterings servern. Om du vill ta bort uppdateringar från din uppdaterings server som inte längre finns i din lagrings plats, se [Expires-program uppdateringar](updates-publisher-options.md#expire-unreferenced-software-updates)som inte är refererade.

## <a name="manage-update-catalogs"></a>Hantera uppdaterings kataloger
Du kan visa de List kataloger som du har importerat i fönstret **Mina program uppdaterings kataloger** i **arbets ytan kataloger**. Från den här arbets ytan kan du:

-   **Lägg till en partner katalog:** Använd något av följande för att hitta nya partner kataloger:

    -   I-konsolen går du till**Översikt över** **updates-arbetsytan** > . I fönstret **komma igång** väljer du **Lägg till partner program uppdaterings kataloger**.

    -   I-konsolen går du till **katalog arbets ytan** > **Mina kataloger**. Välj sedan **Lägg till kataloger**från menyfliksområdet.

-   **Lägg till en användar katalog:** I-konsolen går du till **katalog arbets ytan** > **Mina kataloger**. Välj sedan **Lägg till kataloger**från menyfliksområdet. Utöver platsen för CAB-filen måste du ange en utgivare, ett namn och en beskrivning för att identifiera katalogen.


-   **Sök efter uppdateringar av kataloger:** Välj en eller flera kataloger och välj sedan **Uppdatera** från menyfliksområdet.

-   **Redigera en användar katalog:** Välj en *användar* katalog och välj sedan **Redigera** från menyfliksområdet. Du kan sedan ändra de användardefinierade egenskaperna.

-   **Ta bort kataloger:** Välj en eller flera kataloger och välj sedan **ta bort** från menyfliksområdet. Detta tar bort katalogen, din prenumeration och uppdateringarna från dessa kataloger från din Updates Publisher-lagringsplats.

-   **Lägg till uppdateringar från en katalog i databasen**: Välj **Importera** från menyfliken för att starta guiden **Importera katalog** . Mer information finns i [Importera uppdateringar](#import-updates)

## <a name="import-updates"></a>Importera uppdateringar
När du importerar en katalog lägger uppdaterings hanteraren till uppdateringarna från katalogen till Updates Publisher-lagringsplatsen. När uppdateringarna har importer ATS kan du publicera dem på uppdaterings servern så att de blir tillgängliga för hanterade enheter.

### <a name="to-import-updates"></a>Importera uppdateringar
1. Starta guiden **Importera katalog** genom att välja **Importera** från menyfliken i någon av följande arbets ytor:

   -   Arbets ytan kataloger

   -   Arbets ytan uppdateringar

2. På sidan **import typ** väljer du en eller flera kataloger som du har lagt till i Updates Publisher eller anger en sökväg till en katalog som du ännu inte har lagt till som en prenumeration. Välj **Nästa** för att Visa sammanfattnings skärmen. När du är klar väljer du **Nästa** för att starta importen.

3. I fönstret **säkerhets varning – katalog validering** granskar du katalog certifikatet, och när du är klar väljer du **acceptera** för att importera uppdateringarna.

   > [!CAUTION]
   > Acceptera endast uppdateringar från utgivare som du litar på. Program uppdateringar från utgivare som inte är betrodda kan potentiellt skada klient datorer när de söker efter uppdateringar.
   > 
   >  Om du inte längre litar på utgivaren tar du bort utgivaren från listan över betrodda utgivare. Om du vill ha mer information om hur du accepterar kataloger klickar du på **berätta mer** i dialog rutan **säkerhets varning – katalog validering** .

   Om du väljer att alltid ta emot kataloger från en utgivare läggs utgivaren till i [listan över betrodda utgivare](updates-publisher-options.md#trusted-publishers). Du kan granska och redigera listan som ett alternativ för Updates Publisher.

4. Importera hoppar över import av en uppdatering när uppdateringen redan finns i databasen och något av följande stämmer:

   -   Uppdateringen är oförändrad från den senaste gången den importerades.

   -   Uppdateringen har redigerats och har en ny digital hash. Om du redigerar en uppdatering hindras den nya uppdateringen från att skriva över originalet som detta skulle skriva över ändringar som du kan ha distribuerat.

5. På **bekräftelse** sidan granskar du import resultaten.

6. Klicka på **Stäng** för att slutföra guiden. Nu kan du visa uppdateringarna för den här katalogen i arbets ytan uppdateringar.

## <a name="next-steps"></a>Nästa steg
När du har importerat uppdateringar inkluderar vanliga åtgärder:
-   [Hantera uppdateringar](manage-updates-with-updates-publisher.md) av bunta, tilldela och distribuera uppdaterings servern.
-   [Skapa tillämplighets regler](updates-publisher-applicability-rules.md) som hjälper dig att avgöra när uppdateringarna distribueras till uppdaterings servern.
