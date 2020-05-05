---
title: Tillståndsmeddelanden
titleSuffix: Configuration Manager
description: Beskrivningar av tillstånds meddelanden i Configuration Manager-versioner som stöds.
ms.date: 03/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe173e37d888dfe594ad8953ff5d7167d43a2981
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720935"
---
# <a name="state-messages-in-configuration-manager"></a>Tillstånds meddelanden i Configuration Manager 

*Gäller för: Configuration Manager (aktuell gren)*

Tillstånds meddelanden innehåller kortfattad information om villkor på Configuration Manager-klienten. Tillstånds meddelande systemet används av vissa komponenter i Configuration Manager, t. ex. program uppdateringar och konfigurations inställningar.

Configuration Manager klienter skickar tillstånds meddelanden till återställnings status platsen eller hanterings plats system för att rapportera det aktuella tillståndet för åtgärder. Du kan skapa rapporter för att Visa tillstånds meddelanden som skickas av Configuration Manager klienter.

Varje Configuration Manager funktion som använder tillstånds meddelanden identifieras av ämnes typen för tillstånds meddelandet. Ämnes typerna för tillstånds meddelandet som anges i den här artikeln kan användas för att definiera den Configuration Manager funktionen som ett tillstånds meddelande avser.

> [!NOTE]  
> Ett tillstånds meddelande-ID på noll (0) anger normalt att ämnes typen är i ett okänt tillstånd.

## <a name="300-state_topictype_sum_assignment_compliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 0 | Okänt kompatibilitetstillstånd|
| 1 | Kompatibel | 
| 2 | Icke-kompatibel | 

## <a name="301-state_topictype_sum_assignment_enforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 0  | Okänt tvångs tillstånd |
| 1  | Installerar uppdatering (ar)        | 
| 2  | Väntar på omstart          | 
| 3  | Väntar på att en annan installation ska slutföras         | 
| 4  | Uppdateringen (2) har installerats          | 
| 5  | Väntande systemomstart         | 
| 6  | Det gick inte att installera uppdatering (erna)         | 
| 7  | Hämtar uppdatering (erna)   | 
| 8  | Hämtade uppdateringar    | 
| 9  | Det gick inte att hämta uppdatering (er)     | 
| 10 | Väntar på underhålls perioden innan du installerar         | 
| 11 | Väntar på dirigering         | 

## <a name="302-state_topictype_sum_assignment_evaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|      
| 0 | Okänt utvärderings tillstånd|                 
| 1 |Utvärderingen har Aktiver ATS      |
| 2 |Utvärderingen har slutförts      |
| 3 |Utvärderingen misslyckades      |


## <a name="400-state_topictype_sum_ci_detection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 0 | Okänt identifierings tillstånd|
| 1 | Krävs inte   |
| 2 | Inte identifierat    |
| 3 | Identifierad   |

## <a name="401-state_topictype_sum_ci_compliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 0 | Okänt kompatibilitetstillstånd|
| 1 |Kompatibel     |
| 2 |Icke-kompatibel     |
| 3 |Konflikt identifierad    |
| 4 |Fel      |
| 5 |Okänt     |
| 6 |Delvis överensstämmelse   |
| 7 |Kompatibilitet har inte kon figurer ATS    |

## <a name="402-state_topictype_sum_ci_enforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 0  | Okänt tvångs tillstånd|
| 1  |Tvångs åtgärd har startat          |
| 2  |Tvång väntar på innehåll         |
| 3  | Väntar på att en annan installation ska slutföras        |
| 4  |Väntar på underhålls perioden innan du installerar         |
| 5  |Omstart krävs innan du installerar         |
| 6  |Allmänt haveri        |
| 7  |Väntande installation         |
| 8  |Installerar uppdatering          |
| 9  |Väntande systemomstart        |
| 10 |Uppdateringen har installerats         |
| 11 |Det gick inte att installera uppdateringen        |
| 12 |Hämtar uppdatering        |
| 13 | Hämtad uppdatering        |
| 14 |Det gick inte att hämta uppdateringen        |

## <a name="500-state_topictype_sum_update_detection"></a>500 STATE_TOPICTYPE_SUM_UPDATE_DETECTION

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
|0 |Okänt identifierings tillstånd|
| 1 | Uppdatering krävs inte  |
| 2 | Uppdatering krävs   |
| 3 | Uppdateringen har installerats  |

