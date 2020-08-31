---
title: Hantera inställningar för antivirus med principer för Endpoint Security i Microsoft Intune | Microsoft Docs
description: Konfigurera och distribuera policyer och använd rapporter för enheter du hanterar med antivirusprinciper för slutpunktssäkerhet i Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 63400c81ee678a98a83ed17cf192335acf9c047b
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820312"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Antivirusprincip för slutpunktssäkerhet i Intune

Antivirusprinciperna för slutpunktssäkerhet för Intune hjälper säkerhetsadministratörer att fokusera på att hantera olika grupper av antivirusinställningar för hanterade enheter. Om du vill använda en antiviruspolicy ska du integrera Intune med Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) som en Mobile Threat Defense-lösning.

Antivirusprincipen innehåller flera profiler. Varje profil innehåller bara de inställningar som är relevanta för Microsoft Defender ATP-antivirusprogram för macOS, Windows 10 eller användarmiljön i Windows-säkerhetsappen på Windows 10-enheter.

Du hittar de här antivirusprinciperna under **Hantera** i noden Slutpunktssäkerhet i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

I antivirusprinciperna finns samma inställningar som i *Endpoint Protection* eller profiler för *enhetsbegränsning* för [enhetskonfigurationsprincip](../configuration/device-profile-create.md) och liknar inställningarna från principen från [Enhetsefterlevnad](../protect/device-compliance-get-started.md). De här principtyperna innehåller dock ytterligare kategorier av inställningar som inte är relaterade till antivirus. De ytterligare inställningarna kan komplicera uppgiften att konfigurera antivirusprogram. Dessutom är inställningarna i antivirusprincipen för macOS inte tillgängliga via de andra principtyperna. Antivirusprofilen i macOS ersätter behovet av att konfigurera inställningarna med hjälp av `.plist`-filer.

## <a name="prerequisites-for-antivirus-policy"></a>Krav för antivirusprincip

**Allmänt**:

- **macOS**
  - En version av macOS som stöds
  - För att Intune ska kunna hantera antivirusinställningar på en enhet måste du installera Microsoft Defender ATP på enheten. Se. [Microsoft Defender ATP för macOS](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (i dokumentationen för Microsoft Defender ATP)

- **Windows 10 och senare**
  - Inga ytterligare krav finns.

**Stöd för Configuration Manager-klienter** (*förhandsversion*)

*Det här scenariot är i förhandsversion och kräver användning av Configuration Managers nuvarande grenversion 2006 eller senare*.
<!--*This scenario is in preview and requires use of Configuration Manager Technical Preview version 2007 or later*.-->

- **Konfigurera klientanslutning för Configuration Manager-enheter** – för att stödja distribution av Antivirus-principer till enheter som hanteras av Configuration Manager, konfigurera *klientanslutning*. Konfiguration av klientanslutning omfattar konfiguration av Configuration Manager-enhetssamlingar som stöder slutpunktssäkerhetsprinciper från Intune.

  För att konfigurera en klientanslutning, se [Konfigurera klientanslutning för att stödja Endpoint Protection-principer](../protect/tenant-attach-intune.md).

## <a name="antivirus-profiles"></a>Antivirusprofiler

### <a name="devices-managed-by-intune"></a>Enheter som hanteras av Intune

Följande profiler stöds för enheter du hanterar med Intune:

**macOS**:

- Plattform: **macOS**

  - Profil: **Antivirus** – Hantera [Principinställningar för antivirus](../protect/antivirus-microsoft-defender-settings-macos.md) för macOS.

    När du använder [Microsoft Defender ATP för Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) kan du konfigurera och distribuera antivirusinställningar till dina hanterade macOS-enheter via Intune i stället för att konfigurera inställningarna med `.plist`-filer.

**Windows 10**:

- Plattform: **Windows 10-profiler**

  - Profil: **Microsoft Defender Antivirus** – Hantera [principinställningar för antivirus](../protect/antivirus-microsoft-defender-settings-windows.md) för Windows 10.

    Defender Antivirus är nästa generations skyddskomponent i Microsoft Defender Avancerat skydd (Microsoft Defender ATP). Nästa generations skydd kombinerar teknik som maskininlärning och molninfrastruktur för att skydda enheter i företagsorganisationen.

    *Microsoft Defender Antivirus*-profilen är en separat instans av antivirusinställningarna som finns i *profilen för enhetsbegränsning* för enhetskonfigurationsprincipen.
  
    Till skillnad från antivirusinställningarna i en *profil för enhetsbegränsning* kan du använda de här inställningarna för att hantera enheter som är samhanterade. För att du ska kunna använda de här inställningarna måste [skjutreglaget för arbetsbelastning för samhantering av](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) Endpoint Protection vara inställt på Intune.

  - Profil: **Microsoft Defender Antivirus-undantag** – Hantera principinställningar som endast gäller [Antivirus-undantag](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions).
  
    Med den här principen kan du hantera inställningar för följande Microsoft Defender Antivirus-konfigurationstjänstleverantörer (CSP:er) som definierar Antivirus-undantag:

    - Defender/ExcludedPaths
    - Defender/ExcludedExtensions
    - Defender/ExcludedProcesses

    Dessa CSP:er för Antivirus-undantag hanteras också av *Microsoft Defender Antivirus*-principen som innehåller identiska inställningar för undantag. Inställningar från båda principtyperna (*Antivirus* och *Antivirus-undantag*) omfattas av [principsammanslagning](#policy-merge-for-settings) och skapar en överordnad uppsättning undantag för tillämpliga enheter och användare.

  - Profil: **Windows-säkerhetsupplevelse** – Hantera [inställningar för Windows-säkerhetsappen](../protect/antivirus-security-experience-windows-settings.md) som slutanvändare kan visa i Microsoft Defender Security Center och vilka meddelanden de får.

    Windows-säkerhetsappen används av ett antal Windows-säkerhetsfunktioner för att tillhandahålla meddelanden om datorns hälsotillstånd och säkerhet. Säkerhetsmeddelanden innehåller brandväggar, antivirusprodukter, Windows Defender SmartScreen med mera.

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Enheter som hanteras av Configuration Manager *(förhandsversion)*

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](includes/configmgr-antivirus-profiles.md)]

