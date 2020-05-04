---
title: Skapa startbara media
titleSuffix: Configuration Manager
description: Använd startbara medier i Configuration Manager för att installera en ny version av Windows eller ersätta en dator.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 44c570fc2844093b190e388727dd3799bcbcdb92
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714054"
---
# <a name="create-bootable-media"></a>Skapa startbara media

*Gäller för: Configuration Manager (aktuell gren)*

Startbara medier i Configuration Manager innehåller start avbildningen, valfria för inläsnings kommandon och tillhör ande filer och Configuration Manager filer. Använd förinstallerade medier för följande distributions scenarier för operativ system:  

- [Installera en ny version av Windows på en ny dator (utan operativsystem)](install-new-windows-version-new-computer-bare-metal.md)  

- [Ersätta en befintlig dator och överföra inställningar](replace-an-existing-computer-and-transfer-settings.md)  


## <a name="usage"></a>Användning

Följande processen inträffar när du startar till startbara medier:

1. Mål datorn startar
1. Den ansluter till nätverket
1. Den hämtar följande innehåll från webbplatsen:
    - Den angivna aktivitetssekvensen
    - OS-avbildning
    - Eventuellt annat nödvändigt innehåll

Eftersom aktivitetssekvensen inte finns på mediet kan du ändra aktivitetssekvensen eller innehållet utan att behöva återskapa mediet.

Paketen på startbara medier är inte krypterade. För att se till att paket innehållet skyddas av obehöriga användare bör du vidta lämpliga säkerhets åtgärder. Lägg till exempel till ett lösen ord till mediet.

## <a name="prerequisites"></a>Krav

Innan du skapar startbara media med hjälp av guiden skapa aktivitetssekvens måste du se till att alla dessa villkor är uppfyllda.

### <a name="boot-image"></a>Startavbildning

Tänk på följande om den Start avbildning som du använder i aktivitetssekvensen för att distribuera operativ systemet:

- Start avbildningens arkitektur måste vara lämplig för mål datorns arkitektur. En x64-måldator kan exempelvis starta och köra en x86- eller x64-startavbildning. Men en x86-måldator kan bara starta och köra en x86-startavbildning.
- Kontrol lera att start avbildningen innehåller de nätverks-och lagrings driv rutiner som krävs för att etablera mål datorn.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Skapa en aktivitetssekvens för att distribuera ett operativ system

