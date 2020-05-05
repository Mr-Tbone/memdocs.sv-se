---
title: Definitioner av Endpoint Protection skadlig kod
titleSuffix: Configuration Manager
description: Lär dig att konfigurera Configuration Manager program uppdateringar för att leverera definitions uppdateringar till klient datorer.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c0b734fe2a63373e8fd1af9abe77cde7f52b6824
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126083"
---
# <a name="use-configuration-manager-to-deliver-definition-updates"></a>Använda Configuration Manager för att leverera definitions uppdateringar

*Gäller för: Configuration Manager (aktuell gren)*

Du kan konfigurera Configuration Manager program uppdateringar att automatiskt leverera definitions uppdateringar till klient datorer. Innan du börjar skapa automatiska distributions regler, se till att konfigurera Configuration Manager program uppdateringar. Mer information finns i [Introduktion till program uppdateringar](../../sum/understand/software-updates-introduction.md).

> [!NOTE]
> Den här proceduren är unik för Endpoint Protection. Mer allmän information om regler för automatisk distribution finns i [distribuera program uppdateringar automatiskt](../../sum/deploy-use/automatically-deploy-software-updates.md).

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **program uppdateringar**och välj sedan **automatiska distributions regler**.

1. På fliken **Start** i menyfliksområdet väljer du **Skapa regel för automatisk distribution**i gruppen **skapa** .

1. Ange följande på sidan **Allmänt** i **Guiden skapa regel för automatisk distribution**:

    - **Namn**: Ange namnet på regeln för automatisk distribution.

    - **Samling**: Välj den enhets samling som du vill distribuera definitions uppdateringar till.

        > [!NOTE]
        > Du kan inte distribuera definitions uppdateringar till en användar samling.

1. Välj **Lägg till i en befintlig program uppdaterings grupp**.

1. Välj **Aktivera distributionen när regeln har körts**.

1. På sidan **distributions inställningar** i guiden går du till **detalj nivån**och väljer **endast fel meddelanden**.

    > [!NOTE]
    > När du väljer **endast fel meddelanden**minskar det antalet tillstånds meddelanden som definitions distributionen skickar. Den här konfigurationen hjälper till att minska processor hanteringen på Configuration Manager-servrarna.

1. På sidan **program uppdateringar** :

    1. Välj egenskaps filtret **Uppdatera klassificering** . I listan **Sök villkor** väljer **du<objekt att söka efter\>**.

        I fönstret **Sök filter** väljer du **definitions uppdateringar**och väljer sedan **OK**.

    1. Välj filtret **produkt** egenskap. I listan **Sök villkor** väljer **du<objekt att söka efter\>**.

        I fönstret **Sök villkor** väljer du **System Center Endpoint Protection** för Windows 8,1 och tidigare eller **Windows Defender** för Windows 10 och senare. Välj sedan **OK**.

    > [!NOTE]
    > Du kan också filtrera ut ersatta uppdateringar. Välj egenskaps filtret **ersatt** . I listan **Sök villkor** väljer **du<objekt att söka efter\>**. I fönstret **Sök villkor** väljer du **Nej**och väljer sedan **OK**.

1. På sidan **utvärderings schema** i guiden väljer du **kör regeln efter varje synkronisering av en program uppdaterings plats**.

1. Konfigurera följande inställningar på sidan **Distributionsschema** i guiden:

    - **Tid baserat på**: Välj **UTC**om du vill att alla klienter ska installera de senaste definitionerna samtidigt. Den faktiska installations tiden varierar inom två timmar.

    - **Tillgänglig tid för program vara**: Ange den tillgängliga tiden för distributionen som den här regeln skapar. Den angivna tiden måste infalla minst en timme efter att regeln för automatisk distribution körs. Den här konfigurationen säkerställer att innehållet har tillräckligt med tid för att replikeras till distributions platserna. En del uppdateringar kan även innehålla uppdateringar till skyddsmotorn mot skadlig kod och det tar längre tid för dessa att nå distributionsplatser.

    - **Installationstidsgräns**: Välj **Så snart som möjligt**.

        > [!NOTE]
        > Tids gränser för program uppdateringar varierar under en period på två timmar. Det här beteendet förhindrar att alla klienter begär en uppdatering på samma tid.

1. På sidan **användar upplevelse** i guiden går du till **användar meddelanden** **och väljer Dölj i Software Center och alla meddelanden**. Med den här konfigurationen installeras definitions uppdateringarna i bakgrunden.

1. På sidan **distributions paket** i guiden väljer du ett befintligt distributions paket eller skapar ett nytt.

    > [!NOTE]
    > Överväg att placera definitions uppdateringar i ett paket som inte innehåller andra program uppdateringar. Den här strategin ser till att definitionsuppdateringspaketet är mindre, vilket gör att det kan replikeras snabbare till distributionsplatser.

1. Om du skapar ett nytt distributions paket går du till sidan **distributions platser** i guiden och väljer en eller flera distributions platser. Platsen kopierar innehållet för det här paketet till dessa distributions platser.

1. På sidan **hämtnings plats** väljer du **Hämta program uppdateringar från Internet**.

1. På sidan **Val av språk** väljer du varje språk version av uppdateringarna som ska laddas ned.

1. På sidan **nedladdnings inställningar** väljer du den nödvändiga hämtnings funktionen för program uppdateringar.

1. Slutför guiden.

Kontrol lera att den nya regeln visas i noden **regler för automatisk distribution** i Configuration Manager-konsolen.

> [!div class="nextstepaction"]
> [Skapa och distribuera principer för program mot skadlig kod](endpoint-antimalware-policies.md)
