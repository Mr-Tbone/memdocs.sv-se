---
title: iOS/iPadOS-enhetsinställningar i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Lägg till, konfigurera eller skapa inställningar på iOS/iPadOS-enheter när du vill begränsa funktioner, till exempel lösenordskrav, kontrollera låst skärm, använda inbyggda appar, lägga till begränsade eller godkända appar, hantera bluetooth-enheter, ansluta till molnet för säkerhetskopiering och lagring, aktivera helskärmsläge, lägga till domäner och kontrollera hur användarna samverkar med Safari-webbläsaren i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: ea0968d15572fa9c3bde1e4d133dcb8b4c980274
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80087054"
---
# <a name="ios-and-ipados-device-settings-to-allow-or-restrict-features-using-intune"></a>Enhetsinställningarna för iOS och iPadOS tillåter eller begränsar funktioner med hjälp av Intune

Den här artikeln beskriver de olika inställningar som du kan styra på iOS- och iPadOS-enheter. Som en del av din MDM-lösning (hantering av mobilenheter) använder du dessa inställningar för att tillåta eller inaktivera funktioner, ange lösenordsregler, tillåta eller begränsa specifika appar med mera.

Dessa inställningar läggs till en profil för enhetskonfiguration i Intune som sedan tilldelas eller distribueras till dina iOS/iPadOS-enheter.

> [!TIP]
> De här inställningarna använder Apples MDM-inställningar. Mer information om de här inställningarna finns i [Apples inställningar för hantering av mobilenheter](https://support.apple.com/guide/mdm/welcome/web) (öppnar Apples webbplats).

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en konfigurationsprofil för enhetsbegränsningar](device-restrictions-configure.md).

> [!NOTE]
> Dessa inställningar gäller för olika registreringstyper. Vissa inställningar gäller för alla registreringsalternativ. Mer information om de olika registreringstyperna finns i [iOS/iPadOS-registrering](../enrollment/ios-enroll.md).

## <a name="general"></a>Allmänt

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Dela användningsdata**: **Blockera** förhindrar enheten från att skicka diagnostik- och användningsdata till Apple. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att dessa data skickas.

- **Skärmdump**: **Blockera** förhindrar skärmbilder eller skärmdumpar på enheten. I iOS /iPadOS 9.0 och senare blockeras även skärminspelningar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användaren sparar skärminnehållet som en bild eller video.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Enhetsregistrering, automatisk enhetsregistrering (övervakad)

- **Ej betrodda TLS-certifikat**: **Blockera** stoppar ej betrodda TLS-certifikat på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan om standard tillåta TLS-certifikat.
- **Blockera trådlösa PKI-uppdateringar**: **Blockera** hindrar användarna från att ta emot programuppdateringar om inte enheten är ansluten till en dator. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att en enhet tar emot programuppdateringar utan att vara ansluten till en dator.
- **Begränsa reklamspårning**: Välj **Begränsa** om du vill inaktivera enhetens reklamidentifierare. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard låta det vara aktiverat.
- **Företagsappförtroende**: **Blockera** tar bort knappen **Lita på företagsutvecklare** i Inställningar > Allmänt > Profiler och enhetshantering på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användaren väljer att lita på appar som inte laddats ned från App Store.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Automatisk enhetsregistrering (övervakad)

- **Ändring av inställningar för att skicka diagnostik**: **Blockera** hindrar användarna från att ändra inställningarna för diagnostiköverföring och appanalys i **Diagnostik och användning** (enhetsinställningar). När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ändra dessa enhetsinställningar.

  Om du vill använda den här inställningen anger du inställningen **Dela användningsdata** till **Blockera**.

  Den här funktionen gäller för:  
  - iOS 9.3.2 och senare
  - iPadOS 13.0 och senare

- **Fjärrskärmsvisning via appen Klassrum**: **Blockera** förhindrar appen Klassrum från att visa skärmarna på fjärranslutna enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta appen Apple Klassrum att visa skärmen.

  Om du vill använda den här inställningen anger du inställningen **Skärmdump** till **Blockera**.

  Den här funktionen gäller för:  
  - iOS 9.3 och senare
  - iPadOS 13.0 och senare

- **Skärmvisning utan uppmaning via appen Klassrum**: Om det är inställt på **Tillåt** kan lärarna tyst övervaka skärmarna på elevernas iOS/iPadOS-enheter med hjälp av appen Klassrum utan att eleverna vet om det. Elevenheter som har registrerats i en klass med appen Classroom ger automatiskt behörighet till kursens lärare. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra den här funktionen.

  Om du vill använda den här inställningen anger du inställningen **Skärmdump** till **Blockera**.

- **Kontoändring**: När inställningen är **Blockera** kan användaren inte uppdatera enhetsspecifika inställningar från iOS/iPadOS-appens inställningar. Användarna kan t.ex. inte skapa nya enhetskonton eller ändra användarnamn eller lösenord. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ändra dessa inställningar.

  Den här funktionen gäller även för inställningar som kan nås från appen för iOS/iPadOS-inställningar, som E-post, Kontakter, Kalender, Facebook, Twitter med flera. Den här funktionen gäller inte för appar med kontoinställningar som inte konfigureras från appen för iOS/iPadOS-inställningar, som Microsoft Outlook-appen.

- **Skärmtid**: **Blockera** hindrar användare från att ange sina egna begränsningar vad gäller Skärmtid (enhetsinställningar). När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna konfigurerar enhetsbegränsningar (som kontrollfunktioner för föräldrar eller innehålls- och sekretessbegränsningar) på enheten.

  Den här inställningen har bytt namn från **Aktivera begränsningar i enhetsinställningarna**. Effekten av ändringen:  
  
  - iOS 11.4.1 och senare: **Blockera** förhindrar användarna att ange egna begränsningar i enhetsinställningarna. Beteendet är detsamma. Ingenting har ändrats för användarna.
  - iOS 12.0 och senare: **Blockera** hindrar användarna från att ange sin egen **skärmtid** i enhetsinställningarna (Inställningar > Allmänt > Skärmtid), inklusive innehålls- och sekretessbegränsningar. På enheter som har uppgraderats till iOS 12.0 visas inte längre fliken Begränsningar i enhetsinställningarna (Inställningar > Allmänt > Enhetshantering > Hanteringsprofil > Begränsningar). Dessa inställningar finns i **Skärmtid**.
  
