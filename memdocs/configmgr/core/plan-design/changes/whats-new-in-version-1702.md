---
title: Ny version 1702
titleSuffix: Configuration Manager
description: Få information om ändringar och nya funktioner som introducerats i version 1702 av Configuration Manager.
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: fa29c1b2474d6a0a42b7ff8e3624a3ec8d6a090e
ms.sourcegitcommit: 4f10625e8d12aec294067a1d9138cbce19707560
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87912302"
---
# <a name="what39s-new-in-version-1702-of-configuration-manager"></a>Vad&#39;s nya i version 1702 av Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Uppdatering 1702 för Configuration Manager aktuella grenen är tillgänglig som en uppdatering i konsolen för tidigare installerade platser som kör version 1602, 1606 eller 1610. Den är också tillgänglig som en bas linje version som du kan använda när du installerar en ny distribution.

> [!TIP]  
> Om du vill installera en ny plats måste du använda en bas linje version av Configuration Manager.  
>
> Läs mer om:    
> - [Nya platser installeras](../../servers/deploy/install/installing-sites.md)  
> - [Installera uppdateringar på platser](../../servers/manage/updates.md)  
> - [Bas linje-och uppdaterings versioner](../../servers/manage/updates.md#bkmk_Baselines)

Följande avsnitt innehåller information om ändringar och nya funktioner som introducerats i version 1702 av Configuration Manager.  

## <a name="deprecated-features-and-operating-systems"></a>Föråldrade funktioner och operativ system
Läs om support ändringar innan de implementeras i [borttagna och föråldrade objekt](deprecated/removed-and-deprecated.md).

Version 1702 släpper stöd för följande produkter:
- **SQL Server 2008 R2**för plats databas servrar. Utfasningen av stödet gavs [första gången](deprecated/removed-and-deprecated-server.md#sql-server) den 10 juli 2015. Den här versionen av SQL Server finns kvar när du använder en Configuration Manager version före version 1702.
- **Windows Server 2008 R2**, för plats system servrar och de flesta plats system roller. Utfasningen av stödet gavs [första gången](deprecated/removed-and-deprecated-server.md#server-os) den 10 juli 2015. Den här versionen av Windows stöds inte om du använder en Configuration Manager-version före version 1702.  
- **Windows Server 2008**, för plats system servrar och de flesta plats system roller. Utfasningen av stödet gavs [första gången](deprecated/removed-and-deprecated-server.md#server-os) den 10 juli 2015.
- **Windows XP Embedded**, som ett klient operativ system. Utfasningen [presenterades först](deprecated/removed-and-deprecated-client.md#deprecated-client-operating-systems) den 10 juli 2015. Den här versionen av Windows stöds inte om du använder en Configuration Manager-version före version 1702.




## <a name="site-infrastructure"></a>Plats infrastruktur

### <a name="improvements-for-in-console-search"></a>Förbättringar för i konsols ökning
Följande är förbättringar av att använda Sök i Configuration Manager-konsolen:
- **Objekt Sök väg:**  
  Många objekt har nu stöd för en kolumn med namnet **objekt Sök väg**.  När du söker efter och tar med den här kolumnen i dina visnings resultat kan du Visa sökvägen till varje objekt. Om du till exempel kör en sökning efter appar i noden program och även söker efter underordnade noder, visas sökvägen till varje objekt som returneras i kolumnen *objekt Sök väg* i resultat fönstret.   

- **Bevarande av söktext:**  
  När du anger text i sökrutan och sedan växlar mellan att söka efter en underordnad nod och den aktuella noden, behålls den text som du har angett och är tillgänglig för en ny sökning utan att du behöver ange den igen.

- **Bevarande av ditt beslut om att söka efter underordnade noder:**  
  Det alternativ som du väljer för att söka i den *aktuella noden* eller *alla undernoder* är nu kvar när du ändrar noden som du arbetar i. Det här nya beteendet innebär att du inte behöver återställa det här beslutet hela tiden när du förflyttar dig runt i-konsolen. Som standard när du öppnar-konsolen är alternativet att bara söka i den aktuella noden.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Skicka feedback från Configuration Manager-konsolen

Du kan använda feedback alternativen i konsolen för att skicka feedback direkt till utvecklings teamet.

Du kan hitta **feedback** -alternativet:
- I menyfliksområdet längst till vänster på fliken Start på varje nod.  
  ![Menyfliksområde](./media/feedback-home.png)

- När du högerklickar på ett objekt i-konsolen.   
   ![Skärmdumpsverktygen – Klicka på alternativ](./media/feedback-option.png)   

  Om du väljer **feedback** öppnas webbläsaren på [webbplatsen för Configuration Manager UserVoice feedback](https://configurationmanager.uservoice.com/forums/300492-ideas).


###  <a name="changes-for-updates-and-servicing"></a>Ändringar för uppdateringar och underhåll
Följande är ändringar för uppdateringar och underhåll:

- **Node-plats**   
  När du har installerat version 1702 visas noden **uppdateringar och underhåll** som en nod på den översta nivån under **Administration**. Det är inte längre en underordnad nod nedan **Cloud Services**.

- **Nya uppdaterings tillstånd**  
  När du visar tillgängliga uppdateringar i-konsolen finns det två nya tillstånd:  
  - **Tillgänglig för installation** – det här är en uppdatering som har hämtats och är redo att installeras.
  - **Klar för hämtning** – den här uppdateringen är tillgänglig, men har inte hämtats. Du kan välja att ladda ned uppdateringen, men den har ersatts av en nyare uppdatering.


- **Enklare uppdaterings alternativ**  
  Nästa gången infrastrukturen uppfyller två eller fler uppdateringar laddas bara den senaste uppdateringen ned. Om din aktuella plats version till exempel är två eller fler äldre än den senaste versionen som är tillgänglig, hämtas bara den senaste uppdaterings versionen automatiskt.  

  Du kan välja att ladda ned och installera andra tillgängliga uppdateringar, även om de inte är den senaste versionen. Om du hämtar en äldre uppdatering visas en varning om att uppdateringen har ersatts av en nyare. Om du vill hämta en uppdatering som är *tillgänglig för hämtning*väljer du uppdateringen i-konsolen och klickar sedan på **Ladda ned**.

- **Förbättrad rensning av äldre uppdateringar**   
  Vi har lagt till en automatisk rensning som tar bort onödiga nedladdningar från mappen "EasySetupPayload" på plats servern. Eftersom detta introduceras i version 1702 börjar rensningen att fungera efter att du har installerat en efterföljande uppdatering som en samlad uppdatering eller en framtida uppdaterings version.  


### <a name="data-warehouse-service-point"></a>Informations lager service punkt
Använd informations lager service platsen för att lagra och rapportera långsiktiga historiska data för din Configuration Manager-distribution.

Informations lagret har stöd för upp till 2 TB data, med tidsstämplar för ändrings spårning. Lagring av data görs genom automatiska synkroniseringar från Configuration Manager plats databasen till informations lager databasen. Den här informationen är sedan tillgänglig från repor ting Services-platsen.

Mer information finns i [informations lager service platsen](../../servers/manage/data-warehouse.md).


### <a name="peer-cache-improvements"></a>Förbättringar i peer-cache
Från och med version 1702 avvisar en peer-cache käll dator en begäran om innehåll när peer-cachens käll dator uppfyller något av följande villkor:  
-  Är i läget för låg batteri nivå.
-  CPU-belastningen överskrider 80% vid den tidpunkt då innehållet begärs.
-  Disk-I/O har en *AvgDiskQueueLength* som överstiger 10.
-  Det finns inga fler tillgängliga anslutningar till datorn.   
Mer information finns i **begränsad åtkomst till en peer-cache-källa** i peer- [cache för Configuration Manager klienter](../hierarchy/client-peer-cache.md).   

Dessutom läggs tre nya rapporter till i din rapporterings plats. Du kan använda dessa rapporter för att lära dig mer om avvisade innehålls begär Anden, inklusive vilka gränser, dator och innehåll som har varit inblandade. Se [övervakning](../hierarchy/client-peer-cache.md#monitoring) i avsnittet peer-cache.

### <a name="content-library-cleanup-tool"></a>Rensningsverktyg för innehållsbibliotek
Använd [rensnings verktyget för innehålls bibliotek](../hierarchy/content-library-cleanup-tool.md) för att ta bort innehåll från distributions platser när innehållet inte längre är associerat med ett program.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Använda OMS-anslutningen med Azure Government molnet
Du kan använda OMS-anslutningen för att ansluta till OMS Log Analytics i Microsoft Azure Government molnet. Detta kräver att du ändrar en konfigurations fil innan du installerar OMS-anslutningsprogrammet så att kopplingen kan arbeta med det offentliga molnet. Mer information finns i [använda OMS-anslutningen med Azure Government molnet](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm).

### <a name="software-update-points-are-added-to-boundary-groups"></a>Program uppdaterings platser läggs till i gränser grupper
Från och med version 1702 använder klienterna gränser grupper för att hitta en ny program uppdaterings plats, och för att återgå och hitta en ny program uppdaterings plats om den aktuella inte längre är tillgänglig. Du kan lägga till enskilda program uppdaterings platser i olika gränser grupper för att kontrol lera vilka servrar som en klient kan hitta. Mer information finns i [program uppdaterings platser](../../servers/deploy/configure/boundary-groups.md#software-update-points) i avsnittet [Konfigurera gränser grupper](../../servers/deploy/configure/boundary-groups.md) .


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Kompatibilitetsinställningar

### <a name="new-compliance-settings-for-ios"></a>Nya kompatibilitetsinställningar för iOS

Vi har lagt till många nya inställningar för iOS-enheter för att matcha de som är tillgängliga med Microsoft Intune.


## <a name="application-management"></a>Programhantering

### <a name="improved-support-for-windows-store-for-business-apps"></a>Förbättrat stöd för Windows Store för företag-appar

Nu kan du distribuera licensierade appar online från Windows Store för företag till Windows 10-datorer som du hanterar med hjälp av Configuration Manager-klienten.
Mer information finns i [Hantera appar från Windows Store för företag](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Sök efter körning av körbara filer innan du installerar ett program

I dialog rutan **Egenskaper** för en distributions typ, på fliken **installations beteende** , kan du nu ange en eller flera körbara filer som, om den körs, ska blockera installationen av distributions typen. Användaren måste stänga den körbara filen som körs (eller så kan den stängas automatiskt för distributioner med syftet obligatorisk) innan distributions typen kan installeras.

Om programmet har distribuerats som **tillgängligt**och en användare försöker installera ett program uppmanas de att stänga alla körbara körbara filer som du har angett innan de kan fortsätta med installationen.

Om programmet har distribuerats vid **behov**, och alternativet **automatiskt stänger alla körbara filer som du har angett på fliken installations beteende i dialog rutan Egenskaper för distributions typ** , visas en dialog ruta som informerar dem om att körbara filer som du har angett ska stängas automatiskt när tids gränsen för programinstallationen har uppnåtts.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Förbättringar av program hantering för Hybrid MDM

- [Distribuera iOS-appar som köpts i volym till enhets samlingar](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Stöd för iOS-volym köps program för utbildning](#support-for-ios-volume-purchase-program-for-education)
- [Stöd för flera token för volym köps program](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>Distribution av operativsystem

### <a name="expire-stand-alone-media"></a>Utgånget fristående medium
När du skapar fristående medier finns det nya alternativ för att ange valfria start-och förfallo datum för mediet. De här inställningarna är inaktiverade som standard. Datumen jämförs med system klockan på datorn innan det fristående mediet körs. När system tiden infaller före start tiden eller senare än förfallo tiden startar inte det fristående mediet. Dessa alternativ är också tillgängliga med hjälp av PowerShell-cmdleten New-CMStandaloneMedia. Mer information finns i [skapa fristående media](../../../osd/deploy-use/create-stand-alone-media.md).

### <a name="package-id-displayed-in-task-sequence-steps"></a>Paket-ID som visas i stegen i aktivitetssekvensen
Alla aktivitetssekvenser som refererar till ett paket, driv rutins paket, operativ system avbildning, start avbildning eller uppgraderings paket för operativ system kommer nu att visa paket-ID: t för det refererade objektet. När ett steg i en aktivitetssekvens refererar till ett program visas objekt-ID.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Stöd för ytterligare innehåll i fristående media
Ytterligare innehåll stöds nu i fristående media. Du kan välja ytterligare paket, driv rutins paket och program som ska mellanlagras på mediet tillsammans med det andra innehåll som refereras i aktivitetssekvensen. Tidigare mellanlagrades endast innehåll som refereras i aktivitetssekvensen på fristående media. Mer information finns i [skapa fristående media](../../../osd/deploy-use/create-stand-alone-media.md).

### <a name="hardware-inventory-collects-uefi-information"></a>Maskin varu inventering samlar in UEFI-information
En ny maskin varu inventerings klass (**SMS_Firmware**) och egenskap (**UEFI**) är tillgängliga för att hjälpa dig att avgöra om en dator startar i UEFI-läge. När en dator startas i UEFI-läge anges egenskapen **UEFI** till **True**. Detta är aktiverat i maskin varu inventeringen som standard. Mer information om maskin varu inventering finns i [så här konfigurerar du maskin varu inventering](../../clients/manage/inventory/configure-hardware-inventory.md).

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Förbättringar av varnings meddelanden i Software Center för aktivitetssekvenser med hög effekt
Den här versionen innehåller följande förbättringar av varnings meddelanden i Software Center för aktivitetssekvenser med hög effekt:

- I egenskaperna för aktivitetssekvensen kan du nu konfigurera en aktivitetssekvens, inklusive aktivitetssekvenser som inte är operativ system, som en distribution med hög risk. En aktivitetssekvens som uppfyller vissa villkor definieras automatiskt som hög påverkan. Mer information finns i [Hantera distributioner med hög risk](../../servers/manage/settings-to-manage-high-risk-deployments.md).
- I egenskaperna för aktivitetssekvensen kan du välja att använda standard meddelandet eller skapa ett eget anpassat aviserings meddelande för distributioner med hög effekt.
- I egenskaperna för aktivitetssekvensen kan du konfigurera Software Center-egenskaper, bland annat göra en omstart nödvändig, hämtnings storlek för aktivitetssekvensen och den beräknade körnings tiden.
- Standard distributions meddelandet med hög effekt för uppgraderingar på plats anger nu att dina appar, data och inställningar migreras automatiskt. Tidigare var standard meddelandet för alla installations program för operativ systemet, vilket indikerade att alla appar, data och inställningar skulle gå förlorade, vilket inte var sant för en uppgradering på plats.

Mer information finns i [Konfigurera inställningar för aktivitets sekvenser med hög effekt](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#set-a-task-sequence-as-a-high-impact-task-sequence)

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Gå tillbaka till föregående sida när en aktivitetssekvens Miss lyckas
Du kan nu gå tillbaka till en föregående sida när du kör en aktivitetssekvens och det uppstår ett problem. Innan den här versionen var du tvungen att starta om aktivitetssekvensen när det uppstod ett problem. Du kan till exempel använda knappen **föregående** i följande scenarier:

- När en dator startas i Windows PE kan start dialog rutan för aktivitetssekvens visas innan aktivitetssekvensen är tillgänglig. När du klickar på nästa i det här scenariot visas den sista sidan i aktivitetssekvensen med ett meddelande om att det inte finns några tillgängliga aktivitetssekvenser. Nu kan du klicka på **föregående** för att söka igen efter tillgängliga aktivitetssekvenser. Du kan upprepa den här processen tills aktivitetssekvensen är tillgänglig.
- När du kör en aktivitetssekvens, men beroende innehålls paket ännu inte är tillgängliga på distributions platser, Miss lyckas aktivitetssekvensen. Nu kan du distribuera det innehåll som saknas (om det inte distribuerats ännu) eller vänta tills innehållet är tillgängligt på distributions platserna och klicka sedan på **föregående** om du vill att aktivitetssekvensen ska sökas igen för innehållet.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Innehåll i förinställt cacheminne för tillgängliga distributioner och aktivitetssekvenser
Från och med version 1702 kan du välja att använda förcachet innehåll för tillgängliga distributioner av aktivitetssekvenser. Innehåll i förväg ger dig möjlighet att låta klienten Ladda ned tillämpligt innehåll så fort det tar emot distributionen. När användaren klickar på **Installera** i Software Center är innehållet därför klart och installationen startar snabbt eftersom innehållet finns på den lokala hård disken. Mer information finns i [Konfigurera för-cache-innehåll](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Konvertera från BIOS till UEFI under en uppgradering på plats
Windows 10 Creators Update introducerar ett enkelt konverterings verktyg som automatiserar processen för att partitionera om hård disken för UEFI-aktiverad maskin vara och integrera konverterings verktyget i Windows 7 till Windows 10 uppgraderings process på plats. När du kombinerar det här verktyget med aktivitetssekvensen för uppgradering av operativ system och OEM-verktyget som konverterar den inbyggda program varan från BIOS till UEFI, kan du konvertera datorerna från BIOS till UEFI under en uppgradering på plats till Windows 10 Creators Update. Mer information finns i avsnittet [om aktivitetssekvenser för att hantera BIOS till UEFI-konvertering](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Förbättringar av steget installera program i aktivitetssekvensen
Den här versionen introducerade följande förbättringar:
- Ökat maximalt antal program som du kan installera till 99 i steget **installera program** . Det tidigare maximala antalet var 9 program.
- När du lägger till program i steget **installera program** i aktivitetssekvensen kan du nu välja flera program i rutan **Välj program att installera** .

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Förbättringar av aktivitetssekvensen Använd driv rutin automatiskt
Nya variabler för aktivitetssekvens är nu tillgängliga för konfigurering av timeout-värdet för steget Använd aktivitetssekvensen automatiskt när du gör HTTP-katalog begär Anden. Följande variabler och standardvärden (i sekunder) är tillgängliga:
- SMSTSDriverRequestResolveTimeOut  
  Standard: 60
- SMSTSDriverRequestConnectTimeOut  
  Standard: 60
- SMSTSDriverRequestSendTimeOut  
  Standard: 60
- SMSTSDriverRequestReceiveTimeOut  
  Standard: 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Windows 10 ADK spåras av version
Windows 10 ADK spåras nu av build-versionen för att säkerställa en mer upplevelse vid anpassning av Windows 10-startavbildningar. Om webbplatsen till exempel använder Windows ADK för Windows 10, version 1607, kan endast start avbildningar med version 10.0.14393 anpassas i-konsolen. Mer information om hur du anpassar WinPE-versioner finns i [Anpassa Start avbildningar](../../../osd/get-started/customize-boot-images.md).

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>Käll Sök vägen för standard start avbildning kan inte längre ändras
Standard start avbildningar hanteras av Configuration Manager och standard käll Sök vägen för start avbildningen kan inte längre ändras i Configuration Manager-konsolen eller med hjälp av Configuration Manager SDK. Du kan fortsätta att konfigurera en anpassad käll Sök väg för anpassade Start avbildningar.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Standard start avbildningar återskapas efter uppgradering Configuration Manager till en ny version
Från och med den här versionen, när du uppgraderar Windows ADK-versionen och sedan använder uppdateringar och underhåll för att installera den senaste versionen av Configuration Manager, Configuration Manager återskapar standard start avbildningarna. Detta inkluderar den nya Window PE-versionen från den uppdaterade Windows ADK, den nya versionen av Configuration Manager-klienten, driv rutiner, anpassningar osv. Anpassade Start avbildningar ändras inte. Mer information finns i [Hantera start avbildningar](../../../osd/get-started/manage-boot-images.md#BKMK_BootImageDefault).

## <a name="software-updates"></a>Programuppdateringar

### <a name="deploy-office-365-apps-to-clients"></a>Distribuera Office 365-appar till klienter
Från och med version 1702 kan du från instrument panelen för Office 365-klient hantering starta Office 365-installations programmet där du kan konfigurera installations inställningar för Office 365, ladda ned filer från Office Content Delivery Networks (CDN) och distribuera filerna som ett program i Configuration Manager. Mer information finns i [Hantera Office 365 ProPlus-uppdateringar](../../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps).

> [!IMPORTANT]
> Office 365-appen som du skapar och distribuerar med hjälp av guiden Office 365-program i Configuration Manager hanteras inte automatiskt av Configuration Manager förrän du aktiverar inställningen **aktivera hantering av klient agenten för office 365-klienten igen** . Mer information finns i [om klient inställningar](../../clients/deploy/about-client-settings.md).

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Hantera filer för snabbinstallation för Windows 10-uppdateringar
Från och med version 1702 stöder Configuration Manager Express-installationsfiler för Windows 10-uppdateringar. När du använder en version av Windows 10 som stöds kan du använda Configuration Manager inställningar för att bara hämta ändringarna mellan den kumulativa Windows 10-uppdateringen och föregående månads uppdatering. Utan Express-installationsfiler Configuration Manager laddar ned den fullständiga kumulativa Windows 10-uppdateringen (inklusive alla uppdateringar från föregående månader) varje månad. Med hjälp av Express-installationsfiler kan du få mindre hämtningar och snabbare installations tider på klienter. Mer information finns i [Hantera Express-installationsfiler för Windows 10-uppdateringar](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Hantering av mobila enheter

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Android-och iOS-versioner är inte längre riktade i skapande guider för Hybrid MDM

Från och med version 1702 för hantering av mobila enheter (MDM) behöver du inte längre ange specifika versioner av Android och iOS när du skapar nya principer och profiler för Intune-hanterade enheter. I stället väljer du någon av följande enhets typer:

- Android
- Samsung KNOX Standard 4,0 och högre
- iPhone
- iPad

Den här ändringen påverkar guiderna för att skapa följande objekt:

- Konfigurationsobjekt
- Efterlevnadsprinciper
- Certifikatprofiler
- E-postprofiler
- VPN-profiler
- Wi-Fi-profiler

Med den här ändringen kan hybrid distributioner ge stöd snabbare för nya Android-och iOS-versioner utan att det krävs någon ny Configuration Manager-version eller-tillägg. När en ny version stöds i Intune fristående kommer användarna att kunna uppgradera sina mobila enheter till den versionen.

För att förhindra problem vid uppgradering från tidigare versioner av Configuration Manager är mobila operativ system versioner fortfarande tillgängliga på egenskaps sidorna för dessa objekt. Om du fortfarande behöver ange en viss version som mål, kan du skapa det nya objektet och sedan ange mål versionen på egenskaps sidan för det nya objektet. 

> [!NOTE]
> Den senaste versionen av mobil operativ systemet som är tillgänglig på sidan egenskaper gäller den versionen och alla senare versioner. Egenskaps sidor innehåller följande alternativ för att rikta in operativ system senare än Android 7 och iOS 10: 
> - **Android 7 och högre**
> - **Alla iOS 10 och högre iPhone-eller iPod touch-enheter**
> - **Alla iOS 10 och högre iPad-enheter**

### <a name="android-for-work-support"></a>Stöd för Android for Work
Från och med 1702 stöder hybrid hantering av mobila enheter med Microsoft Intune nu stöd för Android for Work-enheter och-hantering.

### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Distribuera iOS-appar som köpts i volym till enhets samlingar

Nu kan du distribuera licensierade appar till enheter samt användare. Beroende på apparnas förmåga att stödja enhets licensiering kommer en lämplig licens att krävas när du distribuerar den, enligt följande:

| Configuration Manager version | App har stöd för enhets licensiering? | Distributions samlings typ | Ansökan om licens |
| ----------------------------- | ------------------------------ | -------------------------- | --------------- |
|Tidigare än 1702|Ja|Användare|Användar licens|
|Tidigare än 1702|Nej|Användare|Användar licens|
|Tidigare än 1702|Ja|Enhet|Användar licens|
|Tidigare än 1702|Nej|Enhet|Användar licens|
|1702 och senare|Ja|Användare|Användar licens|
|1702 och senare|Nej|Användare|Användar licens|
|1702 och senare|Ja|Enhet|Enhets licens|
|1702 och senare|Nej|Enhet|Användar licens|

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Stöd för iOS-volym köps program för utbildning

Nu kan du även distribuera och spåra appar som du har köpt från iOS-volym köps programmet för utbildning.

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Stöd för flera token för volym köps program

Nu kan du associera flera token för Apples volym köps program med Configuration Manager.

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Stöd för branschspecifika appar i Windows Store för företag

Nu kan du synkronisera anpassade branschspecifika appar från Windows Store för företag.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Förbättringar av efterlevnadsprinciper för villkorlig åtkomst

En ny regel för efterlevnadsprinciper är tillgänglig för att hjälpa dig att blockera åtkomst till företags resurser som har stöd för villkorlig åtkomst, när användare använder appar som ingår i en icke-kompatibel lista över appar. Den icke-kompatibla listan över appar kan definieras av administratören när de nya kompatibla regel **appar som inte kan installeras**läggs till. Den här regeln kräver att administratören anger **appens namn**, **app-ID**och **app utgivare** (valfritt) när de lägger till en app i listan över inkompatibla. Den här inställningen gäller endast iOS-och Android-enheter.

Dessutom hjälper organisationerna att undvika data läckage via oskyddade appar och förhindra onödig data förbrukning via vissa appar.


### <a name="new-mobile-threat-defense-monitoring-tools"></a>Nya övervaknings verktyg för skydd mot mobila hot

Från och med version 1702 har du nya sätt att övervaka kompatibilitetsstatus med din leverantör av Mobile Threat försvar-tjänster.


## <a name="protect-devices"></a>Skydda enheter

### <a name="detect-outdated-antimalware-client-versions"></a>Identifiera inaktuella klient versioner av program mot skadlig kod
Från och med version 1702 kan du konfigurera en avisering för att säkerställa att Endpoint Protection-klienter inte är inaktuella. Mer information finns i [avisering för inaktuell klient för skadlig kod](../../../protect/deploy-use/endpoint-configure-alerts.md#alert-for-outdated-malware-client).

### <a name="device-health-attestation-updates"></a>Uppdateringar av hälsoattestering för enhet
Tjänsten hälsoattestering för enhet för lokala klienter kan nu konfigureras och hanteras från hanterings platsen. Mer information finns i [hälsoattestering](../../servers/manage/health-attestation.md).

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Certifikat profiler för Windows Hello för företag

Om du tänker lagra certifikat profiler i nyckel behållaren för Windows Hello för företag och certifikat profilen använder EKU för smartkortsinloggning måste du konfigurera behörigheter för nyckel registrering för att säkerställa att certifikatet verifieras korrekt.
Mer information finns i [Inställningar för Windows Hello för företag](../../../protect/deploy-use/windows-hello-for-business-settings.md).

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nytt Windows Hello för företag-aviseringar för slutanvändare
Ett nytt meddelande i Windows 10 informerar slutanvändarna om att de måste vidta ytterligare åtgärder för att slutföra installationen av Windows Hello för företag (till exempel att ställa in en PIN-kod).
