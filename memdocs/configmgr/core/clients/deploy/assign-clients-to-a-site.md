---
title: Tilldela klienter till en plats
titleSuffix: Configuration Manager
description: Tilldela klienter till en plats i Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ab2270435ac13585cb0b7d3271f1faa02cc728d3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075752"
---
# <a name="how-to-assign-clients-to-a-site-in-configuration-manager"></a>Tilldela klienter till en plats i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När en Configuration Manager-klient har installerats måste den ansluta till en Configuration Manager primär plats innan du kan hantera den. Den plats som en klient ansluter till kallas dess *tilldelade plats*. Klienter kan inte tilldelas en central administrationsplats eller en sekundär plats.  

Tilldelnings processen sker när klienten har installerats och avgör vilken plats som hanterar klient datorn. Du kan antingen tilldela klienten en plats direkt eller använda automatisk platstilldelning där klienten automatiskt hittar en lämplig plats baserat på dess aktuella nätverks plats eller en återställnings plats som har kon figurer ATS för hierarkin.

När du installerar den mobila enhets klienten under Configuration Manager registreringen, tilldelas enheten alltid en plats automatiskt. När du installerar-klienten på en dator kan du välja om klienten ska tilldelas en plats eller inte. Om klienten installeras men inte tilldelas någon plats, förblir klienten ohanterad tills den har tilldelats en plats.  
 

> [!NOTE]  
>  Tilldela alltid klienter till webbplatser som kör samma version av Configuration Manager. Undvik att tilldela en Configuration Manager-klient från en nyare version till en plats från en äldre version.   Vid behov kan du uppdatera den primära platsen till samma Configuration Manager version som du använder för klienterna.  

När klienten har tilldelats en plats är den fortfarande kopplad till den platsen även om klientens IP-adress ändras eller om den växlar nätverk till en annan plats. Endast en administratör kan manuellt tilldela klienten till en annan plats eller ta bort klient tilldelningen.  

> [!WARNING]  
>  Ett undantag är om du tilldelar klienten på en Windows Embedded-enhet när skrivfiltren är aktiverade. Om du inte först inaktiverar skrivfiltren innan du tilldelar klienten, återgår platstilldelningsstatusen för klienten till ursprungsläget nästa gång enheten startas om.  
>   
>  Om klienten till exempel har konfigurerats för automatisk platstilldelning, omtilldelas den vid start och kan tilldelas en annan plats. Om klienten inte har kon figurer ATS för automatisk platstilldelning utan kräver manuell platstilldelning, måste du manuellt tilldela om klienten efter starten innan du kan hantera den här klienten igen med hjälp av Configuration Manager.  
>   
>  Du kan undvika det här genom att inaktivera skrivfiltren innan du tilldelar klienten på inbäddade enheter och sedan aktivera skrivfiltren när du har kontrollerat att platstilldelningen fungerade.  

Om klient tilldelningen Miss lyckas förblir klient programmet installerad, men kommer inte att hanteras. En klient betraktas som ohanterad när den är installerad men inte tilldelad någon plats, eller har tilldelats en plats men inte kan kommunicera med någon hanteringsport.  

##  <a name="using-manual-site-assignment-for-computers"></a>Använda manuell platstilldelning för datorer  
 Du kan manuellt tilldela klientdatorer en plats med följande två metoder:  

-   Använd en klientinstallationsegenskap som anger platskoden.  

-   På Kontrollpanelen i **Configuration Manager**anger du platskoden.  

> [!NOTE]  
>  Om du manuellt tilldelar en klient dator till en Configuration Manager plats kod som inte finns, Miss lyckas platstilldelning.   

