---
title: Introduktion till rapportering
titleSuffix: Configuration Manager
description: Lär dig mer om en uppsättning av verktyg och resurser som du kan använda för att hantera rapportering i Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1aae76845d18d8191b6f773df5491d3a144940c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713809"
---
# <a name="introduction-to-reporting-in-configuration-manager"></a>Introduktion till rapportering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Rapportering i Configuration Manager innehåller en uppsättning verktyg och resurser som hjälper dig att använda de avancerade rapporterings funktionerna i SQL Server Reporting Services (SSRS) och Power BI-rapportserver. Båda plattformarna för rapportering innehåller omfattande redigerings upplevelser för anpassade rapporter. Med hjälp av rapportering kan du samla in, organisera och presentera information om de stora mängderna av Configuration Manager data i din organisation. Configuration Manager innehåller många fördefinierade rapporter i repor ting Services som du kan använda utan ändringar. Du kan duplicera och ändra standard rapporterna så att de uppfyller dina krav, eller så kan du skapa anpassade rapporter.

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services tillhandahåller en mängd färdiga verktyg och tjänster som hjälper dig att skapa, distribuera och hantera rapporter för din organisation. Den innehåller också programmerings funktioner som gör att du kan utöka och anpassa dina rapporterings funktioner. Repor ting Services är en serverbaserad rapport plattform som tillhandahåller omfattande rapporterings funktioner för olika typer av data källor.

Configuration Manager använder SQL Server Reporting Services som primär rapporterings lösning. Integreringen med Reporting Services ger följande fördelar:  

- Använder ett rapporterings system enligt bransch standard för att fråga Configuration Manager databasen.  

- Visar rapporter med hjälp av Configuration Manager rapport visnings programmet eller genom att använda Rapporthanteraren, som är en webbaserad anslutning till rapporten.  

- Ger höga prestanda, tillgänglighet och skalbarhet.  

- Innehåller prenumerationer på rapporter som användare kan prenumerera på. En chef prenumererar exempelvis på en e-postrapport varje dag som innehåller information om statusen för en program uppdaterings distribution.

- Exportera rapporter i olika typer av populära format.  

