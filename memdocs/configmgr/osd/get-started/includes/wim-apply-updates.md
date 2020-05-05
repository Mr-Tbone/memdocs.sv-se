---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/28/2019
ms.openlocfilehash: e5c15556a7a8dd91db3ae2c4aa4f9830abc8e430
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724113"
---
## <a name="apply-software-updates-to-an-image"></a><a name="BKMK_OSImagesApplyUpdates"></a>Tillämpa program uppdateringar på en avbildning

> [!Note]  
> Det här avsnittet gäller för både **OS-avbildningar** och **uppgraderings paket för operativ system**. Den använder den allmänna termen "image" för att referera till avbildnings filen för Windows (WIM). Båda dessa objekt har en WIM-fil som innehåller Windows-installationsfiler. Program uppdateringar gäller för de här filerna i båda objekten. Beteendet för den här processen är samma som båda objekten.  

Varje månad finns nya program uppdateringar som gäller för avbildningen. Innan du kan tillämpa program uppdateringar på den måste du ha följande krav:

- En infrastruktur för program uppdateringar  
- Program uppdateringarna har synkroniserats  
- Laddade ned program uppdateringarna till innehålls biblioteket på plats servern  

Mer information finns i [distribuera program uppdateringar](../../../sum/deploy-use/deploy-software-updates.md).  

Tillämpa tillämpliga program uppdateringar på en avbildning enligt ett angivet schema. Den här processen kallas ibland *offline-betjäning*. I det här schemat använder Configuration Manager de valda program uppdateringarna på avbildningen. Den kan även distribuera om den uppdaterade avbildningen till distributions platser.

> [!Important]  
> Även om du kan välja en program uppdatering som är tillämplig på avbildningen baserat på version, kan DISM endast tillämpa vissa typer av uppdateringar på avbildningen. Filen **OfflineServicingMgr. log** visar följande post: `Not applying this update binary, it is not supported`.<!-- SCCMDocs issue 1324 -->

Plats databasen innehåller information om avbildningen, inklusive de program uppdateringar som tillämpades vid import tillfället. Program uppdateringar som du tillämpar på avbildningen sedan den först lades till lagras också i plats databasen. När du startar guiden för att tillämpa program uppdateringar hämtar den listan över tillämpliga program uppdateringar som webbplatsen ännu inte har tillämpat på avbildningen. Configuration Manager kopierar de program uppdateringar som du väljer från innehålls biblioteket på plats servern. Sedan tillämpas program uppdateringarna på avbildningen.  

### <a name="servicing-process"></a>Underhålls process

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj sedan antingen **operativ Systems avbildningar** eller **uppgraderings paket för operativ system**.  

2. Välj det objekt som program uppdateringarna ska tillämpas på.  

3. I menyfliksområdet väljer du **Schemalägg uppdateringar** för att starta guiden.  

4. På sidan **Välj uppdateringar** väljer du de program uppdateringar som ska tillämpas på avbildningen. Det kan ta lite tid innan listan med uppdateringar visas i guiden. Använd **filtret** för att söka efter strängar i metadata. Använd List rutan **system arkitektur** för att filtrera på **x86**, **x64**eller **alla**. Du kan välja en, många eller alla uppdateringar i listan. När du är klar med att välja uppdateringar väljer du **Nästa**.  

5. På sidan **Schemalägg** anger du följande inställningar och klickar sedan på **Nästa**.  

    1. **Schema**: Ange schemat för när platsen tillämpar program uppdateringarna på avbildningen.  

    2. **Fortsätt vid fel**: Välj det här alternativet om du vill att program uppdateringarna ska fortsätta tillämpas på avbildningen även när det uppstår ett fel.  

    3. **Uppdatera distributions platser med avbildningen**: Välj det här alternativet om du vill uppdatera avbildningen på distributions platser efter att platsen har tillämpat program uppdateringarna.  

6. Slutför guiden schemalagda uppdateringar.  

> [!NOTE]  
> För att minimera nytto Last storleken tar installationen av OS-uppgraderings paket och OS-avbildningar bort den äldre versionen.  

### <a name="servicing-operations"></a>Underhålls åtgärder

I Configuration Manager-konsolen, i noden **operativ system avbildningar** eller **operativ system uppgraderings paket** , lägger du till följande kolumner i vyn:

- **Schemalagt uppdaterings datum**: den här egenskapen visar nästa schema som du har definierat.  
- **Status för schemalagda uppdateringar**: den här egenskapen visar status. Till exempel **lyckad** eller **pågående**.  

