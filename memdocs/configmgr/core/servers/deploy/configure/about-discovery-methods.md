---
title: Identifierings metoder
titleSuffix: Configuration Manager
description: Lär dig mer om tillgängliga identifierings metoder för att hitta enheter i nätverket, från Active Directory eller Azure Active Directory.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: af35d5a941d5fd9bde2f87c8fb700b9d85e10b00
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078659"
---
# <a name="about-discovery-methods-for-configuration-manager"></a>Om identifierings metoder för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager identifierings metoder hitta olika enheter i nätverket, enheter och användare från Active Directory eller användare från Azure Active Directory (Azure AD). För att effektivt kunna använda en identifierings metod bör du förstå dess tillgängliga konfigurationer och begränsningar.  



##  <a name="active-directory-forest-discovery"></a><a name="bkmk_aboutForest"></a>Active Directory skogs identifiering  
 **Konfigurerbar:** Ja  

 **Aktive rad som standard:** Nej  

 **Konton** som du kan använda för att köra den här metoden:  

-   **Konto för identifiering av Active Directory skog** (användardefinierad)  

-   Plats serverns **dator konto**  

Till skillnad från andra identifierings metoder för Active Directory identifierar Active Directory skogs identifiering inte resurser som du kan hantera. I stället identifierar den här metoden nätverks platser som kon figurer ATS i Active Directory. Den kan konvertera dessa platser till gränser för användning i hela hierarkin.  

När den här metoden körs genomsöks den lokala Active Directory skogen, varje betrodd skog och varje ytterligare skog som du konfigurerar i noden **Active Directory skogar** i Configuration Managers-konsolen.  

Använd Active Directory skogs identifiering för att:  

-   Identifiera Active Directory platser och undernät och skapa sedan Configuration Manager gränser baserat på dessa nätverks platser.  

-   Identifiera supernäten som har tilldelats till en Active Directorys plats. Konvertera varje övernät till ett IP-adressintervall.  

-   Publicera till Active Directory Domain Services (AD DS) i en skog när du publicerar till den skogen är aktive rad. Det angivna Active Directory skogs kontot måste ha behörighet till den skogen.  

Du kan hantera Active Directory skogs identifiering i Configuration Manager-konsolen. Gå till arbets ytan **Administration** och expandera **konfigurationen av hierarkin**.   

-   **Identifierings metoder**: Aktivera Active Directory identifiering av skogar som ska köras på den översta nivån i hierarkin. Du kan också ange ett enkelt schema för att köra identifiering. Konfigurera den för att automatiskt skapa gränser från IP-undernät och Active Directory platser som identifieras. Active Directory skogs identifiering kan inte köras på en underordnad primär plats eller på en sekundär plats.  

-   **Active Directory skogar**: Konfigurera ytterligare skogar att identifiera, ange varje Active Directory skogs konto och konfigurera publicering till varje skog. Övervaka identifierings processen. Lägg till IP-undernät och Active Directory platser som Configuration Manager gränser och medlemmar i gräns grupper.  

Om du vill konfigurera publicering för Active Directory skogar för varje plats i hierarkin ansluter du Configuration Manager-konsolen till platsen på den översta nivån i hierarkin. Fliken **publicering** i dialog rutan **egenskaper** för en Active Directory plats kan bara visa den aktuella platsen och dess underordnade platser. När publicering är aktiverat för en skog och den skogens schema har utökats för Configuration Manager, publiceras följande information för varje plats som är aktive rad för att publicera till den Active Directory skogen:  

-    **SMS-plats-&lt;plats kod>**

-   **SMS-MP –&lt;plats kod>-&lt;plats system serverns namn>**  

-   **SMS-SLP-&lt;plats kod>-&lt;plats system serverns namn>**  

-   **SMS-&lt;platskod>-&lt;Active Directory webbplats namn eller undernät>**  

> [!NOTE]  
>  Sekundära platser använder alltid den sekundära serverns datorkonto för att publicera till Active Directory. Om du vill att sekundära platser ska publicera till Active Directory kontrollerar du att dator kontot för den sekundära plats servern har behörighet att publicera till Active Directory. En sekundär plats kan inte publicera data till en skog som inte är betrodd.  

> [!CAUTION]  
>  När du avmarkerar alternativet för att publicera en plats till en Active Directory skog tas all tidigare publicerad information för den platsen, inklusive tillgängliga plats system roller, bort från Active Directory.  

Åtgärder för identifiering av Active Directory skogar registreras i följande loggar:  

-   Alla åtgärder, förutom åtgärder som rör publicering, registreras i filen **ADForestDisc. log** i mappen ** &lt;InstallationPath> \Logs** på plats servern.  

-   Active Directory publicerings åtgärder för skogs identifiering registreras i **hman. log** -och **sitecomp. log** -filerna i mappen ** &lt;InstallationPath> \Logs** på plats servern.  

