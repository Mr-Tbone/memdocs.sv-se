---
title: Teknisk för hands version 1807
titleSuffix: Configuration Manager
description: Lär dig mer om nya funktioner som är tillgängliga i Configuration Manager Technical Preview Branch version 1807.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 8ead53c71e336001ac820a437fa67758c6375cbd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694380"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Funktioner i Configuration Manager Technical Preview version 1807 

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1807. Installera den här versionen om du vill uppdatera och lägga till nya funktioner till din tekniska för hands versions webbplats. 

Läs artikeln om [teknisk för hands version](technical-preview.md) innan du installerar den här uppdateringen. Den artikeln är bekant med de allmänna kraven och begränsningarna för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback.     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>Kända problem 

### <a name="issues-with-office-365-software-updates"></a><a name="ki_o365"></a> Problem med Office 365-program uppdateringar
<!--521365-->
Om du hanterar Office 365-uppdateringar med teknisk för hands version 1806 och 1806,2 kan de Miss lyckas med att installera på klienter. 

#### <a name="workaround"></a>Lösning
- Ta bort befintliga distributions paket och program uppdaterings grupper för Office 365.  

- Från den 31 juli 2018 synkroniserar du Office 365-program uppdateringar och distribuerar bara de senaste uppdateringarna.  



</br>

**I följande avsnitt beskrivs de nya funktionerna för att prova i den här versionen:**  


## <a name="community-hub"></a><a name="bkmk_hub"></a> Community-hubb
<!--1357766-->

Community-hubb är en central plats för att dela användbara Configuration Manager objekt med andra. Se den nya **Community** -arbetsytan i Configuration Manager-konsolen och välj **Hub** -noden. Använd Community-hubb för att ladda ned följande typer av Configuration Manager objekt: 
- Skript
- Konfigurationsobjekt

![Configuration Manager konsol, community-arbetsyta, hubb](media/1357766-hub.png)

Om du vill se mer information om ett tillgängligt objekt klickar du på det i hubben. På sidan information klickar du på **Hämta** för att hämta objektet. När du laddar ned ett objekt från hubben läggs det automatiskt till på din webbplats. 

![Configuration Manager konsol, community-arbetsyta, hubb, informations sida](media/1357766-hub-details.png)

**Community** -arbetsytan innehåller även följande noder:

- **Dokumentation**: visar Configuration Manager [dokumentations bibliotek](/sccm/)  

- **Feedback**: visar Configuration Manager [UserVoice-webbplatsen](https://configurationmanager.uservoice.com/)  


### <a name="prerequisites"></a>Förutsättningar

- Använd Configuration Manager-konsolen på ett klient-OS.  

    - Alternativt men rekommenderas inte: inaktivera Internet Explorer på ett server-OS [: förbättrad säkerhets konfiguration](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10)).

- Datorn med-konsolen kräver Internet åtkomst och anslutning till följande platser:  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>Kända problem

Bidrags objekt till hubben är för närvarande inte tillgängliga i den här versionen. 



## <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_osd"></a> Ange enhet för etablering av OS-avbildning offline  
<!--1358924-->

Ange den enhet som Configuration Manager använder under offlineunderhåll av OS-avbildningar, baserat på din [feedback från UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive). Den här processen kan förbruka en stor mängd disk utrymme med temporära filer, så det här alternativet ger dig möjlighet att välja den enhet som ska användas. 


### <a name="try-it-out"></a>prova!

Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) med dina tankar om funktionen.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** . I menyfliksområdet klickar du på **Konfigurera plats komponenter** och väljer **program uppdaterings plats**.  

2. Växla **till fliken offlineunderhåll** och ange alternativet för **en lokal enhet som ska användas vid offline-underhåll av avbildningar**.  

Som standard är den här inställningen **Automatisk**. Med det här värdet väljer Configuration Manager den enhet där den är installerad. 

