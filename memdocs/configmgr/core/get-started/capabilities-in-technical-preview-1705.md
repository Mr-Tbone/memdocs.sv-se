---
title: Teknisk för hands version 1705
titleSuffix: Configuration Manager
description: Lär dig mer om de funktioner som finns i teknisk för hands version 1705 för Configuration Manager.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d4594a50f42d6b8e6ea0b88b83920eda11615815
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88591010"
---
# <a name="capabilities-in-technical-preview-1705-for-configuration-manager"></a>Funktioner i Technical Preview 1705 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1705. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. Innan du installerar den här versionen av Technical Preview kan du läsa [Technical Preview för Configuration Manager](../../core/get-started/technical-preview.md) för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.    

**Kända problem i den här tekniska för hands versionen:**
-   **Operations Manager Suite-anslutningsprogrammet uppgraderas inte**. När du uppgraderar från en tidigare version av den tekniska för hands versionen som hade OMS-kopplingen konfigurerad, uppgraderas inte kopplingen och är inte längre tillgänglig i-konsolen. Efter uppgraderingen måste du [använda guiden Azure-tjänster](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) och återupprätta anslutningen till din OMS-arbetsyta.
-   Det **gick inte att synkronisera Surface-drivrutinerna**. Även om stöd för Surface-drivrutiner visas i **Nyheter** i Configuration Manager-konsolen för den tekniska för hands versionen, fungerar inte den här funktionen ännu som förväntat.
-   **Det gick inte att skapa Windows Update för principer för avstängning av företag**. Även om möjligheten att konfigurera Windows Update för principer för förskjutande av företag visas i **vad som är nytt** i Configuration Manager-konsolen för den tekniska för hands versionen, öppnas inte guiden och du kan inte konfigurera några principer.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Följande är nya funktioner som du kan prova med den här versionen.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Uppdateringsverktyg för återställning  
Du kan använda verktyget Configuration Manager uppdaterings återställning, **CMUpdateReset.exe**för att åtgärda problem när uppdateringar i konsolen har problem med att hämta eller replikera. Det här verktyget ingår i teknisk för hands version 1705. Du hittar den på plats servern för den tekniska för hands versionen när du har installerat förhands granskningen i mappen ***\CD.latest\SMSSETUP\TOOLS*** .

Du kan använda det här verktyget med teknisk för hands version 1606 eller senare. Detta stöd för bakåtkompatibilitet har angetts så att verktyget kan användas med en rad tekniska för hands versions uppdaterings scenarier och utan att behöva vänta tills nästa tekniska för hands version blir tillgänglig.

Du kan använda det här verktyget när en uppdatering i konsolen ännu inte har installerats och är i ett felaktigt tillstånd. Ett felaktigt tillstånd kan innebära att uppdaterings nedladdningen fortfarande pågår, men att den fastnar och tar lång tid, kanske timmar som är längre än dina historiska förväntningar för uppdaterings paket av liknande storlek. Det kan också vara ett haveri att replikera uppdateringen till underordnade primära platser.  

När du kör verktyget körs det mot den uppdatering som du anger. Som standard tar verktyget inte bort installerade eller nedladdade uppdateringar.  

### <a name="prerequisites"></a>Förutsättningar
Det konto som du använder för att köra verktyget kräver följande behörigheter:
-   **Läs** -och **Skriv** behörighet till plats databasen för den centrala administrations platsen och varje primär plats i hierarkin. Om du vill ange dessa behörigheter kan du lägga till användar kontot som medlem i **db_datawriter** och **db_datareader** [fasta databas roller](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) i Configuration Manager databasen för varje plats. Verktyget samverkar inte med sekundära platser.
-   **Lokal administratör** på platsen på den översta nivån i hierarkin.
-   **Lokal administratör** på den dator som är värd för tjänst anslutnings punkten.

Du behöver GUID för det uppdaterings paket som du vill återställa. Hämta GUID:
-   Gå till **Administration**  >  **uppdateringar och underhåll** i-konsolen och högerklicka på rubriken för en av kolumnerna (t. ex. **tillstånd**) i visningsfönstret och välj **paket-GUID**. Detta lägger till kolumnen i visningen, och kolumnen visar GUID för uppdaterings paketet.

> [!TIP]  
> Om du vill kopiera GUID väljer du raden för det uppdaterings paket som du vill återställa och använder sedan CTRL + C för att kopiera raden. Om du klistrar in det kopierade valet i en text redigerare kan du sedan kopiera bara GUID för användning som en kommando rads parameter när du kör verktyget.

