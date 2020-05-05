---
title: Så här använder du dokumenten
titleSuffix: Configuration Manager
description: Lär dig mer om att använda Configuration Manager Technical Document Library.
ms.date: 04/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d694f9985e6d1e5118f2620e5cbd556de249788a
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771318"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>Använda Configuration Manager dokument

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller resurser och tips för att använda Configuration Manager-dokumentations biblioteket.

- Så här söker du
- Skicka in dokument buggar, förbättringar, frågor och nya idéer
- Så här får du ett meddelande om ändringar
- Så här bidrar du till dokument

Allmän hjälp med produkten finns i [hitta hjälp](find-help.md).

## <a name="search"></a><a name="bkmk_searchtips"></a>Sök

Använda följande söktips för att hitta den information du behöver:

- När du använder önskad sökmotor för att hitta innehåll för Configuration Manager ska du `ConfigMgr` inkludera tillsammans med Sök nyckelorden.

  - Sök efter resultat från `docs.microsoft.com/configmgr` för Configuration Manager aktuella grenen. Resultat från `docs.microsoft.com/previous-versions` gäller för äldre produkt versioner.

  - Om du vill fokusera Sök resultaten ytterligare till det aktuella innehålls biblioteket inkluderar `site:docs.microsoft.com` du sökmotorns omfång.

- Använd Sök termer som matchar terminologin i användar gränssnittet och onlinedokumentationen. Undvik officiella villkor eller förkortningar som du kan se i Community-innehåll. Sök till exempel efter:

  - "hanterings plats" i stället för "MP"
  - "distributions typ" i stället för "DT"
  - "program uppdateringar" i stället för "SUM"

- Om du vill söka i den aktuella artikeln använder du webbläsarens **Sök** funktion. I de flesta moderna webbläsare trycker du på **CTRL**+**F** och anger sedan Sök villkoren.

- Varje artikel om `docs.microsoft.com` innehåller följande fält för att hjälpa till med sökningen av innehållet:

  - **Sök** i det övre högra hörnet. Om du vill söka i alla artiklar anger du villkoren i det här fältet. Artiklar i Configuration Managers biblioteket innehåller automatiskt Sök `ConfigMgr` omfång för att bara söka i det här dokumentations biblioteket.

  - **Filtrera efter rubrik** ovanför den vänstra innehålls förteckningen. Om du vill söka i den aktuella innehålls förteckningen anger du villkoren i det här fältet. Det här fältet matchar endast termer som visas i artikel titlarna för den aktuella noden. Till exempel **kärn infrastruktur** (`docs.microsoft.com/configmgr/core`) eller **program hantering** (`docs.microsoft.com/configmgr/apps`).

