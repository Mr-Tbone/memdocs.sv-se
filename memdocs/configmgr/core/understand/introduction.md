---
title: Vad är Configuration Manager?
titleSuffix: Configuration Manager
description: Lär dig grunderna för Microsoft Endpoint Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 78b9175c10d4389623bfa08ac7895df200944a13
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722734"
---
# <a name="what-is-configuration-manager"></a>Vad är Configuration Manager?

*Gäller för: Configuration Manager (aktuell gren)*

Från Configuration Manager och med version 1910 är nu en del av Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager är en integrerad lösning för att hantera alla dina enheter. Microsoft sammanför Configuration Manager och Intune, utan en komplex migrering och med förenklad licensiering. Fortsätt att använda dina befintliga Configuration Manager-investeringar och dra nytta av kraften i Microsoft Cloud i din egen takt.

Följande Microsoft-hanterings lösningar är nu en del av **Microsoft Endpoint Manager** -varumärket:

- [Konfigurationshanteraren](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Andra funktioner i [administrations konsolen för enhets hantering](https://go.microsoft.com/fwlink/?linkid=2109094)

Mer information finns i [vanliga frågor och svar om Microsoft Endpoint Configuration Manager](microsoft-endpoint-manager-faq.md).

## <a name="introduction"></a>Introduktion

Använd Configuration Manager för att hjälpa dig med följande system hanterings aktiviteter:

- Öka produktiviteten och effektiviteten genom att minska manuella uppgifter och fokusera på projekt med höga värden.  
- Maximera maskin-och program varu investeringar.  
- Ge användar produktivitet genom att tillhandahålla rätt program vara vid rätt tidpunkt.  

Configuration Manager hjälper dig att leverera mer effektiva IT-tjänster genom att aktivera:

- Säker och skalbar distribution av program, program uppdateringar och operativ system.
- Real tids åtgärder på hanterade enheter.
- Molnbaserad analys och hantering för lokala och Internetbaserade enheter.
- Hantering av kompatibilitetsinställningar.  
- Omfattande hantering av servrar, Station ära datorer och bärbara datorer.

Configuration Manager utökar och fungerar tillsammans med många tekniker och lösningar från Microsoft. Configuration Manager kan till exempel integreras med:  

- Microsoft Intune att samhantera en mängd olika plattformar för mobila enheter
- Microsoft Azure att vara värd för moln tjänster för att utöka dina hanterings tjänster
- Windows Server Update Services (WSUS) för att hantera programuppdateringar
- Certificate Services
- Exchange Server och Exchange Online
- Grupprincip
- DNS
- Windows Automated Deployment Kit (Windows ADK) och User State Migration Tool (USMT)
- WDS (Windows Deployment Services)
- Fjärrskrivbord och fjärrhjälp

Configuration Manager använder också:  

- Active Directory Domain Services och Azure Active Directory för säkerhet, tjänst plats, konfiguration och för att identifiera de användare och enheter som du vill hantera.  
- Microsoft SQL Server som en distribuerad ändrings hanterings databas – och integreras med SQL Server Reporting Services (SSRS) för att skapa rapporter för övervakning och spårning av hanterings aktiviteter.  
- Plats system roller som utökar hanterings funktionerna och använder webb tjänster för Internet Information Services (IIS).
- Leverans optimering, Windows låg extra fördröjning Background transport (LEDBAT), Background Intelligent Transfer Service (BITS), BranchCache och annan peer caching-teknik som hjälper dig att hantera innehåll i nätverk och mellan enheter.

För att lyckas med Configuration Manager i en produktions miljö bör du planera och testa hanterings funktionerna noggrant. Configuration Manager är ett kraftfullt hanterings program, med möjlighet att påverka alla datorer i din organisation. När du distribuerar och hanterar Configuration Manager med noggrann planering och överväganden av dina affärs behov kan Configuration Manager minska din administrativa kostnad och den totala ägande kostnaden.  

## <a name="user-interfaces"></a>Användar gränssnitt

### <a name="the-configuration-manager-console"></a><a name="BKMK_Console"></a>Configuration Manager-konsolen

När du har installerat Configuration Manager använder du Configuration Manager-konsolen för att konfigurera platser och klienter och för att köra och övervaka hanterings uppgifter. Den här konsolen är den viktigaste administrations punkten och låter dig hantera flera platser.  

Du kan installera Configuration Manager-konsolen på ytterligare datorer och begränsa åtkomsten och begränsa vilka administrativa användare som kan visas i-konsolen med hjälp av Configuration Manager rollbaserad administration.  

Mer information finns i [använda Configuration Manager-konsolen](../servers/manage/admin-console.md).

### <a name="software-center"></a><a name="BKMK_ApplicationCatalog"></a>Software Center

**Software Center** är ett program som installeras när du installerar Configuration Manager-klienten på en Windows-enhet. Användare använder Software Center för att begära och installera program vara som du distribuerar. I Software Center kan användarna utföra följande åtgärder:  

- Bläddra efter och installera program, program uppdateringar och nya OS-versioner
- Visa sin historik för program varu begäran
- Visa enhetens efterlevnad mot organisationens principer

Du kan också visa anpassade flikar i Software Center för att möta ytterligare affärs behov.

Mer information finns i [användar handboken för Software Center](software-center.md).

## <a name="next-steps"></a>Nästa steg

Innan du installerar Configuration Manager bör du bekanta dig med grundläggande begrepp och villkor:

- Om du är bekant med System Center 2012 Configuration Manager, se [vad som har ändrats från system center 2012 Configuration Manager](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md).

- En teknisk översikt över Configuration Manager på hög nivå finns i [grunderna i Configuration Manager](fundamentals.md).

När du är bekant med de grundläggande begreppen kan du använda det här dokumentations biblioteket för att distribuera och använda Configuration Manager. Börja med följande artiklar:

- [Funktioner och funktioner i Configuration Manager](../plan-design/changes/features-and-capabilities.md)  
- [Välja en lösning för enhetshantering](../plan-design/choose-a-device-management-solution.md)  
- [Utvärdera Configuration Manager genom att skapa en egen labb miljö](../get-started/set-up-your-lab.md)
- [Få hjälp med att använda Configuration Manager](find-help.md)  
