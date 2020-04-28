---
title: Använda Intune i miljöer utan Google Mobile Services
titleSuffix: Microsoft Intune
description: Lär dig hur du använder Intune i miljöer utan Google Mobile Services.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5aa91a84b2fe5d8870afc93022ab5a468b30e0db
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074800"
---
# <a name="how-to-use-intune-in-environments-without-google-mobile-services"></a>Använda Intune i miljöer utan Google Mobile Services

Microsoft Intune använder Google Mobile Services (GMS) för att kommunicera med Microsofts Intune-företagsportalapp vid hantering av Android-enheter. I vissa fall kan enheterna tillfälligt eller permanent sakna åtkomst till GMS. En enhet kan till exempel levereras utan GMS, eller så kanske enheten ansluter till ett stängt nätverk där GMS inte är tillgängligt. Det här dokumentet sammanfattar de skillnader och begränsningar som du kan observera när du installerar och använder Intune för att hantera Android-enheter utan GMS.

## <a name="install-the-intune-company-portal-app-without-access-to-the-google-play-store"></a>Installera Intune-företagsportalappen utan åtkomst till Google Play Butik 

### <a name="for-users-outside-of-mainland-china"></a>För användare utanför kinesiska fastlandet 

Om Google Play inte är tillgängligt kan Android-enheter ladda ned [Microsofts Intune-företagsportalapp för Android](https://www.microsoft.com/en-us/download/details.aspx?id=49140) och läsa in appen separat. När appen installeras på det här sättet får appen inte uppdateringar eller korrigeringar automatiskt. Du måste vara noga med att regelbundet uppdatera och förse appen med korrigeringar. 

### <a name="for-users-in-mainland-china"></a>För användare på kinesiska fastlandet 

Eftersom Google Play Butik för närvarande inte finns på kinesiska fastlandet, måste Android-enheter hämta appar från kinesiska appmarknadsplatser. Mer information finns i [Installera företagsportalappen på kinesiska fastlandet](../user-help/install-company-portal-android-china.md).

## <a name="limitations-of-intune-device-administrator-management-when-gms-is-unavailable"></a>Begränsningar för administratörshanteringen av Intune-enheter när GMS inte är tillgängligt 

### <a name="unavailable-intune-features"></a>Otillgängliga Intune-funktioner

Vissa Intune-funktioner förlitar sig på komponenter i GMS som Google Play Butik eller Google Play-tjänsterna. Eftersom dessa komponenter inte är tillgängliga i miljöer utan GMS, kan följande funktioner i Intunes administratörskonsol vara otillgängliga.  

| Scenario  | Funktioner  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Efterlevnadsprinciper för enheter  | När du skapar eller redigerar efterlevnadsprinciper för Android-enhetsadministratörer är alla alternativ under **Google Play Protect** otillgängliga.  |
| Appskyddsprinciper (villkorlig start)  | Enhetstillstånden **SafetyNet-enhetsattestering** och **Kräv hotgenomsökning för appar** kan inte användas för villkorlig start.  |
| Klientappar  | Appar av **Android**-typ är inte tillgängliga. Använd **verksamhetsspecifika appar** i stället för att distribuera och hantera appar.  |
| Mobile Threat Defense  | Arbeta med din MTD-leverantör och ta reda på om deras lösning är integrerad med Intune, om den är tillgänglig i intresseregionen och om den förlitar sig på GMS.  |

### <a name="some-tasks-may-be-delayed"></a>Vissa uppgifter kan vara fördröjda 

I miljöer där GMS är tillgängligt är Intune beroende av push-meddelanden för att se till att uppgifter slutförs snabbare. Om du t.ex. försöker rensa enheten, så skickas meddelanden vanligtvis till enheten på bara några sekunder. Under förhållanden där GMS inte är tillgängligt, kan det också vara så att push-meddelanden inte heller är tillgängliga. Därför måste Intune vänta till enhetens nästa incheckningstid för att slutföra uppgifterna.  

Registrerade Android-enheter rapporterar till Intune var åttonde timme. Om till exempel en enhet rapporterar till Intune kl. 13.00 och fjärruppgifterna utfärdas kl. 13.05, kommer Intune att kontakta enheten kl. 21.00 för att slutföra uppgifterna. 

Följande aktiviteter kan kräva upp till åtta timmar för att slutföras: 

**Intune-konsolen**:
- Fullständig rensning
- Selektiv rensning
- Nya eller uppdaterade appdistributioner
- Fjärrlåsning
- Återställning av lösenord

**Intune-företagsportalsappen för Android**:
- Enhetsborttagning på distans
- Återställning av enhet
- Installation av tillgängliga verksamhetsspecifika appar

**Intune-företagsportalens webbplats**:
- Enhetsborttagning (lokal och på distans)
- Återställning av enhet
- Återställning av enhetens lösenord

Om enheten nyligen har registrerats sker efterlevnads-, icke-efterlevnads- och konfigurationsincheckningarna oftare. Mer information om enhetsincheckningar finns i [Vanliga frågor, problem och lösningar med enhetsprinciper och profiler i Microsoft Intune](../configuration/device-profile-troubleshoot.md). 

## <a name="next-steps"></a>Nästa steg

- [Tilldela appar till grupper med Microsoft Intune](../apps/apps-deploy.md)
