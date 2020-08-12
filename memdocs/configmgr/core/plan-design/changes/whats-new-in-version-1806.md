---
title: Nyheter i version 1806
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 1806 av Configuration Manager aktuella grenen.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ae2846c2a5f7fea86287a05c8cc8f6013d660df6
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128958"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Vad är nytt i version 1806 av Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 1806 för Configuration Manager aktuella grenen är tillgänglig som en uppdatering i konsolen. Använd den här uppdateringen på webbplatser som kör version 1706, 1710 eller 1802. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Läs alltid den senaste check listan för att installera den här uppdateringen. Mer information finns i [Check lista för att installera uppdatering 1806](../../servers/manage/checklist-for-installing-update-1806.md). När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).

<!--
> [!Important]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
-->

Följande avsnitt innehåller information om ändringar och nya funktioner i version 1806 av Configuration Manager aktuella grenen.  



## <a name="deprecated-features-and-operating-systems"></a>Föråldrade funktioner och operativ system

Läs om support ändringar innan de implementeras i [borttagna och föråldrade objekt](deprecated/removed-and-deprecated.md).

Den 14 augusti 2018 är funktionen för hantering av hybrid mobila enheter inaktuell. Mer information finns i [vad hände med hybrid MDM](../../../mdm/understand/what-happened-to-hybrid.md).<!--Intune feature 2683117-->  

<!--
Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>Plats infrastruktur

### <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager har alltid tillhandahållit en stor centraliserad lagring av enhets data, som kunder använder för rapporterings syfte. Webbplatsen samlar vanligt vis in dessa data varje vecka. CMPivot är ett nytt konsol verktyg som nu ger till gång till real tids status för enheter i din miljö. Den kör omedelbart en fråga på alla aktuella anslutna enheter i mål samlingen och returnerar resultatet. Sedan kan du filtrera och gruppera dessa data i verktyget. Genom att tillhandahålla real tids data från online-klienter kan du snabbare besvara affärs frågor, felsöka problem och reagera på säkerhets incidenter. 

Mer information finns i [CMPivot](../../servers/manage/cmpivot.md).  


### <a name="site-server-high-availability"></a>Platsserver hög tillgänglighet
<!--1128774-->
Hög tillgänglighet för en fristående primär plats server roll är en Configuration Manager-baserad lösning för att installera ytterligare en plats server i passivt läge. Plats servern i passivt läge är utöver den befintliga plats servern i aktivt läge. En plats server i passivt läge är tillgänglig för omedelbar användning vid behov. 

Mer information finns i följande artiklar: 
- [Platsserver hög tillgänglighet](../../servers/deploy/configure/site-server-high-availability.md) 
- [Flödes schema – konfigurera en plats server i passivt läge](../../servers/deploy/configure/passive-site-server-flowchart.md)
- [Flödesschema – höj upp platsservern (planerat)](../../servers/deploy/configure/promote-site-server-flowchart.md)
- [Flödesschema – höj upp platsservern (oplanerat)](../../servers/deploy/configure/promote-site-server-unplanned-flowchart.md)


### <a name="improvements-to-management-insights"></a>Förbättringar av Management Insights
Den här versionen innehåller följande förbättringar av hanterings insikter:  

- Vissa hanterings insikter har nu möjlighet att vidta en åtgärd. Den här åtgärden navigerar till den associerade noden i-konsolen eller visar en filtrerad, fråge baserad vy.<!--1357930-->  

- En ny grupp för proaktivt underhåll är tillgänglig med sex nya regler, som hjälper dig att framhäva eventuella konfigurations problem för att undvika det vanliga underhållet.<!--1352184-->  

Mer information finns i [hanterings insikter](../../servers/manage/management-insights.md).


### <a name="configuration-manager-tools"></a>Configuration Manager-verktyg
<!--1357145-->
Configuration Manager Server-och klient verktyg ingår nu på servern. Hitta dem i `CD.Latest\SMSSETUP\Tools` mappen på plats servern. Ingen ytterligare installation krävs. 

Mer information finns i [Configuration Manager verktyg](../../support/tools.md).


### <a name="exclude-active-directory-containers-from-discovery"></a>Uteslut Active Directory behållare från identifiering
<!--1358143-->
Om du vill minska antalet identifierade objekt undantar du vissa behållare från Active Directory system identifiering. 

Mer information finns i [konfigurera Active Directory system identifiering](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_config-adsd).



## <a name="content-management"></a>Innehållshantering

### <a name="configure-a-remote-content-library-for-the-site-server"></a>Konfigurera ett fjärrinnehålls bibliotek för plats servern
<!--1357525-->
Om du vill konfigurera hög tillgänglighet för en plats Server eller frigöra hårddisk utrymme på den centrala administrations servern eller den primära plats servern, flytta innehålls biblioteket till en annan lagrings plats. Flytta innehålls biblioteket till en annan enhet på plats servern, en separat server eller feltoleranta diskar i en storage area network (SAN). 

