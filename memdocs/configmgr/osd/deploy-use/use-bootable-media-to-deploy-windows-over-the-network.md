---
title: Använda startbara media för att distribuera Windows via nätverket
titleSuffix: Configuration Manager
description: Använd startbara medie distributioner i Configuration Manager för att distribuera operativ systemet när mål datorn startar.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: db28c89e88ba08f92618c6d5fde1d1516b74afe4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124764"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Använda startbara medier för att distribuera Windows via nätverket med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Startbara medier innehåller bara start avbildningen och en pekare till aktivitetssekvensen. Den hämtar OS-avbildningen och annat innehåll som refereras från nätverket. Eftersom det startbara mediet inte innehåller mycket innehåll kan du uppdatera aktivitetssekvensen och det mesta innehållet utan att behöva ersätta mediet.

Distribuera operativ system över nätverket med start medier i följande scenarier:

- [Uppdatera en befintlig dator med en ny version av Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Installera en ny version av Windows på en ny dator (utan operativsystem)](install-new-windows-version-new-computer-bare-metal.md)

- [Ersätta en befintlig dator och överföra inställningar](replace-an-existing-computer-and-transfer-settings.md)

Slutför stegen i ett av scenarierna för operativ Systems distribution och Använd sedan följande avsnitt för att använda startbara medier för att distribuera operativ systemet.

## <a name="configure-deployment-settings"></a>Konfigurera distributionsinställningar

När du använder startbara medier för att starta operativ Systems distributions processen konfigurerar du aktivitetssekvensdistribution för att göra operativ systemet tillgängligt för mediet. Ange det här alternativet på sidan **distributions inställningar** i distributionen. Välj något av följande alternativ för inställningen **gör tillgängligt för följande** :

- Configuration Manager klienter, media och PXE

- Endast media och PXE

- Endast media och PXE (dolt)

Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md).

## <a name="create-the-bootable-media"></a>Skapa startbara media

När du skapar startbara medier anger du om det är en USB-flashenhet eller en CD-/DVD-uppsättning. Datorn som startar mediet måste ha stöd för det alternativ som du väljer som startbar enhet. Mer information finns i [Skapa startbara media](create-bootable-media.md).

## <a name="install-the-os-from-bootable-media"></a><a name="BKMK_Deploy"></a>Installera operativ systemet från startbara media

Om du vill installera operativ systemet sätter du in det startbara mediet och sätter sedan på datorn.

## <a name="support-for-cloud-based-content"></a>Stöd för molnbaserad innehåll

<!--6209223-->

Från och med version 2006 kan startbara media Ladda ned molnbaserad innehåll. Du kan till exempel skicka en USB-nyckel till en användare på ett fjärran slutet kontor för att återställa en avbildning av enheten. Eller ett kontor som har en lokal PXE-server, men du vill att enheter ska prioritera moln tjänster så mycket som möjligt. I stället för att ytterligare beskattnings WAN för att ladda ned innehåll för stor operativ Systems distribution kan du nu hämta innehåll från molnbaserade källor med start medier och PXE-distributioner. Till exempel en CMG (Cloud Management Gateway) som du aktiverar för att dela innehåll.

> [!NOTE]
> Enheten behöver fortfarande en intranät anslutning till hanterings platsen.

När aktivitetssekvensen körs laddar den ned innehåll från de molnbaserade källorna. Granska **Smsts. log** på klienten.

### <a name="prerequisites"></a>Förutsättningar

- Aktivera följande klient inställning i gruppen **Cloud Services** : **Tillåt åtkomst till moln distributions platsen**. Kontrol lera att klient inställningen har distribuerats till mål klienterna. Mer information finns i [om klient inställningar – Cloud Services](../../core/clients/deploy/about-client-settings.md#cloud-services).

- För den gränser grupp som klienten finns i:

  - Associera de innehålls aktiverade CMG eller moln distributions platsens plats system. Mer information finns i [Konfigurera en avgränsnings grupp](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_config).

  - Aktivera följande alternativ: **föredra molnbaserade källor över lokala källor**. Mer information finns i [gränser grupp alternativ för peer-nedladdningar](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

- Distribuera det innehåll som aktivitetssekvensen hänvisar till som den innehålls aktiverade CMG eller moln distributions platsen.

## <a name="next-steps"></a>Nästa steg

[Användarupplevelser för distribution av operativsystem](../understand/user-experience.md#task-sequence-wizard)
