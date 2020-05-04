---
title: Använda redigeringsprogrammet för aktivitetssekvenser
titleSuffix: Configuration Manager
description: Förstå hur du använder redigeraren för aktivitetssekvenser i Configuration Manager-konsolen
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a4e8bb56-ee85-49fd-8b1c-c8f513cec671
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2047ae9e276ac94b633d1dc30814ed641cd34d03
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711429"
---
# <a name="use-the-task-sequence-editor"></a>Använda redigeringsprogrammet för aktivitetssekvenser

*Gäller för: Configuration Manager (aktuell gren)*

Redigera aktivitetssekvenser i Configuration Manager-konsolen med hjälp av **Redigeraren för aktivitetssekvens**. Använd redigeraren för att:  

- Öppna en skrivskyddad vy av aktivitetssekvensen

- Lägga till eller ta bort steg i aktivitetssekvensen  

- Ändra ordningen på stegen i aktivitetssekvensen  

- Lägg till eller ta bort grupper av steg  

- Kopiera och klistra in steg mellan aktivitetssekvenser

- Ange steg alternativ som om aktivitetssekvensen fortsätter när ett fel uppstår  

- Lägg till villkor i stegen och grupperna i en aktivitetssekvens  

- Kopiera och klistra in villkor mellan stegen i en aktivitetssekvens

- Sök i aktivitetssekvensen för att snabbt hitta steg

Innan du kan redigera en aktivitetssekvens måste du skapa den. Mer information finns i [Hantera och skapa aktivitetssekvenser](../deploy-use/manage-task-sequences-to-automate-tasks.md).

## <a name="about-the-task-sequence-editor"></a>Om redigeraren för aktivitetssekvens

Redigeraren för aktivitetssekvens innehåller följande komponenter:

![Kommenterad skärm bild av exempel fönstret för aktivitetssekvenser](media/task-sequence-editor.png)

<!-- The following numbered steps correspond to annotations in the above screenshot. Don't change the step numbers without also revising the image! -->