## <a name="501-state_topictype_sum_update_source_scan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 0 |Okänt skannings tillstånd|
| 1 | Genomsökning väntar på innehåll   |
| 2 | Genomsökningen körs    |
| 3 | Sökningen är klar    |
| 4 | Försök att skanna väntar   |
| 5 | Sökningen misslyckades   |
| 6 | Skanningen slutfördes med fel |

## <a name="700-state_topictype_resync_state_msg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

Inga tillstånds-ID: n.

## <a name="701-state_topictype_system_heartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

Inga tillstånds-ID: n.

## <a name="702-state_topictype_ckd_update"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
Inga tillstånds-ID: n.

## <a name="800-state_topictype_client_deployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 100 |Klient distributionen startade      |       
| 101 |Väntar på nedladdning       |       
| 102 |Schemalagd distribution       |       
| 103 | Väntar på fönstret före distribution |
| 104 |Distributionen hoppades över       |       
| 301 |Okänt klient distributions problem |       
| 302 |Det gick inte att skapa CCMSetup-tjänsten  |       
| 303 |Det gick inte att ta bort CCMSetup-tjänsten |       
| 304 |Det går inte att installera över inbäddat operativ system med ett filbaserat Skriv filter (FBWF) aktiverat på system enheten |       
| 305 |Enhetligt säkerhets läge är inte giltigt i Windows 2000  |       
| 306 |Det gick inte att starta CCMSetup nedladdnings process  |       
| 307 |Ogiltig kommando rad för CCMSetup |       
| 308 |Det gick inte att ladda ned filen över WINHTTP på adressen |       
| 309 |Det gick inte att ladda ned filerna via BITS på adressen |       
| 310 |Det gick inte att installera BITS-versionen |       
| 311 |Det går inte att verifiera att nödvändig fil är MS-signerad  |       
| 312 |Det gick inte att kopiera filen eftersom disken är full |       
| 313 |Installationen av client. msi misslyckades med MSI-fel |       
| 314 |Det gick inte att läsa in manifest filen CCMSetup. XML |       
| 315 |Det gick inte att hämta ett klient certifikat  |       
| 316 |Nödvändig fil är inte MS-signerad |       
| 317 |Omstart krävs för att fortsätta installationen  |       
| 318 |Det går inte att installera klienten på MP eftersom MP och klient versionerna inte matchar |       
| 319 |Operativ system eller service pack som inte stöds  |       
| 320 |Distributionen stöds inte       |       
| 321 |Bitar saknas        |       
| 322 |Källmappen är inte tillgänglig       |       
| 323 |AppV stöds inte              |       
| 324 |Felaktig plats version              |       
| 325 |Krav på hash-matchningsfel       |       
| 326 |MDM-avregistreringen misslyckades      |       
| 327 |MDM-registrering har identifierats      |       
| 328 |Intune har identifierats       |       
| 329 |Nätverket med datapriser tillåts inte      |       
| 400 |Klient distributionen lyckades |  
| 401 |Distributionen genomförd omstart krävs     |       
| 402 |Distributionen har startats om     |
| 500 |Klient tilldelningen startade|
| 601 |Okänd klient tilldelnings problem|
| 602 |Följande platskod är ogiltig|
| 603 |Det gick inte att tilldela MP|
| 604 |Det gick inte att identifiera standard hanterings platsen|
| 605 |Det gick inte att hämta plats signerings certifikatet|
| 606 |Det gick inte att automatiskt identifiera platskod|
| 607 |Platstilldelning misslyckades; klient version som är större än plats version|
| 608 |Det gick inte att hämta plats version från Active Directory Domain Services och SLP|
| 609 |Det gick inte att hämta klient versionen|
| 700 |Klient tilldelningen lyckades|

## <a name="801-state_topictype_device_client_deployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

Inga tillstånds-ID: n.

## <a name="810-state_topictype_client_comanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 100 | Registreringsstatus   |
| 101 | Registrering har schemalagts   |
| 102 | Registreringen avbröts   |
| 105 | Registrering har startats   |
| 106 | Registreringen lyckades men har inte tillhandahållits
| 107 | Registreringen lyckades och har tillhandahållits
| 108 | Registrering ingen aktiv användare   |
| 110 | Registreringen misslyckades   |


## <a name="820--state_topictype_client_wufb"></a>820 STATE_TOPICTYPE_CLIENT_WUFB

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 | Status för Windows Update för företags klient| 

