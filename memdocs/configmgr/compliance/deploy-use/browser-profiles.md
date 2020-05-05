---
title: Konfigurera Microsoft Edge-inställningar
titleSuffix: Configuration Manager
description: Konfigurera inställningar för Microsoft Edge-webbläsaren på Windows 10-klienter
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 91c11e133c74cd3b55db09e8bf80fd6c4df7774d
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210102"
---
# <a name="configure-microsoft-edge-settings-in-configuration-manager"></a>Konfigurera inställningar för Microsoft Edge i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

<!-- 1357310 -->
Från och med version 1802, för kunder som använder [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) -webbläsaren på Windows 10-klienter, skapar du en princip för Configuration Manager kompatibilitetsinställningar för att konfigurera flera Microsoft Edge-inställningar. 

Den här principen gäller endast för klienter i Windows 10, version 1703 eller senare. <!--511552-->


## <a name="policy-settings"></a>Principinställningar
Den här principen innehåller för närvarande följande inställningar:
- **Ange Microsoft Edge-webbläsare som standard**: konfigurerar Windows 10-standardappens inställning för webbläsare till Microsoft Edge
- **Tillåt listruta för adress fält**: kräver Windows 10, version 1703 eller senare. Mer information finns i [princip för AllowAddressBarDropdown-webbläsare](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Tillåt synkronisering av favoriter mellan Microsoft-webbläsare**: kräver Windows 10, version 1703 eller senare. Mer information finns i [princip för SyncFavoritesBetweenIEAndMicrosoftEdge-webbläsare](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Tillåt rensning av webb data vid avslut**: kräver Windows 10, version 1703 eller senare. Mer information finns i [princip för ClearBrowsingDataOnExit-webbläsare](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Tillåt Not Track-huvuden**: Mer information finns i [AllowDoNotTrack Browser-princip](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Tillåt Autofyll**: Mer information finns i [AllowAutofill Browser-princip](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Tillåt cookies**: Mer information finns i [AllowCookies Browser-princip](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Tillåt blockering av popup-fönster**: Mer information finns i [AllowPopups Browser-princip](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Tillåt Sök förslag i adress fältet**: Mer information finns i [AllowSearchSuggestionsinAddressBar Browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Tillåt sändning av intranäts trafik till Internet Explorer**: Mer information finns i [SendIntranetTraffictoInternetExplorer Browser-princip](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Tillåt lösen ords hanteraren**: Mer information finns i [AllowPasswordManager Browser-princip](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Tillåt utvecklarverktyg**: Mer information finns i [princip för AllowDeveloperTools-webbläsare](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Tillåt tillägg**: Mer information finns i [AllowExtensions Browser-princip](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).


### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Konfigurera Windows Defender SmartScreen-inställningar för Microsoft Edge
<!--1353701-->
Från och med version 1806, lägger den här principen till tre inställningar för [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview). Principen innehåller nu följande ytterligare inställningar på sidan SmartScreen- **Inställningar** :

- **Tillåt SmartScreen**: anger om Windows Defender SmartScreen tillåts. Mer information finns i [AllowSmartScreen Browser-principen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Användare kan åsidosätta SmartScreen-prompten för platser**: anger om användare kan åsidosätta varningar från Windows Defender SmartScreen-filtret om potentiellt skadliga webbplatser. Mer information finns i [PreventSmartScreenPromptOverride Browser-principen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Användare kan åsidosätta SmartScreen-prompten för filer**: anger om användare kan åsidosätta varningar från Windows Defender SmartScreen-filtret om att ladda ned overifierade filer. Mer information finns i [PreventSmartScreenPromptOverrideForFiles Browser-principen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="create-the-microsoft-edge-browser-profile"></a>Skapa Microsoft Edge-webbläsarens profil

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen. Expandera **kompatibilitetsinställningar** och välj noden **Microsoft Edge browser-profiler** . Klicka på alternativet menyfliksområde för att **skapa Microsoft Edge-profil**.
2. Ange ett **namn** för principen, ange en **Beskrivning**(valfritt) och klicka på **Nästa**.
3. På sidan **allmänna inställningar** ändrar du värdet till **konfigurerat** för inställningarna som ska tas med i den här principen och klickar på **Nästa**. Inställningen för att **ställa in Edge-webbläsare som standard** måste konfigureras att fortsätta.
4. I version 1806 och senare konfigurerar du inställningarna på sidan **SmartScreen-inställningar** och klickar sedan på **Nästa**. 
5. På sidan **plattformar som stöds** väljer du de OS-versioner och arkitekturer som den här principen gäller för och klickar på **Nästa**. 
6. Slutför guiden.



## <a name="deploy-the-policy"></a>Distribuera principen

1. Välj din princip och klicka på alternativet för menyfliksområdet som ska **distribueras**.
2. Klicka på **Bläddra** och välj den användar-eller enhets samling som du vill distribuera principen till. 
3. Välj ytterligare alternativ vid behov.  
     a. Generera aviseringar när principen inte är kompatibel.  
     b. Ange det schema enligt vilket klienten utvärderar enhetens kompatibilitet med den här principen. 
4. Klicka på **OK** för att skapa distributionen.



## <a name="next-steps"></a>Nästa steg

Precis som alla inställningar för efterlevnadsprinciper åtgärdar klienten inställningarna enligt det schema du anger. [Övervaka och rapportera om enhetens efterlevnad](monitor-compliance-settings.md) i Configuration Manager-konsolen.
