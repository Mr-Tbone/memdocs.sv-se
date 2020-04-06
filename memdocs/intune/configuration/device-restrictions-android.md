---
title: Enhetsbegränsningsinställningar för Android i Microsoft Intune – Azure | Microsoft Docs
description: Se en lista över alla Android-enhetsadministratörsinställningar du kan kontrollera och begränsa i Microsoft Intune. Använd dessa inställningar för att styra lösenordet, komma åt Google Play-butiken, tillåta eller förbjuda appar, styra webbläsarinställningarna, blockera appar, säkerhetskopiera till Google Cloud och styra alternativen för meddelanden, röst, datanätverksväxling, Wi-Fi och Bluetooth-anslutning.
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
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4afc27680c464f67756340ebcb0958887ae6f795
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407876"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Inställningar av begränsningar för Android- och Samsung Knox Standard-enheter i Intune

I den här artikeln visas alla inställningar av enhetsbegränsningar som du kan konfigurera för enheter som kör Android.

>[!TIP]
>Om de önskade inställningarna inte är tillgängliga så kan du konfigurera dina enheter med hjälp av en [anpassad profil](custom-settings-android.md).

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en enhetskonfigurationsprofil](device-restrictions-configure.md).

## <a name="general"></a>Allmänt

- **Kamera**: **Blockera** förhindrar åtkomst till enhetens kamera. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta åtkomst till enhetens kamera.

  Intune hanterar endast åtkomst till enhetens kamera. Intune har inte åtkomst till bilder eller videor.

- **Kopiera och klistra in (endast Samsung Knox)** : **Blockera** förhindrar kopiering och inklistring. **Inte konfigurerad** tillåter användning av funktioner för att kopiera och klistra in på enheter.
- **Urklippsdelning mellan appar (endast Samsung Knox)** : **Blockera** förhindrar att urklipp används för att kopiera och klistra in mellan appar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta funktioner för att kopiera och klistra in på enheter.
- **Sändning av diagnostikdata (endast Samsung Knox)** : **Blockera** hindrar användare från att skicka felrapporter från enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användare skickar dessa data.
- **Rensning (endast Samsung Knox)** : Tillåter användare att kör en [rensningsåtgärd](../remote-actions/devices-wipe.md) på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Geoplats (endast Samsung Knox)** : **Blockera** hindrar enheter från att använda platsinformation. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att enheter använder platsinformation.
- **Stäng av (endast Samsung Knox)** : **Blockera** hindrar användare från att stänga av enheten. Det gör också att inställningen **Antal felaktiga inloggningar innan enheten rensas** inte kan konfigureras, och inte fungerar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att stänger av enheter.
- **Skärmbild (endast Samsung Knox)** : **Blockera** förhindrar skärmbilder. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användaren sparar skärminnehåll som en bild.
- **Röstassistent (endast Samsung Knox)** : **Blockera** inaktiverar tjänsten S Voice. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att tjänsten och appen S Voice används på enheter. Inställningen gäller inte för Bixby eller röstassistenten för hjälpmedel som läser upp skärmens innehåll.
- **YouTube (endast Samsung Knox)** : **Blockera** hindrar användare från att använda YouTube-appen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att YouTube-appen används på enheter.
- **Delade enheter (endast Samsung Knox)** : Konfigurera en hanterad Samsung Knox Standard-enhet som delad. **Tillåt** låter användare logga in och ut från enheter med sina Azure AD-autentiseringsuppgifter. Enheterna förblir hanterade, oavsett om de används eller inte.

  När detta används med en SCEP-certifikatprofil gör den här funktionen det möjligt för användare att dela en enhet med samma appar för alla användare. Men varje användare har sina egna SCEP-användarcertifikat. Alla appdata rensas när användaren loggar ut. Den här funktionen är begränsad till endast LOB-appar.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra att flera användare loggar in på företagsportalappen på enheter med sina Azure AD-autentiseringsuppgifter.
- **Blockera ändringar av datum och tid (endast Samsung Knox)** : **Blockera** hindrar användare från att ändra inställningar för datum och tid på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ändra inställningar för datum och tid.

## <a name="password"></a>lösenordsinställning

