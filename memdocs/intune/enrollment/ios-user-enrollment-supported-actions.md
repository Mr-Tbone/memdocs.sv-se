---
title: Intune-åtgärder och Intune-alternativ som stöds med Apples användarregistrering
titleSuffix: Microsoft Intune
description: Lär dig vilka Intune-åtgärder och Intune-alternativ som stöds med Apples användarregistrering
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 2/14/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: aa78178f6649e0199aa2de96bac2725ba55208ae
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79359267"
---
# <a name="intune-actions-and-options-supported-with-apple-user-enrollment"></a>Intune-åtgärder och Intune-alternativ som stöds med Apples användarregistrering

Användarregistrering har stöd för en deluppsättning av enhetshanteringsalternativen. Om en redan befintlig konfigurationsprofil tillämpas på en enhet som registreras via Användarregistrering, tillämpas bara de inställningar som stöds av Användarregistrering på enheten.

> [!NOTE]
> Stöd för Apples användarregistrering i Intune är för närvarande tillgängligt som en förhandsversion för iOS och iPadOS.

## <a name="password-settings"></a>Inställningar för lösenord

Om du konfigurerar en lösenordsinställning på en enhet som registreras via Användarregisterring används automatiskt inställningen **Blockera** för **Enkla lösenord**, och en 6-siffrig PIN-kod krävs.

Du kan till exempel konfigurera inställningen **Lösenordets giltighetstid** och skicka den här principen till användarregistrerade enheter. Följande händer på enheterna:
- Inställningen **Lösenordets giltighetstid** ignoreras.
- Enkla lösenord, till exempel `111111` eller `123456`, tillåts inte.
- En 6-siffrig PIN-kod krävs.

## <a name="administrator-remote-device-actions-and-options"></a>Administratörsåtgärder på fjärrenheter
Administratörer kan utföra följande åtgärder på enheter som registrerats via Användarregistrering:
- Pensionera
- Ta bort
- Fjärrlåsning
- Synkronisera

Inga andra åtgärder stöds.

## <a name="end-user-actions"></a>Användaråtgärder
Slutanvändarna kan utföra följande åtgärder på enheter som registrerats via Användarregistrering från appen eller webbplatsen för företagsportalen:
- Byta namn. Den här åtgärden gäller endast namnet på företagsportalen. Namnet ändras inte utanför portalen.
- Ta bort
- Fjärrlåsning
- Kontrollera status

## <a name="app-deployment-options"></a>Appdistributionsalternativ
Du kan distribuera följande apptyper på användarregistreringsenheter:
- Användarlicensierade VPP-appar (Volume Purchasing Plan) inklusive anpassade appar
- Verksamhetsspecifika appar
- Webbappar

## <a name="other-supported-options"></a>Andra alternativ som stöds

Följande alternativ stöds i Intune för enheter som har registrerats via Apples användarregistrering:
- Per app-VPN. Det här alternativet gäller inte Safari-domäner eftersom det inte går att konfigurera Safari-inställningar i Användarregistrering.
- WiFi 
- Borttagning av företagsappar vid avregistrering
- Upplåsningsidentifiering

Följande begränsningar stöds:
- Visa företagsdokument i ohanterade appar
- Visa dokument som inte gäller företag i företagsappar
- Tillåt ohanterade appar att läsa från hanterade kontaktkonton
- Behandla AirDrop som ohanterat mål
- Obligatorisk krypterad säkerhetskopiering
- Synkronisering av hanterade appar till molnet
- Åtkomst till Kontrollcenter när enheten är låst
- Åtkomst till Meddelandecenter när enheten är låst
- Dagsvyn när enheten är låst
- Blockera skärmbilder
- Blockera säkerhetskopiering av företagsbok
- Blockera synkronisering av metadata för företagsbok
- Kräv krypterad säkerhetskopiering
- Kräv handledsavkänning för klockor
- Blockera Siri
- Tillåt Siri när enheten är lås
- Kräv bedrägerivarningar från Safari
- Tillåt inte att diagnostik skickas till Apple


## <a name="options-not-supported"></a>Alternativ som inte stöds
Följande alternativ stöds inte på enheter som har registrerats via Användarregistrering. Om du behöver använda dessa alternativ kan du använda Enhetsregistrering för privatägda enheter eller Automatisk enhetsregistrering för företagsenheter.
- Samla in appinventering för appar utanför den hanterade APFS-volymen.
- Samla in inventering av certifikat och etableringsprofiler utanför den hanterade APFS-volymen.
- Samla in UDID och andra permanenta enhetsidentifierare.
- Användarregistrering stöder unika registrerings-ID:n för registrerade enheter. Dessa ID:n bevaras dock inte efter en avregistrering.
- Följande Intune-funktioner stöds inte på grund av den här begränsningen:
- SCEP-användarprofiler som använder serienummer som format för mottagarnamn.
- VPN på enhetsnivå.
- Enhetslicensierad VPP-appdistribution.
- Installera App Store-appar som hanterade appar.
- MDM-kontroll av program utanför den hanterade APFS-volymen.
- Programskyddsprinciper används fortfarande för dessa appar. Men du kan inte ta över hanteringen eller distribuera en hanterad version av dessa appar om inte användaren tar bort dem från enheten.
- Åtgärder, konfigurationer, inställningar och kommandon som kräver övervakning. 


## <a name="known-issues-in-preview"></a>Kända problem i förhandsversionen
- VPP-licensåterkallelse: Ett meddelande om att licensen har återkallats visas inte. Det aktuella beteendet är att återkallningen lyckas, men slutanvändaren får inget meddelande om det. 
- VPP-programrapportering: I rapporten som finns i Klientappar > Appar > [appnamn] > Installationsstatus för enhet rapporteras att VPP-program som distribuerats till användarregistrerade enheter "misslyckats", även om programmet har distribuerats utan problem till enheten. 
- Programrapportering: För de apptyper som inte stöds för användarregistrering kan rapporter innehålla irrelevanta felmeddelanden. 
- Gränssnittet för företagsportalappen: Användarna ser alla program som är riktade mot dem, oavsett om dessa programtyper stöds för användarregistrerade enheter eller inte. 
- Gränssnittet för företagsportalappen: Användarna ser samma text, vilken indikerar vad organisationer kan se avseende användar- och enhetsregistrering om administratören har anpassat texten så att den indikerar vad organisationerna inte kan se.


## <a name="next-steps"></a>Nästa steg

[Konfigurera användarregistrering för iOS/iPadOS och iPadOS](ios-user-enrollment.md)
