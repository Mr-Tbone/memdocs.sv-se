---
title: Instrument panel för Office 365-klient hantering
titleSuffix: Configuration Manager
description: Granska Microsoft 365 Apps klient information från instrument panelen för Office 365-klient hantering
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.openlocfilehash: ce3947c8ca3c562869fdfed2ddba4d9b160902be
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129406"
---
# <a name="office-365-client-management-dashboard"></a>Instrument panel för Office 365-klient hantering

*Gäller för: Configuration Manager (aktuell gren)*

> [!Note]
> Från och med den 21 april 2020 kommer Office 365 ProPlus att byta namn till **Microsoft 365 appar för företag**. Mer information finns i [namn ändring för Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Du kan fortfarande se referenser till det gamla namnet i Configuration Manager-konsolen och stöd dokumentationen medan-konsolen uppdateras.

Från och med Configuration Manager version 1802 kan du granska Microsoft 365 Apps-klient information från instrument panelen för klient hantering i Office 365. Instrument panelen för Office 365-klient hantering visar en lista över relevanta enheter när diagram avsnitt har marker ATS. <!--1357281 -->

## <a name="prerequisites"></a>Förutsättningar

### <a name="enable-hardware-inventory"></a>Aktivera maskinvaruinventering

De data som visas på instrument panelen för Office 365-klient hantering kommer från maskin varu inventeringen. Aktivera maskin varu inventering och välj maskin varu inventerings klassen för **Office 365 ProPlus konfigurationer** för data som ska visas i instrument panelen.
 
1. Aktivera maskin varu inventering om den inte redan är aktive rad. Mer information finns i [Konfigurera maskin varu inventering](../../core/clients/manage/inventory/configure-hardware-inventory.md).
2. I Configuration Manager-konsolen navigerar du till **Administration**  >  **klient inställningar**  >  **standard klient inställningar**.  
3. På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  
4. I dialogrutan **Inställningar för standardklient** klickar du på **Maskinvaruinventering**.  
5. I listan **Enhetsinställningar** klickar du på **Ange klasser**.  
6. I dialog rutan **maskin varu lager klasser** väljer du **Office 365 ProPlus-konfigurationer**.  
7. Klicka på **OK** för att spara ändringarna och stänga dialogrutan **Maskinvarulagerklasser** .

Instrument panelen för Office 365-klient hantering börjar visa data som maskin varu inventering rapporteras.

### <a name="connectivity-for-top-level-site-server"></a>Anslutning för plats Server på den högsta nivån

*(Lanseras i version 1906 som ett krav)*

Plats servern på den högsta nivån måste ha åtkomst till följande slut punkt för att kunna hämta beredskaps filen:

`https://contentstorage.osi.office.net/sccmreadinessppe/sot_sccm_addinreadiness.cab`

> [!NOTE]
> Ingen Internet anslutning krävs för klient enheterna för något av dessa scenarier.

### <a name="enable-data-collection-for-microsoft-365-apps"></a>Aktivera data insamling för Microsoft 365 appar

*(Lanseras i version 1910 som ett krav)*

Från och med version 1910 måste du aktivera data insamling för Microsoft 365 appar för att fylla i informationen i **instrument panelen för Office 365 ProPlus pilot och hälso tillstånd**. Data lagras i Configuration Manager plats databasen och skickas inte till Microsoft.

Dessa data skiljer sig från diagnostikdata, som beskrivs i [diagnostikdata som skickas från Microsoft 365-appar till Microsoft](https://docs.microsoft.com/deployoffice/privacy/overview-privacy-controls#diagnostic-data-sent-from-office-365-proplus-to-microsoft).

Du kan aktivera data insamling antingen med hjälp av grupprincip eller genom att redigera registret.

#### <a name="enable-data-collection-from-group-policy"></a>Aktivera data insamling från grupprincip

1. Hämta de senaste [administrativa mallarna från Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49030).
2. Aktivera princip inställningen Aktivera **telemetri för data insamling** under `User Configuration\Policies\Administrative Templates\Microsoft Office 2016\Telemetry Dashboard` .
    - Du kan också använda princip inställningen med [Office Cloud policy service](https://docs.microsoft.com/DeployOffice/overview-office-cloud-policy-service).
    - Princip inställningen används också av instrument panelen för Office-telemetri, som du inte behöver distribuera för den här data insamlingen.

#### <a name="enable-data-collection-from-the-registry"></a>Aktivera data insamling från registret

Kommandot nedan är ett exempel på hur du aktiverar data insamlingen från registret:

```cmd
reg add HKCU\Software\Policies\Microsoft\office\16.0\OSM /v EnableLogging /t REG_DWORD /d 1
```

## <a name="viewing-the-office-365-client-management-dashboard"></a>Visa instrument panelen för Office 365-klient hantering

Om du vill visa instrument panelen för Office 365-klient hantering i Configuration Manager-konsolen går du till **program bibliotek**  >  **Översikt**  >  **kontor 365 klient hantering**. Överst på instrument panelen använder du List rutan **samling** för att filtrera instrument panels data efter medlemmar i en angiven samling. Från och med Configuration Manager version 1802 visar instrument panelen en lista över relevanta enheter när diagram avsnitt har marker ATS.

Instrument panelen för Office 365-klient hantering innehåller diagram med följande information:

- Antal Microsoft 365 Apps-klienter
- Versioner av Microsoft 365 Apps-klienter
- Microsoft 365 klient språk för appar
- Microsoft 365 Apps klient kanaler mer information finns i [Översikt över uppdaterings kanaler för Microsoft 365 appar](/DeployOffice/overview-of-update-channels-for-office-365-proplus).


## <a name="integration-for-microsoft-365-apps-readiness"></a><a name="bkmk_o365_readiness"></a>Integrering av beredskap för Microsoft 365 Apps
<!--3735402-->
Från och med Configuration Manager version 1902 kan du använda instrument panelen för att identifiera enheter med hög exakthet som är klara att uppgraderas till Microsoft 365 appar. Den här integrationen ger insikter om potentiella kompatibilitetsproblem med tillägg och makron i din miljö. Använd sedan Configuration Manager för att distribuera Microsoft 365 appar till klara enheter.

Instrument panelen för Office 365-klient hantering innehåller en ny panel, **Office 365 ProPlus uppgraderingsberedskap**. Den här panelen är ett stapeldiagram med enheter i följande tillstånd:
- Ej utvärderat
- Redo för uppgradering
- Kräver granskning

Välj ett tillstånd att gå igenom till en enhets lista. Den här beredskap rapporten innehåller mer information om enheter. Den innehåller kolumner för kompatibilitetsläget för både tillägg och makron.

### <a name="prerequisites-for-microsoft-365-apps-readiness-integration"></a>Krav för integration av Microsoft 365 Apps-beredskap

- Aktivera maskin varu inventering i klient inställningar. Mer information finns i avsnittet [krav](#prerequisites) .  

- Enheten behöver anslutning till Office Content Delivery Network (CDN) för att kunna hämta en tilläggs fil. Mer information finns i [nätverk för innehålls leverans](https://docs.microsoft.com/office365/enterprise/content-delivery-networks). Om enheten inte kan ladda ned den här filen måste tilläggets tillstånd *granskas*.  

    > [!Note]  
    > Inga data skickas till Microsoft för den här funktionen.  

### <a name="detailed-macro-readiness"></a><a name="bkmk_ort"></a>Detaljerad makro beredskap

Som standard tittar skannings agenten på listan över senast använda filer (MRU) på varje enhet. Den räknar filerna i den här listan som stöder makron. Dessa filer innehåller följande typer:
- Makroaktiverade Office-filformat, till exempel Excel-makroaktiverade arbets böcker (. xlsm) eller Word-Makroaktiverat dokument (. docm)  
- Äldre Office-format som inte anger om det finns makro innehåll. Till exempel en Excel 97-2003-arbets bok (. xls).

Om du behöver mer detaljerad information om makro kompatibilitet distribuerar du **readiness Toolkit för Office** för att analysera koden i makro filerna. Det kontrollerar om det finns möjliga kompatibilitetsproblem. Till exempel använder filen en funktion som har ändrats i en senare version av Office. När du har kört readiness Toolkit för Office och valt alternativet för **de senast använda Office-dokumenten och installerade tillägg på den här datorn**, eller om du använder `-mru` flaggan på kommando raden, kan resultaten hämtas av Configuration Manager maskin varu inventerings agenten. Dessa ytterligare data förbättrar beräkningen av enhets beredskap. Mer information finns i [använda readiness Toolkit för Office för att utvärdera programkompatibilitet för Microsoft 365 appar](https://aka.ms/readinesstoolkit).

Observera att readiness Toolkit inte behöver installeras på varje mål enhet för att kunna genomföra genomsökningen. Du kan använda exempel kommando rads alternativet nedan om du vill söka igenom varje enhet som önskas.  Utmatnings flaggan krävs, men filerna kommer inte att användas för att generera resultaten i instrument panelen, så att alla giltiga platser kan väljas.

```cmd
ReadinessReportCreator.exe -mru -output c:\temp -silent
```

Mer information finns i [Hämta beredskaps information för flera användare i ett företag](/deployoffice/use-the-readiness-toolkit-to-assess-application-compatibility-for-office-365-pro#getting-readiness-information-for-multiple-users-in-an-enterprise).

## <a name="microsoft-365-apps-readiness-dashboard"></a><a name="bkmk_readiness-dash"></a>Instrument panel för Microsoft 365 Apps-beredskap

*(Lanseras i version 1906)*

<!--4021125-->
För att hjälpa dig att avgöra vilka enheter som är redo att uppgradera till Microsoft 365-appar, finns det en instrument panel för beredskap som börjar i version 1906. Den innehåller panelen **Office 365 ProPlus Upgrade readiness** som släpptes i Configuration Manager aktuella gren versionen 1902. Följande nya paneler på den här instrument panelen hjälper dig att utvärdera tillägg och makro beredskap:

- Distribution
- Enhets beredskap
- Beredskap för tillägg
- Tilläggs stöd-instruktioner
- Mest populära tillägg efter antal versioner
- Antal enheter som har makron
- Beredskap för makro
- Makro rådgivare

Följande video är en session med att antändning 2019, som innehåller mer information:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3090]

[Metod tips för kompatibilitetskontroll och Microsoft Office 365 ProPlus uppgraderingar med Office-beredskap i Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/79338?source=sessions)

### <a name="using-the-microsoft-365-apps-upgrade-readiness-dashboard"></a>Använda instrument panelen för uppgraderings beredskap för Microsoft 365 Apps

När du har verifierat [kraven](#prerequisites)kan du använda följande instruktioner för att använda instrument panelen:
 
1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **klient hantering för Office 365**.
1. Välj noden **Microsoft 365 appar uppgraderingsberedskap** .
1. Ändra **samlingen** och **mål kontorets arkitektur** för att ändra informationen som vidarebefordras på instrument panelen.

[![Instrument panel för uppgraderings beredskap för Microsoft 365 Apps](./media/4021125-office-365-upgrade-readiness-dashboard.png)](./media/4021125-office-365-upgrade-readiness-dashboard.png#lightbox)

[![Lägg till tillägg i instrument panel för uppgraderings beredskap för Microsoft 365 Apps](./media/4021125-office-365-to-add-ins.png)](./media/4021125-office-365-to-add-ins.png#lightbox)

[![Instrument panel för att uppgradera beredskap för Microsoft 365-appar](./media/4021125-office-365-macro-advisories.png)](./media/4021125-office-365-macro-advisories.png#lightbox)

### <a name="device-readiness-information"></a>Information om enhets beredskap

När tillägget och makrot inventeringen på varje enhet utvärderas grupperas enheterna sedan efter informationen. Enheter vars status är **klart att uppgradera** har troligen inte några kompatibilitetsproblem.

Om du väljer kategorin **klar att uppgradera** i diagrammet visas mer information om enheterna i den begränsande samlingen. Du kan granska enhets listan, göra val enligt dina affärs behov och skapa en ny enhets samling från ditt val. Använd den nya samlingen för att distribuera Microsoft 365 appar med Configuration Manager.

Enheter som kan vara utsatta för kompatibilitetsproblem markeras som **behovs granskning**. Dessa enheter kan behöva åtgärdas innan de kan uppgraderas till Microsoft 365 appar. Du kan till exempel uppdatera viktiga tillägg till en senare version.

### <a name="add-in-information"></a>Information om tillägg

 En inventering av alla installerade tillägg samlas in på varje enhet. Inventeringen jämförs sedan med den information som Microsoft har om tilläggets prestanda för Microsoft 365 appar. Om det finns ett tillägg som sannolikt kommer att orsaka problem efter uppgraderingen, är alla enheter med tillägget flaggade för granskning.

### <a name="macro-information"></a>Makro information

Configuration Manager tittar på de senast använda filerna på varje enhet. Den räknar filerna i den här listan som stöder makron, inklusive följande typer:

- Makroaktiverade Office-filformat.
- Äldre Office-format, som inte anger om det finns makro innehåll.

Den här rapporten kan användas för att identifiera vilka enheter som har nyligen använda filer som kan innehålla makron. **Readiness Toolkit för Office** kan sedan distribueras med hjälp av Configuration Manager för att genomsöka enheter där mer detaljerad information behövs och se om det finns några potentiella kompatibilitetsproblem. Till exempel om filen använder en funktion som har ändrats i en senare version av Microsoft 365 appar.

Mer information om hur du utför genomsökningen finns i [detaljerad makro beredskap](#bkmk_ort).

## <a name="office-365-proplus-pilot-and-health-dashboard"></a><a name="bkmk_pilot"></a>Instrument panel för Office 365 ProPlus pilot och hälso tillstånd
<!--4488272, 4488301-->
*(Lanseras i version 1910)*

Från och med version 1910 kan du planera, pilot och utföra distribution av Microsoft 365 appar med hjälp av **instrument panelen för Office 365 ProPlus pilot och hälso tillstånd** . Instrument panelen tillhandahåller hälso insikter för enheter med Microsoft 365 appar som hjälper dig att identifiera möjliga problem som kan påverka dina distributions planer. **Instrument panelen för Office 365 ProPlus pilot och hälso tillstånd** innehåller en rekommendation för pilotbaserade enheter som baseras på inventering av tillägg. Följande paneler finns på instrument panelen:

- Skapa pilot
- Rekommenderade pilot enheter
- Distribuera pilot
- Enheter som skickar hälso data
- Enheter som inte uppfyller hälso målen
- Tillägg som inte uppfyller hälso målen
- Makron som inte uppfyller hälso målen

### <a name="using-the-office-365-proplus-pilot-and-health-dashboard"></a>Använda instrument panelen för Office 365 ProPlus pilot och hälso tillstånd

När du har verifierat [kraven](#prerequisites)kan du använda följande instruktioner för att använda instrument panelen:

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **klient hantering för Office 365**.
1. Välj noden **Office 365 pilot and Health** .

![Instrument panel för Office 365 ProPlus pilot och hälso tillstånd](./media/4488272-office-365-pro-plus-pilot.png)


### <a name="generate-pilot"></a>Skapa pilot

Skapa en pilot rekommendation från en begränsande samling genom att klicka på en knapp. När åtgärden startas börjar en bakgrunds aktivitet att beräkna pilot samlingen. Den begränsande samlingen måste innehålla minst en enhet med en Office-version som inte är ProPlus.

### <a name="recommended-pilot-devices"></a>Rekommenderade pilot enheter

**Rekommenderade pilot enheter** är en minimal uppsättning enheter som representerar alla installerade tillägg över den begränsnings samling som du använde när du genererade piloten. Öka detalj nivån för att hämta en lista över dessa enheter. Använd sedan informationen för att undanta enheter från piloten om det behövs. Om alla tillägg redan finns på Microsoft 365 Apps-enheter, inkluderas inte enheter med dessa tillägg i beräkningen. Det innebär också att det är möjligt att du inte får några resultat i din pilot samling eftersom alla dina tillägg har setts på enheter där Microsoft 365-appar är installerade.

### <a name="deploy-pilot"></a>Distribuera pilot

När du har accepterat pilot enheterna distribuerar du Microsoft 365-appar till pilot samlingen med hjälp av guiden stegvis distribution. Administratörer kan definiera piloten och begränsa samlingen i guiden för att hantera distributioner.

### <a name="health-data"></a>Hälso data

När Microsoft 365 appar har installerats aktiverar du hälso data på dina pilot enheter. Hälso data ger dig inblick i vilka tillägg och makron som inte uppfyller hälso målen. Enheten som är **redo att distribuera** diagram identifierar icke-pilot enheter som är redo att distribueras med hjälp av hälso insikter. Få ett antal enheter som skickar hälso data från **enheter som skickar hälso data** diagrammet.

### <a name="devices-not-meeting-health-goals"></a>Enheter som inte uppfyller hälso målen

Den här panelen sammanfattar enheter som har problem med tillägg, makron eller både och.

### <a name="add-ins-not-meeting-health-goals"></a>Tillägg som inte uppfyller hälso målen

- Inläsnings fel: det gick inte att starta tillägget.
- Krascher: det gick inte att lägga till tillägget när det kördes.
- Fel: tillägget rapporterade ett fel.
- Flera problem: tillägget har fler än ett av ovanstående problem.

### <a name="macros-not-meeting-health-goals"></a>Makron som inte uppfyller hälso målen

- Inläsnings fel: det gick inte att läsa in dokumentet.
- Körnings fel: ett fel uppstod när makrot kördes. De här felen kan vara beroende av indata, så de kanske inte alltid inträffar.
- Kompileringsfel: makrot kompilerades inte korrekt så det försöker inte att köra.
- Flera problem: makrot har fler än ett av ovanstående problem.

> [!NOTE]
> Makro inventering fylls med data från readiness Toolkit för Office och nyligen använda datafiler. Makrots hälso tillstånd fylls av hälso data. På grund av olika data källor är det möjligt att hälso tillståndet för makrot **måste granskas** när makro lagret **inte genomsöks**. <!--5922845-->

### <a name="known-issues"></a>Kända problem

Det finns ett känt problem med panelen **distribuera pilot** . Vid detta tillfälle kan det inte användas för att distribuera till en pilot. Lösningen är det befintliga arbets flödet för att distribuera ett program med hjälp av guiden stegvis distribution. <!--5525871-->

## <a name="next-steps"></a>Nästa steg

[Hantera uppdateringar av Microsoft 365 appar med Configuration Manager](manage-office-365-proplus-updates.md)
