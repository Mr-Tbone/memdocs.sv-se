---
title: Begränsa enhetsfunktioner med principer i Microsoft Intune – Azure | Microsoft Docs
description: Lägga till en enhetsprofil för att begränsa funktioner i Android-enhetsadministratörs-, Android Enterprise-, macOS-, iOS-, iPadOS-, Windows Phone- och Windows 10-enheter i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 470ca47aa92b30acacc8a251c6d7d1741513bdf1
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359226"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Konfigurera inställningar för enhetsbegränsningar i Microsoft Intune

Intune innehåller principer för begränsning av enheter som hjälper administratörer att kontrollera Android-, iOS/iPadOS-, macOS-, och Windows-enheter. Med dessa begränsningar kan du kontrollera en mängd olika inställningar och funktioner för att skydda din organisations resurser. Administratörerna kan exempelvis:

- Tillåt eller blockera enhetens kamera.
- Kontrollera åtkomst till Google Play, App Store, dokumentvisning och spel.
- Blockera inbyggda appar eller skapa en lista över appar som tillåts eller blockeras.
- Tillåta eller förhindra säkerhetskopiering av filer till moln- och lagringskonton.
- Ange minsta längd på lösenord och blockera enkla lösenord.

Dessa funktioner är tillgängliga i Intune och kan konfigureras av administratören. Intune använder ”konfigurationsprofiler” till att skapa och anpassa inställningarna efter din organisations behov. När du har lagt till dessa funktioner i en profil, kan du skicka eller distribuera profilen till enheter i din organisation.

Den här artikeln beskriver hur du skapar en enhetsbegränsningsprofil. Artikeln innehåller även alla tillgängliga inställningar för olika plattformar.

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
        - **Windows 8.1 och senare**
        - **Windows Phone 8.1**

    - **Profil**: Välj **Enhetsbegränsningar**.

        För att skapa en enhetsbegränsningsprofil för Windows 10 Team-enheter, som en Surface Hub, väljer du sedan **Enhetsbegränsningar (Windows 10 Team)** .

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Ett exempel på ett bra principnamn är **iOS/iPadOS: Blockera kameran på enheterna**.
    - **Beskrivning**: Ange en beskrivning av principen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.

7. Under **Konfigurationsinställningar**  visas olika inställningar som du kan konfigurera beroende på vilken plattform du väljer. Välj din plattform för detaljerade inställningar:

    - [Android-enhetsadministratör](device-restrictions-android.md)
    - [Android enterprise](device-restrictions-android-for-work.md)
    - [iOS/iPadOS](device-restrictions-ios.md)
    - [macOS](device-restrictions-macos.md)
    - [Windows Phone 8.1](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 och senare](device-restrictions-windows-10.md)
    - [Windows 10-teamet](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business](device-restrictions-windows-holographic.md)

8. Välj **Nästa**.
9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar**väljer du de användare eller grupper som ska ta emot din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

## <a name="next-steps"></a>Nästa steg

När profilen har skapats är den klar att tilldelas. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