## <a name="900-state_topictype_branch_dp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 | Disk utrymme   | 

## <a name="901-state_topictype_remote_dp_monitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

Inga tillstånds-ID: n.

## <a name="902-state_topictype_pull_dp_monitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

Inga tillstånds-ID: n.

## <a name="903-state_topictype_dp_usage"></a>903 STATE_TOPICTYPE_DP_USAGE

Inga tillstånds-ID: n.

## <a name="1000--state_topictype_client_framework_comm"></a>1000 STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 | Klienten kommunicerar med hanterings platsen |
| 2 | Klienten kunde inte kommunicera med hanterings platsen |

## <a name="1001-state_topictype_client_framework_local"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 |Klienten har hämtat certifikatet från det lokala certifikat arkivet    |
| 2 |Klienten kunde inte hämta certifikatet från det lokala certifikat arkivet |

## <a name="1002-state_topictype_device_client_framework_comm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

Inga tillstånds-ID: n.

## <a name="1003-state_topictype_device_client_framework_local"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

Inga tillstånds-ID: n.

## <a name="1004-state_topictype_device_client_framework_certificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

Inga tillstånds-ID: n.

## <a name="1005-state_topictype_device_client_wipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

Inga tillstånds-ID: n.

## <a name="1006-state_topictype_device_client_retire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

Inga tillstånds-ID: n.

## <a name="1007-state_topictype_device_client_wipe_intune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

Inga tillstånds-ID: n.

## <a name="1008-state_topictype_device_client_retire_intune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

Inga tillstånds-ID: n.

## <a name="1009-state_topictype_device_client_devicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

Inga tillstånds-ID: n.

## <a name="1010-state_topictype_device_client_devicelock_intune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

Inga tillstånds-ID: n.

## <a name="1011-state_topictype_device_client_devicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

Inga tillstånds-ID: n.

## <a name="1012-state_topictype_device_client_devicepinreset_intune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

Inga tillstånds-ID: n.

## <a name="1013-state_topictype_device_client_devicepinreset_onprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

Inga tillstånds-ID: n.

## <a name="1014-state_topictype_device_client_devicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

Inga tillstånds-ID: n.

## <a name="1015-state_topictype_device_client_devicealbypass_intune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

Inga tillstånds-ID: n.

## <a name="1100-state_topictype_client_framework_modereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 |Klienten är inte klar för enhetligt läge  |
| 2 |Klienten är klar för enhetligt läge     |


## <a name="1300-state_topictype_client_health"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 | Klart|
| 2 | Inte klar |

## <a name="1401-state_topictype_state_report"></a>1401 STATE_TOPICTYPE_STATE_REPORT

Inga tillstånds-ID: n.

## <a name="1500-state_topictype_cal_track_ut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

Inga tillstånds-ID: n.

## <a name="1502-state_topictype_cal_track_mt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

Inga tillstånds-ID: n.

## <a name="1503-state_topictype_cal_track_ml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

Inga tillstånds-ID: n. 

## <a name="1600-state_topictype_user_affinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 |Användar tillhörighets uppsättning       |
| 2 |Användar tillhörighet har tagits bort       |

## <a name="1700-state_topictype_app_ci_scan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

Inga tillstånds-ID: n.

## <a name="1701-state_topictype_app_ci_compliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

Inga tillstånds-ID: n.

