---
title: Skapa konfigurations objekt för Windows
titleSuffix: Configuration Manager
description: Skapa konfigurations objekt för att hantera inställningar för Windows 10-datorer med lokal hantering av mobila enheter (MDM) i Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 26846066aa713d40fdacfe75810d43cafd1c3f04
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693683"
---
# <a name="create-configuration-items-for-windows-devices-with-on-premises-mdm-in-configuration-manager"></a>Skapa konfigurations objekt för Windows-enheter med lokal MDM i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd konfigurations objekt Configuration Manager **Windows 8,1 och Windows 10** för att hantera inställningar för Windows-enheter som du hanterar med lokal hantering av mobila enheter (MDM).

Mer allmän information om kompatibilitetsinställningar i Configuration Manager finns i följande artiklar:

- [Komma igång med kompatibilitetsinställningar](../../compliance/get-started/get-started-with-compliance-settings.md)

- [Planera för och konfigurera kompatibilitetsinställningar](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)

## <a name="create-a-configuration-item"></a>Skapa ett konfigurations objekt

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** , **expanderar kompatibilitetsinställningar och**väljer sedan noden **konfigurations objekt** .

1. Välj **skapa konfigurations objekt**i gruppen **skapa** på fliken **Start** i menyfliksområdet.

1. Ange följande information på sidan **Allmänt** i **guiden skapa konfigurations objekt**:

    - **Namn**: ett unikt namn som identifierar detta konfigurations objekt.

    - **Beskrivning**: en valfri beskrivning som ger ytterligare information om hur den används.

    - Under **Inställningar för enheter som hanteras *utan* Configuration Manager-klienten väljer du** **Windows 8,1 och Windows 10**.

    - **Kategorier**: du kan skapa och tilldela kategorier som hjälper dig att söka efter och filtrera konfigurations objekt i Configuration Manager-konsolen.

1. På sidan **plattformar som stöds** i guiden väljer du de Windows-plattformar som ska utvärdera detta konfigurations objekt.

