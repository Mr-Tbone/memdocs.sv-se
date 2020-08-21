---
title: Funktioner i Technical Preview 1605
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1605.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 1836a4c7d08547405dad08d7e60eb108d0dfd00f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695723"
---
# <a name="capabilities-in-technical-preview-1605-for-configuration-manager"></a>Funktioner i Technical Preview 1605 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1605. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats.      Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.  

 **Kända problem i den här tekniska för hands versionen:**  

- Om du uppdaterar egenskaperna för en hanterings plats efter installationen av Technical Preview 1605 kan du se ett konsol fel som gör att konsolen stängs.  Om detta inträffar kan du avinstallera hanterings platsen och sedan installera om hanterings platsen med hjälp av önskade inställningar. Alternativt kan du ändra hanterings platsen innan du installerar Technical Preview 1605.  

- När du använder funktionen Windows Store för företag med teknisk för hands version 1604 och sedan uppgraderar till teknisk för hands version 1605, kan du inte längre Visa onboarding-data. All annan funktion fortsätter att fungera. Om du har registrerat dig för den tekniska för hands versionen 1604 fortsätter du att vara registrerad när du har installerat Technical Preview 1605 och behöver inte vidta några ytterligare åtgärder.  

  **Följande är nya funktioner som du kan prova med den här versionen.**  

##  <a name="per-app-vpn-for-windows-10-devices"></a><a name="BKMK_PerAppVPN"></a> Per app-VPN för Windows 10-enheter  
 För Windows 10-enheter som hanteras med Configuration Manager med Intune kan du lägga till en lista över appar som automatiskt öppnar en VPN-anslutning som du har konfigurerat via Configuration Manager-administratörskonsolen. Du kan välja att begränsa VPN-trafik till dessa appar, eller så kan du fortsätta att tillåta all trafik via VPN-anslutningen.  

 **Krav**:  

-   Configuration Manager med Intune  

-   En Windows 10 VPN-profil som har distribuerats till minst en enhet  

##  <a name="improvements-to-the-install-software-updates-task-sequence"></a><a name="BKMK_InstallSU"></a> Förbättringar av aktivitetssekvensen installera program uppdateringar  
 Följande förbättringar har gjorts i aktivitetssekvensen installera program uppdateringar:  

-   En ny aktivitetssekvens variabel, SMSTSSoftwareUpdateScanTimeout, är tillgänglig för att ge dig möjlighet att styra tids gränsen för genomsökningen av program uppdateringar under steget installera program uppdateringar. Standardvärdet är 30 minuter.  

-   Det har gjorts förbättringar av loggningen. Logg filen Smsts. log innehåller nya logg poster som hänvisar till andra loggfiler som kan hjälpa dig att felsöka problem under installationen av program uppdateringar.  

##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a><a name="BKMK_PrepareConfigMgrClient"></a> Förbättringar av steget förbereda ConfigMgr-klienten för att avbilda en aktivitetssekvens  
 Steget Förbered ConfigMgr-klient tar nu bort Configuration Manager-klienten fullständigt, i stället för att bara ta bort viktig information. När aktivitetssekvensen distribuerar den avbildade operativ Systems avbildningen kommer den att installera en ny Configuration Manager-klient varje gång.  

##  <a name="grace-period-for-required-application-deployments"></a><a name="BKMK_Grace"></a> Respitperiod för obligatoriska program distributioner  
 I vissa fall kanske du vill ge användare mer tid att installera nödvändiga program distributioner utöver de tids gränser som du har konfigurerat. Om en slutanvändare till exempel precis har returnerat från semestern kan de vänta en stund medan förfallna program distributioner installeras. De kan dock fortfarande installera programmet direkt när de vill.  

 För att hjälpa till att lösa det här problemet kan du nu definiera en **respitperiod** genom att distribuera Configuration Manager klient inställningar till en samling.  

 Utför följande åtgärder för att konfigurera respitperioden:  

1. På sidan **dator agent** i klient inställningar konfigurerar du den nya **periodens respitperiod för tvång efter distributionens tids gräns (timmar)** med ett värde mellan **1** och **120** timmar.  

