---
title: Begränsningar för enhetsregistrering för säkerhetskonfigurationsramverket för Android Enterprise
titleSuffix: Microsoft Intune
description: Begränsningar för enhetsregistrering för säkerhetskonfigurationsramverket för Android Enterprise.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d26040c5a009a9c3877abbc25512e317f584f114
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.contentlocale: sv-SE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85503030"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Enhetsregisteringsbegränsningar för Android Enterprise

Innan du registrerar enheter för [konfigurationsramverket för Android Enterprise]() måste organisationerna konfigurera lämpliga begränsningar. Dessa begränsningar säkerställer att användare bara kan registrera sig
- godkända enheter.
- ett angivet antal enheter.
- enheter med angivna plattformar.
- enheter med angivet operativsystem.
- enheter från angivna tillverkare.

Mer information om begränsningar för enhetsregistrering finns i [Ange begränsningar för registrering](enrollment-restrictions-set.md).

## <a name="work-profile-basic-level-1-security-restrictions"></a>Arbetsprofil grundläggande (nivå 1) säkerhetsbegränsningar

Följande enhetsbegränsningar måste implementeras för Android Enterprise arbetsprofil grundläggande begränsningar (nivå 1):

| Typ | Plattform | Version | Tillåter personliga enheter |
|--------|--------|--------|--------|
| Android enterprise | Tillåt | Android 5.0 och senare.<p>Microsoft rekommenderar att du konfigurerar den lägsta Android-huvudversionen så att den matchar de Android-versioner som stöds för Microsoft-appar. OEM-tillverkare och enheter som följer rekommenderade krav för Android Enterprise måste ha stöd för den aktuella leveransversionen plus en bokstavsuppgradering.   För närvarande rekommenderar Android 8.0 och senare för kunskapsarbetare. Mer information finns i [Rekommenderade krav för Android Enterprise](https://www.android.com/enterprise/recommended/requirements/). | Ja |
| Android-enhetsadministratör| Blockera | Alla versioner | Ja |

## <a name="work-profile-high-level-3-security-restrictions"></a>Arbetsprofil hög (nivå 3) säkerhetsbegränsningar
Följande enhetsbegränsningar måste implementeras för Android Enterprise arbetsprofil hög säkerhet (nivå 3):

| Typ | Plattform | Version | Tillåter personliga enheter |
|--------|--------|--------|--------|
| Android enterprise | Tillåt | Android 8.0 och senare | Ja |
| Android-enhetsadministratör| Blockera | Alla versioner | Ja |

## <a name="fully-managed-security-restrictions"></a>Fullständigt hanterade säkerhetsbegränsningar
Se till att organisationen har stöd för en fullständigt hanterad enhetsregistrering för Android Enterprise genom att granska en fullständigt hanterad Android Enterprise-registrering. 

## <a name="next-steps"></a>Nästa steg

[Ange appkonfigurationsprinciper](android-app-configuration-policies.md)
