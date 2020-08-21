---
title: GRÄNSSNITTs referens för Support Center
titleSuffix: Configuration Manager
description: Lär dig hur du använder Support Center-verktyg.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 41cdebfe-b595-40aa-a385-32e0746255ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 79d483f95c12c1da1e34ca556836a1f42bbffbef
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699457"
---
# <a name="support-center-user-interface-reference"></a>Användar gränssnitts referens för Support Center

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller en referens som beskriver användar gränssnitten för Support Center-verktygen:
- Support Center
- Logg visaren för Support Center
- Support Center Viewer



## <a name="support-center-reference"></a>Support Center-referens

I det här avsnittet beskrivs användar gränssnittet för **Support Center** -verktyget. 
- [Fönster-menyn](#bkmk_support-window)  
- [Fliken Start](#bkmk_support-home)  
- [Fliken klient](#bkmk_support-client)  
- [Fliken princip](#bkmk_support-policy)  
- [Fliken innehåll](#bkmk_support-content)  
- [Fliken inventering](#bkmk_support-inventory)  
- [Fliken fel sökning](#bkmk_support-troubleshoot)  
- [Fliken loggar](#bkmk_support-logs)  


### <a name="window-menu"></a><a name="bkmk_support-window"></a> Fönster-menyn

I det övre vänstra hörnet i Support Center-fönstret väljer du pilen i den blå rutan för att öppna den här menyn.

#### <a name="local-machine-connection"></a>Anslutning till lokal dator
Support Center samlar in loggfiler och utför fel sökning på klienten som kör Support Center.

#### <a name="remote-connection"></a>Fjärr anslutning
Upprätta en fjärr anslutning med en annan Configuration Manager-klient. Efter anslutningen samlar Support Center in loggfiler och utför fel sökning på klienten som den är ansluten till.

#### <a name="about"></a>Om
Tillhandahåller information om Support Center.

#### <a name="options"></a>Alternativ
I dialog rutan **alternativ** kan du:
- Minska förflyttningen av animerade användar gränssnitts element  
- Ändra standard platsen för att spara filer för data paket  
- Ändra platsen för temporära filer    
- Återställ varningar. Eventuella varnings meddelanden som du tidigare ignorerat visas igen när de utlöses.  
- Återställ temporär fil Sök väg till standardvärdet, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

#### <a name="exit"></a>Avsluta
Stäng Support Center.



### <a name="home-tab"></a><a name="bkmk_support-home"></a> Fliken Start

#### <a name="collect-selected-data"></a>Samla in markerade data
Support Center samlar in information från Configuration Manager-klienten. Som standard samlar den in följande typer:
- Loggfiler
- Klient konfigurations insamlare
- Operativsystem

Om du vill samla in andra typer av information markerar du kryss rutan bredvid namnet för den typen.

Välj List rutan längst ned i knappen **samla in markerade data** i menyfliksområdet och välj **samla in alla data**. Den här åtgärden samlar in en fullständig uppsättning klient tillstånds data.

När Support Center samlar in data väljer du **Avbryt samling** för att stoppa det.

#### <a name="data-types"></a>Datatyper
När du markerar kryss rutan för ett alternativ samlar Support Center in den typen av data nästa gång du väljer **samla in markerade data**. Följande typer är tillgängliga:  

- **Loggfiler**: klientens loggfiler inklusive installations loggar  

- **Princip**: klient princip samling  

- **Certifikat**: information om offentlig nyckel för klient certifikat. Support Center samlar inte in certifikatets privata nycklar.  

- **Klient konfigurations insamlare**: Configuration Manager klient information. Du kan inte inaktivera den här data typen.  

- **Klient register**: samlar in klient konfigurations information från registret. Support Center samlar endast in Configuration Manager register information.  

- **Klient-WMI**: klient konfigurations information från WMI. Support Center samlar inte in klient principer.  

- **Fel sökning**: real tids fel söknings data som hjälper dig att diagnostisera vanliga klient problem med Active Directory, hanterings platser, nätverk, princip tilldelningar och registrering.  

    > [!NOTE]  
    > Den här data typen stöds inte när du gör en fjärr anslutning till en annan klient.  

- **Fel söknings dum par**: utför en fel söknings dumpning av klienten och relaterade processer. Fel söknings dum par kan vara stora. Aktivera bara det här alternativet när du felsöker problem med klient prestanda.  

    > [!WARNING]  
    > Insamling av fel söknings dum par gör att data paket blir mycket stora (i vissa fall flera hundra MB).  
    >  
    > Fel söknings dum par innehåller kan innehålla känslig information, inklusive lösen ord, kryptografiska hemligheter eller användar data. Fel söknings dum par bör bara samlas in enligt rekommendationen för Microsoft Support personal. Data paket som innehåller fel söknings dum par bör hanteras noggrant för att skydda dem från obehörig åtkomst.  
    >  
    > Den här data typen stöds inte när du gör en fjärr anslutning till en annan klient.  

- **Operativ system**: samlar in konfigurations information om den lokala datorn. Dessa data innehåller information om Windows-installationen, nätverkskorten och system tjänst konfigurationen. Du kan inte inaktivera den här data typen.  



### <a name="client-tab"></a><a name="bkmk_support-client"></a> Fliken klient

#### <a name="load-or-refresh"></a>Läs in eller uppdatera
Support Center läser in eller uppdaterar information för den Configuration Manager klienten.

#### <a name="control-client-agent-service"></a>Kontrol lera klient Agent tjänsten
Utför någon av följande åtgärder på tjänsten Configuration Manager Client Agent (ccmexec) på den anslutna klienten:  

- **Starta om klient**  

    > [!IMPORTANT]  
    > Om klient Agent tjänsten inte har startats om kan klienten inte hanteras av Configuration Manager förrän tjänsten startar.  

- **Starta klient**  

- **Stoppa klient**  

    > [!IMPORTANT]  
    > Klienten går inte att hantera genom att Configuration Manager förrän tjänsten startar.  

#### <a name="properties"></a>Egenskaper
När du läser in klient information visar Support Center följande egenskaper:  

- **Klient-ID**: en unik identifierare som Configuration Manager använder för att identifiera klienten  

- **Maskinvaru-ID**: en unik identifierare som Configuration Manager använder för att identifiera klient maskin varan  

- **Godkänd**: anger om klienten har godkänts i Configuration Manager  

- **Registrerings tillstånd**: anger om klienten är registrerad på Configuration Manager  

- **Internet**: anger om klienten är ansluten till Internet  

- **Version**: versions numret för den installerade Configuration Manager klienten  

- **Platskod**: plats koden för den primära plats som klienten är tilldelad till  

- **Tilldelad MP**: det fullständigt kvalificerade domän namnet (FQDN) för klientens aktuella tilldelade hanterings plats  

- **Inbyggt MP**: FQDN för den inhemska hanterings platsen  

- **Proxy MP**: värdnamn eller FQDN för hanterings plats för proxy (om det finns)  

- Platskod för **proxy**: plats koden för den sekundära platsen (om den finns)  

- **Proxy-tillstånd**: statusen för den Configuration Manager klientens proxy hanterings plats. Till exempel **aktiv** eller **väntande**.  



### <a name="policy-tab"></a><a name="bkmk_support-policy"></a> Fliken princip

Använd åtgärderna på den här fliken i stället för det äldre [PolicySpy](policy-spy.md) -verktyget.

#### <a name="load-policy"></a>Läs in princip
Det här alternativet varierar beroende på vy:

- **Läs in den faktiska principen**: Välj **faktisk** i visnings gruppen och välj sedan det här alternativet i princip gruppen. Support Center läser in den klient princip som du har valt för tillfället.  

- **Läs in den begärda principen**: Välj **begärd** i visnings gruppen och välj sedan det här alternativet i princip gruppen. Support Center läser in klient principen som begärts av klienten.  

- **Läs in standard princip**: Välj **standard** i gruppen Visa och välj sedan det här alternativet i princip gruppen. Support Center läser in standard principen för den här klienten.  

Välj den nedrullningsbara listan längst ned i den här knappen för ytterligare alternativ:

- **Läs in eller uppdatera alla**: läser in eller uppdaterar den faktiska, begärda och standard principen på samma tidpunkt.  

#### <a name="actual-view"></a>Faktisk vy
Öppnar den faktiska policy vyn

#### <a name="requested-view"></a>Begärd vy
Öppnar den begärda princip visningen

#### <a name="default-view"></a>Standardvy
Öppnar standard princip vyn. (Den här principen är vad enheter får när du installerar Configuration Manager-klienten.)

#### <a name="request-and-evaluate-policy"></a>Begär och utvärdera princip
Support Center begär klient principen från hanterings platsen och utvärderar sedan principen på klienten.

Välj den nedrullningsbara listan längst ned i den här knappen för ytterligare alternativ:  

- **Begär ande princip**: Support Center begär klient principen från hanterings platsen.  

- **Utvärdera princip**: Support Center utvärderar klient principen på klienten.  

- **Återställ principen till standard**: Support Center instruerar Configuration Manager klienten att tillämpa standard principen igen. Den tar bort alla dator-och användar principer på klienten.  

#### <a name="listen-for-policy-events"></a>Lyssna efter princip händelser
Support Center lyssnar efter princip händelser. Välj det här alternativet för att inaktivera lyssning av princip händelser. Om du vill visa **princip händelser**väljer du pilen längst ned på fliken. 

#### <a name="clear-events"></a>Rensa händelser
Support Center tar bort alla princip händelser.



### <a name="content-tab"></a><a name="bkmk_support-content"></a> Fliken innehåll

Visa innehåll på klienten, inklusive cachelagrat innehåll. Övervaka förloppet för program uppdatering och program distributioner. 

#### <a name="load-or-refresh"></a>Läs in eller uppdatera
*Gäller för vyerna innehåll och cache*

Support Center läser in eller uppdaterar listan över innehåll som för närvarande finns på klienten.

#### <a name="invoke-trigger"></a>Anropa utlösare
Följande objekt på den här menyn begär en klient åtgärd som är relaterad till innehållet:  

- **Plats tjänster**  

    - **Uppdatera innehålls platser**: uppdaterar de distributions platser som används av aktiva innehålls hämtningar.  

    - **Uppdatera hanterings platser**: uppdaterar den interna listan över hanterings platser som används av klienten.  

    - **Tids gräns för innehålls begär**Anden: om några innehålls plats begär Anden har körts för länge avbryts begäran av den här åtgärden.  

- **Utvärdering av program distribution**: startar en aktivitet som utvärderar distribuerade program.  

- **Utvärdering av distribution av program uppdateringar**: startar en aktivitet som utvärderar distribuerade program uppdateringar.  

- **Käll genomsökning av program uppdateringar**: startar en aktivitet som genomsöker käll platser för uppdateringar.  

- **Uppdatering av Windows Installer källista**: startar en aktivitet som uppdaterar käll platsen för Windows Installer-installationer (MSI).  

#### <a name="content-view"></a>Innehålls visning
Se program, paket och uppdateringar som läses in på klienten. När du väljer ett program, paket eller en uppdatering kan du Visa information om det innehållet. För vissa program kan du också utföra följande åtgärder:  

- **Uppdatera**: uppdatera vyn information  

- **Verifiera eller ladda ned**: kontrol lera att ett program är tillgängligt för hämtning  

- **Installera**: installera programmet  

- **Avinstallera**: avinstallera programmet  

#### <a name="cache-view"></a>Cache-vy
Visa konfiguration av klientcachen och information om innehållet i cachen. När du ansluter Support Center till en lokal klient, kan du också göra följande:  

- Om du vill ändra cacheplatsen väljer du **ändra** bredvid fältet **cache-plats** .  

- Om du vill justera storleken på cacheminnet väljer du **ändra** bredvid fältet **cachestorlek** .  

- Om du vill rensa klientcachen väljer du **avmarkera** bredvid fältet **cacheminne som används** .  

I den här vyn visas följande egenskaper:  

- **Plats**: platsen för varje cache-mapp. Välj länken för att öppna mappen i Utforskaren i Windows.   
- **Innehålls-ID**  
- **Cache-ID**  
- **Storlek**  
- **Senast refererad**: den här egenskapen är det datum då klienten senast lästes från eller skrevs till det här objektet i cacheminnet.  

#### <a name="monitoring-view"></a>Övervaknings vy
Välj **övervaka** för att visa den aktiva förloppet för program uppdatering och program uppdaterings distributioner. Den här vyn visar tillstånds meddelanden som Aktiver ATS från program-och program uppdaterings händelser WMI-meddelanden.

För varje händelse visar vyn följande egenskaper:  

- **Tid**: den tidpunkt då klienten aktiverade händelsen  
- **Typ av ämne**: typ av tillstånds meddelande  
- **Ämnes-ID**: ID för tillstånds meddelandet som används för att mappa till händelser i loggfiler  
- **Ämnes-ID-typ: undertyp**för tillstånds meddelandet  
- **Tillstånds-ID**: resultatet av den åtgärd som du övervakar  
- **Information** och **händelse data**: Mer information om tillstånds meddelanden som visas i den här vyn. Delstats information kan ibland vara tom.  



### <a name="inventory-tab"></a><a name="bkmk_support-inventory"></a> Fliken inventering

#### <a name="load-or-refresh"></a>Läs in eller uppdatera
Support Center läser in eller uppdaterar klient inventerings listan för den aktuella vyn.

#### <a name="invoke-trigger"></a>Anropa utlösare

> [!Note]  
> För andra uppgifter än **rapport cykel för avläsning av program vara**:  
> - Om du begär uppgiften när en annan inventerings aktivitet redan körs, köar klienten den nya aktiviteten så att den körs när den har slutfört den aktuella aktiviteten och andra köade aktiviteter.  
> - Spåra förloppet för uppgiften i **InventoryAgent. log**.  

Följande objekt på den här menyn begär klient åtgärd relaterad till inventering:  

- **Pulsslag för identifierings data insamling**: utlöser den klient aktivitet som används för att samla in enhets identifierings information  

- **Fil insamlings cykel**: utlöser den klient aktivitet som används för att samla in lokala filer  

- **Maskin varu inventerings cykel**: utlöser den klient aktivitet som används för att samla in maskin varu inventerings data  

- **IDMIF-samlings cykel**: utlöser den klient aktivitet som används för att samla in IDMIF-data  

- **Program varu inventerings cykel**: utlöser den klient aktivitet som används för att samla in program varu inventerings data  

- **Rapport cykel för avläsning av program vara**: utlöser den klient aktivitet som används för att bygga en rapport för avläsning av program vara och skicka den till hanterings platsen. Spåra förloppet för den här uppgiften i **SWMTRReportGen. log**.

- **Skicka tillstånds meddelanden som inte har skickats i kö**: utlöser klient aktiviteten för att tömma kön med tillstånds meddelanden.

- **Avancerat**  
    - **Maskin varu inventerings cykel (fullständig omsynkronisering)**  
    - **Program varu inventerings cykel (fullständig omsynkronisering)**  


#### <a name="views"></a>Vyer
Om en funktion inte är aktive rad visas inte några data i vyn. 

- **Status**: Visa de inventerings data uppsättningar som klienten har samlat in  

- **DDR**: information om klient identifierings data som samlats in från klienten  

- **Hinv**: information om maskin varu inventerings data som samlas in från klienten  

- **SINV**: information om program varu inventerings data som samlas in från klienten  

- **Fil insamling**: information om filerna som samlats in från klienten  

- **IDMIF**: information om IDMIF-och NOIDMIF-data som samlas in från klienten  

- **Mätning**: information om program mätnings data som samlas in från klienten  



### <a name="troubleshooting-tab"></a><a name="bkmk_support-troubleshoot"></a> Fliken fel sökning

Felsök några av de vanligaste problemen med Configuration Manager-klienter:  
- Problem med Active Directory  
- Windows-nätverk  
- Configuration Manager   
    - Hanterings platser  
    - Principtilldelning  
    - Registrering  


> [!NOTE]  
> Den här fliken är inte tillgänglig när du ansluter till en fjärran sluten Configuration Manager-klient.


#### <a name="start"></a>Start
Startar fel sökning av klienten

- **Active Directory**: frågar Active Directory för att hämta publicerad Configuration Manager plats information  
- **MPCERTIFICATE**: hämtar certifikat för hanterings plats  
- **MPLIST**: hämtar en lista över hanterings platser  
- **MPKEYINFORMATION**: hämtar information om kryptografisk nyckel för hanterings platsen  
- **Nätverk**: fel sökning av problem med nätverk  
- **Princip tilldelningar**: hämtar princip tilldelningar  
- **Registrering**: verifierar att klienten är registrerad på platsen  

#### <a name="view-selected-log"></a>Visa vald logg
När du har valt en rad på fliken fel sökning väljer du den här åtgärden för att Visa logg filen.

#### <a name="keep-previous-results"></a>Behåll tidigare resultat
Om du felsöker klienten och sedan vill försöka felsöka igen väljer du det här alternativet för att behålla resultatet från det första försöket. Annars skriver Support Center över tidigare felsöknings loggar.



### <a name="logs-tab"></a><a name="bkmk_support-logs"></a> Fliken loggar

I det här avsnittet visas objekten på fliken **loggar** i Support Center-verktyget. 

Den här fliken är nästan identisk med **logg visnings** verktyget. **Logg visnings** verktyget innehåller inte de funktioner för att **Konfigurera klient loggning** och **logg grupper** som beskrivs i det här avsnittet. Referens avsnittet för [logg visnings programmet för Support Center](#bkmk_log-viewer) innehåller information om andra alternativ som är tillgängliga på den här fliken.

#### <a name="configure-client-logging"></a>Konfigurera klient loggning

Ange följande alternativ: 
- **Klient loggnings nivå**: loggens utförlighet och fil storlek  
- **Maximalt antal filer**: Tillåt fler än en loggfil av en specifik typ  
- **Maximal fil storlek**: storleken i byte för en logg fil innan klienten skapar en ny logg  

> [!NOTE]  
> Om du anger dessa värden för lågt kan klienten inte logga all användbar information. Om du ställer in dessa värden för hög, kan klient loggarna förbruka stora mängder lagring.  

#### <a name="log-groups"></a>Logg grupper

I stället för att manuellt välja loggfiler med knappen **Öppna loggar** använder du den här List rutan för att öppna alla loggfiler som är associerade med följande funktions områden: 
- **Desired Configuration Management**
- **Inventering**
- **Program varu distribution**
- **Program uppdateringar**
- **Program hantering**
- **Princip**
- **Klient registrering**
- **Distribution av operativsystem**


## <a name="support-center-log-viewer-reference"></a><a name="bkmk_log-viewer"></a> Logg visnings referens för Support Center

I det här avsnittet beskrivs användar gränssnittet för **logg visnings verktyget för Support Center** . 

- [Fönster-menyn](#bkmk_log-window)  
- [Fliken Start](#bkmk_log-home)  

**Logg visnings** verktyget är nästan identiskt med fliken **loggar** i **Support Center**. **Logg visnings** verktyget innehåller inte alternativen för att **Konfigurera klient loggning** och **logg grupper**.


### <a name="window-menu"></a><a name="bkmk_log-window"></a> Fönster-menyn

I det övre vänstra hörnet i fönstret logg visaren för Support Center väljer du pilen i den blå rutan för att öppna den här menyn.

#### <a name="open-logs"></a>Öppna loggar
Bläddra till platsen för loggfiler som ska öppnas. 

#### <a name="options"></a>Alternativ
I dialog rutan **alternativ** kan du:
- Minska förflyttningen av animerade användar gränssnitts element  
- Registrera logg visaren som standard program för loggfiler med fil namns tilläggen. log och. lo_  
- Återställ varningar. Eventuella varnings meddelanden som du tidigare ignorerat visas igen när de utlöses.  

#### <a name="about"></a>Om
Visar information om logg visaren för Support Center

#### <a name="close"></a>Stäng
Stänger logg visaren för Support Center


### <a name="home-tab"></a><a name="bkmk_log-home"></a> Fliken Start

#### <a name="open-logs"></a>Öppna loggar 
I Support Center kan du välja en eller flera loggfiler som ska öppnas.

Välj List rutan längst ned i knappen **Öppna loggar** i menyfliksområdet och välj något av följande ytterligare alternativ: 
- **Öppna loggar i aktuell vy**: öppnar de markerade loggfilerna i den aktuella vyn  
- **Öppna loggar i nytt fönster**: öppnar de markerade loggfilerna i ett nytt **logg visnings** fönster  

#### <a name="close-and-clear-logs"></a>Stäng och rensa loggar
Stänger alla öppna loggfiler. Rensar också alla visade logg fils poster från fönstret. Support Center visar inte dessa poster i framtiden.

Välj List rutan längst ned i knappen **Stäng och rensa loggar** i menyfliksområdet och välj något av följande ytterligare alternativ: 
- **Rensa alla poster**: tar bort visade logg fils poster från fönstret. Support Center visar inte dessa poster i framtiden.  
- **Stäng alla loggar**: stänger alla öppna loggfiler  

#### <a name="find"></a>Hitta
Öppnar dialog rutan **Sök** . Ange en sträng att söka efter. För att undvika matchningar på korta strängar i andra strängar, kan du välja att matcha hela ord. Du kan också välja att göra en Skift läges känslig matchning för strängen.

#### <a name="find-next"></a>Sök nästa
När du har hittat en matchning för den sträng som du söker efter, tar det här alternativet dig till nästa matchning.

#### <a name="find-previous"></a>Hitta föregående
När du har hittat två eller flera matchningar för strängen som du söker efter, tar det här alternativet till föregående matchning.

#### <a name="options"></a>Alternativ

- **Direkt uppdatering**: övervaka en för tillfället öppna loggfil för ändringar. Den här funktionen fungerar inte när flera loggfiler är öppna. Det här alternativet är aktiverat som standard.  

- **Automatisk rullning**: om du även väljer alternativet för **direkt uppdatering** bläddrar det här alternativet automatiskt i vyn logg för att visa nyligen tillagda poster. Den här funktionen fungerar inte när flera loggfiler är öppna. Det här alternativet är aktiverat som standard.  

- **Visa information**: när du väljer ett logg fil meddelande visas information om logg fil meddelandet i slutet av fliken **loggar** . Det här alternativet är aktiverat som standard.  

- **Snabb filter**: filtrera logg fil meddelanden i alla öppna loggfiler för att hitta en speciell sträng. Du kan filtrera efter logg text, komponent namn och tråd-ID. Om du vill hitta liknande logg meddelanden högerklickar du på ett logg meddelande och väljer **snabb filter** för logg text.  

- **Figursätta logg text**: radbryta långa och flerradig meddelanden så att de passar i en enda kolumn. Detta gör dessa meddelanden lättare att läsa. Det här alternativet är aktiverat som standard.  

- **Rå logg post visning**: visar obearbetade logg rader.  

- **Avancerade filter**: öppna dialog rutan **Avancerade filter** . Mer information finns i [avancerade logg fils filter](#bkmk_adv-filters).  

- **Fel kods länkar**: felkoder i logg texten är markerade och klicka på. Det här alternativet är aktiverat som standard.  

#### <a name="error-lookup"></a>Fel sökning
Ange en felkod för att söka efter felkoden i för tillfället öppna loggfiler. Använd följande fel kods format:
- **32-bitars heltal (signerat)**: till exempel `-2147024891`  
- **32-bitars heltal (osignerat)**: till exempel `2147942405`  
- **32-bitars hexadecimalt**: till exempel `0x80070005`  

#### <a name="decode-certificate"></a>Avkoda certifikat
I dialog rutan **avkoda certifikat** klistrar du in det serialiserade certifikat svärdet för alla certifikat på klienten. Hitta det här värdet i registret, i loggfiler eller i WMI. Välj **process** för att visa allmän information och information om certifikatet. Den här informationen omfattar certifierings Sök vägen. Välj **Exportera** för att exportera certifikatet som en **CER** -fil.



## <a name="advanced-log-file-filters"></a><a name="bkmk_adv-filters"></a> Avancerade logg fils filter

Med avancerade logg fils filter kan du inkludera, undanta eller markera vissa strängar. De här strängarna kan förekomma i en loggfil eller logg fil grupp när du tittar på logg fils poster. Använd jokertecken för att söka när du skapar ett filter. När du har en användbar kombination av filter sparar du dem som en *filter uppsättning*. 

Avancerade logg fils filter ersätter snabb filter. Använd både tillsammans, men snabb filter gäller endast för visade loggdata. Avancerade filter avgör vilka data som visas först innan alla eventuella snabb filter används.

I dialog rutan Avancerade filter kan du skapa komplexa filter uppsättningar. Dessa filter anger Sök efter strängar i flera logg fil komponenter. Dessa komponenter innehåller meddelanden, trådar, loggnings nivåer och komponenter. En filter uppsättning innehåller flera filter instruktioner som du använder för att inkludera, undanta eller Markera Logg fils meddelanden. Ett filter definierar en logg fils kolumn att söka i, en operator och ett värde. Värdet kan innehålla reguljära uttryck, till exempel *jokertecknet* `*` .


### <a name="add-a-filter"></a>Lägga till ett filter

1. I fönstret **logg visare** eller på fliken Support Center- **loggar** väljer du **Avancerade filter**.  

2. I dialog rutan Avancerade filter väljer du **Lägg till**. Välj sedan ett av följande alternativ för att arbeta med logg poster som matchar ditt filter:  
    - **Inkludera**  
    - **Ingå**  
    - **Höjdpunkt**  

3. I dialog rutan **Avancerad filter konfiguration** väljer du en kolumn och en operator:  

    - **Kolumn**: Välj var du vill söka efter strängar som matchar ditt filter:  

         - **Logg text**: söka i texten i en loggfil  

         - **Allvarlighets grad för logg**: Sök efter loggar med en angiven allvarlighets grad. Ange dessa allvarlighets nivåer i fältet **värde** .  

         - **Komponent**: Sök efter en enskild komponent efter namn  

         - **Tråd-ID**: Sök efter logg meddelanden med ett angivet tråd-ID  

         - **Källfil**: Sök efter logg meddelanden som förekommer i en angiven loggfil  

    - **Operator**: Välj en operator för ditt filter  

4. Ange ett värde att filtrera efter i fältet **värde** . Om värdet innehåller reguljära uttryck väljer du **Aktivera matchning av reguljära uttryck**.  


### <a name="manage-filter-sets"></a>Hantera filter uppsättningar

- Om du vill redigera ett filter väljer du filtret och väljer sedan **Redigera**.  

- Om du vill ta bort ett filter väljer du filtret och väljer sedan **ta bort**.  

- Om du vill rensa alla filter väljer du **Rensa**.  

- Om du vill spara den aktuella filter uppsättningen väljer du **Spara filter**. Spara sedan filter uppsättningen som en **. Filterset** -fil.  

- Om du vill läsa in en sparad filter uppsättning väljer du **läsa in filter**. Bläddra sedan till en tidigare sparad **. Filterset** -fil.  



## <a name="support-center-viewer-reference"></a><a name="bkmk_viewer"></a> Referens för Support Center Viewer

I det här avsnittet beskrivs användar gränssnittet (UI) för verktyget Configuration Manager **Support Center Viewer** . De tillgängliga flikarna varierar beroende på innehållet i fel söknings paketet. [Fönster-menyn](#bkmk_viewer-window) och [fliken Start](#bkmk_viewer-home) visas som standard.
- [Fönster-menyn](#bkmk_viewer-window)
- [Fliken Start](#bkmk_viewer-home)
- [Fliken konfiguration](#bkmk_viewer-config)
- [Fliken loggar](#bkmk_viewer-logs)
- [Fliken fel söknings dum par](#bkmk_viewer-debug)
- [Fliken WMI](#bkmk_viewer-wmi)
- [Fliken register](#bkmk_viewer-registry)
- [Fliken princip](#bkmk_viewer-policy)
- [Fliken certifikat](#bkmk_viewer-certs)
- [Fliken fel sökning](#bkmk_viewer-troubleshoot)


### <a name="window-menu"></a><a name="bkmk_viewer-window"></a> Fönster-menyn

I det övre vänstra hörnet i fönstret Support Center Viewer väljer du pilen i den blå rutan för att öppna den här menyn.

#### <a name="open-bundle"></a>Öppna paket
Bläddra till platsen för ett data paket som skapats av Support Center.

#### <a name="about"></a>Om
Visar information om Support Center Viewer.

#### <a name="options"></a>Alternativ
I dialog rutan **alternativ** kan du:
- Minska förflyttningen av animerade användar gränssnitts element  
- Ändra platsen för temporära filer    
- Återställ varningar. Eventuella varnings meddelanden som du tidigare ignorerat visas igen när de utlöses.  
- Återställ temporär fil Sök väg till standardvärdet, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`  


#### <a name="exit"></a>Avsluta
Avslutar Support Center Viewer


### <a name="home-tab"></a><a name="bkmk_viewer-home"></a> Fliken Start

#### <a name="open-bundle"></a>Öppna paket
Bläddra till platsen för ett data paket som skapats av Support Center.

#### <a name="open-log-file"></a>Öppna logg filen
Välj en eller flera loggfiler som ska öppnas.

#### <a name="decode-certificate"></a>Avkoda certifikat
I dialog rutan **avkoda certifikat** klistrar du in det serialiserade certifikat svärdet för alla certifikat på klienten. Hitta det här värdet i registret, i loggfiler eller i WMI. Välj **process** för att visa allmän information och information om certifikatet. Den här informationen omfattar certifierings Sök vägen. Välj **Exportera** för att exportera certifikatet som en **CER** -fil.


### <a name="configuration-tab"></a><a name="bkmk_viewer-config"></a> Fliken konfiguration

Fliken **konfiguration** i verktyget Support Center Viewer innehåller följande vyer som använder data som hämtats från WMI-providers:

#### <a name="client"></a>Client
Den här vyn visar samma information som visas på fliken **klient** i Support Center.

#### <a name="operating-system"></a>Operativsystem
Information om klientens operativ system. Den använder klassen [Win32_OperatingSystem](/windows/desktop/CIMWin32Prov/win32-operatingsystem) .

#### <a name="computer"></a>Dator
Information för klient datorn. Den använder klassen [Win32_OperatingSystem](/windows/desktop/CIMWin32Prov/win32-operatingsystem) .

#### <a name="services"></a>Tjänster
Information om tjänster som körs på klient datorn. Den använder klassen [Win32_Service](/windows/desktop/CIMWin32Prov/win32-service) .

#### <a name="network-adapters"></a>Nätverkskort
Information om nätverkskort som är installerade på klient datorn. Den använder klassen [Win32_NetworkAdapterConfiguration](/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration) .


### <a name="logs-tab"></a><a name="bkmk_viewer-logs"></a> Fliken loggar

På fliken **loggar** visas en lista över de loggfiler som ingår i paketet. Varje rad på den här fliken innehåller sökvägen, namnet och storleken på logg filen. 

#### <a name="open"></a>Öppna
När du har valt en loggfil väljer du den här knappen för att öppna **logg visaren**. Den innehåller en delmängd av de funktioner som visas på fliken Support Center-loggar.

#### <a name="decode-certificate"></a>Avkoda certifikat
I dialog rutan **avkoda certifikat** klistrar du in det serialiserade certifikat svärdet för alla certifikat på klienten. Hitta det här värdet i registret, i loggfiler eller i WMI. Välj **process** för att visa allmän information och information om certifikatet. Den här informationen omfattar certifierings Sök vägen. Välj **Exportera** för att exportera certifikatet som en **CER** -fil.


### <a name="debug-dumps-tab"></a><a name="bkmk_viewer-debug"></a> Fliken fel söknings dum par

Varje rad på den här fliken innehåller information om de fel söknings dum par som är tillgängliga för export. Använd den här fliken för att exportera fel söknings dum par filer (. dmp) för ytterligare analys. I den här analysen används ett fel söknings verktyg som WinDbg. 

> [!WARNING]  
> Fel söknings dum par kan innehålla känslig information, inklusive lösen ord, kryptografiska hemligheter eller användar data. Samla bara in fel söknings dum par på rekommendationen av Microsoft Support personal. Data paket som innehåller fel söknings dum par bör hanteras noggrant för att skydda dem från obehörig åtkomst.  

#### <a name="export"></a>Exportera
Spara en kopia av den valda felsöknings dumpnings filen.


### <a name="wmi-tab"></a><a name="bkmk_viewer-wmi"></a> Fliken WMI

På den här fliken visas en uppsättning WMI-data från den Configuration Manager klienten som data paketet innehåller. 

#### <a name="find"></a>Hitta
Öppnar dialog rutan Sök som innehåller följande funktioner:  

- **Sök**efter: Ange en sträng att söka efter i WMI-datauppsättningen. Det stöder jokertecken.  

- **Titta på**: Välj om du vill söka i WMI-datauppsättningen efter matchande **klass-eller instans namn**, **egenskap**eller **värde**.  

- **Matcha endast hel sträng**: som standard söker dialog rutan Sök efter strängar som innehåller den sträng som du vill se. Markera den här kryss rutan om du bara vill hitta strängar som är en exakt matchning till den sträng som du har angett.  

#### <a name="find-next"></a>Sök nästa
Den här knappen öppnar nästa instans av strängen som du angav i dialog rutan Sök i WMI-datauppsättningen.

#### <a name="decode-certificate"></a>Avkoda certifikat
I dialog rutan **avkoda certifikat** klistrar du in det serialiserade certifikat svärdet för alla certifikat på klienten. Hitta det här värdet i registret, i loggfiler eller i WMI. Välj **process** för att visa allmän information och information om certifikatet. Den här informationen omfattar certifierings Sök vägen. Välj **Exportera** för att exportera certifikatet som en **CER** -fil.


### <a name="registry-tab"></a><a name="bkmk_viewer-registry"></a> Fliken register

Använd **registret** -fliken för att Visa register data som ingår i data paketet och för att exportera data för ytterligare analys.

#### <a name="export"></a>Exportera
Spara en kopia av den register nyckel och de under nycklar som du väljer som en register fil (REG).

#### <a name="find"></a>Hitta
Öppnar dialog rutan Sök som innehåller följande funktioner:  

- **Sök**efter: Ange en sträng att söka efter i WMI-datauppsättningen. Det stöder jokertecken.  

- **Titta på**: Välj om du vill söka i WMI-datauppsättningen efter matchande **klass-eller instans namn**, **egenskap**eller **värde**.  

- **Matcha endast hel sträng**: som standard söker dialog rutan Sök efter strängar som innehåller den sträng som du vill se. Markera den här kryss rutan om du bara vill hitta strängar som är en exakt matchning till den sträng som du har angett.  

#### <a name="find-next"></a>Sök nästa
Den här knappen öppnar nästa instans av strängen som du angav i dialog rutan Sök i WMI-datauppsättningen.

#### <a name="decode-certificate"></a>Avkoda certifikat
I dialog rutan **avkoda certifikat** klistrar du in det serialiserade certifikat svärdet för alla certifikat på klienten. Hitta det här värdet i registret, i loggfiler eller i WMI. Välj **process** för att visa allmän information och information om certifikatet. Den här informationen omfattar certifierings Sök vägen. Välj **Exportera** för att exportera certifikatet som en **CER** -fil.


### <a name="policy-tab"></a><a name="bkmk_viewer-policy"></a> Fliken princip

Fliken **princip** används för att Visa princip data som ingår i data paketet. 

#### <a name="find"></a>Hitta
Öppnar dialog rutan Sök som innehåller följande funktioner:  

- **Sök**efter: Ange en sträng att söka efter i WMI-datauppsättningen. Det stöder jokertecken.  

- **Titta på**: Välj om du vill söka i WMI-datauppsättningen efter matchande **klass-eller instans namn**, **egenskap**eller **värde**.  

- **Matcha endast hel sträng**: som standard söker dialog rutan Sök efter strängar som innehåller den sträng som du vill se. Markera den här kryss rutan om du bara vill hitta strängar som är en exakt matchning till den sträng som du har angett.  

#### <a name="find-next"></a>Sök nästa
Den här knappen öppnar nästa instans av strängen som du angav i dialog rutan Sök i WMI-datauppsättningen.

#### <a name="decode-certificate"></a>Avkoda certifikat
I dialog rutan **avkoda certifikat** klistrar du in det serialiserade certifikat svärdet för alla certifikat på klienten. Hitta det här värdet i registret, i loggfiler eller i WMI. Välj **process** för att visa allmän information och information om certifikatet. Den här informationen omfattar certifierings Sök vägen. Välj **Exportera** för att exportera certifikatet som en **CER** -fil.


### <a name="certificates-tab"></a><a name="bkmk_viewer-certs"></a> Fliken certifikat

Fliken **certifikat** används för att Visa certifikat som ingår i data paketet och för att exportera dem.

#### <a name="view-certificate"></a>Visa certifikat
Visar information om ett valt certifikat.

#### <a name="export"></a>Exportera
Öppnar dialog rutan **Spara som** för att spara en kopia av det certifikat som du väljer.


### <a name="troubleshooting-tab"></a><a name="bkmk_viewer-troubleshoot"></a> Fliken fel sökning

Använd fliken **fel sökning** om du vill visa loggfiler som skapats med hjälp av fliken fel sökning i Support Center.

#### <a name="view-log"></a>Visa logg
När du har valt en rad på fliken **fel sökning** väljer du det här alternativet för att Visa logg filen med logg visaren.