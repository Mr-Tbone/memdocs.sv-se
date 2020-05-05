---
title: Ersätta en befintlig dator och överföra inställningar
titleSuffix: Configuration Manager
description: I Configuration Manager väljer du från distributions metoder, till exempel startbara media, multicast eller Software Center, för att ersätta en befintlig dator med en ny dator.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d28f4363-9e8a-4c54-9cb7-0594fabfff26
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b494fd5d9623af9de16d68e3d30e0e78a4ef338
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723777"
---
# <a name="replace-an-existing-computer-and-transfer-settings-with-configuration-manager"></a>Ersätt en befintlig dator och överföra inställningar med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller de allmänna stegen i Configuration Manager att ersätta en befintlig dator med en ny dator. I det här scenariot kan du välja bland många olika distributionsmetoder, till exempel startbara media, multicast eller Software Center. Du kan också välja att installera en tillståndsmigreringsplats för att lagra inställningar och återställa dem till det nya operativsystemet när det har installerats. Om du är osäker på om det här är rätt distributions scenario för operativ systemet kan du läsa [scenarier för att distribuera operativ system i företag](scenarios-to-deploy-enterprise-operating-systems.md).  

 Använd följande avsnitt om du vill uppdatera en befintlig dator med en ny version av Windows.  

##  <a name="plan"></a><a name="BKMK_Plan"></a>Projektplan  

-   **Planera och implementera infrastrukturkrav**  

     Det finns flera infrastruktur krav som måste finnas på plats innan du kan distribuera operativ system, till exempel Windows ADK, User State Migration Tool (USMT), Windows Deployment Services (WDS), stöd för hård diskar som stöds osv. Mer information finns i [infrastruktur krav för operativ Systems distribution](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)  

-   **Installera en tillståndsmigreringsplats (krävs endast om du överför inställningar)**  

     När du ska avbilda inställningar från den befintliga datorn och sedan återställa inställningarna till det nya operativsystemet måste du installera en tillståndsmigreringsplats. Mer information finns i avsnittet [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="configure"></a><a name="BKMK_Configure"></a>Konfigurera  

1.  **Förbereda en startavbildning**  

     Startavbildningar startar en dator i en Windows PE-miljö (ett minimalt operativsystem med begränsade komponenter och tjänster) som sedan kan installera ett fullständigt Windows-operativsystem på datorn. När du distribuerar operativsystem måste du välja en startavbildning som ska användas och distribuera avbildningen till en distributionsplats. Använd följande för att förbereda startavbildningen:  

    -   Mer information om start avbildningar finns i [Hantera start avbildningar](../get-started/manage-boot-images.md).  

    -   Mer information om hur du anpassar en start avbildning finns i [Anpassa Start avbildningar](../get-started/customize-boot-images.md).  

    -   Distribuera startavbildningen till distributionsplatser. Mer information finns i avsnittet [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Förbereda en operativsystemavbildning**  

     Operativsystemavbildningen innehåller de filer som krävs för att installera operativsystemet på måldatorn. Använd följande för att förbereda operativsystemavbildningen:  

    -   Mer information om hur du skapar en operativ system avbildning finns i [Hantera operativ system avbildningar](../get-started/manage-operating-system-images.md).  

    -   Distribuera operativsystemavbildningen till distributionsplatser. Mer information finns i avsnittet [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Skapa en aktivitetssekvens för att distribuera operativsystem över nätverket**  

     Använd en aktivitetssekvens för att automatisera installationen av operativsystemet över nätverket. Använd stegen i [skapa en aktivitetssekvens för att installera ett operativ system](create-a-task-sequence-to-install-an-operating-system.md) för att skapa en aktivitetssekvens för att distribuera operativ systemet. Beroende på vilken distributionsmetod du väljer kan det finnas ytterligare överväganden för aktivitetssekvensen.  

    > [!NOTE]  
    >  Om du avbildar och återställer användarinställningar och filer kan du välja att använda en tillståndsmigreringsplats eller spara filen lokalt i det här scenariot. Mer information finns i [hantera användar tillstånd](../get-started/manage-user-state.md).  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a>Distribuera  

-   Använd någon av följande distributionsmetoder för att distribuera operativsystemet:  

    -   [Använda Software Center för att distribuera Windows via nätverket](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Använda startbara media för att distribuera Windows via nätverket](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Använd multicast för att distribuera Windows via nätverket](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Skapa en avbildning för en OEM-tillverkare i fabriken eller lokal anläggning](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

## <a name="monitor"></a>Övervaka  

-   **Övervaka aktivitetssekvensdistributionen**  

     Information om hur du övervakar aktivitetssekvensdistribution för att installera operativ systemet finns i [övervaka operativ Systems distributioner](monitor-operating-system-deployments.md).  
