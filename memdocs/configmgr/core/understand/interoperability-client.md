---
title: Utökad samverkansklient
titleSuffix: Configuration Manager
description: Lär dig mer om att använda den utökade samverkan klienten för långsiktigt stöd för en statisk Configuration Manager-klient med en aktuell förgrenings plats.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 61296321251be45cfa0449a3e4f21ba79a024753
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722783"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Använd Configuration Manager klient program vara för utökad interoperabilitet med framtida versioner av en Current Branch webbplats

*Gäller för: Configuration Manager (aktuell gren)*  

Affärs kraven kanske inte gör det möjligt att regelbundet uppdatera Configuration Manager-klienten på vissa enheter. Du måste till exempel följa principerna för ändrings hantering, eller så är enheten verksamhets kritisk. Anpassa dessa behov genom att installera en ny klient för långsiktig användning, som kallas för EIC (Extended driftskompatibilitet Client). Använd endast EIC för vissa enheter som inte kan uppdateras ofta, t. ex. kiosker eller kassa enheter. Fortsätt att använda [Automatisk klient uppgradering](../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate) för de flesta klienter.

## <a name="how-it-works"></a>Så här fungerar det

När du installerar en ny [uppdatering i konsolen](../servers/manage/install-in-console-updates.md) för Configuration Manager, uppdaterar klienterna automatiskt klient programmet så att de kan använda de nya funktionerna. I det här scenariot uppdaterar du fortfarande den aktuella grenen som tar emot nya funktioner och uppdateringar. De flesta enheter uppdaterar Configuration Manager klient program varan med varje versions uppdatering som du installerar. Men på en delmängd av kritiska system som du inte vill ta emot klient program uppdateringar installerar du den utökade klienten för interoperabilitet. Dessa klienter installerar inte den nya klient program varan förrän du uttryckligen distribuerar en ny version av klient program varan till dem.

## <a name="supported-versions"></a>Versioner som stöds

I följande tabell visas de versioner av Configuration Manager-klienten som stöds för det här scenariot:

| Version | Tillgänglighetsdatum | Stöds till och med |
|---------|---------|---------|
| 1902<br/>5.00.8790 | 27 mars 2019 | Tidigast den 27 mars 2021 |
| 1802<br/>5.00.8634 | Den 1 maj 2018 | Tidigast den 1 maj 2020 |
| 1606<br/>5.00.8412 | 18 november 2016 | Den 1 maj 2019 |

> [!TIP]  
> EIC stöds i minst två år från utgivnings datumet. Mer information om versions datum finns i [stöd för Configuration Manager aktuella gren versioner](../servers/manage/current-branch-versions-supported.md).  

Planera att uppdatera den utöknings bara klienten på enheter som du hanterar med den aktuella grenen innan stöd för klienten upphör att gälla. Det gör du genom att ladda ned en ny version av klienten från Microsoft och sedan distribuera den uppdaterade klient program varan till dina enheter som använder den aktuella klienten för utökad interoperabilitet.

## <a name="how-to-use-the-eic"></a>Använda EIC

1. Lägg till de här enheterna i en samling och exkludera samlingen från automatiska klient uppgraderingar. Mer information finns i [så här utesluter du klienter från uppgradering](../clients/manage/upgrade/exclude-clients-windows.md).  

1. Hämta en version av EIC som stöds från `\SMSSETUP\Client` mappen för installations mediet för Configuration Manager Update. Se till att du kopierar hela innehållet i mappen.  

    > [!TIP]  
    > Om du vill hitta Configuration Manager media i [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC) går du till fliken **nedladdningar och nycklar** , söker `System Center Config`efter och väljer sedan **System Center config hanterare (aktuell gren)**.

1. Installera EIC manuellt på dessa enheter. Mer information finns i [Installera klienten manuellt](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).  

    > [!Important]  
    > När du uppgraderar version 1606-klienter till version 1802 använder du CCMSETUP-alternativet **/AlwaysExcludeUpgrade: true**. Annars kan klienten ta emot principer från hanterings platsen för att automatiskt uppgradera före undantags principen.  

## <a name="limitations"></a>Begränsningar

- Uppdateringar för klient program varan för utökad interoperabilitet är inte tillgängliga med uppdateringar i konsolen. Mer information om hur du uppdaterar EIC finns i [så här uppgraderar du en exkluderad klient](../clients/manage/upgrade/exclude-clients-windows.md#bkmk_override).  

- EIC har endast stöd för följande funktioner:  

  - Programuppdateringar  
  - Inventering av maskin- och programvara
  - Paket och program

## <a name="next-steps"></a>Nästa steg

[Så här undantar du klienter från uppgradering](../clients/manage/upgrade/exclude-clients-windows.md)

Se [övervaka klienter](../clients/manage/monitor-clients.md)för att kontrol lera att klienterna är korrekt installerade på de enheter som du vill ha.
