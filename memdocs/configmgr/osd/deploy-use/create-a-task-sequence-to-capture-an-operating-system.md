---
title: Skapa en aktivitetssekvens för att avbilda ett operativsystem
titleSuffix: Configuration Manager
description: En aktivitetssekvens för att bygga och avbilda skapar en referens dator som kan omfatta specifika driv rutiner och program uppdateringar tillsammans med operativ systemet.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ceb63560c6000b1a76116d0791c98219a66066b8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723070"
---
# <a name="create-a-task-sequence-to-capture-an-os"></a>Skapa en aktivitetssekvens för att avbilda ett operativsystem

*Gäller för: Configuration Manager (aktuell gren)*

När du använder en aktivitetssekvens för att distribuera ett operativ system till en dator i Configuration Manager installerar datorn den OS-avbildning som du anger i aktivitetssekvensen. Du kan anpassa operativ system avbildningen så att den innehåller vissa driv rutiner, program och program uppdateringar. Använd först en aktivitetssekvens för att bygga och avbilda för att bygga en referens dator. Avbilda sedan OS-avbildningen från den referens datorn. Om du redan har en referens dator som är tillgänglig för avbildning skapar du en anpassad aktivitetssekvens för att avbilda operativ systemet.

## <a name="about-the-build-and-capture-task-sequence"></a><a name="BKMK_BuildCaptureTS"></a>Om aktivitetssekvensen för att bygga och avbilda

Aktivitetssekvensen för att bygga och avbilda:

- Partitionerar och formaterar referens datorn
- Installerar operativ systemet
- Installerar Configuration Manager-klienten
- Installerar program
- Tillämpar program uppdateringar
- Avbildar operativ systemet från referens datorn

De paket som är kopplade till aktivitetssekvensen, t. ex. program, måste finnas tillgängliga på distributions platser innan du distribuerar aktivitetssekvensen skapa och avbilda.

## <a name="requirements"></a><a name="BKMK_CreatePackages"></a>Signaturkrav

Innan du skapar en aktivitetssekvens för att installera ett operativ system måste du kontrol lera att följande komponenter finns på plats:  

### <a name="required"></a>Krävs

- [Startavbildning](../get-started/manage-boot-images.md)

- [OS-avbildning](../get-started/manage-operating-system-images.md)

### <a name="required-if-used"></a>Obligatoriskt (om det används)

