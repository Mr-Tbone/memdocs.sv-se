---
title: Användarhandbok för Software Center
titleSuffix: Configuration Manager
description: Lär dig mer om funktionerna i Software Center
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: end-user-help
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 19b1b56c394fbf71e9117ad12fbe900e6f07e5fb
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715558"
---
# <a name="software-center-user-guide"></a>Användarhandbok för Software Center

*Gäller för: Configuration Manager (aktuell gren)*

Din organisations IT-administratör använder Software Center för att installera program, program uppdateringar och uppgraderings fönster. I den här användar guiden beskrivs funktionerna i Software Center för användare av datorn.

Software Center installeras automatiskt på Windows-enheter som din IT-organisation hanterar. Information om hur du kommer igång finns i [så här öppnar du Software Center](#bkmk_open).

Allmänna anmärkningar om Software Center-funktioner:

- Den här artikeln beskriver de senaste funktionerna i Software Center. Om din organisation använder en äldre version av Software Center som fortfarande stöds, är inte alla funktioner tillgängliga. Kontakta IT-administratören om du vill ha mer information.

- IT-administratören kan inaktivera vissa aspekter av Software Center. Din speciella upplevelse kan variera.

- Om flera användare använder en enhet samtidigt kommer användaren med det lägsta sessions-ID: t vara den enda att se alla tillgängliga distributioner i Software Center. Till exempel flera användare i en fjärr skrivbords miljö. Användare med högre sessions-ID kan inte se vissa av distributionerna i Software Center. Till exempel kan användare med högre sessions-ID se distribuerade program, men inte distribuerade paket eller aktivitetssekvenser. Under tiden som användaren med det lägsta sessions-ID: t visas alla distribuerade program, paket och aktivitetssekvenser. Fliken **användare** i aktivitets hanteraren visar alla användare och deras sessions-ID.

- IT-administratören kan ändra färg på Software Center och lägga till din organisations logo typ.

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a>Öppna Software Center

Software Center installeras automatiskt på Windows-enheter som din IT-organisation hanterar. För den enklaste metoden att starta Software Center på en Windows 10-dator trycker du på **Start** och skriv `Software Center` . Du kanske inte behöver ange hela strängen för Windows för att hitta den bästa matchningen.

:::image type="content" source="media/start-menu-software-center.png" alt-text="Bästa matchning av Software Center i Start menyn":::

Du navigerar på Start menyn genom att titta under gruppen **Microsoft Endpoint Manager** för **Software Center** -ikonen.

:::image type="content" source="media/microsoft-endpoint-manager-start-menu.png" alt-text="Ikoner för Start-menyn i Microsoft Endpoint Manager":::

> [!NOTE]
> Sökvägen för Start-menyn ovan är för versioner från november 2019 (version 1910) eller senare. I tidigare versioner är mappnamnet **Microsoft System Center**.

Kontakta IT-administratören om du inte hittar Software Center på Start menyn.

## <a name="applications"></a>Program

:::image type="content" source="media/software-center-apps.png" alt-text="Software Center-fliken program" lightbox="media/software-center-apps.png":::

Välj fliken **program** (1) om du vill söka efter och installera program som din IT-administratör distribuerar till dig eller den här datorn.

- **Alla** (2): visar alla tillgängliga program som du kan installera.

- **Krävs** (3): IT-administratören framtvingar dessa program. Om du avinstallerar något av dessa program installerar Software Center om det.

- **Filter** (4): IT-administratören kan skapa kategorier av program. Om det är tillgängligt väljer du List rutan för att filtrera vyn till endast de program som finns i en viss kategori. Välj **alla** om du vill visa alla program.

- **Sortera efter** (5): ordna om listan över program. Den här listan sorteras som standard efter **senaste**. De senast tillgängliga programmen visas med en **ny** banderoll som är synlig i sju dagar.

- **Sök** (6): hittar du fortfarande inte det du letar efter? Ange nyckelord i sökrutan för att hitta det!

- Växla vy (7): Välj ikonerna för att växla visningen mellan listvyn och vyn sida vid sida. Som standard visas program listan som grafiska paneler.

|Ikon|Visa|Beskrivning|
|----|----|-----------|
|:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::|**Läge för flera val**|Installera mer än ett program i taget. Mer information finns i [installera flera program](#install-multiple-applications).|
|:::image type="icon" source="media/software-center-apps-list-view.png" border="false":::|**Listvy**|I den här vyn visas programmets ikon, namn, utgivare, version och status.|
|:::image type="icon" source="media/software-center-apps-tile-view.png" border="false":::|**Vyn sida vid sida**|IT-administratören kan anpassa ikonerna. Under varje panel visas programmets namn, utgivare och version.|

### <a name="install-an-application"></a>Installera en app

Välj ett program i listan om du vill se mer information om det. Välj **Installera** för att installera den. Om en app redan har installerats kan du välja att **Avinstallera**.

Vissa appar kan kräva godkännande innan de installeras.

- När du försöker installera den kan du ange en kommentar och sedan **begära** appen.

  :::image type="content" source="media/software-center-app-approval-request.png" alt-text="Installations förfrågan för Software Center-appen för godkännande":::

- Software Center visar förfrågnings historiken och du kan avbryta begäran.

  :::image type="content" source="media/software-center-app-approval-status.png" alt-text="Installation av Software Center-appen begärdes":::

- När en administratör godkänner din begäran kan du installera appen. Om du väntar installeras appen automatiskt i Software Center under din arbets tid.

  :::image type="content" source="media/software-center-app-approved.png" alt-text="Installation av Software Center-appen godkändes":::

### <a name="install-multiple-applications"></a>Installera flera program

<!-- 1357126 -->
Installera mer än ett program i taget i stället för att vänta tills det är klart innan du startar nästa. De valda apparna måste kvalificera sig:

- Appen är synlig för dig
- Appen laddas inte redan ned eller är inte installerad
- IT-administratören behöver inte godkänna för att installera appen

Så här installerar du fler än ett program i taget:

1. Välj ikonen för flera markeringar i det övre högra hörnet::::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::

2. Välj två eller fler appar som ska installeras. Markera kryss rutan till vänster om varje app i listan.

3. Välj knappen **Installera markerad** för att starta.

Apparna installeras som vanligt, bara nu i följd.

### <a name="share-an-application"></a>Dela ett program

Om du vill dela en länk till en speciell app väljer du **delnings** ikonen i det övre högra hörnet när du har valt appen::::image type="icon" source="media/software-center-share-app-icon.png" border="false":::

:::image type="content" source="media/software-center-share-app-window.png" alt-text="Dela en app från Software Center":::

**Kopiera** strängen och klistra in den någon annan stans, till exempel ett e-postmeddelande. Exempelvis `softwarecenter:SoftwareID=ScopeId_73F3BB5E-5EDC-4928-87BD-4E75EB4BBC34/Application_b9e438aa-f5b5-432c-9b4f-6ebeeb132a5a`. Andra i din organisation med Software Center kan använda länken för att öppna samma program.

## <a name="updates"></a>Uppdateringar

:::image type="content" source="media/software-center-updates.png" alt-text="Fliken uppdateringar av Software Center" lightbox="media/software-center-updates.png":::

Välj fliken **uppdateringar** (1) om du vill visa och installera program uppdateringar som din IT-administratör distribuerar till den här datorn.  

- **Alla** (2): visar alla uppdateringar som du kan installera

- **Krävs** (3): IT-administratören framtvingar dessa uppdateringar.

- **Sortera efter** (4): ordna om listan med uppdateringar. Som standard sorteras listan efter **program namn: A till ö**.

- **Sök** (5): hittar du fortfarande inte det du letar efter? Ange nyckelord i sökrutan för att hitta det!

Om du vill installera uppdateringar väljer du **Installera alla** (6).

Om du bara vill installera vissa uppdateringar väljer du ikonen för att ange Multi-SELECT-läge (7)::::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::
Kontrol lera uppdateringarna för att installera och välj sedan **Installera markerade**.

## <a name="operating-systems"></a>Operativsystem

:::image type="content" source="media/software-center-os.png" alt-text="Fliken Software Center-operativ system" lightbox="media/software-center-os.png":::

Välj fliken **operativ system** (1) om du vill visa och installera Windows-versioner som IT-administratören distribuerar till den här datorn.  

- **Alla** (2): visar alla Windows-versioner som du kan installera

- **Krävs** (3): IT-administratören framtvingar dessa uppgraderingar.

- **Sortera efter** (4): ordna om listan med uppdateringar. Som standard sorteras listan efter **program namn: A till ö**.

- **Sök** (5): hittar du fortfarande inte det du letar efter? Ange nyckelord i sökrutan för att hitta det!

## <a name="installation-status"></a>Installations status

Välj fliken **installations status** om du vill visa status för program. Du kan se följande tillstånd:

- **Installerat**: Software Center har redan installerat det här programmet på den här datorn.

- **Hämtar**: Software Center laddar ned program varan som ska installeras på den här datorn.

- **Misslyckades**: Software Center kunde inte installera program varan.

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

- Välj de tidigaste och senaste timmarna som du använder den här datorn. Som standard är dessa värden från **5:00** till **10:00 PM**.

- Välj de dagar i veckan som du vanligt vis använder den här datorn. Som standard väljer Software Center bara vecko dagar.

Ange om du regelbundet använder den här datorn för att utföra ditt arbete. Administratören kan installera program automatiskt eller göra ytterligare program tillgängliga för primära datorer.<!--3485366--> Om datorn som du använder är en primär dator väljer **du jag använder regelbundet den här datorn för mitt arbete**.

### <a name="power-management"></a>Energisparfunktioner

IT-administratören kan ange principer för energispar funktioner. Dessa principer hjälper din organisation att spara elektricitet när den här datorn inte används.

Om du vill göra den här datorn undantagen från dessa principer väljer **du Använd inte energi inställningar från min IT-avdelning på den här datorn**. Som standard är den här inställningen inaktive rad och datorn tillämpar energi inställningar.

### <a name="computer-maintenance"></a>Dator underhåll

Ange hur Software Center ska tillämpa ändringar i program varan före tids gränsen.

- **Installera eller avinstallera den program vara som krävs automatiskt och starta om datorn endast under den angivna arbets tiden**: den här inställningen är inaktive rad som standard.

- **Pausa Software Center-aktiviteter när min dator är i presentations läge**: den här inställningen är aktive rad som standard.

När du instrueras av IT-administratören väljer du **Synkronisera princip**. Den här datorn kontrollerar om det finns nya servrar för alla nya, till exempel program, program uppdateringar eller operativ system.

### <a name="remote-control"></a>Fjärrstyrning

Ange inställningar för fjärråtkomst och fjärr styrning för datorn.

**Använd inställningar för fjärråtkomst från IT-avdelningen**: som standard definierar IT-avdelningen inställningarna för att fjärrhjälpa dig. De andra inställningarna i det här avsnittet visar statusen för de inställningar som din IT-avdelning definierar. Inaktivera det här alternativet om du vill ändra några inställningar.

- **Tillåten åtkomst nivå för fjärråtkomst**
  - **Tillåt inte fjärråtkomst**: IT-administratörer kan inte fjärrans luta till den här datorn för att hjälpa dig.
  - **Endast vy**: en IT-administratör kan endast fjärrvisa skärmen.
  - **Fullständig**: en IT-administratör kan fjärrstyra den här datorn. Den här inställningen är standard alternativet.

- **Tillåt fjärr styrning av den här datorn av administratörer när jag är borta**. Den här inställningen är **Ja** som standard.

- **När en administratör försöker styra datorn via en fjärr anslutning**
  - **Fråga efter behörighet varje tid**: den här inställningen är standard alternativet.
  - **Fråga inte om behörighet**

- **Visa följande under fjärr styrning**: dessa visuella meddelanden är båda aktiverade som standard, så att du vet att en administratör kan komma åt enheten via fjärr anslutning.
  - **Status ikon i meddelande fältet**
  - **Ett anslutnings fält för session på Skriv bordet**

- **Spela upp ljud**: det här ljud meddelandet låter dig veta att en administratör har fjärråtkomst till enheten.
  - **När sessionen börjar och slutar**: den här inställningen är standard alternativet.
  - **Upprepade gånger under sessionen**
  - **Aldrig**

## <a name="custom-tabs"></a>Anpassade flikar

IT-administratören kan ta bort standard flikarna eller lägga till ytterligare flikar i Software Center. Anpassade flikar namnges av administratören och de öppnar en webbplats som administratören anger. Du kan till exempel ha en flik med namnet "supportavdelningen" som öppnar IT-organisationens support webbplats. <!--1358132-->

## <a name="more-information-for-it-administrators"></a>Mer information för IT-administratörer

Mer information finns tillgänglig för IT-administratörer om hur du planerar för och konfigurerar Software Center i följande artiklar:

- [Planera för Software Center](../../apps/plan-design/plan-for-software-center.md)
- [Klient inställningar för Software Center](../clients/deploy/about-client-settings.md#software-center)
- [Meddelanden om omstart av enhet](../clients/deploy/device-restart-notifications.md)
- [Introduktion till fjärr styrning](../clients/manage/remote-control/introduction-to-remote-control.md)
