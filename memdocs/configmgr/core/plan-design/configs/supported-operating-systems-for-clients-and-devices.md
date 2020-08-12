---
title: Klienter och enheter som stöds
titleSuffix: Configuration Manager
description: Lär dig vilka versioner av operativ systemet Configuration Manager stöder för klienter och enheter.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 497a43fe6647f1dc2787f16a76f45ddd26d24796
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128856"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>OS-versioner som stöds för klienter och enheter för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager stöder installation av klient program vara på Windows-och macOS-datorer.  

## <a name="general-requirements-and-limitations"></a>Allmänna krav och begränsningar

Granska följande krav och begränsningar för alla klienter:

- Att ändra start typen eller **Logga in som** -inställningarna för en Configuration Manager-tjänst stöds inte. Den här ändringen kan förhindra att viktiga tjänster körs på rätt sätt.

## <a name="windows-computers"></a>Windows-datorer  

Om du vill hantera följande versioner av Windows OS använder du klienten som ingår i Configuration Manager. Mer information finns i [Distribuera klienter till Windows-datorer](../../clients/deploy/deploy-clients-to-windows-computers.md).  

### <a name="supported-client-os-versions"></a>Klient operativ system versioner som stöds

- **Windows 10**  

    Mer detaljerad information finns i [stöd för Windows 10](support-for-windows-10.md).  

- **Windows 8,1** (x86, x64): Professional, Enterprise

#### <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