- [Driv rutins paket](../get-started/manage-drivers.md) som innehåller de Windows-drivrutiner som krävs för att stödja maskin vara på referens datorn. Mer information om aktivitetssekvensstegen för att hantera drivrutiner finns i [Use task sequences to install device drivers](../get-started/manage-drivers.md#BKMK_TSDrivers).

- [Programuppdateringar](../../sum/get-started/synchronize-software-updates.md)

- [Program](../../apps/deploy-use/create-applications.md)

## <a name="create-a-build-and-capture-task-sequence"></a><a name="BKMK_CreateBuildCaptureTS"></a> Skapa en bygg- och avbildningsaktivitetssekvens

Använd följande procedur för att använda en aktivitetssekvens för att bygga en referens dator och avbilda operativ systemet.

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj noden **aktivitetssekvenser** .  

1. På fliken **Start** i menyfliksområdet i gruppen **skapa** väljer du **skapa aktivitetssekvens** för att starta guiden skapa aktivitetssekvens.  

1. På sidan **Skapa en ny aktivitetssekvens** väljer du **Bygga och göra en avbildning av ett referensoperativsystem**.  

1. På sidan **information om aktivitetssekvens** anger du följande inställningar:  

    - **Namn på aktivitetssekvens**: Ange ett namn på aktivitetssekvensen.  

    - **Beskrivning**: Ange en valfri beskrivning av aktivitetssekvensen. Beskriv till exempel det operativ system som aktivitetssekvensen skapar.

    - **Start avbildning**: Ange den Start avbildning som ska användas med aktivitetssekvensen.  

        > [!IMPORTANT]  
        > Startavbildningens arkitektur måste vara kompatibel med måldatorns maskinvaruarkitektur.  

1. På sidan **Installera Windows** anger du följande inställningar:  

    - **Avbildnings paket**: Ange avbildnings paketet för operativ systemet, som innehåller de filer som krävs för att installera operativ systemet.  

    - **Avbildnings index**: Ange index för det operativ system som ska installeras i avbildningen. Om operativ system avbildningen innehåller flera versioner väljer du den version som du vill installera.  

    - **Produkt nyckel**: Ange produkt nyckeln för det Windows-operativsystem som ska installeras vid behov. Du kan ange kodade volymlicensnycklar och standardproduktnycklar. Om du använder en icke-kodad produkt nyckel separerar du varje grupp med fem tecken med ett`-`bindestreck (). Exempelvis: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`  

    - **Server licensierings läge**: om det behövs anger du att Server licensen är **per plats**, **per server**eller att ingen licens har angetts. Om serverlicensen gäller **Per server** anger du också det högsta antalet serveranslutningar.  

    - Ange hur administratörs kontot ska konfigureras för det distribuerade operativ systemet:  

        - **Generera slumpmässigt lösen ord för den lokala administratören och inaktivera kontot för alla plattformar som stöds**: skapa ett slumpmässigt lösen ord för det lokala administratörs kontot. Inaktivera kontot när Windows har kon figurer ATS.

        - **Aktivera kontot och ange lösen ord för den lokala administratören**: Använd samma lösen ord för det lokala administratörs kontot på alla datorer där du distribuerar det här operativ systemet.

1. På sidan **Konfigurera nätverk** anger du följande inställningar:

    - **Anslut till en arbets grupp**: Ange om mål datorn ska läggas till i en arbets grupp när operativ systemet distribueras.  

    - **Anslut till en domän**: Ange om mål datorn ska läggas till i en domän när operativ systemet distribueras. Ange namnet på domänen i **Domän**.  

        > [!IMPORTANT]  
        > Du kan bläddra efter domäner i den lokala skogen. Ange domän namnet för en fjärran sluten skog.

        Du kan också ange en organisationsenhet. Den här inställningen är valfri och anger det unika LDAP X. 500-namnet för den ORGANISATIONSENHET där dator kontot ska skapas, om det inte redan finns.  

    - **Konto**: Ange användarnamn och lösenord för det konto som har behörighet att ansluta till den angivna domänen. Till exempel: `domain\user` eller `%variable%`.  

        > [!IMPORTANT]  
        > Om du planerar att migrera domän inställningarna eller arbets grupps inställningarna under distributionen kontrollerar du att du anger rätt domänautentiseringsuppgifter här.  

1. På sidan **installera Configuration Manager** anger du Configuration Manager klient paketet. Det här paketet innehåller källfiler för att installera Configuration Manager-klienten. Ange även eventuella ytterligare egenskaper som krävs för att installera klienten.  

    Mer information finns i [om klient installations egenskaper](../../core/clients/deploy/about-client-installation-properties.md).

1. På sidan **Inkludera uppdateringar** anger du om nödvändiga program uppdateringar, program uppdateringar eller inga program uppdateringar ska installeras. Om du anger att program uppdateringarna ska installeras, installerar Configuration Manager bara de program uppdateringar som är riktade mot de samlingar som mål datorn är medlem i.  

1. På sidan **installera program** anger du de program som ska installeras på mål datorn. Om du anger flera program kan du också ange att aktivitetssekvensen ska fortsätta om något program inte går att installera.  

    > [!NOTE]
    > Sidan **system förberedelse** visas härnäst i guiden, men den används inte längre. Fortsätt genom att välja **Nästa**.

1. På sidan **avbildnings egenskaper** anger du följande inställningar för operativ system avbildningen:

    - **Skapad av**: Ange namnet på den användare som ska noteras som skapare av OS-avbildningen.  

    - **Version**: Ange det versions nummer som är associerat med operativ system avbildningen. Det här attributet behöver inte vara operativ systemets version, eftersom platsen lagrar värdet separat.

    - **Beskrivning**: Ange en beskrivning av operativ system avbildningen.  

1. På sidan **avbilda avbildning** anger du följande inställningar:

    - **Sökväg**: Ange en delad nätverksmapp där Configuration Manager ska lagra avbildnings filen för utdata (. wim). Den här filen innehåller OS-avbildningen som baseras på de inställningar du anger i den här guiden. Om du anger en mapp som innehåller en befintlig. WIM-fil, den skrivs över.  

    - **Konto**: Ange det Windows-konto som har behörigheter för den nätverksresurs där avbildningen finns sparad.  

1. Slutför guiden.  

Om du vill lägga till ytterligare steg i aktivitetssekvensen markerar du den och väljer **Redigera**. Mer information om hur du redigerar en aktivitetssekvens finns i [använda redigeraren för aktivitetssekvens](../understand/task-sequence-editor.md).  

Distribuera aktivitetssekvensen till en referensdator på något av följande sätt:  

- Om referens datorn redan är en Configuration Manager-klient distribuerar du aktivitetssekvensen skapa och avbilda till en samling som innehåller referens datorn. Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md).

- Om referens datorn inte är en Configuration Manager-klient, eller om du vill köra aktivitetssekvensen manuellt på referens datorn, använder du **guiden skapa aktivitetssekvens** för att skapa startbara media. Mer information finns i [Skapa startbara media](create-bootable-media.md).  

När du har hämtat avbildningen kan du distribuera den till andra datorer. Mer information om hur du distribuerar den insamlade OS-avbildningen finns i [skapa en aktivitetssekvens för att installera ett operativ system](create-a-task-sequence-to-install-an-operating-system.md).  

## <a name="capture-from-an-existing-reference-computer"></a><a name="BKMK_CaptureExistingRefComputer"></a>Avbilda från en befintlig referens dator

När du redan har en referens dator som är redo att avbilda, skapar du en aktivitetssekvens som bara avbildar operativ systemet från referens datorn. Använd steget **avbilda operativ Systems avbildning** för att avbilda en eller flera avbildningar från en referens dator och lagra dem i en avbildnings fil (. wim) på den angivna nätverks resursen. Starta referens datorn i Windows PE med en start avbildning. Aktivitetssekvensen fångar varje hård disk på referens datorn som en separat avbildning i WIM-filen. Om den refererade datorn har flera enheter innehåller den resulterande. wim-filen en separat avbildning för varje volym. Den fångar bara volymer som är formaterade som NTFS eller FAT32. Den hoppar över volymer med andra format eller USB-volymer.  

Använd följande procedur för att avbilda en operativ system avbildning från en befintlig referens dator:

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj noden **aktivitetssekvenser** .  

1. Välj **skapa**aktivitetssekvens i gruppen **skapa** på fliken **Start** i menyfliksområdet. Den här åtgärden startar guiden skapa aktivitetssekvens.  

1. På sidan **Skapa en ny aktivitetssekvens** väljer du **Skapa en ny anpassad aktivitetssekvens**.  

1. På sidan **information** om aktivitetssekvens anger du ett namn på aktivitetssekvensen. Du kan också lägga till en beskrivning av aktivitetssekvensen.  

1. Ange en startavbildning för aktivitetssekvensen. Configuration Manager använder den här start avbildningen för att starta referens datorn med Windows PE. Mer information finns i [Hantera start avbildningar](../get-started/manage-boot-images.md).  

1. Slutför guiden.  

1. I noden **aktivitetssekvenser** väljer du den nya aktivitetssekvensen. På fliken **Start** i menyfliksområdet väljer du **Redigera**i gruppen **aktivitetssekvens** . Den här åtgärden öppnar Redigeraren för aktivitetssekvensen.  

1. Om Configuration Manager-klienten är installerad på referens datorn:

    Gå till menyn **Lägg** till, Välj **avbildningar**och välj sedan [Förbered ConfigMgr-klient för avbildning](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). I det här steget generaliseras Configuration Manager-klienten på referens datorn.

    > [!Note]  
    > Aktivitetssekvensen stöder inte avinstallation av Configuration Manager klienten.

1. Gå till menyn **Lägg** till, Välj **avbildningar**och välj [Förbered Windows för avbildning](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). Det här steget Kör Sysprep och startar sedan om datorn till den Windows PE-startavbildning som angetts för aktivitetssekvensen. För att den här åtgärden ska slutföras, ska du inte ansluta referens datorn till en domän.

1. Gå till menyn **Lägg** till, Välj **avbildningar**och välj [avbilda operativ system avbildning](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage). Det här steget körs bara från Windows PE för att avbilda hård diskarna på referens datorn. Konfigurera följande inställningar:

    - **Namn** och **Beskrivning**: Du kan välja att byta namn på aktivitetssekvenssteget och ange en beskrivning.  

    - **Mål**: Ange en delad nätverksmapp där .WIM-utdatafilen lagras. Den här filen innehåller OS-avbildningen baserat på de inställningar som du anger med hjälp av den här guiden. Om du anger en mapp som innehåller en befintlig. WIM-fil, den skrivs över.  

    - **Beskrivning**, **version**och **skapad av**: du kan också ange information om avbildningen som ska samlas in.  

    - **Avbilda operativsystemsavbildning**: Ange det Windows-konto som har behörigheter för den nätverksresurs där avbildningen finns sparad. Välj **Ange** för att ange namnet på det Windows-kontot.  

Välj **OK** för att spara ändringarna och stänga redigeraren för aktivitetssekvens.  

Distribuera aktivitetssekvensen till en referensdator på något av följande sätt:  

- Om referens datorn redan är en Configuration Manager-klient distribuerar du aktivitetssekvensen till en samling som innehåller referens datorn. Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md).

- Om referens datorn inte är en Configuration Manager-klient, eller om du vill köra aktivitetssekvensen manuellt på referens datorn, använder du **guiden skapa aktivitetssekvens** för att skapa avbildnings medier. Mer information finns i [skapa avbildnings medier](create-capture-media.md).  

När du har hämtat avbildningen kan du distribuera den till andra datorer. Mer information om hur du distribuerar den insamlade OS-avbildningen finns i [skapa en aktivitetssekvens för att installera ett operativ system](create-a-task-sequence-to-install-an-operating-system.md).

## <a name="example-task-sequence"></a><a name="BKMK_BuildandCaptureTSExample"></a>Exempel på aktivitetssekvens

Använd följande tabell som en vägledning när du skapar en aktivitetssekvens som skapar och avbildar en operativ system avbildning. Tabellen hjälper dig att bestämma den allmänna ordningen för stegen i aktivitetssekvensen och hur du ordnar och strukturerar de här stegen i logiska grupper. Den aktivitetssekvens som du skapar kan variera från det här exemplet. Det kan innehålla fler eller färre steg och grupper.

> [!NOTE]  
> Använd alltid guiden Skapa aktivitetssekvens för att skapa den här typen av aktivitetssekvens.
>
> Guiden lägger till steg i aktivitetssekvensen med något annorlunda namn som du ser om du manuellt lägger till samma steg.

### <a name="group-build-the-reference-machine"></a>Grupp: Bygg referens datorn

Den här gruppen innehåller de åtgärder som krävs för att bygga en referensdator.

|Aktivitetssekvenssteg|Beskrivning|  
|-------------------------------|---------------|  
|**Starta om i Windows PE**|Starta om mål datorn till den Start avbildning som är tilldelad i aktivitetssekvensen. Det här steget visar ett meddelande för användaren om att datorn kommer att startas om så att installationen kan fortsätta.<br /><br />I det här steget används variabeln `_SMSTSInWinPE` skrivskyddad aktivitetssekvens. Om det associerade värdet är lika `false`med, fortsätter steget i aktivitetssekvensen.|
|**Partitionsdisk 0 - BIOS**|Partitionera och formatera hård disken på mål datorn i BIOS-läge. Standard disk numret är `0`.<br /><br />Det här steget använder flera variabler för skrivskyddad aktivitetssekvens. Den körs till exempel bara om Configuration Manager-klientcachen inte finns och inte körs om datorn har kon figurer ATS för UEFI.|
|**Partitionsdisk 0 - UEFI**|Partitionera och formatera hård disken på mål datorn i UEFI-läge. Standard disk numret är `0`.<br /><br />Det här steget använder flera variabler för skrivskyddad aktivitetssekvens. Den körs till exempel bara om den Configuration Manager klientcachen inte finns och körs bara om datorn är konfigurerad för UEFI.|
|**Använd operativsystem**|Installera den angivna OS-avbildningen på mål datorn. Det här steget tar först bort alla filer på volymen, förutom Configuration Manager-/regionsspecifika styr filer. Den använder sedan alla volym avbildningar som finns i WIM-filen för motsvarande sekventiell disk volym på mål datorn.|
|**Använd Windows-inställningar**|Konfigurera Windows-inställningar för mål datorn.|
|**Använd nätverksinställningar**|Ange konfigurations information för nätverks-eller arbets grupp för mål datorn.|
|**Använda enhetsdrivrutiner**|Matcha och installera driv rutiner som en del av distributionen av operativ systemet. Mer information finns i avsnittet [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).<br /><br />I det här steget används variabeln `_SMSTSMediaType` skrivskyddad aktivitetssekvens. Om det associerade värdet inte är `FullMedia`lika körs inte det här steget.|
|**Konfigurera Windows och Configuration Manager**|Installera Configuration Manager klient program varan. Configuration Manager installerar och registrerar Configuration Manager-klientens GUID. Inkludera eventuella nödvändiga **installations egenskaper**.|
|**Installera uppdateringar**|Ange hur program uppdateringar installeras på mål datorn. Mål datorn utvärderas inte för tillämpliga program uppdateringar förrän det här steget körs. I det här läget liknar utvärderingen en annan Configuration Manager-hanterad klient. Mer information finns i [installera program uppdateringar](../understand/install-software-updates.md).<br /><br />I det här steget används variabeln `_SMSTSMediaType` skrivskyddad aktivitetssekvens. Om det associerade värdet inte är `FullMedia`lika körs inte det här steget.|
|**Installera program**|Anger alla program som ska installeras på referens datorn.|

### <a name="group-capture-the-reference-machine"></a>Grupp: avbilda referens datorn

Den här gruppen innehåller de steg som krävs för att förbereda och avbilda en referensdator.

|Aktivitetssekvenssteg|Beskrivning|  
|-------------------------------|---------------|  
|**Förbered Configuration Manager-klient**|Generalisera Configuration Manager-klienten på referens datorn.|
|**Förbered operativ system**|Kör Sysprep för att generalisera Windows. Sedan startas datorn om i den Windows PE-startavbildning som angetts för aktivitetssekvensen.|
|**Avbilda referensdatorn**|Avbildningen samlas in på den angivna nätverks resursen och. WIM-fil.|

> [!IMPORTANT]
> När du har hämtat en avbildning från en referens dator ska du inte avbilda en annan operativ system avbildning från referens datorn. Register poster skapas under den inledande konfigurationen. Skapa en ny referens dator varje gång du hämtar operativ Systems avbildningen. Om du planerar att använda samma referens dator för att skapa framtida OS-avbildningar måste du först avinstallera och installera om den Configuration Manager klienten.

## <a name="next-steps"></a>Nästa steg

[Metoder för att distribuera operativsystem i företag](methods-to-deploy-enterprise-operating-systems.md)