- **Användning av alternativet Radera allt innehåll och inställningar på enheten**: Välj **Blockera** så att användarna inte kan alternativet att radera allt innehåll och inställningar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard ge användarna åtkomst till dessa inställningar.
- **Ändra enhetsnamn**: Välj **Blockera** så att enhetsnamnet inte kan ändras. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ändra enhetens namn.
- **Ändring av notisinställningar**: Välj **Blockera** så att meddelandeinställningarna inte kan ändras. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ändra enhetsmeddelandeinställningarna.
- **Ändring av bakgrundsbild**: **Blockera** förhindrar att bakgrundsbilden ändras. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ändra enhetens bakgrund.
- **Ändra konfigurationsprofil**: **Blockera** förhindrar ändringar av konfigurationsprofilen på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att installera konfigurationsprofiler.
- **Aktiveringslås**: Välj **Tillåt** för att aktivera aktiveringslåset på övervakade iOS/iPadOS-enheter. Aktiveringslåset gör det svårare att återaktivera en förlorad eller stulen enhet.
- **Blockera borttagning av app**: **Blockera** förhindrar användarna från att ta bort appar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ta bort appar från enheten.
- **Tillåt USB-tillbehör när enheten är låst**: **Tillåt** låter USB-tillbehör utbyta data med en enhet som har varit låst i över en timme. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet uppdaterar kanske inte USB-begränsat läge som standard på enheten, och USB-tillbehören blockeras från att överföra data från enheten om den är låst i mer än en timma.
- **Tvinga automatiskt datum och tid**: **Kräv** tvingar övervakade enheter att ange datum och tid automatiskt. Enhetens tidszon uppdateras när enheten har mobila anslutningar eller har aktiverats för Wi-Fi med platstjänster.
- **Kräv att deltagarna begär tillstånd för att lämna Klassrumskursen**: **Kräv** tvingar elever som har registrerats i en ohanterad kurs med appen Klassrum att begära tillstånd från läraren om att lämna kursen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet tvingar kanske inte som standard eleven att be om behörighet.

  Den här funktionen gäller för:  
  - iOS 11.3 och senare
  - iPadOS 13.0 och senare

- **Tillåt Klassrum att låsa en app och låsa enheten utan att fråga**: **Aktivera** tillåter att lärare låser appar eller låser enheten med hjälp av Classroom-appen utan att fråga eleven. Applåsning innebär att enheten endast kan komma åt de appar som anges av läraren. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra att lärare låser appar eller enheter med hjälp av Classroom-appen utan att fråga eleven.

  Den här funktionen gäller för:  
  - iOS 11.0 och senare
  - iPadOS 13.0 och senare

- **Delta automatiskt i klassrumsklasser utan att fråga**: **Aktivera** tillåter automatiskt elever att ansluta till en klass i Classroom-appen utan att fråga läraren. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard uppmärksamma läraren på att elever vill ansluta till en klass i Classroom-appen.

  Den här funktionen gäller för:  
  - iOS 11.0 och senare
  - iPadOS 13.0 och senare

- **Blockera möjlighet att skapa VPN**: **Blockera** förhindrar användare från att skapa VPN-konfigurationsinställningar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att skapa virtuella privata nätverk på enheten.
- **Ändrar eSIM-inställningar**: **Blockera** hindrar användarna från att ta bort eller lägga till ett mobilabonnemang till eSIM på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ändra dessa inställningar.

  Den här funktionen gäller för:  
  - iOS 12.1 och senare
  - iPadOS 13.0 och senare

- **Skjut upp programuppdateringar**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa programuppdateringar på enheten när Apple släpper dem. Om en iOS/iPadOS-uppdatering exempelvis släpps av Apple på ett specifikt datum, visas uppdateringen på enheten runt utgivningsdatumet.

  **Aktivera** gör att du kan skjuta upp visningen av programuppdateringar på enheter i 0–90 dagar. Den här inställningen styr inte när uppdateringar installeras eller inte. 

  - **Fördröj visning av programuppdateringar**: Ange ett värde mellan 0–90 dagar. När fördröjningen upphör får användarna ett meddelande om att uppdatera till den tidigaste versionen av OS som var tillgänglig när fördröjningen utlöstes.

    Om iOS 12.a exempelvis blir tillgänglig **den 1 januari** och **Fördröj synlighet** är inställt på **5 dagar**, visas inte iOS 12.som en tillgänglig uppdatering på användarnas enheter. På **den sjätte dagen** efter utgivningen är uppdateringen tillgänglig och användarna kan installera den.

    Den här inställningen gäller för:  
    - iOS 11.3 och senare
    - iPadOS 13.0 och senare

## <a name="password"></a>lösenordsinställning

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Lösenord**: **Kräv** att användarna anger sina lösenord för att få åtkomst till enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan tillåta användarna få åtkomst till enheten utan att behöva ange något lösenord.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Enhetsregistrering, automatisk enhetsregistrering (övervakad)

> [!IMPORTANT]
> Om du konfigurerar en lösenordsinställning på en enhet som registreras via Användarregisterring används automatiskt inställningen **Blockera** för **Enkla lösenord**, och en 6-siffrig PIN-kod krävs.
>
> Du kan till exempel konfigurera inställningen **Lösenordets giltighetstid** och skicka den här principen till användarregistrerade enheter. Följande händer på enheterna:
>
> - Inställningen **Lösenordets giltighetstid** ignoreras.
> - Enkla lösenord, till exempel `1111` eller `1234`, tillåts inte.
> - En 6-siffrig PIN-kod krävs.

- **Enkla lösenord**: **Blockera** kräver mer komplexa lösenord. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta enkla lösenord, som `0000` och `1234`.

- **Lösenordstyp som krävs**: Välj den typ av lösenord som din organisation kräver. Alternativen är:
  - **Standard för enheten**
  - **Numerisk**
  - **Alfanumerisk**
- **Antal icke-alfanumeriska tecken i lösenord**: Ange antalet symboltecken (till exempel `#` eller `@`) som måste tas med i lösenordet.

- **Minsta lösenordslängd**: Ange den minsta längden som en användare måste ange, mellan 4 och 14 tecken. På användarregistrerade enheter anger du en längd på mellan 4 och 6 tecken.
  
  > [!NOTE]
  > För enheter som är användarregistrerade kan användare ange en PIN-kod med fler än 6 siffror. Dock tillämpas högst 6 siffror på enheten. Till exempel anger en administratör minimilängden till `8`. På användarregistrerade enheter behöver användarna bara ange en 6-siffrig PIN-kod. Intune framtvingar inte en PIN-kod som har fler än 6 siffror på användarregistrerade enheter.

- **Antal felaktiga inloggningar innan enheten rensas**: Anger antalet tillåtna felinloggningar innan enheten rensas (mellan 4 och 11).
  
  iOS/iPadOS har inbyggd säkerhet som kan påverka den här inställningen. Till exempel kan iOS/iPadOS fördröja utlösandet av principen beroende på antalet inloggningsförsök. Det kan även betrakta upprepade angivelser av samma lösenord som ett försök. Apples [säkerhetsguide för iOS/iPadOS](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) (öppnar Apples webbplats) är en bra resurs och innehåller mer detaljerad information om lösenord.
  
- **Maximalt antal minuter efter skärmlås innan ett lösenord krävs**<sup>1</sup>: Ange hur länge enheten kan vara inaktiv innan användaren måste ange sitt lösenord på nytt. Om den tid som du anger är längre än vad som är angivet i enhetens inställningar, så ignorerar enheten den tid som du anger. Stöds på enheter som kör iOS 8.0 + och iPad 13.0 +.