### <a name="run-the-tool"></a>Kör verktyget    
Verktyget måste köras på platsen på den översta nivån i hierarkin.

När du kör verktyget använder du kommando rads parametrar för att ange SQL Server på platsen på den översta nivån i hierarkin, plats databasens namn och GUID för det uppdaterings paket som du vill återställa. Verktyget identifierar sedan de ytterligare servrar som krävs för åtkomst baserat på status för uppdateringar.   

Om uppdaterings paketet är i ett *post hämtnings* tillstånd rensar verktyget inte paketet. Som ett alternativ kan du framtvinga borttagningen av en uppdatering som har hämtats genom att använda parametern framtvinga borttagning (se kommando rads parametrar senare i det här avsnittet).

När verktyget har körts:
-   Om ett paket har tagits bort startar du om SMS_Executive tjänsten på den översta nivån och söker efter uppdateringar för att ladda ned paketet igen.
-   Om ett paket inte har tagits bort, behöver du inte vidta några åtgärder när uppdateringen initieras på nytt och startar om replikering eller installation.

**Kommando rads parametrar:**  


|                        Parameter                         |                                                            Beskrivning                                                            |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **-S &lt; FQDN för SQL Server på platsen på den översta nivån>** | *Obligatoriskt* <br> Du måste ange det fullständiga domän namnet för den SQL Server som är värd för plats databasen för platsen på den översta nivån i hierarkin. |
|                **-D &lt; databas namn>**                 |                             *Obligatoriskt* <br> Du måste ange namnet på den översta nivån på plats databasen.                             |
|                 **-P &lt; paket-GUID>**                 |                        *Obligatoriskt* <br> Du måste ange GUID för det uppdaterings paket som du vill återställa.                        |
|           **-I &lt; SQL Server instans namn>**           |                   *Valfritt* <br> Använd detta för att identifiera den instans av SQL Server som är värd för plats databasen.                   |
|                       **-FDELETE**                       |                      *Valfritt* <br> Använd detta för att framtvinga borttagning av ett uppdaterings paket som har hämtats.                      |

 **Exempel:**  
 I ett typiskt scenario vill du återställa en uppdatering som har hämtnings problem. Dina SQL Server-FQDN är *server1.fabrikam.com*, plats databasen är *CM_XYZ*och paketets GUID är *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Du kör: ***CMUpdateReset.exe-S server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 I ett mer extrema scenario vill du framtvinga borttagning av problem med uppdaterings paketet. Dina SQL Server-FQDN är *server1.fabrikam.com*, plats databasen är *CM_XYZ*och paketets GUID är *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Du kör: ***CMUpdateReset.exe-FDELETE-S server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### <a name="test-the-tool-with-the-technical-preview"></a>Testa verktyget med teknisk för hands version  
Du kan använda det här verktyget med teknisk för hands version 1606 eller senare. Detta finns i så fall att du kan använda verktyget med ett större antal uppdaterings scenarier för tekniska för hands versioner, utan att behöva vänta tills nästa tekniska för hands version är tillgänglig.

Kör verktyget på ett uppdaterings paket för en teknisk för hands version innan uppdateringen uppfyller krav kontrollen. Ett slutfört krav kontroll tillstånd identifieras av en av följande status för paketet i **administrations**  >  **uppdateringar och underhåll**:  
-   **Krav kontroll godkändes**
-   **Krav kontroll godkändes med varning**
-   **Krav kontrollen misslyckades**


## <a name="high-dpi-console-support"></a>Stöd för hög DPI-konsol

I den här versionen, problem med hur Configuration Manager-konsolen skalar och visar olika delar av användar gränssnittet när de visas på hög DPI-enheter (t. ex. en Surface Book) bör åtgärdas.


## <a name="peer-cache-improvements"></a>Förbättringar i peer-cache
Från och med den här tekniska för hands versionen använder peer-cache [inte längre nätverks åtkomst kontot](../plan-design/hierarchy/client-peer-cache.md) för att autentisera nedladdnings begär Anden från peer-datorer.


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>Förbättringar för SQL Server Always on-tillgänglighetsgrupper  
Med den här versionen kan du nu använda asynkrona inchecknings repliker i SQL Server Always on-tillgänglighetsgrupper som du använder med Configuration Manager.  Det innebär att du kan lägga till fler repliker i dina tillgänglighets grupper som du kan använda som fjärranslutna platser och sedan använda dem i ett katastrof återställnings scenario.  

