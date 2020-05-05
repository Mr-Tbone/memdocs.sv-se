---
title: Uppgradera den lokala infrastrukturen
titleSuffix: Configuration Manager
description: Lär dig hur du uppgraderar infrastruktur, till exempel SQL Server och operativ systemets plats system.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 033c5de1a85ce2fa8b11fe7a187fcc4d5c023931
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720732"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>Uppgradera en lokal infrastruktur som stöder Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd informationen i den här artikeln som hjälp för att uppgradera Server infrastrukturen som kör Configuration Manager.  

- Om du vill *Uppgradera* från en tidigare version till Configuration Manager, aktuell gren, se [Uppgradera till Configuration Manager](../deploy/install/upgrade-to-configuration-manager.md).  

- Om du vill *Uppdatera* din Configuration Manager, aktuell gren, infrastruktur till en ny version, se [uppdateringar för Configuration Manager](updates.md).  


## <a name="upgrade-the-os-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a>Uppgradera operativ system för plats system  

Configuration Manager stöder uppgradering på plats av det server-OS som är värd för en plats Server och en plats system roll i följande situationer:  

- Om Configuration Manager fortfarande har stöd för den resulterande service packs nivån av Windows, stöder den uppgradering på plats till en senare Windows Server-service pack.  

- Uppgradering på plats från:  

    - Windows Server 2016 till Windows Server 2019  

    - Windows Server 2012 R2 till Windows Server 2019  

    - Windows Server 2012 R2 till Windows Server 2016  

    - Windows Server 2012 till Windows Server 2016  

    - Windows Server 2012 till Windows Server 2012 R2  

    - Windows Server 2008 R2 till Windows Server 2012 R2  

Uppgradera en server genom att använda de uppgraderings procedurer som tillhandahålls av det operativ system som du uppgraderar till. Se följande artiklar:  

- [Windows Server Upgrade Center](https://aka.ms/upgradecenter)  

- [Uppgraderings-och konverterings alternativ för Windows Server 2016](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths)  

- [Uppgraderings alternativ för Windows Server 2012 R2](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11))  

### <a name="upgrade-to-windows-server-2016-or-2019"></a><a name="bkmk_2016-2019"></a>Uppgradera till Windows Server 2016 eller 2019

Använd stegen i det här avsnittet för något av följande uppgraderings scenarier:  

- Uppgradera antingen Windows Server 2012 R2 eller Windows Server 2016 till Windows Server 2019  

- Uppgradera antingen Windows Server 2012 eller Windows Server 2012 R2 till Windows Server 2016  

#### <a name="before-upgrade"></a>Före uppgradering

- (Windows Server 2012 eller Windows Server 2012 R2): ta bort System Center Endpoint Protection-klienten (SCEP). Windows Server har nu inbyggd Windows Defender, som ersätter SCEP-klienten. Förekomsten av SCEP-klienten kan förhindra en uppgradering till Windows Server.  

- Ta bort WSUS-rollen från servern om den är installerad. Du kan behålla SUSDB och bifoga den igen när WSUS har installerats om.  

- Om du uppgraderar plats serverns operativ system kontrollerar du att [filbaserad replikering](../../plan-design/hierarchy/file-based-replication.md) är felfritt för platsen. Kontrol lera alla inkorgar för en efter släpning på både sändande och mottagande platser. Om det finns massor av jobb som fastnat eller väntar på replikering väntar du tills de är klara.<!-- SCCMDocs#1792 -->
    - Granska **Sender. log**på den sändande platsen.
    - Granska **utskrifts loggen**på den mottagande platsen.

#### <a name="after-upgrade"></a>Efter uppgraderingen

- Kontrol lera att Windows Defender är aktiverat, ange för automatisk start och kör.  

- Kontrol lera att följande Configuration Manager-tjänster körs:  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- Kontrol lera att tjänsterna **Windows Process Activation** och **www/W3SVC** har Aktiver ATS och ställts in för automatisk start. Uppgraderings processen inaktiverar dessa tjänster, så se till att de körs för följande plats system roller:  

    - Platsserver  

    - Hanteringsplats  

    - Webbservicepunkt för programkatalog  

    - Webbplats för programkatalog  

- Se till att varje server som är värd för en plats system roll fortsätter att uppfylla alla [krav](../../plan-design/configs/site-and-site-system-prerequisites.md). Du kan till exempel behöva installera om BITS, WSUS eller konfigurera vissa inställningar för IIS.  

