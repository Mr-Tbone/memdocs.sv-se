---
title: Skapa fristående media
titleSuffix: Configuration Manager
description: Använd fristående media för att distribuera operativ systemet på en dator utan någon nätverks anslutning.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c8710c50dc2feabebd7e8f0f84ac49b3b0dd35c
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068029"
---
# <a name="create-stand-alone-media"></a>Skapa fristående media

*Gäller för: Configuration Manager (aktuell gren)*

Fristående media i Configuration Manager innehåller allt som krävs för att distribuera operativ systemet på en dator utan någon nätverks anslutning.

Använd fristående media med följande distributions scenarier för operativ system:  

- [Uppdatera en befintlig dator med en ny version av Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Installera en ny version av Windows på en ny dator (utan operativsystem)](install-new-windows-version-new-computer-bare-metal.md)  

- [Uppgradera Windows till den senaste versionen](upgrade-windows-to-the-latest-version.md)  


## <a name="usage"></a>Användning

Fristående media innehåller den aktivitetssekvens som automatiserar stegen för att installera operativ systemet och allt annat nödvändigt innehåll. Det här innehållet omfattar start avbildningen, OS-avbildningen och enhets driv rutinerna. Eftersom det fristående mediet lagrar allt för att distribuera operativ systemet kräver det mer disk utrymme än vad som krävs för andra typer av medier.

När du skapar fristående media på en central administrations plats hämtar klienten den tilldelade plats koden från Active Directory. Fristående media som skapas på underordnade platser tilldelas automatiskt till klienten plats koden för platsen.  


## <a name="prerequisites"></a>Krav

Innan du skapar fristående media med hjälp av guiden skapa aktivitetssekvens måste du se till att alla dessa villkor är uppfyllda.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Skapa en aktivitetssekvens för att distribuera ett operativ system

Som en del av det fristående mediet anger du aktivitetssekvensen för att distribuera ett operativ system. Mer information finns i [skapa en aktivitetssekvens för att installera ett operativ system](create-a-task-sequence-to-install-an-operating-system.md).

#### <a name="unsupported-actions-for-stand-alone-media"></a>Åtgärder som inte stöds för fristående media

Följande åtgärder stöds inte för fristående media:

- Steget [Använd driv rutiner automatiskt](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) i aktivitetssekvensen. Fristående media stöder inte automatisk tillämpning av enhets driv rutiner från driv rutins katalogen. Använd steget [Använd driv rutins paket](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) för att göra en angiven uppsättning driv rutiner tillgängliga för installationsprogrammet för Windows.  

- Steget [Ladda ned paket innehåll](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) i aktivitetssekvensen. Hanterings plats informationen är inte tillgänglig på fristående media, så steget kan inte försöka räkna upp innehålls platser.  

- Installera programuppdateringar.  

- Installera program vara innan du distribuerar operativ systemet.  

- Anpassade aktivitetssekvenser för distributioner som inte är operativ system.  

- Associera användare med måldatorn som stöd för mappning mellan användare och enhet.  

