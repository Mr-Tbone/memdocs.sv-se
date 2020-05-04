---
title: Teknisk för hands version 1805
titleSuffix: Configuration Manager
description: Lär dig mer om nya funktioner som är tillgängliga i Configuration Manager Technical Preview version 1805.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 88234bb3117850bc3280242671ae459308a5262e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714845"
---
# <a name="capabilities-in-technical-preview-1805-for-configuration-manager"></a>Funktioner i Technical Preview 1805 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1805. Du kan installera den här versionen om du vill uppdatera och lägga till nya funktioner på din tekniska för hands versions webbplats. 

Läs artikeln om [teknisk för hands version](technical-preview.md) innan du installerar den här uppdateringen. Den artikeln är bekant med de allmänna kraven och begränsningarna för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**Följande är nya funktioner som du kan prova med den här versionen.**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>Skapa en stegvis distribution med manuellt konfigurerade faser för en aktivitetssekvens
<!--1358148-->
Nu kan du [skapa en stegvis distribution](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) med manuellt konfigurerade faser för en aktivitetssekvens. Du kan lägga till upp till 10 ytterligare faser från fliken **faser** i guiden skapa stegvis distribution. 


### <a name="try-it-out"></a>prova!
Följ instruktionerna för att skapa en stegvis distribution där du konfigurerar alla faser manuellt. Skicka [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) så att vi vet hur det fungerade. 

1. I arbets ytan **program bibliotek** expanderar du **operativ system**och väljer **aktivitetssekvenser**.  

2. Högerklicka på en befintlig aktivitetssekvens och välj **skapa stegvis distribution**.  

3. På fliken **Allmänt** anger du den stegvisa distributionen ett namn, en beskrivning (valfritt) och väljer **Konfigurera alla faser manuellt**.  

4. Klicka på **Lägg till**på fliken **faser** .  

5. Ange ett **namn** för fasen och bläddra sedan till mål **fas samlingen**.  

6. På fliken **fas inställningar** väljer du ett alternativ för var och en av schemaläggnings inställningarna och väljer **Nästa** när du är klar.  

    - Kriterier för lyckad föregående fas (det här alternativet är inaktiverat för den första fasen).
        - **Procent andel lyckade distributioner**: Ange procent andelen enheter som slutför distributionen för de tidigare fas framgångs kriterierna.  

    - Villkor för att starta den här fasen av distributionen efter en lyckad föregående fas  
        - **Starta den här fasen automatiskt efter en uppskjutnings period (i dagar)**: Välj antalet dagar som du vill vänta innan du påbörjar nästa fas efter att föregående fas lyckades. 
        - **Starta den här distributions fasen manuellt**: Starta inte den här fasen automatiskt efter att den föregående fasen har slutförts.  

    - När en enhet har riktats in installerar du program varan
        - **Så snart som möjligt**: anger tids gränsen för installationen på enheten så snart enheten är riktad mot mål.
        - Tids **gräns (i förhållande till tidsenhetens mål)**: anger tids gräns för installation ett visst antal dagar efter det att enheten har varit riktad.  
     
7. Slutför guiden för fas inställningar.

8. På fliken **faser** i guiden skapa stegvis distribution kan du nu lägga till, ta bort, ändra ordning på eller redigera faser för den här distributionen.  

