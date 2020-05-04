---
title: Aktiverar klienter
titleSuffix: Configuration Manager
description: Planera hur du aktiverar klienter i Configuration Manager att använda Wake On LAN (WOL).
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feea1cdea52b76b900497e84eea210444535fcd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713263"
---
# <a name="plan-how-to-wake-up-clients-in-configuration-manager"></a>Planera aktivering av klienter i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

 Configuration Manager stöder traditionella väcknings paket för att aktivera datorer i vilo läge när du vill installera nödvändig program vara, t. ex. program uppdateringar och program.

> [!NOTE]
> Den här artikeln beskriver hur en äldre version av Wake-on-LAN fungerar. Den här funktionen finns fortfarande i Configuration Manager version 1810, som även innehåller en nyare version av Wake on LAN. Båda versionerna av Wake on LAN kan, och i många fall, aktive ras samtidigt. Mer information om hur den nya versionen av Wake on LAN-funktioner som börjar på 1810 och aktiverar en eller båda versioner finns i [så här konfigurerar du Wake on LAN](../configure-wake-on-lan.md).  

## <a name="how-to-wake-up-clients-in-configuration-manager"></a>Aktivera klienter i Configuration Manager

 Configuration Manager stöder traditionella väcknings paket för att aktivera datorer i vilo läge när du vill installera nödvändig program vara, t. ex. program uppdateringar och program.  

Du kan komplettera den traditionella aktiverings paket metoden genom att använda klient inställningarna för aktiverings-proxy. Wake-up proxy använder ett peer-till-peer-protokoll och valda datorer för att kontrol lera om andra datorer i under nätet är aktiva och för att aktivera dem vid behov. När platsen har kon figurer ATS för Wake On LAN och klienter har kon figurer ATS för Wake-up-proxy, fungerar processen på följande sätt:  

1. Datorer med Configuration Manager-klienten installerad och som inte är i ström spar läge på under nätet kontrollerar om andra datorer i under nätet är aktiva. De utför den här kontrollen genom att skicka vart och ett av ping-kommandona för TCP/IP var femte sekund.  

2. Om det inte finns något svar från andra datorer antas de vara i ström spar läge. De datorer som är aktiva blir *Manager-datorer* för under nätet.  

    Eftersom det är möjligt att en dator inte svarar på grund av en annan orsak än den är i ström spar läge (till exempel om den är inaktive rad, tas bort från nätverket eller om inställningen för proxyns aktiverings klient inte längre tillämpas), skickas datorerna ett väcknings paket varje dag kl. klockan 17:00. lokal tid. Datorer som inte svarar kommer inte längre att anses vara ström spar läge och kommer inte att aktives av Wake-up proxy.  

    För att stödja Wake-up-proxy måste minst tre datorer vara aktiva för varje undernät. För att uppnå detta krav är tre datorer icke-deterministiskt valda för att vara *skyddare datorer* för under nätet. Det här läget innebär att de fortsätter att vara aktiva, trots eventuella konfigurerade energi principer på ström spar läge eller vilo läge efter en period av inaktivitet. Vårdnadshavare-datorer följer kommandon för avstängning eller omstart, till exempel som ett resultat av underhålls aktiviteter. Om den här åtgärden inträffar aktiverar de återstående skyddare datorerna en annan dator i under nätet så att under nätet fortfarande har tre vårdnadshavare-datorer.  

3. Manager-datorer ber nätverks växeln att omdirigera nätverks trafik för de vilande datorerna till sig själva.  

    Omdirigeringen uppnås av att Manager-datorn sänder en Ethernet-ram som använder datorns MAC-adress i vilo läge som käll adress. Det här beteendet gör att nätverks växeln fungerar som om den vilande datorn har flyttat till samma port som Manager-datorn. Manager-datorn skickar även ARP-paket för de vilande datorerna för att hålla posten färska i ARP-cachen. Manager-datorn svarar även på ARP-begäranden för den vilande datorns räkning och svarar med MAC-adressen för datorn i vilo läge.  

   > [!WARNING]  
   >  Under den här processen förblir IP-till-MAC-mappningen för den vilande datorn densamma. Wake-up proxy fungerar genom att informerar nätverks växeln som ett annat nätverkskort använder porten som har registrerats av ett annat nätverkskort. Detta är dock känt som en MAC-klaff och är ovanlig för standard-nätverks drift. Vissa verktyg för nätverks övervakning söker efter det här beteendet och kan anta att något är fel. Dessa övervaknings verktyg kan därför generera aviseringar eller stänga av portar när du använder Wake-up-proxy.  
   >   
   >  Använd inte Wake-up proxy om verktyg och tjänster för nätverks övervakning inte tillåter MAC-klaffar.  

4. När en Manager-dator ser en ny begäran om TCP-anslutning för en dator i vilo läge och begäran är till en port som den vilande datorn lyssnade på innan den gick i vilo läge, skickar Manager-datorn ett väcknings paket till den vilande datorn och stoppar sedan omdirigering av trafiken för den här datorn.  

5. Den vilande datorn tar emot väcknings paket och aktive ras. Den sändande datorn försöker ansluta automatiskt och den här gången, datorn är aktiv och kan svara.  

   Aktiverings-proxyn har följande krav och begränsningar:  

> [!IMPORTANT]  
>  Om du har ett separat team som ansvarar för nätverks infrastrukturen och nätverks tjänsterna, meddelar och inkluderar du det här teamet under utvärderings-och test perioden. Till exempel fungerar inte Wake-up proxy i ett nätverk som använder 802.1 X Network Access Control och kan störa nätverks tjänsten. Dessutom kan Väcknings proxy orsaka att vissa verktyg för nätverks övervakning genererar aviseringar när verktygen identifierar trafiken för att väcka andra datorer.  

