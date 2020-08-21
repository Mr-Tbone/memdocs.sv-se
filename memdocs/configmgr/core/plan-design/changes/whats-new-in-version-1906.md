---
title: Nyheter i version 1906
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 1906 av Configuration Manager aktuella grenen.
ms.date: 10/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0401207ec98331c33e87a0ac03b5cd7f750c17e7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698722"
---
# <a name="whats-new-in-version-1906-of-configuration-manager-current-branch"></a>Vad är nytt i version 1906 av Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 1906 för Configuration Manager aktuella grenen är tillgänglig som en uppdatering i konsolen. Använd den här uppdateringen på webbplatser som kör version 1802 eller senare. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> I den här artikeln sammanfattas ändringar och nya funktioner i Configuration Manager version 1906.  

Läs alltid den senaste check listan för att installera den här uppdateringen. Mer information finns i [Check lista för att installera uppdatering 1906](../../servers/manage/checklist-for-installing-update-1906.md). När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).

För att dra full nytta av nya Configuration Manager funktioner kan du även uppdatera klienter till den senaste versionen när du har uppdaterat platsen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.

> [!Tip]  
> Om du vill få ett meddelande när den här sidan uppdateras kopierar du och klistrar in följande URL i din RSS-feed läsare: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="requirement-changes"></a>Krav ändringar

### <a name="version-1906-client-requires-sha-2-code-signing-support"></a>Version 1906-klienten kräver stöd för SHA-2-kod signering

<!--SCCMDocs-pr#3404-->
På grund av svagheter i SHA-1-algoritmen och för att justera till bransch standarder, signerar Microsoft nu bara Configuration Manager binärfiler med hjälp av säkrare SHA-2-algoritmen. Följande Windows OS-versioner kräver en uppdatering av stöd för SHA-2-kod signering:

- Windows 7 SP1
- Windows Server 2008 R2 SP1
- Windows Server 2008 SP2

Mer information finns i [krav för Windows-klienter](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_sha2).


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Plats infrastruktur

### <a name="site-server-maintenance-task-improvements"></a>Förbättringar av plats serverns underhålls uppgift

<!--3555894-->
Plats serverns underhålls aktiviteter kan nu visas och redige ras från en egen flik i vyn information på en plats Server. På fliken nya **underhålls aktiviteter** får du information om t. ex.:

- Om aktiviteten är aktive rad
- Aktivitets schemat
- Senaste start tid
- Senaste slut för ande tid
- Om uppgiften har slutförts

![Ny flik för underhålls aktiviteter i detaljvyn för en plats Server](./media/3555894-maintenance-tasks.png)