9. Slutför guiden skapa stegvis distribution.  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Stöd för moln distributions plats för Azure Resource Manager
<!--1322209-->
När du skapar en instans av [moln distributions platsen](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)ger guiden nu möjlighet att skapa en **Azure Resource Manager distribution**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) är en modern plattform för att hantera alla lösnings resurser som en enda entitet, som kallas för en [resurs grupp](/azure/azure-resource-manager/resource-group-overview#resource-groups). När du distribuerar en moln distributions plats med Azure Resource Manager använder platsen Azure Active Directory (Azure AD) för att autentisera och skapa nödvändiga moln resurser. Den här moderna distributionen kräver inte det klassiska hanterings certifikatet för Azure.  

Guiden för moln distributions plats innehåller fortfarande alternativet för en **klassisk tjänst distribution** med ett hanterings certifikat för Azure. För att förenkla distributionen och hanteringen av resurser rekommenderar vi att du använder Azure Resource Manager distributions modell för alla nya moln distributions platser. Distribuera om möjligt Befintliga moln distributions platser via Resource Manager.

Configuration Manager migrerar inte befintliga klassiska moln distributions platser till Azure Resource Manager distributions modell. Skapa nya moln distributions platser med hjälp av Azure Resource Manager distributioner och ta sedan bort de klassiska moln distributions platserna. 

> [!IMPORTANT]  
> Den här funktionen aktiverar inte stöd för Azure Cloud Service-leverantörer (CSP). Distributions plats distributionen i Azure Resource Manager fortsätter att använda den klassiska moln tjänsten som inte stöds av KRYPTOGRAFIPROVIDERn. Mer information finns i [tillgängliga Azure-tjänster i Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### <a name="prerequisites"></a>Krav  
- Integrering med [Azure AD](../clients/deploy/deploy-clients-cmg-azure.md). Identifiering av Azure AD-användare krävs inte.  

- Samma [krav för en moln distributions plats](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_requirements), förutom för Azures hanterings certifikat.  


### <a name="try-it-out"></a>prova!  
 Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

1. I Configuration Manager-konsolen, arbets ytan **Administration** , expandera **Cloud Services**och välj **moln distributions platser**. Klicka på **skapa en moln distributions plats** i menyfliksområdet.   

2. På sidan **Allmänt** väljer du **Azure Resource Manager distribution**. Klicka på **Logga** in för att autentisera med ett administratörs konto för Azure-prenumeration. Guiden fyller automatiskt i de återstående fälten från den Azure AD-prenumerations information som lagras under integrations kravet. Om du äger flera prenumerationer väljer du den prenumeration som du vill använda. Klicka på **Nästa**.  

3. På sidan **Inställningar** anger du serverns **PKI-certifikatfil som** vanligt. Det här certifikatet definierar det **FQDN-namn** för moln distributions platsen som används av Azure. Välj **region**och välj sedan ett resurs grupps alternativ för att antingen **skapa nya** eller **använda befintliga**. Ange namnet på den nya resurs gruppen eller Välj en befintlig resurs grupp i list rutan.  

4. Slutför guiden.  

> [!NOTE]  
> För den valda Azure AD server-appen tilldelar Azure prenumerations **deltagar** behörigheten.  

Övervaka förlopps distributionen för tjänsten med **CloudMgr. log** på tjänst anslutnings punkten.



## <a name="take-actions-based-on-management-insights"></a>Vidta åtgärder baserat på hanterings insikter
<!--1357930-->
Vissa [hanterings insikter](../servers/manage/management-insights.md) har nu möjlighet att vidta en åtgärd. Beroende på regeln, har den här åtgärden en av följande beteenden:  

- Navigera automatiskt i-konsolen till noden där du kan vidta ytterligare åtgärder. Om till exempel insikter om hantering rekommenderar att du ändrar en klient inställning, navigerar du till noden klient inställningar. Du kan vidta ytterligare åtgärder genom att ändra standard eller ett anpassat klient inställnings objekt.  

- Navigera till en filtrerad vy baserat på en fråga. Om du till exempel vidtar en åtgärd i den tomma samlings regeln visas bara dessa samlingar i listan över samlingar. Här kan du vidta ytterligare åtgärder, till exempel ta bort en samling eller ändra dess medlemskaps regler.  

Följande insikts regler för hantering har åtgärder i den här versionen:
- Säkerhet
    - Klient versioner av program mot skadlig kod som inte stöds
- Software Center
    - Använd den nya versionen av Software Center
- Program
    - Program utan distributioner
- Förenklad hantering
    - Klient versioner som inte är CB
- Samlingar
    - Tomma samlingar 
- Cloud Services
    - Uppdatera klienter till den senaste versionen av Windows 10



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>Överföra arbets belastning för enhets konfiguration till Intune med hjälp av samhantering
<!--1357903-->

Nu kan du överföra arbets belastningen för enhets konfigurationen från Configuration Manager till Intune efter att du aktiverat samhantering. Genom att överföra den här arbets belastningen kan du använda Intune för att distribuera MDM-principer, samtidigt som du fortsätter att använda Configuration Manager för att distribuera program. 

Om du vill gå över den här arbets belastningen går du till sidan Egenskaper för samhantering och flyttar skjutreglaget från Configuration Manager till **pilot** eller **alla**. Mer information finns i [Co-Management för Windows 10-enheter](../../comanage/overview.md).

> [!Note]  
> Om du flyttar den här arbets belastningen flyttas även **resurs åtkomsten** och **Endpoint Protection** arbets belastningar, som är en del av arbets belastningen för enhets konfigurationen.

När du övergår till den här arbets belastningen kan du fortfarande distribuera inställningar från Configuration Manager till samhanterade enheter, även om Intune är enhets konfigurations utfärdaren. Detta undantag kan användas för att konfigurera inställningar som krävs av din organisation men som ännu inte är tillgängliga i Intune. Ange detta undantag i en Configuration Manager konfigurations bas linje. Aktivera alternativet om du **alltid vill använda den här bas linjen även för samhanterade klienter** när du skapar bas linjen, eller på fliken **Allmänt** i egenskaperna för en befintlig bas linje. 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>Aktivera distributions platser för att använda nätverks överbelastnings kontroll
<!--1358112-->

Windows Server med låg extra fördröjning i bakgrunds transport (LEDBAT) är en funktion i Windows Server som hjälper dig att hantera nätverks överföringar i bakgrunden. För distributions platser som körs på versioner av Windows Server som stöds kan du aktivera ett alternativ för att justera nätverks trafiken. Klienter använder bara nätverks bandbredd när den är tillgänglig. 

Mer information om Windows-LEDBAT finns i blogg inlägget [nya transport förskott](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/) .


### <a name="prerequisites"></a>Krav
- En distributions plats på Windows Server, version 1709.  

- Det finns ingen klient förutsättning.<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Välj noden **distributions platser** . Välj mål distributions plats och klicka på **Egenskaper** i menyfliksområdet.  

2. På fliken **Allmänt** aktiverar du alternativet för att **Justera nedladdnings hastigheten så att den använder oanvänd nätverks bandbredd (Windows LEDBAT)**.  



## <a name="cloud-management-dashboard"></a>Instrument panel för moln hantering
<!--1358461-->
Den nya **moln hanterings instrument panelen** tillhandahåller en centraliserad vy för CMG-användning (Cloud Management Gateway). När platsen har registrerats med Azure AD visas även data om moln användare och enheter.  

Följande skärm bild är en del av instrument panelen för moln hantering som visar två av de tillgängliga panelerna:  
![Instrument panels paneler för moln hantering CMG trafik och aktuella online-klienter](media/1358461-cmg-dashboard.png)

Den här funktionen omfattar även **CMG-anslutnings analys** för verifiering i real tid för att under lätta fel sökningen. I konsol verktyget kontrol leras tjänstens aktuella status och kommunikations kanalen genom CMG anslutnings punkt till alla hanterings platser som tillåter CMG-trafik.


### <a name="prerequisites"></a>Krav
- En aktiv [Cloud Management Gateway](../clients/manage/cmg/plan-cloud-management-gateway.md) som används av Internetbaserade klienter.  

- Den webbplats som publicerats till [Azure-tjänster](../servers/deploy/configure/azure-services-wizard.md) för moln hantering.  


### <a name="try-it-out"></a>prova!
Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

#### <a name="cloud-management-dashboard"></a>Instrument panel för moln hantering

Gå till arbets ytan **övervakning** i Configuration Manager-konsolen. Välj noden **moln hantering** och Visa paneler på instrument panelen.  

#### <a name="cmg-connection-analyzer"></a>Anslutnings analys för CMG

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **Cloud Services** och välj **Cloud Management Gateway**.  

2. Välj mål CMG-instansen och välj sedan **anslutnings analys** i menyfliksområdet.  

3. I fönstret CMG Connection Analyzer väljer du något av följande alternativ för att autentisera med tjänsten:  

     1. **Azure AD-användare**: Använd det här alternativet om du vill simulera kommunikation på samma sätt som en molnbaserad användar identitet som är inloggad på en Azure AD-ansluten Windows 10-enhet. Klicka på **Logga** in för att ange autentiseringsuppgifterna på ett säkert sätt för det här Azure AD-användarkontot.  

     2. **Klient certifikat**: Använd det här alternativet om du vill simulera kommunikation på samma sätt som en Configuration Manager-klient med ett [certifikat för klientautentisering](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_clientauth).  

4. Starta analysen genom att klicka på **Starta** . Resultaten visas i analys fönstret. Välj en post om du vill visa mer information i fältet Beskrivning.  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager har alltid tillhandahållit en stor centraliserad lagring av enhets data, som kunder använder för rapporterings syfte. Dessa data är dock bara så väl som den senaste gången de samlades in från klienter. 

CMPivot är ett nytt konsol verktyg som ger åtkomst till real tids status för enheter i din miljö. Den kör omedelbart en fråga på alla aktuella anslutna enheter i mål samlingen och returnerar resultatet. Sedan kan du filtrera och gruppera dessa data i verktyget. Genom att tillhandahålla real tids data från online-klienter kan du snabbare besvara affärs frågor, felsöka problem och reagera på säkerhets incidenter.

Till exempel, vid [minskning av problem med spekulativ körnings sidans kanal](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974), är ett av kraven att uppdatera systemets BIOS. Du kan använda CMPivot för att snabbt fråga efter systemets BIOS-information och hitta klienter som inte är kompatibla. 

I den här skärm bilden visar CMPivot två separata BIOS-versioner med ett antal enheter. Du kan använda den här exempel frågan när du testar CMPivot:  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![CMPivot-fönster med exempel fråga från BIOSVersion](media/1358456-cmpivot-biosversion.png)

Du kan klicka på enhets antalet för att öka detalj nivån för att se de enskilda enheterna. När du visar enheter i CMPivot kan du högerklicka på en enhet och välja följande [klient meddelande åtgärder](../clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode):
- Kör skript
- Fjärrstyrning
- Resursläsaren

När du högerklickar på en speciell enhet kan du också pivotera vyn för den aktuella enheten till något av följande attribut:
- Autostart-kommandon
- Installerade produkter
- Processer
- Tjänster
- Användare
- Aktiva anslutningar
- Uppdateringar som saknas

### <a name="prerequisites"></a>Krav
- Mål klienterna måste uppdateras till den senaste versionen.  

- Configuration Manager-administratören måste ha behörighet för att köra skript. Mer information finns i [säkerhets roller för skript](../../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles).  

### <a name="try-it-out"></a>prova!
Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen och välj **enhets samlingar**. Välj en mål samling och klicka på **Starta CMPivot** i menyfliksområdet för att starta verktyget.  

2. Gränssnittet innehåller ytterligare information om hur du använder verktyget. 
     - Du kan manuellt ange frågesträngarna överst eller klicka på länkarna i den infogade dokumentationen.
     - Klicka på en av **entiteterna** för att lägga till den i frågesträngen. 
     - Länkarna för **tabell operatorer**, **agg regerings funktioner**och **skalära funktioner** öppnar språk referens dokumentation i webbläsaren. CMPivot använder samma frågespråk som [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).



## <a name="improved-secure-client-communications"></a>Förbättrad säker klient kommunikation
<!--1356889,1358228,1358460-->
Att använda HTTPS-kommunikation rekommenderas för alla Configuration Manager kommunikations vägar, men kan vara utmanande för vissa kunder på grund av omkostnader för hantering av PKI-certifikat. Införandet av Azure Active Directory (Azure AD)-integration minskar vissa, men inte alla certifikat krav. 

Den här versionen innehåller förbättringar av hur klienter kommunicerar med plats system. Det finns två primära mål för dessa förbättringar:  

- Du kan skydda klient kommunikation utan att behöva certifikat för PKI-serverautentisering.  

- Klienter kan få säker åtkomst till innehåll från distributions platser utan att det behövs något konto för nätverks åtkomst.  

> [!Note]  
> PKI-certifikat är fortfarande ett giltigt alternativ för kunder som vill använda det.  


### <a name="scenarios"></a><a name="bkmk_token"></a>Olika
Följande scenarier drar nytta av dessa förbättringar:  

#### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_token1"></a>Scenario 1: klient till hanterings plats
<!--1356889-->
[Azure AD-anslutna enheter](/azure/active-directory/devices/concept-azure-ad-join) kan kommunicera via en Cloud Management Gateway (CMG) med en hanterings plats som är KONFIGURERAD för http. Plats servern genererar ett certifikat för hanterings platsen så att den kan kommunicera via en säker kanal.   

> [!Note]  
> Detta beteende har ändrats från Configuration Manager nuvarande gren version 1802, vilket kräver en HTTPS-aktiverad hanterings plats för det här scenariot. Mer information finns i [Aktivera hanterings plats för https](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

#### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_token2"></a>Scenario 2: klient till distributions plats
<!--1358228-->
En arbets grupp eller Azure AD-ansluten klient kan ladda ned innehåll via en säker kanal från en distributions plats som kon figurer ATS för HTTP.   

#### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_token3"></a>Scenario 3 enhets identitet för Azure AD 
<!--1358460-->
En Azure AD-ansluten eller en [hybrid Azure AD-enhet](/azure/active-directory/devices/concept-azure-ad-join-hybrid) utan en Azure AD-användare som är inloggad kan på ett säkert sätt kommunicera med sin tilldelade plats. Den molnbaserade enhets identiteten räcker nu för att autentisera med CMG och hanterings platsen.  


### <a name="prerequisites"></a>Krav  

- En hanterings plats som kon figurer ATS för HTTP-klientanslutningar. Ange det här alternativet på fliken **Allmänt** i egenskaperna för plats system rollen.  

- En distributions plats som kon figurer ATS för HTTP-klientanslutningar. Ange det här alternativet på fliken **Allmänt** i egenskaperna för plats system rollen. Aktivera inte alternativet för att **tillåta att klienter ansluter anonymt**.  

- En gateway för moln hantering.  

- Publicera webbplatsen till Azure AD för moln hantering.  

    - Om du redan har uppfyllt den här förutsättningen för din webbplats måste du uppdatera Azure AD-programmet. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **Cloud Services**och välj **Azure Active Directory klienter**. Välj Azure AD-klienten, Välj webb programmet i fönstret **program** och klicka sedan på **Uppdatera program inställning** i menyfliksområdet.  

- En klient som kör Windows 10 version 1803 och anslutit till Azure AD. (Detta krav är tekniskt bara för [Scenario 3](#bkmk_token3).) 


### <a name="try-it-out"></a>prova!
Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj **platser**. Välj platsen och klicka på **Egenskaper** i menyfliksområdet.  

2. Växla till fliken **klient dator kommunikation** . Välj alternativet för **https eller http** och aktivera sedan det nya alternativet för att **använda Configuration Manager-genererade certifikat för http-plats system**.  

Se den tidigare [listan över scenarier](#bkmk_token) som ska verifieras.

> [!Tip]
> I den här versionen väntar du upp till 30 minuter för hanterings platsen för att ta emot och konfigurera det nya certifikatet från platsen.

Du kan se dessa certifikat i Configuration Manager-konsolen. Gå till arbets ytan **Administration** , expandera **säkerhet**och välj noden **certifikat** . Leta efter **SMS-utfärdande** rot certifikat och plats server roll certifikat som utfärdats av SMS-utfärdande rot.


### <a name="known-issues"></a>Kända problem
- Användaren kan inte Visa program vara som är riktade mot dem som tillgängliga i Software Center.  

- Distributions scenarier för operativ system kräver fortfarande kontot för nätverks åtkomst.  

- Att aktivera och inaktivera alternativet för att **använda Configuration Manager-genererade certifikat för HTTP-plats system** kan leda till att certifikatet inte binds korrekt till plats system rollerna. Inga certifikat som utfärdats av certifikatet "SMS-utfärdande" är kopplade till en webbplats i Windows Server Internet Information Services (IIS). Undvik det här problemet genom att ta bort alla certifikat som utfärdats av "SMS-utfärdande" från **SMS** -certifikatarkivet i Windows och starta sedan om smsexec-tjänsten.



## <a name="improvements-for-enabling-third-party-software-update-support"></a>Förbättringar för att aktivera stöd för program uppdateringar från tredje part
<!--1357605-->
Som ett resultat av din UserVoice-feedback om [program uppdateringar från tredje part](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co), upprepas den här versionen ytterligare vid integreringen med System Center Updates PUBLISHER (SCUP). Configuration Manager Technical Preview [version 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients) har lagt till möjligheten att läsa certifikatet från WSUS för uppdateringar från tredje part och sedan distribuera certifikatet till klienter. Men du behövde fortfarande använda verktyget SCUP för att skapa och hantera certifikatet för att signera program uppdateringar från tredje part.

I den här versionen kan du aktivera Configuration Manager-platsen för att automatiskt konfigurera certifikatet. Platsen kommunicerar med WSUS för att skapa ett certifikat för det här ändamålet. Configuration Manager fortsätter sedan att distribuera certifikatet till klienter. Den här iterationen tar bort behovet av att använda SCUP-verktyget för att skapa och hantera certifikatet. 

Mer information om allmän användning av SCUP-verktyget finns [System Center Updates Publisher](../../sum/tools/updates-publisher.md).

### <a name="prerequisites"></a>Krav
- Aktivera och distribuera klient inställningen **Aktivera program uppdateringar från tredje part** i **program uppdaterings** gruppen.
- Om WSUS finns på en separat server från program uppdaterings platsen, måste du göra något av följande alternativ på den fjärranslutna WSUS-servern:
    - Aktivera Remote Registry-tjänsten i Windows  
    eller
    - Skapa ett nytt DWORD `HKLM\Software\Microsoft\Update Services\Server\Setup`-värde med namnet **EnableSelfSignedCertificates** med värdet i register nyckeln `1`. 

### <a name="try-it-out"></a>prova!
Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration** och välj **platser**. Välj platsen på den översta nivån, klicka på **Konfigurera plats komponenter** i menyfliksområdet och välj **program uppdaterings plats**.  

2. Växla till fliken **uppdateringar från tredje part** . Välj alternativet för att **Aktivera program uppdateringar från tredje part**och välj sedan alternativet för **Configuration Manager hanterar certifikatet automatiskt**.

3. Fortsätt med resten av det vanliga SCUP-arbetsflödet för att importera en program uppdaterings katalog från tredje part och distribuera sedan uppdateringarna till klienter.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Förbättringar av aktivitetssekvens för Windows 10-uppgradering på plats
<!--1358500-->

Standard mal len för aktivitetssekvenser för Windows 10 uppgradering på plats innehåller nu en annan ny grupp med rekommenderade åtgärder som du kan lägga till om uppgraderingen Miss lyckas. De här åtgärderna gör det enklare att felsöka.

### <a name="new-groups-under-run-actions-on-failure"></a>Nya grupper under **körnings åtgärder vid haverining**
- **Samla in loggar**: om du vill samla in loggar från klienten lägger du till steg i den här gruppen. 
    - En vanlig metod är att kopiera loggfilerna till en nätverks resurs. Använd steget [Anslut till nätverksmapp](../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) för att upprätta anslutningen. 
    - Om du vill utföra kopierings åtgärden använder du ett anpassat skript eller verktyg med [kommando raden kör](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) eller [kör PowerShell-skript](../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) .
    - Filer som ska samlas in kan innehålla följande loggar:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - Mer information om Setupact. log och andra Installationsprogrammet för Windows loggar finns i [installationsprogrammet för Windows loggfiler](/windows/deployment/upgrade/log-files).
    - Mer information om Configuration Manager klient loggar finns i [Configuration Manager klient loggar](../plan-design/hierarchy/log-files.md#BKMK_ClientLogs)
    - Mer information om _SMSTSLogPath och andra användbara variabler finns [inbyggda variabler för aktivitetssekvenser](../../osd/understand/task-sequence-variables.md)

- **Kör diagnostikverktyg**: om du vill köra ytterligare diagnostikverktyg lägger du till steg i den här gruppen. Dessa verktyg bör automatiseras för att samla in ytterligare information från systemet så snart som möjligt.
    - Ett sådant verktyg är Windows- [SetupDiag](/windows/deployment/upgrade/setupdiag). Det är ett fristående diagnostikverktyg som du kan använda för att få information om varför en Windows 10-uppgradering misslyckades.
         - [Skapa ett paket](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) för verktyget i Configuration Manager.
         - Lägg till steget [Kör kommando rad](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) i den här gruppen av aktivitetssekvensen. Använd alternativet **paket** för att referera till verktyget. Följande sträng är ett exempel på en **kommando rad**:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>CMTrace installeras med klienten
<!--1357971-->

CMTrace-logg visnings verktyget installeras nu automatiskt tillsammans med Configuration Manager-klienten. Den läggs till i klient installations katalogen, vilket som standard är `%WinDir%\ccm\cmtrace.exe`.

> [!Note]  
> CMTrace registreras *inte* automatiskt med Windows för att öppna fil namns tillägget. log.



## <a name="improvement-to-the-configuration-manager-console"></a>Förbättra Configuration Manager-konsolen
<!--1358202-->
Vi har gjort följande förbättringar i Configuration Manager-konsolen:

- Enhets listor under till gångar och efterlevnad, enheter visas nu som standard för den inloggade användaren. Värdet är lika aktuellt som [klientens status](../clients/manage/monitor-clients.md#bkmk_indStatus). Värdet rensas när användaren loggar ut. Om ingen användare är inloggad är värdet tomt. 

### <a name="known-issues"></a>Kända problem
Värdet för den inloggade användaren är tomt i noden enheter eller när du visar en enhets lista under noden enhets samlingar. Undvik det här problemet genom att ladda ned det här [SQL-skriptet](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c). Kör sp_BgbUpdateLiveData. SQL på plats databas servern och starta sedan om smsexec och sms_notification_server tjänsterna på hanterings platsen.<!--514471-->



## <a name="improvements-to-console-feedback"></a>Förbättringar av feedback på konsolen
<!--1357542-->
Den här versionen innehåller följande förbättringar av den nya mekanismen för [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) i Configuration Manager-konsolen:  

- Dialog rutan feedback kommer nu ihåg dina tidigare inställningar, till exempel de valda alternativen och din e-postadress.  

- Det stöder nu offline-feedback. Spara feedback från-konsolen och ladda sedan upp till Microsoft från ett Internet-anslutet system. Använd det nya verktyget för uppladdning av offline- `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`feedback som finns i. Om du vill se tillgängliga och nödvändiga kommando rads alternativ kör du verktyget med `--help` alternativet. Det anslutna systemet behöver åtkomst till **Petrol.Office.Microsoft.com**.

### <a name="known-issues"></a>Kända problem
När du använder **Skicka ett leende** eller **skicka en bister min** från-konsolen på en dator med Internet anslutning kan den returnera följande meddelande: "Det gick inte att skicka feedback". Om du klickar på **Mer information**visas följande text: `{"Message":""}`. Det här felet beror på ett känt problem med svaret från system för backend-feedback. Du kan ignorera felet. Microsoft har fortfarande fått din feedback. (Om informationen visar ett annat meddelande använder du alternativet offline-feedback för att försöka skicka feedbacken vid ett senare tillfälle.)



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Förbättringar av PXE-aktiverade distributions platser
<!--1357580-->

Den här versionen innehåller följande ytterligare förbättringar när du använder alternativet för att [**Aktivera en PXE-svarare utan Windows Deployment-tjänst**](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) på en distributions plats:  

- Regler för Windows-brandväggen skapas automatiskt på distributions platsen när du aktiverar det här alternativet  
- Förbättringar av komponent loggning



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>Förbättring av maskin varu inventering för stora heltals värden
<!--1357880-->
Maskin varu inventeringen har för närvarande en gräns för heltal som är större än 4 294 967 296 (2 ^ 32). Den här gränsen kan nås för attribut som hård disk storlekar i byte. Hanterings platsen bearbetar inte heltals värden över den här gränsen, vilket innebär att inget värde lagras i databasen. I den här versionen ökas gränsen till 18446744073709551616 (2 ^ 64). 

För en egenskap med ett värde som inte ändras, t. ex. total disk storlek, kan du inte omedelbart se värdet när du har uppgraderat platsen. De flesta maskin varu inventeringar är en delta rapport. Klienten skickar endast värden som ändras. Undvik det här problemet genom att lägga till en annan egenskap i samma klass. Den här åtgärden gör att klienten uppdaterar alla egenskaper i klassen som har ändrats. 



## <a name="improvement-to-wsus-maintenance"></a>Förbättringar av WSUS-underhåll
<!--1357898-->

I guiden Rensa WSUS nekas uppdateringar som antingen har upphört att gälla eller ersatts enligt ersättnings reglerna. De här reglerna definieras i egenskaperna för komponenten för program uppdaterings platsen.

### <a name="try-it-out"></a>prova!
Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration** och välj **platser**. Välj platsen på den översta nivån, klicka på **Konfigurera plats komponenter** i menyfliksområdet och välj **program uppdaterings plats**.  

2. Växla till fliken **ersättnings regler** . Aktivera alternativet att **köra guiden WSUS-rensning**. Ange önskat ersättnings beteende.  

3. Granska filen WSyncMgr. log.



## <a name="improvement-to-support-for-cng-certificates"></a>Förbättringar av stöd för CNG-certifikat
<!--1357314-->
I den här versionen använder du [CNG-certifikat](../plan-design/network/cng-certificates-overview.md) för följande ytterligare https-aktiverade Server roller:  
- Certifikat registrerings plats, inklusive NDES-servern med modulen Configuration Manager-princip



## <a name="next-steps"></a>Nästa steg
Information om hur du installerar eller uppdaterar den tekniska för hands versionen finns i [teknisk för hands version för Configuration Manager](technical-preview.md).    