- Har du problem med att hitta något? [Fil feedback!](#bkmk_docfeedback) När du har angett problemet anger du den sökmotor som du använder, nyckelorden du försökte och mål artikeln. Den här feedbacken hjälper Microsoft att optimera innehållet för bättre sökning.

> [!TIP]
> Från och med Configuration Manager version 1902 finns en noden **dokumentation** i den nya **Community** -arbetsytan i Configuration Manager-konsolen. Den här noden innehåller uppdaterad information om Configuration Manager dokumentation och support artiklar. Mer information finns i [använda Configuration Manager-konsolen](../servers/manage/admin-console.md#bkmk_doc-dashboard).

## <a name="feedback"></a><a name="bkmk_docfeedback"></a>Oss

Välj länken **feedback** högst upp till höger om en artikel för att gå till feedback-avsnittet längst ned. Det här avsnittet är integrerat med GitHub-problem. Mer information om integrering med GitHub-problem finns i [blogg inlägget dokumentations plattform](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs).

Om du vill dela feedback om själva Configuration Manager själva produkten väljer du **produkt feedback**. Mer information finns i [produkt feedback](find-help.md#product-feedback).

Ett [GitHub-konto](https://github.com/join) är ett krav för att ge feedback om dokumentation. När du har loggat in finns det en engångs auktorisering för Microsoft docs-organisationen. När du sedan väljer **feedback från innehåll**anger du en rubrik och en kommentar och **skickar sedan feedback**. Den här åtgärden skickar ett nytt problem för mål artikeln i [SCCMdocs-lagringsplatsen](https://github.com/MicrosoftDocs/SCCMdocs/issues).

Den här integrationen visar även eventuella befintliga öppna eller stängda problem för mål artikeln. Om det finns en sådan, granskar du dem innan du skickar ett nytt problem. Om du hittar ett relaterat ärende väljer du ikonen ansikte för att lägga till en reaktion, eller så kan du expandera den för att lägga till en kommentar.

#### <a name="types-of-feedback"></a>Typer av feedback

Använd GitHub-problem för att skicka in följande typer av feedback:

- Doc-fel: innehållet är inaktuellt, oklart, förvirrande eller brutet.
- Dokument förbättring: ett förslag för att förbättra artikeln.
- Doc-fråga: du behöver hjälp med att hitta befintlig dokumentation.
- Dokument idé: ett förslag på en ny artikel. Använd den här metoden i stället för UserVoice för feedback från dokumentation.
- Kudos: positiv feedback om en användbar eller informativ artikel!
- Lokalisering: feedback om översättning av innehåll.
- Sökmotor optimering (SEO): feedback om problem med att söka efter innehåll. Lägg till sökmotorn, nyckelorden och mål artikeln i kommentarerna.

Om du skapar ett problem för icke-doc-relaterade ämnen kommer Microsoft att stänga problemen. Ett exempel:

- [Produktfeedback](find-help.md#product-feedback)
- [Produkt frågor](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)
- [Supportförfrågningar](https://aka.ms/cmcbsupport)

Information om hur du delar feedback om den grundläggande docs.microsoft.com-plattformen finns i [feedback om dokument](https://aka.ms/sitefeedback). Plattformen innehåller alla omslutnings komponenter, till exempel sidhuvud, innehålls förteckning och höger meny. Även hur artiklarna återges i webbläsaren, till exempel teckensnitt, varnings rutor och sid ankare.

## <a name="notifications"></a><a name="bkmk_notifications"></a>Ansökningar

Använd följande steg för att ta emot meddelanden när innehålls ändringar i dokumentations biblioteket:

1. Använd [dokument Sök funktionen](https://docs.microsoft.com/search/index?scope=ConfigMgr) för att hitta en artikel eller en uppsättning artiklar. Ett exempel:

    - Sök efter en enskild artikel efter rubrik, ["loggfiler för fel sökning – Configuration Manager"](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr)

    - Sök efter en artikel om [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr)

2. I det övre högra hörnet väljer du **RSS** -länken.

3. Använd den här feeden i valfritt RSS-program för att ta emot meddelanden när något av Sök resultaten ändras.

> [!TIP]
> Du kan också **titta** på [SCCMdocs-lagringsplatsen](https://github.com/MicrosoftDocs/SCCMdocs) på GitHub. Den här metoden genererar många meddelanden. Det inkluderar inte heller ändringar från en privat databas som används av Microsoft.

## <a name="contribute"></a><a name="bkmk_contribute"></a>Ger

Configuration Manager dokumentations biblioteket, t. ex. merparten av innehållet på docs.microsoft.com, har öppen källkod på GitHub. Det här biblioteket godkänner och uppmuntrar community-bidrag. Mer information om hur du kommer igång finns i [deltagar guiden](https://docs.microsoft.com/contribute). Den enda förutsättningen är att skapa ett [GitHub-konto](https://github.com/join).

### <a name="basic-steps-to-contribute-to-sccmdocs"></a>Grundläggande steg för att bidra till SCCMdocs

1. Från mål artikeln väljer du **Redigera**. Den här åtgärden öppnar käll filen i GitHub.

2. Om du vill redigera käll filen väljer du Penn ikonen.

3. Gör ändringar i markdown-källan. Mer information finns i [så här använder du markdown för att skriva dokument](https://docs.microsoft.com/contribute/markdown-reference).

4. I avsnittet föreslå fil ändring anger du den offentliga inchecknings kommentaren som beskriver *vad* du har ändrat. Välj sedan **föreslå fil ändring**.

5. Rulla nedåt och kontrol lera de ändringar du gjort. Välj **skapa pull-begäran** för att öppna formuläret. Beskriv *varför* du har gjort den här ändringen. Tagga artikel författaren och begär att de granskas. Välj **skapa pull-begäran**.

### <a name="what-to-contribute"></a>Vad som ska bidra

Om du vill bidra, men inte vet var du ska starta, kan du läsa följande rekommendationer:

- Sök i listan med problem för Community-riktade etiketter:

  - [bästa-första problem](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)
  - [hjälp – önskas](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Microsoft-författare tilldelar dessa etiketter till problem som är lämpliga kandidater för community-bidrag.

- Granska en artikel som är korrekt. Uppdatera sedan **MS. date** -metadata med `mm/dd/yyyy` hjälp av format. Detta bidrag hjälper till att hålla innehållet uppdaterat.

- Lägg till klargöranden, exempel eller vägledning baserat på din erfarenhet. Detta bidrag använder kraften i communityn för att dela kunskap.

- Korrigera översättningar på ett annat språk än engelska. Detta bidrag förbättrar användbarheten för lokaliserat innehåll.

> [!NOTE]
> Stora bidrag kräver signering av ett licens avtal för bidrag (CLA) om du inte är anställd på Microsoft. GitHub kräver automatiskt att du undertecknar detta avtal när ett bidrag uppfyller tröskelvärdet.

### <a name="tips"></a>Tips

Följ dessa allmänna rikt linjer när du bidrar till Configuration Manager dokument:

- Överraskning oss inte med stora pull-begäranden. Ange i stället [ett problem](#bkmk_docfeedback) och starta en diskussion. Sedan kan vi enas om en riktning innan du investerar en stor del av tiden.

- Läs [Microsofts stil guide](https://aka.ms/MicrosoftStyle). Ta reda på de [10 viktigaste tipsen för Microsofts stil och röst](https://docs.microsoft.com/style-guide/top-10-tips-style-voice).

- Använd [mallen för pull-begäran](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md) som start punkt för ditt arbete.

- Följ [arbets flödet för GitHub Flow](https://guides.github.com/introduction/flow/).

- Blogg och Tweet (eller vad) om dina bidrag, ofta!

(Den här listan har lånats från [.net-bidrags guiden](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts).)

## <a name="consolidation-of-documentation-for-microsoft-endpoint-manager"></a>Konsolidering av dokumentation för Microsoft Endpoint Manager

För att bättre stödja kombinerade scenarier för Intune och Configuration Manager samlas deras dokumentations bibliotek på [webbplatsen för Microsoft Endpoint Manager](https://docs.microsoft.com/mem). Intune-dokumentationen finns nu på [docs.Microsoft.com/MEM/Intune](https://docs.microsoft.com/mem/intune)och Configuration Manager-dokumentationen finns nu på [docs.Microsoft.com/MEM/ConfigMgr](https://docs.microsoft.com/mem/configmgr). Om du fortfarande använder en gammal URL kommer den automatiskt att omdirigeras, så du behöver inte göra några ändringar för att läsa det här innehållet.

Om du ger feedback eller bidrar till artiklar, är vissa ändringar nödvändiga:

- Befintliga GitHub-problem finns kvar i den ursprungliga lagrings platsen, [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs/issues) eller [SCCMDocs](https://github.com/MicrosoftDocs/SCCMDocs/issues).

  - De här problemen visas inte som öppna eller stängda problem i avsnittet feedback i den länkade artikeln.

  - Vi fortsätter att arbeta för att lösa problemen.

  - I vissa fall kan vi fatta det svåra beslutet att stänga ett problem som vi inte tror att vi kan åtgärda.

  - Om du har ett problem i den befintliga lagrings platsen och är passion om det, så kan du lämna feedback på den migrerade artikeln i [MEMDocs-lagringsplatsen](https://github.com/MicrosoftDocs/MEMDocs).

- När du nu skickar feedback eller redigerar en artikel går ärendet eller pull-begäran till MEMDocs-lagringsplatsen.
