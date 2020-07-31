---
title: Övervaka integrering av Microsoft Defender Avancerat skydd (ATP) i Microsoft Intune – Azure | Microsoft Docs
description: Övervaka Microsoft Defender Avancerat skydd (Microsoft Defender ATP) med Intune, inklusive status för enhetsefterlevnad och registrering.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cedb255a575d4b6ea04dd684b5592748e63397c8
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264569"
---
# <a name="monitor-device-status-when-you-integrate-microsoft-defender-atp-with-intune"></a>Övervaka enhetsstatus när du integrerar Microsoft Defender ATP med Intune

När du integrerar Microsoft Intune och Microsoft Defender Avancerat skydd (ATP) kan du visa information om enheternas efterlevnad och registrering i administrationscentret för Microsoft Endpoint Manager.

## <a name="monitor-device-compliance"></a>Övervaka enhetsefterlevnad

Övervaka status för enheter som har Microsoft Defender ATP-policyn för efterlevnad.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Övervaka** > **Principefterlevnad**.

3. Hitta din Microsoft Defender ATP-princip i listan och se vilka enheter som är kompatibla eller inkompatibla.

Du kan också använda den *operativa* rapporten för icke-kompatibla enheter från samma plats:

- Välj **Enheter** > **Övervaka** > **icke-kompatibla enheter**.

Mer information om rapporter finns i [Intune-rapporter](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Visa registreringsstatus

Om du vill se registreringsstatus för dina Intune-hanterade enheter kan du gå till **Slutpunktssäkerhet** > **Microsoft Defender ATP**. Från den här sidan kan du också skapa en enhetskonfigurationsprofil som kan registrera fler enheter i Microsoft Defender ATP.

## <a name="next-steps"></a>Nästa steg

[Tvinga fram kompatibilitet för Microsoft Defender ATP med villkorsstyrd åtkomst i Intune](../protect/advanced-threat-protection.md)