Som en del av det startbara mediet anger du aktivitetssekvensen för att distribuera operativ systemet. Mer information finns i [skapa en aktivitetssekvens för att installera ett operativ system](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuera allt innehåll som är kopplat till aktivitetssekvensen

Distribuera allt innehåll som aktivitetssekvensen kräver till minst en distributions plats. Det här innehållet omfattar start avbildningen och andra kopplade för inläsnings filer. Guiden samlar in innehållet från distributions platsen när det startbara mediet skapas.

Ditt användar konto måste ha minst **Läs** behörighet till innehålls biblioteket på distributions platsen. Mer information finns i avsnittet [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Förbereda den flyttbara USB-enheten

Om du använder en flyttbar USB-enhet ansluter du den till den dator där du kör guiden skapa aktivitetssekvens. USB-enheten måste kunna identifieras av Windows som en borttagnings enhet. Guiden skriver direkt till USB-enheten när mediet skapas.

### <a name="create-an-output-folder"></a>Skapa en utdatamapp

Innan du kör guiden skapa en aktivitetssekvens för att skapa media för en CD-eller DVD-uppsättning skapar du en mapp för de utdatafiler som skapas. Media som den skapar för en CD-eller DVD-uppsättning skrivs som. ISO-fil direkt i mappen.


## <a name="process"></a>Process

 > [!NOTE]  
 > För PKI-miljöer, eftersom rot certifikat utfärdaren har angetts på den primära platsen, kontrollerar du att det startbara mediet har skapats på den primära platsen. CAS-platsen saknar rot certifikat information för att korrekt kunna skapa startbara media.

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **operativ system**och väljer noden **aktivitetssekvenser** .  

2. På fliken **Start** i menyfliksområdet väljer du **skapa media för aktivitetssekvens**i gruppen **skapa** . Den här åtgärden startar guiden skapa aktivitetssekvens.  

3. På sidan **Välj medietyp** anger du följande alternativ:  

    - Välj **Startbart medium**.  

    - Om du bara vill tillåta att operativ systemet distribueras utan indata från användaren väljer du **Tillåt obevakad distribution av operativ system**.  

        > [!IMPORTANT]  
        > När du väljer det här alternativet behöver användaren inte ange information om nätverks konfigurationen eller för valfria aktivitetssekvenser. Om du konfigurerar mediet för lösen ords skydd uppmanas användaren fortfarande att ange ett lösen ord.  

4. På sidan **medie hantering** anger du ett av följande alternativ:  

    - **Dynamiskt medium**: Tillåt en hanterings plats att omdirigera mediet till en annan hanterings plats, baserat på klientens plats i plats gränserna.  

    - **Platsbaserade Media**: mediet kontaktar bara den angivna hanterings platsen.  

5. På sidan **medietyp** anger du om mediet är en **flyttbar USB-enhet** eller en **CD-/DVD-uppsättning**. Konfigurera sedan följande alternativ:  

    > [!IMPORTANT]  
    > Media använder ett FAT32-fil system. Du kan inte skapa media på en USB-enhet vars innehåll innehåller en fil som är större än 4 GB.  

    - Om du väljer **flyttbar USB-enhet**väljer du den enhet där du vill lagra innehållet.  

        - **Formatera en flyttbar USB-enhet (FAT32) och gör startbara**: som standard låter Configuration Manager förbereda USB-enheten. Många nyare UEFI-enheter kräver en startbar FAT32-partition. Detta format begränsar dock också storleken på filer och den övergripande kapaciteten för enheten. Inaktivera det här alternativet om du redan har formaterat och konfigurerat den flyttbara enheten.

    - Om du väljer **CD/DVD-uppsättning**anger du mediets kapacitet (**medie storlek**) och namn och sökväg för utdatafilen (**medie fil**). Guiden skriver utdatafilerna till den här platsen. Exempelvis: `\\servername\folder\outputfile.iso`  

        Om mediets kapacitet är för liten för att lagra hela innehållet skapas flera filer. Sedan måste du lagra innehållet på flera CD-eller DVD-skivor. När det krävs flera mediafiler Configuration Manager lägger till ett sekvensnummer till namnet på alla utdatafiler som skapas.  

        > [!IMPORTANT]  
        > Om du väljer en befintlig .iso-avbildning raderar guiden för aktivitetssekvensmedium den avbildningen från enheten eller resursen så fort du går vidare till nästa sida i guiden. Den befintliga avbildningen tas bort även om du avbryter guiden.  

    - **Mellanlagringsplats**<!--1359388-->: Processen för att skapa media kan kräva mycket temporärt enhets utrymme. Som standard liknar den här platsen följande sökväg: `%UserProfile%\AppData\Local\Temp`. Från och med version 1902, för att ge dig större flexibilitet med var de här temporära filerna ska lagras, ändra värdet till en annan enhet och sökväg.  

    - **Medie etikett**<!--1359388-->: Från och med version 1902 lägger du till en etikett i mediet för aktivitetssekvenser. Med den här etiketten kan du bättre identifiera mediet när du har skapat det. Standardvärdet är `Configuration Manager`. Det här textfältet visas på följande platser:  

        - Om du monterar en ISO-fil visas den här etiketten som namnet på den monterade enheten i Windows.  

        - Om du formaterar en USB-enhet används de första 11 tecknen i etiketten som namn  

        - Configuration Manager skriver en textfil som kallas `MediaLabel.txt` för roten på mediet. Som standard innehåller filen en enskild rad med text: `label=Configuration Manager`. Om du anpassar etiketten för Media använder den här raden den anpassade etiketten i stället för standardvärdet.  

    - **Inkludera filen autorun. inf på mediet**<!-- 4090666 -->: Från och med version 1906 lägger Configuration Manager inte till en autorun. inf-fil som standard. Den här filen blockeras vanligt vis av program mot skadlig kod. Mer information om AutoRun-funktionen i Windows finns i [skapa ett autorun-aktiverat CD-ROM-program](https://docs.microsoft.com/windows/desktop/shell/autoplay). Om det fortfarande behövs för ditt scenario väljer du det här alternativet för att inkludera filen.  

6. På sidan **säkerhet** anger du följande alternativ:  

    - **Aktivera stöd för okända datorer**: Tillåt mediet att distribuera ett operativ system till en dator som inte hanteras av Configuration Manager. Det finns ingen post för de här datorerna i Configuration Managers databasen. Mer information finns i [förbereda för okända dator distributioner](../get-started/prepare-for-unknown-computer-deployments.md).  

    - **Skydda mediet med ett lösen ord**: Ange ett starkt lösen ord för att skydda mediet från obehörig åtkomst. När du anger ett lösenord måste användaren ange lösenordet för att använda startmediet.  

        > [!IMPORTANT]  
        > Som säkerhetsregel bör du alltid tilldela ett lösenord för att skydda startmediet.  

    - För HTTP-kommunikation väljer du **Skapa självsignerat medie certifikat**. Ange sedan start-och förfallo datum för certifikatet.  
    
      > [!NOTE]  
      > Om du väljer det här alternativet kommer HTTPS-hanterings platser inte att vara tillgängliga för val på sidan **Start avbildning** i den här guiden.

    - För HTTPS-kommunikation väljer du **Importera PKI-certifikat**. Ange sedan det certifikat som ska importeras och dess lösen ord.  

        Mer information om det här klient certifikatet som används av start avbildningar finns i [krav för PKI-certifikat](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **Mappning mellan användare och enhet**: om du vill stödja den användarvänliga hanteringen i Configuration Manager anger du hur du vill att mediet ska koppla användare till mål datorn. Mer information om hur operativ system distribution stöder mappning mellan användare och enhet finns i [associera användare med en måldator](../get-started/associate-users-with-a-destination-computer.md).  

        - **Tillåt mappning mellan användare och enhet med automatiskt godkännande**: mediet kopplar automatiskt användare till mål datorn. Den här funktionen baseras på åtgärderna för den aktivitetssekvens som distribuerar operativ systemet. I det här scenariot skapar aktivitetssekvensen en relation mellan de angivna användarna och mål datorn när operativ systemet distribueras till mål datorn.  

        - **Tillåt mappning mellan användare och enhet väntar på administratörs godkännande**: mediet associerar användare med mål datorn när godkännande har beviljats. Den här funktionen baseras på omfånget för den aktivitetssekvens som distribuerar operativ systemet. I det här scenariot skapar aktivitetssekvensen en relation mellan de angivna användarna och mål datorn, men väntar på godkännande från en administrativ användare innan operativ systemet distribueras.  

        - **Tillåt inte mappning mellan användare och enhet**: mediet kopplar inte användare till mål datorn. I det här scenariot associerar aktivitetssekvensen inte användare med mål datorn när operativ systemet distribueras.  

7. På sidan **Start avbildning** anger du följande alternativ:  

    > [!IMPORTANT]  
    > Arkitekturen för den Start avbildning som du distribuerar måste vara lämplig för mål datorns arkitektur. En x64-måldator kan exempelvis starta och köra en x86- eller x64-startavbildning. Men en x86-måldator kan bara starta och köra en x86-startavbildning.  

    - **Start avbildning**: Välj den Start avbildning som ska starta mål datorn.  

    - **Distributions plats**: Välj den distributions plats som har start avbildningen. Guiden hämtar startavbildningen från distributionsplatsen och skriver den till mediet.  

        > [!NOTE]  
        > Ditt användar konto måste ha minst **Läs** behörighet till innehålls biblioteket på distributions platsen.  

    - **Hanterings plats**: endast för *platsbaserade medier*väljer du en hanterings plats från en primär plats.  

    - **Associerade hanterings platser**: endast för *dynamiskt medium*väljer du den primära platsens hanterings platser som ska användas och en prioritetsordning för den inledande kommunikationen.  
    
        > [!NOTE]  
        > HTTPS-aktiverade hanterings platser visas bara när ett PKI-certifikat anges på sidan **säkerhet** i guiden.  

8. På sidan **anpassning** anger du följande alternativ:  

    - Lägg till variabler som används i aktivitetssekvensen.  

    - **Aktivera för inläsnings kommando**: Ange eventuella för inläsnings kommandon som du vill köra innan aktivitetssekvensen körs. För inläsnings kommandon är ett skript eller en körbar fil som kan användas för att interagera med användaren i Windows PE innan aktivitetssekvensen körs. Mer information finns i [för inläsnings kommandon för media i aktivitetssekvensen](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > När ett medium skapas skriver aktivitetssekvensen paket-ID och för inläsnings kommando rad, inklusive värdet för alla variabler i aktivitetssekvensen, till **CreateTSMedia. log** -filen på den dator som kör Configuration Manager-konsolen. Du kan granska loggfilen och kontrollera värdet för aktivitetssekvensvariablerna.  

        Om för inläsnings kommandot kräver innehåll väljer du alternativet för att **inkludera filer för för inläsnings kommandot**.  

9. Slutför guiden.  


## <a name="alternate-method"></a>Alternativ metod

Du kan skapa startbara media på en flyttbar USB-enhet när enheten inte är ansluten till datorn som kör Configuration Manager-konsolen.

1. [Skapa start mediet för aktivitetssekvensen](#process). På sidan **medietyp** väljer du **CD/DVD-uppsättning**. Guiden skriver utdatafilerna till den plats som du anger. Till exempel: `\\servername\folder\outputfile.iso`.  

2. Förbered den flyttbara USB-enheten. Enheten måste vara formaterad, Tom och startbar.

3. Montera ISO-filen från resurs platsen och överför filerna från ISO till USB-enheten.


## <a name="next-steps"></a>Nästa steg

[Använda startbara media för att distribuera Windows via nätverket](use-bootable-media-to-deploy-windows-over-the-network.md)  