Mer information om hur du konfigurerar den här identifierings metoden finns i [Konfigurera identifierings metoder](configure-discovery-methods.md#BKMK_ConfigADForestDisc).  



##  <a name="active-directory-group-discovery"></a><a name="bkmk_aboutGroup"></a>Active Directory grupp identifiering  
**Konfigurerbar:** Ja  

**Aktive rad som standard:** Nej  

**Konton** som du kan använda för att köra den här metoden:  

-   **Konto för Active Directory grupp identifiering** (användardefinierad)  

-   Plats serverns **dator konto**  

> [!TIP]  
>  Utöver informationen i det här avsnittet finns [vanliga funktioner i Active Directory grupp, system och användar identifiering](#bkmk_shared).  

Använd den här metoden för att söka Active Directory Domain Services för att identifiera:  

-   Lokala, globala och universella säkerhets grupper.  

-   Medlemskap i grupper.  

-   Begränsad information om en grupps medlems datorer och användare, även när en annan identifierings metod inte tidigare har identifierat dessa datorer och användare.  

Den här identifierings metoden är avsedd att identifiera grupper och grupp relationer för medlemmar i grupper. Som standard identifieras bara säkerhets grupper. Om du också vill hitta medlemskap i distributions grupper måste du markera kryss rutan för alternativet **identifiera medlemskap i distributions grupper** på fliken **alternativ** i dialog rutan **Egenskaper för Active Directory grupp identifiering** .  

Active Directory grupp identifiering stöder inte utökade Active Directory-attribut som kan identifieras med hjälp av Active Directory system identifiering eller Active Directory användar identifiering. Eftersom den här identifierings metoden inte är optimerad för att identifiera dator-och användar resurser kan du överväga att köra den här identifierings metoden när du har kört Active Directory system identifiering och Active Directory användar identifiering. Detta förslag beror på att den här metoden skapar en fullständig identifierings data post (DDR) för grupper, men bara ett begränsat DDR för datorer och användare som är medlemmar i grupper.  

Du kan konfigurera följande identifierings omfång som styr hur den här metoden söker efter information:  

-   **Plats**: Använd en plats om du vill söka i en eller flera Active Directory behållare. Det här omfångs alternativet stöder en rekursiv sökning av de angivna Active Directory behållarna. Den här processen söker igenom varje underordnad behållare under den behållare som du anger. Den fortsätter tills inga fler underordnade behållare har hittats.  

-   **Grupper**: Använd grupper om du vill söka i en eller flera av de Active Directory grupperna. Du kan konfigurera **Active Directory-domän** att använda standard domänen och skogen, eller begränsa sökningen till en individuell domänkontrollant. Dessutom kan du ange en eller flera grupper att söka i. Om du inte anger minst en grupp genomsöks alla grupper som finns på den angivna **Active Directory-domäns** platsen.  

> [!CAUTION]  
>  När du konfigurerar ett identifierings omfång väljer du bara de grupper som du måste identifiera. Den här rekommendationen beror på att Active Directory grupp identifiering försöker identifiera varje medlem i varje grupp i identifierings omfånget. Identifiering av stora grupper kan kräva stor användning av bandbredd och Active Directory resurser.  

> [!NOTE]  
>  Innan du kan skapa samlingar som baseras på utökade Active Directory-attribut och se till att identifiera korrekta identifierings resultat för datorer och användare, kör Active Directory system identifiering eller Active Directory användar identifiering, beroende på vad du vill identifiera.  

Åtgärder för Active Directory grupp identifiering registreras i filen **adsgdis. log** i mappen ** &lt;\>InstallationPath \Logs** på plats servern.  

Mer information om hur du konfigurerar den här identifierings metoden finns i [Konfigurera identifierings metoder](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



##  <a name="active-directory-system-discovery"></a><a name="bkmk_aboutSystem"></a>Active Directory system identifiering  
**Konfigurerbar:** Ja  

**Aktive rad som standard:** Nej  

**Konton** som du kan använda för att köra den här metoden:  

-   **Active Directory konto för system identifiering** (användardefinierad)  

-   Plats serverns **dator konto**  

> [!TIP]  
>  Utöver informationen i det här avsnittet finns [vanliga funktioner i Active Directory grupp, system och användar identifiering](#bkmk_shared).  

Använd den här identifierings metoden för att söka efter de angivna Active Directory Domain Services platser för dator resurser som kan användas för att skapa samlingar och frågor. Du kan också installera Configuration Manager-klienten på en identifierad enhet genom att använda push-installation av klienter.  

Som standard identifierar den här metoden grundläggande information om datorn, inklusive följande attribut:  

-   Datornamn  

-   Operativ system och version  

-   Namn på Active Directory behållare  

-   IP-adress  

-   Active Directory-plats  

-   Tidstämpel för senaste inloggning  

För att kunna skapa ett DDR för en dator måste Active Directory system identifieringen kunna identifiera dator kontot och sedan matcha dator namnet med en IP-adress.  

I dialog rutan **Active Directory egenskaper för system identifiering** på fliken **Active Directory attribut** kan du Visa en fullständig lista över standardattribut som identifieras av objektet. Du kan också konfigurera metoden för att upptäcka ytterligare (utökade) attribut.  

Åtgärder för Active Directory system identifiering registreras i filen **adsysdis. log** i mappen ** &lt;\>InstallationPath \Logs** på plats servern.  

Mer information om hur du konfigurerar den här identifierings metoden finns i [Konfigurera identifierings metoder](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



##  <a name="active-directory-user-discovery"></a><a name="bkmk_aboutUser"></a>Active Directory användar identifiering  
**Konfigurerbar:** Ja  

**Aktive rad som standard:** Nej  

**Konton** som du kan använda för att köra den här metoden:  

-   **Konto för Active Directory användar identifiering** (användardefinierad)  

-   Plats serverns **dator konto**  

> [!TIP]  
>  Utöver informationen i det här avsnittet finns [vanliga funktioner i Active Directory grupp, system och användar identifiering](#bkmk_shared).  

Använd den här identifierings metoden för att söka Active Directory Domain Services för att identifiera användar konton och associerade attribut. Som standard identifierar den här metoden grundläggande information om användar kontot, inklusive följande attribut:  

-   Användarnamn  

-   Unikt användar namn (inklusive domän namn)  

-   Domain  

-   Active Directory behållar namn  

I dialog rutan **Active Directory egenskaper för användar identifiering** går du till fliken **Active Directory attribut** och visar den fullständiga standard listan över objektattribut som identifieras. Du kan också konfigurera metoden för att upptäcka ytterligare (utökade) attribut.

Åtgärder för Active Directory identifiering av användare registreras i filen **adusrdis. log** i mappen ** &lt;\>InstallationPath \Logs** på plats servern.  

Mer information om hur du konfigurerar den här identifierings metoden finns i [Konfigurera identifierings metoder](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



## <a name="azure-active-directory-user-discovery"></a><a name="azureaddisc"></a>Azure Active Directory användar identifiering

Använd Azure Active Directory (Azure AD) identifiering av användare för att söka i Azure AD-prenumerationen efter användare med modern moln identitet. Identifiering av Azure AD-användare kan hitta följande attribut:

- objectId
- displayName
- e-post
- mailNickname
- onPremisesSecurityIdentifier
- userPrincipalName
- AAD tenantID
- onPremisesDomainName
- Egna namnet onpremisessamaccountname
- onPremisesDistinguishedName

Den här metoden stöder fullständig och delta-synkronisering av användarattribut från Azure AD. Den här informationen kan sedan användas tillsammans med identifierings data som du samlar in från andra identifierings metoder.

Åtgärder för identifiering av Azure AD-användare registreras i filen **SMS_AZUREAD_DISCOVERY_AGENT. log** på plats servern på den översta nivån i hierarkin.

Information om hur du konfigurerar identifiering av Azure AD-användare finns i [Konfigurera Azure-tjänster](azure-services-wizard.md) för moln hantering. Information om hur du konfigurerar den här identifierings metoden finns i [Konfigurera identifiering av Azure AD-användare](configure-discovery-methods.md#azureaadisc).

## <a name="azure-active-directory-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a>Azure Active Directory användar grupp identifiering
<!--3611956-->
*(Introduceras som en [för hands versions funktion](../../manage/pre-release-features.md) i version 1906)*

Du kan identifiera användar grupper och medlemmar i dessa grupper från Azure Active Directory (Azure AD). Identifiering av användar grupper i Azure AD kan hitta följande attribut:

- objectId
- displayName
- mailNickname
- onPremisesSecurityIdentifier
- AAD tenantID

Åtgärder för identifiering av Azure AD-användargrupp registreras i filen **SMS_AZUREAD_DISCOVERY_AGENT. log** på plats servern på den översta nivån i hierarkin. Information om hur du konfigurerar den här identifierings metoden finns i [Konfigurera identifiering av användar grupper i Azure AD](configure-discovery-methods.md#bkmk_azuregroupdisco).

##  <a name="heartbeat-discovery"></a><a name="bkmk_aboutHeartbeat"></a>Pulsslags identifiering  
**Konfigurerbar:** Ja  

**Aktive rad som standard:** Ja  

**Konton** som du kan använda för att köra den här metoden:  

-   Plats serverns **dator konto**  

Pulsslags identifiering skiljer sig från andra Configuration Manager identifierings metoder. Den är aktive rad som standard och körs på varje dator klient (i stället för på en plats Server) för att skapa en DDR. För mobila enhets klienter skapas detta DDR av den hanterings plats som den mobila enhets klienten använder. För att underhålla databas posten för Configuration Manager klienter ska du inte inaktivera pulsslags identifiering. Förutom att underhålla databas posten, kan den här metoden tvinga identifiering av en dator som en ny resurs post. Du kan också fylla i databas posten för en dator som har tagits bort från databasen.  

Pulsslags identifieringen körs enligt ett schema som kon figurer ATS för alla klienter i hierarkin. Standardschemat för pulsslags identifiering anges var sjunde dag. Om du ändrar pulsslags identifierings intervallet bör du se till att det körs oftare än plats underhålls aktiviteten **ta bort föråldrade identifierings data**. Den här uppgiften tar bort inaktiva klient poster från plats databasen. Du kan bara konfigurera aktiviteten **ta bort föråldrade identifierings data** för primära platser. 

Du kan också aktivera pulsslags identifiering manuellt på en enskild klient. Kör **cykeln för identifierings data insamling** på fliken **åtgärd** i en klients Configuration Manager kontroll panel.  

När pulsslags identifieringen körs skapar den ett DDR som innehåller klientens aktuella information. Klienten kopierar sedan den här lilla filen (ungefär 1 KB) till en hanterings plats så att en primär plats kan bearbeta den. Filen har följande information:  

-   Nätverks plats  

-   NetBIOS-namn  

-   Version av klient agenten  

-   Information om drift status  

Pulsslags identifiering är den enda identifierings metod som innehåller information om klient installations status. Det gör det genom att uppdatera system resursens klient-attribut för att ange ett värde som är lika med **Ja**.  

> [!NOTE]  
>  Även om pulsslags identifiering har inaktiverats skapas och skickas fortfarande identifierings data för klienter med aktiva mobila enheter. Det här beteendet säkerställer att aktiviteten för att **ta bort föråldrade identifierings data** inte påverkar aktiva mobila enheter. När aktiviteten **ta bort föråldrade identifierings data** tar bort en databas post för en mobil enhet återkallas även enhets certifikatet. Den här åtgärden blockerar den mobila enheten från att ansluta till hanterings platser.  

Åtgärder för pulsslags identifiering loggas på följande platser:  

-   För dator klienter registreras pulsslags identifierings åtgärder på klienten i filen **InventoryAgent. log** i mappen *%Windir%\CCM\Logs* .  

-   För mobila enhets klienter registreras pulsslags identifierings åtgärder i filen **DMPRP. log** i mappen *% Program Files%\CCM\Logs* för den hanterings plats som den mobila enhets klienten använder.  

Mer information om hur du konfigurerar den här identifierings metoden finns i [Konfigurera identifierings metoder](configure-discovery-methods.md#BKMK_ConfigHBDisc).  



##  <a name="network-discovery"></a><a name="bkmk_aboutNetwork"></a>Nätverks identifiering  
**Konfigurerbar:** Ja  

**Aktive rad som standard:** Nej  

**Konton** som du kan använda för att köra den här metoden:  

-   Plats serverns **dator konto**  

Använd den här metoden för att identifiera nätverkets topologi och identifiera enheter i nätverket med en IP-adress. Nätverks identifiering söker efter IP-aktiverade resurser genom att fråga följande entiteter: 
- Servrar som kör en Microsoft-implementering av DHCP
- ARP-cache (Address Resolution Protocol) i nätverksroutrar
- SNMP-aktiverade enheter
- Active Directory domäner  

Innan du kan använda nätverks identifiering måste du ange den identifierings *nivå* som ska köras. Du kan också konfigurera en eller flera identifierings mekanismer som gör det möjligt för nätverks identifiering att fråga efter nätverks segment eller enheter. Du kan också konfigurera inställningar som hjälper dig att kontrol lera identifierings åtgärder i nätverket. Slutligen definierar du ett eller flera scheman för när nätverks identifieringen körs.  

För att den här metoden ska kunna identifiera en resurs måste nätverks identifieringen identifiera IP-adressen och nät masken för resursen. Följande metoder används för att identifiera nät masken för ett objekt:  

-   **Router ARP-cache:** Nätverks identifiering frågar ARP-cachen för en router för att hitta information om undernät. Normalt har data i en router ARP-cache en kort tid till Live. Därför kanske ARP-cachen inte längre innehåller information om det begärda objektet när nätverks identifieringen frågar ARP-cachen.  

-   **DHCP:** Nätverks identifiering frågar varje DHCP-server som du anger för att identifiera de enheter som DHCP-servern har angett ett lån för. Nätverks identifiering stöder bara DHCP-servrar som kör Microsoft-implementeringen av DHCP.  

-   **SNMP-enhet:** Nätverks identifiering kan fråga en SNMP-enhet direkt. För att nätverks identifiering ska kunna fråga en enhet måste en lokal SNMP-agent vara installerad på enheten. Konfigurera även nätverks identifiering så att det använder det community-namn som SNMP-agenten använder.  

När identifieringen identifierar ett IP-adresserat objekt och kan fastställa objektets nätmask, skapas ett DDR för objektet. Eftersom olika typer av enheter ansluter till nätverket, identifierar nätverks identifieringen resurser som inte stöder Configuration Manager-klienten. Till exempel kan enheter som kan identifieras men inte hanteras inkludera skrivare och routrar.  

Nätverks identifiering kan returnera flera attribut som en del av identifierings posten som den skapar. Dessa attribut är:  

-   NetBIOS-namn  

-   IP-adresser  

-   Resurs domän  

-   System roller  

-   SNMP-gruppens namn  

-   MAC-adresser  

Nätverks identifierings aktivitet registreras i filen **Netdisk. log** i * &lt;\>InstallationPath \Logs* på den plats server som kör identifieringen.  

 Mer information om hur du konfigurerar den här identifierings metoden finns i [Konfigurera identifierings metoder](configure-discovery-methods.md#BKMK_ConfigNetworkDisc).  

> [!NOTE]  
>  Komplexa nätverk och anslutningar med låg bandbredd kan göra att nätverks identifieringen körs långsamt och genererar betydande nätverks trafik. Vi rekommenderar att du bara kör nätverks identifiering när de andra identifierings metoderna inte kan hitta de resurser som du behöver identifiera. Använd till exempel nätverks identifiering om du måste identifiera arbets grupps datorer. Andra identifierings metoder identifierar inte arbets grupps datorer.  

###  <a name="levels-of-network-discovery"></a><a name="BKMK_NetDiscLevels"></a>Nätverks identifierings nivåer  
När du konfigurerar nätverks identifiering anger du en av tre identifierings nivåer:  

|Identifierings nivå|Information|  
|------------------------|-------------|  
|Topologi|Den här nivån identifierar routrar och undernät, men identifierar inte en under nät mask för objekt.|  
|Topologi och klient|Förutom topologi identifierar den här nivån potentiella klienter som datorer och resurser som skrivare och routrar. Den här identifierings nivån försöker identifiera nät masken för objekt som hittas.|  
|Topologi, klient och klient operativ system|Förutom topologi och potentiella klienter försöker den här nivån identifiera datorns operativ system namn och version. På den här nivån används Windows-webbläsare och Windows-baserade nätverks anrop.|  

 Med varje stegvis nivå ökar nätverks identifieringen aktivitetens och nätverkets bandbredds användning. Överväg nätverks trafiken som kan genereras innan du aktiverar alla aspekter av nätverks identifiering.  

 När du till exempel först använder nätverks identifiering kan du starta med bara topologin för att identifiera din nätverks infrastruktur. Konfigurera sedan om nätverks identifieringen för att identifiera objekt och deras enhets operativ system. Du kan också konfigurera inställningar som begränsar nätverks identifieringen till ett bestämt intervall med nätverks segment. På så sätt identifierar du objekt på nätverks platser som du behöver och undviker onödig nätverks trafik. Med den här processen kan du också identifiera objekt från Edge-routrar eller utanför nätverket.  

###  <a name="network-discovery-options"></a><a name="BKMK_NetDiscOptions"></a>Alternativ för nätverks identifiering  
Konfigurera ett eller flera av de här alternativen om du vill aktivera nätverks identifiering för att söka efter IP-adresser bara enheter.  

> [!NOTE]  
>  Nätverks identifiering körs i kontexten för dator kontot för den plats server som kör identifieringen. Om dator kontot inte har behörighet till en obetrodd domän, kan inte domän-och DHCP-serverkonfigurationer identifiera resurser.  

#### <a name="dhcp"></a>DHCP  

Ange varje DHCP-server som du vill att nätverks identifiering ska fråga. (Nätverks identifiering stöder bara DHCP-servrar som kör Microsoft-implementeringen av DHCP.)  

-   Nätverks identifiering hämtar information genom att använda fjärran rop till databasen på DHCP-servern.  

-   Nätverks identifiering kan fråga både 32-bitars och 64-bitars DHCP-servrar för en lista över enheter som är registrerade på varje server.  

-   För att nätverks identifiering ska kunna skicka frågor till en DHCP-server måste dator kontot för den server som kör identifieringen vara medlem i gruppen DHCP-användare på DHCP-servern. Till exempel finns den här åtkomst nivån när något av följande påståenden stämmer:  

    -   Den angivna DHCP-servern är DHCP-servern för den server som kör identifieringen.  

    -   Datorn som kör identifieringen och DHCP-servern finns i samma domän.  

    -   Det finns ett dubbelriktat förtroende mellan datorn som kör identifieringen och DHCP-servern.  

    -   Plats servern är medlem i gruppen DHCP-användare.  

-   När nätverks identifieringen räknar upp en DHCP-server identifierar den inte alltid statiska IP-adresser. Nätverks identifiering hittar inte IP-adresser som ingår i ett undantags intervall av IP-adresser på DHCP-servern. Den identifierar inte heller IP-adresser som är reserverade för manuell tilldelning.  

#### <a name="domains"></a>Domäner  

Ange varje domän som du vill att nätverks identifiering ska fråga.  

-   Dator kontot för plats servern som kör identifiering måste ha behörighet att läsa domän kontrol Lanterna i varje angiven domän.  

-   Om du vill identifiera datorer från den lokala domänen måste du aktivera tjänsten Computer Browser på minst en dator. Datorn måste finnas i samma undernät som den plats server som kör nätverks identifiering.  

-   Nätverks identifiering kan identifiera alla datorer som du kan visa från plats servern när du bläddrar i nätverket.  

-   Nätverks identifiering hämtar IP-adressen. Sedan används en Internet Control Message Protocol (ICMP)-ekobegäran för att pinga varje enhet som hittas. **Ping** -kommandot hjälper till att avgöra vilka datorer som är aktiva för närvarande.  

#### <a name="snmp-devices"></a>SNMP-enheter  

Ange varje SNMP-enhet som du vill att nätverks identifiering ska fråga.  

-   Nätverks identifiering hämtar ipNetToMediaTable-värdet från alla SNMP-enheter som svarar på frågan. Det här värdet returnerar matriser med IP-adresser som är klient datorer eller andra resurser som skrivare, routrar eller andra IP-adresser bara enheter.  

-   Om du vill fråga en enhet måste du ange IP-adressen eller NetBIOS-namnet på enheten.  

-   Konfigurera nätverks identifiering att använda grupp namnet på enheten, eller så avvisar enheten den SNMP-baserade frågan.  


###  <a name="limiting-network-discovery"></a><a name="BKMK_LimitNetDisc"></a>Begränsa nätverks identifiering  
När nätverks identifiering frågar en SNMP-enhet på gränsen för nätverket kan den identifiera information om undernät och SNMP-enheter som ligger utanför ditt omedelbara nätverk. Använd följande information för att begränsa nätverks identifieringen genom att konfigurera de SNMP-enheter som identifieringen kan kommunicera med och genom att ange nätverks segmenten som ska frågas.  

#### <a name="subnets"></a>Undernät  

Konfigurera de undernät som nätverks identifierings frågorna ska använda när de använder alternativen SNMP och DHCP. De här två alternativen söker bara igenom de aktiverade under näten.  

En DHCP-begäran kan till exempel returnera enheter från platser i hela nätverket. Om du bara vill identifiera enheter i ett särskilt undernät anger du och aktiverar det speciella under nätet på fliken **undernät** i dialog rutan **Egenskaper för nätverks identifiering** . När du anger och aktiverar undernät begränsar du framtida identifierings aktiviteter för DHCP och SNMP till dessa undernät.  

> [!NOTE]  
>  Under näts konfigurationerna begränsar inte de objekt som identifieras av **domän** identifierings alternativet.  

#### <a name="snmp-community-names"></a>SNMP-gruppnamn  

Om du vill aktivera nätverks identifiering för att skicka frågor till en SNMP-enhet konfigurerar du nätverks identifiering med enhetens grupp namn. Om nätverks identifiering inte konfigureras med hjälp av SNMP-enhetens community-namn, avvisar enheten frågan.  

#### <a name="maximum-hops"></a>Maximalt antal hopp  

När du konfigurerar maximalt antal router hopp begränsar du antalet nätverks segment och routrar som nätverks identifieringen kan fråga med hjälp av SNMP.  

Antalet hopp som du konfigurerar begränsar antalet ytterligare enheter och nätverks segment som nätverks identifiering kan fråga.  

Till exempel, en topologi – endast identifiering med **0** (noll) router hopp identifierar det undernät som den ursprungliga servern finns på. Den innehåller alla routrar i det under nätet.  

Följande diagram visar vad en topologi – endast nätverks identifierings fråga hittar när den körs på Server 1 med 0 router-hopp angivna: undernät D och router 1.  

 ![Bild av identifiering med noll router-hopp](media/Disc-0.gif)  

 Följande diagram visar hur en topologi och klient nätverks identifierings fråga hittar när den körs på Server 1 med 0 router-hopp angivna: undernät D och router 1 och alla potentiella klienter i undernät D.  

 ![Bild av identifiering med en router-hopp](media/Disc-1.gif)  

 För att få en bättre uppfattning om hur ytterligare router hopp kan öka mängden nätverks resurser som identifieras, bör du tänka på följande nätverk:  

 ![Bild av identifiering med två router-hopp](media/Disc-2.gif)  

 Om du kör en nätverks identifiering med endast topologi från Server 1 med ett router-hopp identifieras följande entiteter:  

-   Router 1 och undernät 10.1.10.0 (hittades med noll hopp)  

-   Undernät 10.1.20.0 och 10.1.30.0, Subnet A och router 2 (finns i det första hoppet)  

> [!WARNING]  
>  Varje ökning av antalet router-hopp kan avsevärt öka antalet identifierade resurser och öka nätverks bandbredden som används av nätverks identifieringen.  



##  <a name="server-discovery"></a><a name="bkmk_aboutServer"></a>Server identifiering  
**Konfigurerbar:** Nej  

Förutom de användar konfigurerbara identifierings metoderna använder Configuration Manager en process som kallas **Server identifiering** (SMS_WINNT_SERVER_DISCOVERY_AGENT). Den här identifierings metoden skapar resurs poster för datorer som är plats system, till exempel en dator som är konfigurerad som hanterings plats.  



##  <a name="common-features-of-active-directory-group-discovery-system-discovery-and-user-discovery"></a><a name="bkmk_shared"></a>Vanliga funktioner i Active Directory grupp identifiering, system identifiering och användar identifiering  
Det här avsnittet innehåller information om funktioner som är gemensamma för följande identifierings metoder:  

-   Identifiering av Active Directory-grupper  

-   Identifiering av Active Directory-system  

-   Identifiering av Active Directory-användare  

> [!NOTE]  
>  Informationen i det här avsnittet gäller inte för identifiering av Active Directory skogar.  

Dessa tre identifierings metoder liknar konfigurationen och åtgärden. De kan identifiera datorer, användare och information om grupp medlemskap i resurser som lagras i Active Directory Domain Services. Identifierings processen hanteras av en identifierings agent. Agenten körs på plats servern på varje plats där identifiering har kon figurer ATS för körning. Du kan konfigurera var och en av dessa identifierings metoder för att söka i en eller flera Active Directory platser som plats instanser i den lokala skogen eller fjär skogar.  

När identifieringen söker i en ej betrodd skog för resurser, måste identifierings agenten kunna lösa följande problem:  

-   För att identifiera en dator resurs genom att använda Active Directory system identifiering måste identifierings agenten kunna matcha FQDN för resursen. Om det inte går att matcha det fullständiga domän namnet försöker den matcha resursen med dess NetBIOS-namn.  

-   För att identifiera en användare eller grupp resurs genom att använda Active Directory identifiering av användare eller Active Directory grupp identifiering måste identifierings agenten kunna matcha FQDN för det domänkontrollant namn som du anger för Active Directory platsen.  

För varje plats som du anger kan du konfigurera enskilda sökalternativ, t. ex. Aktivera en rekursiv sökning av platsens Active Directory underordnade behållare. Du kan också konfigurera ett unikt konto som ska användas när det söker efter den platsen. Det här kontot ger flexibilitet vid konfigurering av en identifierings metod på en plats för att söka efter flera Active Directory platser i flera skogar. Du behöver inte konfigurera ett enda konto som har behörigheter till alla platser.  

När var och en av dessa tre identifierings metoder körs vid en viss plats, kontaktar Configuration Manager plats servern på den platsen närmaste domänkontrollant i den angivna Active Directory skogen för att hitta Active Directory resurser. Domänen och skogen kan vara i ett Active Directory läge som stöds. Det konto som du tilldelar till varje plats instans måste ha **Läs** behörighet för de angivna Active Directory platserna.

Identifiering söker igenom de angivna platserna efter objekt och försöker sedan samla in information om dessa objekt. Ett DDR skapas när tillräckligt med information om en resurs kan identifieras. Den information som krävs varierar beroende på vilken identifierings metod som används.  

Om du konfigurerar samma identifierings metod att köras på olika Configuration Manager-platser för att kunna skicka frågor till lokala Active Directory-servrar kan du konfigurera varje plats med en unik uppsättning identifierings alternativ. Eftersom identifierings data delas med varje plats i hierarkin undviker du överlappa dessa konfigurationer för att effektivt upptäcka varje resurs en gång.

För mindre miljöer bör du överväga att köra varje identifierings metod endast på en plats i hierarkin. Den här konfigurationen minskar administrationen och risken för flera identifierings åtgärder för att identifiera samma resurser igen. När du minimerar antalet webbplatser som kör identifieringen minskar du den totala nätverks bandbredden som identifieringen använder. Du kan också minska det totala antalet identifierings data poster som skapas och måste bearbetas av plats servrarna.  

Många av konfigurationerna för identifierings metoden är själv för klar Ande. Använd följande avsnitt för mer information om de identifierings alternativ som kan kräva ytterligare information innan du konfigurerar dem.  

Följande alternativ är tillgängliga för användning med flera Active Directory identifierings metoder:  

-   [Delta identifiering](#bkmk_delta)  

-   [Filtrera inaktuella dator poster efter domän inloggning](#bkmk_stalelogon)  

-   [Filtrera inaktuella poster efter dator lösen ord](#bkmk_stalepassword)  

-   [Sök efter anpassade Active Directory-attribut](#bkmk_customAD)  


###  <a name="delta-discovery"></a><a name="bkmk_delta"></a>Delta identifiering  
Tillgängligt för:  

-   Identifiering av Active Directory-grupper  

-   Identifiering av Active Directory-system  

-   Identifiering av Active Directory-användare  

Delta identifiering är inte en oberoende identifierings metod, men ett alternativ som är tillgängligt för tillämpliga identifierings metoder. Delta identifiering söker efter vissa Active Directory attribut för ändringar som har gjorts sedan den senaste fullständiga identifierings cykeln för tillämplig identifierings metod. Attributändringar skickas till Configuration Manager databasen för att uppdatera resursens identifierings post.  

Delta identifiering körs som standard på en fem minuters cykel. Det här schemat är mycket mer frekvent än det typiska schemat för en fullständig identifierings cykel. Den här frekventa cykeln är möjlig eftersom delta identifieringen använder färre plats servrar och nätverks resurser än en fullständig identifierings cykel. När du använder delta identifiering kan du minska frekvensen för den fullständiga identifierings cykeln för identifierings metoden.  

Följande är de vanligaste ändringarna som identifieras av delta identifiering:  

-   Nya datorer eller användare som lagts till i Active Directory  

-   Ändringar av grundläggande information om datorer och användare  

-   Nya datorer eller användare som läggs till i en grupp  

-   Datorer eller användare som tas bort från en grupp  

-   Ändringar av system grupps objekt  

Även om delta identifiering kan identifiera nya resurser och ändringar i grupp medlemskap, kan det inte identifiera när en resurs har tagits bort från Active Directory. Identifiering av DDR som skapats av delta identifiering bearbetas på samma sätt som den identifierings data poster som skapas av en fullständig identifierings cykel.  

Du konfigurerar delta identifiering på fliken **avsöknings schema** i egenskaperna för varje identifierings metod.  


###  <a name="filter-stale-computer-records-by-domain-logon"></a><a name="bkmk_stalelogon"></a>Filtrera inaktuella dator poster efter domän inloggning  
Tillgängligt för:  

-   Identifiering av Active Directory-grupper  

-   Identifiering av Active Directory-system  

Du kan konfigurera identifiering så att den utesluter datorer med en inaktuell dator post. Detta undantag baseras på datorns senaste domän inloggning. När det här alternativet är aktiverat utvärderar Active Directory system identifiering varje dator som identifieras. Active Directory Group Discovery utvärderar varje dator som är medlem i en grupp som identifieras.  

Använd det här alternativet:  

-   Datorer måste konfigureras för att uppdatera attributet **lastLogonTimestamp** i Active Directory Domain Services.  

-   Den Active Directory domän funktions nivån måste vara inställd på Windows Server 2003 eller senare.  

När du konfigurerar tiden efter den senaste inloggning som du vill använda för den här inställningen bör du ta hänsyn till intervallet för replikering mellan domänkontrollanter.  

Du konfigurerar filtrering på fliken **alternativ** i dialog rutorna Active Directory egenskaper för **System identifiering** och **Active Directory grupp identifiering** . Välj att **bara identifiera datorer som har loggat in på en domän under en viss tids period**.  

> [!WARNING]  
>  När du konfigurerar det här filtret och **filtrerar inaktuella poster efter dator lösen ord**, utesluter identifieringen datorer som uppfyller kriterierna för något av filtren.  


###  <a name="filter-stale-records-by-computer-password"></a><a name="bkmk_stalepassword"></a>Filtrera inaktuella poster efter dator lösen ord  
Tillgängligt för:  

-   Identifiering av Active Directory-grupper  

-   Identifiering av Active Directory-system  

Du kan konfigurera identifiering så att den utesluter datorer med en inaktuell dator post. Detta undantag baseras på den senaste lösen ords uppdateringen för dator kontot från datorn. När det här alternativet är aktiverat utvärderar Active Directory system identifiering varje dator som identifieras. Active Directory Group Discovery utvärderar varje dator som är medlem i en grupp som identifieras.  

Använd det här alternativet:  

-   Datorer måste konfigureras för att uppdatera attributet **pwdLastSet** i Active Directory Domain Services.  

När du konfigurerar det här alternativet bör du ta hänsyn till intervallet för uppdateringar av det här attributet. Överväg också replikeringsintervall mellan domänkontrollanter.  

Du konfigurerar filtrering på fliken **alternativ** i dialog rutorna Active Directory egenskaper för **System identifiering** och **Active Directory grupp identifiering** . Välj att **bara identifiera datorer som har uppdaterat sina lösen ord för dator kontot under en viss tids period**.  

> [!WARNING]  
>  När du konfigurerar det här filtret och **filtrerar inaktuella poster efter domän inloggning**, exkluderar identifieringen datorer som uppfyller kriterierna för något av filtren.  


###  <a name="search-customized-active-directory-attributes"></a><a name="bkmk_customAD"></a>Sök efter anpassade Active Directory-attribut  
 Tillgängligt för:  

-   Identifiering av Active Directory-system  

-   Identifiering av Active Directory-användare  

Varje identifierings metod stöder en unik lista med Active Directory attribut som kan identifieras.  

Du kan visa och konfigurera listan med anpassade attribut på fliken **Active Directory attribut** i dialog rutorna **Egenskaper för Active Directory System identifiering** och **Active Directory användar identifiering** .  
