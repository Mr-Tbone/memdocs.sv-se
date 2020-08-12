---
title: Uppdateringar i konsolen
titleSuffix: Configuration Manager
description: Installera uppdateringar till Configuration Manager från Microsoft-molnet
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 65071493834c33dac7581075b835e023c74f5706
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128094"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Installera uppdateringar i konsolen för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager synkroniseras med Microsoft Cloud service för att hämta uppdateringar. Installera sedan dessa uppdateringar från Configuration Manager-konsolen.

## <a name="get-available-updates"></a>Hämta tillgängliga uppdateringar

Platsen hämtar endast uppdateringar som gäller för din infrastruktur och version. Den här synkroniseringen kan vara automatisk eller manuell, beroende på hur du konfigurerar tjänst anslutnings punkten för hierarkin:

- I **onlineläge**ansluter tjänstanslutningspunkten automatiskt till Microsoft-molntjänsten och hämtar tillämpliga uppdateringar.  

    Som standard söker Configuration Manager efter nya uppdateringar var 24: e timme. Sök manuellt efter uppdateringar i Configuration Manager-konsolen. Gå till arbets ytan **Administration** , välj noden **uppdateringar och underhåll** och välj **Sök efter uppdateringar** i menyfliksområdet.  

- I **offlineläge**ansluter inte tjänst anslutnings punkten till Microsofts moln tjänst. [Använd tjänst anslutnings verktyget](use-the-service-connection-tool.md)för att ladda ned och sedan importera tillgängliga uppdateringar.  

> [!NOTE]  
> Om det behövs kan du importera out-of-band-korrigeringar till-konsolen. Det gör du med hjälp av [verktyget uppdatera registrering](use-the-update-registration-tool-to-import-hotfixes.md). Dessa out-of-band-korrigeringar kompletterar de uppdateringar som du får när du synkroniserar med Microsofts moln tjänst.  

När uppdateringarna har synkroniserats kan du visa dem i Configuration Manager-konsolen. Gå till arbets ytan **Administration** och välj noden **uppdateringar och underhåll** .  

- Uppdateringar som du inte har installerat visas som **tillgängliga**.  

- Uppdateringar som du har installerat visas som **installerade**. Endast den senast installerade uppdateringen visas. Om du vill visa tidigare installerade uppdateringar väljer du **Historik** i menyfliksområdet.  

Innan du konfigurerar tjänst anslutnings punkten bör du förstå och planera för dess ytterligare användning. Följande användnings områden kan påverka hur du konfigurerar den här plats system rollen:  

