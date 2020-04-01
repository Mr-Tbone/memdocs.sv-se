---
title: Använd massenhetsåtgärder i Microsoft Intune-enheten.
titleSuffix: ''
description: Använd massåtgärder för fjärranslutna enheter.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5f33198e71fd4250ee93207e571bc535abd1c95f
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325372"
---
# <a name="use-bulk-device-actions"></a>Använda massenhetsåtgärder

Du kan använda massenhetsåtgärder för följande fjärråtgärder:
- [Autopilot-återställning](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [Anpassade meddelanden](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [Ta bort](devices-wipe.md#delete-devices-from-the-intune-portal)
- [Byt namn](device-rename.md)
- [Starta om](device-restart.md)
- [Synkronisera](device-sync.md)
- [Rensning](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>Använd en massenhetsåtgärd

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Alla enheter** > **Massenhetsåtgärder**.
![Massenhetsåtgärder](./media/bulk-device-actions/bulk-device-actions.png)
3. På sidan **Massenhetsåtgärd** väljer du ett **Operativsystem** och en **Enhetsåtgärd**. För vissa enhetsåtgärder finns ytterligare alternativ eller fält som ska fyllas i. Välj **Nästa**.
4. På sidan **Enheter** väljer du mellan 1 och 100 enheter > **Nästa**.
5. På sidan **Granska + skapa** väljer du **Skapa**.

## <a name="next-steps"></a>Nästa steg
[Översikt över enhetshantering.](device-management.md)
