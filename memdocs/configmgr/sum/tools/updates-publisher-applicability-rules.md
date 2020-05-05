---
title: Tillämpbarhetsregler
titleSuffix: Configuration Manager
description: Hantera tillämplighets regler för System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53a3aabfe65449723bdb6076486128b76a1a830c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078438"
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>Hantera Tillämplighets regler i Updates Publisher

*Gäller för: System Center Updates Publisher*

Med Updates Publisher definierar tillämplighets reglerna krav som måste uppfyllas innan en enhet kan installera en uppdatering. Reglerna används också för att avgöra om datorn har installerat en uppdatering. En tillämplighets regel som är komplex med flera delar kallas en regel uppsättning.

Uppdaterings paket använder inte tillämplighets regler.

## <a name="overview-of-applicability-rules"></a>Översikt över tillämplighets regler
Du hanterar tillämplighets regler från **arbets ytan regler**. När du skapar en regel anger du ett eller flera villkor. När du har angett flera villkor kan du konfigurera relationer mellan villkoren så att de utvärderas sekventiellt eller kombineras i logiska uttryck **och** or **or** -uttryck.

Följande är till exempel en regel uppsättning som innehåller tre regler. Den första regeln verifierar *att filen finns och att de andra* och tredje reglerna kontrollerar att språket i Windows-operativsystemet är antingen engelska eller japanska.

``` Example
And  
  File '\[PROGRAM\_FILES\] \\Microsoft\\MyFile' exists  
  Or  
    Windows Language is English
    Windows Language is Japanese
```

Alla uppdateringar kräver minst en tillämplighets regel. De uppdateringar du importerar har redan tillämpade tillämplighets regler, och när du skapar egna uppdateringar måste du lägga till en eller flera regler. Du kan ändra och utöka reglerna för uppdateringar i Updates Publisher.

Om du vill visa regler som du har skapat väljer du en regel i listan **mina sparade regler** på **arbets ytan regler**. De enskilda villkoren och logiska åtgärder för den regeln visas i fönstret **Tillämplighets regler** i-konsolen. Regler för uppdateringar som du importerar kan bara visas och ändras när du redigerar uppdateringen.

Du kan skapa regler på två platser i Updates Publisher:

-   På **arbets ytan regler** skapar du och **sparar** regel uppsättningar som du sedan kan använda senare. När du redigerar eller skapar en uppdatering kan du välja **Sparad regel** som **regeltyp**och sedan välja från en lista över de tidigare skapade regel uppsättningarna.

-   Du kan också skapa nya regler vid den tidpunkt då du skapar eller redigerar en uppdatering. Regler som du skapar på det här sättet sparas inte för framtida användning.

## <a name="create-applicability-rule"></a>Skapa tillämplighets regel
Följande information liknar hur du skapar regler i [guiden skapa uppdatering](create-updates-with-updates-publisher.md#use-the-create-update-wizard). Men till skillnad från guiden har du möjlighet att spara regel uppsättningar för framtida bruk.

1. I **arbets ytan regler**väljer du **skapa** för att öppna guiden **Skapa regel** .

2. Ange ett namn för regeln och klicka sedan på ![ny regel.](media/newrule.png) Då öppnas **Tillämplighets regel** sidan där du kan konfigurera regler.

3. Välj något av följande för **regel typ** . De alternativ som du måste konfigurera varierar för varje typ:

   - **Fil** – Använd den här regeln för att kräva att en enhet har en fil med egenskaper som uppfyller ett eller flera villkor som du anger innan uppdateringen kan tillämpas.

   - **Register –** Använd den här typen för att ange register information som måste finnas innan en enhet kvalificerar sig för att installera den här uppdateringen.

   - **System –** Den här regeln använder system information för att fastställa tillämplighet. Du kan välja mellan att definiera en Windows-version, ett Windows-språk, en processor arkitektur eller ange en WMI-fråga för att identifiera enheternas operativ system.

   - **Windows Installer –** Använd den här regel typen för att fastställa tillämplighet baserat på en installerad. MSI eller Windows Installer korrigering (. MSP). Du kan också bestämma om vissa komponenter eller funktioner installeras som en del av kravet.

     > [!IMPORTANT]   
     > På den hanterade inices-enheten kan Windows Update-agenten inte identifiera Windows installations paket som är installerade per användare. När du använder den här regel typen konfigurerar du ytterligare tillämplighets regler, t. ex. fil versioner eller register nyckel värden, så att Windows Installer-paketet kan identifieras på rätt sätt oavsett per användare eller per system.

   - **Sparad regel –** Med det här alternativet kan du hitta och använda regler som du tidigare har konfigurerat och sparat.

4. Fortsätt att lägga till och konfigurera ytterligare regler efter behov.

5. Använd knapparna för logiska åtgärder för att ordna och gruppera olika regler för att skapa mer komplexa krav kontroller.

6. När regel uppsättningen är klar klickar du på **OK** för att spara den. Regel uppsättningen visas nu i listan **mina sparade regler** .

## <a name="edit-applicability-rule-sets"></a>Redigera tillämplighets regel uppsättningar
Om du vill redigera en tillämplighets regel går du till **arbets ytan regler** och väljer en regel som har sparats i listan **mina sparade regler** och väljer sedan **Redigera** från menyfliksområdet. Då öppnas guiden **Redigera regel** .

Guiden **Redigera regel** visar de aktuella reglerna för regel uppsättningen. Du kan redigera regler på samma sätt som du använder guiden **Skapa regel** för att skapa nya regler. Du kan använda den här guiden för att byta namn på regel uppsättningen, ta bort regler, sortera om regler och relationer, eller lägga till nya regler.

När du har gjort ändringarna väljer du **OK** för att spara ändringarna och stänga guiden.

Mer information om hur du använder regel guiden finns i **steg 7**, sidan tillämpbarhet, i [guiden skapa uppdatering](create-updates-with-updates-publisher.md#use-the-create-update-wizard).

## <a name="delete-applicability-rules"></a>Ta bort tillämplighets regler
Om du vill ta bort en sparad tillämplighets regel väljer du regel eller regel uppsättning i listan **mina sparade regler** på **arbets ytan regler** och väljer sedan **ta bort** från menyfliksområdet. Den sparade regeln eller regel uppsättningen tas bort från Updates Publisher.

Om du vill ta bort en regel från en enskild uppdatering måste du [Redigera uppdateringen](manage-updates-with-updates-publisher.md#edit-updates-and-bundles).
