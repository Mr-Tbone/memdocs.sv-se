---
title: Pradeo Mobile Threat Defense-anslutningsapp med Intune
titleSuffix: Intune on Azure
description: Läs mer om hur du integrerar anslutningsprogrammet Intune med Pradeo Mobile Threat Defense för att styra mobila enheters åtkomst till företagsresurser.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: cde4d389-1770-4226-85a3-a2f3b3fb92a3
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: a23155c31586992c82781998bb664bf2ce6a0889
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79339182"
---
# <a name="pradeo-mobile-threat-defense-connector-with-intune"></a>Pradeo Mobile Threat Defense-anslutningsapp med Intune

Du kan styra åtkomsten från mobila enheter till företagsresurser med villkorlig åtkomst baserat på riskbedömning som utförs av Pradeo, en Mobile Threat Defense-lösning (MTD) som är integrerad med Microsoft Intune. Risken bedöms utifrån telemetri som samlas in från enheter som kör Pradeo-appen.

Du kan konfigurera principer för villkorlig åtkomst baserat på Pradeos riskbedömning. Den aktiveras via Intunes efterlevnadsprinciper för enheter, som du kan använda för att tillåta eller blockera åtkomst för icke-kompatibla enheter till företagets resurser baserat på de hot som har identifierats.

> [!NOTE]
> Den här Mobile Threat Defense-leverantören stöds inte för oregistrerade enheter.

## <a name="supported-platforms"></a>Plattformar som stöds

- **Android 4.0.3 och senare**

- **iOS 7 och senare**

## <a name="prerequisites"></a>Förutsättningar

- Azure Active Directory Premium

- Microsoft Intune-prenumeration

- Prenumeration på Pradeo Security for Mobile Threat Defense

  - Mer information finns på [Pradeos webbplats](https://www.pradeo.com/en-US/mobile-threat-protection).

## <a name="how-do-intune-and-pradeo-help-protect-your-company-resources"></a>Hur skyddar Intune och Pradeo företagets resurser?

Pradeo-appen för Android och iOS/iPadOS samlar in tillgängliga telemetridata om filsystem, nätverksstackar, enheter och program. Dessa data skickas sedan till Pradeo-molntjänsten för bedömning av risken för mobila hot på enheten.

Intune-enhetens efterlevnadsprincip innehåller en regel för Pradeo Mobile Threat Defense, som är baserad på Pradeos riskbedömning. När den här regeln är aktiverad utvärderar Intune enhetens efterlevnad med principen som du har aktiverat. Om enheten inte bedöms uppfylla efterlevnadskraven nekas användarna åtkomst till företagsresurser som Exchange Online och SharePoint Online. Användarna får också instruktioner från Pradeo-appen som är installerad på deras enheter, som hjälper dem att åtgärda problemet så att de kan komma åt företagets resurser igen.

## <a name="sample-scenarios"></a>Exempelscenarier

Nedan visas några vanliga scenarier.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Kontrollera åtkomst baserat på hot från skadliga program

När skadliga program som till exempel skadlig kod upptäckts på enheter kan du blockera enheterna från följande åtgärder tills hotet har åtgärdats:

- Ansluta till företagets e-post

- Synkronisera företagets filer med appen OneDrive för arbetet

- Åtkomst till företagsappar

*Blockera när skadliga appar identifieras:*

![Konceptbild av skadliga appar som har identifierats](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-blocked.png)

*Åtkomst beviljad när problemet är löst:*

![Beviljad åtkomst till skadliga appar upptäcktes](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Kontrollera åtkomst baserat på hot mot nätverket

Identifiera hot mot ditt nätverk såsom **man-in-the-middle**-angrepp, och skydda åtkomsten till Wi-Fi-nätverk baserat på enhetens risk.

*Blockera nätverksåtkomst via Wi-Fi:*

![Blockera nätverksåtkomst via Wi-Fi](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-blocked.png)

*Åtkomst beviljad när problemet är löst:*

![Konceptbild av beviljad åtkomst när problemet är löst](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Kontrollera åtkomst till SharePoint Online baserat på hot mot nätverket

Identifiera hot mot ditt nätverk såsom **man-in-the-middle**-angrepp, och förhindra synkronisering av företagsfiler baserat på enhetens risk för angrepp.

*Blockera SharePoint Online när hot identifieras på nätverket:*

![Blockera SharePoint Online när hot identifieras på nätverket](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-blocked.png)

*Åtkomst beviljad när problemet är löst:*

![Konceptbild av beviljad åtkomst när problemet är löst för Sharepoint-exempel](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-unblocked.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Pradeo Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Nästa steg

- [Integrera Pradeo med Intune](pradeo-mtd-connector-integration.md)

- [Konfigurera Pradeo-appar](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Skapa en policy för efterlevnad för Pradeo-enheter](mtd-device-compliance-policy-create.md)

- [Aktivera Pradeo MTD-anslutningsapp](mtd-connector-enable.md)
