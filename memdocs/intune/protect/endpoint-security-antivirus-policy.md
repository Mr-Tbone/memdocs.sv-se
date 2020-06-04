---
title: Hantera inställningar för antivirus med principer för Endpoint Security i Microsoft Intune | Microsoft Docs
description: Konfigurera och distribuera policyer och använd rapporter för enheter du hanterar med antivirusprinciper för slutpunktssäkerhet i Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
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
ms.openlocfilehash: 2f3a378cdb3b5e24371edb2fd6dc240962f80342
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431910"
---
# <a name="antivirus-policy-for-endpoint-security-in-intune"></a>Antivirusprincip för slutpunktssäkerhet i Intune

Antivirusprinciperna för slutpunktssäkerhet för Intune hjälper säkerhetsadministratörer att fokusera på att hantera olika grupper av antivirusinställningar för hanterade enheter. Om du vill använda en antiviruspolicy ska du integrera Intune med Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) som en Mobile Threat Defense-lösning.

Antivirusprincipen innehåller flera profiler. Varje profil innehåller bara de inställningar som är relevanta för Defender ATP-antivirusprogram för macOS, Windows 10 eller användarupplevelsen i Windows-säkerhetsappen på Windows 10-enheter.

Du hittar de här antivirusprinciperna under **Hantera** i noden Slutpunktssäkerhet i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

I antivirusprinciperna finns samma inställningar som i *Endpoint Protection* eller profiler för *enhetsbegränsning* för [enhetskonfigurationsprincip](../configuration/device-profile-create.md) och liknar inställningarna från principen från [Enhetsefterlevnad](../protect/device-compliance-get-started.md). De här principtyperna innehåller dock ytterligare kategorier av inställningar som inte är relaterade till antivirus. De ytterligare inställningarna kan komplicera uppgiften att konfigurera antivirusprogram. Dessutom är inställningarna i antivirusprincipen för macOS inte tillgängliga via de andra principtyperna. Antivirusprofilen i macOS ersätter behovet av att konfigurera inställningarna med hjälp av `.plist`-filer.

## <a name="prerequisites-for-antivirus-policy"></a>Krav för antivirusprincip

- **macOS**
  - En version av macOS som stöds
  - För att Intune ska kunna hantera antivirusinställningar på en enhet måste du installera Defender ATP på enheten. Se. [Defender ATP för macOS](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) (i dokumentationen för Defender ATP)

- **Windows 10 och senare**
  - För att Intune ska kunna hantera antivirusinställningar på en enhet måste du installera Defender ATP på enheten. Läs mer i [Microsoft Defender ATP for Windows](../protect/advanced-threat-protection.md) (Använda Microsoft Defender ATP för Windows) i Intune-dokumentationen.
  - Windows-säkerhetsappen är installerad på alla enheter som kör Windows 10, och inga ytterligare krav finns.

## <a name="antivirus-profiles"></a>Antivirusprofiler

**macOS-profiler**:

- **Antivirus** – Hantera [Principinställningar för antivirus](../protect/antivirus-microsoft-defender-settings-macos.md) för macOS.

  När du använder [Microsoft Defender ATP för Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) kan du konfigurera och distribuera antivirusinställningar till dina hanterade macOS-enheter via Intune i stället för att konfigurera inställningarna med `.plist`-filer.

**Windows 10-profiler**:

- **Microsoft Defender Antivirus** – Hantera [principinställningar för antivirus](../protect/antivirus-microsoft-defender-settings-windows.md) för Windows 10.

  Defender Antivirus är nästa generations skyddskomponent i Microsoft Defender Avancerat skydd (Microsoft Defender ATP). Nästa generations skydd kombinerar maskininlärning, analys av stordata, detaljerad information om resistens mot hot, samt molninfrastruktur för att skydda enheter i företagsorganisationen.

  *Microsoft Defender Antivirus*-profilen är en separat instans av antivirusinställningarna som finns i *profilen för enhetsbegränsning* för enhetskonfigurationsprincipen.
  
  Till skillnad från antivirusinställningarna i en *profil för enhetsbegränsning* kan du använda de här inställningarna för att hantera enheter som är samhanterade. För att du ska kunna använda de här inställningarna måste [skjutreglaget för arbetsbelastning för samhantering av](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) Endpoint Protection vara inställt på Intune.

- **Windows-säkerhetsupplevelse** – Hantera [inställningar för Windows-säkerhetsappen](../protect/antivirus-security-experience-windows-settings.md) som slutanvändare kan visa i Microsoft Defender Security Center och vilka meddelanden de får. Windows-säkerhetsappen används av ett antal Windows-säkerhetsfunktioner för att tillhandahålla meddelanden om datorns hälsotillstånd och säkerhet. Säkerhetsmeddelanden innehåller brandväggar, antivirusprodukter, Windows Defender SmartScreen med mera.

## <a name="antivirus-policy-reports"></a>Rapporter om antivirusprinciper

Rapporter om antivirusprinciper visar statusinformation om dina Endpoint Security -antivirusprinciper och enhetsstatus. Rapporterna är tillgängliga i noden Slutpunktssäkerhet i administrationscentret för Microsoft Endpoint Manager.

Om du vill visa rapporterna går du till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och sedan till Endpoint Security och väljer **Antivirus**. Om du väljer Antivirus öppnas sammanfattningssidan. Ytterligare rapport- och statusvisningar är tillgängliga som ytterligare sidor.

### <a name="summary"></a>Sammanfattning

På sidan **Sammanfattning** kan du [skapa nya principer](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy) och visa en lista över de principer som har skapats tidigare. Listan innehåller detaljerad information nivå om profilen som principen omfattar (principtyp) och om principen är tilldelad.

![Översiktssida för antivirusprincip](./media/endpoint-security-antivirus-policy/antivirus-summary.png)

När du väljer en princip i listan öppnas sidan *Översikt* för principinstansen och visar mer information. När du väljer en panel från den här vyn visar Intune ytterligare information om profilen om den är tillgänglig.

![Översiktssida för antivirusprincip](./media/endpoint-security-antivirus-policy/policy-overview.png)

### <a name="windows-10-unhealthy-endpoints"></a>Defekta slutpunkter i Windows 10

På sidan **Defekta slutpunkter i Windows 10** kan du visa information om antivirusstatusen för dina MDM-hanterade Windows 10-enheter. Den här informationen returneras från Windows Defender Antivirus som körs på enheten, som *agentstatus för hot*.

Endast enheter med identifierade problem visas i den här vyn. Den här vyn visar inte information om enheter som identifieras som rensade.

![Översiktssida för antivirusprincip](./media/endpoint-security-antivirus-policy/antivirus-unhealthy-endpoints.png)

## <a name="next-steps"></a>Nästa steg

[Konfigurera säkerhetsprinciper för slutpunkt](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
