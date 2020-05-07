---
title: Inställningar av Intune-säkerhetsbaslinjer för Microsoft Edge
titleSuffix: Microsoft Intune
description: Inställningar av säkerhetsbaslinjer som stöds av Intune vid hantering av Microsoft Edge-webbläsaren
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
zone_pivot_groups: edge-baseline-versions
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 861d7f526711f2169e8fd03b3df09659440523b9
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693447"
---
<!-- Pivots in use: 
::: zone pivot="edge-october-2019"
::: zone-end

::: zone pivot="edge-april-2020"
::: zone-end

::: zone pivot="edge-october-2019,edge-april-2020"
::: zone-end
-->

# <a name="microsoft-edge-baseline-settings-for-intune"></a>Microsoft Edge-baslinjeinställningar för Intune

Visa inställningarna av Microsoft Edge-webbläsarens säkerhetsbaslinjer som stöds av Microsoft Intune. Microsoft Edge-baslinjen representerar den rekommenderade konfigurationen av Microsoft Edge-webbläsare. Det är inte säkert att den överensstämmer med baslinjens standardvärden för andra säkerhetsbaslinjer.

::: zone pivot="edge-october-2019"

> [!NOTE]
> Microsoft Edge-baslinjen för oktober 2019 är i allmänt tillgänglig förhandsversion.

::: zone-end
::: zone pivot="edge-april-2020"

