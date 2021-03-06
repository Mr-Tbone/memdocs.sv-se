---
title: E-postinställningar för Windows 10-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Skapa en e-postprofil för enhetskonfiguration som använder Exchange-servrar och hämtar attribut från Azure Active Directory. Du kan även aktivera SSL och synkronisera e-post och scheman på Windows 10-enheter med Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0cd3505d0a0067adfe9082d7aa3882f3421a2183
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429609"
---
# <a name="email-profile-settings-for-devices-running-windows-10-in-microsoft-intune"></a>E-postprofilinställningar för enheter som kör Windows 10 i Microsoft Intune

Använd e-postprofilinställningarna till att konfigurera E-post-appen på dina enheter som kör Windows 10 och senare.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa profilen](email-settings-configure.md).

## <a name="email-settings"></a>E-postinställningar

- **E-postserver**: Ange värddatornamnet för din Exchange-server. Ange till exempel `outlook.office365.com`.
- **Kontonamn**: Ange visningsnamnet för e-postkontot. Namnet visas för användare på deras enheter.
- **Användarnamnattribut från AAD**: Namnet är det attribut som Intune hämtar från Azure Active Directory (AAD). Intune genererar användarnamnet som används av den här profilen. Alternativen är:
  - **User Principal Name**: Hämtar namnet, till exempel `user1` eller `user1@contoso.com`.
  - **Primär SMTP-adress**: Hämtar namnet i e-postadressformat, som `user1@contoso.com`.
  - **SAM-kontonamn**: Kräver domänen, till exempel `domain\user1`. Ange även:  
    - **Källa för användardomännamn**: Välj **AAD** (Azure Active Directory) eller **Anpassat**.

      När du hämtar attributen från **AAD** anger du även:
      - **Attribut för användardomännamn från AAD**: Välj att hämta attributet **Fullständigt domännamn** eller **NetBIOS-namn** för användaren.

      När du använder **anpassade** attribut anger du även:
      - **Anpassat domännamn som används**: Ange ett värde som Intune använder för domännamnet, exempelvis `contoso.com` eller `contoso`.

- **E-postadressattribut från AAD**: Intune hämtar det här attributet från Azure Active Directory (AAD). Välj hur e-postadressen för användaren ska genereras. Alternativen är:
  - **Användarens huvudnamn (UPN)** : Använder det fullständiga huvudnamnet som e-postadress, t.ex. `user1@contoso.com` eller `user1`.
  - **Primär SMTP-adress**: Använder den primära SMTP-adressen för att logga in, t.ex. `user1@contoso.com`, för att logga in på Exchange.

### <a name="security"></a>Säkerhet

- **SSL**: **Aktivera** använder Secure Sockets Layer-kommunikation (SSL) för att skicka e-post, ta emot e-post och kommunicera med Exchange-servern. **Inaktivera** kräver inte SSL.

### <a name="synchronization"></a>Synkronisering

- **Antal e-postmeddelanden som ska synkroniseras**: Välj det antal dagars e-post du vill synkronisera. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Välj **Obegränsat** om du vill synkronisera all tillgänglig e-post.
- **Synkroniseringsschema**: Välj det schema som ska användas av enheterna när de synkroniserar data från Exchange-servern. Du kan också välja **När meddelanden tas emot**, som synkroniserar data så fort de anländer. Eller välja **Manuellt** så att enhetens användare startar synkroniseringen.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

### <a name="content-sync"></a>Synkronisering av innehåll

- **Innehållstyp som ska synkroniseras:** Välj vilka typer av innehåll du vill synkronisera till enheterna. Alternativen är:
  - **Kontakter**: **På** synkroniserar kontakterna. **Av** synkroniserar inte automatiskt kontakterna. Användarna synkroniseras manuellt.
  - **Kalender**: **På** synkroniserar kalendern. **Av** synkroniserar inte automatiskt kontakterna. Användarna synkroniseras manuellt.
  - **Uppgifter**: **På** synkroniserar aktiviteterna. **Av** synkroniserar inte automatiskt aktiviteterna. Användarna synkroniseras manuellt.

## <a name="next-steps"></a>Nästa steg

Du kan också konfigurera e-postinställningarna på [Android-](email-settings-android.md), [Android Enterprise-](email-settings-android-enterprise.md) och [iOS/iPad](email-settings-ios.md). 

[Läs mer om e-postinställningarna i Intune](email-settings-configure.md).

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
