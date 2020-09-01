---
title: Nyheter i version 1902
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 1902 av Configuration Manager aktuella grenen.
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78150c497757c1a3f0b65a870c35516983711d9a
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193835"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Vad är nytt i version 1902 av Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 1902 för Configuration Manager aktuella grenen är tillgänglig som en uppdatering i konsolen. Använd den här uppdateringen på webbplatser som kör version 1802, 1806 eller 1810. <!-- baseline only statement:-->När du installerar en ny plats är den också tillgänglig som en bas linje version. I den här artikeln sammanfattas ändringar och nya funktioner i Configuration Manager version 1902.  

Läs alltid den senaste check listan för att installera den här uppdateringen. Mer information finns i [Check lista för att installera uppdatering 1902](../../servers/manage/checklist-for-installing-update-1902.md). När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist).

För att dra full nytta av nya Configuration Manager funktioner kan du även uppdatera klienter till den senaste versionen när du har uppdaterat platsen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.

<!-- > [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
 -->

> [!Tip]  
> Om du vill få ett meddelande när den här sidan uppdateras kopierar du och klistrar in följande URL i din RSS-feed läsare: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Föråldrade funktioner och operativ system

Läs om support ändringar innan de implementeras i [borttagna och föråldrade objekt](deprecated/removed-and-deprecated.md).

- Implementeringen av delning av innehåll från Azure har ändrats. Använd en innehålls aktive rad Cloud Management Gateway genom att aktivera alternativet för att **tillåta att CMG fungerar som en moln distributions plats och hanterar innehåll från Azure Storage**. Du kommer inte att kunna skapa en traditionell moln distributions plats i framtiden.

Version 1902 släpper stöd för följande produkter:  

- Linux och UNIX som en klient. Utfasningen presenterades av [version 1802](whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support). Överväg Microsoft Azure hantering för hantering av Linux-servrar. Azure-lösningar har omfattande Linux-support som i de flesta fall överskrider Configuration Manager-funktioner, inklusive slut punkt till slut punkt för korrigerings hantering för Linux.


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Plats infrastruktur

### <a name="client-health-dashboard"></a>Instrument panel för klient hälsa

<!--3599209-->
Du distribuerar program uppdateringar och andra appar för att skydda din miljö, men de här distributionerna når bara friska klienter. Fel Configuration Manager klienterna har negativ inverkan på övergripande kompatibilitet. Det kan vara svårt att avgöra klient hälsan beroende på vilken nämnare: hur många totala enheter som ska ingå i hanterings området? Om du till exempel upptäcker alla system från Active Directory, även om några av dessa poster är för inaktuella datorer, ökar den här processen din nämnare.

Nu kan du Visa en instrument panel med information om hälsan för Configuration Manager klienter i din miljö. Visa klient hälsan, scenariots hälsa och vanliga fel. Filtrera vyn efter flera attribut för att se eventuella eventuella problem med operativ system och klient versioner.

Gå till arbets ytan **övervakning** i Configuration Manager-konsolen. Expandera **klient status**och välj noden **klient hälso instrument panel** .

![Skärm bild av instrument panelen för klient hälsa](media/3599209-client-health-dashboard.png)

Mer information finns i [övervaka klienter](../../clients/manage/monitor-clients.md#bkmk_health).

### <a name="new-management-insight-rules"></a>Nya regler för hantering av insikter

Funktionen Management Insights har följande nya regler:

- Flera regler med rekommendationer om att hantera samlingar. Använd dessa insikter för att förenkla hanteringen och förbättra prestandan. Granska dessa nya regler i gruppen **samlingar** .<!--3555752-->  

- **Uppdatera klienter till en Windows 10-version som stöds** i den **förenklade hanterings** gruppen. Den här regeln rapporterar om klienter som kör en version av Windows 10 som inte längre stöds. Den innehåller också klienter med en Windows 10-version som är nära tjänstens slut (tre månader).<!--3897268-->  

Mer information finns i [hanterings insikter](../../servers/manage/management-insights.md).

### <a name="improvement-to-enhanced-http"></a>Förbättra till förbättrad HTTP

<!--3798957-->

Nu kan du Aktivera utökad HTTP per primär plats eller för den centrala administrations platsen.

På egenskaperna för den centrala administrations webbplatsen väljer du alternativet för att **använda Configuration Manager-genererade certifikat för HTTP-platssystem**. Den här inställningen gäller endast för plats system roller på den centrala administrations platsen. Det är inte en global inställning för hierarkin.

Mer information finns i [Enhanced http](../hierarchy/enhanced-http.md).

### <a name="improvement-to-setup-prerequisites"></a>Förbättringar av installations kraven

När du installerar eller uppdaterar till version 1902 innehåller Configuration Manager installationen nu följande krav kontroll:

- **Väntande omstart av systemet på fjärrSQL Server**: den här krav kontrollen liknar den **väntande systemomstarts** regeln, men den kontrollerar en fjärran sluten SQL Server. Mer information finns i [lista över krav kontroller](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart-on-the-remote-sql-server). <!--SCCMDocs-pr issue 3377-->  


## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Molnbaserad hantering

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>Stoppa moln tjänsten när den överskrider tröskelvärdet

<!--3735092-->
Configuration Manager kan nu stoppa en CMG-tjänst (Cloud Management Gateway) när den totala data överföringen går över gränsen. CMG har alltid haft aviseringar för att utlösa meddelanden när användningen har nått varnings-eller kritiska nivåer. För att minska eventuella oväntade Azure-kostnader på grund av en ökning i användningen stänger moln tjänsten av det nya alternativet.

Mer information finns i [stoppa CMG när den överskrider tröskelvärdet](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#bkmk_stop).

### <a name="use-azure-resource-manager-for-cloud-services"></a>Använd Azure Resource Manager för moln tjänster

<!--3605704-->
Från och med version 1810 var den klassiska tjänst distributionen i Azure inaktuell för användning i Configuration Manager. Den versionen är den sista som stöd för att skapa dessa Azure-distributioner.

Befintliga distributioner fortsätter att fungera. Från och med den här aktuella gren versionen är Azure Resource Manager den enda distributions metoden för nya instanser av Cloud Management Gateway och moln distributions platsen.

Mer information finns i [Azure Resource Manager för Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).

### <a name="add-cloud-management-gateway-to-boundary-groups"></a>Lägg till Cloud Management Gateway till gränser grupper

<!--3640932-->
Nu kan du associera en Cloud Management Gateway (CMG) med en avgränsnings grupp. Den här konfigurationen gör det möjligt för klienter att default eller återgå till CMG för klient kommunikation baserat på gränser grupp relationer. Det här beteendet är särskilt användbart i avdelnings kontor och VPN-scenarier. Du kan dirigera klient trafiken bort från dyra och långsamma WAN-länkar för att i stället använda snabbare Internet länkar till Microsoft Azure.

Mer information finns i [CMG-hierarki](../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design) och [Konfigurera CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#configure-boundary-groups).


## <a name="real-time-management"></a><a name="bkmk_real"></a> Real tids hantering

### <a name="run-cmpivot-from-the-central-administration-site"></a>Kör CMPivot från den centrala administrations platsen

<!--3610960-->
Configuration Manager stöder nu att köra CMPivot från den centrala administrations platsen i en hierarki. Den primära platsen hanterar fortfarande kommunikationen till klienten. När du kör CMPivot från den centrala administrations platsen kommunicerar den med den primära platsen via prenumerations kanalen för snabb meddelanden. Den här kommunikationen är inte beroende av standard-SQL-replikering mellan platser.

Mer information finns i [CMPivot för real tids data](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1902).

### <a name="edit-or-copy-powershell-scripts"></a>Redigera eller kopiera PowerShell-skript

<!--3705507-->
Nu kan du **redigera** eller **Kopiera** ett befintligt PowerShell-skript som används med funktionen kör skript. I stället för att skapa ett skript som du behöver ändra direkt redigerar du det nu. Båda åtgärderna använder samma guide upplevelse som när du skapar ett nytt skript. När du redigerar eller kopierar ett skript behåller Configuration Manager inte godkännande statusen.

Mer information finns i [köra skript](../../../apps/deploy-use/create-deploy-scripts.md#bkmk_psedit).


## <a name="content-management"></a><a name="bkmk_content"></a> Innehålls hantering

### <a name="distribution-point-maintenance-mode"></a>Underhålls läge för distributions punkt

<!--3555754-->

Nu kan du ange en distributions plats i underhålls läge. Aktivera underhålls läge när du installerar program uppdateringar eller gör ändringar av maskin varan på servern.

Även om distributions platsen är i underhålls läge, har den följande beteenden:

- Webbplatsen distribuerar inget innehåll till den.  

- Hanterings platser returnerar inte platsen för den här distributions platsen till klienter.

- När du uppdaterar platsen uppdateras även en distributions plats i underhålls läge.

- Distributions plats egenskaperna är skrivskyddade. Du kan till exempel inte ändra certifikatet eller lägga till gränser grupper.  

- Alla schemalagda aktiviteter, t. ex. innehålls validering, körs fortfarande i samma schema.

Mer information om den här funktionen finns i [underhålls läge](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_maint).

Mer information om hur du automatiserar den här processen med Configuration Manager SDK finns [i SetDPMaintenanceMode-metoden i klassen SMS_DistributionPointInfo](../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="client-management"></a><a name="bkmk_client"></a> Klient hantering

### <a name="client-provisioning-mode-timeout"></a>Timeout för klient etablerings läge

<!--3197824-->
Aktivitetssekvensen anger en tidsstämpel när klienten placeras i etablerings läge. En klient i etablerings läge kontrollerar var 60: e minut, efter tidsstämpeln. Om den är i etablerings läge i mer än 48 timmar, avslutar klienten automatiskt etablerings läget och startar om processen.

Mer information finns i [etablerings läge](../../../osd/understand/provisioning-mode.md).

### <a name="view-first-screen-only-during-remote-control"></a>Visa endast första skärmen under fjärr styrning

<!--3231732-->
När du ansluter till en klient med två eller flera övervakare kan det vara svårt att visa dem i Configuration Manager fjärr styrnings visaren. En operatör kan nu välja mellan att se **alla skärmar** eller den **första skärmen** .

Mer information finns i [så här fjärradministrerar du en Windows-klientdator](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).

### <a name="specify-a-custom-port-for-peer-wakeup"></a>Ange en anpassad port för aktivering av peer

<!--3605925-->
Nu kan du ange ett anpassat port nummer för Wake-up-proxy. I klient inställningar i gruppen **energispar funktioner** konfigurerar du inställningen för **Wake on LAN port number (UDP)**.  

Mer information finns i [så här konfigurerar du Wake on LAN](../../clients/deploy/configure-wake-on-lan.md).


## <a name="application-management"></a><a name="bkmk_app"></a> Program hantering

### <a name="improvements-to-application-approvals-via-email"></a>Förbättringar av program godkännanden via e-post

<!--3594063-->
Den här versionen har förbättrade funktioner för att ta emot e-postaviseringar för program begär Anden. Användarna kan alltid lägga till en kommentar till begäran från Software Center. Den här kommentaren visar på program förfrågan i Configuration Manager-konsolen. Nu visas kommentaren även i e-postmeddelandet. Med den här kommentaren i e-postmeddelandet kan god kännare fatta ett bättre beslut att godkänna eller avvisa begäran.

Mer information finns i [e-postaviseringar](../../../apps/deploy-use/app-approval.md#bkmk_email-approve).

### <a name="improvements-to-package-conversion-manager"></a>Förbättringar av Package Conversion Manager

<!-- SCCMDocs-pr issue #3357 -->
Den här versionen innehåller följande förbättringar av [Package Conversion Manager](../../../apps/pcm/package-conversion-manager.md):

- Schemalagda paket analyser körs var sjunde dag som standard
- PowerShell-cmdletar för att analysera och konvertera paket
- Allmänna fel korrigeringar och förbättringar


## <a name="os-deployment"></a><a name="bkmk_osd"></a> OS-distribution

### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>Förlopps status under aktivitetssekvensen plats uppgradering

<!--3747129-->
Nu visas en mer detaljerad förlopps indikator under en Windows 10-uppgradering på plats. Det här fältet visar förloppet för Windows-installationen, som annars tyst under aktivitetssekvensen. Användarna har nu viss insyn i det underliggande förloppet. Det hjälper till med problem som uppgraderings processen har pausats på grund av brist på förlopps indikator.  

![Exempel förlopp för aktivitetssekvenser med Windows uppgraderings förlopp](media/3747129-installation-progress.png)

Den här funktionen fungerar med alla versioner av Windows 10 som stöds och endast med aktivitetssekvensen för uppgradering på plats.

### <a name="improvements-to-task-sequence-media-creation"></a>Förbättringar av genereringen av aktivitetssekvenser

<!--3556027, fka 1359388-->
Den här versionen innehåller flera förbättringar som hjälper dig att skapa och hantera media för aktivitetssekvenser bättre. Mer information finns i följande artiklar för olika medie typer:

- [Skapa fristående media](../../../osd/deploy-use/create-stand-alone-media.md)
- [Skapa förinstallerade media](../../../osd/deploy-use/create-prestaged-media.md)
- [Skapa startbara media](../../../osd/deploy-use/create-bootable-media.md)
- [Skapa avbildningsmedia](../../../osd/deploy-use/create-capture-media.md)

#### <a name="specify-temporary-storage"></a>Ange tillfällig lagring

När du skapar media för aktivitetssekvenser kan du nu anpassa platsen som platsen använder för tillfällig data lagring. Den här processen kan kräva mycket temporärt enhets utrymme. Den här ändringen ger dig större flexibilitet att välja var de här temporära filerna ska lagras.

I **guiden skapa aktivitetssekvens**anger du en plats för **mellanlagringsmappen**. Som standard liknar den här platsen följande sökväg: `%UserProfile%\AppData\Local\Temp` .

#### <a name="add-a-label-to-the-media"></a>Lägg till en etikett till mediet

Nu kan du lägga till en etikett till media i en aktivitetssekvens. Med den här etiketten kan du bättre identifiera mediet när du har skapat det. I **guiden skapa aktivitetssekvens**anger du en **medie etikett**.

### <a name="import-a-single-index-of-an-os-image"></a>Importera ett enskilt index för en operativ system avbildning

<!--3719699-->
När du importerar en WIM-fil (Windows Image) till Configuration Manager kan du nu ange att ett enskilt index ska importeras automatiskt i stället för alla bild index i filen. Det här alternativet ger följande fördelar:

- Mindre avbildnings fil  
- Snabbare offlineunderhåll  
- Optimera avbildnings underhåll för en mindre bildfil efter offline-underhåll

När du importerar en operativ system avbildning väljer du alternativet för att **extrahera ett specifikt avbildnings index från den angivna wim-filen**. Välj sedan bild indexet i listan.  

Mer information finns i [lägga till en OS-avbildning](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages).

### <a name="optimized-image-servicing"></a>Optimerad avbildnings underhåll

<!--3555951-->
När du använder program uppdateringar på en operativ system avbildning, finns det ett nytt alternativ för att optimera utdata genom att ta bort alla ersatta uppdateringar. Optimeringen av offlineunderhåll gäller bara för avbildningar med ett enda index.

När du skapar ett schema för att uppdatera en operativ system avbildning väljer du alternativet för att **ta bort ersatta uppdateringar när avbildningen har uppdaterats**.

Mer information finns i [tillämpa program uppdateringar på en avbildning](../../../osd/get-started/manage-operating-system-images.md#bkmk_resetbase).

### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>Förbättringar för att köra PowerShell-skript i aktivitetssekvensen

<!--3556028, fka 1359389-->
Steget **kör PowerShell-skript** innehåller nu följande förbättringar:  

- Nu kan du ange Windows PowerShell-kod direkt i det här steget. Med den här ändringen kan du köra PowerShell-kommandon under en aktivitetssekvens utan att först skapa och distribuera ett paket med skriptet.

- När du väljer alternativet **Ange ett PowerShell-skript** väljer du **Redigera skript**. Det nya PowerShell-skript fönstret innehåller följande åtgärder:  

    - Redigera skriptet direkt  

    - Öppna ett befintligt skript från en fil  

    - Bläddra till ett befintligt godkänt skript i Configuration Manager

- Spara skript resultatet till en anpassad aktivitetssekvens  

- Om du vill inkludera skript parametrarna i aktivitetssekvensen anger du **OSDLogPowerShellParameters** till **Sant**för variabeln. Som standard är parametrarna inte i loggen.  

- Andra förbättringar som ger liknande funktioner som [kommando rads steget Kör](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) . Ange till exempel alternativa användarautentiseringsuppgifter eller ange en timeout.

> [!Important]  
> Om du vill dra nytta av den nya Configuration Manager-funktionen kan du, när du har uppdaterat platsen, även uppdatera klienter till den senaste versionen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.

Mer information finns i [kör PowerShell-skript](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

### <a name="other-improvements-to-os-deployment"></a>Andra förbättringar av OS-distributionen

<!--3633146,3641475,3654172,3734270-->
Den här versionen innehåller följande förbättringar av OS-distributionen:

- Det finns en ny **vy** som standard åtgärd för aktivitetssekvenser. <!--3633146-->  

- Dialog rutan fel i aktivitetssekvens visar nu mer information. Det visar namnet på det steg i aktivitetssekvensen som misslyckades. <!--3641475-->  

- När du ställer in variabeln **OSDDoNotLogCommand** på sant, döljer den nu även kommando raden från steget Kör kommando rad i logg filen. Den har tidigare bara maskerat program namnet från steget installera paket i Smsts. log.<!--3654172-->  

- När du aktiverar en PXE-svarare på en distributions plats utan Windows Deployment-tjänst kan den nu finnas på samma server som DHCP-tjänsten. <!--3734270--> Mer information finns i [Konfigurera minst en distributions plats att acceptera PXE-begäranden](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


## <a name="software-center"></a><a name="bkmk_userxp"></a> Software Center

### <a name="replace-toast-notifications-with-dialog-window"></a>Ersätt popup-meddelanden med dialog fönster

<!--3555947-->
Användare ser ibland inte Windows popup-meddelanden om en omstart eller en nödvändig distribution. Sedan visas inte upplevelsen för att försätta påminnelsen i vilo läge. Det här beteendet kan leda till en låg användar upplevelse när klienten når en tids gräns.

Nu när distributioner behöver en omstart eller program varu ändringar krävs kan du välja att använda en mer påträngande dialog ruta.

Mer information finns i [Planera för Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact)

### <a name="configure-user-device-affinity-in-software-center"></a>Konfigurera mappning mellan användare och enhet i Software Center

<!--3485366-->
Med [förbättringar av Software Center-infrastrukturen](whats-new-in-version-1806.md#software-center-infrastructure-improvements) från och med version 1806 krävs inte längre program katalogens plats Server roller i de flesta fall. Vissa kunder förlitar sig fortfarande på program katalogen så att användarna kan ange sin primära enhet för mappning mellan användare och enhet.

Nu kan användarna ange sin primära enhet i Software Center. Den här åtgärden gör dem till en primär användare av enheten i Configuration Manager.

Mer information finns i [Länka användare och enheter med mappning mellan användare och enhet](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="configure-default-views-in-software-center"></a>Konfigurera standardvyer i Software Center

<!--3612112-->
Den här versionen av Configuration Manager upprepas ytterligare om hur du kan anpassa Software Center:

- Ange standardlayout för program, antingen som paneler eller en lista  

    - Om en användare ändrar den här konfigurationen, behåller Software Center användarnas önskemål i framtiden  

- Konfigurera standard program filtret, antingen alla eller nödvändiga appar  

    - I Software Center används alltid standardvärdet. Användare kan ändra det här filtret, men Software Center behåller inte sina preferenser.

Ange de här inställningarna i **Software Center** -gruppen med klient inställningar.

Mer information finns i [om klient inställningar](../../clients/deploy/about-client-settings.md#bkmk_swctr_defaults).


## <a name="software-updates"></a><a name="bkmk_sum"></a> Program uppdateringar

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>Ange prioritet för funktions uppdateringar i Windows 10-underhåll

<!--3734525-->
Justera prioriteten med vilka klienter installerar en funktions uppdatering via [Windows 10-Underhåll](../../../osd/deploy-use/manage-windows-as-a-service.md). Som standard installerar-klienter nu funktions uppdateringar med högre bearbetnings prioritet.

Använd klient inställningar för att konfigurera det här alternativet. Konfigurera följande inställning i gruppen **program uppdateringar** : **Ange tråd prioritet för funktions uppdateringar**.

Mer information finns i [om klient inställningar](../../clients/deploy/about-client-settings.md#software-updates).


## <a name="office-management"></a><a name="bkmk_o365"></a> Office-hantering

### <a name="redirect-windows-known-folders-to-onedrive"></a>Omdirigera Windows-kända mappar till OneDrive

<!--3556021-->
Använd Configuration Manager för att flytta Windows-kända mappar till OneDrive för företag. Dessa mappar innehåller Skriv bord, dokument och bilder. För att förenkla dina Windows 10-uppgraderingar distribuerar du inställningarna till Windows 7-klienter innan du distribuerar en aktivitetssekvens.

Mer information om den här funktionen i OneDrive för företag finns i [omdirigera och flytta Windows-kända mappar till OneDrive](/onedrive/redirect-known-folders).

Börja [med att hitta Microsoft 365 klient-ID](/onedrive/find-your-office-365-tenant-id). Distribuera sedan 18.111.0603.0004 för OneDrive-synkronisering eller senare. Mer information finns i [distribuera OneDrive-appar med hjälp av Configuration Manager](/onedrive/deploy-on-windows).  

Om du vill skapa och distribuera en OneDrive för företag-profil går du till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen. Expandera **kompatibilitetsinställningar och välj**noden **OneDrive för företag-profiler** .  

Mer information finns i avsnittet omdirigera Windows kända mappar till OneDrive i artikeln om [OneDrive för företag-profiler](../../../compliance/deploy-use/onedrive-profile.md) .

### <a name="integration-for-microsoft-365-apps-for-enterprise-readiness"></a>Integrering för Microsoft 365-appar för företags beredskap

<!--3735402-->
Använd Configuration Manager för att identifiera enheter med hög exakthet som är klara att uppgraderas till Microsoft 365 appar för företag. Integrationen ger insikter om eventuella kompatibilitetsproblem med Office-tillägg och makron som används i din miljö. Använd sedan Configuration Manager för att distribuera Office till färdiga enheter.

Den befintliga Microsoft 365-instrument panelen för klient hantering innehåller nu en ny panel, **Office 365 ProPlus uppgraderingsberedskap**.

Mer information finns i [Microsoft 365 instrument panel för klient hantering](../../../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness)

### <a name="additional-languages-for-microsoft-365-updates"></a>Ytterligare språk för Microsoft 365 uppdateringar

<!--3555955-->
Configuration Manager stöder nu alla språk som stöds för Microsoft 365 klient uppdateringar. Uppdaterings arbets flödet delar nu upp 38-språken för **Windows Update** från de många språken för **klient uppdatering av Office 365**.

Mer information finns i [hantera Microsoft 365 uppdateringar](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_o365_lang)

### <a name="office-products-on-lifecycle-dashboard"></a>Instrument panel för Office-produkter på livs cykel

<!--3556026-->
Instrument panelen för produktens livs cykel innehåller nu information om installerade versioner av Office 2003 via Office 2016. Data visas när platsen har kört aktiviteten för livs cykel sammanfattning, som är var 24: e timme.

Mer information finns i [använda instrument panelen för produktens livs cykel](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md).


## <a name="phased-deployments"></a><a name="bkmk_pod"></a> Stegvisa distributioner

### <a name="dedicated-monitoring-for-phased-deployments"></a>Dedikerad övervakning för stegvisa distributioner

<!--3555949-->
Stegvisa distributioner har nu sin egen dedikerade övervaknings nod. Den här noden gör det lättare att identifiera stegvisa distributioner som du har skapat och navigera sedan till vyn övervakning av stegvis distribution. I Configuration Manager-konsolen går du till arbets ytan **övervakning** och väljer noden stegvisa **distributioner** . Den visar listan med stegvisa distributioner.

Mer information finns i [övervaknings vyn](../../../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_monitor)för stegvis distribution.

### <a name="improvement-to-phased-deployment-success-criteria"></a>Förbättring av lyckade kriterier för stegvis distribution

<!--3555946-->
Ange ytterligare kriterier för lyckad en fas i en stegvis distribution. I stället för en procents ATS kan det här villkoret nu också vara antalet enheter som har distribuerats. Det här alternativet är användbart när samlingens storlek är variabel och du har ett angivet antal enheter för att Visa lyckade innan du går vidare till nästa fas.

Skapa en stegvis distribution för en aktivitetssekvens, program uppdatering eller ett program. På sidan Inställningar i guiden väljer du sedan följande alternativ som kriterier för att lyckas med den första fasen: **antalet enheter har distribuerats**.

Mer information finns i skapa stegvisa [distributioner](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-konsol

### <a name="improvements-to-configuration-manager-console"></a><a name="bkmk_console"></a> Förbättringar i Configuration Manager-konsolen

<!--3594151-->
Baserat på kundfeedback på Mellanvästern Management Summit (MMS) Desert Edition 2018, innehåller den här versionen följande förbättringar av Configuration Manager-konsolen:

- Maximera register fönstret Bläddra efter program identifierings metoder
- Gå till samlingen från en program distribution
- Ta bort innehåll från övervaknings status
- Vyer sorteras efter heltals värden i noden **distributioner** på arbets ytan **övervakning**
- Flytta varningen för ett stort antal resultat

Mer information finns i [Configuration Manager-konsol tips](../../servers/manage/admin-console-tips.md).

### <a name="configuration-manager-console-notifications"></a>Configuration Manager konsol meddelanden

<!--3556016, fka 1318035-->
För att hålla dig informerad så att du kan vidta lämpliga åtgärder, kommer Configuration Manager-konsolen nu att meddela dig om följande händelser:

- När en uppdatering är tillgänglig för Configuration Manager
- När livs cykel-och underhålls händelser inträffar i miljön

Det här meddelandet är ett fält överst i konsol fönstret under menyfliksområdet. Den tidigare upplevelsen ersätts när Configuration Manager uppdateringar är tillgängliga. Dessa meddelanden i konsolen visar fortfarande viktig information, men stör inte ditt arbete i-konsolen. Du kan inte ignorera viktiga meddelanden. I-konsolen visas alla meddelanden i ett nytt meddelande fält i namn listen.

Mer information finns i [Configuration Manager konsol meddelanden](../../servers/manage/admin-console-notifications.md).

### <a name="confirmation-of-console-feedback"></a>Bekräftelse av konsol kommentarer

<!--3556010-->
När du skickar [feedback](../../understand/find-help.md#product-feedback) i Configuration Manager-konsolen visas nu ett bekräftelse meddelande. Det här meddelandet innehåller ett **feedback-ID**, som du kan ge till Microsoft som ett spårnings-ID.

Mer information finns i [produkt feedback](../../understand/find-help.md#bkmk_feedbackid).

### <a name="view-recently-connected-consoles"></a>Visa nyligen anslutna konsoler

<!--3699367-->
Nu kan du Visa de senaste anslutningarna för Configuration Manager-konsolen. Vyn innehåller aktiva anslutningar och de konsoler som nyligen var anslutna. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **säkerhet**och väljer noden **konsol anslutningar** .

Mer information finns i [använda Configuration Manager-konsolen](../../servers/manage/admin-console.md#bkmk_viewconnected).

### <a name="in-console-documentation-dashboard"></a>Instrument panel för dokumentation i konsolen

<!--3556019, fka 1357546-->
Det finns en ny **dokumentations** nod på den nya **Community** -arbetsytan. Den här noden innehåller uppdaterad information om Configuration Manager dokumentation och support artiklar.

Mer information finns i [använda Configuration Manager-konsolen](../../servers/manage/admin-console.md#bkmk_doc-dashboard).

### <a name="search-device-views-using-mac-address"></a>Sök i enhets visningar med MAC-adress

<!--3600878-->
Nu kan du söka efter en MAC-adress i en enhets vy i Configuration Manager-konsolen. Den här egenskapen är användbar för distributions administratörer för operativ system medan PXE-baserade distributioner felsöks. När du visar en lista över enheter, lägger du till kolumnen **MAC-adress** i vyn. Använd Sök fältet för att lägga till Sök kriterierna för **MAC-adressen** .

Mer information finns i [Configuration Manager-konsol tips](../../servers/manage/admin-console-tips.md).

### <a name="use-net-47-for-improved-console-accessibility"></a>Använd .NET 4,7 för förbättrad konsol tillgänglighet

<!-- SCCMDocs-pr issue #3228 -->
Om du vill förbättra hjälpmedels funktionerna i Configuration Manager-konsolen uppdaterar du .NET till version 4,7 eller senare på datorn som kör-konsolen.

Mer information finns [i hjälpmedels funktioner i Configuration Manager](../../understand/accessibility-features.md).

### <a name="changes-to-console-setup-process"></a>Ändringar i installationen av konsolen

<!-- 3612513 -->
Det krävs nya komponenter när du installerar Configuration Manager-konsolen. Om du skapar ett paket för att installera-konsolen på andra datorer måste du kontrol lera att paketet innehåller följande filer:

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab
- ConfigMgr.AC_Extension.amd64.cab

När du installerar eller uppdaterar en plats Server kopieras installationsfilerna och de språk paket som stöds för platsen till undermappen **Tools\ConsoleSetup** . Mer information finns i [installera Configuration Manager-konsolen](../../servers/deploy/install/install-consoles.md).


## <a name="other-updates"></a>Övriga uppdateringar

Förutom nya funktioner innehåller den här versionen även ytterligare ändringar som fel korrigeringar. Mer information finns i [Sammanfattning av ändringar i Configuration Manager aktuella grenen, version 1902](https://support.microsoft.com/help/4498910).

Mer information om ändringar i Windows PowerShell-cmdlets för Configuration Manager finns i [versions anteckningar för PowerShell version 1902](/powershell/sccm/1902-release-notes?view=sccm-ps).

Följande samlade uppdateringar (4500571) är tillgängliga i-konsolen från och med 17 juni 2019: [Samlad uppdatering för Configuration Manager aktuell gren, version 1902](https://support.microsoft.com/help/4500571).

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

När du är redo att installera den här versionen, se [Installera uppdateringar för Configuration Manager](../../servers/manage/updates.md) och [Check lista för att installera uppdatering 1902](../../servers/manage/checklist-for-installing-update-1902.md).

> [!TIP]  
> Om du vill installera en ny plats använder du en bas linje version av Configuration Manager.  
>
> Läs mer om:    
> - [Nya platser installeras](../../servers/deploy/install/installing-sites.md)  
> - [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines)  

För kända, betydande problem, se [viktig information](../../servers/deploy/install/release-notes.md).

När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist).