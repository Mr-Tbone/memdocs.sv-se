---
title: Stöd för virtualisering
titleSuffix: Configuration Manager
description: Kraven för att installera Configuration Manager-klient-och plats system roller i en Virtualization-miljö.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d2977fc34e9c398e9e266cbc9b223ea74a1dd18
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700239"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Stöd för virtualiseringslösningar med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager stöder installation av klient-och plats system roller för operativ system som stöds och som körs som en virtuell dator i vissa virtualiseringslösningar. Det här stödet finns även när den virtuella värden (virtualiseringsplattformen) inte stöds som en klient eller plats Server.

Du kan till exempel använda Microsoft Hyper-V Server 2016 för att vara värd för en virtuell dator som kör Windows Server 2019. Du kan installera klient-eller plats system rollerna på den virtuella datorn som kör Windows Server 2019. Du kan inte installera klienten på värden som kör Microsoft Hyper-V Server 2016.

## <a name="virtualization-environments"></a>Virtualiseringslösningar

- Windows Server 2019  
- Windows Server 2016 <sup> [Anmärkning 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup> [Anmärkning 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

<a name="bkmk_note1"></a>

> [!NOTE]
> Configuration Manager stöder inte [kapslad virtualisering](/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), som är ny i Windows Server 2016.

### <a name="virtualization-environment-support"></a>Stöd för Virtualization Environment

Varje virtuell dator måste ha samma eller större maskin-och program varu krav som du skulle använda för en fysisk Configuration Manager dator.

Om du vill kontrol lera att Configuration Manager stöder din virtualiseringslösning använder du verifierings programmet för Server virtualisering. Den innehåller en guide för support princip för virtualisering online. Mer information finns i [Windows Server Virtualization Validation program](https://www.windowsservercatalog.com/svvp.aspx).

Configuration Manager kan inte hantera virtuella datorer om de är offline. Configuration Manager-klienten på värddatorn kan inte hantera en VM-avbildning offline. Det går till exempel inte att installera program uppdateringar eller samla in maskin varu inventering.

I allmänhet ger Configuration Manager inga särskilda överväganden för virtuella datorer. Om du till exempel stoppar en virtuell dator och inte sparar dess tillstånd kan Configuration Manager kanske inte avgöra om den måste installera om en program uppdatering.

För att hjälpa till med Configuration Manager klient prestanda i virtuella miljöer som stöder flera användarsessioner inaktive ras användar principer som standard. Från och med version 1910 kan du aktivera användar principer i det här scenariot. Mer information finns i [om klient inställningar – aktivera användar princip för flera](../../clients/deploy/about-client-settings.md#enable-user-policy-for-multiple-user-sessions)användarsessioner.

## <a name="microsoft-azure-vms"></a><a name="bkmk_Azure"></a> Microsoft Azure virtuella datorer

Configuration Manager kan köras på virtuella datorer i Azure precis som den körs lokalt i ditt data Center. Använd Configuration Manager med virtuella Azure-datorer i följande scenarier:

- **Scenario 1**: kör Configuration Manager på en virtuell Azure-dator. Använd den för att hantera klienter på andra virtuella Azure-datorer.

- **Scenario 2**: kör Configuration Manager på en virtuell Azure-dator. Använd den för att hantera klienter som inte körs på Azure.

- **Scenario 3**: kör olika Configuration Manager plats system roller på virtuella Azure-datorer. Kör andra roller i ditt lokala data Center som är korrekt anslutna till Azure.

Samma Configuration Manager krav för nätverk, konfigurationer som stöds och maskin varu krav gäller även för virtuella Azure-datorer.

Mer information finns i [Configuration Manager på Azure](../../understand/configuration-manager-on-azure.md).

> [!IMPORTANT]
> Configuration Manager-platser och-klienter som körs på virtuella Azure-datorer omfattas av samma licens krav som lokala installationer.

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

[Windows Virtual Desktop](/azure/virtual-desktop/) är en Desktop-och app Virtualization-tjänst som körs på Microsoft Azure. Från och med version 1906 använder Configuration Manager för att hantera dessa virtuella enheter som kör Windows i Azure. Mer information finns i [operativ system som stöds för klienter och enheter](supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="next-steps"></a>Nästa steg

[Hantera Configuration Manager klienter i en VDI-infrastruktur (Virtual Desktop Infrastructure)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)