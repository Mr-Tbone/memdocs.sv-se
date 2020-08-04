---
title: Övervaka klienter
titleSuffix: Configuration Manager
description: Få detaljerad vägledning om hur du övervakar klienter i Configuration Manager
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 00a10e169db36c62b083c56114159b54185a1040
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87525921"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>Övervaka klienter i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du har installerat Configuration Manager-klienten på Windows-enheterna på din plats kan du övervaka deras hälsa och aktivitet i Configuration Manager-konsolen.  


## <a name="about-client-status"></a><a name="bkmk_about"></a>Om klient status

Configuration Manager innehåller följande typer av information som klient status:  

- **Klientens onlinestatus**: webbplatsen förbehåller sig en enhet som **online** om den är ansluten till den tilldelade hanterings platsen. För att indikera att klienten är online skickar den ping-liknande meddelanden till hanterings platsen. Om hanterings platsen inte tar emot ett meddelande på fem minuter, anser platsen att klienten är **offline**.  

- **Klient aktivitet**: platsen betraktar klienten som **aktiv** om den har kommunicerat med Configuration Manager de senaste sju dagarna. Platsen betraktar klienten **inaktiv** om den inte har utfört följande åtgärder på sju dagar:  

    - Begärd princip uppdatering  
    - Skickade ett pulsslags meddelande  
    - Skickade maskin varu inventering  

