---
title: Ta bort en macOS-enhet
titleSuffix: Microsoft Intune
description: Läs hur du raderar alla data, inklusive operativsystemet, från en macOS-enhet.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ab396092-907a-44b7-a157-aabee62176a9
ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3812dc710c28105436327c4049bfcd61611eeeaf
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80322579"
---
# <a name="erase-all-data-from-a-macos-device"></a>Radera alla data från en macOS-enhet

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Du kan ta bort alla data från en macOS-enhet, inklusive operativsystemet. Enheten tas även bort från Intune-hantering. Ingen varning ges till slutanvändaren.

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **Alla enheter** > välj den enhet som du vill radera.
2. Klicka på **Mer** > **Radera** > och ange 6 siffror för **PIN-kod för återställning**. Det här är PIN-koden som du måste ge användarna så att de kan installera om operativsystemet på enheten. Se till att anteckna den här PIN-koden eftersom den inte är synlig igen när raderingsåtgärden har slutförts.
![Skärmbild](./media/device-erase/providepin.png)
3. Klicka på **OK** för att radera enheten.
