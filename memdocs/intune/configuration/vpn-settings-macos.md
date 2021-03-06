---
title: Konfigurera VPN-inställningar för macOS-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Lägg till eller skapa en VPN-konfigurationsprofil, inklusive anslutningsinformation, delade tunnlar, anpassade VPN-inställningar med identifierare, nyckel- och värdepar, proxyinställningar med ett konfigurationsskript, IP- eller FQDN-adress och TCP-port i Microsoft Intune på enheter som kör macOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b7bcb685a33bc8d06226b51aaa051656360b436d
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88819957"
---
# <a name="add-vpn-settings-on-macos-devices-in-microsoft-intune"></a>Lägg till VPN-inställningar för macOS-enheter i Microsoft Intune

I den här artikeln beskrivs de Intune-inställningar som du kan använda till att konfigurera VPN-anslutningar på enheter som kör macOS.

Beroende på vilka inställningar du väljer kan bara vissa värden i följande lista konfigureras.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en enhetskonfigurationsprofil](vpn-settings-configure.md).

> [!NOTE]
> De här inställningarna är tillgängliga för alla registreringstyper. Mer information om registreringstyperna finns i [macOS-registrering](../enrollment/macos-enroll.md).

## <a name="base-vpn-settings"></a>Grundläggande VPN-inställningar

**Anslutningsnamn**: Ange ett namn på anslutningen. Slutanvändarna ser det här namnet när de bläddrar på enheten i listan över tillgängliga VPN-anslutningar.

- **IP-adress eller fullständigt domännamn**: Ange IP-adress eller fullständigt domännamn för den VPN-server som enheterna ska ansluta till. Ange till exempel `192.168.1.1` eller `vpn.contoso.com`.
- **Autentiseringsmetod**: Välj hur enheter autentiserar mot VPN-servern. Alternativen är:
  - **Certifikat**: Under **Autentiseringscertifikat** väljer du den SCEP- eller PKCS-certifikatprofil som du skapade tidigare för att autentisera anslutningen. Mer information om certifikatprofiler finns i [Så här konfigurerar du certifikat](../protect/certificates-configure.md).
  - **Användarnamn och lösenord**: Slutanvändare måste ange ett användarnamn och lösenord för att logga in på VPN-servern.
- **Anslutningstyp**: Välj VPN-anslutningstypen från följande leverantörslista:
  - **Check Point Capsule VPN**
  - **Cisco AnyConnect**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **NetMotion Mobility**
  - **Pulse Secure**
  - **Anpassat VPN**: Välj det här alternativet om VPN-leverantören inte visas i listan. Konfigurera också:

    - **VPN-identifierare**: Ange en identifierare för den VPN-app som du använder. Den här identifieraren tillhandahålls av din VPN-provider.
    - **Ange nyckel/värdepar för de anpassade VPN-attributen** Lägg till eller importera **Nycklar** och **Värden** som anpassar VPN-anslutningen. Dessa värden tillhandahålls vanligtvis av VPN-leverantören.

- **Delade tunnlar**: **Aktivera** eller **Inaktivera** det här alternativet för att låta enheterna bestämma vilken anslutning som ska användas beroende på trafiken. En användare på ett hotell kan till exempel använda VPN-anslutningen för att komma åt arbetsfiler, men använda hotellets standardnätverk för vanlig webbsurfning.

<!--- **Per-app VPN** - Select this option if you want to associate this VPN connection with an iOS/iPadOS or macOS app so that the connection will be opened when the app is run. You can associate the VPN profile with an app when you assign the software. For more information, see [How to assign and monitor apps](../apps/apps-deploy.md). --->

## <a name="proxy-settings"></a>Proxyinställningar

- **Automatiskt konfigurationsskript**: Använd en fil för att konfigurera proxyservern. Ange den **URL för proxyserver** som innehåller konfigurationsfilen. Ange till exempel `http://proxy.contoso.com`.
- **Adress**: Ange proxyserverns adress (som en IP-adress).
- **Portnummer**: Ange det portnummer som är associerat med proxyservern.

## <a name="next-steps"></a>Nästa steg

Profilen skapas, men den kanske inte gör något än. Kom ihåg att [tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Konfigurera VPN-inställningar på [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [iOS/iPadOS](vpn-settings-ios.md) och [Windows 10](vpn-settings-windows-10.md)-enheter.