1. Namnet på aktivitetssekvensen
2. Sök. Mer information finns i [search](#bkmk_search).
3. **Egenskaper** för den valda gruppen eller steget i sekvensen

    Mer information om egenskaper och alternativ för ett särskilt steg finns i [om aktivitetssekvenser](task-sequence-steps.md).

4. **Alternativ** för den valda gruppen eller steget i sekvensen

    Mer information om allmänna alternativ för alla steg, eller alternativ för ett visst steg, finns i [om aktivitetssekvenser](task-sequence-steps.md).

    Mer information om hur du konfigurerar villkor finns i [villkor](#bkmk_conditions).

5. **Lägg till** en grupp eller några steg
6. **Ta bort** en grupp eller några steg
7. Dölj alla grupper eller expandera alla grupper
8. Flytta en grupp eller ett steg i sekvensen (flytta upp, flytta ned)
9. Aktivitetssekvensen:
    - Se ordningen på stegen och grupperna.
    - Expandera eller komprimera en grupp.
    - När du inaktiverar ett steg eller en grupp på dess **alternativ**, är det grå i sekvensen.
    - En stegs ikon ändras till ett rött fel om det är problem med steget. Till exempel saknas ett obligatoriskt värde.
10. **OK**: Spara och Stäng
11. **Avbryt**: Stäng utan att spara ändringarna
12. **Verkställ**: Spara ändringar och behåll öppna

Du kan ändra storlek på redigeraren för aktivitetssekvens med hjälp av standard kontroller i Windows. Om du vill ändra storlek på de två huvud Fönstren använder du musen för att markera stapeln mellan aktivitetssekvensen och steg egenskaperna. Dra den sedan åt vänster eller höger.

## <a name="view-a-task-sequence"></a><a name="bkmk_view"></a>Visa en aktivitetssekvens

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj noden **aktivitetssekvenser** .  

2. I listan **aktivitetssekvens** väljer du den aktivitetssekvens som du vill visa.  

3. På fliken **Start** i menyfliksområdet väljer du **Visa**i gruppen **aktivitetssekvens** .

    > [!TIP]
    > Den här åtgärden är standardvärdet. Om du dubbelklickar på en aktivitetssekvens **visar** du aktivitetssekvensen.

Den här åtgärden öppnar Redigeraren för aktivitetssekvens i skrivskyddat läge. I det här läget kan du utföra följande åtgärder:

- Visa alla grupper, steg, egenskaper och alternativ
- Expandera och minimera grupper
- Sök i aktivitetssekvensen
- Ändra storlek på redigerings fönstret

I det här skrivskyddade läget kan du inte göra några ändringar, inklusive kopiera ett steg eller ett villkor. Den här åtgärden låser inte heller aktivitetssekvensen för redigering. Mer information om dessa lås finns i [återta lås för att redigera aktivitetssekvenser](#bkmk_sedo).

Om du vill göra ändringar i en aktivitetssekvens stänger du aktivitetssekvensen som du har öppnat i skrivskyddat läge. [Redigera](#bkmk_edit) sedan aktivitetssekvensen.

> [!NOTE]  
> När du visar eller redigerar en aktivitetssekvens som skapats av guiden skapa aktivitetssekvens kan namnet på steget vara åtgärden eller typen av steg. Du kan till exempel se ett steg som har namnet "partition disk 0", vilket är åtgärden för ett steg av typen [format och partition disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk). Alla steg i aktivitetssekvensen dokumenteras av deras *typ*, inte nödvändigt vis av namnet på det steg som visas i redigeraren.  

## <a name="edit-a-task-sequence"></a><a name="bkmk_edit"></a> Redigera en aktivitetssekvens

Använd följande procedur om du vill ändra en befintlig aktivitetssekvens:  

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj noden **aktivitetssekvenser** .  

2. Välj den aktivitetssekvens som du vill redigera i listan **Aktivitetssekvens** .  

3. På fliken **Start** i menyfliksområdet väljer du **Redigera**i gruppen **aktivitetssekvens** . Gör sedan någon av följande åtgärder:  

    - **Lägg till ett steg**: Välj **Lägg till**, Välj en kategori och välj sedan det steg som ska läggas till. Om du till exempel vill lägga till steget [Kör kommando rad](task-sequence-steps.md#BKMK_RunCommandLine) : Välj **Lägg till**, Välj kategorin **Allmänt** och välj sedan **Kör kommando rad**. Den här åtgärden lägger till steget efter det för tillfället valda steget.

    - **Lägg till en grupp**: Välj **Lägg till**och välj sedan **ny grupp**. När du har lagt till en grupp lägger du till steg i den.  

    - **Ändra ordningen**: Välj det steg eller den grupp som du vill ändra ordning på. Använd sedan ikonerna **Flytta upp** eller **Flytta ned** . Du kan flytta enbart ett steg eller en grupp åt gången. Dessa åtgärder är också tillgängliga när du högerklickar på en grupp eller ett steg.

        Du kan klippa ut, kopiera och klistra in en grupp eller ett steg. Högerklicka på objektet och Välj åtgärden. Du kan också använda standard kortkommandon för varje åtgärd:

        - Klipp ut: **CTRL** + **X**
        - Kopiera: **CTRL** + **+ C**
        - Klistra in: **CTRL** + **V**

    - **Ta bort ett steg eller en grupp**: Välj steget eller gruppen och välj **ta bort**.  

4. Spara ändringarna och Stäng fönstret genom att välja **OK** . Välj **Avbryt** om du vill ignorera ändringarna och stänga fönstret. Välj **tillämpa** för att spara ändringarna och se till att redigeraren för aktivitetssekvens är öppen.  

En lista över de tillgängliga stegen för aktivitetssekvenser finns i [stegen i aktivitetssekvensen](task-sequence-steps.md).  

> [!IMPORTANT]  
> Om aktivitetssekvensen har associerade referenser till ett objekt som ett resultat av redigeringen, kräver redigeraren att du korrigerar referensen innan den kan stängas. Möjliga åtgärder är:  
>
> - Korrigera referensen
> - Ta bort det refererade objektet från aktivitetssekvensen  
> - Inaktivera tillfälligt det misslyckade steget i aktivitetssekvensen tills den brutna referensen har åtgärd ATS eller tagits bort  

Du kan öppna fler än en instans av redigeraren för aktivitetssekvens samtidigt. Med det här beteendet kan du jämföra flera aktivitetssekvenser eller kopiera och klistra in steg mellan dem. Du kan **Redigera** en aktivitetssekvens och **Visa** en annan, men du kan inte utföra båda åtgärderna på samma aktivitetssekvens.

## <a name="conditions"></a><a name="bkmk_conditions"></a>Kraven

Använd villkor för att styra hur aktivitetssekvensen beter sig. Lägg till villkor i ett enskilt steg eller en grupp med steg. Aktivitetssekvensen utvärderar villkoren innan steget körs på enheten. Det kör bara steget om villkoren utvärderas som true. Om ett villkor utvärderas som falskt, hoppar aktivitetssekvensen över gruppen eller steget.

Använd fliken **alternativ** för att hantera villkor:

![Hantera villkor på fliken Alternativ i redigeraren för aktivitetssekvens](media/4621098-copy-paste-ts-condition.png)

Följande typer av villkor är tillgängliga:

- **If-instruktion**: Använd en *IF* -sats för att gruppera villkor. Du kan utvärdera **alla villkor**, **eventuella villkor**eller **inga**.

- **Variabel för aktivitetssekvens**. Utvärdera det aktuella värdet för en inbyggd variabel, åtgärd, anpassad eller skrivskyddad [aktivitetssekvens](task-sequence-variables.md) i aktivitetssekvensen. Mer information finns i [steg villkor](using-task-sequence-variables.md#bkmk_access-condition).

    > [!NOTE]
    > Du kan använda en mat ris variabel i det här tillståndet, men du måste ange den angivna mat ris medlemmen. `OSDAdapter0EnableDHCP` Anger till exempel om det *första* nätverkskortet aktiverar DHCP. Mer information finns i [array-variabler](using-task-sequence-variables.md#bkmk_array).

- **OS-version**: utvärdera operativ system versionen för enheten där aktivitetssekvensen körs. Den här listan är de allmänna OS-versioner som används i Configuration Manager. Om du vill utvärdera en mer detaljerad OS-version, till exempel en angiven version av Windows 10, använder du **frågan WMI-** villkor.

- **OS-språk**: utvärdera OS-språket för enheten där aktivitetssekvensen körs. Den här listan innehåller de 257 språk som Windows stöder.

- **Fil egenskaper**: utvärdera versionen eller tidsstämpeln för alla filer på enheten där aktivitetssekvensen körs.

- **Mappegenskaper**: utvärdera tidsstämpeln för alla mappar på enheten där aktivitetssekvensen körs.

- **Register inställning**: utvärdera alla register nyckel värden på enheten där aktivitetssekvensen körs.

- **Fråga WMI**: Ange namn området och frågan som ska utvärderas på den enhet där aktivitetssekvensen körs.

- **Installerad program vara**: ange en Windows Installer-fil för att läsa in produkt information som ska matcha på enheten där aktivitetssekvensen körs. Du kan matcha mot en speciell produkt eller en version av produkten.

### <a name="cmdlets-for-conditions"></a>Cmdletar för villkor

Hantera villkor med följande PowerShell-cmdletar:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConditionFile](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFile?view=sccm-ps)
- [Get-CMTSStepConditionFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFolder?view=sccm-ps)
- [Get-CMTSStepConditionIfStatement](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionIfStatement?view=sccm-ps)
- [Get-CMTSStepConditionOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionOperatingSystem?view=sccm-ps)
- [Get-CMTSStepConditionQueryWmi](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionQueryWmi?view=sccm-ps)
- [Get-CMTSStepConditionRegistry](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionRegistry?view=sccm-ps)
- [Get-CMTSStepConditionSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionSoftware?view=sccm-ps)
- [Get-CMTSStepConditionVariable](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionVariable?view=sccm-ps)

### <a name="copy-and-paste-conditions"></a>Kopiera och klistra in villkor

<!-- 4621098 -->

Om du vill återanvända villkor från ett steg till ett annat, från och med version 1910, kan du nu kopiera och klistra in villkor i redigeraren för aktivitetssekvens. Välj ett villkor för att klippa ut eller kopiera det. Om ett villkor har underordnade objekt kopieras hela blocket. Om det finns ett villkor i Urklipp kan du klistra in det med följande alternativ:

- Klistra in före
- Klistra in efter
- Klistra in under (gäller endast kapslade villkor)

Använd standard tangent bords gen vägar för att kopiera (**CTRL** + **+ C**) och klipp ut (**CTRL** + **X**). Standard kortkommandot för **CTRL** + **V** gör att **Klistra in efter** -åtgärd.

Det finns också nya alternativ för att flytta upp eller ned i listan.

> [!Note]  
> Du kan kopiera och klistra in villkor mellan stegen i en aktivitetssekvens. Den här åtgärden stöds inte mellan olika aktivitetssekvenser.

## <a name="reclaim-lock-for-editing"></a><a name="bkmk_sedo"></a>Frigör lås för redigering

<!--3699337-->
Om Configuration Manager-konsolen slutar svara kan du vara utelåst från att göra ytterligare ändringar tills låset upphör att gälla efter 30 minuter. Det här låset är en del av Configuration Manager SEDO (serialiserad redigering av distribuerade objekt). Mer information finns i [Configuration Manager Sedo](../../develop/core/understand/sedo.md).

Från och med version 1906 kan du rensa låset på en aktivitetssekvens. Den här åtgärden gäller endast för ditt användar konto som har låst och på samma enhet som webbplatsen har beviljat låset. När du försöker komma åt en låst aktivitetssekvens kan du nu **ignorera ändringarna**och fortsätta redigera objektet. Dessa ändringar skulle förloras när låset upphörde att gälla.

> [!TIP]
> Från och med version 1910 kan du rensa låset för alla objekt i Configuration Manager-konsolen. Mer information finns i [använda Configuration Manager-konsolen](../../core/servers/manage/admin-console.md#bkmk_sedo).<!--4786915-->

## <a name="search"></a><a name="bkmk_search"></a>Sök

<!-- 4621085 -->

Om du har en stor aktivitetssekvens med många grupper och steg, kan det vara svårt att hitta vissa steg. Från och med version 1910 kan du nu söka i redigeraren för aktivitetssekvens. Med den här åtgärden kan du snabbare hitta steg i aktivitetssekvensen.

![Sökning i redigeraren för aktivitetssekvens](media/4621085-task-sequence-search.png)

Ange en sökterm att starta. Du kan begränsa sökningen med följande typer:

- Steg namn
- Steg beskrivning
- Steg typ
- Gruppnamn
- Gruppbeskrivning
- Variabelnamn
- Villkor
- Annat innehåll, till exempel strängar som variabel värden eller kommando rader

Den aktiverar alla omfattningar som standard.

Du kan också filtrera efter alla steg med följande attribut:

- Fortsätt vid fel
- Har villkor

Det aktiverar inte något av filtren som standard.

När du söker i redigerings fönstret, markeras i gult de steg som matchar Sök villkoren.

Kom snabbt åt de här Sök fälten och navigera bland Sök resultaten med följande kortkommandon:

- **CTRL** + **F**: Ange en Sök sträng
- **CTRL** + **O**: Välj sökalternativ för att begränsa resultaten
- **F3** eller **RETUR**: stega framåt genom resultaten
- **Shift** + **F3**: steg bakåt i resultatet

## <a name="see-also"></a>Se även

- [Hantera och skapa aktivitetssekvenser](../deploy-use/manage-task-sequences-to-automate-tasks.md)

- [Om aktivitetssekvenssteg](task-sequence-steps.md)

- [Använda aktivitetssekvensvariabler](using-task-sequence-variables.md)

- [Använda Configuration Manager-konsolen](../../core/servers/manage/admin-console.md)
