---
title: Kravkontroller
titleSuffix: Configuration Manager
description: Referens för de särskilda krav kontrollerna för Configuration Manager uppdateringar.
ms.date: 05/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9f0ed1d5913154d90242d1aa2a47efbcf7d22282
ms.sourcegitcommit: 0f02742301e42daaa30e1bde8694653e1b9e5d2a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/08/2020
ms.locfileid: "82943798"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Lista över nödvändiga kontroller för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln beskriver de nödvändiga kontroller som körs när du installerar eller uppdaterar Configuration Manager. Mer information finns i [krav kontroll](prerequisite-checker.md).  



## <a name="errors"></a>Fel

### <a name="active-migration-mappings-on-the-target-primary-site"></a>Aktivera migreringsmappningar på den primära målplatsen

*Gäller för: Central administrations webbplats*

Det finns inga mappningar mellan aktiva migreringar till primära platser.

### <a name="active-replica-mp"></a>HANTERING av aktiva repliker

*Gäller för: primär plats*

Det finns en aktiv hanterings plats replik.

### <a name="administrative-rights-on-expand-primary-site"></a>Administrativ behörighet på expanderad primär plats

*Gäller för: Central administrations webbplats*

När du expanderar en primär plats till en hierarki har det användar konto som kör installations programmet **Administratörs** behörighet på den fristående primära plats servern.

### <a name="administrative-rights-on-site-system"></a>Administratörs behörighet på plats systemet

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

Det användar konto som kör Configuration Manager installations programmet har **Administratörs** behörighet på plats servern.

### <a name="administrator-rights-on-central-administration-site"></a>Administratörs behörighet på den centrala administrations platsen

*Gäller för: primär plats*

Det användar konto som kör Configuration Manager installations programmet har **Administratörs** behörighet på den centrala administrations plats servern.

### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>Tillgångsinformation plats för synkronisering på den expanderade primära platsen

*Gäller för: Central administrations webbplats*

När du expanderar en primär plats till en hierarki installeras inte rollen Tillgångsinformation plats för synkronisering på den fristående primära platsen.

### <a name="bits-enabled"></a>BITS-aktiverad

*Gäller för: hanterings plats*

Background Intelligent Transfer Service (BITS) är installerat på hanterings platsen. Den här kontrollen kan inte utföras av någon av följande orsaker:

- BITS är inte installerat  

- IIS 6,0-komponenten för WMI-kompatibilitet för IIS 7,0 är inte installerad på servern eller en fjärran sluten IIS-värd  

- Det gick inte att verifiera IIS-inställningarna för fjärr anslutning. Delade IIS-komponenter är inte installerade på plats servern.  

### <a name="case-insensitive-collation-on-sql-server"></a>Skift läges känslig sortering på SQL Server

*Gäller för: plats databas server*

Den SQL Server installationen använder en Skift läges känslig sortering, till exempel **SQL_Latin1_General_CP1_CI_AS**.

### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Administrativ behörighet för central administrations plats Server på expanderad primär plats

*Gäller för: Central administrations webbplats*

När du expanderar en primär plats till en hierarki har dator kontot för den centrala administrations plats servern **Administratörs** behörighet på den fristående primära plats servern.

### <a name="client-version-on-management-point-computer"></a>Klient version på hanterings plats dator

*Gäller för: hanterings plats*

Du installerar hanterings platsen på en server som inte har en annan version av Configuration Manager-klienten installerad.

### <a name="cloud-management-gateway-on-the-expanded-primary-site"></a>Cloud Management Gateway på den expanderade primära platsen

*Gäller för: Central administrations webbplats*

När du expanderar en primär plats till en hierarki installeras inte Cloud Management Gateway-rollen på den fristående primära platsen.

### <a name="connection-to-sql-server-on-central-administration-site"></a>Anslutning till SQL Server på den centrala administrations platsen

*Gäller för: primär plats*

Det användar konto som kör Configuration Manager-installationen på den primära platsen för att ansluta till en befintlig hierarki har **sysadmin** -rollen på SQL Server-instansen för den centrala administrations platsen.

### <a name="custom-client-agent-settings-have-nap-enabled"></a>NAP är aktiverat i anpassade klient agent inställningar

*Gäller för: Central administrations webbplats, primär plats*

Det finns inga anpassade klient inställningar som aktiverar NAP (Network Access Protection).

### <a name="data-warehouse-service-point-on-the-expanded-primary-site"></a>Informations lager service punkt på den expanderade primära platsen

*Gäller för: Central administrations webbplats*

När du expanderar en primär plats till en hierarki installeras inte rollen data lager service punkt på den fristående primära platsen.

### <a name="dedicated-sql-server-instance"></a>Dedikerad SQL Server instans

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

