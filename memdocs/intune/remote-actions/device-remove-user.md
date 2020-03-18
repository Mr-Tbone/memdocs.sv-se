---
title: Ta bort en användare från en iOS/iPadOS-enhet med Microsoft Intune
titleSuffix: ''
description: Läs om hur du tar bort en användare från en delad iOS/iPadOS-enhet med Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2ea5941c-a69b-4e1c-b42c-a1fc0c3a7de7
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 08a6ccb30d4397ce5d06483556579c32f3eb2819
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348984"
---
# <a name="remove-a-user-from-a-shared-iosipados-device"></a>Ta bort en användare från en delad iOS/iPadOS-enhet


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Med åtgärden **Ta bort användare** tar du bort en vald användare från den lokala cachen på en delad iPad-enhet. iPad-enheten måste konfigureras för att hantera iOS/iPadOS-klassrumsappen med hjälp av en [iOS/iPadOS-utbildningsprofil](../fundamentals/education-settings-configure-ios.md). 

## <a name="supported-platforms"></a>Plattformar som stöds

- Windows – stöds inte
- Windows Phone – stöds inte
- iOS/iPadOS – stöds på iOS/iPadOS 9.3 och senare (endast delade iPad-enheter)
- macOS – stöds inte
- Android – stöds inte

## <a name="remove-a-user"></a>Ta bort en användare

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Alla enheter**.
3. Välj en iOS/iPadOS-enhet i listan över de enheter du hanterar.
4. Välj **Användare** i fönstret för enheten.
5. Högerklicka på den användare du vill ta bort i listan och välj sedan **Ta bort användare**.

## <a name="next-steps"></a>Nästa steg

- Om du vill se status för åtgärden **Ta bort användare** väljer du **Enheter** > **Enhetsåtgärder**.
