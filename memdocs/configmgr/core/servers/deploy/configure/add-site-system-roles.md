---
title: Lägga till platssystemroller
titleSuffix: Configuration Manager
description: Förstå Configuration Manager plats system roller och hur du lägger till dem för att utöka din webbplats funktioner och kapacitet.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8a4ef1c4377e7b5ffba4ab0f04394ff1253c40df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721152"
---
# <a name="add-site-system-roles-for-configuration-manager"></a>Lägg till plats system roller för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Varje Configuration Manager-plats har stöd för flera plats system roller. Varje roll utökar funktionerna och kapaciteten för din plats att tillhandahålla tjänster till platsen och för att hantera enheter och användare. Varje platssystemroll på en platssystemserver måste komma från samma plats.

Configuration Manager har inte stöd för plats system roller för flera platser på en enda plats system Server.

> [!TIP]
> Om du inte är bekant med grunderna för plats system roller eller skillnaden mellan plats servern, plats system servrar och plats system roller, se [grunderna i Configuration Manager](../../../understand/fundamentals.md).

Följande artiklar beskriver procedurer och relaterade Detaljer för att installera plats system roller:

- [Installera plats system roller](install-site-system-roles.md): grundläggande vägledning om hur du använder de två guiderna i konsolen för att installera nya plats system roller.

- [Installera molnbaserade distributions platser](install-cloud-based-distribution-points-in-microsoft-azure.md): Använd Microsoft Azure som värd för innehåll som du distribuerar till klienter.

- [Installera plats system roller för lokal hantering av mobila enheter (MDM)](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md): Konfigurera plats system roller för att stödja hantering av moderna enheter med hjälp av Configuration Manager lokal MDM.

- [Konfigurations alternativ för plats system roller](configuration-options-for-site-system-roles.md): vissa plats system roller har stöd för konfigurationer som kräver mer information än vad användar gränssnittet kan förklara.

- [Ta bort en plats system roll](../install/uninstall-sites-and-hierarchies.md#bkmk_role): vägledning och procedurer för att ta bort roller från plats system servrar.
