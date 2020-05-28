---
title: Nyheter i version 1910
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 1910 av Configuration Manager aktuella grenen.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a52b70b0a753036c506e5d515cbac048d6771295
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879060"
---
# <a name="whats-new-in-version-1910-of-configuration-manager-current-branch"></a>Vad är nytt i version 1910 av Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 1910 för Configuration Manager aktuella grenen är tillgänglig som en uppdatering i konsolen. Använd den här uppdateringen på webbplatser som kör version 1806 eller senare. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> I den här artikeln sammanfattas ändringar och nya funktioner i Configuration Manager version 1910.

Läs alltid den senaste check listan för att installera den här uppdateringen. Mer information finns i [Check lista för att installera uppdatering 1910](../../servers/manage/checklist-for-installing-update-1910.md). När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).

För att dra full nytta av nya Configuration Manager funktioner kan du även uppdatera klienter till den senaste versionen när du har uppdaterat platsen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.

> [!TIP]
> Om du vill få ett meddelande när den här sidan uppdateras kopierar du och klistrar in följande URL i din RSS-feed läsare:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-configuration-manager"></a><a name="bkmk_mem"></a>Microsoft Endpoint Configuration Manager

<!--4960084-->

Configuration Manager är nu en del av Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager är en integrerad lösning för att hantera alla dina enheter. Microsoft sammanför Configuration Manager och Intune med förenklad licensiering. Fortsätt att använda dina befintliga Configuration Manager investeringar samtidigt som du utnyttjar kraften i Microsoft Cloud i din egen takt.