- Configuration Manager stöder användningen av den asynkrona commit-replikeringen för att återställa din synkrona replik.  Se [återställnings alternativ för plats databas](../servers/manage/recover-sites.md#site-database-recovery-options) i avsnittet säkerhets kopiering och återställning för information om hur du kan göra detta.

- Den här versionen stöder inte redundans för att använda den asynkrona commit-repliken som plats databas.
  > [!CAUTION]  
  > Eftersom Configuration Manager inte validerar statusen för den asynkrona commit-replikeringen för att bekräfta att den är aktuell, och [genom att utforma en sådan replik kan vara osynkroniserade](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-2014#AvailabilityModes), använder en asynkron replik som plats databas och skyddar din webbplats och data på risk.  

- Du kan använda samma antal och typ av repliker i en tillgänglighets grupp som stöds av den version av SQL Server som du använder.   (Tidigare stöd var begränsat till två synkrona commit-repliker.)

### <a name="configure-an-asynchronous-commit-replica"></a>Konfigurera en asynkron commit-replik
Om du vill lägga till en asynkron replik i en [tillgänglighets grupp som du använder med Configuration Manager](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)behöver du inte köra de konfigurations skript som krävs för att konfigurera en synkron replik. (Detta beror på att det inte finns stöd för att använda den asynkrona repliken som plats databasen.) Mer information finns i [lägga till en sekundär replik i en tillgänglighets grupp](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server?view=sql-server-2014).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Använd den asynkrona repliken för att återställa din webbplats
Innan du använder en asynkron replik för att återställa plats databasen måste du stoppa den aktiva primära platsen för att förhindra ytterligare skrivningar till plats databasen. När du har stoppat platsen kan du använda en asynkron replik i stället för att använda en [manuellt återställd databas](../servers/manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).

För att stoppa-platsen kan du använda [verktyget underhåll av hierarki](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md) för att stoppa viktiga tjänster på plats servern. Använd kommando raden: **Preinst.exe/STOPSITE**   

Att stoppa-platsen är detsamma som att stoppa Platskomponenthanteraren tjänsten (sitecomp) följt av SMS_Executive-tjänsten på plats servern.


## <a name="improved-user-notifications-for-office-365-updates"></a>Förbättrade användar meddelanden för Office 365-uppdateringar
Förbättringar har gjorts för att använda Office Klicka-och-kör-funktionen när en klient installerar en Office 365-uppdatering. Detta inkluderar popup-meddelanden och meddelanden i appen och en nedräknings upplevelse. Före den här versionen stängdes Office-program som var öppna automatiskt utan varning när en Office 365-uppdatering skickades till en klient. Efter den här uppdateringen kommer Office-program inte längre att avslutas utan förvarning.

### <a name="prerequisites"></a>Förutsättningar
Den här uppdateringen gäller för Office 365 ProPlus-klienter.

### <a name="known-issues"></a>Kända problem
När en klient utvärderar en uppdaterings tilldelning för Office 365 för första gången och uppdateringen har en tids gräns som har schemalagts tidigare, schemalagts omedelbart eller schemalagt inom 30 minuter, kan Office 365-användar upplevelsen vara inkonsekvent. Klienten kan till exempel få en uppräknings dialog ruta för 30 minuter för uppdateringen, men den faktiska tvångs inläsningen kan starta innan nedräkningen slutfördes. Undvik det här problemet genom att tänka på följande:
- Distribuera Office 365-uppdateringen med en tids gräns som har schemalagts för mer än 60 minuter före den aktuella tiden.
- Konfigurera en underhålls period under icke-kontors tid för samlingen eller konfigurera en tvingande respitperiod för distributionen.

### <a name="try-it-out"></a>prova!
Försök att utföra följande uppgifter och skicka sedan oss **feedback** från fliken **Start** i menyfliksområdet så att vi kan se hur det fungerade:
- Distribuera till en klient en Office 365-uppdatering med en tids gräns angiven till en tid minst 60 minuter före den aktuella tiden. Observera det nya beteendet på klienten.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Konfigurera och distribuera Windows Defender Application Guard-principer

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) är en ny Windows-funktion som hjälper dig att skydda dina användare genom att öppna obetrodda webbplatser i en säker isolerad behållare som inte är tillgänglig för andra delar av operativ systemet. I den här tekniska för hands versionen har vi lagt till stöd för att konfigurera den här funktionen med Configuration Manager kompatibilitetsinställningar som du konfigurerar och sedan distribuera till en samling.
Den här funktionen kommer att publiceras i för hands versionen för 64-bitars versionen av Windows 10 Creators uppdatering. Om du vill testa den här funktionen nu måste du använda en för hands version av den här uppdateringen.


### <a name="before-you-start"></a>Innan du börjar

För att kunna skapa och distribuera Windows Defender Application Guard-principer måste de Windows 10-enheter som du distribuerar principen till konfigureras med en princip för nätverks isolering. Mer information finns i blogg inlägget som refereras senare.
Den här funktionen fungerar bara med de senaste Windows 10 Insider-versionerna. För att testa det måste dina klienter köra en ny Windows 10 Insider-version.

### <a name="try-it-out"></a>prova!

Se till att du har läst blogg inlägget för att förstå grunderna om Windows Defender Application Guard.

Så här skapar du en princip och bläddrar bland de tillgängliga inställningarna:

1.  I Configuration Manager-konsolen väljer du **till gångar och efterlevnad**.
2.  I arbets ytan **till gångar och efterlevnad** väljer du **Översikt**  >  **Endpoint Protection**  >  **Windows Defender Application Guard**.
3.  På fliken **Start** går du till gruppen **skapa** och klickar på **skapa Windows Defender Application Guard-princip**.
4.  Med blogg inlägget som referens kan du bläddra bland och konfigurera de tillgängliga inställningarna för att testa funktionen.
5.  När du är klar slutför du guiden och distribuerar principen till en eller flera Windows 10-enheter.

### <a name="further-reading"></a>Ytterligare läsning

Läs mer om Windows Defender Application Guard i [det här blogg inlägget]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97).
Mer information om fristående läge för Windows Defender Application Guard finns i [det här blogg inlägget](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Nya funktioner för Azure AD och moln hantering

I den här versionen kan du konfigurera moln tjänster för att använda Azure AD för att stödja följande scenario:

- Installera Configuration Manager-klienten manuellt från Internet och tilldela den till en Configuration Manager plats.
- Använd Intune för att distribuera Configuration Manager-klienten till enheter på Internet.

### <a name="advantages"></a>Fördelar

Att använda moln tjänster och Azure AD tar bort behovet av att använda certifikat för klientautentisering.

Du kan identifiera Azure AD-användare på din webbplats som ska användas i samlingar och andra Configuration Manager åtgärder.

### <a name="before-you-start"></a>Innan du börjar

- Du måste ha en Azure AD-klient.
- Enheterna måste köra Windows 10 och vara anslutna till Azure AD.  Klienter kan också vara domänanslutna tillsammans med Azure AD-anslutna).
- Förutom de [befintliga kraven](../plan-design/configs/site-and-site-system-prerequisites.md) för hanterings platsens plats system roll måste du dessutom se till att **ASP.NET 4,5** (och andra alternativ som väljs automatiskt med detta) är aktiverade på den dator som är värd för plats system rollen.
- Så här använder du Microsoft Intune för att distribuera Configuration Manager-klienten:
    - Du måste ha en fungerande Intune-klient (Configuration Manager och Intune behöver inte vara anslutna).
    - I Intune har du skapat och distribuerat en app som innehåller Configuration Manager-klienten. Mer information om hur du gör detta finns i så här installerar du klienter till Intune MDM-hanterade Windows-enheter.
