---
title: Konfigurera definitions uppdateringar
titleSuffix: Configuration Manager
description: Lär dig hur du väljer och konfigurerar metoder med Endpoint Protection i Configuration Manager för att hålla definitionerna av skadlig kod uppdaterade på klient datorer.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce11ba0cbe4298d32a11de409910ebc3e14c097b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715769"
---
# <a name="configure-definition-updates-for-endpoint-protection"></a>Konfigurera definitionsuppdateringar för Endpoint Protection  

*Gäller för: Configuration Manager (aktuell gren)*

 Med Endpoint Protection i Configuration Manager kan du använda någon av flera tillgängliga metoder för att hålla definitionerna av skadlig kod uppdaterade på klient datorer i hierarkin. Informationen i den här artikeln kan hjälpa dig att välja och konfigurera dessa metoder.

 Du kan använda en eller flera av följande metoder för att uppdatera definitionerna för skadlig kod:

- [Uppdateringar som distribuerats från Configuration Manager](endpoint-definitions-configmgr.md) – den här metoden använder Configuration Manager program uppdateringar för att leverera definitions-och motor uppdateringar till datorer i hierarkin.

- [Uppdateringar som distribueras från Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md) – den här metoden använder WSUS-infrastrukturen för att leverera definitions-och motor uppdateringar till datorer.

- [Uppdateringar som distribueras från Microsoft Update](endpoint-definitions-microsoft-updates.md) – med den här metoden kan datorer ansluta direkt till Microsoft Update för att hämta definitions-och motor uppdateringar. Den här metoden är bra att använda för datorer som inte ansluter till företagsnätverket så ofta.

- [Uppdateringar som är distribuerade från Microsoft Malware Protection Center](endpoint-definitions-protection-center.md) – den här metoden hämtar definitions uppdateringar från Microsoft Malware Protection Center.

- [Uppdateringar från UNC-filresurser](endpoint-definitions-network.md) – med den här metoden kan du spara de senaste definitions-och motor uppdateringarna på en resurs i nätverket. Klienterna kan sedan komma åt nätverket för att installera uppdateringarna.

  Du kan konfigurera flera definitionsuppdateringskällor och bestämma i vilken ordning som de bedöms och tillämpas. Det gör du i dialogrutan **Konfigurera definitionsuppdateringskällor** när du skapar en princip för program mot skadlig kod.

> [!IMPORTANT]
>  För Windows 10-datorer måste du konfigurera Endpoint Protection för att uppdatera definitioner för skadlig kod för Windows Defender.

## <a name="how-to-configure-definition-update-sources"></a>Konfigurera definitionsuppdateringskällor
 Använd följande metod för att konfigurera definitionsuppdateringskällor som ska användas till varje princip för program mot skadlig kod.

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.

2.  I arbetsytan **Tillgångar och efterlevnad** expanderar du **Endpoint Protection**och klickar på **Antiskadlig kod-principer**.

3.  Öppna sidan med egenskaper för **Standard-Antiskadlig kod-princip** eller skapa en ny princip för program mot skadlig kod. Mer information om hur du skapar principer för program mot skadlig kod finns i [skapa och distribuera principer för program mot skadlig kod för Endpoint Protection](endpoint-antimalware-policies.md).

4.  I avsnittet **Security Intelligence-uppdateringar** i dialog rutan Egenskaper för program mot skadlig kod klickar du på **Ange källa**.
    - Avsnittet **definitions uppdateringar** har bytt namn till **Security Intelligence-uppdateringar** från Configuration Manager version 1902.

5.  I dialogrutan **Konfigurera definitionsuppdateringskällor** väljer du de källor som ska användas för definitionsuppdateringar. Du kan klicka på **Uppåt** eller **Nedåt** för att ändra användningsordningen för dessa källor.

6.  Klicka på **OK** för att stänga dialogrutan **Konfigurera definitionsuppdateringskällor** .

## <a name="configure-endpoint-protection-definitions"></a>Konfigurera Endpoint Protection definitioner

-   [Uppdateringar som distribuerats från Configuration Manager](endpoint-definitions-configmgr.md) – den här metoden använder Configuration Manager program uppdateringar för att leverera definitions-och motor uppdateringar till datorer i hierarkin.

-   [Uppdateringar som distribueras från Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md) – den här metoden använder WSUS-infrastrukturen för att leverera definitions-och motor uppdateringar till datorer.

-   [Uppdateringar som distribueras från Microsoft Update](endpoint-definitions-microsoft-updates.md) – med den här metoden kan datorer ansluta direkt till Microsoft Update för att hämta definitions-och motor uppdateringar. Den här metoden är bra att använda för datorer som inte ansluter till företagsnätverket så ofta.

-   Uppdateringar som är distribuerade från Microsoft Malware Protection Center – den här metoden hämtar definitions uppdateringar från Microsoft Malware Protection Center.

-   [Uppdateringar från UNC-filresurser](endpoint-definitions-network.md) – med den här metoden kan du spara de senaste definitions-och motor uppdateringarna på en resurs i nätverket. Klienterna kan sedan komma åt nätverket för att installera uppdateringarna.
