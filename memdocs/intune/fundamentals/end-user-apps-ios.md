---
title: Så får dina iOS/iPadOS-användare sina appar
description: Metoder för att göra iOS/iPadOS-appar tillgängliga för slutanvändare
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 957c63c760dcc576ab30bb85440d52833307818d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79344096"
---
# <a name="how-your-iosipados-users-get-their-apps"></a>Så får dina iOS/iPadOS-användare sina appar

Använd informationen för att förstå hur och var dina slutanvändare får de appar som du distribuerar via Microsoft Intune.

**Obligatoriska appar** – Appar som krävs av administratören och som installeras på enheten med minimal inblandning av användaren, beroende på plattform.

**Tillgängliga appar** – Appar som finns i företagsportalens applista och som en användare kan välja att installera.

**Hanterade appar** – Appar som kan hanteras med principer och har blivit "omslutna" av Intune eller skapats med Intune App Software Development Kit (SDK). De här apparna kan hanteras av Intune och appskyddsprinciper kan tillämpas på dem.

**Ohanterade appar** – appar som användare kan ladda ned från iOS/iPadOS App Store som inte är integrerade med Intune App SDK. Intune har ingen kontroll över distribution, hantering eller selektiv rensning av dessa appar.  

Registrerade användare får sina appar genom att trycka på följande paneler på skärmen Appar i företagsportalappen:

- **Alla appar** pekar på en lista över alla appar på fliken ALLA på [företagsportalens webbplats](https://portal.manage.microsoft.com).

- **Aktuella appar** omdirigerar användarna till fliken AKTUELLA på företagsportalens webbplats.

- **Kategorier** pekar på fliken KATEGORIER på företagsportalens webbplats.

![Skärmen Appar på företagsportalen för iOS](./media/end-user-apps-ios/ios-cp-app-main-apps-screen.png)

Mer information om hur man lägger till appar finns i [Så här lägger du till en app i Microsoft Intune](../apps/apps-add.md).

## <a name="app-management-takeover"></a>Övertagande av apphantering
Om en app redan är installerad på en slutanvändares enhet, visar iOS-/iPadOS-enheten ett meddelande om att tillåta hantering av appen av din organisation. Slutanvändaren måste tillåta att organisationen tar över hanteringen av appen innan appkonfigurationer kan tillämpas på en hanterad enhet. Om användaren avbryter meddelandet visas det med jämna mellanrum så länge enheten hanteras och appen är tilldelad.  


![Bild av aviseringen för apphanteringsändringen, med alternativen Avbryt och Hantera.](./media/end-user-apps-ios/intune-app-management-confirmation-2002.png)

## <a name="see-also"></a>Se även  

[Så får dina Android-användare sina appar](end-user-apps-android.md)

[Så får dina Windows-användare sina appar](end-user-apps-windows.md)
