---
title: Hantera drivrutiner
titleSuffix: Configuration Manager
description: Använd Configuration Manager driv rutins katalog för att importera enhets driv rutiner, gruppera driv rutiner i paket och distribuera paketen till distributions platser.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 09cf1b7ee1859043e0839d5a1b5db3518c602b74
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124439"
---
# <a name="manage-drivers-in-configuration-manager"></a>Hantera driv rutiner i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager tillhandahåller en driv rutins katalog som du kan använda för att hantera Windows enhets driv rutiner i din Configuration Manager-miljö. Använd driv rutins katalogen för att importera enhets driv rutiner till Configuration Manager, för att gruppera dem i paket och distribuera paketen till distributions platser. Enhets driv rutiner kan användas när du installerar hela operativ systemet på mål datorn och när du använder Windows PE i en start avbildning. Windows enhets driv rutiner består av en installations informations fil (INF) och eventuella ytterligare filer som krävs för att stödja enheten. När du distribuerar ett operativ system hämtar Configuration Manager information om maskin vara och plattform för enheten från dess INF-fil. 



## <a name="driver-categories"></a><a name="BKMK_DriverCategories"></a>Driv rutins kategorier

När du importerar enhetsdrivrutiner kan du tilldela de nya enhetsdrivrutinerna till en kategori. Enhetsdrivrutinkategorierna hjälper till att gruppera enhetsdrivrutiner som används på liknande sätt i drivenhetskatalogen. Ange till exempel alla enhets driv rutiner för nätverkskort till en viss kategori. När du sedan skapar en aktivitetssekvens som innehåller steget [Använd driv rutiner automatiskt](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) , anger du en kategori med enhets driv rutiner. Configuration Manager genomsöker sedan maskin varan och väljer lämpliga driv rutiner från den kategorin för att mellanlagra i systemet som Installationsprogrammet för Windows ska använda.  



## <a name="driver-packages"></a><a name="BKMK_ManagingDriverPackages"></a> Drivrutinspaket

Gruppera liknande enhets driv rutiner i paket för att förenkla distributioner av operativ system. Skapa till exempel ett driv rutins paket för varje dator tillverkare i nätverket. Du kan skapa ett driv rutins paket när du importerar driv rutiner till driv rutins katalogen direkt i noden **driv rutins paket** . När du har skapat ett driv rutins paket distribuerar du det till distributions platser. Configuration Manager klient datorerna kan installera driv rutinerna efter behov. 

Tänk på följande:  

- När du skapar ett driv rutins paket måste paketets käll plats peka på en tom nätverks resurs som inte används av ett annat driv rutins paket. SMS-providern måste ha **fullständig** behörighet till den platsen.  

- När du lägger till enhets driv rutiner i ett driv rutins paket Configuration Manager kopieras det till käll platsen för paketet. Du kan endast lägga till enhets driv rutiner som du har importerat och som är aktiverade i driv rutins katalogen i ett driv rutins paket.  

- Du kan kopiera en delmängd av enhets driv rutinerna från ett befintligt driv rutins paket. Börja med att skapa ett nytt driv rutins paket. Lägg sedan till den del av enhets driv rutinerna i det nya paketet och distribuera sedan det nya paketet till en distributions plats.  

- När du använder aktivitetssekvenser för att installera drivrutiner skapar du drivrutinspaket som innehåller färre än 500 enhetsdrivrutiner.


### <a name="create-a-driver-package"></a><a name="BKMK_CreatingDriverPackages"></a>Skapa ett driv rutins paket  

> [!IMPORTANT]  
> Om du vill skapa ett driv rutins paket måste du ha en tom nätverksmapp som inte används av ett annat driv rutins paket. I de flesta fall skapar du en ny mapp innan du påbörjar den här proceduren.  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **operativ system**och välj sedan noden **driv rutins paket** .  

2. Välj **skapa driv rutins paket**i gruppen **skapa** på fliken **Start** i menyfliksområdet.  

3. Ange ett beskrivande **namn** på driv rutins paketet.  

4. Ange en valfri **kommentar** för driv rutins paketet. Använd den här beskrivningen för att ange information om innehållet eller syftet med driv rutins paketet.  

