---
title: Inställningar av begränsningar i Microsoft Intune-enheter för Windows Phone 8.1
titleSuffix: ''
description: Läs vilka Intune-inställningar du kan använda för att kontrollera enhetsinställningar och funktioner på enheter som kör Windows Phone 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a655ea2c3770e00ccc685cbe9d59f0fe7e49cd6
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146226"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Inställningar för enhetsbegränsningar för Windows Phone 8.1-enheter i Microsoft Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

I den här artikeln visas inställningarna av enhetsbegränsningar som du kan konfigurera för enheter som kör Windows Phone 8.1.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en Windows Phone 8.1-profil för enhetsbegränsningar](device-restrictions-configure.md).

## <a name="general"></a>Allmänt

- **Kamera**: **Blockera** förhindrar åtkomst till enhetens kamera. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

  Intune hanterar endast åtkomst till enhetens kamera. Intune har inte åtkomst till bilder eller videor.

- **Kopiera och klistra in**: **Blockera** gör att det inte går att kopiera och klistra in mellan appar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Flyttbara lagringsmedier**: **Blockera** förhindrar användning av externa lagringsenheter, till exempel SD-kort, på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Geoplats**: **Blockera** förhindrar aktivering av platstjänster på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Microsoft-konto**: **Blockera** hindrar användare från att associera ett Microsoft-konto med enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Skärmdump**: **Blockera** förhindrar skärmdumpar på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Sändning av diagnostikdata**: **Blockera** förhindrar att diagnostik och telemetridata för användning skickas till Microsoft. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Synkronisering av anpassade e-postkonton**: **Blockera** hindrar enheter från att ansluta till e-postkonton som inte kommer från Microsoft. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

## <a name="password"></a>lösenordsinställning

- **Lösenord**: **Kräv** tvingar användarna att ange lösenord för att få åtkomst till enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Gäller endast för lokala konton. Lösenord för domänkonton förblir konfigurerade av Active Directory (AD) och Azure AD.
  - **Lösenordstyp som krävs**: Välj typ av lösenord. Alternativen är:
    - **Standard för enheten**: Lösenordet kan innehålla siffror och bokstäver.
    - **Alfanumeriskt**: Lösenordet måste innehålla en blandning av siffror och bokstäver.
    - **Numeriskt**: Lösenordet får bara innehålla siffror.
  - **Minsta lösenordslängd**: Ange det minsta antal tecken som krävs (från 4 till 16). Ange till exempel `6` för att kräva minst sex tecken i lösenordet.
  - **Enkla lösenord**: **Blockera** hindrar användare från att skapa enkla lösenord, till exempel `1234` eller `1111`. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
  - **Antal felaktiga inloggningar innan enheten rensas**: Ange antal tillåtna felaktiga lösenord innan enheter rensas.
  - **Maximalt antal minuter av inaktivitet innan skärmen låses**: Anger hur lång tid en enhet måste vara inaktiv innan skärmen låses automatiskt. Ange till exempel `5` om du vill låsa enheter efter 5 minuters inaktivitet. När detta anges till **Inte konfigurerad** eller lämnas tomt, ändrar eller uppdaterar Intune inte den här inställningen.
  - **Lösenordets giltighetstid (dagar)** : Ange det antal dagar efter vilket enhetens lösenord måste ändras (från 1 till 255). Ange till exempel `90` om lösenordet ska upphöra efter 90 dagar. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
  - **Förhindra återanvändning av tidigare lösenord**: Ange antal tidigare använda lösenord som inte får återanvändas, från 1–24. Ange till exempel `5` om användare inte ska kunna ange ett nytt lösenord till sina nuvarande lösenord eller något av de föregående fyra lösenorden. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
- **Kryptering**: **Kräv** kryptering på enhet, inklusive filer. Alla enheter stöder inte kryptering. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du vill konfigurera den här inställningen, och rapportera efterlevnad på korrekt sätt, konfigurerar du även:
  - **Kräv lösenord**: Ange till **Kräv**.
  - **Lösenordstyp som krävs**: Ange till minst **Numeriskt**.
  - **Minsta lösenordslängd**: Ange till minst `4`.

## <a name="app-store"></a>Appbutik

- **App Store**: **Blockera** hindrar användare från att komma åt App Store. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

## <a name="restricted-apps"></a>Begränsade appar

Du kan konfigurera en av följande listor i listan med begränsade appar:

- **Blockerade appar**: Ange de appar (som inte hanteras av Intune) som användarna inte får installera och köra.
- **Tillåtna appar**: Ange de appar som användare tillåts att installera. Appar som hanteras av Intune tillåts automatiskt.

Konfigurera listan genom att klicka på **Lägg till**, ange ett namn, t.ex. appens utgivare samt webbadressen till appen i appbutiken.

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>Så här anger du webbadressen till appen i butiken

Om du vill ange en app-URL i listan över tillåtna och blockerade appar använder du följande format:

Gå till sidan [Windows Phone Store](https://www.microsoft.com/store/apps/windows-phone) och sök efter den app du vill använda.

Öppna appens sida och kopiera webbadressen till Urklipp. Nu kan du använda denna URL som URL i listan över tillåtna eller blockerade appar.

Exempel: Sök i butiken efter Skype-appen. Den URL som du använder är `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51`.

### <a name="additional-options"></a>Ytterligare alternativ

Du kan också klicka på **Importera** för att fylla i listan från en csv-fil i formatet <*app-url*>, <*appnamn*>, <*appens utgivare*>, eller klicka på **Exportera** för att skapa en csv-fil med innehållet i listan över begränsade appar i samma format.

## <a name="browser"></a>Webbläsare

- **Webbläsare**: **Blockera** inaktiverar den inbyggda webbläsaren på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

## <a name="cellular-and-connectivity"></a>Mobilnät och anslutning

- **Trådlöst**: **Blockera** inaktiverar Wi-Fi-funktioner på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Trådlös Internetdelning**: **Blockera** förhindrar delning av Wi-Fi på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Anslut automatiskt till trådlösa surfpunkter**: Gör att enheter ansluter automatiskt till kostnadsfria trådlösa surfzoner och att de automatiskt godkänner användningsvillkoren.
- **Rapportering om trådlös surfzon**: **Blockera** förhindrar att enheter skickar information om anslutningar för trådlösa surfzoner. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **NFC**: **Blockera** inaktiverar åtgärder som använder närfältskommunikation på de enheter som stöds. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Bluetooth**: **Blockera** hindrar användare från att aktivera Bluetooth. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

## <a name="next-steps"></a>Nästa steg

En allmän översikt över enhetsbegränsningsprofilen finns i [Konfigurera inställningar för enhetsbegränsningar i Microsoft Intune](device-restrictions-configure.md).
