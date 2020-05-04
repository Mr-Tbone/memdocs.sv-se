---
title: Hämta definitioner från Microsoft
titleSuffix: Configuration Manager
description: Lär dig hur du aktiverar nedladdning av Endpoint Protection definitioner av skadlig kod från Microsoft Updates för Configuration Manager.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1f0d8ac635d514e750584126458bfde6b5fc24ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715692"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates"></a>Aktivera Endpoint Protection definitioner av skadlig kod för nedladdning från Microsoft Updates

*Gäller för: Configuration Manager (aktuell gren)*

När du väljer att hämta definitions uppdateringar från Microsoft Update, kontrollerar klienterna den Microsoft Update webbplatsen enligt intervallet som definieras i avsnittet **Security Intelligence-uppdateringar** i dialog rutan princip för program mot skadlig kod.

 Den här metoden kan vara användbar när klienten inte har någon anslutning till Configuration Manager-platsen eller när du vill att användarna ska kunna initiera definitions uppdateringar.

> [!IMPORTANT]
> - Klienter måste ha åtkomst till Microsoft Update på Internet för att kunna använda den här metoden för att hämta uppdateringar.
> - Avsnittet **definitions uppdateringar** har bytt namn till **Security Intelligence-uppdateringar** från Configuration Manager version 1902.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Använda Microsoft Malware Protection Center för att hämta definitioner
 Du kan konfigurera klienterna så att de hämtar definitionsuppdateringar från Microsoft Malware Protection Center. Det här alternativet används av Endpoint Protection-klienter för att hämta definitions uppdateringar om de inte har kunnat hämta uppdateringar från en annan källa. Den här uppdaterings metoden kan vara användbar om det uppstår problem med Configuration Manager-infrastrukturen som förhindrar att uppdateringar levereras.

> [!IMPORTANT]
>  Klienter måste ha åtkomst till Microsoft Update på Internet för att kunna använda den här metoden för att hämta uppdateringar.
> 
> 
> [!div class="button"]
> [Nästa steg >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Tillbaka >](endpoint-configure-alerts.md)
