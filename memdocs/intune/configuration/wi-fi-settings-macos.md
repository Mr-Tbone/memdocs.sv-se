---
title: Konfigurera Wi-Fi-inställningar för macOS-enheter i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Skapa eller lägg till en Wi-Fi-enhetskonfigurationsprofil för macOS-enheter. Se de olika inställningarna, lägg till certifikat, välj en EAP-typ och välj en autentiseringsmetod i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/10/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e1cd60b8a9a8612034972e8357d2e346d194ca3a
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85092879"
---
# <a name="add-wi-fi-settings-for-macos-devices-in-microsoft-intune"></a>Lägga till Wi-Fi-inställningar för macOS-enheter i Microsoft Intune

Du kan skapa en profil med specifika Wi-Fi-inställningar och sedan distribuera profilen till dina macOS-enheter. Microsoft Intune innehåller många funktioner, inklusive autentisering till ditt nätverk, lägga till ett PKCS- eller ett SCEP-certifikat och mycket mer.

Dessa Wi-Fi-inställningar är indelade i två kategorier: Grundinställningar och företagsinställningar.

Den här artikeln beskriver dessa inställningar.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en enhetsprofil](wi-fi-settings-configure.md).

> [!NOTE]
> De här inställningarna är tillgängliga för alla registreringstyper. Mer information om registreringstyperna finns i [macOS-registrering](../enrollment/macos-enroll.md).

## <a name="basic-profiles"></a>Grundläggande profiler

Grundläggande eller personliga profiler använder WPA/WPA2 till att skydda Wi-Fi-anslutningen på enheter. Normalt används WPA/WPA2 i hemnätverk eller personliga nätverk. Du kan också lägga till en i förväg delad nyckel för att autentisera anslutningen.

- **Wi-Fi-typ**: Välj **Basic**.
- **Nätverksnamn**: Ange ett namn på Wi-Fi-anslutningen. Detta värde är det namn som användarna ser när de bläddrar i listan med tillgängliga anslutningar på sin enhet.
- **SSID**: Förkortning för **Service Set Identifier**. Den här egenskapen är det verkliga namnet på det trådlösa nätverk som enheterna ansluter till. Användarna ser dock bara det nätverksnamn som du konfigurerade när de väljer anslutningen.
- **Anslut automatiskt**: Välj **Aktivera** för att ansluta till nätverket automatiskt när enheten är i närheten. Välj **Inaktivera** för att förhindra att enheter ansluts automatiskt.
- **Dolt nätverk**: Välj **Aktivera** för att dölja nätverket i listan med tillgängliga nätverk på enheten. SSID skickas inte. Välj **Inaktivera** för att visa nätverket i listan med tillgängliga nätverk på enheten.
- **Säkerhetstyp**: Välj det säkerhetsprotokoll som ska autentiseras med Wi-Fi-nätverket. Alternativen är:

  - **Öppet (ingen autentisering)** : Använd bara det här alternativet om nätverket är oskyddat.
  - **WPA/WPA2 – Personal**: Ange lösenordet i **I förväg delad nyckel**. När nätverket är konfigurerat, konfigureras också ett lösenord eller en nätverksnyckel. Ange lösenordet eller nätverksnyckeln för PSK-värdet.
  - **WEP**

- **Proxyinställningar**: Alternativen är:
  - **Inga**: Inga proxyinställningar konfigureras.
  - **Manuell**: Ange **Proxyserveradress** som en IP-adress och dess **Portnummer**.
  - **Automatiskt**: Använd en fil för att konfigurera proxyservern. Ange den **Proxyserver-URL** (till exempel `http://proxy.contoso.com`) som innehåller konfigurationsfilen.

## <a name="enterprise-profiles"></a>Företagsprofiler

Företagsprofiler använder EAP (Extensible Authentication Protocol) för autentisering av Wi-Fi-anslutningar. EAP används ofta av företag eftersom du kan använda certifikat till att autentisera och skydda anslutningar och konfigurera fler säkerhetsalternativ.

- **Wi-Fi-typ**: Välj **Företag**.
- **SSID**: Förkortning för **Service Set Identifier**. Den här egenskapen är det verkliga namnet på det trådlösa nätverk som enheterna ansluter till. Användarna ser dock bara det nätverksnamn som du konfigurerade när de väljer anslutningen.
- **Anslut automatiskt**: Välj **Aktivera** för att ansluta till nätverket automatiskt när enheten är i närheten. Välj **Inaktivera** för att förhindra att enheter ansluts automatiskt.
- **Dolt nätverk**: Välj **Aktivera** för att dölja nätverket i listan med tillgängliga nätverk på enheten. SSID skickas inte. Välj **Inaktivera** för att visa nätverket i listan med tillgängliga nätverk på enheten.

