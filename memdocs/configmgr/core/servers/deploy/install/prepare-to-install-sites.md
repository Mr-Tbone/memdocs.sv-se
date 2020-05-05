---
title: Förbereda för att installera platser
titleSuffix: Configuration Manager
description: Om du planerar att installera flera Configuration Manager-platser läser du den här informationen för att hjälpa dig att spara tid och förhindra fel.
ms.date: 09/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 87c1713f9903cf704e484c49f7e720e6f0bd3e4a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718184"
---
# <a name="prepare-to-install-configuration-manager-sites"></a>Förbered för att installera Configuration Manager-platser

*Gäller för: Configuration Manager (aktuell gren)*

För att förbereda för en lyckad distribution av en eller flera Configuration Manager webbplatser kan du bekanta dig med informationen i den här artikeln. Med de här stegen kan du spara tid under installationen av flera platser och hjälpa till att förhindra fel steg som kan leda till att du måste installera om en eller flera platser.

> [!TIP]
> När du hanterar Configuration Manager plats-och hierarki-infrastruktur används villkoren *Uppgradera*, *Uppdatera*och *Installera* för att beskriva tre olika begrepp. Information om hur varje term används finns i [om uppgradering, uppdatering och installation](../../../understand/upgrade-update-install.md).

## <a name="options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a>Alternativ för att installera olika typer av platser
När du installerar en ny Configuration Manager-plats beror den version av källfilerna som du kan använda på den version av-platser som redan finns i hierarkin (om det finns några). Vilka installations metoder som du kan använda beror på vilken typ av plats du vill installera.  

Innan du installerar en-plats måste du kontrol lera att du har planerat din hierarki och att du förstår vilken typ av plats du vill installera. Mer information finns i [utforma en hierarki med-platser](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).


### <a name="first-site"></a>Första platsen
Den första platsen som du installerar i en hierarki är antingen en fristående primär plats eller en central administrations plats.

