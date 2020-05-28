---
title: Teknisk för hands version 1806
titleSuffix: Configuration Manager
description: Lär dig mer om nya funktioner som är tillgängliga i Configuration Manager Technical Preview version 1806.
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 2168f844f1c9ef98ea21da68b73531bca7aad999
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905181"
---
# <a name="capabilities-in-technical-preview-1806-for-configuration-manager"></a>Funktioner i Technical Preview 1806 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1806. Du kan installera den här versionen om du vill uppdatera och lägga till nya funktioner på din tekniska för hands versions webbplats. 

Läs artikeln om [teknisk för hands version](technical-preview.md) innan du installerar den här uppdateringen. Den artikeln är bekant med de allmänna kraven och begränsningarna för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>Kända problem i den här tekniska för hands versionen

### <a name="site-fails-to-upgrade-with-remote-content-library"></a><a name="ki_contentlib"></a>Platsen kan inte uppgraderas med fjärrinnehålls bibliotek
<!--514642-->
Det går inte att uppgradera platsen med följande fel i **cmupdate. log**:  

``` Log
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

Det här problemet uppstår i den här versionen när innehålls biblioteket finns på en annan plats.

#### <a name="workaround"></a>Lösning
Flytta innehålls biblioteket till en lokal enhet till plats servern. Mer information finns i [Konfigurera ett fjärrinnehålls bibliotek för plats servern](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server). 



</br>

**Följande är nya funktioner som du kan prova med den här versionen.**  



## <a name="third-party-software-updates"></a><a name="bkmk-3pupdate"></a>Program uppdateringar från tredje part
<!--1352101-->
Den här versionen itererar ytterligare om support för program uppdateringar från tredje part på grund av din [feedback från UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). Du behöver inte längre använda System Center Updates Publisher (SCUP) för några vanliga scenarier. Den nya noden **program uppdaterings kataloger från tredje part** i Configuration Manager-konsolen gör att du kan prenumerera på kataloger från tredje part, publicera sina uppdateringar till program uppdaterings platsen och sedan distribuera dem till klienter. 

Följande program uppdaterings kataloger från tredje part är tillgängliga i den här versionen:

 | Utgivare | Katalog namn |
 |--------|---------------------|
 | HP | HP-katalogen för klient uppdateringar |

SCUP fortsätter att stödja andra kataloger och scenarier. Listan över kataloger i noden program uppdaterings kataloger från tredje part i Configuration Manager-konsolen är dynamisk och kommer att uppdateras eftersom ytterligare kataloger är tillgängliga och stöds.


### <a name="prerequisites"></a>Förutsättningar
- Konfigurera hantering av program uppdateringar med en HTTPS-aktiverad program uppdaterings plats. Mer information finns i [förbereda för hantering av program uppdateringar](../../sum/get-started/prepare-for-software-updates-management.md).  
  - Program uppdaterings platsen måste finnas på plats servern för den här funktionen i den här versionen. <!--515810--> 

    > [!Tip]  
    > Program uppdaterings platsen kräver HTTPS eftersom det är ett krav för de WSUS-API: er som används för att hantera signerings certifikat. Klienterna behöver inte också vara HTTPS-aktiverade. Mer information om hur du aktiverar HTTPS på WSUS finns i följande artiklar om hjälp:  
    > - [Säker WSUS med Secure Sockets Layer Protocol](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) 
    > - [Blogg inlägg för WSUS-support](https://docs.microsoft.com/archive/blogs/sus/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names)

- Det finns tillräckligt med disk utrymme på program uppdaterings platsen, WSUSContent-mappen, för att lagra det binära innehållet för program uppdateringar från tredje part. Hur mycket lagrings utrymme som krävs varierar beroende på leverantör, typer av uppdateringar och vissa uppdateringar som du publicerar för distribution. Om du behöver flytta WSUSContent-mappen till en annan enhet med mer ledigt utrymme läser du blogg inlägget om WSUS support team [så här ändrar du den plats där WSUS lagrar uppdateringar lokalt](https://docs.microsoft.com/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally).  

- Aktivera och distribuera klient inställningen [Aktivera program uppdateringar från tredje part](../clients/deploy/about-client-settings.md#enable-third-party-software-updates) i **program uppdaterings** gruppen.  

- Plats servern kräver Internet åtkomst till download.microsoft.com via HTTPS-port 443. Tjänsten för synkronisering av program uppdateringar från tredje part körs för närvarande på plats servern. Den här tjänsten uppdaterar listan över tillgängliga kataloger från tredje part, laddar ned kataloger när du prenumererar och laddar ned uppdateringarna när de publiceras. Konfigurera Internet proxyinställningar, om det behövs, på fliken **proxy** i plats system rollens egenskaper för plats serverns dator.  


### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.


#### <a name="phase-1-enable-and-set-up-the-feature"></a>Fas 1: Aktivera och konfigurera funktionen
Utför följande steg *en gång per hierarki* för att aktivera och konfigurera funktionen för användning:  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen. Expandera **plats konfiguration**och välj noden **platser** .  

2. Välj platsen på den översta nivån i hierarkin. I menyfliksområdet klickar du på **Konfigurera plats komponenter**och väljer **program uppdaterings plats**.  

3. Växla till fliken **uppdateringar från tredje part** . Välj alternativet för att **Aktivera program uppdateringar från tredje part**. Mer information om certifikat alternativ finns i [förbättringar för att aktivera stöd för program uppdateringar från tredje part](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support).  

   > [!Note]  
   > Om du använder standard alternativet för Configuration Manager för att hantera det här certifikatet skapas ett nytt certifikat av typen **WSUS-signering från tredje part** i noden **certifikat** under **säkerhet** i arbets ytan **Administration** .  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>Fas 2: prenumerera på en katalog och synkronisera uppdateringar från tredje part
Utför följande steg för *varje tredje parts katalog* som du vill prenumerera på:  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **program uppdateringar** och välj noden **program uppdaterings kataloger från tredje part** .  

2. Välj katalogen som du vill prenumerera på och klicka på **Prenumerera på katalog** i menyfliksområdet.   

3. Granska och godkänn katalog certifikatet.  

   > [!Note]  
   > När du prenumererar på en program uppdaterings katalog från tredje part läggs det certifikat som du granskar och godkänner i guiden till på-platsen. Det här certifikatet är av typen **program uppdaterings katalog från tredje part**. Du kan hantera den från noden **certifikat** under **säkerhet** i arbets ytan **Administration** .  

4. Slutför guiden.  

   > [!Tip]  
   > Efter den första prenumerationen ska katalogen börja ladda ned direkt. Den synkroniseras sedan var 24: e timme i den här versionen. Om du inte vill vänta på att katalogen hämtas automatiskt klickar du på **Synkronisera nu** i menyfliksområdet.  
   > 
   > När katalogen har hämtats måste produktens metadata synkroniseras till program uppdaterings platsen. Mer information om den här processen samt hur du initierar manuellt finns i [Synkronisera program uppdateringar](../../sum/get-started/synchronize-software-updates.md). I det här läget kan du se uppdateringar från tredje part i noden **alla uppdateringar** . 

5. Konfigurera sedan program uppdaterings platsens **produkter** för den katalog i tredje part som du prenumererar på. Mer information finns i [Konfigurera klassificeringar och produkter som ska synkroniseras](../../sum/get-started/configure-classifications-and-products.md). När produkt villkoren ändras måste synkroniseringen av program uppdateringen ske igen.

Innan du kan se resultatet från klienterna måste de genomsöka och utvärdera uppdateringarna. Du kan aktivera den här cykeln manuellt från Configuration Manager kontroll panelen på en klient genom att köra åtgärden **genomsöknings cykel för program uppdateringar** . Mer information om processen finns i Introduktion till [program uppdateringar](../../sum/understand/software-updates-introduction.md).


#### <a name="phase-3-deploy-third-party-software-updates"></a>Fas 3: distribuera program uppdateringar från tredje part
Utför följande steg för *alla program uppdateringar från tredje part* som du vill distribuera till klienter:  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **program uppdateringar** och välj noden **alla program uppdateringar** .  

   > [!Tip]  
   > Klicka på **Lägg till kriterier** för att filtrera listan över uppdateringar. Lägg till exempel till **leverantören** för **Adobe Systems, Inc.** för att visa alla uppdateringar från Adobe.  

2. Välj de uppdateringar som krävs av klienterna. Klicka på **Publicera program uppdaterings innehåll från tredje part** och granska förloppet i SMS_ISVUPDATES_SYNCAGENT. log. Den här åtgärden hämtar binärfilerna för uppdateringen från leverantören och lagrar dem i mappen WSUSContent på program uppdaterings platsen. Den ändrar också status för uppdateringen från metadata till med innehåll och kan distribueras.  

   > [!Note]  
   > När du publicerar program uppdaterings innehåll från tredje part läggs alla certifikat som används för att signera innehållet till på-platsen. Dessa certifikat är av typen **program uppdaterings innehåll från tredje part**. Du kan hantera dem från noden **certifikat** under **säkerhet** i arbets ytan **Administration** .  

3. Distribuera uppdateringarna med den befintliga processen för hantering av program uppdateringar. Mer information finns i [distribuera program uppdateringar](../../sum/deploy-use/deploy-software-updates.md). På sidan **hämtnings platser** i guiden distribuera program uppdateringar väljer du standard alternativet för att **Ladda ned program uppdateringar från Internet**. I det här scenariot har innehållet redan publicerats till program uppdaterings platsen, som används för att ladda ned innehållet för distributions paketet.


### <a name="monitoring-progress-of-third-party-software-updates"></a>Övervaknings förlopp för program uppdateringar från tredje part
Synkronisering av program uppdateringar från tredje part hanteras av SMS_ISVUPDATES_SYNCAGENT-komponenten på plats servern. Du kan visa status meddelanden från den här komponenten eller Visa mer detaljerad status i SMS_ISVUPDATES_SYNCAGENT. log. Den här loggen finns på plats servern i undermappen **loggar** i platsens installations katalog. Som standard är den här sökvägen `C:\Program Files\Microsoft Configuration Manager\Logs` . Mer information om övervakning av den allmänna processen för program uppdaterings hantering finns i [övervaka program uppdateringar](../../sum/deploy-use/monitor-software-updates.md).


### <a name="known-issues"></a>Kända problem
- Tjänsten för synkronisering av program uppdateringar från tredje part stöder inte den program uppdaterings plats som kon figurer ATS för att använda ett **anslutnings konto för WSUS-servern**. Om det här kontot har kon figurer ATS på fliken **Proxy-och konto inställningar** på sidan Egenskaper för program uppdaterings plats visas följande fel meddelande i SMS_ISVUPDATES_SYNCAGENT. log:  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
Mer information om det här kontot finns i [anslutnings konto för program uppdaterings plats](../plan-design/hierarchy/accounts.md#software-update-point-connection-account).<!--515492-->  

- Blanda inte användningen av andra verktyg som SCUP med den här nya integrerade funktionen för program uppdatering från tredje part. Tjänsten för synkronisering av program uppdateringar från tredje part kan inte publicera innehåll till uppdateringar som har lagts till i WSUS av ett annat program, verktyg eller skript, till exempel SCUP. Åtgärden **publicera innehålls program från tredje part** kan inte utföras på dessa uppdateringar. Om du behöver distribuera uppdateringar från tredje part som den här funktionen ännu inte stöder, använder du den befintliga processen fullständigt för att distribuera uppdateringarna.<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Konfigurera Windows Defender SmartScreen-inställningar för Microsoft Edge
<!--1353701-->
I den här versionen läggs tre inställningar för [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) till i [inställnings principen för Microsoft Edge-webbläsaren](../../compliance/deploy-use/browser-profiles.md). Principen innehåller nu följande ytterligare inställningar på sidan SmartScreen- **Inställningar** :
- **Tillåt SmartScreen**: anger om Windows Defender SmartScreen tillåts. Mer information finns i [AllowSmartScreen Browser-principen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Användare kan åsidosätta SmartScreen-prompten för platser**: anger om användare kan åsidosätta varningar från Windows Defender SmartScreen-filtret om potentiellt skadliga webbplatser. Mer information finns i [PreventSmartScreenPromptOverride Browser-principen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Användare kan åsidosätta SmartScreen-prompten för filer**: anger om användare kan åsidosätta varningar från Windows Defender SmartScreen-filtret om att ladda ned overifierade filer. Mer information finns i [PreventSmartScreenPromptOverrideForFiles Browser-principen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Synkronisera MDM-princip från Microsoft Intune för en samhanterad enhet
<!--1357377-->
Från och med den här versionen när du [växlar en samhanterings arbets belastning](../../comanage/how-to-switch-workloads.md), synkroniserar de samhanterade enheterna automatiskt MDM-principen från Microsoft Intune. Den här synkroniseringen inträffar även när du startar åtgärden **Ladda ned dator princip** från klient meddelanden i Configuration Manager-konsolen. Mer information finns i [Starta klient princip hämtning med hjälp av klient meddelanden](../clients/manage/manage-clients.md#BKMK_PolicyRetrieval).



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>Över gång till Office 365-arbetsbelastning i Intune med samhantering
<!--1357841-->
Du kan nu gå över arbets belastningen för Office 365 från Configuration Manager till Microsoft Intune när du har aktiverat samhantering. Om du vill gå över den här arbets belastningen går du till sidan Egenskaper för samhantering och flyttar skjutreglaget från Configuration Manager till pilot eller alla. Mer information finns i [Co-Management för Windows 10-enheter](../../comanage/overview.md).

Det finns också ett nytt globalt villkor, **Office 365-program som hanteras av Intune på enheten**. Det här villkoret läggs till som standard som ett krav på nya Office 365-program. När du översätter den här arbets belastningen uppfyller inte samhanterade klienter kraven på programmet. Installera därför inte Office 365 som distribuerats via Configuration Manager.

### <a name="known-issue"></a>Kända problem
- Den här arbets belastnings över gången gäller för närvarande endast för Office 365-distributioner. Configuration Manager fortsätter att hantera Office 365-uppdateringar.<!--510876--> Mer information, inklusive en möjlig lösning, finns i Configuration Manager version 1802 versions meddelande om att [Ändra Office 365-klient inställningen gäller inte](../servers/deploy/install/release-notes.md).



## <a name="package-conversion-manager"></a>Paketomvandlingshanteraren 
<!--1357861-->
Package Conversion Manager är nu ett integrerat verktyg som gör att du kan konvertera äldre Configuration Manager 2007-paket till Configuration Manager aktuella gren program. Sedan kan du använda funktioner i program som beroenden, krav regler och mappning mellan användare och enhet.

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

> [!Important]  
> Om du tidigare har installerat en äldre version av Package Conversion Manager måste du först avinstallera den innan du uppgraderar platsen. Den nya integrerade versionen kräver inte installation, men kan orsaka konflikter med befintliga versioner.  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **program hantering** och välj **paket**.  
2. Välj ett paket. Följande tre alternativ är tillgängliga i **paket konverterings** gruppen i menyfliksområdet:  
     - **Analysera paket**: starta konverterings processen genom att analysera paketet.
     - **Konvertera paket**: vissa paket kan enkelt konverteras till program med den här åtgärden.
     - **Åtgärda och konvertera**: vissa paket kräver att problem korrigeras innan de konverteras till program.  


3. Gå till arbets ytan **övervakning** och välj **paket konverterings status**. Den nya instrument panelen visar den övergripande analys-och konverterings statusen för paket på-platsen. En ny bakgrunds aktivitet sammanfattar automatiskt analys data.  

   > [!Tip]  
   > Package Conversion Manager kräver inte att du planerar analys av paket. Den här åtgärden hanteras nu av den integrerade sammanfattnings uppgiften.  

![Skärm bild av instrument panelen för paket konverterings status](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>Distribuera program uppdateringar utan innehåll
<!--1357933-->
Nu kan du distribuera program uppdateringar till enheter utan att först hämta och distribuera program uppdaterings innehåll till distributions platser. Den här funktionen är fördelaktig vid hantering av mycket stort uppdaterings innehåll eller om du alltid vill att klienter ska hämta innehåll från Microsoft Update moln tjänsten. Klienter i det här scenariot kan också hämta innehåll från peer-datorer som redan har det innehåll som krävs. Den Configuration Manager klienten fortsätter att hantera innehålls hämtningen och kan därför använda funktionen Configuration Manager peer-cache eller andra tekniker som leverans optimering. Den här funktionen stöder alla uppdaterings typer som stöds av Configuration Manager hantering av program uppdateringar, inklusive Windows-och Office-uppdateringar. 

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

1. Starta en program uppdaterings distribution per normal. Mer information finns i [distribuera program uppdateringar](../../sum/deploy-use/deploy-software-updates.md).
2. I guiden distribuera program uppdateringar på sidan **distributions paket** väljer du alternativet nytt för **inget distributions paket**.

### <a name="known-issues"></a>Kända problem
- Ikonen för en uppdatering som distribueras med den här inställningen visas felaktigt med ett rött X som om uppdateringen är ogiltig. Mer information finns i [ikoner som används för program uppdateringar](../../sum/understand/software-updates-icons.md). <!--515556-->  
- Den här inställningen är endast integrerad med guiden distribuera program uppdateringar. Den är för närvarande inte tillgänglig med automatiska distributions regler. <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Office Customization Tool-integrering med Office 365-installations programmet
<!--1358149-->
Office-verktyget för anpassning är nu integrerat med Office 365-installations programmet i Configuration Manager-konsolen. När du skapar en distribution för Office 365 kan du nu konfigurera de senaste Office-hanterbarhets inställningarna dynamiskt. Verktyget Office-anpassning uppdateras samtidigt som lanseringen av nya versioner av Office 365. Nu kan du dra nytta av de nya hanterings inställningarna i Office 365 så snart de är tillgängliga. 

### <a name="prerequisites"></a>Förutsättningar
- Datorn som kör Configuration Managers konsolen behöver Internet åtkomst via HTTPS-port 443. Installations guiden för Office 365-klienten använder ett webb läsar API för Windows standard som öppnas https://config.office.com . Om en Internet-proxy används måste användaren kunna komma åt denna URL.

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** och väljer noden **Office 365 klient hantering** .
2. Klicka på installations panelen för **office 365** i instrument panelen för att starta installations guiden för Office 365-klienten. Mer information finns i [distribuera Office 365-appar](../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps).
3. På sidan **Office-inställning** klickar **du på gå till Office-webb sida**. Använd verktyget för anpassning av Office Online för att ange inställningar för den här distributionen. 
4. Klicka på **Skicka** i det övre högra hörnet när du är klar. Slutför installations guiden för Office 365-klienten.



## <a name="improvements-to-cloud-management-gateway"></a>Förbättringar av Cloud Management Gateway
Den här versionen innehåller följande förbättringar av Cloud Management Gateway (CMG):

### <a name="simplified-client-bootstrap-command-line"></a>Kommando rad för förenklad klient start
<!--1358215-->
När du installerar Configuration Manager-klienten på Internet via en CMG krävs nu färre kommando rads egenskaper. Mer information om ett exempel på det här scenariot finns i [kommando raden för att installera Configuration Manager-klienten](../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client) när du förbereder för samhantering. 

Följande kommando rads egenskaper krävs i alla scenarier:
- CCMHOSTNAME  
- SMSSITECODE  

Följande egenskaper krävs när du använder Azure AD för klientautentisering i stället för PKI-baserade certifikat för klientautentisering:
- AADCLIENTAPPID  
- AADRESOURCEURI  

Följande egenskap krävs om klienten växlar tillbaka till intranätet:
- SMSMP  

Följande exempel innehåller alla ovanstående egenskaper:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Mer information finns i [Egenskaper för klient installation](../clients/deploy/about-client-installation-properties.md).

### <a name="download-content-from-a-cmg"></a>Hämta innehåll från en CMG
<!--1358651-->
Tidigare var du tvungen att distribuera en distributions plats för moln och CMG som separata roller. I den här versionen kan en CMG också hantera innehåll till klienter. Den här funktionen minskar de nödvändiga certifikaten och kostnaden för virtuella Azure-datorer. Aktivera den här funktionen genom att aktivera det nya alternativet för att **tillåta att CMG fungerar som en moln distributions plats och hanterar innehåll från Azure Storage** på fliken **Inställningar** i egenskaperna för CMG. 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Ett betrott rot certifikat krävs inte med Azure AD
<!--503899-->
När du skapar en CMG behöver du inte längre ange ett [betrott rot certifikat](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) på sidan Inställningar. Detta certifikat krävs inte när du använder Azure Active Directory (Azure AD) för klientautentisering, men som används för att krävas i guiden.

> [!Important]  
> Om du använder certifikat för PKI-klientautentisering måste du fortfarande lägga till ett betrott rot certifikat till CMG.



## <a name="improvements-to-secure-client-communications"></a>Förbättringar för säker klient kommunikation
<!--1358278,1358279-->
Den här versionen fortsätter att iterera till [förbättrad säker klient kommunikation](capabilities-in-technical-preview-1805.md#improved-secure-client-communications) genom att ta bort ytterligare beroenden på nätverks åtkomst kontot. När du aktiverar alternativet för nya webbplatser **för att använda Configuration Manager-genererade certifikat för HTTP-plats system**behöver inte följande scenarier ett konto för nätverks åtkomst för att ladda ned innehåll från en distributions plats:  

- Aktivitetssekvenser som körs från startmedia eller PXE
- Aktivitetssekvenser som körs från Software Center  

Dessa aktivitetssekvenser kan vara för distribution av operativ system eller anpassade. Det finns också stöd för arbets grupps datorer.



## <a name="software-center-infrastructure-improvements"></a>Förbättringar av Software Center-infrastrukturen
<!--1358309-->
Program katalog roller krävs inte längre för att Visa användar tillgängliga program i Software Center. Den här ändringen hjälper dig att minska Server infrastrukturen som krävs för att leverera program till användare. Software Center använder nu hanterings platsen för att hämta den här informationen, vilket hjälper större miljöer att skala bättre genom att tilldela dem till [gräns grupper](../servers/deploy/configure/boundary-groups.md#management-points).

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

1. Ta bort alla program katalog roller från platsen. Dessa roller omfattar program katalogens webb tjänst plats och webbplats för program katalog.
2. Distribuera ett program som tillgängligt för en användar samling.
3. Använd Software Center som mål användare för att bläddra efter, begära och installera programmet.

### <a name="known-issue"></a>Kända problem
- Om du använder en Azure Active Directory ansluten klient med den här funktionen ska du inte konfigurera platsen att **använda Configuration Manager-genererade certifikat för HTTP-platssystem**. Den här funktionen är i konflikt med den här funktionen.<!--515846--> Mer information om den här inställningen finns i [förbättrad säker klient kommunikation](capabilities-in-technical-preview-1805.md#improved-secure-client-communications).



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Etablera Windows-appaket för alla användare på en enhet
<!--1358310-->
Nu kan du etablera ett program med ett Windows-appaket för alla användare på enheten. Ett vanligt exempel på det här scenariot är etablering av en app från Microsoft Store för företag och utbildning, till exempel Minecraft: Education Edition, för alla enheter som används av studenter i en skola. Tidigare Configuration Manager endast installera programmen per användare. När du har loggat in på en ny enhet skulle en student behöva vänta på att få åtkomst till en app. Nu när appen är etablerad till enheten för alla användare kan de vara produktivare snabbare.

> [!Important]  
> Var försiktig med att installera, konfigurera och uppdatera olika versioner av samma Windows app-paket på en enhet, vilket kan orsaka oväntade resultat. Det här problemet kan uppstå när du använder Configuration Manager för att etablera appen, men sedan tillåta att användare uppdaterar appen från Microsoft Store. Mer information finns i nästa steg-vägledning när du [hanterar appar från Microsoft Store för företag](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

När du konfigurerar en offline-licensierad app, tillåter Configuration Manager inte att Windows automatiskt uppdaterar den från Microsoft Store.  

### <a name="try-it-out"></a>prova!
 Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

1. Skapa ett nytt program. Den här appen måste vara från ett Windows-appaket eller en offline-licensierad app som du har synkroniserat från Microsoft Store för företag och utbildning.  

2. På sidan **allmän information** i guiden Skapa program aktiverar du alternativet för att **etablera det här programmet för alla användare på enheten**.  

   > [!Tip]  
   > Om du ändrar ett befintligt program finns den här inställningen på fliken **användar upplevelse** i program egenskaperna.  

3. Distribuera programmet till en enhets samling.  

4. Logga in på en målenhet med olika användar konton och starta programmet.  

> [!Note]  
> Om du behöver avinstallera ett etablerad program från enheter som användarna redan har loggat in på, måste du skapa två avinstallations distributioner. Rikta den första avinstallations distributionen till en enhets samling som innehåller enheterna. Rikta den andra avinstallations distributionen till en användar samling som innehåller de användare som redan har loggat in på enheter med det etablerade programmet. När du avinstallerar en etablerad app på en enhet avinstallerar Windows för närvarande inte appen för användare även. 



## <a name="improvements-to-the-surface-dashboard"></a>Förbättringar av Surface-instrumentpanelen
<!--1358654-->
Den här versionen innehåller följande förbättringar av [Surface-instrument panelen](../clients/manage/surface-device-dashboard.md):
- På Surface-instrumentpanelen visas nu en lista över relevanta enheter när diagram avsnitt har marker ATS.
   - Om du klickar på panelen **procent av Surface-enheter** öppnas en lista över Surface-enheter.
   - Om du klickar på en stapel i den **fem översta panelen inbyggda versioner av inbyggd program vara** öppnas en lista över Surface-enheter med den aktuella versionen av den inbyggda program
- När du visar dessa enhets listor på Surface-instrumentpanelen kan du högerklicka på en enhet och utföra vanliga åtgärder.



## <a name="hardware-inventory-default-unit-revision"></a>Standard enhets revision för maskin varu inventering
<!--514442-->
I [Configuration Manager version 1710](../plan-design/changes/whats-new-in-version-1710.md#site-infrastructure), har standard enheten som används i många rapportfunktioner ändrats från megabyte (MB) till gigabyte (GB). På grund av [förbättringar av maskin varu inventeringen för stora heltals värden](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)och utifrån kundfeedback, är standardenheten nu MB igen.



## <a name="next-steps"></a>Nästa steg
Information om hur du installerar eller uppdaterar den tekniska för hands versionen finns i [teknisk för hands version för Configuration Manager](technical-preview.md).    
