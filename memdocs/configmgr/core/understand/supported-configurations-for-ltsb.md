---
title: 'Konfigurationer som stöds för LTSB '
titleSuffix: Configuration Manager
description: Ta reda på vilka operativ system och beroende produkter som fungerar med den långsiktiga etablerings grenen för System Center Configuration Manager.
ms.date: 05/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7de7d562131f97ac21d1c394b176d3b7f4ce7747
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906437"
---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Konfigurationer som stöds för långsiktig etablerings gren i System Center Configuration Manager

*Gäller för: System Center Configuration Manager (långsiktig service gren)*

Använd informationen i det här avsnittet för att ta reda på vilka operativ system och produkt beroenden som stöds av LTSB (Long term Servicing Branch) för Configuration Manager.
Om detta inte anges i det här eller de LTSB specifika ämnena, gäller samma konfigurationer och begränsningar som gäller för Current Branch version 1606 för LTSB.  Använd den information som gäller för den version som du använder när det uppstår konflikter. Normalt är LTSB mer begränsad än Current Branch.

## <a name="general-statement-of-support"></a>Allmän support specifikation
Följande produkter och tekniker stöds av den här grenen av Configuration Manager. Deras införande i det här innehållet uttrycker dock inget tillägg till stöd för någon produkt eller version utöver produktens enskilda support livs cykel. Produkter som ligger utanför support livs cykeln stöds inte för användning med Configuration Manager. Mer information finns på webbplatsen för [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle) och Läs vanliga frågor och svar om Microsoft Support Lifecycle-policyn.

Dessutom stöds inte produkter och produkt versioner som inte visas i följande avsnitt om de inte har annonser ATS på [Enterprise Mobility + Security Blogg](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/bg-p/enterprisemobilityandsecurity).

**Begränsningar för framtida support:** LTSB har begränsat stöd för framtida Server-och klient operativ system och produkt beroenden. Listan med plattformar för LTSB är fast för utgivnings tiden:

**Aktivitets**
- Endast kvalitets-och säkerhets uppdateringar för Windows stöds.
- Inget stöd har lagts till för aktuella grenar (CB), aktuella grenar för företag (CBB) eller LTSB för Windows 10.
- Inget stöd för nya huvud versioner av Windows Server.

**SQL Server:**
- Endast kvalitets-och säkerhets uppdateringar, eller mindre uppgraderingar som Service Pack, stöds för SQL Server.
- Inget stöd för nya huvud versioner av SQL Server.  

## <a name="site-systems-and-servers"></a>Plats system och-servrar
LTSB stöder användning av följande operativ system för Windows-datorer som plats system.  Varje operativ system har samma krav och begränsningar som samma post i [operativ system som stöds för plats system servrar](../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  Till exempel måste Server Core-installationen av Windows 2012 R2 vara en x64-version, stöds bara som värd för en distributions plats och har inte stöd för PXE eller multicast.

**Operativ system som stöds:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): standard, data Center
- Windows Server 2012 (x64): standard, data Center
- Windows 10 Enterprise 2015-LTSB (x86, x64)
- Windows 10 Enterprise 2016-LTSB (x86, x64)
- Windows 8,1 (x86, x64): Professional, Enterprise
- Server Core-installationen av Windows Server 2012
- Server Core-installationen av Windows Server 2012 R2

## <a name="client-management"></a>Klienthantering
I följande avsnitt hittar du de klient operativ system som du kan hantera med LTSB. LTSB har inte stöd för att lägga till nya operativ system som klienter som stöds.

### <a name="windows-computers"></a>Windows-datorer
Du kan använda LTSB för att hantera följande operativ system för Windows-datorer med Configuration Manager-klient program vara som ingår i Configuration Manager. Mer information finns i [Distribuera klienter till Windows-datorer](../clients/deploy/deploy-clients-to-windows-computers.md).

