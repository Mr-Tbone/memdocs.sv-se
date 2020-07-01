---
title: Blockera appar utan modern autentisering i Intune
titleSuffix: Microsoft Intune
description: Läs om appar och modern autentisering (ADAL) med Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.topic: conceptual
ms.technology: ''
ms.assetid: 73db3070-d033-40fb-a8f1-58b9d198021e
ms.reviewer: chrisgre
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4a8e61f30cfc21d6dfebef2315296e60dadcb7f1
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382823"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>Blockera appar som inte använder modern autentisering (ADAL)

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Appbaserad villkorlig åtkomst med appskyddsprinciper är beroende av program som använder [modern autentisering](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) som är en implementering av OAuth2. De senaste Office-programmen för mobila och stationära enheter använder modern autentisering. Det finns dock tredjepartsappar och äldre Office-program som använder andra autentiseringsmetoder, som grundläggande autentisering och formulärbaserad autentisering.

## <a name="block-access-to-apps"></a>Blockera åtkomst till appar

Använd Intunes appskyddsprinciper till att implementera villkorsstyrd åtkomst som blockerar åtkomst till appar utan modern autentisering. Mer information finns i [Appbaserad villkorlig åtkomst med Intune](app-based-conditional-access-intune.md).

## <a name="additional-information"></a>Ytterligare information

Mer information om villkorsstyrd åtkomst i Azure AD finns i följande avsnitt:
- [Vad är villkorlig åtkomst i Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Så här fungerar appbaserad villkorlig åtkomst](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [Konfigurera SharePoint Online och Exchange Online för villkorlig åtkomst i Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## <a name="next-steps"></a>Nästa steg

- [Appbaserad villkorlig åtkomst med Intune](app-based-conditional-access-intune.md)
