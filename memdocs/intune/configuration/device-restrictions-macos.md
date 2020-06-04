---
title: macOS-enhetsinställningar i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Lägg till, konfigurera eller skapa inställningar på macOS-enheter när du vill begränsa funktioner, till exempel lösenordskrav, kontrollera låst skärm, använda inbyggda appar, lägga till begränsade eller godkända appar, hantera bluetooth-enheter, ansluta till molnet för säkerhetskopiering och lagring, aktivera helskärmsläge, lägga till domäner och kontrollera hur användarna samverkar med Safari-webbläsaren i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e48ba131d97e68570f1d6cb85b285ddc3198971c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429755"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>macOS-enhetsinställningar för att tillåta eller begränsa funktioner med hjälp av Intune

I den här artikeln beskrivs de olika inställningar som du kan kontrollera på macOS-enheter. Som en del av din MDM-lösning (hantering av mobilenheter) använder du dessa inställningar för att tillåta eller inaktivera funktioner, ange lösenordsregler, tillåta eller begränsa specifika appar med mera.

Dessa inställningar läggs till en profil för enhetskonfiguration i Intune som sedan tilldelas eller distribueras till dina macOS-enheter.

> [!NOTE]
> Användargränssnittet kanske inte har samma registreringstyper som i den här artikeln. Informationen i den här artikeln är korrekt. Användargränssnittet uppdateras i en kommande version.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en konfigurationsprofil för macOS-enhetsbegränsningar](device-restrictions-configure.md).

> [!NOTE]
> De här inställningarna gäller för olika registreringstyper. Mer information om de olika registreringstyperna finns i [macOS-registrering](../enrollment/macos-enroll.md).

## <a name="built-in-apps"></a>Inbyggda appar

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Blockera autofyll i Safari**: **Ja** inaktiverar funktionen Autofyll i Safari på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användarna ändrar inställningarna för automatisk komplettering i webbläsaren.
- **Blockera kameraanvändning**: **Ja** förhindrar åtkomst till kameran på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta åtkomst till enhetens kamera.

  Intune hanterar endast åtkomst till enhetens kamera. Programmet har inte åtkomst till bilder eller videor.
  
- **Blockera Apple Music**: **Ja** återställer appen Music till klassiskt läge och inaktiverar tjänsten Musik. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att Apple Music-appen används.
- **Blockera spotlight-förslag**: **Ja** förhindrar Spotlight från att returnera resultat från sökningar på internet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta Spotlight-sökningar för att ansluta till Internet och hämta sökresultat.
- **Blockera filöverföring via Finder eller iTunes**: **Ja** inaktiverar fildelningstjänster för program. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta fildelningstjänster för program.

  Den här funktionen gäller för:  
  - macOS 10.13 och senare

## <a name="cloud-and-storage"></a>Moln och lagring

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Blockera synkronisering av iCloud-nyckelring**: **Ja** inaktiverar synkronisering av autentiseringsuppgifter som lagras i nyckelringen till iCloud. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att synkronisera dessa autentiseringsuppgifter.
- **Blockera synkronisering av skrivbord och dokument i iCloud**: **Ja** förhindrar iCloud från att synkronisera dokument och data. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta synkronisering av dokument och nyckelvärden till ditt iCloud-lagringsutrymme.
- **Blockera säkerhetskopiering av Mail i iCloud**: **Ja** förhindrar att iCloud synkroniseras med e-postprogrammet i macOS. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta e-postsynkronisering med iCloud.
- **Blockera säkerhetskopiering av Kontakter i iCloud**: **Ja** förhindrar att iCloud synkroniserar kontakter på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta kontaktsynkronisering med iCloud.
- **Blockera säkerhetskopiering av Kalender i iCloud**: **Ja** förhindrar att iCloud synkroniserar kalenderappen i macOS. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta kalendersynkronisering med iCloud.
- **Blockera säkerhetskopiering av Påminnelser i iCloud**: **Ja** förhindrar att iCloud synkroniserar påminnelseappen i macOS. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta synkronisering av påminnelser med iCloud.
- **Blockera säkerhetskopiering av Bokmärken i iCloud**: **Ja** förhindrar att iCloud synkroniserar enhetens bokmärken. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta synkronisering av bokmärken till iCloud.
- **Blockera säkerhetskopiering av Anteckningar i iCloud**: **Ja** förhindrar att iCloud synkroniserar enhetens anteckningar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta synkronisering av anteckningar till iCloud.
- **Blockera säkerhetskopiering av bilder i iCloud** **Ja** inaktiverar iCloud-bildbiblioteket och förhindrar att iCloud synkroniserar enhetens bilder. Alla bilder som inte har laddats ned till fullo från iCloud-bildbiblioteket tas bort från enheternas lokala lagringsutrymme. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta synkronisering av foton mellan enheten och iCloud-bildbiblioteket.
- **Blockera Handoff**: Funktionen gör det möjligt för användare att påbörja arbete på en macOS-enhet och sedan fortsätta det arbete som de inledde på en annan iOS/iPadOS- eller macOS-enhet. **Ja** förhindrar Handoff-funktionen på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta den här funktionen på enheter.

  Den här funktionen gäller för:  
  - macOS 10.15 och senare

