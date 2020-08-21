---
title: Hitta plats resurser
titleSuffix: Configuration Manager
description: Lär dig hur och när Configuration Manager klienter använder tjänst lokalisering för att hitta plats resurser.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 262234edbd6fac6973653ca6cac62853fde23b2d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700120"
---
# <a name="learn-how-clients-find-site-resources-and-services-for-configuration-manager"></a>Lär dig hur klienter hittar plats resurser och tjänster för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager-klienter använder en process som kallas *tjänst lokalisering* för att hitta plats system servrar som de kan kommunicera med och som tillhandahåller tjänster som klienterna dirigerar att använda. Att förstå hur och när klienter använder tjänst lokalisering för att hitta plats resurser kan hjälpa dig att konfigurera dina platser så att de stöder klient åtgärder. Dessa konfigurationer kan kräva att platsen interagerar med domän-och nätverkskonfigurationer som Active Directory Domain Services (AD DS) och DNS. Eller så kan de kräva att du konfigurerar mer komplexa alternativ.  

Exempel på plats system roller som tillhandahåller tjänster är:

- Den grundläggande plats system servern för klienter.
- Hanterings platsen.
- Ytterligare plats system servrar som klienten kan kommunicera med, t. ex. distributions platser och program uppdaterings platser.  



##  <a name="fundamentals-of-service-location"></a><a name="bkmk_fund"></a> Grunderna för tjänst lokalisering  
 En klient utvärderar sin aktuella nätverks plats, inställningar för kommunikations protokoll och tilldelad plats när den använder tjänst lokalisering för att hitta en hanterings plats som den kan kommunicera med.  

**En klient kommunicerar med en hanterings plats för att:**  
- Hämta information om andra hanterings platser för platsen så att den kan bygga en lista över kända hanterings platser (kallas *MP-listan*) för framtida tjänst lokaliserings cykler.  
- Ladda upp konfigurations information, t. ex. inventering och status.  
- Hämta en princip som ställer in konfigurationer på klienten och kan informera klienten om program vara som den kan eller måste installera samt andra relaterade uppgifter.  
- Begär information om ytterligare plats system roller som tillhandahåller tjänster som klienten har kon figurer ATS att använda. Exempel är distributions platser för program vara som klienten kan installera eller en program uppdaterings plats som uppdateringar ska hämtas från.  

**En Configuration Manager-klient gör en tjänst plats förfrågan:**  
- Var 25: e timme med kontinuerlig åtgärd.  
- När klienten identifierar en ändring i dess nätverks konfiguration eller plats.  
- När **ccmexec.exe** tjänsten på datorn (kärn klient tjänsten) startar.  
- När klienten måste hitta en plats system roll som tillhandahåller en nödvändig tjänst.  

**När en klient försöker hitta servrar som är värdar för plats system roller**använder den tjänst lokalisering för att hitta en plats system roll som stöder klientens protokoll (http eller https). Som standard använder klienter den säkraste metoden som är tillgänglig för dem. Tänk också på följande:  