- Så här använder du Configuration Manager för att distribuera klienten:
    - Minst en hanterings plats måste konfigureras för HTTPS-läge.
    - Du måste konfigurera en Cloud Management Gateway.


### <a name="set-up-the-cloud-management-gateway"></a>Konfigurera Cloud Management Gateway

Konfigurera Cloud Management Gateway så att klienter får åtkomst till din Configuration Manager plats från Internet utan att använda certifikat.

Du hittar hjälp om hur du gör detta i följande avsnitt:

- [Planera för Cloud Management Gateway i Configuration Manager](../clients/manage/cmg/plan-cloud-management-gateway.md).
- [Konfigurera Cloud Management Gateway för Configuration Manager](../clients/manage/cmg/setup-cloud-management-gateway.md).
- [Övervaka Cloud Management Gateway i Configuration Manager](../clients/manage/cmg/monitor-clients-cloud-management-gateway.md).

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Konfigurera appen Azure-tjänster i Configuration Manager Cloud Services

Detta ansluter din Configuration Manager-plats till Azure AD och är en förutsättning för alla andra åtgärder i det här avsnittet. Gör så här:

1. I arbets ytan **Administration** i Configuration Manager-konsolen expanderar du **Cloud Services**och klickar sedan på **Azure-tjänster**.
2. På fliken **Start** går du till gruppen **Azure-tjänster** och klickar på **Konfigurera Azure-tjänster**.
3. På sidan **Azure-tjänster** i guiden Azure-tjänster väljer du **moln hantering** så att klienter kan autentiseras med hierarkin med hjälp av Azure AD.
4. På sidan **Allmänt** i guiden anger du ett namn och en beskrivning för din Azure-tjänst.
5. På sidan **app** i guiden väljer du din Azure-miljö i listan och klickar sedan på **Bläddra** för att välja de server-och klient program som ska användas för att konfigurera Azure-tjänsten:
   - I fönstret **Server App** väljer du den server-app som du vill använda och klickar sedan på **OK**. Server appar är Azure-webbappar som innehåller konfigurationerna för ditt Azure-konto, inklusive klient-ID, klient-ID och en hemlig nyckel för klienter. Om du inte har någon tillgänglig server-app använder du något av följande:
       - **Skapa**: om du vill skapa en ny server app klickar du på **skapa**. Ange ett eget namn för appen och klienten. När du sedan har loggat in på Azure skapar Configuration Manager webbappen i Azure åt dig, inklusive klient-ID och hemlig nyckel för användning med webbappen. Senare kan du visa dessa från Azure Portal.
       - **Importera**: Klicka på **Importera**om du vill använda en webbapp som redan finns i din Azure-prenumeration. Ange ett eget namn för appen och klienten och ange sedan klient-ID, klient-ID och den hemliga nyckeln för den Azure-webbapp som du vill Configuration Manager använda. När du har verifierat informationen klickar du på **OK** för att fortsätta. Det här alternativet är för närvarande inte tillgängligt i den här tekniska för hands versionen.
   - Upprepa samma process för klient programmet.

   Du måste ge behörigheten *läsa katalog data* program när du använder program import för att ange rätt behörigheter i portalen. Om du använder program skapande skapas behörigheterna automatiskt med programmet, men du måste fortfarande ge det ett medgivande till programmet i Azure Portal.
