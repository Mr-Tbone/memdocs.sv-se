---
title: Planera plats system roller
titleSuffix: Configuration Manager
description: Överväg att använda plats system servrar och plats system roller när du planerar din Configuration Manager-hierarki.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fb8c54920c10f8d3601a939c3c7b442c95e1dcf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722447"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>Planera för plats system servrar och plats system roller i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Varje Configuration Manager plats som du installerar inkluderar en plats server som är en **plats system Server**. Platsen kan också innehålla flera platssystemservrar på datorer som är fjärranslutna från platsservern. Platssystemservrar (platsservern eller en fjärransluten platssystemserver) har stöd för **platssystemroller**.  

## <a name="site-system-servers"></a><a name="bkmk_siteservers"></a>Plats system servrar  

När du installerar en plats system roll på en dator blir datorn en plats system Server. På varje plats kan du installera en eller flera ytterligare plats system servrar. Du behöver inte installera fler plats system servrar och du kan välja att köra alla plats system roller direkt på plats serverdatorn. Varje plats system Server stöder en eller flera plats system roller. Ytterligare servrar kan hjälpa dig att utöka funktionerna och kapaciteten för en plats genom att dela bearbetnings belastningen som plats system rollerna placerar på en server.  

När du funderar på att lägga till en plats system Server kontrollerar du att servern uppfyller kraven för den avsedda användningen. Lägg även till den på en nätverks plats som har tillräckligt med bandbredd för att kommunicera med förväntade slut punkter. Dessa slut punkter omfattar plats servern, domän resurser, en molnbaserad plats, plats system servrar och klienter.  


## <a name="site-system-roles"></a><a name="bkmk_planroles"></a>Plats system roller  

Installera plats system roller på en server för att ge ytterligare funktioner till platsen. Exempel på rekommendationer:  

- Ytterligare hanterings platser så att platsen kan stödja fler enheter, upp till platsens kapacitet som stöds.  

- Ytterligare distributions platser för att utöka innehålls infrastrukturen och förbättra prestandan för innehålls distributioner till enheter.  

- En eller flera funktioner som är speciella för vissa plats system roller. En program uppdaterings plats gör det till exempel möjligt att hantera program uppdateringar för hanterade enheter. Med en repor ting Services-plats kan du köra rapporter för att övervaka, förstå och dela information om din miljö.  

Olika Configuration Manager-platser har stöd för olika uppsättningar av plats system roller. Vilken uppsättning plats system roller som stöds beror på typen av plats. (De olika typerna av webbplatser är en central administrations plats, primära platser eller sekundära platser.) Topologin för hierarkin kan begränsa placeringen av vissa roller på vissa plats typer. Tjänst anslutnings punkten stöds till exempel bara på platsen på den översta nivån i hierarkin. Platsen på den översta nivån kan vara en central administrations plats eller en fristående primär plats. Den här rollen stöds inte på en underordnad primär plats eller på sekundära platser.  

När en plats har installerats kan du flytta platsen för vissa plats system roller från standard platsen på plats servern till en annan server. Till exempel installeras hanterings platsen eller distributions plats rollerna som standard på en primär eller sekundär plats Server. Installera också ytterligare instanser av vissa plats system roller för att utöka funktionerna på din plats och för att uppfylla dina affärs behov. Vissa roller är obligatoriska, medan andra är valfria.  

### <a name="configuration-manager-site-server"></a>Configuration Manager plats Server

Den här rollen identifierar servern där Configuration Manager installations programmet körs för att installera en plats eller den server där du installerar en sekundär plats. Du kan inte flytta eller avinstallera den här rollen förrän platsen har avinstallerats.  

### <a name="configuration-manager-site-system"></a>Configuration Manager plats system

Den här rollen tilldelas till alla datorer där du antingen installerar en plats eller installerar en plats system roll. Du kan inte flytta eller avinstallera den här rollen förrän du tar bort den sista plats system rollen från datorn.  

### <a name="configuration-manager-component-site-system-role"></a>Plats system roll för Configuration Manager-komponenten

Den här rollen identifierar ett plats system som kör en instans av tjänsten **SMS Executive** . Det krävs stöd för andra roller, som hanterings platser. Du kan inte flytta eller avinstallera den här rollen förrän du tar bort den sista tillämpliga plats system rollen från datorn.  

### <a name="configuration-manager-site-database-server"></a>Configuration Manager plats databas server

Platsen tilldelar den här rollen till plats system servrar som innehåller en instans av plats databasen. Flytta bara den här rollen till en ny server genom att köra installations programmet för att ändra platsen till att använda en annan instans av SQL Server som värd för plats databasen.  

### <a name="sms-provider"></a>SMS-provider

