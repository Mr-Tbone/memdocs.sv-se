---
title: Installera Windows på en ny dator
titleSuffix: Configuration Manager
description: Använd Configuration Manager för att installera ett operativ system på en ny dator (Bare Metal) med hjälp av PXE, OEM eller fristående media.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7eb880b6cb6f45de06b602bc9caa8ca7b98022d5
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125090"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-configuration-manager"></a>Installera en ny version av Windows på en ny dator (Bare Metal) med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller de allmänna stegen i Configuration Manager för att installera ett operativ system på en ny dator. I det här scenariot kan du välja bland många olika distributionsmetoder, till exempel PXE, OEM eller fristående media. Om du är osäker på om det här är rätt distributions scenario för operativ systemet kan du läsa [scenarier för att distribuera operativ system i företag](scenarios-to-deploy-enterprise-operating-systems.md).  

Använd följande avsnitt om du vill uppdatera en befintlig dator med en ny version av Windows.  

##  <a name="plan"></a><a name="BKMK_Plan"></a>Projektplan  

-   **Planera och implementera infrastrukturkrav**  

     Det finns flera infrastruktur krav som måste finnas på plats innan du kan distribuera operativ system, till exempel Windows ADK, Windows Deployment Services (WDS), konfigurationer som stöds och så vidare. Mer information finns i [infrastruktur krav för operativ Systems distribution](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).

##  <a name="configure"></a><a name="BKMK_Configure"></a>Konfigurera  

1.  **Förbereda en startavbildning**  

     Startavbildningar startar en dator i en Windows PE-miljö (ett minimalt operativsystem med begränsade komponenter och tjänster) som sedan kan installera ett fullständigt Windows-operativsystem på datorn.   När du distribuerar operativsystem måste du välja en startavbildning som ska användas och distribuera avbildningen till en distributionsplats. Använd följande för att förbereda startavbildningen:  

    -   Mer information om start avbildningar finns i [Hantera start avbildningar](../get-started/manage-boot-images.md).  

    -   Mer information om hur du anpassar en start avbildning finns i [Anpassa Start avbildningar](../get-started/customize-boot-images.md).  

    -   Distribuera startavbildningen till distributionsplatser. Mer information finns i avsnittet [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Förbereda en operativsystemavbildning**  

     Operativsystemavbildningen innehåller de filer som krävs för att installera operativsystemet på måldatorn. Använd följande för att förbereda operativsystemavbildningen:  

    -   Mer information om hur du skapar en operativ system avbildning finns i [Hantera operativ system avbildningar](../get-started/manage-operating-system-images.md).

    -   Distribuera operativsystemavbildningen till distributionsplatser. Mer information finns i avsnittet [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

    > [!NOTE]
    > Nya installationer av Windows kan också utföras från installationskällfilerna via uppgraderings paket för operativ system, men Använd OS-avbildningar som **install. wim** i stället.
    >
    > Distribution av nya installationer av Windows via operativ system uppgraderings paket stöds fortfarande, men är beroende av driv rutiner som är kompatibla med den här metoden. När du installerar Windows från ett uppgraderings paket för operativ system installeras driv rutinerna även när du fortfarande använder Windows PE och helt enkelt matas in i Windows PE. Vissa driv rutiner är inte kompatibla med att installeras i Windows PE. Om driv rutinerna inte är kompatibla med att installeras i Windows PE kan du använda en operativ system avbildning i stället.  

3.  **Skapa en aktivitetssekvens för att distribuera operativsystem över nätverket**  

     Använd en aktivitetssekvens för att automatisera installationen av operativsystemet över nätverket. Använd stegen i [skapa en aktivitetssekvens för att installera ett operativ system](create-a-task-sequence-to-install-an-operating-system.md) för att skapa en aktivitetssekvens för att distribuera operativ systemet. Beroende på vilken distributionsmetod du väljer kan det finnas ytterligare överväganden för aktivitetssekvensen.  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a>Distribuera  

-   Använd någon av följande distributionsmetoder för att distribuera operativsystemet:  

    -   [Använda PXE för att distribuera Windows via nätverket](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Använd multicast för att distribuera Windows via nätverket](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Skapa en avbildning för en OEM-tillverkare i fabriken eller lokal anläggning](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Använda fristående media för att distribuera Windows utan att använda nätverket](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Använda startbara media för att distribuera Windows via nätverket](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Övervaka  

-   **Övervaka aktivitetssekvensdistributionen**  

     Information om hur du övervakar aktivitetssekvensdistribution för att installera operativ systemet finns i [övervaka operativ Systems distributioner](monitor-operating-system-deployments.md).  
