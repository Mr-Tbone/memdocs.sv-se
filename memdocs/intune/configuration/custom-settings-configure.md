---
title: Använd anpassade enhetsinställningar i Microsoft Intune – Azure | Microsoft Docs
description: Du kan lägga till eller skapa en profil om du vill använda anpassade inställningar på enheter som kör Windows Phone, Windows 8.1, Windows 10 och senare, Android-enhetsadministratör, Android Enterprise, macOS eller iOS/iPadOS med Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6122f4624cc40152184c1c460afa6a7a39976063
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083993"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Skapa en profil med anpassade inställningar i Intune

Microsoft Intune innehåller många inbyggda inställningar för att styra olika funktioner på en enhet. Du kan också skapa anpassade profiler, som skapas på liknande sätt som inbyggda profiler. Anpassade profiler är användbara om du vill använda enhetsinställningar och funktioner som inte är inbyggda i Intune. Dessa profiler innehåller funktioner och inställningar som du kan styra på enheter i din organisation. Du kan till exempel skapa en anpassad profil som anger samma funktioner för alla iOS/iPadOS-enheter.

Anpassade inställningar konfigureras på olika sätt för respektive plattform. För att styra funktioner på Android- och Windows-enheter kan du till exempel ange OMA-URI-värden (Open Mobile Alliance Uniform Resource Identifier). För Apple-enheter kan du importera en fil som du skapat med [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) eller [Apple profilhanterare](https://support.apple.com/profile-manager).

Mer information om konfigurationsprofiler finns i [Vad är Microsoft Intune-enhetsprofiler?](device-profiles.md)

Den här artikeln visar hur du skapar en anpassad profil för Android-enhetsadministratör, Android Enterprise, iOS/iPad, macOS och Windows. Artikeln innehåller även alla tillgängliga inställningar för olika plattformar.

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

    - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Exempel på ett bra principnamn: **Windows 10: Anpassad profil som aktiverar AllowVPNOverCellular anpassad OMA-URI**.
    - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.
    - **Plattform**: Välj plattform för dina enheter. Alternativen är:

      - **Android-enhetsadministratör**
      - **Android enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 och senare**
      - **Windows 8.1 och senare**

    - **Profiltyp**: Välj **Anpassad**.

4. Inställningarna skiljer sig åt för de olika plattformarna. Om du vill se inställningarna för en viss plattform väljer du din plattform:

    - [Android-enhetsadministratör](custom-settings-android.md)
    - [Android enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

5. När du är klar väljer du **Skapa profil** > **Skapa**.

Profilen skapas och visas i profillistan (**Enhetskonfiguration** > **Profiler**).

## <a name="next-steps"></a>Nästa steg

När profilen har skapats är den klar att tilldelas. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
