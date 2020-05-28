---
title: Teknisk referens för kryptografiska kontroller
titleSuffix: Configuration Manager
description: Lär dig hur signering och kryptering kan hjälpa till att skydda attacker från att läsa data i Configuration Manager.
ms.date: 12/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 623a8dab52e13c4674b961e825033430d34a8f88
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906552"
---
# <a name="cryptographic-controls-technical-reference"></a>Teknisk referens för kryptografiska kontroller

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager använder signering och kryptering för att skydda hanteringen av enheterna i Configuration Manager hierarkin. Vid signering, om data har ändrats under överföringen, ignoreras de. Kryptering bidrar till att förhindra att en angripare läser data med hjälp av en nätverks protokoll analys.  

 Den primära hash-algoritm som Configuration Manager använder för signering är SHA-256. När två Configuration Manager-platser kommunicerar med varandra signerar de sin kommunikation med SHA-256. Den primära krypteringsalgoritm som implementeras i Configuration Manager är 3DES. Detta används för att lagra data i Configuration Manager-databasen och för klient-HTTP-kommunikation. När du använder klient kommunikation via HTTPS kan du konfigurera din PKI (Public Key Infrastructure) att använda RSA-certifikat med de maximala hash-algoritmer och nyckel längder som dokumenteras i [PKI-certifikat krav](../network/pki-certificate-requirements.md).  

 För de flesta kryptografiska åtgärder för Windows-baserade operativ system använder Configuration Manager SHA-2, 3DES och AES och RSA-algoritmer från Windows CryptoAPI-biblioteket rsaenh. dll.  

