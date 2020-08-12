---
title: Uppdatera en befintlig dators operativ system
titleSuffix: Configuration Manager
description: Du kan använda flera metoder i Configuration Manager för att partitionera och formatera en befintlig dator och installera ett nytt operativ system på datorn.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b635301d9d5bd8a0fb81771255acddb21097f23b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124910"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Uppdatera en befintlig dator med en ny version av Windows

*Gäller för: Configuration Manager (aktuell gren)*

Använd Configuration Manager för att partitionera och formatera en befintlig dator och installera ett nytt operativ system. Den här processen kallas ibland för åter *avbildning* eller *rensning och belastning*. I det här scenariot väljer du bland många olika distributions metoder, till exempel PXE, startbara media eller Software Center. Du kan också använda en plats för tillståndsmigrering för att lagra inställningar och sedan återställa dem till det nya operativ systemet.

Om du vill välja rätt distributions scenario för operativ system, se [scenarier för att distribuera operativ system i företag](scenarios-to-deploy-enterprise-operating-systems.md).  

## <a name="plan"></a><a name="BKMK_Plan"></a>Projektplan  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>Planera för och implementera infrastruktur krav

Det finns flera infrastruktur krav som måste finnas på plats innan du kan distribuera ett operativ system. Några av dessa krav är Windows ADK, User State Migration Tool (USMT) och Windows Deployment Services (WDS). Mer information finns i [infrastruktur krav för distribution av operativ system](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="install-a-state-migration-point"></a>Installera en plats för tillståndsmigrering

Om du vill avbilda inställningar från en befintlig dator och sedan återställa inställningarna till det nya operativ systemet, bör du överväga att använda en plats för tillståndsmigrering. Mer information finns i avsnittet [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="configure"></a><a name="BKMK_Configure"></a>Konfigurera  

### <a name="prepare-a-boot-image"></a>Förbereda en startavbildning

Start avbildningar startar en dator i en Windows PE-miljö. Windows PE är ett minimalt operativ system med begränsade komponenter och tjänster. Från Windows PE kan Configuration Manager installera ett fullständigt Windows-operativsystem på datorn.

Mer information finns i följande artiklar:

- [Hantera startavbildningar](../get-started/manage-boot-images.md)

- [Anpassa startavbildningar](../get-started/customize-boot-images.md)

- [Distribuera innehåll](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="prepare-an-os-image"></a>Förbereda en operativ system avbildning

Operativ system avbildningen innehåller de filer som krävs för att installera operativ systemet på mål datorn.

Mer information finns i följande artiklar:

- [Hantera avbildningar av operativsystem](../get-started/manage-operating-system-images.md)

- [Distribuera innehåll](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Skapa en aktivitetssekvens för att distribuera ett operativ system

Använd en aktivitetssekvens för att automatisera installationen av operativ systemet. Beroende på vilken distributionsmetod du väljer kan det finnas ytterligare överväganden för aktivitetssekvensen.

Mer information finns i följande artiklar:

- [Skapa en aktivitetssekvens för att installera ett operativsystem](create-a-task-sequence-to-install-an-operating-system.md)

- [Hantera användartillstånd](../get-started/manage-user-state.md)

## <a name="deploy"></a><a name="BKMK_Deploy"></a>Distribuera

- Använd någon av följande distributions metoder för att distribuera operativ systemet:  

  - [Använda PXE för att distribuera Windows via nätverket](use-pxe-to-deploy-windows-over-the-network.md)  

  - [Använd multicast för att distribuera Windows via nätverket](use-multicast-to-deploy-windows-over-the-network.md)  

  - [Skapa en avbildning för en OEM-tillverkare i fabriken eller lokal anläggning](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [Använda fristående media för att distribuera Windows utan att använda nätverket](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  - [Använda startbara media för att distribuera Windows via nätverket](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [Använda Software Center för att distribuera Windows via nätverket](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Övervaka  

Mer information finns i [övervaka OS-distributioner](monitor-operating-system-deployments.md).  

> [!Note]
> När du skapar en avbildning av en UEFI-enhet skapar Windows Boot Manager en ny post i Start programmet. Det här beteendet märks mest när du upprepade gånger återavbildningen av en enhet, till exempel i en test miljö eller student labb. Det påverkar normalt inte enhetens prestanda eller användning. Om listan blir för stor kan vissa specifika maskin varu enheter drabbas av funktions problem. T. ex. om du inte startar till en extern USB-enhet eller inte kan välja den aktuella start posten i listan. Ta bort oanvända start poster med hjälp av Windows **bcdedit** -kommandot. Mer information finns i [bcdedit-/deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue).<!-- 2841926 -->
