---
title: Skapa en aktivitetssekvens för att installera ett operativsystem
titleSuffix: Configuration Manager
description: Använd aktivitetssekvenser i Configuration Manager för att automatiskt installera en operativ system avbildning och annat innehåll på en måldator.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e1b298856edea3f81cab2e9cd5ab75af49dff51
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723014"
---
# <a name="create-a-task-sequence-to-install-an-os"></a>Skapa en aktivitetssekvens för att installera ett operativsystem

*Gäller för: Configuration Manager (aktuell gren)*

Använd aktivitetssekvenser i Configuration Manager för att automatiskt installera en operativ system avbildning på en måldator. Du skapar en aktivitetssekvens som refererar till en start avbildning som används för att starta mål datorn, operativ system avbildningen som du vill installera på mål datorn och eventuellt ytterligare innehåll, till exempel andra program eller program uppdateringar som du vill installera. Sedan distribuerar du aktivitetssekvensen till en samling som innehåller måldatorn.  

## <a name="create-a-task-sequence-to-install-an-os"></a><a name="BKMK_InstallOS"></a>Skapa en aktivitetssekvens för att installera ett operativ system

Det finns flera scenarier för att distribuera ett operativ system till datorer i din miljö. I de flesta fall skapar du en aktivitetssekvens och väljer **Installera ett befintligt avbildnings paket** i guiden skapa aktivitetssekvens. Med det här alternativet skapas en aktivitetssekvens som installerar operativ systemet, migrerar användar inställningar, tillämpar program uppdateringar och installerar program.

### <a name="prerequisites"></a>Krav

Innan du skapar en aktivitetssekvens för att installera ett operativ system måste följande krav vara på plats:

#### <a name="required"></a>Krävs

- En [Start avbildning](../get-started/manage-boot-images.md)  

- En [OS-avbildning](../get-started/manage-operating-system-images.md)  

#### <a name="required-if-used"></a>Obligatoriskt (om det används)

- Synkronisera [program uppdateringar](../../sum/get-started/synchronize-software-updates.md)  

- Lägg till [program](../../apps/deploy-use/create-applications.md)  

### <a name="process-to-create-a-task-sequence-that-installs-an-os"></a>Process för att skapa en aktivitetssekvens som installerar ett operativ system  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **operativ system**och väljer noden **aktivitetssekvenser** .  

2. Välj **skapa**aktivitetssekvens i gruppen **skapa** på fliken **Start** i menyfliksområdet. Den här åtgärden startar guiden skapa aktivitetssekvens.  

3. På sidan **skapa en ny aktivitetssekvens** väljer du **Installera ett befintligt avbildnings paket**och väljer sedan **Nästa**.  

4. På sidan **information om aktivitetssekvens** anger du följande inställningar:  

    - **Namn på aktivitetssekvens**: Ange ett namn på aktivitetssekvensen.  

    - **Beskrivning**: Ange en beskrivning av vad aktivitetssekvensen gör.  

    - **Start avbildning**: Ange den Start avbildning som aktivitetssekvensen använder för att installera operativ systemet på mål datorn. Start avbildningen innehåller en version av Windows PE plus eventuella ytterligare nödvändiga enhets driv rutiner. Mer information finns i [Hantera start avbildningar](../get-started/manage-boot-images.md).  

        > [!IMPORTANT]  
        > Startavbildningens arkitektur måste vara kompatibel med måldatorns maskinvaruarkitektur.  