## <a name="1702-state_topictype_app_ci_enforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1000  |Konfigurations objekt lyckades           |
| 1001 |Konfigurationsobjektet har redan installerats         |
| 1002 |Konfigurations objekt lyckades preflight          |
| 1003 |Konfigurations objektets snabb status lyckades          |
| 2000 |Konfigurations objekt pågår           |
| 2001 |Konfigurations objekt pågår i väntan på innehåll         |
| 2002 |Konfigurations objekt som installeras          |
| 2003 |Konfigurations objekt pågår väntande omstart         |
| 2004 |Konfigurations objekt pågår i väntan på underhålls period        |
| 2005 |Väntande konfigurations objekt pågår         |
| 2006 |Konfigurations objekt pågår hämtar beroende innehåll     |
| 2007 |Konfigurations objekt som håller på att installeras beroenden        |
| 2008 |Konfigurations objekt pågår som väntar på omstart         |
| 2009 |Innehåll som hämtats i förlopp för konfigurations objekt         |
| 2010 |Konfigurations objekt pågår som väntar på uppdatering         |
| 2011 |Konfigurations objekt pågår väntar på att användaren ska återansluta        |
| 2012 |Konfigurations objekt pågår i väntan på utloggning av användare         |
| 2013 |Konfigurations objekt pågår i väntan på att användaren ska logga in         |
| 2014 |Konfigurations objekt pågår i väntan på installation         |
| 2015 |Konfigurations objekt pågår i väntan på nytt försök         |
| 2016 |Konfigurations objekt pågår i väntan på presmode         |
| 2017 |Konfigurations objekt pågår i väntan på dirigering        |
| 2018 |Konfigurations objekt pågår i väntan på nätverk         |
| 2019 |Konfigurations objekt pågår som väntar på uppdatering VE         |
| 2020 |Konfigurations objekt pågår uppdatering av ra         |
| 3000 |Konfigurations objekt krav har inte uppfyllts           |
| 3001 |Konfigurations objekt krav som inte uppfyllde värden inte tillämpligt        |
| 4000 |Okänt konfigurations objekt           |
| 5000 |Konfigurations objekts fel            |
| 5001 |Fel vid utvärdering av konfigurations objekt          |
| 5002 |Konfigurations objekt fel vid installation          |
| 5003 |Konfigurations objekts fel vid hämtning av innehåll         |
| 5004 |Konfigurations objekt fel vid installation av beroende         |
| 5005 |Konfigurations objekt fel vid hämtning av innehålls beroende        |
| 5006 |Konflikt vid fel regel för konfigurations objekt          |
| 5007 |Konfigurations objekt fel vid väntan på återförsök          |
| 5008 |Konfigurations objekt fel vid avinstallation av ersättning        |
| 5009 |Konfigurations objekts fel vid hämtning av ersatt         |
| 5010 |Konfigurations objekts fel vid uppdatering av ra          |
| 5011 |Konfigurations objekt fel vid installation av licens         |
| 5012 |Konfigurations objekt fel vid hämtning Tillåt alla betrodda appar       |
| 5013 |Konfigurations objekt fel inga tillgängliga licenser         |
| 5014 |Konfigurations objekt fel operativ system stöds inte          |
| 6000 |Konfigurations objekt har startats            |
| 6010 |Fel vid start av konfigurations objekt            |
| 6020 |Start av konfigurations objekt okänd|

## <a name="1703-state_topictype_app_ci_assignment_evaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

Inga tillstånds-ID: n.

## <a name="1704-state_topictype_app_ci_launch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

Inga tillstånds-ID: n.

## <a name="1800-state_topictype_event_intrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

Inga tillstånds-ID: n.

## <a name="1801-state_topictype_event_extrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

Inga tillstånds-ID: n.

## <a name="1900-state_topictype_ep_am_infection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

Inga tillstånds-ID: n.

## <a name="1901-state_topictype_ep_am_health"></a>1901 State_Topictype_Ep_Am_Health

Inga tillstånds-ID: n.

## <a name="1902-state_topictype_ep_malware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

Inga tillstånds-ID: n.

## <a name="1950-state_topictype_atp_health_status"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

Inga tillstånds-ID: n.

## <a name="2001-state_topictype_ep_client_deployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 |Endpoint Protection ohanterad   |
| 2 |Endpoint Protection väntar på installation  |
| 3 |Endpoint Protection hanterad   |
| 4 |Endpoint Protection installationen misslyckades  |
| 5 |Endpoint Protection omstart väntar  |
| 6 |Endpoint Protection stöds inte   |
| 7 |Endpoint Protection samhanterad   |

## <a name="2002-state_topictype_ep_client_policyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 0 |Okänd status för Endpoint Protection princip program    |
| 1 |Endpoint Protection princip programmet lyckades    |
| 2 |Endpoint Protection princip programmet misslyckades    |

## <a name="2003-state_topictype_client_action"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 0 |  Okänt    |
| 1 |  Active    |
| 2 |  Inaktiv    |

## <a name="2100-state_topictype_wp_client_deployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 | Aktiverings-proxyn är inte installerad    |
| 2 | Väcknings proxy väntar på installation   |
| 3 | Aktiverings-proxyn har installerats    |
| 4 | Det gick inte att installera Väcknings proxy   |
| 5 | Aktiverings proxyn väntar på omstart   |
| 6 | Väcknings proxy stöds inte på det här operativ systemet  |
| 7 | Opt-out för Väcknings proxyserver   |
| 8 | Det gick inte att avinstallera Väcknings proxy   |
| 9 | Aktivering av proxy runtime stöds inte   |

