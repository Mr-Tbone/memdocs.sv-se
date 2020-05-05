---
title: Använda startbara media för att distribuera Windows via nätverket
titleSuffix: Configuration Manager
description: Använd startbara medie distributioner i Configuration Manager för att distribuera operativ systemet när mål datorn startar.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 22a3219cdf0bb09061e57f34e52ca7a061f55a2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724365"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Använda startbara medier för att distribuera Windows via nätverket med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan distribuera operativ systemet när mål datorn startar med en startbar medie distribution. Mediet innehåller en pekare till aktivitetssekvensen, operativ system avbildningen och annat nödvändigt innehåll från nätverket. När mål datorn startar hämtar datorn de objekt som refereras till i pekaren. Med det startbara mediet för innehåll kan du uppdatera målet utan att behöva ersätta det på mediet.

Du kan distribuera operativ system via nätverket genom att använda multicast i följande scenarier för operativ Systems distribution:

-   [Uppdatera en befintlig dator med en ny version av Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Installera en ny version av Windows på en ny dator (utan operativsystem)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Ersätta en befintlig dator och överföra inställningar](replace-an-existing-computer-and-transfer-settings.md)  

Utför stegen i ett av scenarierna för operativsystemsdistribution och använd sedan följande avsnitt för att använda startbara media för att distribuera operativsystemet.  

## <a name="configure-deployment-settings"></a>Konfigurera distributionsinställningar  
När du använder startbara medier för att starta operativ systemets distributions process konfigurerar du distributionen så att operativ systemet blir tillgängligt för mediet. Du kan ange det här alternativet på sidan **distributions inställningar** i guiden distribuera program vara eller på fliken **distributions inställningar** i egenskaperna för distributionen. Konfigurera något av följande för inställningen **Gör tillgängligt för följande** :

-   Configuration Manager klienter, media och PXE

-   Endast media och PXE

-   Endast media och PXE (dolt)

## <a name="create-the-bootable-media"></a>Skapa startbara media
Du kan ange om det startbara mediet är ett USB-minne eller en CD-/DVD-uppsättning. Datorn som startar mediet måste ha stöd för det alternativ som du väljer som startbar enhet. Mer information finns i [Skapa startbara media](create-bootable-media.md).  

##  <a name="install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> Installera operativsystemet från startbara media  
Infoga det startbara mediet i en startbar enhet på datorn och starta den sedan för att installera operativsystemet.
