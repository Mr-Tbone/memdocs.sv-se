---
title: Hantera slutpunktssäkerhet i Microsoft Intune | Microsoft Docs
description: Lär dig hur säkerhetsadministratörer kan använda noden Endpoint Security till att hantera enhetssäkerhet och lösa problem med enheter i Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: e3ab2e31aa8a35ef04c150972cd7bb7650e46040
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879714"
---
# <a name="manage-endpoint-security-in-microsoft-intune"></a>Hantera slutpunktssäkerhet i Microsoft Intune

Som säkerhetsadministratör använder du noden *Slutpunktssäkerhet* i Intune till att konfigurera enhetssäkerhet och hantera säkerhetsaktiviteter för enheter när enheterna är utsatta för risk. Endpoint Security-policyerna är utformade för att hjälpa dig att fokusera på enheternas säkerhet och minimera risken. De uppgifter som är tillgängliga hjälper dig att identifiera enheter som är utsatta för risk, att åtgärda enheterna och återställa dem till ett säkrare tillstånd eller ett som uppfyller efterlevnadskraven.

I noden Endpoint Security finns de verktyg som är tillgängliga via Intune och som du använder till att skydda enheter:

- **Granska status för alla dina hanterade enheter**. Använd vyn [Alla enheter](#manage-devices) till att visa enheters efterlevnadsstatus från hög nivå och sedan visa mer information om vissa enheter för att förstå vilka efterlevnadspolicyer som inte uppfylls, så att du kan lösa dem.

- **Distribuera säkerhetsbaslinjer som upprättar beprövade säkerhetskonfigurationer för enheter**. I Intune finns det [säkerhetsbaslinjer](#manage-security-baselines) för Windows-enheter och en växande lista med program som Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) och Microsoft Edge. Säkerhetsbaslinjer är förkonfigurerade grupper av Windows-inställningar som hjälper dig att tillämpa en känd grupp av inställningar och standardvärden som rekommenderas av det relevanta säkerhetsteamet.

- **Hantera säkerhetskonfigurationer på enheter med smalt fokuserade policyer**.  Alla [Endpoint Security-policyer](#use-policies-to-manage-device-security) fokuserar på olika aspekter av enhetssäkerheten som virus, diskkryptering, brandväggar och andra områden som görs tillgängliga via integrering med Microsoft Defender ATP.

- **Upprätta krav på enheter och användare via efterlevnadspolicyer**. Med [efterlevnadspolicyer](../protect/device-compliance-get-started.md) anger du vilka regler som enheter och användare måste uppfylla för att anses uppfylla efterlevnadskraven. Reglerna kan gälla saker som operativsystemversion, lösenordskrav eller enhetens hotnivå.

  När du tillämpar efterlevnadspolicyer via integrering med [policyer för villkorsstyrd åtkomst](#configure-conditional-access) i Azure Active Directory (Azure AD) kan du begränsa åtkomsten till företagets resurser för både hanterade enheter och enheter som inte hanteras än.

- **Integrera Intune med ditt Microsoft Defender ATP-team**. Genom att [integrera med Microsoft Defender ATP](#set-up-integration-with-microsoft-defender-atp) får du tillgång till [säkerhetsaktiviteter](#review-security-tasks-from-microsoft-defender-atp). Säkerhetsaktiviteter integrerar Microsoft Defender ATP och Intune nära tillsammans så att ditt säkerhetsteam kan identifiera enheter som är utsatta för risk och skicka detaljerade åtgärdssteg till Intune-administratörer som sedan kan agera.

I följande avsnitt i den här artikeln går vi igenom olika aktiviteter som du kan utföra från noden Endpoint Security i administrationscentret och de RBAC-behörigheter (rollbaserad åtkomstkontroll) som krävs för att använda dem.

## <a name="manage-devices"></a>Hantera enheter

I noden Endpoint Security finns vyn *Alla enheter* där du kan se en lista med alla enheter från Azure AD som är tillgängliga i Microsoft Endpoint Manager.

I den här vyn kan du välja enheter och visa mer detaljerad information om dem, som vilka policyer en enhet inte efterlever. Du kan också använda den här vyn till att åtgärda problem för en enhet, som att starta om en enhet, starta en genomsökning efter skadlig kod eller rotera BitLocker-nycklar på en Windows 10-enhet.

Mer information finns i [Hantera enheter med slutpunktssäkerhet i Microsoft Intune](../protect/endpoint-security-manage-devices.md).

## <a name="manage-security-baselines"></a>Hantera säkerhetsbaslinjer

Säkerhetsbaslinjer i Intune är förkonfigurerade grupper av inställningar som utgör rekommendationer från det relevanta Microsoft-säkerhetsteamet för produkten. Intune har stöd för säkerhetsbaslinjer med enhetsinställningar för Windows 10, Microsoft Edge, Microsoft Defender Advanced Threat Protection och många fler.

Du kan använda säkerhetsbaslinjer till att snabbt distribuera en *beprövad* konfiguration med enhets- och programinställningar som skyddar dina användare och enheter. Du kan använda säkerhetsbaslinjer för enheter som kör Windows 10 version 1809 eller senare.

Mer information finns i [Använda säkerhetsbaslinjer till att konfigurera Windows 10-enheter i Intune](../protect/security-baselines.md).

Säkerhetsbaslinjer är en av flera metoder för att konfigurera inställningar på enheter i Intune. När du hanterar inställningar är det viktigt att du förstår vilka andra metoder som används till att konfigurera enheter i miljön så att du kan undvika konflikter. Läs mer under [Undvika policykonflikter](#avoid-policy-conflicts) längre fram i den här artikeln.

## <a name="review-security-tasks-from-microsoft-defender-atp"></a>Granska säkerhetsaktiviteter från Microsoft Defender ATP

När du integrerar Intune med Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) kan du granska de *säkerhetsaktiviteter* i Intune som identifierar riskenheter och rekommenderar steg som minimerar risken. Sedan kan du använda aktiviteterna för att rapportera tillbaka till Microsoft Defender ATP när riskerna har åtgärdats.

- Ditt Microsoft Defender ATP-team avgör vilka enheter som är utsatta för risk och skickar informationen till Intune-teamet som en säkerhetsaktivitet. Med några få klick kan de skapa en säkerhetsaktivitet för Intune som identifierar de enheter som är utsatta för risk, sårbarheten och ger vägledning om hur du kan minimera risken.

- Intune-administratörer granskar säkerhetsaktiviteter och arbetar sedan i Intune för att åtgärda de här aktiviteterna. När de har åtgärdats markeras aktiviteten som slutförd, och statusen skickas sedan tillbaka till Microsoft Defender ATP-teamet.

Med säkerhetsaktiviteter är båda teamen synkroniserade gällande vilka enheter som är utsatta för risk, samt hur och när de här riskerna åtgärdas.

Du kan läsa mer om säkerhetsaktiviteter i [Använda Intune till att åtgärda sårbarheter som upptäckts av Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md).

## <a name="use-policies-to-manage-device-security"></a>Använda policyer till att hantera enhetssäkerhet

Som säkerhetsadministratör använder du de säkerhetspolicyer som finns under *Hantera* i noden Endpoint Security. Med de här policyerna kan du konfigurera enhetssäkerhet utan att behöva navigera bland de många fler inställningarna i enhetskonfigurationsprofiler och säkerhetsbaslinjer.

![Hantera principer](./media/endpoint-security/endpoint-security-policies.png)

Mer information om hur du använder de här säkerhetspolicyerna finns i [Hantera enhetssäkerhet med Endpoint Security-policyer](../protect/endpoint-security-policy.md).

Endpoint Security-policyer är en av flera metoder för att konfigurera inställningar på enheter. När du hanterar inställningar är det viktigt att du förstår vilka andra metoder som används till att konfigurera enheter i miljön och att undvika konflikter. Läs mer under [Undvika policykonflikter](#avoid-policy-conflicts) längre fram i den här artikeln.

Under *Hantera* finns även policyer för *Enhetens efterlevnad* och *Villkorsstyrd åtkomst*. De här typerna av policyer är inte fokuserade säkerhetspolicyer för konfigurering av slutpunkter, men de är viktiga verktyg när du ska hantera enheter och åtkomsten till företagets resurser.

## <a name="use-device-compliance-policy"></a>Använda policyn Enhetens efterlevnad

Använd policyn Enhetens efterlevnad till att fastställa de villkor som enheter och användare måste uppfylla för att få åtkomst till nätverket och företagets resurser.

Vilka [efterlevnadsinställningar som är tillgängliga](../protect/device-compliance-get-started.md#next-steps) beror på vilken plattform du använder, men här är några vanliga policyregler:

- Krav på att enheter kör en lägsta eller en viss operativsystemversion
- Lösenordskrav
- En högsta tillåten hotnivå enligt Microsoft Defender ATP eller någon annan Mobile Threat Defense-partner

Utöver policyreglerna så har efterlevnadspolicyer stöd för:

- [Platser](../protect/use-network-locations.md) som du definierar i Intune. När du använder platser med en efterlevnadspolicy kan policyn ange att enheter måste vara anslutna till ett arbetsnätverk.
- [Åtgärder vid inkompatibilitet](../protect/actions-for-noncompliance.md). De här åtgärderna är en tidsordnad sekvens med åtgärder som ska tillämpas på enheter som inte uppfyller efterlevnadsreglerna. Åtgärderna kan vara att skicka e-post eller meddelanden som varnar enhetsanvändaren om att efterlevnaden inte uppfylls, att fjärrlåsa enheter eller till och med att ta enheter som inte uppfyller efterlevnadskraven ur drift och radera eventuell företagsinformation på enheten.

När du tillämpar efterlevnadspolicyer via integrering av Intune med [policyer för villkorsstyrd åtkomst](#configure-conditional-access) i Azure AD kan du använda efterlevnadsdata till att begränsa åtkomsten till företagets resurser för både hanterade enheter och enheter du inte hanterar.

Läs mer i [Ange regler för enheter som tillåter åtkomst till resurser i din organisation med Intune](../protect/device-compliance-get-started.md).

Policyer för enhetens efterlevnad är en av flera metoder för att konfigurera inställningar på enheter. När du hanterar inställningar är det viktigt att du förstår vilka andra metoder som används till att konfigurera enheter i miljön och att undvika konflikter. Läs mer under [Undvika policykonflikter](#avoid-policy-conflicts) längre fram i den här artikeln.

## <a name="configure-conditional-access"></a>Konfigurera villkorlig åtkomst

För att skydda dina enheter och företagets resurser kan du använda policyer för villkorsstyrd åtkomst i Azure Active Directory (Azure AD) med Intune.

Intune skickar resultatet av policyerna för enhetens efterlevnad till Azure AD, som sedan tillämpar policyer för villkorsstyrd åtkomst för att fastställa vilka enheter och appar som har åtkomst till företagets resurser. Policyerna för villkorsstyrd åtkomst kan hjälpa dig att begränsa åtkomsten för enheter som inte hanteras via Intune. Du kan även använda efterlevnadsdata från [Mobile Threat Defense-partner](../protect/mobile-threat-defense.md) som du integrerar med Intune.

Här är två vanliga metoder för att använda villkorsstyrd åtkomst med Intune:

- **Enhetsbaserad villkorsstyrd åtkomst**, som gör att bara hanterade enheter som uppfyller efterlevnadskraven kan komma åt nätverksresurser.
- **Appbaserad villkorsstyrd åtkomst**, där appsäkerhetspolicyer används till att hantera åtkomsten till nätverksresurser för användare på enheter du inte hanterar via Intune.

Mer information om att använda villkorsstyrd åtkomst med Intune finns i [Läs mer om villkorsstyrd åtkomst och Intune](../protect/conditional-access.md).

## <a name="set-up-integration-with-microsoft-defender-atp"></a>Konfigurera integreringen med Microsoft Defender ATP

När du integrerar Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) med Intune förbättrar du möjligheten att identifiera och reagera på risker.

Intune kan visserligen integreras med flera [Mobile Threat Defense-partner](../protect/mobile-threat-defense.md), men när du använder Microsoft Defender ATP får du en nära integrering mellan Defender ATP och Intune och tillgång till flera alternativ för ett djupgående enhetsskydd, bland annat:

- Säkerhetsaktiviteter – smidig kommunikation mellan ATP och Intune-administratörer om enheter utsatta för risk, hur de kan åtgärdas och en bekräftelse när riskerna har åtgärdats.
- Smidigare registrering av Microsoft Defender ATP på klienter.
- Användning av risksignaler för ATP-enheter i Intunes efterlevnadspolicyer.
- Åtkomst till funktioner för *manipulationsskydd*.

 Mer information om att använda Microsoft Defender ATP med Intune finns i [Tvinga fram efterlevnad för Microsoft Defender ATP med villkorsstyrd åtkomst i Intune](../protect/advanced-threat-protection.md).

## <a name="role-based-access-control-requirements"></a>Krav för rollbaserad åtkomstkontroll

För att kunna hantera aktiviteter i noden Endpoint Security i administrationscentret för Microsoft Endpoint Manager måste kontot:

- Ha tilldelats en licens för Intune.
- Ha rollbaserad åtkomstbehörighet som motsvarar de behörigheter som ges med den inbyggda Intune-rollen **Endpoint Security Manager** (Endpoint Security-ansvarig). Rollen som *Endpoint Security-ansvarig* ger åtkomst till administrationscentret för Microsoft Endpoint Manager. Den här rollen kan användas av personer som hanterar säkerhet och efterlevnadsfunktioner som säkerhetsbaslinjer, enhetskompatibilitet, villkorsstyrd åtkomst och Microsoft Defender ATP.

Mer information finns i [Rollbaserad åtkomstkontroll (RBAC) med Microsoft Intune](../fundamentals/role-based-access-control.md)

### <a name="permissions-granted-by-the-endpoint-security-manager-role"></a>Behörigheter som beviljas med rollen som *Endpoint Security-ansvarig*

Du kan visa följande lista med behörigheter i administrationscentret för Microsoft Endpoint Manager genom att gå till **Administration av klientorganisation** > **Roller** > **Alla roller**, välj **Endpoint Security Manager** > **Egenskaper**.

**Behörigheter:**

- **Android for Work**
  - Läs
- **Granska data**
  - Läs
- **ID:n för företagsenheter**
  - Läs
- **Efterlevnadsprinciper för enheter**
  - Tilldela
  - Skapa
  - Ta bort
  - Läs
  - Uppdatera
  - Visa rapporter
- **Enhetskonfigurationer**
  - Läs
- **Hanterare av enhetsregistrering**
  - Läs
- **Endpoint Protection-rapporter**
  - Läs
- **Registreringsprogram**
  - Läs enhet
  - Läs profil
  - Läs token
- **Intune-informationslager**
  - Läs
- **Hanterade appar**
  - Läs
- **Hanterade enheter**
  - Ta bort
  - Läs
  - Ställ in primär användare
  - Uppdatera
- **Mobilappar**
  - Läs
- **Organisation**
  - Läs
- **PolicySets**
  - Läs
- **Fjärrhjälp**
  - Läs
- **Fjärråtgärder**
  - Hämta FileVault-nyckel.
- **Roller**
  - Läs
- **Säkerhetsbaslinjer**
  - Tilldela
  - Skapa
  - Ta bort
  - Läs
  - Uppdatera
- **Säkerhetsaktiviteter**
  - Läs
  - Uppdatera
- **Telekomkostnader**
  - Läs
- **Allmänna villkor**
  - Läs

## <a name="avoid-policy-conflicts"></a>Undvika policykonflikter

Många av de inställningar du kan konfigurera för enheter kan hanteras av olika funktioner i Intune. Här är några exempel på sådana funktioner:

- Endpoint Security-policyer
- Säkerhetsbaslinjer
- Policyer för enhetskonfiguration
- Policyer för Windows 10-registrering

Inställningarna i Endpoint Security-policyerna är till exempel en delmängd av de inställningar som finns i profilerna *slutpunktsskydd* och *enhetsbegränsningar* i enhetenskonfigurationspolicyn, och de kan också hanteras via olika säkerhetsbaslinjer.

Ett sätt att undvika konflikter är att inte använda olika baslinjer, instanser av samma baslinje eller olika typer av policyer och instanser till att hantera samma inställningar för en enhet. Det här kräver att du planerar vilka metoder du ska använda för att distribuera konfigurationer till olika enheter. När du använder flera metoder eller instanser av samma metod till att konfigurera samma inställning måste du se till att dina olika metoder antingen fungerar tillsammans eller inte distribueras till samma enheter.

Om det uppstår konflikter kan du använda Intunes inbyggda verktyg till att identifiera och åtgärda orsaken till konflikterna. Mer information finns i:

- [Felsöka principer och profiler i Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Övervaka dina säkerhetsbaslinjer](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Nästa steg

Konfigurera:

- [Säkerhetsbaslinjer](../protect/security-baselines.md)
- [Efterlevnadspolicyer](../protect/device-compliance-get-started.md)
- [Policyer för villkorsstyrd åtkomst](#configure-conditional-access)
- [Integrering med Microsoft Defender ATP](../protect/advanced-threat-protection.md)