Under offlineunderhåll kan Configuration Manager lagra temporära filer i mappen `<drive>:\ConfigMgr_OfflineImageServicing` . Den monterar även OS-avbildningarna i den här mappen. 

Granska logg filen **OfflineServicingMgr. log** . 



## <a name="co-managed-device-sync-activity-from-intune"></a><a name="bkmk_comgmt"></a> Synkronisera aktivitet för samhanterad enhet från Intune
<!--1358565-->

Visa i Configuration Manager-konsolen om en samhanterad enhet är aktiv med Microsoft Intune. Det här läget baseras på data från [Intunes informations lager](/intune/reports-nav-create-intune-reports). Instrument panelen för **klient status** i Configuration Manager-konsolen visar **inaktiva klienter med Intune**. Den nya kategorin är för samhanterade enheter som är inaktiva med Configuration Manager, men som har synkroniserats med Intune-tjänsten den senaste veckan.


### <a name="try-it-out"></a>prova!

Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) med dina tankar om funktionen.

Om du redan har konfigurerat webbplatsen för samhantering: 

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden för **samtidig hantering** . Klicka på **Egenskaper** i menyfliksområdet.  

2. Växla till fliken **rapportering** . Klicka på **Logga in** och autentisera. Klicka sedan på **Uppdatera** för att aktivera Läs behörighet för Intune Data Warehouse.  

3. När platsen har synkroniserats med Intune går du till arbets ytan **övervakning** och väljer noden **klient status** . I avsnittet **övergripande klient status** , se raden för **inaktiva klienter som använder Intune**.  

Mer information om hur du aktiverar samhantering finns i [Co-Management för Windows 10-enheter](../../comanage/overview.md).



## <a name="repair-applications"></a><a name="bkmk_app-repair"></a> Reparera program
<!--1357866-->

Ange en reparations kommando rad för Windows Installer och skript installations distributions typer med hjälp av din [feedback från UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application). 


### <a name="try-it-out"></a>prova!

Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) med dina tankar om funktionen.

1. Öppna egenskaperna för en Windows Installer-eller skript installations distributions typ i Configuration Manager-konsolen.  

2. Växla till fliken **program** . Ange kommandot **Reparera program** .  

3. Distribuera appen. På fliken **distributions inställningar** i distributionen aktiverar du alternativet så att **slutanvändarna kan försöka reparera programmet**.  


### <a name="known-issue"></a>Kända problem

Den nya knappen i Software Center som användare kan använda för att **Reparera** appen visas inte i den här versionen.  



## <a name="approve-application-requests-via-email"></a><a name="bkmk_email-approve"></a> Godkänn program begär Anden via e-post
<!--1321550-->

Konfigurera e-postaviseringar för begäran om program godkännande. När en användare begär ett program får du ett e-postmeddelande. Klicka på länkar i e-postmeddelandet för att godkänna eller neka begäran, utan att behöva Configuration Manager-konsolen.


### <a name="prerequisites"></a>Förutsättningar

