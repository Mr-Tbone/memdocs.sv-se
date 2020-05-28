---
title: För hands version av Endpoint Analytics
titleSuffix: Configuration Manager
description: Instruktioner för för hands versionen av Endpoint Analytics.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: c7a99931db27b6a55c9e0722cc12c1d7a9cc9e80
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764245"
---
# <a name="endpoint-analytics-preview"></a><a name="bkmk_uea"></a>För hands version av Endpoint Analytics

> [!Note]  
> Den här informationen är relaterad till en förhands gransknings funktion som kan ändras avsevärt innan den släpps kommersiellt. Microsoft lämnar inga garantier, uttryckliga eller underförstådda, avseende informationen som visas här. 
>
> Mer information om ändringar i slut punkts analys finns i [Vad är nytt i slut punkts analys](whats-new-endpoint-analytics.md). 
>
>Om du vill ansluta till den privata för hands versionen av slut punkts analys anger du informationen [i det här formuläret](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR9-ZzmlTlbJMh03eDDHtO81UOERLUkMzNFZKSlBaNFNFUVhFSlE0MzNYMS4u). Klienterna kommer att användas som öppningar för för hands versionen.


## <a name="endpoint-analytics-overview"></a>Översikt över slut punkts analys

Det är inte ovanligt att slutanvändarna får långa start tider eller andra avbrott. Dessa avbrott kan bero på en kombination av:

- Äldre maskin vara
- Program varu konfigurationer som inte är optimerade för slut användar upplevelsen
- Problem som orsakas av konfigurations ändringar och uppdateringar

Dessa problem och andra problem med slut användar upplevelsen behålls eftersom det inte har stor insyn i slut användar upplevelsen. I allmänhet kommer den enda insynen i dessa problem att komma från en långsam dyr support kanal som vanligt vis inte ger tydlig information om vad som behöver optimeras. Det är inte bara IT-support som har stöd för kostnaderna för dessa problem. Tiden som de anställda ägnat åt att hantera problem är också kostsam. Prestanda-, Tillförlitlighets-och support problem som minskar användar produktiviteten kan också ha en stor inverkan på organisationens lägsta linje.

**Slut punkts analys** syftar till att förbättra användar produktiviteten och minska IT-Supportens kostnader genom att tillhandahålla insikter om användar upplevelsen. Insikterna gör det möjligt för IT att optimera slutanvändarens upplevelse med proaktiv support och att identifiera regressioner för användar upplevelsen genom att bedöma användar påverkan av konfigurations ändringar.

Den första versionen fokuserar på tre saker:

