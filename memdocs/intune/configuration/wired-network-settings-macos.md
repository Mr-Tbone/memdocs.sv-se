---
title: Konfigurera inställningar för fast nätverk för macOS-enheter i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Skapa eller lägg till en enhetskonfigurationsprofil för fast nätverk för macOS-enheter. Se de olika inställningarna, lägg till certifikat, välj en EAP-typ och välj en autentiseringsmetod i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1da738611dd5fe114054645170d2b49ef12f0523
ms.sourcegitcommit: e8076576f5c0ea7e72358d233782f8c38c184c8f
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87334614"
---
# <a name="add-wired-network-settings-for-macos-devices-in-microsoft-intune"></a>Lägga till inställningar för kabelanslutna nätverk för macOS-enheter i Microsoft Intune

Du kan skapa en profil med specifika inställningar för fast nätverk och sedan distribuera profilen till dina macOS-enheter. Microsoft Intune innehåller många funktioner, inklusive autentisering till ditt nätverk, lägga till ett SCEP-certifikat och mycket mer.

I den här artikeln beskrivs de inställningar du kan konfigurera.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en konfigurationsprofil för kabelanslutna nätverksenheter](wired-networks-configure.md).

> [!NOTE]
> De här inställningarna är tillgängliga för alla registreringstyper. Mer information om registreringstyperna finns i [macOS-registrering](../enrollment/macos-enroll.md).

## <a name="wired-network"></a>Kabelanslutet nätverk

- **Nätverksgränssnitt**: Välj nätverksgränssnitt på enheten som profilen gäller för baserat på tjänstens prioritetsordning. Alternativen är:
  
  - **Första aktiva Ethernet** (standardvärde)
  - **Andra aktiva Ethernet**
  - **Tredje aktiva Ethernet**
  - **Första Ethernet**
  - **Andra Ethernet**
  - **Tredje Ethernet**
  - **Valfritt Ethernet**

  Alternativ med ”aktiva” i namnet använder gränssnitt som aktivt är igång på enheten. Om det inte finns några aktiva gränssnitt konfigureras nästa gränssnitt i tjänstens prioritetsordning. **Första aktiva Ethernet** väljs som standard, vilket även är standardinställningen som konfigureras av macOS.

- **EAP-typ**: Välj EAP-typ (Extensible Authentication Protocol) för autentisering av skyddade kabelanslutna anslutningar. Alternativen är:

  - **EAP-FAST**: Ange **PAC-inställningar (Protected Access Credential)** . Det här alternativet använder autentiseringsuppgifter för skyddad åtkomst till att skapa en autentiserad tunnel mellan klienten och autentiseringsservern. Alternativen är:
    - **Använd inte (PAC)**
    - **Använd (PAC)** : Om det finns en befintlig PAC-fil använder du den.
    - **Använd och etablera PAC**: Skapar och lägger till PAC-filen till enheterna.
    - **Använd och etablera PAC anonymt**: Skapa och lägg till PAC-filen i dina enheter utan att autentisera till servern.

  - **EAP-TLS**: Ange även:

    - **Serverförtroende** - **Certifikatservernamn**: **Lägg till** ett eller flera gemensamma namn som används i de certifikat som utfärdats av en betrodd certifikatutfärdare (CA). När du anger den här informationen kan du hoppa över fönstret för dynamiskt förtroende som visas på användarenheter när de ansluter till det här nätverket.
    - **Rotcertifikat för serververifiering**: Välj en befintlig betrodd rotcertifikatsprofil. Det här certifikatet presenteras för servern när klienten ansluter till nätverket. Det används till att autentisera anslutningen.
    - **Klientautentisering** - **Certifikat**: Välj den profil för SCEP-klientcertifikatet som även distribueras till enheten. Det här certifikatet är den identitet som presenterades av enheten till servern när anslutningen autentiserades. PKCS-certifikat stöds inte.
    - **Identitetsskydd (yttre identitet)** : Ange den text som skickas som svar på en begäran om EAP-identitet. Den här texten kan ha vilket värde som helst, t.ex. `anonymous`. Vid autentisering skickas den här anonyma identiteten från början och sedan följs den av den verkliga identifieringen som skickas i en säker tunnel.

  - **EAP-TTLS**: Ange även:

    - **Serverförtroende** - **Certifikatservernamn**: **Lägg till** ett eller flera gemensamma namn som används i de certifikat som utfärdats av en betrodd certifikatutfärdare (CA). När du anger den här informationen kan du hoppa över fönstret för dynamiskt förtroende som visas på användarenheter när de ansluter till det här nätverket.
    - **Rotcertifikat för serververifiering**: Välj en befintlig betrodd rotcertifikatsprofil. Det här certifikatet presenteras för servern när klienten ansluter till nätverket. Det används till att autentisera anslutningen.
    - **Klientautentisering**: Välj en **autentiseringsmetod**. Alternativen är:
      - **Användarnamn och lösenord**: Be användaren om ett användarnamn och lösenord för att autentisera anslutningen. Ange även:
        - **Annan metod än EAP (inre identitet)** : Välj hur du ska autentisera anslutningen. Du måste välja samma protokoll som är konfigurerat för nätverket. Alternativen är:
          - **Okrypterat lösenord (PAP)**
          - **CHAP (Challenge Handshake Authentication Protocol)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**
      - **Certifikat**: Välj den profil för SCEP-klientcertifikatet som även distribueras till enheten. Det här certifikatet är den identitet som presenterades av enheten till servern när anslutningen autentiserades. PKCS-certifikat stöds inte.
      - **Identitetsskydd (yttre identitet)** : Ange den text som skickas som svar på en begäran om EAP-identitet. Den här texten kan ha vilket värde som helst, t.ex. `anonymous`. Vid autentisering skickas den här anonyma identiteten från början och sedan följs den av den verkliga identifieringen som skickas i en säker tunnel.

  - **LEAP**

  - **PEAP**: Ange även:

    - **Serverförtroende** - **Certifikatservernamn**: **Lägg till** ett eller flera gemensamma namn som används i de certifikat som utfärdats av en betrodd certifikatutfärdare (CA). När du anger den här informationen kan du hoppa över fönstret för dynamiskt förtroende som visas på användarenheter när de ansluter till det här nätverket.
    - **Rotcertifikat för serververifiering**: Välj en befintlig betrodd rotcertifikatsprofil. Det här certifikatet presenteras för servern när klienten ansluter till nätverket. Det används till att autentisera anslutningen.
    - **Klientautentisering**: Välj en **autentiseringsmetod**. Alternativen är:
      - **Användarnamn och lösenord**: Be användaren om ett användarnamn och lösenord för att autentisera anslutningen.
      - **Certifikat**: Välj den profil för SCEP-klientcertifikatet som även distribueras till enheten. Det här certifikatet är den identitet som presenterades av enheten till servern när anslutningen autentiserades. PKCS-certifikat stöds inte.
      - **Identitetsskydd (yttre identitet)** : Ange den text som skickas som svar på en begäran om EAP-identitet. Den här texten kan ha vilket värde som helst, t.ex. `anonymous`. Vid autentisering skickas den här anonyma identiteten från början och sedan följs den av den verkliga identifieringen som skickas i en säker tunnel.

## <a name="next-steps"></a>Nästa steg

Profilen skapas, men den kanske inte gör någonting. Se till att du [tilldelar profilen](device-profile-assign.md) och [övervakar](device-profile-monitor.md) dess status.
