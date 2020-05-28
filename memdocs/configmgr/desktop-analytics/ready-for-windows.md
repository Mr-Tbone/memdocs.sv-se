---
title: Redo för Windows
titleSuffix: Configuration Manager
description: Om indragningen av webbplatsen för redo för Windows
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ROBOTS: NOINDEX
ms.openlocfilehash: 75dd74e3c1019c9819b44a0ffa8936eeb9eee366
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268359"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Klar för vanliga frågor och svar om moderna skriv bord

<!-- placeholder -->

## <a name="general"></a>Allmänt

### <a name="what-happened-to-the-ready-for-windows-website"></a>Vad hände med webbplatsen för redo för Windows?

Många kunder har utmaningar med att hämta och hålla dig uppdaterad med Windows 10 och Office 365 ProPlus. Den primära utmaningen är att testa program, eftersom den här processen vanligt vis är manuell. Det är tids krävande för IT-administratörer och program ägare att kontinuerligt analysera befintliga program och sedan åtgärda eventuella problem som uppstår.

Det *färdiga för modern Skriv bords* katalog som listas program varu lösningar som stöds och används på kommersiella enheter som kör Windows 10 och Office 365 ProPlus. Katalogen hjälper IT-chefer som överväger de senaste versionerna av Windows 10 och Office 365 för sina distributioner.

Feedback från IT-chefer är att de vill att dessa insikter integreras med de verktyg som redan används för att planera sina distributions planer. Använd funktionerna [Desktop Analytics](https://aka.ms/dadocs) och [Office 365 ProPlus readiness](https://docs.microsoft.com/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch) i Configuration Manager för att planera och hantera dina Windows 10-och Office 365 ProPlus-uppgraderings projekt. 

> [!Note]
> Från och med den 21 april 2020 kommer Office 365 ProPlus att byta namn till **Microsoft 365 appar för företag**. Mer information finns i [namn ändring för Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Du kan fortfarande se referenser till det gamla namnet i Configuration Manager-konsolen och stöd dokumentationen medan-konsolen uppdateras.

### <a name="what-is-desktop-analytics"></a>Vad är Desktop Analytics?

[Desktop Analytics](https://aka.ms/dadocs) är en molnbaserad tjänst som kan integreras med Configuration Manager. Tjänsten ger insikt och information för att fatta mer välgrundade beslut om uppdaterings beredskap för dina Windows-slutpunkter. Den kombinerar den information som är speciell för din organisation med sammanställda insikter från miljon tals Windows-enheter som är anslutna till Microsofts moln tjänster.

-    Få en heltäckande vy över slut punkter, program och driv rutiner som hanteras i din organisation.

-    Utvärdera kompatibilitet för program och driv rutiner med de senaste Windows-funktionerna. Få rekommendationer om åtgärder för kända problem, samt avancerade insikter för branschspecifika appar.

-    Använd artificiell intelligens (AI) från Microsoft-molnet för att optimera den uppsättning pilot enheter som återger din övergripande miljö.

### <a name="why-should-i-use-desktop-analytics-for-my-windows-deployment-plans"></a>Varför ska jag använda Desktop Analytics för mina Windows-distributions planer?

Desktop Analytics ger följande fördelar:

-    **Enhets-och program varu inventering**: inventering av viktiga faktorer, till exempel appar och versioner av Windows.

-    **Pilot identifiering**: identifiering av den minsta uppsättningen enheter som ger flest täckning av faktorer. Den fokuserar på de faktorer som är viktigast för en pilot med Windows-uppgraderingar och uppdateringar. Att se till att piloten är mer framgångs rik gör att du snabbt och säkert kan fortsätta med breda distributioner i produktionen.

-    **Problem identifiering**: med hjälp av sammanställd marknads information tillsammans med data från din miljö förutsäger tjänsten potentiella problem som kan uppstå och bli aktuella med Windows. Därefter föreslås eventuella begränsningar.

-    **Configuration Manager-integrering**: IT-moln – möjliggör din befintliga lokala infrastruktur. Använd dessa data och analyser för att distribuera och hantera Windows på dina enheter.

### <a name="what-does-the-ready-for-windows-status-mean-in-desktop-analytics"></a>Vad är *redo för Windows* -status i Skriv bords analys?

**Tillämpnings status** baseras på information från kommersiella enheter som delar data med Microsoft. Statusen är integrerad med support satser från program varu leverantörer.

Skriv bords analys ger tillämpnings status för varje version av en till gång som finns på kommersiella enheter. Den här statusen omfattar inte data från konsument enheter eller enheter som inte delar data. Statusen är kanske inte representativ för införande frekvensen på alla Windows 10-enheter.

Mer information finns i [kompatibilitetskontroll](compat-assessment.md).

### <a name="what-assets-get-the-ready-for-windows-status-in-desktop-analytics"></a>Vilka till gångar får statusen *redo för Windows* i Desktop Analytics? 

Till gångar har statusen *redo för Windows* i Desktop Analytics om:

-    Program varu leverantören deklarerar support för lösningen.
-    Kunder har distribuerat den på ett stort antal kommersiella Windows 10-enheter som delar information med Microsoft.
-    Till gången är relevant för kommersiella användare.

### <a name="what-additional-insights-do-i-get-in-desktop-analytics"></a>Vilka ytterligare insikter får jag i Skriv bords analys?

Desktop Analytics tillhandahåller en inventering av [enheterna och deras installerade appar](about-assets.md), samt [avancerade insikter](compat-assessment.md#advanced-insights) för branschspecifika appar. 

## <a name="software-providers"></a>Program varu leverantörer

### <a name="can-i-still-list-my-software-solution-in-desktop-analytics"></a>Kan jag fortfarande visa en program varu lösning i Desktop Analytics?

Publicera en support instruktion som produkten fungerar med 32-bitars eller 64-bitars Windows 10 eller Office 365 ProPlus. Prata med din Microsoft-kontakt för att demonstrera dina lösningar i Desktop Analytics.

### <a name="how-can-listing-my-solutions-benefit-me"></a>Hur kan jag få en lista över mina lösningar?

Tusentals IT-administratörer hanterar miljon tals enheter med Configuration Manager-och skriv bords analys. De använder dessa verktyg för att på ett säkert sätt planera och uppgradera sina organisationer till den senaste versionen av Windows 10 och Office 365 ProPlus. De kan också använda dem för att fatta köp beslut för program varu lösningar.

Microsoft integrerar support satser från program varu leverantörer med den information som de får från kommersiella enheter. Organisationer runtom i världen och sedan använda dessa data i verktyg för Skriv bords analys och Office-beredskap. 

Kontakta din Microsoft-kontakt om dina support rapporter inte är korrekt kopplade till till gångar.

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>Kan jag se detaljerade prestanda mått för mina till gångar?

Utvärdera prestanda för dina lösningar med hälso-och mått rapporter via Developer Center: 

- [Windows Store](https://docs.microsoft.com/windows/uwp/publish/health-report)
- [Skrivbord](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)
- [Office Add-ins](https://docs.microsoft.com/office/dev/store/update-unpublish-and-view-metrics) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-office-365-proplus"></a>Hur kan jag utveckla kompatibla till gångar för Windows 10 och Office 365 ProPlus?

Kontrol lera att dina Skriv bords program är kompatibla nu och håll dem kompatibla med Windows 10 i framtiden. Mer information finns i [programkompatibilitet för utvecklare](https://developer.microsoft.com/windows/desktop/app-compatibility).

Om du utvecklar lösningar för Office 365 ProPlus, se [metod tips för utveckling för com, VSTO och VBA-tillägg i Office](https://docs.microsoft.com/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office).
