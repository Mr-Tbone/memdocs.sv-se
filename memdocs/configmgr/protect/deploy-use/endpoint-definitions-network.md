---
title: Hämta definitioner från en nätverks resurs
titleSuffix: Configuration Manager
description: Lär dig hur du hämtar de senaste definitions uppdateringarna manuellt från Microsoft och sedan konfigurera klienter för att hämta dessa definitioner.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9afeee7f7111994f0ae3891c7ecd99a11d7edd7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715685"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share"></a>Aktivera Endpoint Protection definitioner av skadlig kod för nedladdning från en nätverks resurs

*Gäller för: Configuration Manager (aktuell gren)*

 Du kan hämta de senaste definitionsuppdateringarna manuellt från Microsoft och sedan konfigurera klienter för att hämta dessa definitioner från en delad mapp i nätverket. Användarna kan också initiera definitionsuppdateringar när du använder den här uppdateringskällan.

> [!NOTE]
>  Klienterna måste ha läsbehörighet till den delade mappen för att kunna hämta definitionsuppdateringar.

 Mer information om hur du hämtar definitions-och motor uppdateringar för lagring på fil resursen finns i [installera den senaste program varan från Microsoft Antimalware och antispionprogram](https://www.microsoft.com/wdsi/definitions).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Konfigurera definitionshämtningar från en filresurs

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.

2.  I arbetsytan **Tillgångar och efterlevnad** expanderar du **Endpoint Protection**och klickar på **Antiskadlig kod-principer**.

3.  Öppna sidan med egenskaper för **Standard-Antiskadlig kod-princip** eller skapa en ny princip för program mot skadlig kod. Mer information om hur du skapar principer för program mot skadlig kod finns i [skapa och distribuera principer för program mot skadlig kod för Endpoint Protection](endpoint-antimalware-policies.md).

4.  I avsnittet **Security Intelligence-uppdateringar** i dialog rutan Egenskaper för program mot skadlig kod klickar du på **Ange källa**.
    - Avsnittet **definitions uppdateringar** har bytt namn till **Security Intelligence-uppdateringar** från Configuration Manager version 1902.

5.  I dialogrutan **Konfigurera definitionsuppdateringskällor** markerar du **Uppdateringar från UNC-filresurser**.

6.  Klicka på **OK** för att stänga dialogrutan **Konfigurera definitionsuppdateringskällor** .

7.  Klicka på **Ange sökvägar**. I dialogrutan **Konfigurera UNC-sökvägar för definitionsuppdateringar** lägger du sedan till en eller flera UNC-sökvägar till platsen för definitionsuppdateringsfilerna på en nätverksresurs.

8.  Klicka på **OK** för att stänga dialogrutan **Konfigurera UNC-sökvägar för definitionsuppdateringar** .


> [!div class="button"]
> [Nästa steg >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Tillbaka >](endpoint-configure-alerts.md)
