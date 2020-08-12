---
title: Hantera användartillstånd
titleSuffix: Configuration Manager
description: Configuration Manager använder User State Migration Tool för att avbilda och återställa användar tillstånds data i distributions scenarier för operativ system.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0a720c68fc705187dedb6ff04fc3898a8b0b21c8
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124371"
---
# <a name="manage-user-state-in-configuration-manager"></a>Hantera användar tillstånd i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan använda Configuration Manager aktivitetssekvenser för att avbilda och återställa användar tillstånds data vid distributions scenarier för operativ system där du vill behålla användar statusen för det aktuella operativ systemet. Till exempel:  

- Distributioner där du vill avbilda användartillståndet på en dator för att återställa det på en annan.  

- Distributioner av uppdateringar där du vill avbilda och återställa användartillståndet på samma dator.  

Configuration Manager använder User State Migration Tool (USMT) 10,0 för att hantera migreringen av användar tillstånds data från en käll dator till en måldator när installationen av operativ systemet har slutförts. Mer information om vanliga migreringsscenarier för USMT 10.0 finns i  [Vanliga migreringsscenarier](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios).

Använd följande avsnitt för att få hjälp att avbilda och återställa användar data.

## <a name="store-user-state-data"></a><a name="BKMK_StoringUserData"></a> Lagra användartillståndsdata

 När du avbildar användartillstånd kan du lagra användartillståndsdata på måldatorn eller på en tillståndsmigreringsplats. Om du vill lagra användar tillstånd på en plats för migrering av användar tillstånd måste du använda en Configuration Manager plats system server som är värd för plats system rollen för tillståndsmigrering. Om du vill lagra användartillståndet på måldatorn måste du konfigurera aktivitetssekvensen för att lagra informationen lokalt med hjälp av länkar.

> [!NOTE]
> Länkarna som används för att lagra användartillståndet lokalt kallas hårda länkar. Hårda länkar är en funktion i USMT 10.0 som genomsöker datorn efter användarfiler och inställningar och sedan skapar en katalog med hårda länkar till filerna. De hårda länkarna används sedan för att återställa användardata när det nya operativsystemet har distribuerats.

> [!IMPORTANT]
> Du kan inte använda en tillståndsmigreringplats och samtidigt använda hårda länkar för att lagra användartillståndsdata.

När informationen om användartillståndet samlas in, kan den lagras på ett av de följande sätten:  

- Du kan lagra användartillståndsdata genom att konfigurera en tillståndsmigreringsplats. Aktivitetssekvensen **Avbilda** gör att alla data skickas till tillståndsmigreringsplatsen. Efter att operativ systemet har distribuerats **hämtar aktivitetssekvensen data** och återställer användarens tillstånd på mål datorn.  

- Du kan lagra användartillståndsdata lokalt på en viss plats. I det här scenariot kopierar aktivitetssekvensen för **avbildningen** användar data till en angiven plats på mål datorn. Efter att operativ systemet har distribuerats hämtas användar data från den platsen med hjälp av aktivitetssekvensen **Återställ** .  

- Du kan ange hårda länkar som kan användas för att återställa alla användardata till den ursprungliga platsen. I detta scenario blir alla användartillståndsdata kvar på hårddisken när det gamla operativsystemet tas bort. Efter att operativsystemet har distribuerats används de hårda länkarna för att återställa alla användartillståndsdata till den ursprungliga platsen med hjälp av aktivitetssekvensen **Återställ** .  

### <a name="store-user-data-on-a-state-migration-point"></a><a name="BKMK_UserDataSMP"></a> Lagra användardata på en tillståndsmigreringsplats

 Gör så här för att lagra användartillståndsdata på en tillståndsmigreringsplats:  

