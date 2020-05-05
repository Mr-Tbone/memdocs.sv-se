---
title: CMTrace
titleSuffix: Configuration Manager
description: Lär dig mer om hur du använder CMTrace-verktyget för att visa loggfiler för Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8c9c42dcd1e6a6a4ca064953f0513157f5ebb228
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723427"
---
# <a name="cmtrace"></a>CMTrace

*Gäller för: Configuration Manager (aktuell gren)*

CMTrace är ett av de [Configuration Manager verktygen](tools.md). Du kan visa och övervaka loggfiler, inklusive följande typer av filer:  

- Loggfiler i Configuration Manager-eller CCM-format (Client Component Manager)  

- Oformaterad ASCII-eller Unicode-textfiler, till exempel Windows Installer loggar  

Verktyget hjälper till att analysera loggfiler genom att markera, filtrera och söka efter fel.

Från och med version 1806 installeras logg visnings Verktyget CMTrace automatiskt tillsammans med Configuration Manager-klienten. Den läggs till i klient installations katalogen, vilket som standard är `%WinDir%\CCM\CMTrace.exe`.<!--1357971-->

> [!Note]  
> CMTrace registreras inte automatiskt med Windows för att öppna fil namns tillägget. log. Mer information finns i [fil associationer](#file-associations).  

Från och med version 1906 är **OneTrace** ett nytt logg visnings program med Support Center. Det fungerar ungefär som CMTrace, med förbättringar. Mer information finns i [Support Center OneTrace](support-center-onetrace.md).

## <a name="usage"></a>Användning

Kör **CMTrace. exe**. Första gången du kör verktyget visas en prompt för fil Association. Mer information finns i [fil associationer](#file-associations).

Du vidtar de flesta åtgärder i CMTrace från följande menyer:

- [Fil](#file-menu)
- [Verktyg](#tools-menu)

### <a name="file-menu"></a>Arkivmenyn

Följande åtgärder är tillgängliga på menyn **Arkiv** :  

- [Öppna](#open)
- [Öppna på servern](#open-on-server)
- [Utskriftsvy](#print)
- [Inställningar](#preferences)

På Arkiv-menyn visas även de senaste åtta senaste filerna. Öppna snabbt en av dessa loggar genom att välja den från menyn Arkiv.

#### <a name="open"></a>Öppna

Visar dialog rutan Öppna där du kan söka efter en loggfil.

Filtrera vyn efter filer av följande typer:

- Loggfiler (\*. log)  
- Gamla loggfiler (\*. LO_)
- Alla filer (\*.\*)

Följande två alternativ är inte markerade som standard:  

- **Ignorera befintliga rader**: när du väljer CMTrace ignoreras det befintliga innehållet i den valda logg filen och nya rader visas bara när de läggs till. Använd det här alternativet om du vill övervaka endast nya åtgärder när du inte behöver den fullständiga historiken för logg filen.  

- **Sammanfoga markerade filer**: om du aktiverar det här alternativet och väljer fler än en loggfil, sammanfogar CMTrace de valda loggarna i vyn. Den visar dem som om de är en enda loggfil. Den sammanslagna loggen uppdateras på samma sätt och har stöd för alla andra CMTrace-funktioner som om det är en enda loggfil.  

#### <a name="open-on-server"></a>Öppna på servern

Bläddra i mappen Configuration Manager-loggar på en plats system dator med dialog rutan standard bläddring. Du kan också söka i nätverket efter en fjärrdator.

När du väljer en fjärrdator att bläddra i söker CMTrace efter Configuration Managers resursen. Om det inte går att hitta en resurs med Configuration Manager loggfiler visas ett fel meddelande.  

Om du vill ansluta direkt till en känd dator utan att bläddra använder du åtgärden [Öppna](#open) . Ange sedan ett server namn och en resurs med hjälp av UNC-formatet.

#### <a name="print"></a>Skriv ut

Visa dialog rutan standard utskrift i Windows. Den här åtgärden skickar den aktuella logg filen till en skrivare. Den formaterar utdata enligt inställningarna på fliken utskrift i CMTrace inställningar.

#### <a name="preferences"></a>Inställningar

Konfigurera inställningar för CMTrace. Följande alternativ är tillgängliga:  

- Fliken **Allmänt**  

    - **Uppdaterings intervall**: styr hur ofta CMTrace söker efter ändringar i loggfiler och läser in nya rader. Som standard är det här värdet 500 millisekunder.  

    - **Markering**: anger den färg som CMTrace använder när du markerar de logg rader som du väljer. Som standard är den här färgen Basic gul (röd: 255, grön: 255, blå: 0).  

    - **Kolumner**: konfigurerar de kolumner som visas i vyn logg och i vilken ordning de visas. Som standard visar den logg text, komponent, datum/tid och tråd.  

- Fliken **utskrift**  

    - **Kolumner**: Konfigurera vilka kolumner som ska användas vid utskrift av loggfiler och i vilken ordning de visas. Som standard skrivs samma kolumner ut som i den visas.  

    - **Orientering**: anger standard utskrifts orientering när loggfiler skrivs ut. Åsidosätt den här inställningen i dialog rutan Skriv ut. Som standard använder den stående orientering.  

- Fliken **Avancerat**  

    - **Uppdaterings intervall**: tvingar CMTrace att uppdatera logg visningen vid ett visst intervall vid inläsning av ett stort antal rader. Som standard är det här alternativet inaktiverat med värdet noll.  

        > [!Note]  
        > I allmänhet ska du inte ändra **uppdaterings intervallet**. Det kan öka hur lång tid det tar att öppna stora loggfiler.

### <a name="tools-menu"></a>Verktyg-menyn

Följande åtgärder är tillgängliga på **verktyg** -menyn:

- [Reda](#find)
- [Sök nästa](#find-next)
- [Kopiera till Urklipp](#copy-to-clipboard)
- [Höjdpunkt](#highlight)
- [Filter](#filter)
- [Fel sökning](#error-lookup)
- [Pausa](#pause)
- [Visa/Dölj information](#showhide-details)
- [Visa/Dölj informations fönstret](#showhide-info-pane)

#### <a name="find"></a>Hitta

Sök efter en angiven text sträng i den öppna logg filen.  

#### <a name="find-next"></a>Sök nästa

Söker efter nästa matchande sträng, som du tidigare angav i dialog rutan Sök.  

#### <a name="copy-to-clipboard"></a>Kopiera till Urklipp

Kopierar de markerade raderna som oformaterad text till Urklipp i Windows. Om du undersöker Configuration Manager-och CCM-loggfilerna kopieras kolumnerna i samma ordning som vyn. De separerar varje kolumn med tabbtecken. Använd den här åtgärden när du kopierar loggar till e-postmeddelanden eller andra dokument.  

#### <a name="highlight"></a>Höjdpunkt

Ange en sträng som CMTrace använder för att söka efter texten i varje loggpost. Sedan markeras alla logg texter som matchar den sträng som du anger.  

- Markeringen använder den färg som du har angett i inställningar.  

- Om du vill inaktivera markering rensar du strängen från det här fältet.  

- Om du anger ett decimalt eller hexadecimalt tal försöker CMTrace matcha värdet med tråd kolumnen. Använd det här beteendet för att markera bearbetningen av en enskild tråd, utan att filtrera bort andra trådar som kan interagera med den.  

- Om du vill jämföra strängar med Skift läge aktiverar du alternativet för **SKIFT läges känslig**.  

#### <a name="filter"></a>Filter

Visa eller Dölj logg rader baserat på de angivna kriterierna. Använd filter för någon av de fyra kolumnerna oavsett om de visas eller inte. De här inställningarna gäller för varje öppnad loggfil.

Exempel:
<!--SCCMDocs issue #603-->

- Filtrera **Smsts. log** i post texten som innehåller "åtgärden" eller "gruppen".
- Filtrera **InventoryAgent. log** där post texten innehåller "mål".

#### <a name="error-lookup"></a>Fel sökning

Skriv eller klistra in en felkod i antingen ett decimalt eller hexadecimalt format för att visa en beskrivning. Möjliga fel källor är: Windows, WMI eller WinHTTP.

#### <a name="pause"></a>Pausa

Pausa eller starta om logg övervakning. Följande användnings fall är några möjliga orsaker till att du kan använda den här åtgärden:  

- När CMTrace visar information om logg filen för snabbt  

- När du pausar logg övervakning förloras den information som CMTrace visar inte om den aktuella filen rullar till en ny logg  

- När du vill stoppa CMTrace från att visa nya data när du undersöker logg filen  

#### <a name="showhide-details"></a>Visa/Dölj information

Visa eller Dölj alla kolumner förutom logg texten. Den utökar också kolumnen logg text till fönstrets bredd. Använd den här åtgärden när du ska visa loggar på en dator med låg bildskärms upplösning. Det visar mer av logg texten.  

> [!Note]  
> När du visar filer med oformaterad text döljer CMTrace automatiskt information eftersom de alltid är tomma.  

#### <a name="showhide-info-pane"></a>Visa/Dölj informations fönstret

Visa eller Dölj informations fönstret. Använd den här åtgärden när du ska visa loggar på en dator med låg bildskärms upplösning. Den visar mer loggnings information.  


## <a name="log-pane"></a>Logg fönster

Fönstret logg visas överst i fönstret CMTrace. Den visar rader från loggfiler.

När du väljer en rad är den tillfälligt markerad med Windows-Markeringens färg schema.

Markerade rader matchar de kriterier som du definierar med alternativet **Markera** på **verktyg** -menyn. Markeringen använder färgen som du anger i **Inställningar**.

CMTrace visar rader med fel med hjälp av en röd bakgrund och gul text färg. I CCM-format loggar har logg poster ett explicit typ värde som anger posten som ett fel. För andra logg format gör CMTrace en Skift läges känslig sökning i varje post för en text sträng som matchar "fel".

Den visar rader med varningar med hjälp av en gul bakgrund. I CCM-format loggar har logg poster ett explicit typ värde som anger posten som en varning. För andra logg format gör CMTrace en Skift läges känslig sökning i varje post för en text sträng som matchar "warn".


## <a name="info-pane"></a>Informations fönster

Informations fönstret är längst ned i fönstret CMTrace. Det innehåller följande funktioner:

- Information om den markerade logg posten  

- En text ruta som visar logg texten  

- Den visar vagn returer så att formaterad text blir lättare att läsa  

- Enklare att läsa långa poster som inte är helt synliga i logg fönstret  

Visa eller Dölj informations fönstret med alternativet **Visa/Dölj informations fönstret** på **verktyg** -menyn. Om informations fönstret tar upp mer än hälften av logg fönstret, döljs CMTrace automatiskt.

### <a name="progress-bar"></a>Förlopps indikator

När du först öppnar en loggfil ersätter CMTrace informations fönstret med en förlopps indikator. Den här statusen anger hur mycket av det befintliga fil innehållet som den läses in. Förloppet når 100 procent, CMTrace tar bort förlopps indikatorn och ersätter den med informations fönstret. När du läser in stora filer ger det här beteendet en indikation på hur länge belastningen kan ta.

### <a name="status-bar"></a>Statusfält

För loggfilerna Configuration Manager format och CCM-format visar statusfältet den förflutna tiden för de markerade logg posterna. Om du väljer en enda post visar verktyget tiden från den första logg posten till den valda posten. Om du väljer flera poster beräknar den tiden från den översta markerade posten till längst ned till höger. CMTrace formaterar denna information enligt följande:

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`


## <a name="windows-shell-integration"></a>Windows Shell-integrering

CMTrace stöder [fil associationer](#file-associations) och [Dra och släpp](#drag-and-drop)-funktionen.

### <a name="file-associations"></a>Fil associationer

CMTrace kan associeras med. log och. lo_ fil namns tillägg. När programmet startas kontrollerar det registret för att avgöra om det redan är associerat med dessa fil namns tillägg. Om CMTrace inte redan är kopplat till några fil namns tillägg uppmanas du att associera fil namns tilläggen med CMTrace. Om du väljer **fråga inte detta igen**hoppar CMTrace över den här kontrollen när den körs på den här datorn.

### <a name="drag-and-drop"></a>Dra och släpp

CMTrace stöder grundläggande dra-och-släpp-funktioner. Öppna filen genom att dra en loggfil från Utforskaren i Windows till CMTrace.


## <a name="other-tips"></a>Andra tips

### <a name="last-directory-registry-key"></a>Senaste katalog register nyckel

<!--511280-->
Som standard sparar CMTrace den senaste logg platsen som du öppnade. Det här beteendet är användbart på plats servern, eftersom den används som standard loggar Sök väg varje gång.

Första gången du startar den på en klient används den aktuella arbets katalogen som standard. Den här platsen kan vara den sökväg där du sparade CMTrace eller en sökväg som `%userprofile%\Desktop`.

Det **sista katalog** värdet i register nyckeln `HKEY_CURRENT_USER\Software\Microsoft\Trace32` styr den här standard platsen. Om du anger värdet till `%windir%\CCM\Logs` på klienterna öppnar CMTrace filer på klient logg platsen första gången du kör den.


## <a name="see-also"></a>Se även

- [Loggfiler](../plan-design/hierarchy/log-files.md)

- [Logg fils visnings program för Support Center](support-center.md#support-center-log-file-viewer)

- [Support Center OneTrace](support-center-onetrace.md)
