---
title: Konfigurera Check Point SandBlast MTD-anslutningsprogram med Intune
titleSuffix: Microsoft Intune
description: Läs mer om hur du integrerar Intune med Check Point SandBlast Mobile Threat Defense för att styra mobila enheters åtkomst till företagsresurser.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 706a4228-9bdf-41e0-b8d1-64c923dd2d2b
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a0645c771b304bfb4930f5cd365b9291366499b1
ms.sourcegitcommit: 42a4a4454e56fa681f0ad39f5e585492dfbad286
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330924"
---
# <a name="check-point-sandblast-mobile-threat-defense-connector-with-intune"></a>Check Point SandBlast Mobile Threat Defense-anslutningsapp för Intune

Du kan styra åtkomsten från mobila enheter till företagsresurser med villkorlig åtkomst baserat på riskbedömning som utförs av Check Point SandBlast Mobile, en lösning för skydd mot mobila hot som är integrerad med Microsoft Intune. Risken bedöms utifrån telemetri som samlas in från enheter som kör Check Point SandBlast Mobile-appen.

Du kan konfigurera principer för villkorlig åtkomst baserat på Check Point SandBlast Mobiles riskbedömning som aktiveras via Intunes efterlevnadsprinciper för enheter. Du kan använda dessa principer för att tillåta eller neka åtkomsten för icke-kompatibla enheter till företagsresurser baserat på de hot som har identifierats.

> [!NOTE]
> Den här Mobile Threat Defense-leverantören stöds inte för oregistrerade enheter.

## <a name="supported-platforms"></a>Plattformar som stöds

- **Android 4.1 och senare**

- **iOS 8 och senare**

## <a name="pre-requisites"></a>Förutsättningar

- Azure Active Directory Premium

- Microsoft Intune-prenumeration

- Check Point SandBlast Mobile Threat Defense-prenumeration
  - Se [Check Point SandBlasts webbplats](https://www.checkpoint.com/) för mer information.

## <a name="how-do-intune-and-check-point-sandblast-mobile-help-protect-your-company-resources"></a>Hur hjälper Intune och Check Point SandBlast Mobile dig att skydda dina företagsresurser?

Check Point Sandblast Mobile-appen för Android och iOS/iPadOS samlar in tillgängliga telemetridata om filsystem, nätverksstackar, enheter och program. Dessa data skickas sedan till Check Point SandBlast-molntjänsten för bedömning av risken för mobila hot på enheten.

Intunes efterlevnadsprincip för enheter innehåller en regel för Check Point SandBlast Mobile Threat Defense, som baseras på Check Point SandBlasts riskbedömning. När den här regeln är aktiverad utvärderar Intune enhetens efterlevnad med principen som du har aktiverat. Om enheten inte bedöms uppfylla efterlevnadskraven nekas användarna åtkomst till företagsresurser som Exchange Online och SharePoint Online. Användarna får också instruktioner från Check Point SandBlast Mobile-appen som är installerad på deras enheter, som hjälper dem att åtgärda problemet så att de kan komma åt företagets resurser igen.

Nedan visas några vanliga scenarier:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Kontrollera åtkomst baserat på hot från skadliga program

När skadliga program som till exempel skadlig kod upptäckts på enheter kan du blockera enheterna till dess att hotet har åtgärdats:

- Ansluta till företagets e-post

- Synkronisera företagets filer med appen OneDrive för arbetet

- Åtkomst till företagsappar

*Blockera när skadliga appar identifieras:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD-blockering när skadliga appar identifieras](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-2.PNG)

*Åtkomst beviljad när problemet är löst:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD-åtkomst beviljades](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-3.PNG)

### <a name="control-access-based-on-threat-to-network"></a>Kontrollera åtkomst baserat på hot mot nätverket

Identifiera hot, till exempel **Man-in-the-middle**-angrepp i nätverket, samt skydda åtkomsten till WiFi-nätverk baserat på enhetsrisken.

*Blockera nätverksåtkomst via Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD-blockering av nätverksåtkomst via Wi-Fi](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-4.PNG)

*Åtkomst beviljad när problemet är löst:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD-åtkomst via WiFi beviljades](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-5.PNG)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Kontrollera åtkomst till SharePoint Online baserat på hot mot nätverket

Identifiera hot, till exempel **Man-in-the-middle**-angrepp i nätverket och förhindra synkronisering av företagsfiler baserat på enhetsrisken.

*Blockera SharePoint Online när hot identifieras på nätverket:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD-blockering av åtkomst till SharePoint Online](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-6.PNG)

*Åtkomst beviljad när problemet är löst:*

> [!div class="mx-imgBorder"]
> ![Check Point MTD-åtkomst till SharePoint Online beviljades](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/checkpoint-mtd-7.PNG)

<!-- ### Control access on unenrolled devices based on threats from malicious apps

When the Check Point Sandblast Mobile Threat Defense solution considers a device to be infected:
> [!div class="mx-imgBorder"]
> ![App protection policy blocks due to detected malware](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-block.png)

Access is granted on remediation:

> [!div class="mx-imgBorder"]
> ![Access is granted on remediation for App protection policy](./media/checkpoint-sandblast-mobile-mobile-threat-defense-connector/sandblast-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Nästa steg

- [Integrera Check Point SandBlast med Intune](checkpoint-sandblast-mobile-mtd-connector-integration.md)

- [Konfigurera Check Point SandBlast Mobile-app](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Skapa policy för efterlevnad i CheckPoint SandBlast Mobile-enhet](mtd-device-compliance-policy-create.md)

- [Aktivera CheckPoint SandBlast Mobile MTD-anslutningsprogram](mtd-connector-enable.md)
