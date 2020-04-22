---
title: Microsoft Intune-enhetsbegränsningar för Windows 10 Team
titleSuffix: ''
description: Läs mer om enhetsbegränsningar som är tillgängliga för enheter som kör Windows 10 Team.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/6/2018
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31457667612617bb573ddfb145ed26f70de33159
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79361659"
---
# <a name="microsoft-intune-windows-10-team-device-restriction-settings"></a>Inställningar för begränsningar för Windows 10 Team-enheter i Microsoft Intune

I den här artikeln visas inställningarna av enhetsbegränsningar som du kan konfigurera för enheter som kör Windows 10 Team.

## <a name="apps-and-experience"></a>Appar och upplevelse

- **Aktivera skärm när någon är i rummet** – Tillåter att enheten aktiveras automatiskt när dess sensor känner av att någon är i rummet.
- **Mötesinformation som visas på välkomstskärmen** – Aktivera det här alternativet för att välja den information som ska visas i rutan Möten på välkomstskärmen. Du kan:
  - **Visa endast kalender och tid**
  - **Visa kalender, tid och ämne (ämnet är dolt för privata möten)**
- **Webbadress till bakgrundsbild för välkomstskärm** – Aktivera den här inställningen om du vill visa en anpassad bakgrund på **välkomstskärmen** på Windows 10 Team-enheter från den webbadress som du anger.<br>Bilden måste vara i PNG-format och webbadressen måste börja med **https://** .

## <a name="azure-operational-insights"></a>Azure Operational Insights

- **Operational Insights i Azure** – Operational Insights i Azure är en del av Microsoft Operations Manager-programsviten och samlar in, lagrar och analyserar loggfilsdata från Windows 10 Team-enheter.
Om du vill kunna ansluta till Azure Operational Insights måste du ange ett **Arbetsyte-ID** och en **Arbetsytenyckel**.

## <a name="maintenance"></a>Underhåll

- **Underhållsperiod för programuppdateringar** – Konfigurerar tidsperioden då uppdateringar till enheten kan göras. Du kan konfigurera fönstrets **Starttid** och **Varaktighet i timmar** (från 1–5 timmar).

## <a name="wireless-projection"></a>Trådlös projektion

- **PIN-kod för trådlös projektion** – Anger om du måste ange en PIN-kod innan du kan använda funktionerna för trådlös projektion för enheten.
- **Trådlös Miracast-projektion** – Välj det här alternativet om du vill att Windows 10 Team-enheten ska kunna använda Miracast-aktiverade enheter för att projicera innehåll.
- **Kanal för trådlös Miracast-projektion** – Välj den Miracast-kanal som ska användas för att upprätta anslutningen.

## <a name="next-steps"></a>Nästa steg

Använd informationen i [Konfigurera inställningar för enhetsbegränsningar](device-restrictions-configure.md) för att spara och tilldela profilen till användare och enheter.
