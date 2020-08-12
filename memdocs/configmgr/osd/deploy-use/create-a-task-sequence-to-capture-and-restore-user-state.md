---
title: Avbilda och återställa användar tillstånd
titleSuffix: Configuration Manager
description: Använd Configuration Manager aktivitetssekvenser för att avbilda och återställa användar tillstånds data i distributions scenarier för operativ system.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a1f11c46689b213b795c0d71221728f916a68bb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125499"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>Skapa en aktivitetssekvens för att avbilda och återställa användar tillstånd i Configuration Manager

 *Gäller för: Configuration Manager (aktuell gren)*

 Använd Configuration Manager aktivitetssekvenser för att avbilda och återställa användar tillstånds data i distributions scenarier för operativ system. I dessa scenarier vill du behålla användar statusen för det aktuella operativ systemet. Beroende på vilken typ av aktivitetssekvens du skapar kan stegen för avbildning och återställning läggas till automatiskt som en del av aktivitetssekvensen. I andra scenarier kan du behöva lägga till stegen för avbildning och återställning i aktivitetssekvensen manuellt. Den här artikeln innehåller de steg som du måste lägga till i en befintlig aktivitetssekvens för att avbilda och återställa användar tillstånds data.  



## <a name="task-sequence-steps"></a>Aktivitetssekvenssteg  

Om du vill avbilda och återställa användar tillstånd lägger du till följande steg i aktivitetssekvensen:  