- **Lösenord**: **Kräv** att användarna anger sina lösenord för att få åtkomst till enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan tillåta användarna få åtkomst till enheterna utan att behöva ange något lösenord.

    > [!NOTE]
    > Samsung Knox-enheter kräver automatiskt en fyrsiffrig PIN-kod under MDM-registreringen. Android-enheter kan automatiskt kräva att en PIN-kod är kompatibel med villkorsstyrd åtkomst.

- **Minsta lösenordslängd**: Ange det minsta antal tecken som krävs (från 4 till 16). Ange till exempel `6` för att kräva minst sex siffror eller tecken i lösenordet.
- **Maximalt antal minuter av inaktivitet innan skärmen låses**: Anger hur lång tid en enhet måste vara inaktiv innan skärmen låses automatiskt. Ange till exempel `5` om du vill låsa enheter efter 5 minuters inaktivitet. Om värdet är tomt eller inställt på **Inte konfigurerad**, ändrar eller uppdaterar Intune inte inställningen.

  Användare kan inte ange ett tidsvärde på en enhet som är större än den konfigurerade tiden i profilen. Användare kan dock ange ett lägre värde. Om profilen t.ex. är inställd på `15` minuter, kan användare ange värdet till 5 minuter. Användare kan inte ange värdet till 30 minuter.

