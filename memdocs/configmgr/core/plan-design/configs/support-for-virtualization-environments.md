---
title: Stöd för virtualisering
titleSuffix: Configuration Manager
description: Kraven för att installera Configuration Manager-klient-och plats system roller i en Virtualization-miljö.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e266373667efebccdb84fe743f66beeaa5a0e88
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709595"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Stöd för virtualiseringslösningar med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager stöder installation av klient-och plats system roller för operativ system som stöds och som körs som en virtuell dator i virtualiseringslösningar i den här artikeln. Detta stöd finns även när den virtuella datorns värd (virtualiseringsplattformen) inte stöds som en klient eller plats Server.  

Du kan till exempel använda Microsoft Hyper-V Server 2012 för att vara värd för en virtuell dator som kör Windows Server 2012. Du kan installera klient-eller plats system rollerna på den virtuella datorn som kör Windows Server 2012. Du kan inte installera klienten på värden som kör Microsoft Hyper-V Server 2012.  

## <a name="virtualization-environments"></a>Virtualiseringslösningar

- Windows Server 2019  
- Windows Server 2016 <sup> [Anmärkning 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup> [Anmärkning 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

### <a name="note-1-nested-virtualization"></a><a name="bkmk_note1"></a>Anmärkning 1: kapslad virtualisering

Configuration Manager stöder inte [kapslad virtualisering](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), som är ny i Windows Server 2016.

### <a name="virtualization-environment-support"></a>Stöd för Virtualization Environment

Varje virtuell dator måste ha samma eller större maskin-och program varu krav som du skulle använda för en fysisk Configuration Manager dator.  

Om du vill kontrol lera att virtualiseringsplattformen stöds för Configuration Manager använder du verifierings programmet för Server virtualisering. Den innehåller en guide för support princip för virtualisering online. Mer information finns i [Windows Server Virtualization Validation program](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
> Configuration Manager stöder inte virtuella datorer eller virtuella server gäst operativ system som körs på Mac-datorer.  

Configuration Manager kan inte hantera virtuella datorer om de är offline. Det går inte att uppdatera en virtuell dator avbildning offline eller så kan lagret samlas in med hjälp av Configuration Manager-klienten på värddatorn.  

Ingen speciell hänsyn tas till virtuella datorer. Configuration Manager kanske till exempel inte kan avgöra om en uppdatering måste återanvändas på en avbildning av en virtuell dator om den virtuella datorn har stoppats och startats om utan att statusen för den virtuella datorn som uppdateringen tillämpades på har sparats.  

##  <a name="microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a>Microsoft Azure virtuella datorer  

Configuration Manager kan köras på virtuella datorer i Azure precis som den körs lokalt i ditt data Center. Använd Configuration Manager med Azure Virtual Machines i följande scenarier:  

- **Scenario 1**: kör Configuration Manager på en virtuell Azure-dator. Använd den för att hantera klienter på andra virtuella Azure-datorer.  

- **Scenario 2**: kör Configuration Manager på en virtuell Azure-dator. Använd den för att hantera klienter som inte körs på Azure.  

- **Scenario 3**: kör olika Configuration Manager plats system roller på virtuella Azure-datorer. Kör andra roller i ditt lokala data Center som är korrekt anslutna till Azure.  

Samma Configuration Manager krav för nätverk, konfigurationer som stöds och maskin varu krav som gäller för installation lokalt gäller även för installation på virtuella Azure-datorer.  

Mer information finns i [Configuration Manager på Azure](../../understand/configuration-manager-on-azure.md).

> [!IMPORTANT]  
> Configuration Manager-platser och-klienter som körs på virtuella Azure-datorer omfattas av samma licens krav som lokala installationer.  

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

[Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) är en förhands gransknings funktion i Microsoft Azure och Microsoft 365. Från och med version 1906 använder Configuration Manager för att hantera dessa virtuella enheter som kör Windows i Azure. Mer information finns i [operativ system som stöds för klienter och enheter](supported-operating-systems-for-clients-and-devices.md).
