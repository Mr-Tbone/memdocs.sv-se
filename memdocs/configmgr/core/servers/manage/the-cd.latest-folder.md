---
title: Mappen CD.Latest
titleSuffix: Configuration Manager
description: Lär dig mer om den process som levererar uppdateringar till produkten från Configuration Manager-konsolen.
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 577bfd865ad3872c386384c3bba95cb009ef83ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720515"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>CD: n. Den senaste mappen för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager har en process för att leverera uppdateringar till produkten från Configuration Manager-konsolen. För att stödja den nya metoden för att uppdatera Configuration Manager skapas en ny mapp med namnet **CD. Senaste**. Den här mappen innehåller en kopia av Configuration Manager-installationsfilerna för den uppdaterade versionen av webbplatsen.  

CD: n. Den senaste mappen innehåller en mapp med namnet **Redist**, som innehåller de distribuerbara filer som installations programmet hämtar och använder. De här filerna matchas mot den version av Configuration Manager-filerna som hittas i den CD.Latest-mappen. När du kör installationsprogrammet från en CD.Latest-mapp måste du använda filer som matchar den versionen av installationsprogrammet. Du kan antingen dirigera installations programmet för att ladda ned nya och aktuella filer från Microsoft, eller direkt installationen så att filerna från Redist-mappen som ingår i CD: n används. Senaste mappen.

Bas linje Media inkluderar inte en **Redist** -mapp. Platsen skapar inte en Redist-mapp förrän du har installerat en uppdatering i konsolen. Under tiden använder du den Redist-mapp som du använde när du installerade platser från bas linje mediet.  

> [!TIP]  
> Se till att de distribuerbara filer som du använder är aktuella. Om du inte nyligen har hämtat omdistribuerbara filer bör du planera att tillåta installation av installations programmet från Microsoft.   

Följande scenarier skapar eller uppdaterar CD: n. Senaste mappen på en central administrations plats eller primär plats Server:  

- När du installerar en uppdatering eller snabb korrigering från Configuration Manager-konsolen skapar eller uppdaterar platsen mappen i installations katalogen för Configuration Manager.  

- När du kör den Configuration Manager inbyggda säkerhets kopierings åtgärden skapar eller uppdaterar platsen mappen under den angivna platsen för mappen för säkerhets kopiering.  

- När du installerar en ny plats med hjälp av bas linje medier skapar platsen CD: n. Senaste mappen.


## <a name="supported-scenarios"></a>Scenarier som stöds

Källfilerna från CD: n. Den senaste mappen stöds i följande scenarier:  

### <a name="backup-and-recovery"></a>Säkerhetskopiering och återställning
Om du vill återställa en plats använder du källfilerna från en CD. Den senaste mappen som matchar din webbplats. När du kör en säkerhets kopia av en plats med hjälp av den inbyggda säkerhets kopierings åtgärden för platsen, CD: n. Den senaste mappen ingår som en del av säkerhets kopieringen.

- Om du installerar om en plats som en del av en platsåterställning installerar du platsen från mappen CD.Latest som finns i säkerhetskopian. Den här åtgärden installerar platsen med de fil versioner som överensstämmer med platsens säkerhets kopia och plats databas.  

    - Om du inte har åtkomst till rätt CD-skiva. Senaste version av mapp, Hämta CD-skivan. Den senaste mappen med rätt fil versioner genom att installera en plats i en labb miljö. Uppdatera sedan platsen så att den matchar den version som du vill återställa.  

    - Om du inte har rätt CD-skiva. Den senaste mappen och dess innehåll är tillgängligt, det går inte att återställa en plats. I detta fall måste du installera om platsen.  

- När du inte har en CD. Den senaste mappen, men har en fungerande underordnad primär plats eller en central administrations plats kan du använda den platsen som referens plats för en plats återställning.  

### <a name="install-a-child-primary-site"></a>Installera en underordnad primär plats
När du vill installera en ny underordnad primär plats under en central administrations plats som har installerat en eller flera uppdateringar i konsolen, använder du installationen och källfilerna från CD: n. Den senaste mappen från den centrala administrations webbplatsen. Den här processen använder installationskällfilerna som matchar versionen av den centrala administrations webbplatsen. Mer information finns i [använda installations guiden för att installera-platser](../deploy/install/use-the-setup-wizard-to-install-sites.md).  

### <a name="expand-a-stand-alone-primary-site"></a>Expandera en fristående primär plats
När du expanderar en fristående primär plats genom att installera en ny central administrations plats använder du installations programmet och källfilerna från CD: n. Den senaste mappen från den primära platsen. Den här processen använder installationskällfilerna som matchar versionen av den primära platsen. Mer information finns i [expandera en fristående primär plats](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).

### <a name="install-a-secondary-site"></a>Installera en sekundär plats
<!-- SCCMDocs-pr issue #3164 -->
När du vill installera en ny sekundär plats under en primär plats som har installerat en eller flera uppdateringar i konsolen, använder du källfilerna från CD: n. Den senaste mappen från den primära platsen. 

Mer information finns i [installera en sekundär plats](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary). 


## <a name="unsupported-scenarios"></a>Scenarier som inte stöds

Den uppdaterade CD-skivan. De senaste källfilerna stöds inte för:  

- Installera en ny plats för en ny hierarki  
- Uppgradera en Microsoft System Center 2012 Configuration Manager-plats till Configuration Manager aktuell gren
- Installera Configuration Manager klienter
- Installera Configuration Manager-konsoler
