---
title: Lägga till anpassade inställningar för iOS/iPadOS-enheter i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Exportera iOS- och iPadOS-inställningar från Apple Configurator eller Apples Profile Manager och importera sedan dessa inställningar till Microsoft Intune. De här inställningarna kan skapa, använda och kontrollera anpassade inställningar och funktioner på iOS/iPadOS-enheter. Den här anpassade profilen kan sedan tilldelas eller distribueras till iOS/iPadOS-enheter i din organisation så att en baslinje eller standard skapas.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3cec45dae7e0596428b2d7ab5c925889c183d465
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364597"
---
# <a name="use-custom-settings-for-ios-and-ipados-devices-in-microsoft-intune"></a>Använd anpassade inställningar för iOS- och iPadOS-enheter i Microsoft Intune

Med Microsoft Intune kan du lägga till eller skapa anpassade inställningar för dina iOS/iPadOS-enheter med hjälp av ”anpassade profiler”. Anpassade profiler är en funktion i Intune. De gör att du kan lägga till enhetsinställningar och funktioner som inte är inbyggda i Intune.

När du använder iOS/iPadOS-enheter kan du hämta anpassade inställningar till Intune på två sätt:

- [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344?mt=12)
- [Apple Profile Manager](https://support.apple.com/profile-manager)

Du kan använda dessa verktyg för att exportera inställningar till en konfigurationsprofil. I Intune importerar du den här filen och tilldelar sedan dina iOS/iPadOS-användare och -enheter profilen. Inställningarna distribueras så snart de har tilldelats. De skapar också en baslinje eller standard för iOS/iPadOS i din organisation.

Den här artikeln innehåller riktlinjer om hur man använder Apple Configurator och Apple Profile Manager och beskriver de egenskaper som du kan konfigurera.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa profilen](device-profile-create.md).

## <a name="what-you-need-to-know"></a>Vad du behöver veta

- När du använder **Apple Configurator** för att skapa konfigurationsprofilen måste du kontrollera att de inställningar som du exporterar är kompatibla med enheternas iOS/iPadOS-version. Om du vill ha information om hur du löser inkompatibla inställningar kan du söka efter **Referens för konfigurationsprofil** och **Protokollreferens för hantering av mobila enheter** på webbplatsen [Apple Developer](https://developer.apple.com/).

- Om du använder **Apple Profile Manager** måste du göra följande:

  - Aktivera [hantering av mobila enheter](https://help.apple.com/serverapp/mac/5.7/#/apd05B9B761-D390-4A75-9251-E9AD29A61D0C) i Profile Manager.
  - Lägg till [iOS/iPadOS-enheter](https://help.apple.com/profilemanager/mac/5.7/#/pm9onzap1984) i Profile Manager.
  - När du har lagt till en enhet i Profile Manager går du till **Under biblioteket** > **Enheter** > välj din enhet > **Inställningar**. Ange allmänna inställningar för enheten.

    Hämta och spara den här filen. Du ska lägga till den här filen i Intune-profilen.

  - Kontrollera att de inställningar som du exporterar från Apple Profile Manager är kompatibla med enheternas iOS/iPadOS-version. Om du vill ha information om hur du löser inkompatibla inställningar kan du söka efter **Referens för konfigurationsprofil** och **Protokollreferens för hantering av mobila enheter** på webbplatsen [Apple Developer](https://developer.apple.com/).

## <a name="custom-configuration-profile-settings"></a>Anpassade inställningar för konfigurationsprofil

- **Anpassat namn på konfigurationsprofil**: Ange ett namn för principen. Det här namnet visas på enheten och i Intune-statusen.
- **Konfigurationsprofilsfil**: Bläddra till den konfigurationsprofil som du skapade med Apple Configurator eller Apple Profile Manager. Den största filstorleken är 1000000 byte (precis under 1 MB). Filen som du importerade visas i området **Filinnehåll**.

  Du kan också lägga till enhetstoken i dina anpassade konfigurationsfiler. Enhetstoken används för att lägga till enhetsspecifik information. Ange till exempel `{{serialnumber}}` om du vill visa serienumret. På enheten visas texten på ungefär samma sätt som `123456789ABC`, som är unikt för varje enhet. När du anger variabler ska du använda klammerparenteser `{{ }}`. [Token för appkonfiguration](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) innehåller en lista över variabler som kan användas. Du kan också använda `deviceid` eller andra enhetsspecifika värden.

  > [!NOTE]
  > Variablerna är inte validerade i användargränssnittet och är skiftlägeskänsliga. Därför kan du se profiler sparade med felaktiga indata. Om du till exempel anger `{{DeviceID}}` istället för `{{deviceid}}` visas litteralsträngen istället för enhetens unika ID. Se till att du anger rätt information.

Välj **OK** > **Skapa** för att spara ändringarna. Profilen skapas och visas i profillistan.

## <a name="next-steps"></a>Nästa steg

Profilen har skapats, men den gör inte något än. Nu ska du [tilldela profilen](device-profile-assign.md).

Se hur du [skapar profilen på macOS-enheter](custom-settings-macos.md). 
