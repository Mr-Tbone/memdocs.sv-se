---
title: Använda shell-skript på macOS-enheter i Microsoft Intune | Microsoft Docs
description: Skapa, tilldela, övervaka och felsöka shell-skript för macOS-enheter i Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/30/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 36b85fa6713af5679e59382efaeb354bb4949705
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990583"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune"></a>Använda shell-skript på macOS-enheter i Intune

Använd shell-skript för att utöka funktionerna för enhetshantering i Intune utöver vad som stöds av operativsystemet macOS. 

## <a name="prerequisites"></a>Krav
Se till att följande krav uppfylls när du skriver in shell-skript och tilldelar dem till macOS-enheter. 
 - Enheterna kör macOS 10.12 eller senare.
 - Enheterna hanteras av Intune. 
 - Shell-skript börjar med `#!` och måste finnas på en giltig plats, till exempel `#!/bin/sh` eller `#!/usr/bin/env zsh`.
 - Kommandoradstolkar för tillämpliga gränssnitt är installerade.

## <a name="important-considerations-before-using-shell-scripts"></a>Viktiga överväganden innan du använder shell-skript
 - Shell-skript kräver att Microsoft Intune-hanteringsagenten har installerats på macOS-enheten. Mer information finns i [Microsoft Intune-hanteringsagenten för macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).
 - Shell-skript körs parallellt på enheter som separata processer.
 - Shell-skript som körs som den inloggade användaren körs för alla användarkonton som är inloggade på enheten vid körningstillfället.
 - En slutanvändare måste logga in på enheten för att kunna köra skript som körs som en inloggad användare.
 - Rotanvändarbehörigheter krävs om skriptet kräver ändringar som ett standardanvändarkonto inte kan göra.
 - Shell-skript försöker köra oftare än den valda skriptfrekvensen för vissa villkor, till exempel om disken är full, om lagringsplatsen har ändrats, om den lokala cachen tas bort eller om Mac-enheten startas om.
 
## <a name="create-and-assign-a-shell-script-policy"></a>Skapa och tilldela en skriptprincip
1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **macOS** > **Skript** > **Lägg till**.
3. I **Grundläggande** anger du följande egenskaper och väljer sedan **Nästa**:
   - **Namn**: Ange ett namn på shell-skriptet.
   - **Beskrivning**: Ange en beskrivning för shell-skriptet. Denna inställning är valfri, men rekommenderas.
4. I **Skriptinställningar** anger du följande egenskaper och väljer **Nästa**:
   - **Ladda upp skript**: Bläddra till shell-skriptet. Skriptfilen måste vara mindre än 200 KB.
   - **Köra skript som inloggad användare**: Välj **Ja** för att köra skriptet med användarens autentiseringsuppgifter på enheten. Välj **Nej** (standard) om du vill köra skriptet som rotanvändaren. 
   - **Dölja skriptmeddelanden på enheter:** Som standard visas skriptmeddelanden för varje skript som körs. På macOS-enheter ser slutanvändarna en avisering från Intun om att *IT konfigurerar datorn*.
   - **Skriptfrekvens:** Välj hur ofta skriptet ska köras. Välj **Inte konfigurerat** (standard) för att bara köra skriptet en gång.
   - **Maximalt antal nya försök om skriptet misslyckas:** Välj hur många gånger skriptet ska köras om det returnerar en slutkod som inte är noll (noll innebär att det är klart). Välj **Inte konfigurerat** (standard) för att inte försöka igen när ett skript misslyckas.
5. I **Omfångstaggar** väljer du om du vill lägga till omfångstaggar för skriptet och väljer sedan **Nästa**. Du kan använda omfångstaggar för att bestämma vem som kan se skript i Intune. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).
6. Välj **Tilldelningar** > **Välj grupper att ta med**. En befintlig lista över Azure AD-grupper visas. Välj en eller flera användar- eller enhetsgrupper som ska ta emot skriptet. Välj **Välj**. De grupper du väljer visas i listan och tilldelas din skriptprincip.
   > [!NOTE]
   > - Shell-skript som tilldelas till användargrupper gäller för alla användare som loggar in på Mac-enheten.  
   > - Vid uppdatering av tilldelningar för shell-skript uppdateras även tilldelningar för [Microsoft Intune MDM-agent för macOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).

