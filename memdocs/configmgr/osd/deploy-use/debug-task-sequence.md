---
title: Felsök en aktivitetssekvens
titleSuffix: Configuration Manager
description: Använd fel söknings verktyget för aktivitetssekvenser för att felsöka en aktivitetssekvens.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 66f460b7ba5c870a9ee81d10835ceb9f660cba89
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711037"
---
# <a name="debug-a-task-sequence"></a>Felsök en aktivitetssekvens

*Gäller för: Configuration Manager (aktuell gren)*

<!--3612274-->

Från och med version 1906 är aktivitetssekvensen fel söknings verktyg ett nytt fel söknings verktyg. Du distribuerar en aktivitetssekvens i fel söknings läge till en liten samling. Med den kan du gå igenom aktivitetssekvensen på ett kontrollerat sätt för att under lätta fel sökning och undersökning. Fel söknings programmet körs för närvarande på samma enhet som motorn för aktivitetssekvenser, men det är inte en fjärrfelsökning.

> [!Note]  
> I den här versionen av Configuration Manager är aktivitetssekvensen fel sökare en för hands versions funktion. För att aktivera den, se [för hands versions funktioner](../../core/servers/manage/pre-release-features.md).  


## <a name="prerequisites"></a>Krav

- Uppdatera Configuration Manager-klienten på mål enheten

- Logga in på mål enheten som en användare i den lokala **Administratörs** gruppen. Fel söknings programmet körs bara för administratörer.

- Uppdatera start avbildningen som är kopplad till aktivitetssekvensen för att kontrol lera att den har den senaste klient versionen


## <a name="start-the-tool"></a>Starta verktyget

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj **aktivitetssekvenser**.

1. Välj en aktivitetssekvens. I gruppen distribution i menyfliksområdet väljer du **Felsök**.

    > [!Tip]  
    > Du kan också ange variabeln **TSDebugMode** till `TRUE` på en samling eller ett dator objekt som aktivitetssekvensen distribueras till. Alla enheter som har denna variabel uppsättning kommer att placera en aktivitetssekvens som distribueras i fel söknings läge.

1. Skapa en fel söknings distribution. Distributions inställningarna är desamma som för en normal aktivitetssekvensdistribution. Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md#process).

    > [!Note]  
    > Du kan bara välja en liten samling för en fel söknings distribution. Den visar endast enhets samlingar med 10 eller färre medlemmar.

