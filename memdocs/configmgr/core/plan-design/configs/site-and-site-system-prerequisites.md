---
title: Krav på webbplatsen
titleSuffix: Configuration Manager
description: Lär dig hur du konfigurerar en Windows-dator som en Configuration Manager plats system Server.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d4fb94d0ab64cb7c3dc3128c982b0c2b162b22b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719192"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Krav för plats och plats system för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Windows-baserade datorer kräver vissa konfigurationer för att stödja användningen som Configuration Manager plats system servrar.

För vissa produkter som Windows Server Update Services (WSUS) för program uppdaterings platsen måste du läsa produkt dokumentationen för att identifiera ytterligare krav och begränsningar för användning. Endast konfigurationer som används direkt för användning med Configuration Manager finns här.

Mer information om .NET Framework finns i [vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).


## <a name="general-requirements-and-limitations"></a><a name="bkmk_generalprerewq"></a>Allmänna krav och begränsningar

Följande krav gäller för alla plats system servrar:

- Varje plats system Server måste använda ett 64-bitars operativ system. Det enda undantaget är distributions platsens plats system roll, som du kan installera på vissa 32-bitars operativ system.  

- Plats system stöds inte på Server Core-installationer av operativ system. Ett undantag är att Server Core-installationer stöds för plats system rollen för distributions platsen. Mer information finns i [operativ system som stöds för Configuration Manager plats system servrar](supported-operating-systems-for-site-system-servers.md).  

- När en plats system Server har installerats går det inte att ändra:  

    - Domän namnet för den domän där plats system datorn finns (kallas även för ett **domän namns byte**).  

    - Datorns domän medlemskap.  

    - Datorns namn.  

    Om du måste ändra något av dessa objekt måste du först ta bort plats system rollen från datorn. Installera sedan om rollen när ändringen har slutförts. För ändringar som påverkar plats servern måste du först avinstallera platsen. Installera sedan om platsen när ändringen har slutförts.  

- Plats system roller stöds inte på en instans av ett Windows Server-kluster. Det enda undantaget är plats databas servern. Mer information finns i [använda ett SQL Server-kluster för Configuration Manager-plats databasen](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).  

    Från och med version 1810 blockerar Configuration Manager installations processen inte längre installationen av plats Server rollen på en dator med Windows-rollen för redundanskluster. SQL Always on kräver den här rollen, så det var tidigare att du inte kunde hitta plats databasen på plats servern. Med den här ändringen kan du skapa en plats med hög tillgänglighet med färre servrar med hjälp av SQL Always on och en plats server i passivt läge. Mer information finns i [alternativ för hög tillgänglighet](../../servers/deploy/configure/high-availability-options.md). <!--3607761, fka 1359132-->  

- Det finns inte stöd för att ändra start typen eller "logga in som"-inställningar för någon Configuration Manager-tjänst. Om du gör det kan du förhindra att viktiga tjänster körs på rätt sätt.  

### <a name="prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a>Krav för Windows Server 2012 och senare operativ system  

Se huvud avsnitten i den här artikeln för särskilda krav för plats system servrar och roller i Windows Server 2012 och senare:

- [Central administrations plats och primära plats servrar](#bkmk_2012sspreq)
- [Sekundär platsserver](#bkmk_2012secpreq)
- [Databasserver](#bkmk_2012dbpreq)
- [SMS-provider-Server](#bkmk_2012smsprovpreq)
- [Webbplats för programkatalog](#bkmk_2012acwspreq)
- [Webbservicepunkt för programkatalog](#bkmk_2012ACwsitepreq)
- [Tillgångsinformation plats för synkronisering](#bkmk_2012AIpreq)
- [Certifikatregistreringsplats](#bkmk_2012crppreq)
- [Distributionsplats](#bkmk_2012dppreq)
- [Plats för slutpunktsskydd](#bkmk_2012EPPpreq)
- [Registrerings plats](#bkmk_2012Enrollpreq)
- [Proxy för registrerings plats](#bkmk_2012EnrollProxpreq)
- [Status för återställningsplats](#bkmk_2012FSPpreq)
- [Hanterings plats](#bkmk_2012MPpreq)
- [Repor ting Services-plats](#bkmk_2012RSpoint)
- [Tjänst anslutnings punkt](#bkmk_SCPpreq)
- [Program uppdaterings plats](#bkmk_2012SUPpreq)
- [Plats för tillståndsmigrering](#bkmk_2012SMPpreq)

## <a name="central-administration-site-and-primary-site-servers"></a><a name="bkmk_2012sspreq"></a>Central administrations plats och primära plats servrar

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- .NET Framework 3.5

- RDC (Remote Differential Compression)  

- När du använder en program uppdaterings plats på en annan server än plats servern, installerar du administrations konsolen för WSUS på plats servern.

### <a name="net-framework"></a>.NET Framework

Aktivera Windows-funktionen för .NET Framework 3,5.

Installera även en version som stöds av .NET Framework version 4,5 eller senare. Från och med version 1906 stöder Configuration Manager .NET Framework 4,8.

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-adk"></a>Windows ADK  

- Innan du installerar eller uppgraderar en central administrations plats eller primär plats installerar du den version av Windows Assessment and Deployment Kit (ADK) som krävs av den version av Configuration Manager som du installerar eller uppgraderar till. Mer information finns i [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Mer information om det här kravet finns i [infrastruktur krav för distribution av operativ system](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

- Configuration Manager installerar Microsoft Visual C++ 2013 Redistributable Package på varje dator som installerar en plats Server.  

- Centrala administrations platser och primära platser kräver både x86-och x64-versioner av den tillämpliga distribuerbara filen.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="secondary-site-server"></a><a name="bkmk_2012secpreq"></a>Sekundär plats Server

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- .NET Framework 3.5

- RDC (Remote Differential Compression)  

### <a name="net-framework"></a>.NET Framework

Aktivera Windows-funktionen för .NET Framework 3,5.

Installera även en version som stöds av .NET Framework version 4,5 eller senare. Från och med version 1906 stöder Configuration Manager .NET Framework 4,8.

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable

- Configuration Manager installerar Microsoft Visual C++ 2013 Redistributable Package på varje dator som installerar en plats Server.  

- Sekundära platser kräver bara x64-versionen.  

### <a name="default-site-system-roles"></a>Standard plats system roller  

- Som standard installerar en sekundär plats en **hanterings plats** och en **distributions plats**.  

- Se till att den sekundära plats servern uppfyller kraven för dessa plats system roller.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="database-server"></a><a name="bkmk_2012dbpreq"></a>Databas server  

### <a name="remote-registry-service"></a>Tjänsten Remote Registry  

- När du har installerat Configuration Manager-platsen aktiverar du **Remote Registry** -tjänsten på den dator som är värd för plats databasen.  

### <a name="sql-server"></a>SQL Server  

- Innan du installerar en central administrations plats eller primär plats installerar du en version av SQL Server som stöds som värd för plats databasen. Mer information finns i [SQL Server-versioner som stöds](support-for-sql-server-versions.md).  

- Innan du installerar en sekundär plats kan du installera en version av SQL Server som stöds.  

- Om du väljer att Configuration Manager installera SQL Server Express som en del av installationen av den sekundära platsen kontrollerar du att datorn uppfyller kraven för att köra SQL Server Express.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a>SMS-provider-Server  

### <a name="windows-adk"></a>Windows ADK

- Datorn där du installerar en instans av SMS-providern måste ha den version av Windows ADK som krävs för den version av Configuration Manager som du installerar eller uppgraderar till kräver. Mer information finns i [Windows 10 ADK](support-for-windows-10.md#windows-10-adk).  

- Mer information om det här kravet finns i [infrastruktur krav för operativ Systems distribution](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- Om du använder [administrations tjänsten](../../../develop/adminservice/overview.md)måste den server som är värd för SMS-providerns roll ha .NET 4,5 eller senare  <!-- SCCMDocs issue #1203 -->

    > [!NOTE]
    > Configuration Manager version 1810 kräver .NET 4.5.2 eller senare.

- Webb server (IIS): varje provider försöker installera [administrations tjänsten](../../../develop/adminservice/overview.md). Den här tjänsten har ett beroende på IIS för att binda ett certifikat till HTTPS-port 443. Configuration Manager använder IIS-API: er för att kontrol lera den här certifikat konfigurationen. Om du konfigurerar platsen för [utökad http](../hierarchy/enhanced-http.md)använder Configuration Manager IIS-API: er för att binda det site-genererade certifikatet. Från och med version 2002 använder platsen automatiskt platsens självsignerade certifikat.

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a>Plats för program katalog  

> [!Important]  
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- .NET Framework 3.5

- ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Aktivera Windows-funktionen för .NET Framework 3,5.

Installera även en version som stöds av .NET Framework version 4,5 eller senare.

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-konfiguration  

- Vanliga HTTP-funktioner:  

    - Standarddokument  

    - Statiskt innehåll  

- Program utveckling:  

    - ASP.NET 3,5 (och automatiskt valda alternativ)  

    - ASP.NET 4,5 (och automatiskt valda alternativ)  

    - .NET Extensibility 3.5  

    - .NET Extensibility 4.5  

- Bullet  

    - Windows-autentisering  

- IIS 6-hanterings kompatibilitet:  

    - IIS 6-metabaskompatibilitet  


## <a name="application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a>Webb service punkt för program katalog  

> [!Important]  
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- .NET Framework 3.5

- ASP.NET 4,5:  

    - HTTP-aktivering (och automatiskt valda alternativ)  

### <a name="net-framework"></a>.NET Framework

Aktivera Windows-funktionen för .NET Framework 3,5.

Installera även en version som stöds av .NET Framework version 4,5 eller senare.

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-konfiguration

- Vanliga HTTP-funktioner:  

    - Standarddokument  

- IIS 6-hanterings kompatibilitet:  

    - IIS 6-metabaskompatibilitet  

- Program utveckling:  

    - ASP.NET 3,5 (och automatiskt valda alternativ)  

    - .NET Extensibility 3.5  

    - ASP.NET 4,5 (och automatiskt valda alternativ)  

    - .NET Extensibility 4.5  

### <a name="computer-memory"></a>Dator minne  

- Datorn som är värd för plats system rollen måste ha minst 5% av datorns tillgängliga minne ledigt för att plats system rollen ska kunna bearbeta begär Anden.  

- När den här plats system rollen samplaceras med en annan plats system roll som har samma krav, ökar inte det här minnes kravet för datorn, men förblir minst 5%.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a>Tillgångsinformation plats för synkronisering  

### <a name="net-framework"></a>.NET Framework

Installera en version som stöds av .NET Framework version 4,5 eller senare. Från och med version 1906 stöder Configuration Manager .NET Framework 4,8.

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="certificate-registration-point"></a><a name="bkmk_2012crppreq"></a>Certifikat registrerings plats  

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- .NET Framework

    - HTTP-aktivering  

### <a name="net-framework"></a>.NET Framework

Installera en version som stöds av .NET Framework version 4,5 eller senare. Från och med version 1906 stöder Configuration Manager .NET Framework 4,8.

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-konfiguration

- Program utveckling:  

    - ASP.NET 3,5 (och automatiskt valda alternativ)  

    - ASP.NET 4,5 (och automatiskt valda alternativ)  

- IIS 6-hanterings kompatibilitet:  

    - IIS 6-metabaskompatibilitet  

    - IIS 6 WMI-kompatibilitet  

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="distribution-point"></a><a name="bkmk_2012dppreq"></a>Distributions plats  

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- RDC (Remote Differential Compression)  

#### <a name="iis-configuration"></a>IIS-konfiguration

- Program utveckling:  

    - ISAPI-tillägg  

- Bullet  

    - Windows-autentisering  

- IIS 6-hanterings kompatibilitet:  

    - IIS 6-metabaskompatibilitet  

    - IIS 6 WMI-kompatibilitet  

### <a name="powershell"></a>PowerShell  

- På Windows Server 2012 eller senare krävs PowerShell 3,0 eller 4,0 innan du installerar distributions platsen.  

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable

- Configuration Manager installerar Microsoft Visual C++ 2013 Redistributable Package på varje dator som är värd för en distributions plats.  

- Vilken version som installeras beror på datorns plattform (x86 eller x64).  

### <a name="microsoft-azure"></a>Microsoft Azure  

- Du kan använda en moln tjänst i Microsoft Azure som värd för en distributions plats.  

### <a name="to-support-pxe-or-multicast"></a>För att stödja PXE eller multicast  

- Aktivera en PXE-svarare på en distributions plats utan Windows Deployment-tjänst.  

- Installera och konfigurera Windows Server-rollen Windows Deployment Services (WDS).  

    > [!NOTE]  
    > WDS installeras och konfigureras automatiskt när du konfigurerar en distributions plats så att den stöder PXE eller multicast på en server som kör Windows Server 2012 eller senare.  

- Kontrol lera att SQL Server Native Client är installerat och uppdaterat för en multicast-aktiverad distributions plats. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Mer information finns i [Installera och konfigurera distributions platser](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> När distributions platsen överför innehåll överförs den med den **Background Intelligent Transfer Service** (bitar) som är inbyggd i Windows. Distributions plats rollen kräver inte den valfria funktionen BITS IIS-servertillägg för att installeras, eftersom klienten inte överför information till den.  


## <a name="endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a>Endpoint Protection Point  

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server  

- .NET Framework 3.5

- Windows Defender-funktioner (Windows Server 2016 eller senare)  

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a>Registrerings plats  

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- .NET Framework 3.5

    - HTTP-aktivering (och automatiskt valda alternativ)  

    - ASP.NET 4.5  

    - WCF-tjänster (Windows Communication Foundation)<!-- SCCMDocs issue #1168 -->  

### <a name="net-framework"></a>.NET Framework

Aktivera Windows-funktionen för .NET Framework 3,5.

Installera även en version som stöds av .NET Framework version 4,5 eller senare. Från och med version 1906 stöder Configuration Manager .NET Framework 4,8.

> [!Note]
> När den här plats system rollen installeras installeras Configuration Manager automatiskt .NET Framework 4.5.2. Den här installationen kan placera servern i ett tillstånd som väntar på omstart. Om en omstart väntar för .NET Framework, kan .NET-program Miss klar tills servern har startats om och installationen har slutförts.  

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-konfiguration

- Vanliga HTTP-funktioner:  

    - Standarddokument  

- Program utveckling:  

    - ASP.NET 3,5 (och automatiskt valda alternativ)  

    - .NET Extensibility 3.5  

    - ASP.NET 4,5 (och automatiskt valda alternativ)  

    - .NET Extensibility 4.5  

- IIS 6-hanterings kompatibilitet:  

    - IIS 6-metabaskompatibilitet  

### <a name="computer-memory"></a>Dator minne

- Datorn som är värd för plats system rollen måste ha minst 5% av datorns tillgängliga minne ledigt för att plats system rollen ska kunna bearbeta begär Anden.  

- När den här plats system rollen samplaceras med en annan plats system roll som har samma krav, ökar inte det här minnes kravet för datorn, men förblir minst 5%.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a>Proxy för registrerings plats  

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- .NET Framework 3.5

### <a name="net-framework"></a>.NET Framework

Aktivera Windows-funktionen för .NET Framework 3,5.

Installera även en version som stöds av .NET Framework version 4,5 eller senare. Från och med version 1906 stöder Configuration Manager .NET Framework 4,8.

> [!Note]
> När den här plats system rollen installeras installeras Configuration Manager automatiskt .NET Framework 4.5.2. Den här installationen kan placera servern i ett tillstånd som väntar på omstart. Om en omstart väntar för .NET Framework, kan .NET-program Miss klar tills servern har startats om och installationen har slutförts.  

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-konfiguration

- Vanliga HTTP-funktioner:  

    - Standarddokument  

    - Statiskt innehåll  

- Program utveckling:  

    - ASP.NET 3,5 (och automatiskt valda alternativ)  

    - ASP.NET 4,5 (och automatiskt valda alternativ)  

    - .NET Extensibility 3.5  

    - .NET Extensibility 4.5  

- Bullet  

    - Windows-autentisering  

- IIS 6-hanterings kompatibilitet:  

    - IIS 6-metabaskompatibilitet  

### <a name="computer-memory"></a>Dator minne

- Datorn som är värd för plats system rollen måste ha minst 5% av datorns tillgängliga minne ledigt för att plats system rollen ska kunna bearbeta begär Anden.  

- När den här plats system rollen samplaceras med en annan plats system roll som har samma krav, ökar inte det här minnes kravet för datorn, men förblir minst 5%.  


## <a name="fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a>Återställnings status punkt

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- Server tillägg för BITS (och automatiskt valda alternativ) eller BITS (Background Intelligent Transfer Services) (och automatiskt valda alternativ)

#### <a name="iis-configuration"></a>IIS-konfiguration

Standard konfigurationen för IIS krävs med följande tillägg:  

- IIS 6-hanterings kompatibilitet:  

    - IIS 6-metabaskompatibilitet  


## <a name="management-point"></a><a name="bkmk_2012MPpreq"></a>Hanterings plats  

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- Server tillägg för BITS (och automatiskt valda alternativ) eller BITS (Background Intelligent Transfer Services) (och automatiskt valda alternativ)  

### <a name="net-framework"></a>.NET Framework

Installera en version som stöds av .NET Framework version 4,5 eller senare. Från och med version 1906 stöder Configuration Manager .NET Framework 4,8.

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-konfiguration

- Program utveckling:  

    - ISAPI-tillägg  

- Bullet  

    - Windows-autentisering  

- IIS 6-hanterings kompatibilitet:  

    - IIS 6-metabaskompatibilitet  

    - IIS 6 WMI-kompatibilitet  

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="reporting-services-point"></a><a name="bkmk_2012RSpoint"></a>Repor ting Services-plats  

### <a name="net-framework"></a>.NET Framework

Installera en version som stöds av .NET Framework version 4,5 eller senare. Från och med version 1906 stöder Configuration Manager .NET Framework 4,8.

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

- Installera och konfigurera minst en instans av SQL Server för att stödja SQL Server Reporting Services innan du installerar rapporterings platsen.  

- Den instans som du använder för SQL Server Reporting Services kan vara samma instans som du använder för plats databasen.  

- Dessutom kan instansen som du använder delas med andra System Center-produkter, förutsatt att de andra System Center-produkterna inte har några begränsningar för att dela instansen av SQL Server.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="service-connection-point"></a><a name="bkmk_SCPpreq"></a>Tjänst anslutnings punkt  

### <a name="net-framework"></a>.NET Framework

Aktivera Windows-funktionen för .NET Framework 3,5.

Installera även en version som stöds av .NET Framework version 4,5 eller senare. Från och med version 1906 stöder Configuration Manager .NET Framework 4,8.

> [!Note]
> När den här plats system rollen installeras installeras Configuration Manager automatiskt .NET Framework 4.5.2. Den här installationen kan placera servern i ett tillstånd som väntar på omstart. Om en omstart väntar för .NET Framework, kan .NET-program Miss klar tills servern har startats om och installationen har slutförts.  

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable

- Configuration Manager installerar Microsoft Visual C++ 2013 Redistributable Package på varje dator som är värd för en distributions plats.  

- Plats system rollen kräver x64-versionen.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="software-update-point"></a><a name="bkmk_2012SUPpreq"></a>Program uppdaterings plats  

### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- .NET Framework 3.5

Standard konfigurationen för IIS krävs.

### <a name="net-framework"></a>.NET Framework

Aktivera Windows-funktionen för .NET Framework 3,5.

Installera även en version som stöds av .NET Framework version 4,5 eller senare. Från och med version 1906 stöder Configuration Manager .NET Framework 4,8.

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-server-update-services"></a>Windows Server Update Services  

- Installera Windows Server-rollen Windows Server Update Services på en dator innan du installerar en program uppdaterings plats.  

- Mer information finns i [Planera för program uppdateringar](../../../sum/plan-design/plan-for-software-updates.md).  

> [!NOTE]  
> När du använder en program uppdaterings plats på en annan server än plats servern måste du installera WSUS-administrationskonsolen på plats servern.

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).


## <a name="state-migration-point"></a><a name="bkmk_2012SMPpreq"></a>Plats för tillståndsmigrering

<!--SCCMDocs issue 645-->
### <a name="windows-server-roles-and-features"></a>Roller och funktioner i Windows Server

- .NET Framework 3.5

    - HTTP-aktivering (och automatiskt valda alternativ)  

    - ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Aktivera Windows-funktionen för .NET Framework 3,5.

Installera även en version som stöds av .NET Framework version 4,5 eller senare. Från och med version 1906 stöder Configuration Manager .NET Framework 4,8.

> [!Note]
> När den här plats system rollen installeras installeras Configuration Manager automatiskt .NET Framework 4.5.2. Den här installationen kan placera servern i ett tillstånd som väntar på omstart. Om en omstart väntar för .NET Framework, kan .NET-program Miss klar tills servern har startats om och installationen har slutförts.  

Mer information om .NET Framework-versioner finns i följande artiklar:

- [.NET Framework versioner och beroenden](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)
- [Vanliga frågor och svar om livs cykeln – .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-konfiguration

- Vanliga HTTP-funktioner:  

    - Standarddokument  

- Program utveckling:  

    - ASP.NET 3,5 (och automatiskt valda alternativ)  

    - .NET Extensibility 3.5  

    - ASP.NET 4,5 (och automatiskt valda alternativ)  

    - .NET Extensibility 4.5  

- IIS 6-hanterings kompatibilitet:  

    - IIS 6-metabaskompatibilitet  

### <a name="sql-server-native-client"></a>SQL Server Native Client

När du installerar en ny plats installeras Configuration Manager automatiskt SQL Server Native Client som en distribuerbar komponent. Configuration Manager uppgraderar inte SQL Server Native Client när platsen har installerats. Kontrol lera att den här komponenten är aktuell. Mer information finns i [krav kontroll-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

