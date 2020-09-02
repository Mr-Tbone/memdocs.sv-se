---
title: Använda Microsoft Defender ATP i Microsoft Intune – Azure | Microsoft Docs
description: Använd Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) med Intune, inklusive installation och konfiguration, publicering av dina Intune-enheter med ATP och använd en ATP-riskutvärdering för enheter med dina Intune-principer för enhetsefterlevnad och villkorsstyrd åtkomst för att skydda nätverksresurserna.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1420bf03fe236decba0345e299eb5d5893f96c93
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915117"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Tvinga fram kompatibilitet för Microsoft Defender ATP med villkorlig åtkomst i Intune

Du kan integrera Microsoft Defender Avancerat skydd (Microsoft Defender ATP) med Microsoft Intune som en Skydd mot mobilhot-lösning. Integrationen kan hjälpa dig att förhindra säkerhetsöverträdelser och begränsa effekten av överträdelser inom en organisation.

Microsoft Defender ATP kan användas med enheter som kör Windows 10 eller senare och med Android-enheter.

Om det ska lyckas måste du använda följande konfigurationer tillsammans:

- **Etablera en tjänst-till-tjänst-anslutning mellan Intune och Microsoft Defender ATP**. Med den här anslutningen kan Microsoft Defender ATP samla in data om datorrisker från de enheter du hanterar med Intune.
- **Använd en enhetskonfigurationsprofil för att publicera enheter med Microsoft Defender ATP**. Du registrerar enheter för att konfigurera som så att de kommunicerar med Microsoft Defender ATP och för att tillhandahålla data som hjälper dem att utvärdera sin risknivå.
- **Använd en efterlevnadsprincip för enheter för att ange den risknivå som du vill tillåta**. Risknivåer rapporteras av Microsoft Defender ATP. Enheter som överskrider den tillåtna risknivån anses inte uppfylla efterlevnadskraven.
- **Använd en princip för villkorsstyrd åtkomst** till att blockera användare från att komma åt företagsresurser från enheter som inte uppfyller efterlevnadskraven.

När du integrerar Intune med Microsoft Defender ATP kan du använda TVM-funktionen i Microsoft Defender ATP (Threat & Vulnerability Management) och [använda Intune till att åtgärda sårbarheter i slutpunkter som TVM identifierar](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Exempel på användning av Microsoft Defender ATP med Intune

I följande exempel får du hjälp att förklara hur dessa lösningar fungerar tillsammans för att skydda din organisation. I det här exemplet är Microsoft Defender ATP och Intune redan integrerade.

Föreställ dig en händelse där någon skickar en Word-fil med inbäddad skadlig kod till en användare i din organisation.

- Användaren öppnar den bifogade filen och aktiverar innehållet.
- En attack med utökade privilegier startar och en angripare från en fjärrdator har administratörsrättigheter till den drabbade enheten.
- Angripare har sedan via fjärranslutning tillgång till användarens andra enheter. Det här säkerhetsintrånget kan påverka hela organisationen.

Microsoft Defender ATP kan lösa säkerhetshändelser som det här scenariot.

- I vårt exempel identifierar Microsoft Defender ATP att enheten körde onormal kod, upplevde en processeskalering, infogade skadlig kod och utfärdade ett misstänkt fjärrgränssnitt.
- Baserat på dessa åtgärder från enheten klassificerar Microsoft Defender ATP [enheten som associerad med hög risk](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) och inkluderar en detaljerad rapport om misstänkt aktivitet på Microsoft Defender Security Center-portalen.

Du kan integrera Microsoft Defender Avancerat skydd (Microsoft Defender ATP) med Microsoft Intune som en Skydd mot mobilhot-lösning. Integrationen kan hjälpa dig att förhindra säkerhetsöverträdelser och begränsa effekten av överträdelser inom en organisation.

Eftersom du har en efterlevnadspolicy för Intune-enheter som anger att enheter med risknivån *Medelhög* eller *Hög* inte uppfyller efterlevnadskraven anges den angripna enheten som icke-kompatibel. Den här klassificeringen gör att din princip för villkorlig åtkomst kan aktiveras och blockera åtkomst från enheten till företagets resurser.

För enheter som kör Android kan du använda Intune-principer när du ska ändra konfigurationen av Microsoft Defender ATP på Android. Mer information finns i [Microsoft Defender ATP-webbskydd](../protect/advanced-threat-protection-manage-android.md).

## <a name="prerequisites"></a>Krav

Om du vill använda Microsoft Defender ATP med Intune måste du ha följande konfigurerat och klart att använda:

- Licensierad klientorganisation för Enterprise Mobility + Security E3 och Windows E5 (eller Microsoft 365 Enterprise E5)
- Microsoft Intune-miljö med [Intune-hanterade](../enrollment/windows-enroll.md) Windows 10-enheter eller Android-enheter som även är Azure AD-anslutna
- [Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)-miljön som ger åtkomst till Microsoft Defender Security Center (ATP-portal)

> [!NOTE]
> Microsoft Defender ATP stöds inte med Intune-appskyddsprinciper för iOS/iPadOS och Android.

## <a name="next-steps"></a>Nästa steg

- Om du vill ansluta Microsoft Defender ATP till Intune, registrera enheter och konfigurera principer för villkorsstyrd åtkomst, så läs informationen i [Konfigurera Microsoft Defender ATP i Intune](../protect/advanced-threat-protection-configure.md).

Läs mer i Intune-dokumentationen:

- [Använd säkerhetsaktiviteter med ATP:ernas sårbarhetshantering när du ska åtgärda problem på enheterna](atp-manage-vulnerabilities.md)
- [Komma igång med principer för enhetsefterlevnad](device-compliance-get-started.md)

Läs mer i Microsoft Defender ATP-dokumentationen:

- [Villkorlig åtkomst för Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Instrumentpanel för Microsoft Defender ATP-risk](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)