Från och med version 1910 använder du den nya variabeln **TSDebugOnError** för att automatiskt starta fel sökningen när aktivitetssekvensen returnerar ett fel.<!-- 5012536 --> Mer information finns i [variabler för aktivitetssekvens-TSDebugOnError](../understand/task-sequence-variables.md#TSDebugOnError).

## <a name="use-the-tool"></a>Använda verktyget

När aktivitetssekvensen körs på enheten, öppnas fel söknings fönstret för aktivitetssekvensen som liknar följande skärm bild:

![Skärm bild av fel sökning för aktivitetssekvens](media/3612274-tsdebug.png)

Fel söknings programmet innehåller följande kontroller:

- **Steg**: från *nuvarande* position kör du bara nästa steg i aktivitetssekvensen.  

    > [!Note]  
    > När aktivitetssekvensen är i fel söknings läge, om ett steg returnerar ett oåterkalleligt fel, så kommer aktivitetssekvensen inte att fungera som vanligt. Med det här beteendet får du möjlighet att försöka igen när du har gjort en extern ändring.

- **Kör**: från *nuvarande* position, kör aktivitetssekvensen normalt till slutet, nästa *Bryt* punkt eller om ett steg Miss lyckas. Innan du använder den här åtgärden ska du se till att ange eventuella Bryt punkter med åtgärden **Ange rast** .

- **Ange aktuell**: Välj ett steg i fel söknings programmet och välj sedan **Ange aktuell**. Den här åtgärden flyttar den *aktuella* pekaren till det steget. Med den här åtgärden kan du hoppa över steg eller flytta bakåt.  

    > [!Warning]  
    > Fel söknings programmet anser inte typen av steg när du ändrar den aktuella positionen i sekvensen. Vissa steg kan ställa in variabler för aktivitetssekvenser som krävs för villkors utvärdering i senare steg. Om den tar slut kan vissa steg Miss lyckas eller orsaka betydande skador på en enhet. Använd det här alternativet på egen risk.  

- **Ange rast**: Välj ett steg i fel söknings programmet och välj sedan **Ange rast**. Den här åtgärden lägger till en *Bryt* punkt i fel söknings programmet. När du **Kör** aktivitetssekvensen stoppas den vid en *rast*.  

    - Ange Bryt punkter innan du använder åtgärden **Kör** .

    - Från och med version 1910, om du skapar en Bryt punkt i fel söknings programmet och sedan startar om datorn kommer fel söknings programmet att försätta dina Bryt punkter efter omstart.<!-- 5012509 -->

    - I version 1906 sparas inte Bryt punkter efter att datorn har startats om, som i steget [starta om datorn](../understand/task-sequence-steps.md#BKMK_RestartComputer) . Om du till exempel startar fel sökning från Software Center för en aktivitetssekvens, ska du inte ställa in avbrott i Windows PE-fasen. När datorn startas om i Windows PE pausar fel söknings verktyget aktivitetssekvensen så att du kan ställa in brytningar.

- **Rensa alla avbrott**: ta bort alla Bryt punkter.

- **Loggfil**: öppnar den aktuella logg filen för aktivitetssekvensen, **Smsts. log**, med [CMTrace](../../core/support/cmtrace.md). Du kan se logg poster när motorn för aktivitetssekvenser är "väntar på fel sökning".

- Kommando **tolk**: i Windows PE öppnas en kommando tolk.

- **Avbryt**: Stäng fel söknings programmet och rapportera inte aktivitetssekvensen.

- **Avsluta**: koppla från och Stäng fel söknings programmet, men aktivitetssekvensen fortsätter att köras normalt.

Fönstret **variabler för aktivitetssekvens** visar de aktuella värdena för alla variabler i aktivitetssekvensen. Mer information finns i [variabler för aktivitetssekvens](../understand/task-sequence-variables.md). Om du använder [variabel steget Ange aktivitetssekvens](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) med alternativet att **inte Visa det här värdet**visas inte variabelvärdet i fel söknings programmet. Du kan inte redigera variabel värden i fel söknings programmet.

> [!Note]
> Vissa variabler för aktivitetssekvens är endast för internt bruk och visas inte i referens dokumentationen.

Fel söknings programmet för aktivitetssekvenser fortsätter att köras efter en [omstart av datorn](../understand/task-sequence-steps.md#BKMK_RestartComputer) , men du måste återskapa eventuella Bryt punkter. Även om aktivitetssekvensen kanske inte kräver det, eftersom fel söknings programmet kräver användar interaktion, måste du logga in i Windows för att fortsätta. Om du inte loggar in efter en timme för att fortsätta fel sökningen Miss lyckas aktivitetssekvensen.

Det går också igenom en underordnad aktivitetssekvens med steget [Kör aktivitetssekvens](../understand/task-sequence-steps.md#child-task-sequence) . I fel söknings fönstret visas stegen för den underordnade aktivitetssekvensen tillsammans med huvud aktivitetssekvensen.


## <a name="known-issues"></a>Kända problem

Om du riktar både en normal distributions-och fel söknings distribution till samma enhet via flera distributioner kan fel söknings programmet för aktivitetssekvenser inte startas.


## <a name="see-also"></a>Se även

- [Om aktivitetssekvenssteg](../understand/task-sequence-steps.md)
- [Aktivitetssekvensvariabler](../understand/task-sequence-variables.md)
- [Använda aktivitetssekvensvariabler](../understand/using-task-sequence-variables.md)
- [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md)