- **EAP-typ**: Välj den EAP-typ (Extensible Authentication Protocol) som används för att autentisera säkra trådlösa anslutningar. Alternativen är:

  - **EAP-FAST**: Ange **PAC-inställningar (Protected Access Credential)** . Det här alternativet använder autentiseringsuppgifter för skyddad åtkomst till att skapa en autentiserad tunnel mellan klienten och autentiseringsservern. Alternativen är:
    - **Använd inte (PAC)**
    - **Använd (PAC)** : Om det finns en befintlig PAC-fil använder du den.
    - **Använd och etablera PAC**: Skapar och lägger till PAC-filen till enheterna.
    - **Använd och etablera PAC anonymt**: Skapa och lägg till PAC-filen i dina enheter utan att autentisera till servern.

  - **EAP-SIM**

  - **EAP-TLS**: Ange även:

    - **Serverförtroende** - **Certifikatservernamn**: **Lägg till** ett eller flera gemensamma namn som används i de certifikat som utfärdats av en betrodd certifikatutfärdare (CA). När du anger den här informationen kan du hoppa över fönstret för dynamiskt förtroende som visas på användarenheter när de ansluter till Wi-Fi-nätverket.
    - **Rotcertifikat för serververifiering**: Välj en eller flera befintliga betrodda rotcertifikatsprofiler. De här certifikaten presenteras för servern när klienten ansluter till nätverket. De autentiserar anslutningen.

    - **Klientautentisering** - **Klientcertifikat för klientautentisering (identitetscertifikat)** : Välj den SCEP- eller PKCS-profil för klientcertifikatet som även distribueras till enheten. Det här certifikatet är den identitet som presenterades av enheten till servern när anslutningen autentiserades.

  - **EAP-TTLS**: Ange även:

    - **Serverförtroende** - **Certifikatservernamn**: **Lägg till** ett eller flera gemensamma namn som används i de certifikat som utfärdats av en betrodd certifikatutfärdare (CA). När du anger den här informationen kan du hoppa över fönstret för dynamiskt förtroende som visas på användarenheter när de ansluter till Wi-Fi-nätverket.
    - **Rotcertifikat för serververifiering**: Välj en eller flera befintliga betrodda rotcertifikatsprofiler. De här certifikaten presenteras för servern när klienten ansluter till nätverket. De autentiserar anslutningen.

    - **Klientautentisering** – Välj en **Autentiseringsmetod**. Alternativen är:

      - **Användarnamn och lösenord**: Be användaren ange ett användarnamn och ett lösenord för att autentisera anslutningen. Ange även:
        - **Annan metod än EAP (inre identitet)** : Välj hur du ska autentisera anslutningen. Du måste välja samma protokoll som är konfigurerat på ditt Wi-Fi-nätverk.

          Alternativen är: **Okrypterat lösenord (PAP)** , **CHAP (Challenge Handshake Authentication Protocol)** , **MS-CHAP (Microsoft CHAP)** eller **MS-CHAP v2 (Microsoft CHAP Version 2)**

      - **Certifikat**: Välj den SCEP- eller PKCS-profil för klientcertifikatet som även distribueras till enheten. Det här certifikatet är den identitet som presenterades av enheten till servern när anslutningen autentiserades.

      - **Identitetssekretess (yttre identitet)** : Ange den text som ska skickas som svar på en begäran om EAP-identitet. Den här texten kan ha vilket värde som helst, t.ex. `anonymous`. Vid autentisering skickas den här anonyma identiteten från början och sedan följs den av den verkliga identifieringen som skickas i en säker tunnel.

  - **LEAP**

  - **PEAP**: Ange även:

    - **Serverförtroende** - **Certifikatservernamn**: **Lägg till** ett eller flera gemensamma namn som används i de certifikat som utfärdats av en betrodd certifikatutfärdare (CA). När du anger den här informationen kan du hoppa över fönstret för dynamiskt förtroende som visas på användarenheter när de ansluter till Wi-Fi-nätverket.
    - **Rotcertifikat för serververifiering**: Välj en eller flera befintliga betrodda rotcertifikatsprofiler. De här certifikaten presenteras för servern när klienten ansluter till nätverket. De autentiserar anslutningen.

    - **Klientautentisering** – Välj en **Autentiseringsmetod**. Alternativen är:

      - **Användarnamn och lösenord**: Be användaren ange ett användarnamn och ett lösenord för att autentisera anslutningen. 

      - **Certifikat**: Välj den SCEP- eller PKCS-profil för klientcertifikatet som även distribueras till enheten. Det här certifikatet är den identitet som presenterades av enheten till servern när anslutningen autentiserades.

      - **Identitetssekretess (yttre identitet)** : Ange den text som ska skickas som svar på en begäran om EAP-identitet. Den här texten kan ha vilket värde som helst, t.ex. `anonymous`. Vid autentisering skickas den här anonyma identiteten från början och sedan följs den av den verkliga identifieringen som skickas i en säker tunnel.

- **Proxyinställningar**: Alternativen är:
  - **Inga**: Inga proxyinställningar konfigureras.
  - **Manuell**: Ange **Proxyserveradress** som en IP-adress och dess **Portnummer**.
  - **Automatiskt**: Använd en fil för att konfigurera proxyservern. Ange den **Proxyserver-URL** (till exempel `http://proxy.contoso.com`) som innehåller konfigurationsfilen.

## <a name="next-steps"></a>Nästa steg

Profilen har skapats, men den gör inte något än. Därefter [tilldelar du profilen](device-profile-assign.md) och [övervakar dess status](device-profile-monitor.md).

Konfigurera Wi-Fi-inställningar på [Android](wi-fi-settings-android.md), [Android Enterprise](wi-fi-settings-android-enterprise.md), [iOS/iPadOS](wi-fi-settings-ios.md)och [Windows 10](wi-fi-settings-windows.md)-enheter.