## <a name="policy-merge-for-settings"></a>Principsammanslagning för inställningar

Vissa inställningar för Antivirus-principer stöder *principsammanslagning*. Principsammanslagning bidrar till att undvika konflikter när flera principer tillämpas på samma enheter och konfigurerar samma inställning. Intune utvärderar de inställningar som principsammanslagningen stöder för varje användare eller enhet som tas från alla tillämpliga principer. Dessa inställningar sammanfogas sedan till en enda principuppsättning.

Du kan till exempel skapa tre separata Antivirus-principer som definierar olika sökvägsundantag för antivirus. Till sist tilldelas alla tre principerna samma användare. Eftersom CSP:n för sökvägsundantag i Microsoft Defender stöder principsammanslagning utvärderas den av Intune som kombinerar filundantagen från alla tillämpliga principer för användaren. Undantagen läggs till i en överordnad uppsättning och en enda lista över undantag skickas till användarnas enheter.

När principsammanslagning inte stöds för en inställning kan en konflikt uppstå. Konflikter kan leda till att användaren eller enheten inte kan ta emot någon princip för inställningen. Principsammanslagning stöder till exempel inte CSP:n för att förhindra installation av matchande enhets-ID:n (*PreventInstallationOfMatchingDeviceIDs*). Konfigurationer för denna CSP slås inte samman utan bearbetas separat.

När de bearbetas separat löses principkonflikter enligt följande:

1. Den säkraste principen gäller.
2. Om två principer är lika säkra gäller den senast ändrade principen.
3. Om den senast ändrade principen inte kan lösa konflikten skickas ingen princip till enheten.

### <a name="settings-and-csps-that-support-policy-merge"></a>Inställningar och CSP:er som stöder principsammanslagning

Följande inställningar stöder principsammanslagning:

[Microsoft Defender Antivirus-principer](../protect/antivirus-microsoft-defender-settings-windows.md)

- **Defender-processer som ska uteslutas** – CSP: [Defender/ExcludedProcesses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)
- **Filnamnstillägg som ska undantas från genomsökningar och realtidsskydd** – CSP: [Defender/ExcludedExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)
- **Defender-filer och -mappar som ska uteslutas** – CSP: [Defender/ExcludedPaths](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

## <a name="antivirus-policy-reports"></a>Rapporter om antivirusprinciper

Rapporter om antivirusprinciper visar statusinformation om dina Endpoint Security -antivirusprinciper och enhetsstatus. Rapporterna är tillgängliga i noden Slutpunktssäkerhet i administrationscentret för Microsoft Endpoint Manager.

Om du vill visa rapporterna går du till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och sedan till Endpoint Security och väljer **Antivirus**. Om du väljer Antivirus öppnas sammanfattningssidan. Ytterligare rapport- och statusvisningar är tillgängliga som ytterligare sidor.

### <a name="summary"></a>Sammanfattning

På sidan **Sammanfattning** kan du [skapa nya principer](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) och visa en lista över de principer som har skapats tidigare. Listan innehåller detaljerad information nivå om profilen som principen omfattar (principtyp) och om principen är tilldelad.

![Sammanfattningssida för antivirusprincip](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

När du väljer en princip i listan öppnas sidan *Översikt* för principinstansen och visar mer information. När du har valt en panel från den här vyn visar Intune ytterligare information om profilen om den är tillgänglig.

![Översiktssida för antivirusprincip](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Defekta slutpunkter i Windows 10

På sidan **Defekta slutpunkter i Windows 10** kan du visa information om antivirusstatusen för dina MDM-hanterade Windows 10-enheter. Den här informationen returneras från Windows Defender Antivirus som körs på enheten, som *agentstatus för hot*.

Endast enheter med identifierade problem visas i den här vyn. Den här vyn visar inte information om enheter som identifieras som rensade.

![Sida med inte felfria antivirusprinciper](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Nästa steg

[Konfigurera Endpoint Security-policyer](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
