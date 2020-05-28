---
title: Funktioner i Technical Preview 1609
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1609.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 51a974247d7281d6134b699a5865f801d1ed6094
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905711"
---
# <a name="capabilities-in-technical-preview-1609-for-configuration-manager"></a>Funktioner i Technical Preview 1609 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*



Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1609. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats.      Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.    

**Kända problem i den här tekniska för hands versionen:**  
*  När du uppdaterar till Configuration Manager 1609 Technical Preview tas eventuella uppgraderings principer för utgåva som du har distribuerat bort. Om du vill fortsätta att använda dessa principer måste du återskapa och distribuera dem.


**Följande är nya funktioner som du kan prova med den här versionen.**  

## <a name="improvements-to-endpoint-protection"></a>Förbättringar av Endpoint Protection
Förbättringar för att Endpoint Protection princip inställningar för program mot skadlig kod – nu kan du ange på vilken nivå som Endpoint Protection moln skydds tjänsten ska blockera misstänkta filer. Med en ny inställning kan administratörer ange "riskfylld" datorer baserat på de stora mängder skadlig kod som de stöter på.

## <a name="increased-number-of-enrolled-devices"></a>Ökat antal registrerade enheter
Administratörer kan nu göra det möjligt för användare att registrera upp till 15 enheter i hybrid hantering av mobila enheter med Intune. Gränsen var 5 enheter per användare tidigare.

## <a name="additional-apple-dep-settings"></a>Ytterligare Apple DEP-inställningar

Administratörer kan nu konfigurera följande Apple Programmet för enhetsregistrering-inställningar (DEP) i DEP-profilen för iOS-och Mac-enheter:
- **Touch ID**
- **Zoom**
- **Siri**

Om den är aktive rad uppmanas installations assistenten för Apple att använda tjänsten under enhets aktiveringen.

## <a name="integration-with-upgrade-analytics"></a>Integrering med Upgrade Analytics

Med uppgraderings analys kan du utvärdera och analysera enhets beredskap och kompatibilitet med Windows 10 för att ge enklare och smidigare uppgraderingar. Genom att integrera Upgrade Analytics med Configuration Manager kan du komma åt uppgraderingens kompatibilitetsinformation i Configuration Manager-administratörskonsolen och sedan använda enhets listan för att uppgradera eller reparera enheter.


## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Inbyggda anslutnings typer för Windows 10 VPN hybrid profiler

När du använder Configuration Manager med Intune kan du nu skapa Windows 10 VPN-profiler med anslutnings typerna Microsoft Automatic, IKEv2, PPTP och L2TP i Configuration Manager-konsolen utan att använda OMA-URI.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Förbättringar av Windows Store för företag-integration med Configuration Manager

I den här versionen har vi uppdaterat [Windows Store för företag-integrering](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) med dessa nya funktioner:

**Uppdatera:** I den aktuella tekniska för hands versionen fungerar inte funktionen för omedelbar synkronisering.

- Tidigare kunde du bara distribuera kostnads fria appar från Windows Store för företag. Configuration Manager har nu också stöd för distribution av betalade licensierade online-appar (endast för Intune-registrerade enheter).
- Nu kan du starta en omedelbar synkronisering mellan Windows Store för företag och Configuration Manager.
- Nu kan du ändra klientens hemliga nyckel som du fick från Azure Active Directory

### <a name="try-it-out"></a>prova!

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Köp och synkronisera en betald online-licensierad app

1. Köp en betald online-licensierad app från Windows Store för företag.
2. I arbets ytan **Administration** i Configuration Manager-konsolen klickar du på **Cloud Services**  >  **uppdateringar och service**  >  **för Windows Store för företag**.
3. På fliken **Start** går du till gruppen **Synkronisera** och klickar på **Synkronisera nu**.
4. Därefter visas den app du köpte i noden **licens information för Store-appar** i arbets ytan **Application Management** .

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Skapa och distribuera ett Configuration Manager program från synkroniserade AppData