1. [Configure a state migration point](#BKMK_StateMigrationPoint) för att lagra användartillståndsdata.  

1. [Create a computer association](#BKMK_ComputerAssociation) mellan källdatorn och måldatorn. Du måste skapa kopplingen innan du avbildar användartillståndet på källdatorn.  

1. [Skapa en aktivitetssekvens för att avbilda och återställa användar tillstånd](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Mer specifikt måste du lägga till följande steg i aktivitetssekvensen för att avbilda användar data från en dator, lagra användar datum på en plats för tillståndsmigrering och återställa användar data till en dator:  

    - [Request State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore) för att begära åtkomst till en tillståndsmigreringsplats vid avbildning av tillståndet på en dator eller återställning av tillståndet på en dator.  

    - [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) för att lagra användartillståndsdata på tillståndsmigreringsplatsen.  

    - [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) för att återställa användartillståndet på måldatorn genom att hämta data från en migreringsplats för användartillstånd.  

    - [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) för att avisera tillståndsmigreringsplatsen att avbildnings- eller återställningsåtgärden har slutförts.  

### <a name="store-user-data-locally"></a><a name="BKMK_UserDataDestination"></a> Lagra användardata lokalt

 Gör så här om du vill lagra användartillståndsdata lokalt:  

- [Skapa en aktivitetssekvens för att avbilda och återställa användar tillstånd](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Mer specifikt måste du lägga till följande steg i aktivitetssekvensen för att avbilda användar data från en dator och återställa användar data till en dator med hjälp av hårda länkar.

  - [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) för att avbilda och lagra användartillståndsdata i en lokal mapp med hjälp av hårda länkar.  

  - [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) för att återställa användartillståndet på måldatorn genom att hämta data med hjälp av hårda länkar.  

    > [!NOTE]
    > De användartillståndsdata som de hårda länkar hänvisar till är kvar på datorn när det gamla operativsystemet har tagits bort genom aktivitetssekvensen. Det här är de data som används för att återställa användartillståndet när det nya operativsystemet distribueras.  

## <a name="configure-a-state-migration-point"></a><a name="BKMK_StateMigrationPoint"></a>Konfigurera en plats för tillståndsmigrering

Tillståndsmigreringsplatsen använder tillståndsdata som har avbildats på en dator och därefter återställts på en annan dator. När du avbildar användarinställningar för ett operativsystem på samma dator, t.ex. en distribution där du uppdaterar operativsystemet på måldatorn, kan du lagra data på samma dator med hårda länkar eller använda en tillståndsmigreringsplats. För vissa dator distributioner skapar Configuration Manager automatiskt en association mellan tillstånds lagret och mål datorn när du skapar tillstånds lagret. Du kan konfigurera en tillståndsmigreringsplats för att lagra användartillståndsdata på följande sätt:  

- Använd **Guiden skapa platssystemserver** för att skapa en ny platssystemserver för tillståndsmigreringsplatsen.  

- Använd **Guiden lägg till platssystemroller** för att lägga till en tillståndsmigreringsplats i en befintlig server.  

  När du använder guiderna uppmanas du att ange följande information om tillståndsmigreringsplatsen:  

- Mapparna där användartillståndsdata ska lagras.  

- Högsta antal klienter som kan lagra data på tillståndsmigreringsplatsen.  

- Minsta lediga utrymme på tillståndsmigreringsplatsen för lagring av användartillståndsdata.  

- Borttagningsprincip för rollen. Du kan ange att alla användartillståndsdata ska raderas omedelbart efter det att de har återställts på en dator eller efter ett visst antal dagar efter det att de har återställts på en dator.  

- Huruvida tillståndsmigreringsplatsen bara svarar på förfrågningar om att återställa användartillståndsdata. När du aktiverar det här alternativet kan du inte använda tillståndsmigreringsplatsen för att lagra användartillståndsdata.  

  Mer information om tillståndsmigreringsplatsen och hur du konfigurerar den finns i [State migration point](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="create-a-computer-association"></a><a name="BKMK_ComputerAssociation"></a>Skapa en dator koppling

Skapa en datorkoppling för att definiera ett förhållande mellan en källdator och en måldator när du installerar ett operativsystem på ny maskinvara och vill avbilda och återställa inställningar för användardata. Käll datorn är en befintlig dator som Configuration Manager hanterar. När du distribuerar det nya operativsystemet på måldatorn innehåller källdatorn det användartillstånd som migreras till måldatorn.  

> [!NOTE]  
> Det finns inte stöd för att skapa en dator koppling mellan datorer som finns i en Configuration Manager överordnad plats med datorer som finns i en underordnad plats. Dator kopplingarna är sitespecifika och replikeras inte.  

### <a name="to-create-a-computer-association"></a>Skapa en datorkoppling

1. Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

1. I arbetsytan **Tillgångar och efterlevnad** klickar du på **Migrering av användartillstånd**.  

1. På fliken **Start** i gruppen **Skapa** klickar du på **Skapa datorassociation**.  

1. På fliken **Datorkoppling** i dialogrutan **Egenskaper för datorkoppling** anger du den källdator där det användartillstånd som ska avbildas finns, och den måldator dit användartillståndsinformationen ska återställas.  

1. På fliken **Användarkonton** anger du de användarkonton som ska migreras till måldatorn. Ange en av följande inställningar:  

    - **Fånga och återställ alla användarkonton**: Med den här inställningen avbildas och återställs alla användarkonton. Använd den här inställningen om du vill skapa flera kopplingar till samma källdator.  

    - **Fånga alla användarkonton och återställ angivna konton**: Med den här inställningen avbildas alla användarkonton på källdatorn och bara de konton som du har angett på måldatorn återställs. Du kan också använda den här inställningen när vill skapa flera kopplingar till samma källdator.  

    - **Fånga och återställ angivna användarkonton**: Med den här inställningen avbildas och återställs endast de konton du anger. Du kan inte skapa flera kopplingar till samma källdator när du har valt den här inställningen.  

## <a name="restore-user-state-data-when-an-operating-system-deployment-fails"></a><a name="BKMK_MigrationFails"></a>Återställa användar tillstånds data när det inte går att distribuera operativ system

Om distributionen av operativsystemet misslyckas använder du USMT 10.0-funktionen LoadState för att hämta de användartillståndsdata som avbildades under distributionsprocessen. Detta inbegriper data som har lagrats på en tillståndsmigreringsplats och data som har sparats lokalt på en måldator. Mer information om den här USMT-funktionen finns i [LoadState Syntax (Syntax för LoadState)](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).