2. I en ny program distribution, eller i egenskaperna för en befintlig distribution, **väljer du kryss** rutan **fördröj Tvingad tillämpning av distributionen enligt användar inställningar**, upp till den grace-period som definierats i klient inställningarna.  

    Alla distributioner som har den här kryss rutan markerad och som är riktade till enheter som du också distribuerar klient inställningen till använder Grace-perioden.  

   I den här versionen används inte Grace-perioden som du konfigurerar för klient enheter. Om du konfigurerar en respitperiod och markerar kryss rutan kommer programmet att installeras i det första icke-affärsfönster som användaren har konfigurerat efter tids gränsen.  

   Liknande alternativ har lagts till i guiden distribution av program uppdateringar, guiden automatiska distributions regler och egenskaps sidor. Dessa är dock inte implementerade i den här tekniska för hands versionen.  

##  <a name="new-experience-for-remote-device-actions"></a><a name="BKMK_Remote"></a> Ny upplevelse för fjär renhets åtgärder  
 Upplevelsen för att utföra fjär renhets åtgärder från Configuration Manager-konsolen har förbättrats.  
Vanliga åtgärder som att ta bort **/Rensa**, **återställa lösen ord**, **fjärrlåsning**och **kringgå Aktiveringslås** finns nu i den **fjärranslutna enhet åtgärder** -menyn som nås från arbets ytan **till gångar och efterlevnad** .  

 ![Skärm bild för ny fjär renhets åtgärd](media/New-Remote-Device-Actions.png)  

 Du kan se statusen för var och en av dessa åtgärder på följande platser:  

- I informations fönstret när du väljer en enhet från noden **enheter** .  

- På sidan **Egenskaper** för en enhet.  

- På huvud sidan i noden **enheter** (alla kolumner kan inte visas som standard).  

