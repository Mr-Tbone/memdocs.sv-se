---
title: Konfigurera Microsoft Edge-inställningar
titleSuffix: Configuration Manager
description: Konfigurera inställningar för Microsoft Edge Legacy-webbläsaren på Windows 10-klienter
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 57eb9bbaed39ec463afc00d12202a9829729a086
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240554"
---
# <a name="configure-microsoft-edge-legacy-settings-in-configuration-manager"></a>Konfigurera inställningar för Microsoft Edge äldre i Configuration Manager

> [!IMPORTANT]
> Om du använder Microsoft Edge version 77 eller senare och försöker öppna fönstret inställningar, anger du `edge://settings/profiles` i webbläsarens Adress fält i stället för Sök. Mer information finns i [bekanta dig med Microsoft Edge](https://support.microsoft.com/help/17171/microsoft-edge-get-to-know).
>
> Den här artikeln är för IT-proffs som hanterar Microsoft Edge-äldre inställningar med Microsoft Endpoint Configuration Manager.

*Gäller för: Configuration Manager (aktuell gren)*

<!-- 1357310 -->
För kunder som använder [Microsoft Edge äldre](https://docs.microsoft.com/microsoft-edge/deploy/) webbläsare på Windows 10-klienter skapar du en Configuration Manager efterlevnadsprincip för att konfigurera webb läsar inställningarna.

Den här principen gäller bara för klienter i Windows 10, version 1703 eller senare och Microsoft Edge Legacy version 45 och tidigare. <!--511552-->

Mer information om hur du hanterar Microsoft Edge version 77 eller senare med Configuration Manager finns i [distribuera Microsoft Edge, version 77 och senare](../../apps/deploy-use/deploy-edge.md). Mer information om hur du konfigurerar principer för Microsoft Edge version 77 eller senare finns i [Microsofts gräns-principer](https://docs.microsoft.com/DeployEdge/microsoft-edge-policies).

## <a name="policy-settings"></a>Principinställningar

Den här principen innehåller för närvarande följande inställningar:

- **Ange Microsoft Edge-webbläsare som standard**: konfigurerar Windows 10-standardappens inställning för webbläsare till Microsoft Edge

- **Tillåt listruta för adress fält**: kräver Windows 10, version 1703 eller senare. Mer information finns i [princip för AllowAddressBarDropdown-webbläsare](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).

- **Tillåt synkronisering av favoriter mellan Microsoft-webbläsare**: kräver Windows 10, version 1703 eller senare. Mer information finns i [princip för SyncFavoritesBetweenIEAndMicrosoftEdge-webbläsare](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).

- **Tillåt rensning av webb data vid avslut**: kräver Windows 10, version 1703 eller senare. Mer information finns i [princip för ClearBrowsingDataOnExit-webbläsare](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).

- **Tillåt Not Track-huvuden**: Mer information finns i [AllowDoNotTrack Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).

- **Tillåt Autofyll**: Mer information finns i [AllowAutofill Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).

- **Tillåt cookies**: Mer information finns i [AllowCookies Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).

- **Tillåt blockering av popup-fönster**: Mer information finns i [AllowPopups Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).

- **Tillåt Sök förslag i adress fältet**: Mer information finns i [AllowSearchSuggestionsinAddressBar Browser policy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).

- **Tillåt sändning av intranäts trafik till Internet Explorer**: Mer information finns i [SendIntranetTraffictoInternetExplorer Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).

- **Tillåt lösen ords hanteraren**: Mer information finns i [AllowPasswordManager Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).

- **Tillåt utvecklarverktyg**: Mer information finns i [princip för AllowDeveloperTools-webbläsare](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).

- **Tillåt tillägg**: Mer information finns i [AllowExtensions Browser-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

> [!TIP]
> Mer information om hur du använder grup principer för att konfigurera dessa och andra inställningar finns i [Microsoft Edge äldre grup principer](https://docs.microsoft.com/microsoft-edge/deploy/group-policies/).

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge-legacy"></a>Konfigurera Windows Defender SmartScreen-inställningar för Microsoft Edge Legacy
<!--1353701-->
Den här principen lägger till tre inställningar för [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview). Principen innehåller nu följande ytterligare inställningar på sidan SmartScreen- **Inställningar** :

- **Tillåt SmartScreen**: anger om Windows Defender SmartScreen tillåts. Mer information finns i [AllowSmartScreen Browser-principen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).

- **Användare kan åsidosätta SmartScreen-prompten för platser**: anger om användare kan åsidosätta varningar från Windows Defender SmartScreen-filtret om potentiellt skadliga webbplatser. Mer information finns i [PreventSmartScreenPromptOverride Browser-principen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).

- **Användare kan åsidosätta SmartScreen-prompten för filer**: anger om användare kan åsidosätta varningar från Windows Defender SmartScreen-filtret om att ladda ned overifierade filer. Mer information finns i [PreventSmartScreenPromptOverrideForFiles Browser-principen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).

## <a name="create-the-browser-profile"></a>Skapa webb läsar profilen

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen. Expandera **kompatibilitetsinställningar** och välj noden **Microsoft Edge browser-profiler** . I menyfliksområdet väljer du **skapa Microsoft Edge-profil**.

2. Ange ett **namn** för principen, ange en **Beskrivning**(valfritt) och välj **Nästa**.

3. På sidan **allmänna inställningar** ändrar du värdet till **konfigurerat** för inställningarna som ska tas med i den här principen. Om du vill fortsätta med guiden måste du konfigurera inställningen för att **ställa in Edge-webbläsare som standard**.

4. Konfigurera inställningar på sidan **SmartScreen-inställningar** .

5. På sidan **plattformar som stöds** väljer du de OS-versioner och arkitekturer som den här principen gäller.

6. Slutför guiden.

## <a name="deploy-the-policy"></a>Distribuera principen

1. Välj din princip och i menyfliksområdet väljer du **distribuera**.

2. **Bläddra** och välj den användar-eller enhets samling som du vill distribuera principen till.

3. Välj ytterligare alternativ efter behov:

    1. Generera aviseringar när principen inte är kompatibel.

    2. Ange det schema enligt vilket klienten utvärderar enhetens kompatibilitet med den här principen.

4. Klicka på **OK** för att skapa distributionen.

## <a name="next-steps"></a>Nästa steg

Precis som alla inställningar för efterlevnadsprinciper åtgärdar klienten inställningarna enligt det schema du anger. [Övervaka och rapportera om enhetens efterlevnad](monitor-compliance-settings.md) i Configuration Manager-konsolen.