- **Maximalt antal minuter av inaktivitet innan skärmen låses**<sup>1</sup>: Ange det maximala antal minuter av inaktivitet som ska tillåtas på enheten innan skärmen låses.

  **iOS/iPad-alternativ**:  

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Omedelbart**: Skärmen låses efter 30 sekunders inaktivitet.
  - **1**: Skärmen låses efter 1 minuts inaktivitet.
  - **2**: Skärmen låses efter 2 minuters inaktivitet.
  - **3**: Skärmen låses efter 3 minuters inaktivitet.
  - **4**: Skärmen låses efter 4 minuters inaktivitet.
  - **5**: Skärmen låses efter 5 minuters inaktivitet.

  **iPad-alternativ**:  

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Omedelbart**: Skärmen låses efter 2 minuters inaktivitet.
  - **2**: Skärmen låses efter 2 minuters inaktivitet.
  - **5**: Skärmen låses efter 5 minuters inaktivitet.
  - **10**: Skärmen låses efter 10 minuters inaktivitet.
  - **15**: Skärmen låses efter 15 minuters inaktivitet.

  Om ett värde inte gäller för iOS och iPad använder Apple närmaste *lägsta* värde. Om du till exempel anger `4` minuter använder iPad-enheter `2` minuter. Om du anger `10` minuter använder iOS-enheter `5` minuter. Detta är en Apple-begränsning.
  
  > [!NOTE]
  > Intune-användargränssnittet för den här inställningen skiljer inte de värden som stöds för iOS och iPad. Användargränssnittet kan komma att uppdateras i en framtida version.

- **Lösenordets giltighetstid (dagar)** : Ange antalet dagar innan lösenordet måste ändras.
- **Förhindra återanvändning av tidigare lösenord**: Ange hur många nya lösenord som måste ha använts innan ett gammalt kan återanvändas.
- **Upplåsning av Touch ID och Face ID**: **Blockera** förhindrar att fingeravtryck eller ansiktsigenkänning används för att låsa upp enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att låsa upp enheten med hjälp av dessa metoder.

  Om den här inställningen blockeras förhindrar det även användning av FaceID-autentisering för att låsa upp enheten.

  Face ID gäller för:  
  - iOS 11.0 och senare
  - iPadOS 13.0 och senare

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Automatisk enhetsregistrering (övervakad)

- **Ändring av lösenord**: **Blockera** förhindrar att lösenord ändras, läggs till eller tas bort. Ändringar av lösenkodsbegränsningar ignoreras på övervakade enheter när den här funktionen har blockerats. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att lösenord läggs till, ändras eller tas bort.

  - **Ändring av Touch ID och Face ID**: **Blockera** stoppar användarna från att ändra, lägga till eller ta bort TouchID-fingeravtryck och Face ID. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att uppdatera TouchID-fingeravtrycken och Face ID på enheten.

    Om den här inställningen blockeras så hindras användarna även från att ändra, lägga till eller ta bort FaceID-autentisering.

    Face ID gäller för:  
    - iOS 11.0 och senare
    - iPadOS 13.0 och senare

- **Blockera automatisk ifyllning av lösenord**: **Blockera** förhindrar användningen av funktionen för automatisk ifyllning av lösenord i iOS/iPadOS. Inställningen **Blockera** har också följande effekt:

  - Användarna ombeds inte att använda ett sparat lösenord i Safari eller i någon app.
  - Automatisk starka lösenord inaktiveras och starka lösenord föreslås inte för användare.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta de här funktionerna.

- **Blockera förfrågningar om lösenordsnärhet**: Välj **Blockera** så att användarens enhet inte begär lösenord från enheter i närheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta de här funktionerna.
- **Blockera lösenordsdelning**: **Blockera** förhindrar att lösenord delas mellan enheter med hjälp av AirDrop. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att dessa data skickas.
- **Kräv autentisering via Touch ID eller Face ID för automatisk ifyllning av lösenord eller bankkortsuppgifter**: När inställningen **Kräv** används måste användare autentisera med hjälp av TouchID eller FaceID innan lösenord eller kreditkortsinformationen kan fyllas i automatiskt i Safari och andra appar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att kontrollera den här funktionen i enhetsinställningarna.

  Den här funktionen gäller för:  
  - iOS 11.0 och senare
  - iPadOS 13.0 och senare
  
<sup>1</sup> När du konfigurerar **Max. antal minuters inaktivitet tills skärmen låses** och **Max. antal minuter efter skärmlås innan lösenord krävs** tillämpas de i följd. Om du t.ex. ställer in värdet för båda inställningarna till **5** minuter så stängs skärmen av automatiskt efter fem minuter. Enheten låses efter ytterligare fem minuter. Om användarna däremot stänger av skärmen manuellt, så tillämpas den andra inställningen omedelbart. När användaren i det här exemplet har stängt av skärmen låses enheten fem minuter senare.

## <a name="locked-screen-experience"></a>Låsskärm

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Åtkomst till Kontrollcenter när enheten är låst**: **Blockera** förhindrar åtkomst till Kontrollcenter-appen när enheten är låst. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard låta användarna få åtkomst till Kontrollcenter-appen när enheten är låst.
- **Meddelanden när enheten är låst**: **Blockera** förhindrar åtkomst till meddelanden när enheten är låst. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard låta användarna få åtkomst till meddelandena utan att behöva låsa upp enheten.
- **Dagsvyn när enheten är låst**: **Blockera** förhindrar åtkomst till dagsvyn när enheten är låst. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard låta användarna se Idag-appen när enheten är låst.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Enhetsregistrering, automatisk enhetsregistrering (övervakad)

- **Wallet-notiser när enheten är låst**: **Blockera** förhindrar åtkomst till Wallet-appen när enheten är låst. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard låta användarna få åtkomst till Plånbok-appen när enheten är låst.

## <a name="app-store-doc-viewing-gaming"></a>App Store, dokumentvisning, spel

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Visa företagsdokument i ohanterade appar**: **Blockera** förhindrar visning av företagsdokument i ohanterade appar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att företagsdokument visas i vilken app som helst. Exempelvis vill du kanske förhindra användare från att spara filer från OneDrive-appen till Dropbox. Konfigurera den här inställningen som **Blockera**. När enheten har hämtat principen (t.ex. efter en omstart) kommer det inte längre att vara tillåtet att spara.


  > [!NOTE]
  > När den här inställningen blockeras så blockeras även tangentbord från tredje part som är installerade från App Store.

  - **Tillåt ohanterade appar att läsa från hanterade kontaktkonton**: När detta anges till **Tillåt** kan ohanterade appar, till exempel den inbyggda appen för iOS/iPadOS-kontakter, läsa och få åtkomst till kontaktinformation från hanterade appar, däribland Outlook-mobilappen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra läsning, inklusive borttagande av dubbletter, från den inbyggda appen Kontakter på enheten.  
  
    Den här inställningen tillåter eller förhindrar läsning av kontaktinformation. Den styr inte synkronisering av kontakter mellan apparna.
  
    Om du vill använda inställningen ställer du in **Visa företagsdokument i ohanterade appar** på **Blockera**.

  Mer information om de här två inställningarna och deras inverkan på Outlook för synkronisering av iOS/iPadOS-kontaktexport finns i [Supporttips: Använd anpassade Intune-profilinställningar med den inbyggda appen för iOS/iPadOS-kontakter](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Use-Intune-custom-profile-settings-with-the-iOS/ba-p/298453).

