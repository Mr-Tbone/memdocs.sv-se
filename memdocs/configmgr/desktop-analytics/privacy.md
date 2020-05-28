---
title: Data sekretess för Skriv bords analys
titleSuffix: Configuration Manager
description: Skriv bords analys allokeras till kund information
ms.date: 12/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: dd970dc1517a6fcc197b2bf39a141871b4999a02
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268427"
---
# <a name="desktop-analytics-data-privacy"></a>Data sekretess för Skriv bords analys

Skriv bords analys allokeras fullständigt till kundens data sekretess, centrerat på dessa Tenets:

- **Transparens:** Vi har fullständigt dokumenterat Windows Diagnostic-händelser. Granska dem med ditt företags team för säkerhet och efterlevnad. I visnings programmet för Windows-diagnostikdata kan du se diagnostikdata som skickas från en specifik enhet. Mer information finns i [Översikt över Diagnostic data Viewer](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Kontroll:** Du styr vilken nivå av diagnostikdata som ska delas med Microsoft. Windows 10, version 1709, lägger till en ny princip för att begränsa utökade diagnostikdata till minimi kravet för Skriv bords analys.  

- **Säkerhet:** Microsoft skyddar dina data med stark säkerhet och kryptering.  

- **Förtroende:** Desktop Analytics stöder Microsofts [sekretess policy](https://privacy.microsoft.com/privacystatement) och [online service villkoren](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  

Mer information finns i [Windows-tjänster där Microsoft är processorn under GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance#windows-services-where-microsoft-is-the-processor-under-the-gdpr).<!-- 5353168 -->

## <a name="data-flow"></a>Dataflöde

Följande bild visar hur diagnostikdata flödar från enskilda enheter via Diagnostic data service, tillfällig lagring och till din Log Analytics arbets yta:

![Diagram som illustrerar flödet av diagnostikdata från enheter](media/da-data-flow.png)

1. Du loggar in på Azure Portal och registrerar dig för Skriv bords analys. Du skapar Azure AD-appen för att ansluta till Configuration Manager. När du konfigurerar Desktop Analytics skapar du en Azure Log Analytics-arbetsyta på valfri plats.  

2. Du ansluter Configuration Manager och registrerar enheter  

    1. Du konfigurerar moln tjänsten för Skriv bords analys i Configuration Manager med information om Azure AD-appen.  

    2. Inom 15 minuter synkroniserar Configuration Manager följande data med Desktop Analytics med klient-ID: t. Den här processen upprepas varje timme.

      - Information om enhets samlingar som behövs för att [skapa distributions planer](create-deployment-plans.md). Den här informationen omfattar samlings-ID, hierarki-ID, samlings namn och antal enheter. 
      - Information som krävs för att [registrera enheter](enroll-devices.md). Den här informationen omfattar samlings-ID, SMS-unik identifierare, OS-Build-version, enhets namn och serie nummer.
      - Information från instrument panelen för [övervakning av anslutnings hälsa](monitor-connection-health.md) . Den här informationen omfattar antalet enheter per hälso tillstånd och enhets egenskaper.
      - Information om distributions planer, som innehåller samlings-ID, distributions-ID, pilot-eller produktions distributions typ och antalet enheter per uppgraderings beslut.

    3. Configuration Manager anger affärs-ID, diagnostikinformation och andra inställningar för enheterna i mål samlingen. Den här konfigurationen anger vilka enheter som ska visas i arbets ytan för Station ära analyser.  

    4. Du distribuerar kompatibilitetsinställningar till alla mål enheter.  

3. Enheter skickar diagnostikdata till Microsoft Diagnostic Datahantering-tjänsten för Windows. Den här tjänsten finns i USA.  

4. Varje dag skapar Microsoft en ögonblicks bild av IT-fokuserade insikter. Den här ögonblicks bilden kombinerar diagnostikdata från Windows med dina indata för registrerade enheter. Den här processen sker i ett tillfälligt lagrings utrymme som bara används av Desktop Analytics. Den tillfälliga lagrings platsen finns i Microsoft Data Center i USA. Alla data skickas via en krypterad SSL-kanal (HTTPS). Ögonblicks bilderna åtskiljs av ett kommersiellt ID.  

5. Ögonblicks bilderna kopieras sedan till din Azure Log Analytics-arbetsyta. Den här data överföringen sker över HTTPS via webhook-inmatnings protokollet, som är en funktion i Log Analytics. Skriv bords analys har inte Läs-eller Skriv behörighet till din Log Analytics-lagring. Skriv bords analys anropar webhook-API: et med en SAS-URI (signatur för delad åtkomst). Log Analytics hämtar sedan data från lagrings tabellerna via HTTPS.

6. Skriv bords analys lagrar dina indata i Log Analytics Storage. Dessa konfigurationer omfattar distributions planer och till gångs beslut för uppgradering och prioritet.  

## <a name="other-resources"></a>Andra resurser

Vanliga frågor och svar om vanliga frågor och svar om Desktop Analytics finns i [vanliga frågor och svar om sekretess](faq.md#privacy).

Mer information om relaterade sekretess aspekter finns i följande artiklar:

- [Windows 10 och GDPR för IT-besluts fattare](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Konfigurera Windows-diagnostikdata i din organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Windows 7, Windows 8 och Windows 8,1-bedömning av diagnostikdata för data och fält](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10, version 1809 Basic Level Windows diagnostiska händelser och fält](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Windows 10, version 1709 Enhanced Diagnostic data events och fält som används av Desktop Analytics](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Översikt över granskning av diagnostikdata](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Licens villkor och dokumentation](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Log Analytics data säkerhet](https://docs.microsoft.com/azure/azure-monitor/platform/data-security)

- [Säkerhet och sekretess på Microsoft Azure Data Center](https://azure.microsoft.com/global-infrastructure/)  

- [Förtroende i det betrodda molnet](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Säkerhetscenter](https://www.microsoft.com/trustcenter)  

- [Sekretess sköld](https://www.privacyshield.gov/)  

Configuration Manager skickar diagnostik-och användnings data till Microsoft separat från Desktop Analytics. Microsoft använder dessa data för att förbättra installations upplevelsen, kvaliteten och säkerheten i framtida versioner av Configuration Manager. Mer information finns i [diagnostik-och användnings data för Configuration Manager](../core/plan-design/diagnostics/diagnostics-and-usage-data.md).