5. I rutan **Sökväg** anger du en tom källmapp för drivrutinspaketet. Varje drivrutinspaket måste ha en unik mapp. Den här sökvägen krävs som nätverks plats.  

   > [!IMPORTANT]  
   > Plats Server kontot måste ha **fullständig** behörighet till den angivna källmappen.  

Det nya driv rutins paketet innehåller inga driv rutiner. Nästa steg lägger till driv rutiner i paketet.  

Om det finns flera paket i noden **Drivrutinspaket** kan du lägga till mappar i noden för att dela upp paketen i logiska grupper.  


### <a name="additional-actions-for-driver-packages"></a><a name="BKMK_PackageActions"></a> Ytterligare åtgärder för drivrutinspaket  

Du kan utföra ytterligare åtgärder för att hantera driv rutins paket när du väljer ett eller flera driv rutins paket från noden **driv rutins paket** . 


#### <a name="create-prestage-content-file"></a>Skapa förinstallerad innehållsfil
Skapar filer som du kan använda för att manuellt importera innehåll och tillhör ande metadata. Använd förinstallerat innehåll om bandbredden mellan platsservern och distributionsplatserna är låg.

#### <a name="delete"></a>Ta bort
Tar bort drivrutinspaketet från noden **Drivrutinspaket** .

#### <a name="distribute-content"></a>Distribuera innehåll
Distribuerar drivrutinspaketet till distributionsplatser, distributionsplatsgrupper och distributionplatsgrupper som är kopplade till samlingar.

#### <a name="manage-access-accounts"></a>Hantera åtkomstkonton
Lägger till, ändrar eller tar bort åtkomstbehörighet för drivrutinspaketet.

Mer information om paket åtkomst konton finns [i konton som används i Configuration Manager](../../core/plan-design/hierarchy/accounts.md).

#### <a name="move"></a>Flytta
Drivrutinspaketet flyttas till en annan mapp i noden **Drivrutinspaket** .

#### <a name="update-distribution-points"></a>Uppdatera distributionsplatser
Uppdaterar drivrutinspaketet på alla distributionsplatser där paketet är lagrat. Med den här åtgärden kopieras det innehåll som har ändras sedan det senast distribuerades.

#### <a name="properties"></a>Egenskaper
Öppnar dialog rutan **Egenskaper** . Granska och ändra driv Rutinens innehåll och egenskaper. Du kan till exempel ändra namn och beskrivning för driv rutinen, aktivera eller inaktivera den och ange vilka plattformar som ska köras. 

<!--3607716, fka 1358270-->
Från och med version 1810 har driv rutins paket metadata-fält för **tillverkare** och **modell**. Använd de här fälten för att tagga driv rutins paket med information som hjälper dig i allmänna underhåll, eller för att identifiera gamla och duplicerade driv rutiner som du kan ta bort. På fliken **Allmänt** väljer du ett befintligt värde i list rutorna eller anger en sträng för att skapa en ny post.

I noden **driv rutins paket** visas dessa fält i listan som **driv rutins tillverkare** och **driv rutins modell** kolumner. De kan också användas som Sök kriterier.

Från och med version 1906 använder du de här attributen för att förcachelagra innehåll på en klient. Mer information finns i [Konfigurera förinställt innehåll för cache](../deploy-use/configure-precache-content.md).<!--4224642-->  




## <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a>Enhets driv rutiner

Du kan installera driv rutiner på mål datorer utan att inkludera dem i operativ Systems avbildningen som distribueras. Configuration Manager tillhandahåller en driv rutins katalog som innehåller referenser till alla driv rutiner som du importerar till Configuration Manager. Drivrutinskatalogen finns i arbetsytan **Programvarubibliotek** och består av två noder: **Drivrutiner** och **Drivrutinspaket**. I noden **driv rutiner** visas alla driv rutiner som du har importerat till driv rutins katalogen.  


### <a name="import-device-drivers-into-the-driver-catalog"></a><a name="BKMK_ImportDrivers"></a> Importera enhetsdrivrutiner till drivrutinskatalogen  