Mer information finns i följande artiklar: 
- [Innehållsbibliotek](../hierarchy/the-content-library.md)
- [Flödesschema – hantera innehållsbiblioteket](../hierarchy/manage-content-library-flowchart.md)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Stöd för moln distributions plats för Azure Resource Manager
<!--1322209-->
När du skapar en distributions plats för molnet ger guiden nu möjlighet att skapa en **Azure Resource Manager distribution**. Azure Resource Manager är en modern plattform för att hantera alla lösnings resurser som en enda entitet, som kallas för en resurs grupp. När du distribuerar en moln distributions plats med Azure Resource Manager använder platsen Azure Active Directory för att autentisera och skapa nödvändiga moln resurser. Den här moderna distributionen kräver inte det klassiska hanterings certifikatet för Azure. 

Funktions dokumentationen för moln distributions platsen har också ändrats och förbättrats. Mer information finns i följande artiklar:
- [Använd en moln distributions plats](../hierarchy/use-a-cloud-based-distribution-point.md)   
- [Installera en moln distributions plats](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Mottagar distributions platser har stöd för moln distributions platser som källa  
<!--1321554-->
Många kunder använder mottagar distributions platser på fjärr-eller avdelnings kontor som laddar ned innehåll från en käll distributions plats via WAN. Om dina fjärranslutna kontor har en bättre anslutning till Internet, eller om du vill minska belastningen på dina WAN-länkar, kan du nu använda en moln distributions plats i Microsoft Azure som källa. När du lägger till en källa på fliken **mottagar distributions plats** i egenskaperna för distributions platsen, visas nu alla moln distributions platser på platsen som en tillgänglig distributions plats. Beteendet för båda plats system rollerna förblir i övrigt. 

Mer information finns i [använda en mottagar distributions](../hierarchy/use-a-pull-distribution-point.md)plats.


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>Aktivera distributions platser för att använda nätverks överbelastnings kontroll
<!--1358112-->
Windows Server med låg extra fördröjning i bakgrunds transport (LEDBAT) är en funktion i Windows Server som hjälper dig att hantera nätverks överföringar i bakgrunden. För distributions platser som körs på versioner av Windows Server som stöds aktiverar du ett alternativ för att justera nätverks trafiken. Klienter använder bara nätverks bandbredd när den är tillgänglig. 

Mer information finns i [Windows-LEDBAT](../hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat).


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Stöd för delvis hämtning i klient-peer-cache för att minska WAN-användningen
<!--1357346-->
Klientens peer-cache-källor kan nu dela upp innehåll i delar. Dessa delar minimerar nätverks överföringen för att minska WAN-användningen. Hanterings platsen ger en mer detaljerad spårning av innehålls delarna. Det försöker eliminera mer än en hämtning av samma innehåll per gränser grupp. 

Mer information finns i [stöd för partiell hämtning](../hierarchy/client-peer-cache.md#bkmk_parts). 


### <a name="boundary-group-options-for-peer-downloads"></a>Alternativ för gränser-grupp för peer-nedladdningar
<!--1356193-->
Gränser grupper innehåller nu ytterligare inställningar för att ge dig mer kontroll över innehålls distribution i din miljö. Den här versionen lägger till följande alternativ:  

- **Tillåt peer-nedladdningar i den här begränsnings gruppen**: hanterings platsen ger klienter en lista över innehålls platser som innehåller peer-källor. Den här inställningen påverkar också användning av grupp-ID: n för leverans optimering.  

- **Använd endast peer-datorer i samma undernät vid peer-hämtning**: hanterings platsen innehåller bara de peer-källor för innehålls platser som finns i samma undernät som klienten.  

Mer information finns i [gränser grupp alternativ för peer-nedladdningar](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="improvement-to-peer-cache-source-location-status"></a>Förbättringar av käll plats status för peer-cache
<!--SCCMDocs issue 850-->
Configuration Manager är mer effektivt att fastställa om en peer-cache-källa har roamat till en annan plats. Det här beteendet ser till att hanterings platsen erbjuder den som en innehålls källa till klienter på den nya platsen och inte på den gamla platsen. Om du använder funktionen peer-cache med centrala peer-cache-källor, efter att ha uppdaterat platsen till version 1806, uppdaterar du även alla peer-cache-källor till den senaste klient versionen. Hanterings platsen omfattar inte dessa peer cache-källor i listan över innehålls platser förrän de har uppdaterats till minst version 1806.

Mer information finns i [krav för peer-cache](../hierarchy/client-peer-cache.md#requirements).



<!-- ## Migration  -->



## <a name="client-management"></a>Klienthantering

### <a name="improvement-to-client-push-security"></a>Förbättra push-säkerhet för klienter
<!--1358204-->
När klientens push-metod används för att installera Configuration Manager-klienten, kan platsen nu kräva ömsesidig Kerberos-autentisering. Den här förbättringen hjälper till att skydda kommunikationen mellan servern och klienten. 

Mer information finns i [så här installerar du klienter med klient-push](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).


### <a name="enhanced-http-site-system"></a><a name="bkmk_ehttp"></a>Förbättrat HTTP-platssystem
<!--1356889,1358228-->
Att använda HTTPS-kommunikation rekommenderas för alla Configuration Manager kommunikations vägar, men kan vara utmanande för vissa kunder på grund av omkostnader för hantering av PKI-certifikat.

Den här versionen innehåller förbättringar av hur klienter kommunicerar med plats system. På fliken plats egenskaper, fliken **klient dator kommunikation** , väljer du alternativet för **https eller http**och aktiverar sedan det nya alternativet för att **använda Configuration Manager-genererade certifikat för http-plats system**. Den här funktionen är en [för hands versions funktion](../../servers/manage/pre-release-features.md).

Mer information finns i [Enhanced http](../hierarchy/enhanced-http.md).


### <a name="azure-ad-device-identity"></a>Enhets identitet för Azure AD 
<!--1358460-->
En [Azure AD-ansluten](/azure/active-directory/devices/concept-azure-ad-join) eller en [hybrid Azure AD-enhet](/azure/active-directory/devices/concept-azure-ad-join-hybrid) utan en Azure AD-användare som är inloggad kan kommunicera säkert med den tilldelade platsen. Den molnbaserade enhets identiteten räcker nu för att autentisera med CMG och hanterings platsen.  

Mer information finns i [Enhanced http](../hierarchy/enhanced-http.md).


### <a name="cmtrace-installed-with-client"></a>CMTrace installeras med klienten
<!--1357971-->
CMTrace-logg visnings verktyget installeras nu automatiskt tillsammans med Configuration Manager-klienten. Den läggs till i klient installations katalogen, vilket som standard är `%WinDir%\ccm\cmtrace.exe` . 

Mer information finns i [CMTrace](../../support/cmtrace.md).


### <a name="cloud-management-dashboard"></a>Instrument panel för moln hantering
<!--1358461-->
Den nya moln hanterings instrument panelen tillhandahåller en centraliserad vy för CMG-användning (Cloud Management Gateway). När platsen har registrerats med Azure AD visas även data om moln användare och enheter.   

Den här funktionen omfattar även **CMG-anslutnings analys** för verifiering i real tid för att under lätta fel sökningen. I konsol verktyget kontrol leras tjänstens aktuella status och kommunikations kanalen genom CMG anslutnings punkt till alla hanterings platser som tillåter CMG-trafik. 

Mer information finns i följande avsnitt i artikeln [övervaka CMG](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md) :  
- [Instrument panel för moln hantering](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#cloud-management-dashboard)  
- [Anslutnings analys](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#connection-analyzer)  


### <a name="improvements-to-cloud-management-gateway"></a>Förbättringar av Cloud Management Gateway

Version 1806 innehåller följande förbättringar av Cloud Management Gateway (CMG):

#### <a name="simplified-client-bootstrap-command-line"></a>Kommando rad för förenklad klient start
<!--1358215-->
När du installerar Configuration Manager-klienten på Internet via en CMG kräver kommando raden nu färre egenskaper. Den här förbättringen minskar storleken på den kommando rad som används i Microsoft Intune när du förbereder för samhantering. 

Mer information finns i [förbereda Internet-baserade enheter för samhantering](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).

#### <a name="download-content-from-a-cmg"></a>Hämta innehåll från en CMG
<!--1358651-->
Tidigare var du tvungen att distribuera en distributions plats för moln och CMG som separata roller. En CMG kan nu också hantera innehåll till klienter. Den här funktionen minskar de nödvändiga certifikaten och kostnaden för virtuella Azure-datorer. 

Mer information finns i [ändra en CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Ett betrott rot certifikat krävs inte med Azure AD
<!--503899-->
När du skapar en CMG behöver du inte längre ange ett [betrott rot certifikat](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) på sidan Inställningar. Detta certifikat krävs inte när du använder Azure Active Directory (Azure AD) för klientautentisering, men som används för att krävas i guiden. Om du använder certifikat för PKI-klientautentisering måste du fortfarande lägga till ett betrott rot certifikat till CMG.



## <a name="co-management"></a>Samhantering

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Synkronisera MDM-princip från Microsoft Intune för en samhanterad enhet
<!--1357377-->
När du växlar en samhanterings arbets belastning, synkroniserar de samhanterade enheterna automatiskt MDM-principen från Microsoft Intune. Den här synkroniseringen inträffar även när du startar åtgärden **Ladda ned dator princip** från klient meddelanden i Configuration Manager-konsolen. 

Mer information finns i [så här växlar du Configuration Manager-arbetsbelastningar till Intune](../../../comanage/how-to-switch-workloads.md).


### <a name="transition-new-workloads-to-intune-using-co-management"></a>Överföra nya arbets belastningar till Intune med hjälp av samhantering
Följande arbets belastningar kan nu övergå från Configuration Manager till Intune efter aktivering av samhantering:  

- **Enhetskonfiguration**<!--1357903-->: Med den här arbets belastningen kan du använda Intune för att distribuera MDM-principer och fortsätta att använda Configuration Manager för att distribuera program.  

- **Office 365**<!--1357841-->: Enheter installerar inte Office 365-distributioner från Configuration Manager.  

- **Mobilappar**<!--1357892-->: Alla tillgängliga appar som distribueras från Intune finns tillgängliga i Företagsportal. Appar som du distribuerar från Configuration Manager är tillgängliga i Software Center. Den här funktionen är en [för hands versions funktion](../../servers/manage/pre-release-features.md).  

Om du vill gå över dessa arbets belastningar går du till sidan Egenskaper för samhantering och flyttar skjutreglaget för arbets belastning från Configuration Manager till **pilot** eller **alla**. 

Mer information finns i [Co-Management för Windows 10-enheter](../../../comanage/overview.md).


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>Stöd för flera hierarkier till en Intune-klient
<!--1357944-->
Vissa kunder har flera Configuration Manager hierarkier och vill konsolidera i framtiden till en enda klient för Azure Active Directory och Microsoft Intune. Samhantering har nu stöd för att ansluta mer än en Configuration Manager-miljö till samma Intune-klient.

Mer information finns i [krav för samhantering](../../../comanage/overview.md#prerequisites).
 


## <a name="compliance-settings"></a>Kompatibilitetsinställningar

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Konfigurera Windows Defender SmartScreen-inställningar för Microsoft Edge
<!--1353701-->
Inställningen inställningar för Microsoft Edge-webbläsaren lägger till följande tre inställningar för Windows Defender SmartScreen: 
- Tillåt SmartScreen
- Användare kan åsidosätta SmartScreen-prompten för platser
- Användare kan åsidosätta SmartScreen-prompten för filer

Mer information finns i [Konfigurera Microsoft Edge-inställningar](../../../compliance/deploy-use/browser-profiles.md).


### <a name="scap-extensions"></a>SCAP-tillägg
<!--1357552-->
Konvertera SCAP-innehåll (Security Content Automation Protocol) till bas linjer för kompatibilitetsinställningar och skapa SCAP-rapporter med hjälp av ett konsol tillägg. Den här funktionen innehåller också en ny instrument panel som visualiserar klientens efterlevnad samt XCCDF. 





## <a name="application-management"></a>Programhantering

### <a name="phased-deployment-of-applications"></a>Stegvis distribution av program
<!--1358147-->
Skapa en stegvis distribution för ett program. Med stegvisa distributioner kan du dirigera en samordnad, sekvenserad distribution av program vara utifrån anpassningsbara kriterier och grupper. Du kan t. ex. distribuera programmet till en pilot samling och sedan fortsätta distributionen automatiskt baserat på lyckade villkor. 

Mer information finns i följande artiklar:  

- [Skapa en fasindelad distribution](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Hantera och övervaka fasindelade distributioner](../../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Etablera Windows-appaket för alla användare på en enhet
<!--1358310-->
Etablera ett program med ett Windows app-paket för alla användare på enheten. Ett vanligt exempel på det här scenariot är etablering av en app från Microsoft Store för företag och utbildning, till exempel Minecraft: Education Edition, för alla enheter som används av studenter i en skola. Tidigare Configuration Manager endast installera programmen per användare. När du har loggat in på en ny enhet skulle en student behöva vänta på att få åtkomst till en app. Nu när appen är etablerad till enheten för alla användare kan de vara produktivare snabbare. 

Mer information finns i [skapa Windows-program](../../../apps/get-started/creating-windows-applications.md#bkmk_provision).


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Office Customization Tool-integrering med Office 365-installations programmet
<!--1358149-->
Office-verktyget för anpassning är nu integrerat med Office 365-installations programmet i Configuration Manager-konsolen. När du skapar en distribution för Office 365 konfigurerar du de senaste Office-hanterbarhets inställningarna dynamiskt. Microsoft uppdaterar Office-anpassnings verktyget när nya versioner av Office 365 lanseras. Med den här integreringen kan du dra nytta av nya inställningar för hantering i Office 365 så snart de är tillgängliga. 

Mer information finns i [distribuera Office 365-appar](../../../sum/deploy-use/manage-office-365-proplus-updates.md).


### <a name="support-for-new-windows-app-package-formats"></a>Stöd för nya paket format för Windows-appar
<!--1357427-->
Configuration Manager stöder nu distribution av nya Windows 10-appaket (. msix) och app-paket (. msixbundle). 

Mer information finns i [skapa Windows-program](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).


### <a name="uninstall-application-on-approval-revocation"></a>Avinstallera program för åter kallelse av godkännande
<!--1357891-->
Beteendet har ändrats när du återkallar godkännande för ett program. Nu när du nekar begäran för programmet, avinstallerar klienten programmet från användarens enhet. Det här beteendet kräver att du aktiverar den [valfria funktionen](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Godkänn program begär Anden för användare per enhet**. 

Mer information finns i [distribuera program](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).


### <a name="package-conversion-manager"></a>Paketomvandlingshanteraren 
<!--1357861-->
Package Conversion Manager är nu ett integrerat verktyg som gör att du kan konvertera äldre paket till Configuration Manager aktuella gren program. Sedan kan du använda funktioner i program som beroenden, krav regler och mappning mellan användare och enhet.

Mer information finns i [Package Conversion Manager](../../../apps/pcm/package-conversion-manager.md).



## <a name="os-deployment"></a>Distribution av operativsystem

### <a name="improvements-to-phased-deployments"></a>Förbättringar i stegvisa distributioner

I den här versionen ingår följande förbättringar i stegvisa distributioner:  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>Skapa en stegvis distribution med manuellt konfigurerade faser
<!--1358148-->
För en aktivitetssekvens konfigurerar nu fasen manuellt när du skapar en stegvis distribution. Lägg till upp till 10 faser från fliken **faser** i guiden skapa stegvis distribution. Du kan fortfarande automatiskt skapa en standard distribution i två faser. 

Mer information finns i [skapa en stegvis distribution med manuellt konfigurerade faser](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_manual).

#### <a name="phased-deployment-status"></a>Status för stegvis distribution
<!--1358577-->
Stegvisa distributioner har nu en inbyggd övervaknings upplevelse. Välj en stegvis distribution i noden **distributioner** på arbets ytan **övervakning** och klicka sedan på status för stegvis **distribution** i menyfliksområdet. 

Mer information finns i [Hantera och övervaka stegvisa distributioner](../../../osd/deploy-use/manage-monitor-phased-deployments.md).  

#### <a name="gradual-rollout-during-phased-deployments"></a>Gradvis distribution under stegvis distribution
<!--1358578-->
Under en stegvis distribution kan distributionen i varje fas nu ske gradvis. Det här beteendet minskar risken för distributions problem och minskar belastningen på nätverket som orsakas av distribution av innehåll till klienter. Platsen kan gradvis göra program varan tillgänglig beroende på konfigurationen för varje fas. Varje klient i en fas har en tids gräns i förhållande till den tid då program varan görs tillgänglig. Tidsfönstret mellan den tillgängliga tiden och tids gränsen är samma för alla klienter i en fas. 

Mer information finns i [fas inställningar](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_settings).  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Förbättringar av aktivitetssekvens för Windows 10-uppgradering på plats
<!--1358500-->
Standard mal len för aktivitetssekvenser för Windows 10 uppgradering på plats innehåller nu en annan ny grupp med rekommenderade åtgärder som du kan lägga till om uppgraderingen Miss lyckas. De här åtgärderna gör det enklare att felsöka. Ett sådant verktyg är Windows- [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). Det är ett fristående diagnostikverktyg för att få information om varför en Windows 10-uppgradering misslyckades. 

Mer information finns i [skapa en aktivitetssekvens för att uppgradera ett operativ system](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-on-failure).


### <a name="improvements-to-pxe-enabled-distribution-points"></a>Förbättringar av PXE-aktiverade distributions platser
<!--1357580-->
På fliken **PXE** i egenskaperna för distributions platsen markerar du **Aktivera en PXE-svarare utan Windows Deployment-tjänst**. Det här nya alternativet aktiverar en PXE-svarare på distributions platsen, vilket inte kräver Windows Deployment Services (WDS). Eftersom WDS inte krävs kan den PXE-aktiverade distributions platsen vara en klient eller ett server-OS, inklusive Windows Server Core. Den här nya PXE responder-tjänsten stöder IPv6 och förbättrar även flexibiliteten i PXE-aktiverade distributions platser på fjärranslutna kontor. 

Mer information finns i [Aktivera PXE på distributions platsen](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="network-access-account-not-required-for-some-scenarios"></a>Kontot för nätverks åtkomst krävs inte för vissa scenarier
<!--1358278,1358279-->
Funktionen [utökad HTTP-platssystem](#bkmk_ehttp) tar också bort vissa beroenden på kontot för nätverks åtkomst. När du aktiverar alternativet för nya webbplatser **för att använda Configuration Manager-genererade certifikat för HTTP-plats system**behöver inte följande scenarier ett konto för nätverks åtkomst för att ladda ned innehåll från en distributions plats:  

- Aktivitetssekvenser som körs från startmedia eller PXE
- Aktivitetssekvenser som körs från Software Center  

Dessa aktivitetssekvenser kan vara för distribution av operativ system eller anpassade. Det finns också stöd för arbets grupps datorer.

Mer information finns i [aktivitetssekvenser och kontot för nätverks åtkomst](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).


### <a name="other-improvements-to-os-deployment"></a>Andra förbättringar av OS-distributionen

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>Maskera känsliga data som lagras i variabler för aktivitetssekvens
 <!--1358330-->
 I **variabel steget Ställ in aktivitetssekvens** väljer du det nya alternativet för att **inte Visa det här värdet**. 

 Mer information finns i [ange variabel](../../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)för aktivitetssekvens. 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>Maskera program namn under körnings kommando steg i en aktivitetssekvens
 <!--1358493-->
 Om du vill förhindra att potentiellt känsliga data visas eller loggas konfigurerar du variabeln **OSDDoNotLogCommand**i aktivitetssekvensen.  

 Mer information finns i [variabler för aktivitetssekvens](../../../osd/understand/task-sequence-variables.md#OSDDoNotLogCommand). 

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>Variabeln aktivitetssekvens för DISM-parametrar vid installation av driv rutiner
 <!--516679/2840016-->
 Om du vill ange ytterligare kommando rads parametrar för DISM använder du den nya variabeln **OSDInstallDriversAdditionalOptions**i aktivitetssekvensen. 

 Mer information finns i [variabler för aktivitetssekvens](../../../osd/understand/task-sequence-variables.md#OSDInstallDriversAdditionalOptions). 

#### <a name="option-to-use-full-disk-encryption"></a>Alternativ för att använda fullständig disk kryptering
 <!--SCCMDocs-pr issue 2671-->
 Både **Aktivera BitLocker** och **Företablera BitLocker** -stegen innehåller nu ett alternativ för att **använda fullständig disk kryptering**. Som standard krypterar du använt utrymme på enheten. Detta är standard beteendet rekommenderas eftersom det är snabbare och mer effektivt. 

 Mer information finns i [Aktivera BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker) och [Företablera BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker). 

#### <a name="client-provisioning-mode-isnt-enabled-with-windows-10-upgrade-compatibility-scan"></a>Klient etablerings läget är inte aktiverat med Windows 10 Upgrade Compatibility scanning
 <!--SCCMDocs-pr issue 2812-->
 Nu när du aktiverar alternativet för att **utföra installationsprogrammet för Windows kompatibilitetskontroll utan att starta uppgraderingen**, försätts inte steget **uppgradera operativ system** Configuration Manager klienten i etablerings läge.

 Mer information finns i [Uppgradera operativ system](../../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS).

#### <a name="revised-documentation-for-task-sequence-variables"></a>Ändrad dokumentation för variabler i aktivitetssekvens
Två nya artiklar är nu tillgängliga för att förstå variabler i aktivitetssekvensen:  

- [Så här använder du variabler för aktivitetssekvens](../../../osd/understand/using-task-sequence-variables.md) är en ny artikel som beskriver de olika typerna av variabler, metoder för att ange variabler och hur du kommer åt dem.  

- [Variabler för aktivitetssekvens](../../../osd/understand/task-sequence-variables.md) är en referens för alla tillgängliga variabler för aktivitetssekvens. Den här artikeln kombinerar de föregående artiklarna, vilka separerade inbyggda variabler från variabla variabler. 



## <a name="software-center"></a>Software Center

> [!Important]  
> Om du vill dra nytta av nya Configuration Manager funktioner måste du först uppdatera klienter till den senaste versionen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.


### <a name="software-center-infrastructure-improvements"></a>Förbättringar av Software Center-infrastrukturen
<!--1358309-->
Program katalog roller krävs inte längre för att Visa användar tillgängliga program i Software Center. Den här ändringen hjälper dig att minska Server infrastrukturen som krävs för att leverera program till användare. Software Center använder nu hanterings platsen för att hämta den här informationen, vilket hjälper större miljöer att skala bättre genom att tilldela dem till [gräns grupper](../../servers/deploy/configure/boundary-groups.md#management-points).

Mer information finns i [Konfigurera Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)  

> [!Note]  
> Rollerna webbplats för program katalog och webb tjänst punkt *krävs* inte längre i 1806, men *stöds* fortfarande roller. 
> 
> **Användar upplevelsen för Silverlight** för program katalogens webbplats stöds inte längre. Mer information finns i [borttagna och föråldrade funktioner](deprecated/removed-and-deprecated-cmfeatures.md).  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Ange synlighet för länken till program katalogens webbplats i Software Center
<!--1358214-->
Använd klient inställningar för att kontrol lera om länken för att **öppna programkatalog webbplats** visas i noden **installations status** i Software Center.  

Mer information finns i [klient inställningar för Software Center](../../clients/deploy/about-client-settings.md#software-center).

> [!Note]  
> **Användar upplevelsen för Silverlight** för program katalogens webbplats stöds inte längre. Mer information finns i [borttagna och föråldrade funktioner](deprecated/removed-and-deprecated-cmfeatures.md).  


### <a name="custom-tab-for-webpage-in-software-center"></a>Anpassad flik för webb sida i Software Center
<!--1358132-->
Använd klient inställningar för att skapa en anpassad flik för att öppna en webb sida i Software Center. Med den här funktionen kan du Visa innehåll till dina slutanvändare på ett konsekvent och tillförlitligt sätt. Följande lista innehåller några exempel:  

- Kontakta IT-avdelningen: information om hur du kontaktar din organisations IT-avdelning  

- Support Center: IT-självbetjänings åtgärder som att söka i en kunskaps bas eller öppna ett support ärende.  

- Dokumentation om slutanvändare: artiklar om användare i din organisation på olika IT-ämnen, till exempel att använda program eller uppgradera till Windows 10.  

Mer information finns i [klient inställningar för Software Center](../../clients/deploy/about-client-settings.md#software-center) och [Användar handbok för Software Center](../../understand/software-center.md).


### <a name="maintenance-windows-in-software-center"></a>Underhålls fönster i Software Center
<!--1358131-->
I Software Center visas nu nästa schemalagda underhålls period. På fliken installations status växlar du vyn från alla till kommande. Det visar tidsintervallet och listan över distributioner som är schemalagda. Om det inte finns några framtida underhålls fönster är listan tom. 

Mer information finns i [använda underhålls](../../clients/manage/collections/use-maintenance-windows.md) perioder och [användar guiden för Software Center](../../understand/software-center.md).



## <a name="software-updates"></a>Programuppdateringar

### <a name="third-party-software-updates"></a>Programuppdateringar från tredje part
<!--1357605, 1352101, 1358714-->
Program uppdateringar från tredje part gör att du kan prenumerera på partner kataloger i Configuration Manager-konsolen och publicera uppdateringarna på WSUS. Du kan sedan distribuera dessa uppdateringar med den befintliga processen för hantering av program uppdateringar. 

Mer information finns i [Aktivera uppdateringar från tredje part](../../../sum/deploy-use/third-party-software-updates.md).


### <a name="deploy-software-updates-without-content"></a>Distribuera program uppdateringar utan innehåll
<!--1357933-->
Distribuera program uppdateringar till enheter utan att först hämta och distribuera innehåll till distributions platser. Den här funktionen är fördelaktig vid hantering av mycket stort uppdaterings innehåll eller om du alltid vill att klienter ska hämta innehåll från Microsoft Update moln tjänsten. Klienter i det här scenariot kan också hämta innehåll från peer-datorer som redan har det innehåll som krävs. Den Configuration Manager klienten fortsätter att hantera innehålls hämtningen och kan därför använda funktionen Configuration Manager peer-cache eller andra tekniker som leverans optimering. Den här funktionen stöder alla uppdaterings typer som stöds av Configuration Manager hantering av program uppdateringar, inklusive Windows-och Office-uppdateringar. 

Mer information finns i alternativet **ingen distributions paket** när du [distribuerar program uppdateringar manuellt](../../../sum/deploy-use/manually-deploy-software-updates.md) eller [automatiskt distribuerar program uppdateringar](../../../sum/deploy-use/automatically-deploy-software-updates.md).


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrera regler för automatisk distribution efter program uppdaterings arkitektur
 <!--1322266-->
Nu kan du filtrera regler för automatisk distribution (ADR) för att utesluta arkitekturer som Itanium och ARM64. På sidan **program uppdateringar** i guiden Skapa regel för automatisk distribution är **arkitektur** egenskaps filtret nu tillgängligt. 

Mer information finns i [distribuera program uppdateringar automatiskt](../../../sum/deploy-use/automatically-deploy-software-updates.md).


### <a name="improved-wsus-maintenance"></a>Förbättrat WSUS-underhåll 
<!--1357898-->
Rensnings guiden för WSUS avvisar nu uppdateringar som har upphört att gälla enligt de ersättnings regler som definierats för komponent egenskaperna för program uppdaterings platsen. 

Mer information finns i [underhåll av program uppdateringar](../../../sum/deploy-use/software-updates-maintenance.md).



## <a name="reporting"></a>Rapportering

### <a name="new-software-updates-compliance-report"></a>Ny Kompatibilitetsrapport för program uppdateringar
<!--1357775-->
Att visa rapporter om kompatibilitet med program uppdateringar innehåller traditionellt sett data från klienter som inte nyligen har kontaktat platsen. Med en ny rapport, **kompatibilitet 9 – övergripande hälso tillstånd och efterlevnad**kan du filtrera kompatibilitetsstatus för en bestämd program uppdaterings grupp med "friska" klienter. Den här rapporten visar det mer realistiska kompatibilitetstillstånd för aktiva klienter i din miljö. 

Mer information finns i [program uppdaterings rapporter](../../../sum/deploy-use/monitor-software-updates.md#BKMK_SUReports).



## <a name="inventory"></a>Inventering

### <a name="improvement-to-hardware-inventory-for-large-integer-values"></a><a name="bkmk_bigint"></a>Förbättring av maskin varu inventering för stora heltals värden
<!--1357880-->
Maskin varu inventeringen hade tidigare en gräns för heltal som är större än 4 294 967 296 (2 ^ 32). Den här gränsen kan nås för attribut som hård disk storlekar i byte. Hanterings platsen bearbetar inte heltals värden över den här gränsen, vilket innebär att inget värde lagrades i databasen. I den här versionen ökas gränsen till 18446744073709551616 (2 ^ 64). 

Mer information finns i [användandet av stora heltals värden](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md#bkmk_bigint).


### <a name="hardware-inventory-default-unit-revision"></a>Standard enhets revision för maskin varu inventering
<!--514442-->
I [Configuration Manager version 1710](whats-new-in-version-1710.md#site-infrastructure), har standard enheten som används i många rapportfunktioner ändrats från megabyte (MB) till gigabyte (GB). På grund av [förbättringar av maskin varu inventeringen för stora heltals värden](#bkmk_bigint)och utifrån kundfeedback, är standardenheten nu MB igen.



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Configuration Manager-konsolen

### <a name="product-lifecycle-dashboard"></a>Instrument panel för produkt livs cykel
<!--1319632-->
Instrument panelen för produktens livs cykel visar statusen för Microsofts livs cykel princip för Microsoft-produkter som är installerade på enheter som hanteras med Configuration Manager. Du får också information om Microsoft-produkter i din miljö, support tillstånd och slutdatum för support. Använd instrument panelen för att förstå tillgängligheten för varje produkt. Den här informationen hjälper dig att planera för när du ska uppdatera de Microsoft-produkter som du använder innan deras aktuella slut på support nås.   

Mer information finns i [instrument panelen för produktens livs cykel](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


### <a name="copy-asset-details-from-monitoring-views"></a>Kopiera till gångs information från övervaknings Visa vyer
<!--1357856-->
Följande områden i arbets ytan **övervakning** stöder nu kopiering av text:  

- I noden **distributioner** väljer du en distribution och klickar på **Visa status**. I fönstret **till gångs information** i vyn distributions status väljer du en eller flera enheter.  

- Expandera noden **distributions status** och välj **innehålls status**. Välj en program varu enhet och klicka på **Visa status**. I fönstret **till gångs information** i vyn innehålls status väljer du en eller flera distributions platser. 

Högerklicka på till gången och välj **Kopiera**. Den här åtgärden kopierar de valda till gångarna som en kommaavgränsad lista som innehåller all information. Kortkommandot **CTRL**  +  **C** fungerar också i dessa vyer. 

Mer information finns i [konsol förbättringar i version 1806](../../servers/manage/admin-console-tips.md#copy-details-in-monitoring-views).


### <a name="improvements-to-the-surface-dashboard"></a>Förbättringar av Surface-instrumentpanelen
<!--1358654-->
Den här versionen innehåller följande förbättringar av Surface-instrument panelen:  

- På Surface-instrumentpanelen visas nu en lista över relevanta enheter när du väljer vissa diagram avsnitt:  

   - Om du klickar på panelen **procent av Surface-enheter** öppnas en lista över Surface-enheter.  

   - Om du klickar på en stapel i den **fem översta panelen inbyggda versioner av inbyggd program vara** öppnas en lista över Surface-enheter med den aktuella versionen av den inbyggda program  

- När du visar dessa enhets listor på Surface-instrumentpanelen högerklickar du på en enhet för att utföra vanliga åtgärder.  

Mer information finns i [instrument panelen för Surface](../../clients/manage/surface-device-dashboard.md).


### <a name="view-the-currently-signed-on-user-for-a-device"></a>Visa den för tillfället inloggade användaren för en enhet
<!--1358202-->
Nu visar noden **enheter** i arbets ytan **till gångar och efterlevnad** en kolumn för den **för tillfället inloggade användaren**. Den visas också för alla samlingar med olika enhets listor. Värdet är lika aktuellt som [klientens status](../../clients/manage/monitor-clients.md#bkmk_indStatus). När användaren loggar ut rensas detta värde av klienten. Om ingen användare är inloggad är värdet tomt. 

Mer information finns i [konsol förbättringar i version 1806](../../servers/manage/admin-console-tips.md#view-users-for-a-device).


### <a name="submit-feedback-from-the-configuration-manager-console"></a>Skicka feedback från Configuration Manager-konsolen  
<!--1357542-->

Skicka ett leende! Nu kan du direkt tala om för Configuration Manager teamet om dina upplevelser. Det är enkelt att skicka feedback från Configuration Manager-konsolen. Vi vill gärna höra all feedback: Praise, problem och förslag. I Configuration Manager-konsolen klickar du på knappen leende i det övre högra hörnet ovanför menyfliksområdet. Den här feedbacken går direkt till Microsofts produkt team för Configuration Manager. När du använder Windows 10 feedback Hub, rekommenderar vi att du använder återkopplings funktionen i konsolen.  

Mer information finns i [konsol förbättringar i version 1806](../../servers/manage/admin-console-tips.md#send-feedback) och [produkt feedback](../../understand/find-help.md#BKMK_1806Feedback).



## <a name="other-updates"></a>Övriga uppdateringar

Förutom nya funktioner innehåller den här versionen även ytterligare ändringar som fel korrigeringar. Mer information finns i [Sammanfattning av ändringar i Configuration Manager aktuella grenen, version 1806](https://support.microsoft.com/help/4459701).

Mer information om ändringar i Windows PowerShell-cmdletar för Configuration Manager finns i [versions anmärkningar för PowerShell 1806](https://docs.microsoft.com/powershell/sccm/1806_release_notes?view=sccm-ps).

Följande samlade uppdateringar (4462978) är tillgängliga i-konsolen från och med 24 oktober 2018: [Samlad uppdatering för Configuration Manager aktuell gren, version 1806](https://support.microsoft.com/help/4462978).


### <a name="hotfixes"></a>Snabbkorrigeringar

Följande ytterligare snabb korrigeringar är tillgängliga för att åtgärda specifika problem:

| ID | Rubrik | Datum | I-konsolen |
|---------|---------|---------|---------|
| [4346645](https://support.microsoft.com/help/4346645) | Uppdatering för Configuration Manager version 1806, första vågen | 31 augusti 2018 | Ja |
| [4465865](https://support.microsoft.com/help/4465865) | Program uppdateringar laddas inte ned i Configuration Managers miljö om WSUS är frånkopplat<br><br>Den här uppdateringen ingår också i den samlade uppdateringen (4462978) | 01 oktober 2018 | Ja |
| [4471892](https://support.microsoft.com/help/4471892) | PXE-Responder fungerar inte över undernät i Configuration Manager 1806 | 23 november 2018 | No |
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune anslutnings certifikat förnyas inte i Configuration Manager | 18 januari 2019 | Ja |


## <a name="next-steps"></a>Nästa steg

När du är redo att installera den här versionen, se [Installera uppdateringar för Configuration Manager](../../servers/manage/updates.md) och [Check lista för att installera uppdatering 1806](../../servers/manage/checklist-for-installing-update-1806.md).

> [!TIP]  
> Om du vill installera en ny plats använder du en bas linje version av Configuration Manager.  
>
> Läs mer om:    
> - [Nya platser installeras](../../servers/deploy/install/installing-sites.md)  
> - [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines)

För kända, betydande problem, se [viktig information](../../servers/deploy/install/release-notes.md).

När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).
