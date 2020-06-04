---
title: Låsa enheter med Microsoft Intune – Azure | Microsoft Docs
description: Använd åtgärden för fjärrlåsning i Microsoft Intune för att låsa en enhet som skyddas av en PIN-kod eller ett lösenord.
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
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6cafadbecbb0e0f0287b8a6ac4db5a1168e5e84
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983085"
---
# <a name="remotely-lock-devices-with-intune"></a>Fjärrlåsa enheter med Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Åtgärden **Fjärrlås** låser enheten. Enhetens ägare måste ange sitt lösenord för att låsa upp den. Du kan fjärrlåsa enheter som har en PIN-kod eller ett lösenord. Enheter som saknar PIN-kod eller lösenord går inte att fjärrlåsa.

## <a name="supported-platforms"></a>Plattformar som stöds

**Fjärrlås** stöds på följande plattformar:

- Android
- Android enterprise-kioskenheter
- Android enterprise-arbetsprofilenheter
- iOS
- macOS
- Windows 10 Mobil
- Windows Phone 8.1 och senare

**Fjärrlås** stöds inte för:
- Windows 10 desktop

> [!NOTE]
> För macOS-enheter anger du en 6-siffrig PIN-kod för återställning. När enheten är låst visar **Enhetsöversikt** PIN-koden tills en annan enhetsåtgärd skickas. Se till att skriva ner PIN-koden eftersom den bara är tillgänglig i 7 dagar efter att kommandot för fjärrlås har skickats. Efter sju dagar kommer Intune inte längre att ha PIN-koden. Initiera inte heller det här kommandot igen för samma enhet förrän den ursprungliga PIN-koden används för att låsa upp enheten. Du bör skicka det här kommandot, skriva ned PIN-koden och inte skicka kommandot till samma enhet igen förrän du har använt det för att komma till macOS-enheten.  


## <a name="remote-lock-a-device"></a>Fjärrlås på en enhet

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Välj **Enheter** > **Alla enheter**.
4. Välj en enhet i listan över enheter och välj sedan åtgärden **Fjärrlås**.

## <a name="next-steps"></a>Nästa steg

- Om du vill se status för den här åtgärden väljer du **Microsoft Intune** > **Enheter** > **Enhetsåtgärder**. 
- Se [Tillgängliga åtgärder](device-management.md) för fler åtgärder som kan hjälpa dig att hantera enheter.
