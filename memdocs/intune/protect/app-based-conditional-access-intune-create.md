---
title: Konfigurera en appbaserad villkorlig åtkomstprincip med Intune
titleSuffix: Microsoft Intune
description: Läs mer om att skapa en appbaserad villkorlig åtkomstprincip med Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1693515-de18-4553-91ef-801976cd3ec7
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d07b87bca934dac924f2d2c281ecb7b2a2e8a2c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989790"
---
# <a name="set-up-app-based-conditional-access-policies-with-intune"></a>Konfigurera appbaserade villkorliga åtkomstprinciper med Intune

Konfigurera appbaserade principer för villkorlig åtkomst för appar som finns med i listan över godkända appar. Listan över godkända appar består av appar som har testats av Microsoft.

[Intune-appskyddsprinciper](../apps/app-protection-policies.md) måste tillämpas på apparna innan du använder appbaserade principer för villkorlig åtkomst.

> [!IMPORTANT]
> Den här artikeln innehåller stegvisa anvisningar som beskriver hur du lägger till en enkel princip för appbaserad villkorsstyrd åtkomst. Du kan använda samma steg för andra molnappar. Se [Planera distribution av villkorsstyrd åtkomst](https://docs.microsoft.com/azure/active-directory/conditional-access/plan-conditional-access) för mer information.

## <a name="create-app-based-conditional-access-policies"></a>Skapa principer för appbaserad villkorsstyrd åtkomst

Villkorsstyrd åtkomst är en Azure Active Directory-teknik (Azure AD). Noden för villkorlig åtkomst som du kommer åt från *Intune* är samma nod som du kommer åt från *Azure AD*. Eftersom det är samma nod behöver du inte växla mellan Intune och Azure AD för att konfigurera principer.

Innan du kan skapa principer för villkorsstyrd åtkomst från administrationscentret för Microsoft Endpoint Manager måste du ha en Azure AD Premium-licens.

### <a name="to-create-an-app-based-conditional-access-policy"></a>Så här skapar du en appbaserad princip för villkorlig åtkomst

1. Logga in på [Administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)

2. Välj **Slutpunktssäkerhet** > **Villkorlig åtkomst** > **Ny princip**.

3. Ange ett **principnamn** och välj **Användare och grupper** under *Tilldelningar*. Använd inkludera eller exkludera alternativ för att lägga till grupper för principen och välj **Klar**.

4. Välj **Molnappar eller åtgärder** och välj vilka appar som ska skyddas. Välj till exempel **Välj appar** och sedan **Office 365 (förhandsversion)** .

   Klicka på **Klar** för att spara ändringarna.

5. Välj **Villkor** > **Klientappar** för att tillämpa principen till appar och webbläsare. Välj exempelvis **Ja** och aktivera sedan **Webbläsare** och **Mobilappar och skrivbordsklienter**.

   Klicka på **Klar** för att spara ändringarna.

6. Under *Åtkomstkontroller* väljer du **Bevilja** för att tillämpa villkorlig åtkomst baserat på enhetsefterlevnad. Välj till exempel **Bevilja åtkomst** > **Kräv godkänd klientapp** och **Kräv appskyddsprincip (förhandsversion)** och sedan **Kräv en av de markerade kontrollerna**.

   Välj **OK** för att spara ändringarna.

7. För **Aktivera princip** väljer du **På**och väljer sedan **Skapa** för att spara ändringarna.





## <a name="next-steps"></a>Nästa steg
[Blockera appar som inte har modern autentisering](app-modern-authentication-block.md)

## <a name="see-also"></a>Se även

[Skydda appdata med appskyddsprinciper](../apps/app-protection-policies.md)
[Villkorlig åtkomst i Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
