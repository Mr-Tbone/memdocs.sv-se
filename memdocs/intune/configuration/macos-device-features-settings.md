---
title: Funktionsinställningar för macOS-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Se inställningarna för att konfigurera macOS-enheter för AirPrint och anpassa inloggningsfönstret för att visa eller dölja strömknappar i Microsoft Intune. Se även anvisningar för att hämta IP-adress, sökväg och portinställningar för en AirPrint-server i nätverket. Använd dessa inställningar i en enhetskonfigurationsprofil när du konfigurerar funktioner för macOS-enheter.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 79c389767ad3cb796e2cc7b4cd9a35015e17a837
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88819668"
---
# <a name="macos-device-feature-settings-in-intune"></a>Funktionsinställningar för macOS-enheter i Intune

I Intune finns inbyggda inställningar för att anpassa funktioner i dina macOS-enheter. Administratörer kan exempelvis lägga till AirPrint-skrivare, välja hur användare ska logga in, konfigurera energikontrollerna, använda autentisering med enkel inloggning och mycket annat.

Du kan använda dessa funktioner för att styra macOS-enheter som en del av din MDM-lösning för hantering av mobilenheter.

I den här artikeln visas inställningarna, tillsammans med en beskrivning av vad varje inställning gör. Här visas även anvisningar för att hämta IP-adress, sökväg och port för AirPrint-skrivare som använder Terminal-appen (emulator). Om du vill ha mer information om enhetsfunktionerna går du till [Lägg till funktionsinställningar för iOS/iPadOS- eller macOS-enhet](device-features-configure.md).

> [!NOTE]
> Användargränssnittet kanske inte har samma registreringstyper som i den här artikeln. Informationen i den här artikeln är korrekt. Användargränssnittet uppdateras i en kommande version.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en profil för macOS-enhetsfunktioner](device-features-configure.md).