Proceduren för att skapa och distribuera ett Configuration Manager program från en betald Store-app är samma som för att skapa ett program från en kostnads fri app. Se avsnittet **skapa och distribuera ett Configuration Manager program från en app för Windows Store för företag** i [Hantera appar från Windows Store för företag med Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Ändra klientens hemliga nyckel från Azure Active Directory

1. I arbets ytan **Administration** i Configuration Manager-konsolen klickar du på **Cloud Services**  >  **uppdateringar och service**  >  **för Windows Store för företag**.
2. Välj ditt Windows Store för företag-konto och klicka sedan på **Egenskaper**.
3. I dialog rutan **Egenskaper för Windows Store för företag-konto** anger du en ny nyckel i fältet **hemlig nyckel för klienten** och klickar sedan på **Verifiera**. När du har verifierat klickar du på **Använd**och stänger sedan dialog rutan.


## <a name="new-compliance-settings-for-configuration-items"></a>Nya kompatibilitetsinställningar för konfigurations objekt

Vi har lagt till många nya inställningar som du kan använda i konfigurations objekt för olika enhets plattformar.
Detta är inställningar som tidigare fanns i Microsoft Intune i en fristående konfiguration och som nu är tillgängliga när du använder Intune med Configuration Manager.
Om du behöver hjälp med någon av dessa inställningar öppnar du [Hantera inställningar och funktioner på dina enheter med Microsoft Intune principer](/mem/intune/configuration/device-profiles) och väljer sedan underavsnittet inställningar för den plattform som du vill använda.


### <a name="new-settings-for-android-devices"></a>Nya inställningar för Android-enheter

#### <a name="password-settings"></a>Inställningar för lösenord

- **Kom ihåg tidigare lösenord**
- **Tillåt fingeravtrycksupplåsning**

#### <a name="security-settings"></a>Säkerhetsinställningar

- **Kräv kryptering på minneskort**
- **Tillåt skärmbild**
- **Tillåt sändning av diagnostikdata**

#### <a name="browser-settings"></a>Webbläsarinställningar

- **Tillåt webbläsare**
- **Tillåt Autofyll**
- **Tillåt blockering av popup-fönster**
- **Tillåt cookies**
- **Tillåt Active scripting**

#### <a name="app-settings"></a>Appinställningar

- **Tillåt Google Play-butik**

#### <a name="device-capability-settings"></a>Inställningar för enhetskapacitet

- **Tillåt flyttbara lagringsenheter**
- **Tillåt Wi-Fi -delning**
- **Tillåt geolokalisering**
- **Tillåt NFC**
- **Tillåt Bluetooth**
- **Tillåt röstroaming**
- **Tillåt dataroaming**
- **Tillåt SMS/MMS-meddelanden**
- **Tillåt röstassistent**
- **Tillåt röstsamtal**
- **Tillåt kopiera och klistra in**


### <a name="new-settings-for-ios-devices"></a>Nya inställningar för iOS-enheter

#### <a name="password-settings"></a>Inställningar för lösenord

- **Antal avancerade tecken som krävs i lösenord**
- **Tillåt enkla lösenord**
- **Antal minuters inaktivitet innan lösenord krävs**
- **Kom ihåg tidigare lösenord**

### <a name="new-settings-for-mac-os-x-devices"></a>Nya inställningar för Mac OS X-enheter

#### <a name="password-settings"></a>Inställningar för lösenord

- **Antal avancerade tecken som krävs i lösenord**
- **Tillåt enkla lösenord**
- **Kom ihåg tidigare lösenord**
- **Minuter av inaktivitet innan skärmsläckaren aktiveras**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nya inställningar för Station ära och mobila Windows 10-enheter

#### <a name="password-settings"></a>Inställningar för lösenord

- **Lägst antal teckenuppsättningar**
- **Kom ihåg tidigare lösenord**
- **Kräv lösenord när enheten återgår från viloläge**

#### <a name="security-settings"></a>Säkerhetsinställningar

- **Filkryptering på mobil enhet**
- **Tillåt manuell avregistrering**

#### <a name="device-capability-settings"></a>Inställningar för enhetskapacitet

- **Tillåt VPN via mobilnät**
- **Tillåt VPN-roaming via mobilnät**
- **Tillåt telefonåterställning**
- **Tillåt USB-anslutning**
- **Tillåt Cortana**
- **Tillåt action center meddelanden**

### <a name="new-settings-for-windows-10-team-devices"></a>Nya inställningar för Windows 10 team-enheter

#### <a name="device-settings"></a>Enhetsinställningar

- **Aktivera Operational Insights i Azure**
- **Aktivera trådlös Miracast-projektion**
- **Välj den mötesinformation som ska visas på välkomstskärmen**
- **Webbadress till bakgrundsbild för låsskärm**


### <a name="new-settings-for-windows-81-devices"></a>Nya inställningar för Windows 8,1-enheter

#### <a name="applicability-settings"></a>Tillämplighetsinställningar

- **Tillämpa alla konfigurationer på Windows 10**

#### <a name="password-settings"></a>Inställningar för lösenord

- **Lösenordstyp krävs**
- **Lägst antal teckenuppsättningar**
- **Minsta längd på lösenord**
- **Antal tillåtna, upprepade felinloggningar innan enheten rensas**
- **Antal minuter av inaktivitet innan skärmen stängs av**
- **Lösenordets giltighetstid (i dagar)**
- **Kom ihåg tidigare lösenord**
- **Förhindra återanvändning av tidigare lösenord**
- **Tillåt bildlösenord och PIN**

#### <a name="browser-settings"></a>Webbläsarinställningar

- **Tillåt automatisk identifiering av intranätsnätverk**


### <a name="new-settings-for-windows-phone-81-devices"></a>Nya inställningar för Windows Phone 8,1-enheter

#### <a name="applicability-settings"></a>Tillämplighetsinställningar

- **Tillämpa alla konfigurationer på Windows 10**

#### <a name="password-settings"></a>Inställningar för lösenord

- **Lägst antal teckenuppsättningar**
- **Tillåt enkla lösenord**
- **Kom ihåg tidigare lösenord**

#### <a name="device-capability-settings"></a>Inställningar för enhetskapacitet

- **Tillåt automatisk anslutning till kostnadsfria, trådlösa surfpunkter**


## <a name="improvements-for-boundary-groups"></a>Förbättringar av gränser grupper
I den här för hands versionen introduceras viktiga ändringar av gränser grupper och hur de fungerar med distributions platser. Dessa ändringar bidrar till att förenkla utformningen av din innehålls infrastruktur och ger dig mer kontroll över hur och när klienterna återgår till att söka efter ytterligare distributions platser som innehålls käll platser. Detta omfattar både lokala och molnbaserade distributions platser.

Dessa förbättringar ersätter koncept och beteenden som du kan vara bekant med idag (som att konfigurera distributions platser så att de är snabba eller långsamma) och ersätter dem med en ny modell som bör vara enklare att konfigurera och underhålla. De här ändringarna är också gjorda för framtida ändringar som kommer att förbättra andra plats system roller som du associerar till gränser grupper.  

Under uppgraderingen till 1609 konverterar uppgraderingen dina aktuella gränser för konfiguration av gränser så att de passar den nya modellen så att dessa ändringar inte stör dina konfigurationer av innehålls distribution (se [Uppdatera befintliga gränser grupper till den nya modellen](capabilities-in-technical-preview-1609.md#bkmk_update)).

I följande avsnitt beskrivs de ändringar som introduceras i den här för hands versionen, hur den nya modellen fungerar och vad du kan förväntar dig när du uppgraderar en plats som redan har kon figurer ATS.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Ändringar i användar gränssnittet och beteendet för gränser grupper och innehålls platser
Följande är viktiga ändringar i gränser grupper och hur klienter hittar innehåll. Många av dessa ändringar och koncept fungerar tillsammans.
- **Konfigurationer för snabb eller långsam tas bort:** Du kan inte längre konfigurera enskilda distributions platser så att de blir snabba eller långsamma.  I stället behandlas alla plats system som är kopplade till en avgränsnings grupp. På grund av den här ändringen stöder fliken **referenser** för gränser grupp egenskaperna inte längre konfigurationen av snabb eller långsam.
- **Ny standard gränser grupp på varje plats:**  Varje primär plats har en ny standard gränser grupp med namnet ***default-site-bounds-group \<>***.  Om en klient inte finns på en nätverks plats som är tilldelad en avgränsnings grupp, kommer klienten att använda de plats system som är kopplade till standard gruppen från dess tilldelade plats. Planera att använda den här gränser gruppen som ersättning till begreppet återställnings innehålls plats.    
  -  **Tillåt borttagning av återställnings käll platser för innehåll** : du behöver inte längre konfigurera en distributions plats som ska användas för återställningen och alternativen för att ange detta tas bort från användar gränssnittet.

  Resultatet av inställningen **tillåter att klienter använder en återställnings käll plats för innehåll** på en distributions typ för program har ändrats. Den här inställningen för en distributions typ gör nu att en klient kan använda standard platsens gränser-grupp som en innehålls käll plats.

  -  **Relationer för gränser grupper:** Varje avgränsnings grupp kan länkas till en eller flera ytterligare avgränsnings grupper. Dessa länkar Forms relationer som har kon figurer ATS på fliken nya egenskaper för gränser-grupp med namnet **relationer**:
  -   Varje avgränsnings grupp som en klient är direkt associerad med kallas för en **aktuell** avgränsnings grupp.  
  -   En valfri avgränsnings grupp som en klient kan använda på grund av en koppling mellan klientens *aktuella* gränser grupp och en annan grupp kallas för en **intilliggande** avgränsnings grupp.
  -  Det finns på fliken **relationer** som du lägger till gränser grupper som kan användas som *intilliggande* avgränsnings grupp. Du kan också konfigurera en tid i minuter som avgör när en klient som inte kan hitta innehåll från en distributions plats i den *aktuella* gruppen kommer att börja söka efter innehålls platser från de *intilliggande* gräns grupperna.

      När du lägger till eller ändrar en gränser grupp konfiguration har du möjlighet att blockera återställningen till den angivna avgränsnings gruppen från den aktuella gruppen som du konfigurerar.

  Om du vill använda den nya konfigurationen definierar du explicita associationer (länkar) från en gräns grupp till en annan och konfigurerar alla distributions platser i den associerade gruppen med samma tid i minuter. Tiden som du konfigurerar avgör när en klient som inte kan hitta en innehålls källa från den *aktuella* gräns gruppen kan börja söka efter innehålls källor från den intilliggande gräns gruppen.

  Förutom de gränser grupper som du uttryckligen konfigurerar, har varje avgränsnings grupp en underförstådd länk till standard platsens gränser grupp. Den här länken blir aktiv efter 120 minuter då standard plats gräns gruppen blir en intilliggande gräns grupp som gör att klienterna kan använda de distributions platser som är kopplade till den gräns gruppen som innehålls käll platser.

  Det här beteendet ersätter vad som tidigare kallades som reserv för innehåll.  Du kan åsidosätta det här standard beteendet på 120 minuter genom att explicit associera standard plats gräns gruppen till en *aktuell* grupp, och ange en specifik tid i minuter eller blockera reserven helt för att förhindra användningen.


- **Klienter försöker hämta innehåll från varje distributions plats i upp till 2 minuter:** När en klient söker efter en innehålls käll plats försöker den få åtkomst till varje distributions plats i 2 minuter innan du försöker igen med en annan distributions plats. Detta är en förändring från tidigare versioner där klienter försökte ansluta till en distributions plats i upp till två timmar.

  - Den första distributions platsen som en klient försöker använda väljs slumpmässigt från poolen med tillgängliga distributions platser i klientens *aktuella* gränser grupp (eller grupper).

  - Om klienten inte har hittat innehållet efter två minuter växlar den till en ny distributions plats och försöker hämta innehåll från den servern. Den här processen upprepas varannan minut tills klienten hittar innehållet eller når den sista servern i poolen.

  - Om en klient inte kan hitta en giltig innehålls käll plats från den *aktuella* poolen innan perioden för återställning till en *intilliggande* gränser grupp nås, lägger klienten till distributions platserna från den *grann* gruppen i slutet av den aktuella listan och söker sedan i den utökade gruppen med käll platser som innehåller distributions platserna från båda gränserna.

      > [!TIP]  
      > När du skapar en explicit länk från den aktuella gräns gruppen till standard plats gräns gruppen och anger en återställnings tid som är mindre än återställnings tiden för en länk till en intilliggande gräns grupp, börjar klienterna söka i käll platserna från standard plats gräns gruppen innan du inkluderar Grans gruppen.

  - När klienten inte kan hämta innehåll från den sista servern i poolen påbörjas processen igen.


### <a name="how-the-new-model-works"></a>Så här fungerar den nya modellen
När du konfigurerar gräns grupper associerar du gränser (nätverks platser) och plats system roller, t. ex. distributions platser, till gräns gruppen. Detta hjälper till att länka klienter till plats system servrar som distributions platser som finns nära klienterna i nätverket.   
- Du kan tilldela samma avgränsning till flera gränser grupper
- Plats system servrar, t. ex. distributions platser, kan associeras med flera gränser grupper, vilket gör dem tillgängliga för en större mängd nätverks platser
- Om en distributions plats inte är kopplad till en gränser grupp kan inte klienterna använda distributions platsen som en innehålls käll plats.

Från och med den här tekniska för hands versionen definierar du gränser för gränser grupper för att konfigurera återställnings beteendet för innehålls käll platser. Det här nya beteendet konfigureras på fliken nya **relationer** i egenskaperna för begränsnings gruppen och ersätter konfigureringen av plats system för att vara långsam eller snabb och konfigurera en begränsnings grupp för att tillåta återställnings käll platser för innehåll.

På fliken relationer lägger du till andra avgränsnings grupper för att konfigurera en relation till dessa grupper. Varje relation är en enkelriktad länk från den **aktuella** avgränsnings gruppen till den gränser grupp som du lägger till, vilket kallas för en **granne**. För varje länk som du skapar kan du konfigurera distributions platser med en återställnings tid på några minuter. Den här tiden används för att avgöra efter hur länge klienter i den *aktuella* gräns gruppen kan börja använda distributions platser i *intilliggande* gräns grupp om de inte kan hitta en giltig innehålls käll plats från den aktuella gräns gruppen.

När en klient inte kan hitta innehåll och börjar söka efter platser från intilliggande gränser, ökar poolen med tillgängliga distributions platser för klienten på ett kontrollerat sätt.  

- En avgränsnings grupp kan ha mer än en relation. På så sätt kan du konfigurera återställning till olika grannar som inträffar efter olika tids perioder.
- Klienterna återgår bara till en begränsande grupp som är direkt grann för den aktuella gränser gruppen.
- När en klient är medlem i flera gräns grupper definieras den aktuella gräns gruppen som en union av alla klientens gräns grupper.  Klienten kan sedan återgå till en granne till någon av dessa ursprungliga gränser grupper.

Förutom de länkar som du definierar, finns det en underförstådd länk som skapas automatiskt mellan de gränser grupper som du skapar och den standard gränser grupp som skapas automatiskt för varje plats. Den här automatiska länken:
- Används av klienter som inte finns på en kant linje som är kopplad till någon avgränsnings grupp i hierarkin automatiskt använder standard gränser gruppen från deras tilldelade plats för att identifiera giltiga innehålls käll platser.   
-  Är ett standard återställnings alternativ från den aktuella gränser gruppen till de plats standard gränser som används efter 120 minuter.

**Exempel på hur du använder den nya modellen:** Du skapar tre gräns grupper som inte delar gränser eller plats system servrar:
- Grupp BG_A med distributions platser DP_A1 och DP_A2 kopplade till gruppen
- Grupp BG_B med distributions platser DP_B1 och DP_B2 kopplade till gruppen
- Grupp BG_C med distributions platser DP_C1 och DP_C2 kopplade till gruppen

Du lägger till nätverks platser för klienterna som gränser till endast BG_A gräns gruppen och konfigurerar sedan relationer från gräns gruppen till de andra två gräns grupperna:
- Du kan konfigurera distributions platser för den första *Grans* gruppen (BG_B) som ska användas efter 10 minuter. Den här gruppen innehåller distributions platser DP_B1 och DP_B2. Båda är väl anslutna till de första gruppernas gränser platser.
- Du konfigurerar den andra *Grans* gruppen (BG_C) som ska användas efter 20 minuter. Den här gruppen innehåller distributions platser DP_C1 och DP_C2. Båda finns i ett WAN-nätverk från de andra två gränser grupperna.
- Du lägger också till ytterligare en distributions plats som finns på plats servern till platsernas standard plats för plats gränser. Detta är den minsta önskade innehålls käll platsen, men den är centralt placerad i alla dina gränser grupper.

  Exempel på gränser grupper och återställnings tider:

  ![BG_Fallack](media/BG_Fallback.png)


Med den här konfigurationen:
- Klienten börjar söka efter innehåll från distributions platser i dess *aktuella* gränser grupp (BG_A), söka igenom varje distributions plats i två minuter innan du växlar till nästa distributions plats i gränsen grupp. Klient samlingen för giltiga innehålls käll platser innehåller DP_A1 och DP_A2.
- Om klienten inte kan hitta innehåll från den *aktuella* gräns gruppen efter sökningen i 10 minuter, lägger den till distributions platserna från BG_B gräns gruppen till dess sökning. Den fortsätter sedan att söka efter innehåll från en distributions plats i den kombinerade poolen med distributions platser som nu omfattar de från både BG_A-och BG_B-gränser. Klienten fortsätter att kontakta varje distributions plats i två minuter innan du växlar till nästa distributions plats från poolen. Klient samlingen för giltiga innehålls käll platser omfattar DP_A1, DP_A2, DP_B1 och DP_B2.
- Efter ytterligare 10 minuter (totalt 20 minuter) om klienten fortfarande inte har hittat en distributions plats med innehåll, expanderas poolen med tillgängliga distributions platser för att ta med de från den andra *Grans* gruppen, gränsen grupp BG_C. Klienten har nu 6 distributions platser för att söka (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 och DP_C2) och fortsätter att ändra till en ny distributions plats var 2: e minut tills innehållet har hittats.
- Om klienten inte har hittat innehåll efter totalt 120 minuter, går det tillbaka till att inkludera *standard plats gränsen* som en del av den fortsatta sökningen. Nu inkluderar poolen med distributions platser alla distributions platser från de tre konfigurerade gränserna och den sista distributions platsen som finns på plats serverdatorn.  Klienten fortsätter sedan att söka efter innehåll, ändra distributions platser varannan minut tills innehållet har hittats.

Genom att konfigurera de olika grann grupperna så att de blir tillgängliga vid olika tidpunkter, styr du när vissa distributions platser läggs till som en innehålls käll plats och när, eller om, använder klienten återställningen till standard platsens gränser grupp som säkerhets nät för innehåll som inte är tillgängligt från någon annan plats.


### <a name="update-existing-boundary-groups-to-the-new-model"></a><a name="bkmk_update"></a>Uppdatera befintliga gränser grupper till den nya modellen
När du installerar version 1609 och uppdaterar platsen görs följande konfigurationer automatiskt. Dessa är avsedda för att säkerställa att det aktuella återställnings beteendet är tillgängligt tills du konfigurerar nya gränser grupper och relationer.  
- Oskyddade distributions platser på en plats läggs till i *standardvärdet för plats gränser-grupp för \< platskod>* gränser för den platsen.
- En kopia görs av varje befintlig avgränsnings grupp som innehåller en plats server som kon figurer ATS med en långsam anslutning. Namnet på den nya gruppen är namnet på den *** \< ursprungliga avgränsnings gruppen>-långsamma-tmp***:  
  -   Plats system som har en snabb anslutning finns kvar i den ursprungliga avgränsnings gruppen.
  -   En kopia av plats system som har en långsam anslutning läggs till i kopian av gränser gruppen. De ursprungliga plats systemen som kon figurer ATS som långsamma finns kvar i den ursprungliga gränser-gruppen för bakåtkompatibilitet, men används inte från den aktuella gränser gruppen.
  -   Det finns inga associerade gränser för den här kopian av gräns gruppen. En återställnings länk skapas dock mellan den ursprungliga gruppen och den nya kopian av gräns gruppen som har återställnings tiden inställd på noll.

  I följande tabell visas den nya återställnings funktionen som du kan förväntar dig från kombinationen de ursprungliga distributions inställningarna och distributions plats konfigurationerna:

Ursprunglig distributions konfiguration för "kör inte program" i långsamt nätverk  |Ursprunglig distributions plats konfiguration för "Tillåt att klienten använder en återställnings käll plats för innehåll"  |Nytt återställnings beteende  
---------|---------|---------
Vald     |  Vald    |  **Ingen återställnings** punkt Använd endast distributions platser i den aktuella gränser gruppen       
Vald     |  Inte valt|  **Ingen återställnings** punkt Använd endast distributions platser i den aktuella gränser gruppen       
Inte valt |  Inte valt|  **Återgå till granne** – Använd distributions platserna i den aktuella gränser gruppen och Lägg sedan till distributions platserna från intilliggande avgränsnings grupp. Om inte en explicit länk till standard platsens gränser grupp konfigureras, kommer klienterna inte att återgå till den gruppen.    
Inte valt | Vald |   **Normal reserv** -Använd distributions platser i den aktuella gränser gruppen, sedan de från intilliggande och plats standard gränser grupper

 Alla andra distributions konfigurationer resulterar i **Normal reserv**.  



## <a name="office-365-client-management-dashboard"></a>Instrument panel för Office 365-klient hantering  
Configuration Manager 1609 Technical Preview introducerar en ny instrument panel. Om du vill visa instrument panelen går du till **Software Library**  >  **365 översikt över**program varu bibliotek i Configuration Manager-konsolen  >  **Office 365 Client Management**.
>[!NOTE]
>På arbets ytan **Nyheter** i Configuration Manager-konsolen har den nya instrument panelen felaktigt namnet **Office 365 service instrument panel**.

På instrument panelen visas diagram med följande:

- Antal Office 365-klienter
- Office 365-klient versioner
- Office 365-klient språk
- Office 365-klient kanaler     
Mer information finns i [Översikt över uppdateringskanaler för Office 365 ProPlus](https://docs.microsoft.com/deployoffice/overview-update-channels).
- Regler för automatisk distribution som har Office 365-klienten valt i uppsättningen tillgängliga produkter.

Du kan vidta följande åtgärder på instrument panelen:
- Överst på instrument panelen använder du List rutan **samling** för att filtrera instrument panels data efter medlemmar i en angiven samling.
- Klicka på **office 365 installations program** på den övre högra sidan av instrument panelen för att starta installations guiden för Office 365-klienten för att distribuera Office 365-appar till klienter. Mer information finns i [distribuera Office 365-appar till klienter](#deploy-office-365-apps-to-clients).
- Klicka på **skapa en ADR** i den mittersta högra sidan av instrument panelen för att öppna guiden automatisk distributions regel för att skapa en ny regel för automatisk distribution (ADR). Om du vill skapa en ADR för Office 365-appar väljer du **office 365-klienten** när du väljer produkten. Mer information finns i [distribuera program uppdateringar automatiskt](../../sum/deploy-use/automatically-deploy-software-updates.md).
- Klicka på **skapa klient agent inställningar** på den nedre högra sidan av instrument panelen för att öppna inställningarna för klient agenten. Mer information finns i [om klient inställningar](../clients/deploy/about-client-settings.md).



Mer information om uppdateringar för Office 365 ProPlus-uppdateringar finns i [Hantera Office 365 ProPlus updates med Configuration Manager](../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="deploy-office-365-apps-to-clients"></a>Distribuera Office 365-appar till klienter
I den här versionen kan du från instrument panelen för Office 365-klient hantering starta installations programmet för Office 365 som gör att du kan konfigurera installations inställningar för Office 365, hämta filer från Office Content Delivery Networks (CDN) och distribuera filerna som ett program i Configuration Manager.

### <a name="limitations-of-office-365-deployment"></a>Begränsningar för Office 365-distribution
- Du kan ha problem när du försöker importera befintliga klient inställningar (XML) i installations guiden för Office 365-appen. Du kan konfigurera klient inställningarna manuellt utan problem.

#### <a name="to-deploy-office-365-apps-to-clients"></a>Distribuera Office 365-appar till klienter
1. I Configuration Manager-konsolen navigerar du till översikt över **program varu bibliotek**  >  **Overview**  >  **kontor 365-klient hantering**.
2. Klicka på **Office 365 installations program** i det övre högra fönstret. Installations guiden för Office 365-klienten öppnas.
3. På sidan **program inställningar** anger du ett namn och en beskrivning för appen, anger nedladdnings platsen för filerna och klickar sedan på **Nästa**. Observera att platsen måste anges i formatet &#92;&#92;*server*&#92;*resurs*.
4. På sidan **Importera klient inställningar** väljer du om du vill importera klient inställningarna för Office 365 från en befintlig XML-konfigurationsfil eller ange inställningarna manuellt och klicka sedan på **Nästa**.
När du har en befintlig konfigurations fil anger du platsen för filen och hoppar till steg 7. Observera att platsen måste anges i formatet &#92;&#92;*server*&#92;*dela*&#92;*fil namn*. Fil.

    > [!IMPORTANT]
    >Du kan ha problem när du försöker importera befintliga klient inställningar (XML) i den här tekniska för hands versionen.

5. På sidan **klient produkter** väljer du den Office 365-svit som du använder, väljer de program som du vill inkludera, väljer eventuella ytterligare Office-produkter som ska inkluderas och klickar sedan på **Nästa**.
6. På sidan **klient inställningar** väljer du de inställningar som ska inkluderas och klickar sedan på **Nästa**.
7. På sidan **distribution** väljer du om du vill distribuera programmet och klickar sedan på **Nästa**.
Om du väljer att inte distribuera paketet i guiden går du vidare till steg 9.
8. Konfigurera resten av guide sidorna på samma sätt som för en typisk program distribution. Mer information finns i [skapa och distribuera ett program](../../apps/get-started/create-and-deploy-an-application.md).
9. Slutför guiden.
10. Du kan distribuera eller redigera programmet precis som med andra program i Configuration Manager från program **bibliotek**  >  **Översikt**  >  **program hanterings**  >  **program**.

>[!NOTE]
>När du har distribuerat Office 365-appar kan du skapa automatiska distributions regler för att underhålla apparna. Skapa en ADR för Office 365-appar genom att klicka på **skapa en ADR**och välja **Office 365-klient** när du väljer produkten. Mer information finns i [distribuera program uppdateringar automatiskt](../../sum/deploy-use/automatically-deploy-software-updates.md).

## <a name="improvements-for-bios-to-uefi-conversion"></a><a name="BKMK_UEFIConversion"></a>Förbättringar av BIOS till UEFI-konvertering
Nu kan du anpassa en aktivitetssekvens för operativ Systems distribution med en ny variabel, TSUEFIDrive, så att steget starta om datorn ska förbereda en FAT32-partition på hård disken för över gång till UEFI. Följande procedur visar ett exempel på hur du kan skapa steg i aktivitetssekvensen för att förbereda hård disken för BIOS till UEFI-konvertering.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Förbereda FAT32-partitionen för konvertering till UEFI:
I en befintlig aktivitetssekvens för att installera ett operativ system lägger du till en ny grupp med steg för att göra BIOS till UEFI-konvertering.

1. Skapa en ny aktivitetssekvens efter stegen för att avbilda filer och inställningar, och före stegen för att installera operativ systemet. Du kan till exempel skapa en grupp efter mappen **avbilda filer och inställningar som** heter **BIOS-till-UEFI**.
2. På fliken **alternativ** i den nya gruppen lägger du till en ny variabel för aktivitetssekvens som ett villkor där **_SMSTSBootUEFI** **inte är lika** med **Sant**. Detta förhindrar att stegen i gruppen körs när en dator redan är i UEFI-läge.
![BIOS till UEFI-grupp](media/BIOS-to-UEFI-group.png)
3. Under den nya gruppen lägger du till steget **starta om datorn** . I **Ange vad som ska köras efter omstart**väljer **du den Start avbildning som är tilldelad den här aktivitetssekvensen är markerad** för att starta datorn i Windows PE.  
4. På fliken **alternativ** lägger du till en aktivitetssekvens-variabel som ett villkor där **_SMSTSInWinPE är lika med falskt**. Detta förhindrar att det här steget körs om datorn redan finns i Windows PE.

    ![Steg för omstart av dator](media/Restart-in-Windows-PE.png)
5. Lägg till ett steg för att starta OEM-verktyget som kommer att konvertera den inbyggda program varan från BIOS till UEFI. Detta är vanligt vis en åtgärd för att **köra kommando rads** steg med en kommando rad för att starta OEM-verktyget.
5. Lägg till steget för att formatera och partitionera disk som kommer att partitionera och formatera hård disken. I steget gör du följande:
    1. Skapa FAT32-partitionen som ska konverteras till UEFI innan operativ systemet installeras. Välj **GPT** som **disk typ**.
    ![Disk steget formatera och partitionera](media/Format-and-partition-disk.png)
    2. Gå till egenskaperna för FAT32-partitionen. Ange **TSUEFIDrive** i fältet **variabel** . När den här variabeln identifieras av aktivitetssekvensen förbereds den för UEFI-över gången innan datorn startas om.
    ![Egenskaper för partition](media/Partition-properties.png)
    3. Skapa en NTFS-partition som motorn använder för att spara sitt tillstånd och lagra loggfiler.
6. Lägg till steget **starta om dator** i aktivitetssekvensen. I **Ange vad som ska köras efter omstart**väljer **du den Start avbildning som är tilldelad den här aktivitetssekvensen är markerad** för att starta datorn i Windows PE.  




## <a name="intune-compliance-charts"></a>Diagram över efterlevnad för Intune
I den här versionen får du en snabb överblick över övergripande kompatibilitet för enheter och de vanligaste orsakerna till bristande efterlevnad genom att använda nya diagram under **arbets ytan övervakning** i Configuration Manager-konsolen.

#### <a name="to-view-the-intune-compliance-charts"></a>Så här visar du scheman för Intune-efterlevnad
1. I Configuration Manager-konsolen går du till **övervakning**  >  **Översikt över**  >  **kompatibilitetsinställningar**.
2. Diagrammet **övergripande kompatibilitet för enhet** visas.
3. Klicka på noden **efterlevnadsprinciper** om du vill visa de övergripande diagrammen för **enhetens efterlevnad** och de **vanligaste orsakerna** .

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>Begränsningar i Intune-kompatibilitet diagram i TP 1609
- Det går inte att öka detalj nivån för diagrammets **allmänna enhets kompatibilitetstillstånd** .
- Diagrammet **över de vanligaste orsakerna till inkompatibiliteten** visar princip namnet och inte de enskilda orsakerna till inkompatibiliteten. Du kan klicka på principen för att öka detalj nivån och se vilka enheter som inte är kompatibla med principen.

### <a name="try-it-out"></a>Prova nu
Slutför följande avsnitt i ordning:

#### <a name="check-overall-compliance-chart"></a>Kontrol lera diagrammet för övergripande efterlevnad
1. Lägg till i två iOS-efterlevnadsprinciper i Configuration Manager. En princip bör ha en uppsättning inställningar för enheter (till exempel ange PIN-längd till 6). Den andra principen bör ha en annan uppsättning inställningar (till exempel PIN-komplexitet). Princip inställningarna ska inte överlappa eller vara i konflikt.
2. Distribuera de två principerna till en uppsättning användare.
3. Registrera två iOS-enheter i Intune med samma användar konto och ett konto som tog emot principerna i föregående steg. Enheterna bör inte uppfylla villkoren i policyn för efterlevnad.
4. I Configuration Manager kontrollerar du diagrammet **övergripande enhets efterlevnad** . Båda enheterna bör rapporteras som icke-kompatibla.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>Kontrol lera de vanligaste orsakerna till inkompatibilitet
5. Markera de **vanligaste orsakerna till inkompatibilitet** . Det här diagrammet visar de fem främsta orsakerna till inkompatibilitet, men när endast två kompatibilitetsinställningar har ställts in över principer visas endast de 2 vanligaste orsakerna.
6. Klicka på ett av avsnitten i diagrammet. Båda enheterna bör visas i den filtrerade vyn under **till gångar och efterlevnad**  >  **översikts**  >  **enhet**.

#### <a name="make-devices-compliant-and-check-the-charts"></a>Gör enheterna kompatibla och kontrol lera diagrammen
7. Gör en av de enheter som är kompatibla med en av principerna. Kontrol lera det övergripande diagrammet för **enhetskompatibilitet** igen. Diagrammet ska visa en kompatibel enhet och en icke-kompatibel enhet.
8. Gör den andra enheten kompatibel med samma princip. Detta gör en enhet kompatibel med båda principerna och en enhet som är kompatibel med endast en av principerna.
9. Markera de **vanligaste orsakerna till inkompatibilitet** . Det får bara finnas en icke-kompatibel orsak i listan.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Se även
[Teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md)