## <a name="2200-state_topictype_fdm"></a>2200 STATE_TOPICTYPE_FDM

Inga tillstånds-ID: n.

## <a name="2201-state_topictype_ccm_cert_binding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

Inga tillstånds-ID: n.

## <a name="2202-state_topictype_server_statistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

Inga tillstånds-ID: n.

## <a name="3000-state_topictype_dm_wns_channel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
|0 | Kanal uppsättning för Windows Push Notification Service|

## <a name="4000-state_topictype_mdm_device_property"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

Inga tillstånds-ID: n.

## <a name="4002-state_topictype_mdm_client_idenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

Inga tillstånds-ID: n.

## <a name="4003-state_topictype_mdm_application_request"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

Inga tillstånds-ID: n.

## <a name="4004-state_topictype_mdm_application_state"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

Inga tillstånds-ID: n.

## <a name="4005-state_topictype_mdm_license_device_relation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

Inga tillstånds-ID: n.

## <a name="4006-state_topictype_mdm_license_keys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

Inga tillstånds-ID: n.

## <a name="4007-state_topictype_mdm_policy_assignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

Inga tillstånds-ID: n.

## <a name="4008-state_topictype_mdm_android_count"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

Inga tillstånds-ID: n.

## <a name="4009-state_topictype_mdm_slk_status"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

Inga tillstånds-ID: n.

## <a name="4010-state_topictype_mdm_user_company_term_acceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

Inga tillstånds-ID: n.

## <a name="4022-state_topictype_mdm_dep_syncnow_status"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

Inga tillstånds-ID: n.

## <a name="4023-state_topictype_mdm_mam_store_app_sync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

Inga tillstånds-ID: n.

## <a name="5000-state_topictype_certificate_enrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 |Anrop utfärdat         |
| 2 |Utmanings problem misslyckades        |
| 3 |Begäran kunde inte skapas        |
| 4 |Begäran om sändning misslyckades        |
| 5 |Utmanings verifieringen lyckades       |
| 6 |Det gick inte att verifiera kontrollen       |
| 7 |Problemet misslyckades         |
| 8 |Problem väntar         |
| 9 |Ske          |
| 10 |Bearbetning av svar misslyckades       |
| 11 |Svar väntar         |
| 12 |Registreringen lyckades         |
| 13 |Registrering behövs inte         |
| 14 |Revoked          |
| 15 |Borttagen från samling        |
| 16 |Förnya verifierad         |
| 17 |Installationen misslyckades        |
| 18 |Installerad         |
| 19 |Borttagningen misslyckades         |
| 20 |Borttagen         |
| 21 |Förnyelse begärd        |


## <a name="5001-state_topictype_certificate_crp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 |Anrop utfärdat         |
| 2 |Utmanings problem misslyckades        |
| 3 |Begäran kunde inte skapas        |
| 4 |Begäran om sändning misslyckades        |
| 5 |Utmanings verifieringen lyckades       |
| 6 |Det gick inte att verifiera kontrollen       |
| 7 |Problemet misslyckades         |
| 8 |Problem väntar         |
| 9 |Ske          |
| 10 |Bearbetning av svar misslyckades       |
| 11 |Svar väntar         |
| 12 |Registreringen lyckades         |
| 13 |Registrering behövs inte         |
| 14 |Revoked          |
| 15 |Borttagen från samling        |
| 16 |Förnya verifierad         |
| 17 |Installationen misslyckades        |
| 18 |Installerad         |
| 19 |Borttagningen misslyckades         |
| 20 |Borttagen         |
| 21 |Förnyelse begärd        |

## <a name="5200-state_topictype_resource_access_status"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 | Status för PIN-kod har installerats       |
| 2 | Installations status för PIN-kod misslyckades       |
| 3 | Konfiguration av status-PIN-kod stöds inte      |
| 4 | Status-PIN-konfiguration pågår      |

## <a name="6000-state_topictype_remoteapp_subscription_status"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

Inga tillstånds-ID: n.

## <a name="6001-state_topictype_remoteapp_subscription_sync_status"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

Inga tillstånds-ID: n.

## <a name="6002-state_topictype_remoteapp_authcookies_sync_status"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

Inga tillstånds-ID: n.

