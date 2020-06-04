---
title: Inställningar för macOS-tillägg i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Lägg till, konfigurera eller skapa inställningar på macOS-enheter för att använda systemtillägg och kerneltillägg. Tillåt också att användare åsidosätter godkända tillägg, tillåter alla tillägg från ett team-ID eller tillåter vissa tillägg eller appar i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b716a7e85f817e95a9f1fec992458e052570d81
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429520"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-and-system-extensions-in-intune"></a>macOS-enhetsinställningar för att konfigurera och använda kernel- och systemtillägg i Intune

> [!NOTE]
> macOS kernel-tillägg håller på att ersättas med systemtillägg. Mer information finns i [Supporttips: Användning av systemtillägg i stället för kernel-tillägg för macOS Catalina 10.15 i Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

I den här artikeln beskrivs de olika inställningar för kernel- och systemtillägg du kan styra på macOS-enheter. I din MDM-lösning (hantering av mobilenheter) kan du använda de här inställningarna när du lägger till och hanterar tillägg på dina enheter.

Mer information om tillägg i Intune och eventuella förutsättningar finns i [Lägga till macOS-tillägg](kernel-extensions-overview-macos.md).

Dessa inställningar läggs till en profil för enhetskonfiguration i Intune som sedan tilldelas eller distribueras till dina macOS-enheter.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en konfigurationsprofil för macOS-tillägg](kernel-extensions-overview-macos.md).

> [!NOTE]
> De här inställningarna gäller för olika registreringstyper. Mer information om de olika registreringstyperna finns i [macOS-registrering](../enrollment/macos-enroll.md).

## <a name="kernel-extensions"></a>Kerneltillägg

Den här funktionen gäller för:

- macOS 10.13.2 eller senare
- Användargodkänd enhetsregistrering krävs 

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Inställningarna gäller för: Enhetsregistrering som användaren godkänner, automatisk enhetsregistrering