Du har konfigurerat en dedikerad instans av SQL Server som är värd för Configuration Manager plats databasen.

Om en annan plats använder instansen måste du välja en annan instans för den nya platsen. Du kan också avinstallera den andra platsen eller flytta dess databas till en annan instans för SQL Server.

### <a name="default-client-agent-settings-have-nap-enabled"></a>NAP är aktiverat i standardinställningarna för klient agenten

*Gäller för: Central administrations webbplats, primär plats*

Standard klient inställningarna aktiverar inte NAP (Network Access Protection).

### <a name="domain-membership-error"></a>Domän medlemskap (fel)

*Gäller för: Central administrations webbplats, primär plats, sekundär plats, SMS-provider SQL Server*

Den Configuration Manager datorn är medlem i en Windows-domän.

### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Endpoint Protection Point på den expanderade primära platsen

*Gäller för: Central administrations webbplats*

När du expanderar en primär plats till en hierarki installeras inte Endpoint Protection Point-rollen på den fristående primära platsen.

### <a name="existing-configuration-manager-server-components-on-server"></a>Befintliga Configuration Manager Server komponenter på servern

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

En plats Server eller plats system roll är inte redan installerad på den server som har valts för plats installation.

### <a name="existing-stand-alone-primary-site-for-version-and-site-code"></a>Befintlig fristående primär plats för version och platskod

*Gäller för: Central administrations webbplats, primär plats*

Den primära platsen som du planerar att expandera är en fristående primär plats. Den har samma version av Configuration Manager, men en annan platskod än den centrala administrations platsen som ska installeras.

### <a name="firewall-exception-for-sql-server"></a>Brand Väggs undantag för SQL Server

*Gäller för: Central administrations webbplats, primär plats, sekundär plats, hanterings plats*

Windows-brandväggen är inaktive rad eller också finns det ett undantag i Windows-brandväggen för SQL Server.

Tillåt att Sqlservr. exe eller nödvändiga TCP-portar kan nås via fjärr anslutning. SQL Server lyssnar som standard på TCP-port 1433 och SQL Server Service Broker (SSB) använder TCP-port 4022.

### <a name="free-disk-space-on-site-server"></a>Ledigt disk utrymme på plats servern

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

För att kunna installera plats servern måste den ha minst 15 GB ledigt disk utrymme. Om du installerar SMS-providern på samma server behöver den ytterligare 1 GB ledigt utrymme.

### <a name="iis-service-running"></a>IIS-tjänsten körs

*Gäller för: hanterings plats, distributions plats*

IIS är installerat och körs på servern för hanterings platsen eller distributions platsen.

### <a name="incompatible-collection-references"></a>Inkompatibla samlings referenser

*Gäller för: Central administrations webbplats*

Under en uppgradering refererar samlingarna endast till andra samlingar av samma typ.

### <a name="match-collation-of-expand-primary-site"></a>Matcha sortering för expanderad primär plats

*Gäller för: Central administrations webbplats*

När du expanderar en primär plats till en hierarki har plats databasen för den fristående primära platsen samma sortering som plats databasen på den centrala administrations platsen.

### <a name="maximum-text-replication-size-for-sql-server-always-on-availability-groups"></a>Maximal storlek för text replikering för SQL Server Always on-tillgänglighetsgrupper

*Gäller för: plats databas server*