-   Alla Windows-operativsystem som har stöd för klienter i [operativ system som stöds för klienter och enheter](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) stöds för Wake on LAN.  

-   Gäst operativ system som körs på en virtuell dator stöds inte.  

-   Klienter måste aktive ras för Wake-up-proxy med hjälp av klient inställningar. Även om aktivering av proxy inte är beroende av maskin varu inventeringen rapporterar inte klienterna installationen av tjänsten Wake-up proxy, om de inte är aktiverade för maskin varu inventering och har skickat minst en maskin varu inventering.  

-   Nätverkskort (och eventuellt BIOS) måste vara aktiverade och konfigurerade för väcknings paket. Om nätverkskortet inte har kon figurer ATS för väcknings paket eller om den här inställningen är inaktive rad konfigureras och aktive ras Configuration Manager automatiskt för en dator när den tar emot klient inställningen för aktivering av Väcknings-proxy.  

-   Om en dator har fler än ett nätverkskort kan du inte konfigurera vilket kort som ska användas för Wake-up proxy. valet är icke-deterministiskt. Det valda kortet registreras dock i SleepAgent_<s domän\> @SYSTEM_0.log fil.  

-   Nätverket måste tillåta ICMP-ekobegäran (minst inom under nätet). Det går inte att konfigurera det fem sekunders intervallet som används för att skicka ICMP Ping-kommandon.  

-   Kommunikationen är okrypterad och oautentiserad och IPsec stöds inte.  

-   Följande nätverkskonfigurationer stöds inte:  

    -   802.1 x med port-autentisering  

    -   Trådlösa nätverk  

    -   Nätverks växlar som binder MAC-adresser till vissa portar  

    -   Endast IPv6-nätverk  

    -   Varaktighet för DHCP-lån mindre än 24 timmar  

Om du vill aktivera datorer för schemalagd program varu installation måste du konfigurera varje primär plats att använda väcknings paket.  

 Om du vill använda Wake-up-proxy måste du distribuera klient inställningar för Power Management Wake-up-proxy förutom att konfigurera den primära platsen.  

Bestäm om du vill använda undernät-riktade broadcast-paket, eller unicast-paket och vilka UDP-portnummer som ska användas. Som standard överförs traditionella väcknings paket med hjälp av UDP-port 9, men för att öka säkerheten kan du välja en alternativ port för platsen om den här alternativa porten stöds av mellanliggande routrar och brand väggar.  

## <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>Välj mellan unicast och undernät-riktad sändning för Wake-on-LAN  
 Om du väljer att aktivera datorer genom att skicka traditionella väcknings paket, måste du bestämma om unicast-paket eller undernät-direkt sändnings paket ska överföras. Om du använder Wake-up-proxy måste du använda unicast-paket. Annars kan du använda följande tabell som hjälp för att avgöra vilken överförings metod du ska välja.  

|Överförings metod|Fördel|Nackdel|  
|-------------------------|---------------|------------------|  
|Läge|Mer säker lösning än undernät-dirigerad sändning eftersom paketet skickas direkt till en dator i stället för till alla datorer i ett undernät.<br /><br /> Kanske inte kräver omkonfiguration av routrar (du kanske måste konfigurera ARP-cachen).<br /><br /> Förbrukar mindre nätverks bandbredd än dirigerade broadcast-överföringar.<br /><br /> Stöds med IPv4 och IPv6.|Väcknings paket hittar inte mål datorer som har ändrat sin under näts adress efter det senaste maskin varu inventerings schemat.<br /><br /> Växlar kan behöva konfigureras för att vidarebefordra UDP-paket.<br /><br /> Vissa nätverkskort kanske inte svarar på väcknings paket i alla vilo lägen när de använder unicast som överförings metod.|  
|Undernät – riktad sändning|Högre frekvens än unicast om du har datorer som ofta ändrar sin IP-adress i samma undernät.<br /><br /> Ingen omkonfiguration av växlar krävs.<br /><br /> Hög kompatibilitet med dator kort för alla låg energi tillstånd, eftersom undernät-dirigerad sändning är den ursprungliga överförings metoden för att skicka väcknings paket.|Mindre säker lösning än att använda unicast eftersom en angripare kan skicka kontinuerliga strömmar av ICMP-ekobegäran från en förfalskad käll adress till den riktade broadcast-adressen. Detta gör att alla värdar svarar på den käll adressen. Om routrarna är konfigurerade för att tillåta undernät-dirigerad sändning, rekommenderas den ytterligare konfigurationen av säkerhets skäl:<br /><br /> -Konfigurera routrar så att de endast tillåter IP-dirigerad sändning från Configuration Manager plats Server, genom att använda ett angivet UDP-portnummer.<br />-Konfigurera Configuration Manager att använda det angivna port numret som inte är standard.<br /><br /> Kan kräva omkonfiguration av alla mellanliggande routrar för att aktivera undernät-dirigerad sändning.<br /><br /> Förbrukar mer nätverks bandbredd än unicast-överföring.<br /><br /> Stöds endast med IPv4; IPv6 stöds inte.|  

> [!WARNING]  
>  Det finns säkerhets risker kopplade till dirigerade broadcast-meddelanden: en angripare kan skicka kontinuerliga strömmar av Internet Control Message Protocol (ICMP) eko begär Anden från en förfalskad käll adress till den dirigerade broadcast-adressen, som gör att alla värdar svarar på den käll adressen. Den här typen av denial of service-attack kallas ofta en smurfangrepp-attack och minimeras vanligt vis genom att inte aktivera undernät-dirigerad sändning.
