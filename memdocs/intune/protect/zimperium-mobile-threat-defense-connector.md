---
title: Zimperium MTD-anslutningsprogram med Intune
titleSuffix: Intune on Azure
description: Läs mer om hur du integrerar Intune med Zimperium Mobile Threat Defense för att styra mobil enhetsåtkomst till företagets resurser.
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
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b443f922b31523ec6f27971648ba1ea9c5123867
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989394"
---
# <a name="zimperium-mobile-threat-defense-connector-with-intune"></a>Zimperium Mobile Threat Defense-anslutning med Intune

Du kan styra åtkomsten från mobila enheter till företagsresurser med villkorlig åtkomst, baserat på riskbedömning som utförs av Zimperium, en Mobile Threat Defense-lösning (MTD) som är integrerad med Microsoft Intune. Risken bedöms utifrån telemetri som samlas in från enheter som kör Zimperium-appen.

Du kan konfigurera principer för villkorlig åtkomst baserat på Zimperium-riskbedömning. Den aktiveras via Intune-efterlevnadsprinciper för registrerade enheter, som du kan använda för att tillåta eller blockera åtkomst för icke-kompatibla enheter till företagets resurser baserat på de hot som har identifierats. För oregistrerade enheter kan du använda appskyddsprinciper för att framtvinga en blockering eller selektiv rensning baserat på identifierade hot.

## <a name="supported-platforms"></a>Plattformar som stöds

- **Android 4.1 och senare**

- **iOS 8 och senare**

## <a name="prerequisites"></a>Förutsättningar

- Azure Active Directory Premium

- Microsoft Intune-prenumeration

- Prenumeration på Zimperium Mobile Threat Defense

  - Mer information finns på [Zimperiums webbplats](https://www.zimperium.com/zips-mobile-ips).

## <a name="how-do-intune-and-zimperium-help-protect-your-company-resources"></a>Hur skyddar Intune och Zimperium företagets resurser?

Zimperium-appen för Android och iOS/iPadOS samlar in tillgängliga telemetridata om filsystem, nätverksstackar, enheter och program. Dessa data skickas sedan till Zimperium-molntjänsten för bedömning av risken för mobila hot på enheten.

- **Stöd för registrerade enheter** – Intune-enhetens efterlevnadsprincip innehåller en regel för MTD (Mobile Threat Defense) som kan använda informationen om riskbedömning från Zimperium. När MTD-regeln är aktiverad utvärderar Intune enhetens efterlevnad med den princip som du har aktiverat. Om enheten inte bedöms uppfylla efterlevnadskraven nekas användarna åtkomst till företagsresurser som Exchange Online och SharePoint Online. Användarna får också instruktioner från Zimperium-appen som är installerad på deras enheter, som hjälper dem att åtgärda problemet så att de kan komma åt företagets resurser igen. Stöd för användning av Zimperium med registrerade enheter:
  - [Lägga till MTD-appar till enheter](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Skapa en enhetsefterlevnadsprincip som stöder MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Aktivera MTD-anslutningen i Intune](../protect/mtd-connector-enable.md)

- **Stöd för oregistrerade enheter** – Intune kan använda riskbedömningsdata från Zimperium-appen på oregistrerade enheter, om du använder Intunes appskyddsprinciper. Administratörer kan använda den här kombinationen för att skydda företagsdata i en [Microsoft Intune-skyddad app](../apps/apps-supported-intune-apps.md). De kan även utfärda en blockering eller en selektiv rensning av företagsdata på dessa oregistrerade enheter. Stöd för användning av Zimperium med oregistrerade enheter:
  - [Lägga till MTD-appen på oregistrerade enheter](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Skapa en appskyddsprincip för Mobile Threat Defense](../protect/mtd-app-protection-policy.md)
  - [Aktivera MTD-anslutningsprogrammet i Intune för oregistrerade enheter](../protect/mtd-enable-unenrolled-devices.md)
  
## <a name="sample-scenarios"></a>Exempelscenarier

Nedan följer några scenarier vid integrering av Zimperium med Intune:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Kontrollera åtkomst baserat på hot från skadliga program

När skadliga program som till exempel skadlig kod upptäckts på enheter kan du blockera enheterna till dess att hotet har åtgärdats:

- Ansluta till företagets e-post

- Synkronisera företagets filer med appen OneDrive för arbetet

- Åtkomst till företagsappar

*Blockera när skadliga appar identifieras:*

> [!div class="mx-imgBorder"]
> ![Konceptbild av skadliga appar som har identifierats](./media/zimperium-mobile-threat-defense-connector/Maliciousapps-blocked-zimperium.png)

*Åtkomst beviljad när problemet är löst:*

> [!div class="mx-imgBorder"]
> ![Konceptbild av beviljad åtkomst när problemet är löst](./media/zimperium-mobile-threat-defense-connector/maliciousapps-unblocked-zimperium.png)

### <a name="control-access-based-on-threat-to-network"></a>Kontrollera åtkomst baserat på hot mot nätverket

Identifiera hot, till exempel **Man-in-the-middle**-angrepp i nätverket, samt skydda åtkomsten till WiFi-nätverk baserat på enhetsrisken.

*Blockera nätverksåtkomst via Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Blockera nätverksåtkomst via Wi-Fi](./media/zimperium-mobile-threat-defense-connector/network-wifi-blocked-zimperium.png)

*Åtkomst beviljad när problemet är löst:*

> [!div class="mx-imgBorder"]
> ![Åtkomst beviljad när problemet är löst](./media/zimperium-mobile-threat-defense-connector/network-wifi-unblocked-zimperium.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Kontrollera åtkomst till SharePoint Online baserat på hot mot nätverket

Identifiera hot, till exempel **Man-in-the-middle**-angrepp i nätverket och förhindra synkronisering av företagsfiler baserat på enhetsrisken.

*Blockera SharePoint Online när hot identifieras på nätverket:*

> [!div class="mx-imgBorder"]
> ![Blockera SharePoint Online när hot identifieras på nätverket](./media/zimperium-mobile-threat-defense-connector/network-spo-blocked-zimperium.png)

*Åtkomst beviljad när problemet är löst:*

> [!div class="mx-imgBorder"]
> ![Åtkomst beviljad när problemet är löst för Sharepoint-exempel](./media/zimperium-mobile-threat-defense-connector/network-spo-unblocked-zimperium.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Kontrollera åtkomst till oregistrerade enheter baserat på hot från skadliga appar

När Mobile Threat Defense-lösningen för Zimperium bedömer att en enhet är infekterad gäller följande:

> [!div class="mx-imgBorder"]
> ![Appskyddsprincipen blockerar på grund av identifierad skadlig kod](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-block.png)

Åtkomst beviljas när problemet är löst:

> [!div class="mx-imgBorder"]
> ![Åtkomst beviljas när problemet är löst i appskyddsprincipen](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Nästa steg

- [Integrera Zimperium med Intune](zimperium-mtd-connector-integration.md)

- [Konfigurera Zimperium-appar](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Skapa en Zimperium-princip för enhetsefterlevnad](mtd-device-compliance-policy-create.md)

- [Aktivera Zimperium MTD-anslutningsprogram](mtd-connector-enable.md)

- [Skapa en MTD-appskyddsprincip](../protect/mtd-app-protection-policy.md)