5. På sidan **Installera Windows** anger du följande inställningar:  

    - **Avbildnings paket**: Ange det paket som innehåller den operativ Systems avbildning som ska installeras. Mer information finns i [hantera OS-avbildningar](../get-started/manage-operating-system-images.md).  

    - **Avbildning**: om avbildnings paketet för operativ systemet har flera avbildningar anger du index för den OS-avbildning som ska installeras.  

    - **Partitionera och formatera mål datorn installera operativ systemet**: Ange om du vill att aktivitetssekvensen ska partitionera och formatera mål datorn innan operativ systemet installeras.  

    - **Produkt nyckel**: Ange produkt nyckeln för Windows, om det behövs. Du kan ange kodade volymlicensnycklar och standardproduktnycklar. Om du använder en icke-kodad produkt nyckel måste varje grupp med fem tecken avgränsas med ett streck`-`(). Till exempel: *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*  

    - **Serverlicensieringsläge**: Ange att serverlicensen är **Per plats**, **Per server**eller att ingen licens har angetts. Om serverlicensen gäller **Per server** anger du också det högsta antalet serveranslutningar.  

    - Ange hur du vill hantera administratörs kontot för det nya operativ systemet:  

        - **Generera slumpmässigt lösen ord för det lokala administratörs kontot och inaktivera kontot på den plattform som stöds (rekommenderas)**: Windows inaktiverar det lokala administratörs kontot när AKTIVITETSSEKVENSEN distribuerar OS-avbildningen.  

        - **Aktivera kontot och ange lösen ord för den lokala administratören**: Windows använder samma lösen ord för det lokala administratörs kontot på alla datorer där aktivitetssekvensen distribuerar operativ system avbildningen.  

6. På sidan **Konfigurera nätverk** anger du följande inställningar:  

    - **Anslut till en arbets grupp**: Lägg till mål datorn i en arbets grupp.  

    - **Anslut till en domän**: Lägg till mål datorn i en domän. Ange namnet på domänen i **Domän**.  

        > [!IMPORTANT]  
        > Du kan bläddra efter domäner i den lokala skogen men du måste ange domännamnet för en fjärransluten skog.  

        Du kan också ange en organisationsenhet (OU) i fältet **domän organisationsenhet** . Den här inställningen är valfri och anger det LDAP X. 500-unika namnet för ORGANISATIONSENHETen. Om den inte redan finns skapar Windows dator kontot i ORGANISATIONSENHETen.  

    - **Konto**: användar namn och lösen ord för det konto som har behörighet att ansluta till den angivna domänen. Exempel: *domän\användare* eller *%variable%*.  

        > [!IMPORTANT]  
        > Om du planerar att migrera domän inställningarna eller arbets grupps inställningarna anger du lämpliga domänautentiseringsuppgifter.  

7. På sidan **installera Configuration Manager** anger du det Configuration Manager-klient paket som ska installeras på mål datorn. Du kan även inkludera eventuella installations egenskaper.  

8. Ange följande information **på sidan tillståndsmigrering** :  

    - **Avbilda användar inställningar**: aktivitetssekvensen fångar användar tillstånd. Mer information om hur du avbildar och återställer användar tillstånd finns i [hantera användar tillstånd](../get-started/manage-user-state.md).  

    - **Avbilda nätverks inställningar**: aktivitetssekvensen fångar nätverks inställningar från mål datorn. Den samlar in medlemskapet i domänen eller arbets gruppen, även nätverkskortets inställningar.  

    - **Avbilda Microsoft Windows-inställningar**: aktivitetssekvensen fångar Windows-inställningar från mål datorn innan operativ Systems avbildningen installeras. Den samlar in dator namn, registrerat användar-och organisations namn samt tids zons inställningarna.  

9. På sidan **Inkludera uppdateringar** anger du om nödvändiga program uppdateringar, program uppdateringar eller inga program uppdateringar ska installeras. Om du anger att program uppdateringarna ska installeras, installerar Configuration Manager bara de program uppdateringar som är riktade mot de samlingar som mål datorn är medlem i.  

10. På sidan **installera program** anger du de program som ska installeras på mål datorn. Om du anger flera program kan du också ange att aktivitetssekvensen ska fortsätta om något program inte går att installera.  

11. Slutför guiden.  

Du kan nu distribuera aktivitetssekvensen till en samling datorer. Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md).


## <a name="pre-cache-content"></a>Innehåll i för cache

<!--4224642-->
Från och med version 1906 kan du aktivera den här typen av aktivitetssekvens för innehåll i förväg. Med funktionen för cachelagring för tillgängliga distributioner av aktivitetssekvenser kan klienter Ladda ned relevant innehåll innan en användare installerar aktivitetssekvensen.  

Mer information finns i [Konfigurera förinställt innehåll för cache](configure-precache-content.md).