Mer information finns i [underhålls aktiviteter](../../servers/manage/maintenance-tasks.md#bkmk_MTs1906).

### <a name="configuration-manager-update-database-upgrade-monitoring"></a>Configuration Manager uppdatera övervakning av databas uppgradering

<!--4200581-->
När du använder en Configuration Manager uppdatering kan du nu se tillståndet för åtgärden **Uppgradera ConfigMgr-databas** i fönstret installations status.

- Om databas uppgraderingen är blockerad får du en varning, **som pågår, behöver åtgärdas**.
   - Cmupdate. log kommer att logga program namnet och SessionID från SQL som blockerar databas uppgraderingen.
- När databas uppgraderingen inte längre är blockerad återställs statusen till **pågår** eller **slutförs**.
   - När databas uppgraderingen blockeras utförs en kontroll var 5: e minut för att se om den fortfarande är blockerad.

   ![Övervakning av databas uppgradering under installation](./media/4200581-database-upgrade-monitoring.png)

Mer information finns i [Installera uppdateringar i konsolen](../../servers/manage/install-in-console-updates.md#3-monitor-the-progress-of-updates-as-they-install).

### <a name="management-insights-rule-for-ntlm-fallback"></a>Management Insights-regel för NTLM-återställning

<!--4572953-->
Hanterings insikter innehåller en ny regel som identifierar om du har aktiverat återställnings metoden för en mindre säker NTLM-autentisering för platsen: **NTLM-återställning har Aktiver ATS**.

Mer information finns i [hanterings insikter](../../servers/manage/management-insights.md#security).

### <a name="improvements-to-support-for-sql-always-on"></a>Förbättringar av stöd för SQL Always on

- Lägg till en ny synkron replik från installations programmet<!--3127336-->: Nu kan du lägga till en ny sekundär replik-nod till en befintlig SQL Always on-tillgänglighetsgruppen. Använd Configuration Manager-installationsprogrammet i stället för en manuell process för att göra den här ändringen. Mer information finns i [konfigurera SQL Server Always on Availability groups](../../servers/deploy/configure/configure-aoag.md#bkmk_sync).

- Redundans för flera undernät<!-- SCCMDocs-pr#3734 -->: Nu kan du aktivera [nyckelordet MultiSubnetFailover-anslutningssträng](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) i SQL Server. Du måste också konfigurera plats servern manuellt. Mer information finns i krav för [redundans för flera undernät](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover) .

- Stöd för distribuerade vyer<!-- SCCMDocs-pr#3792 -->: Plats databasen kan finnas på en SQL Server Always on-tillgänglighetsgrupper och du kan aktivera Länkar för databasreplikering för att använda [distribuerade vyer](../hierarchy/data-transfers-between-sites.md#bkmk_dbrep).

    > [!Note]  
    > Den här ändringen gäller inte för SQL Server kluster.

- Site Recovery kan återskapa databasen på en grupp med SQL Always On. Den här processen fungerar med både manuell och automatisk dirigering.<!-- SCCMDocs-pr#3846 -->

- Nya krav kontroller för installation:<!-- SCCMDocs-pr#3899 -->  

    - SQL tillgänglighets grupps repliker måste ha samma seeding-läge
    - SQL tillgänglighets grupps repliker måste vara felfria

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Molnbaserad hantering

### <a name="azure-active-directory-user-group-discovery"></a>Azure Active Directory användar grupp identifiering

<!--3611956-->

Nu kan du identifiera användar grupper och medlemmar i dessa grupper från Azure Active Directory (Azure AD). Användare som finns i Azure AD-grupper som platsen inte tidigare har identifierat läggs till som användar resurser i Configuration Manager. En resurs post för användar grupp skapas när gruppen är en säkerhets grupp. Den här funktionen är en [för hands versions funktion](../../servers/manage/pre-release-features.md) och måste aktive ras.

Mer information finns i [Konfigurera identifierings metoder](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco).

### <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a>Synkronisera samlings medlemskaps resultat till Azure Active Directory grupper

<!--3607475-->

Nu kan du aktivera synkroniseringen av samlings medlemskap till en Azure Active Directory (Azure AD)-grupp. Den här synkroniseringen är en för hands versions funktion. För att aktivera den, se [för hands versions funktioner](../../servers/manage/pre-release-features.md).

Med synkroniseringen kan du använda dina befintliga regler för lokal gruppering i molnet genom att skapa Azure AD Group-medlemskap baserat på samlings medlemskaps resultat. Endast enheter med en Azure Active Directory-post avspeglas i Azure AD-gruppen. Både hybrid Azure AD-anslutna och Azure Active Directory anslutna enheter stöds.

Mer information finns i [skapa samlingar](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync).


## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Skriv bords analys

### <a name="readiness-insights-for-desktop-apps"></a>Readiness Insights för skrivbordsappar

<!-- 4021225 -->

Nu kan du få mer detaljerade insikter om dina Skriv bords program, inklusive branschspecifika appar. Det tidigare app Health Analyzer Toolkit är nu integrerat med Configuration Manager-klienten. Den här integrationen fören klar distributionen och hanteringen av app readiness Insights i Skriv bords analys portalen.

Mer information finns [i kompatibilitetskontroll i Desktop Analytics](../../../desktop-analytics/compat-assessment.md#advanced-insights).


### <a name="dalogscollector-tool"></a>DALogsCollector-verktyg

<!--4622989-->
Använd DesktopAnalyticsLogsCollector.ps1-verktyget från Configuration Manager installations katalog för att felsöka Desktop Analytics. Den kör vissa grundläggande fel söknings steg och samlar in relevanta loggar i en enda arbets katalog.

Mer information finns i [loggar insamlare](../../../desktop-analytics/log-collector.md).


## <a name="real-time-management"></a><a name="bkmk_real"></a> Real tids hantering

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a>Lägg till kopplingar, ytterligare operatorer och agg regeringar i CMPivot

<!--4054074-->

För CMPivot har du nu ytterligare aritmetiska operatorer, agg regeringar och möjlighet att lägga till frågor, till exempel att använda register och filer tillsammans.

Mer information finns i [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1906).

### <a name="cmpivot-standalone"></a>Fristående CMPivot

<!--3555890, 4619340, 4692885 -->

Du kan nu använda CMPivot som en fristående app. Fristående CMPivot är en **för hands versions funktion** och är bara tillgänglig på engelska. Kör CMPivot utanför Configuration Manager-konsolen för att Visa real tids status för enheter i din miljö. Den här ändringen gör att du kan använda CMPivot på en enhet utan att först installera-konsolen.

Du kan dela kraften i CMPivot med andra personer, till exempel supportavdelningen eller säkerhets administratörer, som inte har konsolen installerad på datorn. Dessa andra personer kan använda CMPivot för att fråga Configuration Manager tillsammans med andra verktyg som de traditionellt använder. Genom att dela dessa omfattande hanterings data kan du samar beta för att proaktivt lösa affärs problem som uppstår mellan roller.

Mer information finns i [CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone) och [för hands versions funktioner](../../servers/manage/pre-release-features.md#bkmk_table).

### <a name="added-permissions-to-the-security-administrator-role"></a>Behörigheter till rollen säkerhets administratör har lagts till

<!--4683130-->

Följande behörigheter har lagts till i Configuration Manager den inbyggda rollen [**säkerhets administratör**](../../understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) :

- Läs vidare på SMS-skript
- Kör CMPivot för samling
- Läs vidare på inventerings rapport

Mer information finns i [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot_secadmin1906).


## <a name="content-management"></a><a name="bkmk_content"></a> Innehålls hantering

### <a name="delivery-optimization-download-data-in-client-data-sources-dashboard"></a>Leverans optimering hämta data i instrument panelen för klient data källor

<!--3555759-->
Instrument panelen för klient data källor innehåller nu data för [leverans optimering](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) . Den här instrument panelen hjälper dig att förstå varifrån klienter får innehåll i din miljö.

Mer information finns i [instrument panelen för klient data källor](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

### <a name="use-your-distribution-point-as-an-in-network-cache-server-for-delivery-optimization"></a>Använd distributions platsen som en server för nätverks-cache för leverans optimering

<!--3555764-->
Nu kan du installera leverans optimering i-Network cache server på dina distributions platser. Genom att cachelagra det här innehållet lokalt kan dina klienter dra nytta av leverans optimerings funktionen, men du kan skydda WAN-länkar.

Den här cache-servern fungerar som en transparent cache på begäran för innehåll som hämtas av leverans optimering. Använd klient inställningar för att kontrol lera att den här servern endast erbjuds till medlemmar i den lokala Configuration Managers gränser gruppen.

Mer information finns i [leverans optimering i-Network cache i Configuration Manager](../hierarchy/microsoft-connected-cache.md).


## <a name="client-management"></a><a name="bkmk_client"></a> Klient hantering

### <a name="support-for-windows-virtual-desktop"></a>Stöd för virtuella Windows-datorer

<!--3556025-->
[Windows Virtual Desktop](/azure/virtual-desktop/) är en förhands gransknings funktion i Microsoft Azure och Microsoft 365. Du kan nu använda Configuration Manager för att hantera dessa virtuella enheter som kör Windows i Azure.

På samma sätt som en Terminal-Server tillåter de här virtuella enheterna flera samtidiga aktiva användarsessioner. För att hjälpa till med klient prestanda inaktiverar Configuration Manager nu användar principer på alla enheter som tillåter dessa flera användarsessioner. Även om du aktiverar användar principer inaktive RAS klienten som standard på dessa enheter, vilket innefattar virtuella Windows-datorer och Terminal-servrar.

Mer information finns i [operativ system versioner som stöds för klienter och enheter](../configs/supported-operating-systems-for-clients-and-devices.md#windows-computers).

### <a name="support-center-onetrace-preview"></a>Support Center OneTrace (förhandsversion)

<!--3555962-->
OneTrace är ett nytt logg visnings program med Support Center. Det fungerar ungefär som CMTrace, med följande förbättringar:

- En flikad vy
- Docknings bara Windows
- Förbättrade Sök funktioner
- Möjlighet att aktivera filter utan att lämna vyn logg
- Rullnings tips för att snabbt identifiera kluster av fel
- Snabb logg öppning för stora filer

![Skärm bild av OneTrace logg visare](./media/3555962-onetrace.png)

Mer information finns i [Support Center OneTrace](../../support/support-center-onetrace.md).

### <a name="configure-client-cache-minimum-retention-period"></a>Konfigurera minsta kvarhållningsperiod för klient-cache

<!--4485509-->
Nu kan du ange den minsta tiden som den Configuration Manager klienten ska behålla cachelagrat innehåll. Den här klient inställningen definierar den minsta tids period Configuration Manager agenten ska vänta innan den kan ta bort innehåll från cachen om mer utrymme behövs. I gruppen **Inställningar för klient-cache** i klient inställningar konfigurerar du följande inställning: **minsta varaktighet innan cachelagrat innehåll kan tas bort (minuter)**.

> [!Note]  
> I samma klient inställnings grupp har den befintliga inställningen för att **aktivera Configuration Manager-klient i fullständigt operativ system som delar innehåll** nu bytt namn till **som peer-cache-källa**. Beteendet för inställningen ändras inte.  

Mer information finns i [Inställningar för klient-cache](../../clients/deploy/about-client-settings.md#client-cache-settings).


## <a name="co-management"></a><a name="bkmk_comgmt"></a> Samhantering

### <a name="improvements-to-co-management-auto-enrollment"></a>Förbättringar av automatisk registrering för samhantering

- En ny samhanterad enhet registreras nu automatiskt i Microsoft Intune tjänst baserat på dess Azure Active Directory (Azure AD) *-token* . Användaren behöver inte vänta på att en användare loggar in på enheten för automatisk registrering för att starta. Den här ändringen bidrar till att minska antalet enheter med [registrerings statusen](../../../comanage/how-to-monitor.md#co-management-enrollment-status) *väntar på användar inloggning*.<!-- 4454491 -->

- För kunder som redan har enheter som har registrerats för samhantering, registreras nya enheter omedelbart när de uppfyller kraven. Till exempel när enheten är ansluten till Azure AD och Configuration Manager-klienten är installerad.<!--4321130-->

Mer information finns i [Aktivera samhantering](../../../comanage/how-to-enable.md).

### <a name="multiple-pilot-groups-for-co-management-workloads"></a>Flera pilot grupper för samhanterings arbets belastningar

<!--3555750-->
Nu kan du konfigurera olika pilot samlingar för var och en av arbets belastningarna för samtidig hantering. Genom att använda olika pilot samlingar kan du ta en mer detaljerad metod när du växlar arbets belastningar.

- På fliken **aktivering** kan du nu ange en samling för **automatisk registrering i Intune** .
    - Den **automatiska registreringen av Intune** ska innehålla alla klienter som du vill integrera med samhantering. Det är i stort sett en supermängd till alla andra mellanlagrings samlingar.

- På fliken **mellanlagring** , i stället för att använda en pilot samling för alla arbets belastningar, kan du nu välja en individuell samling för varje arbets belastning.

    ![Med fliken mellanlagrings Mellanhantering kan du välja en samling för varje arbets belastning](./media/3555750-co-management-staging-tab.png)

Dessa alternativ är också tillgängliga när du först aktiverar samhantering.

Mer information finns i [Aktivera samhantering](../../../comanage/how-to-enable.md).

### <a name="co-management-support-for-government-cloud"></a>Stöd för samhantering för myndighets moln

<!--4075452-->
Amerikanska myndighets kunder kan nu använda samhantering med Azures moln för amerikanska myndigheter (portal.azure.us). Mer information finns i [Aktivera samhantering](../../../comanage/how-to-enable.md).


## <a name="application-management"></a><a name="bkmk_app"></a> Program hantering

### <a name="filter-applications-deployed-to-devices"></a>Filtrera program som har distribuerats till enheter

<!--4451056-->
Användar kategorier för enhets riktade program distributioner visas nu som filter i Software Center. Ange en **användar kategori** för ett program på **Software Center** -sidan i egenskaperna. Öppna sedan appen i Software Center och titta på tillgängliga filter.

Mer information finns i [Ange programinformation manuellt](../../../apps/deploy-use/create-applications.md#bkmk_manual-app).

### <a name="application-groups"></a>Program grupper

<!--3555907-->
Skapa en grupp av program som du kan skicka till en användar-eller enhets samling som en enda distribution. Metadata som du anger om app-gruppen visas i Software Center som en enda enhet. Du kan beställa apparna i gruppen så att klienten installerar dem i en speciell ordning.

Den här funktionen är för hands version. För att aktivera den, se [för hands versions funktioner](../../servers/manage/pre-release-features.md).

Mer information finns i [skapa program grupper](../../../apps/deploy-use/create-app-groups.md).

### <a name="retry-the-install-of-pre-approved-applications"></a>Gör om installationen av för hands godkända program

<!--4336307-->
Nu kan du försöka att installera en app som du tidigare godkänt för en användare eller enhet. Alternativet för godkännande är endast tillgängligt för distributioner. Om användaren avinstallerar appen, eller om den inledande installationen Miss lyckas, kommer Configuration Manager inte att utvärdera om dess tillstånd och installera om den. Med den här funktionen kan en support tekniker snabbt försöka installera appen igen för en användare som anropar hjälp.

Mer information finns i [godkänna program](../../../apps/deploy-use/app-approval.md).

### <a name="install-an-application-for-a-device"></a>Installera ett program för en enhet

<!--4402180-->
Du kan nu installera program på en enhet i real tid från Configuration Manager-konsolen. Den här funktionen kan hjälpa till att minska behovet av separata samlingar för varje program.

Mer information finns i [installera program för en enhet](../../../apps/deploy-use/install-app-for-device.md).

### <a name="improvements-to-app-approvals"></a>Förbättringar av appens godkännanden

<!--4224910-->
Den här versionen innehåller följande förbättringar av appens godkännanden:

- Om du godkänner en app-begäran i-konsolen och sedan nekar den, kan du nu godkänna den igen. Appen installeras om på klienten när du har godkänt den.  

- I Configuration Manager-konsolen, arbets ytan **program varu bibliotek** , under **program hantering**, byter du namn på noden för **godkännande begär Anden** till **program begär Anden**.<!-- SCCMDocs-pr#4028 -->

- Det finns en ny WMI-metod som är **DeleteInstance** att ta bort en begäran om godkännande av appen. Den här åtgärden avinstallerar inte appen på enheten. Om den inte redan är installerad kan användaren inte installera appen från Software Center.

- Anropa **CreateApprovedRequest** -API: et för att skapa en förauktoriserad begäran om en app på en enhet. Om du vill förhindra att appen installeras automatiskt på klienten anger du parametern för automatisk **installation** till `FALSE` . Användaren ser appen i Software Center, men installeras inte automatiskt.

Mer information finns i [godkänna program](../../../apps/deploy-use/app-approval.md).


## <a name="os-deployment"></a><a name="bkmk_osd"></a> OS-distribution

### <a name="task-sequence-debugger"></a>Fel sökare för aktivitetssekvens

<!--3612274-->
Fel söknings programmet för aktivitetssekvenser är ett nytt fel söknings verktyg. Du distribuerar en aktivitetssekvens i fel söknings läge till en samling med en enhet. Med den kan du gå igenom aktivitetssekvensen på ett kontrollerat sätt för att under lätta fel sökning och undersökning.

![Skärm bild av fel sökning för aktivitetssekvens](./media/3612274-tsdebug.png)

Den här funktionen är för hands version. För att aktivera den, se [för hands versions funktioner](../../servers/manage/pre-release-features.md).

Mer information finns i [fel sökning av en aktivitetssekvens](../../../osd/deploy-use/debug-task-sequence.md).

### <a name="clear-app-content-from-client-cache-during-task-sequence"></a>Rensa appdata från klient-cache under aktivitetssekvensen

<!--4485675-->
I steget **installera program** i aktivitetssekvensen kan du nu ta bort appens innehåll från klientcachen när steget har körts.

Mer information finns i [om aktivitetssekvenser](../../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication).

> [!Important]  
> Uppdatera mål klienten till den senaste versionen för att stödja den här nya funktionen.

### <a name="reclaim-sedo-lock-for-task-sequences"></a>Frigör SEDO-lås för aktivitetssekvenser

<!--3699337-->
Om Configuration Manager-konsolen slutar svara kan du vara utelåst från att göra ytterligare ändringar i en aktivitetssekvens. Nu när du försöker komma åt en låst aktivitetssekvens kan du nu **ignorera ändringarna**och fortsätta redigera objektet.

Mer information finns i [använda redigeraren för aktivitetssekvens](../../../osd/understand/task-sequence-editor.md#bkmk_sedo).

### <a name="pre-cache-driver-packages-and-os-images"></a>Driv rutins paket och OS-avbildningar före cache

<!--4224642-->
I förväg cache i aktivitetssekvensen ingår även ytterligare innehålls typer. Innehåll i förcachen har tidigare endast tillämpats på uppgraderings paket för operativ system. Nu kan du använda för cachelagring för att minska bandbredds förbrukningen för:

- Operativsystemavbildningar
- Drivrutinspaket
- Paket

Mer information finns i [Konfigurera förinställt innehåll för cache](../../../osd/deploy-use/configure-precache-content.md).

### <a name="improvements-to-os-deployment"></a>Förbättringar av OS-distribution

Den här versionen innehåller följande förbättringar av OS-distributionen:

- Använd följande två PowerShell-cmdletar för att skapa och redigera steget [Kör aktivitetssekvens](../../../osd/understand/task-sequence-steps.md#child-task-sequence) :<!--2839943-->

    - **New-CMTSStepRunTaskSequence**

    - **Set-CMTSStepRunTaskSequence**

- Nu är det enklare att redigera variabler när du kör en aktivitetssekvens. När du har valt en aktivitetssekvens i fönstret guiden aktivitetssekvens, innehåller sidan för att redigera variabler för aktivitetssekvens en **redigerings** knapp.<!-- 4668846 --> Mer information finns i [använda variabler för aktivitetssekvens](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-tswiz).

- Steget **inaktivera BitLocker** -aktivitetssekvens har en ny omstart-räknare. Använd det här alternativet om du vill ange antalet omstarter för att behålla BitLocker inaktiverat. Den här ändringen hjälper dig att förenkla aktivitetssekvensen. Du kan använda ett enda steg, i stället för att lägga till flera instanser av det här steget. <!--4512937--> Mer information finns i avsnittet [Disable BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_DisableBitLocker).

- Använd den nya variabeln **SMSTSRebootDelayNext** i aktivitetssekvensen med den befintliga [SMSTSRebootDelay](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelay) -variabeln. Om du vill att senare omstarter ska ske under en annan tids gräns än den första, ställer du in den här nya variabeln på ett annat värde på några sekunder. <!--4447680--> Mer information finns i [SMSTSRebootDelayNext](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelayNext).

- Aktivitetssekvensen anger en ny skrivskyddad variabel **_SMSTSLastContentDownloadLocation**. Den här variabeln innehåller den sista platsen där aktivitetssekvensen hämtades eller försökte ladda ned innehåll. Kontrol lera den här variabeln i stället för att parsa klient loggarna.<!-- 2840337 -->

- När du skapar mediet för aktivitetssekvensen lägger Configuration Manager inte till en autorun. inf-fil. Den här filen blockeras vanligt vis av program mot skadlig kod. Du kan fortfarande inkludera filen om det behövs för ditt scenario.<!-- 4090666 -->

### <a name="improvements-to-pxe"></a>Förbättringar av PXE

Alternativet 82 under PXE DHCP-handskakningen stöds nu med PXE-svarare utan WDS. Alternativet 82 stöds inte med WDS.


## <a name="software-center"></a><a name="bkmk_userxp"></a> Software Center

### <a name="improvements-to-software-center-tab-customizations"></a>Förbättringar av anpassningar av fliken i Software Center

<!--4063773-->
Nu kan du lägga till upp till fem anpassade flikar i Software Center. Du kan också redigera ordningen som flikarna visas i Software Center.

Mer information finns i [klient inställningar för Software Center](../../clients/deploy/about-client-settings.md#software-center).

### <a name="software-center-infrastructure-improvements"></a>Förbättringar av Software Center-infrastrukturen

<!--3555950-->

I den här versionen ingår följande infrastruktur förbättringar för Software Center:

- Software Center kommunicerar nu med en hanterings plats för appar som är riktade till användare som tillgängliga. Den använder inte program katalogen längre. Den här ändringen gör det enklare för dig att ta bort program katalogen från webbplatsen.

- Tidigare valde Software Center den första hanterings platsen från listan över tillgängliga servrar. Från och med den här versionen använder den samma hanterings plats som klienten använder. Den här ändringen gör att Software Center kan använda samma hanterings plats från den tilldelade primära platsen som klienten.

> [!Important]  
> De här iterativa förbättringarna av Software Center och hanterings platsen är att dra tillbaka program katalog rollerna.
>
> - Silverlight-användar upplevelsen stöds inte av den aktuella gren versionen 1806.
> - Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller.
> - Support upphör för program katalog rollerna med version 1910.  

Mer information finns i [ta bort program katalogen](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat) och [Planera för Software Center](../../../apps/plan-design/plan-for-software-center.md).

### <a name="redesigned-notification-for-newly-available-software"></a>Omdesignat meddelande för nyligen tillgänglig program vara

<!--3555904-->
Den **nya program varan som är tillgänglig** visas bara en gång för en användare för ett angivet program och en ny revision. Användaren kommer inte längre att se meddelandet varje gången de loggar in. De ser bara ett annat meddelande för ett program om det har ändrats eller omdistribuerats.

Mer information finns i [skapa och distribuera ett program](../../../apps/get-started/create-and-deploy-an-application.md#end-user-experience).

### <a name="more-frequent-countdown-notifications-for-restarts"></a>Vanliga nedräknings meddelanden för omstarter

<!--3976435-->

Slutanvändare kommer nu att bli påmind oftare om en väntande omstart med aviseringar om återkommande nedräkningar. Du kan definiera intervallet för tillfälliga meddelanden i **klient inställningar** på sidan **starta om datorn** . Ändra värdet för **ange varaktighet för vilo läge för omstart av datorn (minuter)** för att konfigurera hur ofta en användare påminns om en väntande omstart tills det slutgiltiga nedräknings meddelandet inträffar.

Dessutom ökade det maximala värdet för att **Visa ett tillfälligt meddelande till användaren som anger intervallet innan användaren loggas ut eller datorn startas om (minuter)** från 1440 minuter (24 timmar) till 20160 minuter (två veckor).

Mer information finns i [meddelanden om omstart av enhet](../../clients/deploy/device-restart-notifications.md) och [om klient inställningar](../../clients/deploy/about-client-settings.md#computer-restart).

### <a name="direct-link-to-custom-tabs-in-software-center"></a>Direkt länk till anpassade flikar i Software Center

<!--4655176-->

Nu kan du förse användarna med en direkt länk till en [anpassad flik](../../clients/deploy/about-client-settings.md#software-center-tab-visibility) i Software Center.

Använd följande URL-format för att öppna Software Center på en viss flik:

`softwarecenter:page=CustomTab1`

Strängen `CustomTab1` är den första anpassade fliken i ordning.

Skriv till exempel denna URL i fönstret Windows- **körning** .

Du kan också använda den här syntaxen för att öppna standard flikar i Software Center:

|Kommandorad  |Flik  |
|---------|---------|
|`AvailableSoftware`|Program|
|`Updates`|Uppdateringar|
|`OSD`|Operativsystem|
|`InstallationStatus`|Installations status|
|`Compliance`|Efterlevnad för enhet|
|`Options`|Alternativ|

Mer information finns i [Software Center-fliken synlighet](../../clients/deploy/about-client-settings.md#software-center-tab-visibility).

## <a name="software-updates"></a><a name="bkmk_sum"></a> Program uppdateringar

### <a name="additional-options-for-wsus-maintenance"></a>Ytterligare alternativ för WSUS-underhåll

<!--4110109-->
Nu har du ytterligare underhålls aktiviteter för WSUS som Configuration Manager kan köra för att upprätthålla felfria program uppdaterings platser. WSUS-underhållet sker efter varje synkronisering. Förutom att de nekade uppdateringarna i WSUS har gått ut kan Configuration Manager nu:

- Ta bort föråldrade uppdateringar från WSUS-databasen.
- Lägg till icke-grupperade index i WSUS-databasen för att förbättra prestanda för rensning av WSUS.

Mer information finns i [underhåll av program uppdateringar](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-starting-in-version-1906).

### <a name="configure-the-default-maximum-run-time-for-software-updates"></a>Konfigurera den maximala standard körnings tiden för program uppdateringar

<!--3734426-->

Nu kan du ange den maximala tids period som en program uppdaterings installation ska slutföras. Du kan ange följande objekt på fliken **maximal körnings tid** på program uppdaterings platsen:

- **Maximal kör tid för Windows-funktions uppdateringar (minuter)**
- **Maximal kör tid för Office 365-uppdateringar och uppdateringar som inte är av funktioner för Windows (minuter)**

Mer information finns i [Planera för program uppdateringar](../../../sum/plan-design/plan-for-software-updates.md#bkmk_maxruntime).

### <a name="configure-dynamic-update-during-feature-updates"></a>Konfigurera dynamisk uppdatering under funktions uppdateringar

<!--4062619-->

Använd en ny klient inställning för att konfigurera [dynamisk uppdatering](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) under installationen av funktions uppdateringen i Windows 10. Dynamisk uppdatering installerar språk paket, funktioner på begäran, driv rutiner och ackumulerade uppdateringar under Windows-installationen genom att dirigera klienten för att ladda ned uppdateringarna från Internet.

Mer information finns i [klient inställningar för program uppdatering](../../clients/deploy/about-client-settings.md#software-updates) och [hantera Windows som en tjänst](../../../osd/deploy-use/manage-windows-as-a-service.md).

### <a name="new-windows-10-version-1903-and-later-product-category"></a>Ny produkt kategori för Windows 10, version 1903 och senare

<!--4682946-->

**Windows 10, version 1903 och senare** har lagts till i Microsoft Update som sin egen produkt, i stället för att vara en del av **Windows 10**  -produkten som tidigare versioner. Den här ändringen gjorde att du utför ett antal manuella åtgärder för att se till att dina klienter ser dessa uppdateringar. Vi har hjälpt till att minska antalet manuella åtgärder som du behöver vidta för den nya produkten.

När du uppdaterar till Configuration Manager version 1906 och har **Windows 10** -produkten vald för synkronisering sker följande åtgärder automatiskt:

- Produkten **Windows 10, version 1903 och senare** har lagts till för synkronisering.
- Automatiska distributions regler som innehåller **Windows 10** -produkten kommer att uppdateras för att inkludera **Windows 10, version 1903 och senare**.
- Service planer uppdateras för att omfatta produkten **Windows 10, version 1903 och senare** .

Mer information finns i [Konfigurera klassificeringar och produkter som ska synkroniseras](../../../sum/get-started/configure-classifications-and-products.md), [Service planer](../../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)och [automatiska distributions regler](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process).

### <a name="drill-through-required-updates"></a>Granska nödvändiga uppdateringar

<!--4224414-->
Nu kan du granska efterlevnads statistik för att se vilka enheter som kräver en speciell program uppdatering. Om du vill visa enhets listan måste du ha behörighet att visa uppdateringar och de samlingar som enheterna tillhör. Om du vill öka detalj nivån i enhets listan väljer du hyperlänken **vy som krävs** bredvid cirkel diagrammet på fliken **Sammanfattning** för en uppdatering. Om du klickar på hyperlänken tas du till en tillfällig nod under **enheter** där du kan se vilka enheter som kräver uppdateringen.

Hyperlänken för **obligatorisk vy** är tillgänglig på följande platser:

   - **Program varu bibliotek**  >  **Program uppdateringar**  >  **Alla program uppdateringar**
   - **Program varu bibliotek**  >  **Windows 10-Underhåll**  >  **Alla Windows 10-uppdateringar**
   - **Program varu bibliotek**  >  **Office 365-klient hantering**  >  **Office 365-uppdateringar**

Mer information finns i [övervaka program uppdateringar](../../../sum/deploy-use/monitor-software-updates.md#drill-through-required-updates), [hantera Windows som en tjänst](../../../osd/deploy-use/manage-windows-as-a-service.md#drill-through-required-updates)och [Hantera Office 365 ProPlus-uppdateringar](../../../sum/deploy-use/manage-office-365-proplus-updates.md).


## <a name="office-management"></a><a name="bkmk_o365"></a> Office-hantering

### <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Instrument panel för Office 365 ProPlus Upgrade readiness

<!--4021125-->

För att hjälpa dig att avgöra vilka enheter som är klara att uppgradera till Office 365 ProPlus, finns det en ny instrument panel för beredskap. Den innehåller panelen **Office 365 ProPlus Upgrade readiness** som släpptes i Configuration Manager aktuella gren versionen 1902. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **klient hantering för Office 365**och välj noden **Office 365 ProPlus uppgraderingsberedskap** .

Mer information om instrument panelen, krav och hur du använder dessa data finns i [integrering för Office 365 ProPlus readiness](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).


## <a name="protection"></a><a name="bkmk_protect"></a> Skyddas

### <a name="windows-defender-application-guard-file-trust-criteria"></a>Villkor för fil förtroende för Windows Defender Application Guard

<!--3555858-->

Det finns en ny princip inställning som gör det möjligt för användare att lita på filer som normalt öppnas i Windows Defender Application Guard (WDAG). När åtgärden har slutförts öppnas filerna på värd enheten i stället för i WDAG.

Mer information finns i [skapa och distribuera Windows Defender Application Guard-princip](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_FM).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-konsol

### <a name="role-based-access-for-folders"></a>Rollbaserad åtkomst för mappar

<!--3600867-->

Nu kan du ange säkerhets omfattningar i mappar. Om du har åtkomst till ett objekt i mappen men inte har åtkomst till mappen kan du inte se objektet. Om du har åtkomst till en mapp men inte ett objekt i den, ser du inte det objektet. Högerklicka på en mapp, Välj **Ange säkerhets omfattningar**och välj sedan de säkerhets omfattningar som du vill använda.

Mer information finns i [Configuration Manager-konsol tips](../../servers/manage/admin-console-tips.md) och [Konfigurera rollbaserad administration](../../servers/deploy/configure/configure-role-based-administration.md#bkmk_config-folder).

### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Lägg till SMBIOS GUID-kolumn till noder i enhet och enhets samling

<!--4526580-->
I båda noderna **enheter** och **enhets samlingar** kan du nu lägga till en ny kolumn för **SMBIOS GUID**. Värdet är samma som egenskapen för **BIOS-GUID** för system resurs klassen. Det är en unik identifierare för enhetens maskin vara.

### <a name="administration-service-support-for-security-nodes"></a>Administrations tjänstens stöd för säkerhetsnoder

<!--4223683-->
Nu kan du aktivera vissa noder i Configuration Manager-konsolen för att använda administrations tjänsten. Den här ändringen gör att konsolen kan kommunicera med SMS-providern via HTTPS i stället för via WMI.

Mer information finns i [administrations tjänsten](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service).

> [!Note]
> Från och med version 1906 kallas fliken **klient dator kommunikation** på plats egenskaperna **kommunikations säkerhet**.<!-- SCCMDocs#1645 -->  

### <a name="collections-tab-in-devices-node"></a>Fliken samlingar i noden enheter

<!--4616810-->
Gå till noden **enheter** på arbets ytan **till gångar och efterlevnad** och välj en enhet. I informations fönstret växlar du till fliken nya **samlingar** . Den här fliken visar de samlingar som innehåller den här enheten.

> [!Note]  
> - Den här fliken är för närvarande inte tillgänglig från en undernoden enheter under noden **enhets samlingar** . Till exempel när du väljer alternativet för att **Visa medlemmar** i en samling.
> - Den här fliken kanske inte är ifylld som förväntat för vissa användare. Om du vill se en fullständig lista över samlingar som en enhet tillhör måste du ha säkerhets rollen **Fullständig administratör** . Detta är ett känt problem. <!--5107309-->

### <a name="task-sequences-tab-in-applications-node"></a>Fliken aktivitetssekvenser i noden program

<!--4616810-->
I arbets ytan **program bibliotek** expanderar du **program hantering**, går till noden **program** och väljer ett program. I informations fönstret växlar du till fliken nya **aktivitetssekvenser** . Den här fliken listar de aktivitetssekvenser som refererar till det här programmet.

### <a name="show-collection-name-for-scripts"></a>Visa samlings namn för skript

<!--4616810-->
I arbets ytan **övervakning** väljer du noden **skript status** . Nu visas **samlings namnet** förutom ID: t.

### <a name="real-time-actions-from-device-lists"></a>Real tids åtgärder från enhets listor

<!--4616810-->
Det finns olika sätt att visa en lista över enheter under noden **enheter** på arbets ytan **till gångar och efterlevnad** .

- I arbets ytan **till gångar och efterlevnad** väljer du noden **enhets samlingar** . Välj en enhets samling och välj sedan åtgärden för att **Visa medlemmar**. Den här åtgärden öppnar en undernoder till noden **enheter** med en enhets lista för samlingen.  

  - När du väljer undernoden samling kan du nu starta **CMPivot** från samlings gruppen i menyfliksområdet.  

- I arbets ytan **övervakning** väljer du noden **distributioner** . Välj en distribution och Välj åtgärden **Visa status** i menyfliksområdet. I fönstret distributions status dubbelklickar du på den totala till gångar som du vill gå igenom till en enhets lista.  

  - När du väljer en enhet i listan kan du nu starta **CMPivot** och **köra skript** från enhets gruppen i menyfliksområdet.  

### <a name="order-by-program-name-in-task-sequence"></a>Sortera efter program namn i aktivitetssekvens

<!--4616810-->
I arbets ytan **program bibliotek** expanderar du **operativ system**och väljer noden **aktivitetssekvenser** . Redigera en aktivitetssekvens och markera eller Lägg till steget [installera paket](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) . Om ett paket har fler än ett program, sorterar List rutan nu programmen i alfabetisk ordning.

### <a name="correct-names-for-client-operations"></a>Korrekta namn för klient åtgärder

<!--4616810-->
I arbets ytan **övervakning** väljer du **klient åtgärder**. Åtgärden att **byta till nästa program uppdaterings plats** har nu rätt namn.


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Föråldrade funktioner och operativ system

Läs om support ändringar innan de implementeras i [borttagna och föråldrade objekt](deprecated/removed-and-deprecated.md).

Version 1906 släpper stöd för följande funktioner:  

- Du kan inte installera nya program katalog roller. Uppdaterade klienter använder automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Mer information finns i [Planera för Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).

Version 1906-stöd för följande produkter:  

- Windows CE 7,0
- Windows 10 Mobil
- Windows 10 Mobile Enterprise


## <a name="other-updates"></a>Övriga uppdateringar

Från och med den här versionen är följande funktioner inte längre för hands version:

- [Administrations tjänst för SMS-provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Hantering av Windows Defender-programreglering](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)

Förutom nya funktioner innehåller den här versionen även ytterligare ändringar som fel korrigeringar. Mer information finns i [Sammanfattning av ändringar i Configuration Manager aktuella grenen, version 1906](https://support.microsoft.com/help/4514258).

Mer information om ändringar i Windows PowerShell-cmdlets för Configuration Manager finns i [versions anteckningar för PowerShell version 1906](/powershell/sccm/1906-release-notes?view=sccm-ps).

Följande samlade uppdateringar (4517869) är tillgängliga i-konsolen från den 1 oktober 2019: samlad [uppdatering för Configuration Manager aktuell gren, version 1906](https://support.microsoft.com/help/4517869).

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>Nästa steg

<!--At this time, version 1906 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1906.md#early-update-ring). -->
Från och med den 16 augusti 2019 är version 1906 globalt tillgängligt för alla kunder att installera.

När du är redo att installera den här versionen, se [Installera uppdateringar för Configuration Manager](../../servers/manage/updates.md) och [Check lista för att installera uppdatering 1906](../../servers/manage/checklist-for-installing-update-1906.md).

> [!TIP]  
> Om du vill installera en ny plats använder du en bas linje version av Configuration Manager.  
>
> Läs mer om:
>
> - [Nya platser installeras](../../servers/deploy/install/installing-sites.md)  
> - [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines)  

För kända, betydande problem, se [viktig information](../../servers/deploy/install/release-notes.md).

När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).