Välj ett särskilt avbildnings objekt och växla sedan till fliken **uppdaterings status** i informations fönstret. På den här fliken visas en lista med uppdateringar i avbildningen.

Välj ett särskilt avbildnings objekt och välj **Egenskaper** i menyfliksområdet. På fliken **installerade uppdateringar** visas en lista med uppdateringar i avbildningen. Fliken **Underhåll** är en skrivskyddad vy av det aktuella underhålls schemat och de uppdateringar som du har schemalagt att tillämpa.

När statusen är **i processen**kan du välja **Avbryt schemalagda uppdateringar** i menyfliksområdet. Den här åtgärden avbryter den aktiva underhålls processen.

Du kan felsöka den här processen genom att visa filerna **OfflineServicingMgr. log** och **DISM. log** på plats servern. Mer information finns i [loggfiler](../../../core/plan-design/hierarchy/log-files.md).

### <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_servicing-drive"></a>Ange enhet för etablering av OS-avbildning offline

<!--1358924-->

Från och med version 1810 anger du den enhet som Configuration Manager använder under offlineunderhåll av OS-avbildningar. Den här processen kan förbruka en stor mängd disk utrymme med temporära filer. Med det här alternativet kan du välja vilken enhet som ska användas.

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** . I menyfliksområdet klickar du på **Konfigurera plats komponenter** och väljer **operativ Systems distribution**.  

2. På fliken **offlineunderhåll väljer du alternativet** för **en lokal enhet som ska användas vid offlineunderhåll av avbildningar**.  

Som standard är den här inställningen **Automatisk**. Med det här värdet väljer Configuration Manager den enhet där den är installerad.

Om du väljer en enhet som inte finns på plats servern har Configuration Manager beter sig på samma sätt som om du väljer **Automatisk**.

Under offlineunderhåll kan Configuration Manager lagra temporära filer i mappen `<drive>:\ConfigMgr_OfflineImageServicing`. Den monterar även OS-avbildningen i den här mappen.

### <a name="optimized-image-servicing"></a><a name="bkmk_resetbase"></a>Optimerad avbildnings underhåll

<!--3555951-->

Från och med version 1902 finns det ett nytt alternativ för att optimera utdata genom att ta bort alla ersatta uppdateringar när du använder program uppdateringar på en operativ system avbildning. Optimeringen av offlineunderhåll gäller bara för avbildningar med ett enda index.

När du schemalägger platsen för att tillämpa program uppdateringar på en operativ system avbildning, används kommando rads verktyget DISM (Windows Deployment Image Servicing and Management). Under underhålls processen introducerar den här ändringen följande två ytterligare steg:  

- Den Kör DISM mot den monterade offline-avbildningen med `/Cleanup-Image /StartComponentCleanup /ResetBase`parametrarna. Om det här kommandot Miss lyckas, Miss lyckas den aktuella underhålls processen. Den genomför inga ändringar i avbildningen.  

- När Configuration Manager genomför ändringar i avbildningen och demonterar den från fil systemet, exporteras avbildningen till en annan fil. I det här steget används DISM `/Export-Image`-parametern. Den tar bort onödiga filer från avbildningen, vilket minskar storleken.  

Microsoft rekommenderar att du regelbundet installerar uppdateringar för dina offline-avbildningar. Du behöver inte använda det här alternativet varje gång du ska underhålla en avbildning. När du utför den här processen varje månad ger det här nya alternativet den bästa fördelen genom att använda det över tid. Mer information finns i [rekommendationer för att installera program uppdaterings steg](../../understand/install-software-updates.md#recommendations).

Även om det här alternativet bidrar till att minska den totala storleken på den förbrukade avbildningen tar det längre tid att slutföra processen. Använd guiden för att schemalägga underhåll under lämpliga tider. Det kräver också ytterligare lagrings utrymme på plats servern. Du kan anpassa platsen så att den använder en annan plats. Mer information finns i [ange enhet för etablering av OS-avbildningar](#bkmk_servicing-drive).

#### <a name="process-to-optimize-image-servicing"></a>Process för att optimera avbildnings underhåll

1. Starta [underhålls processen](#servicing-process).  

2. På sidan **Ange schema** väljer du alternativet för att **ta bort ersatta uppdateringar när avbildningen har uppdaterats**. Det här alternativet aktive ras inte automatiskt. Om avbildningen har fler än ett index kan du inte använda det här alternativet.  

3. Slutför guiden för att schemalägga avbildnings underhåll.  

Verifiera och övervaka processen med hjälp av **OfflineServicing. log**.
