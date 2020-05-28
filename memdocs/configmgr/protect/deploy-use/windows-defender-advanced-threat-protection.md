---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Lär dig hur du hanterar och övervakar Microsoft Defender Avancerat skydd, en ny tjänst som hjälper företag att reagera på avancerade attacker.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 801aee9665e567ce1a983fba294f1e58f58eee04
ms.sourcegitcommit: 4174f7e485067812c29aea01a4767989ffdbb578
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83406666"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

*Gäller för: Configuration Manager (aktuell gren)*

Endpoint Protection kan hjälpa dig att hantera och övervaka [Microsoft Defender Advanced Threat Protection (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (tidigare Windows Defender ATP). Microsoft Defender ATP hjälper företag att upptäcka, undersöka och reagera på avancerade attacker i sina nätverk. Configuration Managers principer kan hjälpa dig att publicera och övervaka Windows 10-klienter.

Microsoft Defender ATP är en tjänst i [Windows Defender Security Center](https://securitycenter.windows.com). Genom att lägga till och distribuera en konfigurations fil för klient-onboarding kan Configuration Manager övervaka distributions status och Microsoft Defender ATP-agent hälsa. Microsoft Defender ATP stöds på datorer som kör Configuration Manager-klienten eller [hanteras av Microsoft Intune](https://docs.microsoft.com/intune/protect/advanced-threat-protection).

## <a name="prerequisites"></a>Förutsättningar

- Prenumeration på online tjänsten Microsoft Defender Advanced Threat Protection  
- Klient datorer som kör Configuration Manager-klienten
- Klienter som använder ett operativ system som anges i avsnittet [klient operativ system som stöds](#bkmk_os) nedan.

### <a name="supported-client-operating-systems"></a><a name="bkmk_os"></a>Klient operativ system som stöds
Följande klient operativ system kan registreras baserat på den version av Configuration Manager du kör:

#### <a name="configuration-manager-version-1910-and-prior"></a>Configuration Manager version 1910 och tidigare

- Klient datorer som kör Windows 10, version 1607 och senare

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager version 2002 och senare
<!--5229962-->
Från och med Configuration Manager version 2002 kan du publicera följande operativ system:

- Windows 8,1
- Windows 10, version 1607 eller senare
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, version 1803
- Windows Server 2019

## <a name="create-an-onboarding-configuration-file"></a>Skapa en konfigurations fil för onboarding

1. Gå till [Microsoft Defender ATP-online tjänsten](https://securitycenter.windows.com/) och logga in.
1. Välj **dator hantering** under **Inställningar**och välj sedan **onboarding**.
1. Välj de operativ system som du vill publicera i listan.
   - Om du ska publicera Windows 10, Windows Server 1803 och Windows Server 2019:
      1. Välj **Configuration Manager (aktuell gren) version 1606** och välj **Ladda ned paket**.
      1. Hämta den komprimerade Arkiv filen (zip) och extrahera innehållet.
   - Om du registrerar ett annat Windows-operativ system:
      1. Välj de operativ system som du vill publicera från listan som visas i online tjänsten Microsoft Defender ATP.
      1. Kopiera värdena för **arbetsyte nyckeln** och **arbetsyte-ID: t** från avsnittet **Konfigurera anslutning** när processen har slutförts.

> [!IMPORTANT]
> - Konfigurations filen för Microsoft Defender ATP innehåller känslig information som bör vara säker.

## <a name="onboard-devices"></a>Onboard-enheter

1. I Configuration Manager-konsolen navigerar du till **till gångar och efterlevnad**  >  **Endpoint Protection**  >  **Windows Defender ATP-principer** och väljer **skapa Windows Defender ATP-princip**. Guiden Microsoft Defender ATP-princip öppnas.  
1. Ange **namn** och **Beskrivning** för Microsoft Defender ATP-principen och välj **onboarding**.
1. **Bläddra** till konfigurations filen som tillhandahålls av din organisations Microsoft Defender ATP-moln tjänst klient.
   - För Windows 8,1 eller Windows Server 2012 R2 och 2016 anger du **arbets ytans nyckel** och **arbetsyte-ID**.
   - För Configuration Manager version 2002 behöver du **arbets ytans nyckel** och **arbetsyte-ID** även om du bara registrerar Windows Server 2019-och Windows Server 1803-enheter eller senare. Hämta de här värdena genom att välja **Inställningar**som integrerar  >  **Onboarding**  >  **Windows 7 och 8,1** från [online tjänsten Microsoft Defender ATP](https://securitycenter.windows.com/). <!--7054188-->
1. Ange de fil exempel som samlas in och delas från hanterade enheter för analys.  

   - **Inga**

   - **Alla filtyper**  
1. Granska sammanfattningen och Slutför guiden.  

Välj **distribuera** för att rikta in dig på Microsoft Defender ATP-principen till klienter.

## <a name="monitor"></a>Övervaka

1. I Configuration Manager-konsolen, navigerar du till **övervaknings**  >  **säkerhet** och väljer sedan **Windows Defender ATP**.  

1. Granska instrument panelen för Microsoft Defender Avancerat skydd.  

    - **Distributions status för Windows Defender-agent**: antal och procent andel berättigade hanterade klient datorer med aktiv Microsoft Defender ATP-princip onboarded  

    - **Windows Defender ATP-agenthälsa**: procent andel dator klienter som rapporterar status för Microsoft Defender ATP-agenten  

        - **Felfri** fungerar korrekt  

        - **Inaktiv** – inga data har skickats till tjänsten under tids perioden  

        - **Agent tillstånd** – system tjänsten för agenten i Windows körs inte  

        - **Inte** registrerad-principen tillämpades men agenten har inte rapporterat någon princip  

## <a name="create-an-offboarding-configuration-file"></a>Skapa en konfigurations fil för offboarding  

1. Logga in på [online tjänsten Microsoft Defender ATP](https://securitycenter.windows.com/).

1. Välj **dator hantering** under **Inställningar**och välj sedan **onboarding**.  

1. Välj **Configuration Manager (aktuell gren) version 1606** och välj **Endpoint offboarding**.  

1. Hämta den komprimerade Arkiv filen (zip) och extrahera innehållet. Offboarding-filer är giltiga i 30 dagar.

1. I Configuration Manager-konsolen navigerar du till **till gångar och efterlevnad**  >  **Endpoint Protection**  >  **Windows Defender ATP-principer** och väljer **skapa Windows Defender ATP-princip**. Guiden Microsoft Defender ATP-princip öppnas.  

1. Ange **namn** och **Beskrivning** för Microsoft Defender ATP-principen och välj **offboarding**.

1. **Bläddra** till konfigurations filen som tillhandahålls av din organisations Microsoft Defender ATP-moln tjänst klient.

1. Granska sammanfattningen och Slutför guiden.  

Välj **distribuera** för att rikta in dig på Microsoft Defender ATP-principen till klienter.  

> [!IMPORTANT]
> Konfigurationsfiler för Microsoft Defender ATP innehåller känslig information som bör vara säker.

## <a name="next-steps"></a>Nästa steg

- [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Felsöka onboarding-problem i Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
