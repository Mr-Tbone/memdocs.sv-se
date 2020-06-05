---
title: Förbereda appar för hantering av mobilprogram med Microsoft Intune
description: Informationen i det här avsnittet hjälper dig att avgöra när du ska använda apphanteringsverktyget och App SDK för att förbereda dina verksamhetsspecifika appar för användning av hanteringsprinciper för mobilappar.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/27/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 29e22121-8268-48b5-a671-f940a6be1d24
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 739ebebe18628279e5242ab227cf0f43993eff08
ms.sourcegitcommit: 42a4a4454e56fa681f0ad39f5e585492dfbad286
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330873"
---
# <a name="prepare-line-of-business-apps-for-app-protection-policies"></a>Förbered branschspecifika appar för appskyddsprinciper

Du kan använda appskyddsprinciper i dina appar med hjälp av Intunes apphanteringsverktyg eller Intune App SDK. Det här avsnittet innehåller information om dessa metoder och när du ska använda dem.

## <a name="intune-app-wrapping-tool"></a>Intunes apphanteringsverktyg

Apphanteringsverktyget används främst för **interna** affärsappar. Verktyget är ett kommandoradsprogram som skapar en omslutning runt en app, som sedan gör att appen kan hanteras av en Intune-appskyddsprincip. När du skyddar en app som tillhandahålls av en oberoende programvaruleverantör (ISV) är det viktigt att klargöra om ISV:n fortfarande kommer att stödja den omslutna appen.

Du behöver inte källkoden för att använda verktyget, men du behöver autentiseringsuppgifter för signering. Mer information om autentiseringsuppgifter för signering finns i [Intune-bloggen](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/25/how-to-obtain-the-prerequisites-for-the-intune-app-wrapping-tool-for-ios/). Dokumentation om appomslutningsverktyget finns i [Appomslutningsverktyget för Android](app-wrapper-prepare-android.md) respektive [Appomslutningsverktyget för iOS](app-wrapper-prepare-ios.md).

Apphanteringsverktyget stöder **inte** appar i Apple App Store eller Google Play Store. Det stöder inte heller vissa funktioner som kräver utvecklarintegration (se följande tabell med funktionsjämförelser).

Mer information om programhanteringsverktyget för appskyddsprinciper på enheter som inte har registrerats i Intune finns i [Skydda branschspecifika appar och data på enheter som inte har registrerats i Microsoft Intune](../apps/apps-add.md).

### <a name="reasons-to-use-the-app-wrapping-tool"></a>Skäl för att använda programhanteringsverktyget

* Din app har inte några inbyggda dataskyddsfunktioner
* Din app distribueras internt
* Du har inte tillgång till appens källkod
* Du har inte utvecklat appen
* Din app har minimala användarautentiseringsfunktioner

### <a name="supported-app-development-platforms"></a>Utvecklingsplattformar för program som stöds

|**Apphanteringsverktyg** | **Xamarin** |**Cordova** |
|------|----|----|
|**iOS** |Ja|Ja|
|**Android**|Nej – använd [Xamarin-bindningar för Intune App SDK](app-sdk-xamarin.md).|Ja|

## <a name="intune-app-sdk"></a>Intune App SDK

App SDK är främst utformat för kunder som har appar i Apple App Store eller Google Play Store och som vill kunna hantera appar med Intune. Alla appar kan dock dra nytta av integrera SDK, även branschspecifika appar.

Mer information om SDK:n finns i [Översikt](app-sdk.md). Om du vill börja använda SDK:n läser du [Komma igång med Microsoft Intune App SDK](app-sdk-get-started.md).

### <a name="reasons-to-use-the-sdk"></a>Skäl för att använda SDK

* Din app har inte några inbyggda dataskyddsfunktioner
* Din app har distribuerats via en offentlig appbutik som Google Play eller Apple App Store
* Du är en apputvecklare och har de tekniska förutsättningarna att kunna använda SDK:n
* Din app har andra SDK-integrationer
* Din app uppdateras ofta

### <a name="supported-app-development-platforms"></a>Utvecklingsplattformar för program som stöds

|**Intune App SDK** |**Xamarin** |**Cordova**
|------|----|----|
|**iOS**|Ja – Använd [Xamarin-bindningar för Intune App SDK](app-sdk-xamarin.md).|Nej|
|**Android**| Ja – Använd [Xamarin-bindningar för Intune App SDK](app-sdk-xamarin.md).|Nej|