- **Behandla AirDrop som ohanterat mål**: **Kräv** tvingar fram att AirDrop betraktas som ett ohanterat släppmål. Det förhindrar hanterade appar från att skicka data med hjälp av Airdrop. 
- **Visa dokument som inte gäller företag i företagsappar**: **Blockera** förhindrar visning av icke-företagsdokument i företagsappar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att vilket dokument som helst visas i företagshanterade appar.

  **Blockera** förhindrar även kontaktexportssynkronisering i Outlook för iOS/iPadOS. Mer information finns i [Supporttips: Aktivera synkronisering av Outlook iOS/iPadOS-kontakter med iOS12 MDM-kontroller](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Enabling-Outlook-iOS-Contact-Sync-with-iOS12-MDM/ba-p/298453).

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Enhetsregistrering, automatisk enhetsregistrering (övervakad)

- **Kräv iTunes Store-lösenord för alla köp**: **Kräv** att användarna anger Apple ID-lösenordet för varje köp som görs i en app eller i iTunes. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta köp utan krav på lösenord varje gång.
- **Köp i app**: **Blockera** förhindrar att köp görs från butiken i appen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta köp från butiken i en app som körs.
- **Ladda ned innehåll från iBook-butiken flaggat som ”erotik”** : **Blockera** förhindrar användarna från att ladda ned mediainnehåll som klassificeras som erotik från iBook-butiken. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna laddar ned böcker i kategorin Erotik.
- **Tillåt hanterade appar att skriva kontakter till ohanterade kontaktkonton**: När detta anges till **Tillåt** kan hanterade appar, till exempel Outlook-mobilappen, spara eller synkronisera kontaktinformation såsom affärs- och företagskontakter till den inbyggda appen för iOS/iPadOS-kontakter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra hanterade appar från att spara eller synkronisera kontaktinformation till den inbyggda appen för iOS/iPadOS-kontakter på enheten.
  
  Om du vill använda inställningen ställer du in **Visa företagsdokument i ohanterade appar** på **Blockera**.

- **Klassificeringsregion**: Välj den klassificeringsregion som du vill använda för tillåtna hämtningsbara filer. Och välj sedan tillåtna klassificeringar för **filmer**, **TV-program** och **appar**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Automatisk enhetsregistrering (övervakad)

- **App Store**: **Blockera** förhindrar åtkomst till App Store på övervakade enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta åtkomst.

  Från och med iOS/iPadOS 13.0 kräver den här inställningen övervakade enheter.

  - **Installerar appar från App Store**: Välj **Blockera** för att blockera App Store från enhetens startskärm. Användarna kan fortsätta att använda iTunes eller Apple Configurator för att installera appar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att App Store visas på hemskärmen.
  - **Automatisk nedladdning av appar**: **Blockera** förhindrar automatisk nedladdning av appar som har köpts på andra enheter. Det påverkar inte uppdateringar av befintliga appar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att appar som har köpts på andra iOS/iPadOS-enheter laddas ned på enheten.

- **Stötande innehåll i iTunes-musik, podcast eller nyheter**: **Blockera** förhindrar stötande innehåll i iTunes-musik, podcastsändningar eller nyheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att enheten får åtkomst till sådant som är klassificerat som vuxet innehåll i butiken.

  Från och med iOS/iPadOS 13.0 kräver den här inställningen övervakade enheter.

- **Lägga till Game Center-vänner**: **Blockera** förhindrar användare från att lägga till Game Center-vänner. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att lägga till vänner i Game Center.

  Från och med iOS/iPadOS 13.0 kräver den här inställningen övervakade enheter.

- **Spelcenter**: **Blockera** förhindrar användning av Game Center-appen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att Game Center-appen används på enheten.
- **Spel för flera personer**: **Blockera** förhindrar spel för flera personer. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna spelar spel för flera användare på enheten.

  Från och med iOS/iPadOS 13.0 kräver den här inställningen övervakade enheter.

- **Åtkomst till nätverksenhet i Files-appen**: Med hjälp av SMB-protokollet (Server Message Block) har enheter åtkomst till filer eller andra resurser på en nätverksserver. **Inaktivera** förhindrar åtkomst till filer på en SMB-nätverksenhet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta åtkomst.

  Den här funktionen gäller för:  
  - iOS 13.0 och senare
  - iPadOS 13.0 och senare

## <a name="built-in-apps"></a>Inbyggda appar

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Siri**: **Blockera** förhindrar åtkomst till Siri. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att röstassistenten Siri används på enheten.
  - **Siri när enheten är låst**: **Blockera** förhindrar åtkomst till Siri när enheten är låst. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att röstassistenten Siri används på enheten när den är låst.

- **Bedrägerivarningar i Safari**: **Kräv** att bedrägerivarningar ska visas i webbläsaren på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard inaktivera den här funktionen.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Enhetsregistrering, automatisk enhetsregistrering (övervakad)

- **Spotlight-sökning för att returnera resultat från Internet**: **Blockera** förhindrar Spotlight från att returnera resultat från sökningar på Internet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att Spotlight-sökningar ansluter till Internet för att visa sökresultat.

- **Cookies i Safari**: Välj hur cookies ska hanteras på enheten. Alternativen är:
  - Tillåt
  - Blockera alla cookies
  - Tillåt cookies från besökta webbplatser
  - Tillåt cookies från aktuell webbplats

- **Safari JavaScript**: **Blockera** förhindrar att Java-skript i webbläsaren körs på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta Java-skript.

- **Popupfönster i Safari**: **Blockera** så att blockering av popup-fönster inaktiveras i webbläsaren. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta blockering av popup-fönster.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Automatisk enhetsregistrering (övervakad)

- **Kamera**: **Blockera** förhindrar åtkomst till enhetens kamera. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta åtkomst till enhetens kamera.

  Från och med iOS/iPadOS 13.0 kräver den här inställningen övervakade enheter.

  - **FaceTime**: **Blockera** förhindrar åtkomst till FaceTime-appen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta åtkomst till FaceTime-appen på enheten.

    Från och med iOS/iPadOS 13.0 kräver den här inställningen övervakade enheter.

- **Siris filter mot olämpligt språk**: **Kräv** förhindrar att Siri från dikterar eller talar ett olämpligt språk.

  Om du vill använda den här inställningen anger du inställningen **Siri** till **Blockera**.

- **Siri för att söka användargenererat innehåll från Internet**: **Blockera** förhindrar Siri att komma åt webbplatser för att besvara frågor. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta Siri att få åtkomst till användargenererat innehåll på Internet.

  Om du vill använda den här inställningen anger du inställningen **Siri** till **Blockera**.