- **Antal felaktiga inloggningar innan enheten rensas**: Ange antal tillåtna felaktiga lösenord innan enheter rensas (från 4 till 11). `0` (noll) kan inaktivera funktionen för rensning av enheten. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
- **Lösenordets giltighetstid (dagar)** : Ange antalet dagar innan enhetslösenordet måste ändras (från 1 till 365 dagar). Ange till exempel `90` om lösenordet ska upphöra efter 90 dagar. När lösenordet upphör att gälla uppmanas användarna att skapa ett nytt lösenord. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
- **Lösenordstyp som krävs**: Anger den komplexitetsnivå som krävs för lösenordet och om biometriska enheter kan användas. Alternativen är:
  - **Standard för enheten**
  - **Låg säkerhetsbiometri**: [Stark eller svag biometri](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (öppnar Androids webbplats)
  - **Minst numeriskt**: Innehåller numeriska tecken, till exempel `123456789`.
  - **Numeriskt avancerat**: Upprepade eller efterföljande siffror, till exempel ”1111” eller ”1234”, tillåts inte. Innan du tilldelar den här inställningen till enheter ska du se till att företagsportalappen har uppdaterats till den senaste versionen på målenheterna.

    När du anger **numeriskt avancerat** och tilldelar inställningen till enheter som kör en tidigare Android-version än 5.0 gäller följande:

    - Om företagsportalappen kör en tidigare version än 1704 kommer ingen PIN-princip att tillämpas på enheterna och ett fel visas i Microsoft Endpoint Manager admin center.
    - Om företagsportalappen kör version 1704 eller senare, kan bara en enkel PIN-kod användas. Tidigare Android-versioner än 5.0 har inte stöd för den här inställningen. Inget fel visas i administrationscentret för Microsoft Endpoint Manager.

  - **Minst alfabetiskt**: Innehåller bokstäver i alfabetet. Siffror och symboler krävs inte.
  - **Minst alfanumeriskt**: Innehåller versaler, gemener och numeriska tecken.
  - **Minst alfanumeriskt med symboler**: Innehåller versaler, gemener, numeriska tecken, skiljetecken och symboler.

- **Förhindra återanvändning av tidigare lösenord**: Använd den här inställningen för att förhindra att användare återanvänder tidigare använda lösenord. Ange antal tidigare använda lösenord som inte får återanvändas, från 1–24. Ange till exempel `5` om användare inte ska kunna ange ett nytt lösenord till sina nuvarande lösenord eller något av de föregående fyra lösenorden. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
- **Upplåsning med fingeravtryck (endast Samsung Knox)** : **Blockera** förhindrar att fingeravtryck används för att låsa upp enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användare att låsa upp enheter med hjälp av fingeravtryck.
- **Smart Lock och andra betrodda agenter**: **Blockera** hindrar Smart Lock och andra betrodda agenter från att ändra låsskärmsinställningar. Med den här funktionen, även kallad förtroendeagent, kan du inaktivera eller kringgå lösenordet för enhetens låsskärm om enheten finns på en betrodd plats. Funktionen kan till exempel användas när enheter är anslutna till en specifik Bluetooth-enhet eller när de är nära en NFC-tagg. Du kan använda den här inställningen för att förhindra att användare konfigurerar Smart Lock.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

  Den här inställningen gäller för:

  - Samsung KNOX Standard 5.0+

- **Kryptering**: Välj **Krävs** så att filer på enheten krypteras. Alla enheter stöder inte kryptering. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du vill konfigurera den här inställningen, och rapportera efterlevnad på korrekt sätt, konfigurerar du även:
  1. **Lösenord**: Ange till **Kräv**.
  2. **Lösenordstyp som krävs**: Ange till **Minst numeriskt**.
  3. **Minsta lösenordslängd**: Ange till minst `4`.

  > [!NOTE]
  > Om en krypteringsprincip tillämpas kräver Samsung Knox-enheter att användarna anger ett komplext sex tecken långt lösenord för enheten.

## <a name="google-play-store"></a>Google Play Store

- **Google Play Butik (endast Samsung Knox)** : **Blockera** hindrar användare från att använda appen Google Play Butik. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna kommer åt Google Play Butik på enheter.

## <a name="restricted-apps"></a>Begränsade appar

Använd inställningarna för att tillåta eller förhindra specifika appar på enheter. Funktionen stöds på Android- och Samsung Knox Standard-enheter.

- **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
- **Otillåtna appar**: Ange de appar (som inte hanteras av Intune) som användarna inte får installera eller köra. Om en användare installerar en app från den här listan kommer Intune att meddela dig.
- **Godkända appar**: Ange de appar som användare tillåts att installera. Om användarna vill fortsätta följa standard får de inte installera andra appar.  Appar som hanteras av Intune tillåts automatiskt. Det gäller även företagsportalsappen.
- **Applista**: **Lägg till** din app:
  - **Appsamlings-ID**: Ange appsamlings-ID:t.
  - **Webbadress till App Store**: Ange webbadressen till den app du vill ha i Google Play Butik. Om du till exempel vill lägga till Microsoft Remote Desktop-appen för Android anger du `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`.

    Du hittar webbadressen till en app genom att öppna [Google Play Butik](https://play.google.com/store/apps) och söka efter appen. Du kan t.ex. söka efter `Microsoft Remote Desktop Play Store` eller `Microsoft Planner`. Välj appen och kopiera webbadressen.
  
  - **Appnamn**: Ange det namn du vill ha. Namnet visas för användarna.
  - **Utgivare** (valfritt): Ange namnet på appens utgivare, till exempel `Microsoft`.

Du kan också **importera** en CSV-fil med information om appen, inklusive webbadressen. Använd formatet <*app-URL*>, <*appnamn*>, <*appens utgivare*>. Eller, **Exportera** en befintlig lista som innehåller listan över begränsade appar i samma format.

> [!IMPORTANT]
> Enhetsprofiler som använder inställningar för begränsade appar måste tilldelas till användargrupper, inte enhetsgrupper.

## <a name="browser"></a>Webbläsare

- **Webbläsare (endast Samsung Knox)** : **Blockera** förhindrar att standardwebbläsaren används på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användning av enhetens standardwebbläsare.
- **Autofyll (endast Samsung Knox)** : **Blockera** hindrar webbläsaren från att automatiskt fylla i text. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta autofyll.
- **Cookies (endast Samsung Knox)** : Välj hur cookies från webbplatser ska hanteras på enheter. Alternativen är:
  - Tillåt
  - Blockera alla cookies
  - Tillåt cookies från besökta webbplatser
  - Tillåt cookies från aktuell webbplats
- **JavaScript (endast Samsung Knox)** : **Blockera** förhindrar att JavaScript körs i webbläsaren. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta de här skripten.
- **Popup-fönster (endast Samsung Knox)** : **Blockera** aktiverar blockering av popup-fönster i webbläsaren. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta popup-fönster.

## <a name="allow-or-block-apps"></a>Tillåt eller blockera program

Använd inställningarna för att tillåta, blockera eller dölja specifika appar på Samsung Knox Standard-enheter. Användare kan inte öppna eller köra appar som är dolda.

Alternativen är:

- **Appar som kan installeras (endast Samsung Knox Standard)** : Lägg till appar som användare kan installera. Användare kan inte installera appar som inte finns i listan.
- **Appar som blockeras från att starta (endast Samsung Knox Standard)** : Ange appar som användare inte kan köra på sina enheter.
- **Appar som döljs för användaren (endast Samsung Knox Standard)** : Ange de appar som ska vara dolda på enheterna. Användare kan inte identifiera eller köra de här apparna.

Lägg till appar för varje inställning:

- **Lägg till appar efter paketnamn**: Ange namnet på programmet och namnet på appaketet. Används främst för verksamhetsspecifika appar. 
- **Lägg till appar efter URL**: Ange namnet på programmet och dess URL i Google Play Butik.
- **Lägg till Store-app**: Välj en app från den befintliga listan med appar som du hanterar i Intune.

## <a name="cloud-and-storage"></a>Moln och lagring

- **Google-säkerhetskopiering (endast Samsung Knox)** : **Blockera** förhindrar att enheter synkroniserar med Google-säkerhetskopiering. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användning av Google-säkerhetskopiering.
- **Automatisk synkronisering av Google-konto (endast Samsung Knox)** : **Blockera** förhindrar användning av funktionen Automatisk synkronisering av Google-konto på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att Google-kontoinställningarna synkroniseras automatiskt.
- **Flyttbara lagringsenheter (endast Samsung Knox)** : **Blockera** förhindrar att enheter använder flyttbara lagringsenheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att enheter använder flyttbara lagringsenheter, till exempel SD-kort.
- **Kryptering på lagringskort (endast Samsung Knox)** : **Kräv** tvingar lagringskorten att vara krypterade. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att okrypterade lagringskort används. Alla enheter stöder inte kryptering av minneskort. Bekräfta genom att kontrollera detta med enhetstillverkaren.

## <a name="cellular-and-connectivity"></a>Mobilnät och anslutning

- **Datanätverksväxling (endast Samsung Knox)** : **Blockera** förhindrar dataroaming i mobilnätet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta dataroaming.
- **SMS-/MMS-meddelanden (endast Samsung Knox)** : **Blockera** förhindrar SMS på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användning av SMS och MMS.
- **Röstsamtal (endast Samsung Knox)** : **Blockera** hindrar användare från att använda röstsamtalsfunktionen på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta röstsamtal.
- **Röstnätverksväxling (endast Samsung Knox)** : **Blockera** förhindrar röstroaming i mobilnätet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta röstroaming.
- **Bluetooth (endast Samsung Knox)** : **Blockera** förhindrar användning av Bluetooth på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användning av Bluetooth.
- **NFC (endast Samsung Knox)** : **Blockera** inaktiverar åtgärder som använder närfältskommunikation på de enheter som stöds. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta NFC-åtgärder.
- **Wi-Fi (endast Samsung Knox)** : **Blockera** förhindrar användning av Wi-Fi på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användning av Wi-Fi.
- **Trådlös Internetdelning (endast Samsung Knox)** : **Blockera** förhindrar delning av Wi-Fi på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användning av Wi-Fi-delning.

## <a name="kiosk"></a>Helskärmsläge

Inställningarna för helskärmsläget gäller endast för Samsung Knox Standard-enheter och enbart för program som du hanterar med Intune.

- Lägg till appar som du vill ska köras när enheten är i helskärmsläge. I helskärmsläge körs bara appar som du lägger till. Appar som inte har lagts till körs inte. Förinstallerade webbläsare körs inte som en app när enheten är i helskärmsläge. Om en webbläsare krävs ska du fundera på att använda den [hanterade webbläsaren](../apps/app-configuration-managed-browser.md).

  Alternativ för din app:

  - **Lägg till appar efter paketnamn**: Används främst för verksamhetsspecifika appar. Ange namnet på programmet och namnet på appaketet.
  - **Lägg till appar efter URL**: Ange namnet på programmet och dess URL i Google Play Butik.
  - **Lägg till Store-app**: Välj en app från den befintliga listan med appar som du hanterar i Intune.

- **Viloläge för skärm-knapp**: **Blockera** förhindrar eller döljer Viloläge för skärm-knappen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta knappen för aktivering/inaktivering av viloläge för skärm på enheter.
- **Volymknappar**: **Blockera** hindrar användare från att ändra volymen genom att volymknapparna inaktiveras. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att volymknapparna används på enheter.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Du kan också skapa profiler för helskärmsläge för [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)- och [Windows 10](kiosk-settings.md)-enheter.
