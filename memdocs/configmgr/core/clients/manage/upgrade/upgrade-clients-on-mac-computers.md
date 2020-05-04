---
title: Uppgradera macOS-klienter
titleSuffix: Configuration Manager
description: Uppgradera Configuration Manager-klienten på Mac-datorer.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34d0c9233b4f7384dfc2280dc92334450a785ed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715006"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>Uppgradera klienter på Mac-datorer i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Följ de övergripande stegen i den här artikeln för att uppgradera-klienten för Mac-datorer med hjälp av ett Configuration Manager-program. Du kan också hämta installations filen för Mac-klienten, kopiera den till en delad nätverks plats eller en lokal mapp på Mac-datorn och sedan instruera användarna att köra installationen manuellt.  

> [!NOTE]  
> Innan du utför de här stegen måste du kontrol lera att Mac-datorn uppfyller kraven. Se [operativ system som stöds för Mac-datorer](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="download-the-latest-mac-client"></a>Ladda ned den senaste Mac-klienten

Mac-klienten för Configuration Manager anges inte på Configuration Manager-installations mediet. Ladda ned den från Microsoft Download Center, [Microsoft Endpoint Configuration Manager-MacOS-klienten (64-bitars)](https://www.microsoft.com/download/details.aspx?id=100850). Installationsfilerna för Mac-klienten finns i en Windows Installer-fil med namnet **ConfigmgrMacClient. msi**.  

## <a name="create-the-mac-client-installation-file"></a>Skapa installations filen för Mac-klienten

Kör **ConfigmgrMacClient. msi**på en dator som kör Windows. Detta installations program packar upp installations filen för Mac-klienten, med namnet **Macclient. dmg**. Som standard kan du hitta den här filen i följande mapp: **C:\Program Files\Microsoft\System Center Configuration Manager för Mac-klienten**.  

## <a name="extract-the-client-installation-files"></a>Extrahera installationsfilerna för klienten

Kopiera **Macclient. dmg** till en Mac-dator. Montera filen Macclient. dmg i macOS och kopiera sedan innehållet till en mapp på Mac-datorn.  

## <a name="create-a-cmmac-file"></a>Skapa en. cmmac-fil

1. Öppna mappen **verktyg** i installations filen för Mac-klienten. Använd **CMAppUtil** -verktyget för att skapa en. cmmac-fil från klient installations paketet. Du kommer att använda den här filen för att skapa ett Configuration Manager-program.  

2. Kopiera den nya filen **CMClient. pkg. cmmac** till en nätverks plats som är tillgänglig för datorn som kör Configuration Manager-konsolen.  

    Mer information finns i [kompletterande procedurer för att skapa och distribuera program för Mac-datorer](../../../../apps/get-started/creating-mac-computer-applications.md#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="create-and-deploy-the-app"></a>Skapa och distribuera appen

1. I Configuration Manager-konsolen [skapar du ett program](../../../../apps/get-started/creating-mac-computer-applications.md) från filen **CMClient. pkg. cmmac** .  

2. [Distribuera det här programmet](../../../../apps/deploy-use/deploy-applications.md) till Mac-datorer i hierarkin.  

## <a name="install-the-updated-client"></a>Installera den uppdaterade klienten

Den befintliga Configuration Manager-klienten på Mac-datorer kommer att uppmana användaren att en uppdatering är tillgänglig för installation. När användarna installerar klienten måste de starta om Mac-datorn.  

När datorn har startats om körs guiden **dator registrering** automatiskt för att begära ett nytt användar certifikat.

Om du inte använder Configuration Manager registrering, men installerar klient certifikatet oberoende av Configuration Manager, se [Konfigurera klienter att använda ett befintligt certifikat](#BKMK_UpgradingClient_MachineEnrollment).  

## <a name="configure-clients-to-use-an-existing-certificate"></a><a name="BKMK_UpgradingClient_MachineEnrollment"></a>Konfigurera klienter för att använda ett befintligt certifikat

Använd den här proceduren för att förhindra att guiden dator registrering körs, och för att konfigurera den uppgraderade klienten så att den använder ett befintligt klient certifikat.  

1. [Skapa ett konfigurations objekt](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) av typen **Mac OS X**i Configuration Manager-konsolen.  

1. Lägg till en inställning i konfigurationsobjektet med inställningstypen **Skript**.  

1. Lägg till följande skript i inställningen:  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. Lägg till konfigurationsobjektet i en [konfigurations bas linje](../../../../compliance/deploy-use/create-configuration-baselines.md). [Distribuera sedan konfigurations bas linjen](../../../../compliance/deploy-use/deploy-configuration-baselines.md) till alla Mac-datorer som installerar ett certifikat oberoende av Configuration Manager.  
