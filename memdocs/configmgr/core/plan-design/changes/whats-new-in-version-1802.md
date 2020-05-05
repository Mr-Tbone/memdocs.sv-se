---
title: Ny version 1802
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 1802 av Configuration Manager.
ms.date: 10/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 11066470347db0f3ffbfadda9897aed92baa645b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073610"
---
# <a name="whats-new-in-version-1802-of-configuration-manager"></a>Vad är nytt i version 1802 av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 1802 för Configuration Manager aktuella grenen är tillgänglig som en uppdatering i konsolen. Använd den här uppdateringen på webbplatser som kör version 1702, 1706 eller 1710. <!-- baseline only statement: -->När du installerar en ny plats är den också tillgänglig som en bas linje version.

Förutom nya funktioner innehåller den här versionen även ytterligare ändringar som fel korrigeringar. Mer information finns i [Sammanfattning av ändringar i Configuration Manager aktuella grenen, version 1802](https://support.microsoft.com/help/4101375).

Följande ytterligare uppdateringar av den här versionen är nu tillgängliga:
- [Samlad uppdatering för Configuration Manager aktuell gren, version 1802](https://support.microsoft.com/help/4163547)

> [!TIP]  
> Om du vill installera en ny plats måste du använda en bas linje version av Configuration Manager.  
>
> Läs mer om:    
> - [Nya platser installeras](../../servers/deploy/install/installing-sites.md)  
> - [Installera uppdateringar på platser](../../servers/manage/updates.md)  
> - [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines)

Följande avsnitt innehåller information om ändringar och nya funktioner i version 1802 av Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Plats infrastruktur

### <a name="reassign-distribution-point"></a>Omtilldela distributions plats
<!-- 1306937 -->
Många kunder har stora Configuration Manager infrastrukturer och minskar de primära eller sekundära platserna för att förenkla sin miljö. De måste fortfarande behålla distributions platser på avdelnings kontor för att kunna hantera innehåll till hanterade klienter. Dessa distributions platser innehåller ofta flera terabyte eller mer av innehållet. Det här innehållet är kostsamt i fråga om tid och nätverks bandbredd för att distribuera till dessa fjärrservrar. Med den här funktionen kan du omtilldela en distributions plats till en annan primär plats utan att distribuera om innehållet. Den här åtgärden uppdaterar plats system tilldelningen och behåller allt innehåll på servern. Mer information finns i [omtilldela en distributions plats](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_reassign).

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Konfigurera Windows leverans optimering att använda Configuration Manager gränser grupper
<!-- 1324696 -->
Du använder Configuration Manager gränser grupper för att definiera och reglera innehålls distribution i företags nätverket och på fjärranslutna kontor. [Windows-leverans optimering](/windows/deployment/update/waas-delivery-optimization) är en molnbaserad, peer-to-peer-teknik för att dela innehåll mellan Windows 10-enheter. Från och med den här versionen konfigurerar du leverans optimeringen så att du kan använda dina gränser när du delar innehåll mellan peer-datorer. En ny klient inställning tillämpar gränserna för den begränsade gruppen som ID för leverans optimerings grupp på klienten. När klienten kommunicerar med moln tjänsten för leverans optimering används den här identifieraren för att hitta peer-datorer med det önskade innehållet. Mer information finns i [grundläggande begrepp för innehålls hantering](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).

### <a name="support-for-windows-10-arm64-devices"></a>Stöd för Windows 10 ARM64-enheter
<!-- 1353704 -->
Från och med den här versionen stöds Configuration Manager-klienten på Windows 10 ARM64-enheter. Befintliga klient hanterings funktioner bör fungera med de här nya enheterna. Till exempel maskin-och program varu inventering, program uppdateringar och program hantering. Distribution av operativ system stöds inte för närvarande. 

### <a name="improved-support-for-cng-certificates"></a>Förbättrat stöd för CNG-certifikat
<!-- 1357314 -->
Configuration Manager (aktuell gren) version 1710 stöder [kryptografi: CNG-certifikat (Next Generation)](../network/cng-certificates-overview.md). Version 1710 begränsar stödet till klient certifikat i flera scenarier. 

Från och med den här versionen använder du CNG-certifikat för följande HTTPS-aktiverade Server roller:
- Hanteringsplats
- Distributionsplats
- Programuppdateringsplats
- Plats för tillståndsmigrering  


### <a name="boundary-group-fallback-for-management-points"></a>Återställning av gränser grupper för hanterings platser
<!-- 1324594 -->
Konfigurera återställnings relationer för hanterings platser mellan [gränser grupper](../../servers/deploy/configure/boundary-groups.md). Det här beteendet ger större kontroll för de hanterings platser som klienterna använder. Mer information finns i [Konfigurera gränser grupper](../../servers/deploy/configure/boundary-groups.md#management-points).


### <a name="cloud-distribution-point-site-affinity"></a>Plats tillhörighet för moln distributions plats
<!--503719-->
Den här funktionen fördelar kunder med en geografiskt utspridd hierarki med hjälp av moln distributions platser. När en Internetbaserad klient söker efter innehåll tidigare fanns det ingen ordning på listan över moln distributions platser som klienten har tagit emot. Det här beteendet kan leda till att Internetbaserade klienter tar emot innehåll från geografiskt avlägsna moln distributions platser. Att ladda ned innehåll från en sådan avlägsen server är normalt långsammare än en närmare Server.
 
Med plats tillhörighet för moln distributions platser får en Internetbaserad klient en ordnad lista. Den här listan prioriterar moln distributions platser från klientens tilldelade plats. På så sätt kan administratören bevara sina design syften för hämtning av innehåll från plats resurser.
 

## <a name="management-insights"></a>Hanteringsinsikter
<!-- 1353967 -->
Hanterings insikter i Configuration Manager ger information om miljöns aktuella tillstånd. Informationen baseras på analys av data från plats databasen. Insights hjälper dig att bättre förstå din miljö och vidta åtgärder baserat på insikter. Mer information finns i [hanterings insikter](../../servers/manage/management-insights.md)

I Configuration Manager 1802 är följande insikter tillgängliga:
- Program:
    - Program utan distributioner
- Cloud Services: <!--1356412-->
    - Utvärdera beredskap för samhantering 
    - Gör det möjligt för dina enheter att vara hybrid Azure Active Directory-anslutna
    - Modernisera din identitets-och åtkomst infrastruktur
    -  Uppgradera dina klienter till Windows 10, version 1709 eller senare 
- Samlingar
    - Tomma samlingar
- Förenklad hantering:  <!--1355148-->
    - Inaktuella klient versioner  
- Software Center: 
    - Dirigera användare till Software Center i stället för att Programkatalog  
    - Använd den nya versionen av Software Center 
- Windows 10: <!--1357421-->
    - Konfigurera Windows-telemetri och kommersiell ID-nyckel 
    - Anslut Configuration Manager till Uppgraderingsberedskap 
   
<!-- ## Migration  -->



## <a name="client-management"></a>Klienthantering

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Stöd för Cloud Management Gateway för Azure Resource Manager
<!-- 1324735 -->
När du skapar en instans av CMG ( [Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md) ) ger guiden nu möjlighet att skapa en **Azure Resource Manager distribution**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) är en modern plattform för att hantera alla lösnings resurser som en enda entitet, som kallas för en [resurs grupp](/azure/azure-resource-manager/resource-group-overview#resource-groups). När du distribuerar CMG med Azure Resource Manager använder platsen Azure Active Directory (Azure AD) för att autentisera och skapa nödvändiga moln resurser. Den här moderna distributionen kräver inte det klassiska hanterings certifikatet för Azure. Mer information finns i [CMG Topology design](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).

> [!IMPORTANT]
> Den här funktionen aktiverar inte stöd för Azure Cloud Service-leverantörer (CSP). CMG-distributionen med Azure Resource Manager fortsätter att använda den klassiska moln tjänsten som inte stöds av KRYPTOGRAFIPROVIDERn. Mer information finns i [tillgängliga Azure-tjänster i Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="improvements-to-cloud-management-gateway"></a>Förbättringar av Cloud Management Gateway  

- Från och med den här versionen är **Cloud Management Gateway** inte längre en för hands versions funktion.  

- Funktions dokumentationen har ändrats och förbättrats. Mer information finns i följande artiklar:
    - [Planera för Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md)
    - [Storlek och skalnings nummer för Cloud Management Gateway](../configs/size-and-scale-numbers.md#bkmk_cmg)
    - [Säkerhet och sekretess för molnhanteringsgateway](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md)
    - [Vanliga frågor och svar om Cloud Management Gateway](../../clients/manage/cmg/cloud-management-gateway-faq.md)
    - [Certifikat för molnhanteringsgateway](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)
    - [Konfigurera en molnhanteringsgateway](../../clients/manage/cmg/setup-cloud-management-gateway.md)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>Konfigurera maskin varu inventering för att samla in strängar som är större än 255 tecken
<!-- 1357389 -->
Du kan konfigurera längden på strängar som är större än 255 tecken för maskin varu inventerings egenskaper. Den här ändringen gäller endast nyligen tillagda klasser och för maskin varu inventerings egenskaper som inte är nycklar. Mer information finns i artikeln [utöka maskin varu inventering](../../clients/manage/inventory/extend-hardware-inventory.md#bkmk_GreaterThan255) . 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Utfasnings meddelande för stöd för Linux-och UNIX-klienter
 <!--510139-->
Microsoft har för avsikt att ta bort stöd för Linux-och UNIX-klienter i Configuration Manager ungefär ett år, så att klienterna inte tas med i version 1902 i tidiga kalender 2019. Configuration Manager 1810-versionen, i sent kalender 2018, är den sista versionen som omfattar Linux-och UNIX-klienter, och de kommer att stödjas under hela livs cykeln för Configuration Manager 1810. Efter Configuration Manager 1810 bör kunderna överväga Microsoft Azure hantering för att hantera Linux-servrar. Azure-lösningar har omfattande Linux-support som i de flesta fall överskrider Configuration Manager-funktioner, inklusive slut punkt till slut punkt för korrigerings hantering för Linux.

### <a name="surface-device-dashboard"></a>Instrumentpanel för Surface-enhet
<!--1355788-->
På instrument panelen för Surface-enheter finns information om de Surface-enheter som finns i din miljö. I-konsolen går du till **övervakning** > av**Surface-enheter**. Du kan visa objekten:
- Procent av ytor
- Procent av Surface-modeller
- De fem främsta versionerna av inbyggd program vara

Mer information finns i artikeln [Surface Dashboard](../../clients/manage/surface-device-dashboard.md) .

### <a name="change-in-the-configuration-manager-client-install"></a>Ändra i Configuration Manager-klient installationen
<!--1356195-->
Från och med den här versionen installeras Silverlight inte längre på klient enheter automatiskt. Mer information finns i [krav för distribution av klienter till Windows-datorer](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_ExternalDependencies)

## <a name="co-management"></a>Samhantering

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Över gång Endpoint Protection arbets belastning till Intune med hjälp av samhantering
<!-- 1357365 -->
 Endpoint Protection arbets belastningen kan överföras till Intune efter att du aktiverat samhantering. Om du vill överföra Endpoint Protection arbets belastningen går du till sidan Egenskaper för samhantering och flyttar skjutreglaget från Configuration Manager till **pilot** eller **alla**. Mer information om arbets belastningarna finns i [arbets belastningar för samhantering](../../../comanage/workloads.md). Mer information om samhantering finns i [Co-Management för Windows 10-enheter](../../../comanage/overview.md).
 
### <a name="co-management-dashboard-in-configuration-manager"></a>Instrument panel för samhantering i Configuration Manager
<!--1356648-->
Från och med den här versionen kan du Visa en instrument panel med information om samhantering. Instrument panelen hjälper dig att granska datorer som är samhanterade i din miljö. Diagrammen kan hjälpa till att identifiera enheter som kan behöva åtgärdas. Mer information finns i artikeln om [Co-Management-instrumentpanelen](../../../comanage/how-to-monitor.md#co-management-dashboard) . 


## <a name="compliance-settings"></a>Kompatibilitetsinställningar

### <a name="microsoft-edge-browser-policies"></a>Principer för Microsoft Edge-webbläsare
<!-- 1357310 -->
För kunder som använder [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) -webbläsaren på Windows 10-klienter skapar du en princip för Configuration Manager kompatibilitetsinställningar för att konfigurera flera Microsoft Edge-inställningar. Mer information finns i [skapa Microsoft Edge-webbläsarens profil](../../../compliance/deploy-use/browser-profiles.md). 



## <a name="application-management"></a>Programhantering

### <a name="allow-user-interaction-when-installing-an-application"></a>Tillåt användar interaktion när du installerar ett program
<!-- 1356976 -->
Tillåt en slutanvändare att interagera med en programinstallation under körningen av aktivitetssekvensen. Du kan till exempel köra en installations process som efterfrågar slutanvändaren för olika alternativ. Vissa program installations program kan inte göra användaren tyst, eller så kan installations processen behöva specifika konfigurations värden som bara är känd för användaren. Med den här funktionen kan du hantera dessa installations scenarier. Mer information finns i [Ange alternativ för användar upplevelse för distributions typen](../../../apps/deploy-use/create-applications.md#bkmk_dt-ux).

### <a name="do-not-automatically-upgrade-superseded-applications"></a>Uppgradera inte ersatta program automatiskt
<!-- 1351266 -->
Konfigurera en program distribution för att inte automatiskt uppgradera ersatta versioner. Nu när du skapar distributionen, på sidan **distributions inställningar** i **guiden distribuera program vara**, kan du aktivera eller inaktivera **alternativet för att** **automatiskt uppgradera alla ersatta versioner av programmet**. Mer information finns i [Ange distributions inställningar](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).

### <a name="approve-application-requests-for-users-per-device"></a>Godkänn program begär Anden för användare per enhet
<!-- 1357015 -->
Från och med den här versionen, när en användare begär ett program som kräver godkännande, är det specifika enhets namnet nu en del av begäran. Om administratören godkänner begäran kan användaren bara installera programmet på den enheten. Användaren måste skicka en annan begäran om att installera programmet på en annan enhet. Mer information finns i [Ange distributions inställningar](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings).

 > [!Note]  
 > Detta är en valfri funktion. Mer information finns i avsnittet [Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options).  


### <a name="run-scripts-improvements"></a>Köra skript förbättringar 
<!-- 1236459 -->
 Från och med den här versionen kan du **köra skript** som inte längre är en för hands versions funktion. Skriptets utdata returnerar nu med JSON-formatering. Mer information finns i [skapa och köra PowerShell-skript från Configuration Manager-konsolen](../../../apps/deploy-use/create-deploy-scripts.md).


## <a name="operating-system-deployment"></a>Distribution av operativsystem

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Windows 10 på plats-uppgradering av aktivitetssekvensen via Cloud Management Gateway
<!-- 1357149 -->
Aktivitetssekvensen Windows 10 [på plats-uppgradering](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) stöder nu distribution till Internetbaserade klienter som hanteras via [Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md). Den här möjligheten gör att fjärran vändare enklare kan uppgradera till Windows 10 utan att behöva ansluta till företags nätverket. Mer information finns i [Distribuera en aktivitetssekvens](../../../osd/deploy-use/deploy-a-task-sequence.md).

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Förbättringar av aktivitetssekvens för Windows 10-uppgradering på plats
<!-- 1357425 -->
Standard mal len för aktivitetssekvenser för Windows 10 uppgradering på plats innehåller nu ytterligare grupper med rekommenderade åtgärder som ska läggas till före och efter uppgraderings processen. Dessa åtgärder är gemensamma för många kunder som har lyckats uppgradera enheter till Windows 10. Mer information finns i [skapa en aktivitetssekvens för att uppgradera ett operativ system](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-to-prepare-for-upgrade).

### <a name="improvements-to-operating-system-deployment"></a>Förbättringar av operativ Systems distribution
Den här versionen innehåller följande förbättringar av operativ Systems distributionen:
- När du startar CMTrace. exe i Windows PE uppmanas du inte längre att välja om programmet ska vara standard visnings programmet för loggfiler. <!-- SMS 500897 -->
- Lägg till Start avbildningar i steget [Ladda ned paket innehåll](../../../osd/understand/task-sequence-steps.md#BKMK_DownloadPackageContent) i aktivitetssekvensen.
- Förbättringar av steget [Kör aktivitetssekvens](../../../osd/understand/task-sequence-steps.md#child-task-sequence) : <!-- 1261338 -->   
  - Stöd för alla distributions scenarier för operativ system från Software Center, PXE och media.
  - Förbättringar av konsol åtgärder som kopiering, import, export och varning vid borttagning av objekt.
  - Stöd för guiden [Skapa förinstallerad innehålls fil](../hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent) .
  - Integrering med distributions verifiering. Mer information finns i [distributioner med hög risk för aktivitetssekvenser](../../../osd/deploy-use/deploy-a-task-sequence.md). 
  - Steget Kör aktivitetssekvens kan nu användas på flera nivåer av aktivitetssekvenser, inte bara en enda överordnad-underordnad relation. Relationer på flera nivåer ökar komplexiteten, så Använd med försiktighet. Relationerna är fortfarande markerade för cirkulära referenser.

### <a name="deployment-templates-for-task-sequences"></a>Distributionsmall för aktivitetssekvenser
<!-- 1357391 -->
I [distributions guiden för aktivitetssekvenser](../../../osd/deploy-use/deploy-a-task-sequence.md) kan du nu skapa en distributionsmall. Distributions mal len kan sparas och tillämpas på en befintlig eller ny aktivitetssekvens för att skapa en distribution. 

### <a name="phased-deployments-for-task-sequences"></a>Stegvisa distributioner för aktivitetssekvenser
<!--1356837-->
 Stegvisa distributioner är en [för hands versions funktion](../../servers/manage/pre-release-features.md). Stegvisa distributioner automatiserar en samordnad, sekvenserad distribution av en aktivitetssekvens över flera samlingar. Du kan [skapa stegvisa distributioner](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) med standardvärdet två faser eller manuellt konfigurera flera faser. Stegvis distribution av aktivitetssekvenser stöder inte PXE-eller medie installation.




## <a name="software-center"></a>Software Center

### <a name="install-multiple-applications-in-software-center"></a>Installera flera program i Software Center
<!-- 1357126 -->
Om en slutanvändare eller Skriv bords tekniker behöver installera flera program på en enhet, har Software Center nu stöd för att installera flera valda program. Detta gör att användaren är mer effektiv och väntar på att en installation ska slutföras innan nästa steg påbörjas. Mer information finns i [installera flera program](../../understand/software-center.md#install-multiple-applications) i användar handboken för Software Center.

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Använd Software Center för att söka efter och installera användar tillgängliga program på Azure AD-anslutna enheter
<!-- 1322613 -->
Om du distribuerar program som tillgängliga för användare kan de nu bläddra och installera dem via Software Center på Azure Active Directory (Azure AD)-enheter. Mer information finns i [distribuera användar tillgängliga program på Azure AD-anslutna enheter](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).

### <a name="hide-installed-applications-in-software-center"></a>Dölj installerade program i Software Center
<!--1357592-->
Installerade program kan nu döljas i Software Center. Program som redan är installerade visas inte längre på fliken program när det här alternativet är aktiverat under klient inställningar. Det här alternativet anges som standard när du installerar eller uppgraderar till Configuration Manager 1802.  Installerade program är fortfarande tillgängliga för granskning på fliken installations status. [Dölj installerade program i Software Center](../../clients/deploy/about-client-settings.md#bkmk_HideInstalled) har ytterligare information.   

### <a name="hide-unapproved-applications-in-software-center"></a>Dölj ej godkända program i Software Center
 <!--1355146-->
När det här alternativet för klient inställningar är aktiverat är användar tillgängliga program som kräver godkännande dolda i Software Center.  [Dölj ej godkända program i Software Center](../../clients/deploy/about-client-settings.md#bkmk_HideUnapproved) . Ytterligare information.  

### <a name="software-center-shows-user-additional-compliance-information"></a>Software Center visar ytterligare kompatibilitetsinformation för användare
<!-- 1235616 -->
 När du använder Hälsoattestering för enhet status som regel för efterlevnadsprinciper för villkorlig åtkomst till företags resurser, visar Software Center nu användaren inställningen Hälsoattestering för enhet som inte är kompatibel.


 ## <a name="software-updates"></a>Programuppdateringar 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>Schemalägg utvärdering av automatisk distributions regel så att den motbokas från en bas dag. 
<!--1357133-->
Automatiska distributions regler kan schemaläggas för att utvärdera förskjutningen från en bas dag. Om korrigerings tisdag faktiskt är onsdag för dig kan du ställa in ett utvärderings schema för den andra tisdagen i månaden med en dag. Mer information finns i [distribuera program uppdateringar automatiskt](../../../sum/deploy-use/automatically-deploy-software-updates.md#BKMK_CreateAutomaticDeploymentRule). 



## <a name="reporting"></a>Rapportering

### <a name="report-for-default-browser-counts"></a>Rapport för antal standard webbläsare
<!-- 1357830 -->
Nu finns det en ny rapport för att visa antalet klienter med en speciell webbläsare som Windows standard. Se rapporten **standard antal webbläsare** i rapport gruppen **program vara – företag och produkter** . Mer information finns i [listan över rapporter](../../servers/manage/list-of-reports.md#software---companies-and-products).

### <a name="report-on-windows-autopilot-device-information"></a>Rapport om Windows autopilot-enhets information
<!-- 1351442 -->
Windows autopilot är en lösning för att onboarding och konfigurera nya Windows 10-enheter på ett modernt sätt. Mer information finns i [Översikt över Windows autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). En metod för att registrera befintliga enheter med Windows autopilot är att överföra enhets information till Microsoft Store för företag och utbildning. Den här informationen omfattar enhetens serie nummer, Windows produkt identifierare och en maskin varu identifierare. Använd Configuration Manager för att samla in och rapportera denna enhets information med den nya rapporten, **enhets information för Windows autopilot**, i noden **maskin vara – allmänt** rapporter. Mer information finns i [så här förbereder du Internet-baserade enheter för samhantering](../../../comanage/how-to-prepare-Win10.md#windows-autopilot) i förbereda för samhantering.

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>Rapportera om service uppgifter för Windows 10 för en speciell samling
<!--1357653-->
**Service informationen för Windows 10 för en bestämd samlings** rapport visar allmän information om Windows 10-underhåll för en speciell samling. Den här rapporten innehåller resurs-ID, NetBIOS-namn, OS-namn, namn på operativ system version, build, OS-gren och service nivå för Windows 10-enheter. Mer information finns i [listan över rapporter](../../servers/manage/list-of-reports.md#operating-system)



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>Skydda enheter

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Förbättringar av Configuration Manager principer för Windows Defender sårbarhet Guard
<!-- 1356220 -->
Ytterligare princip inställningar för komponenten för [minskning av attack ytan](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_ASR) och [reglerad mappåtkomst](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_CFA) har lagts till i Configuration Manager för [Windows Defender sårbarhet Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-attack-surface-reduction).

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Nya interaktions inställningar för värd för Windows Defender Application Guard
<!-- 1356256 -->
För enheter med Windows 10 version 1709 och senare finns det två nya interaktions inställningar för värd för [Windows Defender Application Guard](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_HIS): 
- Webbplatser kan få åtkomst till värdens virtuella grafik processor. 
- Filer som hämtats inuti behållaren kan sparas på värden. 




## <a name="configuration-manager-console"></a>Configuration Manager-konsolen

### <a name="improvements-to-the-configuration-manager-console"></a>Förbättringar av Configuration Manager-konsolen 
I den här versionen ingår följande förbättringar i Configuration Manager-konsolen.
- Enhets listor under till gångar och efterlevnad, enheter, visar nu den primära användaren som standard. Den här kolumnen visas endast i noden enheter. Den senast inloggade användaren kan också läggas till som en valfri kolumn.<!-- 1357280 --> Aktivera klient inställningarna för [användar-och enhets tillhörighet](../../clients/deploy/about-client-settings.md#user-and-device-affinity) för platsen för att koppla en primär användare till en enhet.
- Om en samling är medlem i en annan samling och den får ett nytt namn uppdateras det nya namnet under medlemskaps regler.<!--1357282--> 
- När du använder fjärr styrning på en klient med flera bildskärmar med olika DPI-skalning, mappar mus markören nu korrekt mellan dem. <!--433170-->
- [Instrument panelen för Office 365-klient hantering](../../../sum/deploy-use/office-365-dashboard.md) visar en lista över relevanta enheter när diagram avsnitt har marker ATS. <!--1357281 --> 



## <a name="next-steps"></a>Nästa steg
När du är redo att installera den här versionen, se [uppdateringar för Configuration Manager](../../servers/manage/updates.md).
