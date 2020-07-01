---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Lär dig hur du hanterar och övervakar Microsoft Defender Avancerat skydd, en ny tjänst som hjälper företag att reagera på avancerade attacker.
ms.date: 06/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cbf7dd3e35db8d2020e96e2511017e43863f724e
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85613502"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

*Gäller för: Configuration Manager (aktuell gren)*

Endpoint Protection kan hjälpa dig att hantera och övervaka [Microsoft Defender Advanced Threat Protection (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (tidigare Windows Defender ATP). Microsoft Defender ATP hjälper företag att upptäcka, undersöka och reagera på avancerade attacker i sina nätverk. Configuration Managers principer kan hjälpa dig att publicera och övervaka Windows 10-klienter.

Microsoft Defender ATP är en tjänst i [Microsoft Defender-Security Center](https://securitycenter.windows.com). Genom att lägga till och distribuera en konfigurations fil för klient-onboarding kan Configuration Manager övervaka distributions status och Microsoft Defender ATP-agent hälsa. Microsoft Defender ATP stöds på datorer som kör Configuration Manager-klienten eller [hanteras av Microsoft Intune](https://docs.microsoft.com/intune/protect/advanced-threat-protection).

## <a name="prerequisites"></a>Krav

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
- Windows Server 2016, version 1803 eller senare
- Windows Server 2019

## <a name="about-onboarding-to-atp-with-configuration-manager"></a>Om att publicera till ATP med Configuration Manager

Olika operativ system har olika behov av onboarding till ATP. Windows 8,1 och andra operativ system enheter för äldre operativ system kräver **arbets ytans nyckel** och **arbetsyte-ID** för att publicera. Konfigurations filen för onboarding-enheter, till exempel Windows Server version 1803, krävs. Configuration Manager installerar även Microsoft Monitoring Agent (MMA) när det behövs av inbyggda enheter, men den uppdaterar inte agenten automatiskt.

Operativ systemen på upp-nivån är:
- Windows 10, version 1607 och senare
- Windows Server 2016, version 1803 eller senare
- Windows Server 2019

Äldre operativ system är:
- Windows 8,1
- Windows Server 2012 R2
- Windows Server 2016, version 1709 och tidigare

När du registrerar enheter till ATP med Configuration Manager distribuerar du ATP-principen till en mål samling eller flera samlingar. Ibland innehåller mål samlingen enheter som kör valfritt antal operativ system som stöds. Anvisningarna för att registrera dessa enheter varierar beroende på om du riktar in en samling med enheter med operativ system som är på nivå, i nivå eller både och.

- Om mål samlingen innehåller både på-nivå-och-nivå-enheter använder du instruktionerna för att registrera [enheter som kör alla operativ system som stöds](#bkmk_any_os) (rekommenderas).
- Om din samling bara innehåller enheter på upp-nivå kan du använda [registrerings anvisningarna på upp-nivån](#bkmk_uplevel).
- Om din samling bara innehåller enheter som är äldre än, kan du använda instruktionerna på inaktive [nivå](#bkmk_downlevel).

> [!Warning]
> - Om mål samlingen innehåller enheter på upp-nivå, och du använder instruktionerna för äldre enheter, så kommer inte enheter på den översta nivån att publiceras.
> - Om mål samlingen innehåller enheter som är äldre, och du använder instruktionerna för att installera-nivå enheter, så kommer inte de äldre enheterna att publiceras.

## <a name="onboard-devices-with-any-supported-operating-system-to-atp-recommended"></a><a name="bkmk_any_os"></a>Publicera enheter med alla operativ system som stöds till ATP (rekommenderas)
 Du kan publicera enheter som kör något av de [operativ system som stöds](#bkmk_os) till ATP genom att ange konfigurations filen, **arbets ytans nyckel**och **arbetsyte-ID** för att Configuration Manager.

### <a name="get-the-configuration-file-workspace-id-and-workspace-key"></a>Hämta konfigurations filen, arbetsyte-ID och nyckel för arbets ytan

1. Gå till [Microsoft Defender ATP-online tjänsten](https://securitycenter.windows.com/) och logga in.
1. Välj **Inställningar**och välj sedan **onboarding** under rubriken **enhets hantering** .
1. För operativ systemet väljer du **Windows 10**.
1. Välj **Microsoft Endpoint Configuration Manager aktuell gren och senare** för distributions metoden.
1. Klicka på **Hämta paket**.
   
   :::image type="content" source="media/5229962-onboarding-configuration.png" alt-text="Hämtar hämtning av konfigurations fil" lightbox="media/5229962-onboarding-configuration.png":::
1. Hämta den komprimerade Arkiv filen (zip) och extrahera innehållet.
1. Välj **Inställningar**och välj sedan **onboarding** under rubriken **enhets hantering** .
1. För operativ systemet väljer du antingen **Windows 7 SP1 och 8,1** eller **Windows Server 2008 R2 SP1, 2012 R2 och 2016** i listan.
   - **Arbets ytans nyckel** och **arbetsyte-ID** är desamma oavsett vilken av de här alternativen du väljer.
1. Kopiera värdena för **arbets ytans nyckel** och **arbetsyte-ID** från avsnittet **Konfigurera anslutning** .

   > [!IMPORTANT]
   > Konfigurations filen för Microsoft Defender ATP innehåller känslig information som bör vara säker.


### <a name="onboard-the-devices"></a>Publicera enheterna

1. I Configuration Manager-konsolen navigerar du till **till gångar och efterlevnad**  >  **Endpoint Protection**  >  **Microsoft Defender ATP-principer**.
1. Välj **skapa Microsoft Defender ATP-princip** för att öppna guiden Microsoft Defender ATP-princip. 
1. Ange **namn** och **Beskrivning** för Microsoft Defender ATP-principen och välj **onboarding**.
1. **Bläddra** till den konfigurations fil som du extraherade från den hämtade ZIP-filen.
1. Ange **arbets ytans nyckel** och **arbetsyte-ID** och klicka sedan på **Nästa**.

   :::image type="content" source="media/5229962-create-atp-policy-wizard.png" alt-text="Guiden Skapa Microsoft Defender ATP-princip" lightbox="media/5229962-create-atp-policy-wizard.png":::

1. Ange de fil exempel som samlas in och delas från hanterade enheter för analys.  
   - **Inga**
   - **Alla filtyper**  
1. Granska sammanfattningen och Slutför guiden.  
1. Högerklicka på principen som du skapade och välj sedan **distribuera** för att rikta in dig mot Microsoft Defender ATP-principen till klienter.

## <a name="onboard-devices-running-up-level-operating-systems-to-atp"></a><a name="bkmk_uplevel"></a>Onboard-enheter som kör operativ system på upp-nivå till ATP

Klient datorer kräver en onboarding-konfigurationsfil för onboarding till ATP. Operativ systemen på upp-nivån är:
- Windows 10, version 1607 och senare 
- Windows Server 2016, version 1803 och senare
- Windows Server 2019

Om mål samlingen innehåller både på-nivå-och-nivå-enheter, eller om du inte är säker, använder du sedan instruktionerna för att registrera [enheter som kör ett operativ system som stöds (rekommenderas)](#bkmk_any_os).

### <a name="get-an-onboarding-configuration-file-for-up-level-devices"></a>Hämta en konfigurations fil för onboarding för enheter på upp-nivå

1. Gå till [Microsoft Defender ATP-online tjänsten](https://securitycenter.windows.com/) och logga in.
1. Välj **Inställningar**och välj sedan **onboarding** under rubriken **enhets hantering** .
1. För operativ systemet väljer du **Windows 10**.
1. Välj **Microsoft Endpoint Configuration Manager aktuell gren och senare** för distributions metoden.
1. Klicka på **Hämta paket**.
1. Hämta den komprimerade Arkiv filen (zip) och extrahera innehållet.

> [!IMPORTANT]
> Konfigurations filen för Microsoft Defender ATP innehåller känslig information som bör vara säker.


### <a name="onboard-the-up-level-devices"></a>Publicera enheter på högre nivå

1. I Configuration Manager-konsolen navigerar du till **till gångar och efterlevnad**  >  **Endpoint Protection**  >  **Microsoft Defender ATP-principer** och väljer **skapa Microsoft Defender ATP-princip**. Guiden Microsoft Defender ATP-princip öppnas.  
1. Ange **namn** och **Beskrivning** för Microsoft Defender ATP-principen och välj **onboarding**.
1. **Bläddra** till den konfigurations fil som du extraherade från den hämtade ZIP-filen.
   > [!Note]
   > För Configuration Manager version 2002 behöver du **arbets ytans nyckel** och **arbetsyte-ID** även om du bara registrerar upp-nivå-enheter. Hämta de här värdena genom att välja **Inställningar**som integrerar  >  **Onboarding**  >  **Windows 7 och 8,1** från [online tjänsten Microsoft Defender ATP](https://securitycenter.windows.com/). <!--7054188-->
1. Ange de fil exempel som samlas in och delas från hanterade enheter för analys.  
   - **Inga**
   - **Alla filtyper**  
1. Granska sammanfattningen och Slutför guiden.  
1. Högerklicka på principen som du skapade och välj sedan **distribuera** för att rikta in dig mot Microsoft Defender ATP-principen till klienter.

## <a name="onboard-devices-running-down-level-operating-systems-to-atp"></a><a name="bkmk_downlevel"></a>Onboard-enheter som kör äldre operativ system till ATP

Äldre klienter kräver nyckel för **arbets yta** och **arbetsyte-ID** för ATP-onboarding. Äldre operativ system är:
- Windows 8,1
- Windows Server 2012 R2
- Windows Server 2016, version 1709 och tidigare

Om mål samlingen innehåller både på-nivå-och-nivå-enheter, eller om du inte är säker, använder du sedan instruktionerna för att registrera [enheter som kör ett operativ system som stöds (rekommenderas)](#bkmk_any_os).

### <a name="get-the-workspace-id-and-workspace-key-for-down-level-devices"></a>Hämta arbetsyte-ID och arbets ytans nyckel för äldre enheter

1. Gå till [Microsoft Defender ATP-online tjänsten](https://securitycenter.windows.com/) och logga in.
1. Välj **Inställningar**och välj sedan **onboarding** under rubriken **enhets hantering** .
1. För operativ systemet väljer du antingen **Windows 7 SP1 och 8,1** eller **Windows Server 2008 R2 SP1, 2012 R2 och 2016** i listan.
   - **Arbets ytans nyckel** och **arbetsyte-ID** är desamma oavsett vilken av de här alternativen du väljer.
1. Kopiera värdena för **arbets ytans nyckel** och **arbetsyte-ID** från avsnittet **Konfigurera anslutning** .

### <a name="onboard-the-down-level-devices"></a>Publicera enheterna på den äldre nivån

1. I Configuration Manager-konsolen navigerar du till **till gångar och efterlevnad**  >  **Endpoint Protection**  >  **Microsoft Defender ATP-principer** och väljer **skapa Microsoft Defender ATP-princip**. Guiden Microsoft Defender ATP-princip öppnas.  
1. Ange **namn** och **Beskrivning** för Microsoft Defender ATP-principen och välj **onboarding**.
1. Ange **arbets ytans nyckel** och **arbetsyte-ID**.
   > [!Note]
   > - För Configuration Manager version 2002 behöver du konfigurations filen även om du bara registrerar äldre enheter. Hämta de här värdena genom att välja **Inställningar**som integrerar  >  **Onboarding**  >  **Windows 10** från [online tjänsten Microsoft Defender ATP](https://securitycenter.windows.com/). <!--7054188--> 
   > - Konfigurations filen för Microsoft Defender ATP innehåller känslig information som bör vara säker.
1. Ange de fil exempel som samlas in och delas från hanterade enheter för analys.  
   - **Inga**
   - **Alla filtyper**  
1. Granska sammanfattningen och Slutför guiden.  
1. Högerklicka på principen som du skapade och välj sedan **distribuera** för att rikta in dig mot Microsoft Defender ATP-principen till klienter.


## <a name="monitor"></a>Övervaka

1. I Configuration Manager-konsolen, navigerar du till **övervaknings**  >  **säkerhet** och väljer sedan **Microsoft Defender ATP**.  

1. Granska instrument panelen för Microsoft Defender Avancerat skydd.  

    - **Microsoft Defender ATP-agentens onboarding-status**: antalet och procent andelen berättigade hanterade klient datorer med aktiv Microsoft Defender ATP-princip  

    - **Microsoft Defender ATP-agenthälsa**: procent andel dator klienter som rapporterar status för Microsoft Defender ATP-agenten  

        - **Felfri** fungerar korrekt  

        - **Inaktiv** – inga data har skickats till tjänsten under tids perioden  

        - **Agent tillstånd** – system tjänsten för agenten i Windows körs inte  

        - **Inte** registrerad-principen tillämpades men agenten har inte rapporterat någon princip  

## <a name="create-an-offboarding-configuration-file"></a>Skapa en konfigurations fil för offboarding  

1. Logga in på [online tjänsten Microsoft Defender ATP](https://securitycenter.windows.com/).
1. Välj **Inställningar**och välj sedan **offboarding** under rubriken **enhets hantering** .
1. Välj **Windows 10** för operativ systemet och **Microsoft Endpoint Configuration Manager aktuella grenen och senare** för distributions metoden.
   - Med alternativet **Windows 10** ser du till att alla enheter i samlingen är offboarded och att MMA avinstalleras vid behov.
1. Hämta den komprimerade Arkiv filen (zip) och extrahera innehållet. Offboarding-filer är giltiga i 30 dagar.

1. I Configuration Manager-konsolen navigerar du till **till gångar och efterlevnad**  >  **Endpoint Protection**  >  **Microsoft Defender ATP-principer** och väljer **skapa Microsoft Defender ATP-princip**. Guiden Microsoft Defender ATP-princip öppnas.  

1. Ange **namn** och **Beskrivning** för Microsoft Defender ATP-principen och välj **offboarding**.

1. **Bläddra** till den konfigurations fil som du extraherade från den hämtade ZIP-filen.

1. Granska sammanfattningen och Slutför guiden.  

Välj **distribuera** för att rikta in dig på Microsoft Defender ATP-principen till klienter.  

> [!IMPORTANT]
> Konfigurationsfiler för Microsoft Defender ATP innehåller känslig information som bör vara säker.

## <a name="next-steps"></a>Nästa steg

- [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Felsöka onboarding-problem i Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
