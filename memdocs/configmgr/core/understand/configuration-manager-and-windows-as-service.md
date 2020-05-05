---
title: Configuration Manager och Windows som en tjänst
titleSuffix: Configuration Manager
description: Få grundläggande information om hur du antar Configuration Manager aktuella grenen för att stödja Windows som en tjänst.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e92a39a91c60734f212c7d1e99e266d0ec9a4008
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718555"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>Configuration Manager och Windows som en tjänst

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager ger omfattande kontroll över funktions uppdateringar för Windows 10. För att fullständigt införa Windows som en tjänst modell måste du också använda Configuration Manager aktuella gren modellen. För att hålla dig uppdaterad med Windows 10 måste du hålla dig uppdaterad med Configuration Manager för bästa möjliga upplevelse. Nya versioner av Configuration Manager krävs för att dra full nytta av de spännande nya företags funktionerna i Windows 10. Den här artikeln är avsedd att vara en landnings sida för viktiga artiklar som krävs för att anta Configuration Manager aktuella grenen. Configuration Manager aktuella grenen får du på ditt sätt till Windows som en tjänst.

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Viktiga artiklar om hur du antar Configuration Manager aktuella grenen

| Artikel        | Beskrivning          | 
| ------------- |-------------|
|[Översikt över Configuration Manager aktuella grenen](../plan-design/changes/whats-new-incremental-versions.md)|Innehåller en kort sammanfattning av viktiga punkter för den nya underhålls modellen för Configuration Manager (Current Branch)|
|[Support livs cykel](../servers/manage/current-branch-versions-supported.md)|Förklarar den nya support-och underhålls modellen.|
|[Borttagna och föråldrade objekt](../plan-design/changes/deprecated/removed-and-deprecated.md)|Ger ett tidigt meddelande om framtida ändringar som kan påverka din användning av Configuration Manager.|
|[Uppdateringar till Configuration Manager aktuella grenen](../servers/manage/updates.md)|Förklarar den enkla konsol metoden för att tillämpa funktions uppdateringar på Configuration Manager.|
|[Hämta tillgängliga uppdateringar](../servers/manage/install-in-console-updates.md#get-available-updates)|Förklarar de två lägena som är tillgängliga för att hämta nya Configuration Manager funktions uppdateringar.|
|[Uppdatera Check lista](../servers/manage/install-in-console-updates.md#bkmk_beforeinstall)|Tillhandahåller uppdaterings-/regionsspecifika check listor, om tillämpligt.| 
|[Installera nya Configuration Manager funktions uppdateringar](../servers/manage/install-in-console-updates.md#bkmk_install)|Förklarar de enkla installations stegen för funktions uppdateringar.|
|[Stöd för Windows 10](../plan-design/configs/support-for-windows-10.md)|Innehåller en support mat ris för Windows 10-versioner (och ADK).|
|[Tekniska för hands versionerna av Configuration Manager](../get-started/technical-preview.md)|Innehåller information om det tekniska för hands versions programmet för ConfigMgr.|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>Viktiga artiklar om hur du antar Windows som en tjänst

| Artikel        | Beskrivning          |
| ------------- |-------------|
|[Hantera Windows som en tjänst](../../osd/deploy-use/manage-windows-as-a-service.md)|Förklarar hur du använder Service planer för att distribuera funktions uppdateringar för Windows 10.|
|[Uppgradera Windows 10 via aktivitetssekvens](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)|Information om att skapa en aktivitetssekvens för att uppgradera Windows 10 med ytterligare rekommendationer.|
|[Fasindelade distributioner](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)|Stegvisa distributioner automatiserar en samordnad, sekvenserad distribution av en aktivitetssekvens över flera samlingar.|  
|[Optimera leverans för Windows 10-uppdatering](../../sum/deploy-use/optimize-windows-10-update-delivery.md)|Använd Configuration Manager för att hantera uppdaterings innehåll för att hålla dig uppdaterad med Windows 10.|
|[Använda Skriv bords analys](../../desktop-analytics/overview.md)|Med Desktop Analytics kan du utvärdera och analysera enheternas beredskap i din miljö för en uppgradering till Windows 10.|
|[Windows Update for Business-integration (valfritt)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)|Förklarar hur du definierar och distribuerar principer för Windows Update för företag (WUfB) med hjälp av Configuration Manager.|
|[Använda samhantering med Microsoft Intune och Windows Update för företag (valfritt)](../../comanage/overview.md)|Ger en översikt över samhantering|


## <a name="related-articles"></a>Relaterade artiklar

- [Uppgradering på plats till Configuration Manager aktuell gren från System Center 2012 Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md)
- [Planera för migrering till Configuration Manager aktuella grenen](../migration/planning-for-migration.md)
