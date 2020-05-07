---
title: Lägga till VPN-inställningar för enheter i Microsoft Intune – Azure | Microsoft Docs
description: För Android-enhetsadministratör-, Android Enterprise-, iOS-, iPadOS-, macOS- och Windows-enheter använder du inbyggda inställningar för att skapa anslutningar för virtuella privata nätverk (VPN) i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 70b0c5693c22b6504016d85e35977c5f99935742
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587204"
---
# <a name="create-vpn-profiles-to-connect-to-vpn-servers-in-intune"></a>Skapa VPN-profiler för att ansluta till VPN-servrar i Intune

Virtuella privata nätverk (VPN) ger användarna säker fjärråtkomst till företagets nätverk. Enheter använder en VPN-anslutningsprofil för att initiera en anslutning till VPN-servern. **VPN-profiler** i Microsoft Intune tilldelar VPN-inställningar till användare och enheter i din organisation så att de enkelt och säkert kan ansluta till nätverket.

Exempel: Du vill konfigurera alla enheter som kör iOS/iPadOS med de inställningar som krävs för att ansluta till en filresurs i företagsnätverket. Du skapar en VPN-profil som innehåller de här inställningarna. Sedan tilldelar du den här profilen till alla användare som har iOS/iPadOS-enheter. Användarna ser VPN-anslutningen i listan med tillgängliga nätverk och kan enkelt ansluta.

> [!NOTE]
> Du kan använda [anpassade konfigurationsprinciper i Intune](custom-settings-configure.md) för att skapa VPN-profiler för följande plattformar:
>
> * Android 4 och senare
> * Registrerade enheter som kör Windows 8.1 och senare
> * Windows Phone 8.1 och senare
> * Registrerade enheter som kör Windows 10 desktop och senare
> * Windows 10 Mobil
> * Windows 10 Holographic for Business

## <a name="vpn-connection-types"></a>VPN-anslutningstyper

Du kan skapa VPN-profiler med följande anslutningstyper:

- Automatiskt
  - Windows 10

- Check Point Capsule VPN
  - Android-enhetsadministratör
  - Android Enterprise-arbetsprofiler
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8,1
  - Windows Phone 8.1

- Cisco AnyConnect
  - Android-enhetsadministratör
  - Android Enterprise-arbetsprofiler
  - Ägare av Android Enterprise-enhet (helt hanterad)
  - iOS/iPadOS
  - macOS

- Cisco (IPSec)
  - iOS/iPadOS

- Citrix SSO
  - Android-enhetsadministratör
  - Android Enterprise-arbetsprofiler: Använd [konfigurationsprincip för app](../apps/app-configuration-policies-use-android.md)
  - Ägare av Android Enterprise-enhet (helt hanterad): Använd [konfigurationsprincip för app](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS
  - Windows 10

- Anpassat VPN
  - iOS/iPadOS
  - macOS

  Skapa anpassade VPN-profiler med hjälp av URI-inställningarna i [Skapa en profil med anpassade inställningar](custom-settings-configure.md).

- F5 Access
  - Android-enhetsadministratör
  - Android Enterprise-arbetsprofiler
  - Ägare av Android Enterprise-enhet (helt hanterad)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8,1
  - Windows Phone 8.1

- IKEv2
  - iOS/iPadOS
  - Windows 10

- L2TP
  - Windows 10

- Palo Alto Networks GlobalProtect
  - Android Enterprise-arbetsprofiler: Använd [konfigurationsprincip för app](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS
  - Windows 10

- PPTP
  - Windows 10

- Pulse Secure
  - Android-enhetsadministratör
  - Android Enterprise-arbetsprofiler
  - Ägare av Android Enterprise-enhet (helt hanterad)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8,1
  - Windows Phone 8.1

- SonicWall Mobile Connect
  - Android-enhetsadministratör
  - Android Enterprise-arbetsprofiler
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8,1
  - Windows Phone 8.1

- Zscaler
  - Android Enterprise-arbetsprofiler: Använd [konfigurationsprincip för app](../apps/app-configuration-policies-use-android.md)
  - iOS/iPadOS

> [!IMPORTANT]
> Innan du kan använda de VPN-profiler som har tilldelats till en enhet måste du installera lämplig VPN-app för profilen. Information om hur du tilldelar appen med Intune finns i [Vad är apphantering i Microsoft Intune?](../apps/app-management.md).  

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

    - **Plattform**: Välj plattform för dina enheter. Alternativen är:
      - **Android-enhetsadministratör**
      - **Android Enterprise** > **endast enhetsägare**
      - **Android Enterprise** > **endast arbetsprofil**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 och senare**
      - **Windows 8.1 och senare**
      - **Windows Phone 8.1**
    - **Profil**: Välj **VPN**.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ett bra profilnamn är t.ex. **VPN-profil för hela företaget**.
    - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.
7. Under **Konfigurationsinställningar**  visas olika inställningar du kan konfigurera beroende på vilken plattform du väljer. Välj din plattform för detaljerade inställningar:

    - [Android-enhetsadministratör](vpn-settings-android.md)
    - [Android enterprise](vpn-settings-android-enterprise.md)
    - [iOS/iPadOS](vpn-settings-ios.md)
    - [macOS](vpn-settings-macos.md)
    - [Windows 10](vpn-settings-windows-10.md) (inklusive Windows Holographic for Business)
    - [Windows 8.1](vpn-settings-windows-8-1.md)
    - [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md)

8. Välj **Nästa**.
9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar** väljer du de användare eller grupper som ska ta emot din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

## <a name="secure-your-vpn-profiles"></a>Skydda dina VPN-profiler

VPN-profiler kan använda ett antal olika anslutningstyper och protokoll från olika tillverkare. Dessa anslutningar skyddas vanligtvis med följande metoder.

### <a name="certificates"></a>Certifikat

När du skapar VPN-profilen väljer du en SCEP- eller PKCS-certifikatprofil som du tidigare har skapat i Intune. Profilen kallas för identitetscertifikat. Det används för att autentisera mot en betrodd certifikatprofil (eller ett *rotcertifikat*) som du har skapat för att användarens enhet ska få ansluta. Det betrodda certifikatet tilldelas datorn som autentiserar VPN-anslutningen, vanligtvis VPN-servern.

Om du använder certifikatbaserad autentisering för din VPN-profil distribuerar du VPN-profilen, certifikatprofilen och profilen för betrodd rot till samma grupper för att säkerställa att varje enhet kan verifiera din certifikatutfärdare.

Mer information om hur du skapar och använder certifikatprofiler i Intune finns i [Konfigurera certifikat i Microsoft Intune](../protect/certificates-configure.md).

### <a name="user-name-and-password"></a>Användarnamn och lösenord

Användaren autentiseras mot VPN-servern genom att ange användarnamn och lösenord.

## <a name="next-steps"></a>Nästa steg

När profilen har skapats gör den ingenting ännu. Härefter [tilldelar du profilen](device-profile-assign.md) till några enheter och [övervakar dess status](device-profile-monitor.md).

Du kan också skapa och använda VPN per app på [Android-enhetsadministratörs-/Android Enterprise-](android-pulse-secure-per-app-vpn.md) och [iOS/iPadOS](vpn-setting-configure-per-app.md)-enheter.
