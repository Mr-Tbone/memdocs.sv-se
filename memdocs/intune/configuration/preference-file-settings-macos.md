---
title: Lägga till filinställningar för macOS-enheter i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Lägg till en xml- eller plist-fil som innehåller viktig information om din app. Använd en inställningsfil för enhetskonfigurationsprofilen för att ändra viktig information i filen med egenskapslistan och tilldela den till dina macOS-enheter.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e83077561ec4492feaf14789cf339e0b3ee86e2
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359320"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Lägg till en fil med egenskapslista på macOS-enheter med Microsoft Intune

Med Microsoft Intune kan du lägga till en fil med egenskapslista (.plist) för macOS-enheter, eller appar på macOS-enheter.

Den här funktionen gäller för:

- macOS 10.7 och senare

Filer med egenskapslistor innehåller information om macOS-program. Mer information finns i [About Information Property List Files](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (Apples webbplats) och [Custom payload settings](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

I den här artikeln beskrivs de olika inställningar för filer med egenskapslistor som du kan lägga till på macOS-enheter. Använd inställningarna som en del av din MDM-lösning när du vill lägga till appsamlings-ID:t (`com.company.application`) och lägg till appens .plist-fil.

Dessa inställningar läggs till en profil för enhetskonfiguration i Intune som sedan tilldelas eller distribueras till dina macOS-enheter.

## <a name="what-you-need-to-know"></a>Vad du behöver veta

- De här inställningarna har inte verifierats. Se till att du testar dina ändringar innan du tilldelar profilen till dina enheter.
- Om du inte är säker på hur du anger en appnyckel så ändrar du inställningen i appen. Granska sedan appens inställningsfil med [Xcode](https://developer.apple.com/xcode/) för att se hur inställningen har konfigurerats. Apple rekommenderar att du tar bort inställningar som inte går att hantera med Xcode innan du importerar filen.
- Endast vissa appar fungerar med hanterade inställningar och de kanske inte tillåter att du hanterar alla inställningar.
- Se till att ladda upp filer med egenskapslistor som riktas mot enhetskanalinställningarna och inte användarkanalinställningarna. Filer med egenskapslistor riktas mot hela enheten.

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

    - **Plattform**: Välj **macOS**
    - **Profil**: Välj **Inställningsfil**.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Till exempel är ett användbart principnamn **macOS: Lägg till en inställningsfil som konfigurerar Microsoft Defender Avancerat skydd på enheter**.
    - **Beskrivning**: Ange en beskrivning av principen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.

7. I **Konfigurationsinställningar** konfigurerar du inställningarna:

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

8. Välj **Nästa**.
9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar**väljer du de användare eller grupper som ska ta emot din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

## <a name="next-steps"></a>Nästa steg

Profilen har skapats, men den gör inte något än. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Ytterligare information om inställningsfiler för Microsoft Edge finns i [Konfigurera Microsoft Edge-principinställningar på macOS](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
