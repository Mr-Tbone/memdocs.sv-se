---
title: Hantera uppgraderingspaket för operativsystem
titleSuffix: Configuration Manager
description: Lär dig hur du hanterar OS-uppgraderings paket i Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a50592815ed4581c01489f90b6c3701e53bb4981
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124422"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Hantera uppgraderings paket för operativ system med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Ett uppgraderings paket för operativ system i Configuration Manager innehåller källfilerna för Windows-installationen för att uppgradera ett befintligt operativ system på en dator. Den här artikeln beskriver hur du lägger till, distribuerar och servicer ett uppgraderings paket för operativ system.

> [!NOTE]
> Uppgraderings paket för operativ system kan också användas för nya installationer av Windows. Det är dock beroende av driv rutiner som är kompatibla med den här metoden. När du utför nya installationer av Windows från ett uppgraderings paket för operativ system installeras driv rutinerna samtidigt som Windows PE och helt enkelt matas in i Windows PE. Vissa driv rutiner är inte kompatibla med att installeras i Windows PE. Om driv rutinerna inte är kompatibla med att installeras i Windows PE kan du använda en [operativ system avbildning](manage-operating-system-images.md), till exempel **install. wim**, i stället.

## <a name="add-an-os-upgrade-package"></a><a name="BKMK_AddOSUpgradePkgs"></a>Lägg till ett uppgraderings paket för operativ system  

Innan du kan använda ett uppgraderings paket för operativ systemet måste du först lägga till det på Configuration Manager-platsen.

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj sedan noden **uppgraderings paket för operativ system** .  

2. Välj **Lägg till uppgraderings paket för operativ system**i gruppen **skapa** på fliken **Start** i menyfliksområdet. Den här åtgärden startar guiden Lägg till uppgradering av operativ system.  

3. På sidan **data källa** anger du följande inställningar:

    - Nätverks **Sök vägen** till installationskällfilerna för operativ systemets uppgraderings paket. Till exempel `\\server\share\path`.  

        > [!NOTE]  
        >  Installations källorna innehåller setup.exe och andra filer och mappar för att installera operativ systemet.  

        > [!IMPORTANT]  
        >  Begränsa åtkomsten till dessa installationskällfilerna för att förhindra oönskade manipulation.  

    - **Extrahera ett särskilt avbildnings index från install. wim-filen för det valda uppgraderings paketet** och välj sedan ett bild index i listan.<!--4931110--> Från och med version 1910 importerar det här alternativet automatiskt ett enskilt index i stället för alla bild index i filen. Med det här alternativet resulterar det i en mindre bildfil och snabbare offlineunderhåll. Det stöder också processen för att [optimera avbildnings underhåll](#bkmk_resetbase)för en mindre bildfil efter att ha tillämpat program uppdateringar.  

        > [!IMPORTANT]  
        > Configuration Manager skriver över den befintliga install. wim-filen i uppgraderings paketet för operativ systemet. Avbildnings indexet extraheras till en tillfällig plats och flyttas sedan till den ursprungliga käll katalogen. Innan du importerar ett uppgraderings paket för operativ systemet och aktiverar det här alternativet, måste du säkerhetskopiera de ursprungliga källfilerna.

    - Om du vill cachelagra innehåll i förväg på en klient anger du avbildningens **arkitektur** och **språk** . Mer information finns i [Konfigurera förinställt innehåll för cache](../deploy-use/configure-precache-content.md).  

4. På sidan **Allmänt** anger du följande information. Den här informationen är användbar i identifierings syfte när du har fler än ett uppgraderings paket för operativ system.  

    - **Namn**: ett unikt namn för operativ systemets uppgraderings paket.  

    - **Version**: en valfri versions identifierare. Den här egenskapen behöver inte vara operativ systemets version av uppgraderings paketet. Det är ofta organisationens version av paketet.  

    - **Kommentar**: en valfri kort beskrivning.  

5. Slutför guiden.  

Distribuera sedan operativ Systems uppgraderings paketet till distributions platser.  

## <a name="distribute-content-to-a-distribution-point"></a><a name="BKMK_Distribute"></a>Distribuera innehåll till en distributions plats  

Distribuera uppgraderings paket för operativ system till distributions platser på samma sätt som andra innehåll. Innan du distribuerar aktivitetssekvensen distribuerar du operativ system uppgraderings paketet till minst en distributions plats. Mer information finns i avsnittet [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]

## <a name="next-steps"></a>Nästa steg

[Skapa en aktivitetssekvens för att uppgradera ett operativsystem](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
