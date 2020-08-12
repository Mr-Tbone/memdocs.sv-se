---
title: Använda fristående media för att distribuera Windows
titleSuffix: Configuration Manager
description: Använd fristående media i Configuration Manager för att distribuera Windows där bandbredden är begränsad som ett alternativ för att uppdatera, installera eller uppgradera datorer.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51b39e450fb5f8ffd7d83b4122d7514489383dfb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124660"
---
# <a name="use-standalone-media-to-deploy-windows-without-using-the-network"></a>Använda fristående media för att distribuera Windows utan att använda nätverket

*Gäller för: Configuration Manager (aktuell gren)*

Fristående media i Configuration Manager innehåller allt som krävs för att distribuera ett operativ system på en dator. Mediet innehåller start avbildningen, OS-avbildningen, aktivitetssekvensen, program, driv rutiner och mycket annat. Med fristående medie distributioner kan du distribuera operativ system under följande omständigheter:

- I miljöer där det inte är praktiskt att kopiera en operativ system avbildning eller andra stora paket över nätverket.

- I miljöer utan nätverks anslutning eller nätverks anslutning med låg bandbredd.

Använd fristående media i följande distributions scenarier för operativ system:

- [Uppdatera en befintlig dator med en ny version av Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Installera en ny version av Windows på en ny dator (utan operativsystem)](install-new-windows-version-new-computer-bare-metal.md)

- [Uppgradera Windows till den senaste versionen](upgrade-windows-to-the-latest-version.md)

Slutför stegen i något av de här distributions scenarierna för operativ systemet. Använd sedan följande avsnitt för att förbereda för och skapa det fristående mediet.

## <a name="unsupported-task-sequence-actions"></a>Åtgärder som inte stöds av aktivitetssekvensen

När du använder fristående medier stöder Configuration Manager inte följande åtgärder i aktivitetssekvensen:

- Steget [Använd driv rutiner automatiskt](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) . Automatisk tillämpning av enhets driv rutiner från driv rutins katalogen stöds inte. Använd steget [Använd driv rutins paket](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) för att göra en speciell uppsättning driv rutiner tillgängliga för installationsprogrammet för Windows.

- Installera programuppdateringar.

- Installera program vara innan du distribuerar operativ systemet.

- Associera användare med mål datorn för mappning mellan användare och enhet.

- Dynamiskt paket installeras med steget [installera paket](../understand/task-sequence-steps.md#BKMK_InstallPackage) .

- Dynamiska program installeras med steget [installera program](../understand/task-sequence-steps.md#BKMK_InstallApplication) .

> [!NOTE]
> Om aktivitetssekvensen för att distribuera ett operativ system omfattar steget **installera paket** och du skapar det fristående mediet på en central administrations plats (ca) kan ett fel uppstå. Certifikat utfärdaren har inte de nödvändiga klient konfigurations principerna för att aktivera program distributions agenten när aktivitetssekvensen körs. Följande fel kan visas i filen **CreateTSMedia. log** :
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>
> För fristående media som innefattar steget **installera paket** skapar du det fristående mediet på en primär plats som har program distributions agenten aktive rad
>
> Du kan också redigera aktivitetssekvensen för att lägga till steget [Kör kommando rad](../understand/task-sequence-steps.md#BKMK_RunCommandLine) efter steget [Installera Windows och ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) . Detta **Kör kommando rads** steg kör följande WMI-kommando för att aktivera program distributions agenten innan steget första **installations paketet** körs:
>
> ```command
> WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
> ```

## <a name="configure-deployment-settings"></a>Konfigurera distributionsinställningar

När du använder fristående media för att starta operativ Systems distributions processen konfigurerar du distributionen så att operativ systemet blir tillgängligt för mediet. På sidan **distributions inställningar** i distributionen väljer du något av följande alternativ för inställningen **gör tillgängligt för följande** :

- Configuration Manager klienter, media och PXE

- Endast media och PXE

- Endast media och PXE (dolt)

## <a name="create-the-standalone-media"></a>Skapa det fristående mediet

Du kan ange om det fristående mediet är ett USB-minne eller en CD-/DVD-uppsättning. Datorn som ska starta mediet måste ha stöd för det alternativ som du väljer som startbar enhet. Mer information finns i [skapa fristående media](create-stand-alone-media.md).

## <a name="install-the-os-from-standalone-media"></a>Installera operativ systemet från fristående media

Om du vill installera operativ systemet sätter du in det fristående mediet på datorn och sätter sedan på det.

## <a name="next-steps"></a>Nästa steg

[Användarupplevelser för distribution av operativsystem](../understand/user-experience.md#task-sequence-wizard)
