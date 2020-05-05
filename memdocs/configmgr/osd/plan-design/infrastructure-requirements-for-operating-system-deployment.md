---
title: Krav för OSD-infrastruktur
titleSuffix: Configuration Manager
description: Lär dig mer om externa och produkt beroenden och krav för operativ Systems distribution i Configuration Manager
ms.date: 07/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34c803cb2b43a2c69cee4c16f5029474e318eb2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724435"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Infrastruktur krav för operativ Systems distribution i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

OS-distribution i Configuration Manager har externa beroenden och beroenden inom produkten. Använd den här artikeln som hjälp för att förbereda infrastrukturen för operativ Systems distribution.  

##  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ExternalDependencies"></a>Externa beroenden till Configuration Manager  

Det här avsnittet innehåller information om externa verktyg, installations paket och OS-versioner som krävs för att distribuera operativ system i Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK för Windows 10  

Windows Assessment and Deployment Kit (ADK) är en uppsättning verktyg och dokumentation som stöder konfiguration och distribution av Windows. Configuration Manager använder Windows ADK för att automatisera åtgärder, till exempel installation av Windows, avbildningar och migrering av användar profiler och data.  

Mer information finns i följande artiklar:  

- [Windows ADK för Windows 10-scenarier för IT-specialister](https://docs.microsoft.com/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [Hämta Windows ADK för Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)  

    > [!IMPORTANT]
    > Se till att ladda ned både **Windows ADK för Windows 10** och **Windows PE-tillägget för ADK**.

- [Stöd för Windows 10](../../core/plan-design/configs/support-for-windows-10.md)  

#### <a name="site-systems"></a>Platssystem
Windows ADK är ett krav för följande plats system servrar:

- Plats servern för platsen på den översta nivån i hierarkin  

- Plats servern för varje primär plats i hierarkin  

- Varje instans av SMS-providern  


> [!NOTE]  
> Installera Windows ADK manuellt på varje plats Server innan du installerar Configuration Manager-platsen.  

#### <a name="windows-adk-features"></a>Windows ADK-funktioner
Installera följande funktioner i Windows ADK:  

-   USMT (User State Migration Tool)  

    > [!Note]  
    > USMT krävs inte på SMS-providern.

-   Windows Deployment Tools  

-   Windows Preinstallation Environment (Windows PE)  

    > [!Important]  
    > Från och med Windows 10 version 1809 är Windows PE ett separat installations program. Annars finns det ingen funktionell skillnad.<!--SCCMDocs-pr issue 2908-->  

En lista över de versioner av Windows 10 ADK som du kan använda med olika versioner av Configuration Manager finns i [stöd för Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).


### <a name="user-state-migration-tool-usmt"></a>USMT (User State Migration Tool)  

Configuration Manager använder ett USMT-paket som innehåller USMT 10-källfiler för att avbilda och återställa användar tillstånd som en del av distributionen av operativ systemet. Configuration Manager-installationen på platsen på den översta nivån skapar automatiskt USMT-paketet. USMT 10 fångar användar tillstånd från Windows 7, Windows 8, Windows 8,1 och Windows 10.  

Mer information finns i följande artiklar:  

- [Vanliga migreringsscenarier för USMT 10](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [Hantera användartillstånd](../get-started/manage-user-state.md)  


### <a name="windows-pe"></a>Windows PE  

Windows PE används för startavbildningar för att starta en dator. Det är en Windows-version med begränsade tjänster som används vid för installation och distribution av Windows. Följande lista innehåller de versioner av Windows ADK som stöds för Configuration Manager, aktuell gren:  

#### <a name="windows-adk-version"></a>Windows ADK-version  
Windows ADK för Windows 10. Mer information finns i [stöd för Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>Windows PE-versioner för start avbildningar som går att anpassa från Configuration Manager-konsolen  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>Windows PE-versioner som stöds för start avbildningar som inte kan anpassas från Configuration Manager-konsolen  
Windows PE 3.1<sup>1</sup> och Windows PE 5  

<sup>1</sup> du kan bara lägga till en start avbildning som ska Configuration Manager när den är baserad på Windows PE 3,1. Installera tillägget Windows AIK för Windows 7 SP1 för att uppgradera Windows AIK för Windows 7 (baserat på Windows PE 3) med tillägget Windows AIK för Windows 7 SP1 (baserat på Windows PE 3.1). Hämta tillägget Windows AIK för Windows 7 SP1 från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188).  

Om du till exempel har Configuration Manager kan du anpassa start avbildningar från Windows ADK för Windows 10 (baserat på Windows PE 10) från Configuration Manager-konsolen. Men även om det finns stöd för start avbildningar baserade på Windows PE 5 måste du anpassa dem från en annan dator och använda den DISM-version som är installerad med Windows ADK för Windows 8. Lägg sedan till Start avbildningen i Configuration Manager-konsolen. Mer information med stegen för att anpassa en start avbildning (lägga till valfria komponenter och driv rutiner), aktivera kommando stöd för start avbildningen, lägga till Start avbildningen i Configuration Manager-konsolen och uppdatera distributions platser med start avbildningen finns i [Anpassa Start avbildningar](../get-started/customize-boot-images.md). Mer information om startavbildningar finns i [Hantera startavbildningar](../get-started/manage-boot-images.md).  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  

WSUS krävs för program uppdaterings platsen, vilket krävs för att installera program uppdateringar under operativ Systems distributionen. Mer information finns i [installera en program uppdaterings plats](../../sum/get-started/install-a-software-update-point.md).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>IIS (Internet Information Services) på platssystemservrarna  

IIS krävs för distributions platsen, platsen för tillståndsmigrering och hanterings platsen. Mer information finns i [krav för plats och plats system](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  


### <a name="windows-deployment-services-wds"></a>WDS (Windows Deployment Services)  

I version 1802 och tidigare krävs WDS för PXE-distributioner. Från och med version 1806 kan du aktivera PXE på en distributions plats utan WDS. Mer information finns i [Windows Deployment Services](#BKMK_WDS) i den här artikeln. 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>DHCP (Dynamic Host Configuration Protocol)  

DHCP krävs för PXE-distribution. Du måste ha en fungerande DHCP-server med en aktiv värd för att distribuera operativsystem med PXE. Mer information om PXE-distributioner finns i [använda PXE för att distribuera Windows via nätverket](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Operativsystem och hårddiskkonfigurationer som stöds  

Mer information om de operativ system versioner och hård diskar som stöds av Configuration Manager när du distribuerar operativ system finns i [operativ system som stöds](#BKMK_SupportedOS) och [konfigurationer som stöds](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Windows-enhetsdrivrutiner  

Windows enhets driv rutiner kan användas när du installerar operativ systemet på mål datorn. De används också när du kör Windows PE i en start avbildning. Mer information finns i [Hantera driv rutiner](../get-started/manage-drivers.md).  



##  <a name="configuration-manager-dependencies"></a><a name="BKMK_InternalDependencies"></a>Configuration Manager beroenden  

Det här avsnittet innehåller information om Configuration Manager distributions krav för operativ system.  


### <a name="os-image"></a>OS-avbildning  

OS-avbildningar i Configuration Manager lagras i fil formatet WIM (Windows Imaging). De representerar en komprimerad samling av referenser och mappar. De här avbildningarna krävs för att kunna installera och konfigurera ett operativ system på en dator. Mer information finns i [hantera OS-avbildningar](../get-started/manage-operating-system-images.md).  


### <a name="driver-catalog"></a>Drivrutinskatalog  

Om du vill distribuera en enhets driv rutin importerar du enhets driv rutinen, aktiverar den och gör den tillgänglig på en distributions plats som Configuration Manager-klienten har åtkomst till. Mer information om driv rutins katalogen finns i [Hantera driv rutiner](../get-started/manage-drivers.md).  


### <a name="management-point"></a>Hanteringsplats  

Hanterings platser överför information mellan klienter och den Configuration Manager webbplatsen. Klienten använder en hanterings plats för att köra aktivitetssekvensen för att slutföra operativ Systems distributionen. Mer information om aktivitetssekvenser finns i [planerings överväganden för automatisering av uppgifter](planning-considerations-for-automating-tasks.md).  


### <a name="distribution-point"></a>Distributionsplats  

Distributions platser används i de flesta distributioner för att lagra de data som används för att distribuera ett operativ system, till exempel avbildningen eller driv rutins paketen. Aktivitetssekvenser hämtar normalt data från en distributions plats för att distribuera operativ systemet. Mer information om hur du installerar distributions platser och hanterar innehåll finns i [Hantera innehåll och innehålls infrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="pxe-enabled-distribution-point"></a>PXE-aktiverad distributionsplats  

Om du vill distribuera PXE-initierade distributioner konfigurerar du en distributions plats så att den accepterar PXE-begäranden från klienter. Mer information finns i [Konfigurera en distributions plats](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


### <a name="multicast-enabled-distribution-point"></a>Multicast-aktiverad distributionsplats  

Konfigurera en distributions plats så att den stöder multicast för att optimera distributioner av operativ system med hjälp av multicast. Mer information finns i [Konfigurera en distributions plats](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).   


### <a name="state-migration-point"></a>Plats för tillståndsmigrering  

När du samlar in och återställer användar tillstånds data för sida-vid-sida-och uppdaterings distributioner konfigurerar du en plats för tillståndsmigrering för att lagra användar tillstånds data på en annan dator.  

Mer information om hur du konfigurerar platsen för tillståndsmigrering finns i [Plats för tillståndsmigrering](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

Mer information om hur du avbildar och återställer användar tillstånd finns i [hantera användar tillstånd](../get-started/manage-user-state.md).  


### <a name="reporting-services-point"></a>Rapporteringstjänstpunkt  

Om du vill använda Configuration Manager rapporter för distributioner av operativ system installerar och konfigurerar du en rapporterings plats. Mer information finns i [Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="security-permissions-for-os-deployments"></a>Säkerhets behörigheter för distributioner av operativ system  

Säkerhets rollen **operativ system distributions hanteraren** är en inbyggd roll som du inte kan ändra. Du kan däremot kopiera rollen, göra ändringar och sedan spara ändringarna som en ny, anpassad säkerhetsroll. Här följer några av de behörigheter som är direkt tillämpliga på distributioner av operativ system:  

- **Startavbildningspaket**: Skapa, ta bort, ändra, ändra mapp, flytta objekt, läsa, ange säkerhetsomfattning  

- **Enhetsdrivrutiner**: Skapa, ta bort, ändra, ändra mapp, ändra rapport, flytta objekt, läsa, köra rapport  

- **Drivrutinspaket**: Skapa, ta bort, ändra, ändra mapp, flytta objekt, läsa, ange säkerhetsomfattning  

- **Operativsystemsavbildning**: Skapa, ta bort, ändra, ändra mapp, flytta objekt, läsa, ange säkerhetsomfattning  

- **Uppgraderings paket för operativ system**: skapa, ta bort, ändra, ändra mapp, flytta objekt, läsa, ange säkerhets omfattning  

- **Aktivitetssekvenspaket**: Skapa, skapa aktivitetssekvensmedia, ta bort, ändra, ändra mapp, ändra rapport, flytta objekt, läsa, köra rapport, ange säkerhetsomfattning  

Mer information finns i [skapa anpassade säkerhets roller](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  


### <a name="security-scopes-for-os-deployments"></a>Säkerhets omfattningar för distributioner av operativ system  

Använd säkerhets omfattningar för att ge administrativa användare åtkomst till de skydds bara objekt som används vid distribution av operativ system, till exempel operativ system och start avbildningar, driv rutins paket och aktivitetssekvenser. Mer information finns i [Säkerhetsomfattningar](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  



##  <a name="windows-deployment-services"></a><a name="BKMK_WDS"></a>Windows Deployment Services  

I version 1802 och tidigare måste Windows Deployment Services (WDS) installeras på samma server som de distributions platser som du konfigurerar för att stödja PXE eller multicast. WDS ingår i serverns operativ system. För PXE-distributioner är WDS den tjänst som utför PXE-starten. När distributions platsen har installerats och Aktiver ATS för PXE, Configuration Manager installerar en provider i WDS som använder WDS PXE-startfunktionerna.  

Från och med version 1806 kan du aktivera PXE på en distributions plats utan WDS. Mer information finns i alternativet **Aktivera en PXE-svarare utan Windows Deployment-tjänst** i [Installera och konfigurera distributions platser](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).


> [!NOTE]  
>  Om servern kräver en omstart kan installationen av WDS Miss Miss Missing. 


### <a name="wds-requirements"></a>WDS-krav  

-   WDS-installationen på servern kräver att administratören är medlem i den lokala administratörs gruppen.  

-   WDS-servern måste antingen vara medlem i en Active Directory-domän eller domänkontrollant för en Active Directory-domän. Alla domän- och skogkonfigurationer för Windows stödjer WDS.  

-   Om providern är installerad på en fjärrserver måste du installera WDS på plats servern och fjärrprovidern.  


###  <a name="considerations-when-you-have-wds-and-dhcp-on-the-same-server"></a><a name="BKMK_WDSandDHCP"></a>Att tänka på när du har WDS och DHCP på samma server  

Om du planerar att samköra distributions platsen på en server som kör DHCP bör du tänka på följande konfigurations problem:  

-   Du måste ha en fungerande DHCP-server med aktivt omfång. WDS använder PXE, som kräver en DHCP-server.  

-   En DNS-server krävs för att köra WDS.  

-   Följande UDP-portar måste vara öppna på WDS-servern:  

    -   Port 67 (DHCP)  

    -   Port 69 (TFTP)  

    -   Port 4011 (PXE)  

    > [!NOTE]  
    >  Om DHCP-auktorisering krävs på servern måste DHCP-klienten port 68 vara öppen på servern.  

-   Både DHCP och WDS kräver port nummer 67. Om du använder WDS och DHCP av samma värd kan du flytta DHCP eller distributions platsen som är konfigurerad för PXE till en separat server. Alternativt kan du använda följande procedur för att konfigurera WDS-servern att lyssna på en annan port.  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>Så här konfigurerar du WDS-servern att lyssna på en annan port  

1.  Ändra följande registernyckel:  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  Ange registervärdet **UseDhcpPorts** till **0**.  

3.  Kör följande kommando på servern för att den nya konfigurationen ska börja gälla:  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

> [!NOTE]
> I version 1810 och tidigare stöds inte PXE-svarare utan WDS på servrar som också kör en DHCP-server.
>
> Från och med version 1902 kan den nu finnas på samma server som DHCP-tjänsten när du aktiverar en PXE-svarare på en distributions plats utan Windows Deployment-tjänst. Mer information finns i [Konfigurera minst en distributions plats att acceptera PXE-begäranden](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure).


##  <a name="supported-operating-systems"></a><a name="BKMK_SupportedOS"></a>Operativ system som stöds  

Alla Windows-operativsystem som har stöd för klienter i [operativ system som stöds för klienter och enheter](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) stöds för distribution av operativ system.  



##  <a name="supported-disk-configurations"></a><a name="BKMK_SupportedDiskConfig"></a>Diskkonfigurationer som stöds  

Kombinationer av hård disk konfiguration på referens-och mål datorerna som stöds för Configuration Manager OS-distribution visas i följande tabell:  

|Hårddiskkonfiguration för referensdator|Hårddiskkonfiguration för måldator|  
|------------------------------------------------|--------------------------------------------------|  
|Standarddisk|Standarddisk|  
|Enkel volym på en dynamisk disk|Enkel volym på en dynamisk disk|  

Configuration Manager stöder endast avbildning av en operativ system avbildning från datorer som är konfigurerade med enkla volymer. Följande konfigurationer för hård diskar stöds inte:  

-   Disklänkade volymer  

-   Stripe-volymer (RAID 0)  

-   Speglade volymer (RAID 1)  

-   Paritetsvolymer (RAID 5)  

Följande tabell innehåller ytterligare en hård disk konfiguration på referens-och mål datorerna som inte stöds med Configuration Manager OS-distribution.  

|Hårddiskkonfiguration för referensdator|Hårddiskkonfiguration för måldator|  
|------------------------------------------------|--------------------------------------------------|  
|Standarddisk|Dynamisk disk|  



## <a name="next-steps"></a>Nästa steg

- [Förbereda platssystemroller för distribution av operativsystem](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
- [Förbereda för distribution av operativsystem](../get-started/prepare-for-operating-system-deployment.md)
