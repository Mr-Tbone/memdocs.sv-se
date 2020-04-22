---
title: macOS-enhetsinställningar i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Lägg till, konfigurera eller skapa inställningar på macOS-enheter när du vill begränsa funktioner, till exempel lösenordskrav, kontrollera låst skärm, använda inbyggda appar, lägga till begränsade eller godkända appar, hantera bluetooth-enheter, ansluta till molnet för säkerhetskopiering och lagring, aktivera helskärmsläge, lägga till domäner och kontrollera hur användarna samverkar med Safari-webbläsaren i Microsoft Intune.
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
ms.openlocfilehash: 50dd3d245b9a89836e3858d71a7ad124189e0973
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80407851"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>macOS-enhetsinställningar för att tillåta eller begränsa funktioner med hjälp av Intune

I den här artikeln beskrivs de olika inställningar som du kan kontrollera på macOS-enheter. Som en del av din MDM-lösning (hantering av mobilenheter) använder du dessa inställningar för att tillåta eller inaktivera funktioner, ange lösenordsregler, tillåta eller begränsa specifika appar med mera.

Dessa inställningar läggs till en profil för enhetskonfiguration i Intune som sedan tilldelas eller distribueras till dina macOS-enheter.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en konfigurationsprofil för enhetsbegränsningar](device-restrictions-configure.md).

> [!NOTE]
> De här inställningarna gäller för olika registreringstyper. Mer information om de olika registreringstyperna finns i [macOS-registrering](../enrollment/macos-enroll.md).

## <a name="general"></a>Allmänt

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Inställningarna gäller för: Enhetsregistrering och automatisk enhetsregistrering

