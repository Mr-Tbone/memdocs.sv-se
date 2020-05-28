---
title: Nyheter i version 1810
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 1810 av Configuration Manager aktuella grenen.
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2a3b322f868c5c203114de4d974ba6682272c5d7
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906255"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Vad är nytt i version 1810 av Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 1810 för Configuration Manager aktuella grenen är tillgänglig som en uppdatering i konsolen. Använd den här uppdateringen på webbplatser som kör version 1710, 1802 eller 1806. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.--> I den här artikeln sammanfattas ändringar och nya funktioner i Configuration Manager version 1810.  

Läs alltid den senaste check listan för att installera den här uppdateringen. Mer information finns i [Check lista för att installera uppdatering 1810](../../servers/manage/checklist-for-installing-update-1810.md). När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist).

Om du vill dra nytta av nya Configuration Manager funktioner måste du först uppdatera klienter till den senaste versionen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.

<!--
> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized. 
-->  

> [!Tip]  
> Om du vill få ett meddelande när den här sidan uppdateras kopierar du och klistrar in följande URL i din RSS-feed läsare:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1810+-+Configuration+Manager%22&locale=en-us`



## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a>Föråldrade funktioner och operativ system

Läs om support ändringar innan de implementeras i [borttagna och föråldrade objekt](deprecated/removed-and-deprecated.md).

Från den 14 augusti 2018 är funktionen för hantering av hybrid mobila enheter inaktuell. Mer information finns i [vad hände med hybrid MDM](../../../mdm/understand/what-happened-to-hybrid.md).<!--Intune feature 2683117-->  

Stöd för System Center Endpoint Protection (SCEP) för Mac och Linux (alla versioner) upphör den 31 december 2018. Tillgänglighet för nya virus definitioner för SCEP för Mac och SCEP för Linux kan komma att upphöra efter Supportens slut. Mer information finns i [blogg inlägget End of support](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257).

Klassiska tjänst distributioner i Azure är nu föråldrade i Configuration Manager. Börja använda Azure Resource Manager distributioner för Cloud Management Gateway och moln distributions platsen. Mer information finns i [plan for CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).



## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Plats infrastruktur

### <a name="support-for-windows-server-2019"></a>Stöd för Windows Server 2019

<!--1359195-->
Configuration Manager stöder nu Windows Server 2019 och Windows Server, version 1809, som plats system.

Mer information finns i [operativ system som stöds för plats system servrar](../configs/supported-operating-systems-for-site-system-servers.md).


### <a name="hierarchy-support-for-site-server-high-availability"></a>Stöd för hierarki för plats serverns hög tillgänglighet

<!--3607755, fka 1358224-->
Centrala administrations platser och underordnade primära platser kan nu ha ytterligare en plats server i passivt läge.

Mer information finns i [hög tillgänglighet för plats Server](../../servers/deploy/configure/site-server-high-availability.md).


### <a name="improvements-to-setup-prerequisites"></a>Förbättringar av installations kraven

När du installerar eller uppdaterar till version 1810 innehåller Configuration Manager installations programmet nu eller förbättrar följande krav kontroller:

- **Väntande**omstart av systemet: den här krav kontrollen är nu mer elastisk. Den kontrollerar ytterligare register nycklar för Windows-funktioner. Mer information finns i [väntan på omstart av systemet](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart). <!--SCCMDocs-pr issue 3010-->  

- **Rensning av SQL-ändrings spårning**: en ny kontroll om plats databasen har en efter släpning av SQL Change tracking-data. Mer information, inklusive en procedur för att kontrol lera och ta bort den här efter släpning, finns i [rensning av SQL ändrings spårning](../../servers/deploy/install/list-of-prerequisite-checks.md#bkmk_changetracking). <!--SCCMDocs-pr issue 3023-->  

- **SQL Native Client version**: den här krav kontrollen har uppdaterats för versioner av SQL Native Client som stöder TLS 1,2. Den lägsta versionen är [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402). Mer information finns i [SQL Native Client version](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client). <!--SCCMDocs-pr issue 3094-->  

- **Plats system på Windows-klusternod**: installations processen för Configuration Manager blockerar inte längre installationen av plats Server rollen på en dator med Windows-rollen för redundanskluster. SQL Always on kräver den här rollen, så det var tidigare att du inte kunde hitta plats databasen på plats servern. Med den här ändringen kan du skapa en plats med hög tillgänglighet med färre servrar med hjälp av SQL Always on och en plats server i passivt läge. Mer information finns i [Windows-redundanskluster](../../servers/deploy/install/list-of-prerequisite-checks.md#windows-failover-cluster). <!--1359132-->  


### <a name="new-permission-for-client-notification-actions"></a>Ny behörighet för klient meddelande åtgärder

<!--SCCMDocs-pr issue #2972-->
Klient aviserings åtgärder kräver nu behörigheten **meddela resurs** för SMS_Collection-klassen. Följande inbyggda roller har den här behörigheten som standard:

- Fullständig administratör  
- Infrastrukturadministratör  

Lägg till den här behörigheten till alla anpassade roller som behöver använda klient aviserings åtgärder.

Mer information finns i [klient meddelanden](../../clients/manage/client-notification.md).



## <a name="content-management"></a><a name="bkmk_content"></a>Innehålls hantering

### <a name="new-boundary-group-options"></a>Nya alternativ för gränser grupp

<!--1358749-->
I gränser grupper ingår nu följande ytterligare inställningar för att ge dig mer kontroll över innehålls distribution i din miljö:

- **Föredra distributions platser över peer-datorer med samma undernät**: hanterings platsen prioriterar peer-cache-källor överst i listan med innehålls platser. Den här inställningen återför den prioriteten för klienter som finns i samma undernät som peer-cachens källa.  

- **Föredra moln distributions platser över distributions platser**: om du har ett avdelnings kontor med en snabbare Internet-länk kan du nu prioritera moln innehåll.  

Mer information finns i [gränser grupp alternativ för peer-nedladdningar](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>Hanterings insikts regel för klient version för peer-cache-källa

<!-- 1358008 -->
Noden för **hanterings insikter** har en ny regel för att identifiera klienter som fungerar som peer-cache-källa, men som inte har uppgraderats från en klient version före 1806. Den nya regeln **uppgraderar peer cache-källor till den senaste versionen av Configuration Manager-klienten**och ingår i den nya **proaktiva underhålls** regel gruppen. Det går inte att använda pre-1806-klienter som peer-cache-källa för klienter som kör version 1806 eller senare. Välj **vidta åtgärd** för att öppna en enhets vy som visar listan över klienter.

Mer information finns i [hanterings insikter](../../servers/manage/management-insights.md).



## <a name="client-management"></a><a name="bkmk_client"></a>Klient hantering

### <a name="new-client-notification-action-to-wake-up-device"></a>Ny klient meddelande åtgärd för aktivering av enhet

<!--1317364-->
Du kan nu aktivera klienter från Configuration Manager-konsolen, även om klienten inte finns i samma undernät som plats servern. Om du behöver utföra underhåll eller fråga enheter är du inte begränsad av fjärranslutna klienter som är i ström spar läge. Plats servern använder klient meddelande kanalen för att identifiera en annan klient som är aktiv i samma fjärrundernät. Den aktiva klienten skickar sedan en begäran om Wake-on-LAN (Magic Packet).

Mer information finns i [Konfigurera Wake on LAN](../../clients/deploy/configure-wake-on-lan.md) och [aktivera klienter](../../clients/deploy/plan/plan-wake-up-clients.md).

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>Nytt alternativ för att utföra klient meddelanden från noden enheter

<!--1317364-->
Upp till 1810 var **klient meddelande** alternativet endast tillgängligt från antingen noden enhets samling eller när du visade medlemskap i en enhets samling. Nu kan du utföra ett **klient meddelande** från noden **enheter** direkt. Det finns inte längre något krav på att det ska finnas i en samlings medlemskaps vy.

Mer information finns i [klient meddelanden](../../clients/manage/client-notification.md).


### <a name="improvements-to-collection-evaluation"></a>Förbättringar av samlings utvärdering

<!--3607726, fka 1358981-->
Följande ändringar i samlingens utvärderings beteende kan förbättra plats prestandan:  

- När du tidigare konfigurerade ett schema för en certifikatbaserad samling, fortsätter platsen att utvärdera frågan oavsett om du har aktiverat samlings inställningen för att **Schemalägga en fullständig uppdatering av den här samlingen**. Om du vill inaktivera schemat fullständigt, var du tvungen att ändra schemat till **inget**. Nu rensar platsen schemat när du inaktiverar den här inställningen. Om du vill ange ett schema för samlings utvärdering aktiverar du alternativet för att **Schemalägga en fullständig uppdatering av den här samlingen**.  

- Du kan inte inaktivera utvärderingen av inbyggda samlingar som **alla system**, men nu kan du konfigurera schemat. Med det här beteendet kan du anpassa den här åtgärden i en tid som uppfyller dina affärs behov.

Mer information finns i [så här skapar du samlingar](../../clients/manage/collections/create-collections.md#bkmk_create).


### <a name="improvement-to-client-installation"></a>Förbättra klient installationen

<!--1358840-->
När du installerar Configuration Manager-klienten kontaktar CCMSetup-processen hanterings platsen för att hitta nödvändigt innehåll. Tidigare i den här processen returnerar hanterings platsen endast distributions platser i klientens aktuella gränser grupp. Om inget innehåll är tillgängligt kommer installations processen att gå tillbaka för att ladda ned innehåll från hanterings platsen. Det finns inget alternativ för att återgå till distributions platser i andra gränser grupper som kan ha nödvändigt innehåll. Nu returnerar hanterings platsen distributions platser baserat på konfigurationen av gränser gruppen.

Mer information finns i [Konfigurera gränser grupper](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup).



## <a name="co-management"></a><a name="bkmk_comgmt"></a>Samhantering

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>Nödvändig app-efterlevnadsprincip för samhanterade enheter

<!--1358196-->
Definiera regler för policyer för efterlevnad i Configuration Manager för nödvändiga program. Den här program utvärderingen är en del av det övergripande kompatibilitetstillstånd som skickas till Microsoft Intune för samhanterade enheter.

Mer information finns i [arbets belastningar för samhantering](../../../comanage/workloads.md).


### <a name="improvement-to-co-management-dashboard"></a>Förbättringar av instrument panelen för samhantering

<!--1358980-->
Instrument panelen för samhantering har förbättrats med följande mer detaljerad information:  

- I panelen för **registrering av samhanterings status** ingår ytterligare tillstånd

- En ny panel för **samhanterings status** med ett trattdiagram visar tillstånd för registrerings processen

- En ny panel med antal **registrerings fel**

![Skärm bild för samhanterings instrument panel som visar de fyra översta panelerna](media/1358980-comgmt-dashboard.png)

Mer information finns i [instrument panelen för samhantering](../../../comanage/how-to-monitor.md#co-management-dashboard).


### <a name="improvements-to-internet-based-client-setup"></a>Förbättringar av Internetbaserad klient installation

<!--3607731, fka 1359181-->
Den här versionen fören klar den Configuration Manager klient installations processen för klienter på Internet. Platsen publicerar ytterligare Azure Active Directory (Azure AD)-information till Cloud Management Gateway (CMG). En Azure AD-ansluten klient hämtar den här informationen från CMG under CCMSetup-processen och använder samma klient organisation som den är ansluten till. Det här beteendet fören klar registreringen av enheter till samhantering i en miljö med fler än en Azure AD-klient. Nu är de enda två obligatoriska CCMSetup-egenskaperna **CCMHOSTNAME** och **SMSSiteCode**.

Mer information finns i [förbereda Internet-baserade enheter för samhantering](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).



## <a name="application-management"></a><a name="bkmk_app"></a>Program hantering

### <a name="convert-applications-to-msix"></a>Konvertera program till MSIX

<!--3607729, fka 1359029-->
Från och med version 1806 stöder Configuration Manager distribution av det nya Windows 10-Appaketet (. msix)-formatet. Nu kan du konvertera dina befintliga Windows Installer-program (. msi) till MSIX-format.

Mer information finns i [skapa Windows-program](../../../apps/get-started/creating-windows-applications.md#bkmk_msix).  


### <a name="repair-applications"></a>Reparera program

<!--1357866-->
Ange en reparations kommando rad för Windows Installer och skript installations distributions typer. Om du aktiverar alternativet i distributionen är en ny knapp tillgänglig i Software Center för att **Reparera** programmet. När du konfigurerar ett program med ett reparations program kan användarna starta kommandot från Software Center.

Mer information finns i [skapa program](../../../apps/deploy-use/create-applications.md#bkmk_dt-content) och [distribuera program](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).


### <a name="approve-application-requests-via-email"></a>Godkänn program begär Anden via e-post

<!--1321550-->
Konfigurera e-postaviseringar för begäran om program godkännande. När en användare begär ett program får du ett e-postmeddelande. Klicka på länkar i e-postmeddelandet för att godkänna eller neka begäran, utan att behöva Configuration Manager-konsolen.

Mer information finns i [godkänna program](../../../apps/deploy-use/app-approval.md).


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>Identifierings metoder läser inte in Windows PowerShell-profiler

<!--3607762, fka 1359239-->
Du kan använda Windows PowerShell-skript för att upptäcka identifierings metoder för program och inställningar i konfigurations objekt. När dessa skript körs på-klienter anropar Configuration Manager-klienten PowerShell med `-NoProfile` parametern. Det här alternativet startar PowerShell utan profiler.

En PowerShell-profil är ett skript som körs när PowerShell startar. Du kan skapa en PowerShell-profil för att anpassa din miljö och lägga till sessionsbaserade element till varje PowerShell-session som du startar.

> [!Note]  
> Den här ändrings funktionen gäller inte för [skript](../../../apps/deploy-use/create-deploy-scripts.md) eller [CMPivot](../../servers/manage/cmpivot.md). Båda dessa funktioner använder redan denna PowerShell-parameter.  

Mer information finns i [skapa program](../../../apps/deploy-use/create-applications.md) och [skapa anpassade konfigurations objekt](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).



## <a name="os-deployment"></a><a name="bkmk_osd"></a>OS-distribution

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>Aktivitetssekvens stöd för Windows autopilot för befintliga enheter

<!--3607717, fka 1358333-->
[Windows autopilot för befintliga enheter](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) är nu tillgängligt med Windows 10, version 1809 eller senare. Med den här nya funktionen kan du återställa avbildningen och etablera en Windows 7-enhet för [Windows autopilot-](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) användarläge med hjälp av en enda, inbyggd Configuration Manager-aktivitetssekvens.

Mer information finns i [Windows Autopilot för befintliga enheter](../../../osd/deploy-use/windows-autopilot-for-existing-devices.md).


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>Ange enhet för etablering av OS-avbildning offline

<!--1358924-->
Ange nu den enhet som Configuration Manager använder för att lägga till program uppdateringar i OS-avbildningar och uppgraderings paket för operativ system. Den här processen kan förbruka en stor mängd disk utrymme med temporära filer, så det här alternativet ger dig möjlighet att välja den enhet som ska användas.

Mer information finns i [hantera OS-avbildningar](../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive) eller [Hantera uppgraderings paket för operativ system](../../../osd/get-started/manage-operating-system-upgrade-packages.md#bkmk_servicing-drive).


### <a name="task-sequence-support-for-boundary-groups"></a>Stöd för aktivitetssekvens för gränser grupper

<!--1359025-->
När en enhet kör en aktivitetssekvens och behöver hämta innehåll använder den nu gränser för gränser som liknar Configuration Manager-klienten.

Mer information finns i [gränser grupper](../../servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd).


### <a name="improvements-to-driver-maintenance"></a>Förbättringar av driv rutins underhåll

<!--3607716, fka 1358270-->
Driv rutins paket har nu ytterligare metadata-fält för **tillverkare** och **modell**. Använd de här fälten för att tagga driv rutins paket med information som hjälper dig i allmänna underhåll, eller för att identifiera gamla och duplicerade driv rutiner som du kan ta bort.

Mer information finns i [Hantera driv rutiner](../../../osd/get-started/manage-drivers.md).

### <a name="improvements-to-windows-10-servicing-plan-filters"></a>Förbättringar av service plan filter för Windows 10

<!--3098809, 3113836, 3204570 -->
Ytterligare filter har lagts till i Service planer för Windows 10. Nu kan du filtrera efter **arkitektur**, **produkt kategori**och om uppgraderingen har **ersatts**.

Mer information finns i [service plan för Windows 10](../../../osd/deploy-use/manage-windows-as-a-service.md#BKMK_ServicingPlan).

### <a name="new-task-sequence-variable-for-last-action-name"></a>Ny aktivitetssekvens-variabel för senaste åtgärds namn

<!--SCCMDocs-pr issue #2964-->
Tillsammans med variabeln _SMSTSLastActionRetCode, anger aktivitetssekvensen också en ny variabel **_SMSTSLastActionName**. Den loggar också det här värdet till filen Smsts. log. Den här nya variabeln är fördelaktig när en aktivitetssekvens felsöks. Om ett steg Miss lyckas kan ett anpassat skript inkludera steg namnet tillsammans med retur koden.

Mer information finns i [variabler för aktivitetssekvens](../../../osd/understand/task-sequence-variables.md#SMSTSLastActionName).



## <a name="software-updates"></a><a name="bkmk_sum"></a>Program uppdateringar

### <a name="phased-deployment-of-software-updates"></a>Stegvis distribution av program uppdateringar

<!--1358146-->
Skapa stegvisa distributioner för program uppdateringar. Med stegvisa distributioner kan du dirigera en samordnad, sekvenserad distribution av program vara utifrån anpassningsbara kriterier och grupper.

Mer information finns i skapa stegvisa [distributioner](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>Förbättringar av underhålls fönster för program uppdateringar

<!--vso2839307-->
Följande klient inställning finns i **program uppdaterings** gruppen för att styra installations beteendet för program uppdateringar i underhålls fönster: **Aktivera installation av uppdateringar i underhålls fönstret för alla distributioner när underhålls fönstret för program uppdatering är tillgängligt**

Som standard är det här alternativet **inte** att vara konsekvent med det befintliga beteendet. Ändra den till **Ja** så att klienterna kan använda andra tillgängliga underhålls fönster för att installera program uppdateringar.

Mer information finns i [klient inställningar för program uppdateringar](../../clients/deploy/about-client-settings.md#bkmk_SUMMaint).


### <a name="improvement-to-software-updates-maintenance"></a>Förbättringar av underhåll av program uppdateringar

<!--2839349-->
Rensnings aktiviteter för WSUS körs nu på sekundära platser. WSUS-rensning för utgångna uppdateringar är igång och ersatta uppdateringar nekas i WSUS för sekundära platser.

Mer information finns i [rensnings beteende för WSUS från och med version 1810](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810)

### <a name="improvement-to-software-update-supersedence-rules"></a>Förbättringar av ersättnings regler för program uppdatering

<!--3098809, 2977644-->
Nu kan du ange ersättnings regler för funktions uppdateringar separat från uppdateringar som inte är av en funktion. Det innebär att dina uppgraderingar inte tas bort från Configuration Manager innan du har slutfört underhållet av Windows 10-klienter.

Mer information finns i [Ersättningsregler](../../../sum/get-started/install-a-software-update-point.md#supersedence-rules).

## <a name="reporting"></a><a name="bkmk_report"></a>Uppgiftslämn

### <a name="improvement-to-lifecycle-dashboard"></a>Förbättra livs cykelns instrument panel

<!--1358702-->
Instrument panelen för produktens livs cykel innehåller nu information om **System Center 2012 Configuration Manager och senare**.

Det finns också en ny rapport, **livs cykel 05A-instrumentpanel**. Den innehåller liknande information som instrument panelen i konsolen.

Mer information om den här instrument panelen finns i [använda instrument panelen för produktens livs cykel](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


### <a name="improvement-to-data-warehouse"></a>Förbättra informations lagret

<!--1358870-->
Nu kan du synkronisera fler tabeller från plats databasen till data lagret. Med den här ändringen kan du skapa fler rapporter utifrån dina affärs behov.

Mer information finns i [informations lager](../../servers/manage/data-warehouse.md).



## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Configuration Manager-konsol

### <a name="configuration-manager-administrator-authentication"></a>Configuration Manager administratörs autentisering

<!--1357013-->
Nu kan du ange lägsta autentiseringsnivå som administratörer kan använda för att komma åt Configuration Manager-platser. Den här funktionen tvingar administratörer att logga in på Windows med den nivå som krävs. Du konfigurerar den här inställningen genom att leta upp fliken **autentisering** i **Inställningar för hierarkin**.

Mer information finns i [Planera för SMS-providern](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth).


### <a name="support-center"></a>Support Center

<!--1357489-->
Använd Support Center för klient fel sökning, real tids logg visning eller för att hämta statusen för en Configuration Manager klient dator för senare analys. Support Center är ett enda verktyg för att kombinera många administratörs fel söknings verktyg. Hitta installations programmet för Support Center på plats servern i mappen **CD. latest\SMSSETUP\Tools\SupportCenter** .

Mer information finns i [Support Center](../../support/support-center.md).


### <a name="management-insights-dashboard"></a>Instrument panel för hanterings insikter

<!--1357979-->
Noden för **hanterings insikter** innehåller nu en grafisk instrument panel. Den här instrument panelen visar en översikt över regel tillstånden, vilket gör det enklare för dig att visa din förloppet. Instrument panelen innehåller följande paneler:

- **Management Insights-index**: spårar övergripande förloppet för hanterings insikter-regler. Indexet är ett viktat medelvärde. Kritiska regler är värda de flesta. Detta index ger minst en vikt till valfria regler.  

- **Hanterings insikter grupper**: visar procent av regler i varje grupp.  

- **Prioritet för Management Insights**: visar procent av regler efter prioritet.  

- **Alla insikter**: en tabell med insikter inklusive prioritet och tillstånd.  

![Skärm bild av instrument panelen för hanterings insikter](media/1357979-management-insights-dashboard.png)

Mer information finns i [hanterings insikter](../../servers/manage/management-insights.md).


### <a name="improvements-to-cmpivot"></a>Förbättringar av CMPivot

<!--1359068-->
CMPivot innehåller följande förbättringar:

- Spara **favorit** frågor  

- På fliken fråga Sammanfattning väljer du antalet misslyckade eller frånkopplade enheter och väljer sedan alternativet för att **skapa samlingen**.

Mer information om ytterligare prestanda och fel sökning av CMPivot finns i [förbättringar av skript](#bkmk_scripts).

Mer information om CMPivot finns i [CMPivot](../../servers/manage/cmpivot.md).


### <a name="improvements-to-scripts"></a><a name="bkmk_scripts"></a>Förbättringar av skript

<!--1358239-->
Nu kan du Visa detaljerade skript utdata i oformaterat eller strukturerat JSON-format. Den här formateringen gör det lättare att läsa och analysera utdata.

Följande förbättringar av prestanda och fel sökning gäller för både CMPivot och skript:

- Uppdaterade klienter returnerar utdata mindre än 80 KB till platsen via en snabb kommunikations kanal. Den här ändringen ökar prestanda för visning av skript eller frågor om utdata.  

- Ytterligare loggar för fel sökning  

Mer information finns i följande artiklar:  

- [Skapa och kör PowerShell-skript från Configuration Manager-konsolen](../../../apps/deploy-use/create-deploy-scripts.md)  

- [Felsöka CMPivot](../../servers/manage/cmpivot-tsg.md)


### <a name="sms-provider-api"></a>API för SMS-provider

<!--3607711, fka 1321523-->
SMS-providern tillhandahåller nu skrivskyddad API-interoperabilitet till WMI över HTTPS, som kallas **administrations tjänsten**. Den här REST API kan användas i stället för en anpassad webb tjänst för att komma åt information från webbplatsen.

**SMS-providern** visas som en roll med ett alternativ för att tillåta kommunikation via Cloud Management Gateway. Det aktuella användnings alternativet är att aktivera program godkännande via e-post från en fjär renhet.

Mer information finns i [Planera för SMS-providern](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service).



## <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a>Lokal MDM

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>En Intune-anslutning krävs inte längre för nya lokala MDM-distributioner

<!--1359124-->
Den lokala MDM-förutsättningen för att konfigurera en Microsoft Intune prenumeration krävs inte längre för nya distributioner. Din organisation kräver fortfarande Intune-licenser för att använda den här funktionen. Du kan för närvarande inte ta bort Intune-anslutningen från befintliga lokala MDM-distributioner. Mer information finns i [blogg inlägget om Intune-support](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).



## <a name="other-updates"></a>Övriga uppdateringar

Förutom nya funktioner innehåller den här versionen även ytterligare ändringar som fel korrigeringar. Mer information finns i [Sammanfattning av ändringar i Configuration Manager aktuella grenen, version 1810](https://support.microsoft.com/help/4482169).

Mer information om ändringar i Windows PowerShell-cmdlets för Configuration Manager finns i [versions anteckningar för PowerShell version 1810](https://docs.microsoft.com/powershell/sccm/1810-release-notes?view=sccm-ps).

Följande samlade uppdateringar (4488598) är tillgängliga i-konsolen från och med 25 mars 2019: Samlad uppdatering [2 för Configuration Manager aktuella grenen, version 1810](https://support.microsoft.com/help/4488598). Detta ersätter den tidigare samlade uppdateringen, KB 4486457.


### <a name="hotfixes"></a>Snabbkorrigeringar

Följande ytterligare snabb korrigeringar är tillgängliga för att åtgärda specifika problem:

| ID | Titel | Datum | I-konsolen |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune anslutnings certifikat förnyas inte i Configuration Manager | 18 januari 2019 | Ja |
| [4490434](https://support.microsoft.com/help/4490434) | Dubbletter av användar identifierings kolumner skapas i Configuration Manager | 22 februari 2019 | Ja |
| [4490575](https://support.microsoft.com/help/4490575) | Uppdaterings installationer slutar svara eller aldrig visar slut för ande i Configuration Manager version 1810 | 22 februari 2019 | Ja |


## <a name="next-steps"></a>Nästa steg

När du är redo att installera den här versionen, se [Installera uppdateringar för Configuration Manager](../../servers/manage/updates.md) och [Check lista för att installera uppdatering 1810](../../servers/manage/checklist-for-installing-update-1810.md).

> [!TIP]  
> Om du vill installera en ny plats använder du en bas linje version av Configuration Manager.  
>
> Läs mer om:
>
> - [Nya platser installeras](../../servers/deploy/install/installing-sites.md)  
> - [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines)  

För kända, betydande problem, se [viktig information](../../servers/deploy/install/release-notes.md).

När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist).
