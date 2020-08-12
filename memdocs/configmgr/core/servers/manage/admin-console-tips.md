---
title: Configuration Manager-konsolens ändringar och tips
titleSuffix: Configuration Manager
description: Lär dig mer om ändringar i Configuration Manager-konsolen och tips om hur du använder den.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 2162d67d-31a9-45b2-bb9e-835f3ac6e6fe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7f46c283bd533d67387ab0abac35e7625438addc
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129698"
---
# <a name="configuration-manager-console-changes-and-tips"></a>Configuration Manager-konsolens ändringar och tips

*Gäller för: Configuration Manager (aktuell gren)*

Använd informationen nedan om du vill veta mer om ändringar i Configuration Manager-konsolen och tips om hur du använder-konsolen:

## <a name="general-tips"></a>Allmänna tips

### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a>Förbättringar av konsols ökning
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

### <a name="role-based-administration-for-folders"></a>Rollbaserad administration för mappar
<!--3600867-->
*(Lanseras i version 1906)*

Du kan ange säkerhets omfattningar för mappar. Om du har åtkomst till ett objekt i mappen men inte har åtkomst till mappen kan du inte se objektet. Om du har åtkomst till en mapp men inte ett objekt i den, ser du inte det objektet. Högerklicka på en mapp, Välj **Ange säkerhets omfattningar**och välj sedan de säkerhets omfattningar som du vill använda.

### <a name="views-sort-by-integer-values"></a>Vyer sortera efter heltals värden

*(Lanseras i version 1902)*

Vi har gjort förbättringar av hur olika vyer sorterar data. I noden **distributioner** på arbets ytan **övervakning** sorteras till exempel följande kolumner som tal i stället för sträng värden:  

- Antal fel
- Antal pågående
- Tal, övrigt
- Antal lyckade
- Okänd siffra  

### <a name="move-the-warning-for-a-large-number-of-results"></a>Flytta varningen för ett stort antal resultat

*(Lanseras i version 1902)*

När du väljer en nod i konsolen som returnerar fler än 1 000 resultat visas följande varning i Configuration Manager:

> Configuration Manager returnerade ett stort antal resultat. Du kan begränsa resultaten med hjälp av Sök funktionen. Eller klicka här för att visa högst 100000 resultat.

Det finns nu ytterligare tomt utrymme mellan den här varningen och Sök fältet. Den här flytten hjälper till att förhindra oavsiktligt att välja varningen för att visa fler resultat.

### <a name="send-feedback"></a>Skicka feedback

*(Lanseras i version 1806)*
<!--1357542-->

Skicka in produkt information från-konsolen.  

- **Skicka ett leende**: skicka feedback om vad du gillade  

- **Skicka en bister min**: skicka feedback om vad du inte gillade  

- **Skicka ett förslag**: tar dig till UserVoice för att dela din idé  

