---
title: Integrera Lookout Mobile Endpoint med Microsoft Intune
titleSuffix: Microsoft Intune
description: Läs mer om hur du integrerar Intune med Lookout Mobile Threat Defense (MTD) för att styra mobil enhetsåtkomst till företagets resurser.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9bf06c5057cecd63b5717440eba8bad0542ab642
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461325"
---
# <a name="lookout-mobile-endpoint-security-connector-with-intune"></a>Lookout Mobile Endpoint Security-anslutningsprogram med Intune

Du kan styra åtkomsten från mobila enheter till företagsresurser baserat på den riskbedömning som utförs av Lookout, en Mobile Threat Defense-lösning som är integrerad med Microsoft Intune. Risken bedöms utifrån telemetri som samlas in från enheter som använder Lookout-tjänsten och inkluderar:
- Säkerhetsproblem med operativsystemversion
- Installerade skadliga program
- Skadliga nätverksprofiler

Du kan konfigurera principer för villkorsstyrd åtkomst baserat på riskbedömningen i Lookout. Den aktiveras via Intune-efterlevnadsprinciper för registrerade enheter, som du kan använda för att tillåta eller blockera åtkomst för icke-kompatibla enheter till företagets resurser baserat på de hot som har identifierats. För oregistrerade enheter kan du använda appskyddsprinciper till att framtvinga en blockering eller selektiv rensning baserat på identifierade hot.

## <a name="how-do-intune-and-lookout-mobile-endpoint-security-help-protect-company-resources"></a>Hur skyddar Intune och Lookout Mobile Endpoint Security företagets resurser?

Lookouts mobilapp, **Lookout for Work**, är installerad och körs på mobila enheter. Den här appen avbildar filsystem, nätverksstackar samt telemetri för enheter och program där det är tillgängligt och skickar det sedan till Lookouts molntjänst för att utvärdera enhetens risk för mobila hot. Du kan ändra risknivåklassificeringen för hot i Lookout-konsolen så som den passar dig.

- **Stöd för registrerade enheter** – Intune-enhetens efterlevnadsprincip innehåller en regel för MTD (Mobile Threat Defense) som kan använda informationen om riskbedömning från Lookout for Work. När MTD-regeln är aktiverad utvärderar Intune enhetens efterlevnad med principen som du har aktiverat. Om enheten inte bedöms uppfylla efterlevnadskraven nekas användarna åtkomst till företagsresurser som Exchange Online och SharePoint Online. Användarna får också instruktioner från Lookout for Work-appen som är installerad på deras enheter, som hjälper dem att åtgärda problemet så att de kan komma åt företagets resurser igen. Stöd för användning av Lookout for Work med registrerade enheter:
  - [Lägga till MTD-appar till enheter](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Skapa en enhetsefterlevnadsprincip som stöder MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Aktivera MTD-anslutningen i Intune](../protect/mtd-connector-enable.md)

- **Stöd för oregistrerade enheter** – Intune kan använda riskbedömningsdata från Lookout for Work-appen på oregistrerade enheter, om du använder Intunes appskyddsprinciper. Administratörer kan använda den här kombinationen för att skydda företagsdata i en [Microsoft Intune-skyddad app](../apps/apps-supported-intune-apps.md). De kan även utfärda en blockering eller en selektiv rensning av företagsdata på dessa oregistrerade enheter. Stöd för användning av Lookout for Work med oregistrerade enheter:
  - [Lägga till MTD-appen på oregistrerade enheter](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Skapa en appskyddsprincip för Mobile Threat Defense](../protect/mtd-app-protection-policy.md)
  - [Aktivera MTD-anslutningsprogrammet i Intune för oregistrerade enheter](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Plattformar som stöds

Följande plattformar har stöd för Lookout efter att ha registrerats i Intune:

- **Android 4.1 och senare**  
- **iOS 8 och senare**  

Mer information om stöd för plattformar och språk finns på [Lookout-webbplatsen](https://personal.support.lookout.com/hc/articles/114094140253).  

## <a name="prerequisites"></a>Krav

- Enterprise-prenumeration för Lookout Mobile EndPoint Security  
- Microsoft Intune-prenumeration
- Azure Active Directory Premium
- Enterprise Mobility och Security (EMS) E3 eller E5, med licenser som tilldelas användare.  

Se [Lookout Mobile EndPoint Security](https://www.lookout.com/products/mobile-endpoint-security) för mer information

## <a name="sample-scenarios"></a>Exempelscenarier

Här visas vanliga scenarier för användning av Mobile Endpoint Security med Intune.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Kontrollera åtkomst baserat på hot från skadliga program

När skadliga program som till exempel skadlig kod upptäckts på enheter kan du blockera enheterna från följande till dess att hotet har åtgärdats:

- Ansluta till företagets e-post
- Synkronisera företagets filer med appen OneDrive för arbetet
- Åtkomst till företagsappar

*Blockera när skadliga appar identifieras:*

> [!div class="mx-imgBorder"]
> ![Konceptbild av hur principen blockerar åtkomst på grund av skadliga appar](./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png)

*Åtkomst beviljad när problemet är löst:*

> [!div class="mx-imgBorder"]
> ![Konceptbild som visar när åtkomst beviljas till enheter efter åtgärd](./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Kontrollera åtkomst baserat på hot mot nätverket

Identifiera hot mot ditt nätverk, till exempel man-in-the-middle-angrepp, och skydda åtkomsten till WiFi-nätverk baserat på enhetens risk.

*Blockera nätverksåtkomst via Wi-Fi:*

> [!div class="mx-imgBorder"]
> ![Bild som visar blockering av WiFi-åtkomst baserat på nätverkshot](./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png)

*Åtkomst beviljad när problemet är löst:*

> [!div class="mx-imgBorder"]
> ![Konceptbild av Villkorlig åtkomst som beviljar åtkomst efter åtgärd](./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Kontrollera åtkomst till SharePoint Online baserat på hot mot nätverket

Identifiera hot mot ditt nätverk, till exempel man-in-the-middle-angrepp, och förhindra synkronisering av företagsfiler baserat på enhetens risk för angrepp.

*Blockera SharePoint Online när hot identifieras på nätverket:*

> [!div class="mx-imgBorder"]
> ![Konceptbild som visar blockerad åtkomst till SharePoint Online](./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png)

*Åtkomst beviljad när problemet är löst:*

> [!div class="mx-imgBorder"]
> ![Konceptbild som visar beviljad åtkomst efter att nätverkshot har åtgärdats](./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Kontrollera åtkomst till oregistrerade enheter baserat på hot från skadliga appar

När MTD-lösningen i Lookout bedömer att en enhet är infekterad:
> [!div class="mx-imgBorder"]
> ![Appskyddsprincipen blockerar på grund av identifierad skadlig kod](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png)

Åtkomst beviljas när problemet är löst:

> [!div class="mx-imgBorder"]
> ![Åtkomst beviljas när problemet är löst i appskyddsprincipen](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png)

## <a name="next-steps"></a>Nästa steg

Här följer de åtgärder du måste utföra för att implementera den här lösningen:

- [Ställa in Lookout-integrering](lookout-mtd-connector-integration.md)
- [Aktivera Mobile Endpoint Security i Intune](mtd-connector-enable.md)
- [Lägga till och tilldela appen Lookout for Work](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Konfigurera Lookout-enhetens efterlevnadsprincip](mtd-device-compliance-policy-create.md)
- [Skapa en MTD-appskyddspolicy](mtd-app-protection-policy.md)
