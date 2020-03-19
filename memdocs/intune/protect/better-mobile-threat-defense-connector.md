---
title: Better Mobile Threat Defense-anslutning i Intune
titleSuffix: Intune on Azure
description: Ställ in Better Mobile Threat Defense-anslutningen i Intune.
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
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05dec05cdc5a16078328d736d2f622cea1b2aa00
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79353989"
---
# <a name="better-mobile-threat-defense-connector-with-intune"></a>Better Mobile Threat Defense-anslutning i Intune

Du kan styra åtkomsten från mobila enheter till företagsresurser med villkorlig åtkomst baserat på riskbedömning som utförs av Better Mobile, en MTD-lösning (Mobile Threat Defense) som är integrerad i Microsoft Intune. Risken bedöms utifrån telemetri som samlas in från enheter som kör Better Mobile-appen.

Du kan konfigurera principer för villkorlig åtkomst baserat på Better Mobiles riskbedömning. Den aktiveras via Intune-efterlevnadsprinciper för registrerade enheter, som du kan använda för att tillåta eller blockera åtkomst för icke-kompatibla enheter till företagets resurser baserat på de hot som har identifierats. För oregistrerade enheter kan du använda appskyddsprinciper för att framtvinga en blockering eller selektiv rensning baserat på identifierade hot.

## <a name="how-do-intune-and-better-mobile-help-protect-your-company-resources"></a>Hur skyddar Intune och Better Mobile företagets resurser?

Better Mobile-appen installeras och körs på mobila enheter. Den här appen avbildar filsystem, nätverksstackar, enheter och programtelemetri där det är tillgängligt, och skickar sedan data till Better Mobiles molntjänst för att utvärdera enhetens risk för mobila hot.

- **Stöd för registrerade enheter** – Intune-enhetens efterlevnadsprincip innehåller en regel för MTD (Mobile Threat Defense) som kan använda informationen om riskbedömning från Better Mobile. När MTD-regeln är aktiverad utvärderar Intune enhetens efterlevnad med principen som du har aktiverat. Om enheten inte bedöms uppfylla efterlevnadskraven nekas användarna åtkomst till företagsresurser som Exchange Online och SharePoint Online. Användarna får också instruktioner från Better Mobile-appen som är installerad på deras enheter, som hjälper dem att åtgärda problemet så att de kan komma åt företagets resurser igen. Stöd för användning av Better Mobile med registrerade enheter:
  - [Lägga till MTD-appar till enheter](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Skapa en enhetsefterlevnadsprincip som stöder MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Aktivera MTD-anslutningsprogrammet i Intune](../protect/mtd-connector-enable.md)

- **Stöd för oregistrerade enheter** – Intune kan använda riskbedömningsdata från Better Mobile-appen på oregistrerade enheter, om du använder Intunes appskyddsprinciper. Administratörer kan använda den här kombinationen för att skydda företagsdata i en [Microsoft Intune-skyddad app](../apps/apps-supported-intune-apps.md). De kan även utfärda en blockering eller en selektiv rensning av företagsdata på dessa oregistrerade enheter. Stöd för användning av Better Mobile med oregistrerade enheter:
  - [Lägga till MTD-appen på oregistrerade enheter](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Skapa en appskyddsprincip för Mobile Threat Defense](../protect/mtd-app-protection-policy.md)
  - [Aktivera MTD-anslutningsprogrammet i Intune för oregistrerade enheter](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Plattformar som stöds

- **Android 4.1 och senare**

- **iOS 8.0 och senare**

## <a name="prerequisites"></a>Krav

- Azure Active Directory Premium

- Microsoft Intune-prenumeration

- Prenumeration på Better Mobile Threat Defense

  - Mer information finns på [Better Mobiles webbplats](https://www.better.mobi/).

## <a name="sample-scenarios"></a>Exempelscenarier

Nedan visas några vanliga scenarier.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Kontrollera åtkomst baserat på hot från skadliga program

När skadliga program som till exempel skadlig kod upptäckts på enheter kan du blockera enheterna från följande åtgärder tills hotet har åtgärdats:

- Ansluta till företagets e-post

- Synkronisera företagets filer med appen OneDrive för arbetet

- Åtkomst till företagsappar

Blockera när skadliga appar identifieras:

![Bild som visar att skadliga appar har identifierats](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png)

Åtkomst beviljas när problemet är löst:

![Beviljad åtkomst till skadliga appar upptäcktes](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Kontrollera åtkomst baserat på hot mot nätverket

Identifiera hot mot ditt nätverk såsom **man-in-the-middle**-angrepp, och skydda åtkomsten till Wi-Fi-nätverk baserat på enhetens risk.

Blockera nätverksåtkomst via Wi-Fi:

![Blockera nätverksåtkomst via Wi-Fi](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png)

Åtkomst beviljas när problemet är löst:

![Bild av beviljad åtkomst när problemet är löst](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Kontrollera åtkomst till SharePoint Online baserat på hot mot nätverket

Identifiera hot mot ditt nätverk såsom **man-in-the-middle**-angrepp, och förhindra synkronisering av företagsfiler baserat på enhetens risk för angrepp.

Blockera SharePoint Online när hot identifieras på nätverket:

![Blockera SharePoint Online när hot identifieras på nätverket](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png)

Åtkomst beviljad efter problemet är löst:

![Åtkomst beviljad när problemet är löst för Sharepoint-exempel](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png)

### <a name="control--access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Kontrollera åtkomst till oregistrerade enheter baserat på hot från skadliga appar

När MTD-lösningen i Better Mobile bedömer att en enhet är infekterad: ![Appskyddsprincipen blockerar på grund av identifierad skadlig kod](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png)

Åtkomst beviljas när problemet är löst:

![Åtkomst beviljas när problemet är löst i appskyddsprincipen](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Nästa steg

- [Integrera Better Mobile med Intune](better-mobile-mtd-connector-integration.md)

- [Konfigurera Better Mobile-appar](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Skapa en efterlevnadsprincip för enheter med Better Mobile](mtd-device-compliance-policy-create.md)

- [Aktivera Better Mobile MTD-anslutningen](mtd-connector-enable.md)

- [Skapa en MTD-appskyddsprincip](mtd-app-protection-policy.md) 
