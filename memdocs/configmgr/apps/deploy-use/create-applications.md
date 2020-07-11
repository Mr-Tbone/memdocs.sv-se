---
title: Skapa program
titleSuffix: Configuration Manager
description: Skapa program med distributions typer, identifierings metoder och krav för att installera program vara.
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 60ca31b73e31ea59b7a854f87262be7fdc4ab5c5
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240345"
---
# <a name="create-applications-in-configuration-manager"></a>Skapa program i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Ett Configuration Manager-program definierar metadata om programmet. Ett program har en eller flera distributions typer. Dessa distributions typer omfattar de installationsfiler och den information som krävs för att installera program vara på enheter. En distributions typ har också regler, till exempel identifierings metoder och krav. De här reglerna anger när och hur klienten ska installera program varan.  

Skapa program med följande metoder:  

- Skapa automatiskt ett program och distributions typer genom att läsa programmets installationsfiler:  
  - [Skapa ett program](#bkmk_create) och [identifiera](#bkmk_auto-app) programinformation automatiskt
  - [Skapa en distributions typ](#bkmk_create-dt) och identifiera information om distributions typ [automatiskt](#bkmk_auto-dt)

- Skapa ett program manuellt och Lägg sedan till distributions typer senare:  
  - [Skapa ett program](#bkmk_create) och [Ange](#bkmk_manual-app) programinformation manuellt
  - [Skapa en distributions typ](#bkmk_create-dt) och ange information om distributions typ [manuellt](#bkmk_manual-dt)

- [Importera ett program](#bkmk_import) från en fil  

Den här artikeln innehåller också följande information för att konfigurera en distributions typ:  

- [Innehåll](#bkmk_dt-content)
- [Aktivitetssekvens](#bkmk_dt-ts)
- [Identifierings metod](#bkmk_dt-detect)
- [Användar upplevelse](#bkmk_dt-ux)
- [Krav](#bkmk_dt-require)
- [Retur koder](#bkmk_dt-return)
- [Beroenden](#bkmk_dt-depend)

## <a name="create-an-application"></a><a name="bkmk_create"></a>Skapa ett program  

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **program hantering**och välj noden **program** .  

2. Välj **skapa program**i gruppen **skapa** på fliken **Start** i menyfliksområdet.  

Sedan identifierar eller manuellt anger du programinformationen automatiskt:  

- [Identifiera](#bkmk_auto-app) program information automatiskt för att skapa ett grundläggande program med en enda distributions typ. Till exempel en Windows Installer-fil som inte har några beroenden eller krav. När du har skapat ett program med hjälp av den här proceduren kan du redigera det efter behov. Du kan lägga till eller ändra distributions typer och lägga till identifierings metoder, beroenden eller krav.  

- [Ange](#bkmk_manual-app) programinformation manuellt om du vill skapa mer komplexa program. Definiera fler än en distributions typ, beroenden, identifierings metoder eller krav.  

### <a name="automatically-detect-application-information"></a><a name="bkmk_auto-app"></a>Identifiera programinformation automatiskt  

1. På sidan **Allmänt** i guiden Skapa program väljer du **hitta automatiskt information om det här programmet i installationsfiler**.  

2. I list rutan **typ** väljer du den programinstallations fil typ som du vill använda för att identifiera programinformation. Mer information om de tillgängliga installations typerna finns i [distributions typer som stöds av Configuration Manager](create-applications.md#bkmk_deploy-types).  

3. I rutan **plats** anger du den programinstallations fil som du vill använda för att identifiera programinformation. Den här platsen är antingen en nätverks Sök väg ( `\\server\share\filename` ) eller en Store-länk. Du måste ha åtkomst till nätverks Sök vägen och eventuella undermappar som innehåller program innehåll.  

    > [!IMPORTANT]  
    > När du väljer **Windows Installer ( \* . msi-fil)** som program typ importerar platsen alla filer i den angivna mappen. Den skickar sedan filerna till distributions platser. Kontrol lera att den angivna mappen bara innehåller de filer som krävs för att installera programmet. Microsoft testar Configuration Manager för att stödja upp till 20 000 filer i programpaketet. Om programmet har fler filer bör du överväga att skapa flera program med färre filer.  

4. På sidan **Importera information** i guiden Skapa program granskar du informationen och väljer sedan **Nästa**. Om det behövs väljer du **föregående** för att gå tillbaka och korrigera eventuella fel.  

5. På sidan **allmän information** i guiden Skapa program anger du följande information:  

    > [!NOTE]  
    > Om Configuration Manager automatiskt identifierar den här informationen från programinstallationsfiler, fylls den redan här. Dessutom kan de olika alternativ som visas vara olika beroende på vilken programtyp som du skapar.  

    - Allmän information om programmet, t. ex. program **namn**, **Administratörs kommentarer**, **utgivare**och **program version**. Om du vill ha hjälp med att hitta programmet i Configuration Manager-konsolen anger du en **valfri referens**eller väljer **administrativa kategorier**.  

    - **Installations program**: Ange installations programmet och eventuella obligatoriska egenskaper som krävs för att installera program distributions typen.  

        > [!TIP]  
        > Om installations programmet inte visas väljer du **Bläddra** och bläddrar till platsen för installations programmet.  

    - **Installations beteende**: Välj ett av de tre alternativen för hur Configuration Manager installerar den här distributions typen. Mer information om de här alternativen finns i [användar upplevelsen](#bkmk_dt-ux).  

    - **Använd en automatisk VPN-anslutning (om konfigurerad)**: om du har distribuerat en VPN-profil till enheten där användaren startar appen ansluter du VPN när appen startar. Det här alternativet är endast för Windows 8,1 och Windows Phone 8,1. Om du distribuerar fler än en VPN-profil till enheten på Windows Phone 8,1-enheter stöds inte automatiska VPN-anslutningar. Mer information finns i [VPN-profiler](../../protect/deploy-use/vpn-profiles.md).  

    - **Etablera det här programmet för alla användare på enheten**<!--1358310-->: Etablera ett program med ett Windows app-paket för alla användare på enheten. Mer information finns i [skapa Windows-program](../get-started/creating-windows-applications.md#bkmk_provision).  

       > [!Tip]  
       > Om du ändrar ett befintligt program finns den här inställningen på fliken **användar upplevelse** i egenskaperna för distributions typ för Windows-appaket.  

6. Välj **Nästa**, granska programinformationen på sidan **Sammanfattning** och slutför sedan guiden Skapa program.  

Det nya programmet visas nu i noden **program** i Configuration Manager-konsolen. Du har skapat ett program.

Om du vill lägga till fler distributions typer eller konfigurera andra inställningar, se [skapa distributions typer för programmet](#bkmk_create-dt).  

### <a name="manually-specify-application-information"></a><a name="bkmk_manual-app"></a>Ange programinformation manuellt  

1. På sidan **Allmänt** i guiden Skapa program väljer du **Ange programinformationen manuellt**och väljer sedan **Nästa**.  

2. Ange **allmän information** om programmet:  

    - Program **namnet** måste anges och måste innehålla färre än 256 tecken.  

    - **Administratörs kommentarer**, **utgivare**och **program varu version** är ytterligare metadata för att ytterligare beskriva programmet.  

    - Om du vill ha hjälp med att hitta programmet i Configuration Manager-konsolen anger du en **valfri referens**eller väljer **administrativa kategorier**.  

    - **Publicerings datum**  

    - Välj användare eller grupper som är ansvariga för det här programmet som **ägare** och **support kontakter**. Som standard anges de här värdena till ditt användar namn.  

3. På sidan **Software Center** i guiden Skapa program anger du följande information:  

    > [!Note]  
    > I version 1902 och tidigare hette den här sidan **programkatalog**.

    - **Valt språk**: i list rutan väljer du den språk version av programmet som du vill konfigurera. Välj **Lägg till/ta bort** om du vill konfigurera fler språk för det här programmet.  

    - **Lokaliserat program namn**: Ange program namnet på det valda språket.  

        > [!IMPORTANT]  
        > Det krävs ett lokaliserat program namn för varje språk version som du konfigurerar.  

    - **Användar kategorier**: Välj **Redigera** för att ange program kategorier på det valda språket. Användare av Software Center kan använda dessa kategorier för att filtrera och sortera programmen.  

        > [!Note]  
        > I version 1902 och tidigare gäller användar kategorier endast för tillgängliga distributioner till användar samlingar. Om ett program distribueras till en dator samling ignoreras användar kategorierna.
        >
        > Från och med version 1906 visas användar kategorier för enhets mål program distributioner som filter i Software Center. Dessa distributioner kan antingen vara tillgängliga eller obligatoriska.
        >
        > <!-- 4726793 -->Att byta namn på eller ta bort en kategori gäller inte automatiskt för appar med den här kategorin. Dessa ändringar gäller nästa revision av appen. Undvik det här problemet för namnbyte eller borttagning:
        >
        > - Först avmarkerar du kryss rutan för kategorin i alla appar som refererar till den. Använd sedan den ändringen, som ändrar appen.
        >     - I stället för åtgärden Byt namn, skapar du en ny kategori med det nya namnet och lägger till den nya kategorin i relevanta appar.
        >     - Du kan ta bort kategorin när du har ändrat apparna.

    - **Användar dokumentation**: Ange platsen för en fil från vilken Software Center-användare kan få mer information om det här programmet. Den här platsen är en webbplats adress eller en nätverks Sök väg och ett fil namn. Se till att användarna har åtkomst till den här platsen.  

    - **Länk text**: Ange den text som visas i stället för "Ytterligare information" när användar dokumentationen har angetts.  

    - **Sekretess-URL**: Ange en webbplats adress till sekretess policyn för programmet.  

    - **Lokaliserad Beskrivning**: Ange en beskrivning av programmet på det valda språket.  

    - **Nyckelord**: Ange en lista med nyckelord på det valda språket. Dessa nyckelord hjälper Software Center-användare att söka efter programmet.  

    - **Ikon**: Välj **Bläddra** för att välja en ikon för det här programmet. Om du inte anger någon ikon använder Configuration Manager en standard ikon. Ikoner kan ha pixel dimensioner på upp till 512x512.  

4. På sidan **distributions typer** i guiden Skapa program väljer du **Lägg till** för att skapa en ny distributions typ. Mer information finns i [skapa distributions typer för programmet](#bkmk_create-dt).  

5. Välj **Nästa**, granska programinformationen på sidan **Sammanfattning** och slutför sedan guiden Skapa program.  

Det nya programmet visas nu i noden **program** i Configuration Manager-konsolen.  

## <a name="create-deployment-types-for-the-application"></a><a name="bkmk_create-dt"></a>Skapa distributions typer för programmet  

Om du [automatiskt identifierar programinformation](#bkmk_auto-app)kanske du inte behöver slutföra några av stegen i det här avsnittet.  

> [!Note]  
> När du visar egenskaperna för en befintlig distributions typ motsvarar följande avsnitt flikar i fönstret Egenskaper för distributions typ:  
>
> - [Innehåll](#bkmk_dt-content)
> - [Aktivitetssekvens](#bkmk_dt-ts)
> - [Identifierings metod](#bkmk_dt-detect)
> - [Användar upplevelse](#bkmk_dt-ux)
> - [Krav](#bkmk_dt-require)
> - [Retur koder](#bkmk_dt-return)
> - [Beroenden](#bkmk_dt-depend)
>  
> Information om fliken **installations beteende** i egenskaperna för en distributions typ finns i [kontrol lera att körbara filer körs](deploy-applications.md#bkmk_exe-check).  

### <a name="start-the-create-deployment-type-wizard"></a>Starta guiden skapa distributions typ  

Det finns tre sätt att starta guiden skapa distributions typ:

- **I noden program**: i Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **program hantering**och väljer noden **program** . Välj ett program och välj sedan **skapa distributions typ** i menyfliksområdet.  

- **När du skapar ett program**: när du [anger programinformation manuellt](#bkmk_manual-app) i guiden Skapa program väljer du **Lägg till** på sidan distributions typer.  

- **Från program egenskaper**: Välj ett befintligt program i noden **program** och välj **Egenskaper**. Växla till fliken **distributions typer** och välj **Lägg till**.

Använd sedan någon av följande procedurer för att [automatiskt identifiera](#bkmk_auto-dt) eller [manuellt ange](#bkmk_manual-dt) distributions typs information.  

### <a name="automatically-identify-deployment-type-information"></a><a name="bkmk_auto-dt"></a>Identifiera information om distributions typ automatiskt  

1. På sidan **Allmänt** i guiden skapa distributions typ:  

    1. Välj programmets installations fil **typ** för att identifiera distributions typs informationen.  

    2. Välj **identifiera information om den här distributions typen automatiskt från installationsfiler**.  

    3. I rutan **plats** anger du den programinstallations fil som du vill använda för att identifiera distributions typs informationen. Den här platsen är antingen en nätverks Sök väg ( `\\server\share\filename` ) eller en Store-länk. Du måste ha åtkomst till nätverks Sök vägen och eventuella undermappar som innehåller program innehåll.  

2. På sidan **Importera information** i guiden skapa distributions typ granskar du informationen och väljer sedan **Nästa**. Om det behövs väljer du **föregående** för att gå tillbaka och korrigera eventuella fel.  

3. På sidan **allmän information** i guiden skapa distributions typ anger du följande information:  

    > [!NOTE]  
    > En del av distributionstypsinformationen kan redan ha fyllts i om den har lästs från programinstallationsfilerna. Dessutom kan de alternativ som visas vara olika beroende på vilken distributions typ som du skapar.  

    - **Allmän information** om distributions typen:  
        - **Namnet** måste anges  

        - **Administratörs kommentarer** för att ytterligare beskriva det  

        - **Språk** som är tillgängliga för IT  

    - **Installations program**: Ange installations programmet och eventuella egenskaper som krävs för att installera distributions typen.  

    - **Installations beteende**: Välj ett av de tre alternativen för hur Configuration Manager installerar den här distributions typen. Mer information om de här alternativen finns i [användar upplevelsen](#bkmk_dt-ux).  

    - **Använd en automatisk VPN-anslutning (om konfigurerad)**: om du har distribuerat en VPN-profil till enheten där användaren startar appen ansluter du VPN när appen startar. Det här alternativet är endast för Windows 8,1 och Windows Phone 8,1. Om du distribuerar fler än en VPN-profil till enheten på Windows Phone 8,1-enheter stöds inte automatiska VPN-anslutningar. Mer information finns i [VPN-profiler](../../protect/deploy-use/vpn-profiles.md).  

4. Välj **Nästa**och fortsätt sedan till [alternativ för distributions typ innehåll](#bkmk_dt-content).  

### <a name="manually-specify-the-deployment-type-information"></a><a name="bkmk_manual-dt"></a>Ange distributions typs informationen manuellt  

1. På sidan **Allmänt** i guiden skapa distributions typ väljer du programmets installations fil typ för den här distributions typen i list rutan **typ** .

2. Välj **Ange distributions typs informationen manuellt**och välj sedan **Nästa**.

3. På sidan **allmän information** i guiden skapa distributions typ anger du ett **namn** för distributions typen. Alternativt kan du ange **Administratörs kommentarer**, välja **språk** för den här distributions typen och sedan välja **Nästa**.  

4. Fortsätt till [alternativ för distributions typ innehåll](#bkmk_dt-content).  

### <a name="deployment-type-content-options"></a><a name="bkmk_dt-content"></a>Alternativ för distributions typ **innehåll**  

Ange följande information på sidan **innehåll** :  

> [!Note]  
> När du visar egenskaperna för en befintlig distributions typ visas vissa av dessa alternativ på fliken **innehåll** och några på fliken **program** .  

- **Innehålls plats**: Ange platsen för innehållet för den här distributions typen eller Välj **Bläddra** för att välja mappen för distributions typen innehåll.  

    > [!IMPORTANT]  
    > System kontot på plats serverdatorn måste ha behörighet till den angivna innehålls platsen.  

  - **Behåll innehåll i klientens cacheminne**: Configuration Manager-klienten är i sin oändlighet i cacheminnet för distributions typs innehållet. Klienten behåller innehållet även om appen redan är installerad. Det här alternativet är användbart med vissa distributioner, t. ex. Windows Installer – baserad program vara. Windows Installer behöver en lokal kopia av käll innehållet för att tillämpa uppdateringar. Det här alternativet minskar det tillgängliga cache-utrymmet. Om du väljer det här alternativet kan det leda till att en stor distribution Miss fungerar vid ett senare tillfälle om cacheminnet inte har tillräckligt med utrymme.  

- **Installations program**: Ange namnet på installations programmet och eventuella obligatoriska installations parametrar.  

  - **Installationen startar i: om**du vill kan du ange den mapp som har installations programmet för distributions typen. Den här mappen kan vara en absolut sökväg på klienten eller en sökväg till den distributions plats mapp som har installationsfilerna.  

- **Avinstallera program**: Alternativt kan du ange namnet på avinstallations programmet och eventuella obligatoriska parametrar.  

  - **Avinstallera startar i: om**du vill kan du ange den mapp som har avinstallations programmet för distributions typen. Den här mappen kan vara en absolut sökväg på klienten. Det kan också vara en relativ sökväg på en distributions plats i mappen med paketet.  

- **Reparera program**: för Windows Installer-och skript installations distributions typer kan du, om du vill, ange namnet på reparations programmet och eventuella obligatoriska parametrar.<!--1357866-->  

  - **Reparera startar i: om**du vill kan du ange den mapp som har reparations programmet för distributions typen. Den här mappen kan vara en absolut sökväg på klienten. Det kan också vara en relativ sökväg på en distributions plats i mappen med paketet.  

- **Kör installations-och avinstallations program som 32-bitars process på 64-bitars klienter**: Använd 32-bitars filen och register platser på Windows-baserade datorer för att köra installations programmet för distributions typen.  

#### <a name="deployment-type-properties-content-options"></a>**Innehålls** alternativ för distributions typs egenskaper

När du visar egenskaperna för en distributions typ visas följande alternativ endast på fliken **innehåll** :

- **Avinstallera innehålls inställningar**:  

  - **Samma som installations innehåll**: om installera och avinstallera innehållet är detsamma väljer du det här alternativet. Det här alternativet är standardinställningen.  

  - **Inget avinstallations innehåll**: om programmet inte behöver innehåll för avinstallation väljer du det här alternativet.  

  - **Annorlunda än installera innehåll**: om avinstallations innehållet skiljer sig från installations innehållet väljer du det här alternativet.  

    - **Avinstallera innehålls plats**: ange nätverks Sök vägen till det innehåll som används för att avinstallera programmet.  

- **Tillåt att klienter använder distributions platser från standard plats begränsnings gruppen**: Ange om klienter ska ladda ned och installera program varan från en distributions plats i standard plats begränsnings gruppen när innehållet inte är tillgängligt från en distributions plats i den aktuella eller intilliggande begränsnings grupper.  

- **Distributions alternativ**: Ange om klienter ska hämta programmet när de använder en distributions plats från en granne eller standard platsens gränser grupper.  

- **Tillåt att klienter delar innehåll med andra klienter i samma undernät**: Ange om användning av BranchCache ska aktiveras för nedladdning av innehåll. Mer information finns i [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). BranchCache är alltid aktiverat på klienter. Den här inställningen har tagits bort i version 1802, eftersom-klienter använder BranchCache om distributions platsen stöder det.  

### <a name="deployment-type-task-sequence-options"></a><a name="bkmk_dt-ts"></a>**Alternativ för aktivitetssekvens för** distributions typen

<!--3555953-->

Mer information om distributions typen för aktivitetssekvensen från och med version 2002 finns i [distributions typ för aktivitetssekvens](../get-started/creating-windows-applications.md#bkmk_tsdt).

Ange följande information på sidan **aktivitetssekvens** :

- **Installera aktivitetssekvens**: Välj en aktivitetssekvens som kör installations processen för den här appen.

- **Avinstallera aktivitetssekvens** (valfritt): Välj en aktivitetssekvens som tar bort den här appen.

> [!TIP]  
> Om aktivitetssekvensen inte visas i listan, kontrollerar du att den inte innehåller några OS-distributioner eller steg för uppgradering av operativ system. Bekräfta också att den inte har marker ATS som en högpåverkad aktivitetssekvens. Mer information hittar du i kraven för [distributions typen för aktivitetssekvensen](../get-started/creating-windows-applications.md#bkmk_tsdt).

### <a name="deployment-type-detection-method-options"></a><a name="bkmk_dt-detect"></a>Alternativ för **identifierings metod** för distributions typ

Den här proceduren ställer in en identifierings metod som anger förekomst av distributions typen. Med andra ord, om Windows-enheten redan har programmet installerat. Använd någon av följande metoder för att skapa en identifierings metod:

- [Konfigurera regler för att identifiera förekomst av den här distributions typen](#bkmk_detect-rule)
- [Använd ett anpassat skript för att identifiera förekomst av den här distributions typen](#bkmk_detect-script)

#### <a name="configure-rules-to-detect-the-presence-of-this-deployment-type"></a><a name="bkmk_detect-rule"></a>Konfigurera regler för att identifiera förekomst av den här distributions typen

1. På sidan **identifierings metod** är alternativet för att **Konfigurera regler för att identifiera förekomst av den här distributions typen** markerad som standard. Välj **Lägg till sats**.  

2. I dialog rutan **identifierings regel** väljer du en **inställnings typ** för att identifiera förekomsten av distributions typen:  

    - **Fil system**: identifiera om en angiven fil eller mapp finns på en enhet. Den här identifieringen anger att programmet är installerat. Ange följande ytterligare information:  

        - **Typ**: Välj om det är en fil eller mapp.  

        - **Sökväg** (krävs): Ange eller bläddra till den lokala sökvägen på enheten som innehåller filen eller mappen. Ett exempel är `C:\Program Files`. Du kan inte ange en delad nätverks Sök väg. Om du väljer **Bläddra**bläddrar du till det lokala fil systemet eller ansluter till en representativ klient för att bläddra.  

        - **Fil-eller mappnamn** (obligatoriskt): Ange den angivna fil-eller mappnamnet som ska identifieras i ovanstående sökväg. Om klienten identifierar den här filen eller mappen på enheten, anses programmet vara installerat på enheten.  

        - **Den här filen eller mappen är associerad med ett 32-bitars program på 64-bitars system**: klienten kontrollerar först 32-bitars fil platser för den angivna filen eller mappen. Om filen eller mappen inte hittas söker klienten på 64-bitars platser.  

    - **Register**: identifiera om en angiven register nyckel eller register värde finns på en klienten het. Den här identifieringen anger att programmet är installerat. Ange följande ytterligare information:  

        - **Hive** (krävs): Välj en registrerings data fil i list rutan. Ett exempel är `HKEY_LOCAL_MACHINE`.  

        - **Nyckel** (obligatoriskt): Ange den register nyckel som ska sökas i stacken ovan. Ett exempel är `SOFTWARE\Microsoft\Office`.  

        - **Värde** (valfritt): Ange ett angivet värde som ska identifieras i ovanstående nyckel. Om du vill att klienten ska identifiera värdet (standard) aktiverar du alternativet för att **använda register nyckel värde (standard) för identifiering**. När du anger ett värde eller aktiverar det här alternativet måste du välja en **datatyp**.  

        - **Den här register nyckeln är associerad med ett 32-bitars program på 64-bitars system**: Välj det här alternativet för att först kontrol lera 32-bitars register platser för den angivna register nyckeln. Om register nyckeln inte hittas söker klienten på 64-bitars platser.  

    - **Windows Installer**: identifiera om en angiven Windows Installer fil finns på en klienten het. Den här identifieringen anger att programmet är installerat. Ange **produkt koden** för MSI som ska identifieras på klienten. Om du väljer **Bläddra**väljer du den MSI-fil som produkt koden ska läsas från.

3. Längst ned i fönstret identifierings regel anger du om objektet måste finnas eller uppfyller en regel. Om du till exempel identifierar med en fil är följande alternativ markerat som standard: **fil system inställningen måste finnas i mål systemet för att indikera förekomst av det här programmet**. Välj det andra alternativet för att skapa en regel för identifiering baserat på fil-eller mappegenskaper. Dessa egenskaper inkluderar ändrings datum, skapad, version eller storlek. Dessa regel villkor är olika för varje inställnings typ.  

4. Välj **OK** för att stänga dialog rutan **identifierings regel** .  

När du skapar fler än en identifierings metod för en distributions typ kan du gruppera satser tillsammans för att skapa mer komplex logik.  

#### <a name="group-detection-clauses-optional"></a>Grupp identifierings satser *(valfritt)*

1. Skapa tre eller fler identifierings metods satser i en distributions typ.  

2. Markera två eller flera efterföljande satser och välj sedan **grupp**. Du ser de parenteser som läggs till i de associerade kolumnerna, vilket visar var gruppen börjar och slutar.  

    Exempel:

    | Anslutningsprogram  |  ( | Sats           |  )  |
    |------------|----|------------------|-----|
    |            |    | MSI produkt kod |     |
    | Eller         | (  | fil1. text finns|     |
    | Och        |    | file2.txt finns | )   |

3. Om du vill ta bort gruppen väljer du de grupperade satserna och väljer sedan **dela upp grupp**.  

*Fortsätt* till nästa avsnitt om hur du använder ett anpassat skript som en identifierings metod. Eller *gå vidare* till alternativen för [användar upplevelse](#bkmk_dt-ux) för distributions typen.

#### <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a><a name="bkmk_detect-script"></a>Använd ett anpassat skript för att söka efter en distributions typ  

1. På sidan **identifierings metod** markerar du kryss rutan **Använd ett anpassat skript för att identifiera förekomst av den här distributions typen** . Välj sedan **Redigera**.  

2. I dialog rutan **skript redigeraren** väljer du en **skript typ** för att identifiera distributions typen: PowerShell, VBScript eller JScript.  

    > [!Note]  
    > När ett Windows PowerShell-skript körs som en identifierings metod för appen anropar Configuration Manager klienten PowerShell med `-NoProfile` parametern. Det här alternativet startar PowerShell utan profiler. En PowerShell-profil är ett skript som körs när PowerShell startar. <!--3607762-->  

3. I rutan **skript innehåll** anger du det skript som du vill använda eller klistrar in innehållet i ett befintligt skript. Välj **Öppna** för att bläddra till ett befintligt sparat skript. Välj **Rensa** för att ta bort texten i fältet skript innehåll. Om det behövs kan du aktivera alternativet att **köra skript som 32-bitars process på 64-bitars klienter**.  

    > [!NOTE]  
    > Den maximala storleken för ett skript är 32 KB.  

4. Välj **OK** för att spara skriptet och stänga dialog rutan **skript redigeraren** . I guiden skapa distributions typ, uppdateras **skript typen** och **skript längds** fälten med information om ditt skript.

#### <a name="about-custom-script-detection-methods"></a>Om anpassade skript identifierings metoder  

Configuration Manager kontrollerar resultatet från skriptet. och läser de värden som skrivits av skriptet till standardutdataströmmen (STDOUT), standardfelströmmen (STDERR) och slutkoden. Om skriptet avslutas med ett värde som inte är noll, Miss lyckas skriptet och status för program identifieringen är *Okänt*. Om slut koden är noll och STDOUT innehåller data *installeras*status för program identifiering.

> [!TIP]
> Om du skriver ett identifierings skript och returnerar slut koden noll men inte returnerar utdata (data i STDOUT), identifieras inte programmet som installerat. Mer information finns i följande exempel.

Använd följande tabeller för att kontrol lera om ett program har installerats från utdata från ett skript:  

##### <a name="zero-exit-code"></a>Avslutnings kod noll

|STDOUT|STDERR|Skript resultat|Tillstånd för program identifiering|
|---------|---------|---------|---------|
|Tom|Tom|Klart|Inte installerad|
|Tom|Inte tom|Fel|Okänt|
|Inte tom|Tom|Klart|Installerad|
|Inte tom|Inte tom|Klart|Installerad|

##### <a name="non-zero-exit-code"></a>Slutkod som inte är noll

|STDOUT|STDERR|Skript resultat|Tillstånd för program identifiering|
|---------|---------|---------|---------|
|Tom|Tom|Fel|Okänt|
|Tom|Inte tom|Fel|Okänt|
|Inte tom|Tom|Fel|Okänt|
|Inte tom|Inte tom|Fel|Okänt|

##### <a name="examples"></a>Exempel

Använd följande PowerShell/VBScript-exempel för att skriva egna skript för program identifiering:  

**Exempel 1**: skriptet returnerar slut koden som inte är noll. Den här koden anger att skriptet inte kunde köras korrekt. I det här fallet är programidentifieringstillståndet okänt.  

``` PowerShell
Exit 1
```

``` VBScript
WScript.Quit(1)
```

**Exempel 2**: skriptet returnerar slut koden noll, men värdet för stderr är inte tomt. Det här resultatet indikerar att skriptet inte kunde köras korrekt. I det här fallet är programidentifieringstillståndet okänt.  

``` PowerShell
Write-Error "Script failed"
Exit 0
```

``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

**Exempel 3**: skriptet returnerar slut koden noll, vilket tyder på att det lyckades. Värdet för STDOUT är dock tomt, vilket anger att programmet inte är installerat.  

``` PowerShell
Exit 0
```

``` VBScript
WScript.Quit(0)
```

**Exempel 4**: skriptet returnerar slut koden noll, vilket tyder på att det lyckades. Värdet för STDOUT är inte tomt, vilket anger att programmet är installerat.  

``` PowerShell
Write-Host "The application is installed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

**Exempel 5**: skriptet returnerar slut koden noll, vilket tyder på att det lyckades. Värdena för STDOUT och STDERR är inte tomma, vilket indikerar att programmet är installerat.  

``` PowerShell
Write-Host "The application is installed"
Write-Error "Completed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```

### <a name="deployment-type-user-experience-options"></a><a name="bkmk_dt-ux"></a>Alternativ för distributions typ för **användar upplevelse**

De här inställningarna anger hur klienten ska installera programmet på enheter och vad användaren ser.  

Ange följande information på sidan **Användarupplevelse** :  

- **Installations beteende**: Välj något av följande alternativ i list rutan:  

  - **Installera för användare**: klienten installerar bara programmet för den användare som du distribuerar programmet till.  

  - **Installera för system**: klienten installerar bara programmet en gång. Den är tillgänglig för alla användare.  

  - **Installera för system om resursen är en enhet. annars installerar du för användare**: om du distribuerar programmet till en enhet installeras det för alla användare. Om du distribuerar programmet till en användare installeras det bara av klienten för den användaren.  

- **Inloggnings krav**: Välj något av följande alternativ:  

  - **Endast när en användare är inloggad**  

  - **Huruvida en användare är inloggad eller inte**  

  - **Endast när ingen användare är inloggad**  

    > [!NOTE]  
    > Det här alternativet används **endast när en användare är inloggad**. Om du väljer **Installera för användare** i list rutan **installations beteende** kan du inte ändra det här alternativet.  

- **Installations programmets synlighet**: Ange i vilket läge distributions typen ska köras på klient enheter. Välj något av följande alternativ:  

  - **Maximerat**: distributions typen körs maximerat på klient enheter. Användare ser all installations aktivitet.  

  - **Normal**: distributions typen körs i normal läge baserat på standardinställningar för system och program. Det här är standardläget.  

  - **Minimerat**: distributions typen körs minimerat på klient enheter. Användare kan se installations aktiviteten i meddelande fältet eller aktivitets fältet.  

  - **Dolt**: distributions typen körs dolt på klient enheter. Användarna ser ingen installations aktivitet.  

- **Tillåt att användare visar och interagerar med programinstallationen**: Ange om en användare kan interagera med distributions typen installation för att konfigurera installations alternativ.  

    Om du har valt alternativet **Installera för användare** i list rutan **installations beteende** är det här alternativet aktiverat som standard.  

    > [!IMPORTANT]  
    > Den här inställningen är valfri när du väljer funktionen **Installera för system** . Den här ändringen är främst till för att låta en användare interagera med installationen under en aktivitetssekvens. Om du till exempel vill köra en installations process som efterfrågar slutanvändaren för olika alternativ. Vissa program installations program kan inte ha användar meddelanden som är i tysthet, eller så kanske installations processen kräver specifika konfigurations värden som bara är kända för användaren. <!--1356976-->  
    >  
    > Att installera i system kontext och tillåta att användare interagerar med installationen är inte en säker konfiguration. Mer information finns i [säkerhet och sekretess för program hantering](../plan-design/security-and-privacy-for-application-management.md#bkmk_interact).  

- **Högsta tillåtna körnings tid (minuter)**: Ange den maximala tid i minuter som du förväntar dig att distributions typen ska köras på klient datorn. Ange den här inställningen som ett heltal som är större än noll. Standardvärdet är 120 minuter (två timmar).  

    Använd det här värdet för följande åtgärder:  

  - För att övervaka resultaten från distributions typen.  

  - För att kontrol lera om en distributions typ installeras när du definierar underhålls perioder på klient enheter. När en underhålls period är på plats, startar en distributions typ endast om det finns tillräckligt med tid i underhålls fönstret för att hantera den **maximalt tillåtna körnings tids** inställningen.  

    > [!IMPORTANT]  
    > En konflikt kan uppstå om den **längsta tillåtna körnings tiden** är längre än det schemalagda underhålls fönstret. Om användaren anger den maximala körnings tiden till en period som är större än längden på ett tillgängligt underhålls fönster körs inte den distributions typen.  

- **Beräknad installations tid (minuter)**: Ange den beräknade installations tiden för distributions typen. Användarna ser den här tiden i Software Center.  

#### <a name="deployment-type-properties-user-experience-options"></a>Egenskaper för distributions typ **användar upplevelse**

När du visar egenskaperna för en distributions typ visas följande alternativ endast på fliken **användar upplevelse** :

Genomdriva en speciell funktion efter installationen. Välj något av följande alternativ:  

- **Bestäm beteende baserat på RETUR koder**: hantera omstarter baserat på de koder som kon figurer ATS på fliken [RETUR koder](#bkmk_dt-return) . **det kan krävas en omstart**av Software Center. Om en användare är inloggad under installationen uppmanas de, beroende på *distributionens* konfiguration av användar upplevelsen.  

- **Ingen angiven åtgärd**: ingen omstart krävs efter installationen. Software Center-rapporter som inte behöver startas om.  

- **Installations programmet för program vara kan tvinga fram en omstart av enheten**: Configuration Manager inte styr eller initierar en omstart, men den faktiska installationen kan göra det utan varning. Använd den här inställningen för att förhindra Configuration Manager från att rapportera installations problem när installations programmet startar en omstart. **Det kan krävas en omstart**av Software Center-visning.  

- **Configuration Manager klienten tvingar fram en obligatorisk omstart av enheten**: Configuration Manager tvingar fram en omstart av enheten när installationen har slutförts. Software Center-rapporter som en omstart krävs. Om en användare är inloggad under installationen uppmanas de, beroende på *distributionens* konfiguration av användar upplevelsen.  

### <a name="deployment-type-requirements"></a><a name="bkmk_dt-require"></a>**Krav** för distributions typ

Configuration Manager verifierar dessa krav på enheter innan du installerar distributions typen. Använd krav för att ytterligare förfina och kontrol lera de enheter eller användare som tar emot programmet. Om du till exempel distribuerar programmet till en användar samling anger du appens maskin varu krav här.

1. På sidan **krav** väljer du **Lägg till** för att öppna dialog rutan **Skapa krav** .  

2. I list rutan **kategori** väljer du om det här kravet gäller för en **enhet** eller en **användare**.  

    Välj **anpassad** om du vill använda ett tidigare skapat globalt villkor. När du väljer **anpassad**kan du också välja **skapa** för att skapa ett nytt globalt villkor. Mer information om globala villkor finns i [så här skapar du globala villkor](create-global-conditions.md).  

    > [!IMPORTANT]  
    > Om du distribuerar programmet till en enhets samling, ignorerar klienten eventuella krav för kategorin **användare** och den primära villkors **enheten**.  

3. I list rutan **villkor** väljer du villkoret för att utvärdera om användaren eller enheten uppfyller installations kraven. Innehållet i listan varierar beroende på vilken kategori som valts.  

4. I list rutan **operator** väljer du den operator som ska användas. Den här operatorn jämför det valda villkoret med det angivna värdet. Den bedömer om användaren eller enheten uppfyller installations kravet. Tillgängliga operatörer varierar beroende på vilket villkor som valts. När du använder `One Of` operatorn, är fältet värden verifierat att du måste ange en post per rad.

    > [!Note]  
    > De tillgängliga kraven varierar beroende på vilken enhets typ som används av distributions typen.  

5. I rutan **värde** anger du de värden som ska användas för jämförelse. Dessa värden, tillsammans med det valda villkoret och den valda operatorn, utvärderar om användaren eller enheten uppfyller installations kraven. Tillgängliga värden varierar beroende på det valda villkoret och den valda operatorn.  

6. Välj **OK** för att spara kravet och stänga dialog rutan **Skapa krav** .  

### <a name="deployment-type-dependencies"></a><a name="bkmk_dt-depend"></a>Distributions typ **beroenden**  

Beroenden definierar en eller flera distributions typer från ett annat program som klienten måste installera innan den här distributions typen installeras.

> [!IMPORTANT]  
> I vissa fall är en distributions typ beroende av en distributions typ som också har beroenden. Det högsta antalet beroenden i kedjan som stöds är fem.  

1. På sidan **beroenden** väljer du **Lägg till**.  

2. Ange **namnet på beroende gruppen**i fönstret Lägg till beroende. Det här namnet avser den här gruppen av program beroenden.  

3. I fönstret Lägg till beroende väljer du **Lägg till**.  

4. I fönstret **Ange obligatoriskt program** väljer du ett tillgängligt program och minst en av de distributions typer som ska användas som ett beroende.  

    > [!TIP]  
    > Välj **Visa** för att visa egenskaperna för det valda programmet eller distributions typen.  

5. Välj **OK** för att stänga fönstret **Ange obligatoriskt program** .  

6. Om du vill att klienten automatiskt ska installera det beroende programmet väljer du **Automatisk installation** bredvid beroende.  

    > [!NOTE]  
    > Du behöver inte distribuera ett beroende program för att klienten ska kunna installera den automatiskt.  

7. Om du lägger till fler än ett beroende använder du knapparna **öka prioritet** och **minska prioritet** . De här åtgärderna ändrar ordningen i vilken klienten utvärderar varje beroende.  

8. Välj **OK** för att stänga fönstret **Lägg till beroende** .  

### <a name="deployment-type-return-codes"></a><a name="bkmk_dt-return"></a>**RETUR koder** för distributions typ

> [!Note]  
> Den här sidan finns inte i guiden skapa distributions typ. Det är bara en flik i egenskaperna för en befintlig distributions typ.  

Ange retur koder för att styra beteenden när distributions typen har slutförts. Till exempel, en signal om att en omstart krävs, är installationen slutförd.

1. På fliken **RETUR koder** i fönstret Egenskaper för distributions typ väljer du **Lägg till**.  

2. I fönstret Lägg till returkod anger du det **RETUR kods värde** som du förväntar dig från den här distributions typen. Det här värdet är ett positivt eller negativt heltal mellan `-2147483648` och `2147483647` .  

3. Välj en **kodtyp** i list rutan. Den här inställningen definierar hur Configuration Manager tolkar den angivna retur koden från den här distributions typen. De tillgängliga typerna varierar beroende på teknik för distributions typ.  

    - **Lyckades (ingen omstart)**: distributions typen har installerats och ingen omstart krävs.  

    - **Fel (ingen omstart)**: det gick inte att installera distributions typen.  

    - **Hård omstart**: distributions typen har installerats, men kräver att enheten startas om. Inget annat kan installeras förrän enheten har startats om.  

    - **Mjuk omstart**: distributions typen har installerats, men begär att enheten ska starta om. Andra installationer kan uppstå innan enheten startas om.  

    - **Snabb återförsök**: en annan installation pågår redan på enheten. Klienten försöker igen varannan timme, totalt 10 gånger.  

4. Du kan också ange ett **namn** och en **Beskrivning** för den här retur koden.

5. Välj **OK** för att stänga fönstret Lägg till returkod.  

#### <a name="example-non-zero-success"></a>Exempel: ej noll klart

Du distribuerar ett program som returnerar avslutnings koden `1` när den har installerats. Som standard identifierar Configuration Manager den här retur koden som inte är noll som ett haveri. Ange retur kods värdet för `1` och välj kodtypen **lyckad (ingen omstart)**. Nu Configuration Manager tolkar att RETUR koden är lyckad för den här distributions typen.

#### <a name="default-return-codes"></a>Standard retur koder

När du skapar vissa distributions typer lägger Configuration Manager automatiskt till följande retur koder som är gemensamma för den tekniken:  

##### <a name="windows-installer-msi-file"></a>Windows Installer ( \* . msi-fil)

|Värde    |Kodtyp|
|---------|---------|
|0        |Lyckades (ingen omstart)|
|1707     |Lyckades (ingen omstart)|
|3010     |Mjuk omstart|
|1641     |Hård omstart|
|1618     |Snabb återförsök|

##### <a name="script-installer"></a>Skriptinstallationsprogram

|Värde    |Kodtyp|
|---------|---------|
|0        |Lyckades (ingen omstart)|
|1641     |Hård omstart|
|3010     |Mjuk omstart|
|1618     |Snabb återförsök|

##### <a name="windows-app-package-appx-appxbundle-msix-msixbundle"></a>Windows-appaket ( \* . appx, \* . appxbundle, \* . msix, \* . msixbundle)

|Värde    |Kodtyp|
|---------|---------|
|15605    |Snabb återförsök|
|15618    |Snabb återförsök|

## <a name="additional-options-for-app-v-deployment-types"></a><a name="bkmk_appv"></a>Ytterligare alternativ för App-V-distributions typer  

Konfigurera ytterligare alternativ som är unika för distributions typer för virtuella program (App-V).  

### <a name="app-v-deployment-type-content-options"></a><a name="bkmk_appv-content"></a>**Innehålls** alternativ för App-V-distributions typ  

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **program hantering**och välj noden **program** .  

2. Välj ett program med en App-V-distributions typ och välj **Egenskaper**.  

3. I program egenskaperna, byter du till fliken **distributions typer** . Välj App-V-distributions typ och välj **Redigera**.  

4. I egenskaper för distributions typ växlar du till fliken **innehåll** . Konfigurera följande alternativ efter behov:  

    - **Behåll innehåll i klientens cacheminne**: den Configuration Manager klienten tar inte bort från cacheminnet för innehållet för den här distributions typen.  

    - **Läs in innehåll till app-v-cache före start**: innan programmet startar läses Configuration Manager klienten in i app-v-cache allt innehåll för den här distributions typen. Klienten fäster inte innehållet i cacheminnet. Det tar bort innehållet vid behov.  

5. Välj **OK** för att stänga egenskaperna för distributions typen. Välj **OK** för att stänga program egenskaperna.  

### <a name="app-v-deployment-type-publishing-options"></a><a name="bkmk_appv-pub"></a>**Publicerings** alternativ för App-V-distributions typ

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **program hantering**och välj noden **program** .  

2. Välj ett program med en App-V-distributions typ och välj **Egenskaper**.  

3. I program egenskaperna, byter du till fliken **distributions typer** . Välj App-V-distributions typ och välj **Redigera**.  

4. I egenskaper för distributions typ växlar du till fliken **publicering** . Välj de objekt i det virtuella programmet som du vill publicera.  

5. Välj **OK** för att stänga egenskaperna för distributions typen. Välj **OK** för att stänga program egenskaperna.  

## <a name="import-an-application"></a><a name="bkmk_import"></a>Importera ett program  

Använd följande procedur för att importera ett program till Configuration Manager:

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **program hantering**och välj noden **program** .  

2. I menyfliksområdet på fliken **Start** och gruppen **skapa** väljer du **importera program**.  

3. På sidan **Allmänt** i guiden Importera program anger du nätverks Sök vägen till **filen** som ska importeras. Ett exempel är `\\server\share\file.zip`. Den här filen är ett giltigt komprimerat arkiv (ZIP-format) för ett exporterat Configuration Manager-program.  

4. På sidan **fil innehåll** väljer du den åtgärd som ska vidtas om programmet är en dubblett av ett befintligt program. Skapa ett nytt program eller ignorera dubbletten och Lägg till en ny revision i det befintliga programmet.  

5. Granska åtgärderna på sidan **Sammanfattning** och slutför sedan guiden.  

Det nya programmet visas i noden **Program**.  

> [!TIP]  
> Windows PowerShell-cmdleten **import-CMApplication** har samma funktion som den här proceduren. Mer information finns i [import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  

Mer information om hur du exporterar ett program finns i [hanterings aktiviteter för program](management-tasks-applications.md).

## <a name="supported-deployment-types"></a><a name="bkmk_deploy-types"></a>Distributions typer som stöds  

Configuration Manager stöder följande distributions typer för program:

| Namn på distributionstyp | Beskrivning |
|--------------------------|----------------------|  
| **Windows Installer ( \* . msi-fil)** | En Windows Installer-fil. |  
| **Windows-appaket ( \* . appx, \* . appxbundle, \* . msix, \* . msixbundle)** | En Windows-appaket (. appx), ett paket för Windows-programpaket (. appxbundle), ett Windows 10-appaket (. msix) eller Windows 10-appaket (. msixbundle).<!--1357427--> |  
| **Windows-appaket (i Windows Store)** | Ange en länk till appen i Windows Store eller bläddra i butiken för att välja appen.<sup>[Anmärkning 1](#bkmk_note1)</sup> |  
| **Skriptinstallationsprogram** | Ange ett skript eller program som körs på Windows-klienter för att installera innehåll eller för att utföra en åtgärd. Använd den här distributions typen för setup.exe installations program eller skript omslutningar. |  
| **Microsoft Application Virtualization 4** | Ett Microsoft App-V v4-manifest. |  
| **Microsoft Application Virtualization 5** | En paket fil för Microsoft App-V v5. |  
| **Windows Phone app-paket ( \* . xap-fil)** | En paket fil för Windows Phone. |  
| **Windows Phone-appaket (i Windows Phone Store)** | Ange en länk till appen i Windows Store. |  
| **Mac OS X** | För macOS-datorer som kör Configuration Manager-klienten. Skapa en. cmmac-fil med **CMAppUtil** -verktyget. |  
| **Webb program** | Ange en länk till ett webb program. Den här distributions typen installerar en genväg till webb programmet på användarens enhet. |  
| **Windows Installer via MDM ( \* . msi)** | Skapa och distribuera Windows Installer-baserade appar till Windows 10-enheter. Mer information finns i [distribuera Windows Installer appar till MDM-registrerade Windows 10-enheter](../get-started/creating-windows-applications.md#bkmk_mdm-msi). |
| **Aktivitetssekvens** | Från och med version 2002 installerar eller avinstallerar du komplexa program med hjälp av aktivitetssekvenser. Mer information finns i [distributions typ för aktivitetssekvens](../get-started/creating-windows-applications.md#bkmk_tsdt). <!--3555953--> |

> [!NOTE]
> Configuration Manager-konsolen kan visa andra distributions typer, men de är för plattformar som inte längre stöds. Mer information finns i [vad hände med hybrid?](../../mdm/understand/what-happened-to-hybrid.md).

### <a name="note-1-windows-app-package-in-the-windows-store"></a><a name="bkmk_note1"></a>Anmärkning 1: Windows-appaket (i Windows Store)

Om du vill distribuera appen som en länk till Windows Store konfigurerar du grup principen **inaktivera Store-programmet**. Ange att den här principen är **inaktive rad** eller **inte konfigurerad**. Om du aktiverar den här inställningen kan klienterna inte ansluta till Windows Store för att hämta och installera program.

Windows-klienter utvärderar alltid distributions typer som använder en länk till en butik före andra distributions typer. Klienten utvärderar sedan distributions typer efter prioritet.

> [!TIP]
> Vissa lager länkar kan orsaka följande fel i guiden Skapa program: "Ogiltig program länk". Vissa butiks *aktuella appar* kan exempelvis orsaka det här felet. Du kan fortfarande välja **Nästa** på sidan **Allmänt** i guiden. Configuration Manager skapar appen och du kan distribuera den.<!-- SCCMDocs-pr #4716 -->

## <a name="next-steps"></a>Nästa steg

När du har skapat ett program i Configuration Manager är nästa steg att [distribuera programmet](deploy-applications.md).

Från och med version 1906 skapar du en grupp av program som du kan skicka till en användar-eller enhets samling som en enskild distribution. Mer information finns i [skapa program grupper](create-app-groups.md).

Mer information om hur du skapar program på olika OS-plattformar finns i följande artiklar:  

- [Skapa Windows-program](../get-started/creating-windows-applications.md)
- [Skapa Mac-program](../get-started/creating-mac-computer-applications.md)
- [Skapa serverprogram för Linux och UNIX](../get-started/creating-linux-and-unix-server-applications.md)
- [Skapa Windows Embedded-program](../get-started/creating-windows-embedded-applications.md)
