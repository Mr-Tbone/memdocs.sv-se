---
title: Configuration Manager-konsolen
titleSuffix: Configuration Manager
description: Lär dig mer om att navigera i Configuration Manager-konsolen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcc1f8e93f4fb312b74fd7e5746928182b05710f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126518"
---
# <a name="how-to-use-the-configuration-manager-console"></a>Använda Configuration Manager-konsolen

*Gäller för: Configuration Manager (aktuell gren)*

Administratörer använder Configuration Manager-konsolen för att hantera Configuration Managers miljön. Den här artikeln beskriver grunderna i att navigera i-konsolen.  

## <a name="open-the-console"></a><a name="bkmk_open"></a>Öppna-konsolen

Configuration Manager-konsolen installeras alltid på varje plats Server. Du kan också installera det på andra datorer. Mer information finns i [installera Configuration Manager-konsolen](../deploy/install/install-consoles.md).

Den enklaste metoden för att öppna-konsolen på en Windows 10-dator, tryck på **Start** och börja skriva `Configuration Manager console` . Du kanske inte behöver ange hela strängen för Windows för att hitta den bästa matchningen.

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

### <a name="prerequisites"></a>Förutsättningar

- För att starta en chatt med en administratör måste det konto som du vill chatta med ha identifierats med [Azure AD eller AD User Discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Microsoft Teams installerat på den enhet från vilken du kör-konsolen.
anteckning
- Alla [krav för att Visa anslutna konsoler](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>Starta Microsoft Teams Chat

1. Gå till **Administration**  >  **säkerhets**  >  **konsol anslutningar**.
1. Högerklicka på en användares konsol anslutning och välj **Starta Microsoft Teams Chat**.
    - Om användarens huvud namn inte hittas för den valda administratören, är det bara att **Starta Microsoft Teams Chat** .
    - Ett fel meddelande, inklusive en nedladdnings länk, visas om Microsoft Teams inte är installerat på den enhet från vilken du kör-konsolen.
    - Om Microsoft Teams är installerat på den enhet där du kör-konsolen öppnas en chatt med användaren.

### <a name="known-issues"></a>Kända problem

Fel meddelandet som meddelar att Microsoft Teams inte är installerat visas inte om följande register nyckel inte finns:

Dator \ HKEY_CURRENT_USER \SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Du kan lösa problemet genom att manuellt skapa register nyckeln.

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


## <a name="next-steps"></a>Nästa steg

- [Konsol meddelanden](admin-console-notifications.md)
- [Konsol tips](admin-console-tips.md)
- [Hjälpmedelsfunktioner](../../understand/accessibility-features.md)
- [Redigeraren för aktivitetssekvens](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
