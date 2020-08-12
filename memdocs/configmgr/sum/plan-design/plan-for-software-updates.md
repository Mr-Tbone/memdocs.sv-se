---
title: Planera programuppdateringar
titleSuffix: Configuration Manager
description: En plan för program uppdaterings platsens infrastruktur är nödvändig innan du använder program uppdateringar i en Configuration Manager produktions miljö.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: b7b3ef78924389232ea292d16c6840fbef9bb321
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88123599"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>Planera för program uppdateringar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du använder program uppdateringar i en Configuration Manager produktions miljö är det viktigt att du går igenom planerings processen. En bra plan för program uppdaterings platsens infrastruktur är en nyckel till en lyckad implementering av program uppdateringar. Information om kapacitets planering för program uppdateringar finns i [storleks-och skalnings nummer](../../core/plan-design/configs/size-and-scale-numbers.md#software-update-point).


##  <a name="determine-the-software-update-point-infrastructure"></a><a name="BKMK_SUPInfrastructure"></a> Fastställ programuppdateringsplatsens infrastruktur  

Det här avsnittet innehåller följande underavsnitt:    
- [Lista över program uppdaterings platser](#BKMK_SUPList)
- [Växling av program uppdaterings plats](#BKMK_SUPSwitching)
- [Växla klienter manuellt till en ny program uppdaterings plats](#BKMK_ManuallySwitchSUPs)
- [Programuppdateringsplatser i en icke-betrodd skog](#BKMK_SUP_CrossForest)
- [Använd en befintlig WSUS-server som synkroniserings källa på platsen på den översta nivån](#BKMK_WSUSSyncSource)
- [Program uppdaterings plats på en sekundär plats](#BKMK_SUPSecSite)  
- [Planera för Internetbaserade klienter](#bkmk_internet-clients)  
- [Planera innehåll för program uppdatering](#bkmk_content)  
- [Planera för uppdateringar från tredje part](#bkmk_thirdparty)  


Den centrala administrations platsen och alla underordnade primära platser måste ha en program uppdaterings plats. När du planerar för program uppdaterings platsens infrastruktur måste du bestämma följande beroenden:
- Var du ska installera program uppdaterings platsen för platsen  
- Vilka platser som kräver en program uppdaterings plats som godkänner kommunikation från Internetbaserade klienter
- Om du behöver en program uppdaterings plats på sekundära platser  

> [!IMPORTANT]  
>  Mer information om interna och externa beroenden som krävs för program uppdateringar finns i [krav för program uppdateringar](prerequisites-for-software-updates.md).  

Lägg till flera program uppdaterings platser på en Configuration Manager primära platsen för att ge fel tolerans. Redundansväxlingen för program uppdaterings platsen skiljer sig från den rent slumpaste modellen som används i designen för hanterings platser. Till skillnad från hanterings platsernas design, finns det kostnader för klient-och nätverks prestanda i design av program uppdaterings platsen när klienter växlar till en ny program uppdaterings plats. När klienten växlar till en ny WSUS-server för att söka efter programuppdateringar ökar storleken på katalogen liksom prestandakraven för nätverk och klient. Därför bevarar klienten tillhörigheten med den senaste program uppdaterings platsen från vilken den har genomsökts.  

Den första programuppdateringsplats som du installerar på den primära platsen är synkroniseringskällan för alla ytterligare programuppdateringsplatser som du lägger till på den primära platsen. När du har lagt till program uppdaterings platser och startat synkronisering visar du status för program uppdaterings platserna och synkroniseringens källa från noden **synkroniseringsstatus för program uppdaterings punkt** på arbets ytan **övervakning** .  

Om program uppdaterings platsen inte har kon figurer ATS som synkroniserings källa för platsen, tar du bort den misslyckade rollen manuellt. Välj sedan en ny program uppdaterings plats som ska användas som synkroniserings källa. Mer information finns i [ta bort en plats system roll](../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_role).  


###  <a name="software-update-point-list"></a><a name="BKMK_SUPList"></a> Lista över programuppdateringsplatser  

Configuration Manager förser klienten med en lista över program uppdaterings platser i följande scenarier:  

- En ny klient får principen att aktivera program uppdateringar  

- En klient kan inte kontakta sin tilldelade program uppdaterings plats och måste växla till en annan  

Klienten väljer slumpmässigt en program uppdaterings plats i listan. Den prioriterar program uppdaterings platserna i samma skog. Configuration Manager ger klienterna olika listor beroende på typ av klient:  

-   **Intranätbaserade klienter**: få en lista över program uppdaterings platser som du kan konfigurera för att bara tillåta anslutningar från intranätet, eller en lista över program uppdaterings platser som tillåter Internet-och intranät klient anslutningar.  

-   **Internetbaserade klienter**: få en lista över program uppdaterings platser som du konfigurerar för att bara tillåta anslutningar från Internet, eller en lista över program uppdaterings platser som tillåter Internet-och intranät klient anslutningar.  


###  <a name="software-update-point-switching"></a><a name="BKMK_SUPSwitching"></a> Växling till annan programuppdateringsplats  

> [!NOTE]  
> Klienter använder gränser grupper för att hitta en ny program uppdaterings plats. Om deras aktuella program uppdaterings plats inte längre är tillgänglig, använder de också gränser grupper för att komma igång och hitta en ny. Lägg till enskilda program uppdaterings platser i olika gränser grupper för att kontrol lera vilka servrar som en klient kan hitta. Mer information finns i [program uppdaterings platser](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  

Om du har flera program uppdaterings platser på en plats och en Miss lyckas eller blir otillgänglig, ansluter klienter till en annan program uppdaterings plats. Med den nya servern fortsätter klienterna att söka efter de senaste program uppdateringarna. När en klient först tilldelas en program uppdaterings plats förblir den tilldelad till den program uppdaterings platsen om den inte kan genomsökas.  

Sökningen efter programuppdateringar kan misslyckas med ett antal olika koder för återförsök och icke-återförsök. När sökningen visar en återförsöksfelkod gör klienten ett nytt försök att söka efter programuppdateringar på programuppdateringsplatsen. Vanligtvis beror ett återförsöksfel på att WSUS-servern är otillgänglig eller tillfälligt överbelastad. När klienten inte kan söka efter program uppdateringar, används följande process:  

1.  Klienten söker efter program uppdateringar:  
    - Vid den schemalagda tiden
    - När den körs manuellt från kontroll panelen på klienten
    - När den körs manuellt från Configuration Manager-konsolen via en klient meddelande åtgärd
    - När den körs från en Configuration Manager SDK-metod  

2.  Om sökningen Miss lyckas väntar klienten i 30 minuter innan genomsökningen görs om. Den använder samma program uppdaterings plats.  

3.  Klienten försöker minst fyra gånger var 30: e minut. Efter det fjärde försöket och efter att ha väntat ytterligare två minuter, flyttas klienten till nästa program uppdaterings plats i listan.  

4.  Klienten upprepar den här processen med den nya program uppdaterings platsen. Efter en lyckad genomsökning fortsätter klienten att ansluta till den nya program uppdaterings platsen.  

Följande lista innehåller ytterligare information som du bör tänka på när du försöker igen och växla mellan program uppdaterings punkter:  

-   Om en klient är frånkopplad från intranätet och inte kan söka efter program uppdateringar, växlar den inte till någon annan program uppdaterings plats. Det här felet förväntas, eftersom klienten inte kan komma åt det interna nätverket eller en program uppdaterings plats som tillåter anslutningar från intranätet. Configuration Manager-klienten fastställer tillgängligheten för intranätets program uppdaterings plats.  

-   Om du hanterar klienter på Internet och har konfigurerat flera program uppdaterings platser för att godkänna kommunikation från klienter på Internet, följer växlings processen den standard process för återförsök som beskrivs tidigare.  

-   Om skannings processen startar, men klienten stängs av innan genomsökningen är klar, betraktas den inte som ett genomsöknings haveri och det räknas inte som en av de fyra Återförsöken.  

När Configuration Manager tar emot någon av följande Windows Update Agent-felkoder, försöker klienten ansluta igen:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Om du vill söka efter en felkod konverterar du decimal fel koden till hexadecimalt och söker sedan efter det hexadecimala värdet på en plats, till exempel [wikin för Windows Update Agent – felkoder](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx). till exempel är decimal felkoden 2149842970 hexadecimal 8024001A, vilket innebär att WU_E_POLICY_NOT_SET ett princip värde inte har angetts.  


###  <a name="manually-switch-clients-to-a-new-software-update-point"></a><a name="BKMK_ManuallySwitchSUPs"></a>Växla klienter manuellt till en ny program uppdaterings plats

Växla Configuration Manager klienter till en ny program uppdaterings plats när det finns problem med den aktiva program uppdaterings platsen. Den här ändringen sker bara när en klient tar emot flera program uppdaterings platser från en hanterings plats.

> [!IMPORTANT]    
> När du växlar enheter till att använda en ny server använder enheterna reserv för att hitta den nya servern. Klienter växlar till den nya program uppdaterings platsen under nästa genomsöknings cykel för program uppdateringar.<!-- SCCMDocs#1537 -->
>
> Innan du börjar den här ändringen granskar du konfigurationerna för gränser-gruppen för att se till att program uppdaterings platserna finns i rätt gränser grupper. Mer information finns i [program uppdaterings platser](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  
>
> Om du växlar till en ny program uppdaterings plats genereras ytterligare nätverks trafik. Mängden trafik beror på inställningarna för WSUS-konfigurationen, till exempel synkroniserade klassificeringar och produkter, eller användning av en delad WSUS-databas. Om du planerar att byta flera enheter bör du göra det under underhålls perioder. Den här tids inställningen minskar påverkan på nätverket när klienterna genomsöks med den nya program uppdaterings platsen.  

#### <a name="process-to-switch-software-update-points"></a>Process för att byta program uppdaterings platser  
Starta den här ändringen på en enhets samling. När den Utlös ATS söker klienterna efter en annan program uppdaterings plats vid nästa genomsökning.  

1.  I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enhets samlingar** .  

2.  Välj mål samling. På fliken **Start** i menyfliksområdet i gruppen **samling** klickar du på **klient meddelande**och sedan på **Byt till nästa program uppdaterings plats**.  


###  <a name="software-update-points-in-an-untrusted-forest"></a><a name="BKMK_SUP_CrossForest"></a>Program uppdaterings platser i en icke-betrodd skog  

Skapa en eller flera program uppdaterings platser på en plats som stöd för klienter i en skog som inte är betrodd. Om du vill lägga till en program uppdaterings plats i en annan skog måste du först installera och konfigurera en WSUS-server i skogen. Starta sedan guiden för att lägga till en Configuration Manager plats server med program uppdaterings platsens plats system roll. Ange följande inställningar i guiden för att ansluta till WSUS-servern i den icke-betrodda skogen:  

-   Ange ett **installations konto för plats system** som har åtkomst till WSUS-servern i den ej betrodda skogen.  

-   Ange ett **anslutnings konto för WSUS-servern** för att ansluta till WSUS-servern.  

Låt säga att du har en primär plats i skog A med två programuppdateringsplatser (SUP01 och SUP02). För samma primära plats har du också två program uppdaterings platser (SUP03 och SUP04) i skog B. När du växlar till nästa program uppdaterings plats prioriterar klienterna servrarna från samma skog.  


###  <a name="use-an-existing-wsus-server-as-the-synchronization-source-at-the-top-level-site"></a><a name="BKMK_WSUSSyncSource"></a>Använd en befintlig WSUS-server som synkroniserings källa på platsen på den översta nivån  

Platsen på den översta nivån i hierarkin är vanligtvis konfigurerad för att synkronisera programuppdateringsmetadata med Microsoft Update. När din organisations säkerhets princip inte tillåter att platsen på den översta nivån får åtkomst till Internet, konfigurerar du synkroniseringens källa för platsen på den översta nivån så att den använder en befintlig WSUS-server. Den här WSUS-servern finns inte i din Configuration Manager-hierarki. Du kan till exempel ha en WSUS-server i ett Internet-anslutet nätverk (DMZ), men platsen på den högsta nivån finns i ett internt nätverk utan Internet åtkomst. Konfigurera WSUS-servern i DMZ som synkroniserings källa för metadata för program uppdateringar. Konfigurera WSUS-servern i DMZ för att synkronisera program uppdateringar med samma villkor som du behöver i Configuration Manager. I annat fall kanske inte platsen på den översta nivån synkroniserar de programuppdateringar som du förväntar dig. När du installerar program uppdaterings platsen konfigurerar du ett anslutnings konto för WSUS-servern. Det här kontot behöver åtkomst till WSUS-servern i DMZ. Bekräfta också att brand väggen tillåter trafik för lämpliga portar. Mer information finns i [portarna som används av program uppdaterings platsen till synkroniseringens källa](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS).  


###  <a name="software-update-point-on-a-secondary-site"></a><a name="BKMK_SUPSecSite"></a> Programuppdateringsplats på en sekundär plats  

Programuppdateringsplatsen är valfri på en sekundär plats. Installera endast en program uppdaterings plats på en sekundär plats. När en program uppdaterings plats inte är installerad på den sekundära platsen använder enheter inom gränserna för en sekundär plats en program uppdaterings plats på den tilldelade primära platsen. Normalt installerar du en program uppdaterings plats på en sekundär plats när det finns begränsad nätverks bandbredd mellan enheterna på den sekundära platsen och program uppdaterings platserna på den överordnade primära platsen. Du kan också använda den här konfigurationen när program uppdaterings platsen på den primära platsen närmar sig kapacitets gränsen. När du har installerat och konfigurerat en program uppdaterings plats på den sekundära platsen, uppdateras en plats-wide-princip för klienter och de börjar använda den nya program uppdaterings platsen.  


### <a name="plan-for-internet-based-clients"></a><a name="bkmk_internet-clients"></a>Planera för Internetbaserade klienter

När du behöver hantera enheter som roamas av nätverket på Internet utvecklar du en plan för hur du hanterar program uppdateringar på dessa enheter. Configuration Manager stöder flera tekniker för det här scenariot. Använd en eller en kombination som krävs för att uppfylla organisationens krav.

#### <a name="cloud-management-gateway"></a>Gateway för molnhantering
Skapa en Cloud Management Gateway i Microsoft Azure och aktivera minst en lokal program uppdaterings plats för att tillåta trafik från Internetbaserade klienter. När klienter växlar till Internet, fortsätter de att söka mot dina program uppdaterings platser. Alla Internetbaserade klienter får alltid innehåll från Microsoft Update moln tjänsten. 

Mer information finns i [Planera för Cloud Management Gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) och [Konfigurera gränser grupper](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  

#### <a name="internet-based-client-management"></a>Internetbaserad klienthantering
Placera en program uppdaterings plats i ett nätverk som riktas mot Internet och gör det möjligt att tillåta trafik från Internetbaserade klienter. När klienter växlar till Internet växlar de till den här program uppdaterings platsen för genomsökning. Alla Internetbaserade klienter får alltid innehåll från Microsoft Update moln tjänsten.

Mer information om fördelar och nack delar med Internetbaserad klient hantering finns i [Hantera klienter på Internet](../../core/clients/manage/manage-clients-internet.md).

#### <a name="windows-update-for-business"></a>Windows Update för företag
Med Windows Update för företag kan du hålla Windows 10-enheter alltid uppdaterade med de senaste kvalitets-och funktions uppdateringarna. Dessa enheter ansluter direkt till Windows Update moln tjänsten. Configuration Manager kan skilja mellan Windows 10-datorer som använder WUfB och WSUS för att hämta program uppdateringar.

Mer information finns i [integration med Windows Update för företag](../deploy-use/integrate-windows-update-for-business-windows-10.md).


### <a name="plan-software-update-content"></a><a name="bkmk_content"></a>Planera innehåll för program uppdatering

Klienterna måste ladda ned innehållsfilerna för program uppdateringar för att kunna installera dem. Configuration Manager tillhandahåller flera tekniker som stöder hantering och leverans av det här innehållet. Eller konfigurera program uppdaterings distributioner för att tillåta eller kräva att klienter hämtar innehåll direkt från Microsoft Update moln tjänsten.

#### <a name="download-and-distribute-content"></a>Hämta och distribuera innehåll 
Som standard använder processen för hantering av program uppdatering i Configuration Manager de inbyggda funktionerna för innehålls hantering. Dessa funktioner omfattar det centraliserade lagrings innehålls biblioteket för en instans och den distribuerade designen för distributions platsens plats system roll. Du använder dessa funktioner när du laddar ned och distribuerar distributions paket för program uppdatering. 

Mer information finns i [Hämta program uppdateringar](../deploy-use/download-software-updates.md).

#### <a name="manage-express-installation-files-for-windows-10"></a>Hantera installationsfiler för Express för Windows 10
Configuration Manager stöder användning av Express-installationsfiler för Windows 10-uppdateringar. Express uppdateringsfiler och stöd tekniker, till exempel leverans optimering, kan minska nätverks effekten hos stora innehållsfiler som hämtas till klienter. 

Mer information finns i [optimera leverans av Windows 10-uppdateringar](../deploy-use/optimize-windows-10-update-delivery.md).

#### <a name="clients-download-content-from-the-internet"></a>Klienter laddar ned innehåll från Internet
När du distribuerar program uppdateringar till klienter konfigurerar du distributionen för klienter att ladda ned innehåll från Microsoft Update moln tjänsten. När klienter inte kan ladda ned innehåll från en annan innehålls källa kan de fortfarande ladda ned innehållet från Internet. 

Från och med version 1806 behöver du inte skapa ett distributions paket när du distribuerar program uppdateringar. När du väljer alternativet **inget distributions paket** kan klienter fortfarande ladda ned innehåll från lokala källor, om det är tillgängligt, men laddas normalt från Microsoft Update-tjänsten.<!--1357933-->

Internetbaserade klienter hämtar alltid innehåll från Microsoft Update moln tjänsten. Distribuera inte distributions paket för program uppdatering till en moln distributions plats. Du debiteras för lagring med moln distributions platsen, men klienterna kommer inte att ladda ned paketen. 


### <a name="plan-for-third-party-updates"></a><a name="bkmk_thirdparty"></a>Planera för uppdateringar från tredje part
Configuration Manager integreras med WSUS, som internt stöder program uppdateringar som publicerats av Microsoft. De flesta kunder använder andra tredjepartsprogram som också behöver uppdateringar. Det finns flera alternativ att överväga för att hålla program från tredje part uppdaterade.

#### <a name="supersede-applications-to-update"></a>Ersätt program att uppdatera
Använd en ersättande relation med program hanterings funktionen i Configuration Manager för att uppgradera eller ersätta befintliga program. När du ersätter ett program anger du en ny distributions typ som ersätter det ersatta programmets distributions typ. Du kan också välja om du vill uppgradera eller avinstallera det ersatta programmet innan det ersättande programmet installeras.

Mer information finns i [ändra och ersätta program](../../apps/deploy-use/revise-and-supersede-applications.md).

#### <a name="third-party-software-updates"></a>Programuppdateringar från tredje part
Från och med version 1806 använder du noden **program uppdaterings kataloger från tredje part** i Configuration Manager-konsolen för att prenumerera på kataloger från tredje part, publicerar sina uppdateringar på program uppdaterings platsen och distribuerar dem sedan till klienter.<!--1352101-->

Mer information finns i [program uppdateringar från tredje part](../deploy-use/third-party-software-updates.md).

#### <a name="system-center-updates-publisher"></a>System Center Updates Publisher
System Center Updates Publisher (SCUP) är ett fristående verktyg som gör det möjligt för oberoende program varu leverantörer eller branschspecifika program utvecklare att hantera anpassade uppdateringar. Dessa uppdateringar omfattar de beroenden som driv rutiner och uppdaterings paket.

Mer information finns i [System Center Updates Publisher](../tools/updates-publisher.md).



##  <a name="plan-for-software-update-point-installation"></a><a name="BKMK_SUPInstallation"></a>Planera för installation av program uppdaterings plats  

Det här avsnittet innehåller följande underavsnitt:  
- [Krav för program uppdaterings platsen](#BKMK_SUPSystemRequirements)
- [Planera för WSUS-installation](#BKMK_PlanningForWSUS)
- [Konfigurera brandväggar](#BKMK_ConfigureFirewalls)  


Det här avsnittet innehåller information om de steg som krävs för att planera och förbereda för installation av program uppdaterings platsen. Innan du skapar en plats system roll för program uppdaterings platsen i Configuration Manager finns det flera krav att tänka på. De särskilda kraven beror på din Configuration Manager-infrastruktur. När du konfigurerar program uppdaterings platsen för att kommunicera med hjälp av HTTPS, är det här avsnittet särskilt viktigt att granska. HTTPS-aktiverade servrar kräver ytterligare åtgärder för att fungera korrekt.  

###  <a name="requirements-for-the-software-update-point"></a><a name="BKMK_SUPSystemRequirements"></a> Krav på programuppdateringsplatsen  

Installera rollen program uppdaterings plats på ett plats system som uppfyller minimi kraven för WSUS och de konfigurationer som stöds för Configuration Manager-plats system.  

-   Mer information om minimi kraven för WSUS-serverrollen i Windows Server finns i [Granska överväganden och system krav](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#11-review-considerations-and-system-requirements).  

-   Mer information om vilka konfigurationer som stöds för Configuration Manager-plats system finns i [krav för plats och plats system](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  


###  <a name="plan-for-wsus-installation"></a><a name="BKMK_PlanningForWSUS"></a> Planera för WSUS-installation  

Installera en version av WSUS som stöds på alla plats system servrar som du konfigurerar för program uppdaterings plats rollen. När du inte installerar program uppdaterings platsen på plats servern installerar du administrations konsolen för WSUS på plats servern. Den här komponenten gör att plats servern kan kommunicera med den WSUS som körs på program uppdaterings platsen.  

När du använder WSUS på Windows Server 2012 eller senare konfigurerar du ytterligare behörigheter för att tillåta **WSUS-Configuration Manager** -komponenten i Configuration Manager att ansluta till WSUS. Den här komponenten utför regelbundna hälso kontroller. Välj något av följande alternativ för att konfigurera den behörighet som krävs:  

-   Lägg till **SYSTEM** -kontot till gruppen **WSUS-administratörer**  

-   Lägg till **NT instans\system** -kontot som en användare för WSUS-databasen (SUSDB). Konfigurera minimi kraven för roll medlemskap för WebService-databasen.  
  
Mer information om hur du installerar WSUS på Windows Server finns i [Installera WSUS-serverrollen](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role).  

Om du installerar fler än en programuppdateringsplats på en primär plats, använder du samma WSUS-databas för varje programuppdateringsplats i samma Active Directory-skog. Att dela samma databas ger bättre prestanda när klienter växlar till en ny program uppdaterings plats. Mer information finns i [använda en delad WSUS-databas för program uppdaterings platser](software-updates-best-practices.md#bkmk_shared-susdb).  

#### <a name="configuring-the-wsus-content-directory-path"></a>Konfigurera katalog Sök vägen för WSUS-innehåll

När du installerar WSUS måste du ange en sökväg till en innehålls katalog. WSUS-innehålls katalogen används i första hand för att lagra de filer för licens villkor för Microsoft-programvara som krävs av klienterna under genomsökningen. Configuration Manager katalog för WSUS-innehåll ska inte överlappa med innehålls käll katalogen för Configuration Manager distributions paket för program vara. Om du överlappar katalogen WSUS-innehåll och källan för Configuration Manager paketet leder till att felaktiga filer tas bort från WSUS-innehålls katalogen.

####  <a name="configure-wsus-to-use-a-custom-website"></a><a name="BKMK_CustomWebSite"></a>Konfigurera WSUS att använda en anpassad webbplats  
När du installerar WSUS har du möjlighet att använda den befintliga IIS-standardwebbplatsen, eller att skapa en anpassad WSUS-webbplats. Skapa en anpassad webbplats för WSUS så att IIS är värd för WSUS-tjänsterna på en dedikerad virtuell webbplats. Annars delar den samma webbplats som används av de andra Configuration Manager plats system eller program. Den här konfigurationen är särskilt nödvändig när du installerar program uppdaterings plats rollen på plats servern. När du kör WSUS i Windows Server 2012 eller senare konfigureras WSUS som standard att använda port 8530 för HTTP och port 8531 för HTTPS. Ange dessa portar när du skapar program uppdaterings platsen på en plats.  


####  <a name="use-an-existing-wsus-infrastructure"></a><a name="BKMK_WSUSInfrastructure"></a> Använda en befintlig WSUS-infrastruktur  
Välj en WSUS-server som var aktiv i din miljö innan du installerade Configuration Manager som en program uppdaterings plats. När program uppdaterings platsen har kon figurer ATS anger du inställningarna för synkronisering. Configuration Manager ansluter till WSUS-servern som körs på program uppdaterings plats servern och konfigurerar WSUS med samma inställningar. 

Innan du konfigurerar servern som en program uppdaterings plats ska du jämföra konfigurationen för produkter och klassificeringar med dina Configuration Manager inställningar. Om du synkroniserar den befintliga WSUS-servern innan du konfigurerade den som en program uppdaterings plats, och listorna över produkter och klassificeringar skiljer sig, synkroniseras alla program uppdaterings metadata oavsett de konfigurerade inställningarna. Detta leder till oväntade metadata för program uppdateringar i plats databasen. 

Du får samma beteende när du lägger till produkter eller klassificeringar direkt i WSUS-administrationskonsolen och sedan initierar en synkronisering direkt. Varje timme Configuration Manager ansluter som standard till WSUS och återställer alla inställningar som har ändrats utanför Configuration Manager. De program uppdateringar som inte uppfyller de produkter och klassificeringar som du anger i synkroniseringsinställningarna anges som upphört att gälla. De tas sedan bort från plats databasen.  

När en WSUS-server är konfigurerad som en program uppdaterings plats kan du inte längre använda den som en fristående WSUS-server. Om du behöver en separat fristående WSUS-server som inte hanteras av Configuration Manager konfigurerar du den på en annan server.  

####  <a name="configure-wsus-as-a-replica-server"></a><a name="BKMK_WSUSAsReplica"></a> Konfigurera WSUS som en replikserver  
När du lägger till rollen program uppdaterings plats på en primär plats Server kan du inte använda en WSUS-server som är konfigurerad som en replik. Om WSUS-servern är konfigurerad som en replik kan Configuration Manager inte konfigurera WSUS-servern och synkroniseringen av WSUS Miss lyckas. Den första programuppdateringsplats som du installerar på en primär plats är den programuppdateringsplats som används som standard. Ytterligare programuppdateringsplatser på platsen konfigureras som repliker av den standardmässiga programuppdateringsplatsen.  

####  <a name="decide-whether-to-configure-wsus-to-use-ssl"></a><a name="BKMK_WSUSandSSL"></a> Avgöra om WSUS ska konfigureras att använda SSL  
Använd SSL-protokollet för att skydda program uppdaterings platsen. WSUS använder SSL för att autentisera klientdatorer och underordnade WSUS-servrar på WSUS-servern. WSUS använder även SSL för att kryptera programuppdateringsmetadata. När du väljer att skydda WSUS med SSL förbereder du WSUS-servern innan du installerar program uppdaterings platsen. Mer information finns i artikeln [Konfigurera SSL på WSUS-servern](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) i dokumentationen för WSUS. 

När du installerar och konfigurerar program uppdaterings platsen väljer du alternativet för att **Aktivera SSL-kommunikation för WSUS-servern**. Annars konfigurerar Configuration Manager WSUS att inte använda SSL. När du aktiverar SSL på en program uppdaterings plats konfigurerar du även eventuella program uppdaterings platser på underordnade platser för att använda SSL.  


###  <a name="configure-firewalls"></a><a name="BKMK_ConfigureFirewalls"></a>Konfigurera brand väggar  

Program uppdaterings platsen på en Configuration Manager Central administrations plats kommunicerar med WSUS på program uppdaterings platsen. WSUS kommunicerar med synkroniseringens källa för att synkronisera metadata för program uppdateringar. Program uppdaterings platser på en underordnad plats kommunicerar med program uppdaterings platsen på den överordnade platsen. Om det finns fler än en program uppdaterings plats på en primär plats kommunicerar de ytterligare program uppdaterings platserna med standard program uppdaterings platsen. Standard rollen är den första program uppdaterings platsen som installeras på platsen.  

Du kan behöva konfigurera brand väggen så att den tillåter HTTP-eller HTTPS-trafik som WSUS använder i följande scenarier: 
- Mellan program uppdaterings platsen och Internet
- Mellan en program uppdaterings plats och dess överordnade synkroniserings källa
- Mellan ytterligare program uppdaterings platser  

Anslutningen till Microsoft Update är alltid konfigurerad för port 80 för HTTP och port 443 för HTTPS. Använd en anpassad port för anslutningen från WSUS på program uppdaterings platsen på en underordnad plats till WSUS på program uppdaterings platsen på den överordnade platsen. Använd metoden exportera och importera synkronisering när säkerhets principen inte tillåter anslutningen. Mer information finns i avsnittet [synkronisering källa](#BKMK_SyncSource) i den här artikeln. Mer information om vilka portar som används av WSUS finns i [så här avgör du vilka port inställningar som används av WSUS i Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  


#### <a name="restrict-access-to-specific-domains"></a>Begränsa åtkomsten till vissa domäner  

Om din organisation begränsar nätverkskommunikation med Internet med en brand vägg eller proxyserver, måste du tillåta att den aktiva program uppdaterings platsen får åtkomst till Internet-slutpunkter. Sedan kan WSUS och automatiska uppdateringar kommunicera med Microsoft Update moln tjänsten.

Mer information finns i [krav för Internet åtkomst](../../core/plan-design/network/internet-endpoints.md#bkmk_sum).


##  <a name="plan-for-synchronization-settings"></a><a name="BKMK_SyncSettings"></a> Planera för synkroniseringsinställningar  

Det här avsnittet innehåller följande underavsnitt:  
- [Synkroniseringskälla](#BKMK_SyncSource)
- [Synkroniseringsschema](#BKMK_SyncSchedule)
- [Uppdaterings klassificeringar](#BKMK_UpdateClassifications)
- [Läkemedle](#BKMK_UpdateProducts)
- [Ersättningsregler](#BKMK_SupersedenceRules)
- [Språk](#BKMK_UpdateLanguages)  
- [Maximal kör tid](#bkmk_maxruntime)


Synkronisering av program uppdateringar i Configuration Manager laddar ned metadata för program uppdateringar baserat på kriterier som du konfigurerar. Platsen på den översta nivån i hierarkin synkroniserar program uppdateringar från Microsoft Update. Du har möjlighet att konfigurera program uppdaterings platsen på platsen på den översta nivån så att den synkroniseras med en befintlig WSUS-server, inte i hierarkin Configuration Manager. De underordnade primära platserna synkroniserar programuppdateringsmetadata från programuppdateringsplatsen på den centrala administrationsplatsen. Informationen i det här avsnittet hjälper dig att planera för synkroniseringsinställningarna innan du installerar och konfigurerar en programuppdateringsplats.  


###  <a name="synchronization-source"></a><a name="BKMK_SyncSource"></a>Källa för synkronisering  

Inställningarna för synkronisering av käll program för program uppdaterings platsen anger var program uppdaterings platsen hämtar metadata för program uppdateringar. Den anger även om synkroniseringsprocessen skapar WSUS-rapporterings händelser.  

-   **Källa för synkronisering**: som standard konfigurerar program uppdaterings platsen på platsen på den översta nivån synkroniseringens källfil för Microsoft Update. Du har möjlighet att synkronisera platsen på den översta nivån med en befintlig WSUS-server. Program uppdaterings platsen på en underordnad primär plats konfigurerar synkroniseringens källa som program uppdaterings plats på den centrala administrations platsen.  

    -  Den första programuppdateringsplatsen som du installerar på en primär plats, vilket är standardprogramuppdateringsplatsen, synkroniseras med den centrala administrationsplatsen. Ytterligare programuppdateringsplatser på den primära platsen synkroniseras med standardprogramuppdateringsplatsen på den primära platsen.  

    - När en program uppdaterings plats är frånkopplad från Microsoft Update eller från den överordnade uppdaterings servern konfigurerar du synkroniseringens källa så att den inte synkroniseras med en konfigurerad synkroniserings källa. Konfigurera i stället det att använda export-och import funktionen i **WSUSUtil** -verktyget för att synkronisera program uppdateringar. Mer information finns i avsnittet [Synkronisera programuppdateringar från en frånkopplad programuppdateringsplats](../get-started/synchronize-software-updates-disconnected.md).  

-   **WSUS-rapporterings händelser:** Windows Update agenten på klient datorer kan skapa händelse meddelanden för WSUS-rapportering. Dessa händelser används inte av Configuration Manager. Alternativet ska därför **inte skapa WSUS-rapporterings händelser**, är valt som standard. När dessa händelser inte skapas är den enda tid som klienten ska ansluta till WSUS-servern under utvärdering av program uppdateringar och kompatibilitetskontroll. Om de här händelserna behövs för rapportering utanför Configuration Manager ändrar du den här inställningen för att skapa WSUS-rapporterings händelser.  


###  <a name="synchronization-schedule"></a><a name="BKMK_SyncSchedule"></a>Synkroniseringsschema  

Konfigurera synkroniseringsschemat endast på program uppdaterings platsen på platsen på den översta nivån i Configuration Manager hierarkin. När du konfigurerar synkroniseringsschemat, synkroniseras programuppdateringsplatsen med synkroniseringskällan vid det datum och den tidpunkt du angett. Med det anpassade schemat kan du synkronisera program uppdateringar så att de optimeras för din miljö. Överväg prestanda kraven för WSUS-servern, plats servern och nätverket. Till exempel 2:00 AM en gång i veckan. Du kan också starta synkroniseringen manuellt på platsen på den översta nivån med åtgärden **Synkronisera program uppdateringar** från noderna **alla program uppdateringar** eller **program uppdaterings grupper** i Configuration Manager-konsolen.  

> [!TIP]  
>  Schemalägg synkroniseringen av program uppdateringar så att den körs genom att använda en tid som är lämplig för din miljö. Ett vanligt scenario är att ställa in synkroniseringsschemat så att det körs strax efter Microsofts vanliga program uppdaterings version den andra tisdagen varje månad. Dagen kallas vanligt vis för *korrigerings tisdag*. Om du använder Configuration Manager för att leverera Endpoint Protection-och Windows Defender-Definitions-och motor uppdateringar bör du överväga att ställa in synkroniseringsschemat så att det körs dagligen.  

När program uppdaterings platsen har synkroniserats skickar den en synkroniseringsbegäran till underordnade platser. Om du har ytterligare program uppdaterings platser på en primär plats skickar den en synkroniseringsbegäran till varje program uppdaterings plats. Den här processen upprepas på alla platser i hierarkin.  


###  <a name="update-classifications"></a><a name="BKMK_UpdateClassifications"></a> Klassificering av uppdateringar  

Alla programuppdateringar får en angiven klassificering så att de olika uppdateringstyperna lätt kan sorteras. Under synkroniseringsprocessen synkroniserar platsen metadata för de angivna klassificeringarna. 

Configuration Manager stöder synkronisering av följande uppdaterings klassificeringar:  

-   **Kritiska uppdateringar**: en brett utgiven uppdatering för ett särskilt problem som åtgärdar en kritisk, ej säkerhetsrelaterad bugg.  

-   **Definitions uppdateringar**: en uppdatering av virus-eller andra definitionsfiler.  

-   **Funktions paket**: nya produkt funktioner som distribueras utanför en produkt lansering och som vanligt vis ingår i nästa fullständiga produkt lansering.  

-   **Säkerhets uppdateringar**: en brett utgiven uppdatering för en produktspecifik, säkerhetsrelaterad fråga.  

-   **Service Pack**: en kumulativ uppsättning snabb korrigeringar som tillämpas på ett operativ system eller program. Dessa snabb korrigeringar innehåller säkerhets uppdateringar, kritiska uppdateringar och program uppdateringar.  

-   **Verktyg**: ett verktyg eller en funktion som hjälper till att slutföra en eller flera uppgifter.  

-   **Samlade uppdateringar**: en kumulativ uppsättning snabb korrigeringar som är paketerade tillsammans för enkel distribution. Dessa snabb korrigeringar innehåller säkerhets uppdateringar, kritiska uppdateringar och program uppdateringar. En samlad uppdatering avser vanligtvis ett visst område, till exempel en säkerhets- eller produktkomponent.  

-   **Uppdateringar**: en uppdatering av ett program eller en fil som är installerad för tillfället.  

-   **Uppgraderingar**: en funktions uppdatering till en ny version av Windows 10.  

Konfigurera inställningarna för uppdaterings klassificering på platsen på den översta nivån. Inställningarna för uppdaterings klassificering är inte konfigurerade på program uppdaterings platsen på underordnade platser eftersom metadata för program uppdateringar replikeras från platsen på den översta nivån. När du väljer uppdaterings klassificeringarna bör du vara medveten om fler klassificeringar som du väljer, desto längre tid tar det att synkronisera program uppdateringarnas metadata.  

> [!WARNING]  
>  Vi rekommenderar att du tar bort alla klassificeringar innan du synkroniserar för första gången. Efter den första synkroniseringen väljer du önskade klassificeringar och kör sedan om synkroniseringen.  


###  <a name="products"></a><a name="BKMK_UpdateProducts"></a>Läkemedle  

Metadata för varje program uppdatering definierar en eller flera produkter som uppdateringen gäller. En produkt är en specifik version av ett operativ system eller program. Ett exempel på en produkt är Microsoft Windows 10. En produkt familj är det grundläggande operativ system eller program som de enskilda produkterna härleds från. Ett exempel på en produkt serie är Microsoft Windows, varav Windows 10 och Windows Server 2016 är medlemmar. Välj en produkt familj eller enskilda produkter inom en produkt familj.  

När program uppdateringar tillämpas på flera produkter och minst en av produkterna har valts för synkronisering, visas alla produkter i Configuration Manager-konsolen även om vissa produkter inte har valts. Du väljer till exempel bara Windows Server 2012-produkten. Om en program uppdatering gäller för Windows Server 2012 och Windows Server 2012 Data Center Edition finns båda produkterna i plats databasen.  

Konfigurera bara produkt inställningarna på platsen på den översta nivån. Produkt inställningarna har inte kon figurer ATS på program uppdaterings platsen för underordnade platser eftersom metadata för program uppdateringar replikeras från platsen på den översta nivån. De fler produkter du väljer, desto längre tid tar det att synkronisera metadata för program uppdateringarna.  

> [!IMPORTANT]  
>  Configuration Manager lagrar en lista med produkter och produkt familjer som du väljer från när du först installerar program uppdaterings platsen. Produkter och produkt familjer som släpps efter Configuration Manager släpps kanske inte är tillgängliga för att väljas förrän du har slutfört synkroniseringen. Synkroniseringsprocessen uppdaterar listan över tillgängliga produkter och produkt familjer som du kan välja mellan. Rensa alla produkter innan du synkroniserar program uppdateringar för första gången. Efter den första synkroniseringen väljer du önskade produkter och kör sedan om synkroniseringen.  


###  <a name="supersedence-rules"></a><a name="BKMK_SupersedenceRules"></a>Ersättnings regler  

En programuppdatering som ersätter en annan fungerar vanligtvis på något av följande sätt:  

-   Förstärker, förbättrar eller uppdaterar den tidigare korrigeringen.  

-   Förbättrar effektiviteten för det ersatta uppdaterings fil paketet, som installeras på klienter om uppdateringen har godkänts för installation. Till exempel kan den ersatta uppdateringen innehålla filer som inte längre är relevanta för korrigeringen eller för de operativ system som stöds av den nya uppdateringen. Filerna ingår inte i det ersättande fil paketet för uppdateringen.  

-   Uppdaterar senare versioner av en produkt. Det innebär att versioner som inte kan användas för äldre versioner eller konfigurationer av en produkt uppdateras. Uppdateringar kan även ersätta andra uppdateringar om det har gjorts ändringar för utökat språkstöd. Till exempel kan en senare revision av en produkt uppdatering för Microsoft 365 appar ta bort stödet för ett äldre operativ system, men det kan lägga till ytterligare stöd för nya språk i den ursprungliga uppdaterings versionen.  

I egenskaperna för program uppdaterings platsen anger du att de ersatta program uppdateringarna ska upphöra att gälla omedelbart. Den här inställningen förhindrar att de inkluderas i nya distributioner. Den flaggar även befintliga distributioner för att ange att de innehåller en eller flera program uppdateringar som har upphört att gälla. Eller ange en tids period innan de ersatta program uppdateringarna upphör att gälla. Med den här åtgärden kan du fortsätta att distribuera dem. 

I till exempel följande scenarier kanske du vill distribuera en ersatt programuppdatering:  

-   En ersättande program uppdatering har endast stöd för nyare versioner av ett operativ system. Några av dina klient datorer kör tidigare versioner av operativ systemet.  

-   En ersättande program uppdatering har mer begränsad användbarhet än den program uppdatering som ersätts. Det här beteendet gör det olämpligt för vissa klienter.  

-   Om en ersättande program uppdatering inte har godkänts för distribution i produktions miljön.  

    > [!NOTE]  
    > - Innan Configuration Manager version 1806, när Configuration Manager anger att en ersatt program uppdatering **har upphört att gälla**, ställer det inte in uppdateringen till **nekad** i WSUS. Klienterna fortsätter att söka efter en utgången uppdatering tills uppdateringen nekas manuellt eller via ett anpassat skript.  Efter Configuration Manager version 1806 kommer Configuration Manager också att neka de ersatta uppdateringarna i WSUS. Mer information om rensnings uppgiften i WSUS finns i [underhåll av program uppdateringar](../deploy-use/software-updates-maintenance.md).
    > - Från och med Configuration Manager version 1810 kan du ange beteendet för ersättnings regler för **funktions uppdateringar** separat från **uppdateringar som inte är**av en funktion.

###  <a name="languages"></a><a name="BKMK_UpdateLanguages"></a>Användning  

Med språk inställningarna för program uppdaterings platsen kan du konfigurera: 
- De språk som sammanfattnings information (metadata för program uppdateringar) synkroniseras med för program uppdateringar  
- De program uppdaterings fil språk som laddas ned för program uppdateringar  

#### <a name="software-update-file"></a>Programuppdateringsfil  
Konfigurera språk för inställningen **program uppdaterings fil** i egenskaperna för program uppdaterings platsen. Den här inställningen tillhandahåller de standard språk som är tillgängliga när du laddar ned program uppdateringar på en plats. Ändra de språk som är markerade som standard varje gången program uppdateringar laddas ned eller distribueras. Under nedladdningsprocessen laddas de angivna språkens programuppdateringsfiler ned till källplatsen för distributionspaket, förutsatt att programuppdateringsfilerna är tillgängliga på det angivna språket. Därefter kopieras de till innehålls biblioteket på plats servern. De distribueras sedan till de distributions platser som har kon figurer ATS för paketet.  

Konfigurera språk inställningarna för program uppdaterings filen med de språk som oftast används i din miljö. Klienter på din plats använder till exempel främst engelska och japanska för Windows eller program. Det finns några andra språk som används på webbplatsen. Välj endast engelska och japanska i kolumnen **program uppdaterings fil** när du laddar ned eller distribuerar program uppdateringen. Med den här åtgärden kan du använda standardinställningarna på sidan **Val av språk** i distributions-och hämtnings guiderna. Den här åtgärden förhindrar också att onödiga uppdateringsfiler laddas ned. Konfigurera den här inställningen vid varje program uppdaterings plats i Configuration Manager hierarkin.  



#### <a name="summary-details"></a>Sammanfattningsinformation  
Under synkroniseringen uppdateras sammanfattningsinformationen (metadata om programuppdatering) för programuppdateringar på de språk som du har valt. I metadata finns information om program uppdateringen, till exempel:
- Name
- Beskrivning
- Produkter som stöds av uppdateringen
- Uppdatera klassificering
- Artikel-ID
- Nedladdnings-URL
- Tillämpbarhetsregler

Konfigurera inställningarna för sammanfattnings information på platsen på den översta nivån. Sammanfattnings informationen konfigureras inte på program uppdaterings platsen på underordnade platser eftersom metadata för program uppdateringar replikeras från den centrala administrations platsen med hjälp av filbaserad replikering. När du väljer språk för sammanfattningsinformationen ska du bara välja de språk som används i miljön. Ju fler språk du väljer, desto längre tid tar det att synkronisera metadata för programuppdateringarna. Configuration Manager visar metadata för program uppdateringar i språk språket för det operativ system som Configuration Manager-konsolen körs på. Om de lokaliserade egenskaperna för program uppdateringarna inte är tillgängliga i språk versionen av detta operativ system visas information om program uppdateringar på engelska.  

> [!IMPORTANT]  
>  Välj alla språk för sammanfattnings information som du behöver. När program uppdaterings platsen på platsen på den översta nivån synkroniseras med synkroniseringens källa, fastställer de valda sammanfattnings informations språken de metadata för program uppdateringar som hämtas. Om du ändrar språk för sammanfattnings information efter att synkroniseringen kördes minst en gången hämtas metadata för program uppdateringen för de modifierade sammanfattnings uppgifterna enbart för nya eller uppdaterade program uppdateringar. De program uppdateringar som redan har synkroniserats uppdateras inte med nya metadata för de ändrade språken, om inte program uppdateringen ändras på synkroniseringens källa.


###  <a name="maximum-run-time"></a><a name="bkmk_maxruntime"></a>Maximal kör tid
<!--3734426-->
*(Lanseras i version 1906)*

Från och med version 1906 kan du ange den maximala tid som en program uppdaterings installation ska slutföras. Du kan ange den maximala körnings tiden för följande:

- **Maximal kör tid för Windows-funktions uppdateringar (minuter)**
  - **Funktions uppdateringar** – en uppdatering som finns i någon av dessa tre klassificeringar:
    - Uppgraderingen
    - Samlade uppdateringar
    - Service Pack

- **Maximal kör tid för Office 365-uppdateringar och uppdateringar som inte är av funktioner för Windows (minuter)**
  - **Icke-funktions uppdateringar** – en uppdatering som inte är funktions uppgradering och vars produkt visas som en av följande:
    - Windows 10 (alla versioner)
    - Windows Server 2012
    - Windows Server 2012 R2
    - Windows Server 2016
    - Windows Server 2019
    - Office 365

- De här inställningarna ändrar bara den maximala körningen för nya uppdateringar som synkroniseras från Microsoft Update. Den ändrar inte körnings tiden för en befintlig funktion eller uppdateringar som inte är av en funktion.
- Alla andra produkter och klassificeringar kan inte konfigureras med den här inställningen. Om du behöver ändra den maximala kör tiden för en av dessa uppdateringar konfigurerar du [inställningarna för program uppdatering](../get-started/manage-settings-for-software-updates.md#BKMK_SoftwareUpdatesSettings)

> [!NOTE]
> I version 1906 är den maximala körningen inte tillgänglig när du installerar program uppdaterings platsen på den översta nivån. Efter installationen redigerar du den maximala körnings tiden för program uppdaterings platsen på den högsta nivån.

##  <a name="plan-for-a-software-updates-maintenance-window"></a><a name="BKMK_MaintenanceWindow"></a>Planera för underhålls perioden för program uppdateringar  

Lägg till en underhålls period som är dedikerad för installation av program uppdateringar. Med den här åtgärden kan du konfigurera ett allmänt underhålls fönster och en annan underhålls period för program uppdateringar. När du konfigurerar både en underhålls period för allmänt underhåll och program uppdateringar installeras endast program uppdateringar under underhålls perioden för program uppdateringar. 

Från och med Configuration Manager version 1810 kan du ändra det här beteendet och tillåta att program uppdateringar installeras under en allmän underhålls period. Mer information om den här klient inställningen finns i [klient inställningar för program uppdateringar](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint).

Mer information om underhålls perioder finns i [använda underhålls](../../core/clients/manage/collections/use-maintenance-windows.md)perioder.  


##  <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Omstartsalternativ för Windows 10-klienter efter installation av programuppdatering

När en program uppdatering som kräver en omstart distribueras och installeras med hjälp av Configuration Manager, schemalägger klienten en väntande omstart och visar en dialog ruta för omstart.

När det finns en väntande omstart för en Configuration Manager program uppdatering, är alternativet för att **Uppdatera och starta om** och **Uppdatera och Stäng** av tillgängligt på Windows 10-datorer i Windows energi alternativ. När du har använt något av dessa alternativ visas inte dialog rutan Starta om när datorn har startats om. I vissa fall kan operativ systemet ta bort de väntande omstarts alternativen. Detta kan inträffa om snabb start funktionen i Windows 10 är aktive rad. Mer information finns i [uppdateringar kanske inte installeras med snabb start i Windows 10](https://support.microsoft.com/help/4011287/windows-updates-not-install-with-fast-startup).

## <a name="evaluate-software-updates-after-a-servicing-stack-update"></a><a name="bkmk_ssu"></a>Utvärdera program uppdateringar efter en underhålls stack uppdatering
<!--4639943-->
Från och med version 2002 identifierar Configuration Manager om en service stack Update (SJÄLVBETJÄNINGS) är en del av en installation av flera uppdateringar. När en SJÄLVBETJÄNINGS identifieras installeras den först. Efter installationen av SJÄLVBETJÄNINGS körs en utvärderings cykel för program uppdateringar för att installera de återstående uppdateringarna. Den här ändringen gör att en beroende ackumulerad uppdatering installeras efter uppdateringen av underhålls stacken. Enheten behöver inte startas om mellan installationer, och du behöver inte skapa ytterligare en underhålls period. SSUs installeras först endast för icke-användarinitierade installationer. Om en användare till exempel initierar en installation för flera uppdateringar från Software Center, kanske SJÄLVBETJÄNINGS inte installeras först. Installationen av SSUs först är inte tillgänglig för Windows Server-operativsystem när du använder Configuration Manager version 2002. <!--7813007-->Den här funktionen har lagts till i Configuration Manager version 2006 för Windows Server-operativsystem.



## <a name="next-steps"></a>Nästa steg
När du planerar för program uppdateringar, se [förbereda för hantering av program uppdateringar](../get-started/prepare-for-software-updates-management.md).  

Mer information om hur du hanterar Windows som en tjänst finns i [grunderna i Configuration Manager som en tjänst och Windows som en tjänst](../../core/understand/configuration-manager-and-windows-as-service.md).
