---
title: Använd VPN-inställningar för Android-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Se alla inställningar för att skapa VPN-anslutningar på Android-enheter i Microsoft Intune. Ange anslutningsnamn, IP-adress eller FQDN för VPN-servern, välj hur användare autentiseras och välj anslutningstyperna Citrix, SonicWall, Check Point Capsule och Pulse Secure.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b43b9671767a2d67bb98db6150799d266fe9fa6
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086566"
---
# <a name="android-device-settings-to-configure-vpn-in-intune"></a>Inställningar för Android-enhet för att konfigurera VPN i Intune

Den här artikeln beskriver de olika inställningar för VPN-anslutningar som du kan styra på Android-enheter. Som en del av din lösning för hantering av mobila enheter (MDM) använder du de här inställningarna för att skapa en VPN-anslutning, välja hur VPN-autentiseringen ska autentiseras, välja en VPN-servertyp med mera.

Som Intune-administratör kan du skapa och tilldela VPN-inställningar till dina Android-enheter. 

Mer information om VPN-profiler i Intune finns i [VPN-profiler](vpn-settings-configure.md).

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en profil för enhetskonfiguration](vpn-settings-configure.md) och välj **Android-enhetsadministratör**.

## <a name="base-vpn"></a>Bas-VPN

- **Anslutningens namn**: Ange ett namn på anslutningen. Slutanvändarna ser det här namnet när de bläddrar på enheten efter tillgängliga VPN-anslutningar. Ange till exempel `Contoso VPN`.
- **IP-adress eller fullständigt domännamn**: Ange IP-adressen eller det fullständiga domännamnet för VPN-servern som enheterna ska ansluta till. Ange till exempel **192.168.1.1** eller **vpn.contoso.com**.

  - **Autentiseringsmetod**: Välj hur enheter autentiserar mot VPN-servern. Alternativen är:

    - **Certifikat**: Välj en befintlig SCEP- eller PKCS-certifikatprofil för att autentisera anslutningen. [Konfigurera certifikat](../protect/certificates-configure.md) visar stegen för att skapa en certifikatprofil.
    - **Användarnamn och lösenord**: Vid inloggning till VPN-servern uppmanas slutanvändarna att ange ett användarnamn och lösenord.

- **Anslutningstyp**: Välj VPN-anslutningstyp. Alternativen är:

  - **Check Point Capsule VPN**
  - **Cisco AnyConnect**
  - **SonicWall Mobile Connect**
  - **F5 Access**
  - **Pulse Secure**
  - **Citrix SSO**

- **Fingeravtryck** (endast Check Point Capsule VPN): Ange en sträng, till exempel **Contoso fingeravtryckskod**, för att verifiera att VPN-servern är betrodd. Ett fingeravtryck skickas till klienten så att klienten kan lita på alla servrar som har samma fingeravtryck. Om enheten inte har fingeravtrycket uppmanar den användaren att lita på VPN-servern medan fingeravtrycket visas. Användaren verifierar fingeravtrycket manuellt och väljer betrodd för att ansluta.
- **Ange nyckel och värdepar för Citrix VPN-attributen** (endast Citrix): Ange nyckel och värdepar som tillhandahålls av Citrix. Dessa värden konfigurerar egenskaperna för VPN-anslutningen. 

  Du kan också **Importera** en fil med kommaavgränsade värden (csv) med nycklar och värdepar. Se till att granska egenskaperna **Data innehåller rubriker** och **Nyckel**.

  När du har lagt till din nyckel och dina värdepar använder du **Exportera** för att säkerhetskopiera dina data till en csv-fil.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Du kan också skapa VPN-profiler för [Android Enterprise](vpn-settings-android-enterprise.md)-, [iOS/iPad](vpn-settings-ios.md)-, [macOS](vpn-settings-macos.md)-, [Windows 10 och senare](vpn-settings-windows-10.md)-, [Windows 8.1](vpn-settings-windows-8-1.md)- och [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md)-enheter.
