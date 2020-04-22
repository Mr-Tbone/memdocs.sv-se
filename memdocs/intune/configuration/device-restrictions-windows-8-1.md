---
title: Inställningar för begränsningar för Windows 8.1-enheter i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Läs vilka Intune-inställningar du kan använda för att kontrollera enhetsinställningar och funktioner på enheter som kör Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59af48b36cb9c76ce7587457d4921356f542493f
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80407668"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Inställningar för begränsningar för Windows 8.1-enheter i Microsoft Intune

I den här artikeln visas inställningarna av enhetsbegränsningar som du kan konfigurera för enheter som kör Windows 8.1.

## <a name="general"></a>Allmänt

- **Dela användningsdata**: **Blockera** hindrar enheter från att skicka telemetriinformation om diagnostik och användning till Microsoft. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Brandvägg**: **Kräv** att Windows-brandväggen är aktiverad. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **User Account Control**: Konfigurerar User Account Control (UAC). Välj hur användare ska meddelas om ändringar på enheter. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Meddela alltid**
  - **Meddela vid appändringar**
  - **Meddela om appändringar (men tona inte ned skrivbordet)**
  - **Meddela aldrig**

## <a name="password"></a>lösenordsinställning

- **Lösenordstyp som krävs**: Välj om användarna måste ange ett lösenord för att få åtkomst till enheten. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Alfanumeriskt**: Lösenordet måste innehålla en blandning av siffror och bokstäver.
  - **Numeriskt**: Lösenordet får bara innehålla siffror.
- **Minsta lösenordslängd**: Ange det minsta antal tecken som krävs (från 6 till 16). Ange till exempel `6` för att kräva minst sex siffror eller tecken i lösenordet.
- **Antal felaktiga inloggningar innan enheten rensas**: Ange antal tillåtna felinloggningar innan enheten rensas (från 1 till 14).
- **Maximalt antal minuter av inaktivitet innan skärmen låses (i minuter)** : Anger hur lång tid enheten måste vara inaktiv innan skärmen låses automatiskt (från 1 till 60 minuter). Ange till exempel `5` om du vill låsa enheter efter 5 minuters inaktivitet. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen.
- **Lösenordets giltighetstid (dagar)** : Ange det antal dagar efter vilket enhetens lösenord måste ändras (från 1 till 255). Ange till exempel `90` om lösenordet ska upphöra efter 90 dagar. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
- **Förhindra återanvändning av tidigare lösenord**: Ange antal tidigare använda lösenord som inte får återanvändas, från 1–24. Ange till exempel `5` om användare inte ska kunna ange ett nytt lösenord till sina nuvarande lösenord eller något av de föregående fyra lösenorden. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
- **Bildlösenord och PIN-kod**: **Blockera** förhindrar användning av en bild eller PIN-kod som lösenord. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Med ett bildlösenord kan användaren logga in med gester på en bild. Med en PIN-kod kan användaren snabbt logga in med en fyrsiffrig kod.
- **Kryptering**: **Kräv kryptering** på enhet, inklusive filer. Alla enheter stöder inte kryptering. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen.

  Om du vill konfigurera den här inställningen, och rapportera efterlevnad på korrekt sätt, konfigurerar du även:
  - **Lösenordstyp som krävs**: Ange till minst **Numeriskt**.
  - **Minsta lösenordslängd**: Ange till minst `4`.

  Om du vill framtvinga kryptering på enheter som kör Windows 8.1 måste du installera [December 2014 MDM-klientuppdateringen för Windows](https://support.microsoft.com/kb/3013816) på varje enhet.

  Om du aktiverar den här inställningen för Windows 8.1-enheter måste alla användare av sådana enheter ha ett Microsoft-konto.

  För att krypteringen ska fungera måste enheterna uppfylla kraven för [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97)-maskinvarucertifiering.

  När du framtvingar kryptering på en enhet är återställningsnyckeln enbart tillgänglig från användarens Microsoft-konto, som nås från användarens OneDrive-konto. Du kan inte återställa den här nyckeln för en användare.

## <a name="browser"></a>Webbläsare

- **Autofyll**: **Blockera** hindrar användare från att ändra inställningarna för automatisk komplettering i webbläsaren och från att använda automatisk ifyllning av formulärfält. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta autofyll.
- **Bedrägerivarningar**: **Kräv** visar varningar i webbläsaren om potentiellt bedrägliga webbplatser. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **SmartScreen för Microsoft Edge**: **Blockera** inaktiverar Microsoft Defender SmartScreen. SmartScreen letar efter potentiella nätfiskebedrägerier och skadlig programvara vid åtkomst till webbplatser och nedladdning av filer. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard aktivera SmartScreen.
- **JavaScript**: **Blockera** hindrar skript (till exempel JavaScript) från att köras i webbläsaren. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Popup-fönster**: **Blockera** aktiverar blockering av popup-fönster i webbläsaren. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Do Not Track-huvuden**: **Blockera** hindrar enheter från att skicka Do Not Track-huvuden till webbplatser som kräver spårningsinfo. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Plugin-program**: **Blockera** hindrar användare från att lägga till plugin-program i Internet Explorer. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Enstaka ord på intranätsplats**: Enstaka ord låter användare gå till en intranätsplats genom att ange ett enskilt ord, till exempel `hr` eller `benefits`. **Blockera** förhindrar den här funktionen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Automatisk identifiering av intranätsplats**: **Blockera** hindrar webbläsaren från att automatiskt identifiera intranätsplatser. Regler för intranätsmappning blockeras. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Internetsäkerhetsnivå**: Anger säkerhetsnivå för webbplatser på Internet. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Medel**
  - **Medelhög**
  - **Hög**
- **Intranätssäkerhetsnivå**: Anger säkerhetsnivå för intranätplatser. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Låg**
  - **Medellåg**
  - **Medel**
  - **Medelhög**
  - **Hög**
- **Säkerhetsnivå för tillförlitliga platser**: Konfigurerar säkerhetsnivån för zonen Betrodda platser. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Låg**
  - **Medellåg**
  - **Medel**
  - **Medelhög**
  - **Hög**
- **Hög säkerhet för ej tillförlitliga platser**: Konfigurerar säkerhetsnivån för zonen Ej betrodda platser. **Konfigurerad** inför hög säkerhet för ej tillförlitliga platser. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Menyåtkomst till företagsläge**: **Blockera** hindrar användare från att komma åt menyalternativen för företagsläge från Internet Explorer. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. När detta anges till **Blockera** anger du även:
  - **Loggningsrapportplats (URL)** : Ange en URL-plats för hämtning av rapporter som visar vilka webbplatser som har aktiverad företagslägesåtkomst.
- **Plats för webbplatslista för företagsläge (endast stationär dator)** : Ange platsen för listan över webbplatser som kan öppnas i företagsläge.

## <a name="cellular"></a>Mobilnät

- **Datanätverksväxling**: **Blockera** förhindrar dataroaming när enheter är i ett mobilnät. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

## <a name="cloud-and-storage"></a>Moln och lagring

- **URL till arbetsmappar**: Anger arbetsmappens URL så att dokument kan synkroniseras mellan enheter. När detta anges till **Inte konfigurerad** (standard) eller lämnas tomt, ändrar eller uppdaterar Intune inte den här inställningen.
- **Åtkomst till Windows Mail-app utan Microsoft-konto**: **Blockera** förhindrar åtkomst till Windows Mail utan ett Microsoft-konto. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

## <a name="next-steps"></a>Nästa steg

Skapa en profil för enhetsbegränsningar på [Windows 10 och senare](device-restrictions-windows-10.md).
