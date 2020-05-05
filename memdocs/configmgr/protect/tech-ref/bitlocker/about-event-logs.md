---
title: BitLocker-händelseloggar
titleSuffix: Configuration Manager
description: Lär dig mer om hur du arbetar med BitLocker-information i Windows-händelseloggen för att felsöka problem
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4875e7875321294d815bfcd8a25a805d3e085aab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722104"
---
# <a name="bitlocker-event-logs"></a>BitLocker-händelseloggar

*Gäller för: Configuration Manager (aktuell gren)*

Hanterings agenten och webb tjänsterna i BitLocker använder Windows-händelseloggen för att registrera meddelanden. I Loggboken går du till **program-och tjänst loggar**, **Microsoft**, **Windows**. Logg kanalen (noden) varierar beroende på datorn och komponenten:

- **MBAM**: BitLocker-hanteringsserver på en klient dator
- **MBAM – webb**:
  - Återställnings tjänst på hanterings platsen
  - Självbetjäningsportalen
  - Webbplats för administration och övervakning

Mer information om vissa meddelanden i dessa loggar finns i följande artiklar:

- [Klienthändelseloggar](client-event-logs.md)
- [Serverhändelseloggar](server-event-logs.md)

I varje nod ser du som standard två logg kanaler: **admin** och **drift**. För mer detaljerad felsöknings information, kan du även visa [analys-och fel söknings loggar](#bkmk_debug).

## <a name="log-properties"></a>Logg egenskaper

I Windows Loggboken väljer du en speciell logg. Till exempel **admin**. Gå till **åtgärd** -menyn och välj **Egenskaper**. Konfigurera följande inställningar:

- **Maximal logg storlek (KB)**: den här inställningen är `1028` som standard (1 MB) för alla loggar.
- **När den maximala logg storleken nås**: som standard är **Administratörs** -och **drift** loggarna inställda på att **skriva över händelser vid behov (äldsta händelserna först)**.

## <a name="analytic-and-debug-logs"></a><a name="bkmk_debug"></a>Analytiska loggar och fel söknings loggar

Du kan aktivera mer detaljerade loggar för fel söknings syfte. I Loggboken går du till menyn **Visa** och väljer **Visa analytiska loggar och fel söknings loggar**. Nu när du bläddrar till logg kanalen visas två ytterligare loggar: **analys** och **fel sökning**.

> [!TIP]
> Som standard har dessa loggar följande egenskaper:
>
> - **Maximal logg storlek (KB)**: `1028` (1 MB)
> - **Skriv inte över händelser (rensa loggar manuellt)**

## <a name="export-logs-to-text"></a>Exportera loggar till text

I synnerhet med [analytiska loggar och fel söknings loggar](#bkmk_debug)kan det vara lättare att granska loggar poster i en enda textfil. Använd följande PowerShell-kommandon för att exportera händelse logg posterna till textfiler:

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