##  <a name="using-automatic-site-assignment-for-computers"></a><a name="BKMK_AutomaticAssignment"></a>Använda automatisk platstilldelning för datorer  
 Automatisk platstilldelning kan ske under klientdistributionen eller när du klickar på **Sök efter plats** på fliken **Avancerat** i **Egenskaper för Configuration Manager** på Kontrollpanelen. Den Configuration Manager klienten jämför den egna nätverks platsen med de gränser som har kon figurer ATS i hierarkin Configuration Manager. När en klients nätverksplats hamnar inom en gränsgrupp som är aktiverad för platstilldelning eller om hierarkin är konfigurerad för en återställningsplats, tilldelas klienten automatiskt den platsen utan att du behöver ange någon platskod.  

 Du kan konfigurera gränser med hjälp av följande:  

-   IP-undernät  

-   Active Directory-plats  

-   IP v6-prefix  

-   IP-adressintervall  

> [!NOTE]  
>  Om en Configuration Manager-klient har flera nätverkskort och därför har flera IP-adresser, tilldelas IP-adressen som används för att utvärdera tilldelningen av klient platser slumpmässigt.  

 Information om hur du konfigurerar gräns grupper för platstilldelning och hur du konfigurerar en återställnings plats för automatisk platstilldelning finns i [definiera plats gränser och gräns grupper för Configuration Manager](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

 Configuration Manager klienter som använder automatisk platstilldelning försöker hitta plats gränser grupper som publiceras till Active Directory Domain Services. Om detta Miss lyckas (till exempel om Active Directory-schemat inte har utökats för Configuration Manager eller om klienterna är arbets grupps datorer) kan klienterna Hämta gräns grupp information från en hanterings plats.  

 Du kan ange en hanteringsplats för klientdatorer som ska användas när de är installerade, eller också kan klienterna hitta en hanteringsplats genom att använda DNS-publicering eller WINS.  

 Om klienten inte hittar någon plats som är kopplad till en gränsgrupp som omfattar dess nätverksplats och det inte finns någon återställningsplats i hierarkin, försöker klienten igen var 10:e minut tills den kan tilldelas en plats.  

 Configuration Manager-klientdatorer kan inte tilldelas automatiskt till en plats om något av följande gäller och de måste tilldelas manuellt:  

-   De har redan tilldelats en plats.  

-   De är på Internet eller konfigurerade som endast Internetklienter.  

-   Deras nätverksplats hamnar inte inom någon av de konfigurerade gränsgrupperna i Configuration Manager-hierarkin och det finns ingen återställningsplats för hierarkin.  

##  <a name="completing-site-assignment-by-checking-site-compatibility"></a>Utföra platstilldelning genom kontroll av platskompatibilitet  
 När en klient har hittat sin tilldelade plats kontrol leras klientens version och operativ system för att säkerställa att en Configuration Manager plats kan hantera den. Configuration Manager kan till exempel inte hantera Configuration Manager 2007-klienter, System Center 2012 Configuration Manager-klienter eller klienter som kör Windows 2000.  

 Platstilldelning Miss lyckas om du tilldelar en klient som kör Windows 2000 till en Configuration Manager-plats. När du tilldelar en Configuration Manager 2007-klient eller en System Center 2012 Configuration Manager-klient till en Configuration Manager-plats (aktuell gren), lyckas platstilldelning att stödja automatisk klient uppgradering. Men tills de äldre generationens klienter uppgraderas till en Configuration Manager-klient (aktuell gren) Configuration Manager inte hantera klienten med hjälp av klient inställningar, program eller program uppdateringar.  

> [!NOTE]  
>  För att stödja platstilldelning av en Configuration Manager 2007 eller en System Center 2012 Configuration Manager-klient till en Configuration Manager-plats (aktuell gren) måste du konfigurera automatisk klient uppgradering för hierarkin. Mer information finns i [Uppgradera klienter för Windows-datorer](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

Configuration Manager kontrollerar också att du har tilldelat Configuration Manager-klienten (aktuell gren) till en plats som stöder den. Följande scenarier kan uppstå under migrering från tidigare versioner av Configuration Manager.  

- Scenario: du har använt automatisk platstilldelning och dina gränser överlappar de som definierats i en tidigare version av Configuration Manager.  

   I det här fallet försöker klienten automatiskt hitta en Configuration Manager-plats (aktuell gren).  

   Klienten kontrollerar först Active Directory Domain Services och om den hittar en Configuration Manager (aktuell gren) publicerad, slutförs platstilldelning. Om detta Miss lyckas (till exempel om den Configuration Manager webbplatsen inte är publicerad eller om datorn är en arbets grupps klient) söker klienten efter plats information från den tilldelade hanterings platsen.  

  > [!NOTE]  
  >  Du kan tilldela klienten en hanterings plats under klient installationen genom att använda client. msi-egenskapen **SMSMP =&lt;server_name>**.  

   Om båda metoderna misslyckas fungerar inte platstilldelningen och du måste tilldela klienten manuellt.  

- Scenario: du har tilldelat Configuration Manager-klienten (aktuell gren) genom att använda en särskild platskod i stället för automatisk platstilldelning och av misstag angett en Platskod för en tidigare version av Configuration Manager än System Center 2012 R2 Configuration Manager.  

   I detta fall Miss lyckas platstilldelning och du måste manuellt tilldela om klienten till en Configuration Manager-plats (aktuell gren).  

  För kontroll av platskompatibilitet krävs något av följande:  

- Klienten har åtkomst till platsinformation som är publicerad i Active Directory Domain Services.  

- Klienten kan kommunicera med en hanteringsplats på platsen.  

  Om kontrollen av kompatibilitetskontrollen inte kan slutföras, Miss lyckas platstilldelning och klienten förblir ohanterad tills platsens kompatibilitetskontroll körs igen och lyckas.  

  Ett undantag är när en klient är konfigurerad för en Internetbaserad hanteringsplats. I detta fall görs ingen kompatibilitetskontroll. Om du tilldelar klienter en plats som innehåller Internetbaserade platssystem och du anger en Internetbaserad hanteringsplats, måste du se till att du tilldelar klienten rätt plats. Om du av misstag tilldelar klienten till en Configuration Manager 2007-plats, en System Center 2012 Configuration Manager-plats eller en Configuration Manager-plats som inte har några Internetbaserade plats system roller, kommer klienten inte att hanteras.  

##  <a name="locating-management-points"></a>Hitta hanteringsplatser  
 När en klient har tilldelats en plats letar den upp en hanteringsplats på den platsen.  

 Klient datorer laddar ned en lista över hanterings platser som de kan ansluta till på platsen. Detta inträffar när klienten startas om eller var 25: e timme, eller om klienten identifierar en nätverks ändring, till exempel om datorn kopplar från och återansluter till nätverket eller om den får en ny IP-adress. Listan innehåller hanteringsplatser på intranätet och huruvida de godkänner klientanslutningar över HTTP eller HTTPS. När klient datorn är på Internet och klienten ännu inte har en lista över hanterings platser ansluter den till den angivna Internetbaserade hanterings platsen för att hämta en lista över hanterings platser. När klienten har en lista över hanteringsplatser för den tilldelade platsen väljer den en att ansluta till:  

-   När klienten är på intranätet och har ett giltigt PKI-certifikat som kan användas, väljer klienten HTTPS-hanteringsplatser framför HTTP-hanteringsplatser. Därefter letar den upp den närmaste hanteringsplatsen baserat på skogsmedlemskapet.  

-   När klienten är på Internet väljer den slumpmässigt en av de Internetbaserade hanterings platserna.  

Mobila enhets klienter som har registrerats av Configuration Manager bara ansluta till en hanterings plats på den tilldelade platsen och ansluter aldrig till hanterings platser på sekundära platser. De här klienterna ansluter alltid över HTTPS och hanteringsplatsen måste vara konfigurerad för att godkänna klientanslutningar över Internet. Om det finns fler än en hanterings plats för mobila enhets klienter på den primära platsen, väljer Configuration Manager slumpmässigt en av dessa hanterings platser under tilldelningen och den mobila enhets klienten fortsätter att använda samma hanterings plats.  

När klienten har laddat ned klientprinciper från en hanteringsplats på platsen är klienten en hanterad klient.  

##  <a name="downloading-site-settings"></a>Ladda ned platsinställningar  
 När platstilldelningen är klar och klienten har hittat en hanteringsplats, laddar en klientdator som använder Active Directory Domain Services för platskompatibilitetskontrollen ned klientrelaterade platsinställningar för sin tilldelade plats. Inställningarna omfattar villkoren för val av klientcertifikat, huruvida en lista över återkallade certifikat ska användas, och portnumren för klientförfrågan. Klienten fortsätter att kontrollera inställningarna regelbundet.  

 Om klientdatorer inte får platsinställningar från Active Directory Domain Services laddar de ned dem från hanteringsplatsen. Klient datorer kan också hämta plats inställningarna när de installeras med push-installation, eller så kan du ange dem manuellt med hjälp av CCMSetup. exe och klient installations egenskaper. Mer information om klient installations egenskaper finns i [om klient installations egenskaper](../../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="downloading-client-settings"></a>Ladda ned klientinställningar  
 Alla klienter laddar ned standardklientinställningsprincipen och eventuella anpassade klientinställningsprinciper. Software Center är beroende av dessa klientkonfigurationsprinciper för Windows-datorer och meddelar användarna att Software Center inte kan köras förrän den här konfigurationsinformationen har laddats ned. Beroende på de konfigurerade klientinställningarna kan den första nedladdningen av klientinställningar ta en stund och vissa klienthanteringsaktiviteter kanske inte kan köras förrän nedladdningen är klar.  

##  <a name="verifying-site-assignment"></a>Kontrollera platstilldelning  
 Du kan kontrol lera att platstilldelning har slutförts på något av följande sätt:  

-   För klienter på Windows-datorer använder du Configuration Manager på kontroll panelen och kontrollerar att plats koden visas korrekt på fliken **plats** .  

-   För klient datorer, i noden **till gångar och efterlevnad** > **enheter** , kontrollerar du att datorn visar **Ja** för kolumnen **klient** och rätt primär Platskod för kolumnen **platskod** .  

-   För mobilenhetsklienter på arbetsytan **Tillgångar och efterlevnad** använder du samlingen **Alla mobila enheter** för att kontrollera att den mobila enheten visar **Ja** för kolumnen **Klient** och rätt primär platskod för kolumnen **Platskod** .  

-   Använd rapporterna för klienttilldelning och registrering av mobila enheter.  

-   Använd filen LocationServices.log på klienten för klientdatorer.  

##  <a name="roaming-to-other-sites"></a>Nätverksväxla till andra platser  
 När klientdatorer på intranätet tilldelas till en primär plats, men ändrar nätverksplats så att den hamnar i en gränsgrupp som är konfigurerad för en annan plats, har de nätverksväxlat till en annan plats. När den här platsen är en sekundär plats för deras tilldelade plats kan klienterna använda en hanteringsplats i den sekundära platsen för att hämta klientprincip och överföra klientdata, vilket hindrar att data sickas via ett potentiellt långsamt nätverk. Om klienterna däremot nätverksväxlar inom gränserna för en annan primär plats eller en sekundär plats som inte är en underordnad plats till deras tilldelade plats använder klienterna alltid en hanteringsplats på deras tilldelade plats för att hämta klientprincip och överföra data till platsen.  

 De här klientdatorerna som nätverksväxlar till andra platser (alla primära och alla sekundära platser) kan alltid använda hanteringsplatser på andra platser för begäranden om innehållsplats. Hanteringsplatser på den aktuella platsen kan ge klienterna en lista över distributionsplatser med det innehåll som klienten begär.  

 För klient datorer som är konfigurerade för endast Internet-klient hantering, och för mobila enheter och Mac-datorer som har registrerats av Configuration Manager, kommunicerar dessa klienter endast med hanterings platser på deras tilldelade plats. De här klienterna kommunicerar aldrig med hanteringsplatser på sekundära platser eller med hanteringsplatser på andra primära platser.  