Innan du kan använda en driv rutin när du distribuerar ett operativ system importerar du den till driv rutins katalogen. För att hantera dem bättre, importera endast de driv rutiner som du planerar att installera som en del av distributionerna av operativ systemet. Lagra flera versioner av driv rutiner i katalogen för att tillhandahålla ett enkelt sätt att uppgradera befintliga driv rutiner när kraven på maskin varu enheter ändras i nätverket.  

Som en del av import processen för enhets driv rutinen läser Configuration Manager följande egenskaper om driv rutinen:
- Leverantör
- Klass
- Version
- Signatur
- Maskin vara som stöds
- Plattforms information som stöds

Som standard är driv rutinen namngiven efter den första maskin varu enhet som stöds. Du kan byta namn på driv rutinen senare. Listan över plattformar som stöds baseras på informationen i drivrutinens INF-fil. Eftersom noggrannheten i den här informationen kan variera, verifiera manuellt att driv rutinen stöds när du har importerat den till katalogen.  

När du har importerat enhets driv rutiner till katalogen lägger du till dem i driv rutins paket eller start avbildnings paket.  

> [!IMPORTANT]  
> Du kan inte importera enhets driv rutiner direkt till en undermapp i noden **driv rutiner** . Om du vill importera en enhetsdrivrutin till en undermapp importerar du först enhetsdrivrutinen till noden **Drivrutiner** och flyttar sedan drivrutinen till undermappen.  


#### <a name="process-to-import-windows-device-drivers-into-the-driver-catalog"></a>Process för att importera Windows-drivrutiner till driv rutins katalogen  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **operativ system**och välj noden **driv rutiner** .  

2. På fliken **Start** i menyfliksområdet väljer du **Importera driv rutin** i gruppen **skapa** för att starta **guiden Importera ny driv rutin**.  

3. På sidan **hitta driv rutin** anger du följande alternativ:  

    - **Importera alla driv rutiner i följande nätverks Sök väg (UNC)**: om du vill importera alla enhets driv rutiner i en angiven mapp anger du nätverks Sök vägen. Till exempel: `\\servername\share\folder`.  

        > [!NOTE]  
        > Om det finns många undermappar och många driv rutins-INF-filer kan den här processen ta tid.  

    - **Importera en speciell driv rutin**: om du vill importera en speciell driv rutin från en mapp anger du nätverks Sök vägen till INF-filen för Windows Device-drivrutinen.  

    - **Ange alternativet för dubbla driv rutiner**: Välj hur du vill Configuration Manager hantera driv rutins kategorier när du importerar en duplicerad driv rutin  
        - **Importera driv rutinen och Lägg till en ny kategori i de befintliga kategorierna**  
        - **Importera driv rutinen och Behåll de befintliga kategorierna**  
        - **Importera driv rutinen och skriv över de befintliga kategorierna**  
        - **Importera inte driv rutinen**  

    > [!IMPORTANT]  
    > När du importerar drivrutiner måste platsservern har **läsbehörighet** för mappen, annars går det inte att importera.  

4. På sidan **driv rutins information** anger du följande alternativ:  

    - **Dölj driv rutiner som inte finns i en lagrings-eller nätverks klass (för start avbildningar)**: Använd den här inställningen för att endast Visa lagrings-och nätverks driv rutiner. Det här alternativet döljer andra driv rutiner som normalt inte behövs för start avbildningar, till exempel en grafik driv rutin eller modem driv rutin.  

    - **Dölj driv rutiner som inte är digitalt signerade**: Microsoft rekommenderar endast att du använder driv rutiner som har signerats digitalt  

    - Markera de drivrutiner i listan som du vill importera till drivrutinskatalogen.  

    - **Aktivera de här drivrutinerna och låt dem installeras på datorer**: Välj den här inställningen om du vill att datorerna ska installera enhetsdrivrutinerna. Det här alternativet är aktiverat som standard.  

        > [!IMPORTANT]  
        > Om det uppstår ett problem med en enhets driv rutin eller om du vill pausa installationen av en driv rutin, inaktiverar du den under importen. Du kan också inaktivera driv rutiner när du har importerat dem.  

    - Om du vill tilldela enhets driv rutinerna till en administrativ kategori för filtrerings syfte, till exempel "station ära datorer" eller "Notebooks", väljer du **Kategorier**. Välj en befintlig kategori eller skapa en ny kategori. Använd kategorier för att kontrol lera vilka enhets driv rutiner som används med steget [Använd aktivitetssekvens automatiskt](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) .  

