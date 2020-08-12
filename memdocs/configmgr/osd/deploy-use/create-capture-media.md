---
title: Skapa avbildningsmedia
titleSuffix: Configuration Manager
description: Använd avbildnings medier i Configuration Manager för att avbilda en operativ system avbildning från en referens dator.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d85ab7e9d66c1206c6741117d7b379c998078708
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125380"
---
# <a name="create-capture-media"></a>Skapa avbildningsmedia

*Gäller för: Configuration Manager (aktuell gren)*

Genom att avbilda media i Configuration Manager kan du avbilda en operativ system avbildning från en referens dator. Avbildnings medier innehåller den Start avbildning som startar referens datorn och den aktivitetssekvens som avbildar operativ system avbildningen. Använd avbildnings medier för scenariot för att [skapa en aktivitetssekvens för att avbilda ett operativ system](create-a-task-sequence-to-capture-an-operating-system.md).  


## <a name="prerequisites"></a>Förutsättningar

Innan du skapar avbildnings medier med hjälp av guiden skapa aktivitetssekvens måste du se till att alla dessa villkor är uppfyllda.

### <a name="boot-image"></a>Startavbildning

Tänk på följande om den Start avbildning som du använder i aktivitetssekvensen för att distribuera operativ systemet:

- Start avbildningens arkitektur måste vara lämplig för mål datorns arkitektur. En x64-måldator kan exempelvis starta och köra en x86- eller x64-startavbildning. Men en x86-måldator kan bara starta och köra en x86-startavbildning.
- Kontrol lera att start avbildningen innehåller de nätverks-och lagrings driv rutiner som krävs för att etablera mål datorn.

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuera allt innehåll som är kopplat till aktivitetssekvensen

Distribuera allt innehåll som aktivitetssekvensen kräver till minst en distributions plats. Det här innehållet omfattar start avbildningen, OS-avbildningen och andra tillhör ande filer. Guiden samlar in innehållet från distributions platsen när avbildnings mediet skapas.

Ditt användar konto måste ha minst **Läs** behörighet till innehålls biblioteket på distributions platsen. Mer information finns i avsnittet [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Förbereda den flyttbara USB-enheten

Om du använder en flyttbar USB-enhet ansluter du den till den dator där du kör guiden skapa aktivitetssekvens. USB-enheten måste kunna identifieras av Windows som en borttagnings enhet. Guiden skriver direkt till USB-enheten när mediet skapas.

### <a name="create-an-output-folder"></a>Skapa en utdatamapp

Innan du kör guiden skapa en aktivitetssekvens för att skapa media för en CD-eller DVD-uppsättning skapar du en mapp för de utdatafiler som skapas. Media som den skapar för en CD-eller DVD-uppsättning skrivs som. ISO-fil direkt i mappen.


## <a name="process"></a>Process

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **operativ system**och väljer noden **aktivitetssekvenser** .  

2. På fliken **Start** i menyfliksområdet väljer du **skapa media för aktivitetssekvens**i gruppen **skapa** . Den här åtgärden startar guiden skapa aktivitetssekvens.  

3. På sidan **Välj medietyp** väljer du **avbilda Media**.  

4. På sidan **medietyp** anger du om mediet är en **flyttbar USB-enhet** eller en **CD-/DVD-uppsättning**. Konfigurera sedan följande alternativ:  

    > [!IMPORTANT]  
    > Media använder ett FAT32-fil system. Du kan inte skapa media på en USB-enhet vars innehåll innehåller en fil som är större än 4 GB.  

    - Om du väljer **flyttbar USB-enhet**väljer du den enhet där du vill lagra innehållet.  

        - **Formatera en flyttbar USB-enhet (FAT32) och gör startbara**: som standard låter Configuration Manager förbereda USB-enheten. Många nyare UEFI-enheter kräver en startbar FAT32-partition. Detta format begränsar dock också storleken på filer och den övergripande kapaciteten för enheten. Inaktivera det här alternativet om du redan har formaterat och konfigurerat den flyttbara enheten.

    - Om du väljer **CD/DVD-uppsättning**anger du mediets kapacitet (**medie storlek**) och namn och sökväg för utdatafilen (**medie fil**). Guiden skriver utdatafilerna till den här platsen. Exempel: `\\servername\folder\outputfile.iso`  

        Om mediets kapacitet är för liten för att lagra hela innehållet skapas flera filer. Sedan måste du lagra innehållet på flera CD-eller DVD-skivor. När det krävs flera mediafiler Configuration Manager lägger till ett sekvensnummer till namnet på alla utdatafiler som skapas.  

        > [!IMPORTANT]  
        > Om du väljer en befintlig .iso-avbildning raderar guiden för aktivitetssekvensmedium den avbildningen från enheten eller resursen så fort du går vidare till nästa sida i guiden. Den befintliga avbildningen tas bort även om du avbryter guiden.  

    - **Mellanlagringsplats**<!--1359388-->: Processen för att skapa media kan kräva mycket temporärt enhets utrymme. Som standard liknar den här platsen följande sökväg: `%UserProfile%\AppData\Local\Temp` . Från och med version 1902, för att ge dig större flexibilitet med var de här temporära filerna ska lagras, ändra värdet till en annan enhet och sökväg.  

    - **Medie etikett**<!--1359388-->: Från och med version 1902 lägger du till en etikett i mediet för aktivitetssekvenser. Med den här etiketten kan du bättre identifiera mediet när du har skapat det. Standardvärdet är `Configuration Manager`. Det här textfältet visas på följande platser:  

        - Om du monterar en ISO-fil visas den här etiketten som namnet på den monterade enheten i Windows.  

        - Om du formaterar en USB-enhet används de första 11 tecknen i etiketten som namn  

        - Configuration Manager skriver en textfil som kallas `MediaLabel.txt` för roten på mediet. Som standard innehåller filen en enskild rad med text: `label=Configuration Manager` . Om du anpassar etiketten för Media använder den här raden den anpassade etiketten i stället för standardvärdet.  

    - **Inkludera filen autorun. inf på mediet**<!-- 4090666 -->: Från och med version 1906 lägger Configuration Manager inte till en autorun. inf-fil som standard. Den här filen blockeras vanligt vis av program mot skadlig kod. Mer information om AutoRun-funktionen i Windows finns i [skapa ett autorun-aktiverat CD-ROM-program](https://docs.microsoft.com/windows/desktop/shell/autoplay). Om det fortfarande behövs för ditt scenario väljer du det här alternativet för att inkludera filen.  

5. På sidan **Start avbildning** anger du följande alternativ:  

    > [!IMPORTANT]  
    > Arkitekturen för den Start avbildning som du distribuerar måste vara lämplig för mål datorns arkitektur. En x64-måldator kan exempelvis starta och köra en x86- eller x64-startavbildning. Men en x86-måldator kan bara starta och köra en x86-startavbildning.  

    - **Start avbildning**: Välj den Start avbildning som ska starta mål datorn.  

    - **Distributions plats**: Välj den distributions plats som har start avbildningen. Guiden hämtar startavbildningen från distributionsplatsen och skriver den till mediet.  

        > [!NOTE]  
        > Ditt användar konto måste ha minst **Läs** behörighet till innehålls biblioteket på distributions platsen.  

6. Slutför guiden.  


## <a name="next-steps"></a>Nästa steg

[Skapa en aktivitetssekvens för att avbilda ett operativsystem](create-a-task-sequence-to-capture-an-operating-system.md)
