---
title: Konfigurera gränser grupper
titleSuffix: Configuration Manager
description: Hjälp klienter att hitta plats system genom att använda gräns grupper för att logiskt organisera relaterade nätverks platser som kallas gränser
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7a925c29b5d186f3ca6f320741f5ca602b0bbb79
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128400"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>Konfigurera gränser grupper för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd gräns grupper i Configuration Manager för att logiskt organisera relaterade nätverks platser ([gränser](boundaries.md)) för att göra det enklare att hantera infrastrukturen. Tilldela gränser till gräns grupper innan du använder gräns gruppen.

Som standard skapar Configuration Manager en standard webbplats gränser på varje plats.

Om du vill konfigurera gräns grupper, associera gränser (nätverks platser) och plats system roller, t. ex. distributions platser, till gräns gruppen. Den här konfigurationen hjälper till att koppla klienter till plats system servrar som distributions platser som finns nära klienterna i nätverket.

För att öka tillgängligheten för servrar till en större mängd nätverks platser, tilldelar du samma begränsning och samma server till fler än en begränsnings grupp.

Klienter använder en avgränsnings grupp för:  

- Automatisk platstilldelning  
- Hitta en plats system server som kan tillhandahålla en tjänst, inklusive:

  - Distributions platser för innehålls plats  
  - Program uppdaterings platser  
  - Platser för tillståndsmigrering  

    > [!NOTE]
    > Platsen för tillståndsmigrering använder inte återställnings relationer. Mer information finns i [fallback](#fallback).

  - Prioriterade hanterings platser  

    > [!NOTE]  
    > Om du använder önskade hanterings platser aktiverar du det här alternativet för hierarkin, inte från gränser grupp konfigurationen. Mer information finns i [Aktivera användning av prioriterade hanterings platser](boundary-group-procedures.md#bkmk_proc-prefer).  

  - Cloud Management Gateway (från och med version 1902)

## <a name="boundary-groups-and-relationships"></a>Gränser grupper och relationer

För varje avgränsnings grupp i hierarkin kan du tilldela:

- En eller flera gränser. En klients **aktuella** gräns grupp är en nätverks plats som definieras som en gräns som tilldelas till en viss gräns grupp. En klient kan ha mer än en aktuell avgränsnings grupp.  

- En eller flera plats system roller. Klienter kan alltid använda roller som är associerade med den aktuella gränser gruppen. Beroende på ytterligare konfigurationer kan de använda roller i ytterligare avgränsnings grupper.  

För varje avgränsnings grupp som du skapar kan du konfigurera en enkelriktad länk till en annan avgränsnings grupp. Länken kallas för en **relation**. De gränser grupper som du länkar till kallas **intilliggande** avgränsnings grupper. En avgränsnings grupp kan ha mer än en relation, var och en med en angiven intilliggande avgränsnings grupp.

När en klient inte kan hitta ett tillgängligt plats system i den aktuella gräns gruppen, avgör konfigurationen för varje relation när den börjar söka efter en intilliggande gräns grupp. Den här sökningen av ytterligare grupper kallas **reserv**.

Mer information finns i följande procedurer:  

- [Skapa en avgränsnings grupp](boundary-group-procedures.md#bkmk_create)  
- [Konfigurera en avgränsnings grupp](boundary-group-procedures.md#bkmk_config)  

### <a name="show-boundary-groups-for-devices"></a><a name="bkmk_show-boundary"></a>Visa gränser grupper för enheter

<!--6521835-->

Från och med version 2002, för att hjälpa dig att bättre identifiera och felsöka enhets beteenden med gränser grupper, kan du Visa gränserna för vissa enheter. I noden **enheter** eller när du visar medlemmar i en **enhets samling**lägger du till kolumnen ny **gränser grupp (er)** i listvyn.

- Om en enhet finns i fler än en gräns grupp är värdet en kommaavgränsad lista över namn på gräns grupper.

- Data uppdateras när klienten gör en plats förfrågan till platsen, eller högst var 24: e timme.

- Om en klient är nätverks växling och inte är medlem i en gränser grupp är värdet tomt.

> [!NOTE]
> Den här informationen är plats data och endast tillgänglig på primära platser. Du ser inte något värde för den här kolumnen när du ansluter Configuration Manager till en central administrations plats.

## <a name="fallback"></a>Återställning

För att förhindra problem när klienter inte kan hitta ett tillgängligt plats system i den aktuella gränser gruppen definierar du relationen mellan gränser grupper för återställnings beteende. Reserv låter en klient utöka sin sökning till ytterligare avgränsnings grupper för att hitta ett tillgängligt plats system.

Relationerna konfigureras på en flik för **relationer** av gränser-grupp. När du konfigurerar en relation definierar du en länk till en intilliggande avgränsnings grupp. Konfigurera oberoende inställningar för återställning till intilliggande gränser grupp för varje typ av plats system roll som stöds. Mer information finns i [Konfigurera återställnings beteende](boundary-group-procedures.md#bkmk_bg-fallback).

Om du till exempel konfigurerar en relation till en angiven avgränsnings grupp, ställer du in återställning för distributions platser efter 20 minuter. Standardvärdet är 120 minuter för ett mer omfattande exempel, se [exempel på användning av gränser grupper](#example-of-using-boundary-groups).

Om en klient inte kan hitta en tillgänglig plats system roll i den aktuella gräns gruppen använder klienten återställnings tiden i minuter. Den här återställnings tiden avgör när klienten börjar söka efter ett tillgängligt plats system som är associerat med intilliggande gräns gruppen.  

När en klient inte kan hitta ett tillgängligt plats system börjar den söka efter platser från intilliggande gränser grupper. Det här beteendet ökar poolen med tillgängliga plats system. Konfigurationen av gränser grupper och deras relationer definierar klientens användning av den här poolen av tillgängliga plats system.

- En avgränsnings grupp kan ha mer än en relation. Med den här konfigurationen kan du konfigurera återställningen för varje typ av plats system till olika grannar som ska inträffa efter olika tids perioder.  

- Klienterna går bara tillbaka till en begränsande grupp som är direkt grann för den aktuella gränser gruppen.  

- När en klient är medlem i mer än en avgränsnings grupp definierar den den aktuella gränsen grupp som en union av alla dess gränser grupper. Klienten går tillbaka till grannar i någon av de ursprungliga gränserna.  

> [!NOTE]
> Plats rollen tillståndsmigrering använder inte återställnings relationer. Om du lägger till både tillståndsmigrering och distributions plats roller på samma plats system server konfigurerar du inte återställningen för dess gränser grupp. Om du behöver använda återställning av gränser grupper för distributions platsen lägger du till rollen plats för tillståndsmigrering på en annan plats system Server.<!-- 2838807 -->

### <a name="the-default-site-boundary-group"></a>Standard platsens gränser grupp

Du kan skapa egna gränser grupper, och varje plats har en standard plats för webbplats gränser som Configuration Manager skapar. Den här gruppen heter **standard-site-bounds-Group &lt; platskod>**. Gruppen för plats ABC skulle till exempel heta **default-site-Enbounds Group &lt; ABC>**.

För varje avgränsnings grupp som du skapar skapar Configuration Manager automatiskt en underförstådd länk till varje standard plats gränser grupp i hierarkin.  

- Den underförstådda länken är ett standard återställnings alternativ från en aktuell avgränsnings grupp till platsens standard gränser grupp. Standard återställnings tiden är 120 minuter.  

- För klienter som inte finns i en gränser som är kopplad till någon avgränsnings grupp: om du vill identifiera giltiga plats system roller använder du standard plats gränser från deras tilldelade plats.  

Så här hanterar du återställningen till standard platsens gränser grupp:  

- Öppna egenskaperna för platsens standard gränser grupp och ändra värdena på fliken **standard beteende** . ändringar som du gör här gäller för *alla* underförstådda länkar till den här gränser gruppen. När du konfigurerar en explicit länk till den här standard platsens gränser-grupp från en annan gränser grupp, åsidosätter du standardinställningarna.  

- Öppna egenskaperna för en anpassad avgränsnings grupp. Ändra värdena för den explicita länken till en standard plats för webbplats gränser. När du anger en ny tid i minuter för återställnings-eller blockerad återställning påverkar ändringen bara den länk som du konfigurerar. Konfigurationen av den explicita länken åsidosätter inställningarna på fliken **standard beteende** i en standard plats för webbplats gränser.  

## <a name="site-assignment"></a>Platstilldelning  

Du kan konfigurera varje gränsgrupp med en tilldelad plats för klienter.  

- En nyinstallerad klient som använder automatisk platstilldelning ansluter till den tilldelade platsen för en begränsande grupp som innehåller klientens aktuella nätverks plats.  

- När du har tilldelat en plats ändrar inte en klient sin platstilldelning när den ändrar sin nätverks plats. Till exempel en klient växlar till en ny nätverks plats. Den här platsen är en kant linje i en avgränsnings grupp med en annan platstilldelning. Klientens tilldelade plats ändras inte.  

- När Active Directory system identifieringen identifierar en ny resurs, utvärderar platsen nätverks information för resursen mot gränserna i gräns grupper. I processen associeras den nya resursen med en tilldelad plats genom metoden för klient-push-installation.  

- När en gränser är medlem i mer än en avgränsnings grupp som har olika tilldelade platser, väljer klienter slumpmässigt en av platserna.  

- Ändringar av en tilldelad plats för gränser gäller endast nya platstilldelning. Klienter som tidigare har tilldelats en plats utvärderar inte sin platstilldelning baserat på ändringar i konfigurationen av en avgränsnings grupp (eller till sin egen nätverks plats).  

Mer information om tilldelning av klient platser finns i [använda automatisk platstilldelning för datorer](../../../clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment).  

Mer information om hur du konfigurerar platstilldelning finns i följande procedurer:

- [Konfigurera platstilldelning och välj plats system servrar](boundary-group-procedures.md#bkmk_references)
- [Konfigurera en återställnings plats för automatisk platstilldelning](boundary-group-procedures.md#bkmk_site-fallback)

## <a name="distribution-points"></a>Distributionsplatser

När en klient begär platsen för en distributions plats, Configuration Manager skickar klienten en lista över plats system. Dessa plats system är av lämplig typ som är kopplad till varje avgränsnings grupp som innehåller klientens aktuella nätverks plats:

- **Under program varu distributionen**begär klienterna en plats för distributions innehåll på en giltig innehålls källa. Den här platsen kan vara en distributions plats eller en källa för peer-cache.  

- **Under operativ Systems distributionen**begär klienterna en plats för att skicka eller ta emot information om tillståndsmigrering.  

  - Klienter hämtar innehåll baserat på gränser för gränser grupper. Mer information finns i [stöd för aktivitetssekvenser för gränser grupper](#bkmk_bgr-osd).  

Om en klient begär innehåll som inte är tillgängligt från en källa i den aktuella gränsens grupp under innehålls distribution, fortsätter klienten att begära det innehållet. Klienten försöker med olika innehålls källor i den aktuella gränsen grupp tills den når reserv perioden för en granne eller standard plats gränsen. Om klienten fortfarande inte har hittat innehåll, expanderar den sin sökning efter innehålls källor för att inkludera intilliggande gränser grupper.

Om du konfigurerar innehållet för att distribuera på begäran och det inte är tillgängligt på en distributions plats när en klient begär det, börjar platsen överföra innehållet till distributions platsen. Det är möjligt att klienten hittar servern som en innehålls källa innan den återgår till att använda en intilliggande avgränsnings grupp.

### <a name="client-installation"></a><a name="bkmk_ccmsetup"></a>Klient installation

Installations programmet för Configuration Manager-klienten, CCMSetup, kan hämta installations innehåll från en lokal källa eller via en hanterings plats. Det ursprungliga beteendet beror på vilka kommando rads parametrar du använder för att installera klienten:<!-- MEMDocs#286 -->

- Om du inte använder någon av **/MP** -eller **/Source** -parametrarna försöker CCMSetup hämta en lista över hanterings platser från Active Directory eller DNS.
- Om du bara anger **/Source**tvingar den installationen från den angivna sökvägen. Det identifierar inte hanterings platser. Om det inte går att hitta ccmsetup.cab på den angivna sökvägen, Miss lyckas CCMSetup.
- Om du anger både **/MP** och **/Source**kontrol leras de angivna hanterings platserna och de identifieras. Om den inte kan hitta en giltig hanterings plats går den tillbaka till den angivna käll Sök vägen.

Mer information om de här CCMSetup-parametrarna finns i [parametrar och egenskaper för klient installation](../../../clients/deploy/about-client-installation-properties.md).

<!--1358840-->
När CCMSetup kontaktar hanterings platsen för att hitta det nödvändiga innehållet, returnerar hanterings platsen distributions platser baserat på konfiguration av gränser grupper. Om du definierar relationer för den begränsade gruppen returnerar hanterings platsen distributions platser i följande ordning:

1. Aktuell avgränsnings grupp  
2. Intilliggande gränser grupper  
3. Platsens standard gränser grupp  

> [!Note]  
> Klient installations processen använder inte återställnings tiden. För att hitta innehåll så snabbt som möjligt går det omedelbart tillbaka till nästa avgränsnings grupp.
>
> I tidigare versioner av Configuration Manager, under den här processen, returnerade hanterings platsen endast distributions platser i klientens aktuella gränser grupp. Om inget innehåll var tillgängligt, sjönk installations processen tillbaka för att ladda ned innehåll från hanterings platsen. Det fanns inget alternativ för att återgå till distributions platser i andra gränser grupper som kan ha nödvändigt innehåll.

### <a name="task-sequence-support-for-boundary-groups"></a><a name="bkmk_bgr-osd"></a>Stöd för aktivitetssekvens för gränser grupper

<!--1359025-->
När en enhet kör en aktivitetssekvens och behöver hämta innehåll, använder den gränser grupp beteenden som liknar Configuration Manager-klienten.

Konfigurera det här beteendet med följande inställningar på sidan **distributions platser** i distributionen av aktivitetssekvensen:

- **Om det inte finns någon lokal distributions plats använder du en fjärrdistributions plats**: för den här distributionen kan aktivitetssekvensen gå tillbaka till distributions platser i en intilliggande avgränsnings grupp.  

- **Tillåt att klienter använder distributions platser från standard plats begränsnings gruppen**: för den här distributionen kan aktivitetssekvensen gå tillbaka till distributions platser i standard plats begränsnings gruppen.  

Se till att uppdatera klienter till den senaste versionen om du vill använda det här nya beteendet.

#### <a name="location-priority"></a>Plats prioritet  

Aktivitetssekvensen försöker hämta innehåll i följande ordning:  

1. Peer-cache-källor  

2. Distributions platser i den *aktuella* gränser gruppen  

3. Distributions platser i en *intilliggande* gränser grupp  

    > [!Important]  
    > På grund av behandlingens natur i real tid väntar det ingen tid på att redundansväxla en intilliggande gräns grupp. Den använder växlings tiderna för att prioritera grupper med intilliggande gränser. Om aktivitetssekvensen till exempel inte kan hämta innehåll från en distributions plats i den aktuella gräns gruppen, försöker den genast med en distributions plats i en intilliggande gräns grupp med den kortaste redundansväxlingen. Om den processen Miss lyckas växlar den över till en distributions plats i en intilliggande gräns grupp med en större växlings tid.  

4. Distributions platser i *standard plats för plats*  

Logg filen **Smsts. log** i aktivitetssekvensen visar prioriteten för de plats källor som används baserat på distributions egenskaperna.

### <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a>Alternativ för gränser-grupp för peer-nedladdningar

<!--1356193, 1358749-->
Gränser grupper innehåller följande ytterligare inställningar för att ge dig mer kontroll över innehålls distribution i din miljö:  

- [Tillåt nedladdning av peer-datorer i den här begränsnings gruppen](#bkmk_bgoptions1)  

- [Använd endast peer-datorer i samma undernät vid peer-hämtning](#bkmk_bgoptions2)  

- [Föredra distributions platser över peer-datorer med samma undernät](#bkmk_bgoptions3)  

- [Föredra moln distributions platser över distributions platser](#bkmk_bgoptions4)  

Mer information om hur du konfigurerar dessa inställningar finns i [Konfigurera en avgränsnings grupp](boundary-group-procedures.md#bkmk_config).

Om en enhet finns i fler än en avgränsnings grupp gäller följande beteenden för dessa inställningar:

- **Tillåt peer-hämtning i den här begränsnings gruppen**: om den är inaktive rad i en begränsnings grupp använder klienten inte leverans optimering.
- **Använd endast peer-datorer med samma undernät under en peer-hämtning**: om den är aktive rad i någon av gränserna grupper börjar den här inställningen gälla.
- **Föredra distributions platser över peer-datorer inom samma undernät**: om den är aktive rad i någon av en avgränsnings grupp gäller den här inställningen.
- **Föredra molnbaserade källor över lokala källor**: om den är aktive rad i någon av en avgränsnings grupp gäller den här inställningen.

#### <a name="allow-peer-downloads-in-this-boundary-group"></a><a name="bkmk_bgoptions1"></a>Tillåt nedladdning av peer-datorer i den här begränsnings gruppen

Den här inställningen är aktiverad som standard. Hanterings platsen ger klienterna en lista över innehålls platser som innehåller peer-källor. Den här inställningen påverkar också användning av grupp-ID: n för [leverans optimering](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).  

Det finns två vanliga scenarier där du bör inaktivera det här alternativet:  

- Om du har en gräns grupp som innehåller gränser från geografiskt spridda platser, till exempel en VPN. Två klienter kan finnas i samma avgränsnings grupp eftersom de är anslutna via VPN, men i stora olika platser som inte är olämpliga för peer-delning av innehåll.  

- Om du använder en enda, stor begränsar grupp för platstilldelning som inte refererar till några distributions platser.  

> [!IMPORTANT]
> Om en enhet finns i fler än en avgränsnings grupp, se till att aktivera den här inställningen på alla gränser grupper för enheten. Annars använder klienten inte leverans optimering. Den anger till exempel inte register nyckeln DOGroupID.

#### <a name="during-peer-downloads-only-use-peers-within-the-same-subnet"></a><a name="bkmk_bgoptions2"></a>Använd endast peer-datorer i samma undernät vid peer-hämtning

Den här inställningen beror på föregående alternativ. Om du aktiverar det här alternativet innehåller hanterings platsen bara den innehålls plats i listan med peer-källor som finns i samma undernät som klienten.

Vanliga scenarier för att aktivera det här alternativet:

- Din gränser grupp design för innehålls distribution innehåller en stor avgränsnings grupp som överlappar andra mindre gränser grupper. Med den här nya inställningen innehåller listan över innehålls källor som hanterings platsen tillhandahåller klienter endast peer-källor från samma undernät.

- Du har en enda stor avgränsnings grupp för alla fjärranslutna kontor. Aktivera det här alternativet och klienter delar bara innehåll inom under nätet på den fjärranslutna arbets platsen, i stället för att dela innehåll mellan platser.

Från och med version 2002 kan du undanta vissa undernät för matchning, beroende på nätverkets konfiguration. Du vill till exempel ta med en kant linje men undanta ett speciellt VPN-undernät. Som standard utesluter Configuration Manager standard-Teredo-undernätet ( `2001:0000:%` ).<!--3555777-->

> [!NOTE]
> När du i version 2002 [expanderar en fristående primär plats](../install/prerequisites-for-installing-sites.md#bkmk_expand) för att lägga till en central administrations plats (CAS), återställs undantags listan för under nätet till standardvärdet. Undvik det här problemet genom att köra PowerShell-skriptet efter plats expansionen för att anpassa undantags listan för under nätet på certifikat utfärdarna.<!-- 6309068 -->

Importera din undantags lista för undernät som en kommaavgränsad under näts sträng. Använd procent tecknet ( `%` ) som jokertecken. På plats servern på den översta nivån ställer du in eller läser egenskapen **SubnetExclusionList** embedded för **SMS_HIERARCHY_MANAGER** -komponenten i **SMS_SCI_Component** -klassen. Mer information finns i [SMS_SCI_Component Server WMI-klass](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md).

##### <a name="sample-powershell-script-to-update-the-subnet-exclusion-list"></a>Exempel på PowerShell-skript för att uppdatera undantags listan för under nätet

Följande skript är ett exempel på hur du kan ändra det här värdet. Lägg till dina undernät i variabeln **PropertyValue** efter `2001:0000:%,172.16.16.0` . Det är en semikolonavgränsad sträng. Kör det här skriptet på toppnivå plats servern i hierarkin.

```PowerShell
$PropertyValue = "2001:0000:%,172.16.16.0"
$PropertyName = "SubnetExclusionList"

$providerMachine = Get-WmiObject -Class "SMS_ProviderLocation" -Namespace "root\sms"

if ($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = Get-WmiObject -Query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_HIERARCHY_MANAGER"' -ComputerName $providerMachine.Machine -Namespace root\sms\site_$SiteCode
$properties = $component.props

Write-host "Updating property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -like $PropertyName)
  {
    Write-host "Current value for SubnetExclusionList is  " $property.value1
    $property.value1 = $PropertyValue
    Write-host "Updating value for SubnetExclusionList to " $property.value1
    break
  }
}

$component.props = $properties
$component.put()
```

> [!NOTE]
> Som standard innehåller Configuration Manager Teredo-undernätet i den här listan. När du ändrar listan ska du alltid läsa det befintliga värdet först. Lägg till ytterligare undernät i listan och ange sedan det nya värdet.

#### <a name="prefer-distribution-points-over-peers-with-the-same-subnet"></a><a name="bkmk_bgoptions3"></a>Föredra distributions platser över peer-datorer med samma undernät

Som standard prioriterar hanterings platsen peer cache-källor överst i listan med innehålls platser. Den här inställningen återför den prioriteten för klienter som finns i samma undernät som peer-cachens källa.

> [!TIP]
> Det här beteendet gäller för Configuration Manager-klienten. Den gäller inte när innehållet i aktivitetssekvensen laddas ned. När aktivitetssekvensen körs föredras peer cache-källor över distributions platser.<!-- SCCMDocs#1376 -->

#### <a name="prefer-cloud-distribution-points-over-distribution-points"></a><a name="bkmk_bgoptions4"></a>Föredra moln distributions platser över distributions platser

Om du har ett avdelnings kontor med en snabbare Internet-länk kan du nu prioritera moln innehåll.  

I version 1902 är den här inställningen nu med rubriken **prioriterade molnbaserade källor över lokala källor**. Molnbaserade källor omfattar följande:<!-- SCCMDocs#1529 -->

- Moln distributions platser
- Microsoft Update (lades till i version 1902)

## <a name="software-update-points"></a><a name="bkmk_sup"></a>Program uppdaterings platser 

Klienter använder gränser grupper för att hitta en ny program uppdaterings plats. Om du vill styra vilka servrar som en klient kan hitta lägger du till enskilda program uppdaterings platser i olika gränser grupper.

Om du lägger till alla befintliga program uppdaterings platser i standard platsens gränser grupp väljer klienten en program uppdaterings plats från poolen med tillgängliga servrar. Detta fungerar på samma sätt som tidigare versioner av Configuration Manager aktuella grenen. För kontrollerat val och reserv sätt kan du lägga till enskilda program uppdaterings platser i olika gränser grupper.

Om du installerar en ny plats läggs inte program uppdaterings platserna till i standard platsens gränser grupp. Tilldela program uppdaterings platser till en avgränsnings grupp så att klienterna kan hitta och använda dem.

### <a name="fallback-for-software-update-points"></a>Återställning av program uppdaterings platser

Återställning av program uppdaterings platser konfigureras som andra plats system roller, men har följande varningar:  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>Nya klienter använder gränser grupper för att välja program uppdaterings platser

När du installerar nya klienter väljer de en program uppdaterings plats från de servrar som är kopplade till de gränser grupper som du konfigurerar. Det här beteendet ersätter det tidigare beteendet där klienter väljer en program uppdaterings plats slumpmässigt från en lista över de servrar som delar klientens skog.

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>Klienterna fortsätter att använda en senast fungerande program uppdaterings plats tills de återgår till att hitta en ny

Klienter som redan har en program uppdaterings plats fortsätter att använda den tills den inte kan nås. Det här beteendet omfattar fortsatt användning av en program uppdaterings plats som inte är associerad med klientens aktuella gränser grupp.

Det här beteendet är avsiktligt. Klienten fortsätter att använda en befintlig program uppdaterings plats, även om den inte finns i klientens aktuella gränser grupp. När program uppdaterings platsen ändras synkroniserar klienten data med den nya servern, vilket orsakar en betydande nätverks användning. Om alla klienter växlar till en ny server samtidigt, hjälper fördröjningen i över gången att undvika nätverket överbelastas nätverket.

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>En klient försöker alltid komma åt sin senast fungerande program uppdaterings plats i 120 minuter innan återställningen påbörjas

Efter 120 minuter påbörjas återställningen om klienten inte har etablerat kontakten. När reserven startar får klienten en lista över alla program uppdaterings platser i dess aktuella gränser grupp. Ytterligare program uppdaterings platser i grann-och plats standard gränser grupper är tillgängliga utifrån reserv konfigurationerna.

### <a name="fallback-configurations-for-software-update-points"></a>Återställnings konfiguration för program uppdaterings platser

Du kan konfigurera **återställnings tider (i minuter)** för att program uppdaterings platser ska vara mindre än 120 minuter. Klienten försöker dock fortfarande att komma åt den ursprungliga program uppdaterings platsen i 120 minuter. Sedan utökas sökningen till ytterligare servrar. Gräns gruppens återställnings tider startar när klienten först inte når sin ursprungliga Server. När klienten utökar sin sökning tillhandahåller platsen alla gränser grupper som kon figurer ATS i mindre än 120 minuter.

Om du vill blockera återställning för en program uppdaterings plats till en intilliggande gränser grupp konfigurerar du inställningen så att den **aldrig**återställs.

När klienten inte har nått sin ursprungliga server i två timmar använder klienten en kortare cykel för att upprätta en anslutning till en ny program uppdaterings plats. Med det här beteendet kan klienten snabbt söka igenom den expanderande listan över potentiella program uppdaterings platser.

#### <a name="example"></a>Exempel

Du konfigurerar program uppdaterings platser i en gränser grupp *A* för återställning efter **10** minuter. Du konfigurerar samma inställning för gränser grupp *B* till **130** minuter. En klient i gräns gruppen *Z* kan inte komma åt sin senast fungerande program uppdaterings plats.

- Under de kommande 120 minuterna försöker klienten bara komma åt sin ursprungliga server i gränsens grupp Z. Efter 10 minuter lägger Configuration Manager till program uppdaterings platserna från gränser grupp A till poolen med tillgängliga servrar. Klienten försöker dock inte kontakta sig eller någon annan server förrän den första 120-minuters perioden har löpt ut.  

- När du försöker kontakta den ursprungliga program uppdaterings platsen i 120 minuter expanderar klienten sin sökning. Den lägger till servrar till den tillgängliga poolen med program uppdaterings platser som är aktuella och alla intilliggande gränser grupper som kon figurer ATS i 120 minuter eller mindre. Den här poolen innehåller servrarna i en gränser grupp A, som tidigare har lagts till i poolen med tillgängliga servrar.  

- Efter 10 minuter expanderar klienten sökningen till att omfatta program uppdaterings platser från gränser grupp B. Denna period är 130 minuter av den totala tiden efter det att klienten först inte kunde ansluta till den senast fungerande program uppdaterings platsen.  

### <a name="manually-switch-to-a-new-software-update-point"></a>Växla manuellt till en ny program uppdaterings plats

Tillsammans med reserv använder du klient meddelanden för att manuellt tvinga en enhet att växla till en ny program uppdaterings plats.

När du växlar till en ny server använder enheterna reserv för att hitta den nya servern. Klienter växlar till den nya program uppdaterings platsen under nästa genomsöknings cykel för program uppdateringar.<!-- SCCMDocs#1537 -->

Granska konfigurationerna för din gränser grupp. Innan du börjar den här ändringen kontrollerar du att program uppdaterings platserna finns i rätt gränser grupper.

Mer information finns i [Växla klienter manuellt till en ny program uppdaterings plats](../../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a><a name="bkmk_cmg-sup"></a>Intranät klienter kan använda en CMG program uppdaterings plats
<!--7102873-->
Från och med version 2006 kan intranät klienter komma åt en CMG program uppdaterings plats när den tilldelas en begränsnings grupp och [ **trafik alternativet Tillåt Configuration Manager Cloud Management Gateway** är aktiverat](../../../clients/manage/cmg/setup-cloud-management-gateway.md#bkmk_role) på program uppdaterings platsen. Du kan tillåta att intranät enheter genomsöker mot en CMG program uppdaterings plats i följande scenarier:

- När en Internet-dator ansluter till VPN-servern fortsätter den att söka mot CMG program uppdaterings plats via Internet.
- Om den enda program uppdaterings platsen för den begränsande gruppen är den CMG program uppdaterings platsen, kommer alla intranät-och Internet enheter att sökas mot den.

## <a name="management-points"></a>Hanterings platser

<!-- 1324594 -->
Konfigurera återställnings relationer för hanterings platser mellan gränser grupper. Det här beteendet ger större kontroll för de hanterings platser som klienterna använder. På fliken **relationer** i egenskaperna för gränser-gruppen finns det en kolumn för hanterings platsen. När du lägger till en ny återställnings gräns grupp är återställnings tiden för hanterings platsen för närvarande alltid noll (0). Det här beteendet är detsamma för **standard beteendet** på platsens standard gränser grupp.

Tidigare uppstod ett vanligt problem när du hade en skyddad hanterings plats i ett säkert nätverk. Klienter i huvud nätverket tog emot en princip som inkluderade denna skyddade hanterings plats, trots att de inte kunde kommunicera med den via en brand vägg. För att åtgärda det här problemet nu, använder du alternativet **aldrig återställning** för att se till att klienterna bara är tillbaka till hanterings platser som de kan kommunicera med.

> [!Note]  
> Om du aktiverar distributions platser i standard plats för platser som ska återanvändas och en hanterings plats samplaceras på en distributions plats lägger platsen också till den hanterings platsen i platsens standard gränser grupp.<!--VSO 2841292-->  

Om en klient finns i en avgränsnings grupp som inte har någon tilldelad hanterings plats, ger platsen klienten hela listan över hanterings platser. Det här beteendet ser till att en klient alltid får en lista över hanterings platser.

Återställningen av hanterings platsens gränser påverkar inte funktions sättet under klient installationen (ccmsetup.exe). Om kommando raden inte anger den första hanterings platsen med hjälp av parametern/MP får den nya klienten fullständig lista över tillgängliga hanterings platser. Vid den första start processen använder klienten den första hanterings plats som den kan komma åt. När klienten registrerar sig på platsen får den hanterings plats listan korrekt sorterad med det nya beteendet.

Mer information om klientens beteende för att hämta innehåll under installationen finns i [klient installation](#bkmk_ccmsetup).

Om du inte anger kommando rads parametern/MP under klient uppgraderingen, frågar klienten källor som Active Directory och WMI för alla tillgängliga hanterings platser. Klient uppgraderingen följer inte konfigurationen av gränser gruppen. <!--VSO 2841292-->  

För att klienter ska kunna använda den här funktionen aktiverar du följande inställning: **klienter föredrar att använda hanterings platser som anges i gränser grupper** i **Inställningar för hierarkin**.

> [!Note]  
> Processerna för operativ Systems distribution är inte medvetna om gränser grupper för hanterings platser.  

### <a name="troubleshooting"></a>Felsökning

Nya poster visas i **filen LocationServices. log**. Attributet för **lokalitet** identifierar något av följande tillstånd:

- **0**: okänd  

- **1**: den angivna hanterings platsen finns bara i platsens standard gränser grupp för återställning  

- **2**: den angivna hanterings platsen finns i en fjärran sluten plats eller i en intilliggande gränser grupp. Om hanterings platsen finns i både en granne och platsens standard gränser, är den lokala platsen 2.  

- **3**: den angivna hanterings platsen finns i den lokala eller aktuella gränser gruppen. Om hanterings platsen finns i den aktuella gränser gruppen och antingen en granne eller platsens standard gränser grupp är platsen 3. Om du inte aktiverar inställningen för önskade hanterings platser i hierarkiska inställningar är den lokala platsen alltid 3 oavsett vilken begränsande grupp hanterings platsen finns i.  

Klienterna använder lokala hanterings platser först (lokal 3), fjärran sluten sekund (plats 2) och sedan reserv (plats 1).

När en klient får fem fel på 10 minuter och inte kan kommunicera med en hanterings plats i den aktuella gräns gruppen försöker den kontakta en hanterings plats i en granne eller standard gräns gruppen för webbplatsen. Om hanterings platsen i den aktuella anspråks gruppen senare kommer tillbaka online återgår klienten till den lokala hanterings platsen vid nästa uppdaterings cykel. Uppdaterings cykeln är 24 timmar eller när den Configuration Manager Agent tjänsten startas om.

## <a name="preferred-management-points"></a><a name="bkmk_preferred"></a>Prioriterade hanterings platser

> [!Note]
> Beteendet för den här inställningen för hierarkin, **klienter föredrar att använda hanterings platser som anges i gränser grupper**, ändrade i version 1802. När du aktiverar den här inställningen använder Configuration Manager funktionen för gränser för den tilldelade hanterings platsen. Mer information finns i [hanterings platser](#management-points).

Prioriterade hanterings platser gör det möjligt för en klient att identifiera en hanterings plats som är kopplad till den aktuella nätverks platsen (gränsen).  

- En klient försöker använda en önskad hanterings plats från sin tilldelade plats innan den använder en som inte har kon figurer ATS som prioriterad från den tilldelade platsen.  

- Om du vill använda det här alternativet ska **klienterna hellre använda hanterings platser som anges i gränser grupper** i **Inställningar för hierarkin**. Konfigurera sedan gränser grupper på enskilda primära platser. Ta med de hanterings platser som ska kopplas till den gräns gruppens associerade gränser. Mer information finns i [Aktivera användning av prioriterade hanterings platser](boundary-group-procedures.md#bkmk_proc-prefer).  

- När du konfigurerar önskade hanterings platser och en klient ordnar sin lista över hanterings platser placerar klienten de prioriterade hanterings platserna överst i listan. Den här listan innehåller alla hanterings platser från klientens tilldelade plats.  

> [!NOTE]  
> Klient nätverks växling innebär att den ändrar sina nätverks platser. Till exempel när en bärbar dator reser till en annan plats i nätverket. När en klient är nätverks växling kan den använda en hanterings plats från den lokala platsen innan du försöker använda en server från dess tilldelade plats. I den här listan över servrar från den tilldelade platsen ingår önskade hanterings platser. Mer information finns i [förstå hur klienter hittar plats resurser och tjänster](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="overlapping-boundaries"></a>Överlappande gränser  

Configuration Manager stöder konfigurationer för överlappande gränser för innehålls platser. När klientens nätverks plats tillhör fler än en avgränsnings grupp:

- När en klient begär innehåll skickar Configuration Manager klienten en lista över alla distributions platser som har innehållet.  

- När en klient begär en server för att skicka eller ta emot information om tillståndsmigrering, skickar Configuration Manager klienten en lista över alla platser för tillståndsmigrering som är associerade med en avgränsnings grupp som innehåller klientens aktuella nätverks plats.  

Tack vare det här beteendet kan klienten välja den närmaste servern att överföra innehåll eller tillståndsmigreringsplats till.  

## <a name="example-of-using-boundary-groups"></a>Exempel på användning av gränser grupper

I följande exempel används en-klient som söker efter innehåll från en distributions plats. Det här exemplet kan tillämpas på andra plats system roller som använder gränser grupper.

Skapa tre gräns grupper som inte delar gränser eller plats system servrar:  

- Grupp BG_A med distributions platser DP_A1 och DP_A2  

- Grupp BG_B med distributions platser DP_B1 och DP_B2  

- Grupp BG_C med distributions platser DP_C1 och DP_C2  

Lägg till nätverks platserna för dina klienter som gränser till endast BG_A gräns gruppen. Konfigurera sedan relationer från den begränsande gruppen till de andra två gränser grupperna:  

- Konfigurera distributions platser för den första *Grans* gruppen (BG_B) som ska användas efter 10 minuter. Den här gruppen innehåller distributions platser DP_B1 och DP_B2. Båda är väl anslutna till den första gruppens gränser platser.  

- Konfigurera den andra *grann* gruppen (BG_C) som ska användas efter 20 minuter. Den här gruppen innehåller distributions platser DP_C1 och DP_C2. Båda finns i ett WAN-nätverk från de andra två gränser grupperna.  

- Lägg också till i standard platsens gränser grupp en annan distributions plats på plats servern. Den här servern är din primära plats för innehålls källan, men den är centralt placerad i alla dina gränser grupper.

    Exempel på gränser grupper och återställnings tider:

    ![Exempel på avgränsnings grupper och återställnings tider](media/BG_Fallback.png)  

Med den här konfigurationen:  

- Klienten börjar söka efter innehåll från distributions platser i dess *aktuella* gränser grupp (BG_A). Den söker igenom varje distributions plats i två minuter och växlar sedan till nästa distributions plats i ram gruppen. Klientens pool med giltiga innehålls käll platser innehåller DP_A1 och DP_A2.  

- Om klienten inte kan hitta innehåll från den *aktuella* gräns gruppen efter sökningen i 10 minuter, lägger den till distributions platserna från BG_B gräns gruppen till dess sökning. Den fortsätter sedan att söka efter innehåll från en distributions plats i dess kombinerade Server grupp. Den här poolen innehåller nu servrar från både BG_A-och BG_B-gränser. Klienten fortsätter att kontakta varje distributions plats i två minuter och växlar sedan till nästa server i poolen. Klientens pool med giltiga innehålls käll platser innehåller DP_A1, DP_A2, DP_B1 och DP_B2.  

- Efter ytterligare 10 minuter (totalt 20 minuter), om klienten fortfarande inte har hittat en distributions plats med innehåll, expanderas poolen så att den inkluderar tillgängliga servrar från den andra *grann* gruppen, gränsen BG_C. Klienten har nu sex distributions platser för att söka: DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 och DP_C2. Den fortsätter att ändra till en ny distributions plats varannan minut tills den hittar innehåll.  

- Om klienten inte har hittat innehåll efter totalt 120 minuter, går det tillbaka till att inkludera *standard plats gränsen* som en del av den fortsatta sökningen. Nu inkluderar poolen alla distributions platser från de tre konfigurerade gränserna och den sista distributions platsen som finns på plats servern. Klienten fortsätter sedan att söka efter innehåll, ändra distributions platser varannan minut tills innehållet har hittats.  

Genom att konfigurera de olika grann grupperna så att de blir tillgängliga vid olika tidpunkter, styr du när vissa distributions platser läggs till som en innehålls käll plats. Klienten använder återställning till standard platsens gränser grupp som säkerhets nät för innehåll som inte är tillgängligt från någon annan plats.

## <a name="changes-from-prior-versions"></a>Ändringar från tidigare versioner

Följande är nyckel ändringar i gränser grupper och hur klienter hittar innehåll i Configuration Manager aktuella grenen. Många av dessa ändringar och koncept fungerar tillsammans.

### <a name="configurations-for-fast-or-slow-are-removed"></a>Konfigurationer för snabb eller långsam tas bort

Du kan inte längre konfigurera enskilda distributions platser så att de blir snabba eller långsamma. I stället behandlas alla plats system som är kopplade till en avgränsnings grupp. På grund av den här ändringen stöder fliken **referenser** för gränser grupp egenskaperna inte längre konfigurationen av snabb eller långsam.  

### <a name="new-default-boundary-group-at-each-site"></a>Ny standard gränser grupp på varje plats

Varje primär plats har en ny standard gränser grupp med namnet **default-site-bounds-group &lt;>**. När en klient inte finns på en nätverks plats som är tilldelad en avgränsnings grupp, används de plats system som är kopplade till standard gruppen från dess tilldelade plats. Planera att använda den här gränser gruppen som ersättning till begreppet återställnings innehålls plats.

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>**Tillåt att återställnings käll platser för innehåll** tas bort

Du behöver inte längre uttryckligen konfigurera en distributions plats som ska användas för återställning. Alternativen för att konfigurera den här inställningen tas bort från-konsolen.

Resultatet av inställningen **tillåter att klienter använder en återställnings käll plats för innehåll** på en distributions typ för program har ändrats. Den här inställningen för en distributions typ gör nu att en klient kan använda standard platsens gränser-grupp som en innehålls käll plats.

#### <a name="boundary-groups-relationships"></a>Relationer för gränser grupper

Du kan länka varje avgränsnings grupp till en eller flera ytterligare avgränsnings grupper. Dessa länkar Forms relationer som du konfigurerar på fliken nya gränser-grupp egenskaper med namnet **relationer**:  

- Varje avgränsnings grupp som en klient är direkt associerad med kallas för en **aktuell** avgränsnings grupp.  

- En valfri avgränsnings grupp som en klient kan använda på grund av en koppling mellan klientens *aktuella* gränser grupp och en annan grupp kallas för en **intilliggande** avgränsnings grupp.  

- På fliken **relationer** lägger du till gränser grupper som ska användas som *intilliggande* avgränsnings grupp. Konfigurera också en tid i minuter för återställningen. När en klient inte kan hitta innehåll från en distributions plats i den *aktuella* gruppen är den här tiden när klienten börjar söka efter innehålls platser från *intilliggande* gräns grupper.  

    När du lägger till eller ändrar en gränser grupp konfiguration kan du blockera återställningen till den angivna avgränsnings gruppen från den aktuella gruppen som du konfigurerar.  

Om du vill använda den nya konfigurationen definierar du explicita associationer (länkar) från en avgränsnings grupp till en annan. Konfigurera alla distributions platser i den associerade gruppen med samma tid i minuter. När en klient inte kan hitta en innehålls källa från den *aktuella* gräns gruppen avgör den tid som du konfigurerar när den börjar söka efter innehålls källor från dess intilliggande gräns grupp.

Förutom de gränser grupper som du uttryckligen konfigurerar, har varje avgränsnings grupp en underförstådd länk till standard platsens gränser grupp. Den här länken aktive ras efter 120 minuter. Sedan blir standard platsens gränser grupp en intilliggande avgränsnings grupp. Det här beteendet gör att klienter kan använda som innehålls källa platser de distributions platser som är kopplade till den gränser gruppen.

Det här beteendet ersätter vad som tidigare kallades som reserv för innehåll. Åsidosätt det här standard beteendet på 120 minuter genom att explicit associera standard platsens gränser grupp till en *aktuell* grupp. Ange en angiven tid i minuter eller blockera reserven helt för att förhindra användningen.

### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>Klienter försöker hämta innehåll från varje distributions plats i upp till två minuter

När en klient söker efter en innehålls käll plats försöker den få åtkomst till varje distributions plats i två minuter innan ett nytt försök görs till en annan distributions plats. Detta är en förändring jämfört med tidigare versioner där klienter försökte ansluta till en distributions plats i upp till två timmar.

- Klienter väljer slumpvis den första distributions platsen från poolen med tillgängliga servrar i klientens *aktuella* gränser grupp (eller grupper).  

- Om klienten inte har hittat innehållet efter två minuter växlar den till en ny distributions plats och försöker hämta innehåll från den servern. Den här processen upprepas varannan minut tills klienten hittar innehållet eller når den sista servern i poolen.  

- Om en klient inte kan hitta en giltig innehålls käll plats från den *aktuella* poolen innan den når perioden för återställning till en *intilliggande* gränser grupp, lägger klienten sedan till distributions platserna från den *grann* gruppen i slutet av den aktuella listan. Sedan genomsöks den utökade gruppen med käll platser som innehåller distributions platserna från båda gränserna.  

    > [!TIP]  
    > När du skapar en explicit länk från den aktuella gräns gruppen till standard plats gräns gruppen och definierar en återställnings tid som är mindre än återställnings tiden för en länk till en intilliggande gräns grupp börjar klienterna söka i käll platserna från standard plats gräns gruppen innan du inkluderar Grans gruppen.  

- När klienten inte kan hämta innehåll från den sista servern i poolen påbörjas processen igen.  

## <a name="see-also"></a>Se även

- [Procedurer för gränsgrupper](boundary-group-procedures.md)  

- [Om gränser](boundaries.md)  

- [Grundläggande begrepp för innehållshantering](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)  