Följande Microsoft-hanterings lösningar är nu en del av Microsoft Endpoint Manager-varumärket:

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](../../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Andra funktioner i [administrations konsolen för enhets hantering](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)

Mer information finns i följande inlägg från Bengt Anderson, Microsoft corporate vice president för Microsoft 365:

- [Blogg inlägg i meddelande](https://aka.ms/cmannounce)
- [Syn papper](https://aka.ms/MEMVisionPaper)
- [Videoklipp om meddelande Sammanfattning](https://youtu.be/GS7oNPInFuw)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Vad har ändrats i Configuration Manager med Microsoft Endpoint Manager?

I version 1910, bortsett från namn ändringen, Configuration Manager fungerar fortfarande på samma sätt. Några av namn ändringarna kan påverka din användning av följande komponenter:

- **Configuration Manager-konsol**: hitta genvägar till-konsolen och **visnings programmet för fjärr styrning** på Start-menyn i **Microsoft Endpoint Manager** -mappen.

- **Software Center**: Leta upp genvägen för Software Center under Start-menyn i **Microsoft Endpoint Manager** -mappen.

![Ikoner för Start-menyn i Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

Se till att uppdatera all intern dokumentation som du upprätthåller för att inkludera dessa nya platser.

> [!TIP]
> När du öppnar Start-menyn i Windows 10 skriver du namnet för att hitta ikonen. Ange till exempel `Configuration Manager` eller `Software Center`.

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Plats infrastruktur

### <a name="reclaim-sedo-lock"></a>Frigör SEDO-lås

<!--4786915-->

Från och med den [aktuella gren versionen 1906](whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences)kan du rensa låset på en aktivitetssekvens. Nu kan du rensa låset för alla objekt i Configuration Manager-konsolen.

Mer information finns i [använda Configuration Manager-konsolen](../../servers/manage/admin-console.md#bkmk_sedo).

### <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Utöka och migrera lokal plats till Microsoft Azure
<!--3556022-->

Det här nya verktyget hjälper dig att program mässigt skapa virtuella Azure-datorer (VM) för Configuration Manager. Den kan installeras med standardinställningar webbplats roller som en passiv plats Server, hanterings platser och distributions platser. När du har validerat de nya rollerna kan du använda dem som ytterligare plats system för hög tillgänglighet. Du kan också ta bort den lokala plats system rollen och bara behålla rollen för den virtuella Azure-datorn.

Mer information finns i [utöka och migrera en lokal plats till Microsoft Azure](../../support/azure-migration-tool.md).

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="desktop-analytics"></a><a name="bkmk_da"></a>Skriv bords analys

Mer information om de månatliga ändringarna i moln tjänsten för Station ära datorer finns i [Nyheter i Skriv bords analys](../../../desktop-analytics/whats-new.md).

## <a name="real-time-management"></a><a name="bkmk_real"></a>Real tids hantering

### <a name="optimizations-to-the-cmpivot-engine"></a>Optimeringar till CMPivot-motorn
<!--3197353-->
Vi har lagt till några betydande optimeringar i CMPivot-motorn. Nu kan du push-överföra mer av bearbetningen till ConfigMgr-klienten. Optimeringarna minskar drastiskt nätverks-och Server CPU-belastningen som krävs för att köra CMPivot-frågor. Med dessa optimeringar kan du nu gå igenom flera gigabyte av klient data i real tid. 

Mer information finns i [optimeringar till CMPivot-motorn](../../servers/manage/cmpivot.md#bkmk_optimization).

### <a name="additional-cmpivot-entities-and-enhancements"></a>Ytterligare CMPivot-enheter och-förbättringar
<!--5410930-->
Vi har lagt till ett antal nya CMPivot-enheter och förbättringar av enheten för att hjälpa till med fel sökning och jakt. Vi har inkluderat följande entiteter för att fråga:

- Windows-händelseloggar ([WinEvent](../../servers/manage/cmpivot.md#bkmk_WinEvent))
- Fil innehåll ([FileContent](../../servers/manage/cmpivot.md#bkmk_File))
- DLL-filer som lästs in av processer ([ProcessModule](../../servers/manage/cmpivot.md#bkmk_ProcessModule))
- Azure Active Directory information ([AADStatus](../../servers/manage/cmpivot.md#bkmk_AadStatus))
- Endpoint Protection-status ([EPStatus](../../servers/manage/cmpivot.md#bkmk_EPStatus))

Den här versionen innehåller även flera [andra förbättringar](../../servers/manage/cmpivot.md#bkmk_Other) av CMPivot. Mer information finns i [CMPivot från och med version 1910](../../servers/manage/cmpivot.md#bkmk_cmpivot1910).

## <a name="content-management"></a><a name="bkmk_content"></a>Innehålls hantering

### <a name="microsoft-connected-cache-support-for-intune-win32-apps"></a>Stöd för Microsoft Connected cache för Intune Win32-appar

<!--5032900-->

När du aktiverar Microsoft Connected cache på Configuration Manager distributions platser kan de nu hantera Microsoft Intune Win32-appar till samhanterade klienter.

Mer information finns [i Microsoft Connected cache i Configuration Manager](../hierarchy/microsoft-connected-cache.md#bkmk_intune).

> [!NOTE]
> Configuration Manager nuvarande gren version 1906 har inkluderat [leverans optimering i nätverket cache](../hierarchy/microsoft-connected-cache.md), ett program som är installerat på Windows Server och fortfarande är under utveckling. Den här funktionen heter nu Microsoft Connected cache från den aktuella gren versionen 1910.
>
> När du installerar den anslutna cachen på en Configuration Manager distributions plats avlastar den leverans optimerings tjänstens trafik till lokala källor. Ansluten cache gör detta genom att effektivt cachelagra innehåll på byte-intervall-nivån.

## <a name="client-management"></a><a name="bkmk_client"></a>Klient hantering

### <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Inkludera anpassade konfigurations bas linjer som en del av utvärderingen av efterlevnadsprinciper
<!--3608345-->

Du kan nu lägga till utvärdering av anpassade konfigurations bas linjer som en bedömnings regel för efterlevnadsprinciper. När du skapar eller redigerar en konfigurations bas linje kan du nu använda alternativet **utvärdera denna bas linje som en del av utvärderings principen för efterlevnadsprinciper** . När du lägger till eller redigerar en regel för efterlevnadsprinciper har du ett villkor som kallas **Inkludera konfigurerade bas linjer i utvärderingen av efterlevnadsprinciper**.

För samhanterade enheter, och när du konfigurerar Intune att ta Configuration Manager utvärderings resultat som en del av den övergripande kompatibilitetsstatus, skickas informationen till Azure Active Directory. Du kan sedan använda den för villkorlig åtkomst till dina Office 365-resurser.

Mer information finns i [Inkludera anpassade konfigurations bas linjer som en del av utvärderingen av efterlevnadsprinciper](../../../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

### <a name="enable-user-policy-for-windows-10-enterprise-multi-session"></a>Aktivera användar princip för Windows 10 Enterprise multi-session

<!--4737447-->

Configuration Manager aktuella gren version 1906 introducerade stöd för [virtuella Windows-datorer](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop). Den här Microsoft Azure miljön stöder flera OS-versioner, varav vissa tillåter flera samtidiga aktiva användarsessioner. Till exempel är Windows 10 Enterprise multi-session en av dessa OS-versioner.

Om du behöver användar princip på dessa enheter för flera sessioner och accepterar eventuella prestanda effekter kan du nu konfigurera en klient inställning för att aktivera användar principer. Konfigurera inställningen **Aktivera användar princip för flera** användarsessioner i gruppen **klient princip** .

Mer information finns i [så här konfigurerar du klient inställningar](../../clients/deploy/configure-client-settings.md).


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="application-management"></a><a name="bkmk_app"></a>Program hantering

### <a name="deploy-microsoft-edge-version-77-and-later"></a>Distribuera Microsoft Edge, version 77 eller senare
<!--4561024-->
Det nya Microsoft Edge är klart för företag. Nu kan du distribuera Microsoft Edge, version 77 och senare till dina användare. Administratörer kan välja beta-, dev-eller stabil kanal, tillsammans med en version av Microsoft Edge-klienten som ska distribueras.

Mer information finns i [distribuera Microsoft Edge, version 77 och senare](../../../apps/deploy-use/deploy-edge.md).

### <a name="improvements-to-application-groups"></a>Förbättringar av program grupper

<!--4760058-->

Från och med den aktuella gren versionen 1906 kan du skapa en grupp med program som ska skickas till en enhets samling som en enda distribution. Den här versionen har förbättrats på följande funktion:

- Användare kan välja **Avinstallera** för app-gruppen i Software Center.
- Du kan distribuera en app-grupp till en **användar samling**.

Mer allmän information finns i [skapa program grupper](../../../apps/deploy-use/create-app-groups.md).


## <a name="os-deployment"></a><a name="bkmk_osd"></a>OS-distribution

### <a name="improvements-to-the-task-sequence-editor"></a>Förbättringar av redigeraren för aktivitetssekvens

 Redigeraren för aktivitetssekvens innehåller följande förbättringar:

- **Sök i redigeraren för aktivitetssekvens:**<!--4621085--> Om du har en stor aktivitetssekvens med många grupper och steg, kan det vara svårt att hitta vissa steg. Nu kan du söka i redigeraren för aktivitetssekvens. Med den här åtgärden kan du snabbare hitta steg i aktivitetssekvensen.
- **Kopiera och klistra in villkor för aktivitetssekvens:**<!--4621098--> Om du vill återanvända villkoren från ett steg i en aktivitetssekvens till ett annat, kan du nu kopiera och klistra in villkor i redigeraren för aktivitetssekvens.

Mer information finns i den nya artikeln om hur du [använder redigeraren för aktivitetssekvens](../../../osd/understand/task-sequence-editor.md).

### <a name="task-sequence-performance-improvements-power-plans"></a>Prestanda förbättringar i aktivitetssekvenser: energi scheman

<!--3555926-->

Nu kan du köra en aktivitetssekvens med ett energi schema med höga prestanda. Det här alternativet förbättrar den övergripande hastigheten i aktivitetssekvensen. Det konfigurerar Windows så att det använder sitt inbyggda energi schema för höga prestanda, vilket ger högsta möjliga prestanda vid kostnad av högre strömförbrukning.

Mer information finns i [prestanda förbättringar för energi scheman](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_perf).

### <a name="task-sequence-download-on-demand-over-the-internet"></a>Aktivitetssekvens laddas ned på begäran via Internet

<!--3601238-->

Du kan använda aktivitetssekvensen för att distribuera en Windows 10-uppgradering på plats via Cloud Management Gateway (CMG). Den kräver dock att distributionen laddar ned allt innehåll lokalt innan aktivitetssekvensen startas.

Från och med den här versionen kan aktivitetssekvensen Ladda ned paket på begäran från en innehålls aktive rad CMG eller en moln distributions plats. Den här ändringen ger ytterligare flexibilitet för distributioner av Windows 10 på plats till Internet-baserade enheter.

Mer information finns i [distribuera uppgradering av Windows 10 på plats via CMG](../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).

### <a name="improvements-to-os-deployment"></a>Förbättringar av OS-distribution

Den här versionen innehåller följande förbättringar av operativ Systems distributionen.

#### <a name="boot-image-keyboard-layout"></a>Tangentbordslayout för start avbildning

<!--4910348-->

Konfigurera standard tangentbordslayouten för en start avbildning. På fliken **anpassning** i en start avbildning använder du alternativet ny **uppsättning standard tangent bords layout i WinPE** . Om du väljer ett annat språk än en-US, kan Configuration Manager fortfarande innehålla en-us i tillgängliga språk. På enheten är den första tangentbordslayouten det valda språket, men användaren kan byta enhet till en-US om det behövs.

Mer information finns i [Hantera start avbildningar](../../../osd/get-started/manage-boot-images.md#customization).

#### <a name="import-a-single-index-of-an-os-upgrade-package"></a>Importera ett enda index för ett uppgraderings paket för operativ system

<!--4931110-->

När du importerar ett operativ system uppgraderings paket kan du använda alternativet **extrahera ett avbildnings index från install. wim-filen för det valda uppgraderings paketet** . Detta fungerar på samma sätt som med [OS-avbildningar](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages), förutom att den skriver över den befintliga install. wim-filen i uppgraderings paketet för operativ systemet. Avbildnings indexet extraheras till en tillfällig plats och flyttas sedan till den ursprungliga käll katalogen.

Mer information finns i [hantera OS-uppgraderings paket](../../../osd/get-started/manage-operating-system-upgrade-packages.md#BKMK_AddOSUpgradePkgs).

#### <a name="output-the-results-of-a-run-command-line-step-to-a-variable-during-a-task-sequence"></a>Resultera i resultatet av ett kommando rads steg för körning till en variabel under en aktivitetssekvens

<!--user story 4977616/bug 4798352-->

Steget **Kör kommando rad** innehåller nu en **utdata till variabel alternativet för aktivitetssekvens** . När du aktiverar det här alternativet sparar aktivitetssekvensen utdata från kommandot till en anpassad variabel för aktivitetssekvensen som du anger.

Mer information finns i [Kör kommando raden](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine).

#### <a name="improvements-to-task-sequence-debugger"></a>Förbättringar av fel sökning av aktivitetssekvens

Den här versionen innehåller följande förbättringar av fel söknings programmet för aktivitetssekvenser:

- Använd den nya variabeln **TSDebugOnError** för att automatiskt starta fel sökningen när aktivitetssekvensen returnerar ett fel.<!-- 5012536 -->
- Om du skapar en Bryt punkt i fel sökaren och startar om datorn kommer fel söknings programmet att behålla Bryt punkterna efter omstart.<!-- 5012509 -->

Mer information finns i avsnittet om [fel sökning av aktivitetssekvenser](../../../osd/deploy-use/debug-task-sequence.md) och [variabler för aktivitetssekvens-TSDebugOnError](../../../osd/understand/task-sequence-variables.md#TSDebugOnError).

#### <a name="improved-language-support-in-task-sequence"></a>Förbättrat språk stöd i aktivitetssekvens

<!--5411057, 5138936-->

Den här versionen lägger till kontroll över språk konfiguration under distribution av operativ system. Om du redan använder dessa språk inställningar kan den här ändringen hjälpa dig att förenkla aktivitetssekvensen för OS-distribution. I stället för att använda flera steg per språk eller separata skript använder du en instans per språk i steget Använd de inbyggda **Windows-inställningarna** med ett villkor för språket.

Använd steget **Använd aktivitets ordningen Använd Windows-inställningar** för att konfigurera följande nya inställningar:

- Inmatnings språk (standard tangentbordslayout)
- System språk
- GRÄNSSNITTs språk
- GRÄNSSNITTs språks reserv
- Användar språk

Mer information finns i avsnittet [Apply Windows Settings](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).

#### <a name="new-variable-for-windows-10-in-place-upgrade"></a>Ny variabel för Windows 10 på plats-uppgradering

<!--4680263-->

Om du vill åtgärda tids problem med Windows 10 på plats-uppgradering för högpresterande enheter när Windows-installationen är klar, kan du nu ange en ny variabel för aktivitetssekvens, **SetupCompletePause**. När du tilldelar ett värde i sekunder till den här variabeln, förskjuter Windows-installationsprogrammet den tiden innan aktivitetssekvensen startas. Denna timeout ger Configuration Manager klienten ytterligare tid att initiera.

Mer information finns i [variabler för aktivitetssekvens-SetupCompletePause](../../../osd/understand/task-sequence-variables.md#SetupCompletePause).

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a>Program uppdateringar

### <a name="additional-options-for-third-party-update-catalogs"></a>Ytterligare alternativ för uppdaterings kataloger från tredje part
<!--4469002-->
Nu har du fler detaljerade kontroller över synkroniseringen av uppdaterings kataloger från tredje part. Från och med Configuration Manager version 1910 kan du konfigurera synkroniseringsschemat för varje katalog oberoende av varandra. När du använder kataloger som innehåller kategoriserade uppdateringar kan du konfigurera synkroniseringen så att den endast innehåller vissa uppdaterings kategorier för att undvika synkronisering av hela katalogen. När du är säker på att du ska distribuera en kategori med kategoriserade kataloger kan du konfigurera den så att den hämtas och publiceras automatiskt till Windows Server Update Services (WSUS).

Mer information finns i [Aktivera uppdateringar från tredje part](../../../sum/deploy-use/third-party-software-updates.md#bkmk_1910).

### <a name="use-delivery-optimization-for-all-windows-updates"></a>Använd leverans optimering för alla Windows-uppdateringar
<!--4699118-->
Tidigare kunde du endast använda leverans optimering för Express-uppdateringar. Med Configuration Manager version 1910 är det nu möjligt att använda leverans optimering för att distribuera allt Windows Update innehåll för klienter som kör Windows 10 version 1709 eller senare.

Mer information finns i:
- [Optimera leverans för Windows 10-uppdatering](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#bkmk_DO-1910)
- [Klient inställningar för program uppdateringar](../../clients/deploy/about-client-settings.md#software-updates)
- [Klient inställningar för leverans optimering](../../clients/deploy/about-client-settings.md#delivery-optimization)

### <a name="additional-software-update-filter-for-adrs"></a>Ytterligare filter för program uppdatering för automatisk distribution
<!--4852033-->
Nu kan du använda **distribuerat** som ett uppdaterings filter för reglerna för automatisk distribution (automatisk distribution). Med det här filtret kan du identifiera nya uppdateringar som kan behöva distribueras till pilot-eller test samlingar.

Mer information finns i [distribuera program uppdateringar automatiskt](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process).

## <a name="office-management"></a><a name="bkmk_o365"></a>Office-hantering


### <a name="office-365-proplus-pilot-and-health-dashboard"></a>Instrument panel för Office 365 ProPlus pilot och hälso tillstånd
<!--4488272, 4488301-->

Instrument panelen för Office 365 ProPlus pilot och hälso tillstånd hjälper dig att planera, pilot och distribuera Office 365 ProPlus. Instrument panelen tillhandahåller hälso insikter för enheter med Office 365 ProPlus för att identifiera eventuella problem som kan påverka dina distributions planer. Instrument panelen för Office 365 ProPlus pilot och hälso tillstånd innehåller en rekommendation för pilotbaserade enheter som baseras på inventering av tillägg.

Mer information finns i [instrument panelen för Office 365 ProPlus pilot och hälso tillstånd](../../../sum/deploy-use/office-365-dashboard.md#bkmk_pilot).

## <a name="protection"></a><a name="bkmk_protect"></a>Skyddas

### <a name="bitlocker-management"></a>BitLocker-hantering

<!--3601034-->

Configuration Manager har nu följande hanterings funktioner för BitLocker-diskkryptering:

- Distribuera BitLocker-klienten till hanterade Windows-enheter.
- Hantera enhets krypterings principer.
- Generera rapporter om efterlevnad.
- Använd en webbplats för administration och övervakning för nyckel återställning.
- Få åtkomst till en självbetjänings Portal för användare.

Mer information finns i [Planera för BitLocker-hantering](../../../protect/plan-design/bitlocker-management.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Configuration Manager-konsol

### <a name="view-active-consoles-and-message-administrators-through-console-connections"></a>Visa aktiva konsoler och meddelande administratörer via konsol anslutningar
<!--4923997-->
Vi har gjort följande förbättringar för **konsol anslutningar**:

- Möjligheten att få meddelanden om andra Configuration Manager-administratörer via Microsoft Teams.
- Den **sista kolumnen med konsol pulsslag** har ersatt den **senaste anslutna Time** -kolumnen.
  - En öppen konsol i förgrunden skickar ett pulsslag var tionde minut för att avgöra vilka konsol anslutningar som för närvarande är aktiva.

Mer information finns i [Visa nyligen anslutna konsoler](../../servers/manage/admin-console.md#bkmk_viewconnected) och [meddelande administratörer](../../servers/manage/admin-console.md#bkmk_message).

### <a name="client-diagnostics-actions"></a>Åtgärder för klientautentisering

<!--4433455-->

Det finns nya enhets åtgärder för **client Diagnostics** i Configuration Manager-konsolen:

- **Aktivera utförlig loggning:** Ändra den globala logg nivån för CCM-komponenten till *verbose*och aktivera fel söknings loggning.
- **Inaktivera utförlig loggning:** Ändra den globala logg nivån till *standard*och inaktivera fel söknings loggning.

Mer information finns i [client Diagnostics](../../clients/manage/client-notification.md#client-diagnostics).

### <a name="improvements-to-console-search"></a>Förbättringar av konsols ökning
<!--4640570-->

Den här versionen innehåller följande förbättringar för sökning i Configuration Manager-konsolen:

- Du kan nu använda sökalternativet **alla undermappar** från noden **driv rutins paket** och **frågor** .<!--2841181,5424892-->
- När en sökning returnerar fler än 1 000 resultat väljer du **OK** i meddelande fältet för att visa fler resultat.<!--4640570-->

## <a name="other-updates"></a>Övriga uppdateringar

Mer information om ändringar i Windows PowerShell-cmdlets för Configuration Manager finns i [versions anteckningar för PowerShell version 1910](https://docs.microsoft.com/powershell/sccm/1910-release-notes?view=sccm-ps).

Mer information om ändringar i administrations tjänsten REST API finns i viktig information om [administrations tjänsten](../../../develop/adminservice/release-notes.md#bkmk_1910).

Förutom nya funktioner innehåller den här versionen även ytterligare ändringar som fel korrigeringar. Mer information finns i [Sammanfattning av ändringar i Configuration Manager aktuella grenen, version 1910](https://support.microsoft.com/help/4535776).

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Device Guard management](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)
-->
Följande samlade uppdateringar (4537079) är tillgängliga i-konsolen från och med den 18 februari 2020: samlad [uppdatering för Microsoft Endpoint Configuration Manager aktuell gren, version 1910](https://support.microsoft.com/help/4537079).



<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4552181](https://support.microsoft.com/help/4552181) | Content distribution stalls in Configuration Manager current branch, version 1910 | 16 March 2020 | No |
| [4552430](https://support.microsoft.com/help/4552430) | Third-party update category synchronization resets to default in Configuration Manager | 18 March 2020 | No |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Nästa steg

<!-- At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1910.md#early-update-ring). -->
Från och med den 20 december 2019 är version 1910 globalt tillgängligt för alla kunder att installera.

När du är redo att installera den här versionen, se [Installera uppdateringar för Configuration Manager](../../servers/manage/updates.md) och [Check lista för att installera uppdatering 1910](../../servers/manage/checklist-for-installing-update-1910.md).

> [!TIP]
> Om du vill installera en ny plats använder du en bas linje version av Configuration Manager.
>
> Läs mer om:
>
> - [Nya platser installeras](../../servers/deploy/install/installing-sites.md) 
> - [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines) 

Information om kända viktiga problem finns i [versions anteckningarna](../../servers/deploy/install/release-notes.md).

När du har uppdaterat en plats granskar du även [Check listan efter uppdatering](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).