Mer information finns i [produkt feedback](../../understand/find-help.md#BKMK_1806Feedback).


## <a name="assets-and-compliance-workspace"></a>Arbets ytan till gångar och efterlevnad

### <a name="real-time-actions-from-device-lists"></a>Real tids åtgärder från enhets listor
<!--4616810-->
*(Lanseras i version 1906)*

Det finns olika sätt att visa en lista över enheter under noden **enheter** på arbets ytan **till gångar och efterlevnad** .

- I arbets ytan **till gångar och efterlevnad** väljer du noden **enhets samlingar** . Välj en enhets samling och välj sedan åtgärden för att **Visa medlemmar**. Den här åtgärden öppnar en undernoder till noden **enheter** med en enhets lista för samlingen.  

  - När du väljer undernoden samling kan du nu starta **CMPivot** från samlings gruppen i menyfliksområdet.  

- I arbets ytan **övervakning** väljer du noden **distributioner** . Välj en distribution och Välj åtgärden **Visa status** i menyfliksområdet. I fönstret distributions status dubbelklickar du på den totala till gångar som du vill gå igenom till en enhets lista.  

  - När du väljer en enhet i listan kan du nu starta **CMPivot** och **köra skript** från enhets gruppen i menyfliksområdet.  


### <a name="collections-tab-in-devices-node"></a>Fliken samlingar i noden enheter
<!--4616810-->
*(Lanseras i version 1906)*

Gå till noden **enheter** på arbets ytan **till gångar och efterlevnad** och välj en enhet. I informations fönstret växlar du till fliken nya **samlingar** . Den här fliken visar de samlingar som innehåller den här enheten. 

> [!Note]  
> - Den här fliken är för närvarande inte tillgänglig från en undernoden enheter under noden **enhets samlingar** . Till exempel när du väljer alternativet för att **Visa medlemmar** i en samling.
> - Den här fliken kanske inte är ifylld som förväntat för vissa användare. Om du vill se en fullständig lista över samlingar som en enhet tillhör måste du ha säkerhets rollen **Fullständig administratör** . Detta är ett känt problem. <!--5107309--> <!--5107309-->


### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Lägg till SMBIOS GUID-kolumn till noder i enhet och enhets samling

*(Lanseras i version 1906)*

<!--4526580-->
I båda noderna **enheter** och **enhets samlingar** kan du nu lägga till en ny kolumn för **SMBIOS GUID**. Värdet är samma som egenskapen för **BIOS-GUID** för system resurs klassen. Det är en unik identifierare för enhetens maskin vara.

### <a name="search-device-views-using-mac-address"></a>Sök i enhets visningar med MAC-adress

<!--3600878-->
*(Lanseras i version 1902)*

Du kan söka efter en MAC-adress i en enhets vy i Configuration Manager-konsolen. Den här egenskapen är användbar för distributions administratörer för operativ system medan PXE-baserade distributioner felsöks. När du visar en lista över enheter, lägger du till kolumnen **MAC-adress** i vyn. Använd Sök fältet för att lägga till Sök kriterierna för **MAC-adressen** .

### <a name="view-users-for-a-device"></a>Visa användare för en enhet

Från och med version 1806 är följande kolumner tillgängliga i noden **enheter** :  

- **Primära användare** <!--1357280-->  

- **Användare som är inloggad** <!--1358202-->  

    > [!NOTE]  
    > För den inloggade användaren krävs [användar identifiering](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) och [mappning mellan användare och enhet](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Mer information om hur du visar en kolumn som inte är standard finns i [använda administratörs konsolen](admin-console.md#columns).

### <a name="improvement-to-device-search-performance"></a>Förbättra prestanda för enhets sökning

<!-- 3614690 -->
Från och med version 1806 söker den inte igenom nyckelordet mot alla objekt egenskaper vid sökning i en enhets samling. När du inte är mer information om vad du ska söka efter söker den igenom följande fyra egenskaper:

- Name
- Primära användare
- Användare som är inloggad
- Senaste användar namn för inloggning

Det här beteendet ökar avsevärt tiden det tar att söka efter namn, särskilt i en stor miljö. Anpassade sökningar efter vissa kriterier påverkas inte av den här ändringen.


## <a name="software-library-workspace"></a>Arbets ytan program varu bibliotek

### <a name="order-by-program-name-in-task-sequence"></a>Sortera efter program namn i aktivitetssekvens
<!--4616810-->
*(Lanseras i version 1906)*

I arbets ytan **program bibliotek** expanderar du **operativ system**och väljer noden **aktivitetssekvenser** . Redigera en aktivitetssekvens och markera eller Lägg till steget [installera paket](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) . Om ett paket har fler än ett program, sorterar List rutan nu programmen i alfabetisk ordning.

### <a name="task-sequences-tab-in-applications-node"></a>Fliken aktivitetssekvenser i noden program
<!--4616810-->
*(Lanseras i version 1906)*

I arbets ytan **program bibliotek** expanderar du **program hantering**, går till noden **program** och väljer ett program. I informations fönstret växlar du till fliken nya **aktivitetssekvenser** . Den här fliken listar de aktivitetssekvenser som refererar till det här programmet.

### <a name="drill-through-required-updates"></a>Granska nödvändiga uppdateringar
<!--4224414-->
*(Lanseras i version 1906)*

1. Gå till någon av följande platser i Configuration Manager-konsolen:

   - **Program varu bibliotek**  >  **Program uppdateringar**  >  **Alla program uppdateringar**
   - **Program varu bibliotek**  >  **Windows 10-Underhåll**  >  **Alla Windows 10-uppdateringar**
   - **Program varu bibliotek**  >  **Office 365-klient hantering**  >  **Office 365-uppdateringar**

1. Välj en uppdatering som krävs av minst en enhet.
1. Titta på fliken **Sammanfattning** och hitta cirkel diagrammet under **statistik**.
1. Välj hyperlänken **vy som krävs** bredvid cirkel diagrammet för att öka detalj nivån i enhets listan.
1. Den här åtgärden tar dig till en tillfällig nod under **enheter** där du kan se vilka enheter som kräver uppdateringen. Du kan också utföra åtgärder för noden, till exempel skapa en ny samling från listan.

> [!NOTE]
> Från och med den 21 april 2020 kommer Office 365 ProPlus att byta namn till **Microsoft 365 appar för företag**. Mer information finns i [namn ändring för Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Du kan fortfarande se referenser till det gamla namnet i Configuration Manager-konsolen och stöd dokumentationen medan-konsolen uppdateras.

### <a name="maximize-the-browse-registry-window"></a>Maximera fönstret bläddra i registret

<!--3594151 includes all MMS 1902 console changes-->
*(Lanseras i version 1902)*

1. I arbets ytan **program bibliotek** expanderar du **program hantering**och väljer noden **program** .
1. Välj ett program som har en distributions typ med en identifierings metod. Till exempel en Windows Installer identifierings metod.
1. I informations fönstret växlar du till fliken **distributions typer** .
1. Öppna egenskaperna för en distributions typ och växla till fliken **identifierings metod** . Välj **Lägg till sats**.
1. Ändra **inställnings typ** till **register** och välj **Bläddra** för att öppna fönstret **Bläddra i registret** . Nu kan du maximera det här fönstret.  

### <a name="edit-a-task-sequence-by-default"></a>Redigera en aktivitetssekvens som standard

*(Lanseras i version 1902)*

I arbets ytan **program bibliotek** expanderar du **operativ system**och väljer noden **aktivitetssekvenser** . **Redigera** är nu standard åtgärden när du öppnar en aktivitetssekvens. Tidigare var standard åtgärden **Egenskaper**.  

### <a name="go-to-the-collection-from-an-application-deployment"></a>Gå till samlingen från en program distribution

*(Lanseras i version 1902)*

1. I arbets ytan **program bibliotek** expanderar du **program hantering**och väljer noden **program** .
1. Välj ett program. I informations fönstret växlar du till fliken **distributioner** .
1. Välj en distribution och välj sedan alternativet ny **samling** i menyfliksområdet på fliken distribution. Den här åtgärden växlar vyn till den samling som är målet för distributionen.
   - Den här åtgärden är också tillgänglig från snabb menyn för snabb klickning i distributionen i den här vyn.


## <a name="monitoring-workspace"></a>Arbets ytan övervakning

### <a name="correct-names-for-client-operations"></a>Korrekta namn för klient åtgärder
<!--4616810-->
*(Lanseras i version 1906)*

I arbets ytan **övervakning** väljer du **klient åtgärder**. Åtgärden att **byta till nästa program uppdaterings plats** har nu rätt namn.

### <a name="show-collection-name-for-scripts"></a>Visa samlings namn för skript
<!--4616810-->
*(Lanseras i version 1906)*

I arbets ytan **övervakning** väljer du noden **skript status** . Nu visas **samlings namnet** förutom ID: t.

### <a name="remove-content-from-monitoring-status"></a>Ta bort innehåll från övervaknings status

*(Lanseras i version 1902)*

1. I arbets ytan **övervakning** expanderar du **distributions status**och väljer **innehålls status**.
1. Markera ett objekt i listan och välj alternativet **Visa status** i menyfliksområdet.
1. I fönstret till gångs information högerklickar du på en distributions plats och väljer det nya alternativet **ta bort**. Den här åtgärden tar bort det här innehållet från den valda distributions platsen.

### <a name="copy-details-in-monitoring-views"></a>Kopiera information i övervaknings vyer

*(Lanseras i version 1806)*
<!--1357856-->
Kopiera information från fönstret **till gångs information** för följande övervaknings noder:  

- **Status för innehålls distribution**  

- **Distributions status**  

![Vyn distributions status, kopiera till gångs information](media/1810-deployment-status.PNG)

## <a name="administration-workspace"></a>Arbets ytan administration

<!--4223683-->
Från och med version 1906 kan du aktivera vissa noder under noden **säkerhet** om du vill använda administrations tjänsten. Den här ändringen gör att konsolen kan kommunicera med SMS-providern via HTTPS i stället för via WMI. Mer information finns i [Konfigurera administrations tjänsten](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Nästa steg

- [Använda konsolen](admin-console.md)
- [Konsol meddelanden](admin-console-notifications.md)
- [Hjälpmedelsfunktioner](../../understand/accessibility-features.md)