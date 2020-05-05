---
title: Teknisk för hands version 1806,2
titleSuffix: Configuration Manager
description: Lär dig mer om nya funktioner som är tillgängliga i Configuration Manager Technical Preview version 1806,2.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 426767b65e0fd770a9a41ce9463948007a524c41
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078761"
---
# <a name="capabilities-in-technical-preview-18062-for-configuration-manager"></a>Funktioner i Technical Preview 1806,2 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1806,2. Du kan installera den här versionen om du vill uppdatera och lägga till nya funktioner på din tekniska för hands versions webbplats. 

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

### <a name="clients-dont-automatically-update"></a><a name="ki_sqlncli"></a>Klienterna uppdateras inte automatiskt
<!--518760-->
När du uppdaterar till version 1806,2 uppdaterar platsen även SQL Native Client, vilket kan orsaka en väntande omstart på plats servern. Den här fördröjningen medför att vissa filer inte uppdateras, vilket påverkar automatisk klient uppgradering.

#### <a name="workarounds"></a>Provisoriska lösningar
Undvik det här problemet genom att uppgradera SQL Native Client manuellt *innan du uppdaterar* Configuration Manager till version 1806,2. Mer information finns i den [senaste service uppdateringen för SQL Server 2012 Native Client](https://www.microsoft.com/download/details.aspx?id=50402).

Om du redan har uppdaterat platsen fungerar inte automatisk klient uppgradering och klient-push. Du måste uppdatera klienter för att testa de flesta nya funktionerna fullständigt. Uppdatera dina Technical Preview-klienter manuellt med följande process:  

1. Leta reda på källfilerna för klienten i mappen **CMUClient** i installations katalogen för Configuration Manager på plats servern. Till exempel, `C:\Program Files\Configuration Manager\CMUClient`  

2. Kopiera hela CMUClient-mappen till klient enheten. Till exempel, `C:\Temp\CMUClient`  

    Den här platsen kan vara en nätverks resurs som är tillgänglig från klienterna.  

3. Kör följande kommando rad från en upphöjd kommando tolk:`C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Om du installerar en ny klient i den tekniska för hands version 1806,2-platsen använder du samma process. 

> [!Important]  
> Använd inte `/MP` kommando rads parametern i det här scenariot. Den här parametern prioriteras `/source` och gör att CCMSetup laddar ned klient innehåll från hanterings platsen eller distributions platsen.
> 
> Kommando rads egenskaper, till exempel SMSSITECODE eller CCMLOGLEVEL, är OK att använda, men bör inte vara nödvändiga när du uppgraderar en befintlig klient. 


### <a name="version-18062-shows-version-1806-in-about-configuration-manager"></a><a name="ki_version"></a>Version 1806,2 visar version 1806 i om Configuration Manager
<!--518148-->
När du har uppgraderat till Technical Preview version 1806,2, om du öppnar fönstret **om Configuration Manager** från det övre vänstra hörnet i konsolen, visas fortfarande **version 1806**. 

#### <a name="workaround"></a>Lösning
Använd egenskapen **plats version** för att fastställa skillnaden mellan 1806 och 1806,2:

| Plats version  | Version
|---------|---------|
| 5,0.**8672**. 1000 | 1806 |
| 5,0.**8685**. 1000 | 1806,2 |
 


</br>

**Följande är nya funktioner som du kan prova med den här versionen.**  


## <a name="improvements-to-phased-deployments"></a><a name="bkmk_pod"></a>Förbättringar i stegvisa distributioner

I den här versionen ingår följande förbättringar i stegvisa [distributioner](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md):
- [Status för stegvis distribution](#bkmk_pod-monitor)
- [Stegvis distribution av program](#bkmk_pod-app)
- [Gradvis distribution under stegvis distribution](#bkmk_pod-throttle)


### <a name="phased-deployment-status"></a><a name="bkmk_pod-monitor"></a>Status för stegvis distribution
<!--1358577-->
Stegvisa distributioner har nu en inbyggd övervaknings upplevelse. Välj en stegvis distribution i noden **distributioner** på arbets ytan **övervakning** och klicka sedan på status för stegvis **distribution** i menyfliksområdet.

![Status instrument panel för stegvis distribution visar status för två faser](media/1358577-phased-deployment-status.png)

Den här instrument panelen visar följande information för varje fas i distributionen:  

- **Totalt antal enheter**: hur många enheter som är riktade till den här fasen.  

- **Status**: aktuell status för den här fasen. Varje fas kan vara i något av följande tillstånd:  

    - **Distributionen har skapats**: den stegvisa distributionen skapade en distribution av program varan till samlingen för den här fasen. Klienterna är aktivt riktade mot den här program varan.  

    - **Väntar**: den föregående fasen har ännu inte nått kraven för lyckad distribution för att fortsätta till den här fasen.  

    - **Pausad**: en administratör pausade distributionen.  

- **Förlopp**: de färgkodade distributions tillstånden från klienter. Till exempel: lyckades, pågår, fel, kraven är inte uppfyllda och okänd. 


#### <a name="known-issue"></a>Kända problem
Instrument panelen för stegvis distributions status kan visa flera rader för samma fas.<!--518510-->


### <a name="phased-deployment-of-applications"></a><a name="bkmk_pod-app"></a>Stegvis distribution av program
<!--1358147-->
Skapa stegvisa distributioner för program. Med stegvisa distributioner kan du dirigera en samordnad, sekvenserad distribution av program vara utifrån anpassningsbara kriterier och grupper.

Gå till **program biblioteket**i Configuration Manager-konsolen, expandera **program hantering**och välj **program**. Välj ett program och klicka sedan på **skapa stegvis distribution** i menyfliksområdet. 

Beteendet för en stegvis distribution av program är detsamma som för aktivitetssekvenser. Mer information finns i skapa stegvisa [distributioner för en aktivitetssekvens](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

#### <a name="prerequisite"></a>Krav
Distribuera innehållet för programmet till en distributions plats innan du skapar fasen för stegvis distribution.<!--518293-->

#### <a name="known-issue"></a>Kända problem
Du kan inte skapa faser för ett program manuellt. Guiden skapar automatiskt två faser för program distributioner.


### <a name="gradual-rollout-during-phased-deployments"></a><a name="bkmk_pod-throttle"></a>Gradvis distribution under stegvis distribution
<!--1358578-->
Under en stegvis distribution kan distributionen i varje fas nu ske gradvis. Det här beteendet minskar risken för distributions problem och minskar belastningen på nätverket som orsakas av distribution av innehåll till klienter. Platsen kan gradvis göra program varan tillgänglig beroende på konfigurationen för varje fas. Varje klient i en fas har en tids gräns i förhållande till den tid då program varan görs tillgänglig. Tidsfönstret mellan den tillgängliga tiden och tids gränsen är samma för alla klienter i en fas. 

När du skapar en stegvis distribution och konfigurerar en fas manuellt, på sidan **fas inställningar** i guiden Lägg till fas, eller på sidan **Inställningar** i guiden skapa stegvis distribution, konfigurerar du alternativet: **progressivt göra den här program varan tillgänglig under den här tids perioden (i dagar)**. Standardvärdet för den här inställningen är **0**, så som standard är distributionen inte begränsad.

> [!Note]  
> Det här alternativet är för närvarande endast tillgängligt för stegvisa distributioner av aktivitetssekvenser.  



## <a name="support-for-new-windows-app-package-formats"></a><a name="bkmk_msix"></a>Stöd för nya paket format för Windows-appar
<!--1357427-->
Configuration Manager stöder nu distribution av nya Windows 10-appaket (. msix) och app-paket (. msixbundle). Den senaste versionen av [Windows Insider Preview](https://insider.windows.com/) stöder för närvarande dessa nya format.

En översikt över MSIX finns i [en närmare titt på MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).

Information om hur du skapar en ny MSIX-app finns [i stöd för MSIX som introducerades i Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).

### <a name="prerequisites"></a>Krav
- En Windows 10-klient som kör minst Windows Insider Preview version 17682
- Ett Windows-appaket i MSIX-format

### <a name="try-it-out"></a>prova!
Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

1. [Skapa ett program](../../apps/deploy-use/create-applications.md)i Configuration Manager-konsolen. 
2. Välj programinstallations fil **typ** som **Windows-appaket (\*. appx, \*. appxbundle, \*. msix, \*. msixbundle)**.
3. [Distribuera programmet](../../apps/deploy-use/deploy-applications.md) till klienten som kör den senaste versionen av Windows Insider Preview.



## <a name="improvement-to-client-push-security"></a><a name="bkmk_client-push"></a>Förbättra push-säkerhet för klienter
<!--1358204-->
När [klientens push](../clients/deploy/plan/client-installation-methods.md#client-push-installation) -metod används för att installera Configuration Manager-klienten, skapar plats servern en fjärr anslutning till klienten för att starta installationen. Från och med den här versionen kan platsen kräva ömsesidig Kerberos-autentisering genom att inte tillåta återställning till NTLM innan anslutningen upprättas. Den här förbättringen hjälper till att skydda kommunikationen mellan servern och klienten. 

Beroende på dina säkerhets principer kanske din miljö redan föredrar eller kräver Kerberos över äldre NTLM-autentisering. Mer information om säkerhets överväganden för dessa autentiseringsprotokoll finns i [säkerhets princip inställningen i Windows för att begränsa NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).


### <a name="prerequisite"></a>Krav

Om du vill använda den här funktionen måste klienterna vara i en betrodd Active Directory skog. Kerberos i Windows förlitar sig på Active Directory för ömsesidig autentisering. 


### <a name="try-it-out"></a>prova!

Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

När du uppgraderar platsen kvarstår det befintliga beteendet. När du har *öppnat* egenskaperna för push-installation av klienter aktiverar platsen automatiskt Kerberos-kontrollen. Om det behövs kan du tillåta att anslutningen återgår till att använda en mindre säker NTLM-anslutning, vilket inte rekommenderas. 

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj **platser**. Välj mål platsen. I menyfliksområdet klickar du på **Inställningar för klient installation** och väljer **push-installation av klient**.  

2. Platsen har nu aktiverat Kerberos-kontrollen för klient-push. Stäng fönstret genom att klicka på **OK**.  

3. Om det behövs för din miljö går du till Fönstret Egenskaper för push-installation av klienten, på fliken **Allmänt** , se alternativet för att **tillåta ANSLUTNINGS återställning till NTLM**. Det här alternativet är inaktiverat som standard. 



## <a name="management-insights-for-proactive-maintenance"></a><a name="bkmk_insights"></a>Hanterings insikter för proaktiv underhåll
<!--1352184,et al-->
Ytterligare hanterings insikter finns i den här versionen för att markera potentiella konfigurations problem. Granska följande regler i den nya **proaktiva underhålls** gruppen:  

- **Oanvända konfigurations objekt**: konfigurations objekt som inte ingår i en konfigurations bas linje och som är äldre än 30 dagar.  

- **Oanvända start avbildningar**: Start avbildningar som inte refereras till PXE-start eller aktivitetssekvens används.  

- **Gränser grupper utan tilldelade plats system**: utan tilldelade plats system kan gränser grupper bara användas för platstilldelning.  

- **Gränser grupper utan medlemmar**: gränser grupper gäller inte för platstilldelning eller innehålls sökning om de inte har några medlemmar.  

- **Distributions platser som inte betjänar innehåll till klienter**: distributions platser som inte har betjänat innehåll till klienter under de senaste 30 dagarna. Dessa data baseras på rapporter från klienter från sina nedladdnings historik.  

- **Utgångna uppdateringar hittades**: utgångna uppdateringar gäller inte för distribution.   



## <a name="transition-mobile-apps-workload-for-co-managed-devices"></a><a name="bkmk_comgmt"></a>Över gången till arbets belastning för mobila appar för samhanterade enheter
<!--1357892-->
Hantera mobilappar med Microsoft Intune samtidigt som du fortsätter att använda Configuration Manager för att distribuera Windows-skrivbordet. Om du vill överföra arbets belastningen för moderna appar går du till sidan Egenskaper för samhantering. Flytta skjutreglaget från Configuration Manager till pilot eller alla. 

När du har övergått till den här arbets belastningen är alla tillgängliga appar som distribueras från Intune tillgängliga i Företagsportal. Appar som du distribuerar från Configuration Manager är tillgängliga i Software Center. 

Mer information finns i följande artiklar:  

- [Samhantering för Windows 10-enheter](../../comanage/overview.md)  

- [Vad är apphantering i Microsoft Intune?](https://docs.microsoft.com/intune/app-management)  



## <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a>Alternativ för gränser-grupp för peer-nedladdningar
<!--1356193-->
Gränser grupper innehåller nu ytterligare inställningar för att ge dig mer kontroll över innehålls distribution i din miljö. Den här versionen lägger till följande alternativ:  

- **Tillåt nedladdning av peer-datorer i den här begränsnings gruppen**: den här inställningen är aktive rad som standard. Hanterings platsen ger klienterna en lista över innehålls platser som innehåller peer-källor. <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    Det finns två vanliga scenarier där du bör inaktivera det här alternativet:  

    - Om du har en gräns grupp som innehåller gränser från geografiskt spridda platser, till exempel en VPN. Två klienter kan finnas i samma avgränsnings grupp eftersom de är anslutna via VPN, men i stora olika platser som inte är olämpliga för peer-delning av innehåll.  

    - Om du använder en enda, stor begränsar grupp för platstilldelning som inte refererar till några distributions platser.  

- **Använd endast peer-datorer i samma undernät vid peer-hämtning**: den här inställningen är beroende av den ovan. Om du aktiverar det här alternativet innehåller hanterings platsen bara den innehålls plats i listan med peer-källor som finns i samma undernät som klienten.

    Vanliga scenarier för att aktivera det här alternativet:

    - Din gränser grupp design för innehålls distribution innehåller en stor avgränsnings grupp som överlappar andra mindre gränser grupper. Med den här nya inställningen innehåller listan över innehålls källor som hanterings platsen tillhandahåller klienter endast peer-källor från samma undernät.

    - Du har en enda stor avgränsnings grupp för alla fjärranslutna kontor. Aktivera det här alternativet och klienter delar bara innehåll inom under nätet på den fjärranslutna arbets platsen, i stället för att dela innehåll mellan platser.


### <a name="known-issue"></a>Kända problem
Om peer-källans klient har fler än en IP-adress (IPv4, IPv6 eller båda) fungerar inte peer-cachelagring. Det nya alternativet, **under peer-nedladdning, använder bara peer-datorer i samma undernät**, utan någon påverkan om peer-källan har fler än en IP-adress.<!--518661-->   



## <a name="third-party-software-updates-support-for-custom-catalogs"></a><a name="bkmk_3pupdate"></a>Stöd för program uppdateringar från tredje part för anpassade kataloger
<!--1358714-->
Den här versionen itererar ytterligare om support för program uppdateringar från tredje part på grund av din [feedback från UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). [Teknisk för hands version 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate) tillhandahöll support för *partner kataloger*, som är registrerade kataloger från program varu leverantörer. Kataloger som du anger, som inte är registrerade hos Microsoft, kallas *anpassade kataloger*. Lägg till anpassade kataloger i Configuration Manager-konsolen.  


### <a name="prerequisites"></a>Krav 

- Konfigurera [program uppdateringar från tredje part](capabilities-in-technical-preview-1806.md#bkmk-3pupdate). Slutför fas 1: Aktivera och konfigurera funktionen.   

- En digitalt signerad, anpassad katalog som innehåller digitalt signerade program uppdateringar.  

- Administratören kräver följande behörigheter:  

    - Webbplats: skapa, ändra  


### <a name="try-it-out"></a>prova!

Försök att slutföra uppgifterna. Skicka sedan [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) för att berätta hur det fungerade.

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **program uppdateringar**och väljer noden **program uppdaterings kataloger från tredje part** . Klicka på **Lägg till anpassad katalog** i menyfliksområdet.  

2. På sidan **Allmänt** anger du följande information:  

    - **Nedladdnings-URL**: en giltig HTTPS-adress för den anpassade katalogen.  

    - **Utgivare**: namnet på den organisation som publicerar katalogen.  

    - **Namn**: namnet på den katalog som ska visas i Configuration Manager-konsolen.  

    - **Beskrivning**: en beskrivning av katalogen.  

    - **Support-URL** (valfritt): en giltig HTTPS-adress till en webbplats för att få hjälp med katalogen.  

    - **Support kontakt** (valfritt): kontakt information för att få hjälp med katalogen.  

3. Slutför guiden. Guiden lägger till den nya katalogen i ett tillstånd med avbrutna prenumerationer.  

4. Prenumerera på den anpassade katalogen med hjälp av den befintliga åtgärden **Prenumerera på katalog** . Mer information finns i [fas 2: prenumerera på en katalog och synkronisera uppdateringar från tredje part](capabilities-in-technical-preview-1806.md#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates).  

> [!Note]  
> Du kan inte lägga till kataloger med samma nedladdnings-URL och du kan inte redigera katalog egenskaper. Om du anger felaktiga egenskaper för en anpassad katalog tar du bort katalogen innan du lägger till den igen.  


#### <a name="unsubscribe-from-a-catalog"></a>Avbryta prenumerationen från en katalog
Om du vill avbryta prenumerationen på en katalog väljer du önskad katalog i listan och klickar på **Avsluta prenumerations katalog** i menyfliksområdet. Om du avbryter prenumerationen på en katalog inträffar följande åtgärder och beteenden: 
- Platsen stoppar synkroniseringen av nya uppdateringar 
- Platsen blockerar de associerade certifikaten för katalog signering och uppdaterings innehåll. 
- Befintliga uppdateringar tas inte bort, men du kanske inte kan publicera eller distribuera dem.

#### <a name="delete-a-custom-catalog"></a>Ta bort en anpassad katalog
Ta bort anpassade kataloger från samma nod i konsolen. Välj en anpassad katalog i ett tillstånd utan *prenumeration* och klicka på **ta bort anpassad katalog**. Om du redan prenumererar på katalogen måste du först avbryta prenumerationen innan du tar bort den. Du kan inte ta bort partner kataloger. Om du tar bort en anpassad katalog tas den bort från listan över kataloger. Den här åtgärden påverkar inte några program uppdateringar som du har publicerat till program uppdaterings platsen.


### <a name="known-issue"></a>Kända problem
Borttagnings åtgärden för anpassade kataloger är nedtonad och du kan därför inte ta bort anpassade kataloger från-konsolen. Du kan lösa problemet genom att använda **WBEMTest** -verktyget på plats servern. Fråga efter den instans som du vill ta bort med namnet eller hämtnings-URL: en `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"`, till exempel:. I fönstret frågeresultat markerar du objektet och klickar på **ta bort**.<!--518676-->  



## <a name="improvements-to-cloud-management-features"></a><a name="bkmk_cloud"></a>Förbättringar av moln hanterings funktioner

Den här versionen innehåller följande förbättringar:  

- Följande funktioner har nu stöd för användning av Azures Azures amerikanska myndigheter:<!--511980-->  

    - Publicera webbplatsen för **moln hantering** via Azure- [tjänster](../servers/deploy/configure/azure-services-wizard.md)  

    - Distribuera en [Cloud Management Gateway med Azure Resource Manager](../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)  

    - Distribuera en [moln distributions plats med Azure Resource Manager](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  

- Kunder använder Windows autopilot för att etablera Windows 10 på Azure Active Directory anslutna enheter som är anslutna till det lokala nätverket. För att installera eller uppgradera Configuration Manager-klienten på dessa enheter behöver du inte en distributions plats för moln eller en lokal distributions plats som kon figurer ATS för att **tillåta klienter att ansluta anonymt**. Aktivera i stället alternativet plats för att **använda Configuration Manager-genererade certifikat för http-platssystem**, vilket gör att en molnbaserad klient som är ansluten till en klient kan kommunicera med en lokal http-aktiverad distributions plats. Mer information finns i [förbättrad säker klient kommunikation](https://docs.microsoft.com/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).<!--515854-->  



## <a name="new-software-updates-compliance-report"></a><a name="bkmk_report"></a>Ny Kompatibilitetsrapport för program uppdateringar
<!--1357775-->
Att visa rapporter om kompatibilitet med program uppdateringar innehåller traditionellt sett data från klienter som inte nyligen har kontaktat platsen. Med en ny rapport kan du filtrera kompabilitets resultat för en bestämd program uppdaterings grupp med "friska" klienter. Den här rapporten visar det mer realistiska kompatibilitetstillstånd för aktiva klienter i din miljö. 
 
Om du vill visa rapporten går du till arbets ytan **övervakning** , expanderar **rapportering**, expanderar **rapporter**, expanderar **program uppdateringar – ett krav**och väljer **efterlevnad 9 – övergripande hälso tillstånd och efterlevnad**. Ange **uppdaterings grupp**, **samlings namn**och **klient hälso** tillstånd.

Rapporten innehåller följande delar:
- **Felfria klienter jämfört med totalt antal klienter**: det här stapeldiagrammet jämför de "friska" klienter som har kommunicerat med platsen under den angivna tids perioden mot det totala antalet klienter i den angivna samlingen.
- **Översikt över efterlevnad**: det här cirkel diagrammet visar det övergripande kompatibilitetstillstånd för den specifika program uppdaterings gruppen på aktiva klienter i den angivna samlingen.
- **5 främsta icke-kompatibla enligt artikel-ID**: det här stapeldiagrammet visar de fem främsta program varu uppdateringarna i den angivna gruppen som inte är kompatibla med aktiva klienter i den angivna samlingen.
- Längst ned i rapporten finns en tabell med ytterligare information som visar program uppdateringar i den angivna gruppen.



## <a name="next-steps"></a>Nästa steg
Information om hur du installerar eller uppdaterar den tekniska för hands versionen finns i [teknisk för hands version för Configuration Manager](technical-preview.md).    
