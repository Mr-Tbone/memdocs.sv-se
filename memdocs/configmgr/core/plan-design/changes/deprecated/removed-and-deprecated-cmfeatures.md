---
title: Föråldrade funktioner
titleSuffix: Configuration Manager
description: Lär dig mer om de funktioner som Configuration Manager inte längre stöder.
ms.date: 08/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: aca9dc5c2ff2d88155ab19656f391cf87a4e977f
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068097"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Borttagna och föråldrade funktioner för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln listas de funktioner som är inaktuella eller borttagna från stöd för Configuration Manager. Inaktuella funktioner tas bort i en framtida uppdatering. De här framtida ändringarna kan påverka din användning av Configuration Manager.  

Den här informationen kan komma att ändras i framtida versioner. Den kan inte innehålla alla inaktuella Configuration Manager-funktioner.

## <a name="deprecated-features"></a>Föråldrade funktioner

Följande funktioner är föråldrade. Du kan fortfarande använda dem nu, men Microsoft planerar att avsluta supporten i framtiden.

|Funktion|Första meddelande om utfasning|Stöd har &nbsp; tagits bort|
|-----------|---|--------------|
|Den geografiska vyn i noden **platshierarki** i arbets ytan **övervakning** i Configuration Manager-konsolen.<!--8116777-->|Augusti 2020|TBD|
|Implementeringen av delning av innehåll från Azure har ändrats. Använd en Content-aktiverad Cloud Management Gateway. Du kommer inte att kunna skapa en traditionell moln distributions plats i framtiden.|Februari 2019|TBD<sup>[Anmärkning 1](#bkmk_note1)</sup>|
|Klassisk tjänst distribution till Azure för Cloud Management Gateway och en moln distributions plats. Mer information finns i [plan for CMG](../../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).|November 2018|TBD<sup>[Anmärkning 1](#bkmk_note1)</sup>|

### <a name="note-1-support-removed-tbd"></a><a name="bkmk_note1"></a> Anmärkning 1: stöd borttagen TBD

Den angivna tids ramen måste bestämmas (TBD). Microsoft rekommenderar att du ändrar till den nya processen eller funktionen, men du kan fortsätta att använda den inaktuella processen eller funktionen för nära framtid.

## <a name="unsupported-and-removed-features"></a>Funktioner som inte stöds och som tagits bort

Följande funktioner stöds inte längre. I vissa fall är de inte längre i produkten.

|Funktion|Första meddelande om utfasning|Stöd har &nbsp; tagits bort|  
|-----------|---|--------------|  
| Skriv bords analys om du vill **Visa senaste data** för enhets registrering och säkerhets uppdateringar.<!-- 7080949 --> Mer information finns i [data svars tid](../../../../desktop-analytics/troubleshooting.md#data-latency).|Maj 2020|Juli 2020|
| Windows Analytics och Uppgraderingsberedskap-integrering. Mer information finns i [KB 4521815: pensionering i Windows Analytics den 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement). | 14 oktober 2019 | 31 januari 2020 |
| Utvärdering av enhetens hälsoattestering för efterlevnadsprinciper för villkorlig åtkomst <!--1235616 aka 3608202--> Mer information finns i [vad hände med hybrid MDM](../../../../mdm/understand/what-happened-to-hybrid.md).| 3 juli 2019 | Version 1910 |
| Configuration Manager Företagsportal-appen | 21 maj, 2019 | Version 1910 |
| Program katalogen, inklusive båda plats system rollerna: webbplatsen för program katalogen och webb tjänst platsen. Mer information finns i [ta bort program katalogen](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). | 21 maj, 2019 | Version 1910 |
|Certifikatbaserad autentisering med Windows Hello för företag-inställningar i Configuration Manager<br>Mer information finns i [Inställningar för Windows Hello för företag](../../../../protect/deploy-use/windows-hello-for-business-settings.md).|December 2017|Version 1910|
|System Center-Endpoint Protection för Mac och Linux<br>Mer information finns i [blogg inlägget End of support](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257).|Oktober 2018|31 december 2018|
|Lokal villkorlig åtkomst<br>Mer information finns i [vad hände med hybrid MDM](../../../../mdm/understand/what-happened-to-hybrid.md).|30 januari 2019|1 september 2019|
|Hantering av mobila hybrid enheter (MDM)<br>Mer information finns i [vad hände med hybrid MDM](../../../../mdm/understand/what-happened-to-hybrid.md).<br><br>Från och med 1902 Intune Service Release, förväntades i slutet av februari 2019, kan nya kunder inte skapa en ny hybrid anslutning.<!--Intune feature 2683117-->|14 augusti 2018|1 september 2019|
|SCAP-tillägg (Security Content Automation Protocol). <!--3607889--><br>Den tidigare certifierade versionen är fortfarande tillgänglig på [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=48741).|September 2018|Version 1810|
|**Användar upplevelsen för Silverlight** för program katalogens webbplats stöds inte längre. Användarna bör använda det nya Software Center. Mer information finns i [Konfigurera Software Center](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).<!--1358309-->|11 augusti 2017| Version 1806|
|Den tidigare versionen av Software Center.<br><br>Mer information om det nya Software Center finns i [Planera för och konfigurera program hantering](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_userex).|13 december 2016|Version 1802|
|Hantering av virtuella hård diskar (VHD: er) med Configuration Manager. <br><br>Den här utfasningen inkluderar borttagning av alternativ för att skapa en ny virtuell hård disk eller hantera en virtuell hård disk med hjälp av en aktivitetssekvens och borttagning av noden virtuella hård diskar från Configuration Manager-konsolen. <br><br>Befintliga virtuella hård diskar tas inte bort, men de är inte längre tillgängliga i Configuration Manager-konsolen.  |6 januari 2017 |Version 1710|
|Aktivitetssekvenser: <br /> -Konvertera disk till dynamisk <br /> -Installera distributions verktyg |18 november 2016|Version 1710|
|Verktyg för uppgraderings bedömning<br><br>Uppgraderings bedömnings verktyget är beroende av både Configuration Manager och Application Compatibility Toolkit (ACT) 6. x. Den slutgiltiga versionen av ACT levererades i Windows 10 v1511 ADK. Eftersom det inte finns några ytterligare uppdateringar av ACT, är supporten för verktyget för uppgraderings bedömning upphör att gälla. Utfasnings meddelandet lades till i [nedladdnings sidan för UAT](https://www.microsoft.com/software-download/windows10) den 12 september 2016. | 12 september 2016  | 11 juli 2017 |
|Program uppdaterings platser med ett NLB-kluster (utjämning av nätverks belastning) | 27 februari 2016 | Version 1702 |
|Aktivitetssekvenser: <br /> - OSDPreserveDriveLetter  <br /><br /> Under en operativ Systems distribution bestämmer Installationsprogrammet för Windows nu den bäst enhets beteckning som ska användas (vanligt vis C:). Om du vill ange en annan enhet som ska användas kan du ändra platsen i steget Använd operativ systemets aktivitetssekvens. Gå till sidan **Välj den plats där du vill använda den här inställningen för operativ systemet** . Välj en **speciell logisk enhets beteckning** och välj den enhet som du vill använda. |20 juni 2016 |Version 1606 |
|Network Access Protection (NAP) – som du hittar i System Center 2012 Configuration Manager|10 juli 2015|Version 1511|  
|Out-of-band-hantering – som hittas i System Center 2012 Configuration Manager|16 oktober 2015|Version 1511|

### <a name="features-removed-in-version-1511"></a>Funktioner som tagits bort i version 1511

Följande avsnitt innehåller ytterligare information om funktioner som har tagits bort med version 1511:

#### <a name="out-of-band-management"></a><a name="bkmk_amt"></a> Out-of-band-hantering  

Med Configuration Manager har det inbyggda stödet för AMT-baserade datorer inifrån Configuration Manager-konsolen tagits bort.  

- AMT-baserade datorer förblir fullständigt hanterade när du använder [Intel SCS-tillägget för Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html). Tillägget ger dig till gång till de senaste funktionerna för att hantera AMT och ta bort begränsningar som introduceras tills Configuration Manager kan inkludera ändringarna.  

- Out-of-band-hantering i System Center 2012 Configuration Manager påverkas inte av den här ändringen.  

#### <a name="network-access-protection"></a><a name="bkmk_nap"></a> Network Access Protection

Configuration Manager har tagit bort stöd för Network Access Protection. Funktionen är föråldrad i Windows Server 2012 R2 och har tagits bort från Windows 10.  

För alternativ till nätverksåtkomstskydd, se avsnittet *Föråldrade funktioner* i [Översikt över nätverkspolicy och åtkomsttjänster](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831683(v=ws.11)).

## <a name="see-also"></a>Se även

- [Borttaget och inaktuellt](removed-and-deprecated.md)
- [Microsoft Support livs cykel](https://support.microsoft.com/lifecycle)
- [Stöd för aktuella gren versioner av Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)