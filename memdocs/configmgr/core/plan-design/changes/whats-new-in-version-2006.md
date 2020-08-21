---
title: Nyheter i version 2006
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 2006 av Configuration Manager aktuella grenen.
ms.date: 08/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4b071746-61e1-404b-8053-60978de028a7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bdfb122173c913274373f41c3932f1ac094ec953
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700290"
---
# <a name="whats-new-in-version-2006-of-configuration-manager-current-branch"></a>Vad är nytt i version 2006 av Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 2006 för Configuration Manager aktuella grenen är tillgänglig som en uppdatering i konsolen. Använd den här uppdateringen på webbplatser som kör version 1810 eller senare. <!-- baseline only statement:When installing a new site, it's also available as a baseline version. -->I den här artikeln sammanfattas ändringar och nya funktioner i Configuration Manager version 2006.

Läs alltid den senaste check listan för att installera den här uppdateringen. Mer information finns i [Check lista för att installera uppdatering 2006](../../servers/manage/checklist-for-installing-update-2006.md). När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).

För att dra full nytta av nya Configuration Manager funktioner kan du även uppdatera klienter till den senaste versionen när du har uppdaterat platsen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.

> [!TIP]
> Om du vill få ett meddelande när den här sidan uppdateras kopierar du och klistrar in följande URL i din RSS-feed läsare: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2006+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a> Microsoft Endpoint Manager-klient anslutning

### <a name="install-applications-from-the-admin-center"></a>Installera program från administrations centret
<!--7518897, 6024389-->
Du kan starta en programinstallation i real tid för en klient som har anslutits till en enhet från administrations centret för Microsoft Endpoint Manager. Från och med Configuration Manager version 2006 innehåller listan över program som är tillgängliga för enheten även program som distribuerats till den inloggade användarens enhet. Mer information finns i [Anslut klientorganisation: Installera ett program från administrationscentret](../../../tenant-attach/applications.md).  

