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
ms.openlocfilehash: 4e558c885098b8b396ca0e6304bd18ef36e3c28b
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252245"
---
# <a name="remotely-lock-devices-with-intune"></a>Fjärrlåsa enheter med Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Åtgärden **Fjärrlås** låser enheten. Enhetens ägare måste ange sitt lösenord för att låsa upp den. Du kan fjärrlåsa enheter som har en PIN-kod eller ett lösenord. Enheter som saknar PIN-kod eller lösenord går inte att fjärrlåsa.

## <a name="supported-platforms"></a>Plattformar som stöds

**Fjärrlås** stöds på följande plattformar:

- Android
- Android Enterprise-kioskenheter
- Android Enterprise-arbetsprofilenheter
- Fullständigt hanterade Android Enterprise-enheter
- Företagsägda Android Enterprise-enheter med arbetsprofil
- iOS
- macOS

**Fjärrlås** stöds inte för:
- Windows 10 desktop

> [!NOTE]
> För macOS-enheter anger du en 6-siffrig PIN-kod för återställning. När enheten är låst visar **Enhetsöversikt** PIN-koden tills en annan enhetsåtgärd skickas. Se till att skriva ner PIN-koden eftersom den bara är tillgänglig i 30 dagar efter att fjärrlåsningskommandot har skickats. Efter 30 dagar har inte Intune PIN-koden längre. Du ser även en misslyckad status i rapporten om du kör kommandot igen för samma enhet medan den ursprungliga PIN-koden inte har använts till att låsa upp enheten. Du bör bara köra det här kommandot en gång, skriva ned PIN-koden och inte skicka kommandot till samma enhet igen förrän du har använt koden till att komma åt macOS-enheten.


## <a name="remote-lock-a-device"></a>Fjärrlås på en enhet

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Välj **Enheter** > **Alla enheter**.
4. Välj en enhet i listan över enheter och välj sedan åtgärden **Fjärrlås**.

## <a name="next-steps"></a>Nästa steg

- Om du vill se status för den här åtgärden väljer du **Microsoft Intune** > **Enheter** > **Enhetsåtgärder**. 
- Se [Tillgängliga åtgärder](device-management.md) för fler åtgärder som kan hjälpa dig att hantera enheter.
