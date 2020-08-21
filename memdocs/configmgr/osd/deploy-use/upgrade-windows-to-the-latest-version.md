---
title: Uppgradera till Windows 10
titleSuffix: Configuration Manager
description: Lär dig hur du använder Configuration Manager för att uppgradera ett operativ system från Windows 7 eller senare till Windows 10.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eb7e2e5c564263c7172d70ec33bb33c0dd73409c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697831"
---
# <a name="upgrade-windows-to-the-latest-version-with-configuration-manager"></a>Uppgradera Windows till den senaste versionen med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller stegen i Configuration Manager för att uppgradera operativ systemet på en dator. Du kan välja mellan olika distributionsmetoder, t.ex. fristående media eller Software Center. Uppgraderings scenariot på plats har följande funktioner:  

- Uppgraderar operativ systemet till Windows 10 eller Windows Server 2016 och senare

- Behåller program, inställningar och användar data på datorn

- Har inga externa beroenden, t. ex. Windows ADK

- Är snabbare och mer flexibelt än vanliga OS-distributioner

> [!Note]  
> Aktivitetssekvensen Windows 10 på plats-uppgradering stöder distribution till Internetbaserade klienter som hanteras via [Cloud Management Gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md). Den här möjligheten gör att fjärran vändare enklare kan uppgradera till Windows 10 utan att behöva ansluta till intranätet. Mer information finns i [distribuera uppgradering av Windows 10 på plats via CMG](deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->


## <a name="supported-versions"></a>Versioner som stöds

### <a name="upgrade-version"></a>Uppgraderings version

Du behöver bara skapa uppgraderings paket för operativ system för att uppgradera till följande OS-versioner:

- Windows 10
- Windows Server 2016
- Windows Server 2019

### <a name="original-version"></a>Ursprunglig version

Enheter måste köra en av följande OS-versioner för att rikta en aktivitetssekvens för operativ system uppgradering:

#### <a name="windows-client"></a>Windows-klient

- Windows 7
- Windows 8,1
- En tidigare version av Windows 10. Du kan till exempel uppgradera Windows 10, version 1809 till Windows 10, version 1903.  

Mer information finns i [uppgraderings vägar för Windows 10](/windows/deployment/upgrade/windows-10-upgrade-paths).

#### <a name="windows-server"></a>Windows Server

- Windows Server 2012
- Windows Server 2012 R2
- En tidigare version av Windows Server 2016
- En tidigare version av Windows Server 2019

Mer information om uppgraderings vägar för Windows Server som stöds finns i [Windows server 2016-uppgraderings vägar som stöds](/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016) och [Windows Server Upgrade Center](https://aka.ms/upgradecenter).


## <a name="plan"></a><a name="BKMK_Plan"></a> Projektplan  

### <a name="task-sequence-requirements-and-limitations"></a>Krav och begränsningar för aktivitetssekvens

Granska följande krav och begränsningar för aktivitetssekvensen för att uppgradera ett operativ system för att kontrol lera att det uppfyller dina behov:  

- Lägg endast till steg i aktivitetssekvensen som är relaterade till kärn uppgiften att uppgradera operativ systemet. De här stegen omfattar främst installation av paket, program eller uppdateringar. Använd också steg som kör kommando rader, PowerShell eller ange dynamiska variabler.  

- Granska driv rutiner och program som är installerade på datorer. Kontrol lera att driv rutinerna är kompatibla med Windows 10 innan du distribuerar aktivitetssekvensen för uppgradering.  

Följande uppgifter är inte kompatibla med uppgradering på plats. De kräver att du använder traditionella OS-distributioner:  

- Ändra datorns domän medlemskap eller uppdatera den lokala administratörs gruppen.  

- Implementera en grundläggande ändring på datorn, till exempel:

  - Ändra diskpartitioner
  - Ändra system arkitekturen från x86 till x64
  - Implementera UEFI. (Mer information om ett möjligt alternativ finns i [konvertera från BIOS till UEFI under en uppgradering på plats](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).)
  - Ändra det grundläggande OS-språket  

- Du har anpassade krav, inklusive att använda en anpassad bas avbildning, med disk kryptering från tredje part eller kräver offline-åtgärder från tredje part.  

### <a name="infrastructure-requirements"></a>Krav på infrastruktur  

Det enda krav som krävs för uppgraderings scenariot är att en distributions plats är tillgänglig. Distribuera uppgraderings paketet för operativ systemet och eventuella andra paket som du tar med i aktivitetssekvensen. Mer information finns i [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).


## <a name="configure"></a><a name="BKMK_Configure"></a> Konfigurera  

### <a name="prepare-the-os-upgrade-package"></a>Förbered uppgraderings paketet för operativ systemet  

Uppgraderings paketet för Windows 10 innehåller de källfiler som krävs för att uppgradera operativ systemet på mål datorn. Uppgraderings paketet måste vara av samma utgåva, arkitektur och språk som de klienter som du uppgraderar. Mer information finns i [hantera OS-uppgraderings paket](../get-started/manage-operating-system-upgrade-packages.md).  

### <a name="create-a-task-sequence-to-upgrade-the-os"></a>Skapa en aktivitetssekvens för att uppgradera operativ systemet  

Använd stegen i [skapa en aktivitetssekvens för att uppgradera ett operativ system](create-a-task-sequence-to-upgrade-an-operating-system.md) för att automatisera uppgraderingen av operativ systemet.  

> [!NOTE]  
> Om du vill skapa en aktivitetssekvens för att uppgradera ett operativ system till Windows 10 använder du vanligt vis stegen i [skapa en aktivitetssekvens för att uppgradera ett operativ system](create-a-task-sequence-to-upgrade-an-operating-system.md). Aktivitetssekvensen inkluderar steget **Uppgradera operativ system** , samt ytterligare rekommenderade steg och grupper för att hantera uppgraderings processen från slut punkt till slut punkt.
>
> Du kan skapa en anpassad aktivitetssekvens och lägga till steget [Uppgradera operativ system](../understand/task-sequence-steps.md#BKMK_UpgradeOS) . Det här steget är det enda som krävs för att uppgradera operativ systemet till Windows 10. Om du väljer den här metoden, för att slutföra uppgraderingen, lägger du även till steget [starta om datorn](../understand/task-sequence-steps.md#BKMK_RestartComputer) efter steget **Uppgradera operativ system** . Se till att använda den **aktuella installerade standard operativ system** inställningen för att starta om datorn i det installerade operativ systemet och inte till Windows PE.  


## <a name="deploy"></a><a name="BKMK_Deploy"></a> Distribuera  

Använd någon av följande distributions metoder för att distribuera operativ systemet:  

- [Använda Software Center för att distribuera Windows via nätverket](use-software-center-to-deploy-windows-over-the-network.md)  

- [Använda fristående media för att distribuera Windows utan att använda nätverket](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  > [!IMPORTANT]  
  > När du använder fristående media måste du inkludera en start avbildning i aktivitetssekvensen. Den här konfigurationen gör aktivitetssekvensen tillgänglig i guiden media för aktivitetssekvens.


## <a name="monitor"></a>Övervaka  

Information om hur du övervakar aktivitetssekvensdistribution för att uppgradera operativ systemet finns i [övervaka OS-distributioner](monitor-operating-system-deployments.md).