- Dynamiskt paket installeras via steget [installera paket](../understand/task-sequence-steps.md#BKMK_InstallPackage) .  

- Dynamiska program installeras via steget [installera program](../understand/task-sequence-steps.md#BKMK_InstallApplication) .

- Alternativet **Använd för produktions klient paket när det är tillgängligt** i steget **Installera Windows och ConfigMgr** . Mer information om den här inställningen finns i [Installera Windows och ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

> [!NOTE]  
> Ett fel kan inträffa om aktivitetssekvensen innehåller steget [installera paket](../understand/task-sequence-steps.md#BKMK_InstallPackage) och du skapar fristående media på en central administrations plats. Den centrala administrations platsen har inte de nödvändiga klient konfigurations principerna. Dessa principer krävs för att aktivera program distributions agenten när aktivitetssekvensen körs. Följande fel kan visas i filen **CreateTSMedia. log** :  
>
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`
>
> För fristående media som innefattar steget **installera paket** skapar du fristående media på en primär plats som har program distributions agenten aktive rad.
>
> Du kan också använda ett anpassat steg för [körnings kommando raden](../understand/task-sequence-steps.md#BKMK_RunCommandLine) . Lägg till den efter steget installera [Windows och ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) och före det första **installera paket** -steget. Steget **Kör kommando rad** kör följande WMIC-kommando för att aktivera program distributions agenten före det första installera paket-steget:  
>
> `WMIC /namespace:\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuera allt innehåll som är kopplat till aktivitetssekvensen

Distribuera allt innehåll som aktivitetssekvensen kräver till minst en distributions plats. Det här innehållet omfattar start avbildningen, OS-avbildningen och andra tillhör ande filer. Guiden samlar in innehållet från distributions platsen när mediet skapas.

Ditt användar konto måste ha minst **Läs** behörighet till innehålls biblioteket på distributions platsen. Mer information finns i avsnittet [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Förbereda den flyttbara USB-enheten

Om du använder en flyttbar USB-enhet ansluter du den till den dator där du kör guiden skapa aktivitetssekvens. USB-enheten måste kunna identifieras av Windows som en borttagnings enhet. Guiden skriver direkt till USB-enheten när mediet skapas.

Fristående media använder ett FAT32-filsystem. Du kan inte skapa fristående media på en flyttbar USB-enhet vars innehåll innehåller en fil som är större än 4 GB.

### <a name="create-an-output-folder"></a>Skapa en utdatamapp

Innan du kör guiden skapa en aktivitetssekvens för att skapa media för en CD-eller DVD-uppsättning skapar du en mapp för de utdatafiler som skapas. Media som den skapar för en CD-eller DVD-uppsättning skrivs som. ISO-fil direkt i mappen.


## <a name="process"></a>Process

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **operativ system**och väljer noden **aktivitetssekvenser** .  

2. På fliken **Start** i menyfliksområdet väljer du **skapa media för aktivitetssekvens**i gruppen **skapa** . Den här åtgärden startar guiden skapa aktivitetssekvens.  

3. På sidan **Välj medietyp** anger du följande alternativ:  

    - Välj **fristående media**.  

    - Om du bara vill tillåta att operativ systemet distribueras utan indata från användaren väljer du **Tillåt obevakad distribution av operativ system**.  

        > [!IMPORTANT]  
        > När du väljer det här alternativet behöver användaren inte ange information om nätverks konfigurationen eller för valfria aktivitetssekvenser. Om du konfigurerar mediet för lösen ords skydd uppmanas användaren fortfarande att ange ett lösen ord.  

4. På sidan **medietyp** anger du om mediet är en **flyttbar USB-enhet** eller en **CD-/DVD-uppsättning**. Konfigurera sedan följande alternativ:  

    > [!IMPORTANT]  
    > Media använder ett FAT32-fil system. Du kan inte skapa media på en USB-enhet vars innehåll innehåller en fil som är större än 4 GB.  

    - Om du väljer **flyttbar USB-enhet**väljer du den enhet där du vill lagra innehållet.  

        - **Formatera en flyttbar USB-enhet (FAT32) och gör startbara**: som standard låter Configuration Manager förbereda USB-enheten. Många nyare UEFI-enheter kräver en startbar FAT32-partition. Detta format begränsar dock också storleken på filer och den övergripande kapaciteten för enheten. Inaktivera det här alternativet om du redan har formaterat och konfigurerat den flyttbara enheten.

    - Om du väljer **CD/DVD-uppsättning**anger du mediets kapacitet (**medie storlek**) och namn och sökväg för utdatafilen (**medie fil**). Guiden skriver utdatafilerna till den här platsen. Exempelvis: `\\servername\folder\outputfile.iso`  

        Om mediets kapacitet är för liten för att lagra hela innehållet skapas flera filer. Sedan måste du lagra innehållet på flera CD-eller DVD-skivor. När det krävs flera mediafiler Configuration Manager lägger till ett sekvensnummer till namnet på alla utdatafiler som skapas.  

        Om du distribuerar ett program tillsammans med operativ systemet och programmet inte får plats på ett enda medium, Configuration Manager lagra programmet på flera media. När det fristående mediet körs Configuration Manager, uppmanas användaren att ange nästa medium där programmet lagras.  

        > [!IMPORTANT]  
        > Om du väljer en befintlig .iso-avbildning raderar guiden för aktivitetssekvensmedium den avbildningen från enheten eller resursen så fort du går vidare till nästa sida i guiden. Den befintliga avbildningen tas bort även om du avbryter guiden.  

    - **Mellanlagringsplats**<!--1359388-->: Processen för att skapa media kan kräva mycket temporärt enhets utrymme. Som standard liknar den här platsen följande sökväg: `%UserProfile%\AppData\Local\Temp` . Från och med version 1902, för att ge dig större flexibilitet med var de här temporära filerna ska lagras, ändra värdet till en annan enhet och sökväg.  

    - **Medie etikett**<!--1359388-->: Från och med version 1902 lägger du till en etikett i mediet för aktivitetssekvenser. Med den här etiketten kan du bättre identifiera mediet när du har skapat det. Standardvärdet är `Configuration Manager`. Det här textfältet visas på följande platser:  

        - Om du monterar en ISO-fil visas den här etiketten som namnet på den monterade enheten i Windows.  

        - Om du formaterar en USB-enhet används de första 11 tecknen i etiketten som namn  

        - Configuration Manager skriver en textfil som kallas `MediaLabel.txt` för roten på mediet. Som standard innehåller filen en enskild rad med text: `label=Configuration Manager` . Om du anpassar etiketten för Media använder den här raden den anpassade etiketten i stället för standardvärdet.  

    - **Inkludera filen autorun. inf på mediet**<!-- 4090666 -->: Från och med version 1906 lägger Configuration Manager inte till en autorun. inf-fil som standard. Den här filen blockeras vanligt vis av program mot skadlig kod. Mer information om AutoRun-funktionen i Windows finns i [skapa ett autorun-aktiverat CD-ROM-program](/windows/desktop/shell/autoplay). Om det fortfarande behövs för ditt scenario väljer du det här alternativet för att inkludera filen.  

5. På sidan **säkerhet** anger du följande alternativ:

    - **Skydda mediet med ett lösen ord**: Ange ett starkt lösen ord för att skydda mediet från obehörig åtkomst. När du anger ett lösen ord måste användaren ange lösen ordet för att använda mediet.  

        > [!IMPORTANT]  
        > Av säkerhets skäl bör du alltid tilldela ett lösen ord för att skydda mediet.  
        >
        > På fristående media krypterar den bara stegen i aktivitetssekvensen och deras variabler. Det krypterar inte det återstående innehållet på mediet. Ta inte med känslig information i aktivitetssekvenser. Lagra och implementera all känslig information med hjälp av variabler i aktivitetssekvensen.  

    - **Välj datum intervall för att det här fristående mediet ska vara giltigt**: Ange valfria start-och förfallo datum för mediet. Den här inställningen är avaktiverad som standard. Datumen jämförs med system klockan på datorn innan det fristående mediet körs. När system tiden infaller före start tiden eller senare än förfallo tiden startar inte det fristående mediet. Dessa alternativ är också tillgängliga med hjälp av PowerShell-cmdleten [New-CMStandaloneMedia](/powershell/module/configurationmanager/new-cmstandalonemedia?view=sccm-ps) .  

6. På sidan **fristående CD/DVD** väljer du den aktivitetssekvens som distribuerar operativ systemet. Du kan bara välja de aktivitetssekvenser som är associerade med en start avbildning. Verifiera listan över innehåll som aktivitetssekvensen refererar till.  

    - **Identifiera associerade program beroenden och Lägg till dem i det här mediet**: Lägg även till innehåll till mediet för program beroenden.  

        > [!TIP]  
        > Om förväntade program beroenden inte visas avmarkerar du det här alternativet för att uppdatera listan.  

7. På sidan **Välj program** anger du ytterligare program innehåll som ska ingå som en del av medie filen.  

8. På sidan **Välj paket** anger du ytterligare paket innehåll som ska ingå som en del av medie filen.  

9. På sidan **Välj driv rutins paket** anger du ytterligare driv rutins paket innehåll som ska ingå som en del av medie filen.  

10. På sidan **distributions platser** anger du de distributions platser som innehåller det begärda innehållet.  

    Configuration Manager visar endast distributions platser som har innehållet. Distribuera allt innehåll som är kopplat till aktivitetssekvensen till minst en distributions plats innan du fortsätter. När du har distribuerat innehållet uppdaterar du distributions plats listan. Ta bort eventuella distributions platser som du redan har valt på den här sidan, gå till föregående sida och sedan tillbaka till sidan **distributions platser** . Du kan också starta om guiden. Mer information finns i [distribuera innehåll som refereras till av en aktivitetssekvens](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) och [Hantera innehåll och innehålls infrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

11. På sidan **anpassning** anger du följande alternativ:  

    - Lägg till variabler som används i aktivitetssekvensen.  

    - **Aktivera för inläsnings kommando**: Ange eventuella för inläsnings kommandon som du vill köra innan aktivitetssekvensen körs. För inläsnings kommandon är ett skript eller en körbar fil som kan användas för att interagera med användaren i Windows PE innan aktivitetssekvensen körs. Mer information finns i [för inläsnings kommandon för media i aktivitetssekvensen](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > När ett medium skapas skriver aktivitetssekvensen paket-ID och för inläsnings kommando rad, inklusive värdet för alla variabler i aktivitetssekvensen, till **CreateTSMedia. log** -filen på den dator som kör Configuration Manager-konsolen. Du kan granska loggfilen och kontrollera värdet för aktivitetssekvensvariablerna.  

        Om för inläsnings kommandot kräver innehåll väljer du alternativet för att **inkludera filer för för inläsnings kommandot**.  

12. Slutför guiden.  

Filer för fristående media (. ISO) skapas i målmappen. Om du **har valt CD-/DVD-uppsättning**kopierar du utdatafilerna till en uppsättning CD-eller DVD-skivor.


## <a name="next-steps"></a>Nästa steg

[Använda fristående media för att distribuera Windows utan att använda nätverket](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)