När du använder SQL Server Always on måste inställningen för **max text repl storlek** vara korrekt konfigurerad. Mer information finns i [förbereda för att använda SQL Server Always on-tillgänglighetsgrupper med Configuration Manager](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Microsoft Intune koppling på den expanderade primära platsen

*Gäller för: Central administrations webbplats*

När du expanderar en primär plats till en hierarki installeras inte rollen Microsoft Intune-anslutning på den fristående primära platsen.

### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>Microsoft RDC-biblioteket (Remote Differential Compression) är registrerat

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

RDC-biblioteket är registrerat på Configuration Manager plats Server.

### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

Verifierar Windows Installer version.

När den här kontrollen Miss lyckas kunde inte installations programmet verifiera versionen, eller så uppfyller inte den installerade versionen minimi kravet på Windows Installer 4,5.

### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Lägsta .NET Framework-version för Configuration Manager-konsolen

*Gäller för: Configuration Manager-konsolen*

Microsoft .NET Framework 4,0 är installerat på Configuration Manager-konsol datorn.

### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Lägsta .NET Framework-version för Configuration Manager plats Server

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

.NET Framework 3,5 är installerad eller aktive rad på Configuration Manager plats Server.

### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Lägsta .NET Framework version för installation av SQL Server Expresss utgåva för Configuration Manager sekundär plats

*Gäller för: sekundär plats*

.NET Framework 4,0 är installerad eller aktive rad på den Configuration Manager sekundära plats servern. Den här versionen krävs av SQL Server Express.

### <a name="parent-database-collation"></a>Överordnad databas sortering

*Gäller för: primär plats, sekundär plats*

Plats databasens sortering överensstämmer med sorteringen för den överordnade platsens databas. Alla platser i en hierarki måste använda samma databassortering.

### <a name="parent-site-replication-status"></a>Replikeringsstatus för överordnad plats

*Gäller för: Central administrations webbplats, primär plats*

Replikeringsstatus för den överordnade platsen är **aktiv replikering** (tillstånd **125**).

### <a name="pending-system-restart"></a>Väntande systemomstart

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

Innan du kör installations programmet kräver ett annat program att servern startas om.

Från och med version 1810 är den här kontrollen mer elastisk. För att se om datorn är i ett väntande omstart-läge kontrollerar den följande platser i registret:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="primary-fqdn"></a>Primär FQDN

*Gäller för: Central administrations webbplats, primär plats, sekundär plats, plats databas server*

Datorns NetBIOS-namn matchar det lokala värd namnet i det fullständigt kvalificerade domän namnet (FQDN).

### <a name="read-only-domain-controller"></a>Skrivskyddad domänkontrollant

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

Plats databas servrar och sekundära plats servrar stöds inte på en skrivskyddad domänkontrollant (RODC).

Mer information finns i Microsoft Support artikel om [problem när du installerar SQL Server på en](https://support.microsoft.com/help/2032911)domänkontrollant.

### <a name="required-sql-server-collation"></a>Obligatorisk SQL Server sortering

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

Instansen för SQL Server har kon figurer ATS för att använda **SQL_Latin1_General_CP1_CI_AS** sorteringen.

Om Configuration Manager plats databasen redan är installerad gäller den här kontrollen även för-databasen. Information om hur du ändrar SQL Server-instansen och databas sorteringar finns i [stöd för SQL-sortering och Unicode](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support).

Om du använder ett kinesiskt operativ system och behöver stöd för GB18030, gäller inte den här kontrollen. Mer information om hur du aktiverar stöd för GB18030 finns i [internationell support](../../../plan-design/hierarchy/international-support.md).

### <a name="server-service-is-running"></a>Server tjänsten körs

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

Server tjänsten har startats och körs.

### <a name="setup-source-folder"></a>Källmapp för installation

*Gäller för: sekundär plats*

Dator kontot för den sekundära platsen har följande behörigheter för installations programmets källmapp och resurs:

- **Läs** NTFS-behörigheter för fil system  

- **Läs** behörigheter för resurs  

> [!Note]  
> Om du använder administrativa resurser, till exempel C $ och D $, måste dator kontot för den sekundära platsen vara en **administratör** på servern.  

### <a name="setup-source-version"></a>Installations käll version

*Gäller för: sekundär plats*

Den Configuration Manager versionen i den angivna källmappen för installationen av den sekundära platsen matchar Configuration Manager versionen av den primära platsen.

### <a name="site-code-in-use"></a>Plats koden används

*Gäller för: primär plats*

Den angivna plats koden används inte redan i Configuration Manager hierarkin. Ange en unik Platskod för den här platsen.

### <a name="site-server-computer-account-administrative-rights"></a>Administratörs behörighet för plats serverns dator konto

*Gäller för: primär plats, plats databas server*

Plats serverns dator konto har **Administratörs** behörighet på SQL-servern och hanterings platsen.

### <a name="site-server-fqdn-length"></a>FQDN-längd för plats Server

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

Längden på FQDN för plats servern.

### <a name="site-server-in-passive-mode-on-the-expanded-primary-site"></a>Plats server i passivt läge på den expanderade primära platsen

*Gäller för: Central administrations webbplats*

När du expanderar en primär plats till en hierarki, är plats servern i passivt läge-rollen inte installerad på den fristående primära platsen.

### <a name="sms-provider-in-same-domain-as-site-server"></a>SMS-provider i samma domän som plats servern

*Gäller för: SMS-provider*

Alla instanser av SMS-providern finns i samma domän som plats servern.

### <a name="software-update-point-in-nlb-configuration"></a>Program uppdaterings plats i NLB-konfiguration

*Gäller för: program uppdaterings plats*

Platsen använder inte NLB (utjämning av nätverks belastning) med virtuella platser för aktiva program uppdaterings platser.

### <a name="software-update-point-using-a-load-balancer"></a>Program uppdaterings plats med hjälp av en belastningsutjämnare

*Gäller för: program uppdaterings plats*

Configuration Manager stöder inte program uppdaterings platser i nätverk (NLB) eller maskinvarubaserade belastningsutjämnare (HLB).

### <a name="sql-server-always-on-availability-groups"></a>SQL Server AlwaysOn-tillgänglighetsgrupper

*Gäller för: plats databas server*

När du använder SQL Server Always on måste det uppfylla minimi kraven för att vara värd för en tillgänglighets grupp. Mer information finns i [förbereda för att använda SQL Server Always on-tillgänglighetsgrupper med Configuration Manager](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="sql-server-availability-group-configured-for-readable-secondaries"></a>SQL Server tillgänglighets grupp har kon figurer ATS för läsbara sekundär servrar

*Gäller för: plats databas server*

När du använder SQL Server Always on, kontrollerar du den sekundära Läs statusen för tillgänglighets grupps repliker.

### <a name="sql-server-availability-group-configured-for-manual-failover"></a>SQL Server tillgänglighets grupp som kon figurer ATS för manuell redundansväxling

*Gäller för: plats databas server*

När du använder SQL Server Always on, konfigureras tillgänglighets grupp repliker för manuell redundansväxling.

### <a name="sql-server-availability-group-replicas-on-default-instance"></a>SQL Server tillgänglighets grupps repliker på standard instansen

*Gäller för: plats databas server*

När du använder SQL Server Always On är tillgänglighets grupps repliker på standard instansen.

### <a name="sql-availability-group-replicas-must-all-have-the-same-seeding-mode"></a>SQL tillgänglighets grupps repliker måste ha samma seeding-läge

<!-- SCCMDocs-pr#3899 -->
*Gäller för: plats databas server*

Från och med version 1906 måste du konfigurera tillgänglighets grupp repliker med samma [seeding-läge](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas)när du använder SQL Server Always On.

### <a name="sql-availability-group-replicas-must-be-healthy"></a>SQL tillgänglighets grupps repliker måste vara felfria

<!-- SCCMDocs-pr#3899 -->
*Gäller för: plats databas server*

Från och med version 1906, när du använder SQL Server Always on, är tillgänglighets grupp repliker i felfritt tillstånd.

### <a name="sql-server-configuration-for-site-upgrade"></a>SQL Server konfiguration för plats uppgradering

*Gäller för: plats databas server*

SQL Server uppfyller minimi kraven för plats uppgradering. Mer information finns i [SQL Server-versioner som stöds](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="sql-server-edition"></a>SQL Server-utgåva

*Gäller för: plats databas server*

SQL Server på platsen är inte SQL Server Express.

### <a name="sql-server-express-on-secondary-site"></a>SQL Server Express på sekundär plats

*Gäller för: sekundär plats*

SQL Server Express kan installeras på den sekundära plats servern.

### <a name="sql-server-on-the-secondary-site-server"></a>SQL Server på den sekundära plats servern

*Gäller för: sekundär plats*

SQL Server är installerat på den sekundära plats servern. Du kan inte installera SQL Server på ett fjärrplatssystem för en sekundär plats.

> [!Warning]  
> Den här kontrollen gäller endast när du väljer att använda en befintlig instans av SQL Server.  

### <a name="sql-server-service-running-account"></a>SQL Server tjänst som kör konto

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

Inloggnings kontot för SQL Server-tjänsten är inte ett lokalt användar konto eller en **Lokal tjänst**.

Konfigurera SQL Server tjänsten så att den använder ett giltigt domän konto, en **nätverks tjänst**eller ett **lokalt system**.

### <a name="sql-server-site-database-consistency"></a>Konsekvens för SQL Server plats databas

*Gäller för: plats databas server*

Kontrol lera databasens konsekvens.

### <a name="sql-server-sysadmin-rights"></a>SQL Server sysadmin-rättigheter

*Gäller för: plats databas server*

Det användar konto som kör Configuration Manager-installationen har **sysadmin** -rollen på den SQL Server-instans som du har valt för installation av plats databas. Den här kontrollen Miss lyckas även när installations programmet inte kan komma åt instansen för den SQL Server för att verifiera behörigheter.

### <a name="sql-server-sysadmin-rights-for-reference-site"></a>SQL Server sysadmin-rättigheter för referens plats

*Gäller för: plats databas server*

Det användar konto som kör Configuration Manager-installationen har **sysadmin** -rollen på den SQL Server roll instans som du valde som referens plats databas. SQL Server **sysadmin** -roll behörigheter krävs för att ändra plats databasen.

### <a name="sql-server-tcp-port"></a>SQL Server TCP-port

*Gäller för: plats databas server*

TCP är aktiverat för SQL Server-instansen och är inställt på att använda en statisk port.

### <a name="sql-server-version"></a>SQL Server-version

*Gäller för: plats databas server*

En version av SQL Server som stöds är installerad på den angivna plats databas servern.

Mer information finns i [stöd för SQL Server-versioner](../../../plan-design/configs/support-for-sql-server-versions.md).

### <a name="unsupported-os-for-configuration-manager-console"></a>OS för Configuration Manager-konsolen stöds inte

*Gäller för: Configuration Manager-konsolen*

Installera Configuration Manager-konsolen på datorer som kör en operativ system version som stöds.

Mer information finns i [operativ system versioner som stöds för Configuration Manager-konsolen](../../../plan-design/configs/supported-operating-systems-consoles.md).

### <a name="unsupported-os-for-site-server"></a>OS för plats server som inte stöds

*Gäller för: Central administrations webbplats, primär plats, sekundär plats, Configuration Manager-konsol, hanterings plats, distributions plats*

Servern kör en operativ system version som stöds.

Mer information finns i [OS-versioner som stöds för Configuration Manager plats system servrar](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

### <a name="unsupported-site-system-role-out-of-band-service-point"></a>Plats system rollen stöds inte: out-of-band-tjänst

*Gäller för: primär plats*

Plats system rollen out-of-band-plats är inte installerad.

### <a name="unsupported-site-system-role-system-health-validation-point"></a>Plats system rollen stöds inte: kontroll punkt för system hälsa

*Gäller för: primär plats*

Plats system rollen för system hälso verifierings platsen är inte installerad.

### <a name="unsupported-upgrade-path"></a>Uppgraderings Sök vägen stöds inte

*Gäller för: Central administrations webbplats, primär plats*

Alla plats servrar i hierarkin uppfyller Configuration Manager lägsta version som krävs för uppgradering.

### <a name="usmt-installed"></a>USMT installerat

*Gäller för: Central administrations webbplats, primär plats (endast fristående)*

Komponenten User State Migration Tool (USMT) i Windows ADK (Assessment and Deployment Kit) för Windows är installerad.

### <a name="validate-fqdn-of-sql-server"></a>Verifiera FQDN för SQL Server

*Gäller för: plats databas server*

Du har angett ett giltigt fullständigt domän namn för SQL Server datorn.

### <a name="verify-central-administration-site-version"></a>Verifiera version av central administrations plats

*Gäller för: primär plats*

Den centrala administrations platsen har samma version av Configuration Manager.

### <a name="verify-database-consistency"></a>Verifiera databasens konsekvens

*Gäller för: Central administrations webbplats, primär plats*

Kontrollerar konsekvensen för plats databasen i SQL Server.  

### <a name="windows-deployment-tools-installed"></a>Windows Deployment Tools har installerats

*Gäller för: SMS-provider*

Windows Deployment tools-komponenten i Windows ADK är installerad.

### <a name="windows-failover-cluster"></a>Windows-redundanskluster

*Gäller för: plats Server, hanterings plats, distributions plats*

Servern med plats servern, hanterings platsen eller distributions plats rollerna ingår inte i ett Windows-kluster.

Från och med version 1810 blockerar Configuration Manager installations processen inte längre installationen av plats Server rollen på en dator med Windows-rollen för redundanskluster. SQL Always on kräver den här rollen, så det var tidigare att du inte kunde hitta plats databasen på plats servern. Med den här ändringen kan du skapa en plats med hög tillgänglighet med färre servrar med hjälp av SQL Always on och en plats server i passivt läge. Mer information finns i [alternativ för hög tillgänglighet](../configure/high-availability-options.md). <!--1359132-->  

### <a name="windows-pe-installed"></a>Windows PE installerat

*Gäller för: SMS-provider*

Komponenten Windows Preinstallation Environment (PE) i Windows ADK har installerats.



## <a name="warnings"></a>Varningar

### <a name="active-directory-domain-functional-level"></a>Active Directory domän funktions nivå

*Gäller för: Central administrations webbplats, primär plats*

Den Active Directory domän-och skogs funktions nivån är minst Windows Server 2008 R2. Mer information finns i [stöd för Active Directory domäner](../../../plan-design/configs/support-for-active-directory-domains.md).

### <a name="administrative-rights-on-distribution-point"></a>Administratörs behörighet på distributions plats

*Gäller för: distributions plats*

Användar kontot som kör installationen har **Administratörs** behörighet på distributions platsen.

### <a name="administrative-rights-on-management-point"></a>Administrativ behörighet för hanterings plats

*Gäller för: hanterings plats, distributions plats*

Dator kontot för plats servern har **Administratörs** behörighet på hanterings platsen och distributions platsen.

### <a name="administrative-share-site-system"></a>Administrativ resurs (plats system)

*Gäller för: hanterings plats*

De nödvändiga administrativa resurserna finns på plats system datorn.

### <a name="application-compatibility"></a>Programkompatibilitet

*Gäller för: Central administrations webbplats, primär plats*

Aktuella program är kompatibla med program schemat.

### <a name="backlogged-inboxes"></a>Eftersläpande inkorgar

*Gäller för: Central administrations webbplats, primär plats*

Plats servern bearbetar kritiska inkorgar inom rimlig tid. Inkorgarna innehåller inte filer som är äldre än en dag.

Den kontrollerar följande mappar i inkorgen:

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

Du kan lösa den här varningen genom att kontrol lera om plats system komponenterna för despooler och Scheduler körs.

### <a name="bits-installed"></a>BITS installerat

*Gäller för: hanterings plats*

Background Intelligent Transfer Service (BITS) har installerats och Aktiver ATS i IIS.

### <a name="check-if-the-site-uses-upgrade-readiness-cloud-service-connector"></a>Kontrol lera om webbplatsen använder Uppgraderingsberedskap Cloud Service Connector

*Gäller för: Central administrations webbplats, primär plats*

Tjänsten Uppgraderingsberedskap tas ur bruk den 31 januari 2020. Mer information finns i [KB 4521815: pensionering i Windows Analytics den 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

Desktop Analytics är utvecklingen av Windows Analytics. Mer information finns i [Vad är Desktop Analytics](../../../../desktop-analytics/overview.md).

Om din Configuration Manager plats hade en anslutning till Uppgraderingsberedskap måste du ta bort den och konfigurera om klienter. Mer information finns i [ta bort uppgraderingsberedskap anslutning](../../../clients/manage/upgrade-readiness.md#bkmk_remove).

Om du ignorerar den här krav varningen tar Configuration Manager-installationen bort Uppgraderingsberedskap-anslutningen automatiskt.<!-- #4898 -->

### <a name="cloud-management-gateway-requires-either-token-based-authentication-or-an-https-management-point"></a>Cloud Management Gateway kräver token-baserad autentisering eller en HTTPS-hanterings plats

*Gäller för: Cloud Management Gateway*

Med vissa versioner av Configuration Manager kan du inte använda en HTTP-hanterings plats med Cloud Management Gateway (CMG). Konfigurera CMG för HTTPS eller konfigurera platsen för utökad HTTP. Mer information finns i [Planera för Cloud Management Gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md).

### <a name="configuration-for-sql-server-memory-usage"></a>Konfiguration för SQL Server minnes användning

*Gäller för: plats databas server*

SQL Server har kon figurer ATS för obegränsad minnes användning. Konfigurera SQL Server minne så att det har en maximal gräns.

### <a name="distribution-point-package-version"></a>Version för distributions plats paket

*Gäller för: distributions platser*

Alla distributions platser på platsen har den senaste versionen av paket för program varu distribution.

### <a name="domain-membership-warning"></a>Domän medlemskap (varning)

*Gäller för: hanterings plats, distributions plats*

Den Configuration Manager datorn är medlem i en Windows-domän.

### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>Brand Väggs undantag för SQL Server (fristående primär plats)

*Gäller för: primär plats (endast fristående)*

Windows-brandväggen är inaktive rad eller också finns det ett undantag i Windows-brandväggen för SQL Server.

Tillåt att Sqlservr. exe eller nödvändiga TCP-portar kan nås via fjärr anslutning. SQL Server lyssnar som standard på TCP-port 1433 och Server Service Broker (SSB) använder TCP-port 4022.

### <a name="firewall-exception-for-sql-server-for-management-point"></a>Brand Väggs undantag för SQL Server för hanterings plats

*Gäller för: hanterings plats*

Windows-brandväggen är inaktive rad eller också finns det ett undantag i Windows-brandväggen för SQL Server.

### <a name="iis-https-configuration"></a>IIS HTTPS-konfiguration

*Gäller för: hanterings plats, distributions plats*

IIS-webbplatsen har bindningar för HTTPS-kommunikations protokollet.

När du installerar plats roller som kräver HTTPS konfigurerar du IIS-webbplats bindningar på den angivna servern med ett giltigt PKI-certifikat (Public Key Infrastructure).

### <a name="invalid-discovery-records"></a>Ogiltiga identifierings poster

*Gäller för: Central administrations webbplats*

Det finns identifierings poster som inte längre är giltiga. Dessa poster kommer att markeras för borttagning.

### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6,0 (MSXML60)

*Gäller för den centrala administrations platsen, primär plats, sekundär plats, Configuration Manager-konsol, hanterings plats, distributions plats*

Verifierar att MSXML 6,0 eller en senare version är installerad.

### <a name="network-access-protection-nap-is-no-longer-supported"></a>NAP (Network Access Protection) stöds inte längre

*Gäller för: primär plats*

Det finns inga aktiverade program uppdateringar för NAP.

### <a name="ntfs-drive-on-site-server"></a>NTFS-enhet på plats servern

*Gäller för: primär plats*

Disk enheten är formaterad med fil systemet NTFS. Installera plats Server komponenter på disk enheter som är formaterade med NTFS-filsystem för bättre säkerhet.

### <a name="pending-configuration-item-policy-updates"></a><a name="bkmk_pending-policy"></a>Väntande uppdateringar av konfigurations objekts princip

<!--SCCMDocs-pr issue 2814-->

*Gäller för: primär plats*

Från och med version 1806 kan du se den här varningen om du uppdaterar från version 1706 eller senare, om du har många program distributioner och minst en av dem kräver godkännande.

Du kan välja mellan två alternativ:  

- Ignorera varningen och fortsätt med uppdateringen. Den här åtgärden medför högre bearbetning på plats servern under uppdateringen när den bearbetar principerna. Du kan också se mer processor belastning på hanterings platsen efter uppdateringen.  

- Ändra ett av de program som saknar krav eller särskilda krav för operativ system. Förbearbeta en del av belastningen på plats servern vid detta tillfälle. Granska **objreplmgr. log**och övervaka sedan processorn på hanterings platsen. Uppdatera platsen när bearbetningen är klar. Det kommer fortfarande att finnas ytterligare bearbetning efter uppdateringen, men mindre än om du ignorerar varningen med det första alternativet.  

### <a name="pending-system-restart-on-the-remote-sql-server"></a>Väntande systemomstart på den fjärranslutna SQL Server

*Gäller för: version 1902 och senare, fjärr SQL Server*

Innan du kör installations programmet kräver ett annat program att servern startas om.

För att se om datorn är i ett väntande omstart-läge kontrollerar den följande platser i registret:<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="powershell-20-on-site-server"></a>PowerShell 2,0 på plats servern

*Gäller för: primär plats med Exchange Connector*

Windows PowerShell 2,0 eller en senare version är installerad på plats servern för Configuration Manager Exchange Connector.

### <a name="remote-connection-to-wmi-on-secondary-site"></a>Fjärr anslutning till WMI på den sekundära platsen

*Gäller för: sekundär plats*

Installations programmet kan upprätta en fjärr anslutning till WMI på den sekundära plats servern.

### <a name="schema-extensions"></a>Schemautökningar

*Gäller för: Central administrations webbplats, primär plats*

Active Directory-schemat har utökats. Om den är utökad är det den version av schema tillägg som användes.

Configuration Manager kräver inte Active Directory schema tillägg för plats Server installationen. Microsoft rekommenderar dem att använda alla Configuration Manager-funktioner fullt ut. Mer information om fördelarna med att utöka schemat finns i [förbereda Active Directory för webbplats publicering](../../../plan-design/network/extend-the-active-directory-schema.md).

### <a name="share-name-in-package"></a>Resurs namn i paket

*Gäller för: Central administrations webbplats, primär plats*

Paketen innehåller inte ogiltiga tecken i resurs namnet, t `#` . ex..

### <a name="site-system-to-sql-server-communication"></a>Plats system för att SQL Server kommunikation

*Gäller för: sekundär plats, hanterings plats*

Det konto som du konfigurerade för att köra SQL Server-tjänsten för plats databas instansen har ett giltigt SPN (Service Principal Name) i Active Directory Domain Services. Registrera ett giltigt SPN i Active Directory som stöder Kerberos-autentisering.

### <a name="sql-server-change-tracking-cleanup"></a><a name="bkmk_changetracking"></a>Rensning av SQL Server ändrings spårning

*Gäller för: plats databas server*

Från och med version 1810 kontrollerar du om plats databasen har en efter släpning av SQL Change tracking-data.<!--SCCMDocs-pr issue 3023-->  

Verifiera den här kontrollen manuellt genom att köra en Diagnostisk lagrad procedur i plats databasen. Skapa först en [diagnostisk anslutning](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017) till din plats databas. Den enklaste metoden är att använda SQL Server Management Studio databas motorns Frågeredigeraren och ansluta till `admin:<instance name>` .

Kör följande kommandon i ett dedikerat fönster för anslutnings frågor för administratörer:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

Den lagrade proceduren kan köras på några minuter eller flera timmar beroende på databasens storlek och den väntande storleken. När frågan har slutförts visas två avsnitt med data som är relaterade till efter släpning. Titta först på **CT_Days_Old**. Det här värdet anger ålder (dagar) för den äldsta posten i syscommittab-tabellen. Det bör vara fem dagar, vilket är Configuration Manager standardvärdet. Ändra inte det här standardvärdet. Vid tung data bearbetning eller replikering kan den äldsta posten i syscommittab vara över fem dagar. Om det här värdet är över sju dagar kan du köra en manuell rensning av ändrings spårnings data.  

Om du vill rensa ändrings spårnings data kör du följande kommando i den dedicerade administrations anslutningen:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

Det här kommandot startar en rensning av syscommittab och alla associerade sido tabeller. Det kan köras på flera minuter eller flera timmar. Fråga vyn **vLogs** för att övervaka förloppet. Kör följande fråga för att se aktuell status:

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

### <a name="sql-server-native-client"></a>SQL Server Native Client

<!--SCCMDocs-pr issue 3094-->

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Uppdatering av SQL Server Native Client kan kräva en omstart, vilket kan påverka plats installations processen.

Den här kontrollen ser till att plats servern har en version av SQL Native Client som stöds. Krav kontrollen kontrollerar inte versionen av SQL Native Client på fjärrplatssystem.

Den lägsta versionen är SQL 2012 SP4 ( `11.*.7001.0` ). Den här SQL Native Client versionen stöder TLS 1,2. Mer information finns i följande artiklar:

- [TLS 1,2-stöd för Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [Så här aktiverar du TLS 1,2 för Configuration Manager](../../../plan-design/security/enable-tls-1-2.md)  

Configuration Manager använder SQL Server Native Client på följande plats system roller:<!-- SCCMDocs issue 1150 -->

- Platsdatabasserver
- Plats Server: Central administrations webbplats, primär plats eller sekundär plats
- Hanteringsplats
- Enhets hanterings plats
- Plats för tillståndsmigrering
- SMS-provider
- Programuppdateringsplats
- Multicast-aktiverad distributionsplats
- Tillgångsinformation uppdaterings tjänst punkt
- Rapporteringstjänstpunkt
- Webb tjänst för program katalog
- Registreringsplats
- Plats för slutpunktsskydd
- Tjänstanslutningspunkt
- Certifikatregistreringsplats
- Informations lager service punkt

### <a name="sql-server-process-memory-allocation"></a>Minnes tilldelning för SQL Server process

*Gäller för: plats databas server*

SQL Server reserverar minst 8 GB minne för den centrala administrations platsen och den primära platsen, och minst 4 GB minne för den sekundära platsen.

Mer information finns i [så här konfigurerar du minnes alternativ med SQL Server Management Studio](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-).

> [!NOTE]  
> Den här kontrollen kan inte användas för SQL Server Express på en sekundär plats. Den här versionen är begränsad till 1 GB reserverat minne.  

### <a name="sql-server-security-mode"></a>SQL Server säkerhets läge

*Gäller för: plats databas server*

SQL Server har kon figurer ATS för säkerhet i Windows-autentisering.

### <a name="unsupported-site-system-os-version-for-upgrade"></a>Plats systemets OS-version stöds inte för uppgradering

*Gäller för: primär plats, sekundär plats*

Andra plats system roller än distributions platser installeras på servrar som kör Windows Server 2012 eller senare.

Mer information finns i [operativ system som stöds för Configuration Manager plats system servrar](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

> [!NOTE]  
> Den här kontrollen kan inte lösa statusen för plats system roller som är installerade i Azure eller för moln lagring som används av Microsoft Intune. Ignorera varningar för dessa roller som falska positiva identifieringar.

### <a name="upgrade-assessment-toolkit-is-unsupported"></a>Verktyg för uppgraderings utvärdering stöds inte

*Gäller för: Central administrations webbplats, primär plats*

Verktyg för uppgraderings utvärdering är inte installerat. Mer information finns i [borttagna och föråldrade funktioner](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Verifiera plats Server behörighet att publicera till Active Directory

*Gäller för: Central administrations webbplats, primär plats, sekundär plats*

Dator kontot för plats servern har **fullständig** behörighet till **System Management** -behållaren i Active Directory-domänen.

Mer information finns i [förbereda Active Directory för webbplats publicering](../../../plan-design/network/extend-the-active-directory-schema.md).

> [!NOTE]  
> Om du verifierar behörigheterna manuellt kan du ignorera den här varningen.

### <a name="windows-remote-management-winrm-v11"></a>Windows Remote Management (WinRM) v 1.1

*Gäller för: primär plats, Configuration Manager-konsol*

WinRM 1,1 installeras på den primära plats servern eller på den Configuration Manager-konsol datorn för att köra out-of-band-hanteringskonsolen.

WinRM installeras automatiskt med alla versioner av Windows som stöds. Mer information finns i [installation och konfiguration för Windows Remote Management](https://docs.microsoft.com/windows/win32/winrm/installation-and-configuration-for-windows-remote-management).

### <a name="wsus-on-site-server"></a>WSUS på plats Server

*Gäller för: Central administrations webbplats, primär plats*

En version av Windows Server Update Services (WSUS) som stöds har installerats på plats servern.

När du använder en program uppdaterings plats på en annan server än plats servern måste du installera WSUS-administrationskonsolen på plats servern. Mer information om WSUS finns [Windows Server Update Services](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).