- **Tillåt användaråsidosättningar**: Med **Ja** kan användare godkänna kerneltillägg som inte ingår i konfigurationsprofilen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra att användare tillåter tillägg som inte ingår i konfigurationsprofilen. Det innebär att endast tillägg som ingår i konfigurationsprofilen tillåts.

  Mer information om den här funktionen finns i [Användargodkänd inläsning av kerneltillägg](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (öppnar Apples webbplats).

- **Tillåtna teamidentifierare**: Använd den här inställningen för att tillåta ett eller flera team-ID:n. Alla kerneltillägg som är signerade med de team-ID:n som du anger är tillåtna och betrodda. Med andra ord kan du använda det här alternativet för att tillåta alla kerneltillägg inom samma team-ID, som kan vara en specifik utvecklare eller partner.

  **Lägg till** ett team-ID för giltiga och signerade kerneltillägg som ska läsas in. Du kan lägga till flera teamidentifierare. Team-ID:n måste vara alfanumeriska (bokstäver och siffror) och ha 10 tecken. Ange till exempel `ABCDE12345`.

  När du har lagt till ett team-ID kan det också tas bort.

  [Leta upp ditt team-ID](https://help.apple.com/developer-account/#/dev55c3c710c) (öppnar Apples webbplats) innehåller mer information.

- **Tillåtna kerneltillägg**: Använd den här inställningen för att tillåta specifika kerneltillägg. Endast de kerneltillägg som du anger är tillåtna eller betrodda.

  **Lägg till** paket-ID och team-ID för ett kerneltillägg som ska läsas in. Använd ett tomt team-ID för osignerade äldre kerneltillägg. Du kan lägga till flera kerneltillägg. Team-ID:n måste vara alfanumeriska (bokstäver och siffror) och ha 10 tecken. Ange till exempel `com.contoso.appname.macos` för **Paket-ID** och `ABCDE12345` för **Team-ID**.

  > [!TIP]
  > Om du vill hämta paket-ID:t för ett kerneltillägg (Kext) på en macOS-enhet kan du:
  >
  > 1. Kör `kextstat | grep -v com.apple` i Terminal och anteckna utdata. Installera den programvara eller Kext som du vill använda. Kör `kextstat | grep -v com.apple` igen och leta efter ändringar.
  >
  >    I Terminal visar `kextstat` alla kerneltillägg i operativsystemet. 
  >
  > 2. Öppna filen med informationsegenskapslistan (Info.plist) för en Kext på enheten. Paket-ID:t visas. Varje Kext har en Info.plist-fil lagrad.

> [!NOTE]
> Du behöver inte lägga till teamidentifierare och kerneltillägg. Du kan konfigurera den ena eller den andra.

## <a name="system-extensions"></a>Systemtillägg

Den här funktionen gäller för:

- macOS 10.15 och senare
- Användargodkänd enhetsregistrering krävs

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Inställningarna gäller för: Enhetsregistrering som användaren godkänner, automatisk enhetsregistrering

- **Blockera användaråsidosättning**: **Ja** förhindrar att användare godkänner systemtillägg som inte finns i listan med tillåtna tillägg. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användare att godkänna okända tillägg som inte ingår i konfigurationsprofilen. Det innebär att tillägg som inte ingår i konfigurationsprofilen tillåts.

- **Tillåtna teamidentifierare**: Använd den här inställningen för att tillåta ett eller flera team-ID:n. Alla systemtillägg som är signerade med de team-ID:n du anger är alltid tillåtna och betrodda. Med andra ord kan du använda det här alternativet om du vill tillåta alla systemtillägg inom samma team-ID, som kan vara en specifik utvecklare eller partner.

  **Lägg till** ett **team-ID** för giltiga och signerade systemtillägg som ska läsas in. Du kan lägga till flera teamidentifierare. Team-ID:n måste vara alfanumeriska (bokstäver och siffror) och ha 10 tecken. Ange till exempel `ABCDE12345`.

  När du har lagt till ett team-ID kan det också tas bort.

  [Leta upp ditt team-ID](https://help.apple.com/developer-account/#/dev55c3c710c) (öppnar Apples webbplats) innehåller mer information.

- **Tillåtna systemtillägg**: Använd den här inställningen om du alltid vill tillåta specifika systemtillägg. Endast de systemtillägg du anger är tillåtna eller betrodda.

  **Lägg till** **paket-ID** och **team-ID** för ett systemtillägg som ska läsas in. Använd ett tomt team-ID för osignerade äldre systemtillägg. Du kan lägga till flera systemtillägg. Team-ID:n måste vara alfanumeriska (bokstäver och siffror) och ha 10 tecken. Ange till exempel `com.contoso.appname.macos` för **Paket-ID** och `ABCDE12345` för **Team-ID**.

- **Tillåtna typer av systemtillägg**: Ange ett team-ID och de typer av systemtillägg som ska tillåtas för team-ID:t:
  - **Teamidentifierare**: Ange Team-ID:t för ett annat systemtillägg som du vill tillåta vissa typer av tillägg. Du kan också ange ett team-ID du har lagt till i **Tillåtna systemtillägg**.
  - **Tillåtna typer av systemtillägg**: Välj de typer av systemtilläggs som ska tillåtas för varje team-ID. Alternativen är:
    - Välj alla
    - Drivrutinstillägg
    - Nätverkstillägg
    - Endpoint Security-tillägg

    Mer information om de här typerna av tillägg finns i [Systemtillägg](https://developer.apple.com/system-extensions/) (öppnar Apples webbplats).

    Du kan lägga till ett team-ID från listan **Tillåtna systemtillägg** och tillåta en viss typ av tillägg. Om tillägget är en typ som inte är tillåten kanske tillägget inte kan köras.

    Om du vill tillåta alla tilläggstyper för ett team-ID lägger du till team-ID:t i listan **Tillåtna systemtillägg**. Lägg inte till team-ID: t i listan **Tillåtna typer av systemtillägg**. Om ett team-ID alltså står i listan **Tillåtna systemtillägg** men inte i listan **Tillåtna typer av systemtillägg** så tillåts alla tilläggstyper för det här grupp-ID:t.

> [!NOTE]
> Om du lägger till samma team-ID i **Tillåtna systemtillägg** och **Tillåtna teamidentifierare** kan det resultera i ett fel så att profilen inte fungerar. Lägg inte till samma exakta team-ID i båda inställningarna. 

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
