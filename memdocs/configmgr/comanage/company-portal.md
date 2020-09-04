---
title: Appar i Företagsportal
titleSuffix: Configuration Manager
description: Använd Företagsportal-appen för att ge en konsekvent användar upplevelse för samhanterade enheter.
ms.date: 09/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: 26456bb7-f46b-4d8d-bb0b-e3fd9a52fe14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cd49546e49d6964cfe37b0b13e1abe9175f4aa0e
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432565"
---
# <a name="use-the-company-portal-app-on-co-managed-devices"></a>Använd Företagsportalappen på samhanterade enheter

*Gäller för: Configuration Manager (aktuell gren)*

<!--CMADO-3601237,INADO-4297660-->

Från och med version 2006 är Företagsportal det nu den plattforms oberoende appens Portal upplevelse för Microsoft Endpoint Manager. Genom att konfigurera samhanterade enheter så att de också använder Företagsportal kan du ge en konsekvent användar upplevelse på alla enheter.

Företagsportal har stöd för följande åtgärder:

- Starta Företagsportal-appen på samhanterade enheter och logga in med Azure Active Directory (Azure AD) enkel inloggning (SSO).
- Visa tillgängliga och installerade Configuration Manager-appar i Företagsportal tillsammans med Intune-appar.
- Installera tillgängliga Configuration Manager appar från Företagsportal och ta emot information om installations status.

:::image type="content" source="media/3601237-company-portal.png" alt-text="Företagsportal med appen från Configuration Manager" lightbox="media/3601237-company-portal.png":::

Hur Företagsportal fungerar beror på arbets belastnings konfigurationen för samhantering:

| Arbetsbelastning | Inställning | Beteende |
|----------|---------|----------|
| Klientappar | **Configuration Manager** | Du kan bara se Configuration Manager klient program |
| Klientappar | **Pilot** -eller **Intune** -Intune | Du kan se både Configuration Manager-och Intune-klientprogram |
| Office Klicka-och-kör-appar | **Configuration Manager** | Du kan bara se Configuration Manager Office Klicka-och-kör-appar |
| Office Klicka-och-kör-appar | **Pilot** -eller **Intune** -Intune | Du kan bara se Intune Office Klicka-och-kör-appar |

Mer information finns i följande artiklar:

- [Diagram över app-arbetsbelastningar](workloads.md#diagram-for-app-workloads)

- [Så här växlar du Configuration Manager-arbetsbelastningar till Intune](how-to-switch-workloads.md)

## <a name="prerequisites"></a>Krav

- Configuration Manager aktuell gren version 2006 eller senare <sup>([Se vanliga frågor och svar](#bkmk_ver-prereq))</sup>

- Företagsportal app version 11.0.8980.0 eller senare

- Windows 10, version 1803 eller senare:

  - Registrerad för [samhantering](how-to-enable.md)

  - Åtkomst till [Internet-slutpunkter för Intune](../../intune/fundamentals/intune-endpoints.md)

- De användar konton som loggar in på dessa enheter kräver följande konfigurationer:

  - En Azure AD-identitet

  - Tilldelad en Intune-licens

## <a name="configure-and-deploy"></a>Konfigurera och distribuera

### <a name="configuration-manager-client-settings"></a>Configuration Manager klient inställningar

För att se till att användarna endast får meddelanden från Företagsportal konfigurerar du Configuration Manager klient inställningar. I **Software Center** -gruppen med enhets inställningar ändrar du **Välj den användar portal** som ska **företagsportal**.

Mer information om klient inställningar finns i följande artiklar:

- [Konfigurera klientinställningar](../core/clients/deploy/configure-client-settings.md)
- [Om klientinställningar](../core/clients/deploy/about-client-settings.md#software-center)

### <a name="deploy-the-company-portal-app"></a>Distribuera Företagsportal-appen

- Användare kan installera Företagsportal-appen manuellt från [Microsoft Store](https://www.microsoft.com/p/company-portal/9wzdncrfj3pz?activetab=pivot:overviewtab).

- Om du vill kräva appen på samhanterade enheter, är distributions processen beroende av statusen för [klient programs](workloads.md#client-apps) arbets belastningen för samhantering:

  - Om arbets belastningen klient appar är med Configuration Manager [skapar och distribuerar du ett program med Configuration Manager](../apps/get-started/create-and-deploy-an-application.md). Hämta offline Företagsportal-appen från [Microsoft Store för företag](https://www.microsoft.com/business-store).

  - Om arbets belastningen klient appar är med Intune kan du distribuera den via Configuration Manager eller [lägga till Windows 10 företagsportal-appen genom att använda Microsoft Intune](../../intune/apps/store-apps-company-portal-app.md).

Mer information om att anpassa Företagsportal för din organisation finns i [anpassa Intune-företagsportal-appen](../../intune/apps/company-portal-app.md).

## <a name="use-the-company-portal"></a>Använd Företagsportal

1. Starta Företagsportal från Start menyn. Den för tillfället inloggade användaren loggas in automatiskt på Företagsportal baserat på deras Azure AD-identitet.

1. Välj sidan **appar** . Du bör se Configuration Manager-apparna i listan.

1. Välj en av de appar som distribuerats från Configuration Manager.

    - Fliken **Översikt** visar information om appen, till exempel storlek, version och Publicerings datum.

    - Om du vill se att Configuration Manager är hanterings tjänsten för den här appen växlar du till fliken **Ytterligare information** .

    - Välj **Installera**för att installera appen. Företagsportal visar installations status och ett meddelande visas när det är klart.

    - Om appen redan är installerad väljer du **Avinstallera** för att ta bort appen.

    - Välj ellipsen ( `...` ) för ytterligare åtgärder, till exempel **Reparera** och **dela**.

        :::image type="content" source="media/3601237-company-portal-app-details.png" alt-text="Configuration Manager app med information i Företagsportal" lightbox="media/3601237-company-portal-app-details.png":::

    - När du har installerat en Configuration Manager-webbapp väljer du ellipsknappen-menyn och väljer sedan **Öppna i webbläsare** för att starta webbappen.

    - Om ett Configuration Manager program inte kan installeras med en känd felkod väljer du länken misslyckad status för att söka efter felkoden.

Om du ändrar klient inställningen för Företagsportal när en användare väljer ett Configuration Manager meddelande, startas Företagsportal. Om meddelandet är ett scenario som Företagsportal inte stöder, väljer du meddelandet startar Software Center.

Information om hur du felsöker problem med installation av Configuration Manager-appar finns i avsnittet **hjälp & support** i företagsportal. När du använder alternativet **Hämta hjälp** kan du skicka Configuration Manager loggfiler som en del av begäran.

## <a name="frequently-asked-questions-faq"></a>Vanliga frågor och svar (FAQ)

### <a name="im-using-configuration-manager-version-2002-why-is-the-new-company-portal-showing-configuration-manager-apps"></a><a name="bkmk_ver-prereq"></a> Jag använder Configuration Manager version 2002, varför är den nya Företagsportal som visar Configuration Manager appar?

Företagsportal version 11.0.8980.0 eller senare visar Configuration Manager-distribuerade program för alla samhanterade klienter som använder den. Configuration Manager version 2006 är förutsättningen eftersom den lägger till klient inställningen för att kontrol lera meddelanden. Om du installerar Företagsportal på en samhanterad enhet i en tidigare version eller inte konfigurerar klient inställningen kommer användarna att se meddelanden från båda portalerna. Den här upplevelsen kan vara förvirrande för användare.

### <a name="does-company-portal-support-applications-deployed-as-software-updates-from-configuration-manager"></a>Har Företagsportal program som distribuerats som program uppdateringar från Configuration Manager?

Ja. Om du distribuerar en app med funktionen program uppdateringar behandlar klienten den på samma sätt oavsett om användar upplevelsen är Företagsportal eller Software Center.

### <a name="can-users-repair-uninstall-and-update-configuration-manager-apps-in-company-portal"></a>Kan användare reparera, avinstallera och uppdatera Configuration Manager appar i Företagsportal?

Ja. Om du konfigurerar Configuration Manager-appen så att den stöder dessa ytterligare åtgärder Företagsportal har stöd för reparation, avinstallation och uppdatering.

## <a name="known-issues"></a>Kända problem

Följande funktioner i Software Center är inte tillgängliga i Företagsportal:

- Viss information om appar, till exempel om en omstart krävs eller den uppskattade tiden för att installera

- [Appgrupper](../apps/deploy-use/create-app-groups.md)

Andra kända problem:

- Om du distribuerar samma app från både Configuration Manager och Intune visas den två gånger i Företagsportal.

- När du söker i Företagsportal visas Intune-appar alltid innan Configuration Manager appar.

## <a name="next-steps"></a>Nästa steg

[Så här växlar du Configuration Manager-arbetsbelastningar till Intune](how-to-switch-workloads.md)

[Anpassa Intune-företagsportal-appen](../../intune/apps/company-portal-app.md)
