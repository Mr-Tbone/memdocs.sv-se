---
title: Hantera avbildningar av operativsystem
titleSuffix: Configuration Manager
description: Läs om metoderna för att hantera OS-avbildningar som lagras i WIM-filer (Windows Image).
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2f8b8a45ff83ce903f5737c94144e6ca5ab50826
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697661"
---
# <a name="manage-os-images-with-configuration-manager"></a>Hantera OS-avbildningar med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

OS-avbildningar i Configuration Manager lagras i fil formatet WIM (Windows Image). De här avbildningarna är en komprimerad samling av indexfiler och mappar som används för att installera och konfigurera ett nytt operativ system på en dator. Många distributions scenarier för operativ system kräver en operativ system avbildning.


## <a name="os-image-types"></a>Typer av operativ system avbildningar

Du kan använda en [standard operativ system avbildning](#default-image)eller bygga operativ system avbildningen från en [referens dator](#bkmk_capture) som du konfigurerar. När du skapar referens datorn lägger du till OS-filer, driv rutiner, stödfiler, program uppdateringar, verktyg och program till operativ systemet. Sedan samlar du in den för att skapa avbildnings filen.

### <a name="default-image"></a>Standardavbildning

Windows-installationsfilerna innehåller standard operativ system avbildningen. Den här avbildningen är en grundläggande operativ system avbildning som innehåller en standard uppsättning med driv rutiner. När du använder standard avbildningen av operativ systemet använder du stegen i aktivitetssekvensen för att installera appar och göra andra konfigurationer efter att operativ systemet har installerats på en enhet. Leta upp standard operativ system avbildningen i Windows-källfilerna: `\Sources\install.wim` .  

#### <a name="default-image-advantages"></a>Fördelar med standard avbildning

- Bildstorleken är mindre än en avbildning.  

- Att installera appar och konfigurationer med stegen i aktivitetssekvensen är mer dynamisk. Du kan till exempel ändra konfigurationerna och apparna som installeras i aktivitetssekvensen utan att behöva göra en avbildning av enheten.  

#### <a name="default-image-disadvantages"></a>Förfördelning av standard avbildningar

- OS-installationen kan ta längre tid. Programinstallationen och andra konfigurationer sker när OS-installationen har slutförts.  


### <a name="captured-image-from-a-reference-computer"></a><a name="bkmk_capture"></a> Avbildning från en referens dator

Skapa en anpassad operativ system avbildning genom att skapa en referens dator med önskat operativ system. Installera sedan program och konfigurera inställningar. Skapa WIM-filen genom att avbilda operativ system avbildningen från referens datorn. Bygg referens datorn manuellt eller Använd en aktivitetssekvens för att automatisera några eller alla Bygg steg. Mer information finns i [Anpassa OS-avbildningar](customize-operating-system-images.md).  

#### <a name="captured-image-advantages"></a>Avbildnings fördelar

- Installationen kan gå fortare än att använda standardavbildningen. Till exempel kan program förinstalleras med avbildningen med avbildningen. Sedan behöver du inte installera samma program senare med hjälp av aktivitetssekvenser.  

#### <a name="captured-image-disadvantages"></a>Avfördelning av avbildningar

- Bild storleken är eventuellt större än standard avbildningen.  

- Du måste skapa en ny avbildning om du behöver uppdateringar för program och verktyg.  


## <a name="add-an-os-image"></a><a name="BKMK_AddOSImages"></a> Lägg till en OS-avbildning  

Innan du kan använda en operativ system avbildning kan du lägga till den på Configuration Manager-platsen.

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj sedan noden **operativ Systems avbildningar** .  

2. Välj **Lägg till operativ system avbildning**i gruppen **skapa** på fliken **Start** i menyfliksområdet. Den här åtgärden startar guiden Lägg till operativ Systems avbildning.  

3. På sidan **data källa** anger du följande information:

    - Nätverks **Sök väg** till avbildnings filen för operativ systemet. Till exempel `\\server\share\path\image.wim`.

    - **Extrahera ett specifikt avbildnings index från den angivna wim-filen** och välj sedan ett bild index i listan.<!--3719699--> Från och med version 1902 importerar det här alternativet automatiskt ett enskilt index i stället för alla bild index i filen. Med det här alternativet resulterar det i en mindre bildfil och snabbare offlineunderhåll. Det stöder också processen för att [optimera avbildnings underhåll](#bkmk_resetbase)för en mindre bildfil efter att ha tillämpat program uppdateringar.  

        > [!Note]  
        > Configuration Manager ändrar inte käll avbildnings filen. Den skapar en ny avbildnings fil i samma käll katalog.
        >
        > Extraherings processen kan inte utföras för extremt stora bildfiler, till exempel över 60 GB. DISM-felet är `Not enough storage is available to process this command.` kommando raden som Configuration Manager använder finns i SMSProv. log och DISM. log. Kör samma kommando manuellt och importera sedan avbildningen.<!-- SCCMDocs-pr issue 3502 -->  

    - Från och med version 1906, om du vill förcachelagra innehåll på en klient, anger du avbildningens **arkitektur** och **språk** . Mer information finns i [Konfigurera förinställt innehåll för cache](../deploy-use/configure-precache-content.md).<!--4224642-->  

4. På sidan **Allmänt** anger du följande information. Den här informationen är användbar i identifierings syfte när du har mer än en operativ system avbildning.  

    - **Namn**: ett unikt namn för avbildningen. Som standard kommer namnet från WIM-filnamnet.  

    - **Version**: en valfri versions identifierare. Den här egenskapen behöver inte vara operativ systemets version av avbildningen. Det är ofta organisationens version av paketet.  

    - **Kommentar**: en valfri kort beskrivning.  

5. Slutför guiden.  

För PowerShell-cmdlet motsvarigheten till den här konsol guiden, se [New-CMOperatingSystemImage](/powershell/module/configurationmanager/new-cmoperatingsystemimage?view=sccm-ps).

Distribuera sedan OS-avbildningen till distributions platser.  


## <a name="distribute-content-to-distribution-points"></a><a name="BKMK_DistributeBootImages"></a> Distribuera innehåll till distributions platser  

Distribuera OS-avbildningar till distributions platser på samma sätt som andra innehåll. Innan du distribuerar aktivitetssekvensen distribuerar du operativ system avbildningen till minst en distributions plats. Mer information finns i avsnittet [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  


[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]


## <a name="prepare-the-os-image-for-multicast-deployments"></a><a name="BKMK_OSImageMulticast"></a> Förbered OS-avbildningen för multicast-distributioner  

Använd multicast-distributioner om du vill att mer än en dator ska kunna hämta en operativ system avbildning samtidigt. Avbildningen är multicast till klienter av distributions platsen, i stället för varje klient som laddar ned en kopia av avbildningen från distributions platsen via en separat anslutning. När du väljer distributions metoden för operativ systemet för att [använda multicast för att distribuera Windows via nätverket](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)konfigurerar du operativ system avbildningen så att den stöder multicast. Distribuera sedan avbildningen till en multicast-aktiverad distributions plats.

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj sedan noden **operativ Systems avbildningar** .  

2. Välj den OS-avbildning som du vill distribuera till en multicast-aktiverad distributions plats.  

3. Välj **Egenskaper**i gruppen **Egenskaper** på fliken **Start** i menyfliksområdet.  

4. Växla till fliken **distributions inställningar** och konfigurera följande alternativ:  

    - **Tillåt att det här paketet överförs via multicast (endast WinPE)**: Välj det här alternativet för Configuration Manager om du vill distribuera OS-avbildningar samtidigt med hjälp av multicast.  

    - **Kryptera multicast-paket**: Ange om platsen ska kryptera avbildningen innan den skickas till distributions platsen. Använd det här alternativet om avbildningen innehåller känslig information. Om bilden inte är krypterad visas dess innehåll i klartext i nätverket. En obehörig användare kan fånga upp och visa innehållet i bilden.  

    - **Överför det här paketet endast via multicast**: Ange om distributionsplatsen ska distribuera avbildningen endast i en multicast-session.  

         Om du väljer **överför det här paketet endast via multicast**måste du också ange distributions alternativet för aktivitetssekvensen för att **Ladda ned innehåll lokalt när det behövs för aktivitetssekvensen som körs**. Mer information finns i [Distribuera en aktivitetssekvens](../deploy-use/deploy-a-task-sequence.md).  

5. Välj **OK** för att spara inställningarna och Stäng avbildnings egenskaperna.