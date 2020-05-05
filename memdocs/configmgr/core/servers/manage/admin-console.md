---
title: Configuration Manager-konsolen
titleSuffix: Configuration Manager
description: Lär dig mer om att navigera i Configuration Manager-konsolen.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 58b66639094a602206114cd75a724504618ad38c
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110040"
---
# <a name="how-to-use-the-configuration-manager-console"></a>Använda Configuration Manager-konsolen

*Gäller för: Configuration Manager (aktuell gren)*

Administratörer använder Configuration Manager-konsolen för att hantera Configuration Managers miljön. Den här artikeln beskriver grunderna i att navigera i-konsolen.  

## <a name="open-the-console"></a><a name="bkmk_open"></a>Öppna-konsolen

Configuration Manager-konsolen installeras alltid på varje plats Server. Du kan också installera det på andra datorer. Mer information finns i [installera Configuration Manager-konsolen](../deploy/install/install-consoles.md).

Den enklaste metoden för att öppna-konsolen på en Windows 10-dator **Start** , tryck på Start `Configuration Manager console`och börja skriva. Du kanske inte behöver ange hela strängen för Windows för att hitta den bästa matchningen.

Om du bläddrar på Start menyn tittar du på ikonen för **Configuration Manager konsolen** i **Microsoft Endpoint Manager** -gruppen.

