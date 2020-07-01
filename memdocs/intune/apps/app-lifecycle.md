---
title: Översikt över applivscykeln för Microsoft Intune
description: Läs mer om livscykeln för hanterade appar i Microsoft Intune. I applivscykeln ingår det att lägga till, distribuera, konfigurera, skydda och ta appar ur bruk.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 60347012-bc3f-4b9a-a4f4-6d3c5021a6e6
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: apps; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 890a42e3668b00a59f12498ab4f2ba3769225a96
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502705"
---
# <a name="overview-of-the-app-lifecycle-in-microsoft-intune"></a>Översikt över applivscykeln i Microsoft Intune

Applivscykeln i Microsoft Intune börjar när en app läggs till och fortsätter genom fler faser tills du tar bort appen. Om du förstår faserna har du den information du behöver för att komma igång med apphantering i Intune.

![Appens livscykel – Lägg till, distribuera, konfigurera, skydda och ta ur bruk.](./media/app-lifecycle/app-lifecycle.png "Intune-applivscykeln")

## <a name="add"></a>Lägg till

Det första steget i appdistributionen är att lägga till de appar som du vill hantera och tilldela i Intune. Det finns många olika apptyper som du kan arbeta med, men de grundläggande procedurerna är samma. Med Intune kan du lägga till olika apptyper, däribland appar som skrivits internt (verksamhetsspecifik), appar från butiken, inbyggda appar och appar på webben. Mer information om varje apptyp finns i [Så här lägger du till en app i Microsoft Intune](apps-add.md).

## <a name="deploy"></a>Distribuera

När du har lagt till appen i Intune kan du sedan [tilldela den till användare och enheter som du hanterar](apps-deploy.md). I Intune är den här processen enkel och när appen har distribuerats kan du [övervaka framgången](apps-monitor.md) för distributionen från Intune i Azure Portal. Dessutom kan du i vissa appbutiker, till exempel appbutikerna för [Apple](vpp-apps-ios.md) och [Windows](windows-store-for-business.md), köpa applicenser gruppvis till företaget. Intune kan synkronisera data med dessa butiker så att du kan distribuera och spåra licensanvändning för dessa typer av appar direkt från Intune-administrationskonsolen.

## <a name="configure"></a>Konfigurera

Som en del av applivscykeln släpps regelbundet nya versioner av appar. Intune tillhandahåller verktyg för att enkelt [uppdatera appar](apps-add.md) som du har distribuerat till en senare version. Dessutom kan du konfigurera ytterligare funktioner för vissa appar, till exempel:

- [Konfigurationsprinciper för iOS/iPadOS-appar](app-configuration-policies-use-ios.md) tillhandahåller inställningar för kompatibla iOS/iPadOS-appar som används när appen körs. En app kan till exempel kräva specifika inställningar för anpassning eller namnet på en server som den måste ansluta till.
- [Hanterade webbläsarprinciper](manage-microsoft-edge.md) hjälper dig att konfigurera inställningar för den hanterade [Microsoft Edge](apps-supported-intune-apps.md#microsoft-apps) som ersätter enhetens standardwebbläsare och du kan begränsa vilka webbplatser som användarna kan besöka.

## <a name="protect"></a>Skydda

Intune ger många sätt att skydda data i dina appar. De viktigaste metoderna är:

- [Villkorlig åtkomst](../protect/conditional-access.md) styr åtkomsten till e-post och andra tjänster utifrån de villkor som du anger. Villkor innefattar enhetstyper eller efterlevnad av en [enhetsefterlevnadsprincip](../protect/device-compliance-get-started.md) som du har distribuerat.
- [Appskyddsprinciperna](app-protection-policy.md) används i enskilda appar för att skydda de företagsdata som de använder. Du kan till exempel begränsa kopiering av data mellan ohanterade appar och appar som du hanterar, eller förhindra att appar körs på enheter som har jailbreakats eller rotats.

## <a name="retire"></a>Pensionera

Så småningom är det troligt att appar som du har distribuerat blir inaktuella och måste tas bort. Intune gör det enkelt att avinstallera appar. Mer information finns i [Avinstallera en app](../apps/apps-add.md#uninstall-an-app).

## <a name="next-steps"></a>Nästa steg

- Läs mer om [apphantering i Microsoft Intune](app-management.md)
