---
title: Windows 10 Antivirus principinställningar för Windows-säkerhetsfunktioner för Intune | Microsoft Docs
description: Inställningar för antivirusprinciperna för slutpunktssäkerhet för Windows Security-appen i Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 089303b76f674d47767afdff72341d09f7f227d4
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431741"
---
# <a name="settings-for-the-windows-security-experience-profile-in-microsoft-intune"></a>Inställningar för Windows-säkerhetsupplevelseprofilen i Microsoft Intune

Visa inställningarna för antivirusprinciper som du kan konfigurera för **Windows-säkerhetsupplevelseprofilen** för Windows 10 i Microsoft Intune som en del av en [säkerhetsprincip för slutpunkter](../protect/endpoint-security-policy.md).

**Windows-säkerhet**

- **Aktivera manipulationsskydd för att förhindra att Microsoft Defender inaktiveras**  
  [Förhindra ändringar av säkerhetsinställningar med manipulationsskydd](https://go.microsoft.com/fwlink/?linkid=2066083)

  - **Inte konfigurerad** (*standard*) – när *Aktivera* eller *Inaktivera*-tillstånd finns på en klient påverkar inte *Inte konfigurerad* inställningen. 
  - **Aktivera** – Aktivera begränsning av manipulationsskydd. Om du vill ändra tillstånd från antingen aktiverad eller inaktiverad distribuerar du den motsatta inställningen.
  - **Inaktivera** – Inaktivera begränsning av manipulationsskydd. Om du vill ändra tillstånd från antingen aktiverad eller inaktiverad distribuerar du den motsatta inställningen.

- **Dölj avsnittet Skydd mot virus och hot i Windows Security-appen**  
  CSP: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)

  - **Inte konfigurerad** (*standard*) – Inställningen återgår till klientens standardvärde för att tillåta användaråtkomst och meddelanden.
  - **Ja** – Avsnittet om virus och skydd mot hot i Windows Security-appen döljs för slutanvändare. Meddelanden om virus och skydd mot hot ignoreras.

  - **Alternativet Dölj dataåterställning efter utpressningstrojanattack i Windows Security-appen**  
    CSP: [](https://go.microsoft.com/fwlink/?linkid=873664)

  - **Inte konfigurerad** (*standard*) – Inställningen återgår till klientens standardvärde för att tillåta användaråtkomst och meddelanden.
  - **Ja** – Avsnittet om dataåterställning efter utpressningstrojanattack i Windows Security-appen döljs för slutanvändare. Meddelanden om utpressningstrojan ignoreras.

- **Dölj avsnittet om kontoskydd i Windows Security-appen**  
  CSP: [DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)

  - **Inte konfigurerad** (*standard*) – Inställningen återgår till klientens standardvärde för att tillåta användaråtkomst och meddelanden.
  - **Ja** – Avsnittet om kontoskydd i Windows Security-appen döljs för slutanvändare. Meddelanden om kontoskydd ignoreras.

- **Dölj avsnittet om brandvägg och nätverksskydd i Windows Security-appen**  
  CSP: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)

  - **Inte konfigurerad** (*standard*) – Inställningen återgår till klientens standardvärde för att tillåta användaråtkomst och meddelanden.
  - **Ja** – Avsnittet om brandvägg och nätverksskydd i Windows Security är dolda från slutanvändare. Meddelanden om brandvägg och nätverksskydd ignoreras.

- **Dölj avsnittet App- och webbläsarkontroll i Windows Security-appen**  
  CSP: [DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)

  - **Inte konfigurerad** (*standard*) – Inställningen återgår till klientens standardvärde för att tillåta användaråtkomst och meddelanden.
  - **Ja** – Avsnittet App- och webbläsarkontroll i Windows-säkerhetsappen döljs för slutanvändare. Meddelanden om app- och webbläsarkontroll ignoreras.

