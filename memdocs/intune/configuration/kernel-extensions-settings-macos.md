---
title: Inställningar för macOS-kerneltillägg i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Lägg till, konfigurera eller skapa inställningar på macOS-enheter för att använda kerneltillägg. Tillåt också att användare åsidosätter godkända tillägg, tillåter alla tillägg från ett team-ID eller tillåter vissa tillägg eller appar i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
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
ms.openlocfilehash: 2e18fad8f1112681a62bcdacd63c652cfd4ad3ac
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80359295"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-extensions-in-intune"></a>macOS-enhetsinställningar för att konfigurera och använda kerneltillägg i Intune

I den här artikeln beskrivs de olika inställningar för kerneltillägg som du kan kontrollera på macOS-enheter. I din MDM-lösning (hantering av mobilenheter) använder du dessa inställningar när du lägger till och hanterar kerneltillägg på dina enheter.

Mer information om kerneltillägg i Intune och eventuella krav finns i [Lägga till macOS-kerneltillägg](kernel-extensions-overview-macos.md).

Dessa inställningar läggs till en profil för enhetskonfiguration i Intune som sedan tilldelas eller distribueras till dina macOS-enheter.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en konfigurationsprofil för enhetskerneltillägg](kernel-extensions-overview-macos.md).

> [!NOTE]
> De här inställningarna gäller för olika registreringstyper. Mer information om de olika registreringstyperna finns i [macOS-registrering](../enrollment/macos-enroll.md).

## <a name="kernel-extensions"></a>Kerneltillägg

### <a name="settings-apply-to-user-approved-automated-device-enrollment"></a>Inställningarna gäller för: Användargodkänd, automatisk enhetsregistrering

- **Tillåt användaråsidosättningar**: Med **Tillåt** kan användare godkänna kerneltillägg som inte ingår i konfigurationsprofilen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra att användare tillåter tillägg som inte ingår i konfigurationsprofilen. Det innebär att endast tillägg som ingår i konfigurationsprofilen tillåts.

  Mer information om den här funktionen finns i [Användargodkänd inläsning av kerneltillägg](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (öppnar Apples webbplats).

- **Tillåtna teamidentifierare**: Använd den här inställningen för att tillåta ett eller flera team-ID:n. Alla kerneltillägg som är signerade med de team-ID:n som du anger är tillåtna och betrodda. Med andra ord kan du använda det här alternativet för att tillåta alla kerneltillägg inom samma team-ID, som kan vara en specifik utvecklare eller partner.

  **Lägg till** ett team-ID för giltiga och signerade kerneltillägg som du vill läsa in. Du kan lägga till flera teamidentifierare. Team-ID:n måste vara alfanumeriska (bokstäver och siffror) och ha 10 tecken. Ange till exempel `ABCDE12345`.

  När du har lagt till ett team-ID kan det också tas bort.

  [Leta upp ditt team-ID](https://help.apple.com/developer-account/#/dev55c3c710c) (öppnar Apples webbplats) innehåller mer information.

- **Tillåtna kerneltillägg**: Använd den här inställningen för att tillåta specifika kerneltillägg. Endast de kerneltillägg som du anger är tillåtna eller betrodda.

  **Lägg till** paket-ID och team-ID för ett kerneltillägg som du vill läsa in. Använd ett tomt team-ID för osignerade äldre kerneltillägg. Du kan lägga till flera kerneltillägg. Team-ID:n måste vara alfanumeriska (bokstäver och siffror) och ha 10 tecken. Ange till exempel `com.contoso.appname.macos` för **Paket-ID** och `ABCDE12345` för **Team-ID**.

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

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
