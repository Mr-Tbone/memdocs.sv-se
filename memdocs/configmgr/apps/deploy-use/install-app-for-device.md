---
title: Installera program för en enhet
titleSuffix: Configuration Manager
description: Använd Configuration Manager för att omedelbart installera ett program på en enhet utan en samling.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c2a71fca-8744-4d72-abf9-9d8c5d2afb00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a9f0c7d6eb7d8ccc42c5740bdb4b67926f676d8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710225"
---
# <a name="install-applications-for-a-device"></a>Installera program för en enhet

<!--4402180-->

Från Configuration Manager-konsolen kan du installera program på en enhet i real tid från och med version 1906. Den här funktionen kan hjälpa till att minska behovet av separata samlingar för varje program.

## <a name="prerequisites"></a>Krav

- Aktivera den [valfria funktionen](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **Godkänn program begär Anden för användare per enhet**.  

- [Distribuera programmet](deploy-applications.md) som *tillgängligt* för en enhets samling.  

    - På sidan **distributions inställningar** i distributions guiden väljer du följande alternativ: **en administratör måste godkänna en begäran om det här programmet på enheten**.  

        > [!Note]  
        > Med de här distributions inställningarna skickas ingen princip till klienten. Appen visas inte som tillgänglig i Software Center och en användare kan inte installera appen med den här distributionen. När du har använt den här åtgärden för att installera appen, kan användaren köra den och se dess installations status i Software Center.

- Ditt användar konto måste ha följande behörigheter:

    - **Program**: läsa, Godkänn

    - **Samling**: läsa, läsa resurs, ändra resurs, Visa insamlad fil

    Den inbyggda rollen **program administratör** har till exempel dessa behörigheter.

> [!TIP]
> I en-hierarki väntar du tills program-och distributions information replikeras till den primära plats som mål klienten är tilldelad.<!-- SCCMDocs#2113 -->

## <a name="process"></a>Process

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enheter** . Välj mål enheten och välj sedan åtgärden **installera program** i menyfliksområdet.

1. Välj ett eller flera program i listan. Listan visar endast program som du redan har distribuerat med nödvändiga inställningar.

Den här åtgärden utlöser installationen av de valda fördistribuerade programmen på enheten.

Om du vill se status för begäran om godkännande, expanderar du **program hantering**på arbets ytan **program varu bibliotek** och väljer noden **program begär Anden** .

Övervaka appens installation på samma sätt som vanligt i noden **distributioner** på arbets ytan **övervakning** .


## <a name="see-also"></a>Se även

[Godkänna program](app-approval.md)