6. På sidan **identifiering** i guiden **aktiverar du Azure Active Directory identifiering av användare**och klickar sedan på **Inställningar**.
   Konfigurera ett schema för när identifiering sker i dialog rutan **Inställningar för identifiering av Azure AD-användare** . Du kan också aktivera delta identifiering som bara söker efter nya eller ändrade konton i Azure AD.
7. Slutför guiden.

Nu har du anslutit din Configuration Manager-plats till Azure AD.


### <a name="install-the-cm-client-from-the-internet"></a>Installera CM-klienten från Internet

Innan du börjar ska du kontrol lera att källfilerna för klient installationen lagras lokalt på den enhet som du vill installera klienten på.
Följ sedan anvisningarna i [Distribuera klienter till Windows-datorer](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual) med följande installations kommando rad (ersätt värdena i exemplet med dina egna värden):

**ccmsetup.exe/NoCrlCheck/Source: C:\CLIENT CCMHOSTNAME = SCCMPROXYCONTOSO. CLOUDAPP. NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode = HEC AADTENANTID = 780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME = contoso AADCLIENTAPPID = \<GUID> AADRESOURCEURI =<code>https://contososerver</code>**

- **/NoCrlCheck**: om hanterings platsen eller Cloud Management Gateway använder ett icke-offentligt Server certifikat, kanske klienten inte kan komma åt CRL-platsen.
- **/Source**: lokal mapp: platsen för klientens installationsfiler.
- **CCMHOSTNAME**: namnet på din Internet hanterings plats. Du kan hitta detta genom att köra **gwmi-namespace root\ccm\locationservices SMS_ActiveMPCandidate** från en kommando tolk på en hanterad klient.
- **SMSMP**: namnet på din uppslags hanterings plats – detta kan finnas på intranätet.
- **SMSSiteCode**: plats koden för din Configuration Manager webbplats.
- **AADTENANTID**, **AADTENANTNAME**: ID och namn för den Azure AD-klient som du länkade till Configuration Manager. Du hittar detta genom att köra dsregcmd.exe/status från en kommando tolk på en Azure AD-ansluten enhet.
- **AADCLIENTAPPID**: ID för Azure AD-klientens app. Information om hur du hittar detta finns i [använda portalen för att skapa ett Azure Active Directory program och tjänstens huvud namn som kan komma åt resurser](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).
- **AADResourceUri**: ID-URI för den inbyggda Azure AD server-appen.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>Använd guiden Azure-tjänster för att konfigurera en anslutning till OMS
Från och med 1705 Technical Preview-versionen använder du **guiden Azure-tjänster** för att konfigurera anslutningen från Configuration Manager till moln tjänsten för Operations Management Suite (OMS). Guiden ersätter tidigare arbets flöden för att konfigurera den här anslutningen.