- [**Rekommenderad program vara**](#bkmk_uea_rs): rekommendationer för att ge den bästa användar upplevelsen
- [**Proaktivt reparations skript**](#bkmk_uea_prs): åtgärda vanliga support problem innan slutanvändare märker problem
- [**Starta prestanda**](#bkmk_uea_bp): hjälpa den att få användare från ström spar läge till produktivitet snabbt utan lång start och inloggnings fördröjning

Den här versionen är bara början. Vi kommer snart att lansera nya insikter om andra viktiga användar upplevelser efter den första versionen. Mer information om ändringar i slut punkts analys finns i [Vad är nytt i slut punkts analys](whats-new-endpoint-analytics.md).

## <a name="getting-started"></a><a name="bkmk_uea_prereq"></a>Komma igång

Du börjar använda slut punkts analys genom att verifiera kraven och sedan börja samla in data. 

### <a name="technical-prerequisites"></a>Tekniska krav

I den här för hands versionen kan du registrera enheter via Configuration Manager eller Microsoft Intune. 

För att kunna registrera enheter via Intune måste den här för hands versionen:
- Intune-registrerade enheter som kör Windows 10
- Start prestanda insikter är bara tillgängliga för enheter som kör version 1903 eller senare av Windows 10 Enterprise (Home-och Pro-utgåvor stöds inte för närvarande) och enheterna måste vara Azure AD-anslutna eller hybrid Azure AD-ansluten. Datorer som är anslutna till en arbets plats stöds inte för närvarande.
- Nätverks anslutning från enheter till det offentliga Microsoft-molnet. Mer information finns i [slut punkter](#bkmk_uea_endpoints).
- [Intune-tjänstens administratörs roll](https://docs.microsoft.com/intune/fundamentals/role-based-access-control) krävs för att [börja samla in data](#bkmk_uea_start).
   - Genom att klicka på **Start**godkänner du och bekräftar att dina kund uppgifter kan lagras utanför den plats som du valde när du etablerade Microsoft Intune-klienten.
   - När du har klickat på **Starta** för att samla in data kan andra skrivskyddade roller Visa data.

För att kunna registrera enheter via Configuration Manager måste den här för hands versionen:
- Configuration Manager version 2002 eller senare
- Klienter som uppgraderats till version 2002 eller senare
- [Microsoft Endpoint Manager-klient ansluter](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions) aktive rad med en Azure-klient plats för Nordamerika eller Europa (vi kommer att utökas till andra regioner snart)

Oavsett om du registrerar enheter via Intune eller Configuration Manager, har [**proaktivt reparations skript**](#bkmk_uea_prs) följande krav:
- Enheter måste vara Azure AD-anslutna eller hybrid Azure AD-ansluten och uppfylla något av följande villkor:
- En Windows 10 Enterprise-, Professional-eller Education-enhet som hanteras av Intune
- En [samhanterad](../../comanage/overview.md) enhet som kör Windows 10 Enterprise, version 1607 eller senare med [arbets belastningen klient appar](../../comanage/workloads.md#client-apps) pekade på Intune.
- En [samhanterad](../../comanage/overview.md) enhet som kör Windows 10 Enterprise, version 1903 eller senare med [arbets belastningen klient appar](../../comanage/workloads.md#client-apps) pekade på Configuration Manager.

### <a name="licensing-prerequisites"></a>Krav för licensiering

Slut punkts analys ingår i följande planer: 

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) eller högre
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) eller högre.

Proaktiva reparationer kräver också en av följande licenser för de hanterade enheterna:
- Windows 10 Enterprise E3 eller E5 (ingår i Microsoft 365 F3, E3 eller E5)
- Windows 10-utbildning a3 eller A5 (ingår i Microsoft 365 a3 eller A5)
- Windows Virtual Desktop Access E3 eller E5

### <a name="permissions"></a>Behörigheter

#### <a name="endpoint-analytics-permissions"></a>Endpoint Analytics-behörigheter

Följande behörigheter används för slut punkts analys:
- **Läs** under kategorin **enhets inställningar** .
- **Läs** i kategorin **organisation** . <!--temporary for pp-->
- Behörigheter som är lämpliga för användarens roll under kategorin **slut punkts analys** .

En skrivskyddad användare behöver bara **Läs** behörighet under både **enhets konfiguration** och **slut punkts analys** kategorier. En Intune-administratör behöver vanligt vis alla behörigheter.

#### <a name="proactive-remediations-permissions"></a>Proaktiva reparations behörigheter

För förebyggande reparationer måste användaren ha behörighet som är lämplig för deras roll under kategorin **enhets inställningar** .  Behörigheter i kategorin **slut punkts analys** behövs inte om användaren bara använder förebyggande reparationer.

En [Intune-tjänsteadministratör](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#intune-service-administrator-permissions) krävs för att bekräfta licensierings kraven innan du använder proaktiva reparationer för första gången.

## <a name="start-gathering-data"></a><a name="bkmk_uea_start"></a>Börja samla in data
- Om du bara registrerar Intune-hanterade enheter går du vidare till utgivaren [i avsnittet slut punkts analys Portal](#bkmk_uea_onboard) .

- Om du registrerar enheter som hanteras av Configuration Manager måste du utföra följande steg:
   - [Aktivera data insamling för slut punkts analys i Configuration Manager](#bkmk_uea_cm_enroll)
   - [Aktivera data uppladdning i Configuration Manager](#bkmk_uea_cm_upload)
   - [Publicera i slut punkts Analytics-portalen](#bkmk_uea_onboard)  

### <a name="enroll-devices-managed-by-configuration-manager"></a><a name="bkmk_uea_cm_enroll"></a>Registrera enheter som hanteras av Configuration Manager
<!--6051638, 5924760-->
Innan du registrerar Configuration Manager enheter kontrollerar du [kraven](#bkmk_uea_prereq) , inklusive aktivering av [Microsoft Endpoint Manager-klient anslutning](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions). 

#### <a name="enable-endpoint-analytics-data-collection-in-configuration-manager"></a><a name="bkmk_uea_cm_enable"></a>Aktivera data insamling för slut punkts analys i Configuration Manager

1. I Configuration Manager-konsolen går du till **Administration**  >  **klient inställningar**  >  **standard klient inställningar**.
1. Högerklicka och välj **Egenskaper** och välj sedan inställningarna för **dator agent** .
1. Ange **Aktivera data insamling för slut punkts analys** till **Ja**.
   > [!Important] 
   > Om du har en befintlig anpassad klient agent inställning som har distribuerats till dina enheter måste du uppdatera alternativet **Aktivera data insamling för slut punkts analys** i den anpassade inställningen och sedan distribuera det på datorerna så att det börjar gälla.

#### <a name="enable-data-upload-in-configuration-manager"></a><a name="bkmk_uea_cm_upload"></a>Aktivera data uppladdning i Configuration Manager

1. I Configuration Manager-konsolen går du till **Administration**  >  **Cloud Services**  >  **samhantering**.
1. Välj **CoMgmtSettingsProd** och klicka sedan på **Egenskaper**.
1. På fliken **Konfigurera uppladdning** markerar du alternativet för att **Aktivera slut punkts analys för enheter som laddats upp till Microsoft Endpoint Manager**

   :::image type="content" source="media/6051638-configure-upload-configmgr.png" alt-text="Aktivera slut punkts analys för enheter som laddats upp till Microsoft Endpoint Manager" lightbox="media/6051638-configure-upload-configmgr.png":::

### <a name="onboard-in-the-endpoint-analytics-portal"></a><a name="bkmk_uea_onboard"></a>Publicera i slut punkts Analytics-portalen
Det krävs registrering från slut punkts analys portalen för både Configuration Manager-och Intune-hanterade enheter.

1. Gå till `https://endpoint.microsoft.com/#blade/Microsoft_Intune_Enrollment/UXAnalyticsMenu`
1. Klicka på **Starta**. Detta tilldelar automatiskt en konfigurations profil för att samla in start prestanda data från alla tillgängliga enheter. Du kan [ändra tilldelade enheter](#bkmk_uea_profile) senare. Det kan ta upp till 24 timmar innan start prestanda data fylls från dina Intune-registrerade enheter efter att de startats om.
   - Mer information om vanliga problem finns i [Felsöka start prestanda enhets registrering](#bkmk_uea_enrollment_tshooter).

## <a name="overview-page"></a>Översikts sida

När dina data är klara kan du se viss information på sidan **Översikt** , förklaras i detalj nedan:

- **Poängen med användar upplevelsen** är ett 50/50 viktat medelvärde för de **rekommenderade program** -och **Start prestanda poängen**. Vi kommer att utöka uppsättningen av under streck över tid.

- Du kan jämföra den aktuella poängen med andra poäng genom att ange en bas linje.
  - Enligt beskrivningen i avsnittet [bas linje](#bkmk_uea_baselines) finns det en inbyggd bas linje för *kommersiella Media* för att se hur du jämför med ett typiskt företag. Du kan skapa nya bas linjer baserade på dina aktuella mått så att du kan spåra förloppet eller Visa regressionar över tid.
   - Bas linje markörer visas för din övergripande Poäng och under streck. Om något av poängen har försämrat med fler än det konfigurerbara tröskelvärdet från den valda bas linjen visas poängen i rött och poängen på den översta nivån flaggas som kräver uppmärksamhet.
  - Status för **otillräckliga data** innebär att du inte har tillräckligt med enhets rapportering för att ge en meningsfull poäng. Vi kräver för närvarande minst fem enheter.

- Med **filter** kan du Visa dina poäng på en delmängd av enheter eller användare. Men filter funktionen är inte aktive rad i den här för hands versionen.

- **Insikter och rekommendationer** är en prioriterad lista för att förbättra dina poäng. Den här listan filtreras till undernodens kontext när du navigerar till **bästa praxis** eller **Rekommenderad program vara**.

[![Översikts sida för slut punkts analys](media/overview-page.png)](media/overview-page.png#lightbox)

## <a name="recommended-software"></a><a name="bkmk_uea_rs"></a>Rekommenderad program vara

> [!Important]  
> Slut punkts analys beräknar poängen för **program varu införande** för alla dina Intune-hanterade enheter, oavsett om de har registrerats i slut punkts analys eller inte.

Vissa program är kända för att förbättra slutanvändarens upplevelse, oberoende av hälso mått på lägre nivå. Windows 10 har till exempel en mycket högre poäng i net-höjningen än Windows 7. Poängen för **program varu införande** är ett tal mellan 0 och 100 som representerar ett viktat medelvärde för procent andelen enheter som har distribuerat olika rekommenderade program varor. Den aktuella viktningen är högre för Windows än för de andra måtten eftersom användarna ofta interagerar med dem. Måtten beskrivs nedan: 

[![Sida för Rekommenderad program vara för slut punkts analys](media/recommended-software.png)](media/recommended-software.png#lightbox)

### <a name="windows-10"></a><a name="bkmk_uea_win10"></a>Windows 10

Windows 10 ger en bättre användar upplevelse än äldre versioner av Windows. Mer information finns i [Tei-rapporten](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf) .

Det här måttet mäter procent andelen enheter i Windows 10 jämfört med en äldre version av Windows.

Den rekommenderade reparations åtgärden för att flytta enheter från äldre versioner av Windows är att skapa en distributions plan med [Desktop Analytics](../../desktop-analytics/overview.md).

### <a name="autopilot"></a><a name="bkmk_uea_ap"></a>Autopilot

Microsoft autopilot ger en enklare första etablerings upplevelse för Windows 10-datorer än den inbyggda upplevelsen genom att minska antalet skärmar i OOBE (out of Box Experience) och tillhandahålla standardvärden för att säkerställa att de anställdas enheter är korrekt etablerade från fabriken eller vid återställning.

Det här måttet mäter procent andelen av Windows 10-enheter som är registrerade för autopilot.

Den rekommenderade reparations åtgärden är att registrera befintliga enheter i autopilot med hjälp av [Microsoft Intune](https://docs.microsoft.com/intune/enrollment-autopilot).

### <a name="azure-active-directory"></a><a name="bkmk_uea_aad"></a>Azure Active Directory

Azure Active Directory (Azure AD) ger användarna flera produktivitets fördelar, inklusive enkel inloggning till appar och tjänster, Windows Hello-inloggning, självbetjäning för BitLocker-återställning och företags data nätverks växling.

Det här måttet mäter procent andelen enheter som har registrerats i Azure AD.

Dina Microsoft-Intune-hanterade enheter är redan registrerade i Azure AD. Den rekommenderade reparations åtgärden för enheter som hanteras av Configuration Manager är att antingen [registrera dem i Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) eller tillsammans med att [hantera dem](../../comanage/overview.md). Att samhantera enheter förbättrar också moln hanterings poängen.

### <a name="cloud-management"></a><a name="bkmk_uea_intune"></a>Moln hantering

Microsoft Intune ger användarna flera produktivitets förmåner, inklusive att aktivera åtkomst till företags resurser även när de är borta från företags nätverket, och eliminerar behovet av och prestanda för grupprincip, vilket resulterar i en bättre slut användar upplevelse. Det här måttet mäter procent andelen datorer som har registrerats i Microsoft Intune. Se hur [Microsoft aktiverar detta för våra anställda](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune).

Den rekommenderade reparations åtgärden för enheter som hanteras av Configuration Manager som ännu inte har registrerats i Intune är att [samhantera dem](../../comanage/overview.md).

### <a name="no-commercial-median"></a><a name="bkmk_uea_np"></a>Inget kommersiellt median

Den inbyggda bas linjen för **kommersiell median** har för närvarande inte mått för de del resultat som anges i avsnitten ovan.

## <a name="startup-performance"></a><a name="bkmk_uea_bp"></a>Start prestanda

> [!NOTE]
> Om du inte ser start prestanda data från alla dina enheter kan du läsa [fel sökning av enhets registrering för start prestanda](#bkmk_uea_enrollment_tshooter).

Start prestanda poängen hjälper IT-användare att komma igång snabbt och produktiviteten snabbt, utan fördröjning av start och inloggning. **Start poängen** är ett tal mellan 0 och 100. Poängen är ett viktat medelvärde för **Start poängen** och **inloggnings** poängen, som beräknas enligt följande:

- **Start Poäng**: baserat på Start tiden för att logga in. Vi tittar på den senaste start tiden från varje enhet, förutom uppdaterings fasen, och visar den sedan från 0 (låg) till 100 (utmärkt). Poängen är genomsnittet för att ge en övergripande start poäng för klient organisationen.
- **Inloggnings Poäng**: baserat på tiden från när autentiseringsuppgifter har angetts tills användaren har åtkomst till ett svars bara skriv bord (vilket innebär att Skriv bordet har renderat och CPU-användningen underskrider 50% i minst 2 sekunder). Vi tittar på den senaste inloggnings tiden för varje enhet, förutom första inloggnings-eller inloggnings tillägg direkt efter en funktions uppdatering, och visar det sedan från 0 (dåligt) till 100 (utmärkt). Poängen är genomsnittet för att ge en övergripande start poäng för klient organisationen.

[![Start prestanda sida för Endpoint Analytics](media/startup-performance.png)](media/startup-performance.png#lightbox)

### <a name="insights"></a>Insikter

På sidan **Start prestanda** får du också en prioriterad lista över **insikter och rekommendationer**, som beskrivs i följande avsnitt:

#### <a name="hard-disk-drives"></a><a name="bkmk_uea_hdd"></a>Hård diskar

Start prestanda ger en insikt om antalet enheter där startenheten är en hård disk. Hård diskar leder vanligt vis till en start tid av tre till fyra gånger längre än solid-state-enheter. Vi rapporterar även den förväntade förbättringen för att starta prestanda som du kan få genom att flytta till solid state-enheter.

Klicka på om du vill visa en lista över enheter som har hård diskar. Den rekommenderade åtgärden är att uppgradera dessa enheter till solid-state-enheter.

#### <a name="group-policy"></a><a name="bkmk_uea_gp"></a>grupprincip

Start prestanda ger en insikt om hur många enheter som har fördröjningar vid start och inloggnings tider som orsakas av grupprincip. Genom att klicka dig igenom går du till vyn enheter. Vyn sorteras efter grupprincip tid, så att du kan se berörda enheter för ytterligare fel sökning.

Om du klickar till en viss enhet kan du se start-och inloggnings historik. Historiken hjälper dig att avgöra om problemet är en regression och när det kan ha inträffat.

Även om det finns många artiklar om hur du optimerar prestanda för grup principer kan du välja att migrera till moln hantering i stället. Genom att migrera till Cloud-Management kan du använda [säkerhets bas linjer i Intune](https://docs.microsoft.com/intune/protect/security-baselines) och det tidigare utgångna princip analys verktyget.

#### <a name="slow-boot-and-sign-in-times"></a><a name="bkmk_uea_sb"></a>Långsam start-och inloggnings tider

Start prestanda ger en insikt om antalet enheter med långsamma start-eller inloggnings tider. Start poängen eller inloggnings poängen på "0" innebär att det är långsamt. Genom att klicka dig igenom går du till vyn enheter. Enheterna sorteras efter kärn start tid eller kärn inloggnings tid, så att du kan se berörda enheter för ytterligare fel sökning.

Om du klickar till en viss enhet kan du se start-och inloggnings historik. Historiken hjälper dig att avgöra om problemet var en regression och när det kan ha inträffat.

### <a name="reporting-tabs"></a>Rapporterings flikar

Sidan **Start prestanda** har rapporterings flikar som ger stöd för insikter, inklusive:
1. **Modell prestanda**. På den här fliken kan du se start-och inloggnings prestanda per enhets modell, vilket kan hjälpa dig att identifiera om prestanda problem är isolerade till vissa modeller.
1. **Enhets prestanda**. Den här fliken innehåller start-och inloggnings mått för alla dina enheter. Du kan sortera efter ett visst mått (till exempel GP-inloggningsnamn) för att se vilka enheter som har sämsta resultat för det måttet för att hjälpa till med fel sökning. Du kan också söka efter en enhet efter namn. Om du klickar på en enhet kan du se start-och inloggnings historiken, vilket kan hjälpa dig att identifiera om det fanns en ny regression
1. **Start processer**. Start processer kan påverka användar upplevelsen negativt genom att öka hur lång tid användarna måste vänta på att Skriv bordet ska svara. Den här fliken (om den är synlig) visar vi bara detta till en del av dig eftersom vi fortfarande utvecklar den här funktionen) visar vilka processer som påverkar "inloggningen" tid för att svara på Skriv bordet ". Det håller processorn över 50% när Skriv bordet har Render ATS. Tabellen visar endast processer som påverkar minst 10 enheter i din klient organisation.  

## <a name="proactive-remediations"></a><a name="bkmk_uea_prs"></a>Proaktiva reparationer

Proaktiva reparationer är skript paket som kan användas för att identifiera och åtgärda vanliga support problem på en användares enhet innan de ens inser att det finns ett problem. Dessa åtgärder kan hjälpa till att minska support samtalen. Du kan skapa ett eget skript paket eller distribuera ett av de skript paket som vi har skrivit och använt i vår miljö för att minska support biljetterna.

Varje skript paket består av ett identifierings skript, ett reparations skript och metadata. Via Intune kan du distribuera dessa skript paket och se rapporter om deras effektivitet. Vi utvecklar aktivt nya skript paket och vill veta vad dina upplevelser använder. Kontakta din för hands version av slut punkts analys om du har några synpunkter på skript paketen.

### <a name="get-the-detection-and-remediation-scripts"></a><a name="bkmk_uea_prs_ps1"></a>Hämta identifierings-och reparations skript

1. Kopiera skripten från slutet av den här artikeln i avsnittet [PowerShell-skript](#bkmk_uea_ps_scripts) .
    - Skriptfiler vars namn börjar med `det` är identifierings skript. Reparations skript börjar med `rem` .
    - En beskrivning av skripten finns i Beskrivning av [skript](#bkmk_uea_scripts).
1. Spara varje skript med det angivna namnet. Namnet visas också i kommentarerna överst i varje skript.
    - Du kan använda ett annat skript namn, men det stämmer inte överens med det namn som anges i avsnittet [skript beskrivningar](#bkmk_uea_scripts) .


### <a name="deploying-and-monitoring-scripts"></a><a name="bkmk_uea_prs_deploy"></a>Distribuera och övervaka skript
Tjänsten för **Microsoft Intune hanterings tillägg** hämtar skripten från Intune och kör dem. Skripten körs igen var 24: e timme. Följ instruktionerna nedan för att distribuera och övervaka skripten:

1. Gå till noden **förebyggande reparationer** i-konsolen.
1. Klicka på knappen **skapa skript paket** för att skapa ett skript paket.
     [![Slut punkts analys-sidan för förebyggande reparationer. Välj länken Skapa.](media/proactive-remediations-create.png)](media/proactive-remediations-create.png#lightbox)
1. I **grundläggande** steg ger du skript paketet ett **namn** och eventuellt en **Beskrivning**. Fältet **utgivare** kan redige ras, men som standard används klient namnet. Det går inte att redigera **versionen** . 
1. I steget **Inställningar** kopierar du texten från skripten som du laddade ned till **identifierings skriptet** och **reparations skript** fälten. 
   - Du behöver motsvarande identifierings-och reparations skript för samma paket. Till exempel `Detect_stale_Group_Policies.ps1` motsvarar identifierings skriptet med `Remediate_stale_GroupPolicies.ps1` reparations skriptet.
       [![Slut punkts analys för proaktiva reparationer skript inställningar sidan.](media/proactive-remediations-script-settings.png)](media/proactive-remediations-script-settings.png#lightbox)
1. Slutför alternativen på sidan **Inställningar** med följande rekommenderade konfigurationer:
   - **Kör det här skriptet med de inloggade autentiseringsuppgifterna**: Detta beror på skriptet. Mer information finns i [skript beskrivningar](#bkmk_uea_scripts).
   - **Framtvinga kontroll av skript signatur**: Nej
   - **Kör skript i 64-bitars PowerShell**: Nej
1. Klicka på **Nästa** och tilldela sedan alla **omfångs etiketter** som du behöver.
1. I steget **tilldelningar** väljer du de enhets grupper som du vill distribuera skript paketet till.
1. Slutför **granskningen och skapa** steget för distributionen.
1. Under **rapportering**  >  av**slut punkts analys – proaktiva reparationer**kan du se en översikt över identifierings-och reparations status.
       [![Slut punkts analys rapport över aktiva reparationer, översikts sida.](media/proactive-remediations-report-overview.png)](media/proactive-remediations-report-overview.png#lightbox)
1. Klicka på **enhets status** om du vill hämta statusinformation för varje enhet i distributionen.
       [![Status för enhets status för slut punkts analys proaktiva reparationer.](media/proactive-remediations-device-status.png)](media/proactive-remediations-device-status.png#lightbox)


## <a name="endpoint-analytics-settings"></a><a name="bkmk_uea_set"></a>Inställningar för slut punkts analys

På sidan inställningar kan du välja **Allmänt** eller **bas linje**. Var och en av dessa inställningar beskrivs nedan:

### <a name="general"></a><a name="bkmk_uea_gen"></a>Redovisningsjournalmallar

På sidan **Allmänt** i **Inställningar** kan du se om insamlingen av start prestanda data för Intune har Aktiver ATS. Den aktive ras automatiskt för alla enheter som standard när du klickar på **Starta** för att aktivera användar upplevelse analys. Du kan välja att gå till noden Intune data insamlings princip för att ändra den uppsättning enheter där start-och inloggnings poster samlas in.


#### <a name="intune-data-collection-policy"></a><a name="bkmk_uea_profile"></a>Princip för data insamling i Intune

Om du vill tilldela den här inställningen till en delmängd av enheter [skapar du en profil](/intune/configuration/device-profile-create#create-the-profile) med följande information: 

  - **Namn**: Ange ett beskrivande namn för profilen, till exempel **insamlings princip för Intune-data**
   
  - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.
    
  - **Plattform**: Välj **Windows 10 och senare**
   
  - **Profil typ**: Välj **övervakning av Windows-hälsa**
   
  - Konfigurera **inställningarna**:
   
       - **Hälso övervakning**: Välj **Aktivera** om du vill samla in händelse information från Windows 10-enheter
    
    - **Omfång**: Välj **Start prestanda** 

  - Använd [omfattnings taggarna](/intune/configuration/device-profile-create#scope-tags) och [tillämplighets reglerna](/intune/configuration/device-profile-create#applicability-rules) för att filtrera profilen till vissa IT-grupper eller enheter i en grupp som uppfyller ett särskilt villkor.

> [!NOTE]
> Det finns en plats hållare för instruktioner om hur du konfigurerar Configuration Manager data Connector. Den här funktionen har dock inte implementerats i den här inledande privata förhands granskningen.

  [![Sidan allmänna inställningar för slut punkts analys](media/settings-general.png)](media/settings-general.png#lightbox)

### <a name="baseline-management"></a><a name="bkmk_uea_baselines"></a>Bas linje hantering

Du kan jämföra aktuella poäng och del poäng till andra genom att ange en bas linje.

1. Det finns en inbyggd bas linje för **kommersiell median**som gör att du kan jämföra dina resultat med ett typiskt företag.
1. Du kan skapa nya bas linjer baserade på dina aktuella mått för att spåra förloppet eller Visa regressionar över tid. Klicka på knappen **Skapa nytt** och ge din nya bas linje ett namn. Vi rekommenderar ett namn som innehåller datumet, så det är enklare att välja i list rutan på rapport sidorna.
1. Det finns en gräns på 100-bas linjer per klient. Du kan ta bort gamla bas linjer som inte längre behövs.
1. Dina aktuella mått är flaggade som röda och visas som försämrat om de faller under den aktuella bas linjen i dina rapporter. Eftersom det är helt vanligt att måtten fluktuerar från dag till dag, kan du ange ett Regressions tröskel som är standard 10%. Med det här tröskelvärdet flaggas endast mått som försämrat om de har försämrat med mer än 10%.

   [![Sidan bas linje inställningar för slut punkts analys](media/settings-baseline.png)](media/settings-baseline.png#lightbox)

## <a name="troubleshooting"></a><a name="bkmk_uea_tshoot"></a>Telefonbaserad

Avsnitten nedan kan användas för att hjälpa till med fel sökning av problem som kan uppstå.

### <a name="troubleshooting-startup-performance-device-enrollment"></a><a name="bkmk_uea_enrollment_tshooter"></a>Felsöka start prestanda enhets registrering

Om sidan Översikt visar start prestanda poängen noll tillsammans med en banderoll som visar att den väntar på data, eller om fliken enhets prestanda i Start prestanda visar färre enheter än vad du förväntar dig, finns det några steg som du kan vidta för att felsöka problemet.

Först här är en snabb sammanfattning av begränsningarna för insamling av start prestanda data:
1. Enheter måste vara Windows 10 version 1903 eller senare.
2. Enheter måste vara Azure AD-anslutna. Vi har för närvarande inte stöd för enheter som är anslutna till arbets platsen, men det är aktivt att undersöka möjligheten att lägga till den här funktionen i Windows.
3. Enheter måste vara Windows 10 Enterprise Edition. Windows 10 Home och Professional stöds inte för närvarande, men det är aktivt att det är möjligt att lägga till den här funktionen i Windows.

Observera att de här problemen inte gäller data som kommer från den kommande Configuration Manager anslutningen. den kommer att kunna samla in data från alla Configuration Manager klient datorer, oavsett version, version eller katalog konfiguration.

För det andra är en snabb lista att gå igenom för fel sökning:
1. Kontrol lera att du har Windows Health Monitoring-profilen som är avsedd för alla enheter som du vill ha prestanda data för. Du kan hitta en länk till den här profilen inifrån inställnings sidan för slut punkts analys, eller så går du till den som en annan Intune-profil. Titta på fliken tilldelning för att se till att den är tilldelad till den förväntade uppsättningen enheter. 
1. Ta en titt på vilka enheter som har kon figurer ATS för data insamling. Du kan också se den här informationen på sidan profil översikt.  
   - Det finns ett känt problem där kunder kan se fel vid profil tilldelning, där berörda enheter visar felkoden `-2016281112 (Remediation failed)` . Vi undersöker aktivt det här problemet.
1. Enheter som har kon figurer ATS för data insamling måste startas om efter att data insamlingen har Aktiver ATS och du måste vänta upp till 24 timmar efter att enheten har visats på fliken enhets prestanda.
1. Om enheten har kon figurer ATS för data insamling, har startats om och efter 24 timmar ser du fortfarande att enheten inte kan komma åt våra samlings slut punkter. Det här problemet kan inträffa om ditt företag använder en proxyserver och slut punkterna inte har Aktiver ATS i proxyn. Mer information finns i [fel sökning av slut punkter](#bkmk_uea_endpoints).


### <a name="endpoints"></a><a name="bkmk_uea_endpoints"></a>Slut punkter

För att registrera enheter till slut punkts analys måste de skicka nödvändiga funktions data till Microsoft. Om din miljö använder en proxyserver använder du den här informationen för att konfigurera proxyn.

Om du vill aktivera funktionell data delning konfigurerar du proxyservern så att den tillåter följande slut punkter:

> [!Important]  
> För sekretess och data integritet söker Windows efter ett Microsoft SSL-certifikat (certifikat fästning) vid kommunikation med de nödvändiga slut punkterna för funktions data delning. SSL-avlyssning och inspektion är inte möjlig. Om du vill använda slut punkts analys utesluter du dessa slut punkter från SSL-kontroll.<!-- BUG 4647542 -->

| Slutpunkt  | Funktion  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Används för att skicka [nödvändiga funktions data](#bkmk_uea_datacollection) till data insamlings slut punkten för Intune. |
| `https://graph.windows.net` | Används för att automatiskt hämta inställningar när du kopplar din hierarki till Endpoint Analytics (på Configuration Manager Server roll). Mer information finns i [Konfigurera proxyservern för en plats system Server](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Används för att synkronisera enhets samling och enheter med slut punkts analys (endast på Configuration Manager Server roll). Mer information finns i [Konfigurera proxyservern för en plats system Server](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |


### <a name="proxy-server-authentication"></a>Autentisering av proxyserver

Om din organisation använder proxyautentisering för Internet åtkomst kontrollerar du att den inte blockerar data på grund av autentisering. Om proxyn inte tillåter att enheter skickar dessa data visas de inte i Skriv bords analys.

#### <a name="bypass-recommended"></a>Kringgå (rekommenderas)

Konfigurera proxyservrarna så att de inte kräver proxyautentisering för trafik till data delnings slut punkter. Det här alternativet är den mest omfattande lösningen. Det fungerar för alla versioner av Windows 10.  

#### <a name="user-proxy-authentication"></a>Autentisering av användar-proxy

Konfigurera enheter så att de använder den inloggade användarens kontext för proxyautentisering. Den här metoden kräver följande konfigurationer:

- Enheter har den aktuella kvalitets uppdateringen för en version av Windows som stöds

- Konfigurera proxy för användar nivå (WinINET-proxy) i **proxyinställningar** i nätverks & Internet grupp för Windows-inställningar. Du kan också använda den äldre kontroll panelen för Internet alternativ.

- Kontrol lera att användarna har proxy-behörighet för att komma åt data delnings slut punkterna. Det här alternativet kräver att enheterna har konsol användare med proxy-behörigheter, så att du inte kan använda den här metoden med hjälp av omdirigerings enheter.

> [!IMPORTANT]
> Autentiseringsmetoden för användarautentisering är inte kompatibel med användning av Microsoft Defender Avancerat skydd. Det här problemet beror på att den här autentiseringen är beroende av register nyckeln **DisableEnterpriseAuthProxy** `0` , medan Microsoft Defender ATP kräver att den är inställd på `1` . Mer information finns i [Konfigurera inställningar för Machine proxy och Internet anslutning i Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

#### <a name="device-proxy-authentication"></a>Enhets-proxy-autentisering

Den här metoden har stöd för följande scenarier:

- Konsol lösta enheter, där ingen användare loggar in eller användare av enheten inte har Internet åtkomst

- Autentiserade proxyservrar som inte använder Windows-integrerad autentisering

- Om du också använder Microsoft Defender Avancerat skydd

Den här metoden är den mest komplexa eftersom den kräver följande konfigurationer:

- Se till att enheterna kan komma åt proxyservern via WinHTTP i lokalt system sammanhang. Använd något av följande alternativ för att konfigurera det här beteendet:

  - Kommando raden`netsh winhttp set proxy`

  - WPAD-protokoll (Web Proxy Auto-Discovery)

  - Transparent proxy

  - Konfigurera en enhets omfattande WinINET-proxy med följande grup princip inställning: **gör proxyinställningar per dator (i stället för per användare)** (ProxySettingsPerUser = `1` )

  - Dirigerad anslutning eller som använder Network Address Translation (NAT)

- Konfigurera proxyservrar så att dator kontona i Active Directory kan komma åt data slut punkterna. Den här konfigurationen kräver att proxyservrar har stöd för Windows-integrerad autentisering.  


## <a name="frequently-asked-questions"></a><a name="bkmk_uea_faq"></a>Vanliga frågor och svar

### <a name="will-my-endpoint-analytics-data-migrate-if-i-move-my-intune-tenant-to-a-different-tenant-location"></a>Kommer mina slut punkts analys data att migrera om jag flyttar min Intune-klient till en annan klient plats?

Om du migrerar din Intune-klient till en annan plats går alla data i din slut punkts analys lösning vid tidpunkten för migreringen förlorade. Eftersom slut punkter rapporterar till slut punkts analys kontinuerligt, överförs alla händelser som inträffar efter migrering automatiskt till din nya klient plats och dina rapporter börjar fyllas i igen, förutsatt att enheterna förblir korrekt registrerade. 

### <a name="why-are-the-scripts-exiting-with-a-code-of-1"></a>Varför avslutas skripten med en kod på 1?

Skripten avslutas med en kod på 1 för att signalera till Intune att reparationen ska ske. I det här fallet, om du avslutar ett identifierings skript med 1 innebär det att det är sant att reparation krävs. Många skript paket som bara körs i CM kan visa att de uppfyller kraven, men avslutas med kod 1. För de här skripten går det inte att avsluta med en kod på 1, men du kanske vill kontrol lera att enheten är korrekt åtgärdad.

### <a name="why-did-the-update-stale-group-policies-script-return-with-error-0x87d00321"></a>Varför returnerade skriptet uppdatera föråldrade grup principer med fel 0x87D00321?

0x87D00321 är ett tids gräns fel för skript körning. Det här felet uppstår vanligt vis med datorer som är fjärranslutna. En potentiell minskning kan vara att bara distribuera till en dynamisk samling datorer som har intern nätverks anslutning.

## <a name="script-descriptions"></a><a name="bkmk_uea_scripts"></a>Skript beskrivningar

I den här tabellen visas skript namn, beskrivningar, identifieringar, reparationer och konfigurerbara objekt. Skriptfiler vars namn börjar med `Detect` är identifierings skript. Reparations skript börjar med `Remediate` . Dessa skript kan kopieras från nästa avsnitt i den här artikeln.

|Skriptets namn|Beskrivning|
|---|---|
|**Uppdatera inaktuella grup principer** </br>`Detect_stale_Group_Policies.ps1` </br> `Remediate_stale_GroupPolicies.ps1`| Identifierar om senaste grupprincip uppdatering är större än `7 days` sedan.  </br>Anpassa tröskelvärdet för 7 dagar genom att ändra värdet för `$numDays` i identifierings skriptet. </br></br>Åtgärdar genom att köra `gpupdate /target:computer /force` och`gpupdate /target:user /force`  </br> </br>Kan hjälpa till att minska antalet nätverks anslutnings support samtal när certifikat och konfigurationer levereras via grupprincip. </br> </br> **Kör skriptet med de inloggade autentiseringsuppgifterna**: Ja|
|**Starta om Office Klicka-och-kör-tjänsten** </br> `Detect_Click_To_Run_Service_State.ps1` </br> `Remediate_Click_To_Run_Service_State.ps1`| Identifierar om tjänsten Klicka-till-kör är inställd på att starta automatiskt och om tjänsten stoppas. </br> </br> Åtgärdar genom att ställa in tjänsten att starta automatiskt och starta tjänsten om den stoppas. </br></br> Hjälper till att åtgärda problem där Win32 Microsoft 365-appar för företag inte startar, eftersom tjänsten för att klicka och köra har stoppats. </br> </br> **Kör skriptet med de inloggade autentiseringsuppgifterna**: Nej|
|**Kontrol lera nätverks certifikat** </br>`Detect_Expired_Issuer_Certificates.ps1` </br>`Remediate_Expired_Issuer_Certificates.ps1`|Identifierar certifikat som utfärdats av en certifikat utfärdare antingen i datorns eller användarens personliga arkiv som har upphört att gälla eller snart upphör att gälla. </br> Ange CA: n genom att ändra värdet för `$strMatch` i identifierings skriptet. Ange 0 om `$expiringDays` du vill hitta utgångna certifikat eller ange ett annat antal dagar för att hitta certifikat som snart upphör att gälla.  </br></br>Åtgärdar genom att öka ett popup-meddelande till användaren. </br> Ange `$Title` värdena och `$msgText` med den meddelande rubrik och text som du vill att användarna ska se. </br> </br> Meddelar användare om utgångna certifikat som kan behöva förnyas. </br> </br> **Kör skriptet med de inloggade autentiseringsuppgifterna**: Nej|
|**Rensa inaktuella certifikat** </br>`Detect_Expired_User_Certificates.ps1` </br> `Remediate_Expired_User_Certificates.ps1`| Identifierar utgångna certifikat som utfärdats av en certifikat utfärdare i den aktuella användarens personliga arkiv. </br> Ange CA: n genom att ändra värdet för `$certCN` i identifierings skriptet. </br> </br> Åtgärdar genom att ta bort utgångna certifikat som utfärdats av en certifikat utfärdare från den aktuella användarens personliga arkiv. </br> Ange CA: n genom att ändra värdet för `$certCN` i reparations skriptet. </br> </br> Söker efter och tar bort utgångna certifikat som utfärdats av en certifikat utfärdare från den aktuella användarens personliga arkiv. </br> </br> **Kör skriptet med de inloggade autentiseringsuppgifterna**: Ja|

## <a name="powershell-scripts"></a><a name="bkmk_uea_ps_scripts"></a>PowerShell-skript

### <a name="detect_stale_group_policiesps1"></a>Detect_stale_Group_Policies. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_stale_Group_Policies.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $numDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables
$numDays = 7

try {
    $gpResult = gpresult /R | Select-String -pattern "Last time Group Policy was applied:" | Select-Object -last 1

    if ($gpResult){
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        if ($lastGPUpdateDays -gt $numDays){
            #We want within last $numDays so we get "Match"
            Write-Host "Match"
            exit 1
        }
        else {
            #Script succeeds but > $numDays since last update so remediate
            #Exit 1 for Intune and "Match" for ConfigMan
            Write-Host "No_Match"
            exit 0
        }
    }
}
catch {
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_stale_grouppoliciesps1"></a>Remediate_stale_GroupPolicies. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_stale_GroupPolicies.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try{
    $compGP = gpupdate /target:computer /force | out-string
    $userGP = gpupdate /target:user /force | out-string
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="detect_click_to_run_service_stateps1"></a>Detect_Click_To_Run_Service_State. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Click_To_Run_Service_State.ps1
# Description:     Detect if Office 16 installed and if "Click to Run Service" is running.
# Notes:           No variable substitution should be necessary
#
#=============================================================================================================================

# Define Variables
$curSvcStat,$svcCTRSvc,$errMsg = "","",""

# Main script
If (-not (Test-Path -Path 'hklm:\Software\Microsoft\Office\16.0')){
    Return "Office 16.0 (or greater) not present on this machine"
    exit 0   
} 

Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
}

Catch{    
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}

If ($curSvcStat -eq "Running"){
    Write-Output $curSvcStat
    exit 0                        
}
Else{
    If($curSvcStat -eq "Stopped"){
    Write-Output $curSvcStat
    exit 1     
    }
}
Else{
    Write-Error "Error: " + $errMsg
    exit 1
}
```

### <a name="remediate_click_to_run_service_stateps1"></a>Remediate_Click_To_Run_Service_State. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Click_To_Run_Service_State.ps1
# Description:     Start the "Click to Run Service" and change its startup type to Automatic
#       Notes:     No variable substitution needed
#
#=============================================================================================================================

# Define Variables
$svcCur = "ClickToRunSvc"
$curSvcStat,$svcCTRSvc,$errMsg = "","",""
$ctr = 0

# Main script
# Make sure nothing has changed since detection, the service exists and is stopped
Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
    }

Catch{    
    $errMsg = $_.Exception.Message
    }
        
# If the service got started between detection and now (nested if) then return
# If the service got uninstalled or corrupted between detection and now (else) then return the "Error: " + the error
If ($curSvcStat -ne "Stopped"){
    If ($curSvcStat -eq "Running"){
        return
    }
    Else{
        return "Error: " + $errMsg
    }
}

# Service should be there and stopped, change the startup type and start
Try{        
    Set-Service $svcCur -StartupType Automatic
    Start-Service $svcCur
    $svcCTRSvc = Get-Service $svcCur
    $curSvcStat = $svcCTRSvc.Status
        While ($curSvcStat.Equals("Stopped")){
            Start-Sleep -Seconds 5
            ctr++
            if(ctr == 12){
                Return "Service could not be started after 60 seconds"
                break
            }
        }
    }

Catch{    
    $errMsg = $_.Exception.Message
    Return $errMsg
    }

Return $curSvcStat
```

### <a name="detect_expired_issuer_certificatesps1"></a>Detect_Expired_Issuer_Certificates. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_Issuer_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_issuer_certificatesps1"></a>Remediate_Expired_Issuer_Certificates. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_Issuer_Certificates.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

### <a name="detect_expired_user_certificatesps1"></a>Detect_Expired_User_Certificates. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_User_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_user_certificatesps1"></a>Remediate_Expired_User_Certificates. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_User_Certificates.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## <a name="endpoint-analytics-data-privacy"></a><a name="bkmk_uea_privacy"></a>Data sekretess för Endpoint Analytics

### <a name="data-flow"></a>Dataflöde

Följande bild visar hur nödvändiga funktionella data flödar från enskilda enheter via våra data tjänster, tillfälliga lagring och till din klient organisation. Data flödar genom våra befintliga företags pipeliner utan att det är beroende av Windows-diagnostikdata.

[![Data flödes diagram för användar upplevelse](media/dataflow.png)](media/dataflow.png#lightbox)

1. Konfigurera **Intune data insamlings** princip för registrerade enheter. Som standard tilldelas den här principen till "alla enheter" när du **startar** slut punkts analys. Du kan dock [ändra tilldelningen](#bkmk_uea_set) när som helst till en delmängd av enheterna eller inga enheter alls.

2. Enheter skickar nödvändiga funktions data.

    - För Intune-enheter med den tilldelade principen skickas data från Intune Management-tillägget. Mer information finns i [krav](#bkmk_uea_prereq).
    - För Configuration Manager hanterade enheter kan data även flöda till Microsoft Endpoint Management via ConfigMgr-anslutningen. ConfigMgr-kopplingen är kopplad till molnet. Den kräver bara anslutning till en Intune-klient, som inte aktiverar samhantering.

> [!Note]  
> De data som krävs för att beräkna start poängen för en enhet genereras under start tiden. Beroende på energi inställningar och användar beteende kan det ta flera veckor efter att en enhet har tilldelats en korrekt princip för att visa start poängen i administratörs konsolen.  

3. Microsoft Endpoint Management-tjänsten bearbetar data för varje enhet och publicerar resultaten för både enskilda enheter och organisations mängder i administrations konsolen med MS Graph API: er.

Den genomsnittliga svars tiden för slut punkt till slut punkt är ungefär 12 timmar och är bryggad efter den tid det tar att utföra den dagliga bearbetningen. Alla andra delar av data flödet är nästan i real tid.

### <a name="data-collection"></a><a name="bkmk_uea_datacollection"></a>Datainsamling

De grundläggande funktionerna i slut punkts analys samlar för närvarande in information som är kopplad till Start prestanda poster som hamnar i de [identifierade](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#identified-data) och [pseudonymized](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#pseudonymized-data) kategorierna. När vi lägger till ytterligare funktioner över tid, kommer de data som samlas in att variera efter behov. Huvud-Datapoints som för närvarande samlas in:

#### <a name="identified-data"></a>Identifierade data

- Information om maskinvaruinventering
  - **gör:** Enhets tillverkare
  - **modell:** Enhets modell
  - **deviceClass:** Enhets klassificeringen. Till exempel Desktop, server eller Mobile.
  - **Land:** Enhets regions inställningen
- Programinventering såsom
  - **Namn:** Aktivitets
  - **ver:** Den aktuella operativ system versionen.
  
#### <a name="pseudonymized-data"></a>Pseudonymiserade data

- Diagnostik-, prestanda- och användningsdata som är kopplade till en användare och/eller en enhet
  - **logOnId**
  - Start" **:** Systemets start-ID
  - **coreBootTimeInMilliseconds:** Tid för Core-start
  - **totalBootTimeInMilliseconds:** Total start tid
  - **updateTimeInMilliseconds:** Tid för att OS-uppdateringar ska slutföras
  - **gpLogonDurationInMilliseconds**: tid för grup principer som ska bearbetas
  - **desktopShownDurationInMilliseconds:** Tid för skriv bord (Explorer. exe) som ska läsas in
  - **desktopUsableDurationInMilliseconds:** Tiden för Skriv bordet (Explorer. exe) ska kunna användas
  - **topProcesses:** Lista över processer som lästs in under start med namn, med information om processor användnings statistik och appar (namn, utgivare, version). Till exempel *{ \" processname \" : \" svchost \" , \" CpuUsage \" : 43, \" ProcessFullPath \" : \" C: \\ \\ Windows \\ \\ system32 \\ \\ svchost. exe \" , \" ProductName \" : \" Microsoft &reg; Windows &reg; operativ system \" , \" Publisher \" : \" Microsoft Corporation \" , \" ProductVersion \" : \" 10.0.18362.1 \" }*
- Enhetsdata som inte är kopplade till en enhet eller en användare (om dessa data är kopplade till en enhet eller en användare behandlar Intune dem som identifierade data)
  - **ID:** Unikt enhets-ID som används av Windows Update
  - **localId:** Ett lokalt definierat unikt ID för enheten. Detta är inte det läsliga enhets namnet. Troligen lika med värdet som lagras vid HKLM\Software\Microsoft\SQMClient\MachineId.
  - **aaddeviceid:** Azure Active Directory enhets-ID
  - **orgId:** Unikt GUID som representerar Microsoft O365-klienten
  
> [!Important]  
> Våra data hanterings principer beskrivs i [Sekretess policyn för Microsoft Intune](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement). Vi använder bara dina kund uppgifter för att tillhandahålla de tjänster som du har registrerat dig för. Som beskrivs under onboarding-processen maskera vi och sammanställer poängen från alla registrerade organisationer för att hålla bas linjerna uppdaterade.


### <a name="resources"></a>Resurser

Mer information om relaterade sekretess aspekter finns i följande artiklar:

- [Microsoft Intune sekretess policy](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Kompatibilitet med Windows 10 och sekretess](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [Licens villkor och dokumentation](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Säkerhet och sekretess på Microsoft Azure Data Center](https://azure.microsoft.com/global-infrastructure/)  
- [Förtroende i det betrodda molnet](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Säkerhetscenter](https://www.microsoft.com/trustcenter)  