5. På sidan **Lägg till driv rutin till paket** väljer du om du vill lägga till driv rutinerna i ett paket.  

    - Välj de drivrutinspaket som ska användas för att distribuera enhetsdrivrutinerna.  

        Om det behövs väljer du **nytt paket** för att skapa ett nytt driv rutins paket. När du skapar ett nytt driv rutins paket anger du en nätverks resurs som inte används av andra driv rutins paket.  

    - Om paketet redan har distribuerats till distributions platser väljer du **Ja** i dialog rutan för att uppdatera start avbildningarna på distributions platserna. Du kan inte använda enhets driv rutiner förrän de har distribuerats till distributions platser. Om du väljer **Nej**kör du åtgärden **Uppdatera distributions plats** innan du använder start avbildningen. Om driv rutins paketet aldrig har distribuerats måste du använda åtgärden **distribuera innehåll** i noden **driv rutins paket** .  

6. På sidan **Lägg till driv rutin i Start avbildningar** väljer du om du vill lägga till enhets driv rutiner i befintliga start avbildningar.  

    > [!NOTE]  
    > Lägg endast till lagrings-och nätverks driv rutiner i Start avbildningarna.  

    - Välj **Ja** i dialog rutan för att uppdatera start avbildningarna på distributions platser. Du kan inte använda enhets driv rutiner förrän de har distribuerats till distributions platser. Om du väljer **Nej**kör du åtgärden **Uppdatera distributions plats** innan du använder start avbildningen. Om driv rutins paketet aldrig har distribuerats måste du använda åtgärden **distribuera innehåll** i noden **driv rutins paket** .  

    - Configuration Manager varnar dig om arkitekturen för en eller flera driv rutiner inte matchar arkitekturen för de start avbildningar som du har valt. Om de inte matchar väljer du **OK**. Gå tillbaka till sidan med **driv rutins information** och rensa de driv rutiner som inte matchar arkitekturen i den valda start avbildningen. Om du till exempel väljer en x64- och x86-startavbildning måste alla drivrutiner ha stöd för båda arkitekturerna. Om du till exempel väljer en x64-startavbildning måste alla drivrutiner ha stöd för x64-arkitekturen.  

        > [!NOTE]  
        > - Arkitekturen baseras på arkitekturen som rapporteras i INF-filen från tillverkaren.  
        > - Om en driv rutin rapporterar att den har stöd för båda arkitekturerna kan du importera den till valfri start avbildning.  

    - Configuration Manager varnar dig om du lägger till enhets driv rutiner som inte är nätverks-eller lagrings driv rutiner i en start avbildning. I de flesta fall är de inte nödvändiga för start avbildningen. Välj **Ja** om du vill lägga till driv rutinerna i Start avbildningen eller **Nej** om du vill gå tillbaka och ändra valet av driv rutin.  

    - Configuration Manager varnar om en eller flera av de valda driv rutinerna inte är korrekt digitalt signerade. Välj **Ja** om du vill fortsätta och välj **Nej** för att gå tillbaka och göra ändringar i valet av driv rutin.  

7. Slutför guiden.  


### <a name="manage-device-drivers-in-a-driver-package"></a><a name="BKMK_ModifyDriverPackage"></a> Hantera enhetsdrivrutiner i ett drivrutinspaket  

Använd följande metoder om du vill ändra drivrutinspaket och startavbildningar. Om du vill lägga till eller ta bort en driv rutin måste du först leta upp den i noden **driv rutiner** . Redigera sedan de paket eller start avbildningar som den valda driv rutinen är kopplad till.  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **operativ system**och välj sedan noden **driv rutiner** .  

2. Välj de enhets driv rutiner som du vill lägga till i ett driv rutins paket.  

3. På fliken **Start** i menyfliksområdet i gruppen **driv rutin** väljer du **Redigera**och väljer sedan **driv rutins paket**.  