- Platsen använder tjänst anslutnings punkten för att överföra användnings information om din webbplats. Den här informationen hjälper Microsoft-molntjänsten att identifiera vilka uppdateringar som är tillgängliga för den aktuella versionen av infrastrukturen. Mer information finns i [diagnostik-och användnings data](../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

För att bättre förstå vad som händer när uppdateringar hämtas, se följande flödes scheman:  

- [Flödesschema – hämta uppdateringar](download-updates-flowchart.md)  

- [Flödesschema – Uppdatera replikering](update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Tilldela behörigheter för att visa och hantera uppdateringar och funktioner

Om du vill visa uppdateringar i-konsolen måste en användare ha en rollbaserad administrations säkerhets roll som innehåller **uppdaterings paket**för säkerhets klasser. Den här klassen ger åtkomst till att visa och hantera uppdateringar i Configuration Manager-konsolen.

### <a name="about-the-update-packages-class"></a>Om klassen uppdaterings paket

Som standard är klassen **uppdaterings paket** (SMS_CM_Updatepackages) en del av följande inbyggda säkerhets roller med de angivna behörigheterna:  

- **Fullständig administratör** med behörigheter för att **ändra** och **läsa** :  

  - En användare med den här säkerhets rollen och åtkomst till säkerhets omfattningen **alla** kan visa och installera uppdateringar. Användaren kan också aktivera funktioner under installationen och aktivera enskilda funktioner när platsen har uppdaterats.  

  - En användare med den här säkerhets rollen och åtkomst till **standard** säkerhets omfattningen kan visa och installera uppdateringar. Användaren kan också aktivera funktioner under installationen och Visa funktioner efter att platsen har uppdaterats. Men den här användaren kan inte aktivera funktioner efter att platsen har uppdaterats.  

- **Analytiker med läsbehörighet** med behörigheten **Läsa** :  

  - En användare med den här säkerhets rollen och åtkomst till **standard** omfånget kan visa uppdateringar, men inte installera dem. Den här användaren kan även Visa funktioner efter att platsen har uppdaterats, men de kan inte aktivera dem.  

### <a name="permissions-required-for-updates-and-servicing"></a>Behörigheter som krävs för uppdateringar och underhåll

- Använd ett konto som du tilldelar en säkerhets roll som inkluderar klassen **uppdaterings paket** med både behörigheterna **ändra** och **läsa** .  

- Tilldela kontot till **standard** omfånget.  

### <a name="permissions-to-only-view-updates"></a>Behörigheter för att endast visa uppdateringar

- Använd ett konto som du tilldelar en säkerhets roll som inkluderar klassen **uppdaterings paket** med bara **Läs** behörighet.  

- Tilldela kontot till **standard** omfånget.  

### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Behörigheter som krävs för att aktivera funktioner efter att platsen har uppdaterats

- Använd ett konto som du tilldelar en säkerhets roll som inkluderar klassen **uppdaterings paket** med både behörigheterna **ändra** och **läsa** .  

- Tilldela kontot till området **alla** .  

## <a name="before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a>Innan du installerar en uppdatering i konsolen  

Granska följande steg innan du installerar en uppdatering från Configuration Manager-konsolen.  

### <a name="step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a>Steg 1: granska check lista för uppdateringar  

Granska tillämplig check lista för uppdateringar för åtgärder som ska vidtas innan du startar uppdateringen:

- [Check lista för att installera uppdatering 2006](checklist-for-installing-update-2006.md)

- [Checklista för att installera uppdatering 2002](checklist-for-installing-update-2002.md)

- [Checklista för att installera uppdatering 1910](checklist-for-installing-update-1910.md)  

- [Checklista för att installera uppdatering 1906](checklist-for-installing-update-1906.md)  

### <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step2"></a>Steg 2: kör krav kontrollen innan du installerar en uppdatering  

Överväg att köra kravkontrollen för en uppdatering innan du installerar en den. Om du kör kravkontrollen innan du installerar en uppdatering:  

- Platsen replikerar uppdateringsfiler till andra platser innan uppdateringen installeras.  

- När du väljer att installera uppdateringen körs krav kontrollen automatiskt igen.  

> [!NOTE]  
> När du startar en krav kontroll och sedan visar statusen, verkar **installations** fasen vara aktiv. Platsen installerar dock inte uppdateringen. För att köra krav kontrollen extraherar uppdaterings processen paketet från innehålls biblioteket. Den placerar sedan paketet i en mellanlagringsmappen där de kan komma åt de aktuella nödvändiga kontrollerna. När du installerar en uppdatering körs samma process. Detta är orsaken till att installations fasen visas som **pågående**. Endast steget *extrahera uppdaterings paket* visas i kategorin installation.  

När du senare installerar uppdateringen kan du konfigurera uppdateringen att ignorera krav kontroll varningar.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>För att köra kravkontrollen innan du installerar en uppdatering  

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **uppdateringar och underhåll** .  

2. Välj det uppdaterings paket som du vill köra krav kontrollen för.  

3. Välj **Kör krav kontroll** i menyfliksområdet.  

    När du kör kravkontrollen replikeras innehåll för uppdateringen till underordnade platser. Visa **Distmgr. log** på plats servern för att bekräfta att innehållet har repliker ATS.  

4. Så här visar du resultatet av krav kontrollen:  

    1. Gå till arbets ytan **övervakning** i Configuration Manager-konsolen.  

    2. Välj noden **uppdateringar och underhålls status** och leta efter krav status.  

    3. Mer information finns i **ConfigMgrPrereq. log** på plats servern.  

## <a name="install-in-console-updates"></a><a name="bkmk_install"></a>Installera uppdateringar i konsolen  

När du är redo att installera uppdateringar inifrån Configuration Manager-konsolen börjar du med platsen på den översta nivån i hierarkin. Den här platsen är antingen den centrala administrations platsen eller en fristående primär plats.  

Installera uppdateringen utanför normal kontors tid för varje plats för att minimera påverkan på affärs verksamhet. Installationen av uppdateringen kan omfatta åtgärder som att installera om plats komponenter och plats system roller.  

- Underordnade primära platser startar uppdateringen automatiskt när den centrala administrations platsen har slutfört installationen av uppdateringen. Den här processen är som standard och rekommenderas. Om du vill styra när en primär plats installerar uppdateringar använder du [Service Windows för plats servrar](service-windows.md).  

- Uppdatera sekundära platser manuellt från Configuration Manager-konsolen när den primära överordnade platsens uppdatering är klar. Automatisk uppdatering av sekundära plats servrar stöds inte.  

- När du använder en Configuration Manager-konsol när platsen har uppdaterats uppmanas du att uppdatera konsolen.  

- När plats servern har slutfört installationen av en uppdatering uppdaterar den automatiskt alla tillämpliga plats system roller. Alla distributions platser installeras dock inte om och går inte att uppdatera på samma gång. Plats servern använder i stället platsens innehålls distributions inställningar för att distribuera uppdateringen till en delmängd av distributions platserna i taget. Resultatet är att endast vissa distributions platser går offline för att installera uppdateringen. Distributions platser som inte har börjat uppdateras eller som har slutfört uppdateringen är online och kan tillhandahålla innehåll till klienter.

### <a name="overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a>Översikt över uppdaterings installation i konsolen  

#### <a name="1-when-the-update-installation-starts"></a>1. När installationen av uppdateringen startar

Du visas i uppdaterings guiden som visar en lista över de produkt områden som uppdateringen gäller.  

- På sidan **Allmänt** i guiden konfigurerar du nödvändiga **varningar** om det behövs:  

  - Kravfel avbryter alltid installationen av uppdateringar. Åtgärda felen innan du kan försöka installera uppdateringen igen. Mer information finns i [gör om installationen av en misslyckad uppdatering](#bkmk_retry).  

  - Kravkontrollvarningar kan också avbryta installationen av uppdateringen. Åtgärda varningar innan du försöker installera uppdateringen igen. Mer information finns i [gör om installationen av en misslyckad uppdatering](#bkmk_retry).  

  - **Ignorera eventuella krav kontroll varningar och installera den här uppdateringen oavsett vilka krav som saknas**: Ange ett villkor för att uppdaterings installationen ska ignorera krav varningar. Med det här alternativet kan installationen av uppdateringen fortsätta. Om du inte väljer det här alternativet avbryts installationen av uppdateringen när en varning påträffas av processen. Om du inte tidigare har kört krav kontrollen och korrigerade krav varningar för en plats använder du inte det här alternativet.  

    På arbets ytan **Administration** och **övervakning** innehåller noden uppdateringar och underhåll en knapp i menyfliksområdet med namnet **Ignorera krav varningar**. Den här knappen blir tillgänglig när ett uppdaterings paket inte kan slutföra installationen på grund av krav kontroll varningar. Du kan till exempel installera en uppdatering utan att använda alternativet för att ignorera krav kontroll varningar (inifrån uppdaterings guiden). Installationen av uppdateringen stoppas med ett tillstånd med krav varning men inga fel. Senare väljer du **Ignorera krav varningar** i menyfliksområdet. Den här åtgärden utlöser en automatisk fortsättning av uppdateringen, som ignorerar krav kontroll varningar. När du använder det här alternativet fortsätter installationen av uppdateringen automatiskt efter några minuter.  

- När en uppdatering gäller för den Configuration Manager klienten väljer du att testa klient uppdateringen med en begränsad uppsättning klienter. Mer information finns i [så här testar du klient uppgraderingar i en för produktions samling](../../clients/manage/upgrade/test-client-upgrades.md).  

#### <a name="2-during-the-update-installation"></a>2. Under installationen av uppdateringen

Som en del av installationen av uppdateringen utför Configuration Manager följande åtgärder:  

- Installerar om alla påverkade komponenter, t. ex. plats system roller eller Configuration Manager-konsolen.  

- Hanterar uppdateringar till klienter baserat på de val du har gjort för klient pilotering och för [automatiska klient uppgraderingar](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).  

- Plats system servrar behöver normalt inte startas om som en del av uppdateringen. Om en roll använder .NET och paketet uppdaterar den nödvändiga komponenten, kan det hända att plats systemet startas om.  

> [!TIP]  
> När du installerar Configuration Manager uppdateringar uppdaterar webbplatsen även CD: n. Senaste mappen. Mer information finns [på CD-skivan. Senaste mappen](the-cd.latest-folder.md).  

#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Övervaka förloppet för uppdateringar under tiden de installeras

Använd följande steg för att övervaka förloppet:  

- I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **uppdateringar och underhåll** . Den här noden visar installationsstatus för alla uppdateringspaket.  

- I Configuration Manager-konsolen går du till arbets ytan **övervakning** och väljer noden **uppdateringar och underhålls status** . Den här noden visar installations status för endast det aktuella uppdaterings paket som platsen installeras på.  

    Installationen av uppdateringen är uppdelad i flera faser för enklare övervakning. För var och en av följande faser inkluderar ytterligare information i installations statusen vilken loggfil som ska visas för mer information:  

  - **Hämta**: den här fasen gäller endast platsen på den översta nivån med tjänst anslutnings punkten.

  - **Replikering**

  - **Kravkontroll**

  - **Installation**

  - **Efter installation**: Mer information finns i [Skicka installations uppgifter](#post-installation-tasks).  

- Visa filen **CMUpdate. log** i `<ConfigMgr_Installation_Directory>\Logs` på plats servern.  

>[!NOTE]
> Från och med version 1906 kan du se statusen för åtgärden **Uppgradera ConfigMgr-databasen** under **installations** fasen.
>
> - Om databas uppgraderingen är blockerad får du en varning om att en **pågående**varning krävs.
>   - Cmupdate. log kommer att logga program namnet och SessionID från SQL som blockerar databas uppgraderingen.
> - När databas uppgraderingen inte längre är blockerad återställs statusen till **pågår** eller **slutförs**.
>   - När databas uppgraderingen blockeras utförs en kontroll var 5: e minut för att se om den fortfarande är blockerad.

#### <a name="4-when-the-update-installation-completes"></a>4. När installationen av uppdateringen slutförts

Efter den första installationen av platsuppdateringen har slutförts:  

- Underordnade primära platser installerar uppdateringen automatiskt. Ingen ytterligare åtgärd krävs.  

- Uppdatera sekundära platser manuellt från Configuration Manager-konsolen. Mer information finns i [starta installationen av uppdateringen på en sekundär plats](#bkmk_secondary).  

- Hierarkin körs i ett läge för blandade versioner till dess att alla platser i hierarkin har uppdaterats till den nya versionen. Mer information finns i [samverkan mellan olika versioner](../../plan-design/hierarchy/interoperability-between-different-versions.md).  

#### <a name="5-update-configuration-manager-consoles"></a>5. uppdatera Configuration Manager-konsoler

När en central administrations plats eller primär plats uppdateras måste varje Configuration Manager-konsol som ansluter till platsen också uppdateras. Du uppmanas att uppdatera en konsol:  

- När du öppnar konsolen  

- När du går till en ny nod i en öppen konsol  

Uppdatera-konsolen direkt när platsen har uppdaterats.  

När konsolen har uppdaterats kontrollerar du att konsolen och plats versionerna är korrekta. Gå till **om Configuration Manager** i det övre vänstra hörnet i konsolen.  

> [!Note]  
> Konsol versionen skiljer sig något från plats versionen. Den lägre versionen av konsolen motsvarar Configuration Manager version. I Configuration Manager version 1802 är till exempel den första plats versionen 5.0.8634.1000 och den inledande konsol versionen är 5. **1802**. 1082,1700. Versions numren för build (1082) och revision (1700) kan ändras med framtida snabb korrigeringar.

### <a name="to-start-the-update-installation-at-the-top-level-site"></a><a name="bkmk_toptier"></a>Starta installationen av uppdateringen på platsen på den översta nivån  

På platsen på den översta nivån i hierarkin går du till arbets ytan **Administration** i Configuration Manager-konsolen och väljer noden **uppdateringar och underhåll** . Välj en uppdatering med den **tillgängliga**statusen och välj sedan **Installera uppdaterings paket** i menyfliksområdet.  

### <a name="to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a>Starta installationen av uppdateringen på en sekundär plats  

När den sekundära platsens överordnade primära plats uppdateras uppdaterar du den sekundära platsen från Configuration Manager-konsolen. För att göra det använder du **Uppgraderingsguiden för sekundära platser**.  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** . Välj den sekundära plats som du vill uppdatera och välj sedan **Uppgradera** i menyfliksområdet.  

2. Välj **Ja** om du vill starta uppdateringen av den sekundära platsen.  

Om du vill övervaka installationen av uppdateringen på en sekundär plats väljer du den sekundära platsen och väljer **Visa installations status** i menyfliksområdet. Lägg också till kolumnen **version** i noden platser så att du kan visa versionen för varje sekundär plats.  

I vissa fall uppdateras inte statusen i konsolen eller så föreslås uppdateringen inte. När en sekundär plats har uppdaterats kan du använda alternativet för att **försöka installera igen** . Det här alternativet installerar inte om uppdateringen för en sekundär plats där uppdateringen har installerats, men tvingar konsolen att uppdatera statusen.

### <a name="post-installation-tasks"></a>Uppgifter efter installationen

När en plats installerar en uppdatering finns det flera aktiviteter som inte kan starta förrän efter att uppdateringen är klar med installationen på plats servern. Den här listan innehåller de uppgifter efter installationen som är kritiska för plats-och hierarki-åtgärder. Eftersom de är kritiska övervakas de aktivt. Ytterligare aktiviteter som inte är direkt övervakade inkluderar ominstallation av plats system roller. Om du vill visa statusen för de kritiska uppgifterna efter installationen väljer du aktiviteten **efter installation** medan du övervakar uppdaterings installationen för en plats.

Alla aktiviteter slutförs inte omedelbart. Vissa aktiviteter startar inte förrän varje plats har slutfört installationen av uppdateringen. Nya funktioner som du kan förväntar dig kan förskjutas tills dessa uppgifter har slutförts. Det går inte att aktivera nya funktioner förrän alla platser har slutfört installationen av uppdateringen, så nya funktioner kanske inte visas under en viss tid.

Uppgifterna efter installationen är:

- **Installera SMS_EXECUTIVE tjänst**

  - Kritisk tjänst som körs på plats servern.
  - Ominstallation av den här tjänsten bör slutföras snabbt.

- **Installerar SMS_DATABASE_NOTIFICATION_MONITOR komponent**

  - Viktig plats komponent tråd för SMS_EXECUTIVE tjänst.
  - Ominstallation av den här tjänsten bör slutföras snabbt.

- **Installerar SMS_HIERARCHY_MANAGER komponent**

  - Kritisk plats komponent som körs på plats servern.
  - Ansvarig för ominstallation av roller på plats system servrar. Status för enskild ominstallation av plats system rollen visas inte.
  - Ominstallation av den här tjänsten bör slutföras snabbt.

    > [!Note]
    > Vissa Configuration Manager plats roller delar klient ramverket. Till exempel hanterings platsen och mottagar distributions platsen. När de här rollerna uppdateras uppdateras klient versionen på de här servrarna på samma gång. Mer information finns i [Uppgradera klienter](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

- **Installerar SMS_REPLICATION_CONFIGURATION_MONITOR komponent**

  - Kritisk plats komponent som körs på plats servern.
  - Ominstallation av den här tjänsten bör slutföras snabbt.

- **Installerar SMS_POLICY_PROVIDER komponent**

  - Kritisk plats komponent som bara körs på primära platser.
  - Ominstallation av den här tjänsten bör slutföras snabbt.

- **Övervaka replikeringsinitieringen**

  - Den här uppgiften visas bara på den centrala administrations platsen och underordnade primära platser.
  - Beroende av SMS_REPLICATION_CONFIGURATION_MONITOR.
  - Bör slutföras snabbt.

- **Uppdatera Configuration Manager-klient för produktions paket**

  - Den här uppgiften visar även när klient-för-produktion (även kallat klient pilot) inte är aktive rad för användning.
  - Startar inte förrän alla platser i hierarkin har slutfört installationen av uppdateringen.

- **Uppdaterar klientens mapp på plats servern**

  - Den här uppgiften visas inte om du använder-klienten i för produktion.  
  - Bör slutföras snabbt.

- **Uppdatera Configuration Manager klient paket**

  - Den här uppgiften visas inte om du använder-klienten i för produktion.  
  - Slutförs bara när alla platser har installerat uppdateringen.  

- **Aktivera funktioner**

  - Den här uppgiften visas endast på platsen på den översta nivån i hierarkin.
  - Startar inte förrän alla platser i hierarkin har slutfört installationen av uppdateringen.
  - Enskilda funktioner visas inte.

## <a name="retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a>Gör om installationen av en misslyckad uppdatering  

Granska feedbacken i konsolen för att identifiera lösningar för varningar och fel när en installation av en uppdatering misslyckas. Mer information finns i **ConfigMgrPrereq. log** på plats servern. Innan du försöker installera en uppdatering igen måste du åtgärda felen och åtgärda varningar.  

> [!TIP]  
> Om en uppdatering har problem med att hämta eller replikera använder du [verktyget uppdatera återställning](update-reset-tool.md).  

När du är redo att försöka installera en uppdatering igen väljer du den misslyckade uppdateringen och väljer sedan ett lämpligt alternativ. Återförsöket att installera uppdateringen beror på den nod där du startar återförsöket och det alternativ för återförsök som du använder.  

### <a name="retry-installation-for-the-hierarchy"></a>Gör om installationen för hierarkin

Gör om installationen av en uppdatering för hela hierarkin när uppdateringen är i något av följande tillstånd:  

- Krav kontroller godkändes med en eller flera varningar och alternativet för att ignorera krav kontroll varningar angavs inte i uppdaterings guiden. (Uppdateringens värde för **Ignorera krav-varning** i noden **uppdateringar och underhåll** är **Nej**.)

- Kraven misslyckades

- Installationen misslyckades  

- Det gick inte att replikera innehållet till platsen

Gå till arbets ytan **Administration** och välj noden **uppdateringar och underhåll** . Välj uppdateringen och välj sedan ett av följande alternativ:  

- **Försök**igen: när du **försöker igen** från **uppdateringar och underhåll**startar uppdaterings installationen igen och ignorerar automatiskt nödvändiga varningar. Om det tidigare har misslyckats med att replikera innehållet replikeras innehållet för uppdateringen igen.  

- **Ignorera krav kontroll varningar**: om installationen av uppdateringen stoppas på grund av en varning kan du välja **Ignorera krav varningar**. Den här åtgärden gör att uppdateringen kan fortsätta efter några minuter och använder alternativet för att ignorera krav kontroll varningar.

### <a name="retry-installation-for-the-site"></a>Gör om installationen för platsen

Gör om installationen av en uppdatering på en speciell plats när uppdateringen är i något av följande tillstånd:  

- Krav kontroller godkändes med en eller flera varningar och alternativet för att ignorera krav kontroll varningar angavs inte i uppdaterings guiden. (Värdet updates för **Ignorera krav-varning** i noden uppdateringar och underhåll är **Nej**.)  

- Kraven misslyckades

- Installationen misslyckades

Gå till arbets ytan **övervakning** och välj noden **plats underhålls status** . Välj uppdateringen och välj sedan ett av följande alternativ:  

- **Försök igen**: när du **försöker igen** från **plats underhålls statusen**startar du om installationen av uppdateringen på den platsen. Till skillnad från att köra **försök igen** från noden **uppdateringar och underhåll** , ignorerar det här försöket inga krav varningar.  

- **Ignorera krav kontroll varningar**: om installationen av uppdateringen stoppas på grund av en varning kan du välja **Ignorera krav varningar**. Den här åtgärden gör att uppdateringen kan fortsätta efter några minuter och använder alternativet för att ignorera krav kontroll varningar.  

## <a name="after-a-site-installs-an-update"></a><a name="bkmk_after"></a>När en plats har installerat en uppdatering  

När platsen har uppdaterats granskar du check listan efter uppdatering för den aktuella versionen:  

- [Check lista för uppdatering efter uppdatering för version 2006](checklist-for-installing-update-2006.md#post-update-checklist)

- [Check lista för uppdatering efter uppdatering för version 2002](checklist-for-installing-update-2002.md#post-update-checklist)

- [Check lista för uppdatering efter uppdatering för version 1910](checklist-for-installing-update-1910.md#post-update-checklist)  

- [Check lista för uppdatering efter uppdatering för version 1906](checklist-for-installing-update-1906.md#post-update-checklist)  

## <a name="enable-optional-features-from-updates"></a><a name="bkmk_options"></a>Aktivera valfria funktioner från uppdateringar  

När en uppdatering innehåller en eller flera valfria funktioner har du möjlighet att aktivera de funktionerna i hierarkin. Aktivera funktioner när uppdateringen installeras eller gå tillbaka till konsolen senare för att aktivera de valfria funktionerna.

Om du vill visa tillgängliga funktioner och deras status går du till arbets ytan **Administration** i-konsolen, expanderar **uppdateringar och service**och väljer noden **funktioner** .

När en funktion inte är valfri installeras den automatiskt. Den visas inte i noden **funktioner** .  

> [!IMPORTANT]
> I en hierarki med flera platser aktiverar du valfria eller för hands versions funktioner enbart från den centrala administrations platsen. Det här beteendet garanterar att det inte finns några konflikter i hierarkin. <!--507197-->  

När du aktiverar en ny funktion eller för hands versions funktion måste Configuration Manager Hierarchy Manager (HMAN) bearbeta ändringen innan funktionen blir tillgänglig. Bearbetningen av ändringen är ofta omedelbar. Beroende på bearbetnings cykeln för HMAN kan det ta upp till 30 minuter att slutföra. När ändringen har bearbetats startar du om-konsolen innan du kan använda funktionen.

Från och med version 2002,<!--5834830--> När nya molnbaserade funktioner är tillgängliga i administrations centret för Microsoft Endpoint Manager, eller andra anslutna moln tjänster för din lokala Configuration Manager-installation, kan du nu välja dessa nya funktioner i Configuration Manager-konsolen.

### <a name="list-of-optional-features"></a>Lista med valfria funktioner

Följande funktioner är valfria i den senaste versionen av Configuration Manager:<!--505213-->  

<!--Note to include in target articles

> [!NOTE]
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

-->

- [Community-hubb](community-hub.md)<!--3555935, C098DA03-C33C-4E15-B337-6C0FEEB3CB8A-->
- [Orkestreringsgrupper](../../../sum/deploy-use/orchestration-groups.md)<!--3098816, 290B66D8-C735-4895-B59A-DD732D84A697-->
- [Distributions typ för aktivitetssekvens](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!-- 3555953, CB0CDFFB-9C6F-4B18-8954-A43A387302A2-->
- [BitLocker-hantering](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [Synkronisera samlings medlemskaps resultat till Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->
- [Azure Active Directory användar grupp identifiering](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->
- [Program grupper](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->
- [Fel sökare för aktivitetssekvens](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71-->
- [Paket konverterings hanterare](../../../apps/pcm/package-conversion-manager.md) <!--1357861,4E0C09AF-7FC1-4412-A8BB-166D9BCD0093-->
- [Programuppdateringar från tredje part](../../../sum/deploy-use/third-party-software-updates.md)<!--1357605,1352101,1358714;B5E192AE-C81F-4348-9EF9-07A3C0FBE597-->
- [Godkänn program begär Anden för användare per enhet](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings) <!--1357015,4BA987C9-08FC-48E2-BFFE-C9DCF35B496A-->  
- [Skapa och köra skript](../../../apps/deploy-use/create-deploy-scripts.md) <!--1236459,566F8720-F415-4E10-9A51-CDE682BA2B2E-->
- [Uppdateringar av Surface-drivrutin](../../../sum/get-started/configure-classifications-and-products.md) <!--1098490,82AD973A-7CDF-4B67-A665-72875D6E099A-->
- [Gateway för molnhantering](../../clients/manage/cmg/plan-cloud-management-gateway.md) <!--1101764,DD043119-789C-4158-AC79-725E999F385A-->
- [Skapa PFX](../../../protect/deploy-use/introduction-to-certificate-profiles.md) <!--1321368,CED76B79-929C-4C45-981F-B9BCA6D38A17-->
- [Azure Log Analytics-anslutning](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm) <!--1258052,73A7EC4D-EF22-4EA4-82A9-419C2A8CFC4D-->
- [Windows Defender sårbarhet Guard-princip](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) <!--1355468,8491D4C8-8484-46B8-BCD6-17DC2CADBAEB-->
- [VPN för Windows 10](../../../protect/deploy-use/vpn-profiles.md) <!--1283610,EDBEBA3D-3A4D-4465-84D9-D71EB811E7F6-->
- [Underhålla en kluster medveten samling (Server grupper)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697-->
- [Windows Hello för företag](../../../protect/deploy-use/windows-hello-for-business-settings.md) (kallades tidigare *Passport for Work*) <!--1245704,8BCA2642-3719-4862-A355-9D39C979E1B4-->

> [!TIP]
> Mer information om funktioner som kräver medgivande för att aktivera finns i [för hands versions funktioner](pre-release-features.md).  
>
> Mer information om funktioner som endast är tillgängliga i den tekniska för hands versionen finns i [Technical Preview](../../get-started/technical-preview.md).

## <a name="use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a>Använd för hands versions funktioner från uppdateringar

Den aktuella grenen innehåller för hands versions funktioner för tidig testning i en produktions miljö. Mer information finns i [för hands versions funktioner](pre-release-features.md).

## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a>Vanliga frågor och svar

### <a name="why-dont-i-see-certain-updates-in-my-console"></a>Varför visas inte vissa uppdateringar i konsolen?

Om du inte kan hitta en speciell uppdatering i konsolen efter en lyckad synkronisering med Microsofts moln tjänst kan det här problemet bero på någon av följande orsaker:  

- Uppdateringen kräver en konfiguration som din infrastruktur inte använder, eller så uppfyller inte din nuvarande produkt version ett krav för att ta emot uppdateringen.  

    Om du tror att du har nödvändiga konfigurationer och krav för en saknad uppdatering kontrollerar du att tjänst anslutnings punkten är i onlineläge. Använd sedan alternativet **Sök efter uppdateringar** i noden **uppdateringar och underhåll** för att tvinga en kontroll. Om tjänst anslutnings punkten är i offlineläge använder du tjänst anslutnings verktyget för att synkronisera manuellt med moln tjänsten.  

- Ditt konto saknar rätt rollbaserade administrations behörigheter för att visa uppdateringar i Configuration Manager-konsolen. Mer information finns i [behörigheter för att hantera uppdateringar](#assign-permissions-to-view-and-manage-updates-and-features).  