## <a name="not-using-an-app-development-platform-listed-above"></a>Använder du inte någon av de plattformar för programutveckling som anges ovan?

Intune SDK-utvecklingsteamet testar och underhåller aktivt stödet för appar som skapats med de ursprungliga Android-, iOS (Obj-C, Swift), Xamarin- och Xamarin.Forms-plattformarna. Även om vissa kunder har lyckats integrera Intune SDK med andra plattformar som React Native och NativeScript, tillhandahåller vi inte någon uttrycklig vägledning eller några plugin-program för apputvecklare som använder något annat än våra stödda plattformar. 

## <a name="feature-comparison"></a>Jämförelse av funktioner

Den här tabellen visar de inställningar som aktiveras om en app använder app-SDK eller App Wrapping Tool. Vissa funktioner kräver att apputvecklare använder en del logik utanför den grundläggande integreringen med Intune SDK, och därför är de inte aktiverade om appen använder App Wrapping Tool. 

|Funktion|App SDK|Apphanteringsverktyg|
|-----------|---------------------|-----------|
|Begränsa webbinnehåll till att bara visas i en företagshanterad webbläsare|X|X|
|Förhindra Android-, iTunes- och iCloud-säkerhetskopieringar|X|X|
|Tillåt att appen överför information till andra appar|X|X|
|Tillåt att appen hämtar data från andra appar|X|X|
|Begränsa klipp ut, kopiera och klistra in med andra appar|X|X|
|Ange hur många tecken som kan klippas ut eller kopieras från en hanterad app|X|X|
|Kräv enkel PIN-kod för åtkomst|X|X|
|Ange antal försök innan PIN-koden återställs|X|X|
|Tillåt fingeravtryck istället för PIN|X|X|
|Tillåt ansiktsigenkänning istället för PIN-kod (endast iOS)|X|X|
|Kräv företagets autentiseringsuppgifter för åtkomst|X|X|
|Ange ett förfallodatum för PIN-kod|X|X|
|Hindra hanterade appar från att köras på jailbrokade eller rotade enheter|X|X|
|Kryptera appdata|X|X|
|Kontrollera åtkomstbehörigheterna på nytt efter angivet antal minuter|X|X|
|Ange offlinerespitperiod|X|X|
|Blockera skärmdump (endast Android)|X|X|
|Stöd för MAM utan enhetsregistrering|X|X|
|Fullständig rensning av appdata|X|X|
|Selektiv rensning av arbets- och skoldata i scenarier med flera identiteter <br><br>**Obs:** När hanteringsprofilen tas bort i iOS/iPadOS tas även appen bort.|X||
|Förhindra ”Spara som”|X||
|Riktad programkonfiguration (eller appkonfiguration via MAM-kanal)|X|X|
|Stöd för flera identiteter|X||
|Anpassningsbar stil |X|||
|VPN-anslutningar för program på begäran med Citrix mVPN|X|X| 
|Inaktivera synkronisering av kontakter|X|X|
|Inaktivera utskrift|X|X|
|Minimikrav på appversion|X|X|
|Minimikrav på operativsystem|X|X|
|Minimikrav på Android-säkerhetskorrigeringsversion (endast Android)|X|X|
|Minimikrav på Intune SDK för iOS (endast iOS)|X|X|
|SafetyNet-enhetsattestering (endast Android)|X|X|
|Hotgenomsökning för appar (endast Android)|X|X|
|Kräv maximalt skydd mot mobilhot som risknivå för leverantörsenheter|X||
|Konfigurera innehåll i appmeddelande för organisationskonton|X|X|
|Kräv användning av godkända tangentbord (endast Android)|X|X|
|Kräv appskyddsprincip (villkorlig åtkomst)|X||

## <a name="next-steps"></a>Nästa steg

Mer information om appskyddsprinciper i Intune finns i följande avsnitt:

- [Apphanteringsverktyg för Android](app-wrapper-prepare-android.md)<br>
- [Apphanteringsverktyg för iOS](app-wrapper-prepare-ios.md)<br>
- [Aktivera hantering av mobilprogram i appar med SDK](app-sdk.md)