- **Dölj avsnittet om enhetsskydd i Windows-säkerhetsappen**  
  CSP: [DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)

  - **Inte konfigurerad** (*standard*) – Inställningen återgår till klientens standardvärde för att tillåta användaråtkomst och meddelanden.
  - **Ja** – Avsnittet om maskinvaruskydd i Windows-säkerhetsappen döljs för slutanvändare. Meddelanden om maskinvaruskydd ignoreras.
  
- **Dölj avsnittet Enhetsprestanda och hälsa i Windows-säkerhetsappen**  
  CSP: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)

  - **Inte konfigurerad** (*standard*) – Inställningen återgår till klientens standardvärde för att tillåta användaråtkomst och meddelanden.
  - **Ja** – Avsnittet Enhetsprestanda och hälsa i Windows-säkerhetsappen är dolda från slutanvändarna. Meddelanden om enhetsprestanda och hälsa ignorerades

- **Dölj avsnittet familjealternativ i Windows-säkerhetsappen**  
  CSP: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)

  - **Inte konfigurerad** (*standard*) – Inställningen återgår till klientens standardvärde för att tillåta användaråtkomst och meddelanden.
  - **Ja** – Avsnittet om familjealternativ i Windows-säkerhetsappen döljs för slutanvändare. Dessutom ignoreras meddelanden som rör familjealternativ.

- **Meddelanden i Windows-säkerhetsappen**  
  CSP: [](https://go.microsoft.com/fwlink/?linkid=873675)

  Använd den här inställningen för att blockera Windows-säkerhetsmeddelanden för dina användare för alla föregående funktionsinställningar. Du kan också hantera Windows-säkerhetsappens meddelanden per funktion med hjälp av inställningarna för att fortsätta.

  - **Inte konfigurerad** (*standard*) – Alla Windows-säkerhetsappmeddelanden som inte styrs av en annan inställning tillåts.
  - **Blockera icke-kritiskt meddelande** – Meddelanden som till exempel sökning efter slutförande blockeras.
  - **Blockera alla meddelanden** – Kritiska och icke-kritiska meddelanden blockeras för alla säkerhetsfunktioner i Windows.

- **Dölj ikonen för Windows-säkerhetsappen på meddelandeområdet**  
  CSP: [HideWindowsSecurityNotificationAreaControl](https://go.microsoft.com/fwlink/?linkid=2114313&clcid=0x409)

  För att inställningen ska börja gälla måste användaren antingen logga ut och logga in eller starta om datorn.
  - **Inte konfigurerat** (*standard*) – Inställningen returnerar klienten till standardvärdet för att visa ikonen.
  - **Ja** – Dölj Windows-säkerhetsikonen från användarens systemfält.
  
- **Inaktivera alternativet Rensa TPM i Windows-säkerhetsappen**  
  CSP: [DisableClearTpmButton](https://go.microsoft.com/fwlink/?linkid=2114125&clcid=0x409)

  - **Inte konfigurerad** (*standard*) – Inställningen återgår till klientens standardvärde, som tillåter åtkomst till knappen.
  - **Ja** – Inaktivera åtkomst till knappen Rensa TPM i Windows-säkerhetsappen.

- **Meddela användarna att de ska uppdatera den inbyggda TPM-programvaran om en säkerhetsrisk upptäcks**  
  CSP: [DisableTpmFirmwareUpdateWarning](https://go.microsoft.com/fwlink/?linkid=2114212&clcid=0x409)

  - **Inte konfigurerat** (*standard*) – Inställningen går tillbaka till klientens standardvärde för att användare inte ska meddelas.
  - **Ja** – Tillåt att Windows meddelar slutanvändare när en potentiell säkerhetsrisk påträffas i den inbyggda TPM-programvaran. De uppmanas sedan att köra uppdateringar av inbyggd programvara för att lösa problemet.

- **Organisationens kontaktuppgifter för support**  
  CSP: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)

  Förklara var du vill att din IT-organisations information ska visas i Windows-säkerhetsappen och -meddelanden.
  - **Ej konfigurerat** (*standard*)
  - **Visa i app och i meddelanden**
  - **Visa bara i app**
  - **Visa bara i meddelanden**