#### <a name="to-send-email-notifications"></a>Skicka e-postmeddelanden
- Aktivera den [valfria funktionen](../servers/manage/install-in-console-updates.md#bkmk_options) **Godkänn program begär Anden för användare per enhet**.  

- Konfigurera [e-postavisering för aviseringar](../servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts).  

#### <a name="to-approve-or-deny-requests-from-email"></a>Godkänna eller Neka förfrågningar från e-post
Om du inte konfigurerar de här förutsättningarna skickar-platsen e-postavisering om program begär Anden utan länkar till att godkänna eller neka begäran.  

- I plats egenskaperna aktiverar du **REST-slutpunkt för alla providers-roller på den här platsen och tillåter Configuration Manager Cloud Management Gateway-trafik**. Mer information finns i [data åtkomst för OData-slutpunkt](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access).  

    - Starta om tjänsten SMS_EXEC när du har aktiverat REST-slutpunkten

- [Gateway för molnhantering](../clients/manage/cmg/plan-cloud-management-gateway.md)  

- Publicera webbplatsen till [Azure-tjänster](../servers/deploy/configure/azure-services-wizard.md) för **moln hantering**  

    - Aktivera [identifiering av Azure AD-användare](../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

    - Konfigurera följande inställningar manuellt för den här inbyggda appen i Azure AD:  

        - **Omdirigerings-URI**: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth` . Använd det fullständigt kvalificerade domän namnet (FQDN) för CMG-tjänsten (Cloud Management Gateway), till exempel GraniteFalls.Contoso.com.   

        - **Manifest**: ange **oauth2AllowImplicitFlow** till True: `"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>prova!

Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) med dina tankar om funktionen.

1. I Configuration Manager-konsolen distribuerar du ett program som är tillgängligt för en användar samling. På sidan **distributions inställningar** aktiverar du det för godkännande. Ange en *enskild* e-postadress för att ta emot meddelandet.  

     > [!Note]  
     > Alla i din Azure AD-organisation som tar emot e-postmeddelandet kan godkänna begäran. Vidarebefordra inte e-postmeddelandet till andra såvida du inte vill att de ska vidta åtgärder.  

2. Som användare kan du begära programmet i Software Center.  

3. Du får ett e-postmeddelande som liknar följande exempel:  

![Exempel på e-postavisering om program godkännande](media/1321550-email.png)

> [!Note]  
> Länken för att godkänna eller neka är för eng ång slö tillfället. Du kan till exempel konfigurera ett grupp-alias för att ta emot meddelanden. MB godkänner begäran. Nu kan Bruce inte neka begäran.  



## <a name="improvement-to-script-output"></a><a name="bkmk_script"></a> Förbättring av utdata från skript
<!--1236459-->

Nu kan du Visa detaljerade skript utdata i oformaterat eller strukturerat JSON-format. Den här formateringen gör det lättare att läsa och analysera utdata. Om skriptet returnerar en giltig JSON-formaterad text, visar du de detaljerade utdata som antingen **JSON-utdata** eller **rå data**. I annat fall är det enda alternativet **skript-utdata**. 

#### <a name="example-script-output-is-valid-json"></a>Exempel: skriptets utdata är giltig JSON
Kommandoprompt `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>Exempel: skriptets utdata är inte giltig JSON
Kommandoprompt `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>prova!

Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) med dina tankar om funktionen.

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enhets samlingar** . Högerklicka på en samling och välj **Kör skript**. Mer information om hur du skapar och kör skript finns i [skapa och köra PowerShell-skript från Configuration Manager-konsolen](../../apps/deploy-use/create-deploy-scripts.md).  

2. Kör ett skript i mål samlingen.  

3. På sidan **övervakning av skript status** i guiden kör skript väljer du fliken **Sammanfattning** längst ned. Ändra de två List rutorna överst till **skript utdata** och **data tabell**. Dubbelklicka sedan på raden resultat för att öppna dialog rutan **detaljerade utdata** .  

4. På sidan **skript status övervakning** i guiden kör skript väljer du fliken **körnings information** längst ned. Dubbelklicka på en resultat rad för att öppna dialog rutan detaljerade utdata för den enheten.  



## <a name="improvement-to-third-party-software-updates"></a><a name="bkmk_3pupdate"></a> Förbättringar av program uppdateringar från tredje part
<!--1358714-->

Nu kan du ändra egenskaperna för anpassade kataloger.

Mer information finns i [stöd för program uppdateringar från tredje part för anpassade kataloger](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate).



## <a name="next-steps"></a>Nästa steg

Mer information om hur du installerar eller uppdaterar den tekniska för hands versionen finns i [Technical Preview](technical-preview.md).    

Mer information om de olika grenarna med Configuration Manager finns i [vilken gren av Configuration Manager ska jag använda?](../understand/which-branch-should-i-use.md)