Platsen tilldelar den här rollen till varje dator som är värd för en instans av SMS-providern. Providern är gränssnittet mellan en Configuration Manager-konsol och plats databasen. Som standard installeras den här rollen automatiskt på plats servern för en central administrations plats och primära platser. Installera ytterligare instanser på varje plats för att ge åtkomst till ytterligare administrativa användare eller för redundans.  

Installera ytterligare providrar genom att köra Configuration Manager-installationen för att [Hantera SMS-providern](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Installera sedan ytterligare providrar på ytterligare datorer. Installera bara en instans av SMS-providern på en dator. Datorn måste finnas i samma domän som plats servern.  

### <a name="application-catalog-web-service-point"></a>Webb service punkt för program katalog

> [!Important]
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

En plats system roll som tillhandahåller program varu information till webbplatsen för program katalogen från program varu biblioteket. Även om den här rollen endast stöds på primära platser kan du installera flera instanser av den här rollen på en plats eller på flera platser i samma hierarki.  

### <a name="application-catalog-website-point"></a>Plats för program katalog

> [!Important]
> Program katalogens Silverlight-användar upplevelse stöds inte av den aktuella gren versionen 1806. Från och med version 1906 använder uppdaterade klienter automatiskt hanterings platsen för program distributioner som är tillgängliga för användare. Du kan inte heller installera nya program katalog roller. Support upphör för program katalog rollerna med version 1910.  
>
> Mer information finns i följande artiklar:
>
> - [Konfigurera Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Borttagna och föråldrad funktioner](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

En plats system roll som förser användare med en lista över tillgängliga program från program katalogen. Även om den här rollen endast stöds på primära platser kan du installera flera instanser av den här rollen på en plats eller på flera platser i samma hierarki.  

### <a name="asset-intelligence-synchronization-point"></a>Plats för synkronisering av tillgångsinformation

En plats system roll som ansluter till Microsoft för att hämta information för Tillgångsinformation katalogen. Den här rollen överför också Okategoriserade titlar, så att Microsoft kan betrakta dem för framtida inkludering i katalogen. En hierarki har endast stöd för en enda instans av den här rollen på platsen på den översta nivån i hierarkin. Om du expanderar en fristående primär plats till en större hierarki måste du avinstallera den här rollen från den primära platsen. Installera den på den centrala administrations webbplatsen.

Mer information finns i [tillgångsinformation i Configuration Manager](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

### <a name="certificate-registration-point"></a>Certifikatregistreringsplats

En plats system roll som kommunicerar med en server som kör registrerings tjänsten för nätverks enheter (NDES). Den här rollen hanterar begär Anden om enhets certifikat som använder Simple Certificate Enrollment Protocol (SCEP). Den här rollen stöds endast på primära platser och den centrala administrationswebbplatsen.

Även om en enda certifikat registrerings plats kan tillhandahålla funktioner till en hel hierarki, kanske du vill installera flera instanser av den här rollen på en plats och på flera platser i samma hierarki. Den här designen hjälper till med belastnings utjämning. När det finns flera instanser i en hierarki tilldelas klienter slumpmässigt till en certifikatregistreringsplats.  

Varje certifikat registrerings plats kräver åtkomst till en separat NDES-instans. Du kan inte konfigurera två eller fler certifikat registrerings platser att använda samma NDES-instans. Installera dessutom inte certifikat registrerings platsen på samma server som kör NDES.  

### <a name="cloud-management-gateway-connection-point"></a>Anslutning punkt för moln hanterings-Gateway

En plats system roll för kommunikation med [Cloud Management Gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md).  

### <a name="data-warehouse-service-point"></a>Informations lager service punkt

Använd informations lager service punkten för att lagra och rapportera långsiktiga historiska data i din Configuration Managers miljö. Mer information finns i [informations lager](../../servers/manage/data-warehouse.md).  

### <a name="distribution-point"></a>Distributionsplats

En plats system roll som innehåller källfiler för klienter som ska laddas ned, till exempel:

- Program innehåll
- Program varu paket
- Programuppdateringar
- Operativsystemavbildningar
- Startavbildningar  

Som standard installeras den här rollen på plats servern när du installerar en ny primär eller sekundär plats. Den här rollen stöds inte på en central administrations plats. Installera flera instanser av den här rollen på en plats som stöds, och på flera platser i samma hierarki. Mer information finns i [grundläggande begrepp för innehålls hantering](fundamental-concepts-for-content-management.md)och [Hantera innehåll och innehålls infrastruktur](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="endpoint-protection-point"></a>Plats för slutpunktsskydd

En plats system roll som Configuration Manager använder för att godkänna licens villkoren för Endpoint Protection och för att konfigurera standard medlemskap för moln skydds tjänsten. En hierarki har endast stöd för en instans av den här rollen och måste finnas på platsen på den översta nivån. Om du expanderar en fristående primär plats till en större hierarki måste du avinstallera den här rollen från den primära platsen och sedan installera den på den centrala administrations platsen. Mer information finns i [Endpoint Protection i Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="enrollment-point"></a>Registreringsplats

En plats system roll som använder PKI-certifikat för Configuration Manager för att registrera mobila enheter och macOS-datorer. Även om den här rollen endast stöds på primära platser kan du installera flera instanser av den här rollen på en plats eller på flera platser i samma hierarki.  

Om en användare registrerar mobila enheter med hjälp av Configuration Manager och användarens Active Directory konto finns i en skog som inte är betrodd av plats serverns skog, installerar du en registrerings plats i användarens skog. Sedan kan Configuration Manager autentisera användaren.  

### <a name="enrollment-proxy-point"></a>Registreringsproxyplats

En plats system roll som hanterar Configuration Manager registrerings förfrågningar från mobila enheter och macOS-datorer. Även om den här rollen endast stöds på primära platser kan du installera flera instanser av den här rollen på en plats eller på flera platser i samma hierarki.  

När du har stöd för mobila enheter på Internet installerar du en proxy för registrerings plats i ett perimeternätverk och installerar en på intranätet.

### <a name="exchange-server-connector"></a>Exchange Server-anslutning

Information om den här rollen finns i [Hantera mobila enheter med Configuration Manager och Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="fallback-status-point"></a>Status för återställningsplats

En plats system roll som hjälper dig att övervaka klient installationen. Den identifierar klienter som är ohanterade eftersom de inte kan kommunicera med sin hanterings plats. Även om den här rollen endast stöds på primära platser kan du installera flera instanser av den här rollen på en plats och på flera platser i samma hierarki.

### <a name="management-point"></a>Hanteringsplats

En plats system roll som tillhandahåller information om principer och tjänst platser till klienter. Den tar också emot konfigurations data från klienter.  

Som standard installeras den här rollen på plats servern när du installerar en ny primär eller sekundär plats. Primära platser har stöd för flera instanser av den här rollen. Sekundära platser har stöd för en enda hanterings plats. Den här rollen på en sekundär plats kallas även för en hanterings plats för proxy, och tillhandahåller en lokal kontakt punkt där klienter kan hämta principer för datorer och användare.  

Konfigurera hanterings platser för att stödja antingen HTTP eller HTTPs. De kan också stödja mobila enheter som du hanterar med Configuration Manager lokal hantering av mobila enheter (MDM). För att minska belastningen på plats databas servern av hanterings platser när de hanterar begär Anden från klienter använder du [databas repliker för hanterings platser](../../servers/deploy/configure/database-replicas-for-management-points.md).  

### <a name="reporting-services-point"></a>Rapporteringstjänstpunkt

En plats system roll som integreras med SQL Server Reporting Services för att skapa och hantera rapporter för Configuration Manager. Den här rollen stöds på primära platser och den centrala administrations platsen, och du kan installera flera instanser av den här rollen på en plats som stöds. Mer information finns i [Planera för rapportering](../../servers/manage/planning-for-reporting.md).  

### <a name="service-connection-point"></a>Tjänstanslutningspunkt

En plats system roll som överför användnings data från din plats och krävs för att göra uppdateringar för Configuration Manager tillgängliga i-konsolen. En hierarki har endast stöd för en enda instans av den här rollen och måste finnas på den översta nivån i hierarkin. Om du expanderar en fristående primär plats till en större hierarki måste du avinstallera den här rollen från den primära platsen och sedan installera den på den centrala administrations platsen. Mer information finns i [om tjänst anslutnings punkten](../../servers/deploy/configure/about-the-service-connection-point.md).  

### <a name="software-update-point"></a>Programuppdateringsplats

En plats system roll som integreras med Windows Server Update Services (WSUS) för att tillhandahålla program uppdateringar till Configuration Manager-klienter. Den här rollen stöds på alla platser:  

- Installera det här plats systemet på den centrala administrations platsen för att synkronisera med WSUS.  

- Konfigurera varje instans av den här rollen på underordnade primära platser för att synkronisera med den centrala administrations platsen.  

- När data överföringen i nätverket är långsam bör du överväga att installera en program uppdaterings plats på sekundära platser.  

Mer information finns i [Planera för program uppdateringar](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>Plats för tillståndsmigrering

När du migrerar en dator till ett nytt operativ system lagrar den här plats system rollen användar tillstånds data. Den här rollen stöds på primära platser och på sekundära platser. Installera flera instanser av den här rollen på en plats och på flera platser i samma hierarki. Mer information om att lagra användar tillstånd när du distribuerar ett operativ system finns i [hantera användar tillstånd](../../../osd/get-started/manage-user-state.md).  


## <a name="next-steps"></a>Nästa steg

Vissa Configuration Manager plats system roller kräver anslutning till Internet. Om din miljö kräver Internet trafik för att använda en proxyserver konfigurerar du dessa plats system roller för att använda proxyn. Mer information finns i [stöd för proxy server](../network/proxy-server-support.md).  