**Operativ system som stöds:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): standard, data Center (anmärkning 1)
- Windows Server 2012 (x64): standard, data Center (anmärkning 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows 10 Enterprise 2015-LTSB (x86, x64)
- Windows 10 Enterprise 2016-LTSB (x86, x64)
- Windows 8,1 (x86, x64): Professional, Enterprise
- Server Core-installationen av Windows Server 2012 R2 (x64) (anmärkning 2)
- Server Core-installationen av Windows Server 2012 (x64) (anmärkning 2)

**(Anmärkning 1)** Data Center-versioner stöds men är inte certifierade för Configuration Manager.  
**(Anmärkning 2)** För att stödja push-installation av klienter måste datorn som kör den här operativ system versionen köra roll tjänsten fil server för Server rollen fil-och lagrings tjänster. Information om hur du installerar Windows-funktioner på en Server Core-dator finns i [Installera Server roller och funktioner på en Server Core-server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574158(v=ws.11)).

### <a name="windows-embedded"></a>Windows Embedded
Du kan använda LTSB för att hantera följande Windows Embedded-enheter genom att installera-klient program varan på enheten.  Mer information finns i [Planera för klient distribution till Windows Embedded-enheter](../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).

**Krav och begränsningar:**  

-   Alla klient funktioner stöds på Windows Embedded-system som stöds och som inte har Skriv filter aktiverade.  

-   Klienter som använder något av följande stöds för alla funktioner förutom energispar funktioner:  

    -   Förbättrade Skriv filter (EWF)    

    -   Filbaserade RAM-baserade Skriv filter (FBWF)    

    -   Enhetliga Skriv filter (UWF)  

-   Programkatalog stöds inte för någon Windows Embedded-enhet.  

-   Innan du kan övervaka identifierad skadlig kod på Windows Embedded-enheter som baseras på Windows XP måste du installera Microsoft Windows WMI Scripting-paketet på den inbäddade enheten. Använd Windows Embedded Target designer för att installera det här paketet. *WBEMDISP. DLL* och *WBEMDISP. TLB* -filer måste finnas och vara registrerade i mappen%windir%\System32\WBEM på den inbäddade enheten för att säkerställa att identifierad skadlig kod rapporteras.  

**Operativ system som stöds:**  
-   Windows 10 Enterprise 2016-LTSB (x86, x64)  
-   Windows 10 Enterprise 2015-LTSB (x86, x64)  
-   Windows Embedded 8,1-bransch (x86, x64)    
-   Windows tunn dator (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 med SP1 (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 Du kan hantera Windows CE enheter med Configuration Manager äldre klient för mobila enheter som ingår i Configuration Manager.  

**Krav och begränsningar:**  

-   Den mobila enhets klienten kräver 0,78 MB lagrings utrymme för att installera-klienten. En mobil enhet kan kräva upp till 256 KB ytterligare lagrings utrymme för att logga in.    

-   Funktionerna för dessa mobila enheter varierar efter plattform och klient typ. Information om vilka typer av hanterings funktioner som Configuration Manager stöd för en äldre mobilen hets klient finns i [Välj en enhets hanterings lösning för Configuration Manager](../plan-design/choose-a-device-management-solution.md).  

**Operativ system som stöds:**  

-   Windows CE 7,0 (ARM-och x86-processorer)  

**Språk som stöds:**  
-   Kinesiska (förenklad och traditionell)    
-   Engelska (USA)    
-   Franska (Frankrike)    
-   Tyska    
-   Italienska    
-   Japanska  
-   Koreanska  
-   Portugisiska (Brasilien)  
-   Ryska  
-   Spanska (Spanien)  

### <a name="mac-computers"></a>Mac-datorer  
 Du kan använda LTSB för att hantera Mac OS X-datorer med Configuration Manager-klienten för Mac.

Installations paketet för Mac-klienten levereras inte med Configuration Manager mediet. Du kan ladda ned det som en del av hämtningen "klienter för ytterligare operativ system" från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719).  

Stöd för Mac-operativsystem är begränsat till de som anges i det här avsnittet. Support omfattar inte ytterligare operativ system som kan stödjas av en framtida uppdatering av Mac-installationspaket för Current Branch.

Mer information finns i [Distribuera klienter till Mac-datorer](../clients/deploy/deploy-clients-to-macs.md).

**Versioner som stöds:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Linux-och UNIX-servrar
Du kan använda LTSB för att hantera Linux-och UNIX-servrar med Configuration Manager-klienten för Linux och UNIX.

Klient installations paketen för Linux och UNIX levereras inte med Configuration Manager mediet. Du kan ladda ned dem som en del av hämtningen "klienter för ytterligare operativ system" från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719). Utöver klientinstallationspaketen omfattar klientnedladdningen install -skriptet som hanterar installationen av klienten på varje dator.

Stöd för Linux-och UNIX-operativsystem är begränsat till de som anges i det här avsnittet. Support omfattar inte ytterligare operativ system som kan stödjas av en framtida uppdatering av Linux-och UNIX-klient paket för Current Branch.

**Krav och begränsningar:**  

-   Om du vill granska beroenden för operativ system filen för-klienten för Linux och UNIX, se [krav för klient distribution till Linux-och UNIX-servrar](../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  
-   En översikt över de hanterings funktioner som stöds för datorer som kör Linux eller UNIX finns i [Distribuera klienter till UNIX-och Linux-servrar](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  
-   För versioner av Linux och UNIX som stöds omfattar den listade versionen alla efterföljande del versioner. Till exempel, där support anges för CentOS version 6, innehåller detta även efterföljande lägre versioner av CentOS 6, t. ex. CentOS 6,3. På samma sätt gäller att när supporten visas för ett operativ system som använder Service Pack, t. ex. SUSE Linux Enterprise Server 11 SP1, innehåller stödet efterföljande Service Pack för den versionen av operativ systemet.
-   Information om klient installations paket och Universal Agent finns i [Distribuera klienter till UNIX-och Linux-servrar](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).


**Versioner som stöds:**   
Följande versioner stöds med den angivna. tar-filen.  
### <a name="aix"></a>AIX  

|Version|Fil|  
|-|-|  
|Version 5,3 (Power)|CCM-Aix53ppc. &lt; bygge \> . tar|  
|Version 6,1 (Power)|CCM-Aix61ppc. &lt; bygge \> . tar|  
|Version 7,1 (Power)|CCM-Aix71ppc. &lt; bygge \> . tar|  

### <a name="centos"></a>CentOS  

|Version|Fil|  
|-|-|  
|Version 5 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 5 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 6 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 6 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 7 x64|CCM-Universalx64. &lt; bygge \> . tar|  

### <a name="debian"></a>Debian  

|Version|Fil|    
|-|-|  
|Version 5 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 5 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 6x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 6 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 7 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 7 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 8 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 8 x64|CCM-Universalx64. &lt; bygge \> . tar|  

### <a name="hp-ux"></a>HP-UX  

|Version|Fil|  
|-|-|  
|Version 11iv2 IA64|CCM-HpuxB. 11.23-I64. &lt; bygge \> . tar|  
|Version 11iv2 PA – RISC|CCM – HpuxB. 11.23 PA. &lt; bygge \> . tar|  
|Version 11iv3 IA64|CCM-HpuxB. 11.31-I64. &lt; bygge \> . tar|  
|Version 11iv3 PA – RISC|CCM – HpuxB. 11.31 PA. &lt; bygge \> . tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Version|Fil|    
|-|-|  
|Version 5 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 5 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 6 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 6 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 7 x64|CCM-Universalx64. &lt; bygge \> . tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Version|Fil|  
|-|-|  
|Version 4 x86|CCM-RHEL4x86. &lt; bygge \> . tar|  
|Version 4 x64|CCM-RHEL4x64. &lt; bygge \> . tar|  
|Version 5 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 5 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 6 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 6 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 7 x64|CCM-Universalx64. &lt; bygge \> . tar|  

### <a name="solaris"></a>Solaris  

|Version|Fil|   
|-|-|  
|Version 9-SPARC|CCM-Sol9sparc. &lt; bygge \> . tar|  
|Version 10 x86|CCM-Sol10x86. &lt; bygge \> . tar|  
|Version 10-SPARC|CCM-Sol10sparc. &lt; bygge \> . tar|  
|Version 11 x86|CCM-Sol11x86. &lt; bygge \> . tar|  
|Version 11-SPARC|CCM-Sol11sparc. &lt; bygge \> . tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Version|Fil|  
|-|-|  
|Version 9 x86|CCM-SLES9x86. &lt; bygge \> . tar|  
|Version 10 SP1 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 10 SP1 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 11 SP1 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 11 SP1 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 12 x64|CCM-Universalx64. &lt; bygge \> . tar|  

### <a name="ubuntu"></a>Ubuntu  

|Version|Fil|    
|-|-|  
|Version 10,04 LTS x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 10,04 LTS x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 12,04 LTS x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 12,04 LTS x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 14,04 LTS x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 14,04 LTS x64|CCM-Universalx64. &lt; bygge \> . tar|  

### <a name="exchange-server-connector"></a>Exchange Server-anslutning
 LTSB stöder begränsad hantering av enheter som ansluter till Exchange Server-instansen, utan att installera klient program vara. Mer information finns i [Hantera mobila enheter med Configuration Manager och Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

 **Krav och begränsningar:**  

-   Configuration Manager erbjuder begränsad hantering för mobila enheter. Begränsad hantering är tillgängligt när du använder Exchange Server-anslutningen för Exchange Active Sync (EAS)-kompatibla enheter som ansluter till en server som kör Exchange Server eller Exchange Online.  

-   Mer information om de hanterings funktioner som Configuration Manager stöder för mobila enheter som hanteras med Exchange Server-anslutningen finns i [Välj en enhets hanterings lösning för Configuration Manager](../plan-design/choose-a-device-management-solution.md).  

**Versioner av Exchange Server som stöds:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> LTSB har inte stöd för hantering av enheter som ansluter via en online tjänst, t. ex. Exchange Online (Office 365).


## <a name="configuration-manager-console"></a>Configuration Manager-konsolen
LTSB stöder följande operativ system för att köra Configuration Manager-konsolen. Varje dator som är värd för konsolen måste ha en lägsta .NET Framework version av 4.5.2 Förutom Windows 10, vilket kräver minst .NET Framework 4,6.

**Operativ system som stöds:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): standard, data Center
- Windows Server 2012 (x64): standard, data Center
- Windows 10 Enterprise 2016-LTSB (x86, x64)
- Windows 10 Enterprise 2015-LTSB (x86, x64)
- Windows 8,1 (x86, x64): Professional, Enterprise


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>SQL Server versioner som stöds för plats databasen och rapporterings platsen
LTSB har stöd för följande versioner av SQL Server som värd för plats databasen och rapporterings platsen. För varje version som stöds, samma konfigurations krav och begränsningar som visas i [stöd för SQL Server versioner](../plan-design/configs/support-for-sql-server-versions.md) för Current Branch gäller för LTSB.  Detta inkluderar användningen av ett SQL Server-kluster eller en SQL Server AlwaysOn-tillgänglighetsgruppen.  

**Versioner som stöds:**

- SQL Server 2016: standard, Enterprise
- SQL Server 2014 SP2: standard, Enterprise
- SQL Server 2014 SP1: standard, Enterprise
- SQL Server 2012 SP3: standard, Enterprise
- SQL Server 2008 R2 SP3: standard, Enterprise, data Center
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Stöd för Active Directory-domäner
Alla LTSB-plats system måste vara medlemmar i en Windows Active Directory-domän som stöds. Stöd för Active Directory domäner har samma krav och begränsningar som visas i [stöd för Active Directory domäner](../plan-design/configs/support-for-active-directory-domains.md), men är begränsat till följande domän funktions nivåer:

**Nivåer som stöds:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Ytterligare support avsnitt som gäller för långsiktig service gren
Informationen i följande Current Branch avsnitt gäller för LTSB:
- [Antal och gränsvärden](../plan-design/configs/size-and-scale-numbers.md)
- [Plats och krav för platssystem](../plan-design/configs/site-and-site-system-prerequisites.md)
- [Alternativ för hög tillgänglighet](../servers/deploy/configure/high-availability-options.md)
- [Rekommenderad maskinvara](../plan-design/configs/recommended-hardware.md)
- [Stöd för Windows-funktioner och nätverk](../plan-design/configs/support-for-windows-features-and-networks.md)
- [Stöd för virtualiseringsmiljöer](../plan-design/configs/support-for-virtualization-environments.md)
