---
title: E-postinställningar för Windows Phone 8.1 i Microsoft Intune
titleSuffix: ''
description: Läs mer om de Intune-inställningar som du kan använda för att konfigurera e-post-anslutningar på enheter som kör Windows Phone 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 369e856b26ecbf8a7d6d7f8c0a87a9bfdf69e318
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086933"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>E-postprofilinställningar i Microsoft Intune för enheter som kör Windows Phone 8.1

Den här artikeln visar de e-postprofilinställningar som du kan konfigurera för enheter som kör Windows Phone 8.1.

>[!IMPORTANT]
>E-postprofiler för Windows Phone 8.1 tillämpas även på Windows 10-enheter.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en Windows Phone 8.1 e-postprofil](email-settings-configure.md).

## <a name="email-settings"></a>E-postinställningar

- **E-postserver**: Ange värddatornamnet för din Exchange-server. Ange till exempel `outlook.office365.com`.
- **Kontonamn**: Ange visningsnamnet för e-postkontot. Namnet visas för användare på deras enheter.
- **Användarnamnattribut från AAD**: Namnet är det attribut som Intune hämtar från Azure Active Directory (AAD). Intune genererar användarnamnet som används av den här profilen. Alternativen är:
  - **User Principal Name**: Hämtar namnet, till exempel `user1` eller `user1@contoso.com`.
  - **Primär SMTP-adress**: Hämtar namnet i e-postadressformat, som `user1@contoso.com`.
  - **SAM-kontonamn**: Kräver domänen, till exempel `domain\user1`. Ange även:
    - **Källa för användardomännamn**: Alternativen är:
      - **AAD** (Azure Active Directory): Ange **Attribut för användardomännamn från AAD**. Välj att hämta attributet **Fullständigt domännamn** eller **NetBIOS-namn** för användaren.
      - **Anpassad**: Ange **Anpassat domännamn som ska användas**. Ange ett värde som Intune använder för domännamnet, exempelvis `contoso.com` eller `contoso`.

- **E-postadressattribut från AAD**: Intune hämtar det här attributet från Azure Active Directory (AAD). Välj hur e-postadressen för användaren ska genereras. Alternativen är:
  - **Användarens huvudnamn (UPN)** : Använder det fullständiga huvudnamnet som e-postadress, t.ex. `user1@contoso.com` eller `user1`.
  - **Primär SMTP-adress**: Använder den primära SMTP-adressen för att logga in, t.ex. `user1@contoso.com`, för att logga in på Exchange.

## <a name="security-settings"></a>Säkerhetsinställningar

- **SSL**: **Aktivera** använder Secure Sockets Layer-kommunikation (SSL) för att skicka e-post, ta emot e-post och kommunicera med Exchange-servern. **Inaktivera** kräver inte SSL.

## <a name="synchronization-settings"></a>Synkroniseringsinställningar

- **Antal e-postmeddelanden som ska synkroniseras**: Välj det antal dagar med e-post du vill synkronisera. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Välj **Obegränsat** om du vill synkronisera all tillgänglig e-post.
- **Synkroniseringsschema**: Välj det schema som ska användas av enheterna när de synkroniserar data från Exchange-servern. Du kan också välja **När meddelanden tas emot**, som synkroniserar data så fort de anländer. Eller välja **Manuellt** så att enhetens användare startar synkroniseringen.

## <a name="content-sync-settings"></a>Synkroniseringsinställningar för innehåll

- **Innehållstyp som ska synkroniseras:** Välj vilka typer av innehåll du vill synkronisera till enheterna:
  - **Kontakter**: **På** synkroniserar kontakterna. **Av** synkroniserar inte automatiskt kontakterna. Användarna synkroniseras manuellt.
  - **Kalender**: **På** synkroniserar kalendern. **Av** synkroniserar inte automatiskt kontakterna. Användarna synkroniseras manuellt.
  - **Uppgifter**: **På** synkroniserar aktiviteterna. **Av** synkroniserar inte automatiskt aktiviteterna. Användarna synkroniseras manuellt.

## <a name="next-steps"></a>Nästa steg

Du kan också konfigurera e-postinställningarna på [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md), [iOS/iPad](email-settings-ios.md) och [Windows 10](email-settings-windows-10.md).

[Konfigurera e-postinställningar i Intune](email-settings-configure.md).
