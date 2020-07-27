---
title: Skapa en Wi-Fi-profil för enheter i Microsoft Intune – Azure | Microsoft Docs
description: Se stegen för att skapa en konfigurationsprofil för Wi-Fi-enheter i Microsoft Intune. Skapa profiler för Android-enhetsadministratör, Android Enterprise, Android Kiosk, iOS, iPadOS, macOS, Windows 10 och senare, samt Windows Holographic for Business. Använd de här profilerna till att skapa en Wi-Fi-anslutning som ska använda certifikat, välja en EAP-typ, välja en autentiseringsmetod, aktivera en proxy och mycket mer.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 25b07dcbb76f6d4a8aae964d0123a880d179784e
ms.sourcegitcommit: 2e0bc4859f7e27dea20c6cc59d537a31f086c019
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/21/2020
ms.locfileid: "86871941"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>Lägga till och använda Wi-Fi-inställningar på dina enheter i Microsoft Intune

Wi-Fi är ett trådlöst nätverk som används av många mobila enheter för att få åtkomst till nätverket. Microsoft Intune innehåller inbyggda Wi-Fi-inställningar som kan distribueras till användare och enheter i din organisation. Den här gruppen med inställningar kallas en ”profil” och kan tilldelas till olika användare och grupper. När den har tilldelats får användare tillgång till organisationens Wi-Fi-nätverk, utan att de behöver konfigurera något själva.

Anta till exempel att du installerar ett nytt Wi-Fi-nätverk som heter Contoso Wi-Fi. Du vill sedan konfigurera att alla iOS/iPadOS-enheter kan ansluta till nätverket. Så här ser processen ut:

1. Skapa en Wi-Fi-profil som innehåller inställningar som ansluter till det trådlösa nätverket Contoso Wi-Fi.
2. Tilldela profilen till en grupp som innehåller alla användare av iOS/iPadOS-enheter.
3. På enheterna hittar användarna det nya Contoso Wi-Fi-nätverket i listan med trådlösa nätverk. De kan sedan ansluta till nätverket med hjälp av den autentiseringsmetod som du har valt.

Den här artikeln visar stegen för att skapa en Wi-Fi-profil. Den innehåller även länkar som beskriver de olika inställningarna för varje plattform.

## <a name="supported-device-platforms"></a>Mobila enhetsplattformar som stöds

Wi-Fi-profiler stöder följande enhetsplattformar:

- Android 5 och senare
- Android Enterprise och Kiosk
- iOS 11.0 och senare
- iPadOS 13.0 och senare
- macOS X 10.12 och senare
- Windows 10 och senare, Windows 10 Mobile och Windows Holographic for Business

> [!NOTE]
> För enheter som kör Windows 8.1 kan du importera en Wi-Fi-konfiguration som tidigare har exporterats från en annan enhet.

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

    - **Profil**: Välj **Wi-Fi**.

      > [!TIP]
      >
      > - För **Android Enterprise**-enheter som körs som en dedikerad enhet (kiosk) väljer du **Fullständigt hanterad, Dedikerad och Företagsägd arbetsprofil** > **Wi-Fi**.
      > - För **Windows 8.1 och senare** kan du välja **Wi-Fi-import**. Med det alternativet kan du importera en XML-fil med Wi-Fi-inställningarna, som du tidigare har exporterat från en annan enhet.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ett bra profilnamn är t.ex. **WiFi-profil för hela företaget**.
    - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.
7. Under **Konfigurationsinställningar**  visas olika inställningar du kan konfigurera beroende på vilken plattform du väljer. Välj din plattform för detaljerade inställningar:

    - [Android-enhetsadministratör](wi-fi-settings-android.md)
    - [Android Enterprise](wi-fi-settings-android-enterprise.md), inklusive dedikerade enheter
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 och senare](wi-fi-settings-windows.md)
    - [Windows 8.1 och senare](wi-fi-settings-import-windows-8-1.md), inklusive Windows Holographic for Business

8. Välj **Nästa**.
9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar** väljer du de användare eller grupper som ska ta emot din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

> [!TIP]
> Om du använder certifikatbaserad autentisering för din Wi-Fi-profil distribuerar du Wi-Fi-profilen, certifikatprofilen och profilen för betrodd rot till samma grupper för att säkerställa att varje enhet kan verifiera din certifikatutfärdare.  Mer information finns i [Konfigurera certifikat med Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Nästa steg

Profilen skapas, men den kanske inte gör någonting. Därefter [tilldelar du profilen](device-profile-assign.md) och [övervakar dess status.](device-profile-monitor.md)

[Problem med Wi-Fi-profiler i Intune](troubleshoot-wi-fi-profiles.md).
