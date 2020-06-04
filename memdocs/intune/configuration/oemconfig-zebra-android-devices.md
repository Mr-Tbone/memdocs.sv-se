---
title: Distribuera många OEMConfig-profiler till Zebra-enheter med Microsoft Intune – Azure | Microsoft Docs
description: Använd Microsoft Intune till att skapa och distribuera flera OEMConfig-profiler för enhetskonfiguration på Zebra-enheter som kör Android Enterprise. Använd Zebra-åtgärder och steg till att ordna dina profiler.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2227face347e6d82cf7807bea241eda4856c1d67
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988687"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>Distribuera flera OEMConfig-profiler till Zebra-enheter i Microsoft Intune

I Microsoft Intune kan du använda OEMConfig till att anpassa OEM-specifika inställningar för Android Enterprise-enheter. De här inställningarna är speciella för enhetstillverkaren och distribueras med hjälp av konfigurationsprofiler i Intune.

På Zebra-enheter kan du distribuera eller tilldela flera profiler till samma enhet. Befintliga OEMConfig-profiler kan använda den här funktionen nästa gången enheten synkroniseras med Intune.

Den här funktionen gäller för:

- Zebra-enheter som kör Android Enterprise

Mer information om OEMConfig, inklusive vad det gör och hur du använder det, finns i [OEMConfig-konfigurationsprofil](android-oem-configuration-overview.md).

Den här artikeln beskriver hur du distribuerar flera OEMConfig-profiler till Zebra-enheter, hur du ordnar dem och använder rapportfunktionerna i Microsoft Intune.

## <a name="prerequisites"></a>Krav

Skapa en [OEMConfig-konfigurationsprofil](android-oem-configuration-overview.md).

## <a name="use-multiple-profiles"></a>Använda flera profiler

På Zebra-enheter kan du ha flera profiler på varje enhet samtidigt. Den här funktionen gör att du kan dela upp dina Zebra OEMConfig-inställningar i mindre profiler. Zebras OEMConfig-schema använder också **åtgärder**. Åtgärder är operationer som körs på enheten. De konfigurerar inte några inställningar. Använd de här åtgärderna till saker som att utlösa filnedladdning eller rensa Urklipp. Du hittar en fullständig lista med åtgärder som stöds i [Zebra-dokumentationen](https://techdocs.zebra.com/oemconfig/10-0/about/) (detta öppnar Zebra-webbplatsen).

Du kan till exempel skapa en Zebra OEMConfig-profil som tillämpar vissa inställningar på enheten. En annan Zebra OEMConfig-profil innehåller en åtgärd som rensar Urklipp. Du tilldelar den första profilen till en Zebra-enhetsgrupp. Senare måste du rensa Urklipp på de här enheterna. Du tilldelar den andra profilen till samma enhetsgrupp utan att ändra den första profilen. Enheternas Urklipp rensas utan att du skickar eller påverkar konfigurationsinställningarna som skapades i den första profilen.

I ett annat exempel har du tilldelat en OEMConfig-profil som konfigurerade några Zebra-enhetsinställningar. Användare har börjat rapportera problem med ett visst program och du vill rensa appens cacheminne. Skapa en ny OEMConfig-profil som endast innehåller åtgärden ”rensa cacheminnet”. Tilldela profilen till de enheter som behöver den.

## <a name="ordering"></a>Ordna profiler

När du har flera profiler på varje enhet är inte ordningen som profilerna distribueras i självklar. Det här beteendet är en begränsning hos Google Play. Om du vill köra åtgärderna i en viss följd kan du använda [Zebras transaktionsfunktion](https://techdocs.zebra.com/oemconfig/9-1/mc/) (öppnar Zebras webbplats). Nu ska vi titta på ett exempel.

Vi har två profiler:

- **Profil 1**: Aktiverar Bluetooth. Den här profilen tilldelas på måndagen till gruppen **Alla enheter**.
- **Profil 2**: Konfigurerar andra inställningar. Den här profilen tilldelas på tisdagen till gruppen **Alla enheter**.

Bluetooth måste vara aktiverat innan den andra inställningen konfigureras.

På onsdagen registrerar du 10 nya Zebra-enheter i Intune. Profil 1 och profil 2 tilldelas till gruppen **Alla enheter**. När de nya enheterna synkroniseras med Intune får de profilerna. De här enheterna kan få profil 2 innan profil 1.

Med funktionen **Steg** i Zebra-schemat kan du se till att åtgärderna körs i rätt följd. I det här fallet skapar du en profil som har två transaktionssteg. Det första steget innehåller Bluetooth-inställningarna och det andra steget konfigurerar den andra inställningen. När Zebras OEMCong-app tar emot profilen körs stegen i rätt ordning.

Mer information finns i [Zebras transaktionssteg](https://techdocs.zebra.com/oemconfig/9-1/mc/) (öppnar Zebras webbplats).

## <a name="enhanced-reporting"></a>Förbättrad rapportering

Du distribuerar en profil och den körs av Zebras OEMConfig-app på enheten. Zebras OEMConfig-app rapporterar profilstatusen till Intune. I administrationscentret för Endpoint Manager ser du statusen för distribuerade OEMConfig-profiler och eventuella fel eller varningar.

1. Öppna [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj din Zebra OEMConfig-profil > **Övervaka** > **Enhetsstatus**. Det här alternativet visar de enheter som har tilldelats din OEMConfig-profil.
3. Välj en enhet > **Enhetskonfiguration** > välj din Zebra OEMConfig-profil. Med det här alternativet visas de profilinställningarna som har lyckats eller misslyckats.

    Välj en rad med ett fel. Du ser mer information om vad som orsakat felet.

## <a name="next-steps"></a>Nästa steg

- Läs mer om [OEMConfig-konfigurationsprofiler](android-oem-configuration-overview.md).
- Konfigurera [Mobility Extensions (MX)](android-zebra-mx-overview.md) i Android-enhetsadministratör.
- [Övervaka profilstatus](device-profile-monitor.md).
