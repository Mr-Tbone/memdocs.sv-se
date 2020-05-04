---
title: Så här analyserar och konverterar du paket
titleSuffix: Configuration Manager
description: Lär dig hur du analyserar och konverterar paket med Package Conversion Manager i Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f3bf1737-827d-48fa-8bb1-f48fe71afe0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f72e7330909bc5653e69790e38ae043e539cc239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709938"
---
# <a name="how-to-analyze-and-convert-packages-with-package-conversion-manager"></a>Analysera och konvertera paket med Package Conversion Manager

*Gäller för: Configuration Manager (aktuell gren)*

<!--1357861-->

Innan du kan konvertera ett paket måste du först analysera det. Beroende på resultatet av analysen kan du göra något av följande:

- **Konvertera** paketet till ett program. I listan **paket** i-konsolen visas beredskaps statusen **Automatisk**.  

- **Åtgärda och konvertera** paketet, bifoga samlingar och skapa globala villkor. I listan **paket** i-konsolen visas beredskaps statusen **Automatisk**.  

- **Åtgärda och konvertera** paketet. I listan **paket** i-konsolen visas beredskaps status **manuellt**.  

- Lämna paketet utan att konverteras. I listan **paket** i-konsolen visas beredskaps statusen **inte tillämpligt**.  



## <a name="how-to-analyze-packages"></a><a name="bkmk_analyze"></a>Analysera paket

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **program hantering**och välj noden **paket** .  

2. Välj det paket som ska konverteras. På fliken **Start** i menyfliksområdet väljer du **analysera paket**i gruppen **paket konvertering** . Package Conversion Manager analyserar paketet.  

3. Om du vill se paketets beredskaps tillstånd lägger du till kolumnen **beredskap** i listan över paket. Paketets beredskaps tillstånd bestämmer din nästa åtgärd:  

    - **Automatiskt**: [så här konverterar du paket](#bkmk_convert)  

        Om du också vill koppla samlingar och skapa globala villkor med ett **automatiskt** beredskaps tillstånd, se [hur du korrigerar och konverterar paket](#bkmk_fix).  

    - **Manuellt**: [åtgärda och konvertera paket](#bkmk_fix)

    - **Inte tillämpligt**: det här paketet saknar nödvändigt innehåll eller program. Lägg till innehåll eller program som saknas och försök igen. Eller lämna det i ett tillstånd som inte har konverterats och fortsätta att distribuera det som ett paket.  

    - **Okänd**: kör först **analys** uppgiften eller vänta på nästa schemalagda analys. Om tillståndet inte ändras går du till [Felsöka Package Conversion Manager](troubleshoot-pcm.md).<!-- SCCMDocs#2044 -->

## <a name="how-to-convert-packages"></a><a name="bkmk_convert"></a>Så här konverterar du paket

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **program hantering**och välj noden **paket** .  

2. Välj det paket som ska konverteras med beredskaps tillstånd **automatiskt**. På fliken **Start** i menyfliksområdet väljer du **konvertera paket**i gruppen **paket konvertering** . Guiden konvertera paket till program öppnas.  

3. Gå igenom listan med valda paket i guiden konvertera paket till program. Ta bort alla paket som du inte vill konvertera och välj **OK**. Package Conversion Manager konverterar paketet. I fönstret konvertering slutförd visas konverterings statusen för de nya programmen.  

    > [!Note]  
    > När du konverterar ett paket registrerar platsen datum och tid för konverteringen som UTC-tid.  

4. Följ instruktionerna i fönstret. Välj antingen **Visa program** eller **Stäng**.  



## <a name="how-to-fix-and-convert-packages"></a><a name="bkmk_fix"></a>Åtgärda och konvertera paket

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **program hantering**och välj noden **paket** .  

2. Välj ett paket med beredskaps status **manuell** eller **Automatisk**. På fliken **Start** i menyfliksområdet väljer du **korrigera och konvertera**i gruppen **paket konvertering** .  

3. Granska informationen på sidan **paket val** i guiden paket konvertering och notera **objekten som ska åtgärdas**. Välj **Nästa**.  

4. På sidan **beroende granskning** granskar du om paketet är beroende av andra listade paket och väljer sedan **Nästa**.  

    > [!Note]  
    > Om du inte har konverterat något av de beroende paket som visas, måste du först konvertera paketen. Starta sedan om paket konverterings processen.  
    >  
    > Om ett beroende inte krävs tar du bort det eller ignorerar det och fortsätter konverterings processen.  

5. På sidan **distributions typ** granskar du distributions typerna för det nya programmet. Ändra deras prioritet eller ta bort distributions typerna.  

6. Om någon av de nya distributions typerna inte har en associerad identifierings metod visas en varnings ikon i kolumnen **identifierings metod** . Utför följande åtgärder:  

    1. Välj **Redigera identifierings metod**.  

    2. Välj **Lägg till**.  

    3. I dialog rutan identifierings regel anger du en **inställnings typ**.  

    4. Ange ytterligare information som krävs för identifierings regeln för den angivna inställnings typen.  

    5. Välj **OK**. Om det behövs upprepar du den här processen för att lägga till flera identifierings metoder till varje distributions typ.  

    6. Välj **OK**. Kontrol lera kolumnen **identifierings metod** visar en ikon för att bekräfta en korrekt angiven identifierings metod.  

7. Välj **Nästa**.  

8. På sidan **krav urval** granskar du distributions typerna för det nya programmet. Välj en distributions typ och granska kraven för den distributions typen.  

    > [!Note]  
    > Guiden visar bara de krav som Package Conversion Manager konverterar. Den konverterar inte alla WQL-frågor i enhets samlingar till krav.  

9. Lägg till krav för en vald distributions typ, om det behövs.  

10. Välj **Nästa**.  

11. Skapa programmet genom att slutföra guiden.  

    > [!Note]  
    > När du konverterar ett paket registrerar platsen datum och tid för konverteringen som UTC-tid.  



## <a name="monitor"></a><a name="bkmk_monitor"></a>Övervakningsprogrammet

Gå till arbets ytan **övervakning** i Configuration Manager-konsolen och välj **paket konverterings status**. Den här instrument panelen visar den övergripande analys-och konverterings statusen för paket på-platsen. En ny bakgrunds aktivitet sammanfattar automatiskt analys data.

> [!Tip]  
> Package Conversion Manager integrerat med Configuration Manager kräver inte att du planerar analys av paket. Den här åtgärden hanteras av den integrerade sammanfattnings aktiviteten.

![Skärm bild av instrument panelen för konverterings status i exempel paket](media/1357861-pcm-dashboard.png)