## <a name="example-task-sequence"></a><a name="BKMK_InstallExistingOSImageTSExample"></a>Exempel på aktivitetssekvens

Använd följande tabell som en vägledning när du skapar en aktivitetssekvens som distribuerar ett operativ system med en befintlig avbildning. Tabellen hjälper dig att bestämma den allmänna ordningen för stegen i aktivitetssekvensen och hur du ordnar och strukturerar stegen i logiska grupper. Aktivitetssekvensen som du skapar kan skilja sig från det här exemplet och kan innehålla fler eller färre aktivitetssekvenssteg och grupper.  

> [!NOTE]  
> Använd guiden skapa aktivitetssekvens för att skapa den här aktivitetssekvensen.  
>
> När du använder guiden skapa aktivitetssekvens för att skapa den här nya aktivitetssekvensen, skiljer sig några av de olika steg namnen än vad de skulle vara om du manuellt lade till de här stegen i aktivitetssekvensen i en befintlig aktivitetssekvens.

|Aktivitetssekvensgrupp eller -steg|Beskrivning|  
|---------------------------------|-----------------|  
|Avbilda fil och inställningar – **(ny aktivitetssekvens)**|Skapa en aktivitetssekvensgrupp. En aktivitetssekvensgrupp samlar liknande aktivitetssekvenssteg för att få bättre organisation och kontroll över fel.<br /><br /> Den här gruppen innehåller de steg som krävs för att avbilda filer och inställningar från operativsystemet på en referensdator.|  
|Avbilda Windows-inställningar|Använd det här aktivitetssekvenssteget för att identifiera Microsoft Windows-inställningar som ska avbildas från referensdatorn. Du kan avbilda datornamn, användar- och organisationsinformation samt tidszonsinställningar.|  
|Avbilda nätverksinställningar|Använd det här aktivitetsekvenssteget för att samla in nätverksinställningar från referensdatorn. Du kan avbilda referensdatorns domän- eller arbetsgruppsmedlemskap och inställningsinformation för nätverkskortet.|  
|Avbilda användarfiler och inställningar – (ny underordnad **aktivitetssekvens)**|Skapa en aktivitetssekvensgrupp inom en aktivitetssekvensgrupp. Den här undergruppen innehåller de steg som krävs för att avbilda användartillståndsdata. På samma sätt som den första gruppen som du har lagt till, behåller den här under gruppen liknande steg i aktivitetssekvensen för bättre organisation och fel kontroll.|  
|Begär lagring av användartillstånd|Använd det här aktivitetssekvenssteget för att begära åtkomst till en tillståndsmigreringsplats där användartillståndsdata lagras. Du kan konfigurera det här aktivitetssekvenssteget om du vill avbilda och återställa information om användartillstånd.|  
|Avbilda användarfiler och inställningar|Använd den här aktivitetssekvensen för att använda User State Migration Tool (USMT) för att avbilda användar tillstånd och inställningar från referens datorn som ska ta emot den aktivitetssekvens som är associerad med det här uppgifts steget. Du kan avbilda standard alternativ eller konfigurera vilka alternativ som ska samlas in.|  
|Frisläpp lagring av användartillstånd|Använd det här aktivitetssekvenssteget för att meddela platsen för tillståndsmigrering att avbildnings- eller återställningsåtgärden har slutförts.|  
|Installera operativ system – **(ny aktivitetssekvens)**|Skapa en annan under grupp för aktivitetssekvens. Denna underordnade grupp innehåller de steg som krävs för att installera och konfigurera Windows PE-miljön.|  
|Starta om i Windows PE|Använd det här aktivitetssekvenssteget för att ange omstartsalternativ för måldatorn som tar emot denna aktivitetssekvens. Det här steget visar ett meddelande för användaren som anger att datorn kommer att starta om så att installationen kan fortsätta.<br /><br /> Det här steget använder den skrivskyddade aktivitetssekvensvariabeln **_SMSTSInWinPE** . Om det associerade värdet är lika med **falskt** fortsätter aktivitetssekvenssteget.|  
|Partitionsdisk 0|Det här aktivitetssekvenssteget anger de åtgärder som krävs för att formatera hårddisken på destinationsdatorn. Standarddisknumret är **0**.<br /><br /> Det här steget använder den skrivskyddade aktivitetssekvensvariabeln **_SMSTSClientCache** . Det här steget körs om Configuration Manager-klientcachen inte finns.|  
|Använd operativsystem|Använd det här aktivitetssekvenssteget för att installera en angiven operativsystemavbildning på måldatorn. Det här steget tar först bort alla filer på volymen, förutom eventuella Configuration Manager-/regionsspecifika styr filer. Den använder sedan alla volym avbildningar som finns i WIM-filen för motsvarande sekventiell disk volym på mål datorn. Du kan ange en **sysprep** -svarsfil och även konfigurera vilken diskpartition som används för installationen.|  
|Använd Windows-inställningar|Använd det här aktivitetssekvenssteget för att konfigurera konfigurationsinformation för Windows-inställningarna för måldatorn. Windows-inställningar som du kan tillämpa är användar- och organisationsinformation, produkt- eller licensnyckelinformation, tidszon och det lokala administratörslösenordet.|  
|Använd nätverksinställningar|Använd det här aktivitetssekvenssteget för att ange nätverks- eller arbetsgruppskonfigurationsinformation för måldatorn. Du kan även ange om datorn använder en DHCP-server eller så kan du tilldela IP-adressinformation statiskt.|  
|Använda enhetsdrivrutiner|Använd det här aktivitetssekvenssteget för att installera drivrutiner som en del av operativsystemets distribution. Du kan låta installationsprogrammet för Windows söka igenom alla befintliga drivrutinskategorier genom att markera **Överväg drivrutiner från alla kategorier** eller begränsa vilka drivrutinskategorier som installationsprogrammet för Windows söker igenom genom att välja **Begränsa matchning av drivrutiner till att endast överväga drivrutiner i valda kategorier**.<br /><br /> Det här steget använder den skrivskyddade aktivitetssekvensvariabeln **_SMSTSMediaType** . Den här aktivitetssekvensen körs bara om värdet för variabeln inte är lika med **FullMedia**.|  
|Använd drivrutinspaket|Använd det här aktivitetssekvenssteget för att göra alla enhetsdrivrutiner i ett drivrutinspaket tillgängliga för användning i Windows-installationen.|  
|Installera operativ system – **(ny aktivitetssekvens)**|Skapa en annan under grupp för aktivitetssekvens. Den här undergruppen innehåller de steg som krävs för att konfigurera det installerade operativsystemet.|  
|Installera Windows och ConfigMgr|Använd den här aktivitetssekvensen för att installera Configuration Manager-klient program varan. Configuration Manager installerar och registrerar Configuration Manager-klientens GUID. Du kan tilldela nödvändiga installationsparametrar i fönstret **Installationsegenskaper** .|  
|Installera uppdateringar|Använd det här aktivitetssekvenssteget för att ange hur programuppdateringar installeras på måldatorn. Mål datorn utvärderas inte för tillämpliga program uppdateringar förrän det här steget körs. I det här läget utvärderas mål datorn för program uppdateringar som liknar andra Configuration Manager-hanterade klienter.<br /><br /> Det här steget använder den skrivskyddade aktivitetssekvensvariabeln **_SMSTSMediaType** . Den här aktivitetssekvensen körs bara om värdet för variabeln inte är lika med **FullMedia**.|  
|Återställ användarfiler och inställningar – (ny underordnad **aktivitetssekvens)**|Skapa en annan under grupp för aktivitetssekvens. Den här undergruppen innehåller de steg som krävs för att återställa användarfiler och inställningar.|  
|Begär lagring av användartillstånd|Använd det här aktivitetssekvenssteget för att begära åtkomst till en tillståndsmigreringsplats där användartillståndsdata lagras.|  
|Återställ användarfiler och inställningar|Använd den här aktivitetssekvensen för att köra User State Migration Tool (USMT) för att återställa användar tillstånd och inställningar till en måldator.|  
|Frisläpp lagring av användartillstånd|Använd det här aktivitetssekvenssteget för att meddela platsen för tillståndsmigrering att användartillståndsdata inte längre behövs.|  