- **Apple News**: **Blockera** förhindrar åtkomst till Apple News-appen på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att Apple News-appen används.
- **iBooks store**: **Blockera** förhindrar åtkomst till iBooks-butiken. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att söka efter och köpa böcker i iBooks Store.
- **Appen Meddelanden på enheten**: **Blockera** förhindrar att användare använder appen Meddelanden för iMessage. Om enheten har stöd för SMS kan användarna fortfarande skicka och ta emot SMS-meddelanden. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att appen Meddelanden skickar och läser meddelanden via Internet.
- **Poddsändningar**: **Blockera** förhindrar användare från att använda appen Podcaster. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att Podcaster-appen används.
- **Musiktjänst**: **Blockera** återställer appen Apple Music till klassiskt läge och inaktiverar tjänsten Musik. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att Apple Music-appen används.
- **iTunes Radio-tjänst**: **Blockera** förhindrar användare från att använda appen iTunes Radio. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att iTunes Radio-appen används.
- **iTunes Store**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta iTunes på enheterna. **Blockera** förhindrar användare från att använda iTunes på enheten.

  Den här funktionen gäller för:  
  - iOS 4.0 och senare
  - iPadOS 13.0 och senare

- **Hitta min iPhone**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att den här Hitta min-funktionen används för att hämta enhetens ungefärliga plats. **Blockera** förhindrar den här funktionen i Hitta min-appen. 

  Den här funktionen gäller för:  
  - iOS 13.0 och senare
  - iPadOS 13.0 och senare

- **Hitta mina vänner**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att den här Hitta min-funktionen används för att hitta släkt och vänner från en Apple-enhet eller iCloud.com. **Blockera** förhindrar den här funktionen i Hitta min-appen.

  Den här funktionen gäller för:  
  - iOS 13.0 och senare
  - iPadOS 13.0 och senare

- **Ändringar av inställningarna för appen Hitta mina vänner**: **Blockera** förhindrar ändringar i Find My Friends-appinställningar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna ändrar inställningarna för appen Hitta mina vänner.

- **Spotlight-sökning för att returnera resultat från Internet**: **Blockera** förhindrar Spotlight från att returnera resultat från sökningar på Internet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att Spotlight-sökningar ansluter till Internet för att visa sökresultat.

- **Blockera borttagning av systemappar från enheten**: Om du väljer **Blockera** inaktiverar du möjligheten att ta bort systemappar från enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ta bort systemappar.

- **Safari**: **Blockera** att webbläsaren Safari används på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att använda webbläsaren Safari.

  Från och med iOS/iPadOS 13.0 kräver den här inställningen övervakade enheter.

- **Autofyll i Safari**: **Blockera** inaktiverar funktionen Autofyll i Safari på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna ändrar inställningarna för automatisk komplettering i webbläsaren.

  Från och med iOS/iPadOS 13.0 kräver den här inställningen övervakade enheter.

## <a name="restricted-apps"></a>Begränsade appar

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Enhetsregistrering, automatisk enhetsregistrering (övervakad)

- **Lista över typer av begränsade appar**: Skapa en lista över appar som användarna inte får installera eller använda. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Användare har åtkomst till appar som du tilldelar samt inbyggda appar.
  - **Otillåtna appar**: Appar som inte hanteras av Intune som du inte vill ha installerade på enheten. Användare hindras inte från att installera en förbjuden app. Men om en användare installerar en app från den här listan rapporteras det i Intune.
  - **Godkända appar**: Appar som användare tillåts att installera. Användarna får inte installera appar som inte finns med i listan. Appar som hanteras av Intune tillåts automatiskt. Användarna hindras inte från att installera en app som inte finns med i listan över godkända appar. Men om de gör det rapporteras det i Intune.

Om du vill lägga till appar i listorna kan du:

- **Lägga till** iTunes App Store-webbadressen för den önskade appen. Om du t.ex. vill lägga till appen Microsoft Work Folders anger du `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` eller `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`.

  Du hittar webbadressen till en app genom att öppna iTunes App Store och söka efter appen. Du kan t.ex. söka efter `Microsoft Remote Desktop` eller `Microsoft Word`. Välj appen och kopiera webbadressen.

  Du kan även använda iTunes för att hitta appen och sedan använda uppgiften **Kopiera länk** för att hämta appens webbadress.

- **Importera** en CSV-fil med information om appen, inklusive webbadressen. Använd formatet `<app url>, <app name>, <app publisher>`. Eller, **Exportera** en befintlig lista som innehåller listan över begränsade appar i samma format.

> [!IMPORTANT]
> Enhetsprofiler som använder inställningar för begränsade appar måste tilldelas grupper av användare.

## <a name="show-or-hide-apps"></a>Visa eller dölja appar

Gäller enheter som kör iOS 9.3 + och iPad 13.0 +.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Automatisk enhetsregistrering (övervakad)

