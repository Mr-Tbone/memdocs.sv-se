---
title: Begränsningar för enhetsregistrering för säkerhetskonfigurationsramverket för Android Enterprise
titleSuffix: Microsoft Intune
description: Begränsningar för enhetsregistrering för säkerhetskonfigurationsramverket för Android Enterprise.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/02/2020
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
ms.openlocfilehash: 6629f416dbbc9555514dfc305db8f224f6b76526
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088453"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Enhetsregisteringsbegränsningar för Android Enterprise

Innan du registrerar enheter för [konfigurationsramverket för Android Enterprise](android-configuration-framework.md) måste organisationerna konfigurera lämpliga begränsningar. Dessa begränsningar säkerställer att användare bara kan registrera sig

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
Se till att organisationen har stöd för en fullständigt hanterad enhetsregistrering för Android Enterprise genom granska [Registrera fullständigt hanterade enheter](android-fully-managed-enroll.md#enroll-the-fully-managed-devices). 

## <a name="conditional-access-policies"></a>Villkorliga åtkomstprinciper
Organisationer kan använda principer för villkorsstyrd åtkomst i Azure AD för att säkerställa att användarna endast kan komma åt arbets- eller skolinnehåll på registrerade Android-enheter. För att göra detta behöver du en princip för villkorsstyrd åtkomst som är riktad mot alla potentiella användare. Information om hur du skapar den här principen finns i [Kräva hanterade enheter för åtkomst till molnapp med villkorsstyrd åtkomst](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices). 

Följ stegen i [Scenario: Kräv enhetsregistrering för iOS- och Android-enheter](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices#scenario-require-device-enrollment-for-ios-and-android-devices), vilket garanterar att endast registrerade mobila enheter som är kompatibla kan ansluta till Office 365-slutpunkter.

## <a name="next-steps"></a>Nästa steg

[Ange appkonfigurationsprinciper](android-app-configuration-policies.md)
