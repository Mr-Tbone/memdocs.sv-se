---
title: Klient-peer-cache
titleSuffix: Configuration Manager
description: Använd klientens peer-cache för käll platser när du distribuerar innehåll med Configuration Manager.
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c302e839c2a41ba27d160db24928f7e202de78dc
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110193"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Peer-cache för Configuration Manager klienter

*Gäller för: Configuration Manager (aktuell gren)*

<!--1101436-->
Använd peer-cache för att hantera distribution av innehåll till klienter på fjärrplatser. Peer-cache är en inbyggd Configuration Manager-lösning som gör det möjligt för klienter att dela innehåll med andra klienter direkt från deras lokala cacheminne.   

> [!Note]  
> Configuration Manager aktiverar den här funktionen som standard i version 1906. I version 1902 eller tidigare aktiverar Configuration Manager inte den här valfria funktionen som standard. Du måste aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  



## <a name="overview"></a>Översikt

Definieras  

- **Peer-cache-klient**: alla Configuration Manager-klienter som laddar ned innehåll från en peer  

- **Källa för peer-cache**: en Configuration Manager-klient som du aktiverar för peer-cache och som har innehåll som ska delas med andra klienter  

Använd klient inställningar för att göra det möjligt för klienter att vara peer-cache-källor. Du behöver inte aktivera peer-cache-klienter. När du gör det möjligt för klienter att vara peer cache-källor, innehåller hanterings platsen dem i listan över innehålls plats källor.<!--510397--> Mer information om den här processen finns i [åtgärder](#operations).  

En peer-cache-källa måste vara medlem i den aktuella gränser-gruppen för peer-cache-klienten. Hanterings platsen omfattar inte peer-cache-källor från en intilliggande avgränsnings grupp i listan med innehålls källor som den tillhandahåller klienten. Den omfattar bara distributions platser från en intilliggande avgränsnings grupp. Mer information om aktuella och intilliggande avgränsnings grupper finns i [gränser grupper](../../servers/deploy/configure/boundary-groups.md).<!--SCCMDocs issue 685-->  

Configuration Manager klienten använder peer-cache för att betjäna andra klienter varje typ av innehåll i cacheminnet. Det här innehållet innehåller Microsoft 365 appar för företags-och installationsfiler.<!--SMS.500850-->  

Peer-cache ersätter inte användningen av andra lösningar som Windows BranchCache eller leverans optimering. Peer-cache fungerar tillsammans med andra lösningar. Dessa tekniker ger dig fler alternativ för att utöka traditionella innehålls distributions lösningar som distributions platser. Peer-cache är en anpassad lösning som inte är beroende av BranchCache. Om du inte aktiverar eller använder BranchCache fungerar peer-cache fortfarande.  

> [!Note]  
> Från och med version 1802 är Windows BranchCache alltid aktiverat vid distributioner. Inställningen för att **tillåta att klienter delar innehåll med andra klienter i samma undernät** tas bort.<!--SCCMDocs issue 539--> Om distributions platsen har stöd för den, och den är aktive rad i klient inställningarna, använder klienterna BranchCache. Mer information finns i [Konfigurera BranchCache](../../clients/deploy/about-client-settings.md#configure-branchcache).<!--SCCMDocs issue 735-->   



## <a name="operations"></a>Åtgärder

Om du vill aktivera peer-cache distribuerar du [klient inställningarna](#bkmk_settings) till en samling. Medlemmar i den samlingen fungerar sedan som en peer-cache-källa för andra klienter i samma avgränsnings grupp.  

- En klient som fungerar som en peer-innehålls källa skickar en lista över tillgängligt cachelagrat innehåll till hanterings platsen med tillstånds meddelanden.

   > [!NOTE]
   > Se [tillstånds meddelanden i Configuration Manager](state-messaging-system-center-configuration-manager.md#7200-state_topictype_super_peer_update_cache_map) för listan över tillämpliga peer-innehålls tillstånds meddelanden specifcally de med status meddelande-ID: n 7200, 7201, 7202 och 7203.

- En annan klient i samma avgränsnings grupp gör en begäran om innehålls plats till hanterings platsen. Servern returnerar listan över potentiella innehålls källor. Den här listan innehåller varje peer-cache-källa som innehåller innehållet och är online. Den innehåller även distributions platser och andra platser för innehålls källor i den aktuella gränser gruppen. Mer information finns i [innehålls källans prioritet](fundamental-concepts-for-content-management.md#content-source-priority).  

- Som vanligt väljer den klient som söker innehållet en källa från den angivna listan. Klienten försöker sedan hämta innehållet.  

Från och med version 1806 innehåller gränser grupper ytterligare inställningar för att ge dig mer kontroll över innehålls distribution i din miljö. Mer information finns i [gränser grupp alternativ för peer-nedladdningar](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).<!--1356193-->

> [!NOTE]  
> Om klienten går tillbaka till en intilliggande gränser grupp för innehåll, lägger hanterings platsen inte till peer-cache-källor från intilliggande gränser grupp till listan över potentiella innehålls käll platser.  

Välj endast de klienter som är bäst lämpade som peer cache-källor. Utvärdera klientens lämplighet baserat på attribut som chassi typ, disk utrymme och nätverks anslutning. Mer information som kan hjälpa dig att välja de bästa klienterna som ska användas för peer-cache finns i [den här bloggen av en Microsoft-konsult](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/configuration-manager-peer-cache-custom-reporting-examples/ba-p/570801).


### <a name="limited-access-to-a-peer-cache-source"></a>Begränsad åtkomst till en peer-cache-källa  

En peer-cache-källa avvisar begär Anden om innehåll när det uppfyller något av följande villkor vid den tidpunkt då en peer begär innehåll:  

- Läge för låg batteri nivå  

- Processor belastningen överskrider 80%  

- Disk-I/O har en *AvgDiskQueueLength* som överstiger 10  

- Det finns inga fler tillgängliga anslutningar till datorn  

> [!Tip]  
> Konfigurera de här inställningarna med hjälp av klient konfigurations serverns WMI-klass för funktionen peer-källa (*SMS_WinPEPeerCacheConfig*) i Configuration Manager SDK.  

När peer-cachens källa avvisar en begäran om innehållet fortsätter peer-cache-klienten att söka efter innehåll från listan med innehålls käll platser.   



## <a name="requirements"></a>Krav

- Peer-cache har stöd för alla Windows-versioner som listas som stöd i [operativ system som stöds för klienter och enheter](../configs/supported-operating-systems-for-clients-and-devices.md). Operativ system som inte är Windows-operativsystem stöds inte som peer-cache-källor eller peer-cache-klienter.  

- En peer-cache-källa måste vara en domänansluten Configuration Manager-klient. En klient som inte är domänansluten kan dock hämta innehåll från en domänansluten peer-cache-källa.  

- Klienter kan bara hämta innehåll från peer cache-källor i den aktuella gränser gruppen.  

- Ett [konto för nätverks åtkomst](accounts.md#network-access-account) krävs inte med följande undantag:  

  - Konfigurera ett konto för nätverks åtkomst på platsen när en peer-cache-aktiverad klient kör en aktivitetssekvens från Software Center och startar om till en start avbildning. När enheten är i Windows PE används nätverks åtkomst kontot för att hämta innehåll från peer-cachens källa.  

  - Vid behov använder peer-cache-källan nätverks åtkomst kontot för att autentisera hämtnings begär Anden från peer-datorer. Det här kontot kräver bara domän användar behörigheter för det här ändamålet.  

- Med version 1802 och tidigare fastställer klientens senaste pulsslags identifierings överföring den aktuella gränserna för en peer-cache-källa. En klient som växlar till en annan avgränsnings grupp kan fortfarande vara medlem i sin tidigare gränser grupp för peer-cache. Detta innebär att en klient erbjuds en peer-cache-källa som inte finns på den omedelbara nätverks platsen. Aktivera inte centrala klienter som en peer-cache-källa.<!--SCCMDocs issue 641-->  

  > [!Important]  
  > Från och med version 1806 är Configuration Manager mer effektivt vid bestämmande av om en peer-cache-källa har roamat till en annan plats. Det här beteendet ser till att hanterings platsen erbjuder den som en innehålls källa till klienter på den nya platsen och inte på den gamla platsen. Om du använder funktionen peer-cache med centrala peer-cache-källor, efter att ha uppdaterat platsen till version 1806, uppdaterar du även alla peer-cache-källor till den senaste klient versionen. Hanterings platsen omfattar inte dessa peer cache-källor i listan över innehålls platser förrän de har uppdaterats till minst version 1806.<!--SCCMDocs issue 850-->  

- Innan du försöker ladda ned innehåll, verifierar hanterings platsen först att peer-cachens källa är online.<!--sms.498675--> Den här verifieringen sker via "snabb kanal" för klient meddelanden, som använder TCP-port 10123.<!--511673-->  

> [!Note]  
> Om du vill dra nytta av nya Configuration Manager funktioner måste du först uppdatera klienter till den senaste versionen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.  



## <a name="peer-cache-client-settings"></a><a name="bkmk_settings"></a>Klient inställningar för peer-cache

Mer information om klient inställningarna för peer-cache finns i [Inställningar för klient-cache](../../clients/deploy/about-client-settings.md#client-cache-settings). 

Mer information om hur du konfigurerar dessa inställningar finns i [Konfigurera klient inställningar](../../clients/deploy/configure-client-settings.md).

På peer-cache-aktiverade klienter som använder Windows-brandväggen konfigurerar Configuration Manager de brand Väggs portar som du anger i klient inställningarna.



## <a name="partial-download-support"></a><a name="bkmk_parts"></a>Stöd för delvis hämtning
<!--1357346-->
Från och med version 1806 kan klient-peer cache-källor nu dela upp innehåll i delar. Dessa delar minimerar nätverks överföringen för att minska WAN-användningen. Hanterings platsen ger en mer detaljerad spårning av innehålls delarna. Det försöker eliminera mer än en hämtning av samma innehåll per gränser grupp. 


### <a name="example-scenario"></a>Exempelscenario

Contoso har en enda primär plats med två gränser grupper: huvud kontor (HQ) och avdelnings kontor. Det finns en 30-minuters återställnings relation mellan gränser grupperna. Hanterings platsen och distributions platsen för platsen finns bara i HQ-gränser. Avdelnings kontorets plats har ingen lokal distributions plats. Två av de fyra klienterna på avdelnings kontoret är konfigurerade som peer-cache-källor. 

![Diagram över nätverks konfiguration enligt beskrivningen i exempel scenariot](media/1357346-peer-cache-source-parts.png)

1. Du riktar en distribution till innehåll till alla fyra klienter på avdelnings kontoret. Du distribuerar bara innehållet till distributions platsen.  

2. Client3 och Client4 har ingen lokal källa för distributionen. Hanterings platsen instruerar klienterna att vänta 30 minuter innan de återgår till den fjärranslutna avgränsnings gruppen.  

3. KLIENT1 (PCS1) är den första peer-cache-källan för att uppdatera principen med hanterings platsen. Eftersom den här klienten är aktive rad som en peer cache-källa instruerar hanterings platsen att den omedelbart börjar hämta del A från distributions platsen.  

4. När KLIENT2 (PCS2) kontaktar hanterings platsen, som del A redan pågår men inte har slutförts, instruerar hanterings platsen att den omedelbart börjar ladda ned del B från distributions platsen.  

5. PCS1 har slutfört hämtningen av del A, och meddelar genast hanterings platsen. Eftersom del B redan pågår men inte har slutförts instruerar hanterings platsen att den börjar ladda ned del C från distributions platsen.  

6. PCS2 har slutfört nedladdning av del B och meddelar genast hanterings platsen. Hanterings platsen instruerar den att börja ladda ned del D från distributions platsen.  

7. PCS1 har slutfört nedladdning av del C och meddelar genast hanterings platsen. Hanterings platsen informerar om att det inte finns några fler tillgängliga delar från den fjärranslutna distributions platsen. Hanterings platsen instruerar den att ladda ned del B från dess lokala peer, PCS2.  

8. Den här processen fortsätter tills både klientens peer-cache-källor har alla delar från varandra. Hanterings platsen prioriterar delar från den fjärranslutna distributions platsen innan de instruerar peer-cachens källor för att ladda ned delar från lokala peer-datorer.  

9. Client3 är den första att uppdatera principen när återställnings perioden på 30 minuter upphör att gälla. Nu kontrol leras den igen med hanterings platsen, vilket informerar klienten om nya lokala källor. I stället för att ladda ned innehållet fullständigt från distributions platsen i WAN-nätverket laddar den ned innehållet från en av klientens peer-cache-källor. Klienter prioriterar lokala peer-källor. 

> [!Note]  
> Om antalet klient-peer cache-källor är större än antalet innehålls delar, instruerar hanterings platsen ytterligare peer cache-källor för att vänta på återställning som en normal klient. 


### <a name="configure-partial-download"></a>Konfigurera delvis hämtning

1. Konfigurera [gränser grupper](../../servers/deploy/configure/boundary-groups.md) och peer-cache-källor per normal.  

2. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj **platser**. Klicka på **Inställningar för hierarki** i menyfliksområdet.  

3. På fliken **Allmänt** aktiverar du alternativet för att **Konfigurera klientens peer-cache-källor för att dela upp innehåll i delar**.  

4. Skapa en nödvändig distribution med innehåll.  

   > [!Note]  
   > Den här funktionen fungerar bara när klienten laddar ned innehåll i bakgrunden, till exempel med en nödvändig distribution. Hämtningar på begäran, till exempel när användaren installerar en tillgänglig distribution i Software Center, fungerar som vanligt.  

Om du vill se vilka som hanterar nedladdningen av innehåll i delar, granskar du **ContentTransferManager. log** på klientens peer-cache-källa och **MP_Location. log** på hanterings platsen.  



## <a name="guidance-for-cache-management"></a>Vägledning för hantering av cache
<!--510645-->
Peer-cache förlitar sig på Configuration Manager klientcachen för att dela innehåll. Tänk på följande när du hanterar klientens cacheminne i din miljö:  

- Configuration Manager-klientcachen liknar innehålls biblioteket på en distributions plats. När du hanterar det innehåll som du distribuerar till en distributions plats hanterar den Configuration Manager klienten automatiskt innehållet i cacheminnet. Det finns inställningar och metoder som hjälper dig att kontrol lera vilket innehåll som finns i cacheminnet för en peer-cache-källa. Mer information finns i [Konfigurera klientens cacheminne för Configuration Manager klienter](../../clients/manage/manage-clients.md#BKMK_ClientCache).  

- Normal cache-storlek och underhåll gäller för peer-cache-källor. Mer information finns i [Konfigurera cache-storlek för klienter](../../clients/deploy/about-client-settings.md#configure-client-cache-size). Överväg storleken på större innehåll, t. ex. operativ system uppgraderings paket eller Windows 10 Express-uppdateringsfiler. Jämför ditt behov av det här innehållet mot tillgängligt disk utrymme på peer-cache-källor.  

- Klienten för peer-cache-källa uppdaterar den senaste refererade tiden för innehållet i cachen när en peer laddar ned den. Klienten använder den här tidsstämpeln när den automatiskt behåller sin cache, tar bort gammalt innehåll först. Därför bör det dröja att ta bort innehåll som peer-cache-klienter ofta laddar ned.  

- Om det behövs kan du använda variabeln **SMSTSPreserveContent** för att behålla innehållet i klientcachen under en aktivitetssekvens för operativ system distribution. Mer information finns i [variabler för aktivitetssekvens](../../../osd/understand/task-sequence-variables.md#SMSTSPreserveContent).  

- Om det behövs kan du använda alternativet för att **bevara innehåll i klientcachen**när du skapar följande program vara:  
  - Program
  - Paket
  - Operativsystemavbildningar
  - Uppgraderings paket för operativ system
  - Startavbildningar



## <a name="monitoring"></a>Övervakning   

Du kan hjälpa dig att förstå användningen av peer-cache genom att visa instrument panelen för **klient data källor** . Mer information finns i [instrument panelen för klient data källor](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

Använd även rapporter för att visa användning av peer-cache. I-konsolen går du till arbets ytan **övervakning** , expanderar **rapportering**och väljer noden **rapporter** . Följande rapporter har en typ av innehåll för **program varu distribution**:  

1.  **Avvisning av käll innehåll i peer-cache**: hur ofta peer cache-källor i en begränsande grupp avvisar en innehålls förfrågan.  

    > [!Note]  
    > **Känt problem**<!--486652-->: Vid ökad detalj nivå i resultat som *MaxCPULoad* eller *MaxDiskIO*kan det hända att du får ett fel meddelande om att rapporten eller informationen inte kan hittas. Undvik det här problemet genom att använda de andra två rapporterna som visar resultaten direkt.  

2. **Avvisning av käll innehåll i peer-cache efter villkor**: visar avvisnings information för en angiven avgränsnings grupp eller avvisande typ. 

    > [!Note]  
    > **Känt problem**<!--486652-->: Du kan inte välja från tillgängliga parametrar och måste i stället ange dem manuellt. Ange värdena för namn och *avvisnings typ* för *avgränsnings grupp* enligt vad som visas i **innehålls avvisnings** rapporten för peer-cache. För *avvisnings typ* kan du till exempel ange *MaxCPULoad* eller *MaxDiskIO*.  

3. **Information om avvisning av käll innehåll i peer-cache**: Visa innehållet som klienten begärde när den avvisades.  

    > [!Note]  
    > **Känt problem**<!--486652-->: Du kan inte välja från tillgängliga parametrar och måste i stället ange dem manuellt. Ange värdet för *avvisnings typ* som visas i **innehålls avvisnings** rapporten för peer-cache. Ange sedan *resurs-ID* för innehålls källan som du vill ha mer information om. 
    > 
    > Så här hittar du resurs-ID för innehålls källan:  
    > 
    > 1. Hitta det dator namn som visas som *peer-cache-källa* i resultatet av rapporten **innehåll för avvisning av peer-cache-källa enligt villkor** .  
    > 
    > 2. Gå till arbets ytan **till gångar och efterlevnad** , välj noden **enheter** och Sök efter datorns namn. Använd värdet från kolumnen resurs-ID.  