4. Om du vill lägga till en drivrutin markerar du kryssrutan för de drivrutinspaket där drivrutinerna ska läggas till. Om du vill ta bort en drivrutin markerar du kryssrutan för de drivrutinspaket som drivrutinen ska tas bort från.  

    Om du lägger till enhets driv rutiner som är associerade med driv rutins paket kan du skapa ett nytt paket om du vill. Välj **nytt paket**, som öppnar dialog rutan **nytt driv rutins paket** .  

5. Om paketet redan har distribuerats till distributions platser väljer du **Ja** i dialog rutan för att uppdatera start avbildningarna på distributions platserna. Du kan inte använda enhets driv rutiner förrän de har distribuerats till distributions platser. Om du väljer **Nej**kör du åtgärden **Uppdatera distributions plats** innan du använder start avbildningen. Om driv rutins paketet aldrig har distribuerats måste du använda åtgärden **distribuera innehåll** i noden **driv rutins paket** . Innan drivrutinerna blir tillgängliga måste du uppdatera drivrutinspaketet på distributionsplatserna.  

    Välj **OK** när du är färdig.  


### <a name="manage-device-drivers-in-a-boot-image"></a><a name="BKMK_ManageDriversBootImage"></a>Hantera enhets driv rutiner i en start avbildning  

Du kan lägga till i Start avbildningar Windows-drivrutiner som har importer ATS till katalogen. Använd följande riktlinjer när du lägger till enhetsdrivrutiner till en startavbildning:  

- Lägg endast till lagrings-och nätverks driv rutiner i Start avbildningar. Andra typer av driv rutiner behövs vanligt vis inte i Windows PE. Driv rutiner som inte krävs onödigt ökar storleken på Start avbildningen.  

- Lägg endast till enhets driv rutiner för Windows 10 i en start avbildning. Den version av Windows PE som krävs är baserad på Windows 10.  

- Kontrol lera att du använder rätt enhets driv rutin för start avbildningens arkitektur. Lägg inte till en x86-enhets driv rutin till en x64-start avbildning.  

#### <a name="process-to-modify-the-device-drivers-associated-with-a-boot-image"></a>Process för att ändra de enhets driv rutiner som är associerade med en start avbildning  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **operativ system**och välj sedan noden **driv rutiner** .  

2. Välj de enhets driv rutiner som du vill lägga till i driv rutins paketet.  

3. På fliken **Start** i menyfliksområdet i gruppen **driv rutin** väljer du **Redigera**och sedan **Start avbildningar**.  

4. Om du vill lägga till en drivrutin markerar du kryssrutan för de startavbildningar där drivrutinerna ska läggas till. Om du vill ta bort en drivrutin markerar du kryssrutan för den startavbildning som drivrutinen ska tas bort från.  

5. Om du inte vill uppdatera distributions platserna där start avbildningen är lagrad avmarkerar du kryss rutan **Uppdatera distributions platser när** du är klar. Distributionsplatserna uppdateras som standard när startavbildningen uppdateras.  

    - Välj **Ja** i dialog rutan för att uppdatera start avbildningarna på distributions platser. Du kan inte använda enhets driv rutiner förrän de har distribuerats till distributions platser. Om du väljer **Nej**kör du åtgärden **Uppdatera distributions plats** innan du använder start avbildningen. Om driv rutins paketet aldrig har distribuerats måste du använda åtgärden **distribuera innehåll** i noden **driv rutins paket** .  

    - Configuration Manager varnar dig om arkitekturen för en eller flera driv rutiner inte matchar arkitekturen för de start avbildningar som du har valt. Om de inte matchar väljer du **OK**. Gå tillbaka till sidan med **driv rutins information** och rensa de driv rutiner som inte matchar arkitekturen i den valda start avbildningen. Om du till exempel väljer en x64- och x86-startavbildning måste alla drivrutiner ha stöd för båda arkitekturerna. Om du till exempel väljer en x64-startavbildning måste alla drivrutiner ha stöd för x64-arkitekturen.  

        > [!NOTE]
        > - Arkitekturen baseras på arkitekturen som rapporteras i INF-filen från tillverkaren.  
        > - Om en drivrutin rapporterar stöd för båda arkitekturerna kan du importera den till valfri startavbildning.  

    - Configuration Manager varnar dig om du lägger till enhets driv rutiner som inte är nätverks-eller lagrings driv rutiner i en start avbildning. I de flesta fall är de inte nödvändiga för start avbildningen. Välj **Ja** om du vill lägga till driv rutinerna i Start avbildningen eller **Nej** om du vill gå tillbaka och ändra valet av driv rutin.  

    - Configuration Manager varnar om en eller flera av de valda driv rutinerna inte är korrekt digitalt signerade. Välj **Ja** om du vill fortsätta eller Välj **Nej** om du vill gå tillbaka och göra ändringar i valet av driv rutin.  


