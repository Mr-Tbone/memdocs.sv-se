---
title: Kompatibilitetsinställningar för Android-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Visa en lista över alla inställningar som du kan använda när du konfigurerar kompatibilitet för Android-enheter i Microsoft Intune. Ange regler för lösenord, välj en lägsta eller högsta operativsystemversion, begränsa specifika appar, förhindra att lösenord återanvänds och mycket mer.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e1258fe4-0b5c-4485-8bd1-152090df6345
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f8cb75907befaa747ebae1718815d9722ff7085
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729218"
---
# <a name="android-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Android-inställningar för att markera enheter som kompatibla eller inkompatibla med hjälp av Intune

Den här artikeln innehåller en lista över och beskriver de olika kompatibilitetsinställningar som du kan konfigurera på Android-enheter i Intune. Använd dessa inställningar som en del av din MDM-lösning för hantering av mobilenheter, t.ex. för att markera rotade (jailbreakade) enheter som inkompatibla, ange en tillåten hotnivå eller aktivera Google Play-skydd.

Den här funktionen gäller för:

- Android-enhetsadministratör

Som Intune-administratör kan du använda dessa kompatibilitetsinställningar för att skydda din organisations resurser. Mer om kompatibilitetsprinciper och vad de gör finns i [Komma igång med kompatibilitet](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en efterlevnadsprincip](create-compliance-policy.md#create-the-policy). Som **Plattform** väljer du **Android-enhetsadministratör**.

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

- **Kräv att enheten ska hållas vid eller under riskpoängen**  

  Välj den högsta tillåtna riskpoängen för enheter som utvärderas av Microsoft Defender ATP. Enheter som överskrider den här poängen markeras som inkompatibla.
  - **Ej konfigurerat** (*standard*)
  - **Rensa**
  - **Låg**
  - **Medel**
  - **Hög**

## <a name="device-health"></a>Enhetens hälsotillstånd

- **Enheter som hanteras med enhetsadministratör**  
  *Enhetsadministratörsfunktioner* ersätts av Android Enterprise.

  - **Ej konfigurerat** (*standard*)
  - **Blockering** – När enhetsadministratören blockeras ombeds användarna att gå över till Android Enterprise-arbetsprofilhantering för att få åtkomst igen.

- **Rotade enheter**  
  Förhindra företagsåtkomst för rotade enheter. (Den här kompatibilitetskontrollen stöds för Android 4.0 och senare.)

  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Blockera** – Markera rotade (jailbreakade) enheter som inkompatibla.

- **Kräv att enheten ligger på eller under enhetshotnivån**  
  Använd den här inställningen för att använda riskbedömningen från en ansluten Mobile Threat Defense-tjänst  för skydd mot hot som ett villkor för efterlevnad.

  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Säkrad** – Det här alternativet är det säkraste eftersom enheten inte kan ha några hot. Om hot på någon nivå identifieras på enheten betraktas den som inkompatibel.
  - **Låg** – Enheten utvärderas som kompatibel om det bara finns lågnivåhot på den. Om hot på en högre nivå identifieras får enheten statusen icke-kompatibel.
  - **Medel** – Enheten utvärderas som kompatibel om befintliga hot på enheten är på en låg eller medelhög nivå. Om hot på en högre nivå identifieras på enheten får den statusen inkompatibel.
  - **Hög** – Det här alternativet är det minst säkra, och det tillåter alla hotnivåer. Det skulle kunna vara användbart om lösningen endast används i rapporteringssyfte.

### <a name="google-play-protect"></a>Google Play-skydd

- **Google Play-tjänster har konfigurerats**  
  Google Play-tjänster tillåter säkerhetsuppdateringar, vilket är ett beroende på grundnivå för många säkerhetsfunktioner på certifierade Google-enheter.

  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.  
  - **Kräv** – Kräv att Google Play-tjänstappen installeras och aktiveras.  

- **Uppdaterad säkerhetsprovider**

  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Kräv** – Kräv att en uppdaterad säkerhetsprovider kan skydda enheten mot kända säkerhetsproblem.

- **Hotgenomsökning för appar**

  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Kräv** – Kräv att funktionen **Verifiera appar** i Android har aktiverats.

  > [!NOTE]
  > Den här funktionen är en kompatibilitetsinställning på den äldre Android-plattformen. Intune kan bara kontrollera om den här inställningen är aktiverad på enhetsnivå.

- **SafetyNet-enhetsattestering**  
  Ange den nivå av [SafetyNet-attestering](https://developer.android.com/training/safetynet/attestation.html) som måste uppfyllas. Alternativen är:

  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Kontrollera grundläggande integritet**
  - **Kontrollera grundläggande integritet och certifierade enheter**

> [!NOTE]
> Information om hur du konfigurerar inställningar för Google Play-skydd med hjälp av appskyddsprinciper finns i [Inställningar för appskyddsprinciper i Intune](../apps/app-protection-policy-settings-android.md#conditional-launch) på Android.

## <a name="device-properties"></a>Egenskaper för enhet

### <a name="operating-system-version"></a>Operativsystemversion

- **Lägsta version av operativsystemet**  
  När en enhet inte uppfyller minimikravet på operativsystemversion, rapporteras den som inkompatibel. En länk med information om hur du uppgraderar visas. Slutanvändaren kan välja att uppgradera enheten och kan sedan komma åt företagets resurser.

  *Som standard finns det ingen konfigurerad version*.

- **Högsta version av operativsystemet**  
  När en enhet använder en senare version av operativsystemet än den som har specificerats i regeln, så blockeras åtkomsten till företagets resurser. Användaren uppmanas sedan att kontakta IT-administratören. Den här enheten kan inte komma åt företagsresurser förrän en regel ändras så att operativsystemversionen tillåts.

  *Som standard finns det ingen konfigurerad version*.

## <a name="system-security"></a>Systemsäkerhet

### <a name="password"></a>lösenordsinställning

- **Kräv ett lösenord för att låsa upp mobila enheter**  
  *Stöds på Android 4.0 och senare eller KNOX 4.0 och senare.*

  Den här inställningen anger huruvida användaren måste ange ett lösenord för att komma åt information på sin mobila enhet. Rekommenderat värde: Kräver  

  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Kräv** – Användarna måste ange ett lösenord innan de får åtkomst till sina enheter.

- **Lösenordstyp krävs**  
  *Stöds på Android 4.0 och senare eller KNOX 4.0 och senare.*

  Välj om ett lösenord endast ska innehålla numeriska tecken, eller en blandning av siffror och andra tecken.

  - **Standard för enheten** – för att utvärdera lösenordsefterlevnad ska du välja en annan lösenordsstyrka än **Standard för enheten**.
  - **Låg säkerhetsbiometri**
  - **Minst numeriskt**
  - **Numeriskt avancerat** – Upprepade eller efterföljande siffror, till exempel `1111` eller `1234`, tillåts inte.
  - **Minst alfabetiskt**
  - **Minst alfanumeriskt**
  - **Minst alfanumeriskt med symboler**

  Baserat på konfigurationen av den här inställningen är ett eller flera av följande alternativ tillgängliga:

  - **Minsta längd på lösenord**  
    *Stöds på Android 4.0 och senare eller KNOX 4.0 och senare.*

    Ange det minsta antal siffror eller tecken som användarens lösenord måste innehålla.

  - **Maximalt antal minuters inaktivitet innan lösenord krävs**  
    *Stöds på Android 4.0 och senare eller KNOX 4.0 och senare.*

    Ange efter hur lång tids inaktivitet som användaren måste ange sitt lösenord igen. Om du väljer **Ej konfigurerad** (standard) görs ingen kompatibilitetskontroll för den här inställningen.

  - **Antal dagar tills lösenordet går ut**  
  *Stöds på Android 4.0 och senare eller KNOX 4.0 och senare.*

  Ange efter hur många dagar lösenordet upphör att gälla och då användaren måste skapa ett nytt lösenord.

  - **Antal tidigare lösenord för att förhindra återanvändning**  
    Ange antalet senast använda lösenord som inte får återanvändas. Använd den här inställningen för att förhindra att användaren återanvänder tidigare använda lösenord. (Stöds för Android 4.0 och senare eller KNOX 4.0 och senare.)

### <a name="encryption"></a>Kryptering

- **Kryptering av datalagring på en enhet**  
  *Stöds på Android 4.0 och senare eller KNOX 4.0 och senare.*

  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Kräv** – kryptera datalagring på dina enheter. Enheter krypteras när du väljer inställningen **Kräv lösenord för att låsa upp mobila enheter**.

### <a name="device-security"></a>Enhetssäkerhet

- **Blockera appar från okända källor**  
  *Stöds från Android 4.0 till Android 7.x. Stöds inte av Android 8.0 och senare*

  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Blockera** – blockera enheter med källor med **Säkerhet > Okända källor** aktiverat (*stöds i Android 4.0 till Android 7.x. Stöds inte på Android 8.0 och senare.* ).

  Om du vill att läsa in appar separat, måste okända källor tillåtas. Om du inte läser in Android-appar separat konfigurerar du den här funktionen med **Blockera** om du vill aktivera den här efterlevnadsprincipen.

  > [!IMPORTANT]
  > Inställningen **Blockera appar från okända källor** måste vara aktiverad för program med separat inläsning. Du bör endast tillämpa den här efterlevnadsprincipen om du inte läser in Android-appar separat på enheter.

- **Körningsintegritet för företagsportalappen**
  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Kräv** – Välj *Kräv* om du vill bekräfta att företagsportalsappen uppfyller följande krav:

    - Har standardkörningsmiljön installerad
    - Är korrekt signerad
    - Är inte i felsökningsläge
    - Har installerats från en känd källa

- **Blockera USB-felsökning på enheten**  
  *(Stöds på Android 4.2 eller senare)*

  - **Ej konfigurerad** (*standard*) – Ingen kompatibilitetskontroll görs för den här inställningen.
  - **Blockera** – Förhindra att enheter använder USB-felsökningsfunktionen.

- **Lägsta säkerhetskorrigeringsnivå**  
  *(Stöds på Android 6.0 eller senare)*

  Välj den äldsta säkerhetskorrigeringsnivå som en enhet kan ha. Enheter som inte har minst den här korrigeringsnivån räknas som inkompatibla. Datumet måste anges i formatet `YYYY-MM-DD`.

  *Som standard finns det inget konfigurerat datum*.

- **Begränsade appar**  
  Ange **appnamnet** och **appsamlings-ID:t** för appar som ska vara begränsade, och välj sedan **Lägg till**. En enhet med minst en begränsad app installerad har markerats som inkompatibel.

## <a name="next-steps"></a>Nästa steg

- [Lägga till åtgärder för inkompatibla enheter](actions-for-noncompliance.md) och [Filtrera principer med hjälp av omfångstaggar](../fundamentals/scope-tags.md).
- [Övervaka dina kompatibilitetsprinciper](compliance-policy-monitor.md).
- Mer information finns i [Inställningar för kompatibilitetsprinciper för Android Enterprise-enheter](compliance-policy-create-android-for-work.md).
