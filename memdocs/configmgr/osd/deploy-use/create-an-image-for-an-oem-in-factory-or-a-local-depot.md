---
title: Skapa en avbildning för en OEM-tillverkare i fabriken eller lokal anläggning
titleSuffix: Configuration Manager
description: Använd förinstallerade medie distributioner för att minska nätverks trafiken när du distribuerar ett operativ system till en dator som inte är helt etablerad.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c4d445d18b9e239ace673199f6a7d0f26d10a42
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723000"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Skapa en avbildning för en OEM-tillverkare i fabriken eller ett lokalt lager med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Med förinstallerade medie distributioner i Configuration Manager kan du distribuera ett operativ system till en dator som inte är helt etablerad. Det förinstallerade mediet är en WIM-fil (Windows Imaging format) som kan installeras på en dator utan operativ system av tillverkaren (OEM) eller till ett företag som inte är anslutet till Configuration Managers miljön. Senare i Configuration Managers miljön startar datorn med hjälp av den Start avbildning som tillhandahålls av mediet, en hash-kontroll körs på det förinstallerade mediet för att kontrol lera att den är giltig och sedan ansluter datorn till plats hanterings platsen för tillgängliga aktivitetssekvenser som slutför nedladdnings processen.


Den här distributionsmetoden kan minska nätverkstrafiken, eftersom startavbildningen och operativsystemsavbildningen redan finns på måldatorn. Du kan ange vilka program, paket och drivrutinspaket som du vill ha med på förinstallerade media. När operativsystemet har installerats på datorn kontrolleras den lokala aktivitetssekvenscachen först för program, paket och drivrutinspaket och om innehållet inte kan hittas eller har ändrats, hämtas innehållet från en distributionsplats som har konfigurerats i det förinstallerade mediet och installeras därefter.  

 Du kan använda förinstallerade medier i följande scenarier för operativ Systems distribution:  

- [Installera en ny version av Windows på en ny dator (utan operativsystem)](install-new-windows-version-new-computer-bare-metal.md)  

- [Ersätta en befintlig dator och överföra inställningar](replace-an-existing-computer-and-transfer-settings.md)  

  Utför stegen i ett av scenarierna för distribution av operativsystem och använd sedan följande avsnitt för att förbereda för och skapa förinstallerade medier.  

## <a name="configure-deployment-settings"></a>Konfigurera distributionsinställningar  
 När du använder förinstallerade medier för att starta operativsystemsdistributionen måste du konfigurera distributionen för att göra operativsystemet tillgängligt för media. Du kan konfigurera detta på sidan **Distributionsinställningar** i guiden Distribuera programvara eller på fliken **Distributionsinställningar** i egenskaperna för distributionen.  Konfigurera något av följande för inställningen **Gör tillgängligt för följande** :  

-   **Configuration Manager-klienter, media och PXE**  

-   **Endast media och PXE**  

-   **Endast media och PXE (dolt)**  

## <a name="create-the-prestaged-media"></a>Skapa förinstallerade medier  
 Skapa den förinstallerade mediefilen som ska skickas till OEM eller den lokala anläggningen. Mer information finns i [Skapa förinstallerade media med Configuration Manager](create-prestaged-media.md).  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>Skicka den förinstallerade mediefilen till OEM eller den lokala anläggningen  
 Skicka mediet till OEM eller den lokala anläggningen som ska förinstalleras på datorerna. Den förinstallerade mediefilen används på en formaterad hårddisk på datorn.  

## <a name="start-the-computer-to-install-the-operating-system"></a>Starta datorn för att installera operativsystemet  
 Den förinstallerade mediefilen används på datorer. Processen för installation av operativsystem startar när datorn startas för första gången.  
