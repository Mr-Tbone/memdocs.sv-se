---
title: Hantera VDI-klienter
titleSuffix: Configuration Manager
description: Hantera Configuration Manager klienter i en VDI-infrastruktur (Virtual Desktop Infrastructure).
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6df9238cd81f14a64a42c45136c778357acb89c4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126958"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Hantera Configuration Manager klienter i en VDI-infrastruktur (Virtual Desktop Infrastructure)

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager stöder installation av Configuration Manager-klienten i följande VDI-scenarier (Virtual Desktop Infrastructure):

- **Personliga virtuella datorer**: den virtuella datorn (VM) underhåller användar data och inställningar mellan sessioner.

- **Fjärrskrivbordstjänster sessioner**: värd för flera samtidiga klientsessioner på en central server. Användare ansluter till en session och kör program på den servern.

- **Virtuella datorer i pooler**: den virtuella datorn behålls inte mellan sessioner. När en användare stänger en session, ignorerar den virtuella miljön alla data och inställningar. Virtuella datorer i pooler är användbara när du inte kan använda Fjärrskrivbordstjänster. Till exempel, om ett program som krävs inte kan köras på den Windows-Server som är värd för-klientsessioner.

- **Windows Virtual Desktop**: en Desktop-och app Virtualization-tjänst som körs på Microsoft Azure. Från och med version 1906 använder Configuration Manager för att hantera dessa virtuella enheter som kör Windows i Azure.

## <a name="personal-vms"></a>Personliga VM

Configuration Manager behandlar personliga virtuella datorer på samma sätt som en fysisk dator. Du kan förinstallera Configuration Manager-klienten på den virtuella dator avbildningen eller efter att du har etablerat den.

Mer information finns i [stöd för virtualiseringslösningar](../../../plan-design/configs/support-for-virtualization-environments.md).

## <a name="remote-desktop-services"></a>Fjärrskrivbordstjänster

Du installerar inte Configuration Manager-klienten för enskilda fjärr skrivbords-sessioner. Installera den en gång på den server som är värd för Fjärrskrivbordstjänster. Du kan använda alla Configuration Manager klient funktioner på Fjärrskrivbordstjänster-servern.

Mer information finns i [Välkommen till Fjärrskrivbordstjänster](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/welcome-to-rds).

## <a name="pooled-vms"></a>Virtuella datorer i pooler

När du inaktiverar en virtuell dator i poolen försvinner eventuella ändringar som gjorts av Configuration Manager.

Eftersom den virtuella datorn kanske bara kan användas under en kort tids period kan vissa Configuration Manager funktioner inte returnera relevanta data. Till exempel maskin varu inventering, program varu inventering och avläsning av program vara. Överväg att utesluta poolen virtuell dator från inventerings aktiviteter.

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

Mer information finns i [operativ system som stöds för klienter och enheter](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

## <a name="other-considerations"></a>Ytterligare överväganden

Eftersom virtualisering har stöd för att köra flera Configuration Manager-klienter på samma fysiska dator har många klient åtgärder en inbyggd slumpmässig fördröjning för schemalagda åtgärder. Till exempel maskin-och program varu inventering, genomsökning mot skadlig kod, program varu installationer och genomsökning av program uppdateringar. Den här fördröjningen hjälper till att distribuera CPU-bearbetning och data överföring för en server som har flera virtuella datorer som kör Configuration Manager-klienten.

Förutom för Windows Embedded-klienter i behandlings läge använder Configuration Manager klienter som inte finns i virtualiserade miljöer även denna slumpmässiga fördröjning. Den här funktionen bidrar till att undvika toppar i nätverks bandbredden. Det minskar också CPU-bearbetningen på plats system, till exempel hanterings platsen och plats servern. Fördröjnings intervallet varierar beroende på Configuration Manager funktion. Se till exempel [om klient inställningar – inaktivera slumpmässig tids gräns](../about-client-settings.md#disable-deadline-randomization).

För att hjälpa till med Configuration Manager klient prestanda i virtuella miljöer som stöder flera användarsessioner inaktive ras användar principer som standard. Från och med version 1910 kan du aktivera användar principer i det här scenariot. Mer information finns i [om klient inställningar – aktivera användar princip för flera](../about-client-settings.md#enable-user-policy-for-multiple-user-sessions)användarsessioner.
