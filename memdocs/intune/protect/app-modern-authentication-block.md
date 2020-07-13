---
title: Blockera appar utan modern autentisering i Intune
titleSuffix: Microsoft Intune
description: Läs om appar och modern autentisering (ADAL) med Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/22/2020
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
ms.openlocfilehash: bd8070dd1584beac0744ebfae63aa4fd066fa2bf
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022253"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>Blockera appar som inte använder modern autentisering (ADAL)

> [!NOTE]
> Azure Active Directory-autentiseringsbibliotek (ADAL) och Azure AD Graph API kommer att bli inaktuella. Mer information finns i [Uppdatera dina program för användning med Microsoft Authentication Library (MSAL) och Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

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
