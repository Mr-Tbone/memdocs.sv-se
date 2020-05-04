---
title: Skapa förinstallerade media
titleSuffix: Configuration Manager
description: Använd förinstallerade medier i Configuration Manager för att förenkla distributionen av Windows i flera olika scenarier.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d5219b518d46ccca174c7aa3fef62fe3334def35
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711114"
---
# <a name="create-prestaged-media"></a>Skapa förinstallerade media

*Gäller för: Configuration Manager (aktuell gren)*

Förinstallerade medier i Configuration Manager är en WIM-fil (Windows Image). Den kan installeras på en dator utan operativ system av tillverkaren eller i mellanlagrings centret som inte är ansluten till produktions Configuration Managers miljön. För beredda medier innehåller den Start avbildning som används för att starta mål datorn och den OS-avbildning som används på mål datorn. Du kan även ange program, paket och drivrutinspaket som ska ingå som en del av de förinstallerade medierna. Den aktivitetssekvens som distribuerar operativ systemet ingår inte i mediet. Förberedda medier tillämpas på hårddisken på en ny dator innan datorn skickas till slutanvändaren.

Använd förinstallerade medier för följande distributions scenarier för operativ system:  

- [Skapa en avbildning för en OEM-tillverkare i fabriken eller lokal anläggning](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [Installera en ny version av Windows på en ny dator (utan operativsystem)](install-new-windows-version-new-computer-bare-metal.md)  

- [Distribuera Windows to Go](deploy-windows-to-go.md)  


## <a name="usage"></a>Användning

När datorn startas första gången efter att du har tillämpat det förinstallerade mediet startar datorn i Windows PE. Den ansluter till en hanterings plats för att hitta aktivitetssekvensen som slutför distributions processen för operativ systemet. När du distribuerar en aktivitetssekvens som använder för beredda medier kontrollerar klienten om det finns giltigt innehåll i den lokala aktivitetssekvensen. Om innehållet inte hittas eller har ändrats laddar klienten ned innehållet från en distributions plats eller en peer.  


## <a name="prerequisites"></a>Krav

Innan du skapar för beredda medier med hjälp av guiden skapa aktivitetssekvens måste du se till att alla villkor är uppfyllda.

### <a name="boot-image"></a>Startavbildning

Tänk på följande om den Start avbildning som du använder i aktivitetssekvensen för att distribuera operativ systemet:

- Start avbildningens arkitektur måste vara lämplig för mål datorns arkitektur. En x64-måldator kan exempelvis starta och köra en x86- eller x64-startavbildning. Men en x86-måldator kan bara starta och köra en x86-startavbildning.
- Kontrol lera att start avbildningen innehåller de nätverks-och lagrings driv rutiner som krävs för att etablera mål datorn.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Skapa en aktivitetssekvens för att distribuera ett operativ system

Som en del av de för beredda medierna anger du aktivitetssekvensen för att distribuera operativ systemet. Mer information finns i [skapa en aktivitetssekvens för att installera ett operativ system](create-a-task-sequence-to-install-an-operating-system.md).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuera allt innehåll som är kopplat till aktivitetssekvensen

Distribuera allt innehåll som aktivitetssekvensen kräver till minst en distributions plats. Det här innehållet omfattar start avbildningen, OS-avbildningen och andra tillhör ande filer. Guiden samlar in innehållet från distributions platsen när det skapar det förinstallerade mediet.

Ditt användar konto måste ha minst **Läs** behörighet till innehålls biblioteket på distributions platsen. Mer information finns i avsnittet [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="hard-drive-on-the-destination-computer"></a>Hårddisken på måldatorn

Mål datorns hård disk måste vara formaterad innan det förinstallerade mediet används. Om hård disken inte är formaterad när mediet används, Miss lyckas den aktivitetssekvens som distribuerar operativ systemet när den försöker starta mål datorn.

> [!NOTE]  
> Följande variabel villkor för aktivitetssekvens anges på mediet i guiden skapa aktivitetssekvens: **_SMSTSMediaType = OEMMedia**. Du kan använda samma villkor i aktivitetssekvensen.  


## <a name="process"></a>Process

 > [!NOTE]  
 > För PKI-miljöer, eftersom rot certifikat utfärdaren har angetts på den primära platsen, kontrollerar du att det förinstallerade mediet har skapats på den primära platsen. CAS-webbplatsen har inte rot certifikat utfärdarens information för att korrekt kunna skapa det förinstallerade mediet.

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **operativ system**och väljer noden **aktivitetssekvenser** .  

2. På fliken **Start** i menyfliksområdet väljer du **skapa media för aktivitetssekvens**i gruppen **skapa** . Den här åtgärden startar guiden skapa aktivitetssekvens.  

3. På sidan **Välj medietyp** anger du följande alternativ:  

    - Välj **Förberett medium**.  

    - Om du bara vill tillåta att operativ systemet distribueras utan indata från användaren väljer du **Tillåt obevakad distribution av operativ system**.  

        > [!IMPORTANT]  
        > När du väljer det här alternativet behöver användaren inte ange information om nätverks konfigurationen eller för valfria aktivitetssekvenser. Om du konfigurerar mediet för lösen ords skydd uppmanas användaren fortfarande att ange ett lösen ord.  

4. På sidan **medie hantering** anger du ett av följande alternativ:  

    - **Dynamiskt medium**: Tillåt en hanterings plats att omdirigera mediet till en annan hanterings plats, baserat på klientens plats i plats gränserna.  

    - **Platsbaserade Media**: mediet kontaktar bara den angivna hanterings platsen.  

5. På sidan **medie egenskaper** anger du följande information:  

    - **Skapad av**: Ange vem som skapade mediet.  

    - **Version**: Ange mediets versionsnummer.  

    - **Kommentar**: Ange en unik beskrivning av mediets avsedda användning.  

    - **Mediefil**: Ange namn och sökväg för utdatafilerna. Guiden skriver utdatafilerna till den här platsen. Exempelvis: `\\servername\folder\outputfile.wim`  

    - **Mellanlagringsplats**<!--1359388-->: Processen för att skapa media kan kräva mycket temporärt enhets utrymme. Som standard liknar den här platsen följande sökväg: `%UserProfile%\AppData\Local\Temp`. Från och med version 1902, för att ge dig större flexibilitet med var de här temporära filerna ska lagras, ändra värdet till en annan enhet och sökväg.  

6. På sidan **säkerhet** anger du följande alternativ:  

    - **Aktivera stöd för okända datorer**: Tillåt mediet att distribuera ett operativ system till en dator som inte hanteras av Configuration Manager. Det finns ingen post för de här datorerna i Configuration Managers databasen. Mer information finns i [förbereda för okända dator distributioner](../get-started/prepare-for-unknown-computer-deployments.md).  

    - **Skydda mediet med ett lösen ord**: Ange ett starkt lösen ord för att skydda mediet från obehörig åtkomst. När du anger ett lösenord måste användaren ange lösenordet för att använda det förberedda mediet.  

        > [!IMPORTANT]  
        > Som säkerhetsregel bör du alltid tilldela ett lösenord för att skydda det förberedda mediet.  
 
    - För HTTP-kommunikation väljer du **Skapa självsignerat medie certifikat**. Ange sedan start-och förfallo datum för certifikatet.  
    
        > [!NOTE] 
        > Om du väljer det här alternativet kommer HTTPS-hanterings platser inte att vara tillgängliga för val på sidan **Start avbildning** i den här guiden.

    - För HTTPS-kommunikation väljer du **Importera PKI-certifikat**. Ange sedan det certifikat som ska importeras och dess lösen ord.  

        Mer information om det här klient certifikatet som används av start avbildningar finns i [krav för PKI-certifikat](../../core/plan-design/network/pki-certificate-requirements.md).  

    - **Mappning mellan användare och enhet**: om du vill stödja den användarvänliga hanteringen i Configuration Manager anger du hur du vill att mediet ska koppla användare till mål datorn. Mer information om hur operativ system distribution stöder mappning mellan användare och enhet finns i [associera användare med en måldator](../get-started/associate-users-with-a-destination-computer.md).  

        - **Tillåt mappning mellan användare och enhet med automatiskt godkännande**: mediet kopplar automatiskt användare till mål datorn. Den här funktionen baseras på åtgärderna för den aktivitetssekvens som distribuerar operativ systemet. I det här scenariot skapar aktivitetssekvensen en relation mellan de angivna användarna och mål datorn när operativ systemet distribueras till mål datorn.  

        - **Tillåt mappning mellan användare och enhet väntar på administratörs godkännande**: mediet associerar användare med mål datorn när godkännande har beviljats. Den här funktionen baseras på omfånget för den aktivitetssekvens som distribuerar operativ systemet. I det här scenariot skapar aktivitetssekvensen en relation mellan de angivna användarna och mål datorn, men väntar på godkännande från en administrativ användare innan operativ systemet distribueras.  

        - **Tillåt inte mappning mellan användare och enhet**: mediet kopplar inte användare till mål datorn. I det här scenariot associerar aktivitetssekvensen inte användare med mål datorn när operativ systemet distribueras.  

7. På sidan **aktivitetssekvens** väljer du den aktivitetssekvens som körs på mål datorn. Verifiera listan över innehåll som aktivitetssekvensen refererar till.  

    - **Identifiera associerade program beroenden och Lägg till dem i det här mediet**: Lägg även till innehåll till mediet för program beroenden.  

        > [!TIP]  
        > Om förväntade program beroenden inte visas avmarkerar du det här alternativet för att uppdatera listan.  

8. På sidan **Start avbildning** anger du följande alternativ:  

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

9. På sidan **avbildningar** anger du följande alternativ:  

    - **Avbildnings paket**: Ange den OS-avbildning som ska användas. Mer information finns i [hantera OS-avbildningar](../get-started/manage-operating-system-images.md).  

    - **Avbildnings index**: om paketet innehåller flera OS-avbildningar anger du index för den avbildning som ska distribueras.  

    - **Distributions plats**: Ange den distributions plats som innehåller OS-avbildnings paketet. Guiden hämtar operativ Systems avbildningen från distributions platsen och skriver den till mediet.  

10. På sidan **Välj program** väljer du ytterligare program som ska läggas till i den förinstallerade medie filen.  

11. På sidan **Välj paket** väljer du ytterligare paket som ska läggas till i den förinstallerade medie filen.  

12. På sidan **Välj driv rutins paket** väljer du ytterligare driv rutins paket som ska läggas till i den förinstallerade medie filen.  

13. På sidan **distributions platser** väljer du en eller flera distributions platser som innehållet ska hämtas från.  

    Configuration Manager visar endast distributions platser som har innehållet. Distribuera allt innehåll som är kopplat till aktivitetssekvensen till minst en distributions plats innan du fortsätter. När du har distribuerat innehållet uppdaterar du distributions plats listan. Ta bort eventuella distributions platser som du redan har valt på den här sidan, gå till föregående sida och sedan tillbaka till sidan **distributions platser** . Du kan också starta om guiden. Mer information finns i [distribuera innehåll som refereras till av en aktivitetssekvens](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) och [Hantera innehåll och innehålls infrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

14. På sidan **anpassning** anger du följande alternativ:  

    - Lägg till variabler som används i aktivitetssekvensen.  

    - **Aktivera för inläsnings kommando**: Ange eventuella för inläsnings kommandon som du vill köra innan aktivitetssekvensen körs. För inläsnings kommandon är ett skript eller en körbar fil som kan användas för att interagera med användaren i Windows PE innan aktivitetssekvensen körs. Mer information finns i [för inläsnings kommandon för media i aktivitetssekvensen](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        > När ett medium skapas skriver aktivitetssekvensen paket-ID och för inläsnings kommando rad, inklusive värdet för alla variabler i aktivitetssekvensen, till **CreateTSMedia. log** -filen på den dator som kör Configuration Manager-konsolen. Du kan granska loggfilen och kontrollera värdet för aktivitetssekvensvariablerna.  

        Om för inläsnings kommandot kräver innehåll väljer du alternativet för att **inkludera filer för för inläsnings kommandot**.  

15. Slutför guiden.  


## <a name="next-steps"></a>Nästa steg

[Skapa en avbildning för en OEM-tillverkare i fabriken eller lokal anläggning](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
