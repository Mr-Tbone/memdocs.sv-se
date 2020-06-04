---
title: Uppgradera till Windows Holographic for Business i Microsoft Intune – Azure | Microsoft Docs
description: Uppgradera till Windows 10 Holographic for Business med en enhetskonfigurationsprofil i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d561d2682cf90d5d7075640c260d8f21c8b891b1
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556123"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Uppgradera enheter som kör Windows Holographic till Windows Holographic for Business

Microsoft Intune innehåller många inställningar som hanterar och skyddar dina enheter. I den här artikeln visas och beskrivs inställningarna för att uppgradera Windows Holographic-enheter till Windows Holographic for Business.

I din MDM-lösning (hantering av mobilenheter) använder du dessa inställningar när du uppgraderar dina Windows Holographic-enheter. Du kan köpa Commercial Suite om du behöver licensen som krävs vid uppgraderingen av Microsoft HoloLens. Mer information finns i [Unlock Windows Holographic for Business features](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise) (Lås upp funktioner i Windows Holographic for Business).

Som Intune-administratör kan du skapa och tilldela dessa inställningar till dina enheter.

Mer information om den här funktionen finns i [Uppgradera Windows 10-utgåvor eller aktivera S-läget](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en Windows 10-versionuppgradering och lägesväxla enhetskonfigurationsprofilen](edition-upgrade-configure-windows-10.md#create-the-profile).

När du skapar en Windows 10-versionsuppgradering och lägesväxlar enhetskonfigurationsprofilen finns det fler inställningar än vad som anges i den här artikeln. Inställningarna i den här artikeln stöds på Windows Holographic for Business-enheter.

## <a name="edition-upgrade"></a>Versionsuppgradering

- **Utgåva att uppgradera till**: Välj **Windows 10 Holographic for Business**.
- **Licensfil**: Bläddra till och välj den XML-licensfil som du har fått.

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="Ange XML-filnamnet som innehåller licensinformationen för Holographic for Business i Intune.":::

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Du kan också skapa uppgraderingsprofiler för utgåvan till enheter som har [Windows 10 och senare](edition-upgrade-windows-settings.md).