> [!NOTE]
> Dessa inställningar gäller för olika registreringstyper. Vissa inställningar gäller för alla registreringsalternativ. Mer information om de olika registreringstyperna finns i [macOS-registrering](../enrollment/macos-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **AirPrint-mål**: **Lägg till** en eller flera AirPrint-skrivare där användare kan skriva ut från sina enheter. Ange även:
  - **Port** (iOS 11.0+, iPadOS 13.0+): Ange lyssningsporten för AirPrint-målet. Om du lämnar den här egenskapen tom, kommer AirPrint att använda standardporten.
  - **IP-adress**: Ange skrivarens IPv4- eller IPv6-adress. Ange till exempel `10.0.0.1`. Om du använder värdnamn till att identifiera skrivare, kan du hämta IP-adressen genom att pinga skrivaren i Terminal-appen. Det finns mer information under [Hämta IP-adress och sökväg](#get-the-ip-address-and-path) (i den här artikeln).
  - **Sökväg**: Ange resurssökvägen till skrivaren. Sökvägen är vanligtvis `ipp/print` för skrivare i nätverket. Det finns mer information under [Hämta IP-adress och sökväg](#get-the-ip-address-and-path) (i den här artikeln).
  - **TLS** (iOS 11.0+, iPadOS 13.0+): Alternativen är:
    - **Nej** (standard): TLS (Transport Layer Security) används inte vid anslutning till AirPrint-skrivare.
    - **Ja**: Skyddar AirPrint-anslutningar med TLS (Transport Layer Security).

- **Importera** en kommaavgränsad fil (.csv) med en lista över AirPrint-skrivare. När du har lagt till AirPrint-skrivarna i Intune, kan du också **Exportera** listan.

### <a name="get-the-ip-address-and-path"></a>Hämta IP-adress och sökväg

Om du vill lägga till AirPrinter-servrar, behöver du ha skrivarens IP-adress, resurssökväg och port. Följande steg visar hur du hämtar den här informationen.

1. Öppna **Terminal** (från **/Program/Verktyg**) på en Mac som är ansluten till samma lokala nätverk (undernät) som AirPrint-skrivarna.
2. I Terminal-appen skriver du `ippfind` och väljer Retur.

    Observera skrivarinformationen. Du kan exempelvis ange något i stil med `ipp://myprinter.local.:631/ipp/port1`. Den första delen är namnet på skrivaren. Den sista delen (`ipp/port1`) är resurssökvägen.

3. I Terminal skriver du `ping myprinter.local` och väljer Retur.

   Observera IP-adressen. Den visar något i stil med `PING myprinter.local (10.50.25.21)`.

4. Använd värdena för IP-adressen och resurssökvägen. I det här exemplet är IP-adressen `10.50.25.21` och resurssökvägen är `/ipp/port1`.

## <a name="associated-domains"></a>Tillhörande domäner

Med Intune kan du:

- Lägg till många app-till-domän-associationer.
- Associera många domäner med samma app.

Den här funktionen gäller för:

- macOS 10.15 och senare

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Inställningarna gäller för: Enhetsregistrering som användaren godkänner och automatisk enhetsregistrering

- **Tillhörande domäner**: **Lägg till** en koppling mellan din domän och en app. Den här funktionen delar inloggningsuppgifter mellan en Contoso-app och en Contoso-webbplats. Ange även:

  - **App-ID**: Ange app-ID:t för den app som ska associeras med en webbplats. App-ID:t innehåller team-ID:t och ett bunt-ID: `TeamID.BundleID`.

    Team-ID:t är en sträng med 10 tecken (bokstäver och siffror) som genereras av Apple för dina apputvecklare, t.ex. `ABCDE12345`. [Leta upp ditt team-ID](https://help.apple.com/developer-account/#/dev55c3c710c) (öppnar Apples webbplats) innehåller mer information.

    Bunt-ID:t identifierar appen unikt och är vanligtvis formaterat i omvänd domännamnsnotation. Bunt-ID:t för Finder är t.ex. `com.apple.finder`. Om du vill hitta bunt-ID:t, så använd AppleScript i Terminal:

    `osascript -e 'id of app "ExampleApp"'`

  - **Domän**: Ange den webbplatsdomän som ska associeras med en app. Domänen innehåller en tjänsttyp och ett fullständigt kvalificerat värdnamn, t. ex. `webcredentials:www.contoso.com`.

    Du kan matcha alla underdomäner i en associerad domän genom att ange `*.` (en asterisk som jokertecken och en punkt) framför domänens början. Du måste ange perioden. Exakta domäner har högre prioritet än domäner med jokertecken. Därför matchas mönster från överordnade domäner *om* någon matchning inte finns i den fullständigt kvalificerade underdomänen.

    Tjänsttypen kan vara:

    - **authsrv**: Tillägg för enkel inloggning
    - **applink**: Universell länk
    - **webbinloggningsuppgifter**: Automatisk ifyllning av lösenord

> [!TIP]
> Du kan felsöka på din macOS-enhet genom att öppna **Systeminställningar** > **Profiler**. Bekräfta att profilen du skapade finns i enhetens profillista. Om den finns med i listan, såse till att **Associerad domänkonfiguration** finns i profilen och att den innehåller rätt app-ID och domäner.

## <a name="content-caching"></a>Innehållscachelagring

Med innehållscachelagring sparar du en kopia av innehållet lokalt. Andra Apple-enheter kan hämta den här informationen utan att ansluta till internet. Den här cachelagringen gör nedladdningar snabbare genom att programuppdateringar, appar, foton och annat innehåll sparas första gången de laddas ned. Eftersom appar laddas ned en gång och delas till andra enheter kan skolor och organisation med många enheter spara bandbredd.

> [!NOTE]
> Använd bara en profil för de här inställningarna. Om du tilldelar flera profiler med de här inställningarna uppstår ett fel.
>
> Mer information om att övervaka innehållscachelagring finns i [Visa loggar och statistik för innehållscachelagring](https://support.apple.com/guide/mac-help/view-content-caching-logs-statistics-mac-mchl0d8533cd/10.15/mac/10.15) (öppnar Apples webbplats).

Den här funktionen gäller för:

- macOS 10.13.4 och senare

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

Mer information om de här inställningarna finns i [Inställningar för innehållscachelagring](https://support.apple.com/guide/mdm/content-caching-mdm163612d39/1/web/1) (öppnar Apples webbplats).

**Aktivera innehållscachelagring**: **Ja** aktiverar innehållscachelagring och användarna kan inte inaktivera alternativet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan stänga av den som standard.

- **Typ av innehåll som ska cachelagras**: Alternativen är:
  - **Allt innehåll**: iCloud-innehåll och delat innehåll cachelagras.
  - **Endast användarinnehåll**: Användarens iCloud-innehåll som foton och dokument cachelagras.
  - **Endast delat innehåll**: Appar och programvaruuppdateringar cachelagras.

- **Maximal cachestorlek**: Ange den maximala mängden diskutrymme (i byte) som används för cachelagring av innehåll. När du lämnar fältet tomt (standardinställningen) varken ändrar eller uppdaterar Intune den här inställningen. Operativsystemet kan som standard ange värdet noll (`0`) byte för den här inställningen, vilket ger obegränsat diskutrymme till cachelagringen.

  Se till att du inte överskrider det tillgängliga utrymmet på enheterna. Mer information om enheters lagringskapacitet finns i [Så rapporteras lagringskapacitet i iOS och macOS](https://support.apple.com/HT201402) (öppnar Apples webbplats).

- **Cacheplats**: Ange sökvägen där cacheinnehållet ska lagras. Standardplatsen är `/Library/Application Support/Apple/AssetCache/Data`. Vi rekommenderar att du inte ändrar den här platsen.

  Om du ändrar den här inställningen flyttas inte det cachelagrade innehållet till den nya platsen. Om innehållet ska flyttas automatiskt måste användarna ändra platsen på enheten (**Systeminställningar** > **Delning** > **Innehållscachelagring**).

- **Port**: Ange de TCP-portnummer där cachelagringen ska acceptera förfrågningar om nedladdning och uppladdning som 0–65535. Ange noll (`0`) (standardvärdet) om du vill kunna använda valfri tillgänglig port.
- **Blockera delning av internetanslutning och cachelagrat innehåll**: Kallas även för bunden cachelagring. **Ja** förhindrar delning av internetanslutningar och delning av cachelagrat innehåll med iOS/iPad-enheter som är anslutna till Mac-datorn via USB. Användarna kan inte aktivera den här funktionen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

- **Aktivera delning av internetanslutning**: Kallas även för bunden cachelagring. **Ja** tillåter delning av internetanslutningar och delning av cachelagrat innehåll med iOS/iPad-enheter som är anslutna till Mac-datorn via USB. Användarna kan inte inaktivera den här funktionen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan stänga av den här funktionen som standard.

  Den här funktionen gäller för:

  - macOS 10.15.4 och senare

- **Aktivera cachelagring för att logga klientinformation**: **Ja** loggar IP-adress och portnummer för enheter som begär innehåll. Om du felsöker problem med enheter kan den här loggfilen vara till hjälp. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske inte loggar den här informationen som standard.

- **Behåll alltid innehåll från cachen även när systemet behöver diskutrymme för andra appar**: **Ja** behåller innehållet i cachen och ser till att ingenting tas bort, även om det blir ont om diskutrymme. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard rensa innehåll från cachen automatiskt när det behövs lagringsutrymme för andra appar.

  Den här funktionen gäller för:

  - macOS 10.15 och senare

- **Visa statusaviseringar**: **Ja** visar aviseringar som systemmeddelanden. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske inte visar de här aviseringarna som systemmeddelanden som standard.

  Den här funktionen gäller för:

  - macOS 10.15 och senare

- **Förhindra att enheten är i viloläge när cachelagring är aktiverat**: **Ja** förhindrar att datorn försätts i viloläge när cachelagring är aktiverat. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske tillåter att enheten försätts i viloläge som standard.

  Den här funktionen gäller för:

  - macOS 10.15 och senare

- **Enheter som ska cachelagras**: Välj vilka enheter som ska cachelagra innehåll. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. 
  - **Enheter i samma lokala nätverk**: Innehållscachen tillhandahåller innehåll till enheter i samma omedelbara lokala nätverk. Inget innehåll tillhandahålls till enheter i andra nätverk, inklusive enheter som kan nås av innehållscachen.
  - **Enheter som använder samma offentliga IP-adress**: Innehållscachen tillhandahåller innehåll till enheter som använder samma offentliga IP-adress. Inget innehåll tillhandahålls till enheter i andra nätverk, inklusive enheter som kan nås av innehållscachen.
  - **Enheter som använder anpassade lokala nätverk**: Innehållscachen tillhandahåller innehåll till enheter i de IP-adressintervall du anger.
    - **Lyssnarintervall för klient**: Ange intervallet av IP-adresser som ska ta emot innehåll från cachelagringen.
  - **Enheter som använder anpassade lokala nätverk med återställning**: Innehållscachen tillhandahåller innehåll till enheter i lyssningsintervall, peer-lyssningsintervall och överordnade IP-adresser.
    - **Lyssnarintervall för klient**: Ange intervallet av IP-adresser som ska ta emot innehåll från cachelagringen.

- **Anpassade offentliga IP-adresser**: Ange ett intervall med offentliga IP-adresser. Molnservrarna använder det här intervallet till att matcha klientenheter mot cachelagringar.

- **Dela innehåll med annan cachelagring**: När det finns fler än en innehållscache i nätverket blir cacheinnehållet på andra enheter automatiskt peer-enheter. Sådana enheter kan fråga efter och dela cachelagrad programvara. 

  När ett efterfrågat objekt inte finns i en innehållscache kontrolleras peer-enheterna. Om objektet finns där laddas det ned från innehållscachen på peer-enheten. Om objektet fortfarande inte är tillgänglig laddar innehållscachen ned objektet från:

  - en överordnad IP-adress om en sådan är konfigurerad
  
    ELLER
    
  - från Apple via internet.

  När det finns fler än en innehållscache väljer enheterna rätt innehållscache automatiskt. 

  Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Innehållscachelagring som använder samma lokala nätverk**: Dela endast cachelagring med peer-enheter i samma omedelbara lokala nätverk.
  - **Innehållscachelagring med samma offentliga IP-adress**: Dela endast cachelagring med peer-enheter som har samma offentliga IP-adress.
  - **Innehållscachelagring som använder anpassade lokala nätverk**: Dela endast cachelagring med peer-enheter i de IP-adressintervall du anger:

    - **Lyssnarintervall för peer**: Ange start- och slutadress i IPv4- eller IPv6-format för ditt intervall. Innehållscachen svarar bara på peer-förfrågningar från cachelagring i de IP-adressintervall du anger.
    - **Filterintervall för peer**: Ange start- och slutadress i IPv4- eller IPv6-format för ditt intervall. Innehållscachen filtrerar listan med peer-datorer enligt de IP-adressintervall du anger.

- **Överordnade IP-adresser**: Ange den lokala IP-adressen till en annan innehållscache som ska läggas till som överordnad cache. Din cachelagring laddar upp och ned innehåll till och från dessa cachelagringar snarare än direkt via Apple. Lägg endast till en överordnad IP-adress en gång.
- **Princip för val av överordnad**: När det finns flera överordnade cachelagringar anger du hur den överordnade IP-adressen väljs. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Resursallokering**: Använd de överordnade IP-adresserna i turordning. Det här alternativet är bra i scenarier med belastningsutjämning.
  - **Först tillgänglig**: Använd alltid den första tillgängliga IP-adressen i listan.
  - **Hash**: Skapar ett hashvärde för sökvägsdelen av den begärda webbadressen. Det här alternativet ser till att samma överordnade IP-adress alltid används för samma webbadress.
  - **Slumpvis**: Använd en slumpmässigt vald IP-adress i listan. Det här alternativet är bra i scenarier med belastningsutjämning.
  - **Fästlapp tillgänglig**: Använd alltid den första IP-adressen i listan. Använd den andra IP-adressen i listan om den första inte är tillgänglig. Fortsätt att använda den andra IP-adressen tills den inte är tillgänglig, och så vidare.

## <a name="login-items"></a>Inloggningsobjekt

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Lägg till filer, mappar och egna appar som ska starta vid inloggning**: **Lägg till** sökvägen för en fil, mapp, anpassad app eller systemapp som ska öppnas när användare loggar in på sina enheter. Ange även:

  - **Sökväg för objekt**: Ange sökvägen till filen, mappen eller appen. Systemappar eller appar som har skapats eller anpassats för din organisation finns vanligtvis i `Applications`-mappen, med en sökväg liknande `/Applications/AppName.app`.

    Du kan lägga till många filer, mappar och appar. Ange till exempel:  
  
    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`
  
    När du lägger till en app, mapp eller fil måste du ange rätt sökväg. Alla objekt finns inte i `Applications`-mappen. Om användare flyttar ett objekt från en plats till en annan ändras sökvägen. Det här flyttade objektet öppnas inte när användaren loggar in.

  - **Dölj**: Välj om du vill visa eller dölja appen. Alternativen är:
    - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Operativsystemet kanske som standard visar objekt i listan Användare och grupper med alternativet Dölj avmarkerat.
    - **Ja**: Döljer appen i listan Användare och grupper vid inloggning.

## <a name="login-window"></a>Inloggningsfönstret

### <a name="settings-apply-to-all-enrollment-types"></a>Inställningarna gäller för: Alla registreringstyper

- **Visa ytterligare information i menyfältet**: **Ja** innebär att värdnamnet och macOS-versionen visas när du väljer tidsområdet i menyfältet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard inte visa den här informationen på menyraden.
- **Banderoll**: Ange ett meddelande som visas på inloggningsskärmen på enheter. Du kan till exempel ange organisationsinformation, ett välkomstmeddelande eller information för Upphittat.
- **Kräv textfälten användarnamn och lösenord**: Välj hur användare loggar in på enheter. **Ja** kräver att användarna anger ett användarnamn och lösenord. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard kräva att användare väljer sitt användarnamn i en lista och sedan skriver sitt lösenord.

  Ange även:

  - **Dölj lokala användare**: Om du väljer **Ja** visas inte lokala användarkonton i användarlistan, som kan innehålla standardkonton och administratörskonton. Endast nätverks- och systemanvändarkonton visas. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa de lokala användarkonton i användarlistan.
  - **Dölj mobilkonton**: Om du väljer **Ja** visas inte mobilkonton i användarlistan. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa mobilkonton i användarlistan. Vissa mobilkonton kan visas som nätverksanvändare.
  - **Visa nätverksanvändare**: Välj **Ja** om du vill visa nätverksanvändare i användarlistan. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa nätverksanvändarkonton i användarlistan.
  - **Dölj datorns administratörer**: Om du väljer **Ja** visas inte administratörskonton i användarlistan. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa administratörskonton i användarlistan.
  - **Visa andra användare:** : Välj **Ja** om du vill visa **Andra...** användare i användarlistan. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard inte visa andra användarkonton i användarlistan.

- **Dölj nedstängningsknapp**: Om du väljer **Ja** visas inte avstängningsknappen på inloggningsskärmen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa avstängningsknappen.
- **Dölj knappen Starta om**: Om du väljer **Ja** visas inte omstartsknappen på inloggningsskärmen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa omstartsknappen.
- **Dölj knappen Vila**: Om du väljer **Ja** visas inte knappen Vila på inloggningsskärmen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard visa Vila-knappen.
- **Inaktivera användarinloggning från konsol**: Om du väljer **Ja** döljs kommandoraden i macOS som används för att logga in. Vanliga användare kan ange den här inställningen till **Ja**. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta avancerade användare att logga in med macOS-kommandoraden. För att gå till konsolläget anger användarna `>console` i fältet Användarnamn. Användarna måste sedan autentiseras i konsolfönstret.
- **Inaktivera nedstängning när inloggad**: Om du väljer **Ja** kan användarna inte välja alternativet **Stäng av** efter att de har loggat in. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användare att välja menyalternativet **Stäng av** på enheter.
- **Inaktivera omstart när inloggad**: Om du väljer **Ja** kan användarna inte välja alternativet **Starta om** efter att de har loggat in. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användare att välja menyalternativet **Starta om** på enheter.
- **Inaktivera avstängning när inloggad**: Om du väljer **Ja** kan användarna inte välja alternativet **Ström av** efter att de har loggat in. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användare att välja menyalternativet **Ström av** på enheter.
- **Inaktivera utloggning när inloggad** (macOS 10.13 eller senare): Om du väljer **Ja** kan användarna inte välja alternativet **Logga ut** efter att de har loggat in. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användare att välja menyalternativet **Logga ut** på enheter.
- **Inaktivera låsskärm när inloggad** (macOS 10.13 eller senare): Om du väljer **Ja** kan användarna inte välja alternativet **Låsskärm** efter att de har loggat in. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användare att välja menyalternativet **Lås skärm** på enheter.

## <a name="single-sign-on-app-extension"></a>Tillägg för enkel inloggning

Den här funktionen gäller för:

- macOS 10.15 och senare

### <a name="settings-apply-to-user-approved-device-enrollment-and-automated-device-enrollment"></a>Inställningarna gäller för: Enhetsregistrering som användaren godkänner och automatisk enhetsregistrering

- **Typ av SSO-apptillägg**: Välj typ av SSO-apptillägg. Alternativen är:

  - **Inte konfigurerad**: Apptilläggen används inte. Om du vill inaktivera ett apptillägg, så ändra SSO-apptilläggstypen till **Inte konfigurerad**.
  - **Microsoft Azure AD**: Använder Microsoft Enterprise SSO-plugin-programmet, som är ett SSO-apptillägg av omdirigeringstyp. Det här plugin-programmet ger enkel inloggning för Active Directory-konton i alla macOS-program som har stöd för [Apples Enterprise-funktion för enkel inloggning](https://developer.apple.com/documentation/authenticationservices). Använd denna typ av SSO-apptillägg för att aktivera SSO på Microsoft-appar, organisationsappar och webbplatser som autentiseras med hjälp av Azure AD.

    Plugin-programmet för enkel inloggning fungerar som en avancerad autentiseringsprovider som tillhandahåller förbättringar vad gäller säkerhet och användarupplevelse.

    > [!IMPORTANT]
    > Om du vill uppnå enkel inloggning med tilläggstypen för Microsoft Azure AD SSO-appen, måste du installera macOS-företagsportalappen på enheterna. Företagsportalappen levererar Microsoft Enterprise SSO-tilläggsprogrammet till enheterna. Inställningarna för MDM-tillägget för MDM aktiverar tilläggsprogrammet. Företagsportalappen och SSO-apptilläggsprofilen har installerats på enheterna, måste användarna ange sina autentiseringsuppgifter för att kunna logga in och upprätta en session på sina enheter. Den här sessionen används av olika program utan att användarna behöver autentisera sig igen.
    >
    > Mer information om företagsportalappen finns i [Vad händer när jag installerar företagsportalappen och registrerar macOS-enheten i Intune](../user-help/what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md). [Ladda ned](https://go.microsoft.com/fwlink/?linkid=853070) företagsportalappen.

  - **Omdirigera**: Använd ett allmänt, anpassningsbart omdirigeringsapptillägg om du vill använda SSO med moderna autentiseringsflöden. Försäkra dig om att du känner till tillägget och grupp-ID:t för din organisations apptillägg.
  - **Autentiseringsuppgift**: Använd ett generiskt, anpassningsbart apptillägg för autentiseringsuppgifter om du vill använda SSO med autentiseringsflöden med anrop och svar. Försäkra dig om att du känner till tilläggs-ID och grupp-ID för din organisations SSO-apptillägg.  
  - **Kerberos**: Använd Apples inbyggda Kerberos-tillägg, som ingår i macOS Catalina 10.15 och senare. Det här alternativet är en Kerberos-specifik version av apptillägget **Autentiseringsuppgifter**.

  > [!TIP]
  > Gå igenom tillägget genom att lägga till dina egna konfigurationsvärden med hjälp av typerna **Omdirigering** och **Autentiseringsuppgifter**. Om du använder **autentiseringsuppgifter**bör du överväga att använda inbyggda konfigurationsinställningar från Apple i **Kerberos**-typen.

- **Tilläggs-ID** (omdirigering, autentiseringsuppgift): Ange det paket-ID som identifierar ditt SSO-apptillägg, exempelvis `com.apple.ssoexample`.
- **Team-ID** (omdirigering, autentiseringsuppgift): Ange SSO-apptilläggets team-ID. Ett team-ID är en sträng med 10 tecken (siffror och bokstäver) som genereras av Apple, t. ex. `ABCDE12345`. 

  [Leta upp ditt team-ID](https://help.apple.com/developer-account/#/dev55c3c710c) (öppna Apples webbplats) om du vill ha mer information.

- **Sfär** (autentiseringsuppgift, Kerberos): Ange namnet på din autentiseringssfär. Sfärnamnet måste skrivas med versaler, t. ex. `CONTOSO.COM`. Vanligtvis är sfärnamnet detsamma som ditt DNS-domännamn, men skrivet enbart med versaler.

- **Domäner** (autentiseringsuppgift, Kerberos): Ange domän- eller värdnamnen för de webbplatser som kan autentiseras via SSO. Om din webbplats exempelvis är `mysite.contoso.com`, så är `mysite` värdnamnet och `contoso.com` domännamnet. När användarna ansluter till någon av dessa platser så hanterar apptillägget autentiseringsutmaningen. Med den här autentiseringen kan användarna logga in med hjälp av Ansiktsigenkänning-ID, Touch ID eller PIN-kod/lösenord för Apple.

  - Alla domäner i Intune-profiltilläggen för enkel inloggning måste vara unika. Du kan inte upprepa en domän i vilken apptilläggsprofil för enkel inloggning som helst, även om du använder olika typer av SSO-apptillägg.
  - Dessa domäner är inte skiftlägeskänsliga.

- **URL:er** (endast omdirigering): Ange URL-prefixen för dina identitetsprovidrar för vilkas räkning apptillägget för omdirigering använder SSO. När användarna omdirigeras till dessa URL:er ingriper SSO-apptillägget och frågar efter SSO.

  - Alla URL:er i Intune-apptilläggsprofilerna för enkel inloggning måste vara unika. Du kan inte upprepa en domän i vilken SSO-apptilläggsprofil som helst, även om du använder olika typer av SSO-tillägg.
  - URL:erna måste inledas med `http://` eller `https://`.

- **Ytterligare konfiguration** (Microsoft Azure AD, omdirigering, autentiseringsuppgift): Ange ytterligare tilläggsspecifika data som ska skickas till SSO-apptillägget:
  - **Nyckel**: Ange namnet på det objekt som du vill lägga till, t.ex. `user name`.
  - **Typ**: Ange datatyp. Alternativen är:

    - Sträng
    - Boolesk: I **Konfigurationsvärde** anger du `True` eller `False`.
    - Heltal: Ange ett tal i **Konfigurationsvärde**.

  - **Värde**: Ange data.
  
  - **Lägg till**: Välj om du vill lägga till dina konfigurationsnycklar.

- **Användning av nyckelring** (endast Kerberos): Förhindra att lösenord sparas och lagras i nyckelringen genom att välja **Blockera**. Om den blockeras uppmanas inte användarna att spara sina lösenord och de måste ange lösenordet på nytt när Kerberos-biljetten upphör att gälla. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att lösenord sparas och lagras i nyckelringen. Användarna uppmanas inte att ange sitt lösenord igen när biljetten upphör att gälla.
- **Face ID, Touch ID eller lösenord** (endast Kerberos): **Kräv** tvingar användarna att ange sitt Face ID, Touch ID eller enhetslösenord när autentiseringsuppgiften krävs för att uppdatera Kerberos-biljetten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte kräver att användare använder biometrik eller enhetslösenord för att uppdatera Kerberos-biljetten. Om **Användning av nyckelring** är blockerad gäller inte den här inställningen.
- **Standardsfär** (endast Kerberos): Välj **Aktivera** om du vill ange det **Sfär**-värde som du angav som standardsfär. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte anger en standardsfär.

  > [!TIP]
  > - **Aktivera** den här inställningen om du konfigurerar flera Kerberos SSO-ap-tillägg i din organisation.
  > - **Aktivera** den här inställningen om du använder flera sfärer. Den anger det **Sfär**-värde som du angav som standardsfär.
  > - Om du bara har en sfär så låt inställningen vara **Inte konfigurerad** (standard).

- **Identifiera automatiskt** (endast Kerberos): När värdet ställts in på **Blockera** använder Kerberos-tillägget inte LDAP eller DNS automatiskt för att fastställa Active Directory-platsens namn. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att tillägget automatiskt hittar Active Directory-platsens namn.
- **Ändringar av lösenord** (endast Kerberos): **Blockera** förhindrar att användarna ändrar sina lösenord för inloggning på de domäner som du har angett. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta ändringar av lösenord.  
- **Lösenordssynkronisering** (endast Kerberos): Välj **Aktivera** om du vill synkronisera dina användares lokala lösenord med Azure AD. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard inaktivera synkronisering av lösenord med Azure AD. Använd den här inställningen som alternativ till eller säkerhetskopia för SSO. Den här inställningen fungerar inte om användarna är inloggade med ett Apple-mobilkonto.
- **Lösenordskomplexitet för Windows Server Active Directory** (endast Kerberos): Välj **Kräv** för att tvinga användarlösenorden att uppfylla komplexitetskraven för Active Directory-lösenord. Mer information finns i [Lösenord måste uppfylla komplexitetskraven](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements). När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte kräver att användarna uppfyller Active Directory-lösenordskraven.
- **Minsta längd på lösenord (tecken)** (endast Kerberos): Ange det minsta antal tecken som användarnas lösenord måste innehålla. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte framtvingar någon minsta längd för användarens lösenord.
- **Gräns för återanvändning av lösenord** (endast Kerberos): Ange det antal nya lösenord, från 1 till 24, som ska användas innan ett tidigare lösenord kan återanvändas på domänen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kräver kanske inte kräver en gräns för återanvändning av lösenord som standard.
- **Lägsta lösenordsålder** (endast Kerberos): Ange det antal dagar som ett lösenord ska användas på domänen innan användare kan ändra det. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte framtvingar någon lägsta ålder på lösenord innan de kan ändras.
- **Meddelande om förfallodatum för lösenord** (endast Kerberos): Ange hur många dagar innan lösenordets förfallodatum som användaren ska få ett meddelande om detta. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard använda `15` dagar.
- **Lösenordets giltighetstid** (endast Kerberos): Ange antalet dagar innan enhetslösenordet måste ändras. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kanske lösenord aldrig upphör.
- **URL för lösenordsändring** (endast Kerberos): Ange den URL som öppnas när användare startar en Kerberos-lösenordsändring.
- **Huvudnamn** (endast Kerberos): Ange användarnamnet för Kerberos-huvudkontot. Du behöver inte inkludera sfärnamnet. I `user@contoso.com` är t.ex. `user` huvudkontots namn och `contoso.com` är sfärens namn.

  > [!TIP]
  > - Du kan också använda variabler i huvudkontots namn genom inom klammerparenteser `{{ }}`. Om du t.ex. vill visa användarnamnet anger du `Username: {{username}}`. 
  > - Var dock försiktig med variabel ersättning eftersom variablerna inte verifieras i användargränssnittet och är skiftlägeskänsliga. Se till att du anger rätt information.
  
- **Active Directory-platskod** (endast Kerberos): Ange namnet på den Active Directory-plats som Kerberos-tillägget ska använda. Du kanske inte behöver ändra det här värdet eftersom Kerberos-tillägget kan hitta Active Directory-platskoden automatiskt.
- **Cachenamn** (endast Kerberos): Ange GSS-namnet (Generic Security Services) för Kerberos-cachen. Du behöver förmodligen inte ange det här värdet.  
- **Meddelande om lösenordskrav** (endast Kerberos): Ange en textversion av organisationens lösenordskrav som ska visas för användarna. Meddelandet visas om du inte har några krav på Active Directory-lösenordens komplexitet eller på minsta längd för lösenord.  
- **Aktivera läget Delad enhet** (endast Microsoft Azure AD): Välj **Ja** om du ska distribuera Microsoft Enterprise SSO-plugin-programmet till macOS-enheter som konfigurerats för Azure AD:s funktion för läget Delad enhet. Enheter i delat läge gör det möjligt för många användare att logga in och ut globalt på program som stöder läget Delad enhet. När detta anges till **Inte konfigurerad** ändrar eller uppdaterar Intune inte den här inställningen. 

  När du har valt **Ja** rensas alla befintliga användarkonton från enheterna. Om du vill undvika dataförlust eller förhindra en fabriksåterställning måste du förstå hur den här inställningen påverkar dina enheter.

  Mer information om läget delad enhet finns i [Översikt över läget delad enhet](https://docs.microsoft.com/azure/active-directory/develop/msal-shared-devices).

- **Programpaket-ID** (Microsoft Azure AD, Kerberos): **Lägg till** de programpakets-ID:n som ska använda enkel inloggning på dina enheter. Dessa appar beviljas åtkomst till den biljettbeviljande biljetten för Kerberos och autentiseringsbiljetten. Apparna autentiserar även användare för tjänster som de har behörighet till.
- **Domänsfärsmappning** (endast Kerberos): **Lägg till** DNS-suffixen för den domän som ska mappas till din sfär. Använd den här inställningen när värdarnas DNS-namn inte matchar sfärnamnet. Du behöver förmodligen inte skapa den här anpassade domän-till-sfär-mappningen.
- **PKINIT-certifikat** (endast Kerberos): **Välj** den kryptering för offentlig nyckel för inledande autentisering (PKINIT) som kan användas för Kerberos-autentisering. Du kan välja mellan [PKCS](../protect/certficates-pfx-configure.md)- eller [SCEP](../protect/certificates-scep-configure.md) -certifikat som du har lagt till i Intune. Mer information om certifikat finns i [Använda certifikat för autentisering i Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Du kan också konfigurera enhetsfunktioner på [iOS/iPadOS](ios-device-features-settings.md).
