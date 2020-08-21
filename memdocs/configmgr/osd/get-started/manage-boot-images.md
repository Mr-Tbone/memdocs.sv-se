---
title: Hantera startavbildningar
titleSuffix: Configuration Manager
description: I Configuration Manager kan du läsa om hur du hanterar de Windows PE-startavbildningar som du använder under en operativ Systems distribution.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 74b8b0f29172140a19c402c79b7ea9b7339cf3e5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697644"
---
# <a name="manage-boot-images-with-configuration-manager"></a>Hantera start avbildningar med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

En start avbildning i Configuration Manager är en [Windows PE](/windows-hardware/manufacture/desktop/winpe-intro) -avbildning (WinPE) som används under en operativ Systems distribution. Start avbildningar används för att starta en dator i WinPE. Detta minimala operativ system innehåller begränsade komponenter och tjänster. Configuration Manager använder WinPE för att förbereda mål datorn för Windows-installation.

## <a name="default-boot-images"></a><a name="BKMK_BootImageDefault"></a> Standard start avbildningar

Configuration Manager tillhandahåller två standard start avbildningar: en som stöder x86-plattformar och en som stöder x64-plattformar. De här avbildningarna lagras i mapparna *x64* eller *i386* i följande resurs på plats servern: `\\<SiteServerName>\SMS_<sitecode>\osd\boot\` . Standard start avbildningarna uppdateras eller återskapas beroende på vilken åtgärd du utför.

Tänk på följande om några av de åtgärder som beskrivs för standard start avbildningar:

- Käll driv rutins objekt måste vara giltiga. Dessa objekt inkluderar källfilerna för driv rutinen. Om objekten inte är giltiga, lägger platsen inte till driv rutinerna i Start avbildningarna.  

- Start avbildningar som inte baseras på standard start avbildningarna, även om de använder samma Windows PE-version, ändras inte.  

- Distribuera om de ändrade start avbildningarna till distributions platser.  

- Återskapa alla media som använder de ändrade start avbildningarna.  

- Om du inte vill att dina anpassade/standard start avbildningar ska uppdateras automatiskt ska du inte lagra dem på standard platsen.  

> [!NOTE]
> Configuration Manager logg verktyget (**CMTrace**) läggs till i alla start avbildningar i **program varu biblioteket**. Starta verktyget genom att skriva `cmtrace` från kommando tolken när du är i Windows PE.
>
> CMTrace är standard visnings programmet för loggfiler i Windows PE.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Använd uppdateringar och underhåll för att installera den senaste versionen av Configuration Manager

När du uppgraderar Windows Assessment and Deployment Kit (ADK)-versionen och sedan använder uppdateringar och underhåll för att installera den senaste versionen av Configuration Manager, återskapar platsen standard start avbildningarna. Den här uppdateringen innehåller den nya WinPE-versionen från den uppdaterade Windows ADK, den nya versionen av Configuration Manager-klienten, driv rutiner och anpassningar. Platsen ändrar inte anpassade Start avbildningar.

### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>Uppgradera från Configuration Manager 2012 till aktuell gren

När du uppgraderar Configuration Manager 2012 till den aktuella grenen återskapar platsen standard start avbildningarna. Den här uppdateringen innehåller den nya WinPE-versionen från den uppdaterade Windows ADK och den nya versionen av Configuration Manager-klienten. Alla anpassningar av start avbildningen förblir oförändrade. Platsen ändrar inte anpassade Start avbildningar.

### <a name="update-distribution-points-with-the-boot-image"></a>Uppdatera distributions platser med start avbildningen

När du använder åtgärden **Uppdatera distributions platser** från noden **Start avbildningar** i-konsolen, uppdaterar platsen mål start avbildningen med klient komponenter, driv rutiner och anpassningar.

Du kan läsa in start avbildningen igen med den senaste versionen av WinPE från installations katalogen för Windows ADK. Sidan **Allmänt** i guiden Uppdatera distributions platser innehåller följande information:

- Den aktuella Windows ADK-versionen som är installerad på plats servern
- Aktuell produktions klient version
- Windows ADK-versionen av WinPE i Start avbildningen
- Versionen av Configuration Manager-klienten i Start avbildningen

Om versionerna i Start avbildningen är inaktuella använder du alternativet för att **läsa in den här start avbildningen igen med den aktuella Windows PE-versionen från Windows ADK**.

> [!Important]  
> Den här åtgärden är tillgänglig för både standard-och anpassade Start avbildningar. Under den här processen för att läsa in start avbildningen behåller platsen inte några manuella anpassningar utanför Configuration Manager. Dessa anpassningar inkluderar tillägg från tredje part. Med det här alternativet återbyggs start avbildningen med den senaste versionen av WinPE och den senaste klient versionen. Endast de konfigurationer som du anger i egenskaperna för start avbildningen tillämpas igen. <!--SCCMDocs issue #1283-->

Noden **Start avbildningar** innehåller också en ny kolumn för (**klient version**). Använd den här kolumnen för att snabbt Visa Configuration Manager klient version i varje start avbildning.

## <a name="customize-a-boot-image"></a><a name="BKMK_BootImageCustom"></a> Anpassa en start avbildning  

När en start avbildning baseras på WinPE-versionen från den version av Windows ADK som stöds, kan du anpassa eller [ändra en start avbildning](#BKMK_ModifyBootImages) från-konsolen. När du uppgraderar en plats och installerar en ny version av Windows ADK, uppdateras inte anpassade Start avbildningar med den nya versionen av Windows ADK. När det händer kan du inte anpassa start avbildningarna i Configuration Manager-konsolen. De fortsätter dock att fungera som de gjorde före uppgraderingen.  

När en start avbildning baseras på en annan version av Windows ADK som är installerad på en plats måste du anpassa start avbildningarna. Använd en annan metod för att anpassa de här start avbildningarna, till exempel genom att använda kommando rads verktyget DISM (Deployment Image Servicing and Management). DISM är en del av Windows ADK. Mer information finns i [Anpassa Start avbildningar](customize-boot-images.md).  

## <a name="add-a-boot-image"></a><a name="BKMK_AddBootImages"></a> Lägg till en start avbildning  

Under plats installationen lägger Configuration Manager automatiskt till Start avbildningar som baseras på en WinPE-version från den version av Windows ADK som stöds. Beroende på vilken version av Configuration Manager kan du lägga till Start avbildningar baserat på en annan WinPE-version än den version av Windows ADK som stöds. Ett fel inträffar när du försöker lägga till en start avbildning som innehåller en version av WinPE som inte stöds. Följande lista är de Windows ADK-och WinPE-versioner som stöds för närvarande:

- Windows ADK-version: Windows ADK för Windows 10

- Windows PE-versioner för start avbildningar som går att anpassa från Configuration Manager-konsolen: Windows PE 10

- Windows PE-versioner som stöds för start avbildningar som *inte kan anpassas* från Configuration Manager-konsolen

  - Windows PE 3,1<sup>[Anmärkning 1](#bkmk_note1)</sup>

  - Windows PE 5

Använd exempelvis Configuration Manager-konsolen för att anpassa start avbildningar baserade på Windows PE 10 från Windows ADK för Windows 10. För en start avbildning som baseras på Windows PE 5, anpassar du den från en annan dator med hjälp av DISM-versionen från Windows ADK för Windows 8. Lägg sedan till den anpassade Start avbildningen i Configuration Manager-konsolen. Mer information finns i följande artiklar:

- [Anpassa startavbildningar](customize-boot-images.md)
- [Stöd för Windows 10 ADK](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)
- [Plattformar som stöds av DISM](/windows-hardware/manufacture/desktop/dism-supported-platforms)

<a name="bkmk_note1"></a>

> [!NOTE]
> **Anmärkning 1: stöd för Windows PE 3,1**
>
> Lägg endast till en start avbildning i Configuration Manager baserat på Windows PE *version 3,1*. Uppgradera Windows AIK för Windows 7 (baserat på Windows PE 3,0) med tillägget Windows AIK för Windows 7 SP1 (baserat på Windows PE 3,1). Hämta tillägget Windows AIK för Windows 7 SP1 från [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188).  

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj sedan noden **Start avbildningar** .  

2. Välj **Lägg till Start avbildning**i gruppen **skapa** på fliken **Start** i menyfliksområdet. Den här åtgärden startar guiden Lägg till Start avbildning.  

3. På sidan **data källa** anger du följande alternativ:  

    - I rutan **Sökväg** anger du sökvägen till WIM-filen med startavbildningen. Den angivna sökvägen måste vara en giltig nätverkssökväg i UNC-format. Exempel: `\\ServerName\ShareName\BootImageName.wim`

    - Välj startavbildningen i den nedrullningsbara listan **Startavbildningsfil**. Om WIM-filen innehåller flera start avbildningar väljer du lämplig avbildning.  

4. På sidan **Allmänt** anger du följande alternativ:  

    - I rutan **Namn** anger du ett unikt namn på startavbildningen.  

    - I rutan **Version** anger du ett versionsnummer för startavbildningen.  

    - I rutan **kommentar** anger du en kort beskrivning av hur du använder start avbildningen.  

5. Slutför guiden.  

Start avbildningen visas nu i noden **Start avbildning** . Innan du använder start avbildningen för att distribuera ett operativ system distribuerar du Start avbildningen till distributions platser.

> [!Tip]  
> I noden **Start avbildning** i-konsolen visar kolumnen **storlek (KB)** den okomprimerade storleken för varje start avbildning. När platsen skickar en start avbildning över nätverket skickas en komprimerad kopia. Den här kopian är vanligt vis mindre än den storlek som anges i kolumnen **storlek (KB)** .  

## <a name="distribute-boot-images"></a><a name="BKMK_DistributeBootImages"></a> Distribuera start avbildningar  

Du distribuerar startavbildningar till distributionsplatser på samma sätt som du distribuerar annat innehåll. Innan du distribuerar ett operativ system eller skapar media måste du distribuera start avbildningen till minst en distributions plats.

Mer information om hur du distribuerar en start avbildning finns i [distribuera innehåll](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

Om du vill använda PXE för att distribuera ett operativ system bör du tänka på följande innan du distribuerar start avbildningen:  

- Konfigurera distributions platsen så att den accepterar PXE-begäranden.  
- Distribuera både en x86-och en x64 PXE-aktiverad start avbildning till minst en PXE-aktiverad distributions plats.  
- Configuration Manager distribuerar start avbildningarna till mappen **RemoteInstall** på den PXE-aktiverade distributions platsen.  
  
Mer information om hur du använder PXE för att distribuera operativ system finns i [använda PXE för att distribuera Windows via nätverket](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## <a name="modify-a-boot-image"></a><a name="BKMK_ModifyBootImages"></a> Ändra en start avbildning  

Lägg till eller ta bort enhets driv rutiner i avbildningen eller redigera egenskaperna för start avbildningen. De driv rutiner som du lägger till eller tar bort kan omfatta nätverks-eller lagrings driv rutiner. Tänk på följande när du ändrar startavbildningar:  

- Innan du lägger till driv rutiner i Start avbildningen importerar du och aktiverar dem i enhets driv rutins katalogen.  

- När du ändrar en start avbildning ändrar inte start avbildningen något av de associerade paketen som start avbildningen refererar till.  

- När du har gjort ändringar i en start avbildning **uppdaterar** du Start avbildningen på de distributions platser där den redan finns. Den här processen gör den senaste versionen av start avbildningen tillgänglig för klienter. Mer information finns i [Hantera innehåll som du har distribuerat](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="modify-the-properties-of-a-boot-image"></a>Ändra egenskaperna för en start avbildning  

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj sedan noden **Start avbildningar** .  

2. Markera den startavbildning som du vill ändra.  

3. Välj **Egenskaper**i gruppen **Egenskaper** på fliken **Start** i menyfliksområdet.  

4. Ange följande inställningar för att ändra startavbildningens uppträdande:  

#### <a name="images"></a>Avbildningar

Om du ändrar egenskaperna för start avbildningen med hjälp av ett externt verktyg på fliken **avbildningar** väljer du **Läs in igen**.  

#### <a name="drivers"></a>Drivrutiner

På fliken **driv rutiner** lägger du till de Windows-drivrutiner som WinPE kräver för att starta. Tänk på följande när du lägger till enhets driv rutiner:  

- Kontrol lera att de driv rutiner som du lägger till i Start avbildningen matchar start avbildningens arkitektur.  

- Om du bara vill visa driv rutiner för start avbildningens arkitektur väljer du **Dölj driv rutiner som inte matchar start avbildningens arkitektur**. Driv Rutinens arkitektur baseras på arkitekturen som rapporteras i INF-filen från tillverkaren.  

- WinPE innehåller redan många inbyggda driv rutiner. Lägg endast till nätverks-och lagrings driv rutiner som inte ingår i WinPE.  

- Lägg endast till nätverks-och lagrings driv rutiner i Start avbildningen, såvida det inte finns krav på andra driv rutiner i WinPE.  

- Om du bara vill visa lagrings-och nätverks driv rutiner väljer du **Dölj driv rutiner som inte finns i en lagrings-eller nätverks klass (för start avbildningar)**. Det här alternativet döljer också andra driv rutiner som normalt inte behövs för start avbildningar, t. ex. video-eller modem driv rutiner.  

- Om du vill dölja driv rutiner som inte har en giltig digital signatur väljer du **Dölj driv rutiner som inte är digitalt signerade**.  

> [!NOTE]  
> Importera enhets driv rutiner till driv rutins katalogen innan du lägger till dem i en start avbildning. Information om hur du importerar enhets driv rutiner finns i [Hantera driv rutiner](manage-drivers.md).  

#### <a name="customization"></a>Anpassning

På fliken **Anpassning** väljer du någon av följande inställningar:  

- Välj alternativet för att **Aktivera för inläsnings kommandon** för att ange ett kommando som ska köras innan aktivitetssekvensen körs. När du aktiverar det här alternativet anger du också den kommando rad som ska köras och eventuella stödfiler som krävs av kommandot.  

    > [!WARNING]  
    > Lägg till `cmd /c` i början av kommando raden. Om du inte anger något `cmd /c` stängs inte kommandot när det har körts. Distributionen fortsätter att vänta tills kommandot har slutförts och inga andra konfigurerade kommandon eller åtgärder startas.  

    > [!TIP]  
    > När du skapar en aktivitetssekvens skriver guiden paket-ID och för inläsnings kommando rad till filen **CreateTSMedia. log** . Den här informationen inkluderar värdet för alla variabler i en aktivitetssekvens. Den här loggen finns på den dator som kör Configuration Manager-konsolen. Granska logg filen för att verifiera värdena för variablerna för aktivitetssekvensen.  

- Ange inställningarna för **Bakgrundsavbildning för Windows PE** för att ange om du vill använda standardbakgrunden för WinPE eller en anpassad bakgrund.  

- Konfigurera det tillfälliga **utrymmet för Windows PE (MB)**, vilket är tillfälligt lagrings utrymme (RAM-enhet) som används av WinPE. När t.ex. ett program körs inom WinPE och behöver skriva tillfälliga filer dirigerar WinPE om filerna till det tillfälliga utrymmet i minnet för att simulera närvaron av en hårddisk. Som standard är den här mängden 512 MB för enheter med mer än 1 GB RAM-minne, annars är standardvärdet 32 MB.  

- Markera **Aktivera kommandostöd (bara för test)** så att du kan öppna en kommandotolk med tangenten **F8** medan startavbildningen distribueras. Det här alternativet är användbart för fel sökning när du testar din distribution. Att använda den här inställningen i en produktions distribution rekommenderas inte på grund av säkerhets problem.  

- **Ange standard tangentbordslayout i WinPE**: <!--4910348-->Från och med version 1910 konfigurerar du standard tangentbordslayouten för en start avbildning. Om du väljer ett annat språk än en-US, kan Configuration Manager fortfarande innehålla en-us i tillgängliga språk. På enheten är den första tangentbordslayouten det valda språket, men användaren kan byta enhet till en-US om det behövs.

> [!Tip]
> Använd cmdleten [set-CMBootImage](/powershell/module/configurationmanager/set-cmbootimage?view=sccm-ps) PowerShell-cmdlet för att konfigurera inställningarna från ett skript.

#### <a name="optional-components"></a>Valfria komponenter

På fliken **valfria komponenter** anger du de komponenter som ska läggas till i Windows PE för användning med Configuration Manager. Mer information om tillgängliga valfria komponenter finns i [WinPE: Lägga till paket (referens för valfria komponenter)](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

Följande komponenter krävs av Configuration Manager och har alltid lagts till i Start avbildningar:

- Skript (WinPE-skript)
- Start (WinPE-SecureStartup)
- Nätverk (WinPE-WDS-tools)
- Skript (WinPE-WMI)

I listan **komponenter** visas ytterligare objekt som läggs till i den här start avbildningen. Om du vill lägga till fler komponenter väljer du guld asterisken. Om du vill ta bort en komponent markerar du den i listan och väljer sedan det röda krysset.

Följande komponenter används ofta av kunder:

- Microsoft .NET (WinPE-NetFX): den här komponenten är en förutsättning för PowerShell. Det är en av de större valfria komponenterna.  
- Windows PowerShell (WinPE-PowerShell): den här komponenten kräver .NET och ger begränsad PowerShell-support. Om du kör anpassade PowerShell-skript under WinPE-fasen i aktivitetssekvensen lägger du till den här komponenten. Det finns andra komponenter som kan krävas för andra PowerShell-cmdletar.
- HTML (WinPE-HTA): om du kör anpassade HTML-program under WinPE-fasen i aktivitetssekvensen lägger du till den här komponenten.

Mer information om hur du lägger till språk finns i [Konfigurera flera språk](#BKMK_BootImageLanguage).

#### <a name="data-source"></a>Datakälla

På fliken **Datakälla** uppdaterar du någon av följande inställningar:  

- Om du vill ändra start avbildningens källfil anger du **bild Sök väg** och **bild index**.  

- Om du vill skapa ett schema för när platsen uppdaterar start avbildningen väljer du **Uppdatera distributions platser enligt ett schema**.  

- Om du inte vill att innehållet i det här paketet ska åldras ut från klientcachen för att göra plats för annat innehåll, väljer du **Behåll innehåll i klientens cacheminne**.  

- Om du vill ange att platsen bara distribuerar ändrade filer när den uppdaterar start avbildnings paketet på distributions platsen väljer du **Aktivera binär differentiell replikering** (BDR). Den här inställningen minimerar nätverks trafiken mellan platser. BDR är särskilt användbart när start avbildnings paketet är stort och ändringarna är relativt små.  

- Om du använder start avbildningen i en PXE-aktiverad distribution väljer du **distribuera den här start avbildningen från den PXE-aktiverade distributions platsen**. Mer information finns i [använda PXE för att distribuera Windows via nätverket](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

#### <a name="data-access"></a>Data åtkomst

På fliken **data åtkomst** kan du konfigurera inställningar för paket delning. Om det behövs i din miljö ställer du in alternativet att **Kopiera innehållet i det här paketet till en paket resurs på distributions platser**. Sedan har du ytterligare möjlighet att **använda ett eget namn för paket resursen** och ange namnet på den anpassade **resursen**. Det krävs ytterligare disk utrymme på distributions platserna när du aktiverar det här alternativet. Den gäller för alla distributions platser som tar emot den här start avbildningen.

#### <a name="distribution-settings"></a>Distributions inställningar

På fliken **Distributionsinställningar** väljer du någon av följande inställningar:  

- I listan **distributions prioritet** anger du prioritets nivå. Configuration Manager använder den här prioritets listan när platsen distribuerar flera paket till samma distributions plats.  

- Om du vill aktivera innehålls distribution på begäran till prioriterade distributions platser väljer du **Aktivera för distribution på begäran**. När du aktiverar den här inställningen, om en klient begär innehållet för paketet och innehållet inte är tillgängligt på några distributions platser, distribuerar hanterings platsen innehållet. Mer information finns i [innehålls distribution på begäran](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

- Om du vill ange hur du vill att platsen ska distribuera start avbildningen till distributions platser som är aktiverade för förinstallerat innehåll anger du **inställningarna för förinstallerad distributions plats**. Mer information om förinstallerat innehåll finns i [Förinstallera innehåll](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

#### <a name="content-locations"></a>Innehålls platser

På fliken **innehålls platser** väljer du distributions platsen eller distributions plats gruppen och använder följande åtgärder:  

- **Verifiera**: kontrol lera start avbildnings paketets integritet på den valda distributions platsen eller distributions plats gruppen.  

- **Distribuera**om: Distribuera start avbildningen till den valda distributions platsen eller distributions plats gruppen igen.  

- **Ta bort**: ta bort start avbildningen från den valda distributions platsen eller distributions plats gruppen.  

#### <a name="security"></a>Säkerhet

På fliken **säkerhet** visar du de administrativa användare som har behörighet till objektet.

## <a name="configure-a-boot-image-for-pxe"></a><a name="BKMK_BootImagePXE"></a> Konfigurera en start avbildning för PXE  

Innan du kan använda en start avbildning för en PXE-baserad distribution konfigurerar du Start avbildningen så att den distribueras från en PXE-aktiverad distributions plats.  

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj sedan noden **Start avbildningar** .  

2. Markera den startavbildning som du vill ändra.  

3. Välj **Egenskaper**i gruppen **Egenskaper** på fliken **Start** i menyfliksområdet.  

4. Markera **Distribuera den här avbildningen från den PXE-aktiverade distributionsplatsen** på fliken **Datakälla**. Mer information finns i [använda PXE för att distribuera Windows via nätverket](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

## <a name="configure-multiple-languages"></a><a name="BKMK_BootImageLanguage"></a> Konfigurera flera språk

> [!TIP]
> Från och med version 1910 konfigurerar du standard tangentbordslayouten för egenskaperna för en start avbildning. Mer information finns i avsnittet [anpassning](#customization).<!--4910348-->

Startavbildningar är språkneutrala. Med den här funktionen kan du använda en start avbildning för att visa text för aktivitetssekvensen på flera språk i WinPE. Ta med lämpligt språk stöd på fliken Start avbildning **valfria komponenter** . Ange sedan lämplig variabel för aktivitetssekvenser för att ange vilket språk som ska visas. Språket i det distribuerade operativ systemet är oberoende av språket i WinPE. Språket som WinPE visar för användaren bestäms enligt följande:  

- När en användare kör aktivitetssekvensen från ett befintligt operativ system använder Configuration Manager automatiskt det språk som kon figurer ATS för användaren. När aktivitetssekvensen körs automatiskt som ett resultat av en obligatorisk distributions tids gräns, använder Configuration Manager språket i operativ systemet.  

- För OS-distributioner som använder PXE eller media anger du språk-ID-värdet i variabeln **SMSTSLanguageFolder** som en del av ett för inläsnings kommando. När datorn startas med WinPE visas alla meddelanden på det språk som du har angett i variabeln. Om det uppstår ett fel vid åtkomst till språk resurs filen i den angivna mappen eller om du inte anger variabeln, visar WinPE meddelanden på standard språket.  

    > [!NOTE]  
    > När du skyddar mediet med ett lösen ord visas alltid texten som efterfrågar användaren för lösen ordet i WinPE-språket.  

Använd följande procedur för att ställa in WinPE-språket för PXE-eller media-initierade OS-distributioner.  

### <a name="set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>Ange Windows PE-språk för en PXE-eller distribution av operativ system som initieras av media  

1. Innan du uppdaterar start avbildningen måste du kontrol lera att rätt resurs fil för aktivitetssekvensen (tsres.dll) finns i motsvarande språkmapp på plats servern. Till exempel finns den engelska resurs filen på följande plats: `<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. Som en del av ditt för inläsnings kommando ställer du in miljövariabeln **SMSTSLanguageFolder** till rätt språk-ID. Språk-ID: t måste anges med decimal och inte hexadecimalt format. Om du till exempel vill ange språk-ID: t till engelska anger du decimal värdet **1033**, inte det hexadecimala värdet 00000409 på mappnamnet.