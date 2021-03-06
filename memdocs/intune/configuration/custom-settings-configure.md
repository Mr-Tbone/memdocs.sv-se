---
title: Använd anpassade enhetsinställningar i Microsoft Intune – Azure | Microsoft Docs
description: Du kan lägga till eller skapa en profil om du vill använda anpassade inställningar på enheter som kör Windows 8.1, Windows 10 och senare, Android-enhetsadministratör, Android Enterprise, macOS eller iOS/iPadOS med Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: aaa0deaf2c6332965f40ae02a47b7541cf2f9e8e
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146413"
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

    - **Plattform**: Välj plattform för dina enheter. Alternativen är:  

        - **Android-enhetsadministratör**
        - **Android enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 och senare**

    - **Profil**: Välj **Anpassad**.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Exempel på ett bra principnamn: **Windows 10: Anpassad profil som aktiverar AllowVPNOverCellular anpassad OMA-URI**.
    - **Beskrivning**: Ange en beskrivning av principen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.

7. Under **Konfigurationsinställningar**  visas olika inställningar som du kan konfigurera beroende på vilken plattform du väljer. Välj din plattform för detaljerade inställningar:

    - [Android-enhetsadministratör](custom-settings-android.md)
    - [Android enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)

8. Välj **Nästa**.
9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar**väljer du de användare eller grupper som ska ta emot din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

## <a name="example"></a>Exempel

I följande exempel är inställningen **Connectivity/AllowVPNOverCellular** aktiverad. Med den här inställningen kan en Windows 10-enhet öppna en VPN-anslutning vid användning av ett mobilnät.

> [!div class="mx-imgBorder"]
> ![Exempel på en anpassad princip som innehåller VPN-inställningar i Intune och Endpoint Manager](./media/custom-settings-configure/custom-policy-example.png)

## <a name="next-steps"></a>Nästa steg

Profilen skapas, men den kanske inte gör något än. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
