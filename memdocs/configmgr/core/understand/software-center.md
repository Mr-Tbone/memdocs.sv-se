---
title: Användarhandbok för Software Center
titleSuffix: Configuration Manager
description: Lär dig mer om funktionerna i Software Center
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: c4fa0819bf6427d93adf44a7b6284a8266e3a6a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722664"
---
# <a name="software-center-user-guide"></a>Användarhandbok för Software Center

*Gäller för: Configuration Manager (aktuell gren)*

Din organisations IT-administratör använder Software Center för att installera program, program uppdateringar och uppgraderings fönster. I den här användar guiden beskrivs funktionerna i Software Center för användare av datorn.

Allmänna anmärkningar om Software Center-funktioner:

- Den här artikeln beskriver de senaste funktionerna i Software Center. Om din organisation använder en äldre version av Software Center som fortfarande stöds, är inte alla funktioner tillgängliga. Kontakta IT-administratören om du vill ha mer information.

- IT-administratören kan inaktivera vissa aspekter av Software Center. Din speciella upplevelse kan variera.

- Om flera användare använder en enhet samtidigt, kan det vara en användare med det lägsta sessions-ID: t att se alla tillgängliga distributioner i Software Center via flera fjärrskrivbordssessioner. Användare med högre sessions-ID kan inte se vissa av distributionerna i Software Center. Till exempel kan användare med högre sessions-ID se distribuerade program, men inte distribuerade paket eller aktivitetssekvenser. Under tiden som användaren med det lägsta sessions-ID: t visas alla distribuerade program, paket och aktivitetssekvenser.

<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a>Öppna Software Center

För den enklaste metoden att starta Software Center på en Windows 10-dator trycker **Start** du på Start `Software Center`och skriv. Du kanske inte behöver ange hela strängen för Windows för att hitta den bästa matchningen.

Om du navigerar på Start menyn tittar du under gruppen **Microsoft Endpoint Manager** för **Software Center** -ikonen.

