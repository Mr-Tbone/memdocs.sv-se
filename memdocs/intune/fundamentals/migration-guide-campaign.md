---
title: Starta en kampanj för Intune-migrering
titleSuffix: Microsoft Intune
description: Den här artikeln innehåller anvisningar för hur du startar en migreringskampanj i Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f781b029-50f2-46ee-8ff7-03b4a6719e80
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 11959de1d03c7aa9cd29de2b4069c6d7bc133f79
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79358448"
---
# <a name="phase-2-migration-campaign"></a>Fas 2: Migreringskampanj

Välj den migreringsmetod som passar din organisations behov bäst och justera implementeringsstrategin baserat på dina specifika krav. Resten av den här guiden beskriver de verktyg som du behöver för att dina användares enheter ska kunna registreras i Intune.

## <a name="keys-to-a-successful-migration"></a>Nycklar till en lyckad migrering

Punkterna nedan hjälper dig att säkerställa en lyckad migrering från en tredje parts MDM-provider till Intune:

- En tydlig och relevant kommunikation kan minimera driftstopp för och klagomål från slutanvändarna.

- Använd alltid specifika och konkreta migreringsinstruktioner.

- Alla hanterade enheter måste avregistreras från den befintliga MDM-providern innan de kan registreras i Intune.

- Ge slutanvändarna vägledning som beskriver hur de avregistrerar sina enheter från den befintliga MDM-providern.

- Använd en fasad metod. Börja med en liten grupp pilotanvändare och lägg stegvis till flera användargrupper tills du uppnår fullskalig distribution.

- Övervaka supportavdelningens belastning och hur registreringen fortskrider för varje cykel. Reservera tid i schemat så att du får tid att utvärdera framgångskriterierna för respektive grupp innan nästa migreras. Pilotdistributionen bör verifiera följande:

  - Graden av lyckade och misslyckade registreringar ligger inom det förväntade.

  - Användarproduktivitet:

    - Företagsresurser, som VPN, Wi-Fi, e-post och certifikat, fungerar.

    - Etablerade appar är tillgängliga.

  - Datasäkerhet:

    - Efterlevnadsrapporter genereras.

    - Mobilappsskydd tillämpas.

När du är nöjd med den första migreringsfasen upprepar du [migreringscykeln](migration-guide-cycle.md) för nästa fas.

- Upprepa de fasade cyklerna tills alla användare har migrerats till Intune.

- Se till att supportpersonalen finns till hands och kan hjälpa slutanvändarna under hela migreringskampanjen. Kör en frivillig migrering tills du kan beräkna arbetsbelastningen för supportsamtal.

- Sätt inga tidsgränser för registreringen förrän supportavdelningen har möjlighet att hantera all belastning

> [!IMPORTANT]
> Konfigurera inte både Intune och din befintliga MDM-lösning från tredje part när du vill tillämpa åtkomstkontroller på resurser som Exchange eller SharePoint Online. Dessutom bör enheterna bara vara registrerade i en lösning åt gången.

## <a name="next-steps"></a>Nästa steg

Skapa en [kommunikationsplan](migration-guide-communication-plan.md).
