---
title: macOS Antivirus principinställningar för Microsoft Defender Antivirus för Intune | Microsoft Docs
description: Se en lista över inställningarna i Microsoft Defender Antivirus-profilen för macOS. Den här profilen är en del av antivirusprinciperna för slutpunktssäkerhet för macOS i Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: samyada
ms.openlocfilehash: a75fe5bac4bb99b30e21ec842dcbbe3be83e9e5b
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909456"
---
# <a name="settings-for-microsoft-defender-atp-for-mac-in-microsoft-intune"></a>Inställningar för Microsoft Defender ATP för Mac i Microsoft Intune

Visa profilinställningarna för *Antivirus* som du kan konfigurera för Microsoft Defender ATP för Mac i Microsoft Intune. Mer information om de här inställningarna finns i texten om [Microsoft Defender Advanced Threat Protection för Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) i Windows-dokumentationen.

Lär dig mer med hjälp av [Endpoint Security-policyer](../protect/endpoint-security-policy.md) i Intune.

**Microsoft Defender ATP**

- **Realtidsskydd**  
  Kräv att Defender på macOS-enheter ska använda funktionen för övervakning i realtid. Övervakning i realtid hittar och hindrar skadlig kod från att installeras eller köras på enheten. Du kan inaktivera den här inställningen en kort stund och sedan aktiveras den igen automatiskt.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Aktiverad** – Framtvinga användning av övervakning i realtid. Enhetsanvändare kan inte ändra den här inställningen.
  - **Inaktiverad** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.

- **Molnlevererat skydd**  
  Som standard skickar Defender information till Microsoft om eventuella problem som identifieras. Microsoft analyserar informationen för att lära sig mer om problem som påverkar dig och andra kunder och erbjuda bättre lösningar. Skyddet fungerar bäst när *Skicka stickprov automatiskt* har aktiverats.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Aktiverad** – Molnlevererat skydd är aktiverat. Enhetsanvändare kan inte ändra den här inställningen.
  - **Inaktiverad** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.

- **Skicka stickprov automatiskt**  
  Skickar exempelfiler till Microsoft för att hjälpa till att skydda enhetsanvändare och din organisation från potentiella hot.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Aktiverad** – Molnlevererat skydd är aktiverat.  Enhetsanvändare kan inte ändra den här inställningen.
  - **Inaktiverad** – Inställningen är inaktiverad. Enhetsanvändare kan inte ändra den här inställningen.

- **Insamling av diagnostikdata**

  Konfigurera hur diagnostik- och användningsdata delas med Microsoft.

  - **Inte konfigurerad** (*standard*) – Inställningen återställs till systemets standard.
  - **Obligatoriskt**
  - **Valfritt**

- **Mappar som undantas från genomsökning**  
  Välj **Lägg till** och ange sedan mappar som ska ignoreras vid en genomsökning.

- **Filer som undantas från genomsökning**  
  Välj **Lägg till** och ange sedan filer som ska ignoreras vid en genomsökning.

- **Filtyper som inte ska genomsökas**  
  Välj **Lägg till** och ange sedan filtillägg som ska ignoreras vid en genomsökning.

- **Processer som inte ska genomsökas**  
  Välj **Lägg till** och ange sedan processer som ska ignoreras vid en genomsökning.