---
title: Konfigurera VPN-inställningar för Windows 8.1 Phone-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Lägg till eller skapa en VPN-konfigurationsprofil med hjälp av konfigurationsinställningar för virtuellt privat nätverk (VPN), inklusive anslutningsinformation och proxyinställningar för att inkludera IP- eller FQDN-adress samt TCP-port i Microsoft Intune på enheter med Windows Phone 8.1.
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
ms.openlocfilehash: df05c4b1a7a5ee3f30d33e40620a8a116f508333
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086485"
---
# <a name="add-vpn-settings-on-windows-phone-81-devices-in-microsoft-intune"></a>Lägga till VPN-inställningar för Windows Phone 8.1-enheter i Microsoft Intune

I den här artikeln beskrivs de Intune-inställningar som du kan använda för att konfigurera VPN-anslutningar på enheter som kör Windows Phone 8.1. 

Beroende på vilka inställningar du väljer kan bara vissa värden i följande lista konfigureras.

>[!IMPORTANT]
>VPN-profiler för Windows Phone 8.1 tillämpas även på Windows 10-enheter.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en VPN-enhetskonfigurationsprofil](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Grundläggande VPN-inställningar

- **Tillämpa alla inställningar endast på Windows Phone 8.1**: Konfigurera den här inställningen i den klassiska Intune-portalen. I administrationscentret för Microsoft Endpoint Manager går det inte att ändra den här inställningen. När det är inställt på **Konfigurerad** tillämpas inställningar endast på Windows Phone 8.1-enheter. Om inställningen är **Inte konfigurerad** gäller inställningarna även för Windows 10 Mobile-enheter.
- **Anslutningens namn**: Ange ett namn på anslutningen. Användarna ser det här namnet när de bläddrar på enheten i listan med tillgängliga VPN-anslutningar.
- **Autentiseringsmetod**: Välj hur enheter ska autentiseras mot VPN-servern från:
  - **Certifikat**: Under **Autentiseringscertifikat** väljer du den SCEP- eller PKCS-certifikatprofil som du skapade tidigare för att autentisera anslutningen. Mer information om certifikatprofiler finns i [Så här konfigurerar du certifikat](../protect/certificates-configure.md).
  - **Användarnamn och lösenord**: Slutanvändare måste ange ett användarnamn och lösenord för att logga in på VPN-servern.
- **Servrar**: Lägg till en eller flera VPN-servrar som enheterna ska ansluta till.
  - **Lägg till**: Öppnar bladet **Lägg till rad** där du kan ange följande information:
    - **Beskrivning**: Ange ett beskrivande namn för servern, som t.ex. **Contoso VPN-server**.
    - **IP-adress eller fullständigt domännamn**: Ange IP-adress eller fullständigt domännamn för den VPN-server som enheterna ska ansluta till. Exempel: **192.168.1.1**, **vpn.contoso.com**.
    - **Standardserver**: Gör servern till den standardserver som enheterna använder för att upprätta anslutningen. Du ska endast ange en server som standard.
  - **Importera**: Bläddra till en kommateckenavgränsad fil som innehåller en lista med servrar i formatet: beskrivning, IP-adress eller FQDN, samt standardserver. Välj **OK** för att importera dessa servrar till listan **Servrar**.
  - **Exportera**: Exporterar listan med servrar till en kommateckenavgränsad fil (csv).

- **Kringgå VPN i företagets trådlösa nätverk**: Aktivera det här alternativet om du vill ange att VPN-anslutningen inte ska användas när enheten är ansluten till företagets Wi-Fi-nätverk.
- **Kringgå VPN i trådlöst hemnätverk**: Aktivera det här alternativet om du vill ange att VPN-anslutningen inte ska användas när enheten är ansluten till ett trådlöst hemnätverk.

- **Anslutningstyp**: Välj VPN-anslutningstyp. Alternativen är:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

- **Inloggningsgrupp eller domän** (endast SonicWall Mobile Connect): Ange namnet för den inloggningsgrupp eller domän som du vill ansluta till.
- **Roll** (endast Pulse Secure): Ange namnet för den användarroll som har åtkomst till anslutningen. En användarroll definierar personliga inställningar och alternativ, och aktiverar eller inaktiverar vissa åtkomstfunktioner.
- **Område** (endast Pulse Secure): Ange namnet för den autentiseringssfär som ska användas. En autentiseringssfär är en grupp av autentiseringsresurser som används av Pulse Secure-anslutningstypen.

- **Söklista för DNS-suffix**: **Lägg till** ett eller flera DNS-suffix. Varje DNS-suffix som du anger genomsöks vid anslutning till en webbplats med ett kort namn. Ange exempelvis DNS-suffixen **domain1.contoso.com** och **domain2.contoso.com** och gå till URL:en `http://mywebsite`, så söks URL:erna `http://mywebsite.domain1.contoso.com` och `http://mywebsite.domain2.contoso.com` igenom.

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

- **Identifiera proxyinställningar automatiskt**: Om VPN-servern kräver en proxyserver för anslutningen kan du ange om du vill att enheterna automatiskt ska identifiera anslutningsinställningarna.
- **Automatiskt konfigurationsskript**: Använd en fil för att konfigurera proxyservern. Ange den **Proxyserver-URL** (till exempel `http://proxy.contoso.com`) som innehåller konfigurationsfilen.
- **Använd proxyserver**: Aktivera det här alternativet om du vill ange inställningarna för proxyservern manuellt.
  - **Adress**: Ange proxyserverns adress (som en IP-adress).
  - **Portnummer**: Ange det portnummer som är associerat med proxyservern.
- **Kringgå proxy för lokala adresser**: Om VPN-servern kräver en proxyserver för anslutningen och du inte vill använda proxyservern för de lokala adresser som du anger väljer du det här alternativet.

## <a name="next-steps"></a>Nästa steg

Profilen har skapats, men den gör inte något än. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Konfigurera VPN-inställningar på [Android](vpn-settings-android.md)-, [Android Enterprise](vpn-settings-android-enterprise.md)-, [macOS](vpn-settings-macos.md)- och [Windows 10](vpn-settings-windows-10.md)-enheter.