Mer information finns i [Vad är SQL Server Reporting Services (SSRS)?](https://docs.microsoft.com/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports?view=sql-server-ver15)

## <a name="power-bi-report-server"></a>Power BI-rapportserver

<!-- 3721603 -->

Från och med version 2002, integrera Power BI-rapportserver med Configuration Manager repor ting. Den här integrationen ger modern visualisering och bättre prestanda. Det lägger till konsol stöd för Power BI rapporter på liknande sätt som redan finns med SQL Server Reporting Services. Mer information finns i [integrera med Power BI-rapportserver](powerbi-report-server.md).

Power BI-rapportserver är en lokal rapport server med en webb portal där du kan visa och hantera rapporter. Den innehåller verktyg för att skapa Power BI rapporter, sid brytnings rapporter, mobila rapporter och KPI: er. Mer information finns i [Vad är Power BI-rapportserver?](https://docs.microsoft.com/power-bi/report-server/get-started).

## <a name="reporting-services-point"></a>Rapporteringstjänstpunkt

Repor ting Services-platsen är en plats system roll som du lägger till på en server som kör Microsoft SQL Server Reporting Services. Repor ting Services-platsen har följande funktioner:

- Kopierar Configuration Manager rapport definitioner till repor ting Services
- Skapar rapportmallar baserat på rapport kategorier
- Anger säkerhets princip för rapportens mappar och rapporter. Dessa principer baseras på rollbaserade behörigheter för Configuration Manager administrativa användare. I ett 10-minuters intervall ansluter repor ting Services-platsen till repor ting Services för att tillämpa säkerhets principen igen om du har ändrat den.

Mer information om hur du planerar för och installerar en repor ting Services-plats finns i följande artiklar:

- [Planera för rapportering](planning-for-reporting.md)

- [Konfigurera rapporter](configuring-reporting.md)

## <a name="configuration-manager-reports"></a>Configuration Manager-rapporter

Configuration Manager innehåller rapport definitioner för över 400 rapporter i över 50 rapport-mappar. Under installationen av repor ting Services-platsen kopieras de till rot rapportens mapp i SQL Server Reporting Services. Configuration Manager-konsolen visar rapporterna och ordnar dem i undermappar baserat på rapport kategorin.

Rapporter sprider inte upp eller ned Configuration Manager hierarkin. De körs bara mot databasen för den webbplats där du skapar dem. Eftersom Configuration Manager replikerar globala data i hela hierarkin, har du till gång till information om hela hierarkin i rapporter. När en rapport hämtar data från en platsdatabas har den åtkomst till platsinformationen för den aktuella platsen och underordnade platser och globala data för alla platser i hierarkin.

Precis som andra Configuration Manager objekt måste en administrativ användare ha rätt behörighet för att köra eller ändra rapporter. För att kunna köra en rapport måste en administrativ användare ha behörigheten **Kör rapport** för objektet. För att kunna skapa eller ändra en rapport måste en administrativ användare ha behörigheten **Ändra rapport** för objektet.

### <a name="create-and-modify-reports"></a>Skapa och ändra rapporter

För repor ting Services-baserade rapporter använder Configuration Manager Microsoft SQL Server Report Builder som exklusivt redigerings-och redigerings verktyg för modellbaserade och SQL-baserade rapporter. När du skapar eller redigerar en rapport i Configuration Manager-konsolen öppnas Report Builder. Mer information finns i [åtgärder och underhåll för rapportering](operations-and-maintenance-for-reporting.md).

Från och med version 2002, för att skapa eller redigera Power BI rapporter, integreras-konsolen med Power BI Desktop. Mer information finns i [skapa Power BI rapporter](powerbi-report-server.md#create-power-bi-reports).

### <a name="run-reports"></a>Köra rapporter

När du kör en repor ting Services-baserad rapport i Configuration Manager-konsolen öppnas Report Viewer och ansluter till repor ting Services. När du har angett eventuella nödvändiga parametrar hämtar Reporting Services data och visar informationen i visningsprogrammet. Du kan också ansluta till SQL Services Reporting Services, ansluta till platsens datakälla och köra rapporterna.

Från och med version 2002 öppnas den i webbläsaren när du kör en Power BI-baserad rapport.

### <a name="report-prompts"></a>Rapportprompter

Du kan konfigurera en rapport prompt eller parameter när du skapar eller ändrar en rapport. Skapa rapport-prompter för att begränsa eller rikta in data som en rapport hämtar. En rapport kan innehålla fler än en prompt. Kontrol lera att prompternas namn är unika och bara innehåller alfanumeriska tecken som stämmer överens med SQL Server reglerna för identifierare.

När du kör en rapport begär prompten ett värde för en obligatorisk parameter. Baserat på parametervärdet hämtas rapport data. Till exempel uppmanas **dator informationen för en speciell dator** att ange ett dator namn. Repor ting Services skickar det angivna värdet till en variabel som definierats i rapportens SQL-instruktion.

### <a name="report-links"></a>Rapportlänkar

Rapport länkar i Configuration Manager används i en käll rapport för att ge enkel åtkomst till ytterligare data. Den kan till exempel länka till mer detaljerad information om varje objekt i käll rapporten. Om målrapporten kräver att en eller flera prompter körs måste källrapporten innehålla en kolumn med lämpliga värden för varje prompt.

Länken måste ange kolumn numret med värdet för prompten. Ett exempel:

- Det finns en rapport som visar datorer som platsen nyligen har identifierat.
- Du länkar från den till en annan rapport som visar de senaste meddelanden som platsen tar emot för en speciell dator.
- Du skapar länken och anger att kolumnen `2` i käll rapporten innehåller dator namnet. Det här värdet är en obligatorisk prompt för mål rapporten.
- Du kör käll rapporten och en länk ikon visas till vänster om varje rad med data.
- Du väljer ikonen på en rad så skickas värdet i den angivna kolumnen för den raden som prompt-värde för mål rapporten i rapport visnings programmet.

Du kan bara konfigurera en länk för en rapport och den länken kan bara ansluta till en enda mål rapport.

> [!WARNING]  
> Om du flyttar en målrapport till en annan rapportmapp ändras platsen för målrapporten. Configuration Manager uppdaterar inte rapport länken automatiskt i käll rapporten med den nya platsen och länken fungerar inte i käll rapporten.

## <a name="report-folders"></a>Rapportmappar

Rapportmallar innehåller en metod för att sortera och filtrera rapporter som Configuration Manager butiker i repor ting Services. Rapportmallar är användbara när du har många rapporter att hantera. När du installerar en repor ting Services-plats kopieras rapporter till repor ting Services och organiseras i fler än 50 rapportmallar. Rapportmapparna är skrivskyddade. Du kan inte ändra dem i Configuration Manager-konsolen.

## <a name="report-subscriptions"></a>Rapportprenumerationer

En rapport prenumeration i repor ting Services är en återkommande begäran om att leverera en rapport vid en angiven tidpunkt eller som svar på en händelse. Du anger ett program fil format i prenumerationen. Prenumerationer är ett alternativ till att köra en rapport på begäran. När du använder rapporter på begäran måste du aktivt välja rapporten varje gång du vill visa den. Prenumerationer kan däremot användas för att schemalägga och sedan automatisera rapportleveransen.

Du kan hantera rapport prenumerationer i Configuration Manager-konsolen. Rapport servern bearbetar prenumerationerna. Den distribuerar dem med hjälp av leverans tillägg som distribueras på servern. Som standard kan du skapa prenumerationer som skickar rapporter till en delad mapp eller till en e-postadress.

Mer information finns i [Hantera rapport prenumerationer](operations-and-maintenance-for-reporting.md#bkmk_subscription).

## <a name="report-builder"></a>Report Builder

För repor ting Services-baserade rapporter använder Configuration Manager Microsoft SQL Server Report Builder som exklusivt redigerings-och redigerings verktyg för både modellbaserade och SQL-baserade rapporter. Om du skapar eller redigerar en rapport i Configuration Manager-konsolen öppnas Report Builder. När du skapar eller ändrar en rapport för första gången installeras Report Builder automatiskt. Den Report Builder-version som är kopplad till den installerade SQL Server-versionen öppnas när du kör eller redigerar rapporter.  

 Report Builder-installation tillför stöd för över 20 språk. När du kör Report Builder visas data på språket för den lokala datorns operativ system. Om Report Builder inte stöder språket visas informationen på engelska. Report Builder har stöd för alla funktioner i SQL Server Reporting Services som innehåller följande funktioner:

- Levererar en intuitiv rapportredigeringsmiljö som liknar Microsoft Office.  

- Erbjuder den flexibla rapportlayouten i SQL Server Report Definition Language (RDL).  

- Tillhandahåller olika former av datavirtualisering inklusive diagram och mätare.  

- Tillhandahåller formaterade textrutor.  

- Exporterar till Microsoft Word-format.  

Du kan också öppna Report Builder direkt från SQL Server Reporting Services.

## <a name="report-models-in-sql-server-reporting-services"></a>Rapportmodeller i SQL Server Reporting Services

SQL Reporting Services använder rapport modeller för att hjälpa dig att välja objekt från Configuration Manager-databasen som ska tas med i modellbaserade rapporter. När du skapar en rapport visar rapport modeller endast angivna vyer och objekt att välja bland. Minst en rapportmodell måste vara tillgänglig för att du ska kunna skapa modellbaserade rapporter.

Rapportmodeller har följande funktioner:

- Ge logiska företags namn till databas fält och vyer. Om du vill skapa rapporter behöver du inte känna till Configuration Manager databas strukturen.

- Gruppera objekt logiskt.  

- Definiera relationer mellan objekt.  

- Skydda modell element så att administrativa användare bara kan se de data som de har behörighet att se.

Även om Configuration Manager innehåller exempel rapport modeller, kan du också definiera rapport modeller som uppfyller dina egna affärs behov. Mer information om hur du skapar rapport modeller finns i [skapa anpassade rapport modeller](creating-custom-report-models-in-sql-server-reporting-services.md).

## <a name="next-steps"></a>Nästa steg

[Planera för rapportering](planning-for-reporting.md)
