---
title: Vanliga frågor och svar om Endpoint Protection klient
titleSuffix: Configuration Manager
description: Få svar på vanliga frågor om Windows Defender och Endpoint Protection.
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3b206c1556c2e9550ade5c2322acd65ad2b19412
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906835"
---
# <a name="endpoint-protection-client-frequently-asked-questions"></a>Vanliga frågor och svar om Endpoint Protection klient

*Gäller för: Configuration Manager (aktuell gren)*


Dessa vanliga frågor och svar är avsedda för datoranvändare vars IT-administratör har distribuerat Windows Defender eller Endpoint Protection på deras hanterade datorer. Innehållet här kanske inte gäller för andra program mot skadlig kod. Microsoft System Center Endpoint Protection hanterar Windows Defender i Windows 10. Det kan också distribuera och hantera Endpoint Protection-klienten på datorer före Windows 10. Windows Defender beskrivs i den här artikeln, men informationen gäller även för Endpoint Protection.  

-   [Varför behöver jag antivirus-och antispionprograms program vara?](#why-do-i-need-antivirus-and-antispyware-software)  
-   [Hur vet jag om datorn har smittats av skadlig programvara?](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [Hur kan jag hitta versionen av Windows Defender?](#how-can-i-find-the-version-of-windows-defender)
-   [Vad ska jag göra om Windows Defender eller Endpoint Protection upptäcker skadlig programvara på datorn?](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer)  
-   [Vad är ett virus?](#what-is-a-virus)  
-   [Vad är ett spionprogram?](#what-is-spyware)  
-   [Vad är skillnaden mellan virus, spionprogram och annan potentiellt skadlig program vara?](#whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [Var kommer virus, spionprogram och annan potentiellt oönskad programvara från?](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [Kan jag få skadlig program vara utan att känna till det?](#can-i-get-malicious-software-without-knowing-it)  
-   [Varför är det viktigt att granska licensavtal innan du installerar programvara?](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [Vad är skillnaden mellan Endpoint Protection och Windows Defender?](#whats-the-difference-between-endpoint-protection-and-windows-defender)  
-   [Varför identifieras inte cookies i Windows Defender?](#why-doesnt-windows-defender-detect-cookies)  
-   [Hur kan jag förhindra skadlig kod?](#how-can-i-prevent-malware)  
-   [Vad är virus-och spionprograms definitioner?](#what-are-virus-and-spyware-definitions)  
-   [Hur gör jag för att hålla virus-och spionprograms definitioner uppdaterade?](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [Hur gör jag för att ta bort eller återställa objekt som har satts i karantän av Windows Defender eller Endpoint Protection?](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [Vad är real tids skydd?](#what-is-real-time-protection)  
-   [Hur gör jag för att vet du att Windows Defender eller Endpoint Protection körs på datorn?](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [Hur konfigurerar jag aviseringar i Windows Defender eller Endpoint Protection?](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  <a name="why-do-i-need-antivirus-and-antispyware-software"></a> Varför behöver jag virus- och spionprogramsprogramvara?  

 Det är viktigt att se till att din dator kör programvara som skyddar den mot skadlig programvara. Skadlig programvara, vilket inkluderar virus, spionprogram eller annan potentiellt oönskad programvara, kan försöka installera sig på datorn varje gång du ansluter till Internet. Den kan också smitta din dator när du installerar ett program från en CD, DVD eller annat flyttbart medium. Skadlig programvara kan också vara programmerad att köras vid oväntade tidpunkter, inte bara när det installeras.  

 Windows Defender eller Endpoint Protection erbjuder tre sätt som hjälper dig att förhindra att skadlig programvara smittar datorn:  

-   När real tids skyddet **används** i real tid kan Windows Defender övervaka datorn hela tiden och varna dig när skadlig program vara, inklusive virus, spionprogram eller annan potentiellt oönskad program vara försöker installera sig själv eller köras på datorn. Windows Defender stoppar sedan programvaran och gör det möjligt för dig att följa rekommendationen för programvaran eller välja ett annat alternativ.

-   **Genomsöknings alternativ** – du kan använda Windows Defender för att söka efter potentiella hot, till exempel virus, spionprogram och annan skadlig program vara som kan innebära att datorn är utsatt för risk. Du kan också använda det för att schemalägga genomsökningar regelbundet och ta bort skadlig programvara som upptäcks under en genomsökning.  

-   **Microsoft Active Protection Service community** – online Microsoft Active Protection Service community hjälper dig att se hur andra personer svarar på program vara som ännu inte har klassificerats för risker. Denna information hjälper dig att välja huruvida du vill tillåta programvaran på datorn. Om du dessutom deltar, läggs dina val till i gemenskapens klassificeringar som sedan hjälper andra användare att vidta lämpliga åtgärder.  

##  <a name="how-can-i-tell-if-my-computer-is-infected-with-malicious-software"></a>Hur vet jag om datorn har smittats av skadlig programvara?  

 Det kan finnas någon form av skadlig programvara, inklusive virus, spionprogram och annan potentiellt oönskad programvara på din dator om:  

-   Du upptäcker nya verktygsfält, länkar eller favoriter som du inte avsiktligt lagt till i din webbläsare.  

-   Din startsida, pekare eller sökprogram ändras oväntat.  

-   Du skriver adressen till en viss plats, till exempel en sökmotor, men du hamnar på annan webbplats utan föregående meddelande.  

-   Filer tas bort automatiskt från datorn.  

-   Datorn används för att angripa andra datorer.  

-   Du ser popupannonser, fast du inte är ute på Internet.  

-   Datorn går plötsligt långsammare än vanligt. Det är inte alla prestandaproblem som orsakas av skadlig programvara, men skadlig programvara, särskilt spionprogram kan orsaka en tydlig förändring.  

Det kan finnas skadlig programvara på datorn även om du inte ser några problem. Den här typen av program kan samla in information om dig och din dator utan din vetskap eller godkännande. För att skydda din integritet och datorn ska du alltid köra Windows Defender eller Endpoint Protection.  

## <a name="how-can-i-find-the-version-of-windows-defender"></a>Hur kan jag hitta versionen av Windows Defender?
 Om du vill se vilken version av Windows Defender som körs på datorn öppnar du Windows Defender (klicka på **Start** och Sök sedan efter **Windows Defender**), klickar på **Inställningar**och bläddrar till slutet av Windows Defender-inställningarna för att hitta **versions information**.

##  <a name="what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer"></a>Vad ska jag göra om Windows Defender eller Endpoint Protection upptäcker skadlig programvara på datorn?  

 Om Windows Defender upptäcker skadlig programvara eller potentiellt oönskad programvara på datorn (antingen vid övervakning av datorn med hjälp av realtidsskydd eller efter att du har kört en genomsökning) visas ett meddelande om det upptäckta objektet i det nedre högra hörnet på skärmen.  

 Meddelandet innehåller en **Rensa dator** -knapp och en **Visa information** -länk där du kan visa mer information om det upptäckta objektet. Klicka på länken **Visa information** för att öppna fönstret **Infgormation om potentiellt hot** för att få mer information om det upptäckta objektet. Du kan välja vilken åtgärd som ska användas för objektet eller klicka på **Rensa dator**. Om du behöver hjälp med att fastställa vilken åtgärd som ska användas för objektet, använder du den varningsnivå som Windows Defender tilldelat objektet som riktlinje (mer information finns i Förstå varningsnivåer).  

 Varningsnivåer hjälpa dig att välja hur du ska svara på virus, spionprogram och annan oönskad programvara. Även om Windows Defender rekommenderar att du tar bort alla virus och spionprogram, är det inte alla program som har flaggats som är skadliga eller oönskade. Följande information kan hjälpa dig att avgöra vad du gör om Windows Defender upptäcker potentiellt oönskad programvara på datorn.  

 Beroende på varningsnivån kan du välja någon av följande åtgärder för identifierade objekt:  

- **Ta bort** – den här åtgärden tar permanent bort program varan från datorn.  

- **Karantän** – den här åtgärden placerar program varan i karantän så att den inte kan köras. När Windows Defender placerar programvara i karantän flyttas den till en annan plats på din dator så att den förhindras att köras till du väljer att återställa den eller ta bort den från datorn.  

- **Tillåt** – den här åtgärden lägger till program varan i listan över tillåtna program i Windows Defender och tillåter att den körs på datorn. Windows Defender slutar varnar dig för risker som programvaran kan medföra för din integritet eller din dator.  

  Om du väljer **Tillåt** för ett objekt, t.ex programvara, slutar Windows Defender varna dig för risker som programmet kan utgöra för din integritet eller din dator. Därför bör du endast lägga till program i listan över tillåtna objekt om du litar på programvaran och dess utgivare.  

### <a name="how-to-remove-potentially-harmful-software"></a>Ta bort potentiellt skadlig programvara

Om du vill ta bort alla oönskade eller potentiellt skadliga objekt som Windows Defender identifierar snabbt och enkelt använder du alternativet **Rensa dator** .  

1.  När du ser aviseringsmeddelandet som visas i meddelandeområdet efter att potentiella hot upptäckts klickar du på **Rensa dator**.  

2.  Windows Defender tar bort det potentiella hotet (eller hoten) och meddelar dig när datorn har rensats.  

3.  Om du vill veta mer om de identifierade hoten klickar du på fliken **Historik** och väljer sedan **Alla identifierade objekt**.  

4.  Om du inte ser alla identifierade objekt, klickar du på **Visa information**. Skriv/bekräfta administratörslösenordet om du uppmanas att göra det för att bekräfta åtgärden.

> [!NOTE]  
>  Under rensning av datorn tar Windows Defender om möjligt bort enbart den smittade delen av en fil, inte hela filen.  

##  <a name="what-is-a-virus"></a>Vad är ett virus?  
 Datorvirus är program som medvetet utformats för att störa datorns funktion, för att registrera, förstöra eller ta bort data eller för att smitta andra datorer på Internet. Virus gör ofta att saker går långsammare och skapar andra problem i processen.  

##  <a name="what-is-spyware"></a> Vad är spionprogram?  
 Spionprogram är program som kan installera sig själva eller köras på din dator utan ditt medgivande eller på annat sätt meddela dig om det. Spionprogram uppvisar kanske inte några symtom efter att ha infekterat datorn, men många skadliga eller oönskade program kan påverka hur din dator fungerar. Till exempel kan spionprogram övervaka ditt onlinebeteende eller samla in information om dig (inklusive information som kan identifiera dig eller annan känslig information), ändra inställningar på datorn eller göra att datorn körs långsamt.  

##  <a name="whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software"></a> Vad är skillnaden mellan virus, spionprogram och annan potentiellt skadlig programvara?  
 Både virus och spionprogram installeras på din dator utan din vetskap och båda har möjlighet att vara påträngande och destruktiva. De har också möjlighet att samla in information om din dator och skada eller ta bort den informationen. Båda kan påverka datorns prestanda negativt.  

 De största skillnaderna mellan virus och spionprogram är hur de beter sig på datorn. Virus, precis som levande organismer, vill infektera en dator, replikeras och sedan spridas till så många datorer som möjligt. Spionprogram är dock mer som en Mole – det vill "flytta in i" din dator och stanna där så länge som möjligt, och skicka värdefull information om din dator till en extern källa medan det finns där.  

##  <a name="where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from"></a>Var kommer virus, spionprogram och annan potentiellt oönskad programvara från?  
 Oönskad programvara, till exempel virus, kan installeras av webbplatser eller av program som du hämtar eller som du installerar med hjälp av en CD, DVD, extern hårddisk eller en annan enhet. Spionprogram installeras vanligen via kostnadsfri programvara, till exempel fildelning, skärmsläckare eller sökverktygsfält.  

##  <a name="can-i-get-malicious-software-without-knowing-it"></a> Kan jag få skadlig programvara utan att känna till det?  
 Ja, viss skadlig program vara kan installeras från en webbplats via ett inbäddat skript eller ett program på en webb sida. En del skadliga programvaror kräver din hjälp för att installeras. Den här programvaran använder popupfönster eller kostnadsfri programvara som kräver att du accepterar en hämtningsbar fil. Om du däremot håller Microsoft Windows® uppdaterat och inte sänker dina säkerhetsinställningar kan du minimera risken att smittas.  

##  <a name="why-is-it-important-to-review-license-agreements-before-installing-software"></a>Varför är det viktigt att granska licensavtal innan du installerar programvara?  
 När du besöker webbplatser ska du inte automatiskt acceptera att ladda ned något som webbplatsen erbjuder. Om du hämtar kostnadsfri programvara, till exempel fildelningsprogram eller skärmsläckare, bör du läsa licensavtalet noggrant. Leta efter villkor som säger att du måste acceptera annonser och popupfönster från företaget, eller att programvaran kommer att skicka viss information tillbaka till programvaruutgivaren.  

##  <a name="whats-the-difference-between-endpoint-protection-and-windows-defender"></a>Vad är skillnaden mellan Endpoint Protection och Windows Defender?  
 Endpoint Protection är en programvara som skyddar mot skadlig programvara, vilket innebär att den har utformats för att identifiera och skydda datorn mot en mängd skadlig programvara, inklusive virus, spionprogram och annan oönskad programvara. Windows Defender, som installeras automatiskt med Windows, är ett program som identifierar och stoppar spionprogram.  

##  <a name="why-doesnt-windows-defender-detect-cookies"></a> Varför identifieras inte cookies i Windows Defender?  
 Cookies är små textfiler som webbplatser lagrar på datorn för att lagra information om dig och dina inställningar. Webbplatser använder cookies för att erbjuda en anpassad upplevelse och samla in information om webbplats användning. Windows Defender identifierar inte cookies eftersom det inte anses vara ett hot mot din sekretess eller datorns säkerhet. I de flesta webbläsare kan du blockera cookies.  

##  <a name="how-can-i-prevent-malware"></a> Hur kan jag förhindra skadlig kod?  
 Två av de största bekymren för datoranvändare idag är virus och spionprogram. I båda fallen kan de vara ett problem, men du kan enkelt skydda dig mot dessa med bara lite planering:  

-   Håll datorns program vara uppdaterad och kom ihåg att installera alla korrigeringsfiler. Kom ihåg att uppdatera operativsystemet regelbundet.  

-   Kontrollera att ditt antivirus- och antispionprogram, Windows Defender, använder de senaste uppdateringarna mot potentiella hot (se Hur håller jag virus-och spionprogramsdefinitioner uppdaterade?). Kontrollera också att du alltid använder den senaste versionen av Windows Defender.  

-   Hämta bara uppdateringar från välkända källor. För Windows-operativsystem går du alltid till [Microsoft Update katalogen](https://catalog.update.microsoft.com).  För annan program vara använder du alltid legitima webbplatser för det företag eller den person som tillverkar det.

-   Om du får ett e-postmeddelande med en bifogad fil och du är osäker på källan, bör du ta bort den direkt. Hämta inte några program eller filer från okända källor och var försiktig när du använder handelsfiler med andra användare.  

-   Installera och använd en brandvägg. Vi rekommenderar att du aktiverar Windows-brandväggen.  

##  <a name="what-are-virus-and-spyware-definitions"></a> Vad är virus- och spionprogramsdefinitioner?  
 När du använder Windows Defender eller Endpoint Protection är det viktigt att ha uppdaterade virus- och spionprogramsdefinitioner. Definitioner är filer som fungerar som ett ständigt växande uppslagsverk för potentiella programvaruhot. Windows Defender eller Endpoint Protection använder definitioner för att avgöra om misstänkt programvara är virus, spionprogram eller annan oönskad programvara och för att varna dig om potentiella risker. För att hålla definitionerna uppdaterade fungerar Windows Defender eller Endpoint Protection med Microsoft Update så att nya definitioner installeras automatiskt när de blir tillgängliga. Du kan också ställa in Windows Defender eller Endpoint Protection på att söka efter uppdaterade definitioner före genomsökningen.  

##  <a name="how-do-i-keep-virus-and-spyware-definitions-up-to-date"></a> Hur håller jag kontinuerligt virus-och spionprogramsdefinitioner uppdaterade?  
 Virus-och spionprogramsdefinitioner är filer som fungerar som ett uppslagsverk över känd skadlig programvara, inklusive virus, spionprogram och annan oönskad programvara. Eftersom skadlig programvara ständigt utvecklas förlitar sig Windows Defender eller Endpoint Protection på uppdaterade definitioner för att avgöra om programvara som försöker installeras, köras eller ändra inställningar på din dator är ett virus, spionprogram eller annat potentiellt oönskad programvara.  

### <a name="to-automatically-check-for-new-definitions-before-scheduled-scans-recommended"></a>Sök automatiskt efter nya definitioner före schemalagda sökningar (rekommenderas)  

1.  Öppna Windows Defender eller Endpoint Protection-klienten genom att klicka på ikonen i meddelandefältet eller starta om den från **Start** -menyn.  

2.  Klicka på **Inställningar**och klicka sedan på **Schemalagd genomsökning**.  

3.  Kontrollera att kryssrutan **Sök efter uppdaterade virus- och spionprogramsdefinitioner före en schemalagd sökning** är markerad och klicka sedan på **Spara ändringar**. Skriv/bekräfta administratörslösenordet om du uppmanas att göra det för att bekräfta åtgärden.  

### <a name="to-check-for-new-definitions-manually"></a>Söka efter nya definitioner manuellt

 Windows Defender eller Endpoint Protection uppdaterar virus- och spionprogramsdefinitioner på datorn automatiskt. Om definitionerna inte har uppdaterats på över sju dagar (till exempel om du inte har aktiverat datorn i en vecka), meddelar Windows Defender eller Endpoint Protection dig att definitionerna är inaktuella.  

1.  Öppna Windows Defender eller Endpoint Protection-klienten genom att klicka på ikonen i meddelandefältet eller starta om den från **Start** -menyn.  

2.  Om du vill söka efter nya definitioner manuellt klickar du på fliken **Uppdatera** och sedan på **Uppdatera definitioner**.  

##  <a name="how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a> Hur tar jag bort eller återställer objekt som placerats i karantän av Windows Defender eller Endpoint Protection?  

 När Windows Defender eller Endpoint Protection placerar programvara i karantän, flyttas programvaran till en annan plats på din dator och förhindras sedan från att köras tills du väljer att återställa den eller ta bort den från datorn.  

 Skriv/bekräfta administratörslösenordet om du uppmanas att göra det.  

###  <a name="to-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Ta bort eller återställa objekt som placerats i karantän av Windows Defender eller Endpoint Protection


1.  Klicka på fliken **Historik** , välj **Objekt i karantän**och välj sedan alternativet **Objekt i karantän** .  

2.  Klicka på **Visa information** för att se alla objekt.  

3.  Granska alla objekt och klicka på **Ta bort** eller **Återställ**för varje. Om du vill ta bort alla objekt i karantän från datorn klickar du på **Ta bort alla**.  

##  <a name="what-is-real-time-protection"></a> Vad är realtidsskydd?  

 Realtidsskydd gör det möjligt för Windows Defender att ständigt övervaka datorn och avisera dig om när potentiella hot, till exempel virus och spionprogram, försöker installeras eller köras på datorn. Eftersom den här funktionen är en viktig del av Windows Defenders förmåga att skydda din dator, bör du se till att realtidsskyddet alltid är aktiverat. Om real tids skyddet är inaktiverat meddelar Windows Defender dig och ändrar datorns status till **utsatt för risk**.  

 När realtidsskyddet identifierar ett hot eller potentiella hot visar Windows Defender ett meddelande. Du kan välja bland följande alternativ:  

- Klicka på **Rensa dator** för att ta bort identifierade objekt. Windows Defender tar automatiskt bort objektet från datorn.  

- Klicka på länken **Visa information** om du vill visa fönstret med information om det potentiella hotet och välj sedan vilken åtgärd som ska användas för det identifierade objektet.  

  Du kan välja vilka program och inställningar som du vill att Windows Defender ska övervaka, men vi rekommenderar att du slår på realtidsskyddet och aktiverar alla alternativ för realtidsskydd. De tillgängliga alternativen förklaras i följande tabell.  

|||  
|-|-|  
|**Realtidsskyddsalternativ**|**Syfte**|  
|Skanna alla hämtningar|Det här alternativet övervakar filer och program som hämtas, inklusive filer som hämtas automatiskt via Windows Internet Explorer och Microsoft Outlook® Express, till exempel ActiveX®-kontroller och installationsprogram. De här filerna kan hämtas, installeras eller köras av webbläsaren. Skadlig programvara, inklusive virus, spionprogram och annan potentiell oönskad programvara kan ingå i dessa filer och installeras utan din vetskap.<br /><br /> Med realtidsskyddsalternativet övervakar Windows Defender din dator ständigt och söker efter skadliga filer eller program som du kan ha råkat hämta. Den här övervakningsfunktionen innebär att Windows Defender inte behöver göra din surfning eller e-postupplevelse långsammare genom att kräva en kontroll av filer eller program som du vill hämta.|  
|Övervaka fil- och programaktivitet på datorn|Det här alternativet övervakar när filer och program startar på datorn och varnar dig sedan om alla åtgärder de utför och åtgärder som vidtas på dem. Detta är viktig eftersom skadlig programvara kan använda sårbarheter i program som du har installerat för att köra skadlig eller oönskad programvara utan din vetskap. Till exempel kan spionprogram köras automatiskt i bakgrunden när du startar ett program som du ofta använder. Windows Defender övervakar dina program och varnar dig om misstänkt aktivitet.|  
|Aktivera prestandaövervakning|Det här alternativet övervakar kända beteenden efter misstänkta mönster som inte kan identifieras av traditionella identifieringsmetoder i antivirusprogram.|  
|Aktivera system för nätverksinspektion|Det här alternativet hjälper till att skydda din dator mot noll dagars sårbarhet av kända sårbarheter, vilket minskar tidsfönstret mellan tidpunkten då ett säkerhets problem upptäcks och en uppdatering tillämpas.|  

### <a name="to-turn-off-real-time-protection"></a>Så här stänger du av realtidsskyddet  

1.  Klicka på **Inställningar**och sedan på **Realtidsskydd.**  

2.  Avmarkera de realtidsskyddsalternativ du vill avaktivera och klicka sedan på **Spara ändringar**. Skriv/bekräfta administratörslösenordet om du uppmanas att göra det för att bekräfta åtgärden.  

##  <a name="how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer"></a> Hur vet jag att Windows Defender eller Endpoint Protection är igång på min dator?  

 När du har installerat Windows Defender på datorn kan du stänga huvudfönstret och låta Windows Defender köras tyst i bakgrunden. Windows Defender fortsätter att köras på din dator, övervakar den och skyddar mot hot.  

 Naturligtvis vet du att Windows Defender körs när meddelanden visas i meddelandefältet. Dessa aviseringar varnar dig om potentiella hot som Windows Defender har identifierat.  

 Du får även andra aviseringar, till exempel om realtidsskydd av någon anledning av avaktiverats, om du saknar uppdaterade definitioner för virus- och spionprogram efter ett visst antal dagar eller när uppgraderingar till programmet blir tillgängliga. Windows Defender visar även kort en avisering om att din dator genomsöks.  

> [!TIP]
> 
> Om du inte ser ikonen för Windows Defender i meddelande fältet, klickar du på pilen i meddelande fältet för att visa dolda ikoner, inklusive ikonen för Windows Defender.  


 Ikonens färg beror på datorns aktuella status:  

-   Grönt anger att datorns status är "skyddad".  

-   Gult anger att datorns status är "potentiellt oskyddad".  

-   Rött anger att datorns status är "oskyddad".  

##  <a name="how-to-set-up-windows-defender-or-endpoint-protection-alerts"></a>Hur konfigurerar jag aviseringar i Windows Defender eller Endpoint Protection?  
 När Windows Defender körs på din dator varnas du automatiskt för virus, spionprogram eller oönskad programvara som upptäcks. Du kan också ställa in Windows Defender på att varna dig om du kör programvara som inte har analyserats än och du kan välja att få aviseringar när programvara försöker göra ändringar i din dator.  

### <a name="to-set-up-alerts"></a>Ställa in aviseringar  

1.  Klicka på **Inställningar**och sedan på **Realtidsskydd.**  

2.  Kontrollera att kryssrutan **Aktivera realtidsskydd (rekommenderas)** är markerad.  

3.  Markera kryssrutorna bredvid de realtidsskyddsalternativ som du vill köra och klicka sedan på **Spara ändringar**. Skriv/bekräfta administratörslösenordet om du uppmanas att göra det för att bekräfta åtgärden.  

### <a name="see-also"></a>Se även  
 [Felsöka Windows Defender eller Endpoint Protection-klient](troubleshoot-endpoint-client.md)   

 [Hjälp om Endpoint Protection-klienten](endpoint-protection-client-help.md)