- [Begär tillstånds lager](../understand/task-sequence-steps.md#BKMK_RequestStateStore): om du lagrar användar tillstånd på platsen för tillståndsmigrering, behöver du det här steget.  

- [Avbilda användar tillstånd](../understand/task-sequence-steps.md#BKMK_CaptureUserState): det här steget samlar in användar tillstånds data. Sedan lagras data antingen på platsen för tillståndsmigrering eller den lokala disken med hjälp av hardlinks.  

- [Återställ användartillstånd](../understand/task-sequence-steps.md#BKMK_RestoreUserState): Med det här steget återställs användartillståndsinformationen på måldatorn. Den kan hämta data från en plats för tillståndsmigrering eller om hardlinked på den lokala disken.  

- [Frisläpp tillstånds lager](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore): om du lagrar användar tillstånd på platsen för tillståndsmigrering, behöver du det här steget. Det här steget tar bort data från platsen för tillståndsmigrering.  


 Använd följande procedurer för att lägga till de steg i aktivitetssekvensen som krävs för att avbilda och återställa användar tillstånd. Mer information om hur du skapar en aktivitetssekvens finns i [Hantera aktivitetssekvenser för att automatisera uppgifter](manage-task-sequences-to-automate-tasks.md).  



## <a name="capture-the-user-state"></a>Avbilda användar tillstånd  

 Följ stegen nedan om du vill lägga till steg i aktivitetssekvensen för att avbilda användar tillstånd:

1.  Välj en aktivitetssekvens i listan **Aktivitetssekvens** och klicka sedan på **Redigera**.  

2.  Om du använder en plats för tillståndsmigrering för att lagra användar tillstånd lägger du till steget **begär tillstånds lager** i aktivitetssekvensen. I **Redigeraren för aktivitetssekvens**klickar du på **Lägg till**. Peka på **användar tillstånd**och klicka sedan på **begär tillstånds lager**. Konfigurera egenskaperna och alternativen för det här steget och klicka sedan på **Använd**. Mer information om de tillgängliga inställningarna finns i [begär tillstånds lager](../understand/task-sequence-steps.md#BKMK_RequestStateStore).  

3.  Lägg till steget **Avbilda användartillstånd** i aktivitetssekvensen. I **Redigeraren för aktivitetssekvens**klickar du på **Lägg till**. Peka på **användar tillstånd**och klicka sedan på **avbilda användar tillstånd**. Konfigurera egenskaperna och alternativen för det här steget och klicka sedan på **Använd**. Mer information om de tillgängliga inställningarna finns i [avbilda användar tillstånd](../understand/task-sequence-steps.md#BKMK_CaptureUserState).  

    > [!IMPORTANT]  
    >  När du lägger till det här steget i aktivitetssekvensen anger du också **aktivitetssekvensvariabeln OSDStateStorePath** -variabeln för att ange var du vill lagra användar tillstånds data. Om du lagrar användar tillstånd lokalt ska du inte ange en rotmapp som kan leda till att aktivitetssekvensen inte kan köras. Använd alltid en mapp eller undermapp när du lagrar användardata lokalt. Mer information om den här variabeln finns i [variabler för aktivitetssekvensen](../understand/task-sequence-variables.md#OSDStateStorePath).  

4.  Om du använder en plats för tillståndsmigrering lägger du till steget **Frisläpp tillstånds lager** i aktivitetssekvensen. I **Redigeraren för aktivitetssekvens**klickar du på **Lägg till**. Peka på **användar tillstånd**och klicka sedan på **Frisläpp tillstånds lager**. Konfigurera egenskaperna och alternativen för det här steget och klicka sedan på **Använd**. Mer information om de tillgängliga inställningarna finns i [publicerings tillstånds lager](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

    > [!IMPORTANT]  
    >  Den aktivitetssekvens som körs innan steget **Frisläpp tillstånds lager** måste lyckas innan steget **Frisläpp tillstånds lager** startar.  


 Distribuera den här aktivitetssekvensen för att avbilda användartillståndet på en måldator. Information om hur du distribuerar aktivitetssekvenser finns i [Deploy a task sequence](deploy-a-task-sequence.md).  



## <a name="restore-the-user-state"></a>Återställa användar tillstånd  

 Följ stegen nedan om du vill lägga till steg i aktivitetssekvensen för att återställa användar tillstånd:

1. Välj en aktivitetssekvens i listan **Aktivitetssekvens** och klicka sedan på **Redigera**.  

2. Lägg till steget **Restore User State** i aktivitetssekvensen. I **Redigeraren för aktivitetssekvens**klickar du på **Lägg till**. Peka på **användar tillstånd**och klicka sedan på **Återställ användar tillstånd**. Det här steget upprättar en anslutning till platsen för tillståndsmigrering vid behov. Konfigurera egenskaperna och alternativen för det här steget och klicka sedan på **Använd**. Mer information om de tillgängliga inställningarna finns i [restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState).  

   > [!Important]  
   >  När du använder steget [avbilda användar tillstånd](../understand/task-sequence-steps.md#BKMK_CaptureUserState) med alternativet att **avbilda alla användar profiler med standard alternativ**måste du markera inställningen **Återställ användar profiler för den lokala datorn** i steget **Återställ användar tillstånd** . Annars Miss kommer aktivitetssekvensen.  

   > [!Note]  
   > Om du lagrar användar tillstånd med hjälp av lokala hardlinks och återställningen inte lyckas, kan du manuellt ta bort hardlinks som har skapats för att lagra data. Aktivitetssekvensen kan köra USMTUtils-verktyget för att automatisera åtgärden med [kommando rads steget Kör](../understand/task-sequence-steps.md#BKMK_RunCommandLine) . Om du använder USMTUtils för att ta bort hardlink lägger du till steget [starta om datorn](../understand/task-sequence-steps.md#BKMK_RestartComputer) när du har kört USMTUtils.  

3. Om du använder en plats för tillståndsmigrering för att lagra användar tillstånd lägger du till steget **Frisläpp tillstånds lager** i aktivitetssekvensen. I **Redigeraren för aktivitetssekvens**klickar du på **Lägg till**. Peka på **användar tillstånd**och klicka sedan på **Frisläpp tillstånds lager**. Konfigurera egenskaperna och alternativen för det här steget och klicka sedan på **Använd**. Mer information om de tillgängliga inställningarna finns i [publicerings tillstånds lager](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

   > [!IMPORTANT]  
   >  Den aktivitetssekvens som körs innan steget **Frisläpp tillstånds lager** måste lyckas innan steget **Frisläpp tillstånds lager** startar.  


 Distribuera den här aktivitetssekvensen för att återställa användartillståndet på en måldator. Information om att distribuera aktivitetssekvenser finns i [Deploy a task sequence](deploy-a-task-sequence.md).  



## <a name="next-steps"></a>Nästa steg

[Övervaka aktivitetssekvensdistributionen](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