- Om du vill använda HTTPS måste du ha en PKI (public key infrastructure) och installera PKI-certifikat på klienterna och servrarna. Information om hur du använder certifikat finns i avsnittet [om krav för PKI-certifikat för Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

- När du distribuerar en platssystemsroll som använder IIS (Internet Information Services) och stöder kommunikation från klienter, måste du ange om klienterna ansluter till platssystemet via HTTP eller HTTPS. Om du använder HTTP, måste du även fundera på signerings- och krypteringsval. Mer information finns i  [Planera för signering och kryptering](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) i [planen för säkerhet](../../../core/plan-design/security/plan-for-security.md).  

##  <a name="service-location-and-how-clients-determine-their-assigned-management-point"></a><a name="BKMK_Plan_Service_Location"></a> Tjänst lokalisering och hur klienter avgör sina tilldelade hanterings platser  
När en klient först tilldelas till en primär plats väljer den en standard hanterings plats för platsen. Primära platser har stöd för flera hanterings platser, och varje klient identifierar oberoende av en hanterings plats som standard hanterings plats. Den här standard hanterings platsen blir sedan klientens tilldelade hanterings plats. (Du kan också använda kommandon för klient installation för att ange den tilldelade hanterings platsen för en klient när den installeras.)  

En klient väljer en hanterings plats för att kommunicera med baserat på klientens aktuella nätverks plats och konfiguration av gränser grupper. Även om den har en tilldelad hanterings plats kanske det inte är den hanterings plats som klienten använder.  

> [!NOTE]  
> Klienten använder alltid den tilldelade hanteringsplatsen för registreringsmeddelanden och vissa principmeddelanden även när andra meddelanden skickas till en proxy eller lokal hanteringsplats.

Du kan använda prioriterade, eller önskade, hanteringsplatser. Prioriterade hanterings platser är hanterings platser från en klients tilldelade plats som är associerade med en avgränsnings grupp som klienten använder för att hitta plats system servrar. En prioriterad hanterings platss koppling med en avgränsnings grupp som plats system Server liknar hur distributions platser eller platser för tillståndsmigrering är kopplade till en avgränsnings grupp. Om du aktiverar önskade hanteringsplatser för hierarkin kommer en klient att försöka använda en önskad hanteringsplats innan den använder andra hanteringsplatser från den tilldelade webbplatsen när den använder en hanteringsplats från den tilldelade webbplatsen.  

Du kan också använda informationen i bloggen för [hanterings plats tillhörighet](/archive/blogs/jchalfant/management-point-affinity-added-in-configmgr-2012-r2-cu3) för att konfigurera tillhörighet mellan hanterings platser. Mappning mellan hanterings platser åsidosätter standard beteendet för tilldelade hanterings platser och gör att klienten kan använda en eller flera olika hanterings platser.  

Varje gång en klient behöver kontakta en hanterings plats kontrollerar den MP-listan, som den lagrar lokalt i Windows Management Instrumentation (WMI). Klienten skapar en första MP-lista när den installeras. Klienten uppdaterar sedan regelbundet listan med information om varje hanterings plats i hierarkin.  

När klienten inte kan hitta en giltig hanterings plats i MP-listan söker den igenom följande tjänst lokaliserings källor, i ordning, tills den hittar en hanterings plats som den kan använda:  

1.  Hanteringsplats  
2.  AD DS  
3.  DNS  
4.  WINS  

När en klient har hittat och kontaktat en hanterings plats laddar den ned den aktuella listan över hanterings platser som är tillgängliga i hierarkin och uppdaterar den lokala MP-listan. Detta gäller såväl de klienter som är domänanslutna som de som inte är det.  

Om till exempel en Configuration Manager-klient som finns på Internet ansluter till en Internetbaserad hanterings plats skickar hanterings platsen en lista över tillgängliga Internetbaserade hanterings platser på platsen. På samma sätt klienter som är domänanslutna eller i arbetsgrupper kan på motsvarande sätt få en lista över hanteringspunkter som de kan använda.  

En klient som inte har kon figurer ATS för Internet har inte någon hanterings plats som endast är riktad mot Internet. Arbets grupps klienter som kon figurer ATS för Internet kommunicerar bara med Internet-riktade hanterings platser.  

##  <a name="the-mp-list"></a><a name="BKMK_MPList"></a> MP-listan  
MP-listan är den prioriterade tjänst lokaliserings källan för en klient, eftersom det är en prioriterad lista med hanterings platser som klienten identifierade tidigare. Den här listan sorteras efter respektive klient baserat på dess nätverksplats när klienten uppdaterar listan och sedan sparas lokalt på klienten i WMI.  

### <a name="building-the-initial-mp-list"></a>Skapa den första MP-listan  
Under installationen av klienten används följande regler för att bygga klientens första MP-lista:  

- Den inledande listan innehåller hanterings platser som anges under klient installationen (när du använder alternativet **SMSMP**= eller **/MP** ).  
- Klienten frågar AD DS om publicerade hanterings platser. För att kunna identifieras från AD DS måste hanterings platsen vara från klientens tilldelade plats och den måste vara av samma produkt version som klienten.  
- Om ingen hanterings plats angavs vid klient installationen och Active Directory schemat inte har utökats kontrollerar klienten DNS och WINS efter publicerade hanterings platser.  
- När klienten skapar den initiala listan kanske information om vissa hanterings platser i hierarkin inte är känd.  

### <a name="organizing-the-mp-list"></a>Organisera MP-listan  
Klienterna ordnar sin lista över hanterings platser med hjälp av följande klassificeringar:  

- **Proxy**: en hanterings plats på en sekundär plats.  
- **Lokalt**: alla hanterings platser som är associerade till klientens aktuella nätverks plats, enligt definitionen i plats gränser. Observera följande information om gränser:
  - När en klient tillhör mer än en gränsgrupp bestäms listan över lokala hanteringsplatser från sammanslagningen av alla gränser som innehåller klientens aktuella nätverksplats.  
  - Lokala hanterings platser är vanligt vis en delmängd av en klients tilldelade hanterings platser, såvida inte klienten finns på en nätverks plats som är kopplad till en annan plats med hanterings platser som betjänar dess gränser grupper.   


- **Tilldelad**: alla hanterings platser som är ett plats system för klientens tilldelade plats.  

Du kan använda prioriterade, eller önskade, hanteringsplatser. Hanterings platser på en plats som inte är associerade med en avgränsnings grupp eller som inte finns i en kant linje som är kopplad till en klients aktuella nätverks plats, anses inte vara prioriterade. De kommer att användas när klienten inte kan identifiera en tillgänglig prioriterad hanterings plats.  

### <a name="selecting-a-management-point-to-use"></a>Välja en hanteringsplats att använda  
Vid normal kommunikation försöker en klient använda en hanterings plats från klassificeringarna i följande ordning, baserat på klientens nätverks plats:  

1.  Proxy  
2.  Lokal  
3.  Tilldelad  

Klienten använder dock alltid den tilldelade hanteringsplatsen för registreringsmeddelanden och vissa principmeddelanden även när andra meddelanden skickas till en proxy eller lokal hanteringsplats.  

I varje klassificering (proxy, lokal eller tilldelad) försöker klienten använda en hanterings plats baserat på inställningar i följande ordning:  

1.  HTTPS-kompatibel i en betrodd eller lokal skog (när klienten har konfigurerats för HTTPS-kommunikation)  
2.  HTTPS fungerar inte i en betrodd eller lokal skog (när klienten har kon figurer ATS för HTTPS-kommunikation)  
3.  HTTP-kompatibel i en betrodd eller lokal skog  
4.  HTTP-stöd inte i en betrodd eller lokal skog  

Från uppsättningen av hanterings platser sorterade efter inställningar försöker klienten att använda den första hanterings platsen på listan. Den här sorterade listan över hanterings platser är slumpmässig och kan inte beställas. Ordningen i listan kan ändras varje gången klienten uppdaterar sin MP-lista.  

När en klient inte kan upprätta kontakt med den första hanterings platsen görs ett försök till varje efterföljande hanterings plats på listan. Den försöker med varje prioriterad hanterings plats i klassificeringen innan du testar de icke-prioriterade hanterings platserna. Om en klient inte kan kommunicera med någon hanterings plats i klassificeringen försöker den kontakta en önskad hanterings plats från nästa klassificering, och så vidare tills den hittar en hanterings plats som ska användas.  

När en klient upprättar kommunikation med en hanterings plats fortsätter den att använda samma hanterings plats tills:  

- 25 timmar har passerat.  
- Klienten kan inte kommunicera med hanterings platsen för fem försök under en period på 10 minuter.

Klienten väljer slumpmässigt en ny hanterings plats som ska användas.  

##  <a name="active-directory"></a><a name="bkmk_ad"></a> Active Directory  
Klienter som är domänanslutna kan använda AD DS för tjänstlokalisering. Detta kräver att webbplatserna [publicerar data till Active Directory](../../servers/deploy/configure/publish-site-data.md).  

En klient kan använda AD DS för tjänst lokalisering när samtliga följande villkor är uppfyllda:  

- Active Directory- [schemat har utökats](../network/extend-the-active-directory-schema.md) eller utökats för System Center 2012 Configuration Manager.  
- [Active Directorys skogen har kon figurer ATS för publicering](../../servers/deploy/configure/publish-site-data.md)och Configuration Manager-platser är konfigurerade att publicera.  
- Klientdatorn är medlem i en Active Directory-domän och har åtkomst till en global katalogserver.  

Om en klient inte kan hitta en hanterings plats som ska användas för tjänst lokalisering från AD DS försöker den använda DNS.  

##  <a name="dns"></a><a name="bkmk_dns"></a> DNS  
Klienter på intranätet kan använda DNS för tjänstlokalisering. Detta kräver minst en plats i en hierarki för att publicera information om hanteringsplatser till DNS.  

Överväg att använda DNS för tjänstlokalisering när något av följande villkor är uppfyllt:
- AD DS-schemat har inte utökats till stöd för Configuration Manager.
- Klienter på intranätet finns i en skog som inte är aktive rad för Configuration Manager publicering.  
- Du har klienter på arbets grupps datorer och dessa klienter är inte konfigurerade för klient hantering enbart för Internet. (En arbets grupps klient som kon figurer ATS för Internet kommer endast att kommunicera med Internet-riktade hanterings platser och använder inte DNS för tjänst lokalisering.)  
- Du kan [konfigurera klienter för att hitta hanteringsplatser från DNS](../../clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

När en plats publicerar tjänstlokaliseringsposter för hanteringsplatser till DNS:  

- Publicering gäller endast för hanteringsplatser som accepterar klientanslutningar från intranätet.  
- Publicering lägger till en resurspost för tjänstlokalisering (SRV RR) i hanteringsplatsdatorns DNS-zon. Det måste finnas en motsvarande värdpost i DNS för den datorn.  

Som standard söker domänanslutna klienter i DNS efter hanterings plats poster från klientens lokala domän. Du kan konfigurera en klient egenskap som anger ett domänsuffix för en domän som har hanterings plats information som publicerats till DNS.  

Mer information om hur du konfigurerar klient egenskapen för DNS-suffix finns i [så här konfigurerar du klient datorer för att hitta hanterings platser med hjälp av DNS-publicering](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Om en klient inte kan hitta en hanterings plats som ska användas för tjänst lokalisering från DNS försöker den använda WINS.  

### <a name="publish-management-points-to-dns"></a>Publicera hanteringsplatser i DNS  
Följande villkor måste vara uppfyllda för att publicera hanteringsplatser i DNS:  

- DNS-servrarna har stöd för resursposter för att hitta tjänster genom att använda Berkely Internet Name Domän (BIND) med lägst version 8.1.2.  
- De angivna intranät-FQDN: erna för hanterings platserna i Configuration Manager ha värd poster (till exempel A-poster) i DNS.  

> [!IMPORTANT]  
> Configuration Manager DNS-publicering stöder inte en åtskild namnrymd. Om du har en uppdelad namnrymd kan du publicera hanterings platser manuellt till DNS eller använda någon av de andra tjänst lokaliserings metoderna som beskrivs i det här avsnittet.  

**När DNS-servrarna har stöd för automatiska uppdateringar**kan du konfigurera Configuration Manager att automatiskt publicera hanterings platser på intranätet till DNS, eller så kan du publicera posterna manuellt till DNS. När hanteringsplatser publiceras i DNS publiceras deras fullständiga intranätdomännamn och portnummer i posten för att hitta en tjänst (SRV). Du konfigurerar DNS-publicering på en plats i platsens komponent egenskaper för hanterings platsen. Mer information finns i  [plats komponenter för Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

**När DNS-zonen är inställd på "endast säker" för dynamiska uppdateringar**kan bara den första hanterings platsen som ska publiceras till DNS göra det med standard behörighet.

Om endast en hanterings plats kan publicera och ändra sin DNS-post och hanterings plats servern är felfri, kan klienterna hämta den fullständiga MP-listan från hanterings platsen och sedan hitta den önskade hanterings platsen.


**Om DNS-servrarna inte har stöd för automatiska uppdateringar men har stöd för tjänstlokaliseringsposter**, kan du publicera hanteringsplatser manuellt till DNS. Det gör du genom att manuellt ange resursposten för att hitta en tjänst (SRV RR) i DNS.  

Configuration Manager stöder RFC 2782 för tjänst lokaliserings poster. Dessa poster har följande format:   *_Service. _Proto. namn TTL-klass SRV prioritet vikt port mål*  

Om du vill publicera en hanterings plats till Configuration Manager anger du följande värden:  

- **_Service**: ange **_mssms_mp**_ &lt; platskod \> , där &lt; SiteCode \> är hanterings platsens platskod.  
- **._Proto**: Ange **._tcp**.  
- **.Name**: Ange hanteringsplatsens DNS-suffix, till exempel **contoso.com**.  
- **TTL**: Ange **14400**, vilket är fyra timmar.  
- **Klass**: Ange **IN** (kompatibelt med RFC 1035).  
- **Prioritet**: Configuration Manager inte använder det här fältet.
- **Vikt**: Configuration Manager använder inte det här fältet.  
- **Port**: Ange det portnummer som hanteringsplatsen använder, till exempel **80** för HTTP och **443** för HTTPS.  

  > [!NOTE]  
  >  SRV-postporten ska matcha den kommunikations port som hanterings platsen använder. Som standard är detta **80** för HTTP-kommunikation och **443** för HTTPS-kommunikation.  

- **Mål**: Ange det fullständiga intranätdomännamnet som är angivet för det platssystem som är konfigurerat med hanteringsplatsens platsroll.  

Om du använder Windows Server-DNS kan du ange DNS-posten för intranäthanteringsplatser på följande sätt. Om du använder en annan DNS-implementering läser du informationen om fältvärden i det här avsnittet, och läser den DNS-dokumentationen för att använda den här metoden.  

##### <a name="to-configure-automatic-publishing"></a>Konfigurera automatisk publicering:  

1.  I Configuration Manager-konsolen expanderar du **Administration**  >  **plats konfiguration**  >  **platser**.  

2.  Välj din webbplats och välj sedan **Konfigurera plats komponenter**.  

3.  Välj **hanterings plats**.  

4.  Välj de hanterings platser som du vill publicera. (Det här alternativet gäller för publicering till AD DS och DNS.)  

5.  Markera kryss rutan om du vill publicera till DNS. Den här rutan:  

    - Låter dig välja vilka hanterings platser som ska publiceras i DNS.  

    - Konfigurerar inte publicering till AD DS.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>Publicera hanteringsplatser manuellt i DNS på Windows Server  

1.  I Configuration Manager-konsolen anger du intranätets FQDN för plats system.  

2.  Ange DNS-zonen för hanteringsplatsdatorn i DNS-hanteringskonsolen.  

3.  Kontrollera att det finns en värdpost (A eller AAA) för intranätets fullständiga domännamn för platsssystemet. Om posten inte finns skapar du den.  

4.  Genom att använda alternativet **nya andra poster** väljer du **tjänst lokalisering (SRV)** i dialog rutan **typ av resurs post** , väljer **skapa post**, anger följande information och väljer sedan **färdig**:  

    - **Domän**: Ange hanteringsplatsens DNS-suffix om det behövs, till exempel **contoso.com**.  
    - **Tjänst**: typ **_mssms_mp**_ &lt; platskod \> , där &lt; SiteCode \> är hanterings platsens platskod.  
    - **Protokoll**: Skriv **_tcp**.  
    - **Prioritet**: Configuration Manager inte använder det här fältet.  
    - **Vikt**: Configuration Manager använder inte det här fältet.  
    - **Port**: Ange det portnummer som hanteringsplatsen använder, till exempel **80** för HTTP och **443** för HTTPS.  

      > [!NOTE]  
      > SRV-postporten ska matcha den kommunikations port som hanterings platsen använder. Som standard är detta **80** för HTTP-kommunikation och **443** för HTTPS-kommunikation.  

    - **Värd som erbjuder den här tjänsten**: Ange intranätets FQDN som har angetts för det plats system som är konfigurerat med hanterings platsens plats roll.  

Upprepa de här stegen för alla hanteringsplatser på intranätet som du vill publicera i DNS.  

##  <a name="wins"></a><a name="bkmk_wins"></a> UPPTÄCKT  
Om andra metoder för att hitta en tjänst misslyckas kan klienterna hitta en första hanteringsplats genom att söka i WINS.  

En primär plats publiceras som standard till WINS den första hanterings platsen på den plats som är konfigurerad för HTTP och den första hanterings platsen som är konfigurerad för HTTPS.  

Om du inte vill att klienter ska hitta en HTTP-hanteringsplats i WINS konfigurerar du klienterna med CCMSetup.exe-egenskapen Client.msi **SMSDIRECTORYLOOKUP=NOWINS**.