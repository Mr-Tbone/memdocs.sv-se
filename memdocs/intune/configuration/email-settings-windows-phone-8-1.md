---
title: E-postinställningar för Windows Phone 8.1 i Microsoft Intune
titleSuffix: ''
description: Läs mer om de Intune-inställningar som du kan använda för att konfigurera e-post-anslutningar på enheter som kör Windows Phone 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/6/2018
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a0dd12ea12e2127c678f8805f3d50b2b24f37c11
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343563"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>E-postprofilinställningar i Microsoft Intune för enheter som kör Windows Phone 8.1



Den här artikeln visar de e-postprofilinställningar som du kan konfigurera för enheter som kör Windows Phone 8.1.

>[!IMPORTANT]
>E-postprofiler för Windows Phone 8.1 tillämpas även på Windows 10-enheter.

- **E-postserver** – Värdnamnet för din Exchange-server.
- **Kontonamn** – Visningsnamnet för e-postkontot som det visas för användare på deras enheter.
- **Användarnamnattribut för AAD** – Det här är attributet i Active Directory (AD) eller Azure AD som används för att generera användarnamn för den här e-postprofilen. Välj **Primär SMTP-adress**, t.ex. **user1@contoso.com** eller **Användarens huvudnamn (UPN)** som **user1** eller **user1@contoso.com** .
- **E-postadressattribut från AAD** – Hur e-postadressen för användaren på varje enhet ska skapas. Välj **Primär SMTP-adress** om du vill använda den primära SMTP-adressen för att logga in på Exchange eller använd **UPN (User Principal Name)** om du vill använda det fullständiga huvudnamnet som e-postadress.


## <a name="security-settings"></a>Säkerhetsinställningar

- **SSL** – Använd Secure Sockets Layer-kommunikation (SSL) för att skicka e-post, ta emot e-post och kommunicera med Exchange-servern.



## <a name="synchronization-settings"></a>Synkroniseringsinställningar

- **Mängd e-post som ska synkroniseras** – Välj antalet dagar med e-post som du vill synkronisera eller välj **Obegränsad** för att synkronisera alla tillgängliga e-postmeddelanden.
- **Synkroniseringsschema** – Välj det schema som ska användas av enheterna som ska synkronisera data från Exchange-servern. Du kan även välja **Efter hand som meddelanden kommer** varvid data synkroniseras när de anländer eller **Manuell** där enhetens användare måste starta synkroniseringen.

## <a name="content-sync-settings"></a>Synkroniseringsinställningar för innehåll

- **Innehållstyp som ska synkroniseras** – Välj vilka innehållstyper som du vill synkronisera till enheterna från:
  - **Kontakter**
  - **Kalender**
  - **aktiviteter**
