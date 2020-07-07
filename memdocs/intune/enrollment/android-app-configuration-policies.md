---
title: Säkerhetskonfiguration för ramverk för Android Enterprise
titleSuffix: Microsoft Intune
description: Läs om de begränsningar och inställningar som föreslås för grundläggande och hög säkerhet för Android Enterprise-enheter.
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
ms.openlocfilehash: 6ecd15ea98ff9fa5ff0ff6ff570e644a8dcf5003
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.contentlocale: sv-SE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85503047"
---
# <a name="android-enterprise-security-configuration-framework-app-configuration-policies"></a>Appkonfigurationsprinciper för säkerhetskonfigurationsramverk för Android Enterprise

Som en del av [säkerhetskonfigurationsramverket för Android Enterprise](android-configuration-framework.md) måste du korrekt ange appkonfigurationsprinciper för Android Enterprise-enheter.

Android Enterprise arbetsprofilenheter är utformade för att isolera arbetsdata och personliga data från varandra. Fullständigt hanterade Android Enterprise-enheter är endast utformade för arbets- eller skoldata. Därför behöver Microsoft-appar som distribueras på dessa enheter konfigureras för att neka personliga konton.

## <a name="disallow-personal-accounts-for-microsoft-apps-on-android-enterprise-devices"></a>Neka personliga konton för Microsoft-appar på Android Enterprise-enheter

1. Lägg till apparna i hanterad Google Play. Du hittar mer information i [Lägg till hanterade Google Play-appar till Android enterprise-enheter med Intune](../apps/apps-add-android-for-work.md).
2. Skapa en princip för varje hanterad Google Play-app enligt beskrivningen i [Lägga till appkonfigurationsprinciper för hanterade Android Enterprise-enheter]().
3. Skapa följande enskilda nyckel i varje princip:

    | Tangent | Värden |
    | --- | --- |
    | com.microsoft.intune.mam.AllowedAccountUPNs | Ett eller flera avgränsade UPN-namn.<br>Endast tillåtna konton är de hanterade användarkonton som anges av den här nyckeln.<br>För Intune-registrerade enheter, kan {{userprincipalname}}-token användas för att representera det registrerade användarkontot. |


## <a name="next-steps"></a>Nästa steg
Använd [Säkerhetsinställningarna för Android Enterprise-arbetsprofilen](android-work-profile-security-settings.md) eller [Säkerhetsinställningarna för fullständigt hanterad Android Enterprise](android-fully-managed-security-settings.md).