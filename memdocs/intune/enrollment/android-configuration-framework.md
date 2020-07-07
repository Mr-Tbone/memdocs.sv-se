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
ms.openlocfilehash: 6f0e4452f5209d569e11a782528582f4d5a76045
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.contentlocale: sv-SE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85503035"
---
# <a name="android-enterprise-security-configuration-framework"></a>Säkerhetskonfiguration för ramverk för Android Enterprise

Säkerhetskonfigurationsramverket för Android Enterprise är en serie rekommendationer för inställningarna för enhetsefterlevnad och konfigurationsprinciper. Med dessa rekommendationerna kan du skräddarsy din organisations säkerhetsskydd för mobila enheter efter dina behov.

Säkerhetsmedvetna organisationer ser till att företagsdata på mobila enheter är skyddade. En metod som används för att skydda dessa data är genom enhetsregistrering. Enhetsregistrering hjälper organisationer:
- distribuera efterlevnadsprinciper (t.ex. PIN-styrka, upplåsning/rotverifiering och så vidare).
- distribuera konfigurationsprinciper (som WiFi, certifikat, VPN).
- hantera applivscykeln.

För att hjälpa dig att skapa ett komplett säkerhetsscenario introducerade Microsoft en ny taxonomi för [säkerhetskonfigurationer i Windows 10](https://aka.ms/secconframework). Intune använder en liknande taxonomi för säkerhetskonfigurationsramverket för Android Enterprise. De innehåller rekommenderade inställningar för enhetskompatibilitet och enhetsbegränsningar för grundläggande, utökad och hög säkerhet. Den här taxonomin beskrivs i följande artiklar:

1. [Distributionsmetod för Android Enterprise-ramverket](framework-deployment-methodology.md): En rekommenderad metod för att distribuera säkerhetskonfigurationsramverket.
2. [Begränsningar för Android-enhetsregistrering](device-enrollment-restrictions.md): Enhetsbegränsningar före registreringen för Android Enterprise-enheter.
3. [Lägga till appkonfigurationsprinciper för Android Enterprise-enheter](android-app-configuration-policies.md): Konfigurera appar på enheterna så att de inte tillåter personliga konton.
4. [Säkerhetsinställningar för Android Enterprise-arbetsprofiler](android-work-profile-security-settings.md): Specifika konfigurationsinställningar för grundläggande och hög säkerhet på arbetsprofilsenheter.
5. [Säkerhetsinställningar för fullständigt hanterade Android Enterprise-enheter](android-fully-managed-security-settings.md): Specifika konfigurationsinställningar för grundläggande, utökad och hög säkerhet för fullständigt hanterade enheter.

## <a name="android-enterprise-enrollment-modes"></a>Android Enterprise-registreringslägen

Med Android 5.0 har Google introducerat Android Enterprise, som innehåller två registreringslägen. Säkerhetskonfigurationsramverket för Android Enterprise innehåller rekommendationer för bägge lägena.
- [Fullständigt hanterade enheter (enhetsägare)](android-fully-managed-enroll.md): För företagsägda som är associerade med en enskild användare. Sådana enheter är exklusivt till för arbete och inte personligt bruk.
- [Arbetsprofil (profilägare)](android-work-profile-enroll.md): Normalt för personligt ägda enheter där IT vill ha en tydlig gräns mellan arbetsdata och personliga data. Principer som styrs av IT ser till att arbetsdata inte kan överföras till den personliga profilen.


## <a name="next-steps"></a>Nästa steg

[Distributionsmetod för Android Enterprise-ramverket](framework-deployment-methodology.md)