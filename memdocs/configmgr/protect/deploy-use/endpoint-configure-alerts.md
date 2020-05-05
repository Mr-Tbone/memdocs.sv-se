---
title: Konfigurera Endpoint Protection aviseringar
titleSuffix: Configuration Manager
description: Lär dig hur du konfigurerar Endpoint Protection aviseringar i Configuration Manager.
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b44147006a9ae4d38d2275a4515d71d61eec55c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074868"
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Konfigurera aviseringar för Endpoint Protection i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

 Du kan konfigurera Endpoint Protection aviseringar i Microsoft Configuration Manager för att meddela administrativa användare när vissa händelser, t. ex. en infektion av skadlig kod, inträffar i hierarkin. Meddelanden visas i Endpoint Protection-instrumentpanelen i Configuration Manager-konsolen i noden **aviseringar** på arbets ytan **övervakning** , eller så kan de skickas via e-post till angivna användare.

 Använd följande steg och de kompletterande procedurerna i det här avsnittet för att konfigurera aviseringar för Endpoint Protection i Configuration Manager.

> [!IMPORTANT]
>  Du måste ha behörighet för **tvinga säkerhet** för samlingar för att kunna konfigurera Endpoint Protection aviseringar.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Steg för att konfigurera aviseringar för Endpoint Protection i Configuration Manager

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.

2.  I arbetsytan **Tillgångar och efterlevnad** klickar du på **Enhetssamlingar**.

3.  I listan **Enhetssamlingar** väljer du den samling som du vill konfigurera aviseringar för. Klicka sedan på **Egenskaper** i gruppen **Egenskaper** på fliken **Start**.

    > [!NOTE]
    >  Det går inte att konfigurera aviseringar för användarsamlingar.

4.  På fliken **aviseringar** i dialog rutan **Egenskaper** för _\><samlings namn_ väljer du **Visa den här samlingen på instrument panelen Endpoint Protection** om du vill visa information om åtgärder mot skadlig kod för den här samlingen i arbets ytan **övervakning** i Configuration Manager-konsolen.

    > [!NOTE]
    >  Det här alternativet är inte tillgängligt för samlingen **Alla system** .

5.  På fliken **aviseringar** i dialog rutan **Egenskaper** för _\><samlings namn_ klickar du på **Lägg till**.

6.  I dialog rutan **Lägg till nya samlings varningar** i avsnittet **Generera en avisering när följande villkor är uppfyllda** väljer du de aviseringar som du vill att Configuration Manager ska generera när de angivna Endpoint Protection händelserna inträffar och klickar sedan på **OK**.

7.  I listan **villkor** på fliken **aviseringar** markerar du varje Endpoint Protection avisering och anger följande information:

    -   **Aviserings namn** – acceptera standard namnet eller ange ett nytt namn för aviseringen.

    -   **Allvarlighets grad för avisering** – i listan väljer du den aviserings nivå som ska visas i Configuration Manager-konsolen.

8.  Ange följande ytterligare information beroende på vilken avisering du väljer:

    -   **Identifiering av skadlig kod** – den här aviseringen skapas om skadlig kod upptäcks på en dator i den samling som du övervakar. **Tröskeln för identifiering av skadlig kod** anger identifierings nivåer för skadlig kod som aviseringen genereras i:

        -   **Hög-alla identifieringar** – aviseringen genereras när det finns en eller flera datorer i den angivna samlingen där skadlig kod upptäcks, oavsett vilken åtgärd som Endpoint Protection klienten vidtar.

        -   **Medel-identifierad, väntande åtgärd** – aviseringen genereras när det finns en eller flera datorer i den angivna samlingen där skadlig kod identifieras och du måste ta bort den skadliga koden manuellt.

        -   **Låg-identifierad, fortfarande aktiv** – aviseringen genereras när det finns en eller flera datorer i den angivna samlingen där skadlig kod har identifierats och fortfarande är aktiv.

    -   **Utbrott av skadlig kod** – den här aviseringen genereras om en skadlig kod har identifierats på en angiven procent andel av datorerna i den samling som du övervakar.

        -   **Procent andel datorer där skadlig kod har identifierats** – aviseringen genereras när procent andelen datorer med skadlig kod som har identifierats i samlingen överskrider procent andelen som du anger. Ange ett procentvärde från **1** till **99**.

            > [!NOTE]
            >  Procentvärdet baseras på antalet datorer i samlingen, men omfattar inte datorer som inte har någon installerad Configuration Manager-klient. Den innehåller datorer som inte har installerat Endpoint Protection-klienten än.

    -   **Upprepad identifiering av skadlig kod** – den här aviseringen genereras om en viss skadlig kod upptäcks mer än ett visst antal gånger under ett angivet antal timmar på datorerna i den samling som du övervakar. Ange följande information för att konfigurera den här aviseringen:

        -   **Antalet gånger skadlig kod har identifierats:** – Aviseringen genereras när samma skadliga kod identifieras på datorer i samlingen mer än det angivna antalet gånger. Ange ett tal från **2** till **32**.

        -   **Identifieringsintervall (timmar):** Ange identifieringsintervallet (i timmar) under vilka antalet identifieringar av skadlig kod måste inträffa. Ange ett tal från **1** till **168**.

    -   **Identifiering av flera skadlig kod** – den här aviseringen genereras om fler än ett angivet antal typer av skadlig kod upptäcks under ett visst antal timmar på datorer i den samling som du övervakar. Ange följande information för att konfigurera den här aviseringen:

        -   **Antalet typer av skadlig kod som identifierats:** – Aviseringen genereras när det angivna antalet olika typer av skadlig kod identifieras på datorer i samlingen. Ange ett tal från **2** till **32**.

        -   **Identifierings intervall (timmar):** Ange identifierings intervallet, i timmar, under vilka antalet identifieringar av skadlig kod måste inträffa. Ange ett tal från **1** till **168**.

9. Stäng dialog rutan **Egenskaper** för _<samlings\> namn_ genom att klicka på **OK** .  

## <a name="alert-for-outdated-malware-client"></a>Avisering för inaktuell klient för skadlig kod

Från och med Configuration Manager version 1702 kan du konfigurera en avisering så att Endpoint Protection-klienter inte är inaktuella. Från valfri enhets samling kan du nu lägga till kolumner i listan för följande attribut för **klient versionen av program mot skadlig kod** och **Endpoint Protection distributions tillstånd**. I-konsolen navigerar du till exempel till till **gångar och efterlevnad** > **Översikt** > **enhets samlingar** > **alla Station ära datorer och Server klienter**. Högerklicka på kolumn rubriken och välj de kolumner som du vill lägga till. Om du vill söka efter en avisering kan du Visa **aviseringar** i arbets ytan **övervakning** . Om fler än 20% av de hanterade klienterna kör en inaktuell version av program mot skadlig kod, visas en inaktuell varning i klient versionen av program mot skadlig kod. Den här aviseringen visas inte på fliken **övervakning** > **Översikt** . Aktivera program uppdateringar för klienter för program mot skadlig kod för att uppdatera utgångna klienter för program mot skadlig kod.

Om du vill konfigurera den procent andel som aviseringen genereras vid expanderar du **övervaknings** > **aviseringar** > **alla aviseringar**, dubbelklickar på **klienter för program mot skadlig kod** och ändrar **varningen om procent andelen hanterade klienter med en inaktuell klient version av program mot skadlig kod är mer än** alternativet.

> [!div class="button"]
> [Nästa steg >](endpoint-definition-updates.md)
> 
> [!div class="button"]
> [Tillbaka >](endpoint-protection-site-role.md)