**Installations medium**: om du vill installera en central administrations plats eller en fristående primär plats som första plats i en ny hierarki måste du [använda en bas linje version](../../../../core/servers/manage/updates.md#bkmk_Baselines) av Configuration Manager. Installera inte den första platsen i en ny hierarki genom att använda uppdaterade källfiler från [CD: n. Den senaste mappen](../../../../core/servers/manage/the-cd.latest-folder.md) på en plats.

**Installations metod**: du kan installera valfri typ av plats med hjälp av [installations guiden för Configuration Manager](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md), eller så kan du konfigurera ett skript som ska användas med en [kommando rads installation med skript](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Ytterligare platser
När den första platsen har installerats kan du lägga till fler platser när som helst. Du har följande alternativ för att lägga till platser (upp till [gränser som stöds](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

|Plats som du har|Ytterligare plats typ som du kan installera|
|---|---|
|Central administrationsplats|Underordnad primär plats|
|Underordnad primär plats|Sekundär plats|
|Fristående primär plats|Sekundär plats (du kan expandera den primära platsen, som konverterar den fristående primära platsen till en underordnad primär plats)|

**Installations medium**: när du installerar en central administrations plats för att expandera en fristående primär plats, eller om du installerar en ny underordnad primär plats i en befintlig hierarki, måste du använda installationsmedia (som innehåller källfiler) som matchar versionen av den befintliga platsen eller platserna.

> [!IMPORTANT]
> Om du har installerat uppdateringar i konsolen som har ändrat versionen av de tidigare installerade platserna ska du inte använda det ursprungliga installations mediet. I det scenariot använder du i stället källfiler från [CD: n. Den senaste mappen](../../../../core/servers/manage/the-cd.latest-folder.md) på en uppdaterad webbplats. Configuration Manager kräver att du använder källfiler som matchar versionen av den befintliga platsen som den nya platsen kommer att ansluta till.

En sekundär plats måste installeras från Configuration Manager-konsolen. På så sätt installeras sekundära platser alltid med hjälp av källfiler från den överordnade primära platsen.

**Installations metod**: den metod som du använder för att installera ytterligare platser beror på vilken typ av plats du vill installera.
- **Lägg till en central administrations plats**: du kan använda installations guiden för Configuration Manager eller en skriptad kommando rad för att installera den nya centrala administrations platsen som en överordnad plats till din befintliga fristående primära plats. Mer information finns i [expandera en fristående primär plats](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
- **Lägg till en underordnad primär plats**: du kan använda installations guiden för Configuration Manager eller en kommando rads installation för att lägga till en underordnad primär plats under en central administrations plats.
- **Lägg till en sekundär plats**: Använd Configuration Manager-konsolen för att installera en sekundär plats som en underordnad plats under en primär plats. Andra metoder stöds inte för att lägga till sekundära platser.

## <a name="common-tasks-to-complete-before-starting-an-installation"></a><a name="bkmk_tasks"></a>Vanliga aktiviteter som ska slutföras innan en installation startas
- **Förstå hierarkin som du ska använda för din distribution**    
Mer information finns i [utforma en hierarki med webbplatser för Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

- **Förbered och konfigurera enskilda servrar för att uppfylla krav och konfigurationer som stöds för användning med Configuration Manager**         
Mer information finns i [krav för plats och plats system](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

- **Installera och konfigurera SQL Server som värd för plats databasen**     
Mer information finns i [stöd för SQL Server-versioner för Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

- **Förbered nätverks miljön för att stödja Configuration Manager**      
Mer information finns i [Konfigurera brand väggar, portar och domäner för att förbereda för Configuration Manager](../../../../core/plan-design/network/configure-firewalls-ports-domains.md).  

- **Om du ska använda en PKI (Public Key Infrastructure), Förbered din infrastruktur och dina certifikat**      
Mer information finns i [krav på PKI-certifikat för Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).

- **Installera de senaste säkerhets uppdateringarna på datorer som du kommer att använda som plats servrar eller plats system servrar, och vid behov startar du om dem**

## <a name="about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a>Om plats namn och plats koder
Plats koder och plats namn används för att identifiera och hantera platserna i en Configuration Manager hierarki. I &lt;Configuration Manager-konsolen visas plats koden och plats namnet i formatet plats*namn* \> för *plats kod*\> - &lt;. Alla plats koder som du använder i hierarkin måste vara unika. Om Active Directory-schemat har utökats för Configuration Manager och dina platser publicerar data, måste de plats koder som används i en Active Directory skog vara unika, även om de används i en annan Configuration Manager-hierarki eller om de har använts i tidigare Configuration Manager installationer. Var noga med att planera dina plats koder och plats namn innan du distribuerar din-hierarki.

### <a name="specify-a-site-code-and-site-name"></a>Ange platskod och plats namn
När du kör Configuration Manager installationen uppmanas du att ange en platskod och ett plats namn för den centrala administrations platsen och för varje primär plats och sekundär plats installation. En platskod måste unikt identifiera varje plats i hierarkin. Eftersom plats koden används i mappnamn ska du aldrig använda följande namn för plats koden, som inkluderar reserverade namn för Configuration Manager och Windows:
- AUX
- CON
- NUL
- PRN
- SMS
- ENV <!--SCCMDocs-1871 and 5399453-->

> [!NOTE]
> Installations programmet för Configuration Manager kontrollerar inte att ingen platskod redan används.

Om du vill ange plats koden för en plats när du kör Configuration Manager installationen måste du ange tre alfanumeriska tecken. Endast bokstäverna *A* till *Z* och siffrorna *0* till *9*, i valfri kombination, är tillåtna i plats koder. Sekvensen av bokstäver eller siffror har ingen påverkan på kommunikationen mellan platser. Till exempel är det inte nödvändigt att namnge en primär plats *ABC* och en sekundär plats *definition*.

Plats namnet är en identifierare för eget namn för platsen. Du kan bara använda tecknen *a* till *z*, *a* till *z*, *0* till *9*och bindestreck (*-*) i webbplats namn.

> [!IMPORTANT]
> Det finns inte stöd för att ändra plats koden eller plats namnet när du har installerat platsen.

### <a name="reuse-a-site-code"></a>Återanvänd en platskod
Plats koder kan inte användas mer än en tid i en Configuration Manager-hierarki för en central administrations plats eller för en primär plats, även om den ursprungliga platsen och plats koden har avinstallerats. Om du återanvänder en platskod riskerar du att ha objekt-ID-konflikter i hierarkin. Du kan återanvända plats koden för en sekundär plats om den sekundära platsen och plats koden inte längre används i Configuration Manager-hierarkin eller i Active Directory skogen.

## <a name="limits-and-restrictions-for-installed-sites"></a>Begränsningar och begränsningar för installerade platser
Innan du installerar en-plats är det viktigt att förstå följande begränsningar som gäller för platser och plats-hierarkier:
- När du har kört installationen kan du inte ändra följande plats egenskaper utan att avinstallera platsen och sedan installera om den med hjälp av de nya värdena:  
  - Installations katalog för programfiler  
  - Platskod  
  - Plats Beskrivning  
- När din-hierarki innehåller en central administrations plats:  
  - Configuration Manager har inte stöd för att flytta en underordnad primär plats från en hierarki för att skapa en fristående primär plats eller för att koppla den till en annan hierarki. Avinstallera i stället den underordnade primära platsen och installera sedan om den som en ny fristående primär plats eller som en underordnad plats till den centrala administrations platsen i en annan hierarki.  


## <a name="optional-steps-before-running-setup"></a><a name="bkmk_optionalsteps"></a>Valfria steg innan du kör installations programmet
**Kör [installations hämtaren](../../../../core/servers/deploy/install/setup-downloader.md) manuellt**

Om du vill hämta de uppdaterade installationsfilerna för Configuration Manager kan du köra installations hämtaren. Om datorn där du ska köra installations programmet inte är ansluten till Internet, eller om du förväntar dig att installera flera plats servrar, bör du överväga att använda installations hämtaren för att hämta de uppdateringar som krävs för installationen. Här är ytterligare information:
- Som standard ansluter installations programmet till Internet för att hämta uppdaterade installationsfiler.
- Som standard lagras filerna i Redist-mappen.
- Du kan dirigera installationen till en plats i nätverket där du tidigare har lagrat en kopia av filerna.

**Kör [krav kontrollen](../../../../core/servers/deploy/install/prerequisite-checker.md) manuellt**

För att identifiera och åtgärda problem innan du kör installations programmet för att installera en plats och innan du installerar en plats system roll på en server, kan du köra krav kontrollen. Krav kontrollen hjälper till att säkerställa att datorn uppfyller kraven för att vara värd för plats-eller plats system rollen. Här är ytterligare information:
- Som standard kör installations programmet krav kontroll.
- Om det finns några fel stoppas installationen tills problemet har åtgärd ATS.

**Identifiera valfria portar**

Du kan identifiera valfria portar för plats system och klienter som ska användas. Här är ytterligare information:
- Som standard använder plats system och klienter fördefinierade portar för att kommunicera.
- Under installationen kan du konfigurera alternativa portar.

Mer information finns i [portar som används](../../../../core/plan-design/hierarchy/ports.md).
