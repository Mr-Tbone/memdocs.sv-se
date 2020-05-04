---
title: Stöd för Windows 10
titleSuffix: Configuration Manager
description: Lär dig mer om de Windows 10-versioner som stöds som klienter eller för OSD med Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7241db0220bf4adf9b55341514afb03de33c2589
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709630"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Stöd för Windows 10 i Configuration Manager  

*Gäller för: Configuration Manager (aktuell gren)*

Lär dig mer om de Windows 10-versioner som Configuration Manager stöder, inklusive:

- [Windows 10 som en Configuration Manager-klient](#windows-10-as-a-client)
- [Windows Assessment and Deployment Kit (ADK) för Windows 10](#windows-10-adk)

> [!Tip]
> Windows Server-versioner som en-klient stöds på samma sätt som den associerade Windows 10-versionen. Windows Server 2016 är till exempel samma versions version som Windows 10 LTSB 2016 och Windows Server version 1803 är samma version som Windows 10 version 1803.
>
> Mer information om Windows Server som ett plats system finns i [operativ system som stöds för Configuration Manager plats system servrar](supported-operating-systems-for-site-system-servers.md#bkmk_core).

## <a name="windows-10-as-a-client"></a>Windows 10 som en klient

Configuration Manager försöker tillhandahålla stöd som en klient för varje ny Windows 10-version så snart som möjligt när den blir tillgänglig. Eftersom produkterna har separata utvecklings-och publicerings scheman är det stöd som Configuration Manager som är beroende av när de blir tillgängliga.

En Configuration Manager-version sjunker från matrisen när [stöd för den versionen](../../servers/manage/current-branch-versions-supported.md) avslutas. På samma sätt kan stöd för Windows 10-versioner som Enterprise 2015 LTSB eller 1511 försvinna från matrisen när de tas bort från supporten.

- Den senaste versionen av Configuration Manager aktuella grenen tar emot både säkerhets uppdateringar och viktiga uppdateringar, som kan innehålla korrigeringar för problem med Windows 10-versioner. När Microsoft släpper en ny version av Configuration Manager aktuella grenen, tar tidigare versioner bara emot säkerhets uppdateringar. Mer information finns i [stöd för Configuration Manager aktuella gren versioner](../../servers/manage/current-branch-versions-supported.md).  

    > [!Note]  
    > Det bästa sättet att hålla sig uppdaterad med Windows 10 är att hålla dig uppdaterad med Configuration Manager. Mer information finns i [Configuration Manager och Windows som en tjänst](../../understand/configuration-manager-and-windows-as-service.md).  

- Den här informationen kompletterar [operativ system som stöds för klienter och enheter](supported-operating-systems-for-clients-and-devices.md).  

- Om du använder den långsiktiga etablerings grenen för Configuration Manager, se [konfigurationer som stöds för långsiktig service gren](../../understand/supported-configurations-for-ltsb.md).  

I följande tabell visas de versioner av Windows 10 som du kan använda som en klient med olika versioner av Configuration Manager.

| Windows 10-version | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|---------------------|-----|-----|-----|-----|-----|
| **Enterprise 2015-LTSB** <!--10/14/2025-->   | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) |
| **Enterprise 2016-LTSB** <!--10/13/2026-->   | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) |
| **Enterprise LTSC 2019** <!--01/09/2029-->   | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) |
| **1709**<br>(10.0.16299)   <!--04/14/2020-->   | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![Stöds inte](media/Red_X.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/11/2021-->   | ![Stöds inte](media/Red_X.png) | ![Stöds inte](media/Red_X.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

Mer information om Windows-livscykel finns i [fakta bladet för Windows-livscykel](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)

| Nyckel |
|--|
| ![Stöds](media/green_check.png) = **Supported**  |
| ![](media/Red_X.png) = **Stöds inte** |

### <a name="windows-10-client-support-notes"></a><a name="bkmk_win10-notes"></a>Support anteckningar för Windows 10-klienten

- Stöd för Windows 10-halvårs kanal versioner innehåller följande utgåvor: Enterprise, Pro, Education och Pro Education.  

- Från och med version 1906 stöder Configuration Manager Windows 10 Pro för arbets Station.

- För Windows 10, version 1909, visar operativ Systems distributions mediet versionen som 10.0.18362.418.

### <a name="windows-10-on-arm64"></a><a name="bkmk_arm64"></a>Windows 10 på ARM64

Configuration Manager stöder klienten på Windows 10 ARM64-enheter. OS-distribution stöds inte.<!-- 1353704 -->

Från och med version 2002,<!--5954175--> **alla Windows 10-plattformar (arm64)** finns i listan över operativ system versioner som stöds på objekt med krav regler eller tillämplighets listor.

> [!NOTE]
> Om du tidigare har valt **Windows 10** -plattformen på den översta nivån, markeras den här åtgärden automatiskt både **alla windows 10 (64-bitars)** och **alla Windows 10 (32-bitars)**. Den här nya plattformen väljs inte automatiskt. Om du vill lägga till **alla Windows 10 (arm64)** väljer du det manuellt i listan.

### <a name="support-for-windows-insider"></a><a name="bkmk_WIfB-support"></a>Stöd för Windows Insider

Från och med Configuration Manager version 1906 kan du [Uppdatera och underhålla Windows Insider-](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB) versioner. Den här funktionen tillhandahålls som en bekvämlighet för våra kunder. Även om den här funktionen ska fungera är supporten för den bästa ansträngningen. Configuration Manager kanske inte utfärdar någon snabb korrigering för den här funktionen om den upphör att fungera.  

Om du vill ge feedback om Windows Insider använder du [feedback Hub](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback).

## <a name="windows-10-adk"></a>Windows 10 ADK

När du distribuerar operativ system med Configuration Manager är Windows ADK ett nödvändigt externt beroende. Mer information finns i följande artiklar:

- [Infrastrukturkrav för distribution av operativsystem](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [Hämta Windows ADK för Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > Från och med Windows 10 version 1809 är Windows PE ett separat installations program. Annars finns det ingen funktionell skillnad.
    >
    > Se till att ladda ned både **Windows ADK för Windows 10** och **Windows PE-tillägget för ADK**.

I följande tabell visas de versioner av Windows 10 ADK som du kan använda med olika versioner av Configuration Manager.

| Windows 10 ADK-version  | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|--------------------|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![Stöds inte](media/Red_X.png)   | ![Stöds inte](media/Red_X.png) | ![Stöds inte](media/Red_X.png) | ![Stöds inte](media/Red_X.png) | ![Stöds inte](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![Bakåtkompatibla](media/blue_compat.png) | ![Bakåtkompatibla](media/blue_compat.png) | ![Stöds inte](media/Red_X.png) | ![Stöds inte](media/Red_X.png) | ![Stöds inte](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Bakåtkompatibla](media/blue_compat.png) | ![Bakåtkompatibla](media/blue_compat.png) | ![Stöds inte](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![Stöds inte](media/Red_X.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) | ![Stöds](media/green_check.png) |

|Nyckel|
|--|
| ![Stöds](media/green_check.png) = **Supported** <br/> I den här tabellen visas endast stöd för Windows ADK i relation till versionen av Configuration Manager. Microsoft rekommenderar att du använder Windows ADK som matchar den version av Windows som du distribuerar. Använd den senaste Windows ADK-versionen när du distribuerar den senaste versionen av Windows 10. Den senaste versionen av Windows ADK kan ha stöd för distribution av äldre OS-versioner, t. ex. Windows 8,1.<!-- SCCMDocs issue 1229 --> Mer information om stöd för Windows ADK-komponenter finns i [DISM-plattformar som stöds](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) och [USMT-krav](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![  = **Backward compatible** Bakåtkompatibelt](media/blue_compat.png)bakåtkompatibla <br/> Den här kombinationen testas inte utan bör fungera. Vi kommer att dokumentera eventuella kända problem eller varningar. |
| ![](media/Red_X.png) = **Stöds inte** |

### <a name="windows-10-adk-support-notes"></a><a name="bkmk_adk-notes"></a>Support anteckningar för Windows 10 ADK

- Configuration Manager stöder endast x86-och amd64-komponenter i Windows 10 ADK. Det stöder för närvarande inte ARM-eller ARM64-komponenter.

- Windows Server-versioner har samma Windows ADK-krav som den associerade Windows 10-versionen. Windows Server 2016 är till exempel samma versions version som Windows 10 LTSB 2016.