### <a name="import-previously-created-azure-ad-application-during-tenant-attach-onboarding"></a>Importera tidigare skapade Azure AD-program under klient kopplings registrering
<!--6479246-->
Under en ny onboarding kan en administratör ange ett program som skapats tidigare under onboarding to klient anslutning. Mer information finns i [Microsoft Endpoint Manager-klientorganisation: Enhetssynkronisering och enhetsåtgärder](../../../tenant-attach/device-sync-actions.md#bkmk_aad_app).

## <a name="endpoint-analytics"></a><a name="bkmk_ea"></a> Slut punkts analys

### <a name="endpoint-analytics-data-collection-enabled-by-default"></a>Slut punkts analys data insamling aktiverat som standard
<!--7065447, 7741111-->
Klient inställningen **Aktivera slut punkts analys data insamling** är nu aktive rad som standard. Med den här inställningen kan dina hanterade slut punkter skicka data, till exempel start prestanda insikter, till din Configuration Manager plats Server. Den här ändringen påverkar endast lokal data insamling. Slut punkts analys data överförs inte till administrations centret för Microsoft Endpoint Manager förrän du [aktiverar data uppladdning i Configuration Manager](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload). Det nya standardvärdet gäller för standard klient inställningarna och eventuella anpassade klient inställningar som skapats efter uppgraderingen till version 2006.

- Om du uppgraderar från version 2002 till version 2006 behålls befintliga anpassade klient inställnings värden. Standardvärdet för **Aktivera slut punkts analys data insamling** i Configuration Manager version 2002 är **Nej**.
- Om du uppgraderar till version 2006 från Configuration Manager version 1910 eller tidigare ärver alla befintliga anpassade klient inställningar som innehåller **dator agent** gruppen med inställningar den nya standarden **Yes** för **Aktivera slut punkts analys data insamling**.

Mer information finns i [Konfigurera data insamling för slut punkts analys i Configuration Manager](../../../../analytics/enroll-configmgr.md#bkmk_cm_upload).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Plats infrastruktur

### <a name="vpn-boundary-type"></a>VPN-avgränsnings typ

<!--7020519-->

För att förenkla hanteringen av fjärrklienter kan du nu skapa en ny avgränsnings typ för VPN-nätverk. Tidigare var du tvungen att skapa gränser för VPN-klienter baserat på IP-adressen eller under nätet. Den här konfigurationen kan vara utmanande eller inte möjlig på grund av under näts konfigurationen eller VPN-designen.

Nu när en klient skickar en plats förfrågan innehåller den ytterligare information om nätverks konfigurationen. Utifrån den här informationen avgör servern om klienten finns på en VPN-anslutning.

Mer information finns i [definiera gränser](../../servers/deploy/configure/boundaries.md).

### <a name="management-insights-to-optimize-for-remote-workers"></a>Hanterings insikter för att optimera för fjärranslutna arbetare

<!--6982226-->

Den här versionen lägger till en ny grupp med hanterings insikter, **som är optimerad för fjärran vändare**. Med dessa insikter kan du skapa bättre upplevelser för fjärran vändare och minska belastningen på din infrastruktur. Insikterna i den här versionen fokuserar främst på VPN:

- **Definiera VPN-gränser**
- **Konfigurera VPN-anslutna klienter för att föredra molnbaserade innehålls källor**
- **Inaktivera delning av peer-till-peer-innehåll för VPN-anslutna klienter**

Mer information finns i [hanterings insikter](../../servers/manage/management-insights.md).

### <a name="improved-support-for-windows-virtual-desktop"></a>Förbättrat stöd för virtuella Windows-datorer

<!--6527576-->

Plattformen **Windows 10 Enterprise multi-session** finns i listan över OS-versioner som stöds på objekt med krav regler eller tillämplighets listor.

Mer information om Configuration Manager Support för virtuella Windows-datorer finns i [OS-versioner som stöds för klienter och enheter](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop).

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a>Intranät klienter kan använda en CMG program uppdaterings plats
<!--7102873-->
Intranät klienter kan nu komma åt en CMG program uppdaterings plats när den tilldelas en avgränsnings grupp. Mer information finns i [Konfigurera gränser grupper](../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup).

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Molnbaserad hantering

### <a name="use-the-company-portal-app-on-co-managed-devices"></a>Använd Företagsportal-appen på samhanterade enheter

<!--CMADO-3601237,INADO-4297660-->

Företagsportal är nu den plattforms oberoende applikations portalen för Microsoft Endpoint Manager. Genom att konfigurera samhanterade enheter så att de också använder Företagsportal kan du ge en konsekvent användar upplevelse på alla enheter.

Mer information finns i [Använd Företagsportalappen på samhanterade enheter](../../../comanage/company-portal.md).

### <a name="use-microsoft-azure-china-21vianet-for-co-management"></a>Använd Microsoft Azure Kina för samhantering
<!--7133238-->
Nu kan du välja Azure Kina-molnet som Azure-miljö när du aktiverar samhantering. Mer information finns i [så här aktiverar du samhantering](../../../comanage/how-to-enable.md).

### <a name="notification-for-azure-ad-app-secret-key-expiration"></a>Meddelande om förfallo datum för Azure AD-appens hemliga nyckel

<!--6386392-->

Om du konfigurerar Azure-tjänster till molnet och ansluter till platsen visar Configuration Manager-konsolen nu meddelanden under följande omständigheter:

- En eller flera Azure AD-appens hemliga nycklar upphör snart att gälla
- En eller flera Azure AD-appens hemliga nycklar har upphört att gälla

Mer information finns i [förnya hemlig nyckel](../../servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### <a name="desktop-analytics"></a>Desktop Analytics

Mer information om de månatliga ändringarna i moln tjänsten för Station ära datorer finns i [Nyheter i Skriv bords analys](../../../desktop-analytics/whats-new.md).

#### <a name="change-to-diagnostic-data-labels"></a>Ändra till data etiketter för diagnostikdata

<!-- 7363467 -->

För att bättre justera med kraven för Skriv bords analys för Windows-diagnostikdata har de här inställningarna nya etiketter:

| Version 2006 och senare | Version 2002 och tidigare |
|---------|---------|
| Obligatorisk | Basic |
| Valfritt (begränsat) | Utökad (begränsad) |
| Ej tillämpligt | Optimerad |
| Valfritt | Fullständig |

Om du tidigare har konfigurerat några enheter på den **förbättrade** nivån, kommer de att återgå till **valfria (begränsat)** när du uppgraderar till version 2006. De skickar då mindre data till Microsoft. Den här ändringen påverkar inte vad du ser i Skriv bords analys.

Mer information finns i [Aktivera data delning för Skriv bords analys](../../../desktop-analytics/enable-data-sharing.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a> Real tids hantering

### <a name="improvements-to-cmpivot"></a>Förbättringar av CMPivot
<!--6518631-->
Följande förbättringar har gjorts i CMPivot:

- CMPivot från-konsolen och fristående CMPivot har konvergerats
- Köra CMPivot från en enskild enhet eller flera enheter utan att behöva välja eller skapa en samling
- Från CMPivot frågeresultat kan du välja en enskild enhet eller flera enheter och sedan starta en separat CMPivot-instans som omfattas av ditt val.

Mer information finns i [CMPivot från och med version 2006](../../servers/manage/cmpivot-changes.md#bkmk_2006).

## <a name="client-management"></a><a name="bkmk_client"></a> Klient hantering

### <a name="install-and-upgrade-the-client-on-a-metered-connection"></a>Installera och uppgradera klienten på en avgiftsbelagd anslutning

<!--6976145-->

Om enheten tidigare var ansluten till ett nätverk med datapriser installerades inte nya klienter. Befintliga klienter uppgraderas bara om du har tillåtit all klient kommunikation. För enheter som ofta är centralt i ett nätverk med datapriser kan de vara ohanterade eller på en äldre klient version. Från och med den här versionen kan du installera och uppgradera klienten när du anger klient inställningen **klient kommunikation på avgiftsbelagda Internet anslutningar** för att **tillåta** eller **begränsa**. Med den här inställningen kan du tillåta att klienten hålls aktuell, men fortfarande hanterar klient kommunikationen i ett nätverk med datapriser.

För att definiera beteendet för en ny klient installation finns det en ny CCMSetup-parameter **/AllowMetered**. När du tillåter klient kommunikation i ett nätverk med datapriser för CCMSetup, laddar den ned innehållet, registrerar på platsen och laddar ned den ursprungliga principen. All ytterligare klient kommunikation följer konfigurationen av klient inställningen från den principen.

Mer information finns i följande artiklar:

- [Om klientinställningar](../../clients/deploy/about-client-settings.md#client-communication-on-metered-internet-connections)
- [Om parametrar och egenskaper för klient installation](../../clients/deploy/about-client-installation-properties.md#allowmetered)

### <a name="improvements-to-managing-device-restarts"></a>Förbättringar av hantering av omstarter av enheter

<!--3601213-->

Configuration Manager innehåller många alternativ för att hantera omstarter av enheter och starta om aviseringar. Nu kan du konfigurera en klient inställning för att förhindra att enheter startar om automatiskt när en distribution kräver det. Den här inställningen ger dig mer kontroll i unika situationer. Som standard kan klient inställningen **Configuration Manager tvinga en enhet att starta om** vara aktive rad, så Configuration Manager kan fortfarande tvinga enheter att starta om. Den här inställningen gäller endast för program, program uppdateringar och paket distributioner som kräver en omstart.

Mer information finns i [meddelanden om omstart av enhet](../../clients/deploy/device-restart-notifications.md).

## <a name="application-management"></a><a name="bkmk_app"></a> Program hantering

### <a name="improvements-to-available-apps-via-cmg"></a>Förbättringar av tillgängliga appar via CMG

<!--6935376-->
I den här versionen åtgärdas ett problem med Software Center och Azure Active Directory (Azure AD)-autentisering. För en klient som identifierats som i intranätet, men som kommunicerar via Cloud Management Gateway (CMG), skulle tidigare Software Center använda Windows-autentisering. Det gick inte att hämta listan över tillgängliga appar för användare. Den använder nu Azure Active Directory (Azure AD)-identitet för enheter som är anslutna till Azure AD. Dessa enheter kan vara molnbaserad eller hybrid-anslutna.

Mer information finns i [distribuera användar tillgängliga appar](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications).

### <a name="microsoft-365-apps-for-enterprise"></a>Microsoft 365-appar för företag
<!--6298093-->
Office 365 ProPlus har bytt namn till Microsoft 365 appar för företag den 21 april 2020. Från och med version 2006 har följande ändringar gjorts:

- Configuration Managers konsolen har uppdaterats med det nya namnet.
  - Den här ändringen inkluderar även uppdatering av kanal namn för Microsoft 365 appar.
- Ett banner-meddelande har lagts till i-konsolen för att meddela dig om en eller flera regler för automatisk distribution refererar till inaktuella kanal namn i **rubrik** villkoren för uppdateringar av Microsoft 365 appar.

Mer information finns i [Microsoft 365 Apps kanal namn](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_channel) och [instrument panel för instrument paneler för Microsoft 365 Apps](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).

## <a name="os-deployment"></a><a name="bkmk_osd"></a> OS-distribution

### <a name="task-sequence-media-support-for-cloud-based-content"></a>Medie stöd för aktivitetssekvens för molnbaserad innehåll

<!--6209223-->

Media för aktivitetssekvenser kan nu ladda ned molnbaserad innehåll. Du kan till exempel skicka en USB-nyckel till en användare på ett fjärran slutet kontor för att återställa en avbildning av enheten. Eller ett kontor som har en lokal PXE-server, men du vill att enheter ska prioritera moln tjänster så mycket som möjligt. I stället för att ytterligare beskattnings WAN för att ladda ned innehåll för stor operativ Systems distribution kan du nu hämta innehåll från molnbaserade källor med start medier och PXE-distributioner. Till exempel en CMG (Cloud Management Gateway) som du aktiverar för att dela innehåll.

> [!NOTE]
> Enheten behöver fortfarande en intranät anslutning till hanterings platsen.

Mer information finns i [använda startbara medier för att distribuera Windows via nätverket](../../../osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

### <a name="improvements-to-task-sequences-via-cmg"></a>Förbättringar av aktivitetssekvenser via CMG

Den här versionen innehåller följande förbättringar för att distribuera aktivitetssekvenser till enheter som kommunicerar via en Cloud Management Gateway (CMG):

- Stöd för distribution av operativ system<!--6997525-->: Med en aktivitetssekvens som använder en start avbildning för att distribuera ett operativ system kan du distribuera det till en enhet som kommunicerar via CMG. Användaren måste starta aktivitetssekvensen från Software Center. Mer information finns i [Planera för CMG-specifikationer](../../clients/manage/cmg/plan-cloud-management-gateway.md#specifications).

- Den här versionen åtgärdar de två [kända problemen](../../servers/deploy/install/release-notes.md#task-sequences-cant-run-over-cmg) från Configuration Manager aktuella gren versionen 2002.<!-- 6983320 --> Nu kan du köra en aktivitetssekvens på en enhet som kommunicerar via CMG under följande omständigheter:

  - En arbets grupps enhet som du registrerar med en [token för Mass registrering](../../clients/deploy/deploy-clients-cmg-token.md)

  - Du konfigurerar platsen för [utökad http](../hierarchy/enhanced-http.md) och hanterings platsen är http

### <a name="improvements-to-bitlocker-task-sequence-steps"></a>Förbättringar av stegen i BitLocker-aktivitetssekvensen

<!--6995601-->

Nu kan du ange disk krypterings läget i stegen **Aktivera BitLocker** och **Företablera BitLocker** . Som standard fortsätter stegen att använda standard krypterings metoden för operativ system versionen.

Steget **Aktivera BitLocker** innehåller nu även en inställning för att **hoppa över det här steget för datorer som inte har TPM eller när TPM inte är aktiverat**. När du aktiverar den här inställningen loggar steget ett fel på en enhet utan TPM eller TPM som inte initieras och aktivitetssekvensen fortsätter. Den här inställningen gör det lättare att hantera aktivitetssekvenser på enheter som inte har fullständigt stöd för BitLocker.

Mer information finns i avsnittet om [aktivitetssekvenser](../../../osd/understand/task-sequence-steps.md).

### <a name="management-insight-rules-for-os-deployment"></a>Regler för insikter för operativ system distribution

<!--6982275-->

När storleken på aktivitetssekvensen överskrider 32 MB, kan klienten inte bearbeta den stora principen. Klienten kan sedan inte köra distribution av aktivitetssekvensen. I den här versionen ingår följande hanterings information för att hjälpa dig att hantera princip storleken för aktivitetssekvenser:

- **Stora aktivitetssekvenser kan bidra till att överskrida den maximala princip storleken**

- **Den totala princip storleken för aktivitetssekvenser överskrider princip gränsen**

> [!TIP]
> Dessa regler finns i en ny grupp för **distribution av operativ system**. Den befintliga regeln för **oanvända start avbildningar** finns nu i den här gruppen.

Mer information finns i avsnittet om [hanterings insikter](../../servers/manage/management-insights.md#operating-system-deployment).

### <a name="improvements-to-os-deployment"></a>Förbättringar av OS-distribution

I den här versionen ingår följande ytterligare förbättringar av OS-distributionen:

- Använd en aktivitetssekvens för att ange målet för steget [format och partition disk](../../../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk) . Detta nya variabel alternativ stöder mer komplexa aktivitetssekvenser med dynamiska beteenden. Ett anpassat skript kan till exempel identifiera disken och ange variabeln baserat på maskin varu typen. Sedan kan du använda flera instanser av det här steget för att konfigurera olika typer av maskin vara och partitioner.<!--6610288-->

- Steget [kontrol lera beredskap](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness) innehåller nu en kontroll för att avgöra om enheten använder UEFI. Den innehåller också en ny variabel för skrivskyddad aktivitetssekvens **_TS_CRUEFI**.<!--6452769-->

- Om du aktiverar [fönstret förlopp för aktivitetssekvens](../../../osd/understand/user-experience.md#task-sequence-progress) för att visa mer detaljerad information om förloppet räknas nu inte aktiverade steg i en inaktive rad grupp. Den här ändringen gör att förloppet blir mer exakt.<!--6448412-->

- Tidigare var det ett kommando tolks fönster som öppnades i en av de sista stegen i Windows-konfigurationen under en aktivitetssekvens för att uppgradera en enhet till Windows 10. Fönstret var ovanpå OOBE (out-of-Box Experience) och användare kan interagera med det för att avbryta uppgraderings processen. Nu kan du använda SetupCompleteTemplate. cmd-och SetupRollbackTemplate. cmd-skripten från Configuration Manager inkludera en ändring för att dölja kommando tolkens fönster.<!--2837795-->

- Vissa kunder skapar anpassade aktivitetssekvenser med hjälp av metoden **IProgressUI:: ShowMessage** , men returnerar inte något värde för användarens svar. Den här versionen lägger till metoden [IProgressUI:: ShowMessageEx](../../../develop/reference/core/clients/client-classes/iprogressui--showmessageex-method.md) . Den här nya metoden liknar den befintliga metoden, men innehåller även en ny heltals resultat variabel, **pResult**.<!--6448458-->

## <a name="protection"></a>Skydd

### <a name="cmg-support-for-endpoint-protection-policies"></a>CMG-stöd för Endpoint Protection-principer

<!--4773948-->

Även om CMG (Cloud Management Gateway) har stöd för Endpoint Protection-principer, måste enheterna ha åtkomst till lokala domänkontrollanter. Från och med den här versionen kan klienter som kommunicerar via en CMG omedelbart tillämpa Endpoint Protection-principer utan en aktiv anslutning till Active Directory.

Mer information finns i [CMG-stöd för Configuration Manager-funktioner](../../clients/manage/cmg/plan-cloud-management-gateway.md#support-for-configuration-manager-features).

### <a name="bitlocker-management-support-for-hierarchies"></a>Stöd för BitLocker-hantering för hierarkier

<!-- 5925693 -->

Nu kan du installera självbetjänings portalen för BitLocker och webbplatsen för administration och övervakning på den centrala administrations platsen.

Mer information finns i [Konfigurera BitLocker-portaler](../../../protect/deploy-use/bitlocker/setup-websites.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-konsol

### <a name="community-hub-and-github"></a>Community Hub och GitHub
<!--3555935, 3555936, deep link included 4224406-->

*(Först infördes i juni 2020)*

IT-administratörs gruppen har utvecklat en enorm mängd kunskap under åren. I stället för att göra om objekt som skript och rapporter från grunden har vi skapat en Configuration Manager **Community-hubb** där du kan dela med varandra. Genom att använda arbetet med andra kan du spara arbets timmar. Community Hub utvecklar kreativitet genom att bygga vidare på andras arbete och låta andra personer bygga på din. GitHub har redan branschspecifika processer och verktyg som skapats för delning. Nu kommer community-navet att utnyttja dessa verktyg direkt i Configuration Manager-konsolen som grundläggande delar för att driva den nya gruppen. För den första versionen kommer det innehåll som görs tillgängligt i Community Hub endast att överföras av Microsoft. 

Mer information finns i [Community Hub och GitHub](../../servers/manage/community-hub.md).

### <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a> Direkta länkar till community Hub-objekt
<!--4224406-->
Du kan enkelt navigera till och referens objekt i noden Configuration Manager-konsolen community Hub med en direkt länk. Mer information finns i [direkt länkar till community Hub-objekt](../../servers/manage/community-hub.md#bkmk_deeplink).

### <a name="notifications-from-microsoft"></a>Meddelanden från Microsoft
<!--3953121-->
Du kan nu välja att ta emot meddelanden från Microsoft i Configuration Manager-konsolen. De här aviseringarna hjälper dig att hålla dig informerad om nya eller uppdaterade funktioner, ändringar av Configuration Manager och anslutna tjänster och problem som kräver åtgärder för att åtgärda problemet.

Mer information finns i [Konfigurera en plats för att ta emot meddelanden från Microsoft](../../servers/manage/admin-console-notifications.md#bkmk_msft).

### <a name="power-bi-sample-reports"></a>Power BI exempel rapporter
<!--5679791-->

*(Först infördes i juni 2020)*

När du integrerar Power BI-rapportserver med Configuration Manager repor ting finns nu exempel på Power BI rapporter tillgängliga. Hämta och installera följande exempel rapporter:

- Status för program Uppdateringsefterlevnad
- Distributions status för program uppdatering

Mer information finns i [installera Power BI exempel rapporter](../../servers/manage/powerbi-sample-reports.md).

<!-- Unused sections in this release:
## Reporting
## <a name="bkmk_userxp"></a> User experience
## <a name="bkmk_sum"></a> Software updates
## Office management
## <a name="bkmk_content"></a> Content management
## <a name="bkmk_comgmt"></a> Co-management
-->

## <a name="deprecated-operating-systems"></a><a name="bkmk_deprecated"></a> Föråldrade operativ system

Läs om support ändringar innan de implementeras i [borttagna och föråldrade objekt](deprecated/removed-and-deprecated.md).

Som först presenterade i version 1906 har version 2006 stöd för följande klient operativ system versioner:  

- Windows CE 7,0
- Windows 10 Mobil
- Windows 10 Mobile Enterprise

## <a name="other-updates"></a>Övriga uppdateringar

<!--
Starting with this version, the following features are no longer [pre-release](../../servers/manage/pre-release-features.md):

### Azure Active Directory user group discovery](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956
-->

Mer information om ändringar i Windows PowerShell-cmdlets för Configuration Manager finns i [versions anteckningar för PowerShell version 2006](/powershell/sccm/2006-release-notes?view=sccm-ps).

Mer information om ändringar i administrations tjänsten REST API finns i viktig information om [administrations tjänsten](../../../develop/adminservice/release-notes.md#bkmk_2006).

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 2006](https://support.microsoft.com/help/4556203).

<!--
The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Nästa steg

För tillfället släpps version 2006 för tidig uppdatering av ringen. Om du vill installera den här uppdateringen måste du välja. Mer information finns i [tidig uppdaterings ring](../../servers/manage/checklist-for-installing-update-2006.md#early-update-ring).

<!-- As of May 11, 2020, version 2006 is globally available for all customers to install. -->

När du är redo att installera den här versionen, se [Installera uppdateringar för Configuration Manager](../../servers/manage/updates.md) och [Check lista för att installera uppdatering 2006](../../servers/manage/checklist-for-installing-update-2006.md).

> [!TIP]
> Om du vill installera en ny plats använder du en bas linje version av Configuration Manager.
>
> Läs mer om:
>
> - [Nya platser installeras](../../servers/deploy/install/installing-sites.md)
> - [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines)

Information om kända viktiga problem finns i [versions anteckningarna](../../servers/deploy/install/release-notes.md).

När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-2006.md#post-update-checklist).