-   Guiden används för att konfigurera moln tjänster för Configuration Manager, till exempel OMS, Windows Store för företag (WSfB) och Azure Active Directory (Azure AD).  

-   Configuration Manager ansluter till OMS för funktioner som Log Analytics eller Uppgraderingsberedskap.

### <a name="prerequisites-for-the-oms-connector"></a>Krav för OMS-kopplingen
Krav för att konfigurera en anslutning till OMS är oförändrad från de [som dokumenteras för Current Branch version 1702](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm). Informationen upprepas här:  

-   Ge Configuration Manager behörighet till OMS.

-   OMS-anslutningsprogrammet måste vara installerat på den dator som är värd för en [tjänst anslutnings punkt](../servers/deploy/configure/about-the-service-connection-point.md) i [onlineläge](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).

-   Du måste installera en Microsoft Monitoring Agent för OMS installerat på tjänst anslutnings punkten tillsammans med OMS-anslutningsprogrammet. Agenten och OMS-kopplingen måste konfigureras för att använda samma **OMS-arbetsyta**. Information om hur du installerar agenten finns i [Hämta och installera agenten](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) i OMS-dokumentationen.
-   När du har installerat anslutningen och agenten måste du konfigurera OMS för att använda Configuration Manager data. Det gör du genom att [importera Configuration Manager samlingar](/azure/log-analytics/log-analytics-sccm#import-collections)i OMS-portalen.

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Använd guiden Azure-tjänster för att konfigurera anslutningen till OMS

1.  I-konsolen går du till **administrations**  >  **Översikt**  >  **Cloud Services**  >  **Azure-tjänster**och väljer sedan **Konfigurera Azure-tjänster** på fliken **Start** i menyfliksområdet för att starta **guiden Azure-tjänster**.

2.  På sidan **Azure-tjänster** väljer du moln tjänsten operation Management Suite. Ange ett eget namn på **Azure-tjänstens namn** och en valfri beskrivning och klicka sedan på **Nästa**.

3.  På sidan **app** anger du din Azure-miljö (den tekniska för hands versionen stöder bara det offentliga molnet). Klicka sedan på **Bläddra** för att öppna fönstret Server App.

4.  Välj en webbapp:

    -   **Importera**: Klicka på **Importera**om du vill använda en webbapp som redan finns i din Azure-prenumeration. Ange ett eget namn för appen och klienten och ange sedan klient-ID, klient-ID och den hemliga nyckeln för den Azure-webbapp som du vill Configuration Manager använda. När du har **verifierat** informationen klickar du på **OK** för att fortsätta.   

    > [!NOTE]   
    > När du konfigurerar OMS med den här för hands versionen stöder OMS endast *import* funktionen för en webbapp. Det finns inte stöd för att skapa en ny webbapp. På samma sätt kan du inte återanvända en befintlig app för OMS.

5.  Om du har utfört alla andra procedurer visas informationen på skärmen **konfiguration av OMS-anslutning** automatiskt på den här sidan. Information för anslutnings inställningarna ska visas för din **Azure-prenumeration**, **Azure Resource-grupp**och **Operations Management Suite-arbetsyta**.

6.  Guiden ansluter till OMS-tjänsten med den information som du har angett. Välj de enhets samlingar som du vill synkronisera med OMS och klicka sedan på **Lägg till**.

7.  Verifiera anslutnings inställningarna på sidan **Sammanfattning** och välj sedan **Nästa**. På skärmen **förlopp** visas anslutnings status och bör sedan **slutföras**.

8.  När guiden har slutförts visar Configuration Manager-konsolen att du har konfigurerat **operation Management Suite** som en **moln tjänst typ**.
