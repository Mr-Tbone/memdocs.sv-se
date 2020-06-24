---
title: Helskärmsinställningar för Windows- och Holographic-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Konfigurera enheter med Windows 10 (och senare) samt Windows Holographic for Business med helskärmsläge för en app eller flera appar, anpassa startmenyn, lägg till appar, visa aktivitetsfältet och konfigurera en webbläsare i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f58e457a5868053a94e1f2c1185bbae0e4b69327
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093081"
---
# <a name="windows-10-and-windows-holographic-for-business-device-settings-to-run-as-a-dedicated-kiosk-using-intune"></a>Inställningar för enheter med Windows 10 (och senare) och Windows Holographic for Business som ska köras i dedikerat helskärmsläge med Intune

Använd Intune på Windows 10-enheter att köras som kioskenhet, som ibland kallas dedikerad enhet. En enhet i helskärmsläge kan köra en app eller många appar. Du kan visa och anpassa en startmeny, lägga till olika appar, inklusive Win32-appar, lägga till en viss startsida i en webbläsare och mycket mer. 

Den här funktionen gäller för:

- Windows 10 och senare
- Windows 10 Holographic for Business

Information om hur du skapar kioskprofiler för andra plattformar finns i [Android-enhetsadministratör](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience) och [iOS/iPad](device-restrictions-ios.md#kiosk).

Intune stöder en helskärmsprofil per enhet. Om du behöver flera helskärmsprofiler på en enskild enhet, kan du använda en [Anpassad OMA-URI](custom-settings-windows-10.md).

Intune använder ”konfigurationsprofiler” till att skapa och anpassa inställningarna efter din organisations behov. När du har lagt till funktionerna i en profil, skickar eller distribuerar du dessa inställningar till grupperna i din organisation.

Den här artikeln beskriver hur du skapar en enhetskonfigurationsprofil. En lista med alla inställningar och vad de gör finns i [Inställningar för helskärmsläge i Windows 10](kiosk-settings-windows.md) och [Inställningar för helskärmsläge i Windows Holographic for Business](kiosk-settings-holographic.md).

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

   - **Plattform**: Välj **Windows 10 och senare**.
   - **Profil**: Välj **Helskärmsläge**.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

   - **Namn**: Ange ett beskrivande namn på den nya profilen.
   - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.
7. I **Konfigurationsinställningar** > **Välj ett helskärmsläge** väljer du den typ av helskärmsläge som stöds av policyn. Alternativen är:

    - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Principen aktiverar inte helskärmsläge.
    - **En app, helskärmsläge**: Enhet körs som ett enda användarkonto och låser det till en enda Store-app. När användaren loggar in startar alltså en specifik app. Det här läget gör också att användaren inte kan öppna nya appar eller ändra appen som körs.
    - **Helskärmsläge för flera appar**: Enheten kör flera Store-appar, Win32-appar eller inkorgens Windows-appar med hjälp av ett ID för programanvändarmodell (AUMID). Det är bara de appar som du lägger till som är tillgängliga på enheten.

        Med en kiosk för flera appar, eller en enhet för ett bestämt ändamål, skapas en mer användarvänlig upplevelse för användarna eftersom de endast ser de appar de behöver. Appar som de inte behöver visas inte.

    En lista med alla inställningar och vad de gör finns i:

      - [Inställningar för helskärmsläge i Windows 10](kiosk-settings-windows.md)
      - [Inställningar för helskärmsläge i Windows Holographic for Business](kiosk-settings-holographic.md)

8. Välj **Nästa**.

9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar** väljer du de användare eller den användargrupp som ska få din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

Nästa gång varje enhet checkar in tillämpas principen.

## <a name="next-steps"></a>Nästa steg

När [profilen har tilldelats](device-profile-assign.md) [övervakar du dess status](device-profile-monitor.md).

Du kan skapa helskärmsprofiler för enheter som kör följande plattformar:

- [Android-enhetsadministratör](device-restrictions-android.md#kiosk)
- [Android enterprise](device-restrictions-android-for-work.md#device-experience)
- [Windows 10 och senare](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
