---
title: Lägga till filinställningar för macOS-enheter i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Lägg till en xml- eller plist-fil som innehåller viktig information om din app. Använd en inställningsfil för enhetskonfigurationsprofilen för att ändra viktig information i filen med egenskapslistan och tilldela den till dina macOS-enheter.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d226888c3d710a7b80357ebb92130b34ab2fef94
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79360762"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Lägg till en fil med egenskapslista på macOS-enheter med Microsoft Intune

Med Microsoft Intune kan du lägga till en fil med egenskapslista (.plist) för macOS-enheter, eller appar på macOS-enheter.

Den här funktionen gäller för:

- macOS-enheter som kör 10.7 och senare

Filer med egenskapslistor innehåller vanligtvis information om macOS-program. Mer information finns i [About Information Property List Files](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (Apples webbplats) och [Custom payload settings](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

I den här artikeln beskrivs de olika inställningar för filer med egenskapslistor som du kan lägga till på macOS-enheter. Använd inställningarna som en del av din MDM-lösning när du vill lägga till appsamlings-ID:t (`com.company.application`) och lägg till .plist-filen.

Dessa inställningar läggs till en profil för enhetskonfiguration i Intune som sedan tilldelas eller distribueras till dina macOS-enheter.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa profilen](device-profile-create.md).

## <a name="what-you-need-to-know"></a>Vad du behöver veta

- De här inställningarna har inte verifierats. Se till att du testar dina ändringar innan du tilldelar profilen till dina enheter.
- Om du inte är säker på hur du anger en appnyckel så ändrar du inställningen i appen. Granska sedan appens inställningsfil med [Xcode](https://developer.apple.com/xcode/) för att se hur inställningen har konfigurerats. Apple rekommenderar att du tar bort inställningar som inte går att hantera med Xcode innan du importerar filen.
- Endast vissa appar fungerar med hanterade inställningar och de kanske inte tillåter att du hanterar alla inställningar.
- Se till att ladda upp filer med egenskapslistor som riktas mot enhetskanalinställningarna och inte användarkanalinställningarna. Filer med egenskapslistor riktas mot hela enheten.

## <a name="preference-file"></a>Inställningsfil

- **Önskat domännamn**: Filer med egenskapslistor används vanligtvis för webbläsare (Microsoft Edge), [Microsoft Defender Avancerat skydd](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) och anpassade appar. När du skapar en inställningsdomän skapas även ett samlings-ID. Ange samlings-ID:t, t.ex. `com.company.application`. Ange till exempel `com.Contoso.applicationName`, `com.Microsoft.Edge` eller `com.microsoft.wdav`.
- **Fil med egenskapslista**: Välj filen med egenskapslistan som är kopplad till din app. Se till att det är en `.plist`- eller `.xml`-fil. Du kan till exempel ladda upp filen `YourApp-Manifest.plist` eller `YourApp-Manifest.xml`.
- **Filinnehåll**: Nyckelinformationen i filen med egenskapslistan visas. Om du behöver ändra nyckelinformationen öppnar du listfilen i en annan redigerare och laddar sedan upp filen igen i Intune.

Se till att filen är korrekt formaterad. Filen får bara innehålla nyckelvärdepar och får inte vara omslutas av taggtypen `<dict>`, `<plist>` eller `<xml>`. Till exempel bör filen med egenskapslistan likna följande fil:

```xml
<key>SomeKey</key>
<string>someString</string>
<key>AnotherKey</key>
<false/>
...
```

Välj **OK** > **Skapa** för att spara ändringarna. Profilen skapas och visas i profillistan.

## <a name="next-steps"></a>Nästa steg

Profilen har skapats, men den gör inte något än. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Ytterligare information om inställningsfiler för Microsoft Edge finns i [Konfigurera Microsoft Edge-principinställningar på macOS](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
