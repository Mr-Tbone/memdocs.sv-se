---
title: Hantera Application Guard-principer
titleSuffix: Configuration Manager
description: Lär dig hur du skapar och distribuerar Microsoft Defender Application Guard-principer
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3fb7559f624afdb16ef228c61331387c163fbd54
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697117"
---
# <a name="create-and-deploy-microsoft-defender-application-guard-policy"></a>Skapa och distribuera Microsoft Defender Application Guard-princip

*Gäller för: Configuration Manager (aktuell gren)*
<!-- 1351960 -->  
Du kan skapa och distribuera [Microsoft Defender Application Guard-principer (Application Guard)](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview) med hjälp av Configuration Manager Endpoint Protection. Dessa principer hjälper dig att skydda dina användare genom att öppna obetrodda webbplatser i en säker isolerad behållare som inte är tillgänglig för andra delar av operativ systemet.

## <a name="prerequisites"></a>Förutsättningar

Om du vill skapa och distribuera en Microsoft Defender Application Guard-princip måste du använda Windows 10s uppdaterings uppdatering (1709). De Windows 10-enheter som du distribuerar principen till måste konfigureras med en [princip för nätverks isolering](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard#network-isolation-settings). Mer information finns i [Översikt över Microsoft Defender Application Guard](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview).

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Skapa en princip och bläddra bland de tillgängliga inställningarna

1. I Configuration Manager-konsolen väljer du **till gångar och efterlevnad**.
2. I arbets ytan **till gångar och efterlevnad** väljer du **Översikt**  >  **Endpoint Protection**  >  **Windows Defender Application Guard**.
3. På fliken **Start** går du till gruppen **skapa** och klickar på **skapa Windows Defender Application Guard-princip**.
4. Med hjälp av [artikeln](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard) som en referens kan du bläddra och konfigurera de tillgängliga inställningarna. Med Configuration Manager kan du ange vissa princip inställningar:
   - [Inställningar för värd interaktion](#bkmk_HIS)
   - [Program beteende](#bkmk_ABS)
   - [Fil hantering](#bkmk_FM)
5. På sidan **nätverks definition** anger du företagets identitet och definierar företagets nätverks gränser.

    > [!NOTE]
    > Windows 10-datorer lagrar bara en lista över nätverks isolering på klienten. Du kan skapa två olika typer av nätverks isolerings listor och distribuera dem till klienten:
    >
    >  - en från Windows Information Protection
    >  - en från Microsoft Defender Application Guard
    >
    > Om du distribuerar båda principerna måste dessa listor för nätverks isolering matcha. Om du distribuerar listor som inte matchar samma klient kommer distributionen att Miss Don. Mer information finns i dokumentationen till [Windows information Protection](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. När du är klar slutför du guiden och distribuerar principen till en eller flera Windows 10 1709-enheter.

### <a name="host-interaction-settings"></a><a name="bkmk_HIS"></a> Inställningar för värd interaktion

Konfigurerar interaktioner mellan värd enheter och Application Guard-behållaren. Innan Configuration Manager version 1802 var både program beteendet och värd interaktionen under fliken **Inställningar** .

- **Urklipp** – under inställningar före Configuration Manager 1802
  - Tillåten innehålls typ
    - Text
    - Avbildningar
- **Skrivs**
  - Aktivera utskrift till XPS
  - Aktivera utskrift till PDF
  - Aktivera utskrift till lokala skrivare
  - Aktivera utskrift till nätverks skrivare
- **Grafik:** (från och med Configuration Manager version 1802)
  - Åtkomst till virtuell grafik processor
- **Filer:** (från och med Configuration Manager version 1802)
  - Spara hämtade filer på värden

### <a name="application-behavior-settings"></a><a name="bkmk_ABS"></a> Inställningar för program beteende

Konfigurerar program beteende i Application Guard-sessionen. Innan Configuration Manager version 1802 var både program beteendet och värd interaktionen under fliken **Inställningar** .

- **Innehåll**
  - Företags webbplatser kan läsa in icke-Enterprise-innehåll, till exempel plugin-program från tredje part.
- **Andra**
  - Behåll användargenererade webbläsardata
  - Granska säkerhets händelser i den isolerade Application Guard-sessionen

### <a name="file-management"></a><a name="bkmk_FM"></a> Fil hantering
<!--3555858-->
Från och med Configuration Manager version 1906 finns en princip inställning som gör det möjligt för användare att lita på filer som normalt öppnas i Application Guard. När åtgärden har slutförts öppnas filerna på värd enheten i stället för i Application Guard. Mer information om Application Guard-principer finns i [Konfigurera princip inställningar för Microsoft Defender Application Guard](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard).

- **Tillåt användare att lita på filer som öppnas i Windows Defender Application Guard** – aktivera användaren för att markera filer som betrodda. När en fil är betrodd öppnas den på värden i stället för i Application Guard. Gäller för Windows 10 version 1809 eller senare klienter.
  - **Förbjuden:** Tillåt inte att användare markerar filer som betrodda (standard).
  - **Filen kontrollerades av antivirus programmet:** Tillåt användare att markera filer som betrodda efter en virus kontroll.
  - **Alla filer:** Tillåt användare att markera en fil som betrodd.

När du aktiverar fil hantering kan du se fel som loggats i klientens DCMReporting. log. Felen nedan utträder normalt inte av funktioner: <!--4619457-->

- På kompatibla enheter:
  - FileTrustCriteria_condition hittades inte
- På icke-kompatibla enheter:
  - FileTrustCriteria_condition hittades inte
  - Det gick inte att hitta FileTrustCriteria_condition på kartan
  - FileTrustCriteria_condition hittades inte i sammandrag

Om du vill redigera Application Guard-inställningarna expanderar du **Endpoint Protection** i arbets ytan **till gångar och efterlevnad** och klickar sedan på **Windows Defender Application Guard** -noden. Högerklicka på den princip som du vill redigera och välj sedan **Egenskaper**.

## <a name="known-issues"></a>Kända problem

Enheter som kör Windows 10, version 2004 visar problem i kompatibilitets rapportering för Microsoft Defender Application Guard fil förtroende kriterier. Det här problemet beror på att vissa underklasser har tagits bort från WMI-klassen `MDM_WindowsDefenderApplicationGuard_Settings01` i Windows 10, version 2004. Alla andra Microsoft Defender Application Guard-inställningar gäller fortfarande. det går bara att använda villkor för fil förtroende. För närvarande finns det inga lösningar för att kringgå felet. <!--7099444,5946790-->

## <a name="next-steps"></a>Nästa steg

Mer information om Microsoft Defender Application Guard finns i
 - [Översikt över Microsoft Defender Application Guard](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview).
- [Vanliga frågor och svar om Microsoft Defender Application Guard](/windows/security/threat-protection/microsoft-defender-application-guard/faq-md-app-guard).