<!--3556025-->
[Windows Virtual Desktop](https://docs.microsoft.com/azure/virtual-desktop/) är en Desktop-och app Virtualization-tjänst som körs på Microsoft Azure. Från och med version 1906 använder Configuration Manager för att hantera dessa virtuella enheter som kör Windows i Azure.

På samma sätt som en Terminal-Server tillåter vissa av dessa virtuella enheter flera samtidiga aktiva användarsessioner. För att hjälpa till med klient prestanda inaktiverar Configuration Manager nu användar principer på alla enheter som tillåter dessa flera användarsessioner. Även om du aktiverar användar principer inaktive RAS klienten som standard på dessa enheter, som omfattar Windows 10 Enterprise multi-session och Terminal-servrar.

Klienten inaktiverar bara användar principen när den identifierar den här typen av enhet under en ny installation. För en befintlig klient av den här typen som du uppdaterar till den här versionen kvarstår det tidigare beteendet. På en befintlig enhet konfigurerar den användar princip inställningen även om den upptäcker att enheten tillåter flera användarsessioner.

Om du behöver en användar princip i det här scenariot och godkänner eventuell prestanda påverkan kan du använda någon av följande metoder för att aktivera användar princip:

- I version 1910 och senare använder du [klient inställningar](../../clients/deploy/configure-client-settings.md). Konfigurera följande inställning i **klient princip** gruppen: **Aktivera användar princip för flera**användarsessioner.<!-- 4737447 -->

- I version 1906 använder du Configuration Manager SDK med [WMI-klassen SMS_PolicyAgentConfig Server](../../../develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class.md). Ange den nya `PolicyEnableUserPolicyOnTS` egenskapen till `true` .

> [!Note]  
> Du kan inte använda samhantering med en klient som kör Windows 10 Enterprise multi-session. <!-- SCCMDocs-pr#3950 -->

Från och med version 2006 finns **Windows 10 Enterprise multi-session** -plattformen i listan över OS-versioner som stöds på objekt med krav regler eller tillämplighets listor.<!--6527576-->

> [!NOTE]
> Om du tidigare har valt **Windows 10** -plattformen på den översta nivån, markeras automatiskt alla underordnade plattformar i den här åtgärden. Den här nya plattformen väljs inte automatiskt. Om du vill lägga till **Windows 10 Enterprise multi-session**väljer du det manuellt i listan.

Mer information finns i följande artiklar:

- [Stöd för virtualiseringsmiljöer](support-for-virtualization-environments.md)
- [Hantera Configuration Manager klienter i en VDI-infrastruktur (Virtual Desktop Infrastructure)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)

### <a name="supported-server-os-versions"></a>OS-versioner som stöds

- **Windows Server 2019**: standard, data Center <sup> [Anmärkning 1](#bkmk_note1)</sup>  
    (Från och med Configuration Manager version 1806.)

- **Windows Server 2016**: standard, data Center <sup> [Anmärkning 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**: arbets grupp, standard  

- **Windows Server 2012 R2** (x64): standard, data Center <sup> [Anmärkning 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64): standard, data Center <sup> [Anmärkning 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### <a name="server-core"></a>Server Core

Följande versioner refererar specifikt till Server Core-installationen av operativ systemet. <sup>[Anmärkning 3](#bkmk_note3)</sup>  

Windows Server-halvårs kanal versioner är Server Core-installationer, till exempel Windows Server, version 1809. Som en Configuration Manager-klient stöds de på samma sätt som den associerade Windows 10-halvårs kanal versionen. Mer information finns i [stöd för Windows 10](support-for-windows-10.md).

- **Windows Server 2019** (x64) <sup> [Anmärkning 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup> [Anmärkning 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup> [Anmärkning 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup> [Anmärkning 2](#bkmk_note2)</sup>

#### <a name="note-1"></a><a name="bkmk_note1"></a>Anmärkning 1

Configuration Manager test och stöder Windows Server Data Center-versioner, men är inte officiellt certifierat för Windows Server. Stöd för Configuration Manager Hotfix erbjuds inte för problem som är specifika för Windows Server Data Center Edition. Mer information om certifierings programmet för Windows Server finns i [Windows Server-katalogen](https://www.windowsservercatalog.com/).

#### <a name="note-2"></a><a name="bkmk_note2"></a>Anmärkning 2

Om du vill använda [push-installation av klienter](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)lägger du till fil Server tjänsten för Server rollen fil-och lagrings tjänster. Mer information om hur du installerar Windows-funktioner på Server Core finns i [Installera roller, roll tjänster och funktioner med hjälp av Windows PowerShell-cmdletar](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets).  

#### <a name="note-3"></a><a name="bkmk_note3"></a>Anmärkning 3

Den nya Software Center-appen stöds inte på någon version av Windows Server Core.<!--SCCMDocs issue 683-->

## <a name="windows-embedded-computers"></a>Windows Embedded-datorer  

Hantera Windows Embedded-enheter genom att installera Configuration Manager-klienten på enheten. Mer information finns i [Planera för klient distribution till Windows Embedded-enheter](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

### <a name="requirements-and-limitations"></a>Krav och begränsningar

- Alla klient funktioner stöds på Windows Embedded-system som inte har Skriv filter aktiverade.  

- Klienter som använder något av följande stöds för alla funktioner förutom energispar funktioner:  

  - Förbättrade Skriv filter (EWF)

  - Filbaserade RAM-baserade Skriv filter (FBWF)

  - Enhetliga Skriv filter (UWF)  

- Program katalogen stöds inte för någon Windows Embedded-enhet.  

### <a name="supported-os-versions"></a>OS-versioner som stöds  

- **Windows 10 Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Den här versionen omfattar LTSC (Long-term Servicing Channel). Mer information finns i [Översikt över Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows Embedded 8,1-bransch** (x86, x64)

- **Windows Embedded 8 standard** (x86, x64)

- **Windows tunn dator** (x86, x64)

- **Windows Embedded POSReady 7** (x86, x64)

- **Windows Embedded Standard 7 med SP1** (x86, x64)

## <a name="windows-ce-computers"></a>Windows CE datorer

Hantera Windows CE enheter med Configuration Manager äldre klient för mobila enheter som ingår i Configuration Manager.  

### <a name="requirements-and-limitations"></a>Krav och begränsningar

- Den mobila enhets klienten kräver 0,78 MB lagrings utrymme för installation. Inloggning kan kräva upp till 256 KB ytterligare lagrings utrymme.

- Funktionerna för dessa mobila enheter varierar efter plattform och klient typ. Information om vilka hanterings funktioner som stöds finns i [Välj en lösning för enhets hantering](../choose-a-device-management-solution.md).  

### <a name="supported-os-versions"></a>OS-versioner som stöds

- Windows CE 7,0 (ARM-och x86-processorer)  

    > [!IMPORTANT]
    > Configuration Manager version 2006 släpper stöd för Windows CE 7,0 som en klient. Utfasningen presenterades av [version 1906](../changes/whats-new-in-version-1906.md#bkmk_deprecated).

#### <a name="supported-languages-include"></a>Språk som stöds är

- Kinesiska (förenklad och traditionell)

- Engelska (USA)

- Franska (Frankrike)

- Tyska

- Italienska

- Japanska  

- Koreanska  

- Portugisiska (Brasilien)  

- Ryska  

- Spanska (Spanien)  

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a>Utökade säkerhets uppdateringar och Configuration Manager

[ESU-programmet (Extended Security updates)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) är ett sista utväg-alternativ för kunder som behöver köra vissa äldre Microsoft-produkter efter Supportens slut. Till exempel Windows 7. Den innehåller viktiga och/eller viktiga säkerhets uppdateringar (enligt definitionen i [Microsoft Security Response Center (MSRC)](https://www.microsoft.com/msrc)) i högst tre år efter produktens slut på datum för utökad support.

Produkter som ligger utanför support livs cykeln stöds inte för användning med Configuration Manager. Detta omfattar alla produkter som omfattas av ESU-programmet. Säkerhets uppdateringar som släpps under ESU-programmet publiceras till Windows Server Update Services (WSUS). De här uppdateringarna visas i Configuration Manager-konsolen. Även om produkter som omfattas av ESU-programmet inte längre stöds för användning med Configuration Manager, kan den [senaste utgivna versionen av Configuration Manager aktuella grenen](../../servers/manage/updates.md#version-details) användas för att distribuera och installera Windows-säkerhetsuppdateringar som lanseras i programmet. Den senaste versionen kan också användas för att distribuera Windows 10 till enheter som kör Windows 7.

Klient hanterings funktioner som inte är relaterade till Windows program uppdaterings hantering eller operativ system distribution kommer inte längre att testas på de operativ system som omfattas av ESU-programmet och vi garanterar inte att de kommer att fortsätta att fungera. Vi rekommenderar starkt att du uppgraderar eller migrerar till en aktuell version av operativ systemen så snart som möjligt för att få klient hanterings stöd.

## <a name="mac-computers"></a>Mac-datorer  

Hantera Apple Mac-datorer med Configuration Manager-klienten för macOS.  

Installations paketet för macOS-klienten levereras inte med Configuration Manager mediet. Ladda ned den från Microsoft Download Center, [Microsoft Endpoint Configuration Manager-MacOS-klienten (64-bitars)](https://www.microsoft.com/download/details.aspx?id=100850).  

Mer information finns i [Distribuera klienter till Mac-datorer](../../clients/deploy/deploy-clients-to-macs.md).  

### <a name="requirements-and-limitations"></a>Krav och begränsningar

- Det finns inte stöd för att installera eller köra Configuration Manager-klienten för macOS på datorer under ett annat konto än root. Om du gör det kan det hindra att viktiga tjänster körs på rätt sätt.  

### <a name="supported-versions"></a>Versioner som stöds

- **MacOS-Catalina (10,15)** (kräver Configuration Manager plats version 1910 eller senare och Configuration Manager klienten för MacOS-version 5.0.8742.1000 eller senare)

- **macOS-Mojave (10,14)**

- **macOS, hög Sierra (10,13)**

## <a name="linux-and-unix-servers"></a>Linux-och UNIX-servrar  

> [!Important]  
> Configuration Manager version 1902 släpper stöd för Linux och UNIX som en klient. Utfasningen presenterades av [version 1802](../changes/whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support). Överväg Microsoft Azure hantering för hantering av Linux-servrar. Azure-lösningar har omfattande Linux-support som i de flesta fall överskrider Configuration Manager-funktioner, inklusive slut punkt till slut punkt för korrigerings hantering för Linux.

Klient installations paketen för Linux och UNIX levereras inte med Configuration Manager mediet. Hämta **klienter för ytterligare operativ system** från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719). Utöver klient installations paketen omfattar klient nedladdningen skriptet som hanterar installationen av klienten på varje dator.  

### <a name="requirements-and-limitations"></a>Krav och begränsningar

- Om du vill granska operativ system fil beroenden för-klienten för Linux och UNIX, se [krav för klient distribution till Linux-och UNIX-servrar](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

- En översikt över vilka hanterings funktioner som stöds för Linux eller UNIX finns i [Distribuera klienter till UNIX-och Linux-servrar](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

- För versioner av Linux och UNIX som stöds omfattar den listade versionen alla efterföljande del versioner. CentOS version 6 innehåller till exempel CentOS 6,3. På samma sätt innehåller stöd för ett operativ system som använder Service Pack (till exempel SUSE Linux Enterprise Server 11 SP1) efterföljande Service Pack för den OS-versionen.  

- Information om klient installations paket och Universal Agent finns i [Distribuera klienter till UNIX-och Linux-servrar](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

### <a name="supported-versions"></a>Versioner som stöds

Följande versioner stöds med den angivna. tar-filen.  

#### <a name="aix"></a>AIX  

|Version|TAR-fil|  
|-|-|  
|Version 6,1 (Power)|CCM-Aix61ppc. &lt; bygge \> . tar|  
|Version 7,1 (Power)|CCM-Aix71ppc. &lt; bygge \> . tar|  

#### <a name="centos"></a>CentOS  

|Version|TAR-fil|  
|-|-|  
|Version 5 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 5 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 6 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 6 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 7 x64|CCM-Universalx64. &lt; bygge \> . tar|  

#### <a name="debian"></a>Debian  

|Version|TAR-fil|  
|-|-|  
|Version 5 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 5 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 6 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 6 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 7 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 7 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 8 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 8 x64|CCM-Universalx64. &lt; bygge \> . tar|  

#### <a name="hp-ux"></a>HP-UX  

|Version|TAR-fil|  
|-|-|  
|Version 11iv3 IA64|CCM-HpuxB. 11.31-I64. &lt; bygge \> . tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Version|TAR-fil|  
|-|-|  
|Version 5 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 5 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 6 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 6 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 7 x64|CCM-Universalx64. &lt; bygge \> . tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Version|TAR-fil|  
|-|-|  
|Version 5 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 5 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 6 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 6 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 7 x64|CCM-Universalx64. &lt; bygge \> . tar|  

#### <a name="solaris"></a>Solaris  

|Version|TAR-fil|  
|-|-|  
|Version 10 x86|CCM-Sol10x86. &lt; bygge \> . tar|  
|Version 10-SPARC|CCM-Sol10sparc. &lt; bygge \> . tar|  
|Version 11 x86|CCM-Sol11x86. &lt; bygge \> . tar|  
|Version 11-SPARC|CCM-Sol11sparc. &lt; bygge \> . tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Version|TAR-fil|  
|-|-|  
|Version 10 SP1 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 10 SP1 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 11 SP1 x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 11 SP1 x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 12 x64|CCM-Universalx64. &lt; bygge \> . tar|  

#### <a name="ubuntu"></a>Ubuntu  

|Version|TAR-fil|  
|-|-|  
|Version 10,04 LTS x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 10,04 LTS x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 12,04 LTS x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 12,04 LTS x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 14,04 LTS x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 14,04 LTS x64|CCM-Universalx64. &lt; bygge \> . tar|  
|Version 16,04 LTS x86|CCM-Universalx86. &lt; bygge \> . tar|  
|Version 16,04 LTS x64|CCM-Universalx64. &lt; bygge \> . tar|  


## <a name="on-premises-mdm"></a><a name="bkmk_OnpremOS"></a>Lokal MDM

Configuration Manager har inbyggda funktioner för att hantera mobila enheter som finns lokalt utan att installera klient program vara. Mer information finns i [Hantera mobila enheter med lokal infrastruktur](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="supported-operating-systems"></a>Operativsystem som stöds

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Den här versionen omfattar LTSC (Long-term Servicing Channel). Mer information finns i [Översikt över Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 IoT Mobile Enterprise**  

- **Windows 10 team för Surface Hub**  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

    > [!IMPORTANT]
    > Configuration Manager version 2006 släpper stöd för Windows 10 Mobile och Windows 10 Mobile Enterprise som en klient. Utfasningen presenterades av [version 1906](../changes/whats-new-in-version-1906.md#bkmk_deprecated).

## <a name="exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a>Exchange Server-anslutning  

Configuration Manager stöder begränsad hantering av enheter som ansluter till Exchange-servern, utan att installera Configuration Manager-klienten. Mer information finns i [Hantera mobila enheter med Configuration Manager och Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="supported-versions-of-exchange-server"></a>Versioner av Exchange Server som stöds

- **Exchange Online (Office 365)**: den här versionen omfattar Business Productivity Online Standard Suite  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange server 2010 SP1** eller **Exchange Server 2010 SP2**