##  <a name="windows-store-for-business-apps"></a><a name="BKMK_WSFB"></a> Windows Store för företag-appar  
 [Windows Store för företag](https://www.microsoft.com/business-store) är där du kan hitta och köpa appar för din organisation, enskilt eller i volym. Genom att ansluta butiken till Configuration Manager kan du hantera volym köpta appar från Configuration Manager-konsolen, till exempel:  

- Du kan synkronisera listan med köpta appar med Configuration Manager  

- Appar som är synkroniserade visas i Configuration Manager-konsolen och du kan distribuera dem precis som andra appar  

- Var 24: e timme Configuration Manager hämtar information om program licensiering från Store och du kan granska detta i Configuration Manager-konsolen  

  I 1604 Technical Preview-versionen kan du synkronisera och Visa appar från Windows Store för företag i Configuration Manager-konsolen. I den här versionen har vi lagt till möjligheten att skapa och distribuera Configuration Manager program från synkroniserade Store-appar.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Konfigurera synkronisering av Windows Store för företag  

1.  I Azure Active Directory registrerar du Configuration Manager som hanterings verktyg för webb program och/eller webb-API. Då får du ett klient-ID som du kommer att behöva senare.  

    1.  I noden Active Directory i [https://manage.windowsazure.com](https://manage.windowsazure.com) väljer du din Azure Active Directory och klickar sedan på **program**  >  **Lägg till**.  

    2.  Klicka på **Lägg till ett program som min organisation utvecklar**.  

    3.  Ange ett namn för programmet, Välj **webb program** och/eller **webb-API**och klicka sedan på pilen **Nästa** .  

    4.  Ange samma URL för både **inloggnings-URL: en** och **app-ID-URI: n**. URL: en kan vara vad som helst och behöver inte matcha en riktig adress. Du kan till exempel ange **https:// &lt; dindomän>/SCCM**.  

    5.  Slutför guiden.  

2.  I Azure Active Directory skapar du en klient nyckel för det registrerade hanterings verktyget.  

    1.  Markera det program som du nyss skapat och klicka på **Konfigurera**.  

    2.  Under **nycklar**väljer du en varaktighet i listan och klickar på **Spara**. Då skapas en ny klient nyckel. Navigera inte från den här sidan förrän du har registrerat Windows Store för företag till Configuration Manager.  

3.  Konfigurera Configuration Manager som lagrings hanterings verktyg i Windows Store för företag.  

    1.  Öppna [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools) och logga in om du uppmanas att göra det.  

    2.  Godkänn användnings villkoren om det behövs.  

    3.  Under **hanterings verktyg**klickar du på **Lägg till ett hanterings verktyg**.  

    4.  I **Sök efter verktyget efter namn**, anger du namnet på det program som du skapade i AAD tidigare och klickar sedan på **Lägg till**.  

    5.  Klicka på **Aktivera** bredvid det program som du nyss importerade.  

    6.  I guiden **Visa offline-licensierade appar** klickar du på **Ja** om du vill tillåta att offline-licensierade program kan köpas.  

4.  Köp minst en app från Windows Store för företag.  

5.  I arbets ytan **Administration** i Configuration Manager-konsolen expanderar du **Cloud Services**och klickar sedan på **Windows Store för företag.**  

6.  På fliken **Start** går du till gruppen **skapa** och klickar på **Lägg till Windows Store för företag-konto**.  

7.  Lägg till klient-ID, klient-ID och klient nyckel från Azure Active Directory och slutför sedan guiden.  

8.  När du är färdig visas det konto som du konfigurerade i listan **Windows Store för företag-konton** i Configuration Manager-konsolen.  

### <a name="try-it-out"></a>prova!  
 Försök att utföra följande uppgift och berätta sedan för oss hur den fungerade genom att använda vårt feedback-formulär på sidan för [Configuration Manager feedback-program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) på Microsoft Connect-webbplatsen:  

 Skapa och distribuera ett Configuration Manager-program från en Windows Store för företag-licensierad app.  

1. I arbets ytan **program varu bibliotek** i Configuration Manager-konsolen expanderar du **program hantering**och klickar sedan på **licens information för Store-appar**.  

2. Välj den app som du vill distribuera och klicka sedan på **skapa program**i gruppen **skapa** på fliken **Start** .  

   Ett Configuration Manager program skapas som innehåller appen Windows Store för företag. Sedan kan du distribuera och övervaka programmet på samma sätt som andra Configuration Manager program.  

> [!IMPORTANT]  
>  När du skapar ett Configuration Manager program med en enda distributions typ från en offline-licensierad app, kan detta distribueras till enheter som hanteras med MDM och som även hanteras med Configuration Manager-klienten. Om du försöker distribuera en app med flera distributions typer fungerar inte installationen.  
>   
>  Du kan för närvarande inte distribuera licensierade appar online med Configuration Manager.  

##  <a name="general-improvements-for-volume-purchased-apps"></a><a name="BKMK_VPP2"></a> Allmänna förbättringar för appar som har köpts i volym  

-   I den här versionen har volym inköpta appar från Windows Store för företag och iOS App Store samlats in i samma vy, **licens information för Store-appar**.  

-   För iOS-köpta appar har fliken Apples volymköpsprogram tagits bort från **appen appaket för iOS-webbläsare** i guiden Skapa program. Använd följande steg för att skapa en volym köps app för iOS:  

    1.  1.  I arbets ytan **program varu bibliotek** i Configuration Manager-konsolen expanderar du **program hantering**och klickar sedan på **licens information för Store-appar**.  

    2.  2.  Välj den app som du vill distribuera och klicka sedan på **skapa program**i gruppen **skapa** på fliken **Start** .  

-   Den plats du använder för att hämta och ladda upp en Apple VPP-token för volym köps appar i Configuration Manager-konsolen har ändrats. Du kan nu göra detta på arbets ytan **admin** under noden **Cloud Services**  >  **Apples volymköpsprogram tokens** .  

##  <a name="enterprise-data-protection-edp"></a><a name="BKMK_VPP"></a> Enterprise Data Protection (EDP)  
 Du kan skapa konfigurations objekt som du kan använda för att distribuera EDP-principer (Enterprise Data Protection), inklusive att låta dig välja dina skyddade appar, din EDP-skydds nivå och hur du hittar företags data i nätverket. Mer information om EDP finns i följande avsnitt:  

- [Skydda dina företags data med Windows Information Protection (Pia)](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Skapa och distribuera en princip för Windows Information Protection (Pia) med Configuration Manager](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)


##  <a name="end-users-can-install-apps-from-the-company-portal"></a><a name="BKMK_End"></a> Slutanvändare kan installera appar från Företagsportal  
 Lokal MDM introducerades i Configuration Manager version 1511. I tidigare versioner kan du distribuera program till MDM-hanterade Windows 10-enheter med distributions syftet **obligatorisk** installation för lokala MDM-hanterade enheter.  

 I den här versionen kan du nu distribuera appar med ett distributions syfte som **är tillgängligt** för användare av lokala MDM-hanterade Windows 10-datorer och användare kan nu installera apparna från företagsportal.
Om Företagsportal är öppen i mer än 15 minuter i den här tekniska för hands versionen visas ett fel meddelande i slutanvändaren. Undvik problemet genom att starta om Företagsportal.  

### <a name="before-you-start"></a>Innan du börjar  

#### <a name="server-prerequisites"></a>Server krav  

-   .NET 4,5 eller högre (omstart krävs)  

-   PowerShell 3,0 för konfigurations skript (omstart krävs)  

#### <a name="client-prerequisites"></a>Klient krav  

-   Windows 10 Desktop 1511 (OS-version 10586,218) eller senare  

#### <a name="general-prerequisites"></a>Allmänna krav  

-   Se till att du har slutfört [förberedelse stegen för lokal MDM](../../mdm/plan-design/plan-on-premises-mdm.md) och [registrerat dina enheter](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md).  

-   För bästa möjliga installations upplevelse när du använder Företagsportal kontrollerar du att Configuration Manager har en aktiv anslutning till Microsoft Intune.  

-   Om du väljer alternativet för Mass registrering konfigurerar du mappning mellan användare och enhet för den registrerade enheten innan du provar det här scenariot.  

### <a name="configuration-steps"></a>Konfigurationssteg  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>Installera Programkatalog roller och aktivera stöd för hantering av mobila enheter  

1.  Lägg till rollerna Programkatalog-webbtjänst och webbplats  

    1.  Välj **https-läge** och alternativet **Tillåt att mobila enheter använder den här programkatalog-webb tjänst punkten** .  

    2.  Begränsningar i den här tekniska för hands versionen:  

        -   Du måste avinstallera alla befintliga Programkatalog-roller innan du väljer alternativet för att tillåta att mobila enheter ansluter.  

        -   Kontrol lera att det bara finns en uppsättning Programkatalog roller och att rollerna är samplacerade på samma plats system med registrerings platsen och proxy för registrerings plats.  

2.  Kontrol lera att följande komponenter fungerar från noden komponent status i Configuration Manager-konsolen:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Konfigurera gränser  
 Konfigurera de nödvändiga gränserna för distributions platser för endast intranät.  

> [!NOTE]  
>  Endast IPv4-intervall gränser stöds för tillfället för hantering av mobila enheter.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>Distribuera Företagsportal programmet och konfigurationen  

1. Använd konfigurations skriptet som ingår i den tekniska för hands versionen för att förbereda Företagsportal distribution och konfiguration:  

   1. Öppna ett upphöjt PowerShell-kommando fönster.  

   2. Kör **set-ExecutionPolicy RemoteSigned**  

   3. I \Cd.latest\SMSSETUP\TOOLS\MDM för katalogens ** &lt; SCCM \> -installation** kör **.\ConfigurationScript.ps1**  

      Konfigurations skriptet gör följande:  

   4. Skapar ett Configuration Manager program med en distributions typ för Windows-appaket med hjälp av **CompanyPortalOnPremisesMDM. appx** i samma mapp.  

   5. Skapar ett konfigurations objekt och en konfigurations bas linje som konfigurerar Företagsportal.  

   6. Distribuerar både konfigurations bas linjen och programmet och lägger till programmet till alla distributions platser.  

   > [!NOTE]
   >  Om Programkatalog-rollerna inte är samplacerade med den primära platsen, vidta följande åtgärder:  
   > 
   > - Gå till arbets ytan **till gångar och efterlevnad** och leta upp konfigurationsobjektet konfigurations objekt för **ONPREMMDM Portal Configuration CI-Server URL: er**  
   >   -   Ändra värdet för **efterlevnadsprinciper** till det fullständigt kvalificerade domän namnet för det plats system där programkatalog roller finns.  

2. När Företagsportal programmet och dess konfiguration båda har distribuerats kontrollerar du att program-och konfigurations bas linjen är kompatibla för den enhet som använder **distributions** avsnittet i Configuration Manager-konsolen. Företagsportal visas som **företagsportal (Technical Preview)** på Start menyn på enheten.  

### <a name="try-it-out"></a>prova!  
 Försök att utföra följande uppgifter och berätta sedan för oss hur det fungerade genom att använda vårt feedback-formulär på sidan för [Configuration Manager feedback-program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) på Microsoft Connect-webbplatsen:  

1.  Distribuera flera program med distributions typer som stöds till en användar samling med ett distributions syfte **tillgängligt**. För den här tekniska för hands versionen stöds inte program som kräver administratörs godkännande och kommer inte att visas i Företagsportal.  

2.  Användarna kan sedan bläddra efter och installera appar från Företagsportal.  

     När du har öppnat Företagsportal visas en dialog ruta med namnet **Configuration Manager** ange användarens Active Directory autentiseringsuppgifter (antingen i formatet user@domain eller domän \ användare) för att logga in.  

##  <a name="new-tabs-for-updates-and-operating-systems-in-software-center"></a><a name="BKMK_SW1"></a> Nya flikar för uppdateringar och operativ system i Software Center  
 I den här versionen har följande ändringar gjorts för att förbättra layouten för Software Center-programmet:  

-   Fliken **program** har delats in i tre separata flikar för **uppdateringar**, **operativ system** (som båda fanns tidigare i listan med **filter** ) och **program**.  

##  <a name="service-a--server-group"></a><a name="BKMK_ServerGroups"></a> Underhålla en Server grupp  
 Technical Preview för Configuration Manager, version 1511, innehöll möjlighet att skapa en samling där alla enheter i samlingen utgör en Server grupp. Sedan kan du konfigurera de Server grupps inställningar som ska användas när du distribuerar program uppdateringar till Server gruppen, styra procent andelen datorer som uppdateras vid en viss tidpunkt och konfigurera PowerShell-skript för för distribution och efter distribution för att köra anpassade åtgärder.  

 Technical Preview för Configuration Manager, version 1605, lägger till möjligheten att uppdatera datorerna i Server gruppen i en angiven ordning som du definierar, lägger till förbättrad övervakning för att visa status för datorerna i Server gruppen och ger möjlighet att ta bort de distributions lås som är användbara när klienter har misslyckats med att installera program uppdateringarna och hindrar andra klienter från att installera sina program uppdateringar.  

### <a name="try-it-out"></a>prova!  
 Försök att utföra följande uppgifter och berätta sedan för oss hur det fungerade genom att använda vårt feedback-formulär på sidan för [Configuration Manager feedback-program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) på Microsoft Connect-webbplatsen:  

-   Jag kan skapa en samling som representerar en Server grupp. För det här testet kan du konfigurera insamlade medlemskaps regler så att de har två datorer i den här samlingen.   

-   Jag kan ange att datorer i Server gruppen ska installera program uppdateringar i en speciell ordning baserat på Server grupps inställningarna för samlingen. Använd exempel skripten i proceduren för att ange skript för för distribution och efter distribution.  

-   Jag kan distribuera en program uppdatering till den här samlingen. Granska start.txt och end.txt filer (som skapats från exempel skripten) i C:\Temp och kontrol lera start-och slut tider för distributionen på datorerna i Server gruppen. Se filen UpdatesDeployment. log för mer information.  

#### <a name="to-create-a-collection-for-a-server-group"></a>Så här skapar du en samling för en Server grupp  

1.  [Skapa en enhets samling](../clients/manage/collections/create-collections.md) som innehåller datorerna i Server gruppen.  

2.  I arbets ytan **till gångar och efterlevnad** klickar du på **enhets samlingar**, högerklickar på den samling som innehåller datorerna i Server gruppen och klickar sedan på **Egenskaper**.  

3.  På fliken **Allmänt** väljer du **alla enheter tillhör samma server grupp**och klickar sedan på **Inställningar**.  

4.  På sidan **Inställningar för Server grupp** anger du en av följande inställningar:  

    -   **Tillåt att en procent andel av datorerna uppdateras samtidigt**: anger att endast en viss procent andel av klienterna uppdateras vid ett och samma tillfälle. Om samlingen till exempel har 10 klienter och samlingen har kon figurer ATS för att uppdatera 30% av klienterna samtidigt, kommer bara 3 klienter att installera program uppdateringar vid en angiven tidpunkt.  

    -   **Tillåt att ett antal datorer uppdateras samtidigt**: anger att endast ett visst antal klienter uppdateras vid ett och samma tillfälle.  

    -   **Ange underhålls ordningen**: anger att klienterna i samlingen ska uppdateras en i taget i den ordning som du konfigurerar. En klient kommer bara att installera program uppdateringar när klienten är före den i listan har installerat program uppdateringarna.  

5.  Ange om du vill använda ett skript för för distribution (Node dränering) eller efter distribution (Node Resume).  

    > [!TIP]  
    >  Följande är exempel som du kan använda vid testning av skript för för distribution och efter distribution som skriver den aktuella tiden till en textfil:  
    >   
    >  **Före distribution**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Efter distributionen**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Distribuera program uppdateringar till Server gruppen och övervaka status  

1.  [Distribuera program uppdateringar](../../sum/deploy-use/deploy-software-updates.md) till Server grupps samlingen.  

2.  [Övervaka program uppdaterings distributionen](../../sum/deploy-use/monitor-software-updates.md). Förutom standardvyerna för övervakning av program uppdateringar visas en ny tillstånds Beskrivning när en klient väntar på att program uppdateringarna ska installeras. **Väntar på Lås** visas för det nya läget.  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>Så här tar du bort distributions lås för datorer i en Server grupp  

1.  Klicka på **enhets samlingar**på arbets ytan **till gångar och efterlevnad** och klicka på samlingen för att rensa distributions lås.  

2.  På fliken **Start** går du till gruppen **distribution** och klickar på **ta bort Server grupp distributions lås**. När klienterna har misslyckats med att installera program uppdateringarna och hindrar andra klienter från att installera sina program uppdateringar, kan distributions låsen rensas manuellt.  

##  <a name="support-for-microsoft-defender-advanced-threat-protection-service"></a><a name="BKMK_ATP"></a> Stöd för tjänsten Microsoft Defender Avancerat skydd  
 Microsoft Defender Avancerat skydd (ATP) är en tjänst som hjälper företag att upptäcka, undersöka och svara på avancerade attacker i sina nätverk. Microsoft Defender ATP kallas tidigare Windows Defender ATP. Läs mer om [Microsoft Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). Configuration Manager kan hjälpa dig att publicera och övervaka hanterade klient enheter för Windows 10 jubileums version.  

### <a name="try-it-now"></a>Prova nu!  
 Försök att utföra följande uppgifter och berätta sedan för oss hur det fungerade genom att använda vårt feedback-formulär på sidan för [Configuration Manager feedback-program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) på Microsoft Connect-webbplatsen:  

- Publicera enheter till online tjänsten Microsoft Defender Advanced Threat Protection (ATP)  

- Övervaka Microsoft Defender ATP-distribution till hanterade enheter  

  **Förutsättningar**  

- Prenumeration på online tjänsten Microsoft Defender Advanced Threat Protection  

- Klienter som kör Windows 10, jubileums version (version 14328 och senare)  

- Skapa en konfigurations fil för klient onboarding  

  ##### <a name="how-to-create-an-onboarding-configuration-file"></a>Så här skapar du en konfigurations fil för onboarding  

  1.  Logga in på Microsoft Defender ATP-online tjänsten  

  2.  Klicka på meny alternativet **klient**  

  3.  Välj **Configuration Manager** och klicka på **Ladda ned paket**.  

  4.  Hämta den komprimerade Arkiv filen (zip) och extrahera innehållet.  


##### <a name="onboard-devices-for-microsoft-defender-atp"></a>Onboard-enheter för Microsoft Defender ATP  

1. I Configuration Manager-konsolen navigerar du **till gångar och efterlevnad**-  >  **Översikt**  >  **Endpoint Protection**  >  **Windows Defender ATP-principer** och klickar på **skapa Windows Defender ATP-princip**. Guiden Microsoft Defender ATP-princip öppnas.  

2. Ange **namn** och **Beskrivning** för Microsoft Defender ATP-principen och välj **onboarding**. Klicka på Nästa.  

3. **Bläddra** till konfigurations filen som tillhandahålls av din organisations Microsoft Defender ATP-moln tjänst klient. Klicka på **Nästa**.  

4. Ange de fil exempel som samlas in och delas från hanterade enheter för analys.  

   - **Ingen** – inga exempelfiler samlas in för analys  

   - **Portable körbara filer** – filer som programfiler (. exe), DLL-filer (Dynamic-Library Link), teckensnittsfiler och liknande filer som kan utnyttjas i cyberattacker samlas in och delas för analys  

     Klicka på **Nästa**.  

5. Granska sammanfattningen och Slutför guiden.  

6. Nu kan du distribuera Microsoft Defender ATP-principen till hanterade klient datorer genom att klicka på **distribuera**.  

##### <a name="monitor-microsoft-defender-atp"></a>Övervaka Microsoft Defender ATP  

1.  I Configuration Manager-konsolen, navigerar du till **övervakning**  >  **Översikt**  >  **säkerhet** och klickar sedan på **Windows Defender ATP**.  

2.  Granska instrument panelen för Microsoft Defender Avancerat skydd.  

    -   **Distributions status för Windows Defender-agent** – antal och procent andel berättigade hanterade klient datorer med aktiv Microsoft Defender ATP-princip onboarded  

    -   **Windows Defender ATP-agenthälsa** – procent andel dator klienter som rapporterar status för Microsoft Defender ATP-agenten  

        -   **Felfri** fungerar korrekt  

        -   **Inaktiv** – inga data har skickats till tjänsten under tids perioden  

        -   **Agent tillstånd** – system tjänsten för agenten i Windows körs inte  

        -   **Ingen onboarding** – principen tillämpades men agenten har inte rapporterat någon princip  

##  <a name="on-premises-device-health-attestation"></a><a name="BKMK_DHA"></a> Lokala Hälsoattestering för enhet  
 Hälsoattestering för Windows 10-enheter kan nu konfigureras för att kommunicera med den lokala infrastrukturen. Administratörer kan ange om rapportering görs via molnet eller lokala resurser. Om lokalt har valts för rapportering av hälso deklarationen kan du ange en URL för tjänsten. Detta gör att klient datorer utan Internet åtkomst kan aktivera och hantera enheter med hälsoattestering.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Aktivera hälsoattestering för lokala enheter  
 I 1605 har vi åtgärdat några buggar som upptäckts i 1604 Technical Preview.  Konfigurera tjänsten för lokal hälsoattestering med hjälp av inställningarna för klient agenten för att testa den.  

1.  I Configuration Manager-konsolen navigerar du till **Administration**  >  **Översikt**  >  **klient inställningar**och ställer sedan in **Använd tjänsten för lokal hälsoattestering** på **Ja**.  

2.  Ange **URL till lokal hälsoattesteringstjänst**och klicka sedan på **OK**.  

##  <a name="new-restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Nya alternativ för omstart för Windows 10-klienter efter installation av program uppdatering  
 När en program uppdatering som kräver en omstart distribueras med hjälp av Configuration Manager och installeras på en dator, är en väntande omstart schemalagd och en dialog ruta för omstart visas. För närvarande, för Windows 8 och senare, om du stänger av eller startar om datorn med hjälp av Windows energi alternativ (i stället för från dialog rutan Starta om), förblir starta om-dialog rutan efter det att datorn startats om och datorn måste startas om vid den konfigurerade tids gränsen. I den här tekniska för hands versionen kommer alternativet att **Uppdatera och starta om** och **Uppdatera och stänga** av att vara tillgängligt på Windows 10-datorer i Windows energi alternativ när det finns en väntande omstart för en Configuration Manager program uppdatering. När du använder något av dessa alternativ visas inte omstartsdialogrutan efter omstarten av datorn.  

##  <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a><a name="BKMK_IMEI"></a> Fördeklarera företagsägda enheter med IMEI-eller iOS-serienummer  
 Nu kan du identifiera företagsägda enheter genom att importera sina ID-nummer (International Station Mobile Equipment Identity). Du kan ladda upp en fil med kommaavgränsade värden (. csv) som innehåller IMEI-nummer för enheten, eller så kan du ange enhets information manuellt.  Du kan också importera serie nummer för iOS-enheter.  Importerade information anger ägarskap för de enheter som registreras som "företag".  En Intune-licens krävs fortfarande för varje användare som har åtkomst till tjänsten.  

### <a name="try-it-out"></a>prova!  
 Försök att utföra följande uppgifter och berätta sedan för oss hur det fungerade genom att använda vårt feedback-formulär på sidan för [Configuration Manager feedback-program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) på Microsoft Connect-webbplatsen:  

-   Importera en uppsättning IMEI-nummer i en. csv-fil. Varje rad kan innehålla IMEI-numret följt av ett informations fält.  

-   Importera IMEI-nummer manuellt från Configuration Manager-konsolen.  

-   Importera en uppsättning iOS-serienummer i en. csv-fil. Återigen innehåller varje rad ett tal följt av all information om enheten.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Fördeklarera företagsägda enheter med IMEI- eller iOS-serienummer  

1. I Configuration Manager-konsolen går du **till till gångar och efterlevnad**,  >  **Översikt**  >  **alla företagsägda**enheter  >  **fördeklarerade enheter**och klickar sedan på **skapa fördeklarerade enheter**. Guiden för fördeklarerade enheter öppnas.  

2. Ange hur du vill lägga till enhets information:  

   -   **Ladda upp en. csv-fil som innehåller IMEI-nummer och information** – för att ladda upp en lista med tal, se steg #3.  

   -   **Lägg till IMEI-nummer och information manuellt** – om du vill ange information manuellt skriver du IMEI-numret eller iOS-serienummeret och information om enheterna och fortsätter sedan till steg #4.  

3. För överförda filer bläddrar du till CSV-filen som innehåller information för att fördeklarera företagsägda enheter. Filen måste ha följande format, exklusive den översta raden (endast för vägledning):  

   |**IMEI #**|**iOS-serie**|**Operativsystem**|**Information**|
   |---|---|---|---|
   |123456789012345||WINDOWS|Företagsägda Windows-enhet|
   |123456789012|A0BCD0EFGH0J|iOS|Företagsägda iOS-enheter|
   |123456789012346||ANDROID|Företagsägda Android-enhet|

    **Sammanfattning**  

   - Kolumn 1: IMEI-nummer – antingen krävs ett IMEI-nummer eller iOS-serienummer för varje rad  

   - Kolumn 2: iOS-serienummer – endast serie serie nummer kan vara fördeklarerade. Använd IMEI-nummer för andra enhets plattformar  

   - Kolumn 3: enhetens operativ system (Skift läge krävs):  

     -   IOS – alla iOS-enheter  

     -   WINDOWS – innehåller Windows Phone, Window 10 Mobile och Windows-datorer  

     -   ANDROID – alla Android-enheter  

   - Kolumn 4: information – ytterligare enhets information som visas i Configuration Manager-konsolen  

     Klicka på **Nästa**.  

4. Granska resultatet av fil importen. Tidigare importerade IMEI-eller serie nummer kommer att ha information uppdaterad med nya uppgifter.  Klicka på **Nästa** för att fortsätta eller **tillbaka** för att bevara uppdaterad information och slutför sedan guiden.