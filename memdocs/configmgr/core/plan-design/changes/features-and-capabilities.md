---
title: Funktioner
titleSuffix: Configuration Manager
description: Lär dig mer om de primära hanterings funktionerna i Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5cdd0a9497f07d80813aca5dc169c4d61944e85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722377"
---
# <a name="features-and-capabilities-of-configuration-manager"></a>Funktioner och funktioner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln sammanfattas de primära hanterings funktionerna i Configuration Manager. Varje funktion har sina egna krav och hur du använder dem kan påverka utformningen och implementeringen av din Configuration Manager-hierarki. Om du till exempel vill distribuera program uppdateringar till enheter i din hierarki behöver du en plats system roll för program uppdaterings plats.  

Mer information om hur du planerar och installerar Configuration Manager för att stödja dessa hanterings funktioner i din miljö finns i [bli redo för Configuration Manager](../get-ready.md).  

## <a name="co-management"></a>Samhantering

Samhantering är ett av de främsta sätten att koppla din befintliga Configuration Manager-distribution till Microsoft 365 molnet. Det gör att du kan hantera Windows 10-enheter samtidigt genom att använda både Configuration Manager och Microsoft Intune. Med samhantering kan du molnbaserad din befintliga investering i Configuration Manager genom att lägga till nya funktioner som villkorlig åtkomst. Mer information finns i [Vad är co-Management](../../../comanage/overview.md)?

## <a name="desktop-analytics"></a>Desktop Analytics

Desktop Analytics är en molnbaserad tjänst som kan integreras med Configuration Manager. Tjänsten ger insikt och information för att fatta mer välgrundade beslut om uppdaterings beredskap för dina Windows-klienter. Den kombinerar data från din organisation med data som sammanställs från miljon tals enheter som är anslutna till Microsofts moln tjänster. Mer information finns i [Vad är Desktop Analytics](../../../desktop-analytics/overview.md)?

## <a name="cloud-attached-management"></a>Molnansluten hantering

Använd funktioner som gateway för molnhantering, molnbaserade distributionsplatser och Azure Active Directory för att hantera Internetbaserade klienter.

Mer information finns i följande artiklar:

- [Hantera klienter på Internet](../../clients/manage/manage-clients-internet.md)
- [Prenumerationsavtal för Azure AD](../security/plan-for-security.md#bkmk_planazuread)
- [Azure-tjänster](../../servers/deploy/configure/azure-services-wizard.md)

## <a name="real-time-management"></a>Realtidshantering

Använd CMPivot för att omedelbart fråga online-enheter och filtrera sedan och gruppera data efter djupare insikter. Använd också Configuration Manager-konsolen för att hantera och distribuera Windows PowerShell-skript till klienter. Mer information finns i [CMPivot](../../servers/manage/cmpivot.md) och [skapa och köra PowerShell-skript](../../../apps/deploy-use/create-deploy-scripts.md).

## <a name="application-management"></a>Programhantering

Hjälper dig att skapa, hantera, distribuera och övervaka program på en rad olika enheter som du hanterar. Distribuera, uppdatera och hantera Office 365 från Configuration Manager-konsolen. Dessutom kan Configuration Manager integreras med Microsoft Store för företag och utbildning för att leverera molnbaserade appar. Mer information finns i [Introduktion till program hantering](../../../apps/understand/introduction-to-application-management.md).

## <a name="os-deployment"></a>Distribution av operativsystem

Distribuera en uppgradering på plats av Windows 10 eller avbilda och distribuera OS-avbildningar. Distribution av avbildningar kan använda PXE, multicast eller startbara media. Det kan också hjälpa att distribuera om befintliga enheter med Windows autopilot. Mer information finns i [Introduktion till OS-distribution](../../../osd/understand/introduction-to-operating-system-deployment.md).  

## <a name="software-updates"></a>Programuppdateringar

Hantera, distribuera och övervaka program uppdateringar i organisationen. Integrera med Windows-leverans optimering och annan peer caching-teknik som hjälper dig att kontrol lera nätverks användningen. Mer information finns i [Introduktion till program uppdateringar](../../../sum/understand/software-updates-introduction.md).  

## <a name="company-resource-access"></a>Åtkomst till företagsresurser

Gör att du kan ge användare i organisationen åtkomst till data och program från fjärranslutna platser. Den här funktionen inkluderar Wi-Fi-, VPN-, e-post-och certifikat profiler. Mer information finns i [skydda data och plats infrastruktur](../../../protect/understand/protect-data-and-site-infrastructure.md).

## <a name="compliance-settings"></a>Kompatibilitetsinställningar

Hjälper dig att utvärdera, spåra och åtgärda konfigurationens kompatibilitet för klient enheter i organisationen. Dessutom kan du använda kompatibilitetsinställningar för att konfigurera en mängd funktioner och säkerhets inställningar på enheter som du hanterar. Mer information finns i [Se till att enheten uppfyller kraven](../../../compliance/understand/ensure-device-compliance.md).  

## <a name="endpoint-protection"></a>Slutpunktsskydd

Tillhandahåller säkerhet, program mot skadlig kod och hantering av Windows-brandväggen för datorer i din organisation. Det här avsnittet omfattar hantering och integrering med följande Windows Defender Suite-funktioner:

- Windows Defender Antivirus
- Microsoft Defender Advanced Threat Protection
- Windows Defender Exploit Guard
- Windows Defender Application Guard
- Windows Defender Application Control
- Windows Defender-brandvägg

Mer information finns i [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

## <a name="inventory"></a>Inventering

Hjälper dig att identifiera och övervaka till gångar.

### <a name="hardware-inventory"></a>Maskinvaruinventering

Samlar in detaljerad information om maskin varan för enheter i din organisation. Mer information finns i [Introduktion till maskin varu inventering](../../clients/manage/inventory/introduction-to-hardware-inventory.md).  

### <a name="software-inventory"></a>Programvaruinventering

Samlar in och rapporterar information om de filer som lagras på klient datorer i din organisation. Mer information finns i [Introduktion till program varu inventering](../../clients/manage/inventory/introduction-to-software-inventory.md).  

### <a name="asset-intelligence"></a>Tillgångsinformation

Innehåller verktyg för att samla in inventerings data och övervaka program licens användningen i din organisation. Mer information finns i [Introduktion till tillgångsinformation](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

## <a name="on-premises-mobile-device-management"></a>Lokal hantering av mobila enheter

Registrerar och hanterar enheter med hjälp av den lokala Configuration Manager infrastrukturen med de hanterings funktioner som är inbyggda i enhetens plattformar. (Typisk hantering använder en separat installerad Configuration Manager-klient.) Den här funktionen stöder för närvarande hantering av Windows 10 Enterprise-och Windows 10 Mobile-enheter. Mer information finns i [Hantera mobila enheter med lokal infrastruktur](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="power-management"></a>Energisparfunktioner

Hantera och övervaka strömförbrukningen för klient datorer i organisationen. Konfigurera energi scheman och Använd Wake-on-LAN för att utföra underhåll utanför kontors tid. Mer information finns i [Introduktion till energispar funktioner](../../clients/manage/power/introduction-to-power-management.md).  

## <a name="remote-control"></a>Fjärrstyrning

Innehåller verktyg för att fjärradministrera klient datorer från Configuration Manager-konsolen. Mer information finns i [Introduktion till fjärr styrning](../../clients/manage/remote-control/introduction-to-remote-control.md).  

## <a name="reporting"></a>Rapportering

Använd de avancerade rapporterings funktionerna i SQL Server Reporting Services från Configuration Manager-konsolen. Den här funktionen ger hundratals standard rapporter. Mer information finns i [Introduktion till rapportering](../../servers/manage/introduction-to-reporting.md).  

## <a name="software-metering"></a>Avläsning av programvara

Övervaka och samla in program varu användnings data från Configuration Manager-klienter. Du kan använda dessa data för att avgöra om program varan används efter att den installerats. Mer information finns i [övervaka app-användning med avläsning av program vara](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  