7. I **Granska + lägg till** visas en sammanfattning av de inställningar som du har konfigurerat. Välj **Lägg till** för att spara skriptet. När du väljer **Lägg till** distribueras skriptprincipen till de grupper som du har valt.

Skriptet som du har skapat visas nu i listan över skript. 

## <a name="monitor-a-shell-script-policy"></a>Övervaka en princip för shell-skript
Du kan övervaka körningsstatus för alla tilldelade skript för användare och enheter genom att välja någon av följande rapporter:
- **Skript** > **välj skriptet som ska övervakas** > **Enhetsstatus**
- **Skript** > **välj skriptet som ska övervakas** > **Användarstatus**

>[!IMPORTANT]
> Oberoende av den valda **skriptfrekvensen** rapporteras körningsstatus för skript endast den första gången ett skript körs. Skriptkörningsstatus uppdateras inte vid efterföljande körningar. Däremot behandlas uppdaterade skript som nya skript och rapporterar körningsstatus igen.

När ett skript körs returnerar det något av följande tillstånd:
- Skriptkörningsstatusen **Misslyckades** anger att skriptet returnerade en slutkod som inte är noll eller att skriptet har fel format. 
- Skriptkörningsstatusen **Lyckades** anger att skriptet returnerade noll som slutkod. 

## <a name="troubleshoot-macos-shell-script-policies-using-log-collection"></a>Felsöka principer för macOS-gränssnittsskript med hjälp av logginsamling

Du kan samla in enhetsloggar för att felsöka skriptproblem på macOS-enheter. 

### <a name="requirements-for-log-collection"></a>Krav för logginsamling
Följande objekt krävs för insamling av loggar på en macOS-enhet:
- Du måste ange den fullständiga absoluta loggfilsökvägen.
- Filsökvägar får endast avgränsas med ett semikolon (;).
- Den högsta storleken på loggsamlingar som kan laddas upp är 60 MB (komprimerat) eller högst 25 filer, beroende på vilken gräns som nås först.
- Filtyper som tillåts för logginsamling inkluderar följande filnamnstillägg: *.log, .zip, .gz, .tar, .txt, .xml, .crash och .rtf*

#### <a name="collect-device-logs"></a>Samla in enhetsloggar
1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. I rapporten för **Enhetsstatus** eller **Användarstatus** väljer du en enhet.
3. Välj **Samla in loggar** och ange sökvägar till loggfiler som endast avgränsas med semikolon (;) utan blanksteg eller radbrytningar mellan sökvägar.<br>Till exempel ska flera sökvägar skrivas som `/Path/to/logfile1.zip;/Path/to/logfile2.log`. 

   >[!IMPORTANT]
   > Flera loggfilsökvägar som avgränsas med kommatecken, punkt, radbrytning eller citattecken med eller utan blanksteg leder till logginsamlingsfel. Blanksteg är inte heller tillåtna som avgränsare mellan sökvägar.

4. Välj **OK**. Loggar samlas in nästa gång Intune-hanteringsagenten på enheten checkar in med Intune. Den här kontrollen sker vanligtvis var 8:e timme.

   >[!NOTE]
   > 
   > - Insamlade loggar krypteras på enheten, överförs och lagras i Microsoft Azure-lagring i 30 dagar. Lagrade loggar dekrypteras på begäran och laddas ned med hjälp av administrationscentret för Microsoft Endpoint Manager.
   > - Utöver de administratörsangivna loggarna samlas även loggarna för Intune-hanteringsagenten in från dessa mappar: `/Library/Logs/Microsoft/Intune` och `~/Library/Logs/Microsoft/Intune`. Agentloggfilernas namn är `IntuneMDMDaemon date--time.log` och `IntuneMDMAgent date--time.log`. 
   > - Om någon administratörsangiven fil saknas eller har fel filnamnstillägg hittar du dessa filnamn i `LogCollectionInfo.txt`.     