### <a name="additional-actions-for-device-drivers"></a><a name="BKMK_DriverActions"></a>Ytterligare åtgärder för enhets driv rutiner  

Du kan utföra ytterligare åtgärder för att hantera driv rutiner när du väljer dem i noden **driv rutiner** .  

#### <a name="categorize"></a>Kategorisera
Rensar, hanterar eller anger en administrativ kategori för de valda driv rutinerna.

#### <a name="delete"></a>Ta bort
Tar bort driv rutinen från noden **driv rutiner** och tar också bort driv rutinen från de associerade distributions platserna.

#### <a name="disable"></a>Inaktivera
Förhindrar att driv rutinen installeras. Den här åtgärden inaktiverar tillfälligt driv rutinen. Aktivitetssekvensen kan inte installera en inaktive rad driv rutin när du distribuerar ett operativ system. 

> [!Note]  
> Den här åtgärden förhindrar bara att driv rutiner installeras med hjälp av steget **automatisk användning av driv Rutinens** aktivitetssekvens.

#### <a name="enable"></a>Aktivera
Låter Configuration Manager klient datorer och aktivitetssekvenser installera enhets driv rutinen när du distribuerar operativ systemet.

#### <a name="move"></a>Flytta
Enhetsdrivrutinen flyttas till en annan mapp i noden **Drivrutiner** .

#### <a name="properties"></a>Egenskaper
Öppnar dialog rutan **Egenskaper** . Granska och ändra egenskaperna för driv rutinen. Du kan till exempel ändra dess namn och beskrivning, aktivera eller inaktivera det och ange vilka plattformar som den kan köras på.



## <a name="use-task-sequences-to-install-drivers"></a><a name="BKMK_TSDrivers"></a>Använda aktivitetssekvenser för att installera driv rutiner  

Använd aktivitetssekvenser för att automatisera hur operativ systemet distribueras. Varje steg i aktivitetssekvensen kan utföra en speciell åtgärd, till exempel att installera en driv rutin. Du kan använda följande två steg för att installera enhets driv rutiner när du distribuerar ett operativ system:  

- [Använd drivrutiner automatiskt](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): Det här steget kan användas för automatisk matchning och installation av enhetsdrivrutiner inom ramen för operativsystemsdistributionen. Du kan konfigurera steget aktivitetssekvens så att endast den bäst matchade driv rutinen installeras för varje identifierad maskin varu enhet. Alternativt kan du ange att steget installerar alla kompatibla driv rutiner för varje identifierad maskin varu enhet och låt Installationsprogrammet för Windows välja den bästa driv rutinen. Du kan också ange en driv rutins kategori för att begränsa de driv rutiner som är tillgängliga för det här steget.  

- [Använd drivrutinspaket](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): Med det här steget kan du göra alla enhetsdrivrutiner i ett visst drivrutinspaket tillgängliga för Windows Setup. I de specificerade drivenhetspaketen söker Windows Setup efter de enhetsdrivrutiner som krävs. När du skapar fristående media måste du använda det här steget för att installera enhetsdrivrutiner.  

När du använder dessa steg i aktivitetssekvensen kan du också ange hur driv rutinerna ska installeras på den dator där du distribuerar operativ systemet. Mer information finns i [Hantera aktivitetssekvenser för att automatisera uppgifter](../deploy-use/manage-task-sequences-to-automate-tasks.md).  



## <a name="driver-reports"></a><a name="BKMK_DriverReports"></a>Driv rutins rapporter  

Du kan använda flera rapporter i rapportkategorin **Drivrutinshantering** för att avgöra allmän information om enhetsdrivrutinerna i drivenhetskatalogen. Mer information om rapporter finns i [Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md).