![Ikoner för Start-menyn i Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Sökvägen till Start-menyn har ändrats i version 1910. I version 1906 och tidigare är mappnamnet **Microsoft System Center**. När du uppdaterar Configuration Manager till version 1910 eller senare, måste du uppdatera all intern dokumentation som du upprätthåller för att ta med den nya platsen.

## <a name="applications"></a>Program

Välj fliken **program** för att söka efter och installera program som din IT-administratör distribuerar till dig eller den här datorn.

- **Alla**: visar alla program som du kan installera
- **Krävs**: IT-administratören framtvingar dessa program. Om du avinstallerar något av dessa program installerar Software Center om det.
- **Filter**: IT-administratören kan skapa kategorier av program. Om det är tillgängligt väljer du List rutan för att filtrera vyn till endast de program som finns i en viss kategori. Välj **alla** om du vill visa alla program.
- **Sortera efter**: ordna om listan över program. Den här listan sorteras som standard efter **senaste**. Nyligen tillgängliga program visas med en **ny** tagg som är synlig i 7 dagar.
- **Sök**: hittar du fortfarande inte det du letar efter? Ange nyckelord i sökrutan för att hitta det!
- **Växla vy**: Välj ikonerna för att växla visningen mellan listvyn och vyn sida vid sida. Som standard visas program listan som grafiska paneler.
    - Vyn sida vid sida: IT-administratören kan anpassa ikonerna. Under varje panel visas programmets namn, utgivare och version.
    - Listvy: den här vyn visar programmets ikon, namn, utgivare, version och status.

### <a name="install-multiple-applications"></a>Installera flera program

<!-- 1357126 -->
Installera mer än ett program i taget i stället för att vänta tills det är klart innan du startar nästa. Alla program är inte kvalificerade:

- Appen är synlig för dig
- Appen laddas inte redan ned eller är inte installerad
- IT-administratören behöver inte godkänna för att installera appen

Så här installerar du fler än ett program i taget:

1. Om du vill ange flera markerings lägen i listvyn väljer du ikonen för flera markeringar ![Ikon för Software Center-flera val](media/software-center-multi-select-apps.png) i det övre högra hörnet.
2. Välj två eller fler appar som ska installeras genom att markera kryss rutan till vänster om apparna i listan.
3. Välj knappen **Installera markerad** .

Apparna installeras som vanligt, bara nu i följd.


## <a name="updates"></a>Uppdateringar

Välj fliken **uppdateringar** om du vill visa och installera program uppdateringar som din IT-administratör distribuerar till den här datorn.  

- **Alla**: visar alla uppdateringar som du kan installera
- **Krävs**: IT-administratören framtvingar dessa uppdateringar.
- **Sortera efter**: ordna om listan med uppdateringar. Som standard sorteras listan efter **program namn: A till ö**.

Om du vill installera uppdateringar väljer du **Installera alla**.

Om du bara vill installera vissa uppdateringar väljer du ikonen för att ange läge för flera val. Kontrol lera uppdateringarna för att installera och välj sedan **Installera markerade**.


## <a name="operating-systems"></a>Operativsystem

Välj fliken **operativ system** om du vill visa och installera Windows-versioner som IT-administratören distribuerar till den här datorn.  

- **Alla**: visar alla Windows-versioner som du kan installera
- **Krävs**: IT-administratören framtvingar dessa uppgraderingar.
- **Sortera efter**: ordna om listan med uppdateringar. Som standard sorteras listan efter **program namn: A till ö**.


## <a name="installation-status"></a>Installations status

Välj fliken **installations status** om du vill visa status för program. Du kan se följande tillstånd:

- **Installerat**: Software Center har redan installerat det här programmet på den här datorn.
- **Hämtar**: Software Center laddar ned program varan som ska installeras på den här datorn.
- **Misslyckades**: Software Center påträffade ett fel vid försök att installera program varan.
- **Schemalagd att installeras efter**: visar datum och tid för enhetens nästa underhålls period för att installera kommande program vara. Underhålls fönster definieras av IT-administratören.<!--1358131-->
    - Status kan visas på fliken **alla** och på den **kommande** .
    - Du kan installera före underhålls periodens tid genom att välja knappen **Installera nu** .


## <a name="device-compliance"></a>Efterlevnad för enhet

Välj fliken **efterlevnad** på fliken enhet för att visa den här datorns kompatibilitetsstatus.

Välj **kontrol lera efterlevnad** för att utvärdera enhetens inställningar mot de säkerhets principer som definierats av IT-administratören.


## <a name="options"></a>Alternativ

Välj fliken **alternativ** om du vill visa ytterligare inställningar för datorn.

### <a name="work-information"></a>Arbets information

Ange de timmar som du normalt arbetar. IT-administratören kan schemalägga program varu installationer utanför kontors tid. Tillåt minst fyra timmar varje dag för system underhålls aktiviteter. IT-administratören kan fortfarande installera kritiska program och program varu uppdateringar under kontors tid.

- Markera List rutorna för att välja de tidigaste och senaste timmarna som du använder den här datorn. Som standard är dessa värden mellan **5** och **10 PM**

- Markera kryss rutan bredvid de vecko dagar som du vanligt vis använder den här datorn. Software Center väljer bara vecko dagar som standard.  

Ange om du regelbundet använder den här datorn för att utföra ditt arbete. Administratören kan installera program automatiskt eller göra ytterligare program tillgängliga för primära datorer. <!--3485366-->

- Välj **Jag använder regelbundet den här datorn för mitt arbete** om datorn du använder är en primär dator.

### <a name="power-management"></a>Energisparfunktioner

IT-administratören kan ange principer för energispar funktioner. Dessa principer hjälper din organisation att spara elektricitet när den här datorn inte används.

Om du vill göra den här datorn undantagen från dessa principer markerar du kryss rutan **Använd inte energi inställningar från min IT-avdelning på den här datorn**. Den här inställningen är inaktive rad som standard. datorn tillämpar energi inställningar.

### <a name="computer-maintenance"></a>Dator underhåll

Ange hur Software Center tillämpar ändringar i program varan före tids gränsen

- **Installera eller avinstallera den program vara som krävs automatiskt och starta om datorn endast under den angivna arbets tiden**: den här inställningen är inaktive rad som standard.
- **Pausa Software Center-aktiviteter när min dator är i presentations läge**: den här inställningen är aktive rad som standard.
- **Princip för synkronisering**: Välj den här knappen när du instrueras av IT-administratören. Den här datorn kontrollerar om det finns nya servrar för alla nya, till exempel program, program uppdateringar eller operativ system.

### <a name="remote-control"></a>Fjärrstyrning

Ange inställningar för fjärråtkomst och fjärr styrning för datorn

- **Använd inställningar för fjärråtkomst från IT-avdelningen**: den här kryss rutan är markerad som standard.
- **Tillåten åtkomst nivå**: Välj bland följande tre alternativ
    - **Tillåt inte fjärråtkomst**
    - **Visa endast**
    - **Fullständig**: den här nivån är aktive rad som standard.
- **Tillåt fjärr styrning av den här datorn av administratörer när jag är borta**. Den här inställningen är inställd på **Ja** som standard.
- **När en administratör försöker att fjärrstyra datorn**: den här inställningen har två alternativ
    - **Fråga efter behörighet varje tid**: det här alternativet är valt som standard.
    - **Fråga inte om behörighet**
- **Visa följande under fjärr styrning**: båda alternativen är markerade som standard
    - **Status ikon i meddelande fältet**
    - **Ett anslutnings fält för session på Skriv bordet**
- **Spela upp ljud**: den här inställningen har tre alternativ
    - **När sessionen börjar och slutar**: den här inställningen är markerad som standard.
    - **Upprepade gånger under sessionen**
    - **Aldrig**

    Mer information finns i [Introduktion till fjärr styrning](../clients/manage/remote-control/introduction-to-remote-control.md)
    

## <a name="custom-tab-in-software-center"></a>Anpassad flik i Software Center

IT-administratören kan ha lagt till ytterligare en flik i Software Center. Den här fliken namnges av din administratör och leder till en webbplats som de anger. Du kan till exempel ha en flik med namnet "supportavdelningen" som leder till din organisations support webbplats. <!--1358132-->