### <a name="log-collection-errors"></a>Logginsamlingsfel
Logginsamling lyckas kanske inte på grund av något av följande skäl som anges i tabellen nedan. Följ reparationsstegen nedan för att lösa felen.

| Felkod (hex) | Felkod (dec) | Felmeddelande | Reparationssteg |
|------------------|------------------|---------------|-------------------|
| 0X87D300D1 | 2016214834 | Loggfilstorleken får inte överskrida 60 MB. | Se till att komprimerade loggar är mindre än 60 MB stora. |
| 0X87D300D1 | 2016214831 | Den angivna loggfilsökvägen måste finnas. Systemanvändarmappen är en ogiltig plats för loggfiler. | Se till att den angivna filsökvägen är giltig och tillgänglig. |
| 0X87D300D2 | 2016214830 | Det gick inte att ladda upp logginsamlingsfilen eftersom uppladdningswebbadressen upphört att gälla. | Prova åtgärden **Samla in loggar** igen. |
| 0X87D300D3, 0X87D300D5, 0X87D300D7 | 2016214829, 2016214827, 2016214825 | Det gick inte att ladda upp logginsamlingsfilen på grund av ett krypteringsfel. Prova att ladda upp logar igen. | Prova åtgärden **Samla in loggar** igen. |
| | 2016214828 | Antalet loggfiler överskred den tillåtna gränsen på 25 filer. | Endast upp till 25 loggfiler kan samlas in åt gången. |
| 0X87D300D6 | 2016214826 | Det gick inte att ladda upp logginsamlingsfilen på grund av ett zipfel. Försök att ladda upp loggar igen. | Prova åtgärden **Samla in loggar** igen. |
| | 2016214740 | Det gick inte att kryptera loggarna eftersom de komprimerade loggarna inte hittades. | Prova åtgärden **Samla in loggar** igen. |
| | 2016214739 | Loggarna samlades in men kunde inte lagras. | Prova åtgärden **Samla in loggar** igen. |

## <a name="frequently-asked-questions"></a>Vanliga frågor och svar
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Varför körs inte tilldelade shell-skript på enheten?
Det här kan ha flera orsaker:
* Agenten kan behöva checka in för att ta emot nya eller uppdaterade skript. Incheckningsprocessen sker var åttonde timme och skiljer sig från MDM-incheckningen. Kontrollera att enheten är igång och ansluten till ett nätverk för en lyckad agentinloggning, och vänta tills agenten checkar in. Du kan också begära att slutanvändaren öppnar företagsportalen på Mac, markerar enheten och klickar på **Kontrollera inställningar**.
* Agenten kanske inte är installerad. Kontrollera att agenten är installerad på `/Library/Intune/Microsoft Intune Agent.app` på macOS-enheten.
* Agenten kanske inte är i felfritt tillstånd. Agenten kommer att försöka återställa i 24 timmar och sedan ta bort och ominstallera sig själv om shell-skripten fortfarande är tilldelade.

### <a name="how-frequently-is-script-run-status-reported"></a>Hur ofta rapporteras skriptkörningsstatus?
Skriptkörningsstatus rapporteras till Microsoft Endpoint Manager-administratörskonsolen så fort skriptkörningen har slutförts. Om ett skript har schemalagts för regelbunden körning med en angiven frekvens, rapporterar det bara status första gången det körs.

### <a name="when-are-shell-scripts-run-again"></a>När körs shell-skript igen?
Ett skript körs bara igen när inställningen för **högsta antal nya försök om skriptet misslyckas** har konfigurerats och skriptet misslyckas vid körning. Om inställningen för **högsta antal nya försök om skriptet misslyckas** inte har konfigurerats och ett skript inte kan köras, körs det inte igen och körningsstatusen rapporteras som **misslyckad**. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Vilka rollbehörigheter i Intune krävs för shell-skript?
Din tilldelade Intune-roll kräver behörigheter för **enhetskonfiguration** för att ta bort, tilldela, skapa, uppdatera eller läsa shell-skript.

## <a name="microsoft-intune-management-agent-for-macos"></a>Microsoft Intune-hanteringsagenten för macOS
 ### <a name="why-is-the-agent-required"></a>Varför behövs agenten?
