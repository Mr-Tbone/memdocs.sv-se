---
title: Lägg till eller konfigurera utbildningsinställningar i Microsoft Intune – Azure | Microsoft Docs
description: Använd appen Gör ett prov i konfigurationsprofilen på Windows 10 och senare enheter i Microsoft Intune. Skapa en konfigurationsprofil med Education-inställningar och ange en URL för testappen, välj hur användare loggar in, övervaka skärmen under provet och tillåt eller förhindra textförslag under provet.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 52eae65e6735ad655c2e8db53e34383ccc5e3b30
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988400"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Använd appen Gör ett prov på Windows 10-enheter i Microsoft Intune

Utbildningsprofiler i Intune är utformade för elever som ska göra ett prov på enheter. Den här funktionen innehåller appen **Gör ett prov** och inställningar för att lägga till en test-URL, välja hur slutanvändare loggar in på provet och mycket mer. Den här funktionen har stöd för följande plattform:

- Windows 10 och senare

När användaren loggar in öppnas automatiskt appen Gör ett prov med det prov som du har angett. Inga andra appar kan köras på enheten medan provet pågår. [Gör prov i Windows 10](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) innehåller mer information om appen Gör ett prov.

Artikeln visar stegen för att skapa en konfigurationsprofil för enheter i Microsoft Intune. Den innehåller även information om du vill läsa och lära dig mer om tillgängliga utbildningsinställningar för Windows 10-enheter.

## <a name="create-a-device-profile"></a>Skapa en enhetsprofil

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

    - **Plattform**: Välj **Windows 10 och senare**.
    - **Profil**: Välj **Begränsad provmiljö (utbildning)** .

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på den nya profilen.
    - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.
7. Ange de inställningar du vill konfigurera i **Konfigurationsinställningar**:

    - [Windows 10 och senare](education-settings-windows.md)

8. Välj **Nästa**.

9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar** väljer du de användare eller den användargrupp som ska få din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

Nästa gång varje enhet checkar in tillämpas principen.

## <a name="next-steps"></a>Nästa steg

Se en lista över [utbildningsinställningarna för Windows 10](education-settings-windows.md) och deras beskrivningar.

När [profilen har tilldelats](device-profile-assign.md) [övervakar du dess status](device-profile-monitor.md).
