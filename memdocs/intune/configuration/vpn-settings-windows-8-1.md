---
title: Konfigurera VPN-inställningar för Windows 8.1-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Lägg till eller skapa en VPN-konfigurationsprofil med hjälp av konfigurationsinställningar för virtuellt privat nätverk (VPN), inklusive anslutningsinformation och proxyinställningar för att inkludera IP- eller FQDN-adress samt TCP-port i Microsoft Intune på enheter som kör Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0f242f336fadf9dd31641849462a5dd24c09e3f
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556361"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>Lägga till VPN-inställningar för Windows 8.1-enheter i Microsoft Intune

I den här artikeln beskrivs de Intune-inställningar som du kan använda för att konfigurera VPN-anslutningar på enheter som kör Windows 8.1.

Beroende på vilka inställningar du väljer kan bara vissa värden i följande lista konfigureras.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en enhetskonfigurationsprofil för Windows 8.1 VPN](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Grundläggande VPN-inställningar

- **Anslutningens namn**: Ange ett namn på anslutningen. Användarna ser det här namnet när de bläddrar på enheten i listan med tillgängliga VPN-anslutningar. Ange till exempel `Contoso VPN`.
- **Servrar**: Lägg till en eller flera VPN-servrar som enheterna ska ansluta till. När du lägger till en server, anger du följande information:
  - **Beskrivning**: Ange ett beskrivande namn för servern, som t.ex. **Contoso VPN-server**.
  - **IP-adress eller fullständigt domännamn**: Ange IP-adressen eller det fullständiga domännamnet för VPN-servern som enheterna ska ansluta till. Ange till exempel `192.168.1.1` eller `vpn.contoso.com`.
  - **Standardserver**: **True** gör servern till den standardserver som enheterna använder för att upprätta anslutningen. Ange endast en server som standard.
  - **Importera**: Bläddra till en kommateckenavgränsad fil som innehåller en lista med servrar i formatet: beskrivning, IP-adress eller FQDN, samt standardserver. Välj **OK** för att importera dessa servrar till listan **Servrar**.
  - **Exportera**: Exporterar listan med servrar till en kommateckenavgränsad fil (csv).

- **Anslutningstyp**: Välj VPN-anslutningstyp. Alternativen är:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **Inloggningsgrupp eller domän** (endast SonicWall Mobile Connect): Ange namnet för den inloggningsgrupp eller domän som du vill ansluta till.

- **Roll** (endast Pulse Secure): Ange namnet för den användarroll som har åtkomst till anslutningen. En användarroll definierar personliga inställningar och alternativ, och aktiverar eller inaktiverar vissa åtkomstfunktioner.

- **Område** (endast Pulse Secure): Ange namnet för den autentiseringssfär som ska användas. En autentiseringssfär är en grupp av autentiseringsresurser som används av Pulse Secure-anslutningstypen.

- **Anpassad XML**: Ange anpassade XML-kommandon som konfigurerar VPN-anslutningen.

  **Pulse Secure-exempel**:

  ```xml
  <pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
  ```

  **Kontrollpunkt för mobilt VPN-exempel**:

  ```xml
  <CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
  ```

  **SonicWall Mobile Connect-exempel**:

  ```xml
  <MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
  ```

  **F5 Edge Client-exempel**:

  ```xml
  <f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
  ```

  Mer information om hur du skriver anpassade XML-kommandon finns i tillverkarens VPN-dokumentation.

- **Delade tunnlar**: **Aktivera** gör att enheterna kan bestämma vilken anslutning som ska användas beroende på trafiken. En användare på ett hotell kan till exempel använda VPN-anslutningen för att komma åt arbetsfiler, men använda hotellets standardnätverk för vanlig webbsurfning. Om du vill att all trafik ska att använda VPN-tunneln när VPN-anslutningen är aktiv väljer du **Inaktivera**.

## <a name="proxy-settings"></a>Proxyinställningar

- **Automatiskt konfigurationsskript**: Använd en fil för att konfigurera proxyservern. Ange den **URL för proxyserver** som innehåller konfigurationsfilen. Ange till exempel `http://proxy.contoso.com`.
- **Adress**: Ange proxyserverns adress såsom en IP-adress eller `vpn.contoso.com`.
- **Portnummer**: Ange TCP-portnumret som används av proxyservern.
- **Identifiera proxyinställningar automatiskt**: Om VPN-servern kräver en proxyserver för anslutningen kan du ange om du vill att enheterna automatiskt ska identifiera anslutningsinställningarna. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Aktivera**: Identifierar automatiskt anslutningsinställningarna.
  - **Inaktivera**: Identifierar inte anslutningsinställningarna automatiskt.
- **Kringgå proxy för lokala adresser**: Välj att använda proxyservern för lokala adresser. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Aktivera**: Använd inte en proxyserver för lokala adresser.
  - **Inaktivera**: Använd en proxyserver för lokala adresser.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Konfigurera VPN-inställningar på [Android](vpn-settings-android.md)-, [Android Enterprise](vpn-settings-android-enterprise.md)-, [macOS](vpn-settings-macos.md)- och [Windows 10](vpn-settings-windows-10.md)-enheter.