1. På sidan **enhets inställningar** väljer du de inställnings grupper som du vill konfigurera. Mer information om de tillgängliga inställningarna finns i [Inställningar referens](#bkmk_setref).

    > [!TIP]
    > Om den inställning som du vill använda inte visas väljer du alternativet för att **Konfigurera ytterligare inställningar som inte finns i standardinställnings grupperna**. Med det här alternativet läggs sidan **ytterligare inställningar** till i guiden.

1. Konfigurera de nödvändiga inställningarna på varje inställnings sida. När inställningarna har stöd för det kan du också **Reparera inkompatibla inställningar**. Om en enhet utvärderar inställningen som inkompatibel med detta konfigurations objekt, åtgärdas inställningen så att den blir kompatibel.

    För varje inställnings grupp kan du också konfigurera allvarlighets graden som rapporteras när inställningen är inkompatibel. Välj något av följande värden för alternativet **allvarlighets grad för inkompatibilitet för rapporter** :

    - **Ingen**: enheter som inte uppfyller den här regeln rapporterar inte allvarlighets grad för Configuration Manager rapporter.

    - **Information**

    - **Varning**

    - **Kritiskt**

    - **Kritisk med händelse**: enheter som inte uppfyller den här regeln rapporterar allvarlighets graden **kritisk** för Configuration Manager rapporter. Den loggar också inkompatibla tillstånd som en Windows-händelse i program händelse loggen.

1. På sidan **plattforms tillämplighet** i guiden granskar du alla inställningar som inte är kompatibla med de valda plattformarna som stöds. Gå tillbaka och ta bort inställningarna, ändra support plattformarna eller Fortsätt.

    > [!IMPORTANT]
    > Enheterna bedömer inte kompatibiliteten för inställningar som inte stöds.

1. Slutför guiden.

Du kan visa det nya konfigurationsobjektet i noden **Konfigurationsobjekt** på arbetsytan **Tillgångar och efterlevnad** .

## <a name="settings-reference"></a><a name="bkmk_setref"></a> Inställnings referens  

I följande avsnitt beskrivs de olika inställningarna som är tillgängliga i varje grupp. Konfigurera de här inställningarna på sidan **enhets inställningar** i **guiden skapa konfigurations objekt** för **Windows 8,1-och Windows 10** -enheter som hanteras *utan* Configuration Manager-klienten.

### <a name="password"></a>lösenordsinställning

Dessa inställningar gäller endast för enheter som kör Windows 10 och senare.

- **Kräv lösen ords inställningar på enheter**: Kräv ett lösen ord på enheter som stöds.
- **Minsta längd på lösen ord (tecken)**: minsta längd på lösen ordet.
- **Lösen ordets giltighets tid i dagar**: antalet dagar innan användaren måste ändra sina lösen ord.
- **Antal lagrade lösen ord**: förhindrar åter användning av tidigare använda lösen ord.
- **Antal misslyckade inloggnings försök innan enheten rensas**: om detta antal inloggnings försök Miss lyckas rensar MDM enheten
- **Tid av inaktivitet innan enheten låses**: Ange hur lång tid en enhet kan vara inaktiv innan den låses. Enheten är inaktiv när det inte finns några användarindata.
- **Lösen ords komplexitet**: Välj om du kan ange en numerisk PIN-kod, till exempel `1234` , eller om du måste ange ett starkt lösen ord.
  - **Antal avancerade teckenuppsättningar som krävs i lösen ord**: om lösen ords komplexiteten är **stark**väljer du hur många typer av tecken lösen ordet kräver: versaler, gemener, siffror eller symboler. Som standard är det här värdet `2` .
- **Skicka PIN-koden för återställning av lösenord till Exchange Server**

### <a name="device"></a>Enhet

- **Skärmdump**: Aktivera den här inställningen så att användaren kan ta en skärm bild av enhetens bildskärm. (Endast Windows 10)
- **Sändning av diagnostikdata**: Aktivera den här inställningen för att tillåta diagnostikdata i Windows för analys. (Endast Windows 8.1)
- **Tillåt sändning av diagnostikdata (Windows 10)**: ange nivån för Windows-diagnostikdata för analys: inaktivera, grundläggande, utökad eller fullständig. (Endast Windows 10)
- **Geolokalisering**: Aktivera den här inställningen för att tillåta att enheten använder plats tjänst information. (Endast Windows 10)
- **Kopiera och klistra in**: Aktivera den här inställningen om du vill använda kopiera och klistra in för att överföra data mellan appar. (Endast Windows 10)
- **Fabriks återställning**: Aktivera den här inställningen för att tillåta att användaren återställer enheten till de ursprungliga inställningarna. (Endast Windows 10)
- **Bluetooth**: Tillåt eller förhindra användning av enhetens Bluetooth-kapacitet.
- **Läge för identifierbart Bluetooth**: Tillåt eller förhindra att enheten kan identifieras av andra Bluetooth-enheter. (Endast Windows 10)
- **Bluetooth-annonsering**: Tillåt eller förhindra användning av Bluetooth-annonsering. (Endast Windows 10)
- **Röst inspelning**: Tillåt eller förhindra användning av enhetens röst inspelnings funktioner. (Endast Windows 10)
- **Cortana**: Tillåt eller förhindra användning av Cortana-röst assistenten. (Endast Windows 10)
- **Aviseringar från åtgärds Center**: Aktivera eller inaktivera meddelande fönstret i Windows 10. (Endast Windows 10)
- **Ändring av regions inställningar (endast skriv bord)**: Tillåt eller förhindra att användaren ändrar de nationella inställningarna på enheten.
- **Ändra energi-och vilo läges inställningar (endast skriv bord)**: Tillåt eller förhindra att användaren ändrar energi-och vilo läges inställningar på enheten.
- **Ändra språk inställningar (endast skriv bord)**: Tillåt eller förhindra att användaren ändrar språk inställningarna på enheten.
- **Ändring av system tid**: Tillåt eller förhindra att användaren ändrar enhetens datum och tid.
- **Ändring av enhets namn**: Tillåt eller förhindra att användaren ändrar enhetens namn.

### <a name="email-management"></a>E-posthantering

Dessa inställningar gäller för enheter som kör Windows 8.1 och Windows 10.  

- **Pop-och IMAP-e-post**: Tillåt eller förhindra anslutningar till e-postkonton som använder pop-och IMAP-standarder.
- **Maximal tid att behålla e-post**: hur lång tid det tar att behålla e-post innan servern tar bort den.
- **Tillåtna meddelande format**: Ange om e-postmeddelanden är **oformaterad text** eller **HTML och oformaterad text**.
- **Maximal storlek för e-post i oformaterad text (hämtas automatiskt)**: Ange den maximala storleken för e-postmeddelanden i oformaterad text när de hämtas automatiskt.
- **Maximal storlek för HTML-e-post (hämtas automatiskt)**: Ange den maximala storleken för HTML-e-postmeddelanden när de hämtas automatiskt.
- **Maximal storlek på bifogad fil (hämtas automatiskt)**: Ange den maximala storleken på e-postbilagor som hämtas automatiskt.
- **Synkronisering av kalender**: Tillåt eller förhindra synkronisering av kalendrar till enheten.
- **Anpassat e-postkonto**: Tillåt eller förhindra användning av ett e-postkonto som inte är ett organisations konto på enheten.
- **Gör Microsoft-konto valfritt i Windows Mail-app**: aktivera det här alternativet om du inte behöver ett Microsoft-konto i Windows Mail.

### <a name="store"></a>Lagringsplats

Dessa inställningar gäller endast för enheter som kör Windows 10 och senare.

- **Program Arkiv**: Tillåt eller förhindra åtkomst till Microsoft Store på enheten.
- **Ange ett lösen ord för att komma åt program arkivet**: aktivera det här alternativet om du vill kräva att användarna anger ett lösen ord för att få åtkomst till Microsoft Store-appen.
- **Köp via app**: Tillåt eller förhindra att användare gör köp i appen.
- **Start av app från Store**: inaktivera alla appar som har förinstallerats på enheten eller installerats från Microsoft Store.
- **Uppdatera appar automatiskt från Store**: Tillåt eller förhindra att appar som är installerade från Microsoft Store uppdateras automatiskt.
- **Installera appar på systemen het**: Tillåt eller förhindra att enheten installerar appar på system enheten, vilket vanligt vis är `C:` enheten.
- **Installera AppData på system volym**: aktivera det här alternativet om du vill tillåta att appar lagrar data på system enheten.
- **Använd endast privat lagring**: Kräv att användare laddar ned appar från ditt privata arkiv.
- **Spel-DVR**: inaktivera inspelning och sändning av Windows-spel

### <a name="browser"></a>Webbläsare

Dessa inställningar gäller för enheter som kör Windows 8.1 och Windows 10.

- **Tillåt webbläsare**: Tillåt eller förhindra användning av webbläsaren på enheten.
- **Autofyll**: Tillåt eller förhindra att ändra inställningar för Komplettera automatiskt i webbläsaren.
- **Active Scripting**: Tillåt eller förhindra om webbläsaren kan köra skript, till exempel ActiveX-skript.
- **Plugin-program**: Tillåt eller förhindra tillägg av plugin-program i Internet Explorer.
- Blockering av **popup-** fönster: Tillåt eller förhindra webbläsarens blockering av popup-fönster.
- **Cookies**: Tillåt eller förhindra att cookies sparas på enheten.
- **Bedrägeri varning**: Tillåt eller förhindra varningar för potentiella bedrägliga webbplatser.

### <a name="internet-explorer"></a>Internet Explorer

Dessa inställningar gäller för enheter som kör Windows 8.1 och Windows 10.

- **Skicka alltid spåra inte-huvud**: Tillåt eller förhindra att information skickas till tredje parts webbplatser.
- **Intranätets säkerhets zon**: Tillåt eller förhindra tilldelning av säkerhets nivåer till intranätets säkerhets zon.
- **Säkerhets nivå för zonen Internet**: Ange säkerhets nivån för zonen Internet: hög, medel högt eller medel.
- **Säkerhets nivå för zonen Intranät**: Ange säkerhets nivån för zonen Intranät: hög, medium-hög, medium, medium-Low eller Low.
- **Säkerhets nivå för zonen betrodda**platser: Ange säkerhets nivån för zonen betrodda platser: hög, medium-hög, medium, medium-Low eller Low.
- **Säkerhets nivå för zonen ej betrodda platser**: Ange säkerhets nivån för zonen ej betrodda platser: hög.
- **Namn områden för zonen Intranät**: Konfigurera webbplatser som ska läggas till eller tas bort från zonen Intranät.
- **Gå till intranäts plats för enstaka ord**: Tillåt eller förhindra att Internet Explorer automatiskt går till en intranäts plats om användaren anger ett giltigt plats namn utan föregående protokoll, till exempel `https://` .
- **Meny alternativet Enterprise-läge**: gör att användare kan aktivera och inaktivera Enterprise-läget från **verktyg** -menyn i Internet Explorer.
  - **Loggnings rapport plats (URL)**: när Enterprise-läget är aktivt anger du en URL för att logga besökta webbplatser.
- **Plats för webbplats lista för företags läge (URL)**: när Enterprise-läget är aktivt anger du listan över webbplatser som använder den.

### <a name="cloud"></a>Moln

Dessa inställningar gäller för enheter som kör Windows 8.1 och Windows 10.

- **Synkronisering av inställningar**: Tillåt eller förhindra att inställningar synkroniseras mellan enheter.
- **Synkronisering av autentiseringsuppgifter**: Tillåt eller förhindra autentiseringsuppgifter för synkronisering mellan enheter.
- **Microsoft-konto**: Aktivera den här inställningen för att tillåta användning av en Microsoft-konto på enheten.
- **Synkronisering av inställningar över anslutningar med datapriser**: Tillåt eller förhindra att inställningar synkroniseras när nätverks anslutningen mäts.

### <a name="security"></a>Säkerhet

- **Osignerad fil installation**: tillåter vem som kan installera en osignerad fil. (Endast Windows 10)
- **Osignerade program**: Tillåt eller förhindra att osignerade appar installeras. (Endast Windows 10)
- **SMS och MMS**: Tillåt eller förhindra SMS-meddelanden på enheten. (Endast Windows 10)
- **Flyttbara lagringsmedia**: Tillåt eller förhindra användning av flyttbara lagringsmedia, t. ex. ett SD-kort. (Endast Windows 10)
- **Kamera**: Tillåt eller förhindra användning av enhetens kamera. (Endast Windows 10)
- **NFC (nära fält kommunikation)**: Tillåt eller förhindra kommunikation med hjälp av NFC. (Endast Windows 10)
- **Stöldskydds läge**: Tillåt eller förhindra användning av Windows 10 stöldskydds läge. (Endast Windows 10)
- **Tillåt USB-anslutning**: Tillåt eller förhindra andra enheter att ansluta till den här enheten med en USB-anslutning. (Endast Windows 10)
- **Windows RT VPN-profil**: etablerar en VPN-profil för Windows RT-enheter (endast Windows 8,1)

### <a name="peak-synchronization"></a>Synkronisering vid högsta användningsnivå

Dessa inställningar gäller endast för enheter som kör Windows 10 och senare.

- **Ange hög belastnings tid**: Ange den högsta tillåtna tiden och vecko dagarna för synkronisering av mobila enheter.
- **Synkroniseringsfrekvens vid hög belastning**: konfigurera hur ofta synkroniseringen ska ske under de högsta timmarna.
- **Synkroniseringsfrekvens vid låg belastning**: konfigurera hur ofta synkronisering sker utanför det högsta antalet timmar.

### <a name="roaming"></a>Nätverksväxling

- **Enhets hantering vid nätverks växling**: Tillåt eller förhindra Configuration Manager från att hantera enheten vid nätverks växling. (Endast Windows 10)
- **Hämtning av program vara vid nätverks växling**: Tillåt eller förhindra nedladdning av appar och program vara vid nätverks växling. (Endast Windows 10)
- **Hämtning av e-post vid nätverks växling**: Tillåt eller förhindra att e-post hämtas vid nätverks växling. (Endast Windows 10)
- **Data nätverks växling**: Tillåt eller förhindra nätverks växling mellan nätverk vid åtkomst till data.
- **VPN via mobil nät**: Tillåt eller förhindra att enheten använder en VPN-anslutning när den är ansluten till ett mobil nät verk. (Endast Windows 10)
- **VPN-roaming via mobil nät**: Tillåt eller förhindra att enheten använder en VPN-anslutning under nätverks växling på ett mobil nät verk. (Endast Windows 10)

### <a name="encryption"></a>Kryptering

- **Kryptering av lagrings kort**: Ange på om du vill kräva att användaren krypterar alla minnes kort som används i enheten. (Endast Windows 10)
- **Fil kryptering på enhet**: inställt på för att kryptera filer som lagras på enheten.
- **Kräv e-postsignering**: användaren måste signera e-postmeddelanden digitalt innan de skickas.
  - **Signeringsalgoritm**: Välj algoritm för signering av e-post: standard, SHA eller MD5
- **Kräv e-postkryptering**: användaren måste kryptera e-post innan de skickas.
  - **Krypteringsalgoritm**: Välj algoritm för kryptering av e-post: standard, tredubbel DES, des, RC2 128-bit, RC2 64-bit, RC2 40-bit

### <a name="wireless-communications"></a>Trådlös kommunikation

Dessa inställningar gäller endast för enheter som kör Windows 10 och senare.

- **Trådlös nätverks anslutning**: Tillåt eller förhindra enhetens Wi-Fi-funktion.
- **Trådlös Internet delning**: gör att användaren kan använda enheten som ett mobilt hotspot-nätverk.
- **Avlasta data till Wi-Fi när**det är möjligt: Aktivera enheten för att använda Wi-Fi-anslutningen så mycket som möjligt.
- **Rapportering för trådlös hotspot**: gör att enheten kan skicka information om Wi-Fi-anslutningar för att hjälpa användaren att identifiera närliggande anslutningar.
- **Manuell Wi-Fi-konfiguration**: gör det möjligt för användaren att manuellt konfigurera trådlösa anslutningar.

#### <a name="configured-wireless-network-connections"></a>Konfigurerade trådlösa nätverks anslutningar

1. På sidan **Konfigurera inställningar för trådlös kommunikation med mobila enheter** väljer du **Lägg till**.

1. I fönstret **trådlös nätverks anslutning** anger du följande information om den trådlösa anslutningen som ska etableras på mobila enheter:

    - **Nätverks namn (SSID)**: Ange namnet på Wi-Fi-nätverket.
    - **Nätverks anslutning**: Välj antingen **Internet** eller **arbete**.
    - **Autentisering**: Välj autentiseringsmetod för den trådlösa anslutningen:
        - **Öppna**
        - **Delad**
        - **WPA**
        - **WPA-PSK**
        - **WPA2**
        - **WPA2-PSK**
    - **Data kryptering**: Välj den krypterings metod som används av den här anslutningen. De tillgängliga värdena ändras baserat på den **autentiseringsmetod** du väljer:
        - **Disabled** (Inaktiverat)
        - **WEP**
        - **TKIP**
        - **AES**
    - **Nyckel index**: när du anger **data kryptering** till **WEP**väljer du ett nyckel index från **1** till **4**.
    - **Det här nätverket ansluter till Internet**: ange proxyinställningar för att tillåta att mobila enheter i ett trådlöst nätverk ansluter till Internet.
        - **Inställningar för proxyserver**: konfigurera **servern** och **port** inställningarna för **http**-, **WAP**-och **socket** -proxyservrar.
    - **802.1 x-inställningar**:
        - **Aktivera 802.1 x-nätverks åtkomst**: skydda anslutningen genom att ange en EAP-typ.
        - **EAP-typ**: Välj något av följande autentiseringsprotokoll:
            - **PEAP**
            - **Smartkort eller certifikat**

### <a name="certificates"></a>Certifikat

Importera certifikat som ska installeras på mobila enheter.

Välj **Importera**och ange sedan följande värden:

- **Certifikat fil**: Bläddra till och välj en certifikat fil (**. cer**) som ska importeras.
- **Mål Arkiv**: Välj ett eller flera av följande certifikat Arkiv:
  - **Rot**
  - **CA**
  - **Normal**
  - **Med privilegier**
  - **SPC**
  - **Peer**
- **Roll**: om du väljer certifikat arkivet **SPC** (Software Publisher Certificate) väljer du den roll som ska associeras med certifikatet:
  - **Mobiloperatör**
  - **Ansvarig**
  - **Användaren har autentiserats**
  - **IT-administratör**
  - **Användaren har inte autentiserats**
  - **Betrodd etableringsserver**

### <a name="system-security"></a>Systemsäkerhet

- **User Account Control**: Konfigurera Windows-User Account Controls beteende på enheten.
- **Nätverks brand vägg**: Kräv att Windows ska aktivera den inbyggda brand väggen. (Windows 8,1)
- **Uppdateringar**: Konfigurera Windows-programuppdateringarnas beteende. (Windows 8,1)
  - **Lägsta klassificering av uppdateringar**: Välj den lägsta klassificeringen av uppdateringar som ska hämtas och installeras: **ingen**, **viktig**eller **Rekommenderad**.
- **Uppdateringar (Windows 10)**: konfigurera beteendet för Windows-program uppdateringar. (Endast Windows 10)
  - **Installations dag**: Välj den schemalagda dag då enheten automatiskt installerar uppdateringar och omstarter. (Endast Windows 10)
  - **Installations tid**: Välj den schemalagda tid när enheten installerar uppdateringar och omstarter automatiskt. (Endast Windows 10)
- **SmartScreen**: Aktivera eller inaktivera Smart skärm i Windows.
- **Virus skydd**: Kräv att Windows har antivirus program.
- **Virus skyddets signaturer är uppdaterade**: Kräv att antivirus programmets signaturfiler är aktuella.
- **Meddelande vy för lås skärmen**: Aktivera eller inaktivera aviseringar som ska visas på Lås skärmen.
- **För hands versions funktioner**: Ange om enheten ska acceptera för hands versions inställningar och-funktioner. (Endast Windows 10)
- **Manuell installation av rot certifikat**: Aktivera eller inaktivera användaren för att manuellt installera ett rot certifikat, vilket möjliggör förtroende för alla certifikat som utfärdas av roten. (Endast Windows 10)
- **Tillåt manuell avregistrering**: Tillåt eller förhindra att användaren avregistrerar enheten från lokal hantering av mobila enheter med Configuration Manager.

### <a name="windows-server-work-folders"></a>Windows Server-arbetsmappar

Dessa inställningar gäller för enheter som kör Windows 8.1 och Windows 10.

- **URL för arbetsmappar**: Ange platsen för en Windows Server-arbetsmapp som användarna kan ansluta till från sin enhet.

### <a name="allowed-and-blocked-apps-list"></a>Lista över tillåtna och blockerade appar

Dessa inställningar gäller endast för enheter som kör Windows Phone, som Configuration Manager lokalt MDM inte stöder. Mer information finns i [vad hände med hybrid?](../understand/what-happened-to-hybrid.md).

### <a name="windows-10-team"></a>Windows 10-teamet

Dessa inställningar gäller endast för enheter som kör Windows 10 team.

- **Tillåt att skärmen aktive ras automatiskt när sensorer identifierar någon i rummet**: Tillåt eller förhindra att enheten aktive ras automatiskt när dess sensor känner av att någon är i rummet.
- **Kräv PIN-kod för trådlös projektion**: Aktivera eller inaktivera om du måste ange en PIN-kod innan en annan enhet kan ansluta trådlöst för projektion.
- **Underhålls period**: Aktivera den här inställningen för att konfigurera fönstret när uppdateringar kan installera och starta om enheten.
  - **Start tid**: Ange start tiden för underhålls perioden.
  - **Varaktighet (timmar)**: ange längden i timmar för underhålls perioden.
- **Azure Operational Insights**: tillåt [Azure Operational Insights](https://azure.microsoft.com/resources/videos/azure-operational-insights-overview/) att samla in, lagra och analysera logg fils data från Windows 10 team-enheter.
  - **Arbetsyte-ID**: Ange ett giltigt arbetsyte-ID
  - **Arbets**ytans nyckel: Ange nyckeln för den associerade arbets ytan
- **Trådlös Miracast-projektion**: Tillåt att Miracast-aktiverade enheter projiceras till den här Windows 10 team-enheten.
  - **Miracast-kanal**: Välj en Miracast-kanal för att projicera innehåll.
- **Mötes information som visas på Välkomst skärmen**: Välj den typ av information som enheten visar på panelen **möten** på **välkomst** skärmen:
  - **Visa endast kalender och tid**
  - **Visa kalender, tid och ämne (ämnet är dolt för privata möten)**
- **URL för låsskärm bakgrunds bild**: Ange en URL för att visa en anpassad bakgrund på **välkomst** skärmen på en Windows 10 team-enhet. Starta URL: en med `https://` och Använd PNG-formatet.

### <a name="windows-information-protection"></a>Windows informationsskydd  

Mer information om hur du konfigurerar företags data skydd med Configuration Manager finns i [skydda företags data med Windows information Protection (Pia)](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).

### <a name="microsoft-edge-legacy"></a>Microsoft Edge-bakåtkompatibelt

Dessa inställningar gäller endast för enheter som kör Windows 10 och senare.  

- **Tillåt Sök förslag i adress fältet**: låt sökmotorn föreslå platser när du skriver Sök fraser.
- **Tillåt spåra inte**: informera webbplatser som du inte vill att de ska spåra ditt besök.
- **Aktivera SmartScreen**: kontrol lera att hämtade filer inte innehåller skadlig kod.
- **Tillåt popup-fönster**: Konfigurera popup-fönster i webbläsaren.
- **Tillåt cookies**: Konfigurera användningen av cookies.
- **Tillåt Autofyll**: låt webbläsaren fylla i formulär automatiskt med lagrad information, t. ex. namn, adress och telefonnummer.
- **Tillåt lösen ords hanteraren**: låt webbläsaren lagra och hantera lösen ord för webbplatser.
- **Utvecklarverktyg**: Tillåt eller förhindra funktionen för utvecklarverktyg i Edge.
- **Tillägg**: Tillåt eller förhindra Edge-tillägg.
- **InPrivate-surfning**: Tillåt eller förhindra InPrivate-surfning, som inte lagrar historik eller cookies.
- **WebRTC localhost-IP-adress**: Tillåt eller förhindra att enhetens LOCALHOST-IP-adress visas när användaren ringer telefonsamtal med hjälp av webb-protokollet.
- **Blockera åtkomst till about: Flags**: Tillåt eller förhindra att användaren kommer åt `about:flags` sidan, som innehåller inställningar för utvecklare och experiment.
- **Åsidosättning av SmartScreen-meddelande för filer**: Tillåt eller förhindra att användaren kringgår SmartScreen-filtrets varningar om nedladdning av potentiellt skadliga filer.
- **Åsidosättning av SmartScreen-meddelande**: Tillåt eller förhindra att användaren kringgår SmartScreen-filtrets varningar om potentiellt skadliga webbplatser.
- **Första körnings webb adress**: Ange en webbplats som ska visas när en användare öppnar Edge för första gången.

### <a name="windows-defender-antivirus"></a>Windows Defender Antivirus

Dessa inställningar gäller endast för enheter som kör Windows 10 och senare.

- **Tillåt övervakning i real tid**: Aktivera genomsökning i real tid efter skadlig kod, spionprogram och annan oönskad program vara.
- **Tillåt beteende övervakning**: Defender söker efter vissa kända mönster på misstänkt aktivitet på enheter.
- **Aktivera kontrollsystem för nätverk**: kontrollsystem för nätverk (NIS) hjälper till att skydda enheter mot nätverksbaserade sårbarheter. Det använder signaturer för kända problem från Microsoft Endpoint Protection Center för att identifiera och blockera skadlig trafik.
- **Sök igenom alla hämtningar**: Defender söker igenom alla filer som du hämtar från Internet.
- **Tillåt skript genomsökning**: Defender söker igenom skript som används i Internet Explorer.
- **Övervaka fil-och program aktivitet**: Defender övervakar fil-och program aktivitet på enheter.
  - **Övervakade filer**: Välj den typ av filer som ska övervakas: alla, inkommande eller utgående.
- **Dagar som löst skadlig kod ska spåras**: Defender fortsätter att spåra skadlig kod för det antal dagar som du anger. Sedan kan du kontrol lera tidigare berörda enheter manuellt. Om du anger antalet dagar till 0 förblir skadlig kod kvar i mappen karantän och tas inte bort automatiskt. Det maximala värdet är 90.
- **Tillåt klientens användar gränssnitts åtkomst**: anger om användar gränssnittet för Defender ska döljas från användare. När du ändrar den här inställningen börjar den gälla nästa gång enheten startas om.
- **Schemalägg en Systems ökning**: Välj antingen en fullständig eller snabb sökning som inträffar regelbundet på den dag och tid som du väljer:
  - **Schemalagd dag**: Välj den schemalagda dag då Defender kör sökningen.
  - **Schemalagd tid**: Välj den schemalagda tid då Defender kör sökningen.
- **Schemalägg daglig snabb sökning**: Välj den schemalagda tid då Defender kör en snabb genomsökning varje dag.
- **Begränsa processor användning under en sökning**: Ange den procent andel av processorn som Defender kan använda när en sökning körs. Ange ett värde mellan 1 och 100.
- **Sök igenom arkivfiler**: Defender genomsöker komprimerade Arkiv, t. ex. zip-eller CAB-filer.
- **Sök igenom e-postmeddelanden**: Defender söker igenom e-postmeddelanden när de tas emot på enheten.
- **Genomsök flyttbara enheter**: Defender söker igenom flyttbara enheter, till exempel USB-käppar.
- **Sök igenom mappade enheter**: Defender söker igenom enheter som är mappade till nätverks resurser. Till exempel `H:` mappas till en användares personliga enhet. Om filerna på enheten är skrivskyddade kan inte Defender ta bort skadlig kod som hittas där.
- **Sök igenom filer öppnade från delade**nätverksmappar: Defender söker igenom filer när en användare öppnar dem från en delad nätverks Sök väg. Till exempel `\\server\share\file.doc`. Om filen på resursen är skrivskyddad kan inte Defender ta bort skadlig kod som hittas.
- **Uppdaterings intervall för signatur**: Välj det tidsintervall då Defender söker efter nya signaturfiler.
- **Tillåt moln skydd**: Defender använder Microsoft-molnet för att ta emot information om aktivitet för skadlig kod och aktivera funktioner som blockera vid första sikten.
- **Uppmana användarna att skicka exempel**: Välj beteende för Defender när filer kan kräva ytterligare analys. Till exempel kan Defender automatiskt skicka filer till Microsoft för att avgöra om de är skadliga.
- **Identifiering av potentiellt oönskade program**: skyddar enheten mot att köra program vara som klassificeras av Defender som potentiellt oönskade. Du kan skydda dig mot dessa program som körs eller använda gransknings läget för att rapportera när en användare installerar ett potentiellt oönskat program.
- **Filer och**mappar som ska undantas: Lägg till en eller flera filer och mappar i undantags listan. Exempel: `C:\Path` eller `%ProgramFiles%\Path\filename.exe`. Defender inkluderar inte dessa filer och mappar i real tids-eller schemalagda genomsökningar.
- **Undantag för fil tillägg**: Lägg till ett eller flera fil namns tillägg i undantags listan. Exempel: `java` eller `exe`. Defender inkluderar inga filer med dessa fil namns tillägg i real tids-eller schemalagda genomsökningar.
- **Process undantag**: Lägg till vissa processer i undantags listan. Till exempel `C:\path\myproc.exe`. Den här typen av undantag stöder endast följande tillägg: `exe` , `com` , eller `scr` . Defender inkluderar inte dessa processer i real tids-eller schemalagda genomsökningar.

### <a name="additional-settings"></a>Ytterligare inställningar

På sidan **enhets inställningar** i guiden, om du väljer alternativet för att **Konfigurera ytterligare inställningar som inte finns i standardinställnings grupperna**, använder du den här **ytterligare inställnings** sidan för att konfigurera dessa inställningar. Välj **Lägg till** och välj sedan i listan med tillgängliga mobil inställningar. Välj **Välj** om du vill ändra den inbyggda inställningen eller **Skapa inställning** för att skapa ett anpassat register värde eller en typ av OMA-URI-inställning.

## <a name="next-steps"></a>Nästa steg

[Övervaka kompatibilitetsinställningar](../../compliance/deploy-use/monitor-compliance-settings.md)