> [!IMPORTANT]  
>  Visa information om rekommenderade ändringar som svar på SSL-säkerhetsproblem i [About SSL Vulnerabilities](#about-ssl-vulnerabilities).  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Kryptografiska kontroller för Configuration Manager åtgärder  
 Information i Configuration Manager kan signeras och krypteras, oavsett om du använder PKI-certifikat med Configuration Manager.  

### <a name="policy-signing-and-encryption"></a>Princip signering och kryptering  
 Klientprinciptilldelningar signeras av den självsignerade platsservens signeringscertifikat för att bidra till att eliminera säkerhetsrisken med en utsatt hanteringsplats som skickar principer som har manipulerats. Detta är viktigt om du använder Internetbaserad klient hantering eftersom den här miljön kräver en hanterings plats som exponeras för Internetkommunikation.  

 Principen krypteras med 3DES när den innehåller känsliga data. En princip som innehåller känsliga data skickas enbart till auktoriserade klienter En princip som inte har några känsliga data krypteras inte.  

 När en princip lagras på klienterna krypteras den med Data Protection application programming interface (DPAPI).  

### <a name="policy-hashing"></a>Princip-hashing  
 När Configuration Manager-klienter begär en princip, får de först en princip tilldelning så att de vet vilka principer som gäller för dem, och de begär endast dessa princip texter. Varje principtilldelning innehåller den beräknade hashen för motsvarande principinnehåll. Klienten hämtar lämpligt principinnehåll och beräknar sedan hashen för innehållet. Om hashen för det nedladdade principinnehållet inte matchar hashen i principtilldelningen ignorerar klienten principinnehållet.  

 Hash-algoritmen för principen är SHA-1 och SHA-256.  

### <a name="content-hashing"></a>Hashing av innehåll  

Distributionshanterartjänsten på platsservern hashar innehållsfilerna för alla paket. Principleverantören tar med hashen i programvarans distributionsprincip. När den Configuration Manager klienten laddar ned innehållet återskapar klienten hashen lokalt och jämför den med den som anges i principen. Om hash-värdena matchar har innehållet inte ändrats och det installeras av klienten. Om en enda byte med innehåll har ändrats matchar inte hashvärdena och programvaran installeras inte. Den här kontrollen bidrar till att säkerställa att korrekt programvara installerats eftersom det faktiska innehållet dubbelkontrolleras mot principen.  

Den hash-algoritm som används som standard för innehåll är SHA-256.

Det är inte alla enheter som har stöd för innehållshashing. Undantagen är:  

- Windows-klienter när de strömmar App-V-innehåll.  

- Windows Phone klienter, men dessa klienter verifierar signaturen för ett program som har signerats av en betrodd källa.  

- Windows RT-klienten, men de här klienterna verifierar signaturen för ett program som har signerats av en betrodd källa och även använder PFN-verifiering (paketets fullständiga namn).  

- Klienter som kör på versioner av Linux och UNIX som inte har stöd för SHA-256. Mer information finns i [Planera för klient distribution till Linux-och UNIX-datorer](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).  

### <a name="inventory-signing-and-encryption"></a>Signering och kryptering av inventering  
 En inventering som klienter skickar till hanteringsplatserna signeras alltid av enheterna, oberoende av om de kommunicerar med hanteringsplatserna via HTTP eller HTTPS. Om de använder HTTP kan du välja att kryptera dessa data, vilket är en bra säkerhetsrutin.  

### <a name="state-migration-encryption"></a>Kryptering av tillståndsmigrering  
 Data som finns lagrade på tillståndsmigreringsplatserna för operativsystemsdistribution krypteras alltid av verktyget för migrering av användartillstånd med hjälp av 3DES.  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>Kryptering för multicast-paket för att distribuera operativ system  
 För varje distributionspaket till ett operativsystem kan du aktivera kryptering när paketet överförs till datorerna via multicast. För krypteringen används standarden AES (Advanced Encryption Standard). Om du aktiverar kryptering behövs ingen ytterligare certifikatkonfiguration. Den multicast-aktiverade distributionsplatsen genererar automatiskt symmetriska nycklar för kryptering av paketet. Alla paket har olika krypteringsnycklar. Nyckeln sparas på den multicast-aktiverade distributionsplatsen med hjälp av Windows API:er av standardtyp. När klienten ansluter till multicast-sessionen sker nyckelbytet via en kanal som är krypterad med antingen det PKI-utfärdade klientautentiseringscertifikatet (om klienten använder HTTPS) eller det självsignerade certifikatet (om klienten använder HTTP). Klienten sparar nyckeln i minnet enbart under den tid multicast-sessionen varar.  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>Kryptering för media för att distribuera operativ system  
 När du använder medier för att distribuera operativsystem och anger ett lösenord för att skydda mediet krypteras miljövariablerna med hjälp av AES (Advanced Encryption Standard). Övriga data på mediet, inklusive paket och innehåll för program, krypteras inte.  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>Kryptering av innehåll som finns på molnbaserade distributions platser  
 Från och med System Center 2012 Configuration Manager SP1, och när du använder molnbaserade distributions platser, krypteras det innehåll som du överför till dessa distributions platser med hjälp av Advanced Encryption Standard (AES) med en 256-bitars nyckel storlek. Innehållet omkrypteras när du uppdaterar det. När klienterna laddar ned innehållet krypteras det och skyddas av HTTPS-anslutningen.  

### <a name="signing-in-software-updates"></a>Logga in program uppdateringar  
 Alla programuppdateringar måste signeras av en betrodd utgivare för att skyddas mot manipulation. På klientdatorer söker Windows Update-agenten efter uppdateringarna från katalogen, men kommer inte att installera uppdateringen om den inte kan hitta det digitala certifikatet i Betrodda utgivare på den lokala datorn. Om ett självsignerat certifikat har använts för publicering av uppdateringskatalogen, exempelvis WSUS Publishers Self-signed, måste certifikatet också finnas i certifikatarkivet Betrodda rotcertifikatutfärdare på den lokala datorn för att det ska gå att verifiera certifikatets giltighet. Uppdateringsagenten kontrollerar även om inställningen **Grupprincipen Tillåt signerat innehåll från Microsoft-uppdateringstjänst på intranätet** är aktiverad på den lokala datorn. Denna principinställning måste aktiveras för att Windows Update-agenten ska söka efter de uppdateringar som har skapats och publicerats med Updates Publisher.  

 När programuppdateringarna publiceras i System Center Updates Publisher signerar ett digitalt certifikat programuppdateringarna när de publiceras på en uppdateringsserver. Du kan antingen ange ett PKI-certifikat eller konfigurera Updates Publisher att generera ett självsignerat certifikat för att signera programuppdateringen.  

### <a name="signed-configuration-data-for-compliance-settings"></a>Signerade konfigurations data för kompatibilitetsinställningar  
 När du importerar konfigurations data verifierar Configuration Manager filens digitala signatur. Om filerna inte har signerats, eller om verifieringskontrollen av den digitala signaturen misslyckas visas en varning och du tillfrågas om du vill fortsätta med importen. Fortsätt att importera konfigurationsdata enbart om du uttryckligen litar på utgivaren och filernas integritet.  

### <a name="encryption-and-hashing-for-client-notification"></a>Kryptering och hashing för klient meddelande  
 Om du använder klientmeddelanden används TLS vid all kommunikation samt den högsta kryptering som servern och klientoperativsystemet kan förhandla fram. Till exempel kan en klient dator som kör Windows 7 och en hanterings plats som kör Windows Server 2008 R2 stödja 128-bitars AES-kryptering, medan en klient dator som kör Vista till samma hanterings plats försätts i 3DES-kryptering. Samma förhandling sker för hashing av de paket som överförs genom klientmeddelanden där SHA-1 eller SHA-2 används.  

##  <a name="certificates-used-by-configuration-manager"></a>Certifikat som används av Configuration Manager  
 En lista över PKI-certifikat (Public Key Infrastructure) som kan användas av Configuration Manager, eventuella särskilda krav eller begränsningar och hur certifikaten används finns i [krav för PKI-certifikat](../network/pki-certificate-requirements.md). I listan anges de hash-algoritmer och nyckellängder som stöds. De flesta certifikat har stöd för SHA-256 och 2 048 bitars nyckellängd.  

> [!NOTE]  
>  Alla certifikat som Configuration Manager använder får bara innehålla tecken med enkla byte i ämnes namnet eller det alternativa ämnes namnet.  

 PKI-certifikat krävs för följande scenarion:  

- När du hanterar Configuration Manager-klienter på Internet.  

- När du hanterar Configuration Manager-klienter på mobila enheter.  

- När du hanterar Mac-datorer.  

- När du använder molnbaserade distributionsplatser.  

  För de flesta andra Configuration Manager-kommunikation som kräver certifikat för autentisering, signering eller kryptering, Configuration Manager använder automatiskt PKI-certifikat om de är tillgängliga. Om de inte är tillgängliga genererar Configuration Manager självsignerade certifikat.  

  Configuration Manager använder inte PKI-certifikat när de hanterar mobila enheter med hjälp av Exchange Server-anslutningen.  

### <a name="mobile-device-management-and-pki-certificates"></a>Hantering av mobila enheter och PKI-certifikat  
 Om den mobila enheten inte har låsts av mobil operatören kan du använda Configuration Manager eller Microsoft Intune för att begära och installera ett klient certifikat. Det här certifikatet ger ömsesidig autentisering mellan klienten på den mobila enheten och Configuration Manager plats system eller Microsoft Intune-tjänster. Om den mobila enheten är låst kan du inte använda Configuration Manager eller Intune för att distribuera certifikat.  

 Om du aktiverar maskin varu inventering för mobila enheter, kan Configuration Manager eller Intune också inventera de certifikat som är installerade på den mobila enheten.   

### <a name="operating-system-deployment-and-pki-certificates"></a>Operativ Systems distribution och PKI-certifikat  
 När du använder Configuration Manager för att distribuera operativ system och en hanterings plats kräver HTTPS-klientanslutningar måste klient datorn också ha ett certifikat för att kommunicera med hanterings platsen, även om den är i en över gångs fas, till exempel starta från aktivitetssekvenser eller en PXE-aktiverad distributions plats. För att stödja det här scenariot måste du skapa ett certifikat för PKI-klientautentisering och exportera det med den privata nyckeln och sedan importera det till plats serverns egenskaper och även lägga till hanterings platsens betrodda rot certifikat för certifikat utfärdare.  

 Om du skapar ett startbart medium importerar du klientautentiseringscertifikatet när du skapar det startbara mediet. Konfigurera ett lösenord för det startbara mediet för att bidra till att skydda den privata nyckeln och andra känsliga data som konfigureras i aktivitetssekvensen. Varje dator som startar från det startbara mediet kommer att presentera samma certifikat för hanteringsplatsen som krävs för klientfunktioner, exempelvis att begära en klientprincip.  

 Om du använder PXE-start importerar du klientautentiseringscertifikatet till den PXE-aktiverade distributionsplatsen och använder samma certifikat för varje klient som startar från den PXE-aktiverade distributionsplatsen. Det är en bra säkerhetsrutin att kräva att användare som ansluter sina datorer till en PXE-tjänst uppger ett lösenord för att bidra till att skydda den privata nyckeln och andra känsliga data i aktivitetssekvenserna.  

 Om något av dessa klientautentiseringscertifikat blir komprometterat blockerar du certifikaten i noden **Certifikat** på arbetsytan **Administration** , noden **Säkerhet** . För att kunna hantera dessa certifikat måste du ha rättigheten **Hantera operativsystemets distributionscertifikat** .  

 Efter att operativ systemet har distribuerats och Configuration Manager har installerats kräver klienten ett eget certifikat för PKI-klientautentisering för HTTPS-klient kommunikation.  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>ISV-proxyservrar och PKI-certifikat  
 Oberoende program varu leverantörer (ISV) kan skapa program som utökar Configuration Manager. En oberoende programvaruleverantör kan exempelvis skapa tillägg som stöder andra klientplattformar än Windows-plattformar, exempelvis Macintosh eller UNIX-datorer. Om platssystemen kräver HTTPS klientanslutningar måste dessa klienter dock även använda PKI-certifikat för kommunikation med platsen. Configuration Manager innehåller möjlighet att tilldela ISV-proxyn ett certifikat som möjliggör kommunikation mellan ISV-proxyservrarna och hanterings platsen. Om du använder tillägg som kräver ISV-proxycertifikat finner du mer information i dokumentationen till den här produkten. Mer information om hur du skapar ISV-proxy-certifikat finns i Configuration Manager Software Developer Kit (SDK).  

 Om ISV-certifikatet komprometteras blockerar du certifikatet i noden **Certifikat** på arbetsytan **Administration** , noden **Säkerhet** .  

### <a name="asset-intelligence-and-certificates"></a>Till gångs information och certifikat  
 Configuration Manager installeras med ett X. 509-certifikat som Tillgångsinformation-platsen använder för att ansluta till Microsoft. Configuration Manager använder det här certifikatet för att begära ett certifikat för klientautentisering från Microsoft Certificate service. Certifikatet för klientautentisering installeras på platssystemservern till platsen för synkronisering av tillgångsinformation och används för att autentisera servern åt Microsoft. Configuration Manager använder certifikatet för klientautentisering för att ladda ned tillgångsinformationskatalogen och för att överföra programvarunamn.  

 Certifikatet har en nyckellängd på 1 024 bitar.  

### <a name="cloud-based-distribution-points-and-certificates"></a>Molnbaserade distributions platser och certifikat  
 Från och med System Center 2012 Configuration Manager SP1 kräver molnbaserade distributions platser ett hanterings certifikat (självsignerat eller PKI) som du överför till Microsoft Azure. Detta hanteringscertifikat kräver en serverautentiseringsfunktion och en certifikatnyckel med en längd på 2 048 bitar. Dessutom måste du konfigurera ett tjänstcertifikat för varje molnbaserad distributionsplats, som inte får var självsignerat utan även har en serverautentiseringsfunktion och en minsta certifikatnyckellängd på 2 048 bitar.  

> [!NOTE]  
>  Det självsignerade hanteringscertifikatet är enbart avsett för teständamål och kan inte användas i produktionsnätverk.  

 Klienterna behöver inte ha något PKI-klientcertifikat för att använda molnbaserade distributionsplatser; de autentiseras för hanteringen med hjälp av antingen ett självsignerat certifikat eller ett PKI-klientcertifikat. Hanterings platsen utfärdar sedan en Configuration Manager åtkomsttoken till klienten, som klienten presenterar för den molnbaserade distributions platsen. En token är giltig i åtta timmar.  

### <a name="the-microsoft-intune-connector-and-certificates"></a>Microsoft Intune anslutning och certifikat  
 När Microsoft Intune registrerar mobila enheter kan du hantera dessa mobila enheter i Configuration Manager genom att skapa en Microsoft Intune koppling. Anslutningen använder ett PKI-certifikat med funktioner för klientautentisering för att autentisera Configuration Manager Microsoft Intune och överföra all information mellan dem med hjälp av SSL. Certifikatets nyckelstorlek är 2 048 bitar och hash-algoritmen SHA-1 används.  

 När du installerar anslutningen skapas ett signeringscertifikat som sparas på platsservern för sidladdningsnycklar, och ett krypteringscertifikat skapas och sparas på certifikatsregistreringsplatsen för att kryptera SCEP-anropet (Simple Certificate Enrollment Protocol). Dessa certifikat har också en nyckelstorlek på 2 048 bitar och använder hash-algoritmen SHA-1.  

 När Intune registrerar mobila enheter installerar den ett PKI-certifikat på den mobila enheten. Detta certifikat har en klientautentiseringsfunktion, en nyckelstorlek på 2 048 bitar och använder hash-halgoritmen SHA-1.  

 Dessa PKI-certifikat begärs, genereras och installeras automatiskt av Microsoft Intune.  

### <a name="crl-checking-for-pki-certificates"></a>CRL-kontroll för PKI-certifikat  
 En PKI-lista över återkallade certifikat ökar det administrativa arbetet och behandlingen men är samtidigt säkrare. Om kontrollen av listan över återkallade certifikat är aktiverad men listan inte är tillgänglig, misslyckas dock PKI-anslutningen. Mer information finns i [säkerhet och sekretess för Configuration Manager](security-and-privacy.md).  

 Kontrollen av listan över återkallade certifikat är aktive rad som standard i IIS, så om du använder en CRL med din PKI-distribution finns det ingenting ytterligare att konfigurera på de flesta Configuration Manager-plats system som kör IIS. Undantaget är programuppdateringar, som kräver ett manuellt steg för att aktivera kontrollen av listan över återkallade certifikat för att verifiera signaturerna för programuppdateringsfilerna.  

 Kontrollen av listan över återkallade certifikat är aktiverad som standard för klientdatorer när de använder HTTPS-klientanslutningar. Du kan inte inaktivera CRL-kontroll för klienter på Mac-datorer i Configuration Manager SP1 eller senare.  

 CRL-kontroll stöds inte för följande anslutningar i Configuration Manager:  

-   Server-till-server anslutningar.  

-   Mobila enheter som har registrerats med Configuration Manager.  

-   Mobila enheter som har registrerats med Microsoft Intune.  

##  <a name="cryptographic-controls-for-server-communication"></a>Kryptografiska kontroller för server kommunikation  
 Configuration Manager använder följande kryptografiska kontroller för server kommunikation.  

### <a name="server-communication-within-a-site"></a>Server kommunikation inom en plats  
 Varje plats system Server använder ett certifikat för att överföra data till andra plats system på samma Configuration Manager plats. Vissa platssystemroller använder även certifikat för autentisering. Om du till exempel installerar registreringsproxyplatsen på en server och registreringsplatsen på en annan server kan de autentisera varandra med hjälp av det här identitetscertifikatet. När Configuration Manager använder ett certifikat för den här kommunikationen, om det finns ett PKI-certifikat som har funktioner för serverautentisering, Configuration Manager använder det automatiskt. annars genererar Configuration Manager ett självsignerat certifikat. Detta självsignerade certifikat har en serverautentiseringsfunktion, använder SHA-256, och har en nyckellängd på 2 048 bitar. Configuration Manager kopierar certifikatet till arkivet Betrodda personer på andra plats system servrar som kan behöva lita på plats systemet. Platssystemen kan sedan lita på varandra genom att använda dessa certifikat samt PeerTrust.  

 Förutom det här certifikatet för varje plats system Server skapar Configuration Manager ett självsignerat certifikat för de flesta plats system roller. Om det finns fler än en instans av platssystemrollen på samma plats delar de samma certifikat. Du kan till exempel ha flera hanteringsplatser eller flera registreringsplatser på samma plats. Detta självsignerade certifikat använder också SHA-256 och har en nyckellängd på 2 048 bitar. Det kopieras också till arkivet Betrodda personer på platssystemservrar som kan behöva betro det. Följande platssystemroller skapar detta certifikat:  

- Webbservicepunkt för programkatalog  

- Webbplats för programkatalog  

- Plats för synkronisering av tillgångsinformation  

- Certifikatregistreringsplats  

- Plats för slutpunktsskydd  

- Registreringsplats  

- Status för återställningsplats  

- Hanteringsplats  

- Multicast-aktiverad distributionsplats  

- Rapporteringstjänstpunkt  

- Programuppdateringsplats  

- Plats för tillståndsmigrering  

- Microsoft Intune Connector  

Dessa certifikat hanteras automatiskt av Configuration Manager, och där det behövs genereras automatiskt.  

Configuration Manager använder också ett certifikat för klientautentisering för att skicka status meddelanden från distributions platsen till hanterings platsen. Om hanteringsplatsen är konfigurerad för enbart HTTPS-klientanslutningar måste du använda ett PKI-certifikat. Om hanteringsplatsen godtar HTTP-anslutningar kan du använda ett PKI-certifikat eller välja möjligheten att använda ett självsignerat certifikat som har klientautentiseringsfunktion, använder SHA-256 och har en nyckellängd på 2 048 bitar.  

### <a name="server-communication-between-sites"></a>Server kommunikation mellan platser  
 Configuration Manager överför data mellan platser med hjälp av databasreplikering och filbaserad replikering. Mer information finns i [kommunikation mellan slut punkter](../hierarchy/communications-between-endpoints.md).  

 Configuration Manager konfigurerar databasreplikering automatiskt mellan platser och använder PKI-certifikat som har funktioner för serverautentisering om de är tillgängliga. annars skapar Configuration Manager självsignerade certifikat för serverautentisering. I båda fallen åstadkoms autentisering mellan platserna med hjälp av certifikat i det arkiv med betrodda personer som använder PeerTrust. Detta certifikat Arkiv används för att säkerställa att endast de SQL Server datorer som används av Configuration Manager-hierarkin deltar i plats-till-plats-replikering. Medan primära platser och den centrala administrationsplatsen kan replikera konfigurationsändringar till alla platser i hierarkin, kan sekundära platser enbart replikera konfigurationsändringar till sin överordnade plats.  

 Platsservar upprättar plats-till-plats-kommunikation genom att använda ett säkert nyckelutbyte som sker automatiskt. Den avsändande platsservern skapar en hash och signerar den med sin privata nyckel. Den mottagande platsservern kontrollerar signaturen med hjälp av den offentliga nyckeln och jämför hashen med ett värde som skapats lokalt. Om de matchar godkänner den mottagande platsen replikerade data. Om värdena inte matchar, Configuration Manager avvisar replikeringsdata.  

 Databasreplikering i Configuration Manager använder SQL Server Service Broker för att överföra data mellan platser med hjälp av följande mekanismer:  

- SQL Server- till SQL Server-anslutning: Här används Windows-autentiseringsuppgifter för serverautentisering och självsignerade certifikat med 1 024 bitar för att signera och kryptera data med hjälp av AES (Advanced Encryption Standard). Om PKI-certifikat med serverautentiseringsfunktioner finns tillgängliga används dessa. Certifikatet måste finnas i det personliga arkivet till datorns certifikatarkiv.  

- SQL Service Broker: Här används självsignerade certifikat med 2 048 bitar för autentisering och för att signera och kryptera data med hjälp av AES (Advanced Encryption Standard). Certifikatet måste finnas i SQL Server-huvuddatabasen.  

  Vid filbaserad replikering används SMB-protokollet (Server Message Block) och SHA-256 används för att signera dessa data som inte är krypterade men som inte innehåller några känsliga data. Om du vill kryptera dessa data kan du använda IPsec och implementera detta oberoende av Configuration Manager.  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>Kryptografiska kontroller för klienter som använder HTTPS-kommunikation till plats system  
 Om platssystemrollerna godtar klientanslutningar kan du konfigurera dem att godta HTTPS- och HTTP-anslutningar, eller enbart HTTPS-anslutningar. Platssystemroller som godtar anslutningar från Internet godtar enbart klientanslutningar via HTTPS.  

 Klientanslutningar via HTTPS ger en högre säkerhetsnivå genom att integrera med en PKI-infrastruktur (Public Key Infrastructure) för att hjälpa till att skydda klient-till-server-kommunikationen. Att konfigurera HTTPS-klientanslutningar utan att ha en omfattande förståelse av PKI-planering, -distribution och -åtgärder kan dock fortfarande göra dig utsatt för sårbarheter. Om du exempelvis inte skyddar din rotcertifikatutfärdare kan en angripare kompromettera tillförlitligheten hos hela din PKI-infrastruktur. Att inte distribuera och hantera PKI-certifikat med hjälp av kontrollerade och säkra processer kan resultera i ohanterade klienter som inte kan ta emot viktiga programuppdateringar eller paket.  

> [!IMPORTANT]  
>  De PKI-certifikat som används för klientkommunikation skyddar enbart kommunikationen mellan klienten och vissa platssystem. De skyddar inte kommunikationskanalen mellan platsservern och platssystemen eller mellan platsservrarna.  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>Kommunikation som är okrypterad när klienter använder HTTPS-kommunikation  
 När klienterna kommunicerar med platssystemen med hjälp av HTTPS, krypteras kommunikationen vanligtvis med SSL. I följande situationer kommunicerar dock klienterna med platssystemen utan att använda kryptering:  

- Klienten misslyckas med att upprätta en HTTPS-anslutning på intranätet och återgår till att använda HTTP om platssystemen tillåter denna konfiguration.  

- Kommunikation till följande platssystemroller:  

  -   Klienten skickar tillståndsmeddelanden till återställningsstatuspunkten  

  -   Klienten skickar PXE-begäran den till en PXE-aktiverad distributionsplats  

  -   Klienten skickar meddelandedata till en hanteringsplats  

  Rapporttjänstplatserna konfigureras för att använda HTTP eller HTTPS oberoende av klientkommunikationsläget.  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>Kryptografiska kontroller för klienter som chattar använder HTTP-kommunikation till plats system  
 När klienter använder HTTP-kommunikation till plats system roller kan de använda PKI-certifikat för klientautentisering, eller självsignerade certifikat som Configuration Manager genererar. När Configuration Manager genererar självsignerade certifikat har de en anpassad objekt identifierare för signering och kryptering, och dessa certifikat används för att identifiera klienten unikt. Certifikaten använder SHA-256 för alla operativsystem som stöds, utom Windows Server 2003, och de har en nyckellängd på 2 048 bitar. För Windows Server 2003 används SHA1 med en nyckellängd på 1 024 bitar.  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>Operativ Systems distribution och självsignerade certifikat  
 När du använder Configuration Manager för att distribuera operativ system med självsignerade certifikat måste en klient dator också ha ett certifikat för att kommunicera med hanterings platsen, även om datorn är i en över gångs fas, till exempel starta från aktivitetssekvensen eller en PXE-aktiverad distributions plats. För att stödja det här scenariot för HTTP-klientanslutningar skapar Configuration Manager självsignerade certifikat som har en anpassad objekt identifierare för signering och kryptering, och dessa certifikat används för att identifiera klienten unikt. Certifikaten använder SHA-256 för alla operativsystem som stöds, utom Windows Server 2003, och de har en nyckellängd på 2 048 bitar. För Windows Server 2003 används SHA1 med en nyckellängd på 1 024 bitar. Om de självsignerade certifikaten skulle skadas kan du hindra eventuella angripare från att använda dem för att personifiera betrodda klienter, genom att blockera certifikaten i noden **Certifikat** i arbetsytan **Administration** , noden **Säkerhet** .  

### <a name="client-and-server-authentication"></a>Autentisering av klient och Server  
 När klienter ansluter via HTTP autentiserar de hanterings platserna genom att använda antingen Active Directory Domain Services eller genom att använda den betrodda rot nyckeln för Configuration Manager. Klienter autentiserar inte andra platssystemroller, till exempel tillståndsmigreringsplatser eller programuppdateringsplatser.  

 Metoden att låta en hanteringsplats först autentisera en klient genom att använda det självsignerade certifikatet ger minimal säkerhet, eftersom vilken dator som helst kan generera ett självsignerat certifikat. I den här scenariot måste klientidentifieringen förstärkas med en godkännandeprocess. Endast betrodda datorer måste godkännas, antingen automatiskt av Configuration Manager eller manuellt av en administrativ användare. Mer information finns i avsnittet om godkännande i [kommunikation mellan slut punkter](../hierarchy/communications-between-endpoints.md).  

## <a name="about-ssl-vulnerabilities"></a>Om SSL-sårbarheter
Gör så här för att förbättra säkerheten för dina Configuration Manager-klienter och-servrar:

- Aktivera TLS 1.2

  Om du vill aktivera TLS 1,2 för Configuration Manager, se [så här aktiverar du tls 1,2 för Configuration Manager](enable-tls-1-2.md).
- Inaktivera SSL 3,0, TLS 1,0 och TLS 1,1 
- Ändra ordning på TLS-relaterade chiffersviter 

Mer information finns i [så här begränsar du användningen av vissa kryptografiska algoritmer och protokoll i Schannel. dll](https://support.microsoft.com/help/245030/) och [prioriterar Schannel cipher-paket](https://docs.microsoft.com/windows/win32/secauthn/prioritizing-schannel-cipher-suites). Dessa procedurer påverkar inte Configuration Manager funktioner.

