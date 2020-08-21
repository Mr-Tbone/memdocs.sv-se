---
title: Inställningar för Windows 10-uppgradering och S-läge i Microsoft Intune – Azure | Microsoft Docs
description: Se en lista med alla inställningar och vad de gör när du uppgraderar en Windows 10-utgåva på en enhet, eller när du aktiverar S-läget på en enhet med en enhetskonfigurationsprofil i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8d050139ae017f5800670518a41d75fba469ceac
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146481"
---
# <a name="windows-10-and-newer-device-settings-to-upgrade-editions-or-enable-s-mode-in-intune"></a>Enhetsinställningar för Windows 10 (och senare) vid uppgradering av utgåvor, eller när S-läget aktiveras i Intune

Microsoft Intune innehåller många inställningar som hanterar och skyddar dina enheter. I den här artikeln visas och beskrivs inställningarna för att uppgradera utgåvor eller aktivera S-läget på Windows 10-enheter. Inställningarna skapas i uppgraderingens konfigurationsprofil i Intune, som sedan skickas eller distribueras till enheterna.

I din MDM-lösning (hantering av mobilenheter) använder du dessa inställningar för att styra alternativen för utgåvan och S-läget på dina Windows 10-enheter.

Mer information om den här funktionen finns i [Uppgradera Windows 10-utgåvor eller aktivera S-läget](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Innan du börjar

[Skapa profilen](edition-upgrade-configure-windows-10.md#create-the-profile).

## <a name="edition-upgrade"></a>Versionsuppgradering

- **Utgåva att uppgradera till**: Välj den Windows 10-utgåva som du uppgraderar till. De enheter som omfattas av principen uppgraderas till den valda utgåvan.
- **Produktnyckel**: Ange produktnyckeln som du fick från Microsoft. När du har skapat en princip som innehåller en produktnyckel går den inte att uppdatera och den är dold av säkerhetsskäl. Om du vill ändra produktnyckeln måste du ange hela nyckeln igen.
- **Licensfil**: För **Windows 10 Holographic for Business** väljer du **Bläddra** och väljer licensfilen som du har fått från Microsoft. Licensfilen innehåller licensinformation för de utgåvor som du uppgraderar enheterna till.

## <a name="mode-switch"></a>Växla läge

- **Växla från S-läge**: Växlar enheten från S-läget. Alternativen är:

  - **Ingen konfiguration**: Intune varken ändrar eller uppdaterar den här inställningen. Som standard kan S-lägesenheten stanna kvar i S-läge. Användaren kan ange att enheten ska växla från S-läget.
  - **Behåll i S-läget**: Förhindrar att användare växlar enheten från S-läget.
  - **Växla**: Användare kan ange att enheten ska växla från S-läget.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Du kan också skapa uppgraderingsprofiler för utgåvan i [Windows Holographic for Business](holographic-upgrade.md)-enheter.
