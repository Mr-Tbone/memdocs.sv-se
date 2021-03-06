---
title: Registrera Android-enheter i Intune
titleSuffix: Microsoft Intune
description: Läs hur du registrerar Android-enheter i Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/23/2019
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f276d98c-b077-452a-8835-41919d674db5
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d8506661c49fa4f9c8481a3caa96883c91e6d8bb
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461767"
---
# <a name="enroll-android-devices"></a>Registrera Android-enheter

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Du kan hantera registrera Android-enheter som Intune-administratör på följande sätt:
- Android Enterprise (erbjuder en uppsättning registreringsalternativ som ger användarna de mest aktuella och säkra funktionerna):
    - [**Android Enterprise-arbetsprofil**](android-work-profile-enroll.md): För personliga enheter som har åtkomst till företagets data. Administratörer kan hantera arbetskonton, appar och data. Personliga data på enheten lagras separat från arbetsdata och administratörer har ingen kontroll över personliga inställningar eller data. 
    - [**Android Enterprise-dedikerad**](android-kiosk-enroll.md): För företagsägda enheter med ett enda användningsområde, till exempel digital signering, biljettutskrift eller lagerhantering. Administratörer låser användningen av enheten för en begränsad uppsättning appar och webblänkar. Användarna kan heller inte lägga till andra appar eller att vidta andra åtgärder på enheten.
    - [**Fullständigt hanterad Android Enterprise**](android-fully-managed-enroll.md): För företagsägda enheter med enskilda användare som används enbart för arbete och inte för personligt bruk. Administratörer kan hantera hela enheten och tillämpa principkontroller som inte är tillgängliga för arbetsprofiler.
    - [**Android Enterprise – företagsägd med arbetsprofil**](android-corporate-owned-work-profile-enroll.md): För företagsägda enheter är enheter för enkelanvändare avsedda för företagsbruk och personligt bruk.
- [**Android-enhetsadministratör**](android-enroll-device-administrator.md), inklusive Samsung Knox Standard-enheter och [Zebra-enheter](../configuration/android-zebra-mx-overview.md). 

## <a name="prerequisites"></a>Krav

Förbered hantering av mobila enheter genom att ange MDM-utfärdare som **Microsoft Intune**. Fler anvisningar finns i [Ange MDM-utfärdare](../fundamentals/mdm-authority-set.md). Du anger det här objektet bara när du konfigurerar Intune för hantering av mobila enheter.

För Android Enterprise, se följande supportartikel från Google för att säkerställa att Android Enterprise är tillgänglig i ditt land eller din region: https://support.google.com/work/android/answer/6270910

För enheter som har tillverkats av Zebra Technologies kan du behöva bevilja ytterligare behörigheter till företagsportalen beroende på kapaciteten hos enheten i fråga. Mer information finns i [Mobility Extensions på Zebra-enheter](../configuration/android-zebra-mx-overview.md).

För Samsung Knox Standard-enheter finns [fler krav](android-samsung-knox-mobile-enroll.md).

## <a name="next-steps"></a>Nästa steg

- [Konfigurera registrering av Android Enterprise-arbetsprofiler](android-work-profile-enroll.md)
- [Konfigurera registrering av dedikerade Android Enterprise-enheter](android-kiosk-enroll.md)
- [Konfigurera registrering av fullständigt hanterade Android Enterprise-registreringar](android-fully-managed-enroll.md)
- [Konfigurera administratörsregistrering för Android-enhet](android-enroll-device-administrator.md)