## <a name="connected-devices"></a>Anslutna enheter

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Blockera AirDrop**: **Ja** förhindrar användning av AirDrop på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att funktionen AirDrop används för att utbyta innehåll med enheter i närheten.
- **Blockera automatisk upplåsning av Apple Watch**: **Ja** förhindrar att användaren låser upp en macOS-enhet med Apple Watch. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att användaren låser upp en macOS-enhet med Apple Watch.

## <a name="domains"></a>Domains

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Avmarkerade e-postdomäner**: Ange en eller flera **webbadresser till e-postdomäner** i listan. När användarna skickar eller får ett e-postmeddelande från en annan domän än de du lägger till markeras e-postmeddelandet som ej betrott i e-postprogrammet i macOS.

## <a name="general"></a>Allmänt

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Blockera sökning**: **Ja** förhindrar att användare markerar ett ord och sedan söker upp dess definition på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta definitionssökningsfunktionen.
- **Blockera diktering**: **Ja** förhindrar att användarna anger text med hjälp av röstindata. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att använda diktering.
- **Blockera innehållscachelagring**: **Ja** förhindrar cachelagring av innehåll. Innehållscachelagring lagrar till exempel appdata, data i webbläsaren och nedladdningar lokalt på enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard aktivera innehållscachelagring.

  Mer information om cachelagring av innehåll på macOS finns i [Hantera cachelagring av innehåll på Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (en annan webbplats öppnas).

  Den här funktionen gäller för:  
  - macOS 10.13 och senare

- **Skjut upp programuppdateringar**: **Ja** gör att du kan skjuta upp när programuppdateringar visas på enheter i 0–90 dagar. Den här inställningen styr inte när uppdateringar installeras eller inte. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa uppdateringar på enheter när Apple släpper dem. Om Apple exempelvis ger ut en macOS-uppdatering på ett specifikt datum, visas uppdateringen på enheter runt utgivningsdatumet. Startuppsättningar av versionsuppdateringar tillåts utan fördröjning.  

  - **Fördröj visning av programuppdateringar**: Ange ett värde mellan 0–90 dagar. När fördröjningen upphör får användarna ett meddelande om att uppdatera till den tidigaste versionen av OS som var tillgänglig när fördröjningen utlöstes.

    Exempel: Om en macOS-uppdatering är tillgänglig **den 1 januari** och **Fördröjd visning** är inställt på **5 dagar**, så visas inte uppdateringen som en tillgänglig uppdatering. På **den sjätte dagen** efter utgivningen är uppdateringen tillgänglig och användarna kan installera den.

    Den här funktionen gäller för:  
    - macOS 10.13.4 och senare

- **Blockera skärmbilder och skärminspelning**: Enheten måste vara registrerad i Apples automatiska enhetsregistrering (DEP). **Ja** förhindrar att användare sparar skärmdumpar. Det förhindrar också att appen Klassrum styr fjärrskärmar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att användare samlar in skärmbilder och tillåter appen Klassrum att visa fjärrskärmar.

  - **Inaktivera AirPlay, visning av skärm via appen Klassrum och skärmdelning**: **Ja** blockerar AirPlay och förhindrar skärmdelning med andra enheter. Dessutom förhindras lärare från att använda appen Klassrum till att se elevernas skärmar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att lärare ser sina elevers skärmar.

    Om du vill använda den här inställningen anger du inställningen **Blockera skärmbilder och skärminspelning** till **Inte konfigurerad** (skärmbilder tillåts).

  - **Tillåt appen Klassrum att utföra AirPlay och skärmvisning utan att fråga**: **Ja** gör att lärare kan se elevernas skärmar utan att behöva elevernas medgivande. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativ systemet kräva att eleverna accepterar innan lärare kan se skärmarna.

    Om du vill använda den här inställningen anger du inställningen **Blockera skärmbilder och skärminspelning** till **Inte konfigurerad** (skärmbilder tillåts).

- **Kräv lärartillstånd för att lämna ohanterade klasser i appen Klassrum**: **Ja** tvingar elever som är registrerade i en ohanterad kurs i Klassrum att få ett godkännande från läraren att lämna kursen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att eleverna lämnar lektionen när de vill.

- **Tillåt Klassrum att låsa enheten utan att fråga**: **Ja** låter lärare låsa en elevs enhet eller app utan elevens godkännande. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet kräva att eleverna accepterar lärare kan låsa enheten eller appen.

- **Elever kan delta automatiskt i Klassrum-lektioner utan fråga**: **Ja** låter elever delta i en lektion utan att fråga läraren. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet kräva en lärares godkännande för anslutning till en lektion.

## <a name="password"></a>lösenordsinställning

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Kräv lösenord**: **Ja** tvingar användarna att ange lösenord för att få åtkomst till enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kräver operativsystemet inte alltid lösenord. Det gäller inte heller några begränsningar, till exempel att blockera enkla lösenord eller att ange en minsta längd.
  - **Lösenordstyp som krävs**: Ange den nivå av lösenordskomplexitet som krävs för din organisation. När värdet är tomt varken ändrar eller uppdaterar Intune den här inställningen. Alternativen är:
    - **Inte konfigurerad**: Enhetens standardvärde används.
    - **Alfanumeriskt**: Innehåller versaler, gemener och numeriska tecken.
    - **Numeriskt**: Lösenordet får bara innehålla siffror, till exempel 123456789.

    Den här funktionen gäller för:  
    - macOS 10.10.3 och senare

  - **Antal icke-alfanumeriska tecken i lösenord**: Ange det antal avancerade tecken som krävs i lösenordet, från 0–4. Ett avancerat tecken är en symbol, till exempel `?`. När värdet lämnas tomt eller anges till **Inte konfigurerad** ändrar eller uppdaterar inte Intune den här inställningen.
  - **Minsta lösenordslängd**: Ange den minsta längd som lösenordet måste ha (mellan 4 och 16 tecken). När värdet är tomt varken ändrar eller uppdaterar Intune den här inställningen.
  - **Blockera enkla lösenord**: **Ja** förhindrar användning av enkla lösenord som `0000` eller `1234`. Om värdet är tomt eller inställt på **Inte konfigurerad**, ändrar eller uppdaterar Intune inte inställningen. Operativsystemet kan som standard tillåta enkla lösenord.
  - **Maximalt antal minuter av inaktivitet innan skärmen låses**: Ange hur lång tid enheterna måste vara inaktiva innan skärmen låses automatiskt. Ange till exempel `5` om du vill låsa enheter efter 5 minuters inaktivitet. Om värdet är tomt eller inställt på **Inte konfigurerad**, ändrar eller uppdaterar Intune inte inställningen.
  - **Maximalt antal minuter efter skärmlås innan ett lösenord krävs**: Ange hur länge enheter måste vara inaktiva innan ett lösenord krävs för att låsa upp dem. Om värdet är tomt eller inställt på **Inte konfigurerad**, ändrar eller uppdaterar Intune inte inställningen.
  - **Lösenordets giltighetstid (dagar)** : Ange antalet dagar innan lösenordet måste ändras (från 1 till 65535 dagar). Ange till exempel `90` om lösenordet ska upphöra efter 90 dagar. När lösenordet upphör att gälla uppmanas användarna att skapa ett nytt lösenord. Om värdet är tomt eller inställt på **Inte konfigurerad**, ändrar eller uppdaterar Intune inte inställningen.
  - **Förhindra återanvändning av tidigare lösenord**: Förhindra att användare återanvänder tidigare använda lösenord. Ange antal tidigare använda lösenord som inte får återanvändas, från 1–24. Ange till exempel 5 om användare inte ska kunna ange ett nytt lösenord till sina nuvarande lösenord eller något av de föregående fyra lösenorden. Intune varken ändrar eller uppdaterar den här inställningen om värdet lämnas tomt.

- **Blockera användare från att ändra lösenkod**: **Ja** förhindrar att lösenord ändras, läggs till eller tas bort. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att lösenord läggs till, ändras eller tas bort.

- **Blockera Touch ID för att låsa upp enhet**: **Ja** förhindrar att fingeravtryck används till att låsa upp enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att låsa upp enheten med hjälp av fingeravtryck.

- **Blockera automatisk ifyllning av lösenord**: **Ja** förhindrar användningen av funktionen för automatisk ifyllning av lösenord i macOS. Inställningen **Ja** har också följande effekt:

  - Användarna ombeds inte att använda ett sparat lösenord i Safari eller i någon app.
  - Automatisk starka lösenord inaktiveras och starka lösenord föreslås inte för användare.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta de här funktionerna.

- **Blockera förfrågningar om lösenordsnärhet**: **Ja** förhindrar att enheter begär lösenord från enheter i närheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta de här funktionerna.

- **Blockera lösenordsdelning**: **Ja** förhindrar att lösenord delas mellan enheter med hjälp av AirDrop. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att dessa data skickas.

## <a name="privacy-preferences"></a>Sekretessinställningar

På macOS-enheter uppmanar appar och processer ofta användarna att tillåta eller neka åtkomst till enhetsfunktioner som kameran, mikrofonen, kalendern och dokumentmappen. Med de här inställningarna kan administratörer godkänna eller neka åtkomst till sådana enhetsfunktioner i förväg. När du konfigurerar de här inställningarna hanterar du godkännandet av dataåtkomst åt användarna. Dina inställningar åsidosätter deras tidigare beslut.

Målet med de här inställningarna är att minska antalet uppmaningar från appar och processer.

Den här funktionen gäller för:

- macOS 10.14 och senare
- Vissa inställningar gäller för macOS 10.15 och senare.
- De här inställningarna gäller endast för enheter som har profilen för sekretessinställningar installerad innan uppgraderingen.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Inställningarna gäller för: Enhetsregistrering som användaren godkänner, automatisk enhetsregistrering

- **Appar och processer**: **Lägg till** appar eller processer för att konfigurera åtkomsten. Ange även:
  - **Namn**: Ange ett namn för appen eller processen. Ange till exempel `Microsoft Remote Desktop` eller `Microsoft Office 365`.
  
  - **Typ av identifierare**: Alternativen är:
    - **Samlings-ID**: Välj det här alternativet för appar.
    - **Sökväg**: Välj det här alternativet för icke-paketerade binärfiler som är en process eller körbar fil.

    Hjälpverktyg som bäddats in i ett programpaket ärver automatiskt behörigheterna från det överordnade programpaketet.

  - **Identifierare**: Ange programpaketets ID eller installationssökvägen för processen eller den körbara filen. Ange till exempel `com.contoso.appname`.

    Hämta programpaket-ID:t genom att öppna appen Terminal och köra kommandot `codesign`. Det här kommandot identifierar kodsignaturen. Då kan du hämta paket-ID:t och kodsignaturen samtidigt.

  - **Kodkrav**: Ange kodsignaturen för programmet eller processen.

    En kodsignatur skapas när en app eller en binärfil signeras med ett utvecklarcertifikat. Du hittar beteckningen genom att köra kommandot `codesign` manuellt i appen Terminal: `codesign --display -r -/path/to/app/binary`. Kodsignaturen är allt som står efter `=>`.

  - **Aktivera verifiering av statisk kod**: Välj **Ja** om appen eller processen ska validera kodkravet statiskt. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen.

    Aktivera bara den här inställningen om processen gör den dynamiska kodsignaturen ogiltig. Annars använder du **Inte konfigurerad**.  

  - **Blockera kamera**: **Ja** förhindrar appens åtkomst till systemets kamera. Du kan inte tillåta åtkomst till kameran. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen.

  - **Blockera mikrofon**: **Ja** förhindrar appens åtkomst till systemets mikrofon. Du kan inte tillåta åtkomst till mikrofonen. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen.

  - **Blockera skärminspelning**: **Ja** blockerar appen från att fånga innehållet på systemets skärm. Du kan inte tillåta åtkomst till skärminspelning eller skärmdumpar. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen.

    Kräver macOS 10.15 eller senare.

  - **Blockera övervakning av indata**: **Ja** blockerar appen från att använda API:erna CoreGraphics och HID till att lyssna på CGEvents och HID-händelser från alla processer. **Ja** förhindrar även att appar och processer lyssnar till och samlar in data från indataenheter som en mus, ett tangentbord eller en trackpad. Du kan inte tillåta åtkomst till API:erna CoreGraphics och HID.

    När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen.

    Kräver macOS 10.15 eller senare.

  - **Taligenkänning**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter att appen får tillgång till systemets taligenkänning och gör det möjligt att skicka taldata till Apple.
    - **Blockera**: Förhindrar appens åtkomst till systemets taligenkänning och förhindrar att taldata skickas till Apple.

    Kräver macOS 10.15 eller senare.

  - **Hjälpmedel**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter att appen får tillgång till systemappen Tillgänglighet. Den här appen innehåller funktioner för undertexter, hovringstext och röststyrning.
    - **Blockera**: Förhindrar appens åtkomst till systemappen Tillgänglighet.

  - **Kontakter**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter att appen får åtkomst till kontaktinformation som hanteras av systemappen Kontakter.  
    - **Blockera**: Förhindrar appens åtkomst till den här kontaktinformationen.

  - **Kalender**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter att appen får åtkomst till kalenderinformation som hanteras av systemappen Kalender.
    - **Blockera**: Förhindrar appens åtkomst till den här kalenderinformationen.

  - **Påminnelser**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter att appen får åtkomst till information om påminnelser som hanteras av systemappen Påminnelser.
    - **Blockera**: Förhindrar appens åtkomst till den här informationen om påminnelser.

  - **Foton**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter att appen får åtkomst till bilder som hanteras av systemappen Foton i `~/Pictures/.photoslibrary`.
    - **Blockera**: Förhindrar appens åtkomst till de här bilderna.

  - **Mediebibliotek**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter appen att komma åt Apple Music, musik- och videoaktivitet samt mediebiblioteket.  
    - **Blockera**: Förhindrar appens åtkomst till de här medierna.

    Kräver macOS 10.15 eller senare.

  - **Närvaro av filleverantör**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter appen att komma åt appen Filleverantör och att identifiera när användare använder filer som hanteras av Filleverantör. En Filleverantör-app gör att andra Filleverantör-appar kan komma åt dokument och kataloger som lagras och hanteras av den aktuella appen.
    - **Blockera**: Förhindrar appens åtkomst till appen Filleverantör.

    Kräver macOS 10.15 eller senare.

  - **Fullständig diskåtkomst**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter appen att komma åt alla skyddade filer, inklusive systemadministrationsfiler. Var försiktig när du använder den här inställningen.
    - **Blockera**: Förhindrar appens åtkomst till de här skyddade filerna.

  - **Systemadministrationsfiler**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter att appen får åtkomst till vissa filer som används i systemadministrationen.
    - **Blockera**: Förhindrar appens åtkomst till de här filerna.

  - **Mappen Skrivbord**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter appen att komma åt filer i användarmappen Skrivbord.
    - **Blockera**: Förhindrar appens åtkomst till de här filerna.

    Kräver macOS 10.15 eller senare.

  - **Mappen Dokument**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter appen att komma åt filer i användarmappen Dokument.
    - **Blockera**: Förhindrar appens åtkomst till de här filerna.

    Kräver macOS 10.15 eller senare.

  - **Mappen Nedladdningar**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter appen att komma åt filer i användarmappen Nedladdningar.
    - **Blockera**: Förhindrar appens åtkomst till de här filerna.

    Kräver macOS 10.15 eller senare.

  - **Nätverksvolymer**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter att appen får åtkomst till filer på nätverksvolymer.
    - **Blockera**: Förhindrar appens åtkomst till de här filerna.

    Kräver macOS 10.15 eller senare.

  - **Flyttbara volymer**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter att appen får åtkomst till filer på flyttbara volymer, till exempel hårddiskar.
    - **Blockera**: Förhindrar appens åtkomst till de här filerna.

    Kräver macOS 10.15 eller senare.

  - **Systemhändelser**: Alternativen är:
    - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
    - **Tillåt**: Tillåter appen att använda CoreGraphics-API:er till att skicka CGEvents till strömmen med systemhändelser.
    - **Blockera**: Förhindrar att appen använder CoreGraphics-API:er till att skicka CGEvents till strömmen med systemhändelser.

  - **Apple-händelser**: Med den här inställningen kan appar skicka en begränsad Apple-händelse till en annan app eller process. Välj **Lägg till** för att lägga till en app eller process som mottagare. Ange följande information om den mottagande appen eller processen:

    - **Typ av identifierare**: Välj **Paket-ID** om mottagaren är ett program. Välj **Sökväg** om mottagaren är en process eller körbar fil.
    
    - **Identifierare**: Ange programpaketets ID eller installationssökvägen för processen som ska ta emot en Apple-händelse.  

    - **Kodkrav**: Ange kodsignaturen för den mottagande appen eller processen.

      En kodsignatur skapas när en app eller en binärfil signeras med ett utvecklarcertifikat. Du hittar beteckningen genom att köra kommandot `codesign` manuellt i appen Terminal: `codesign --display -r -/path/to/app/binary`. Kodsignaturen är allt som står efter `=>`.

    - **Åtkomst**: Tillåt att en macOS Apple-händelse skickas till den mottagande appen eller processen. Alternativen är:
      - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen.
      - **Tillåt**: Tillåter att appen eller processen skickar den begränsade Apple-händelsen till den mottagande appen eller processen.
      - **Blockera**: Förhindrar att appen eller processen skickar en begränsad Apple-händelse till den mottagande appen eller processen.

  - **Spara** ändringarna.

## <a name="restricted-apps"></a>Begränsade appar

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Lista över typer av begränsade appar**: Skapa en lista över appar som användarna inte får installera eller använda. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Användare kan som standard få åtkomst till appar som du tilldelar samt inbyggda appar.
  - **Godkända appar**: Ange de appar som användare tillåts att installera. Om användarna vill fortsätta följa standard får de inte installera andra appar. Appar som hanteras av Intune tillåts automatiskt. Det gäller även företagsportalsappen. Användarna hindras inte från att installera en app som inte finns med i listan över godkända appar. Men om de gör det rapporteras det i Intune.
  - **Otillåtna appar**: Ange de appar (som inte hanteras av Intune) som användarna inte får installera eller köra. Användare hindras inte från att installera en förbjuden app. Om en användare installerar en app från den här listan rapporteras det i Intune.

- **Applista**: **Lägg till** appar i listan:
  - **Appsamlings-ID**: Ange appens [samlings-ID](bundle-ids-built-in-ios-apps.md). Du kan lägga till inbyggda appar och verksamhetsspecifika appar. På Apple-webbplatsen finns en lista med [inbyggda Apple-appar](https://support.apple.com/HT208094).

    Du hittar webbadressen till en app genom att öppna iTunes App Store och söka efter appen. Du kan t.ex. söka efter `Microsoft Remote Desktop` eller `Microsoft Word`. Välj appen och kopiera webbadressen. Du kan även använda iTunes för att hitta appen och sedan använda uppgiften **Kopiera länk** för att hämta appens webbadress.

  - **Appnamn**: Ange ett användarvänligt namn som hjälper dig att identifiera samlings-ID:t. Ange till exempel `Intune Company Portal app`.
  - **Utgivare**: Ange appens utgivare.

- **Importera** en CSV-fil med information om appen, inklusive webbadressen. Använd formatet `<app bundle ID>, <app name>, <app publisher>`. Eller välj **Exportera** om du vill skapa en lista över appar som du har lagt till, i samma format.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Du kan också begränsa enhetens funktioner och inställningar på [iOS/iPadOS](device-restrictions-ios.md)-enheter.