*Den nya baslinjen distribueras till klientorganisationer under de närmaste veckorna. Vi förväntar oss att alla klientorganisationer kommer att ha den nya baslinjen i början av maj.*
För att förstå vad som är nytt i den här versionen av baslinjen jämfört med tidigare versioner kan du använda aktiviteten [Jämför baslinjer](../protect/security-baselines.md#compare-baseline-versions) som är tillgänglig när du visar fönstret *Versioner* för den här baslinjen. För att förstå vad som är nytt i den här versionen av baslinjen jämfört med tidigare versioner kan du använda aktiviteten [Jämför baslinjer](../protect/security-baselines.md#compare-baseline-versions) som är tillgänglig när du visar fönstret *Versioner* för den här baslinjen.

::: zone-end
::: zone pivot="edge-october-2019,edge-april-2020"

## <a name="microsoft-edge"></a>Microsoft Edge

::: zone-end
::: zone pivot="edge-april-2020"

- **Autentiseringsscheman som stöds**  
  Anger vilka HTTP-autentiseringsscheman som stöds. Du kan konfigurera principen med hjälp av följande värden: *basic*, *digest*, *ntlm* och *negotiate*. Avgränsa flera värden med kommatecken. Om du inte konfigurerar den här principen används alla fyra scheman.

  - **Aktiverad** (*standard*) – scheman som du väljer används.
  - **Inaktiverad**
  - **Inte konfigurerad** – alla fyra scheman används.
  
  När detta anges till *Aktiverad* kan du konfigurera följande inställning där du väljer vilken autentisering som ska användas:

  - **Autentiseringsscheman som stöds**  
    Välj bland följande alternativ:
    - **Basic**
    - **Digest**
    - **NTLM** *(valt som standard)*
    - **Negotiate** *(valt som standard)*

- **Adobe Flash-standardinställning**  
  CSP: [Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash) och [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)

  Ge åtkomst till följande inställning där du kan konfigurera beteende för att köra Adobe Flash-plugin-programmet.  

  - **Aktiverad** (*standard*)
  - **Inaktiverad**
  - **Inte konfigurerat**

  När detta anges till *Aktiverad* kan du konfigurera följande inställning.

  - **Adobe Flash-standardinställning**

    - **Blockera Adobe Flash-pluginprogrammet** (*standard*) – blockera Adobe Flash på alla webbplatser
    - **Klicka för att spela** – Adobe Flash körs men användaren måste välja alternativet för att starta det.

- **Styr vilka tillägg som inte kan installeras**  
  Aktivera användning av en lista som innehåller de specifika tillägg som användarna inte kan installera i Microsoft Edge. När listan används inaktiveras alla inställningar i listan som tidigare har installerats, och användaren kan inte aktivera dem. Om du tar bort ett objekt från listan med blockerade tillägg, aktiveras tillägget automatiskt på nytt oavsett var det har installerats.

  - **Aktiverad** (*standard*) – aktivera användning av listan för att blockera tillägg.
  - **Inaktiverad**
  - **Inte konfigurerad** – användarna kan installera alla tillägg i Microsoft Edge.
  
  När detta anges till *Aktiverad* kan du konfigurera följande inställning som definierar listan över tillägg som ska blockeras.

  - **Tilläggs-ID:n som användaren inte får installera (eller * för alla)**

    Välj **Lägg till** och ange ytterligare tillägg. **\*** är valt som standard.

- **Tillåt inbyggda meddelandetjänstvärdar på användarnivå (installerade utan administratörsbehörighet)**  
  Aktiverar installation på användarnivå av interna meddelandetjänstvärdar.

  - **Aktiverad**
  - **Inaktiverad** (*standard*) – Microsoft Edge använder endast interna meddelandevärdar som är installerade på systemnivå.
  - **Inte konfigurerad** – som standard tillåter Microsoft Edge användning av interna meddelandevärdar på användarnivå.

- **Sparar lösenord i lösenordshanteraren**  
  CSP för Microsoft Edge: [Browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Aktivera Microsoft Edge för att spara användarlösenord.

  - **Aktiverad** – användarna kan spara sina lösenord i Microsoft Edge. Nästa gång de besöker webbplatsen kommer Microsoft Edge att ange lösenordet automatiskt. Användare kan inte ändra eller åsidosätta den här principen i Microsoft Edge.
  - **Inaktiverad** (*standard*) – användarna kan inte spara nya lösenord men kan fortsätta använda lösenord som sparats tidigare. Användare kan inte ändra eller åsidosätta den här principen i Microsoft Edge.
  - **Inte konfigurerad** – användarna kan spara lösenord och stänga av den här funktionen.

- **Förhindra att Microsoft Defender SmartScreen-varningar för webbplatser kringgås**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Välj om användarna ska kunna åsidosätta Microsoft Defender SmartScreen-varningar om potentiellt skadliga webbplatser.

  - **Aktiverad** (*standard*) – användarna kan inte ignorera Microsoft Defender SmartScreen-varningar, utan blockeras från att fortsätta till webbplatsen.
  - **Inaktiverad** – användarna kan ignorera Microsoft Defender SmartScreen-varningar och fortsätta till webbplatsen.
  - **Inte konfigurerad** – användarna kan ignorera Microsoft Defender SmartScreen-varningar och fortsätta till webbplatsen

- **Förhindra att Microsoft Defender SmartScreen-varningar om nedladdningar kringgås**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Välj om användarna ska kunna åsidosätta Microsoft Defender SmartScreen-varningar om ej verifierade nedladdningar.

  - **Aktiverad** (*standard*) – användarna kan inte ignorera Microsoft Defender SmartScreen-varningar, och de hindras från att slutföra ej verifierade nedladdningar.
  - **Inaktiverad** – användarna kan ignorera Microsoft Defender SmartScreen-varningar och slutföra ej verifierade nedladdningar.
  - **Inte konfigurerad** – användarna kan ignorera Microsoft Defender SmartScreen-varningar och slutföra ej verifierade nedladdningar.

- **Aktivera webbplatsisolering för alla webbplatser**  
  Konfigurera isolering av webbplatser för att förhindra att användarna väljer bort standardbeteendet att isolera alla webbplatser.
  
  - **Aktiverad** (*standard*) – användarna kan inte välja bort standardbeteendet där varje webbplats körs i en egen process.
  - **Inaktiverad** – användarna kan välja bort isolering av webbplatser. Isolering av webbplatser är inte inaktiverat.
  - **Inte konfigurerad** – användarna kan välja bort isolering av webbplatser. Isolering av webbplatser är inte inaktiverat.

  Microsoft Edge stöder även principen [IsolateOrigins](https://docs.microsoft.com/deployedge/microsoft-edge-policies#isolateorigins), som kan isolera ytterligare, mer detaljerade ursprung.  Intune stöder inte konfiguration av principen IsolateOrigins.
  
- **Konfigurera Microsoft Defender SmartScreen**  
  CSP: [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  Microsoft Defender SmartScreen använder varningsmeddelanden för att skydda användarna mot potentiella nätfiskeförsök och skadlig programvara. Som standard är Microsoft Defender SmartScreen aktiverat.
  
  - **Aktiverad** (*standard*) – Microsoft Defender SmartScreen aktiveras och användarna kan inte inaktivera det.
  - **Inaktiverad** – Microsoft Defender SmartScreen inaktiveras och användarna kan inte aktivera det.
  - **Inte konfigurerad** – användarna kan välja om de vill använda Microsoft Defender SmartScreen.

  Den här principen är endast tillgänglig på Windows-instanser som är anslutna till en Microsoft Active Director-domän, eller på Windows 10 Pro- eller Enterprise-instanser som har registrerats för enhetshantering.

- **Konfigurera Microsoft Defender SmartScreen för att blockera potentiellt oönskade appar**  
    Konfigurera Microsoft Defender SmartScreen-beteende för att blockera potentiellt oönskade appar. Microsoft Defender SmartScreen kan tillhandahålla varningsmeddelanden som hjälper till att skydda användare från annonsprogram, kryptogrävare, inbäddade skadeprogram och andra appar med lågt anseende som finns på olika webbplatser. Blockering av potentiellt oönskade appar i Microsoft Defender SmartScreen är inaktiverat som standard.

  - **Aktiverad** (*standard*) – potentiellt oönskade appar blockeras.
  - **Inaktiverad** – potentiellt oönskade appar blockeras inte.
  - **Inte konfigurerad** – användarna kan välja om de vill använda potentiellt oönskad appblockering i Microsoft Defender SmartScreen.

  Den här principen är endast tillgänglig på Windows-instanser som är anslutna till en Microsoft Active Director-domän, eller på Windows 10 Pro- eller Enterprise-instanser som har registrerats för enhetshantering.

- **Tillåt att användarna fortsätter från SSL-varningssidan**  
   CSP: [Browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge visar en varningssida när användarna besöker webbplatser som innehåller SSL-fel.
  - **Aktiverad** – användarna kan klicka genom varningssidorna.
  - **Inaktiverad** (*standard*) – användarna blockeras från att klicka genom någon varningssida.
  - **Inte konfigurerad** – användarna kan klicka genom dessa varningssidor.

- **Lägsta SSL-version som är aktiverad**  
  Aktivera alternativet för att ange den lägsta version av SSL som stöds.

  - **Aktiverad** (*standard*) – aktivera åtkomst till nästa inställning där du anger den lägsta version av TLS som ska användas.
  - **Inaktiverad**
  - **Inte konfigurerad** – Microsoft Edge använder en lägsta standardversion på *TLS 1.0*.

  När detta anges till *Aktiverad* kan du konfigurera TLS med hjälp av följande inställning.

  - **Lägsta SSL-version aktiverad** – ange den lägsta TLS-version som ska användas. Microsoft Edge använder inte någon version av SSL/TLS som är lägre än den angivna versionen.
    - **TLS 1.0**
    - **TLS 1.1**
    - **TLS 1.2** (*standard*)

::: zone-end

::: zone pivot="edge-october-2019"

- **Förhindra att Microsoft Defender SmartScreen-varningar för webbplatser kringgås**  
  **Standard**: Aktiverad  
  CSP för Microsoft Edge: [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Med den här principinställningen kan du bestämma om användarna ska kunna åsidosätta Microsoft Defender SmartScreen-varningar om potentiellt skadliga webbplatser. 
  - Om du aktiverar inställningen kan användarna inte ignorera Microsoft Defender SmartScreen-varningar, utan blockeras från att fortsätta till webbplatsen. 
  - Om du inaktiverar eller inte konfigurerar inställningen, kan användarna ignorera Microsoft Defender SmartScreen-varningar och fortsätta till webbplatsen.

- **Lägsta SSL-version som är aktiverad**  
  **Standard**: Aktiverad  

  Ange den lägsta version av SSL som stöds. Om du ställer in den här principen som *Inte konfigurerad*, använder Microsoft Edge en lägsta standardversion på *TLS 1.0*. När du har angett *Aktiverad* kan du välja en lägsta version bland följande värden:

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - **Lägsta SSL-version som är aktiverad**  
    **Standard**: TLS 1.2

- **Förhindra att Microsoft Defender SmartScreen-varningar om nedladdningar kringgås**  
  **Standard**: Aktiverad  
  CSP för Microsoft Edge: [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Med den här principen kan du bestämma om användarna ska kunna åsidosätta Microsoft Defender SmartScreen-varningar om hämtningar som inte har verifierats.
  - Om du aktiverar principen kan inte användarna i din organisation ignorera SmartScreen-varningar från Microsoft Defender, och de hindras från att slutföra de overifierade hämtningarna.
  - Om du inaktiverar eller låter bli att konfigurera principen kan användarna ignorera Microsoft Defender SmartScreen-varningar och utföra overifierade nedladdningar.

- **Tillåt att användarna fortsätter från SSL-varningssidan**  
  **Standard**: Inaktiverad  
  CSP för Microsoft Edge: [Browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge visar en varningssida när användarna besöker webbplatser som innehåller SSL-fel. Om du anger att den här principen ska vara *Aktiverad* eller *Inte konfigurerad*, kan användarna klicka på dessa varningssidor. När den här principen är *Inaktiverad*, blockeras användarna från att klicka på någon varningssida. 

- **Adobe Flash-standardinställning**  
  **Standard**: Aktiverad  
  CSP för Microsoft Edge: [Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash) och [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  Avgör om webbplatser som inte omfattas av ”PluginsAllowedForUrls” eller ”PluginsBlockedForUrls” kan köra plugin-programmet för Adobe Flash automatiskt. 

  - Välj ”BlockPlugins” om du vill blockera Adobe Flash på alla webbplatser
  - Välj ”ClickToPlay” om du vill tillåta att Adobe Flash körs, men att användaren måste klicka på platshållaren för att starta det.
  
  I samtliga fall har principerna ”PluginsAllowedForUrls” och ”PluginsBlockedForUrls” företräde över ”DefaultPluginsSetting”. Automatisk uppspelning tillåts endast för domäner som uttryckligen anges i ”PluginsAllowedForUrls”-principen. 
   Om du vill aktivera automatisk uppspelning för alla webbplatser, kan du lägga till http://* och https://* i listan.

  - Om du anger *Inte konfigurerad* för principen, kan användaren ändra inställningen manuellt. * 2 = Blockerar plugin-programmet för Adobe Flash * 3 = Klicka för att spela upp det tidigare alternativet ”1” som tillåter alla, men funktionen hanteras nu bara av ”PluginsAllowedForUrls”-principen. Befintliga principer som använder ”1” kommer att köras i läget Klicka för att spela upp.  

  - **Adobe Flash-standardinställning**  
    **Standard**: Blockera Adobe Flash-pluginprogrammet

- **Aktivera webbplatsisolering för alla webbplatser**  
  **Standard**: Aktiverad  

  ”SitePerProcess”-principen kan användas för att förhindra att användarna väljer bort standardbeteendet att isolera alla webbplatser. Du kan också använda IsolateOrigins-principen för att isolera ytterligare, mer detaljerade ursprung.

  - När den här principen är inställd på *Aktiverad*, kan användarna inte välja bort standardbeteendet där varje webbplats körs i en egen process. 
  - Om du använder *Inaktiverad* eller *Inte konfigurerad*, kan användaren välja bort webbplatsisoleringen. (Till exempel med hjälp av posten ”Inaktivera webbplatsisolering” i edge://flags.) Om principen inaktiveras eller inte konfigureras stängs inte webbplatsisoleringen av.

- **Autentiseringsscheman som stöds**  
  **Standard**: Aktiverad  

  Anger vilka HTTP-autentiseringsscheman som stöds. Du kan konfigurera principen med hjälp av följande värden: ”basic”, ”digest”, ”ntlm” och ”negotiate”. Avgränsa flera värden med kommatecken. Om du inte konfigurerar den här principen används alla fyra scheman.

  - **Autentiseringsscheman som stöds**  
    Välj bland följande alternativ:
    - Basic
    - Sammandrag
    - NTLM *(markerat som standard)*
    - Negotiate *(valt som standard)*

- **Sparar lösenord i lösenordshanteraren**  
  **Standard**: Inaktiverad  
  CSP för Microsoft Edge: [Browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Aktivera Microsoft Edge för att spara användarlösenord.
  - Om du aktiverar den här principen kan användarna spara sina lösenord i Microsoft Edge. Nästa gång de besöker webbplatsen kommer Microsoft Edge att ange lösenordet automatiskt.
  - Om du inaktiverar principen kan användarna inte spara nya lösenord, men de kan fortfarande använda tidigare sparade lösenord.
  
  Om du ställer in principen på antingen *Aktiverad* eller *Inaktiverad*, kan användarna inte ändra eller åsidosätta principen i Microsoft Edge.
  
  Om du väljer *Inte konfigurerad* kan användarna spara lösenord, samt stänga av funktionen.

- **Styr vilka tillägg som inte kan installeras**  
  **Standard**: Aktiverad  

  Lista med de specifika tillägg som användarna inte kan installera i Microsoft Edge. När du distribuerar principen inaktiveras alla tillägg i listan som tidigare har installerats och användarna kan inte aktivera dem. Om du tar bort ett objekt från listan med blockerade tillägg, aktiveras tillägget automatiskt på nytt oavsett var det har installerats.
  
  Använd **\*** för att blockera alla tillägg som inte uttryckligen finns med i listan över tillåtna. Om den här principen är inställd på *Inte konfigurerad*, kan användarna installera alla tillägg i Microsoft Edge.
  
  Exempelvärde: extension_id1 extension_id2.  
  <br>
  - **Tilläggs-ID:n som användaren inte får installera (eller * för alla)**  
    Välj **Lägg till** och ange ytterligare tillägg. **\*** är valt som standard.

- **Konfigurera Microsoft Defender SmartScreen**  
  **Standard**: Aktiverad  
  CSP för Microsoft Edge: [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  Med den här principinställningen kan du konfigurera om du vill aktivera Microsoft Defender SmartScreen. Microsoft Defender SmartScreen använder varningsmeddelanden för att skydda användarna mot potentiella nätfiskeförsök och skadlig programvara.
  
  - Som standard är Microsoft Defender SmartScreen aktiverat. Om du aktiverar inställningen aktiveras Microsoft Defender SmartScreen och användarna kan inte inaktivera det.
  - Om du inaktiverar inställningen inaktiveras Microsoft Defender SmartScreen och användarna kan inte aktivera det.
  - När du har angett *Inte konfigurerad* kan användarna välja om de vill använda Microsoft Defender SmartScreen.
  
  Den här principen är endast tillgänglig på Windows-instanser som är anslutna till en Microsoft Active Director-domän, eller på Windows 10 Pro- eller Enterprise-instanser som har registrerats för enhetshantering.

- **Tillåt inbyggda meddelandetjänstvärdar på användarnivå (installerade utan administratörsbehörighet)**  
  **Standard**: Inaktiverad

  Aktiverar installation på användarnivå av interna meddelandetjänstvärdar. 
  - Om du inaktiverar den här principen används endast interna meddelandetjänstvärdar som är installerade på systemnivå i Microsoft Edge. Om du inte konfigurerar den här principen kommer Microsoft Edge som standard att tillåta användning av interna meddelandetjänstvärdar på användarnivå.

::: zone-end

## <a name="next-steps"></a>Nästa steg

- [Läs mer om säkerhetsbaslinjer](security-baselines.md)
- [Undvika konflikter](security-baselines.md#avoid-conflicts)
- [Felsöka principer och profiler i Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
