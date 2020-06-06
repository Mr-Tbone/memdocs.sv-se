---
title: Loggfilsreferens
titleSuffix: Configuration Manager
description: En referens till alla loggfiler för Configuration Manager klient, server och beroende komponenter.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11efada9eaf7e16a68902d7d6d78fb6708916d05
ms.sourcegitcommit: e618ea7cb864635c838b672bc71a1e926bf7c047
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2020
ms.locfileid: "84458142"
---
# <a name="log-file-reference"></a>Loggfilsreferens

*Gäller för: Configuration Manager (aktuell gren)*

I Configuration Manager registrerar klient-och plats Server komponenter process information i individuella loggfiler. Du kan använda informationen i dessa loggfiler för att felsöka problem som kan uppstå. Som standard aktiverar Configuration Manager loggning för klient-och Server komponenter.

Mer allmän information om loggfiler i Configuration Manager finns i [logg filen](about-log-files.md). Artikeln innehåller information om vilka verktyg som ska användas, hur du konfigurerar loggarna och var de finns.

I följande avsnitt finns information om de olika loggfilerna som är tillgängliga för dig. Övervaka Configuration Manager klient-och Server loggar för åtgärds information och Visa fel information för att felsöka problem.  

- [Loggfiler för klienter](#BKMK_ClientLogs)  

  - [Klient åtgärder](#BKMK_ClientOpLogs)  

  - [Klient installation](#BKMK_ClientInstallLog)  

  - [Klienter för Linux och UNIX](#BKMK_LogFilesforLnU)  

  - [Klient för Mac-datorer](#BKMK_LogfilesforMac)  

- [Serverns loggfiler](#BKMK_ServerLogs)  

  - [Platsserver och platssystem](#BKMK_SiteSiteServerLog)  

  - [Installation av plats Server](#BKMK_SiteInstallLog)

  - [Informations lager service punkt](#BKMK_DataWarehouse)

  - [Status för återställningsplats](#BKMK_FSPLog)  

  - [Hanterings plats](#BKMK_MPLog)  

  - [Tjänst anslutnings punkt](#BKMK_WITLog)  

  - [Program uppdaterings plats](#BKMK_SUPLog)  

- [Loggfiler efter funktioner](#BKMK_FunctionLogs)  

  - [Programhantering](#BKMK_AppManageLog)  

  - [Tillgångsinformation](#BKMK_AILog)  

  - [Säkerhetskopiering och återställning](#BKMK_BnRLog)  

  - [Certifikat registrering](#BKMK_CertificateEnrollment)

  - [Klientmeddelande](#BKMK_BGB)

  - [Gateway för molnhantering](#cloud-management-gateway)

  - [Kompatibilitetsinställningar och åtkomst till företags resurser](#BKMK_CompSettingsLog)  

  - [Configuration Manager-konsol](#BKMK_ConsoleLog)  

  - [Innehållshantering](#BKMK_ContentLog)  

  - [Desktop Analytics](#desktop-analytics)

  - [Identifikation](#BKMK_DiscoveryLog)  

  - [Endpoint Protection](#BKMK_EPLog)  

  - [Tillägg](#BKMK_Extensions)  

  - [Lager](#BKMK_InventoryLog)  

  - [Migrering](#BKMK_MigrationLog)  

  - [Mobila enheter](#BKMK_MDMLog)  

  - [Distribution av operativsystem](#BKMK_OSDLog)  

  - [Energisparfunktioner](#BKMK_PowerMgmtLog)  

  - [Fjärrstyrning](#BKMK_RCLog)  

  - [Rapportering](#BKMK_ReportLog)  

  - [Rollbaserad administration](#BKMK_RBALog)  

  - [Avläsning av program vara](#BKMK_MeteringLog)  

  - [Programuppdateringar](#BKMK_SU_NAPLog)  

  - [Wake On LAN](#BKMK_WOLLog)  

  - [Windows 10-underhåll](#BKMK_WindowsServicingLog)

  - [Windows Update-agent](#BKMK_WULog)  

  - [WSUS-Server](#BKMK_WSUSLog)  

## <a name="client-log-files"></a><a name="BKMK_ClientLogs"></a>Loggfiler för klienter

I följande avsnitt listas loggfilerna som rör klient åtgärder och klient installation.  

### <a name="client-operations"></a><a name="BKMK_ClientOpLogs"></a>Klient åtgärder

I följande tabell listas loggfilerna som finns på Configuration Manager-klienten.  

|Loggnamn|Beskrivning|  
|--------------|-----------------|  
|ADALOperationProvider. log|Information om begär Anden om klientautentisering med Azure Active Directory (Azure AD) Authentication Library (ADAL).|
|BitLockerManagementHandler. log|Registrerar information om hanterings principer för BitLocker.|
|CAS.log|Innehålls åtkomst tjänsten. Underhåller den lokala paketcachen på klienten.|  
|Ccm32BitLauncher.log|Registrerar åtgärder för att starta program på klienten markerad *som kör som 32-bit*.|  
|CcmEval.log|Registrerar Configuration Manager utvärderings aktiviteter för klient status och Detaljer för komponenter som krävs av Configuration Manager-klienten.|  
|CcmEvalTask.log|Registrerar utvärderings aktiviteter för Configuration Manager klient status som startas av den schemalagda utvärderings aktiviteten.|  
|CcmExec.log|Registrerar aktiviteter för klienten och tjänsten Värd för SMS-agent. Den här loggfilen innehåller även information om aktivering och inaktivering av aktiveringsproxy.|  
|CcmMessaging.log|Registrerar aktiviteter relaterade till kommunikation mellan klienten och hanterings platserna.|  
|CCMNotificationAgent.log|Registrerar aktiviteter relaterade till klientaviseringsåtgärder.|  
|Ccmperf.log|Innehåller information om aktiviteter som rör underhållet och insamlingen av data som rör klienters prestandaräknare.|  
|CcmRestart.log|Registrerar omstartsaktivitet för klienttjänster.|  
|CCMSDKProvider.log|Registrerar aktiviteter för klientens SDK-gränssnitt.|  
|ccmsqlce. log|Registrerar aktiviteter för den SQL Compact-version som klienten använder. Den här loggen används vanligt vis bara när du aktiverar fel söknings loggning eller också är det problem med komponenten. Klient hälso aktiviteten (ccmeval) brukar korrigera problem med den här komponenten.|
|CertificateMaintenance.log|Underhåller certifikat för Active Directory Domain Services och hanteringsplatser.|  
|CIDownloader.log|Registrerar detaljer om nedladdningar av definitioner av konfigurationsobjekt.|  
|CITaskMgr.log|Registrerar aktiviteter för varje program och distributions typ, t. ex. innehåll som hämtas och installeras eller avinstalleras.|  
|ClientAuth.log|Registrerar signerings-och autentiserings aktivitet för klienten.|  
|ClientIDManagerStartup.log|Skapar och underhåller klient-GUID och identifierar aktiviteter under klient registrering och-tilldelning.|  
|ClientLocation.log|Registrerar aktiviteter relaterade till klientplatstilldelning.|  
|CMHttpsReadiness.log|Registrerar resultaten av att köra verktyget Configuration Manager HTTPS readiness Assessment. Det här verktyget kontrollerar om datorer har ett certifikat för PKI-klientautentisering (Public Key Infrastructure) som kan användas med Configuration Manager.|  
|CmRcService.log|Registrerar information för fjärrstyrningstjänsten.|  
|CoManagementHandler. log|Använd för att felsöka samhantering på klienten.|
|ContentTransferManager.log|Schemalägger Background Intelligent Transfer Service (BITS) eller SMB (Server Message Block) för att ladda ned eller komma åt paket.|  
|DataTransferService.log|Innehåller information om all BITS-kommunikation för princip- eller paketåtkomst.|  
|DeltaDownload. log|Registrerar information om hämtning av Express uppdateringar och uppdateringar som hämtats med hjälp av leverans optimering.|  
|Diagnostics. log|Registrerar status för klient diagnos åtgärder.|
|EndpointProtectionAgent|Innehåller information om installationen av System Center Endpoint Protection-klienten och tillämpningen av principer för program mot skadlig kod på klienten.|  
|execmgr.log|Registrerar information om paket och aktivitetssekvenser som körs på klienten.|  
|ExpressionSolver.log|Registrerar Detaljer om förbättrade identifierings metoder som används när utförlig loggning eller fel söknings loggning aktive ras.|  
|ExternalEventAgent.log|Registrerar historiken för igenkänning av skadlig kod med Endpoint Protection och händelser relaterade till klientstatus.|  
|FileBITS.log|Registrerar alla aktiviteter gällande SMB-paketåtkomst.|  
|FileSystemFile.log|Registrerar aktiviteten för providern för WMI (Windows Management Instrumentation) för programvaruinventering och filinsamling.|  
|FSPStateMessage.log|Registrerar aktiviteten för statusmeddelanden som skickas till återställningsstatusplatsen av klienten.|  
|InternetProxy.log|Registrerar konfigurationen för nätverks-proxy och använder aktiviteten för-klienten.|  
|InventoryAgent.log|Innehåller information om aktiviteter som rör maskinvaruinventering, programinventering och pulsslagsidentifieringsåtgärder på klienten.|  
|LocationCache.log|Registrerar aktiviteten för platsens cache-användning och underhåll för-klienten.|  
|LocationServices.log|Registrerar klientaktivitet för att hitta hanteringsplatser, programuppdateringsplatser och distributionsplatser.|  
|M365AHandler. log|Information om inställnings principen för Skriv bords analys|
|MaintenanceCoordinator.log|Registrerar aktiviteten för allmänna underhålls aktiviteter för klienten.|  
|Mifprovider.log|Registrerar aktiviteten för WMI-providern för MIF-filer (Management information format).|  
|mtrmgr.log|Övervakar alla programmätningsprocesser.|  
|PolicyAgent.log|Registrerar begäran om principer som görs med hjälp av tjänsten Dataöverföring.|  
|PolicyAgentProvider.log|Registrerar ändringar i principer.|  
|PolicyEvaluator.log|Innehåller information om utvärderingen av principer på klientdatorer, däribland principer från programuppdateringar.|  
|PolicyPlatformClient.log|Registrerar processen för reparation och efterlevnad för alla providers som finns i \Program\microsoft Policy Platform, förutom fil leverantören.|  
|PolicySdk.log|Registrerar aktiviteter för principsystem-SDK-gränssnitt.|  
|Pwrmgmt.log|Registrerar information om aktivering, inaktivering och konfigurering av klientinställningar för aktiveringsproxy.|  
|PwrProvider.log|Registrerar aktiviteter för Power Management-providern (PWRInvProvider) som finns i WMI-tjänsten. På alla versioner av Windows som stöds räknar providern upp de aktuella inställningarna på datorer som inventerar maskinvara och använder energisparinställningar.|  
|SCClient_ &lt; *domän* \> @ &lt; *användar namn* \> _1. log|Registrerar aktiviteten i Software Center för angiven användare på klientdatorn.|  
|SCClient_ &lt; *domän* \> @ &lt; *användar namn* \> _2. log|Registrerar den historiska aktiviteten i Software Center för angiven användare på klientdatorn.|  
|Scheduler.log|Registrerar aktiviteter för schemalagda aktiviteter för alla klientåtgärder.|  
|SCNotify_ &lt; *domän* \> @ &lt; *användar namn* \> _1. log|Registrerar aktiviteten för att avisera användare om programvara för den angivna användaren.|  
|SCNotify_ &lt; *domän* \> @ &lt; *användar namn* \> _1- &lt; *Date_Time*>. log|Registrerar den historiska informationen för att avisera användare om programvara för den angivna användaren.|  
|setuppolicyevaluator.log|Registrerar konfiguration och skapande av inventeringsprincip i WMI.|  
|SleepAgent_ &lt; *domän*\>@SYSTEM_0.log|Huvud logg filen för Väcknings-proxy.|  
|smscliui.log|Registrerar användningen av Configuration Manager-klienten i kontroll panelen.|  
|SrcUpdateMgr.log|Registrerar aktivitet för installerade Windows Installer-program som uppdateras med aktuella källplaceringar för distributionsplatser.|  
|StatusAgent.log|Registrerar statusmeddelanden som skapas av klientkomponenter.|  
|SWMTRReportGen.log|Genererar en användnings data rapport som samlas in av mätar agenten. Dessa data loggas i Mtrmgr.log.|  
|UserAffinity.log|Registrerar detaljer om mappning mellan användare och enhet.|  
|VirtualApp.log|Registrerar information som är specifik för utvärderingen av distributions typer för Application Virtualization (App-V).|  
|Wedmtrace.log|Registrerar operationer relaterade till skrivfilter på Windows Embedded-klienter.|  
|wakeprxy-install.log|Registrerar installations information när klienter tar emot klient inställnings alternativet för aktivering av Väcknings proxy.|  
|wakeprxy-uninstall.log|Innehåller information om avinstallation av Wake-up-proxy när klienter tar emot klient inställnings alternativet för att inaktivera Wake-up-proxy, om Wake-up proxy tidigare har Aktiver ATS.|  

### <a name="client-installation"></a><a name="BKMK_ClientInstallLog"></a>Klient installation

I följande tabell listas loggfilerna som innehåller information som rör installationen av Configuration Manager-klienten.  

|Loggnamn|Beskrivning|  
|--------------|-----------------|  
|ccmsetup.log|Registrerar CCMSetup. exe-aktiviteter för klient konfiguration, klient uppgradering och borttagning av klienter. Kan användas för att felsöka problem med klientinstallation.|  
|ccmsetup-ccmeval.log|Registrerar CCMSetup. exe-aktiviteter för klient status och reparation.|  
|CcmRepair.log|Registrerar klientagentens reparationsaktiviteter.|  
|client.msi.log|Registrerar konfigurations uppgifter som gjorts av client. msi. Kan användas för att felsöka problem med installation eller borttagning av klient.|  

### <a name="client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a>Klient för Linux och UNIX

> [!Important]  
> Från och med version 1902 stöder Configuration Manager inte Linux-eller UNIX-klienter.
>
> Överväg Microsoft Azure hantering för hantering av Linux-servrar. Azure-lösningar har omfattande Linux-support som i de flesta fall överskrider Configuration Manager-funktioner, inklusive slut punkt till slut punkt för korrigerings hantering för Linux.

Configuration Manager-klienten för Linux och UNIX registrerar information i följande loggfiler:  

> [!TIP]
> Använd CMTrace för att Visa loggfilerna för klienten för Linux och UNIX.

|Loggnamn|Information|
|-------------------|-----------------------------------------------------------------|
|Scxcm. log| Logg filen för kärn tjänsten i Configuration Manager-klienten för Linux och UNIX (ccmexec. bin). Den här loggfilen innehåller information om installation och pågående drift av ccmexec.bin. Den här logg filen finns som standard på **/var/opt/Microsoft/scxcm.log**. Du ändrar placeringen för loggfilen genom att redigera **/opt/microsoft/configmgr/etc/scxcm.conf** och ändra fältet **PATH**. Du behöver inte starta om klient datorn eller tjänsten för att ändringen ska börja gälla. Du kan ange loggnings nivån till någon av fyra olika inställningar. |
| Scxcmprovider. log |Logg filen för CIM-tjänsten för Configuration Manager-klienten för Linux och UNIX (omiserver. bin). Den här loggfilen innehåller information om pågående drift av nwserver.bin. Den här loggen finns på `/var/opt/microsoft/configmgr/scxcmprovider.log` . Du ändrar placeringen för loggfilen genom att redigera **/opt/microsoft/omi/etc/scxcmprovider.conf** och ändra fältet **PATH**. Du behöver inte starta om klient datorn eller tjänsten för att ändringen ska börja gälla. Du kan ange loggnings nivån till någon av tre inställningar.|

Båda loggfiler stöder flera loggningsnivåer:  

- **scxcm. log**. Ändra loggnings nivån genom att redigera **/opt/Microsoft/ConfigMgr/etc/scxcm.conf** och ändra varje instans av taggen **modul** till den logg nivå som du vill använda:  

  - FEL: anger problem som kräver åtgärd  

  - Varning: anger möjliga problem för klient åtgärder  

  - INFO: mer detaljerad loggning som anger status för olika händelser på klienten  

  - SPÅRA: utförlig loggning som vanligt vis används för att diagnostisera problem  

- **scxcmprovider. log**. Ändra loggnings nivån genom att redigera **/opt/microsoft/omi/etc/scxcmprovider.conf** och ändra varje instans av taggen **modul** till den logg nivå som du vill använda:  

  - FEL: anger problem som kräver åtgärd  

  - Varning: anger möjliga problem för klient åtgärder

  - INFO: mer detaljerad loggning som anger status för olika händelser på klienten  

Under normala drifts förhållanden använder du fel loggnings nivån. Den här logg nivån skapar den minsta logg filen. När logg nivån ökas från fel till varning, till information och sedan till spårning, skapas en större loggfil när mer data skrivs till filen.  

#### <a name="manage-log-files-for-the-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a>Hantera loggfiler för Linux-och UNIX-klienten

Klienten för Linux och UNIX begränsar inte den maximala storleken för klientens loggfiler. Innehållet i dess. log-filer kopieras inte heller automatiskt till en annan fil, till exempel en. lo_-fil. Om du vill kontrol lera den maximala storleken på loggfiler implementerar du en process för att hantera loggfilerna oberoende av Configuration Manager-klienten för Linux och UNIX.  

Du kan till exempel använda standard kommandot **logrotate** i Linux och UNIX för att hantera storlek och rotation för klientens loggfiler. Configuration Manager-klienten för Linux och UNIX har ett gränssnitt som gör det möjligt för **logrotate** att signalera klienten när logg rotationen är klar, så att klienten kan återuppta loggningen till logg filen.  

Du hittar mer information om **logrotate** i dokumentationen till de Linux- och UNIX-distributioner du använder.  

### <a name="client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a>Klient för Mac-datorer

Configuration Manager-klienten för Mac-datorer registrerar information i följande loggfiler på Mac-datorn:  

|Loggnamn|Information|Location|
|--------------|-------------|-------------|
|CCMClient- &lt; *Date_Time*>. log|Registrerar aktiviteter som är relaterade till Mac-klienternas åtgärder, inklusive program hantering, inventering och fel loggning.| `/Library/Application Support/Microsoft/CCM/Logs`|  
|CCMAgent- &lt; *Date_Time*>. log|Registrerar information som rör klient åtgärder, inklusive inloggnings-och inloggnings åtgärder samt Mac-datorns aktivitet.| `~/Library/Logs`|  
|CCMNotifications- &lt; *Date_Time*>. log|Registrerar aktiviteter som är relaterade till Configuration Manager-meddelanden som visas på Mac-datorn.| `~/Library/Logs`|  
|CCMPrefPane- &lt; *Date_Time*>. log|Registrerar aktiviteter relaterade till dialog rutan Configuration Manager inställningar på Mac-datorn, vilket omfattar allmän status och fel loggning.| `~/Library/Logs`|  

Logg filen **SMS_DM. log** på plats system servern registrerar även kommunikationen mellan Mac-datorer och hanterings platsen som har kon figurer ATS för mobila enheter och Mac-datorer.  

## <a name="server-log-files"></a><a name="BKMK_ServerLogs"></a>Serverns loggfiler

I följande avsnitt listas loggfiler som finns på plats servern eller som är relaterade till vissa plats system roller.  

### <a name="site-server-and-site-systems"></a><a name="BKMK_SiteSiteServerLog"></a>Plats Server och plats system

I följande tabell visas de loggfiler som finns på Configuration Manager plats Server och plats system servrar.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Registrerar registreringsbehandlingsaktivitet.|Platsserver|  
|ADForestDisc.log|Innehåller information om åtgärder som rör Identifiering av Active Directory-skogar.|Platsserver|  
|adminservice. log|Registrerar åtgärder för administrations tjänsten för SMS-provider REST API|Dator med SMS-provider|
|ADService.log|Registrerar skapande av konton och säkerhetsgruppsdetaljer i Active Directory.|Platsserver|  
|adsgdis.log|Registrerar åtgärder för identifiering av Active Directory-grupper.|Platsserver|  
|adsysdis.log|Innehåller information om åtgärder som rör Identifiering av Active Directory-system.|Platsserver|  
|adusrdis.log|Innehåller information om åtgärder som rör Identifiering av Active Directory-användare.|Platsserver|  
|BusinessAppProcessWorker. log|Bearbetar bearbetning för Microsoft Store för företags program.|Platsserver|
|ccm.log|Registrerar aktiviteter för push-installation av klienter.|Platsserver|  
|CertMgr.log|Registrerar certifikat aktiviteter för kommunikation mellan platser.|Platssystemserver|  
|chmgr.log|Registrerar aktiviteter för klientens hälsoindikator.|Platsserver|  
|Cidm.log|Registrerar ändringar som görs i klientinställningarna av CIDM (Client Install Data Manager).|Platsserver|  
|CollectionAADGroupSyncWorker. log | Från och med version 2002, logg filen för synkronisering av samlings medlemskaps resultat till Azure Active Directory. I version 1910 och tidigare har loggning för den här funktionen kombinerats i SMS_AZUREAD_DISCOVERY_AGENT. log. | Platsserver|
|colleval.log|Registrerar information när samlingar skapas, ändras och tas bort av Samlingsutvärderaren.|Platsserver|  
|compmon.log|Registrerar status för komponenttrådar som övervakas för platsservern.|Platssystemserver|  
|compsumm.log|Registrerar aktiviteter för Sammanfattning för komponentstatus.|Platsserver|  
|ComRegSetup.log|Registrerar den ursprungliga installationen av COM-registreringsresultat för en platsserver.|Platssystemserver|  
|Dataldr.log|Registrerar information om bearbetning av MIF-filer och maskin varu inventering i Configuration Manager databasen.|Platsserver|  
|ddm.log|Registrerar aktiviteter hos identifieringsdatahanteraren.|Platsserver|  
|despool.log|Registrerar inkommande kommunikationsöverföring mellan platser.|Platsserver|  
|distmgr.log|Registrerar information om skapande av paket, komprimering, deltareplikering och informationsuppdateringar. Den kan även innehålla andra aktiviteter från distributions hanterarens komponent. Till exempel när du installerar en distributions plats, anslutnings försök och installerar komponenter. Mer information om andra funktioner som använder den här loggen finns i [tjänst anslutnings punkt](#BKMK_WITLog) och [distribution av operativ system](#BKMK_OSDLog).|Platsserver|  
|EPCtrlMgr.log|Innehåller information om synkronisering av information om hot från skadlig kod från Endpoint Protection plats system roll servern med Configuration Manager-databasen.|Platsserver|  
|EPMgr.log|Registrerar status för platssystemrollen Endpoint Protection.|Platssystemserver|  
|EPSetup.log|Ger information om installationen av Endpoint Protections platssystemsroll.|Platssystemserver|  
|EnrollSrv.log|Registrerar aktiviteter för registreringstjänstprocessen.|Platssystemserver|  
|EnrollWeb.log|Registrerar aktiviteter för registreringswebbplatsprocessen.|Platssystemserver|  
|fspmgr.log|Registrerar status för platssystemrollen återställningsstatusplats.|Platssystemserver|  
|hman.log|Registrerar information om ändringar i plats konfigurationen och om publicering av plats information i Active Directory Domain Services.|Platsserver|  
|Inboxast.log|Registrerar de filer som flyttas från hanteringsplatsen till motsvarande INBOXES-mapp på platsservern.|Platsserver|  
|inboxmgr.log|Registrerar filöverföringsaktiviteter mellan mappar för inkorgar.|Platsserver|  
|inboxmon.log|Registrerar behandling av filer för inkorgar och uppdateringar av prestandaräknaren.|Platsserver|  
|invproc.log|Innehåller information om vidarebefordran av MIF-filer från en sekundär plats till dess överordnade plats.|Platsserver|  
|migmctrl.log|Innehåller information om migrations åtgärder som involverar migreringsjobb, delade distributions platser och uppgraderingar av distributions platser.|Platsen på den översta nivån i Configuration Manager hierarkin och varje underordnad primär plats. Använd logg filen som skapas på den centrala administrations webbplatsen i en hierarki med flera primära platser.|  
|mpcontrol.log|Registrerar registreringen av hanterings platsen med Windows Internet Name Service (WINS). Registrerar tillgängligheten för hanteringsplatsen var 10:e minut.|Platssystemserver|  
|mpfdm.log|Registrerar åtgärder för den hanteringsplatskomponent som flyttar klientfiler till motsvarande INBOXES-mapp på platsservern.|Platssystemserver|  
|mpMSI.log|Registrerar information om installation av hanterings platsen.|Platsserver|  
|MPSetup.log|Registrerar adapterprocessen för installationen av hanteringsplatsen.|Platsserver|  
|netdisc.log|Innehåller information om nätverksidentifieringsåtgärder.|Platsserver|  
|NotiCtrl. log|Meddelanden om program begär Anden.|Platsserver|  
|ntsvrdis.log|Registrerar identifieringsaktivitet för platssystemservrar.|Platsserver|  
|Objreplmgr|Registrerar behandling av aviseringar om objektförändringar för replikering.|Platsserver|  
|offermgr.log|Registrerar annonsuppdateringar.|Platsserver|  
|offersum.log|Registrerar sammanfattningen av distributionsstatusmeddelanden.|Platsserver|  
|OfflineServicingMgr.log|Registrerar aktiviteter för att använda uppdateringar på operativsystemavbildningsfiler.|Platsserver|  
|outboxmon.log|Registrerar behandling av filer för utkorgar och uppdateringar av prestandaräknaren.|Platsserver|  
|PerfSetup.log|Registrerar resultaten av installationen av prestandaräknare.|Platssystemserver|  
|PkgXferMgr.log|Registrerar åtgärder för SMS_Executive-komponenten som ansvarar för att skicka innehåll från en primär plats till en fjärrdistributions plats.|Platsserver|  
|policypv.log|Registrerar uppdateringar som görs i klientprinciperna för att avspegla ändringar i klientinställningar eller distributioner.|Primär platsserver|  
|rcmctrl.log|Registrerar aktiviteter för databasreplikering mellan platser i hierarkin.|Platsserver|  
|replmgr.log|Registrerar replikering av filer mellan platsserverkomponenterna och komponenten Schemaläggaren.|Platsserver|  
|ResourceExplorer.log|Registrerar fel, varningar och information om att köra Resursläsaren.|Dator som kör Configuration Manager-konsolen|  
|RESTPROVIDERSetup. log|Installation av administrations tjänsten för SMS-provider REST API|Dator med SMS-provider|
|ruleengine.log|Registrerar detaljer om regler för automatisk distribution för grupperna för identifiering, nedladdning av innehåll och programuppdatering samt skapande av distributioner.|Platsserver|  
|schedule.log|Registrerar information om jobb mellan platser och filreplikering.|Platsserver|  
|sender.log|Registrerar de filer som överförs genom filbaserad replikering mellan platser.|Platsserver|  
|sinvproc.log|Innehåller information om bearbetningen av programinventeringsdata till platsdatabasen.|Platsserver|  
|sitecomp.log|Registrerar detaljer om underhåll av de installerade platskomponenterna på alla platsens platssystemservrar.|Platsserver|  
|sitectrl.log|Registrerar ändringar i platsinställningarna som gjorts på platskontrollobjekt i databasen.|Platsserver|  
|sitestat.log|Registrerar tillgänglighet och processen för övervakning av diskutrymme för alla platssystem.|Platsserver|
|SMS_AZUREAD_DISCOVERY_AGENT. log| Loggfil för användar-och användar grupp identifiering i Azure Active Directory (Azure AD). I version 1910 och tidigare innehöll den även synkronisering av medlemskaps resultat för samlingar till Azure AD.| Platsserver|
|SMS_BUSINESS_APP_PROCESS_MANAGER. log|Loggfil för komponent som synkroniserar appar från Microsoft Store för företag.|Platsserver|
|SMS_ISVUPDATES_SYNCAGENT. log| Loggfil för synkronisering av program uppdateringar från tredje part.| Program uppdaterings plats på den översta nivån i Configuration Manager hierarkin.|
|SMS_OrchestrationGroup. log| Loggfil för Orchestration-grupper|Platsserver|
|SMS_PhasedDeployment. log| Loggfil för stegvisa distributioner|Platsen på den översta nivån i Configuration Manager hierarkin|
|SMS_REST_PROVIDER. log|Tjänstens hälso tillstånd för administrations tjänsten för SMS-provider REST API, inklusive certifikat information|Dator med SMS-provider|
|SmsAdminUI.log|Registrerar Configuration Manager-konsol aktivitet.|Dator som kör Configuration Manager-konsolen|  
|SMSAWEBSVCSetup.log|Registrerar installationsaktiviteter för webbtjänsten för programkatalogen.|Platssystemserver|  
|smsbkup.log|Registrerar utdata från processen för att säkerhetskopiera platsen.|Platsserver|  
|smsdbmon.log|Registrerar ändringar i databasen.|Platsserver|  
|SMSENROLLSRVSetup.log|Registrerar installationsaktiviteter för webbtjänsten för registrering.|Platssystemserver|  
|SMSENROLLWEBSetup.log|Registrerar installationsaktiviteter för webbplatsen för registrering.|Platssystemserver|  
|smsexec.log|Registrerar behandling av alla platsserverkomponenttrådar.|Platsserver eller platssystemsserver|  
|SMSFSPSetup.log|Registrerar meddelanden som skapas av installation av en återställningsstatusplats.|Platssystemserver|  
|SMSPORTALWEBSetup.log|Registrerar installationsaktiviteter för webbplatsen för programkatalogen.|Platssystemserver|  
|SMSProv.log|Innehåller information om WMI-providerns åtkomst till platsdatabasen.|Dator med SMS-provider|  
|srsrpMSI.log|Registrerar detaljerade resultat från installationsprocessen för rapporteringsplatsen från MSI-utdata.|Platssystemserver|  
|srsrpsetup.log|Registrerar resultat från installationsprocessen för rapporteringsplatsen.|Platssystemserver|  
|statesys.log|Registrerar behandling av tillståndssystemmeddelanden.|Platsserver|  
|statmgr.log|Registrerar skrivning av alla statusmeddelanden till databasen.|Platsserver|  
|swmproc.log|Registrerar behandling av avläsningsfiler och inställningar.|Platsserver|  

### <a name="site-server-installation"></a><a name="BKMK_SiteInstallLog"></a>Installation av plats Server

Följande tabell listar de loggfiler som innehåller information relaterad till platsinstallationen.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Registrerar nödvändig komponent utvärderings-och installations aktiviteter.|Platsserver|  
|ConfigMgrSetup.log|Registrerar detaljerade utdata från installationen av plats servern.|Platsserver|  
|ConfigMgrSetupWizard.log|Registrerar information relaterad till aktivitet i installations guiden.|Platsserver|  
|SMS_BOOTSTRAP.log|Registrerar information om förloppet för att starta installationen av en sekundär plats. Detaljer om själva installationsprocessen finns i ConfigMgrSetup.log.|Platsserver|  
|smstsvc.log|Registrerar information om installation, användning och borttagning av en Windows-tjänst. Windows använder den här tjänsten för att testa nätverks anslutningar och behörigheter mellan servrar. Det använder dator kontot för den server som skapar anslutningen.|Plats Server och plats system Server|  

### <a name="data-warehouse-service-point"></a><a name="BKMK_DataWarehouse"></a>Informations lager service punkt

I följande tabell listas loggfilerna som innehåller information som rör informations lager tjänst platsen.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|DWSSMSI. log|Registrerar meddelanden som genereras av installationen av en service punkt för informations lager.|Platssystemserver|  
|DWSSSetup. log|Registrerar meddelanden som genereras av installationen av en service punkt för informations lager.|Platssystemserver|  
|Microsoft. ConfigMgrDataWarehouse. log|Registrerar information om datasynkronisering mellan plats databasen och informations lager databasen.|Platssystemserver|  

### <a name="fallback-status-point"></a><a name="BKMK_FSPLog"></a>Återställnings status punkt

Följande tabell listar de loggfiler som innehåller information relaterad till återställningsstatusplatsen.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Innehåller information om kommunikationen till återställningsstatusplatsen från äldre mobila klienter och klientdatorer.|Platssystemserver|  
|fspMSI.log|Registrerar meddelanden som skapas av installation av en återställningsstatusplats.|Platssystemserver|  
|fspmgr.log|Registrerar status för platssystemrollen återställningsstatusplats.|Platssystemserver|  

### <a name="management-point"></a><a name="BKMK_MPLog"></a>Hanterings plats

Följande tabell listar de loggfiler som innehåller information relaterad till hanteringsplatsen.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Registrerar klientmeddelandeaktivitet på slutpunkten.|Platssystemserver|  
|MP_CliReg.log|Registrerar den klientregistreringsaktivitet som behandlas av hanteringsplatsen.|Platssystemserver|  
|MP_Ddr.log|Registrerar konvertering av XML. DDR-poster från klienter och kopierar dem sedan till plats servern.|Platssystemserver|  
|MP_Framework.log|Registrerar aktiviteter för komponenterna för kärnhanteringsplatser och klientramverk.|Platssystemserver|  
|MP_GetAuth.log|Registrerar klientauktoriseringsaktivitet.|Platssystemserver|  
|MP_GetPolicy.log|Registrerar aktivitet för principbegäran från klientdatorer.|Platssystemserver|  
|MP_Hinv.log|Registrerar detaljer om konvertering av XML-poster för maskinvaruinventering från klienter och kopiering av dessa filer till platsservern.|Platssystemserver|  
|MP_Location.log|Registrerar aktivitet för placeringsbegäran och svar från klienter.|Platssystemserver|  
|MP_OOBMgr.log|Registrerar hanterings plats aktiviteter som är relaterade till att ta emot en eng ång slö sen ord från en klient.|Platssystemserver|  
|MP_Policy.log|Registrerar principkommunikation.|Platssystemserver|  
|MP_Relay.log|Registrerar överföring av filer som har samlats in från klienten.|Platssystemserver|  
|MP_Retry.log|Registrerar nya försök att bearbeta maskin varu inventering.|Platssystemserver|  
|MP_Sinv.log|Registrerar detaljer om konvertering av XML-poster för programvaruinventering från klienter och kopiering av dessa filer till platsservern.|Platssystemserver|  
|MP_SinvCollFile.log|Registrerar detaljer om filinsamling.|Platssystemserver|  
|MP_Status.log|Registrerar detaljer om konvertering av XML.svf-statusmeddelanden från klienter och kopiering av dessa filer till platsservern.|Platssystemserver|
|mpcontrol.log|Registrerar registreringen av hanteringsplatsen på WINS. Registrerar tillgängligheten för hanteringsplatsen var 10:e minut.|Platsserver|  
|mpfdm.log|Registrerar åtgärder för den hanteringsplatskomponent som flyttar klientfiler till motsvarande INBOXES-mapp på platsservern.|Platssystemserver|  
|mpMSI.log|Registrerar information om installation av hanterings platsen.|Platsserver|  
|MPSetup.log|Registrerar adapterprocessen för installationen av hanteringsplatsen.|Platsserver|  
|UserService. log|Registrerar användar förfrågningar från Software Center, hämtar/installerar användar tillgängliga program från servern.|Platssystemserver|

### <a name="service-connection-point"></a><a name="BKMK_WITLog"></a>Tjänst anslutnings punkt

I följande tabell listas loggfilerna som innehåller information som rör tjänstanslutningspunkten.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Innehåller certifikat- och proxykontoinformation.|Platsserver|  
|CollEval.log|Registrerar information när samlingar skapas, ändras och tas bort av Samlingsutvärderaren.|Primär plats och central administrationswebbplats|  
|Cloudusersync.log|Innehåller information om licensaktivering för användare.|Dator med tjänstanslutningspunkten|  
|Dataldr.log|Innehåller information om behandlingen av MIF-filer.|Platsserver|  
|ddm.log|Registrerar aktiviteter hos identifieringsdatahanteraren.|Platsserver|  
|Distmgr.log|Innehåller information om begäranden om innehållsdistribution.|Platsserver på översta nivån|  
|Dmpdownloader.log|Registrerar Detaljer om nedladdningar från Microsoft Intune.|Dator med tjänstanslutningspunkten|  
|Dmpuploader.log|Registrerar information som rör överföring av databas ändringar till Microsoft Intune.|Dator med tjänstanslutningspunkten|  
|hman.log|Innehåller information om vidarebefordran av meddelanden.|Platsserver|  
|MSfBSyncWorker. log|Registrerar information om kommunikationen med Microsoft Store för företag.|Dator med tjänstanslutningspunkten|
|objreplmgr.log|Innehåller information om bearbetningen av principer och tilldelningar.|Primär platsserver|  
|PolicyPV.log|Innehåller information om principgenerering för alla principer.|Platsserver|  
|outgoingcontentmanager.log|Registrerar innehåll som har överförts till Microsoft Intune.|Dator med tjänstanslutningspunkten|  
|Sitecomp.log|Innehåller information om installation av tjänstanslutningspunkt.|Platsserver|  
|SmsAdminUI.log|Registrerar Configuration Manager-konsol aktivitet.|Dator som kör Configuration Manager-konsolen|  
|SMS_CLOUDCONNECTION. log|Registrerar information om moln tjänster.|Dator med tjänstanslutningspunkten|
|Smsprov.log|Registrerar SMS-providerns aktiviteter. Configuration Manager-konsol aktiviteter använder SMS-providern.|Dator med SMS-provider|  
|SrvBoot.log|Innehåller information om installationstjänsten för tjänstanslutningspunkt.|Dator med tjänstanslutningspunkten|  
|Statesys.log|Innehåller information om bearbetningen av hanteringsmeddelanden för mobila enheter.|Primär plats och central administrationswebbplats|  

### <a name="software-update-point"></a><a name="BKMK_SUPLog"></a>Program uppdaterings plats

I följande tabell listas loggfilerna som innehåller information som rör program uppdaterings platsen.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Innehåller information om replikeringen av meddelandefiler av program uppdateringar från en överordnad plats till underordnade platser.|Platsserver|  
|PatchDownloader.log|Innehåller information om processen för att hämta programuppdateringar från uppdateringskällan till nedladdningsmålet på platsservern.|När du hämtar uppdateringar manuellt finns filen i din `%temp%` katalog på den dator där du använder-konsolen. För regler för automatisk distribution, om Configuration Manager-klienten är installerad på plats servern finns den här filen på plats servern i `%windir%\CCM\Logs` .|  
|ruleengine.log|Registrerar detaljer om regler för automatisk distribution för grupperna för identifiering, nedladdning av innehåll och programuppdatering samt skapande av distributioner.|Platsserver|
|SMS_ISVUPDATES_SYNCAGENT. log| Loggfil för synkronisering av program uppdateringar från tredje part.| Program uppdaterings plats på den översta nivån i Configuration Manager hierarkin.|
|SUPSetup.log|Innehåller information om installation av programuppdateringsplatsen. När installationen av programuppdateringsplatsen är klar skrivs texten **Installationen slutfördes** till denna loggfil.|Platssystemserver|  
|WCM.log|Innehåller information om konfigurationen av program uppdaterings platsen och anslutningar till WSUS-servern för prenumerationer på uppdaterings kategorier, klassificeringar och språk.|Plats server som ansluter till WSUS-servern|  
|WSUSCtrl.log|Innehåller information om konfigurationen, databasanslutningarna och hälsotillståndet hos platsens WSUS-server.|Platssystemserver|  
|wsyncmgr.log|Registrerar information om synkronisering av program uppdateringar.|Platssystemserver|  
|WUSSyncXML.log|Innehåller information om inventerings verktyget för Sync-processen för Microsoft Updates.|En klient dator som är konfigurerad som Sync-värd för inventerings verktyget för Microsoft Updates|  


## <a name="log-files-by-functionality"></a><a name="BKMK_FunctionLogs"></a>Loggfiler efter funktioner

I följande avsnitt listas loggfiler relaterade till Configuration Manager functions.  

### <a name="application-management"></a><a name="BKMK_AppManageLog"></a>Program hantering

I följande tabell listas loggfilerna som innehåller information som rör program hantering.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Innehåller information om det aktuella och avsedda programtillståndet, huruvida kraven var uppfyllda, distributionstyper och beroenden.|Klient|  
|AppDiscovery.log|Innehåller information om identifieringen eller detekteringen av program på klientdatorer.|Klient|  
|AppEnforce.log|Innehåller information om verkställningsåtgärder (installation och avinstallation) som har vidtagits med program på klienten.|Klient|  
|AppGroupHandler. log|Från och med version 1906, identifiering och tillämpnings information för program grupper|Klient|
|awebsctl.log|Registrerar övervaknings aktiviteter för plats system rollen Programkatalog-webbtjänst punkt.|Platssystemserver|  
|awebsvcMSI.log|Innehåller detaljerad installationsinformation om programkatalogens webbtjänstplats platssystemsroll.|Platssystemserver|  
|BusinessAppProcessWorker. log|Bearbetar bearbetning för Microsoft Store för företags program.|Platsserver|
|Ccmsdkprovider.log|Innehåller information om aktiviteterna som genomförs med programhanteringens SDK.|Klient|  
|colleval.log|Registrerar information när samlingar skapas, ändras och tas bort av Samlingsutvärderaren.|Platssystemserver|  
|ConfigMgrSoftwareCatalog.log|Innehåller information om programkatalogens aktiviteter, däribland hur den använder Silverlight.|Klient|  
|MSfBSyncWorker. log|Registrerar information om kommunikationen med Microsoft Store för företag.|Dator med tjänstanslutningspunkten|
|NotiCtrl. log|Meddelanden om program begär Anden.|Platsserver|  
|portlctl.log|Innehåller information om övervakningsaktiviteter för programkatalogens webbplats platssystemsroll.|Platssystemserver|  
|portlwebMSI.log|Innehåller information om MSI-installationsaktiviteter för programkatalogens webbplatsroll.|Platssystemserver|  
|PrestageContent.log|Innehåller information om användningen av verktyget ExtractContent. exe på en fjärran sluten distributions plats. Det här verktyget packar upp innehåll som har exporterats till en fil.|Platssystemserver|  
|ServicePortalWebService.log|Innehåller information om programkatalogens webbtjänsts aktiviteter.|Platssystemserver|  
|ServicePortalWebSite.log|Innehåller information programkatalogens webbplats aktiviteter.|Platssystemserver|  
|SettingsAgent. log|Tillämpning av specifika program, registrerar dirigering av program grupps utvärdering och information om samhanterings principer.|Klient|
|SMS_BUSINESS_APP_PROCESS_MANAGER. log|Loggfil för komponent som synkroniserar appar från Microsoft Store för företag.|Platsserver|
|SMS_CLOUDCONNECTION. log|Registrerar information om moln tjänster.|Dator med tjänstanslutningspunkten|
|SMSdpmon.log|Innehåller information om den schemalagda aktiviteten för övervakning av distributionsplatsens hälsa som är konfigurerad på en distributionsplats.|Platsserver|  
|SoftwareCatalogUpdateEndpoint.log|Registrerar aktiviteter för att hantera URL: en för Programkatalog som visas i Software Center.|Klient|  
|SoftwareCenterSystemTasks.log|Innehåller information om aktiviteter som är relaterade till den nödvändiga komponent valideringen av Software Center.|Klient|  
|TSDTHandler. log|För distributions typen för aktivitetssekvensen. Den loggar processen från App-tvång (installera eller avinstallera) till påstarten av aktivitetssekvensen. Använd den med AppEnforce. log och Smsts. log.|Klient|<!-- MEMDocs#336 -->

#### <a name="packages-and-programs"></a>Paket och program

I den följande tabellen listas loggfilerna som innehåller information som rör distribution av paket och program.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|colleval.log|Registrerar information när samlingar skapas, ändras och tas bort av Samlingsutvärderaren.|Platsserver|  
|execmgr.log|Innehåller information om paket och aktivitetssekvenser som körs.|Klient|  

### <a name="asset-intelligence"></a><a name="BKMK_AILog"></a>Tillgångsinformation

I den följande tabellen listas loggfilerna som innehåller information som rör Tillgångsinformation.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Innehåller information om aktiviteter som rör Tillgångsinformations inventeringsåtgärder.|Klient|  
|aikbmgr.log|Innehåller information om bearbetningen av XML-filer från inkorgen för uppdateringen av Tillgångsinformations katalog.|Platsserver|  
|AIUpdateSvc.log|Registrerar interaktionen för Tillgångsinformation-platsen för synkronisering med moln tjänsten.|Platssystemserver|  
|AIUSMSI.log|Innehåller information om installationen av plats system rollen för Tillgångsinformation-synkroniseringstjänsten.|Platssystemserver|  
|AIUSSetup.log|Innehåller information om installationen av plats system rollen för Tillgångsinformation-synkroniseringstjänsten.|Platssystemserver|  
|ManagedProvider.log|Innehåller information om identifiering av program med en motsvarande programidentifieringstagg. Registrerar även aktiviteter som rör maskin varu inventering.|Platssystemserver|  
|MVLSImport.log|Innehåller information om bearbetningen av importerade licensfiler.|Platssystemserver|  

### <a name="backup-and-recovery"></a><a name="BKMK_BnRLog"></a>Säkerhets kopiering och återställning

I följande tabell listas loggfiler som innehåller information som rör säkerhets kopierings-och återställnings åtgärder, inklusive webbplats återställning och ändringar av SMS-providern.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Innehåller information om installations-och återställnings uppgifter när Configuration Manager återställer en plats från en säkerhets kopia.|Platsserver|  
|Smsbkup.log|Innehåller information om aktiviteterna för att säkerhetskopiera platser.|Platsserver|  
|smssqlbkup.log|Innehåller utdata från säkerhets kopierings processen för plats databasen när SQL Server installeras på en server som inte är plats Server.|Platsdatabasserver|  
|Smswriter.log|Registrerar information om status för den Configuration Manager VSS-skrivaren som används av säkerhets kopierings processen.|Platsserver|  

### <a name="certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a>Certifikat registrering

I följande tabell visas Configuration Manager loggfiler som innehåller information som rör certifikat registrering. Certifikat registrering använder certifikat registrerings platsen och Configuration Manager-principmodulen på den server som kör registrerings tjänsten för nätverks enheter (NDES).  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|Crp.log|Registrerar registrerings aktiviteter.|Certifikatregistreringsplats|  
|Crpctrl.log|Innehåller information om driftstatusen för certifikatregistreringsplatsen.|Certifikatregistreringsplats|  
|Crpsetup.log|Innehåller information om installationen och konfigurationen av certifikatregistreringsplatsen.|Certifikatregistreringsplats|  
|Crpmsi.log|Innehåller information om installationen och konfigurationen av certifikatregistreringsplatsen.|Certifikatregistreringsplats|  
|NDESPlugin.log|Registrerar utmanings verifiering och certifikat registrerings aktiviteter.|Configuration Manager Principmodulen och registrerings tjänsten för nätverks enheter|  

Tillsammans med Configuration Manager loggfilerna granskar du Windows-programloggarna i Loggboken på servern som kör registrerings tjänsten för nätverks enheter och servern som är värd för certifikat registrerings platsen. Du kan t.ex. leta efter meddelanden från källan **NetworkDeviceEnrollmentService**.

Du kan även använda de följande loggfilerna:  

- IIS-loggfiler för registrerings tjänsten för nätverks enheter: **%systemdrive%\inetpub\logs\LogFiles\W3SVC1**  

- IIS-loggfiler för certifikat registrerings platsen: **%systemdrive%\inetpub\logs\LogFiles\W3SVC1**  

- Loggfilen för registreringsprincipen för nätverksenheter: **mscep.log**  

    > [!NOTE]  
    > Den här filen finns i mappen för NDES-konto profilen, till exempel i C:\Users\SCEPSvc. Mer information om hur du aktiverar NDES-loggning finns i avsnittet [Aktivera loggning](https://social.technet.microsoft.com/wiki/contents/articles/9063.active-directory-certificate-services-ad-cs-network-device-enrollment-service-ndes.aspx#Enable_Logging) i NDES-wikin.  

### <a name="client-notification"></a><a name="BKMK_BGB"></a>Klient meddelande

I den följande tabellen listas loggfilerna som innehåller information som rör klientmeddelanden.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Innehåller information om plats Server aktiviteter relaterade till klient aviserings aktiviteter och bearbetning av online-och uppgifts status filer.|Platsserver|  
|BGBServer.log|Registrerar meddelande serverns aktiviteter, till exempel klient-server-kommunikation och skickar uppgifter till klienter. Registrerar också information om genereringen av online-och uppgifts status-filer som ska skickas till plats servern.|Hanteringsplats|  
|BgbSetup.log|Registrerar aktiviteter för installations omslutningen av aviserings servern under installation och avinstallation.|Hanteringsplats|  
|bgbisapiMSI.log|Registrerar information om installation och avinstallation av meddelande servern.|Hanteringsplats|  
|BgbHttpProxy.log|Innehåller information om HTTP-meddelandeproxyns aktiviteter då den vidarebefordrar meddelanden från klienter som använder HTTP till och från meddelandeservern.|Klient|  
|CcmNotificationAgent.log|Registrerar meddelande agentens aktiviteter, till exempel kommunikation mellan klienter och information om uppgifter som tagits emot och skickas till andra klient agenter.|Klient|  

### <a name="cloud-management-gateway"></a>Gateway för molnhantering

I följande tabell listas loggfilerna som innehåller information som rör Cloud Management Gateway.

|Loggnamn|Beskrivning|Dator med loggfil|
|--------------|-----------------|----------------------------|  
|CloudMgr.log|Innehåller information om hur du distribuerar tjänsten Cloud Management Gateway, kontinuerlig tjänst status och använder data som är kopplade till tjänsten. Om du vill konfigurera loggnings nivån redigerar du **loggnings nivå** svärdet i följande register nyckel:`HKLM\SOFTWARE\ Microsoft\SMS\COMPONENTS\ SMS_CLOUD_ SERVICES_MANAGER`|Mappen *INSTALLDIR* på den primära plats servern eller certifikat utfärdaren.|
|CMGSetup. log <sup> [Anmärkning 1](#bkmk_note1)</sup>|Innehåller information om den andra fasen av distributionen av moln hanterings Gateway (lokal distribution i Azure). Om du vill konfigurera loggnings nivån använder du inställningen **spåra nivå** (**information** (standard), **utförligt**, **fel**) på fliken **konfiguration av Azure portal\Cloud Services** .|**%AppRoot%\Logs** på din Azure-Server eller mappen SMS/logs på plats system servern|
|CMGService. log <sup> [Anmärkning 1](#bkmk_note1)</sup>|Innehåller information om kärn komponenten för Cloud Management Gateway-tjänsten i Azure. Om du vill konfigurera loggnings nivån använder du inställningen **spåra nivå** (**information** (standard), **utförligt**, **fel**) på fliken **konfiguration av Azure portal\Cloud Services** .|**%AppRoot%\Logs** på din Azure-Server eller mappen SMS/logs på plats system servern|
|SMS_Cloud_ProxyConnector. log|Innehåller information om hur du konfigurerar anslutningar mellan Cloud Management Gateway-tjänsten och anslutnings punkten för Cloud Management Gateway.|Platssystemserver|
|CMGContentService. log <sup> [Anmärkning 1](#bkmk_note1)</sup>|<!--SCCMDocs-pr issue #2822-->När du aktiverar en CMG för att även hantera innehåll från Azure Storage, registrerar den här loggen information om tjänsten.|**%AppRoot%\Logs** på din Azure-Server eller mappen SMS/logs på plats system servern|

- Vid fel sökning av distributioner använder du **CloudMgr. log** och **CMGSetup. log**
- Använd **CMGService. log** och **SMS_Cloud_ProxyConnector. log**för fel sökning av tjänstens hälsa.
- Vid fel sökning av klient trafik använder du **CMGHttpHandler. log**, **CMGService. log**och **SMS_Cloud_ProxyConnector. log**.

#### <a name="note-1-logs-synchronized-from-azure"></a><a name="bkmk_note1"></a>Anmärkning 1: loggar synkroniserade från Azure

Dessa är lokala Configuration Manager loggfiler som Cloud Service Manager synkroniserar från Azure Storage var femte minut. Cloud Management Gateway pushar loggar till Azure Storage var femte minut. Den maximala fördröjningen är 10 minuter. Utförliga växlar påverkar både lokala och fjärranslutna loggar. De faktiska fil namnen inkluderar tjänst namnet och roll instans identifieraren. Till exempel CMG-*ServiceName* - *RoleInstanceID*-CMGSetup. log

### <a name="compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a>Kompatibilitetsinställningar och åtkomst till företags resurser

I den följande tabellen listas loggfilerna som innehåller information som rör efterlevnadsinställningar och åtkomst till företagets resurser.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Innehåller information om processen för reparation och efterlevnad för efterlevnadsinställningar, programuppdateringar och programhantering.|Klient|  
|CITaskManager.log|Innehåller information om schemaläggning av konfigurationsobjekt.|Klient|  
|DCMAgent.log|Innehåller översiktlig information om utvärderingen, konfliktrapporteringen och reparationen av konfigurationsobjekt och program.|Klient|  
|DCMReporting.log|Innehåller information om rapporteringen av principplattformsresultat till tillståndsmeddelanden för konfigurationsobjekt.|Klient|  
|DcmWmiProvider.log|Registrerar information om att läsa konfigurations objekt konfigurationsobjektssynkroniseringsprogram från WMI.|Klient|  

### <a name="configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a>Configuration Manager-konsol

I följande tabell listas loggfilerna som innehåller information som rör Configuration Manager-konsolen.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Registrerar installationen av Configuration Manager-konsolen.|Dator som kör Configuration Manager-konsolen|  
|SmsAdminUI.log|Innehåller information om driften av Configuration Manager-konsolen.|Dator som kör Configuration Manager-konsolen|  
|Smsprov.log|Registrerar SMS-providerns aktiviteter. Configuration Manager-konsol aktiviteter använder SMS-providern.|Platsserver eller platssystemsserver|  

### <a name="content-management"></a><a name="BKMK_ContentLog"></a>Innehålls hantering

I den följande tabellen listas loggfilerna som innehåller information som rör innehållshantering.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|CloudDP- &lt; GUID \> . log|Innehåller information för en specifik molnbaserad distributionsplats, däribland information om lagring och åtkomst till innehåll.|Platssystemserver|  
|CloudMgr.log|Innehåller information om innehålls etablering, insamling av lagrings-och bandbredds statistik och åtgärder som initierats av administratören för att stoppa eller starta moln tjänsten som kör en molnbaserad distributions plats.|Platssystemserver|  
|DataTransferService.log|Innehåller information om all BITS-kommunikation för princip- eller paketåtkomst. Den här loggen används även för innehålls hantering av mottagar distributions platser.|Dator som är konfigurerad som en mottagar distributions plats|  
|PullDP.log|Innehåller information om innehåll som pull-distributionsplatsen överför från källdistributionsplatser.|Dator som är konfigurerad som en mottagar distributions plats|  
|PrestageContent.log|Registrerar information om användningen av verktyget ExtractContent. exe på en fjärran sluten distributions plats. Det här verktyget packar upp innehåll som har exporterats till en fil.|Platssystemroll|  
|SMSdpmon.log|Innehåller information om schemalagda aktiviteter för distributions platsens hälso övervakning som är konfigurerade på en distributions plats.|Platssystemroll|  
|smsdpprov.log|Innehåller information om uppackningen av komprimerade filer som tagits emot från en primär plats. Den här loggen genereras av WMI-providern för den fjärranslutna distributions platsen.|Distributions plats dator som inte finns med på plats servern|  
|smsdpusage. log|Innehåller information om smsdpusage. exe som kör och samlar in data för rapporten användnings översikt för distributions platser.|Platssystemroll|  

### <a name="desktop-analytics"></a>Desktop Analytics

Använd följande loggfiler för att felsöka problem med Desktop Analytics integrerat med Configuration Manager.

Loggfilerna för tjänst anslutnings punkten finns i följande katalog: `%ProgramFiles%\Configuration Manager\Logs\M365A` .
Loggfilerna på Configuration Manager-klienten finns i följande katalog: `%WinDir%\CCM\logs` .

| Logga | Beskrivning |Dator med loggfil|
|---------|---------|---------|
| M365ADeploymentPlanWorker. log | Information om distributions plan synkronisera från Desktop Analytics Cloud service till lokala Configuration Manager |Tjänstanslutningspunkt|
| M365ADeviceHealthWorker. log | Information om enhetens hälso överföring från Configuration Manager till Microsoft Cloud |Tjänstanslutningspunkt|
| M365AHandler. log | Information om inställnings principen för Skriv bords analys |Klient|
| M365AUploadWorker. log | Information om samling och enhets uppladdning från Configuration Manager till Microsoft Cloud |Tjänstanslutningspunkt|
| SmsAdminUI.log | Information om Configuration Manager-konsol aktivitet som att konfigurera Azure Cloud Services  |Tjänstanslutningspunkt|

### <a name="discovery"></a><a name="BKMK_DiscoveryLog"></a>Identifikation

I följande tabell listas loggfilerna som innehåller information som rör identifiering.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Innehåller information om åtgärder som rör Gruppidentifiering för Active Directory-säkerhet.|Platsserver|  
|adsysdis.log|Innehåller information om åtgärder som rör Identifiering av Active Directory-system.|Platsserver|  
|adusrdis.log|Innehåller information om åtgärder som rör Identifiering av Active Directory-användare.|Platsserver|  
|ADForestDisc.Log|Innehåller information om åtgärder som rör Identifiering av Active Directory-skogar.|Platsserver|  
|ddm.log|Registrerar aktiviteter hos identifieringsdatahanteraren.|Platsserver|  
|InventoryAgent.log|Innehåller information om aktiviteter som rör maskinvaruinventering, programinventering och pulsslagsidentifieringsåtgärder på klienten.|Klient|  
|netdisc.log|Innehåller information om nätverksidentifieringsåtgärder.|Platsserver|  

### <a name="endpoint-protection"></a><a name="BKMK_EPLog"></a>Endpoint Protection

I den följande tabellen listas loggfilerna som innehåller information som rör Endpoint Protection.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Innehåller information om installationen av Endpoint Protection-klienten och tillämpningen av principer mot skadlig kod på den klienten.|Klient|  
|EPCtrlMgr.log|Innehåller information om synkronisering av information om hot från skadlig kod från Endpoint Protection roll server med Configuration Manager-databasen.|Platssystemserver|  
|EPMgr.log|Övervakar statusen för Endpoint Protections platssystemsroll.|Platssystemserver|  
|EPSetup.log|Ger information om installationen av Endpoint Protections platssystemsroll.|Platssystemserver|  

### <a name="extensions"></a><a name="BKMK_Extensions"></a>Tillägg

I följande tabell listas loggfilerna som innehåller information som rör tillägg.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Registrerar information om hämtning av tillägg från Microsoft, samt installation och avinstallation av alla tillägg.|Dator som kör Configuration Manager-konsolen|  
|FeatureExtensionInstaller.log|Registrerar information om installation och borttagning av enskilda tillägg när de är aktiverade eller inaktiverade i Configuration Manager-konsolen.|Dator som kör Configuration Manager-konsolen|  
|SmsAdminUI.log|Registrerar Configuration Manager-konsol aktivitet.|Dator som kör Configuration Manager-konsolen|  

### <a name="inventory"></a><a name="BKMK_InventoryLog"></a>Hantering

I den följande tabellen listas loggfilerna som innehåller information som rör bearbetning av inventeringsdata.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|Dataldr.log|Registrerar information om bearbetning av MIF-filer och maskin varu inventering i Configuration Manager databasen.|Platsserver|  
|invproc.log|Innehåller information om vidarebefordran av MIF-filer från en sekundär plats till dess överordnade plats.|Sekundär platsserver|  
|sinvproc.log|Innehåller information om bearbetningen av programinventeringsdata till platsdatabasen.|Platsserver|  

### <a name="metering"></a><a name="BKMK_MeteringLog"></a>Avläsning

I den följande tabellen listas loggfiler som innehåller information som rör mätning.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Övervakar alla programmätningsprocesser.|Klient|  
|SWMTRReportGen.log|Genererar en användnings data rapport som samlas in av mätar agenten. Dessa data loggas i Mtrmgr.log.|Klient|
|swmproc.log|Registrerar behandling av avläsningsfiler och inställningar.|Platsserver|

### <a name="migration"></a><a name="BKMK_MigrationLog"></a>Migreringsarkivet

I den följande tabellen listas loggfiler som innehåller information som rör migrering.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Innehåller information om migreringsåtgärder som inbegriper migreringsjobb, delade distributionsplatser och uppgraderingar av distributionsplatser.|Platsen på den översta nivån i Configuration Manager hierarkin och varje underordnad primär plats. Använd loggfilen som skapades på den centrala administrationswebbplatsen i en hierarki med flera primära platser.|  

### <a name="mobile-devices"></a><a name="BKMK_MDMLog"></a>Mobila enheter

I följande avsnitt listas loggfilerna som innehåller information som rör hantering av mobila enheter.  

#### <a name="enrollment"></a><a name="BKMK_EnrollmentLog"></a>Registrerings

I den följande tabellen finns det loggar med information som rör registrering av mobila enheter.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Innehåller kommunikationen mellan hanteringsplatser som är aktiverade för mobila enheter och hanteringsplatsens slutpunkter.|Platssystemserver|  
|dmpmsi.log|Innehåller Windows Installer-data om konfigurationen av en hanteringsplats som är aktiverad för mobila enheter.|Platssystemserver|  
|DMPSetup.log|Registrerar konfigurationen av hanterings platsen när den är aktive rad för mobila enheter.|Platssystemserver|  
|enrollsrvMSI.log|Innehåller Windows Installer-data om konfigurationen av en registreringsplats.|Platssystemserver|  
|enrollmentweb.log|Innehåller information om kommunikationen mellan mobila enheter och registreringsproxyplatsen.|Platssystemserver|  
|enrollwebMSI.log|Innehåller Windows Installer-data om konfigurationen av en registreringsproxyplats.|Platssystemserver|  
|enrollmentservice.log|Innehåller kommunikationen mellan en registreringsproxyplats och en registreringsplats.|Platssystemserver|  
|SMS_DM.log|Registrerar kommunikationen mellan mobila enheter, Mac-datorer och hanterings platsen som är aktive rad för mobila enheter och Mac-datorer.|Platssystemserver|  

#### <a name="exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a>Exchange Server-anslutning

Följande loggar innehåller information som rör Exchange Server-anslutningen.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Innehåller Exchange Server-anslutningens aktiviteter och status.|Platsserver|  

#### <a name="mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a>Äldre mobil enhet

I den följande tabellen finns det loggar med information som rör äldre klienters mobila enheter.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Innehåller information om certifikatregistreringsdata på äldre klienters mobila enheter.|Klient|  
|DMCertResp.htm|Innehåller HTML-svaret från certifikatservern när programmet för registrering av äldre mobila enheter begär ett PKI-certifikat.|Klient|  
|DmClientHealth.log|Registrerar GUID för alla äldre mobila enhets klienter som kommunicerar med hanterings platsen som är aktive rad för mobila enheter.|Platssystemserver|  
|DmClientRegistration.log|Innehåller registreringsbegäranden och svar till och från äldre mobila klienter.|Platssystemserver|  
|DmClientSetup.log|Innehåller klientkonfigurationsdata för äldre mobila klienter.|Klient|  
|DmClientXfer.log|Innehåller information om klientöverföringsdata för äldre mobila klienter och för ActiveSync-distributioner.|Klient|  
|DmCommonInstaller.log|Innehåller information om installationen av klientöverföringsfilen för konfiguration av äldre mobila enheters överföringsfiler.|Klient|  
|DmInstaller.log|Innehåller information om huruvida DMInstaller anropar DmClientSetup korrekt, och om huruvida DmClientSetup avslutas korrekt eller inte för äldre mobila klienter.|Klient|  
|DmpDatastore.log|Innehåller alla anslutningar och frågor till platsdatabasen från hanteringsplatsen som är aktiverad för mobila enheter.|Platssystemserver|  
|DmpDiscovery.log|Innehåller information om alla identifieringsdata från äldre mobila klienter på hanteringsplatsen som är aktiverad för mobila enheter.|Platssystemserver|  
|DmpHardware.log|Innehåller information om maskinvaruinventeringen från äldre mobila klienter på hanteringsplatsen som är aktiverad för mobila enheter.|Platssystemserver|  
|DmpIsapi.log|Innehåller information om klientkommunikationen mellan äldre mobila enheter och en hanteringsplats som är aktiverad för mobila enheter.|Platssystemserver|  
|dmpmsi.log|Innehåller Windows Installer-data om konfigurationen av en hanteringsplats som är aktiverad för mobila enheter.|Platssystemserver|  
|DMPSetup.log|Registrerar konfigurationen av hanterings platsen när den är aktive rad för mobila enheter.|Platssystemserver|  
|DmpSoftware.log|Innehåller information om programdistribution från äldre mobila klienter på en hanteringsplats som är aktiverad för mobila enheter.|Platssystemserver|  
|DmpStatus.log|Innehåller information om statusmeddelanden från äldre mobila klienter på en hanteringsplats som är aktiverad för mobila enheter.|Platssystemserver|  
|DmSvc.log|Innehåller klientkommunikationen mellan äldre mobila enheter och en hanteringsplats som är aktiverad för mobila enheter.|Klient|  
|FspIsapi.log|Innehåller information om kommunikationen till återställningsstatusplatsen från äldre mobila klienter och klientdatorer.|Platssystemserver|  

### <a name="os-deployment"></a><a name="BKMK_OSDLog"></a>OS-distribution

I följande tabell listas loggfilerna som innehåller information som rör operativ Systems distribution.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|CAS.log|Innehåller information om när distributionsplatser hittas för innehåll som refereras till.|Klient|  
|ccmsetup.log|Registrerar ccmsetup-aktiviteter för klientkonfiguration, klientuppgradering och borttagning av klienter. Kan användas för att felsöka problem med klientinstallation.|Klient|  
|CreateTSMedia.log|Innehåller information om skapandet av aktivitetssekvensmedier.|Dator som kör Configuration Manager-konsolen|  
|Dism.log|Registrerar installations åtgärder för driv rutiner eller uppdaterar program åtgärder för offlineunderhåll.|Platssystemserver|  
|Distmgr.log|Innehåller information om konfigurationen för att aktivera en distributions plats för PXE (Pre-Boot Execution Environment).|Platssystemserver|  
|DriverCatalog.log|Innehåller information om enhetsdrivrutiner som har importerats till drivrutinskatalogen.|Platssystemserver|  
|mcsisapi.log|Innehåller information om överföringen av multicast-paket och svar på klientförfrågningar.|Platssystemserver|  
|mcsexec.log|Registrerar hälso kontroll, namnrymd, skapande av session och certifikat kontroll åtgärder.|Platssystemserver|  
|mcsmgr.log|Registrerar ändringar i konfigurationen, säkerhets läget och tillgängligheten.|Platssystemserver|  
|mcsprv.log|Innehåller information om multicast-providerns samverkan med Windows Deployment Services (WDS).|Platssystemserver|  
|MCSSetup.log|Innehåller information om installation av multicast-serverrollen.|Platssystemserver|  
|MCSMSI.log|Innehåller information om installation av multicast-serverrollen.|Platssystemserver|  
|Mcsperf.log|Innehåller information om uppdateringar av multicast-prestandaräknaren.|Platssystemserver|  
|MP_ClientIDManager.log|Registrerar hanterings plats svar på klient-ID-begäranden som aktivitetssekvenser startar från PXE eller start medier.|Platssystemserver|  
|MP_DriverManager.log|Innehåller hanteringsplatsens svar på Använd drivrutinspaket-aktivitetssekvensens åtgärdssvar.|Platssystemserver|  
|OfflineServicingMgr.log|Registrerar information om offline-etablerings scheman och uppdaterar tillämpa åtgärder på operativ systemets WIM-filer (Windows Imaging format).|Platssystemserver|  
|Setupact.log|Registrerar information om Windows Sysprep och installationsloggar. Mer information finns i [loggfiler](https://docs.microsoft.com/windows/deployment/upgrade/log-files).|Klient|  
|Setupapi.log|Registrerar information om Windows Sysprep och installationsloggar.|Klient|  
|Setuperr.log|Registrerar information om Windows Sysprep och installationsloggar.|Klient|  
|smpisapi.log|Innehåller information om åtgärder för att spara och återställa klienttillstånd, och tröskelinformation.|Klient|  
|Smpmgr.log|Innehåller information om resultatet av tillståndsmigreringsplatsers hälsokontroller och konfigurationsändringar.|Platssystemserver|  
|smpmsi.log|Innehåller information om installations- och konfigurationsuppgifter som rör tillståndsmigreringsplatsen.|Platssystemserver|  
|smpperf.log|Innehåller uppdateringar av tillståndsmigreringspunktens prestandaräknare.|Platssystemserver|  
|smspxe.log|Innehåller information om svar på klienter som använder PXE-start och information om utökningen av start avbildningar och startfiler.|Platssystemserver|  
|smssmpsetup.log|Innehåller information om installations- och konfigurationsuppgifter som rör tillståndsmigreringsplatsen.|Platssystemserver|
| SMS_PhasedDeployment. log| Loggfil för stegvisa distributioner|Platsen på den översta nivån i Configuration Manager hierarkin|
|Smsts.log|Innehåller information om aktivitetssekvensaktiviteter.|Klient|  
|TSAgent.log|Innehåller information om resultatet av aktivitetssekvensberoenden innan en aktivitetssekvens startas.|Klient|  
|TaskSequenceProvider.log|Registrerar Detaljer om aktivitetssekvenser när de importeras, exporteras eller redige ras.|Platssystemserver|  
|loadstate.log|Innehåller information om USMT (User State Migration Tool) och återställningen av användartillståndsdata.|Klient|  
|scanstate.log|Innehåller information om USMT (User State Migration Tool) och sparandet av användartillståndsdata.|Klient|  

### <a name="power-management"></a><a name="BKMK_PowerMgmtLog"></a>Energispar funktioner

I den följande tabellen listas loggfilerna som innehåller information som rör energisparfunktioner.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|pwrmgmt.log|Innehåller information om Energis par aktiviteter på klient datorn, inklusive övervakning och verk ställandet av inställningar av klient agenten för energispar funktioner.|Klient|  

### <a name="remote-control"></a><a name="BKMK_RCLog"></a>Fjärr styrning

I den följande tabellen listas loggfilerna som innehåller information som rör fjärrstyrning.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Innehåller information om fjärrstyrningsvisarens aktiviteter.|På den dator som kör visaren för fjärr styrning, i mappen% Temp%.|  

### <a name="reporting"></a><a name="BKMK_ReportLog"></a>Uppgiftslämn

I följande tabell visas Configuration Manager loggfiler som innehåller information som rör rapportering.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Innehåller information om rapporttjänstplatsens aktivitet och status.|Platssystemserver|  
|srsrpMSI.log|Innehåller detaljerade resultat från installationen av rapporttjänstplatsen från MSI-utdata.|Platssystemserver|  
|srsrpsetup.log|Innehåller resultatet från rapporttjänstplatsens installationsprocess.|Platssystemserver|  

### <a name="role-based-administration"></a><a name="BKMK_RBALog"></a>Rollbaserad administration

I den följande tabellen listas loggfilerna som innehåller information som rör hantering av rollbaserad administration.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|hman.log|Registrerar information om ändringar i plats konfigurationen och publicering av plats information till Active Directory Domain Services.|Platsserver|  
|SMSProv.log|Innehåller information om WMI-providerns åtkomst till platsdatabasen.|Dator med SMS-provider|  

### <a name="software-metering"></a><a name="BKMK_MeteringLog"></a>Avläsning av program vara

I följande tabell listas loggfilerna som innehåller information som rör Avläsning av program vara.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Övervakar alla programmätningsprocesser.|Platsserver|  

### <a name="software-updates"></a><a name="BKMK_SU_NAPLog"></a>Program uppdateringar

Följande tabell listar de loggfiler som innehåller information relaterad till programuppdateringar.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|AlternateHandler. log|Registrerar information när klienten anropar COM-gränssnittet i Office Klicka-och-kör för att ladda ned och installera Microsoft 365 appar för företags klient uppdateringar. Det liknar användningen av WuaHandler när den anropar Windows Update Agent-API: n för att ladda ned och installera Windows-uppdateringar.<!-- SCCMDocs#888 -->|Klient|
|ccmperf.log|Innehåller information om aktiviteter som rör underhållet och insamlingen av data som rör klienters prestandaräknare.|Klient|
|DeltaDownload. log|Registrerar information om hämtning av Express uppdateringar och uppdateringar som hämtats med hjälp av leverans optimering.|Klient|  
|PatchDownloader.log|Innehåller information om processen för att hämta programuppdateringar från uppdateringskällan till nedladdningsmålet på platsservern.|När du hämtar uppdateringar manuellt finns logg filen i% Temp%-katalogen för användaren som kör-konsolen på den dator som du kör-konsolen på. För automatiska distributions regler finns logg filen på plats servern i%windir%\CCM\Logs om ConfigMgr-klienten är installerad på plats servern.|  
|PolicyEvaluator.log|Innehåller information om utvärderingen av principer på klientdatorer, däribland principer från programuppdateringar.|Klient|  
|RebootCoordinator.log|Innehåller information om koordinationen av systemomstarter på klientdatorer efter installation av programuppdateringar.|Klient|  
|ScanAgent.log|Innehåller information om avsökningsbegäranden om programuppdateringar, WSUS-platsen och relaterade åtgärder.|Klient|  
|SdmAgent.log|Registrerar information om spårning av reparation och efterlevnad. Men logg filen för program uppdateringar, Updateshandler. log, innehåller mer information om hur du installerar program uppdateringar som krävs för efterlevnad. Den här loggfilen delas med efterlevnadsinställningarna.|Klient|  
|ServiceWindowManager.log|Innehåller information om utvärderingen av underhållsperioder.|Klient|
|SMS_ISVUPDATES_SYNCAGENT. log| Loggfil för synkronisering av program uppdateringar från tredje part.| Program uppdaterings plats på den översta nivån i Configuration Manager hierarkin.|
|SMS_OrchestrationGroup. log| Loggfil för Orchestration-grupper|Platsserver|
|SmsWusHandler.log|Innehåller information om genomsökningsprocessen för inventeringsverktyget för Microsoft Updates.|Klient|  
|StateMessage.log|Innehåller information om program uppdaterings tillstånds meddelanden som skapas och skickas till hanterings platsen.|Klient|  
|SUPSetup.log|Innehåller information om installation av programuppdateringsplatsen. När installationen av programuppdateringsplatsen är klar skrivs texten **Installationen slutfördes** till denna loggfil.|Platssystemserver|  
|UpdatesDeployment.log|Innehåller information om distribution på klienten, däribland aktivering, utvärdering och verkställandet av programuppdateringar. Vid utförlig loggning visas ytterligare information om samspelet med klientens användargränssnitt.|Klient|  
|UpdatesHandler.log|Innehåller information om efterlevnadssökning av programuppdateringar och om nedladdning och installation av programuppdateringar på klienten.|Klient|  
|UpdatesStore.log|Innehåller information om efterlevnadsstatusen för programuppdateringarna som analyserades under efterlevnadssökningscykeln.|Klient|  
|WCM.log|Registrerar information om program uppdaterings platsens konfigurationer och anslutningar till WSUS-servern för prenumerationer på uppdaterings kategorier, klassificeringar och språk.|Platsserver|  
|WSUSCtrl.log|Innehåller information om konfigurationen, databasanslutningarna och hälsotillståndet hos platsens WSUS-server.|Platssystemserver|  
|wsyncmgr.log|Innehåller information om synkronisering av program uppdaterings processen.|Platsserver|  
|WUAHandler.log|Innehåller information om Windows Update-agenten på klienten när den söker efter programuppdateringar.|Klient|  

### <a name="wake-on-lan"></a><a name="BKMK_WOLLog"></a>Wake On LAN

I följande tabell listas loggfilerna som innehåller information som rör hur du använder Wake On LAN.  

> [!NOTE]  
> När du kompletterar Wake On LAN med hjälp av Wake-up-proxy loggas den här aktiviteten på klienten. Se till exempel ccmexec. log och SleepAgent_<*domän* \> @SYSTEM_0.log i avsnittet [klient åtgärder](#BKMK_ClientOpLogs) i den här artikeln.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Innehåller information om vilka klienter som behöver tillsändas aktiveringspaket, antalet aktiveringspaket som har skickats samt antalet aktiveringspaket som har skickats igen.|Platsserver|  
|wolmgr.log|Innehåller information om aktiveringsprocedurer, t.ex. när distributioner som är konfigurerade för Wake On LAN ska aktiveras.|Platsserver|  

### <a name="windows-10-servicing"></a><a name="BKMK_WindowsServicingLog"></a>Windows 10-underhåll

I följande tabell listas loggfilerna som innehåller information som rör Windows 10-underhåll.  
Underhåll använder samma infrastruktur och process som program uppdateringar. Andra loggar som gäller för underhålls scenariot finns i [program uppdateringar](#BKMK_SU_NAPLog).

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|CBS. log|Registrerar etablerings problem som rör ändringar i Windows-uppdateringar eller-roller och-funktioner.|Klient|
|DISM. log|Registrerar alla åtgärder med DISM. Om det behövs kommer DISM. log att peka på CBS. log för mer information.|Klient|
|Setupact. log|Primär logg fil för de flesta fel som inträffar under Windows-installationen. Logg filen finns i mappen% windir% \$ Windows. ~ BT\sources\panther.|Klient|

Mer information finns i [online Servicing-relaterade loggfiler](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-troubleshooting-and-log-files#online-servicing-related-log-files).

### <a name="windows-update-agent"></a><a name="BKMK_WULog"></a>Windows Update Agent

I den följande tabellen listas loggfilerna som innehåller information som rör Windows Update-agenten.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Innehåller information om när Windows Update-agenten ansluter till WSUS-servern och hämtar program uppdateringarna för kompatibilitetskontroll och om det finns uppdateringar av agent komponenterna.|Klient|  

Mer information finns i [Windows Update loggfiler](https://docs.microsoft.com/windows/deployment/update/windows-update-logs).

### <a name="wsus-server"></a><a name="BKMK_WSUSLog"></a>WSUS-Server

I den följande tabellen listas loggfilerna som innehåller information som rör WSUS-servern.  

|Loggnamn|Beskrivning|Dator med loggfil|  
|--------------|-----------------|----------------------------|  
|Change.log|Innehåller information om information om WSUS-serverdatabasen som har ändrats.|WSUS-servern|  
|SoftwareDistribution.log|Innehåller information om program uppdateringar som synkroniseras från den konfigurerade uppdaterings källan till WSUS-serverdatabasen.|WSUS-servern|  

Loggfilerna finns i `%ProgramFiles%\Update Services\LogFiles` mappen.

## <a name="see-also"></a>Se även

- [Om loggfiler](about-log-files.md)

- [Support Center OneTrace](../../support/support-center-onetrace.md)

- [Logg fils visnings program för Support Center](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
