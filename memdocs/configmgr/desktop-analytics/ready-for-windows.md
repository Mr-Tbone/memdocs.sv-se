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
ms.openlocfilehash: 2d431f744ab09aeb938a7961ebf713f71c0f8015
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193690"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Klar för vanliga frågor och svar om moderna skriv bord

<!-- placeholder -->

## <a name="ready-for-windows-adoption-status"></a>Redo för Windows tillämpnings status

Tillämpnings status baseras på information från kommersiella enheter som delar data med Microsoft. Statusen är integrerad med support satser från program varu leverantörer.

Skriv bords analys ger tillämpnings status för varje version av en till gång som finns på kommersiella enheter. Den här statusen omfattar inte data från konsument enheter eller enheter som inte delar data. Statusen är kanske inte representativ för införande frekvensen på alla Windows 10-enheter.

Möjliga kategorier är:

- **Starkt infört**: minst 100 000 kommersiella Windows 10-enheter har installerat den här appen.

- **Antog**: minst 10 000 kommersiella Windows 10-enheter har installerat den här appen.

- **Otillräckliga data**: det finns för få kommersiella Windows 10-enheter som delar information för den här appen för Microsoft att kategorisera dess införande.

- **Kontakta utvecklaren**: det kan finnas kompatibilitetsproblem med den här versionen av appen. Microsoft rekommenderar att du kontaktar program leverantören och lär dig mer.

- **Okänd**: det finns ingen tillgänglig information för den här versionen av programmet. Information kan vara tillgänglig för andra versioner av programmet.

## <a name="general"></a>Allmänt

### <a name="what-happened-to-the-ready-for-windows-website"></a>Vad hände med webbplatsen för redo för Windows?

Många kunder har utmaningar med att hämta och hålla dig uppdaterad med Windows 10 och Microsoft 365 appar för företag. Den primära utmaningen är att testa program, eftersom den här processen vanligt vis är manuell. Det är tids krävande för IT-administratörer och program ägare att kontinuerligt analysera befintliga program och sedan åtgärda eventuella problem som uppstår.

Det *färdiga för modern Skriv bords* katalog som listas program varu lösningar som stöds och används på kommersiella enheter som kör Windows 10 och Microsoft 365 appar för företag. Katalogen hjälper IT-chefer som överväger de senaste versionerna av Windows 10 och Microsoft 365 för deras distributioner.

Feedback från IT-chefer är att de vill att dessa insikter integreras med de verktyg som redan används för att planera sina distributions planer. Använd funktionerna för [stationär analys](https://aka.ms/dadocs) och [Microsoft 365 Apps-beredskap](/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch) i Configuration Manager för att planera och hantera dina Windows 10-och Microsoft 365-appar för Enterprise Upgrade-projekt. 

> [!Note]
> Från och med den 21 april 2020 kommer Office 365 ProPlus att byta namn till **Microsoft 365 appar för företag**. Mer information finns i [namn ändring för Office 365 ProPlus](/deployoffice/name-change). Du kan fortfarande se referenser till det gamla namnet i Configuration Manager-konsolen och stöd dokumentationen medan-konsolen uppdateras.

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

Publicera en support instruktion som produkten fungerar med 32-bitars eller 64-bitars Windows 10-eller Microsoft 365-appar för företag. Prata med din Microsoft-kontakt för att demonstrera dina lösningar i Desktop Analytics.

### <a name="how-can-listing-my-solutions-benefit-me"></a>Hur kan jag få en lista över mina lösningar?

Tusentals IT-administratörer hanterar miljon tals enheter med Configuration Manager-och skriv bords analys. De använder dessa verktyg för att på ett säkert sätt planera och uppgradera sina organisationer till den senaste versionen av Windows 10 och Microsoft 365 appar för företag. De kan också använda dem för att fatta köp beslut för program varu lösningar.

Microsoft integrerar support satser från program varu leverantörer med den information som de får från kommersiella enheter. Organisationer runtom i världen och sedan använda dessa data i verktyg för Skriv bords analys och Office-beredskap. 

Kontakta din Microsoft-kontakt om dina support rapporter inte är korrekt kopplade till till gångar.

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>Kan jag se detaljerade prestanda mått för mina till gångar?

Utvärdera prestanda för dina lösningar med hälso-och mått rapporter via Developer Center: 

- [Windows Store](/windows/uwp/publish/health-report)
- [Skrivbord](/windows/desktop/appxpkg/windows-desktop-application-program)
- [Office Add-ins](/office/dev/store/update-unpublish-and-view-metrics) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-microsoft-365-apps-for-enterprise"></a>Hur kan jag utveckla kompatibla till gångar för Windows 10 och Microsoft 365 appar för företag?

Kontrol lera att dina Skriv bords program är kompatibla nu och håll dem kompatibla med Windows 10 i framtiden. Mer information finns i [programkompatibilitet för utvecklare](https://developer.microsoft.com/windows/desktop/app-compatibility).

Om du utvecklar lösningar för Microsoft 365 appar för företag, se [metod tips för utveckling för com, VSTO och VBA-tillägg i Office](/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office).