---
title: Skapa en aktivitetssekvens för annat än distributioner av operativsystem
titleSuffix: Configuration Manager
description: Skapa aktivitetssekvenser som inte används för att distribuera ett operativ system, till exempel att distribuera program vara eller automatisera uppgifter
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1fcae4d520b1e81d0ef3470cd12ee68488b4f589
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125534"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>Skapa en aktivitetssekvens för annat än distributioner av operativsystem

*Gäller för: Configuration Manager (aktuell gren)*

Aktivitetssekvenser i Configuration Manager används för att automatisera olika typer av aktiviteter i din miljö. Dessa uppgifter designas och testas i första hand för distribution av operativsystem. Configuration Manager har många andra funktioner som ska vara den primära teknik som du använder i följande scenarier:

- [Programinstallation](../../apps/understand/introduction-to-application-management.md)

    > [!NOTE]
    > Från och med version 2002 installerar du komplexa program med hjälp av aktivitetssekvenser via program modellen. Lägg till en distributions typ till en app som är en aktivitetssekvens, antingen för att installera eller avinstallera appen. Mer information finns i [skapa Windows-program](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt).<!-- 3555953 -->

- [Installation av program uppdateringar](../../sum/understand/software-updates-introduction.md)

- [Ställer in konfiguration](../../compliance/understand/ensure-device-compliance.md)

Överväg också andra automatiserings tekniker för Microsoft System Center, till exempel [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) och [Service Management Automation](https://docs.microsoft.com/system-center/sma/).  

Kraften i aktivitetssekvenser är i sin flexibilitet och hur du använder dem. De kan konfigurera klient inställningar, distribuera program vara, uppdatera driv rutiner, redigera användar tillstånd och utföra andra uppgifter som är oberoende av operativ Systems distributionen. Du kan skapa en anpassad aktivitetssekvens för att lägga till ett antal olika uppgifter. Användning av anpassade aktivitetssekvenser för distribution utan operativ system stöds i Configuration Manager. Men om en aktivitetssekvens resulterar i oönskade eller inkonsekventa resultat, kan du se hur du fören klar åtgärden:

- Använd enklare steg
- Dela upp åtgärder över flera aktivitetssekvenser
- Ta en stegvis metod för att skapa och testa aktivitetssekvensen

## <a name="supported-steps"></a>Steg som stöds

Följande steg kan användas i en anpassad aktivitetssekvens för distribution utan operativ system:  

- [Kontrollera beredskap](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [Anslut till nätverksmappen](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [Hämta paketinnehåll](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [Installera program](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [Installera paket](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [Installera programuppdateringar](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [Starta om dator](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [Kör kommando rad](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [Kör PowerShell-skript](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [Kör aktivitetssekvens](../understand/task-sequence-steps.md#child-task-sequence)  

- [Ställ in dynamiska variabler](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [Ange aktivitetssekvensvariabel](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Nästa steg

[Skapa en anpassad aktivitetssekvens](create-a-custom-task-sequence.md)