- **Klient kontroll**: statusen för den periodiska utvärderingen som Configuration Manager-klienten kör på enheten. Utvärderingen kontrollerar enheten och kan åtgärda några av de problem som hittas. Mer information finns i [klient hälso kontroller](#BKMK_ClientHealth).  

     På enheter som kör Windows 7 körs klient kontrollen som en schemalagd aktivitet. På senare operativ system versioner körs klient kontrollen automatiskt under Windows-underhålls fönstret.  

     Du kan konfigurera reparationen så att den inte körs på specifika enheter, till exempel en verksamhets kritisk Server. Om det finns fler objekt som du vill utvärdera använder du Configuration Manager kompatibilitetsinställningar för att övervaka ytterligare konfigurationer. Mer information om kompatibilitetsinställningar finns i [Planera för och konfigurera kompatibilitetsinställningar](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

- Inaktive **rad: platsen**har markerat enhets posten för borttagning. Det här problemet kan inträffa när en ny registrering för samma enhet tilldelas samma eller en annan primär plats i en hierarki. Platsen tar bort de här enheterna nästa gången den kör plats underhålls uppgiften **ta bort föråldrade identifierings data**.<!-- SCCMDocs issue #1418 -->  

- **Föråldrad**: platsen har identifierat en ny enhets post med samma maskinvaru-ID, så den gamla posten som föråldrad markeras. Rapporter räknar inte över gamla poster av samma enhet flera gånger. Du kan fortfarande rikta in dig på principer till inaktuella enheter. Om platsen inte får ett pulsslag för en inaktuell post efter 90 dagar av inaktivitet tas den föråldrade enheten bort när den kör plats underhålls uppgiften **ta bort föråldrade klient identifierings data**.


## <a name="monitor-individual-clients"></a><a name="bkmk_indStatus"></a>Övervaka enskilda klienter

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen. Välj antingen noden **enheter** eller Välj en samling under **enhets samlingar**.  

    Ikonerna i början av varje rad anger enhetens onlinestatus:  

    | Ikon | Description |
    | ---- | ----------- |  
    |![ikon för onlinestatus för klienter](../../../core/clients/manage/media/online-status-icon.png)|Enheten är online|  
    |![ikon för offlinestatus för klienter](../../../core/clients/manage/media/offline-status-icon.png)|Enheten är offline|  
    |![ikon för okänd status för klienter](../../../core/clients/manage/media/unknown-status-icon.png)|Online-statusen är okänd|  
    |![klienten är inte installerad](../../../core/clients/manage/media/client-not-installed.png)|Klienten är inte installerad på enheten|  

2. Om du vill ha mer detaljerad onlinestatus lägger du till statusinformation om klient online i vyn enhet. Högerklicka på kolumn rubriken och välj de online status fält som du vill lägga till:

    - **Status för enhet online**: anger om klienten är online eller offline. (Denna status är samma information som anges av ikonerna.)  

    - **Senaste online-tid**: anger när klientens onlinestatus ändrades till online  

    - **Senast offline** anger när statusen ändrades till offline  

3. Välj en enskild klient i list rutan för att se mer status i informations fönstret. Den här informationen omfattar klient aktivitet och klient kontroll status.  


## <a name="client-health-dashboard"></a><a name="bkmk_health"></a>Instrument panel för klient hälsa

<!--3599209-->
Du distribuerar program uppdateringar och andra appar för att skydda din miljö, men de här distributionerna når bara friska klienter. Fel Configuration Manager klienterna har negativ inverkan på övergripande kompatibilitet. Det kan vara svårt att avgöra klient hälsan beroende på vilken nämnare: hur många totala enheter som ska ingå i hanterings området? Om du till exempel upptäcker alla system från Active Directory, även om några av dessa poster är för inaktuella datorer, ökar den här processen din nämnare.

Från och med version 1902 kan du Visa en instrument panel med information om hälsan för Configuration Manager klienter i din miljö. Visa klient hälsan, scenariots hälsa och vanliga fel. Filtrera vyn efter flera attribut för att se eventuella eventuella problem med operativ system och klient versioner.

Gå till arbets ytan **övervakning** i Configuration Manager-konsolen. Expandera **klient status**och välj noden **klient hälso instrument panel** .

![Skärm bild för klient hälso instrument panel](media/3599209-client-health-dashboard.png)

> [!Tip]  
> Det finns inga ändringar i ccmeval.  

Som standard visar instrument panelen för klient hälsa online klienter och klienter som är aktiva under de senaste tre dagarna. Därför kan du se olika nummer på den här instrument panelen än i andra historiska källor av klient hälsan. Till exempel andra noder under **klient status**eller rapporter i kategorin klient status.

### <a name="filters"></a>Filter

Överst på instrument panelen finns det en uppsättning filter för att justera de data som visas i instrument panelen.

- **Samling**: som standard visar instrument panelen enheter i samlingen **alla system** . Välj en enhets samling i listan om du vill begränsa vyn till en delmängd enheter i en viss samling.  

- **Online/offline**: på instrument panelen visas som standard endast online-klienter. Det här tillståndet kommer från klient meddelande kanalen som uppdaterar en klients status var femte minut. Mer information finns i [om klient status](monitor-clients.md#bkmk_about).  

- **Aktiva \# dagar**: instrument panelen visar som standard klienter som är aktiva under de senaste tre dagarna.  

- **Endast fel**: begränsa vyn till endast enheter som rapporterar ett klient hälso fel.  

    > [!Tip]  
    > Använd det här filtret tillsammans med klient versionen och operativ systemets versions paneler. Mer information finns i [versions paneler](#version-tiles).

### <a name="client-health-percentage"></a>Procent för klient hälsa

Den här panelen visar det övergripande klient hälsan i hierarkin.

En felfri Configuration Manager-klient har följande egenskaper:

- Online  
- Skicka data aktivt  
- Överför alla utvärderings kontroller för klient hälsa  

Mer information finns i [om klient status](monitor-clients.md#bkmk_about).

En felfri klient kommunicerar med platsen. Den rapporterar alla data baserat på de definierade schemana i klient inställningar.

Välj ett segment i det här diagrammet för att öka detalj nivån för en enhets List visning.

### <a name="version-tiles"></a>Versions paneler

Det finns två paneler som visar klient hälsan med Configuration Manager klient version och operativ system version. Dessa paneler är användbara när du gör ändringar i filtren, t. ex. **endast felaktiga**. De kan hjälpa dig att framhäva om några problem är konsekventa i en speciell version. Använd den här informationen för att hjälpa dig att fatta beslut om uppgradering.

Välj ett segment av de här diagrammen för att öka detalj nivån för en enhets List visning.

### <a name="scenario-health"></a>Scenariots hälsa

Det här stapeldiagrammet visar det övergripande hälso tillståndet för följande kärn scenarier:

- Klient princip
- Pulsslags identifiering
- Maskinvaruinventering
- Programvaruinventering
- Statusmeddelanden

Använd markeringarna för att justera fokus på vissa scenarier i diagrammet.

Följande två staplar visas alltid:

- **Kombinerat (alla)**: kombinationen av alla scenarier (och)  
- **Kombinerat (any)**: minst ett av scenarierna (eller)

> [!Tip]  
> Scenariots hälsa mäts inte i konfigurationen av klient inställningar. Dessa värden kan variera beroende på gällande princip uppsättning per enhet. Använd följande steg för att justera utvärderings perioder för scenario hälsa:
>
> - I Configuration Manager-konsolen går du till arbets ytan **övervakning** och väljer noden **klient status** .  
> - I menyfliksområdet väljer du **Inställningar för klient status**.  
>
> Som standard, om en klient inte skickar scenariobaserade data på **sju dagar**, anser Configuration Manager att den inte är felfri för det scenariot.

### <a name="top-10-client-health-failures"></a>Främsta 10 klient hälso fel

Det här diagrammet visar de vanligaste felen i din miljö. Felen kommer från Windows eller Configuration Manager.

<!-- The following list includes some of the more common failures overall:

#### Failure 1 title
Failure 1 description

Solution for failure 1 -->


## <a name="monitor-the-status-of-all-clients"></a><a name="bkmk_allStatus"></a>Övervaka status för alla klienter

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** och väljer noden **klient status** . Granska den övergripande statistiken för klient aktivitet och klient kontroller på platsen. Ändra omfattningen för informationen genom att välja en annan samling.  

2. Om du vill öka detalj nivån om den rapporterade statistiken väljer du namnet på den rapporterade informationen. Till exempel **aktiva klienter som har godkänts i klient kontrollen eller inga resultat**. Granska sedan informationen om de enskilda klienterna.  

3. Välj **klient aktivitet** för att visa diagram som visar klient aktiviteten på din Configuration Manager webbplats.  

4. Välj **klient kontroll** för att visa diagram som visar statusen för klient kontroller på din Configuration Manager webbplats.  

    Konfigurera aviseringar för att meddela dig när klient kontroll resultat eller klient aktivitet sjunker under en angiven procent andel. Platsen kan också varna dig när reparationen Miss lyckas på en angiven procent andel av klienterna. Mer information finns i [så här konfigurerar du klient status](../deploy/configure-client-status.md).  


## <a name="client-health-checks"></a><a name="BKMK_ClientHealth"></a>Klient hälso kontroller

Klient kontrollen kör följande kontroller och reparationer:  

|Klientkontroll|Reparationsåtgärd|Mer information|  
|------------------|------------------------|----------------------|  
|Kontrollera att klientkontrollen nyligen har körts|Kör klientkontroll|Kontrollerar att klientkontrollen har körts minst en gång under de senaste tre dagarna.|  
|Kontrollera att alla klientkrav är installerade|Installera klientkrav|Kontrollerar att alla klientkrav är installerade. Identifierar krav genom att läsa filen ccmsetup.xml i klientinstallationsmappen.|  
|Integritetstest för WMI-lagringsplats|Installera om Configuration Manager-klienten|Kontrollerar att Configuration Manager klient poster finns i WMI.|  
|Verifiera att klienttjänsten körs|Starta klienttjänsten (SMS Agent Host)|Ingen ytterligare information|  
|Mottagartest för WMI-händelse.|Starta om klienttjänsten|Kontrol lera om den Configuration Manager relaterade WMI-händelsens Sink går förlorad|  
|Verifiera att WMI-tjänsten (Windows Management Instrumentation) finns|Ingen reparation|Ingen ytterligare information|  
|Verifiera att klienten har installerats|Installera klienten|Ingen ytterligare information|  
|Verifiera att antivirustjänstens starttyp är automatisk|Återställ tjänstens starttyp till automatisk|Ingen ytterligare information|  
|Verifiera att antivirustjänsten körs|Starta antivirustjänsten|Ingen ytterligare information|  
|Verifiera att Windows Update-tjänstens starttyp är automatisk eller manuell|Återställ tjänstens starttyp till automatisk|Ingen ytterligare information|  
|Verifiera att klienttjänstens (SMS Agent Host) starttyp är automatisk|Återställ tjänstens starttyp till automatisk|Ingen ytterligare information|  
|Verifiera att WMI-tjänsten (Windows Management Instrumentation) körs.|Starta Windows Management Instrumentation-tjänsten|Ingen ytterligare information|  
|Verifiera att Microsoft SQL CE-databasen är felfri|Installera om Configuration Manager-klienten|Ingen ytterligare information|  
|Integritetstest för Microsofts Policy Platform WMI|Reparera Microsofts Policy Platform|Ingen ytterligare information|  
|Kontrollera att tjänsten Microsoft Policy Platform finns|Reparera Microsofts Policy Platform|Ingen ytterligare information|  
|Verifiera att starttypen för tjänsten Microsoft Policy Platform är manuell|Återställ tjänstens starttyp till manuell|Ingen ytterligare information|  
|Verifiera att BITS-tjänsten (Background Intelligent Transfer Service) finns|Ingen reparation|Ingen ytterligare information|  
|Verifiera att BITS-tjänstens starttyp är automatisk eller manuell|Återställ tjänstens starttyp till automatisk|Ingen ytterligare information|  
|Verifiera att starttypen för nätverksinspektionstjänsten är manuell.|Återställ tjänstens starttyp till manuell om tjänsten är installerad|Ingen ytterligare information|  
|Verifiera att WMI-tjänstens (Windows Management Instrumentation) starttyp är automatisk.|Återställ tjänstens starttyp till automatisk|Ingen ytterligare information|  
|Verifiera att Windows Update tjänstens starttyp på Windows 8-enheter är automatisk eller manuell|Återställ tjänstens starttyp till manuell|Ingen ytterligare information|  
|Verifiera att klienttjänsten (SMS Agent Host) finns.|Ingen reparation|Ingen ytterligare information|  
|Verifiera att tjänsten för Configuration Manager-fjärrstyrning har starttypen automatisk eller manuell|Återställ tjänstens starttyp till automatisk|Ingen ytterligare information|  
|Verifiera att tjänsten för Configuration Manager-fjärrstyrning körs|Starta fjärrstyrningstjänsten|Ingen ytterligare information|  
|Verifiera att aktiveringsproxytjänsten (ConfigMgr Wake-up Proxy) körs|Starta tjänsten ConfigMgr Wakeup Proxy|Den här klient kontrollen görs bara om klient inställningen **energispar funktioner**: **Aktivera aktivering av proxy** är inställd på **Ja** på klient operativ system som stöds.|  
|Verifiera att aktiveringsproxytjänstens (ConfigMgr Wake-up Proxy) starttyp är automatisk|Återställ ConfigMgr Wakeup Proxy-tjänstens starttyp till automatisk|Den här klient kontrollen görs bara om klient inställningen **energispar funktioner**: **Aktivera aktivering av proxy** är inställd på **Ja** på klient operativ system som stöds.|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>Loggfiler för klient distribution

Mer information om loggfiler som används av distributions-och hanterings åtgärder för klienter finns i [loggfiler](../../plan-design/hierarchy/log-files.md#BKMK_ClientLogs).