![Ikoner för Start-menyn i Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Sökvägen till Start-menyn har ändrats i version 1910. I version 1906 och tidigare är mappnamnet **System Center**. När du uppdaterar Configuration Manager till version 1910 eller senare, måste du uppdatera all intern dokumentation som du upprätthåller för att ta med den nya platsen.

## <a name="connect-to-a-site-server"></a>Anslut till en plats Server

-Konsolen ansluter till den centrala administrations plats servern eller till dina primära plats servrar. Du kan inte ansluta en Configuration Manager-konsol till en sekundär plats. Under installationen angav du det fullständigt kvalificerade domän namnet (FQDN) för den plats server som-konsolen ansluter till.

Använd följande steg för att ansluta till en annan plats Server:

1. Välj pilen överst i [menyfliksområdet](#ribbon)och välj **Anslut till en ny plats**.  

    ![Ansluta-konsolen till en ny plats](media/connect-to-a-new-site.png)  

2. Ange plats serverns fullständiga domän namn. Om du har anslutit till plats servern tidigare väljer du servern i list rutan.  

    ![Fönstret plats anslutning anger du FQDN för plats servern](media/site-server-fqdn.png)  

3. Välj **Anslut**.  

Från och med version 1810 kan du ange den lägsta autentiseringsnivån som administratörer kan använda för att komma åt Configuration Manager-platser. Den här funktionen tvingar administratörer att logga in på Windows med den nivå som krävs. Mer information finns i [Planera för SMS-providern](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  

## <a name="navigation"></a>Navigering

Vissa delar av konsolen kanske inte syns beroende på din tilldelade säkerhets roll. Mer information om roller finns i [grunderna i rollbaserad administration](../../understand/fundamentals-of-role-based-administration.md).

### <a name="workspaces"></a>Arbetsytor

Configuration Manager-konsolen har fyra **arbets ytor**:  

- **Till gångar och efterlevnad**  

- **Program varu bibliotek**  

- **Övervakning**  

- **Administration**  

![Configuration Manager arbets ytor med snabb meny](media/configuration-manager-workspaces.png)  

Ändra ordning på arbets ytans knappar genom att välja nedpilen och välja **alternativ för navigerings fönstret**. Markera ett objekt som du vill **Flytta upp** eller **Flytta ned**. Välj **Återställ** för att återställa standard knappens ordning.  

![Fönstret alternativ för navigerings fönstret för att ändra ordning på arbets ytor](media/navigation-pane-options.png)  

Minimera knappen för en arbets yta genom att välja **Visa färre knappar**. Den sista arbets ytan i listan minimeras först. Välj en minimerad knapp och välj **Visa fler knappar** för att återställa knappen till dess ursprungliga storlek.

![Minimerade arbets ytor i Configuration Managers konsolen](media/workspace-buttons.png)  

### <a name="nodes"></a>Noder

Arbets ytor är en samling **noder**. Ett exempel på en nod är noden **program uppdaterings grupper** i arbets ytan **program varu bibliotek** .

När du är i noden kan du välja pilen för att minimera navigerings fönstret.  

![Exempel nod och markera minimera pil](media/software-update-groups-node.png)  

Använd **navigerings fältet** för att flytta runt i konsolen när du minimerar navigerings fönstret.  

![Configuration Manager minimerat navigerings fönster](media/minimized-navigation-pane.png)  

I-konsolen är noder ibland ordnade i mappar. När du väljer mappen visas vanligt vis ett **navigerings index** eller en **instrument panel**.  

![Navigerings index för Configuration Manager program uppdateringar](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>Menyfliksområde

Menyfliksområdet är överst i Configuration Manager-konsolen. Menyfliksområdet kan ha mer än en flik och kan minimeras med hjälp av pilen till höger. Knapparna i menyfliksområdet ändras baserat på noden. De flesta knappar i menyfliksområdet är också tillgängliga i snabb menyer.  

![Exempel på menyfliksområdet, markera flera flikar och minimera pil](media/ribbon.png)

### <a name="details-pane"></a>Informations fönster

Du kan få mer information om objekten genom att granska informations fönstret. Informations fönstret kan ha en eller flera flikar. Flikarna varierar beroende på noden.  

![Configuration Manager exempel på informations fönster](media/details-pane.png)

### <a name="columns"></a>Kolumner

Du kan lägga till, ta bort, ändra ordning på och ändra storlek på kolumner. Med dessa åtgärder kan du Visa de data du föredrar. Tillgängliga kolumner varierar beroende på noden. Om du vill lägga till eller ta bort en kolumn från vyn högerklickar du på en befintlig kolumn rubrik och väljer ett objekt. Ordna om kolumner genom att dra kolumn rubriken där du vill att den ska vara.  

![Lägg till kolumn i konfigurations hanterare](media/add-columns.png)  

Längst ned i snabb menyn kolumn kan du sortera eller gruppera efter en kolumn. Dessutom kan du sortera efter en kolumn genom att välja dess rubrik.  

![Configuration Manager gruppera efter kolumn](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a>Frigör lås för att redigera objekt

<!--4786915-->

Om Configuration Manager-konsolen slutar svara kan du vara utelåst från att göra ytterligare ändringar tills låset upphör att gälla efter 30 minuter. Det här låset är en del av Configuration Manager SEDO (serialiserad redigering av distribuerade objekt). Mer information finns i [Configuration Manager Sedo](../../../develop/core/understand/sedo.md).

Från och med den [aktuella gren versionen 1906](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences)kan du rensa låset på en aktivitetssekvens. Från och med version 1910 kan du rensa låset för alla objekt i Configuration Manager-konsolen.

Den här åtgärden gäller endast för ditt användar konto som har låst och på samma enhet som webbplatsen har beviljat låset. När du försöker komma åt ett låst objekt kan du nu **ignorera ändringarna**och fortsätta redigera objektet. Dessa ändringar skulle förloras när låset upphörde att gälla.

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a>Visa nyligen anslutna konsoler

<!--3699367-->
Från och med version 1902 kan du se de senaste anslutningarna för Configuration Manager-konsolen. Vyn innehåller aktiva anslutningar och de anslutningar som nyligen var anslutna. Du ser alltid din aktuella konsol anslutning i listan och du ser bara anslutningar från Configuration Manager-konsolen. Du ser inte PowerShell eller andra SDK-baserade anslutningar till SMS-providern. Platsen tar bort instanser från listan som är äldre än 30 dagar.

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a>Krav för att Visa anslutna konsoler

- Ditt konto måste ha **Läs** behörighet för **SMS_SITE** -objektet

- Konfigurera administrations tjänsten REST API. Mer information finns i [Vad är administrations tjänsten?](../../../develop/adminservice/overview.md)

### <a name="view-connected-consoles"></a>Visa anslutna konsoler

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen.  

2. Expandera **säkerhet** och välj noden **konsol anslutningar** .  

3. Visa de senaste anslutningarna med följande egenskaper:  

    - Användarnamn
    - Dator namn
    - Ansluten platskod
    - Konsol version
    - Senast ansluten: när användaren senast *öppnade* konsolen
    - Från och med version 1910 har den sista kolumnen med **konsol pulsslag** ersatt den **senaste anslutna tids** kolumnen. <!--4923997-->
       - En öppen konsol i förgrunden skickar ett pulsslag var tionde minut.

![Visa Configuration Manager konsol anslutningar](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a>Starta Microsoft Teams chat från konsol anslutningar
<!--4923997-->
*(Lanseras i version 1910)*

Från och med version 1910 kan du meddelande om andra Configuration Manager-administratörer från noden **konsol anslutningar** med hjälp av Microsoft Teams. När du väljer att **Starta Microsoft Teams chatt** med en administratör lanseras Microsoft Teams och en chatt öppnas med användaren.

### <a name="prerequisites"></a>Krav

- För att starta en chatt med en administratör måste det konto som du vill chatta med ha identifierats med [Azure AD eller AD User Discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Microsoft Teams installerat på den enhet från vilken du kör-konsolen.
anteckning
- Alla [krav för att Visa anslutna konsoler](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>Starta Microsoft Teams Chat

1. Gå till **Administration** > **säkerhets** > **konsol anslutningar**.
1. Högerklicka på en användares konsol anslutning och välj **Starta Microsoft Teams Chat**.
    - Om användarens huvud namn inte hittas för den valda administratören, är det bara att **Starta Microsoft Teams Chat** .
    - Ett fel meddelande, inklusive en nedladdnings länk, visas om Microsoft Teams inte är installerat på den enhet från vilken du kör-konsolen.
    - Om Microsoft Teams är installerat på den enhet där du kör-konsolen öppnas en chatt med användaren.

### <a name="known-issues"></a>Kända problem

Fel meddelandet som meddelar att Microsoft Teams inte är installerat visas inte om följande register nyckel inte finns:

Dator \ HKEY_CURRENT_USER \SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Du kan lösa problemet genom att manuellt skapa register nyckeln.

## <a name="configuration-manager-console-notifications"></a><a name="bkmk_notify"></a>Configuration Manager konsol meddelanden

<!--3556016, fka 1318035-->
Från och med Configuration Manager version 1902 meddelar konsolen om följande händelser:

- När en uppdatering är tillgänglig för Configuration Manager
- När livs cykel-och underhålls händelser inträffar i miljön

Det här meddelandet är ett fält överst i konsol fönstret under menyfliksområdet. Den tidigare upplevelsen ersätts när Configuration Manager uppdateringar är tillgängliga. Dessa meddelanden i konsolen visar fortfarande viktig information, men stör inte ditt arbete i-konsolen. Du kan inte ignorera viktiga meddelanden. I-konsolen visas alla meddelanden i ett nytt meddelande fält i namn listen.

![Meddelande fältet och flaggan i-konsolen](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>Konfigurera en plats för att visa meddelanden som inte är kritiska

Du kan konfigurera varje plats så att den visar icke-kritiska meddelanden i egenskaperna för platsen.

1. I arbets ytan **Administration** expanderar du **plats konfiguration**och väljer noden **platser** .
1. Välj den plats som du vill konfigurera för icke-kritiska meddelanden.
1. I menyfliksområdet väljer du **Egenskaper**.
1. På fliken **aviseringar** väljer du alternativet för att **Aktivera konsol meddelanden för icke-kritiska plats hälso ändringar**.
   - Om du aktiverar den här inställningen ser alla konsol användare viktiga, varnings-och informations meddelanden. Den här inställningen är aktiverad som standard.  
   - Om du inaktiverar den här inställningen visas endast viktiga meddelanden i konsol användare.  

De flesta konsol meddelanden är per session. -Konsolen utvärderar frågor när en användare startar den. Starta om-konsolen om du vill se ändringar i meddelandena. Om en användare avstår från ett icke-kritiskt meddelande, meddelas du igen när konsolen startas om, om det fortfarande är tillämpligt.

Följande meddelanden utvärderas var femte minut:

- Platsen är i underhålls läge  
- Platsen är i återställnings läge  
- Platsen är i uppgraderings läge  

Meddelanden följer behörigheterna för rollbaserad administration. Om en användare till exempel inte har behörighet att se Configuration Manager uppdateringar visas inte dessa meddelanden.

Vissa aviseringar har en relaterad åtgärd. Om konsol versionen till exempel inte matchar plats versionen väljer **du installera den nya konsol versionen**. Den här åtgärden startar konsol installations programmet.

Följande meddelanden är mest tillämpliga för den Technical Preview-grenen:  

- Utvärderings versionen är inom 30 dagar efter förfallo datum (varning): det aktuella datumet infaller inom 30 dagar från utvärderings versionens förfallo datum  
- Utvärderings versionen har upphört att gälla (kritiskt): det aktuella datumet infaller efter utvärderings versionens förfallo datum  
- Felaktig matchning av konsol version (kritisk): konsol versionen matchar inte plats versionen  
- Plats uppgradering är tillgänglig (varning): det finns ett nytt uppdaterings paket tillgängligt  

Mer information och fel söknings hjälp finns i filen **SmsAdminUI. log** på-konsol datorn. Som standard har logg filen följande sökväg: `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.


## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a>Instrument panel för dokumentation i konsolen

<!--3556019 FKA 1357546-->
Från och med Configuration Manager version 1902 finns det en noden **dokumentation** i den nya **Community** -arbetsytan. Den här noden innehåller uppdaterad information om Configuration Manager dokumentation och support artiklar. Den innehåller följande avsnitt:  

### <a name="product-documentation-library"></a>Produkt dokumentations bibliotek

- **Rekommenderat**: en manuellt granskad lista över viktiga artiklar.
- **Trends**: de mest populära artiklarna för den senaste månaden.
- **Nyligen uppdaterad**: artiklar som revideras den senaste månaden.

### <a name="support-articles"></a>Supportartiklar

- **Fel söknings artiklar**: guidade genom gångar som hjälper dig att felsöka Configuration Manager-komponenter och-funktioner.
- **Nya och uppdaterade support artiklar**: artiklar som är nya eller uppdaterade under de senaste två månaderna.

### <a name="troubleshooting-connection-errors"></a>Felsöka anslutnings fel
Noden **dokumentation** har ingen explicit proxykonfiguration. Den använder valfri OS-definierad proxy i **Internet alternativ** på kontroll panelen. Uppdatera noden **dokumentation** om du vill försöka igen efter ett anslutnings fel.


## <a name="command-line-options"></a>Kommandoradsalternativ

Configuration Manager-konsolen har följande kommando rads alternativ:

|Alternativ|Beskrivning|  
|------------|-----------------|  
|`/sms:debugview=1`|En DebugView ingår i alla ResultViews som anger en vy. DebugView visar RAW-egenskaper (namn och värden).|  
|`/sms:NamespaceView=1`|Visar namn områdes visning i-konsolen.|  
|`/sms:ResetSettings`|Konsolen ignorerar användarens sparade anslutningar och visar tillstånd. Fönster storleken har inte återställts.|  
|`/sms:IgnoreExtensions`|Inaktiverar eventuella Configuration Manager-tillägg.|  
|`/sms:NoRestore`|Konsolen ignorerar den tidigare sparade noden navigering.|  


## <a name="tips"></a>Tips

### <a name="general"></a>Allmänt

#### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a>Förbättringar av konsols ökning
<!--4640570-->
*(Lanseras i version 1910)*

- Du kan använda Sök alternativet **alla undermappar** i noderna **driv rutins paket** och **frågor** .<!--2841181,5424892--> Från och med version 2002 använder du även det här alternativet från noderna **konfigurations objekt** och **konfigurations bas linjer** .<!--5891241-->

- När en sökning returnerar fler än 1 000 resultat väljer du knappen **OK** i meddelande fältet för att visa fler resultat.<!--4640570-->

    ![Skärm bild av meddelande fältet för för många Sök Resultat](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > Standard gränsen för Sök resultat är 1 000. Du kan ändra det här standardvärdet. I Configuration Manager-konsolen går du till fliken **Sök** i menyfliksområdet. I gruppen **alternativ** väljer du **Sök inställningar**. Ändra värdet för **Sök Resultat** . Det kan ta längre tid att visa ett stort antal Sök resultat.
    >
    > Som standard är den övre maximala gränsen 100 000. Om du vill ändra den här gränsen ställer du in DWORD-värdet **QueryResultCountMaximum** i följande register nyckel:
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > Inställningen i konsolen motsvarar **QueryResultCountLimit** -värdet i samma nyckel. En administratör kan konfigurera dessa värden i HKLM Hive för alla användare av enheten. Värdet för HKCU åsidosätter inställningen HKLM.

#### <a name="role-based-administration-for-folders"></a>Rollbaserad administration för mappar
<!--3600867-->
*(Lanseras i version 1906)*

Du kan ange säkerhets omfattningar för mappar. Om du har åtkomst till ett objekt i mappen men inte har åtkomst till mappen kan du inte se objektet. Om du har åtkomst till en mapp men inte ett objekt i den, ser du inte det objektet. Högerklicka på en mapp, Välj **Ange säkerhets omfattningar**och välj sedan de säkerhets omfattningar som du vill använda.

#### <a name="views-sort-by-integer-values"></a>Vyer sortera efter heltals värden

*(Lanseras i version 1902)*

Vi har gjort förbättringar av hur olika vyer sorterar data. I noden **distributioner** på arbets ytan **övervakning** sorteras till exempel följande kolumner som tal i stället för sträng värden:  

- Antal fel
- Antal pågående
- Tal, övrigt
- Antal lyckade
- Okänd siffra  

#### <a name="move-the-warning-for-a-large-number-of-results"></a>Flytta varningen för ett stort antal resultat

*(Lanseras i version 1902)*

När du väljer en nod i konsolen som returnerar fler än 1 000 resultat visas följande varning i Configuration Manager:

> Configuration Manager returnerade ett stort antal resultat. Du kan begränsa resultaten med hjälp av Sök funktionen. Eller klicka här för att visa högst 100000 resultat.

Det finns nu ytterligare tomt utrymme mellan den här varningen och Sök fältet. Den här flytten hjälper till att förhindra oavsiktligt att välja varningen för att visa fler resultat.

#### <a name="send-feedback"></a>Skicka feedback

*(Lanseras i version 1806)*
<!--1357542-->

Skicka in produkt information från-konsolen.  

- **Skicka ett leende**: skicka feedback om vad du gillade  

- **Skicka en bister min**: skicka feedback om vad du inte gillade  

- **Skicka ett förslag**: tar dig till UserVoice för att dela din idé  

Mer information finns i [produkt feedback](../../understand/find-help.md#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Arbets ytan till gångar och efterlevnad

#### <a name="real-time-actions-from-device-lists"></a>Real tids åtgärder från enhets listor
<!--4616810-->
*(Lanseras i version 1906)*

Det finns olika sätt att visa en lista över enheter under noden **enheter** på arbets ytan **till gångar och efterlevnad** .

- I arbets ytan **till gångar och efterlevnad** väljer du noden **enhets samlingar** . Välj en enhets samling och välj sedan åtgärden för att **Visa medlemmar**. Den här åtgärden öppnar en undernoder till noden **enheter** med en enhets lista för samlingen.  

  - När du väljer undernoden samling kan du nu starta **CMPivot** från samlings gruppen i menyfliksområdet.  

- I arbets ytan **övervakning** väljer du noden **distributioner** . Välj en distribution och Välj åtgärden **Visa status** i menyfliksområdet. I fönstret distributions status dubbelklickar du på den totala till gångar som du vill gå igenom till en enhets lista.  

  - När du väljer en enhet i listan kan du nu starta **CMPivot** och **köra skript** från enhets gruppen i menyfliksområdet.  


#### <a name="collections-tab-in-devices-node"></a>Fliken samlingar i noden enheter
<!--4616810-->
*(Lanseras i version 1906)*

Gå till noden **enheter** på arbets ytan **till gångar och efterlevnad** och välj en enhet. I informations fönstret växlar du till fliken nya **samlingar** . Den här fliken visar de samlingar som innehåller den här enheten. 

> [!Note]  
> - Den här fliken är för närvarande inte tillgänglig från en undernoden enheter under noden **enhets samlingar** . Till exempel när du väljer alternativet för att **Visa medlemmar** i en samling.
> - Den här fliken kanske inte är ifylld som förväntat för vissa användare. Om du vill se en fullständig lista över samlingar som en enhet tillhör måste du ha säkerhets rollen **Fullständig administratör** . Detta är ett känt problem. <!--5107309--> <!--5107309-->


#### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Lägg till SMBIOS GUID-kolumn till noder i enhet och enhets samling

*(Lanseras i version 1906)*

<!--4526580-->
I båda noderna **enheter** och **enhets samlingar** kan du nu lägga till en ny kolumn för **SMBIOS GUID**. Värdet är samma som egenskapen för **BIOS-GUID** för system resurs klassen. Det är en unik identifierare för enhetens maskin vara.

#### <a name="search-device-views-using-mac-address"></a>Sök i enhets visningar med MAC-adress

<!--3600878-->
*(Lanseras i version 1902)*

Du kan söka efter en MAC-adress i en enhets vy i Configuration Manager-konsolen. Den här egenskapen är användbar för distributions administratörer för operativ system medan PXE-baserade distributioner felsöks. När du visar en lista över enheter, lägger du till kolumnen **MAC-adress** i vyn. Använd Sök fältet för att lägga till Sök kriterierna för **MAC-adressen** .

#### <a name="view-users-for-a-device"></a>Visa användare för en enhet

Från och med version 1806 är följande kolumner tillgängliga i noden **enheter** :  

- **Primära användare** <!--1357280-->  

- **Användare som är inloggad** <!--1358202-->  

    > [!NOTE]  
    > För den inloggade användaren krävs [användar identifiering](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) och [mappning mellan användare och enhet](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Mer information om hur du visar en kolumn som inte är standard finns i [kolumner](#columns).

#### <a name="improvement-to-device-search-performance"></a>Förbättra prestanda för enhets sökning

<!-- 3614690 -->
Från och med version 1806 söker den inte igenom nyckelordet mot alla objekt egenskaper vid sökning i en enhets samling. När du inte är mer information om vad du ska söka efter söker den igenom följande fyra egenskaper:

- Name
- Primära användare
- Användare som är inloggad
- Senaste användar namn för inloggning

Det här beteendet ökar avsevärt tiden det tar att söka efter namn, särskilt i en stor miljö. Anpassade sökningar efter vissa kriterier påverkas inte av den här ändringen.


### <a name="software-library-workspace"></a>Arbets ytan program varu bibliotek

#### <a name="order-by-program-name-in-task-sequence"></a>Sortera efter program namn i aktivitetssekvens
<!--4616810-->
*(Lanseras i version 1906)*

I arbets ytan **program bibliotek** expanderar du **operativ system**och väljer noden **aktivitetssekvenser** . Redigera en aktivitetssekvens och markera eller Lägg till steget [installera paket](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) . Om ett paket har fler än ett program, sorterar List rutan nu programmen i alfabetisk ordning.

#### <a name="task-sequences-tab-in-applications-node"></a>Fliken aktivitetssekvenser i noden program
<!--4616810-->
*(Lanseras i version 1906)*

I arbets ytan **program bibliotek** expanderar du **program hantering**, går till noden **program** och väljer ett program. I informations fönstret växlar du till fliken nya **aktivitetssekvenser** . Den här fliken listar de aktivitetssekvenser som refererar till det här programmet.

#### <a name="drill-through-required-updates"></a>Granska nödvändiga uppdateringar
<!--4224414-->
*(Lanseras i version 1906)*

1. Gå till någon av följande platser i Configuration Manager-konsolen:

   - **Program varu bibliotek** > **program uppdateringar** > **alla program uppdateringar**
   - **Program varu bibliotek** > **Windows 10 Underhåll** > **alla Windows 10-uppdateringar**
   - **Program varu bibliotek** > **kontor 365 klient hantering** > **Office 365 uppdateringar**

1. Välj en uppdatering som krävs av minst en enhet.
1. Titta på fliken **Sammanfattning** och hitta cirkel diagrammet under **statistik**.
1. Välj hyperlänken **vy som krävs** bredvid cirkel diagrammet för att öka detalj nivån i enhets listan.
1. Den här åtgärden tar dig till en tillfällig nod under **enheter** där du kan se vilka enheter som kräver uppdateringen. Du kan också utföra åtgärder för noden, till exempel skapa en ny samling från listan.

> [!NOTE]
> Från och med den 21 april 2020 kommer Office 365 ProPlus att byta namn till **Microsoft 365 appar för företag**. Mer information finns i [namn ändring för Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Du kan fortfarande se referenser till det gamla namnet i Configuration Manager-konsolen och stöd dokumentationen medan-konsolen uppdateras.

#### <a name="maximize-the-browse-registry-window"></a>Maximera fönstret bläddra i registret

<!--3594151 includes all MMS 1902 console changes-->
*(Lanseras i version 1902)*

1. I arbets ytan **program bibliotek** expanderar du **program hantering**och väljer noden **program** .
1. Välj ett program som har en distributions typ med en identifierings metod. Till exempel en Windows Installer identifierings metod.
1. I informations fönstret växlar du till fliken **distributions typer** .
1. Öppna egenskaperna för en distributions typ och växla till fliken **identifierings metod** . Välj **Lägg till sats**.
1. Ändra **inställnings typ** till **register** och välj **Bläddra** för att öppna fönstret **Bläddra i registret** . Nu kan du maximera det här fönstret.  

#### <a name="edit-a-task-sequence-by-default"></a>Redigera en aktivitetssekvens som standard

*(Lanseras i version 1902)*

I arbets ytan **program bibliotek** expanderar du **operativ system**och väljer noden **aktivitetssekvenser** . **Redigera** är nu standard åtgärden när du öppnar en aktivitetssekvens. Tidigare var standard åtgärden **Egenskaper**.  

#### <a name="go-to-the-collection-from-an-application-deployment"></a>Gå till samlingen från en program distribution

*(Lanseras i version 1902)*

1. I arbets ytan **program bibliotek** expanderar du **program hantering**och väljer noden **program** .
1. Välj ett program. I informations fönstret växlar du till fliken **distributioner** .
1. Välj en distribution och välj sedan alternativet ny **samling** i menyfliksområdet på fliken distribution. Den här åtgärden växlar vyn till den samling som är målet för distributionen.
   - Den här åtgärden är också tillgänglig från snabb menyn för snabb klickning i distributionen i den här vyn.


### <a name="monitoring-workspace"></a>Arbets ytan övervakning

#### <a name="correct-names-for-client-operations"></a>Korrekta namn för klient åtgärder
<!--4616810-->
*(Lanseras i version 1906)*

I arbets ytan **övervakning** väljer du **klient åtgärder**. Åtgärden att **byta till nästa program uppdaterings plats** har nu rätt namn.

#### <a name="show-collection-name-for-scripts"></a>Visa samlings namn för skript
<!--4616810-->
*(Lanseras i version 1906)*

I arbets ytan **övervakning** väljer du noden **skript status** . Nu visas **samlings namnet** förutom ID: t.

#### <a name="remove-content-from-monitoring-status"></a>Ta bort innehåll från övervaknings status

*(Lanseras i version 1902)*

1. I arbets ytan **övervakning** expanderar du **distributions status**och väljer **innehålls status**.
1. Markera ett objekt i listan och välj alternativet **Visa status** i menyfliksområdet.
1. I fönstret till gångs information högerklickar du på en distributions plats och väljer det nya alternativet **ta bort**. Den här åtgärden tar bort det här innehållet från den valda distributions platsen.

#### <a name="copy-details-in-monitoring-views"></a>Kopiera information i övervaknings vyer

*(Lanseras i version 1806)*
<!--1357856-->
Kopiera information från fönstret **till gångs information** för följande övervaknings noder:  

- **Status för innehålls distribution**  

- **Distributions status**  

![Vyn distributions status, kopiera till gångs information](media/1810-deployment-status.PNG)

### <a name="administration-workspace"></a>Arbets ytan administration

<!--4223683-->
Från och med version 1906 kan du aktivera vissa noder under noden **säkerhet** om du vill använda administrations tjänsten. Den här ändringen gör att konsolen kan kommunicera med SMS-providern via HTTPS i stället för via WMI. Mer information finns i [Konfigurera administrations tjänsten](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Nästa steg

[Hjälpmedelsfunktioner](../../understand/accessibility-features.md)

[Redigeraren för aktivitetssekvens](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
