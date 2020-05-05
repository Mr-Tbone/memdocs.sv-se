---
title: MMS 2019-Docathon
ms.date: 05/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8fe2ecfc-f5c1-4fa6-8703-245339400723
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e671118578d059e2b8416e6854a701ce7c405c0f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718527"
---
# <a name="mms-2019-docathon"></a>MMS 2019-Docathon

Under Mellanvästern Management Summit (MMS) 2019 kör Microsoft Content-teamet för Configuration Manager och Microsoft Intune en docathon. Om du deltar i den [docs.Microsoft.com praktiska labb](https://sched.co/N6fd) sessionen på måndag 6 maj, är det dags att arbeta med bidrag med support från Microsoft-skribenterna. Docathon kör hela konferensen och alla registrerade MMS 2019-deltagare kan delta.

Varför ska du delta? Docs.microsoft.com är en plattform med öppen källkod för Microsofts produkt dokumentation som drivs av GitHub. Microsoft uppmuntrar alla att bidra till dokumenten! När du bidrar med känner plattformen igen i listan över deltagare i varje artikel. Följande bidrag är några av de typer som communityn kan tillhandahålla:

- Stavfel
- Tydliganden
- Exempel
- Verkliga vägledning och tips
- Innehålls granskning, aktualitet

## <a name="set-up"></a>Konfigurera

Om du inte redan har konfigurerat för att bidra, gör du följande i förväg.

### <a name="github-account"></a>GitHub-konto

Skapa ett [GitHub-konto](https://github.com/join)

- Identifiera eventuella anknytningar i din profil  

- Aktivera tvåfaktorsautentisering  

#### <a name="additional-considerations"></a>Annat som är bra att tänka på

- Kontrol lera företagets policy angående bidrag med öppen källkod  

    > [!Note]  
    > Större bidrag kräver att du godkänner licens avtalet för Microsoft Open Source [Contributor (CLA)](https://cla.opensource.microsoft.com/). Granska detta avtal i förväg.  

- Bidrag till antal docs.microsoft.com gentemot MVP Award  

- Microsoft-anställda har några mer obligatoriska engångs steg och en något annorlunda bidrags process  

Mer information finns i [GitHub Account Setup](https://docs.microsoft.com/contribute/get-started-setup-github) i guiden docs.Microsoft.com Contributor.

## <a name="scope"></a>Omfång

Den här händelsen omfattar endast följande GitHub-databaser:

- [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs)
- [SCCMDocs](https://github.com/MicrosoftDocs/SCCMdocs)
- [SCCM-dokument – PowerShell-Ref](https://github.com/MicrosoftDocs/sccm-docs-powershell-ref)

Du är också välkommen och uppmuntrar till att göra ändringar i annat docs.microsoft.com innehåll, men det kommer inte att kreditera den här händelsen.

## <a name="learn-the-process"></a>Lär dig processen

Läs information om [hur du skickar problem](../understand/use-docs.md#bkmk_docfeedback) och [hur du kan bidra](../understand/use-docs.md#bkmk_contribute). De flesta grundläggande ändringar kan göras via GitHub Browser-upplevelsen.  

> [!Note]  
> Om du är intresse rad av mer komplexa arbets flöden med git och VSCode kan du läsa [Installera verktyg för innehålls redigering](https://docs.microsoft.com/contribute/get-started-setup-tools). Och/eller be Aaron/Erik om hjälp. Följande åtgärder är några av orsakerna till att använda det mer komplexa arbets flödet:
>
> - Skapa en ny artikel
> - Lägg till bilder
> - Sök och ersätt sträng, inklusive reguljära uttryck
> - Större, mer komplexa ändringar  

## <a name="determine-your-goals"></a>Fastställ ditt eller dina mål

Börja fundera över och planera målet för den här händelsen. Vad vill du göra?

- Titta igenom befintliga problem i databaserna i det aktuella området. Etiketter som till exempel **första utfärdande** eller hjälp som **önskas** kan identifiera lämpliga start punkter. Om du vill ta itu med ett av dessa problem kan du kommentera det med **#MMS2019Docathon** och tagga @authordet, och be dem att tilldela ärendet till dig. Du kan med andra ord [anropa DIBS](https://www.merriam-webster.com/words-at-play/word-origin-dibs) på den. Upprepa den här processen så många gånger du vill.  
    Till exempel, i SCCMDocs, där Aaron är artikel författaren:`@aczechowski I'm claiming this issue for #MMS2019Docathon`

- Du känner till ett problem med en artikel, men det har inte arkiverats någon feedback. Det finns med andra ord inget i avsnittet **feedback** längst ned i artikeln. Skapa ett nytt problem och Använd sedan samma instruktioner som ovan för att kräva det.  

    - Du kan till exempel lägga till ett kod exempel, ett verkligt exempel eller ett vanligt tips.  

    - Undvik att ändra grammatik eller stil, om du inte pratar med Aaron/Erik i förväg.  

    - Din favorit artikel har ett datum som är äldre än 90 dagar, före den 6 februari 2019. Du kan granska den och sedan redigera filen till **MS. date** -metadata-egenskapen. Det bidraget innebär: "Jag har granskat den här artikeln och den är fortfarande tekniskt korrekt, så uppdatera datumet." Ange ett problem för att göra anspråk på det.  

    - Kontrol lera att det inte finns något öppet ärende för någon som redan har begärt det. Den här åtgärden krävs inte tekniskt. Om du inte gör det, och någon annan skickar det första, tar vi bara det första bidraget.  

- En timme lunch-session på måndagen är ägnad tid att arbeta med dessa mål. Aaron & Erik finns tillgängliga för att hjälpa dig med frågor eller problem.

## <a name="contest-summary"></a>Tävlings översikt

Tävlingen körs hela veckan, 6-9 maj. Alla registrerade MMS 2019-deltagare kan delta. Skicka in poster med 3:00 PM Central på torsdag den 9 maj 2019. Priserna kommer att tilldelas på torsdag, 9 kan efter det att [ConfigMgr-produktsortimentet Q&en session](https://sched.co/N6ge). Du måste vara på MMS 2019 för att kunna vinna, men du behöver inte delta i sessionen. Om du inte befinner dig i sessionen kan du kontakta Aaron innan han lämnar fredagen morgon.

> [!Important]  
> Du måste inkludera **#MMS2019Docathon** hashtagg i alla bidrag för kredit.

### <a name="award-categories"></a>Belönings kategorier

#### <a name="grand-prize"></a>Grand pris

- **Mest påverkan**: baserat på följande kriterier, som bedöms av Aaron & Erik. Om du tror att ditt bidrag ska kvalificeras, kan du kommentera i din pull-begäran för att övertyga oss om varför.

    - Förmån för communityn (50%)
    - Att säga av Microsofts formatmall (25%)
    - Korrekt markdown (25%)  

Grand pris vinnare får följande priser:

- Ett registrerings pass för [MMS Jazz-versionen](https://mmsmoa.com/sessions/jazz-edition.html), som är förregistrerade i MMS-ledningskommittén, ett $1799-värde!
- En anpassad Yeti Rambler 30 oz Tumbler
- En anpassad Popsocket bil ventilation montering + grepp

#### <a name="first-place-prizes"></a>Börja med att sätta priser

Följande priser beräknas efter antalet legitima bidrag till lagrings platser i området. De behöver inte slås samman eller publiceras, precis som skickas som en pull-begäran i slutet av konferensen. Vi förbehåller oss rätten att diskvalificera alla som verkar vara spel i systemet. Vinnare i varje kategori får en anpassad Yeti-Rambler 30 oz Tumbler och märkes Popsocket bil ventilation montering + grepp. En vinnare per kategori.

- **De flesta incheckningar har skickats**

- **De flesta rader har ändrats**

- **De flesta artiklar som vidrörs**

> [!Note]  
> Vi har inte tilldelat något pris för de flesta problem som har arkiverats. Feedbacken är användbar, men syftet med den här händelsen är att bidra.

## <a name="resources"></a>Resurser

- [Microsoft-stil](https://aka.ms/MicrosoftStyle)

    - [Snabb start](https://docs.microsoft.com/contribute/style-quick-start)

    - [De 10 viktigaste tipsen för Microsofts stil och röst](https://docs.microsoft.com/style-guide/top-10-tips-style-voice)

- [Deltagarguide](https://docs.microsoft.com/contribute)

- [Använda Markdown för att skriva i Docs](https://docs.microsoft.com/contribute/markdown-reference)

## <a name="official-rules"></a>Officiella regler

Microsoft Cloud + AI Developer Relations innehåll & Learning MMS 2019 Docathon Event tävling officiella regler

1. FINANSIÄR

    Dessa officiella regler ("regler") styr driften av Microsoft C + AI DevRel-innehåll MMS 2019 Docathon Event tävling ("tävling"). Microsoft Corporation är sponsorn ("sponsor").

2. DEFINIERAS

    I dessa regler, "Microsoft", "vi", "vår" och "oss", se sponsorn. "Du" och "själv" syftar på en tävlings deltagare. "Event" syftar på MMS 2019 Docathon-händelsen som lagras i Minneapolis, MN. Genom att ange samtycker du till att bindas av de här reglerna.

3. POST PERIOD

    Tävlingen kommer att köras under regelbundna händelse timmar från den 6 maj 2019 till den 9 maj 2019 ("ingångs period").

4. BEHÖRIGHET

    Öppen för alla registrerade händelse deltagare 18 år som är ålder eller äldre och som är en juridisk person av 50-USA (inklusive distriktet Columbia). Anställda och chefer hos Microsoft Corporation och dess dotter bolag, personer som är inblandade i genomförandet eller administrationen av denna befordran, och familje medlemmarna för varje (beroende, omedelbara familje medlemmar och personer som bor i samma hushåll) är inte berättigade. Annullera där det är förbjudet.

    För Business/Tradeshow-händelser: om du deltar i evenemanget i din kapacitet som anställd, är det ensam ansvar att följa din arbetsgivares presentkorts principer. Microsoft kommer inte att vara part i några tvister eller åtgärder som rör detta. OFFENTLIGA anställda, inklusive lärare: Microsoft strävar efter att följa reglerna för gåva och etik, och därför är myndigheter och offentliga anställda inte berättigade till denna befordran.

5. SÅ HÄR ANGER DU

    Om du vill skapa en post skickar du ändringar till artiklar i följande GitHub-databaser: IntuneDocs, SCCMDocs, SCCM-dok-PowerShell-Ref. Mer information om sändnings processen finns i [så här bidrar du till](https://docs.microsoft.com/sccm/core/understand/use-docs#bkmk_contribute).

    Skicka en pull-begäran på GitHub för att skicka in en post.

    Du kan skicka ett obegränsat antal poster. Vi tilldelar bara ett pris per kategori per person.

    Vi ansvarar inte för överskott, förlorade, sena, skadade eller ofullständiga poster. Om det är tvistat kommer poster att anses skickas av behörig konto innehavare av GitHub-kontot.

6. BERÄTTIGAD POST

    För att vara berättigad måste en post uppfylla följande innehåll/tekniska krav:

    - Din post måste vara ditt eget ursprungliga arbete. särskilt
    - Din post musn't har valts som vinnare i någon annan tävling. särskilt
    - Du måste ha fått alla medgivanden, godkännanden eller licenser som krävs för att du ska kunna skicka in ditt bidrag. särskilt
    - I den utsträckning som posten kräver att en användardefinierad tävling skickas, till exempel program vara, foton, videor, musik, teckningar, uppsatser och så vidare, är det befogat att deras uppgift är sitt ursprungliga arbete, inte har kopierats från andra utan tillstånd eller uppenbara rättigheter och inte strider mot sekretess, immateriell ägande rätt eller andra rättigheter till någon annan person eller enhet. Du kan inkludera Microsoft-varumärken, logo typer och design, där Microsoft ger dig en begränsad licens som du kan använda för att göra det enda syftet med att skicka in en post i denna tävling. särskilt
    - Din post får inte innehålla, som bestäms av oss i vårt enda och absolut gottfinnande, allt innehåll som är obscent eller stötande, våldsam, kränkande, nedsättande eller olaglig, eller som befordrar alkohol, olaglig droger, tobak eller en särskild politisk agenda eller som kommunicerar meddelanden som kan avspegla negativt på goodwill av Microsoft.

7. ANVÄNDNING AV POSTER

    Vi frånsäger sig inte ägande rätten till ditt bidrag. Genom att skicka in en post beviljar du oss en oåterkallelig, royalty fri, världs omspännande och licens för att använda, granska, utvärdera, testa och på annat sätt analysera din post och allt dess innehåll i samband med den här tävlingen och använda din post i något medium som nu är känt eller senare och som har uppfyllts i marknadsförings syfte eller befordran av Microsofts produkter eller tjänster, utan ytterligare behörighet från dig. Du får ingen kompensation eller kredit för användning av din post, förutom vad som beskrivs i dessa officiella regler.

    Genom att ange det, bekräftar vi att vi kan ha utvecklat eller förbrukat material liknande eller identisk med din post och du avstår från eventuella anspråk som är resultatet av eventuella likheter med din registrering. Du förstår att vi inte kommer att begränsa arbets uppgifter för representanter som har haft till gång till ditt bidrag och att du samtycker till att använda information i våra representanters sina-minnen i utvecklingen eller distributionen av våra produkter eller tjänster inte skapar något ansvar för oss enligt detta avtal eller upphovs rätts lagstiftning eller handels hemligheter.

    Din post kan publiceras på en offentlig webbplats. Vi ansvarar inte för obehörig användning av din post av besökarna på den här webbplatsen. Vi är inte skyldig att använda din post för något ändamål, även om den har valts som en vinnande post.

8. VAL AV VINNARE OCH MEDDELANDE

    I väntan på bekräftelse av berättigande kommer potentiella pris vinnare att väljas av Microsoft eller deras agent eller en kvalificerad bedömnings panel från bland alla berättigade poster som tagits emot baserat på följande bedömnings-kriterier:

    - Grand pris: mest påverkan, baserat på följande kriterier:
        - 50% – förmåns grupp
        - 25%-ändra till Microsofts formatmall
        - 25% – korrekt markdown
    - Följande första priser, som beräknas efter antalet legitima bidrag till lagrings platsens lagrings plats. De behöver inte slås samman eller publiceras, precis som skickas som en pull-begäran i slutet av konferensen. Vi förbehåller oss rätten att diskvalificera alla som verkar vara spel i systemet.
        - De flesta incheckningar har skickats
        - De flesta rader har ändrats
        - De flesta artiklar som vidrörs

    Vinnarna väljs efter 3:00 PM, Central tid på torsdag, 9 maj 2019.

    Vinnar kommer att meddelas vid händelsen och måste kräva pris innan händelsen stängs.

    Om det finns en förbindelse mellan alla berättigade poster, kommer en ytterligare bedömning att bryta anknyten baserat på de bedömnings kriterier som beskrivs ovan. Besluten om domare är slutliga och bindande. Om vi inte får ett tillräckligt antal poster som uppfyller registrerings kraven kan vi, i vårt eget gottfinnande, välja färre vinnar än antalet tävlings priser som beskrivs nedan.

    Vinnarna kommer att meddelas via den kontakt information som anges under registreringen och kan behövas för att slutföra ett pris-och skatte form ("Forms"). Om det inte går att kontakta en vald vinnare, om det inte går att kontakta ett pris, eller om det inte går att returnera några formulär, blir de valda Vinnarena förverkade med sitt pris och en alternativ vinnare väljs tid att tillåta. Endast tre alternativa vinnar väljs, efter vilken de priser som inte har angjorts, inte kan betalas.  

9. PRISER

    Följande priser kommer att tilldelas:

    - En (1) total pris. Ett pris paket som består av följande objekt:
        - Ett registrerings pass för [MMS Jazz-versionen](https://mmsmoa.com/sessions/jazz-edition.html) (tillhandahålls av MMS-styrningen). Ungefärligt detalj handels värde (ARV) $1799.
        - En Yeti Rambler 30 oz Tumbler. Ungefärligt detalj handels värde (ARV) $35,00.
        - En Popsocket bil ventilations montering + grepp. Ungefärligt detalj handels värde (ARV) $15,00.

        Det totala ungefärliga detalj handels värdet (ARV) för det här paketet är $1849.

    - Tre (3) första pris (er). Ett pris paket som består av följande objekt:
        - En Yeti Rambler 30 oz Tumbler. Ungefärligt detalj handels värde (ARV) $35,00.
        - En Popsocket bil ventilations montering + grepp. Ungefärligt detalj handels värde (ARV) $15,00.

        Det totala ungefärliga detalj handels värdet (ARV) för det här paketet är $50.

    Totalt ungefärliga detalj handels värde (ARV) för alla priser: $1999

    Vi kommer bara att tilldela en (1) pris per person. Högst det angivna antalet priser kommer att tilldelas. Ingen ersättning, överföring eller tilldelning av pris tillåts, förutom att Microsoft förbehåller sig rätten att ersätta ett pris med samma eller högre värde i händelse av att det erbjudna priset inte är tillgängligt. Priserna tilldelas "i befintligt skick" utan garanti av något slag, varken uttrycklig eller underförstådd, inklusive men inte begränsat till, underförstådda garantier eller säljbar het, lämplighet för ett särskilt ändamål eller frånvaro av intrång. Pris vinnarna kan krävas för att slutföra och returnera pris anspråk och/eller skatte formulär ("Forms") inom den tids gräns som anges i meddelandet om vinnare. Skatter på priset, om det finns, är det enda ansvar som vinnare har, som rekommenderas att söka oberoende jurister om skatte konsekvenserna av att godkänna ett pris. Genom att acceptera ett pris, samtycker du till att Microsoft kan använda din post, ditt namn, din avbildning och din hemorts online och i utskrift, eller på något annat medium, i samband med den här tävlingen utan betalning eller ersättning till dig, förutom där det är förbjudet enligt lag.

10. STRIDER

    Strider är baserat på antalet och kvaliteten på berättigade poster som tas emot.

11. ALLMÄNNA VILLKOR OCH ANSVARS FRI SLÄP

    I den utsträckning som lagen tillåter, genom att ange dig samtycker till att lansera och hålla ofarligt Microsoft och dess respektive föräldrar, partners, dotter bolag, dotter bolag, anställda och agenter, oavsett ansvar eller skada, förlust eller skada av något slag som uppstår i samband med den här tävlingen eller någon pris vinst.

    Alla lokala lagar gäller. Besluten från Microsoft är definitiva och bindande.

    Vi förbehåller oss rätten att säga upp, ändra eller pausa tävlingen av någon anledning, inklusive fusk, teknik fel, Catastrophe, krig eller andra oförutsedda eller oväntade händelser som påverkar integriteten för den här tävlingen, oavsett om den är mänsklig eller mekanisk. Om tävlings integriteten inte kan återställas kan vi välja vinnar bland alla berättigade poster som mottagits innan vi hade för att säga upp, ändra eller pausa tävlingen. Regler som strider mot dessa regler kommer att åsidosättas i hela lag och kan förbjudas från deltagande i Microsoft-tävlingar.

12. VINNAR LISTA

    Listan med pris vinnar skickas till https://aka.ms/mms2019docathon inom 30 dagar från den 9 maj 2019.

13. SEKRETESS

    På Microsoft strävar vi efter att skydda din integritet. Microsoft använder den information som du anger i det här formuläret för att meddela dig om viktig information om våra produkter, uppgraderingar och förbättringar och för att skicka information om andra produkter och tjänster från Microsoft. Microsoft delar inte den information som du tillhandahåller med tredje part utan ditt tillstånd, om det behövs för att slutföra de tjänster eller transaktioner som du har begärt, eller som krävs enligt lag. Microsoft förbinder sig att skydda säkerheten för din personliga information. Vi använder en rad säkerhetstekniker och -metoder för att skydda din personliga information från obehörig åtkomst, användning eller avslöjande. Din personliga information delas aldrig utanför företaget utan ditt tillstånd, förutom under villkor som beskrivs ovan.

    Om du anser att Microsoft inte har följt den här policyn kontaktar du Microsoft genom att skicka ett e- privrc@microsoft.com postmeddelande till eller post-till Microsoft Privacy Response Center, Microsoft Corporation, One Microsoft Way, REDMOND, WA 98052.
