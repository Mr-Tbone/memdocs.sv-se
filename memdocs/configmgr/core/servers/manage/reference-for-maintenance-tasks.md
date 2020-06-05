---
title: Referens för underhållsaktivitet
titleSuffix: Configuration Manager
description: Information för var och en av Configuration Manager plats underhålls aktiviteter
ms.date: 06/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e989de5acab778374c233862d0ab4d7077899d28
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428601"
---
# <a name="reference-for-maintenance-tasks-in-configuration-manager"></a>Referens för underhålls aktiviteter i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller information om var och en av de Configuration Manager plats underhålls aktiviteterna. Varje post anger de plats typer där aktiviteten är tillgänglig och om den är aktive rad som standard.

Mer information finns i [Konfigurera underhålls aktiviteter](maintenance-tasks.md#set-up-maintenance-tasks).  

## <a name="tasks"></a>Aktiviteter

### <a name="backup-site-server"></a>Platsserver för säkerhetskopiering

Använd den här aktiviteten för att skapa en säkerhets kopia av den viktiga informationen för att återställa en plats och den Configuration Manager databasen. Mer information finns i [säkerhetskopiera en Configuration Manager webbplats](backup-and-recovery.md).  

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Inte aktiverat|
|Sekundär plats|Inte tillgänglig|

### <a name="check-application-title-with-inventory-information"></a>Kontrol lera program titel med inventerings information

Använd den här aktiviteten för att bevara program varu titlarnas konsekvens mellan program varu inventeringen och Tillgångsinformation katalogen. Mer information finns i [Introduktion till tillgångsinformation](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|Primär plats|Inte tillgänglig|
|Sekundär plats|Inte tillgänglig|

### <a name="clear-undiscovered-clients"></a>Rensa klienter som inte är identifierade

> [!Tip]
> Du kan också se den här uppgiften i-konsolen med namnet **Rensa installations flagga**.

Använd den här aktiviteten för att ta bort den installerade flaggan för klienter som inte skickar en pulsslags identifierings post under perioden för **Återidentifiering av klienten** . Den installerade flaggan förhindrar automatisk push-installation av klienter till en dator som kan ha en aktiv Configuration Manager-klient.  

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Inte aktiverat|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-application-request-data"></a>Ta bort föråldrade program förfrågnings data

Använd den här aktiviteten för att ta bort föråldrade program begär Anden från databasen. Mer information finns i [skapa och distribuera ett program](../../../apps/get-started/create-and-deploy-an-application.md).  

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-application-revisions"></a>Ta bort föråldrade program revisioner

Använd den här aktiviteten för att ta bort program revisioner som inte längre refereras. Mer information finns i [ändra och ersätta program](../../../apps/deploy-use/revise-and-supersede-applications.md).

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-client-download-history"></a>Ta bort föråldrad klient hämtnings historik

Använd den här aktiviteten för att ta bort historiska data om nedladdnings källan som används av klienter. Webbplatsen använder nedladdnings käll information för att fylla i [instrument panelen för klient data källor](../deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-client-operations"></a>Ta bort föråldrade klientåtgärder

Använd den här aktiviteten för att ta bort alla föråldrade data för klient åtgärder från plats databasen. Dessa data innehåller till exempel följande åtgärder:

- Föråldrade eller utgångna klient meddelanden, t. ex. nedladdnings begär Anden för datorn eller användar
- Endpoint Protection, som begär anden av en administrativ användare för klienter, köra en sökning eller hämta uppdaterade definitioner
- Kör skript status resultat

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-client-presence-history"></a>Ta bort närvaro historik för inaktuell klient
<!-- not listed in dogfood for either primary or CAS, was it renamed? -->
Använd den här aktiviteten för att ta bort historik information om onlinestatus för klienter som registrerats av klient meddelanden. Den tar bort information för klienter med status som är äldre än den angivna tiden. Mer information finns i [övervaka klienter](../../clients/manage/monitor-clients.md).

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-cloud-management-gateway-traffic-data"></a>Ta bort föråldrade Cloud Management Gateway trafik data

Använd den här aktiviteten för att ta bort alla föråldrade data om den trafik som passerar via [Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md). Dessa data omfattar:

- Antal begär Anden
- Totalt antal byte för begäran
- Totalt antal svars byte
- Antal misslyckade förfrågningar
- Maximalt antal samtidiga begär Anden

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-cmpivot-results"></a>Ta bort föråldrade CMPivot-resultat

Använd den här aktiviteten för att ta bort information om föråldrade plats databaser från klienter i CMPivot-frågor. Mer information finns i [CMPivot för real tids data](cmpivot.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-collected-files"></a>Ta bort föråldrade insamlade filer

Använd den här aktiviteten för att ta bort information om insamlade filer från databasen. Den här aktiviteten tar också bort insamlade filer från platsservermappstrukturen på den valda platsen. Som standard lagras de fem senaste kopiorna av insamlade filer på plats servern i **katalogen Inboxes\sinv.box\Filecol** -katalogen. Mer information finns i [Introduktion till program varu inventering](../../clients/manage/inventory/introduction-to-software-inventory.md).  

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-computer-association-data"></a>Ta bort föråldrade dator Associations data

Använd den här aktiviteten för att ta bort från databasen föråldrade operativ system för distribution av dator Association data. Den här informationen används när du återställer användar tillstånd under en aktivitetssekvens. Mer information finns i [hantera användar tillstånd](../../../osd/get-started/manage-user-state.md).  

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-console-connection-data"></a>Ta bort föråldrade konsol anslutnings data

Den här uppgiften tar bort data från plats databasen om konsol anslutningar till platsen.<!-- SCCMDocs#528 -->

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-delete-detection-data"></a>Ta bort föråldrade borttagnings identifierings data

Använd den här aktiviteten för att ta bort föråldrade data från databasen som har skapats av extraherings vyer. Den tar bort gammal data ändrings information som används av externa system för att extrahera data från databasen.<!--SCCMDocs#1590--><!--By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.-->

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-device-wipe-record"></a>Ta bort föråldrad enhets rensnings post

Använd den här aktiviteten för att ta bort inaktuella data om rensnings åtgärder för mobila enheter. Mer information finns i [skydda data med fjär rensning, låsning eller lösen ords återställning](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-discovery-data"></a>Ta bort föråldrade identifieringsdata

Använd den här aktiviteten för att ta bort föråldrade identifierings data från databasen. Dessa data kan innehålla poster från:

- Pulsslags identifiering
- Nätverksidentifiering
- Active Directory identifierings metoder: system, användare och grupp

Den här aktiviteten tar också bort föråldrade enheter som marker ATS som inaktiverade. När den här aktiviteten körs på en plats tas data som är kopplad till den platsen bort och dessa ändringar replikeras till andra platser. Mer information finns i [Kör identifiering](../deploy/configure/run-discovery.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-distribution-point-usage-stats"></a>Ta bort föråldrad distributions plats användnings statistik

Använd den här aktiviteten för att ta bort föråldrade data för distributions platser som har lagrats längre än en angiven tid.  

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-enrolled-devices"></a>Ta bort föråldrade registrerade enheter

Använd den här aktiviteten för att ta bort föråldrade data om mobila enheter som inte har rapporterat någon information till platsen under en viss tid.

Den här uppgiften gäller enheter som har registrerats med Configuration Manager [lokal MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md). Mer information om dessa enheter finns i [operativ system som stöds för klienter och enheter](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Inte aktiverat|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-ep-health-status-history-data"></a>Ta bort föråldrade historik data över EP-hälsostatus

Använd den här aktiviteten om du vill ta bort informationen om föråldrad databas för Endpoint Protection (EP). Mer information finns i [så här övervakar du Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-exchange-partnership"></a>Ta bort föråldrat Exchange-partnerskap

> [!Tip]
> > Du kan också se den här uppgiften i-konsolen med namnet **ta bort föråldrade enheter som hanteras av Exchange Server-anslutningen**.

Använd den här aktiviteten för att ta bort föråldrade data om mobila enheter som hanteras av Exchange Server-anslutningen. Platsen tar bort dessa data enligt inställningen **Ignorera mobila enheter som är inaktiva i mer än (dagar)** på fliken **identifiering** i egenskaperna för Exchange Server-anslutningen. Mer information finns i [Hantera mobila enheter med Configuration Manager och Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-inventory-history"></a>Ta bort föråldrad inventerings historik

Använd den här aktiviteten för att ta bort data från databas inventerings data som har lagrats längre än en angiven tid. Mer information finns i [använda Resursläsaren för att Visa maskin varu inventering](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-log-data"></a>Ta bort föråldrade loggdata

Använd den här aktiviteten för att ta bort inaktuella loggdata som används för fel sökning. Dessa data är inte relaterade till Configuration Manager komponent åtgärder.  

> [!IMPORTANT]  
> Som standard körs den här aktiviteten dagligen på varje plats. På en central administrations plats och primära platser, tar aktiviteten bort data som är äldre än 30 dagar. När du använder SQL Server Express på en sekundär plats, se till att den här aktiviteten körs dagligen och tar bort data som är inaktiva i sju dagar.  

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|**Sekundär plats**|Enabled|

### <a name="delete-aged-metering-data"></a>Ta bort föråldrade mätnings data

Använd den här aktiviteten för att ta bort inaktuella data från databasen för avläsning av program vara som har lagrats längre än en angiven tid. Mer information finns i [avläsning av program vara](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-metering-summary-data"></a>Ta bort föråldrade mätar sammanfattnings data

Använd den här aktiviteten för att ta bort inaktuella sammanfattnings data för program mätning som har lagrats längre än en angiven tid. Mer information finns i [avläsning av program vara](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-notification-server-history"></a>Ta bort föråldrad meddelande Server historik

Den här uppgiften tar bort föråldrade klient närvaro historik.

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-notification-task-history"></a>Ta bort föråldrade meddelande uppgifts historik

Använd den här aktiviteten för att ta bort information om klient aviseringar från plats databasen. Den här uppgiften gäller för data som inte har uppdaterats under en viss tid. Mer information finns i [klient meddelanden](../../clients/manage/client-notification.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-passcode-records"></a>Ta bort föråldrade lösen post poster

Använd den här aktiviteten på platsen på den översta nivån i hierarkin för att ta bort föråldrade lösen ords återställnings data för Windows Phone enheter. Data för återställning av lösen ord krypteras, men innehåller PIN-koden för enheter. Den här aktiviteten är aktive rad som standard och tar bort data som är äldre än en dag.  

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-replication-data"></a>Ta bort föråldrade replikeringsdata

Använd den här aktiviteten för att ta bort inaktuella data om databasreplikering mellan Configuration Manager-platser. När du ändrar konfigurationen för den här underhållsaktiviteten så används konfigurationen på alla tillämpliga platser i hierarkin. Mer information finns i [övervaka databasreplikering](monitor-replication.md).  

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|**Sekundär plats**|Enabled|

### <a name="delete-aged-replication-summary-data"></a>Ta bort sammanfattnings data för föråldrad replikering

Använd den här aktiviteten för att ta bort sammanfattnings data för föråldrad replikering av plats databasen när den inte har uppdaterats för en angiven tid. Mer information finns i [övervaka databasreplikering](monitor-replication.md).  

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|**Sekundär plats**|Enabled|

### <a name="delete-aged-status-messages"></a>Ta bort föråldrade status meddelanden

Använd den här aktiviteten för att ta bort data från databasen föråldrade status meddelanden som har kon figurer ATS i status filter regler. Mer information finns i [övervaka status systemet för Configuration Manager](use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus).

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-threat-data"></a>Ta bort föråldrade hot data

Använd den här aktiviteten för att ta bort inaktuella Endpoint Protection hot data från databasen som har lagrats längre än en angiven tid. Mer information finns i [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-unknown-computers"></a>Ta bort föråldrade okända datorer

Använd den här aktiviteten för att ta bort information om okända datorer från plats databasen när den inte har uppdaterats under en viss tid. Mer information finns i [förbereda för okända dator distributioner](../../../osd/get-started/prepare-for-unknown-computer-deployments.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-aged-user-device-affinity-data"></a>Ta bort föråldrade tillhörighets data för användare

Använd den här aktiviteten för att ta bort föråldrade tillhörighets data för användare och enheter från databasen. Mer information finns i [Länka användare och enheter med mappning mellan användare och enhet](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-duplicate-system-discovery-data"></a>Ta bort dubbla system identifierings data

Använd den här aktiviteten om du vill ta bort alla dubblettposter som skapats av system identifieringen från plats databasen.<!-- SCCMDocs#1339 -->

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|Primär plats|Inte tillgänglig|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-expired-mdm-bulk-enroll-package-records"></a>Ta bort utgångna poster i MDM-Mass registrering

Använd den här aktiviteten för att ta bort gamla Mass registrerings certifikat och motsvarande profiler när registrerings certifikatet har gått ut. Mer information finns i [Skapa certifikat profiler](../../../protect/deploy-use/create-certificate-profiles.md).

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-inactive-client-discovery-data"></a>Ta bort inaktiva klient identifierings data

Använd den här aktiviteten för att ta bort data från databas identifierings data för inaktiva klienter. Platsen markerar klienter som inaktiva när klienten flaggas som föråldrad och av konfigurationer som har gjorts för klient status.

Den här aktiviteten fungerar bara på resurser som är Configuration Manager klienter. Det skiljer sig från aktiviteten **ta bort föråldrade identifierings data** , vilket tar bort alla föråldrade identifierings data poster. När den här aktiviteten körs på en plats tas data bort från databasen på alla platser i en hierarki. Mer information finns i [så här konfigurerar du klient status](../../clients/deploy/configure-client-status.md).

> [!IMPORTANT]  
> När den är aktive rad konfigurerar du den här aktiviteten så att den körs vid ett intervall som är större än schemat för **pulsslags identifiering** . Den här konfigurationen gör det möjligt för aktiva klienter att skicka en pulsslags identifierings post för att markera klient posten som aktiv så att den här aktiviteten inte tar bort dem.  

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Inte aktiverat|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-obsolete-alerts"></a>Ta bort föråldrade aviseringar

Använd den här aktiviteten för att ta bort inaktuella aviseringar som har lagrats längre än en angiven tid. Mer information finns i [använda aviseringar och status systemet](use-alerts-and-the-status-system.md).

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-obsolete-client-discovery-data"></a>Ta bort föråldrade klient identifierings data

Använd den här aktiviteten för att ta bort föråldrade klient poster från databasen. En post som är markerad som föråldrad har vanligt vis ersatts av en nyare post för samma klient. Den nyare posten blir klientens aktuella post. Information om identifiering finns i [Kör identifiering](../deploy/configure/run-discovery.md).

> [!IMPORTANT]  
> När den är aktive rad konfigurerar du den här aktiviteten så att den körs vid ett intervall som är större än schemat för pulsslags identifiering. Den här konfigurationen gör att klienten kan skicka en pulsslags identifierings post som anger den föråldrade statusen korrekt.  

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Inte aktiverat|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-obsolete-forest-discovery-sites-and-subnets"></a>Ta bort föråldrade identifierings platser och undernät för skogar

Använd den här aktiviteten för att ta bort data om Active Directory platser, undernät och domäner. Den tar bort data som platsen inte har identifierat av Active Directory skogs identifierings metod under de senaste 30 dagarna. Den här uppgiften tar bort identifierings data, men påverkar inte gränser som du skapar från dessa identifierings data. Mer information finns i [Kör identifiering](../deploy/configure/run-discovery.md).

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="delete-orphaned-client-deployment-state-records"></a>Ta bort överblivna poster för klient distributions tillstånd

Använd den här aktiviteten för att regelbundet rensa den tabell som innehåller information om klient distributions tillstånd. Den här uppgiften rensar poster som är associerade med inaktuella eller inaktiverade enheter.  

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="evaluate-collection-members"></a>Utvärdera samlings medlemmar

Du konfigurerar utvärderingen av samlings medlemskap som en plats komponent. Mer information finns i [plats komponenter](../deploy/configure/site-components.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="monitor-keys"></a>Övervaka nycklar

Använd den här aktiviteten för att övervaka integriteten för primära nycklar för Configuration Manager databasen. En primär nyckel är en kolumn eller en kombination av kolumner som unikt identifierar en rad. Nyckeln särskiljer raden från andra rader i en Microsoft SQL Server databas tabell.

|||
|---------|---------|
|**Central administrationsplats**|Enabled|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="rebuild-indexes"></a>Återskapa index

Använd den här aktiviteten för att återskapa Configuration Manager databas index. Ett index är en databas struktur som skapas i en databas tabell för att påskynda data hämtningen. Till exempel går det ofta mycket snabbare att söka i en indexerad kolumn än att söka i en kolumn som inte är indexerad.

För att förbättra prestanda, uppdateras Configuration Manager databas index ofta så att de förblir synkroniserade och ständigt föränderliga data som lagras i databasen. Den här uppgiften:

- Skapar index för databas kolumner som är minst 50 procent unika
- Släpper index för kolumner som är mindre än 50 procent unika
- Återskapar alla befintliga index som uppfyller villkoren för data unikhetsvillkor

|||
|---------|---------|
|**Central administrationsplats**|Inte aktiverat|
|**Primär plats**|Inte aktiverat|
|**Sekundär plats**|Inte aktiverat|

### <a name="summarize-file-usage-metering-data"></a>Sammanfatta data för fil användnings mätning

Använd den här aktiviteten för att sammanfatta data från flera poster för användning av program mätnings fil till en allmän post. Med data sammanfattning kan du komprimera mängden data som lagras i den Configuration Manager databasen.

Om du vill sammanfatta data för avläsning av program vara och spara disk utrymme i databasen använder du den här uppgiften med uppgiften **sammanfatta månatliga användnings data för program mätare** . Mer information finns i [avläsning av program vara](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="summarize-installed-software-data"></a>Sammanfatta installerade program varu data

Med den här uppgiften kan du sammanfatta data från insamlad till gångs information i program varu inventeringen för att slå samman flera poster till en allmän post. Med data sammanfattning kan du komprimera mängden data som lagras i den Configuration Manager databasen. Mer information finns i [konfigurera tillgångsinformation underhålls aktiviteter](../../clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_ConfigureMaintenanceTasks).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="summarize-monthly-usage-metering-data"></a>Sammanfatta månatliga användnings mätnings data

Använd den här aktiviteten för att sammanfatta data från flera poster för månatlig användning av program vara i en allmän post. Med data sammanfattning kan du komprimera mängden data som lagras i den Configuration Manager databasen.

Om du vill sammanfatta data för avläsning av program vara och spara utrymme i databasen använder du den här uppgiften med uppgiften **sammanfatta användnings data för program mätnings fil** . Mer information finns i [avläsning av program vara](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="update-application-available-targeting"></a>Uppdatera program tillgänglig för mål anpassning

Använd den här aktiviteten för att Configuration Manager beräkna om mappningen av princip-och program distributioner till resurser i samlingar. När du distribuerar principer eller program till en samling skapar Configuration Manager en första mappning mellan de objekt som du distribuerar och medlemmarna i samlingen.

Dessa mappningar sparas i en tabell för snabbreferens. När ett medlemskap i samlingar ändras uppdaterar platsen dessa lagrade mappningar för att avspegla ändringarna. Det är dock möjligt att dessa mappningar inte är synkroniserade. Om platsen till exempel inte kan bearbeta en aviserings fil kanske inte den ändringen visas i en ändring i mappningarna. Den här uppgiften uppdaterar mappningen baserat på aktuell samling medlemskap.  

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|

### <a name="update-application-catalog-tables"></a>Uppdatera Programkatalog tabeller

Använd den här aktiviteten för att synkronisera Programkatalog webbplatsens Databascache med den senaste programinformationen. När du ändrar konfigurationen för den här underhålls uppgiften gäller den för alla primära platser i hierarkin.  

|||
|---------|---------|
|Central administrationsplats|Inte tillgänglig|
|**Primär plats**|Enabled|
|Sekundär plats|Inte tillgänglig|


## <a name="see-also"></a>Se även

[Underhållsaktiviteter](maintenance-tasks.md)
