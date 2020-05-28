---
title: Klientmeddelande
titleSuffix: Configuration Manager
description: Hantera klienter genom att vidta omedelbara åtgärder från den centrala Configuration Manager-konsolen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7680c8f955773f169d56f36eb9bbe6507d2d7ce6
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427812"
---
# <a name="client-notification-in-configuration-manager"></a>Klient meddelande i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Om du vill vidta omedelbara åtgärder på fjärrklienter skickar du en åtgärd för klient meddelanden från Configuration Manager-konsolen. Starta dessa åtgärder på en enskild enhet eller på en samling enheter.

## <a name="actions"></a>Åtgärder

Följande åtgärder finns i menyfliksområdet i enheten eller samlings gruppen på fliken Start.

### <a name="install-client"></a>Installera klient

Öppnar **guiden Installera klient**. Den här guiden använder push-installation av klienter för att installera en Configuration Manager-klient. Mer information finns i [push-installation av klienter](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

#### <a name="permissions---install-client"></a>Behörigheter – Installera klient

Den här åtgärden kräver behörigheten **Ändra resurs** och **Läs** för objektet **samling** .

Följande inbyggda roller har dessa behörigheter som standard:

- Programadministratör  
- Fullständig administratör  
- Infrastrukturadministratör  
- Driftsadministratör  
- OS Deployment Manager  

Lägg till dessa behörigheter till alla anpassade roller som behöver push-överföra klienten.

### <a name="run-script"></a>Köra skriptet

Öppnar guiden **Kör skript** för att köra ett PowerShell-skript på alla klienter i samlingen. Mer information finns i [skapa och köra PowerShell-skript](../../../apps/deploy-use/create-deploy-scripts.md).

#### <a name="permissions---run-script"></a>Behörigheter-kör skript

Den här åtgärden kräver behörighet att **köra skript** för objektet **samling** .

Följande inbyggda roller har den här behörigheten som standard:

- Fullständig administratör  
- Infrastrukturadministratör  
- Driftsadministratör  

Lägg till den här behörigheten till alla anpassade roller som behöver köra skript.

### <a name="start-cmpivot"></a>Starta CMPivot

Startar **CMPivot**, som kör frågor i real tid mot de riktade enheterna. Mer information finns i [CMPivot](../../servers/manage/cmpivot.md).

#### <a name="permissions---start-cmpivot"></a>Behörigheter-starta CMPivot

Den här åtgärden kräver samma behörigheter som [Kör skript](#run-script) åtgärden.

Från och med version 1906 kan du använda behörigheten **Kör CMPivot** för objektet **samling** .

## <a name="client-notification"></a>Klientmeddelande

De här åtgärderna finns under menyn **klient meddelande** i menyfliksområdet i gruppen enhet eller samling på fliken Start.

I version 1806 eller tidigare är alternativet **klient meddelande** bara tillgängligt från noden enhets samling eller när du visade medlemskap i en enhets samling. Från och med version 1810 kan du starta ett **klient meddelande** direkt från noden **enheter** . Det finns inte längre något krav på att det ska finnas i en samlings medlemskaps vy. <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions---client-notification"></a>Behörigheter – klient meddelande

<!--SCCMDocs-pr issue #2972-->
Från och med version 1810 kräver klient meddelande åtgärder nu behörigheten **meddela resurs** för objektet samling. Den här behörigheten gäller för alla åtgärder på menyn **klient avisering** .

Följande inbyggda roller har den här behörigheten som standard:

- Fullständig administratör  
- Driftsadministratör  

Lägg till den här behörigheten till alla anpassade roller som behöver använda klient aviserings åtgärder.

### <a name="download-computer-policy"></a>Ladda ned dator princip

Uppdatera enhets principen. Mer information finns i [Starta princip hämtning för en Configuration Manager-klient](manage-clients.md#BKMK_PolicyRetrieval).  

### <a name="download-user-policy"></a>Hämta användar princip

Uppdatera användar principen.  

### <a name="collect-discovery-data"></a>Samla in identifierings data

Utlös klienter för att skicka en identifierings data post (DDR). Mer information finns i [pulsslags identifiering](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).  

### <a name="collect-software-inventory"></a>Samla in program varu inventering

Utlös klienter för att köra en program varu inventerings cykel. Mer information finns i [Introduktion till program varu inventering](inventory/introduction-to-software-inventory.md).  

### <a name="collect-hardware-inventory"></a>Samla in maskinvaruinventering

Utlös klienter för att köra en maskin varu inventerings cykel. Mer information finns i [Introduktion till maskin varu inventering](inventory/introduction-to-hardware-inventory.md).  

### <a name="evaluate-application-deployments"></a>Utvärdera program distributioner

Utlös klienter för att köra en utvärderings cykel för program distribution. Mer information finns i [Schemalägg omvärdering för distributioner](../deploy/about-client-settings.md#schedule-re-evaluation-for-deployments).  

### <a name="evaluate-software-update-deployments"></a>Utvärdera distributioner av program uppdateringar

Utlös klienter för att köra en utvärderings cykel för distribution av program uppdateringar. Mer information finns i [Introduktion till program uppdateringar](../../../sum/understand/software-updates-introduction.md).  

### <a name="switch-to-the-next-software-update-point"></a>Växla till nästa program uppdaterings plats

Utlös klienter för att växla till nästa tillgängliga program uppdaterings plats. Mer information finns i [byte av program uppdaterings punkt](../../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching).  

### <a name="evaluate-device-health-attestation"></a>Utvärdera hälsoattestering för enhet

Utlös Windows 10-klienter för att kontrol lera och skicka sitt senaste enhets hälso tillstånd. Mer information finns i [hälsoattestering](../../servers/manage/health-attestation.md).  

### <a name="wake-up"></a>Vakna

Från och med version 1810 utlöses enheter som kon figurer ATS för att stödja Wake-on-LAN för att väcka användning av andra enheter i samma undernät för att skicka Wake-on-LAN-paketet. Mer information finns i [så här konfigurerar du Wake on LAN](../deploy/configure-wake-on-lan.md).

### <a name="restart"></a>Starta om

Utlös de valda enheterna för omstart. Mer information finns i [starta om klienter](manage-clients.md#restart-clients).

## <a name="client-diagnostics"></a>Klient diagnostik
<!--4433455-->

Från och med version 1910 finns nya enhets åtgärder för **client Diagnostics** i Configuration Manager-konsolen. Följande åtgärder har lagts till:

- **Aktivera utförlig loggning**: ändra den globala logg nivån för CCM-komponenten till utförlig och aktivera fel söknings loggning.
- **Inaktivera utförlig loggning**: ändra den globala logg nivån till standard och inaktivera fel söknings loggning.
- **Samla in klient loggar** (från 2002): ett klient meddelande skickas till de valda klienterna för att samla in CCM-loggarna. Loggarna returneras med program varu inventerings fil insamling. <!--4226618-->
   - Storleks gränsen för de komprimerade klient loggarna är 100 MB. <!--6366098-->
   - Använd [Resursläsaren](inventory/use-resource-explorer-to-view-software-inventory.md#bkmk_diag) hantera och Visa de här filerna.

   [![Samla in klient loggar från-konsolen](./media/4226618-collect-client-logs.png)](./media/4226618-collect-client-logs.png#lightbox)

> [!IMPORTANT]
> - De här åtgärderna ändrar bara loggens utförlighet, inte storlek eller historik. Mer utförlig loggning kan generera mer logg innehåll.
> - Hanterings plats rollen använder även CCM-komponenten. Om mål enheten också är en hanterings plats gäller den här åtgärden även för den rollen.

Mer information om de här inställningarna finns i [logg filen](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client).

Spåra status för uppgiften i **diagnostik. log** på klienten. När klient loggar samlas in loggas ytterligare information i **MP_SinvCollFile. log** på hanterings platsen och **lera filen sinvproc. log** på plats servern.

> [!Tip]
> Insamlade klient loggar lagras enligt inställningarna för fil samling för program varu inventering. Filerna lagras på plats servern i **katalogen Inboxes\sinv.box\Filecol** -katalogen. Det finns ingen definierad gräns för antalet versioner. Aktiviteten [ta bort föråldrade filer](../../servers/manage/reference-for-maintenance-tasks.md#delete-aged-collected-files) plats underhåll tar bort filerna enligt ett schema, vilket som standard är var 90: e dag.

### <a name="prerequisites---client-diagnostics"></a>Krav – klientautentisering

- Uppdatera mål klienten till den senaste versionen.

- Din Configuration Manager administrativa användare behöver behörigheten **meddela resurs** .

  Följande inbyggda roller har den här behörigheten som standard:

  - Fullständig administratör  
  - Infrastrukturadministratör  

  Lägg till den här behörigheten till alla anpassade roller som behöver använda klient aviserings åtgärder.


## <a name="endpoint-protection"></a>Slutpunktsskydd

Följande åtgärder finns på **Endpoint Protection** -menyn. Den här menyn finns i menyfliksområdet i gruppen samling på fliken Start. När du väljer en eller flera enheter finns dessa åtgärder på fliken **valt objekt** i menyfliksområdet.

Mer information finns i [Endpoint Protection i Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).

### <a name="permissions---endpoint-protection"></a>Behörigheter – Endpoint Protection

Den här åtgärden kräver behörigheten **tvinga säkerhet** för objektet **samling** .

Följande inbyggda roller har den här behörigheten som standard:

- Fullständig administratör  
- Endpoint Protection Manager  
- Driftsadministratör  

Lägg till den här behörigheten till alla anpassade roller som behöver utlösas Endpoint Protection åtgärder.

### <a name="full-scan"></a>Fullständig sökning

Utlös Endpoint Protection eller Windows Defender för att köra en *fullständig* genomsökning av program mot skadlig kod.  

### <a name="quick-scan"></a>Snabb sökning

Utlös Endpoint Protection eller Windows Defender för att köra en *snabb* sökning efter skadlig kod.  

### <a name="download-definition"></a>Hämta definition

Utlös Endpoint Protection eller Windows Defender för att ladda ned de senaste definitionerna för skadlig kod.  

## <a name="see-also"></a>Se även

- [Hantera klienter](manage-clients.md)
- [Hantera samlingar](collections/manage-collections.md)
