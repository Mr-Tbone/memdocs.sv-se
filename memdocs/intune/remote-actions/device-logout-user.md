---
title: Logga ut användaren från en iOS/iPadOS-enhet
titleSuffix: Microsoft Intune
description: Lär dig hur du kan logga ut den aktuella användaren från en iOS/iPadOS-enhet med Intune."
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 702bc46c-1a6f-4689-bd53-3b778a447baa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e151110a39e28d00a2a98cd6ea3c3fc9214ef4a0
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983477"
---
# <a name="logout-the-current-user-on-intune-managed-iosipados-devices"></a>Logga ut den aktuella användaren från Intune-hanterade iOS/iPadOS-enheter


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Åtgärden **Logga ut aktuell användare** loggar ut den aktuella användaren på en delad iPad-enhet. 

## <a name="supported-platforms"></a>Plattformar som stöds

- Windows – stöds inte
- Windows Phone – stöds inte
- iOS/iPadOS – stöds på iOS/iPadOS 9.3 och senare (endast delade iPad-enheter)
- macOS – stöds inte
- Android – stöds inte

## <a name="how-to-log-out-the-current-user"></a>Så här loggar du ut den aktuella användaren

1. Logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj **Enheter** > **Alla enheter**.
2. Välj en iOS-/iPad-enhet > **...**  > **Logga ut aktuell användare**.

## <a name="next-steps"></a>Nästa steg

Om du vill se status för den åtgärd som du vidtog, går du till bladet **Enheter och grupper** och väljer **Enhetsåtgärder**.