- **Lista över typer av appar**: Skapa en lista över appar som ska visas eller döljas. Du kan visa eller dölja inbyggda appar och verksamhetsspecifika appar. På Apple-webbplatsen finns en lista med [inbyggda Apple-appar](https://support.apple.com/HT208094). Alternativen är:

  - **Dolda appar**: Ange en lista med appar som är dolda för användarna. Användarna kan varken visa eller öppna de här apparna.
  
    Apple förhindrar att vissa inbyggda appar döljs. Du kan till exempel inte dölja appen **Inställningar** på enheten. [Ta bort inbyggda Apple-appar](https://support.apple.com/HT208094) visar en lista över appar som kan döljas.
  
  - **Synliga appar**: Ange en lista med appar som användarna ska kunna se och starta. Inga andra appar kan visas eller startas.

- **Appens webbadress**: Ange butiks-URL:en för den app som du vill visa eller dölja. Exempel:

  - Om du vill lägga till appen Microsoft Work Folders anger du `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` eller `https://apps.apple.com/us/app/work-folders/id950878067?mt=8`. 

  - Om du vill lägga till appen Microsoft Word anger du `https://itunes.apple.com/de/app/microsoft-word/id586447913` eller `https://apps.apple.com/de/app/microsoft-word/id586447913`.

  Du hittar webbadressen till en app genom att öppna iTunes App Store och söka efter appen. Du kan t.ex. söka efter `Microsoft Remote Desktop` eller `Microsoft Word`. Välj appen och kopiera webbadressen.

  Du kan även använda iTunes för att hitta appen och sedan använda uppgiften **Kopiera länk** för att hämta appens webbadress.

- **Appsamlings-ID**: Ange [appsamlings-ID](bundle-ids-built-in-ios-apps.md) för den app som du vill lägga till. Du kan visa eller dölja inbyggda appar och verksamhetsspecifika appar. På Apple-webbplatsen finns en lista med [inbyggda Apple-appar](https://support.apple.com/HT208094).
- **Appnamn**: Ange namnet på den app som du vill lägga till. Du kan visa eller dölja inbyggda appar och verksamhetsspecifika appar. På Apple-webbplatsen finns en lista med [inbyggda Apple-appar](https://support.apple.com/HT208094).
- **Utgivare**: Ange namnet på den utgivare som du vill lägga till.

Om du vill lägga till appar kan du:

- **Lägg till**: Välj om du vill skapa din lista över appar.
- **Importera** en CSV-fil med information om appen, inklusive webbadressen. Använd formatet `<app url>, <app name>, <app publisher>`. Eller välj **Exportera** om du vill skapa en lista över begränsade appar som du har lagt till, i samma format.

## <a name="wireless"></a>Trådlöst

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Enhetsregistrering, automatisk enhetsregistrering (övervakad)

Information som krävs för datanätverksväxling (tips eller viktig information för att hjälpa förvirrade kunder): Den här inställningen visas inte i målenhetens hanteringsprofil. Det beror på att den här inställningen behandlas som en fjärrenhetsåtgärd, och varje gång tillståndet för dataroaming ändras på enheten blockeras den igen av Intune-tjänsten. Även om den inte finns i hanteringsprofilen fungerar den om den visas som lyckad från rapporteringen i administratörskonsolen. 
- **Datanätverksväxling**: **Blockera** förhindrar dataroaming i mobilnätet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta dataroaming när enheten använder ett mobilnät.

  > [!IMPORTANT]
  > Den här inställningen behandlas som en fjärrenhetsåtgärd. Därför visas inte den här inställningen i hanteringsprofilen på enheten. Varje gång statusen för dataroaming ändras på enheten blockeras **Dataroaming** av Intune-tjänsten. Om rapporteringsstatusen i Intune visar att den lyckades vet du att den fungerar, även om inställningen inte visas i hanteringsprofilen på enheten.

- **Hämtning av global bakgrund under nätverksväxling**: **Blockera** förhindrar att funktionen för global bakgrundssamling används under nätverksväxling i mobilnätverket. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att enheten hämtar data, t.ex. e-post, vid dataroaming i ett mobilnät.
- **Röstsamtal**: **Blockera** förhindrar användare från att använda enhetens röstsamtalsfunktion. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta röstsamtal på enheten.
- **Röstnätverksväxling**: **Blockera** förhindrar röstroaming i mobilnätet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta röstroaming när enheten använder ett mobilnät.
- **Internetdelning**: **Blockera** inaktiverar Internetdelning på enheter vid varje enhetssynkronisering. Den här inställningen kanske inte är kompatibel med vissa operatörer. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard behålla användarnas standardinställning för Internetdelning.

  > [!IMPORTANT]
  > Den här inställningen behandlas som en fjärrenhetsåtgärd. Därför visas inte den här inställningen i hanteringsprofilen på enheten. Varje gång statusen för personlig hotspot ändras på enheten blockeras **Personlig hotspot** av Intune-tjänsten. Om rapporteringsstatusen i Intune visar att den lyckades vet du att den fungerar, även om inställningen inte visas i hanteringsprofilen på enheten.

- **Regler för mobilanvändning (endast hanterade appar)** : Definiera de datatyper som hanterade appar kan använda i mobilnät. Alternativen är:
  - **Blockera användning av mobildata**: Blockera användningen av mobildata för **Alla hanterade appar** eller **Välj särskilda appar**.
  - **Blockera användning av mobildata vid nätverksväxling**: Blockera användningen av mobildata vid nätverksväxling för **Alla hanterade appar** eller **Välj särskilda appar**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Automatisk enhetsregistrering (övervakad)

- **Ändringar av inställningar för mobildataanvändning**: **Blockera** förhindrar att inställningarna för användning av appmobildata ska kunna ändras. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna bestämmer vilka appar som ska få använda mobildata.
- **Ändringar av mobilabonnemangsinställningar**: **Blockera** hindrar användarna från att ändra inställningar i mobilabonnemanget. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att göra ändringar.

  Den här funktionen gäller för:  
  - iOS 11.0 och senare
  - iPadOS 13.0 och senare

- **Användarändring av Internetdelning**: När inställningen är **Blockera** kan användarna inte ändra inställningen för Internetdelning. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna aktiverar eller inaktiverar sin Internetdelning.

  Om du blockerar den här inställningen och blockerar inställningen **Personlig hotspot** stängs personlig hotspot av.

  Den här funktionen gäller för:  
  - iOS 12.2 och senare
  - iPadOS 13.0 och senare

- **Anslut till trådlösa nätverk med endast konfigurationsprofiler**: **Kräv** tvingar enheten att endast använda trådlösa nätverk som har konfigurerats med Intunes konfigurationsprofiler. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att enheten använder andra Wi-Fi-nätverk.

  När detta anges till **Kräv** bör du se till att enheten har en Wi-Fi-profil. Om du inte tilldelar en Wi-Fi-profil kan den här inställningen hindra enheten från att ansluta till Internet. Om den här profilen för enhetsbegränsningar tilldelas före en Wi-Fi-profil kan enheten alltså blockeras från att ansluta till Internet.
  
  Om den inte kan ansluta avregistrerar du enheten och registrerar den igen med en Wi-Fi-profil. Ange sedan den här inställningen till **Kräv** i en profil för enhetsbegränsningar och tilldela profilen till enheten.

- **Wi-Fi är alltid aktiverat**: När detta anges till **Kräv** förblir Wi-Fi aktiverat i appen Inställningar. Den kan inte inaktiveras i Inställningar eller i Kontrollcenter, även när enheten är i flygplansläge. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard låta användarna styra aktivering eller inaktivering av Wi-Fi.

  Konfiguration av den här inställningen hindrar inte användare från att välja ett Wi-Fi-nätverk.

  Den här funktionen gäller för:  
  - iOS 13.0 och senare
  - iPadOS 13.0 och senare

## <a name="connected-devices"></a>Anslutna enheter

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Handledsavkänning för parkopplad Apple Watch**: **Kräv** tvingar en parkopplad Apple Watch att använda handledsavkänning. När så krävs visar inte Apple Watch meddelanden när den inte bärs runt handleden. 

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Enhetsregistrering, automatisk enhetsregistrering (övervakad)

- **Kräv parkopplingslösenord för utgående AirPlay-förfrågningar**: **Kräv** ett parkopplingslösenord när användarna använder AirPlay för att strömma innehåll till andra Apple-enheter. **Inte konfigurerad** (standard) tillåter att användarna strömmar innehåll med AirPlay utan att behöva ange något lösenord.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Automatisk enhetsregistrering (övervakad)

- **AirDrop**: **Blockera** förhindrar att du använder AirDrop på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att funktionen AirDrop används för att utbyta innehåll med enheter i närheten.
- **Apple Watch-parkoppling**: **Blockera** förhindrar att enheten parkopplas med en Apple Watch. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att enheten parkopplas med en Apple Watch.
- **Bluetooth-ändring**: **Blockera** förhindrar användarna från att ändra enhetens Bluetooth-inställningar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ändra dessa inställningar.
- **Parkoppling av värd för att styra de enheter som en iOS/iPadOS-enhet kan parkopplas till**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta parkoppling så att administratören kan kontrollera vilka enheter som en iOS/iPadOS-enhet kan parkopplas med. **Blockera** förhindrar parkoppling av värd.
- **Blockera AirPrint**: **Blockera** förhindrar att AirPrint-funktionen används på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att använda AirPrint.
  - **Blockera lagring av AirPrint-autentiseringsuppgifter i nyckelringen**: **Blockera** förhindrar användning av nyckelring vid lagring av användarnamn och lösenord på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att AirPrint-användarnamnet och lösenordet lagras i nyckelringsappen.
  - **Kräv ett betrott TLS-certifikat för AirPrint**: **Kräv** tvingar enheten att använda betrodda certifikat för TLS-utskriftskommunikation.
  - **Blockera iBeacon-identifiering av AirPrint-skrivare**: **Blockera** förhindrar skadliga AirPrint Bluetooth-sändare från att nätfiska nätverkstrafik. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta reklam för AirPrint-skrivare på enheten.
- **Blockera inställning av nya enheter i närheten**: **Blockera** inaktiverar uppmaningen om att konfigurera nya enheter som finns i närheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna uppmanas ansluta till andra Apple-enheter i närheten.

  Den här funktionen gäller för:  
  - iOS 11.0 och senare
  - iPadOS 13.0 och senare

- **Åtkomst till filer på USB-enhet**: Enheter kan ansluta till och öppna filer på en USB-enhet. **Inaktivera** förhindrar enhetsåtkomst till USB-enheten i Files-appen när en USB-enhet är ansluten till enheten. Om den här funktionen inaktiveras blockeras även användarna från att överföra filer till en USB-enhet som är ansluten till en iPad. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta åtkomst till en USB-enhet i Files-appen.

  Den här funktionen gäller för:  
  - iOS 13.0 och senare
  - iPadOS 13.0 och senare

## <a name="keyboard-and-dictionary"></a>Tangentbord och ordlista

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Automatisk enhetsregistrering (övervakad)

- **Slå upp definition av ord**: **Blockera** förhindrar användare från att markera ett ord och sedan söka upp dess definition på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard ge åtkomst till definitionssökningsfunktionen.
- **Tangentbord med förslag**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta tangentbord med förslag på ord som användarna kan ha nytta av. **Blockera** förhindrar den här funktionen.
- **Automatisk korrigering**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta enheten att automatiskt korrigera felstavade ord. **Blockera** förhindrar att autokorrigering används.
- **Tangentbord med stavningskontroll**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att stavningskontroll används på enheten. **Blockera** tillåter stavningskontroll.
- **Kortkommandon**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att kortkommandon används på enheten. **Blockera** hindrar användarna från att använda kortkommandon.
- **Diktering**: **Blockera** hindrar användarna från att ange text med hjälp av röstindata. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att använda diktering.
- **QuickPath**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna använder QuickPath, som möjliggör kontinuerlig inmatning på enhetens tangentbord. Användare kan skriva genom att svepa över tangenterna för att skapa ord. **Blockera** förhindrar användare från att använda QuickPath. 

  Den här funktionen gäller för:  
  - iOS 13.0 och senare
  - iPadOS 13.0 och senare

## <a name="cloud-and-storage"></a>Moln och lagring

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Krypterad säkerhetskopiering**: **Kräv** att säkerhetskopior av enheter måste vara krypterade.
- **Synkronisering av hanterade appar till molnet**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att dina Intune-hanterade appar synkroniserar data med användarens iCloud-konto. **Blockera** förhindrar denna datasynkronisering till iCloud.
- **Blockera säkerhetskopiering av företagsbok**: **Blockera** förhindrar användarna från att säkerhetskopiera företagsböcker. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att säkerhetskopiera dessa böcker.
- **Blockera synkronisering av företagsboksmetadata (anteckningar och markeringar)** : **Blockera** förhindrar synkronising av anteckningar och markeringar i företagsböcker. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta synkronisering.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Enhetsregistrering, automatisk enhetsregistrering (övervakad)

- **Synkronisering av bildström till iCloud**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard låta användarna aktivera **My Photo Stream** på sina enheter så att de kan synkronisera med iCloud och låta foton vara tillgängliga på alla sina enheter. **Blockera** förhindrar bildströmssynkronisering till iCloud. Om den här funktionen blockeras kan det leda till dataförlust. 
- **iCloud-bildbiblioteket**: **Blockera** inaktiverar användning av iCloud-bildbiblioteket för att lagra foton och videoklipp i molnet. Alla bilder som inte har laddats ned till fullo från iCloud-bildbiblioteket till enheten tas bort från enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att iCloud-bildbiblioteket används.
- **Delad bildström**: **Blockera** inaktiverar **iCloud-bilddelning** på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta delad direktuppspelning av bilder.
- **Handoff**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att påbörja arbete på en iOS/iPadOS-enhet och sedan fortsätta det arbete som de inledde på en annan iOS/iPadOS- eller macOS-enhet. **Blockera** förhindrar den här överlämningen.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Automatisk enhetsregistrering (övervakad)

- **Säkerhetskopiera till iCloud**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att säkerhetskopiera enheten till iCloud. **Blockera** hindrar användarna från att säkerhetskopiera enheten till iCloud.

  Från och med iOS/iPadOS 13.0 kräver den här inställningen övervakade enheter.

- **Blockera synkronisering av iCloud-dokument**: När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta synkronisering av dokument och nyckelvärden till ditt iCloud-lagringsutrymme. **Blockera** förhindrar iCloud från att synkronisera dokument och data.

  Från och med iOS/iPadOS 13.0 kräver den här inställningen övervakade enheter.

- **Blockera synkronisering av iCloud-nyckelring**: **Blockera** inaktiverar synkronisering till iCloud av autentiseringsuppgifter som lagras i nyckelringen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att synkronisera dessa autentiseringsuppgifter.

  Från och med iOS/iPadOS 13.0 kräver den här inställningen övervakade enheter.

## <a name="autonomous-single-app-mode"></a>Autonomt enkelt appläge

Använd inställningarna för att konfigurera iOS/iPadOS-enheter så att de kör specifika appar i autonomt enkelt appläge. När det här läget har konfigurerats och användaren startar någon av de konfigurerade apparna låses enheten till den appen. Det går inte att byta app/aktivitet förrän användaren avslutar den tillåtna appen.

På en skola eller ett universitet kan du till exempel lägga till en app som gör att användarna kan skriva prov på enheten. Du kan också låsa enheten i företagsportalsappen tills användarna har autentiserats. När appens åtgärder har slutförts av användaren, eller om du tar bort principen, återgår enheten till sitt normala tillstånd.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Automatisk enhetsregistrering (övervakad)

- **Appnamn**: Ange namnet på appen som du vill ha.
- **Appsamlings-ID**: Ange [samlings-ID](bundle-ids-built-in-ios-apps.md) för den önskade appen.
- **Lägg till**: Välj om du vill skapa din lista över appar.

Du kan även **Importera** en CSV-fil med listan över appnamn och deras samlings-ID:n. Eller **exportera** en befintlig lista som innehåller dessa appar.

## <a name="kiosk"></a>Helskärmsläge

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Automatisk enhetsregistrering (övervakad)

- **App som ska köras i helskärmsläge**: Välj den apptyp som du vill köra i helskärmsläge. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Operativsystemets standardinställning kan vara att inte använda inställningarna för helskärmsläge. Enheten körs inte i helskärmsläge.
  - **Store App**: Ange webbadressen till en app i iTunes App Store.
  - **Hanterad app**: Välj en app som du lagt till i Intune.
  - **Inbyggd app**: Ange den inbyggda appens [samlings-ID](bundle-ids-built-in-ios-apps.md).

- **AssistiveTouch**: **Kräv** att hjälpmedelsinställningen för AssistiveTouch ska finnas på enheten. Den här funktionen hjälper användarna med skärmgester som de behöver hjälp med. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemets standardinställning kan vara att inte köra eller aktivera den här funktionen i helskärmsläge.
- **Invertera färger**: **Kräv** att hjälpmedelsinställningen Invertera färger ska användas, så att användare med synsvårigheter kan anpassa skärmen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemets standardinställning kan vara att inte köra eller aktivera den här funktionen i helskärmsläge.
- **Monoljud**: **Kräv** att hjälpmedelsinställningen för Monoljud ska finnas på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemets standardinställning kan vara att inte köra eller aktivera den här funktionen i helskärmsläge.
- **Röststyrning**: **Kräv** aktiverar röststyrning på enheten och gör det möjligt för användare att fullständigt styra operativsystemet med hjälp av Siri-kommandon. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard inaktivera röstkontroll på enheten.

  Den här inställningen gäller för:  
  - iOS 13.0 och senare
  - iPadOS 13.0 och senare
  
  > [!TIP]
  > Om du har LOB-appar tillgängliga för din organisation och de inte är redo för **Röstkontroll** på dag 0 när iOS 13.0 lanseras rekommenderar vi att du låter den här inställningen vara **Inte konfigurerad**.

- **VoiceOver**: **Kräv** att hjälpmedelsinställningen VoiceOver ska finnas på enheten så att text på skärmen kan läsas upp. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemets standardinställning kan vara att inte köra eller aktivera den här funktionen i helskärmsläge.
- **Zooma**: **Kräv** att zoominställningen ska finnas på enheten så att användarna kan använda pekskärmen för att zooma in på skärmen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemets standardinställning kan vara att inte köra eller aktivera den här funktionen i helskärmsläge.
- **Autolås**: **Blockera** förhindrar automatisk låsning av enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta den här funktionen.
- **Ringsignalsknapp**: **Blockera** inaktiverar tyst läge på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta den här funktionen.
- **Skärmrotation**: **Blockera** förhindrar att skärmorienteringen ändras när användaren roterar enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta den här funktionen.
- **Viloläge för skärm-knapp**: **Blockera** inaktiverar vila-/väckningsknappen på enhetens skärm. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta den här funktionen.
- **Touch**: **Blockera** inaktiverar enhetens pekskärm. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att använda pekskärmen.
- **Volymknappar**: **Blockera** förhindrar att enhetens volymknappar används. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta volymknapparna.
- **AssistiveTouch-knapp**: **Tillåt** låter användarna använda funktionen AssistiveTouch. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard inaktivera den här funktionen.
- **Invertera färger-knapp**: **Tillåt** att inställningarna för att invertera färger kan justeras. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard inaktivera den här funktionen.
- **Läs upp markerad text**: **Tillåt** att hjälpmedelsinställningen Läs upp markering finns på enheten. Den här funktionen läser upp den text som användaren väljer. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard inaktivera den här funktionen.
- **Ändring av röststyrning**: **Tillåt** användare att ändra tillståndet för röststyrning på sina enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard blockera användarna från att ändra tillståndet för röstkontroll på sina enheter.

  Den här inställningen gäller för:  
  - iOS 13.0 och senare
  - iPadOS 13.0 och senare

- **VoiceOver-knapp**: **Tillåt** VoiceOver-ändringar så att användarna kan uppdatera VoiceOver-funktionen, t.ex. när det gäller hur snabbt texten ska läsas upp. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra VoiceOver-ändringar.
- **Zoomkontroll**: **Tillåt** att användarna kan ändra zoominställningarna. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard förhindra zoomändringar.

> [!NOTE]
> Innan du kan konfigurera en iOS/iPadOS-enhet för helskärmsläge måste du använda Apple Configurator-verktyget eller Apple-programmet för enhetsregistrereing för att placera enheten i övervakat läge. Information om hur du använder Apple Configurator-verktyget finns i Apples guide.
> Om den iOS/iPadOS-appen som du anger har installerats efter det att du har tilldelat profilen så går inte enheten över i helskärmsläge förrän den startas om.

## <a name="domains"></a>Domains

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Enhetsregistrering, automatisk enhetsregistrering (övervakad)

- **Omarkerade e-postdomäner** > **Webbadress till e-postdomän**: Lägg till en eller flera webbadresser i listan. När användarna får ett e-postmeddelande från en annan domän än någon av de du har angett, så markeras e-postmeddelandet som ej betrott i iOS/iPadOS-e-postappen.

- **Hanterade webbdomäner** > **Webbadress till webbdomän**: Lägg till en eller flera webbadresser i listan. Dokument som laddas ned från de domäner du anger här anses vara hanterade. Den här inställningen gäller enbart för dokument som hämtas i Safari-webbläsaren.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Inställningarna gäller för: Automatisk enhetsregistrering (övervakad)

- **Fyll i lösenord automatiskt på Safari-domäner** > **Domänwebbadress**: Lägg till en eller flera webbadresser i listan. Användarna kan bara spara webblösenord från webbadresser i den här listan. Den här inställningen gäller enbart för Safari-webbläsaren och enheter i övervakat läge. Om du inte anger någon webbadress, kan lösenorden sparas från alla webbplatser.

  Den här inställningen gäller för:  
  - iOS 9.3 och senare
  - iPadOS 13.0 och senare

## <a name="settings-that-require-supervised-mode"></a>Inställningar som kräver övervakat läge

Övervakat läge för iOS/iPadOS kan bara aktiveras under den inledande enhetsinställningen via Apple-programmet för enhetsregistrering eller med hjälp av Apple Configurator. När du har aktiverat övervakat läge kan Intune konfigurera en enhet med följande funktioner:

- Applås (enkelt appläge) 
- Global HTTP-proxy 
- Inaktivera aktiveringslås 
- Autonomt enkelt appläge 
- Webbinnehållsfilter 
- Ange bakgrund och låsskärm 
- Tyst app-push 
- VPN alltid på 
- Tillåt exklusiv installation av hanterad app 
- iBookstore 
- iMessages 
- Spelcenter 
- Airdrop 
- AirPlay 
- Värdkoppling 
- Molnsynkronisering 
- Spotlight-sökning 
- Handoff 
- Radera enhet 
- Begränsningar för gränssnitt 
- Installation av konfigurationsprofiler genom gränssnittet 
- Nyheter 
- Kortkommandon 
- Ändringar av lösenord 
- Ändringar av enhetsnamn 
- Automatisk nedladdning av appar 
- Apple Music 
- Mail Drop 
- Koppla med Apple Watch 

> [!NOTE]
> Apple har bekräftat att vissa inställningar flyttas till endast övervakat läge under 2019. Vi rekommenderar att du tänker på detta när du använder de här inställningarna i stället för att vänta på att Apple ska migrera dem till endast övervakat läge:
>
> - Appinstallation av slutanvändare
> - Borttagning av app
> - FaceTime
> - Safari
> - iTunes
> - Barnförbjudet innehåll
> - Dokument och data i iCloud
> - Spel för flera personer
> - Lägg till Game Center-vänner
> - Siri

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Du kan också begränsa enhetens funktioner och inställningar på [macOS](device-restrictions-macos.md)-enheter.