- **Slå upp definition**: **Blockera** förhindrar användare från att markera ett ord och sedan söka upp dess definition på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta definitionssökningsfunktionen.
- **Diktering**: **Blockera** hindrar användarna från att ange text med hjälp av röstindata. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att använda diktering.
- **Cachelagring av innehåll**: **Blockera** förhindrar innehållscachelagring. Innehållscachelagring lagrar till exempel appdata, data i webbläsaren och nedladdningar lokalt på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard aktivera innehållscachelagring.

  Mer information om cachelagring av innehåll på macOS finns i [Hantera cachelagring av innehåll på Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (en annan webbplats öppnas).

  Den här funktionen gäller för:  
  - macOS 10.13 och senare

- **Skjut upp programuppdateringar**: **Aktivera** gör att du kan skjuta upp visningen av programuppdateringar på enheter i 0–90 dagar. Den här inställningen styr inte när uppdateringar installeras eller inte. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa uppdateringar på enheter när Apple släpper dem. Om Apple exempelvis ger ut en macOS-uppdatering på ett specifikt datum, visas uppdateringen på enheter runt utgivningsdatumet. Startuppsättningar av versionsuppdateringar tillåts utan fördröjning.  

  - **Fördröj visning av programuppdateringar**: Ange ett värde mellan 0–90 dagar. När fördröjningen upphör får användarna ett meddelande om att uppdatera till den tidigaste versionen av OS som var tillgänglig när fördröjningen utlöstes.

    Exempel: Om en macOS-uppdatering är tillgänglig **den 1 januari** och **Fördröjd visning** är inställt på **5 dagar**, så visas inte uppdateringen som en tillgänglig uppdatering. På **den sjätte dagen** efter utgivningen är uppdateringen tillgänglig och användarna kan installera den.

    Den här funktionen gäller för:  
    - macOS 10.13.4 och senare

- **Skärmbilder**: Enheten måste vara registrerad i Apples automatiska enhetsregistrering (DEP). **Blockera** förhindrar att användare sparar skärmdumpar av skärmen. Det förhindrar också att appen Klassrum styr fjärrskärmar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att användare samlar in skärmbilder och tillåter appen Klassrum att visa fjärrskärmar.

### <a name="settings-apply-to-automated-device-enrollment"></a>Inställningarna gäller för: Automatisk enhetsregistrering

- **Fjärrstyrd skärm genom appen Klassrum**: **Inaktivera** hindrar lärare från att använda appen Klassrum för att se sina studenters skärmar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att lärare ser sina elevers skärmar.

  Om du vill använda den här inställningen anger du inställningen **Skärmbilder** till **Inte konfigurerad** (skärmbilder tillåts).

- **Skärmvisning utan uppmaning via appen Klassrum**: **Tillåt** ger lärare möjlighet att se sina elevers skärmar utan att behöva elevernas medgivande. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativ systemet kräva att eleverna accepterar innan lärare kan se skärmarna.

  Om du vill använda den här inställningen anger du inställningen **Skärmbilder** till **Inte konfigurerad** (skärmbilder tillåts).

- **Studenter måste begära tillstånd att lämna klassrum-klass**: **Kräv** tvingar studenter som är registrerade i en ohanterad klassrum-klass att få ett godkännande från läraren att lämna klassen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att eleverna lämnar lektionen när de vill.

- **Lärare kan låsa enheter och appar i appen Klassrum automatiskt**: **Tillåt** låter lärare låsa en studerandes enhet eller app utan den studerandes godkännande. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet kräva att eleverna accepterar lärare kan låsa enheten eller appen.

- **Studerande kan delta automatiskt i Klassrum-klasser**: **Tillåt** låter studerande delta i en lektion utan att tillkalla läraren. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet kräva en lärares godkännande för anslutning till en lektion.

## <a name="password"></a>lösenordsinställning

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Inställningarna gäller för: Enhetsregistrering och automatisk enhetsregistrering

- **Lösenord**: **Kräv** att användarna anger sina lösenord för att få åtkomst till enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kräver operativsystemet inte alltid lösenord. Det gäller inte heller några begränsningar, till exempel att blockera enkla lösenord eller att ange en minsta längd.
  - **Lösenordstyp som krävs**: Ange den nivå av lösenordskomplexitet som krävs för din organisation. Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Numeriskt**: Lösenordet får bara innehålla siffror, till exempel 123456789.
    - **Alfanumeriskt**: Innehåller versaler, gemener och numeriska tecken.

    Den här funktionen gäller för:  
    - macOS 10.10.3 och senare

  - **Antal icke-alfanumeriska tecken i lösenord**: Ange det antal avancerade tecken som krävs i lösenordet, från 0–4. Ett avancerat tecken är en symbol, till exempel `?`
  - **Minsta lösenordslängd**: Ange den minsta längd som lösenordet måste ha (mellan 4 och 16 tecken).
  - **Enkla lösenord**: Tillåt användning av enkla lösenord, till exempel `0000` eller `1234`.
  - **Maximalt antal minuter efter skärmlås innan ett lösenord krävs**: Ange hur länge enheter måste vara inaktiva innan ett lösenord krävs för att låsa upp dem. Om värdet är tomt eller inställt på **Inte konfigurerad**, ändrar eller uppdaterar Intune inte inställningen.
  - **Maximalt antal minuter av inaktivitet innan skärmen låses**: Anger hur lång tid enheterna måste vara inaktiva innan skärmen låses automatiskt. Ange till exempel 5 om du vill låsa enheter efter 5 minuters inaktivitet. Om värdet är tomt eller inställt på **Inte konfigurerad**, ändrar eller uppdaterar Intune inte inställningen.
  - **Lösenordets giltighetstid (dagar)** : Ange antalet dagar innan lösenordet måste ändras (från 1 till 65535 dagar). Ange till exempel `90` om lösenordet ska upphöra efter 90 dagar. När lösenordet upphör att gälla uppmanas användarna att skapa ett nytt lösenord. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.
  - **Förhindra återanvändning av tidigare lösenord**: Använd den här inställningen för att förhindra att användare återanvänder tidigare använda lösenord. Ange antal tidigare använda lösenord som inte får återanvändas, från 1–24. Ange till exempel 5 om användare inte ska kunna ange ett nytt lösenord till sina nuvarande lösenord eller något av de föregående fyra lösenorden. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.

- **Blockera användare från att ändra lösenkod**: **Blockera** förhindrar att lösenord ändras, läggs till eller tas bort. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att lösenord läggs till, ändras eller tas bort.
- **Blockera upplåsning med fingeravtryck**: **Blockera** förhindrar att fingeravtryck används för att låsa upp enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att låsa upp enheten med hjälp av fingeravtryck.

- **Blockera automatisk ifyllning av lösenord**: **Blockera** förhindrar användningen av funktionen för automatisk ifyllning av lösenord i macOS. Inställningen **Blockera** har också följande effekt:

  - Användarna ombeds inte att använda ett sparat lösenord i Safari eller i någon app.
  - Automatisk starka lösenord inaktiveras och starka lösenord föreslås inte för användare.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta de här funktionerna.

- **Blockera förfrågningar om lösenordsnärhet**: **Blockera** förhindrar att enheter begär lösenord från enheter i närheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta de här funktionerna.

- **Blockera lösenordsdelning**: **Blockera** förhindrar att lösenord delas mellan enheter med hjälp av AirDrop. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att dessa data skickas.

## <a name="built-in-apps"></a>Inbyggda appar

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Inställningarna gäller för: Enhetsregistrering och automatisk enhetsregistrering

- **Blockera autofyll i Safari**: **Blockera** inaktiverar funktionen Autofyll i Safari på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna ändrar inställningarna för automatisk komplettering i webbläsaren.
- **Blockera kamera**: **Blockera** förhindrar åtkomst till kameran på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta åtkomst till enhetens kamera.

  Intune hanterar endast åtkomst till enhetens kamera. Programmet har inte åtkomst till bilder eller videor.

- **Blockera Apple Music**: **Blockera** återställer appen Apple Music till klassiskt läge och inaktiverar tjänsten Musik. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att Apple Music-appen används.
- **Blockera Internetsökresultat i Spotlight**: **Blockera** förhindrar Spotlight från att returnera resultat från sökningar på Internet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta Spotlight-sökningar för att ansluta till Internet och hämta sökresultat.
- **Blockera filöverföring via iTunes**: **Blockera** inaktiverar fildelningstjänster för program. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta fildelningstjänster för program.

  Den här funktionen gäller för:  
  - macOS 10.13 och senare

## <a name="restricted-apps"></a>Begränsade appar

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Inställningarna gäller för: Enhetsregistrering och automatisk enhetsregistrering

- **Lista över typer av begränsade appar**: Skapa en lista över appar som användarna inte får installera eller använda. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Användare kan som standard få åtkomst till appar som du tilldelar samt inbyggda appar.
  - **Otillåtna appar**: Ange de appar (som inte hanteras av Intune) som användarna inte får installera eller köra. Användare hindras inte från att installera en förbjuden app. Om en användare installerar en app från den här listan rapporteras det i Intune.
  - **Godkända appar**: Ange de appar som användare tillåts att installera. Om användarna vill fortsätta följa standard får de inte installera andra appar. Appar som hanteras av Intune tillåts automatiskt. Det gäller även företagsportalsappen. Användarna hindras inte från att installera en app som inte finns med i listan över godkända appar. Men om de gör det rapporteras det i Intune.

- **Appsamlings-ID**: Ange [appsamlings-ID](bundle-ids-built-in-ios-apps.md) för den app som du vill lägga till. Du kan visa eller dölja inbyggda appar och verksamhetsspecifika appar. På Apple-webbplatsen finns en lista med [inbyggda Apple-appar](https://support.apple.com/HT208094).
- **Appnamn**: Ange namnet på den app som du vill lägga till. Du kan visa eller dölja inbyggda appar och verksamhetsspecifika appar. På Apple-webbplatsen finns en lista med [inbyggda Apple-appar](https://support.apple.com/HT208094).
- **Utgivare**: Ange appens utgivare.

Om du vill lägga till appar i listorna kan du:

- **Lägg till**: Välj om du vill skapa din lista över appar.
- **Importera** en CSV-fil med information om appen, inklusive webbadressen. Använd formatet `<app bundle ID>, <app name>, <app publisher>`. Eller välj **Exportera** om du vill skapa en lista över appar som du har lagt till, i samma format.

## <a name="connected-devices"></a>Anslutna enheter

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Inställningarna gäller för: Enhetsregistrering och automatisk enhetsregistrering

- **Blockera AirDrop**: **Blockera** förhindrar användning av AirDrop på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att funktionen AirDrop används för att utbyta innehåll med enheter i närheten.
- **Blockera automatisk upplåsning av Apple Watch**: **Blockera** hindrar användaren från att låsa upp en macOS-enhet med Apple Watch. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användaren låser upp en macOS-enhet med Apple Watch.

## <a name="cloud-and-storage"></a>Moln och lagring

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Inställningarna gäller för: Enhetsregistrering och automatisk enhetsregistrering

- **Blockera synkronisering av iCloud-nyckelring**: **Blockera** inaktiverar synkronisering till iCloud av autentiseringsuppgifter som lagras i nyckelringen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att synkronisera dessa autentiseringsuppgifter.
- **Blockera synkronisering av iCloud-dokument**: **Blockera** förhindrar iCloud från att synkronisera dokument och data. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta synkronisering av dokument och nyckelvärden till ditt iCloud-lagringsutrymme.
- **Blockera säkerhetskopiering av Mail i iCloud**: **Blockera** förhindrar att iCloud synkroniseras med e-postprogrammet i macOS. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta e-postsynkronisering med iCloud.
- **Blockera säkerhetskopiering av Kontakter i iCloud**: **Blockera** förhindrar att iCloud synkroniserar kontakter på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta kontaktsynkronisering med iCloud.
- **Blockera säkerhetskopiering av Kalender i iCloud**: **Blockera** förhindrar att iCloud synkroniserar kalenderappen i macOS. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta kalendersynkronisering med iCloud.
- **Blockera säkerhetskopiering av Påminnelser i iCloud**: **Blockera** förhindrar att iCloud synkroniserar påminnelseappen i macOS. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta synkronisering av påminnelser med iCloud.
- **Blockera säkerhetskopiering av Bokmärken i iCloud**: **Blockera** förhindrar att iCloud synkroniserar enhetens bokmärken. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta synkronisering av bokmärken till iCloud.
- **Blockera säkerhetskopiering av Anteckningar i iCloud**: **Blockera** förhindrar att iCloud synkroniserar enhetens anteckningar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta synkronisering av anteckningar till iCloud.
- **Blockera iCloud-bildbibliotek**: **Blockera** inaktiverar iCloud-bildbiblioteket och förhindrar att iCloud synkroniserar enhetens bilder. Alla bilder som inte har laddats ned till fullo från iCloud-bildbiblioteket tas bort från enheternas lokala lagringsutrymme. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta synkronisering av foton mellan enheten och iCloud-bildbiblioteket.
- **Handoff**: Funktionen gör det möjligt för användare att påbörja arbete på en macOS-enhet och sedan fortsätta det arbete som de inledde på en annan iOS/iPadOS- eller macOS-enhet. **Blockera** förhindrar Handoff-funktionen på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta den här funktionen på enheter.

  Den här funktionen gäller för:  
  - macOS 10.15 och senare

## <a name="domains"></a>Domains

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Inställningarna gäller för: Enhetsregistrering och automatisk enhetsregistrering

- **Webbadress till e-postdomän**: **Lägg till** en eller flera webbadresser i listan. När slutanvändarna får ett e-postmeddelande från en annan domän än den du har konfigurerat, markeras e-postmeddelandet som ej betrott i macOS-e-postappen.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Du kan också begränsa enhetens funktioner och inställningar på [iOS/iPadOS](device-restrictions-ios.md)-enheter.
