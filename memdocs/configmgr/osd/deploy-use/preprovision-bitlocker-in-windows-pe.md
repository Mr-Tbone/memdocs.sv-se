---
title: Företablera BitLocker i Windows PE
titleSuffix: Configuration Manager
description: Åtgärden för att företablera BitLocker i Configuration Manager aktiverar BitLocker från Windows Preinstallation Environment innan operativ Systems distributionen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9e9acb35354e9962fe838964d3afad0bacceace
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124951"
---
# <a name="preprovision-bitlocker-in-windows-pe-with-configuration-manager"></a>Företablera BitLocker i Windows PE med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med steget för att **Företablera BitLocker** i Configuration Manager kan du aktivera bitlocker från Windows Preinstallation Environment (Windows PE) innan du distribuerar operativ system. Endast det utrymme som används på enheten krypteras, och därför går krypteringen snabbare. Detta görs genom att ett slumpmässigt genererat rensningsskydd tillämpas på den formaterade volymen, som sedan krypteras innan Windows-installationen körs. Möjligheten att företablera BitLocker infördes med Windows 8 och Windows Server 2012. Du kan dock företablera BitLocker på en hårddisk och installera Windows 7 om du följer vissa anvisningar. När installationen av Windows 7 är klar måste du ange ett BitLocker-nyckelskydd, eftersom kontrollpanelen för BitLocker i Windows 7 inte har stöd för BitLocker med klartextskydd. Du måste lägga till ett nyckelskydd genom att använda steget **Aktivera BitLocker** eller med kommandoradsverktyget manage-bde.exe.  

 I allmänhet måste du göra följande för att företablera BitLocker på en dator där du ska installera Windows 7:  

- Starta om datorn i Windows PE  

  > [!IMPORTANT]  
  >  Du måste använda en startavbildning med Windows PE 4 eller senare för att företablera BitLocker. Mer information om Windows PE-versioner som stöds i Configuration Manager finns i [externa beroenden till Configuration Manager](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies).  

- Partitionera och formatera hårddisken  

- Företablera BitLocker  

- Installera Windows 7 med specifika inställningar för operativsystem och nätverk  

- Lägga till nyckelskydd till BitLocker  

  I Configuration Manager är det rekommenderade sättet att företablera BitLocker på en hård disk och installera Windows 7 att skapa en ny aktivitetssekvens och välja **Installera ett befintligt avbildnings paket** på sidan **Skapa ny aktivitetssekvens** i **guiden skapa aktivitetssekvens**. Guiden skapar de aktivitetssekvenssteg som visas i följande tabell.  

> [!NOTE]  
>  Aktivitetssekvensen kan ha ytterligare steg, beroende på hur du konfigurerade inställningarna i guiden. Du kan t.ex. ha steget **Avbilda Windows-inställningar** om du valde **Avbilda Microsoft Windows-inställningar** på sidan **Tillståndsmigrering** i guiden.  

|Aktivitetssekvenssteg|Information|  
|------------------------|-------------|  
|Inaktivera BitLocker|Det här steget inaktiverar BitLocker-kryptering, om det är aktiverat. Mer information finns i avsnittet [Disable BitLocker](../understand/task-sequence-steps.md#BKMK_DisableBitLocker).|  
|Starta om datorn i Windows PE|Det här steget startar om datorn i Windows PE genom att köra den startavbildning som tilldelats aktivitetssekvensen. Du måste använda en startavbildning med Windows PE 4 eller senare för att företablera BitLocker. Mer information finns i avsnittet [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer).|  
|Partitionsdisk 0 - BIOS<br /><br /> Partitionsdisk 0 - UEFI|De här stegen formaterar och partitionerar den angivna enheten på måldatorn med BIOS eller UEFI. Aktivitetssekvensen använder UEFI när den känner av att måldatorn är i UEFI-läge. Mer information finns i avsnittet [Format and Partition Disk](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk).|  
|Företablera BitLocker|Det här steget aktiverar BitLocker på en enhet i Windows PE. Endast det diskutrymme som används krypteras. Eftersom du partitionerade och formaterade hårddisken i föregående steg finns det inga data, och krypteringen går mycket fort. Mer information finns i avsnittet [Pre-provision BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker).|  
|Använd operativsystem|Det här steget förbereder den svarsfil som används för att installera operativsystemet på måldatorn och anger uppgiftssekvensvariabeln OSDTargetSystemDrive till enhetsbokstaven för den partition som innehåller operativsystemfilerna. Svarsfilen och variabeln används av steget Installera Windows och ConfigMgr för att installera operativsystemet. Mer information finns i [Använd operativsystemavbildningar](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|Använd Windows-inställningar|Det här steget lägger till Windows-inställningar i svarsfilen. Svarsfilen används av steget Installera Windows och ConfigMgr för att installera operativsystemet. Mer information finns i avsnittet [Apply Windows Settings](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).|  
|Använd nätverksinställningar|Det här steget lägger till nätverksinställningar i svarsfilen. Svarsfilen används av steget Installera Windows och ConfigMgr för att installera operativsystemet. Mer information finns i [Apply Network Settings Step](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings).|  
|Använda enhetsdrivrutiner|Det här steget matchar och installerar drivrutiner som en del av operativsystemdistributionen. Mer information finns i avsnittet [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).|  
|Installera Windows och ConfigMgr|Det här steget utför övergången från Windows PE till det nya operativsystemet. Det här aktivitetssekvenssteget är en obligatorisk del av alla operativsystemdistributioner. Den installerar Configuration Manager-klienten i det nya operativ systemet och förbereder att aktivitetssekvensen ska fortsätta köras i det nya operativ systemet. Mer information finns i avsnittet [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).|  
|Aktivera BitLocker|Det här steget aktiverar BitLocker-kryptering på hårddisken och anger nyckelskydd. Eftersom hårddisken företablerades med BitLocker går det här steget mycket fort. Windows 7 kräver att du lägger till ett nyckelskydd. Om du inte använder det här steget kan du ange ett nyckelskydd med kommandoradsverktyget manage-bde.exe. Mer information finns i [Enable BitLocker](../understand/task-sequence-steps.md#BKMK_EnableBitLocker).|  