Microsoft Intune-hanteringsagenten måste vara installerad på hanterade macOS-enheter för att du ska kunna använda avancerade enhetshanteringsfunktioner som inte stöds av det inbyggda macOS-operativsystemet.
 
 ### <a name="how-is-the-agent-installed"></a>Hur installeras agenten?
 Agenten installeras automatiskt och tyst på Intune-hanterade macOS-enheter som du tilldelar minst ett shell-skript i administrationscentret för Microsoft Endpoint Manager. Agenten installeras på `/Library/Intune/Microsoft Intune Agent.app` när det är tillämpligt och visas inte i **Finder** > **Program** på macOS-enheter. Agenten visas som `IntuneMdmAgent` i **Aktivitetskontroll** när den körs på macOS-enheter.

### <a name="what-does-the-agent-do"></a>Vad gör agenten?
 - Agenten autentiseras tyst med Intune-tjänster innan den checkar in för att ta emot tilldelade shell-skript för macOS-enheten.
 - Agenten tar emot tilldelade shell-skript och kör skripten baserat på det konfigurerade schemat, nya försök, meddelandeinställningar och andra inställningar som angetts av administratören.
 - Agenten söker normalt efter nya eller uppdaterade skript hos Intune-tjänster var 8:e timme. Incheckningsprocessen sker oberoende av MDM-incheckningen. 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>Hur kan jag starta en agentincheckning manuellt från en Mac?
På en hanterad Mac som har agenten installerad öppnar du **företagsportalen**, väljer den lokala enheten, klickar på **Kontrollera inställningar**. Detta initierar en MDM-incheckning och en agentincheckning.

Du kan också öppna **terminalen** och köra kommandot `sudo killall IntuneMdmAgent` för att avsluta `IntuneMdmAgent`-processen. Processen `IntuneMdmAgent` startas om omedelbart, vilket initierar en incheckning hos Intune.

> [!NOTE]
> Åtgärden **Synkronisera** för enheter i Microsoft Endpoint Manager-administratörskonsolen initierar en MDM-incheckning och tvingar inte fram en agentincheckning.

 ### <a name="when-is-the-agent-removed"></a>När tas agenten bort?
 Det finns flera villkor som kan orsaka att agenten tas bort från enheten, till exempel:
 - Shell-skripten tilldelas inte längre till enheten. 
 - macOS-enheten hanteras inte längre.
 - Agenten är i ett oåterkalleligt tillstånd i mer än 24 timmar (enhetens aktiva tid).

 ### <a name="why-are-scripts-running-even-though-the-mac-is-no-longer-managed"></a>Varför körs skript även om Mac inte längre hanteras?
 När en Mac med tilldelade skript inte längre hanteras tas agenten inte bort omedelbart. Agenten upptäcker att Mac inte hanteras vid nästa agentincheckning (vanligtvis var åttonde timme) och avbryter schemalagda skriptkörningar. Därför körs alla lokalt lagrade skript som är schemalagda att köras oftare än nästa schemalagda agentincheckning. När agenten inte kan checka in igen försöker den att checka in i upp till 24 timmar (enhetens aktiva tid) och tas sedan bort från Mac-enheten.
 
 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Vill du veta hur du stänger av de användningsdata som skickas till Microsoft för shell-skript?
 Om du vill stänga av användningsdata som skickas till Microsoft från Intune-hanteringsagenten öppnar du Företagsportal och väljer **Meny** > **Inställningar** > *avmarkera Tillåt att Microsoft samlar in användningsdata*. Åtgärden stänger av användningsdata som skickas för både Intune-hanteringsagenten och Företagsportal.

## <a name="known-issues"></a>Kända problem
- **Ingen körningsstatus för skript:** Skulle det osannolika inträffa att ett skript tas emot på enheten och enheten kopplas från innan körningsstatusen rapporteras, kommer enheten inte att rapportera körningsstatus för skriptet i administratörskonsolen.

## <a name="next-steps"></a>Nästa steg

- [Skapa en efterlevnadsprincip i Microsoft Intune](..\protect\create-compliance-policy.md)