- När du har återställt alla saknade komponenter startar du om servern en gång för att se till att tjänsterna startas och fungerar.  

- Om du uppgraderar den primära plats servern [kör du en plats återställning](modify-your-infrastructure.md#bkmk_reset).  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Känt problem för fjärranslutna Configuration Manager-konsoler

När du har uppgraderat plats servern eller en instans av SMS-providern kan du inte ansluta till Configuration Manager-konsolen. Undvik det här problemet genom att manuellt återställa behörigheter för **SMS Admins** -gruppen i WMI. Behörigheter måste anges på plats servern och på varje fjärrserver som är värd för en instans av SMS-providern:

1. Öppna Microsoft Management Console (MMC) på lämpliga servrar och Lägg till snapin-modulen för **WMI-kontroll**och välj sedan **lokal dator**.  

2. I MMC öppnar du **egenskaperna** för **WMI-kontroll (lokal)** och väljer fliken **säkerhet** .  

3. Expandera trädet nedanför roten, Välj **SMS** -noden och välj sedan **säkerhet**.  Kontrol lera att gruppen **SMS-administratörer** har följande behörigheter:  

    - Aktivera konto  

    - Fjärraktivering  

4. På **fliken säkerhet** under **SMS** -noden väljer du noden **site_&lt;SiteCode**> och väljer sedan **säkerhet**. Kontrol lera att gruppen **SMS-administratörer** har följande behörigheter:  

    - Köra metoder  

    - Skrivning av Provider  

    - Aktivera konto  

    - Fjärraktivering  

5. Spara behörigheterna för att återställa åtkomsten för Configuration Manager-konsolen.  

#### <a name="known-issue-for-remote-site-systems"></a>Känt problem för fjärrplatssystem

När du har uppgraderat en server som är värd för en plats system `Software\Microsoft\SMS` roll kan värdet saknas i följande register nyckel:`HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths`

Om det här värdet saknas när du har uppgraderat Windows på servern, lägger du till det manuellt. Andra plats system roller kan ha problem med att ladda upp filer till plats serverns inkorgar.

### <a name="upgrade-to-windows-server-2012-r2"></a><a name="bkmk_2012r2"></a>Uppgradera till Windows Server 2012 R2

När du uppgraderar från antingen Windows Server 2008 R2 eller Windows Server 2012 till Windows Server 2012 R2 gäller följande villkor:

#### <a name="before-upgrade"></a>Före uppgradering

- På Windows Server 2012: ta bort WSUS-rollen från servern om den är installerad. Du kan behålla SUSDB och bifoga den igen när WSUS har installerats om.  

- På Windows Server 2008 R2: innan du uppgraderar till Windows Server 2012 R2 måste du avinstallera WSUS 3,2 från servern. Du kan behålla SUSDB och bifoga den igen när WSUS har installerats om. Mer information finns i [Windows Server Update Services översikt](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality).  

- Om du uppgraderar plats serverns operativ system kontrollerar du att [filbaserad replikering](../../plan-design/hierarchy/file-based-replication.md) är felfritt för platsen. Kontrol lera alla inkorgar för en efter släpning på både sändande och mottagande platser. Om det finns massor av jobb som fastnat eller väntar på replikering väntar du tills de är klara.<!-- SCCMDocs#1792 -->
    - Granska **Sender. log**på den sändande platsen.
    - Granska **utskrifts loggen**på den mottagande platsen.

#### <a name="after-upgrade"></a>Efter uppgraderingen

- Uppgraderings processen inaktiverar Windows Deployment Services. Kontrol lera att den här tjänsten har startats och körs för följande plats system roller:  

    - Platsserver  

    - Hanteringsplats  

    - Webbservicepunkt för programkatalog  

    - Webbplats för programkatalog  

- Kontrol lera att tjänsterna **Windows Process Activation** och **www/W3SVC** har Aktiver ATS och ställts in för automatisk start. Uppgraderings processen inaktiverar dessa tjänster, så se till att de körs för följande plats system roller:  

    - Platsserver  

    - Hanteringsplats  

    - Webbservicepunkt för programkatalog  

    - Webbplats för programkatalog  

- Se till att varje server som är värd för en plats system roll fortsätter att uppfylla alla [krav](../../plan-design/configs/site-and-site-system-prerequisites.md). Du kan till exempel behöva installera om BITS, WSUS eller konfigurera vissa inställningar för IIS.  

    När du har återställt alla saknade komponenter startar du om servern en gång för att se till att tjänsterna startas och fungerar.  

### <a name="unsupported-upgrade-scenarios"></a>Uppgraderings scenarier som inte stöds

Följande uppgraderings scenarier för Windows Server är vanliga, men stöds inte av Configuration Manager:  

- Windows Server 2008 till Windows Server 2012 eller senare  

- Windows Server 2008 R2 till Windows Server 2012  


## <a name="upgrade-the-os-of-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a>Uppgradera klienternas operativ system  

Configuration Manager stöder en uppgradering på plats av operativ systemet för Configuration Manager-klienter i följande situationer:  

- Om Configuration Manager har stöd för den resulterande service packs nivån stöder den uppgradering på plats till en senare Windows-service pack.  

- Uppgradering på plats av Windows från en version som stöds till Windows 10. Mer information finns i [uppgradera Windows till den senaste versionen](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Uppgraderingar av build to build-etablering av Windows 10. Mer information finns i [hantera Windows som en tjänst](../../../osd/deploy-use/manage-windows-as-a-service.md).  


## <a name="upgrade-sql-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a>Uppgradera SQL Server  

Configuration Manager stöder en uppgradering på plats av SQL Server på plats databas servern.

Information om vilka versioner av SQL Server som Configuration Manager stöder finns i [stöd för SQL Server versioner](../../plan-design/configs/support-for-sql-server-versions.md).  

### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Uppgradera service pack-versionen av SQL Server

Om Configuration Manager fortfarande har stöd för den resulterande SQL Server service pack nivån stöder den uppgradering på plats av SQL Server till en senare service pack.

Om du har fler än en Configuration Manager-plats i en hierarki kan varje plats köra en annan service pack version av SQL Server. Det finns ingen begränsning för i vilken ordning platserna uppgraderas service pack versionen av SQL Server.

### <a name="upgrade-to-a-new-version-of-sql-server"></a>Uppgradera till en ny version av SQL Server

Configuration Manager stöder uppgradering på plats av SQL Server till följande versioner:

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

Detta inkluderar uppgradering av SQL Server Express till en nyare version av SQL Server Express på sekundära platser.

När du uppgraderar den version av SQL Server som är värd för plats databasen måste du uppgradera SQL Server-versionen som används på platserna i följande ordning:

1. Uppgradera SQL Server på den centrala administrations platsen först  

2. Uppgradera sekundära platser innan du uppgraderar en sekundär platss överordnade primära plats  

3. Uppgradera överordnade primära platser sist. Dessa platser omfattar både underordnade primära platser som rapporterar till en central administrations plats, och fristående primära platser som är platsen på den översta nivån i en hierarki.  

### <a name="sql-server-cardinality-estimation-level"></a>Beräknings nivå för SQL Server kardinalitet

När du uppgraderar en plats databas från en tidigare version av SQL Server, behåller databasen sin befintliga beräknings nivå för SQL-kardinalitet, om den är i det minsta tillåtna antalet för den instansen av SQL Server. Om du uppgraderar SQL Server med en databas på en kompatibilitetsnivå som är lägre än den tillåtna nivån, ställs databasen automatiskt in på den lägsta kompatibilitetsnivån som tillåts av SQL Server.

I följande tabell visas rekommenderade kompatibilitetsnivå för Configuration Manager plats databaser:

|SQL Server-version | Kompatibilitetsnivå som stöds | Rekommenderad nivå |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Om du vill identifiera den kompatibilitetsnivå för SQL Server kardinalitet som används för plats databasen kör du följande SQL-fråga på plats databas servern:  

```SQL
SELECT name, compatibility_level FROM sys.databases
```

Mer information om kompatibilitetsnivån för SQL CE och hur du ställer in dem finns i [Alter Database Compatibility Level (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).

Mer information om hur du uppgraderar SQL Server finns i följande SQL Server artiklar:  

- [Uppgradera till SQL Server 2017](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [Uppgradera till SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [Uppgradera till SQL Server 2014](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  

### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Så här uppgraderar du SQL Server på platsdatabasservern  

1. Stoppa alla Configuration Manager-tjänster på platsen  

2. Uppgradera SQL Server till en version som stöds  

3. Starta om Configuration Manager-tjänsterna  

> [!NOTE]  
> När du ändrar SQL Server versionen som används på den centrala administrations webbplatsen från standard till antingen ett Data Center eller ett företag, ändras inte databasens partition. Denna databas partition begränsar antalet klienter som stöds av hierarkin.  
