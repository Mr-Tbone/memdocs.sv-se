---
title: Använd VPN-inställningar för Android Enterprise i Microsoft Intune – Azure | Microsoft Docs
description: Visa alla inställningar för att skapa VPN-anslutningar på Android Enterprise-enheter i Microsoft Intune. Ange anslutningsnamn, IP-adress eller FQDN för VPN-servern, välj hur användare autentiseras och välj anslutningstyperna Citrix, SonicWall, Check Point Capsule och Pulse Secure.
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
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 87e6484939324abc5566386ffbe48f04ddbbe100
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146464"
---
# <a name="android-enterprise-device-settings-to-configure-vpn-in-intune"></a>Inställningar för Android Enterprise-enhet för att konfigurera VPN i Intune

Den här artikeln beskriver de olika inställningar för VPN-anslutningar som du kan styra på Android Enterprise-enheter. Som en del av din lösning för hantering av mobila enheter (MDM) använder du de här inställningarna för att skapa en VPN-anslutning, välja hur VPN-autentiseringen ska autentiseras, välja en VPN-servertyp med mera.

Som Intune-administratör kan du skapa och tilldela VPN-inställningar till dina Android Enterprise-enheter. 

Mer information om VPN-profiler i Intune finns i [VPN-profiler](vpn-settings-configure.md).

> [!NOTE]
> Om du vill konfigurera Always-on-VPN måste du skapa en VPN-profil och en profil för [enhets begränsningar](device-restrictions-android-for-work.md#connectivity) med inställningen Always-on VPN konfigurerad.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en profil för enhetskonfiguration](vpn-settings-configure.md) och välj **Android Enterprise**.

## <a name="fully-managed-dedicated-and-corporate-owned-work-profile"></a>Fullständigt hanterad, Dedikerad och Företagsägd arbetsprofil

- **Anslutningsnamn**: Ange ett namn på anslutningen. Slutanvändarna ser det här namnet när de bläddrar på enheten efter tillgängliga VPN-anslutningar. Ange till exempel `Contoso VPN`.
- **IP-adress eller fullständigt domännamn**: Ange IP-adressen eller det fullständiga domännamnet för VPN-servern som enheterna ska ansluta till. Ange till exempel **192.168.1.1** eller **vpn.contoso.com**.

  - **Autentiseringsmetod**: Välj hur enheter autentiserar mot VPN-servern. Alternativen är:
  
    - **Certifikat**:Välj en befintlig SCEP- eller PKCS-certifikatprofil för att autentisera anslutningen. [Konfigurera certifikat](../protect/certificates-configure.md) visar stegen för att skapa en certifikatprofil.
    - **Användarnamn och lösenord**: Vid inloggning till VPN-servern uppmanas slutanvändarna att ange ett användarnamn och lösenord.

- **Anslutningstyp**: Välj VPN-anslutningstyp. Alternativen är:

  - **Cisco AnyConnect**
  - **F5 Access**
  - **Pulse Secure**

## <a name="work-profile-only"></a>Endast arbetsprofil

- **Anslutningsnamn**: Ange ett namn på anslutningen. Slutanvändarna ser det här namnet när de bläddrar på enheten efter tillgängliga VPN-anslutningar. Ange till exempel `Contoso VPN`.
- **IP-adress eller fullständigt domännamn**: Ange IP-adressen eller det fullständiga domännamnet för VPN-servern som enheterna ska ansluta till. Ange till exempel **192.168.1.1** eller **vpn.contoso.com**.

  - **Autentiseringsmetod**: Välj hur enheter autentiserar mot VPN-servern. Alternativen är:
  
    - **Certifikat**:Välj en befintlig SCEP- eller PKCS-certifikatprofil för att autentisera anslutningen. [Konfigurera certifikat](../protect/certificates-configure.md) visar stegen för att skapa en certifikatprofil.
    - **Användarnamn och lösenord**: Vid inloggning till VPN-servern uppmanas slutanvändarna att ange ett användarnamn och lösenord.

- **Anslutningstyp**: Välj VPN-anslutningstyp. Alternativen är:

  - **Cisco AnyConnect**
  - **F5 Access**
  - **Pulse Secure**
  - **SonicWall Mobile Connect**
  - **Check Point Capsule VPN**

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Du kan också skapa VPN-profiler för [Android](vpn-settings-android.md), [iOS/iPad](vpn-settings-ios.md), [macOS](vpn-settings-macos.md), [Windows 10 och senare](vpn-settings-windows-10.md) och [Windows 8.1](vpn-settings-windows-8-1.md).