## <a name="6003-state_topictype_remoteapplications_sync_status"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

Inga tillstånds-ID: n.

## <a name="6004-state_topictype_remoteapp_lock_result"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

Inga tillstånds-ID: n.

## <a name="7000-state_topictype_user_company_term_acceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

Inga tillstånds-ID: n.

## <a name="7001-state_topictype_pfx_certificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 |Anrop utfärdat    |
| 2 |Utmanings problem misslyckades   |
| 3 |Begäran kunde inte skapas   |
| 4 |Begäran om sändning misslyckades   |
| 5 |Utmanings verifieringen lyckades  |
| 6 |Det gick inte att verifiera kontrollen  |
| 7 |Problemet misslyckades    |
| 8 |Problem väntar    |
| 9 |Ske     |
| 10 |Bearbetning av svar misslyckades  |
| 11 |Svar väntar    |
| 12 |Registreringen lyckades    |
| 13 |Registrering behövs inte    |
| 14 |Revoked     |
| 15 |Borttagen från samling   |
| 16 |Förnya verifierad    |
| 17 |Installationen misslyckades   |
| 18 |Installerad    |
| 19 |Borttagningen misslyckades    |
| 20 |Borttagen    |
| 21 |Förnyelse begärd   |

## <a name="7010-state_topictype_conditional_access_compliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
|| 1 | Kompatibiliteten lyckades    |
| 2 | Kompatibiliteten fungerar inte vid MP   |
| 3 | Kompatibiliteten kunde inte utföras på klienten   |
| 4 | Kompatibiliteten fungerar inte i Intune   |
| 5 | Kompatibiliteten fungerar inte vid AAD   |
| 6 | Hanterings Intune för efterlevnad   |

## <a name="7200-state_topictype_super_peer_update_cache_map"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 |Källa för peer-cache har lagts till       |
| 2 |Källa för peer-cache har tagits bort      |

## <a name="7201-state_topictype_super_peer_update_config"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 |Källa för peer-cache inaktive rad       |
| 2 |Källa för peer-cache är aktiv       |

## <a name="7202-state_topictype_download_aggregate_data"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 |Hämta Samlad data uppladdning       |

## <a name="7203-state_topictype_peersource_req_rejection_stats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 |Överföring av data uppladdning för avvisning av peer-källa     |

## <a name="7300-state_topictype_proxy_traffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

Inga tillstånds-ID: n.

## <a name="7301-state_topictype_proxy_connection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

Inga tillstånds-ID: n.

## <a name="7302-state_topictype_srs_usage_data"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

Inga tillstånds-ID: n.

## <a name="7303-state_topictype_proxy_traffic_identity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

Inga tillstånds-ID: n.

## <a name="8001-state_topictype_has_report"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     ID för tillstånds meddelande     |  Beskrivning av tillstånds meddelande |
|:-------------|:------|
| 1 |Hälsoattestering stöds      |
| 2 |Hälsoattestering stöds inte      |

## <a name="state_topictype_device_client_edplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

Inga tillstånds-ID: n.

## <a name="8003-state_topictype_enable_lostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

Inga tillstånds-ID: n.

## <a name="8004-state_topictype_disable_lostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

Inga tillstånds-ID: n.

## <a name="8005-state_topictype_locate_device"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

Inga tillstånds-ID: n.

## <a name="8006-state_topictype_reboot_device"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

Inga tillstånds-ID: n.

## <a name="8007-state_topictype_logoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

Inga tillstånds-ID: n.

## <a name="8008-state_topictype_userslist"></a>8008 STATE_TOPICTYPE_USERSLIST

Inga tillstånds-ID: n.

## <a name="8009-state_topictype_deleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

Inga tillstånds-ID: n.

## <a name="8010-state_topictype_cleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

Inga tillstånds-ID: n.

## <a name="8011-state_topictype_cleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

Inga tillstånds-ID: n.

## <a name="8012-state_topictype_setdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

Inga tillstånds-ID: n.

## <a name="9000-state_topictype_book_ci_compliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

Inga tillstånds-ID: n.

## <a name="9001-state_topictype_book_ci_enforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

Inga tillstånds-ID: n.

## <a name="next-steps"></a>Nästa steg

- [Beskrivning av tillstånds meddelanden i Configuration Manager](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Dokumentation om hantering av program uppdateringar för Configuration Manager](https://www.microsoft.com/download/details.aspx?id=44578)
