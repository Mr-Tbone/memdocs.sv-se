---
title: Paket och program
titleSuffix: Configuration Manager
description: Stöd distributioner som använder äldre paket och program med Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c87ae35fa3e5a76c57342a0d1cad4167b0f14685
ms.sourcegitcommit: e43e6e83e3b38137ceebc6d299eacd94a925db85
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88895954"
---
# <a name="packages-and-programs-in-configuration-manager"></a>Paket och program i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Configuration Manager fortsätter att stödja paket och program som användes i Configuration Manager 2007. En distribution som använder paket och program kan vara lämpligare än ett program när du distribuerar något av följande verktyg eller skript:  

- Administrativa verktyg som inte installerar ett program på en dator
- "En-av"-skript som inte behöver övervakas kontinuerligt  
- Skript som körs enligt ett återkommande schema och som inte kan använda global utvärdering

> [!TIP]  
> Överväg att använda [skript](create-deploy-scripts.md) funktionen i Configuration Manager-konsolen. Skript kan vara en bättre lösning för några av föregående scenarier i stället för att använda paket och program.

När du migrerar paket från en tidigare version av Configuration Manager kan du distribuera dem i din Configuration Manager-hierarki. När migreringen är klar visas paketen i noden **Paket** i arbetsytan **Programvarubibliotek**.

Du kan ändra och distribuera paketen på samma sätt som du gjorde med program varu distribution. **Guiden Importera paket från definition** finns kvar i Configuration Manager för att importera äldre paket. Annonser konverteras till distributioner när du migrerar från Configuration Manager 2007 till en Configuration Manager-hierarki.  

> [!NOTE]  
> Använd Package Conversion Manager för att konvertera paket och program till Configuration Manager program.  
>
> Från och med version 1806 integreras Package Conversion Manager med Configuration Manager. Mer information finns i [Package Conversion Manager](../pcm/package-conversion-manager.md).  

Paket kan använda vissa nya funktioner i Configuration Manager, inklusive distributions plats grupper och övervakning. Du kan inte distribuera Microsoft Application Virtualization (App-V)-program med paket och program i Configuration Manager. Om du vill distribuera virtuella program skapar du dem som Configuration Manager program. Mer information finns i [distribuera virtuella App-V-program](../get-started/deploying-app-v-virtual-applications.md).  


## <a name="create-a-package-and-program"></a>Skapa ett paket och program

### <a name="use-the-create-package-and-program-wizard"></a>Använda guiden Skapa paket och program

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **program hantering**och väljer noden **paket** .  

2. På fliken **Start** i menyfliksområdet väljer du **skapa paket**i gruppen **skapa** .  

3. Ange följande information på sidan **paket** i **guiden Skapa paket och program**:  

    - **Namn**: Ange ett namn på paketet med högst 50 tecken.  

    - **Beskrivning**: Ange en beskrivning för det här paketet med högst 128 tecken.  

    - **Tillverkare** (valfritt): Ange ett namn på tillverkaren som hjälper dig att identifiera paketet i Configuration Manager-konsolen. Namnet får innehålla högst 32 tecken.

    - **Språk** (valfritt): Ange språk versionen för paketet med högst 32 tecken.  

    - **Version** (valfritt): Ange ett versions nummer för paketet med högst 32 tecken.

    - **Det här paketet innehåller källfiler**: den här inställningen anger om paketet kräver att källfiler måste finnas på klient enheter. Som standard aktiverar guiden inte det här alternativet och Configuration Manager inte använder distributions platser för paketet. När du väljer det här alternativet anger du det paket innehåll som ska distribueras till distributions platser.  

    - **Källmapp**: om paketet innehåller källfiler väljer du **Bläddra** för att öppna dialog rutan **Ange källmapp** och anger platsen för paketets källfiler.  

        > [!NOTE]  
        > Datorkontot på platsservern måste ha läsbehörighet för den källmapp du anger.
        >
        > Windows begränsar käll Sök vägen till 256 tecken eller mindre. Den här gränsen gäller för paket källa och program. Mer information finns i [Namnge filer, sökvägar och namn områden](/windows/win32/fileio/naming-a-file).

    - Från och med version 1906, om du vill förcachelagra innehåll på en klient, anger du paketets **arkitektur** och **språk** . Mer information finns i [Konfigurera förinställt innehåll för cache](../../osd/deploy-use/configure-precache-content.md).<!--4224642-->  

4. På sidan **program typ** i **guiden Skapa paket och program**väljer du vilken typ av program som ska skapas och väljer sedan **Nästa**. Du kan skapa ett program för en [dator](#create-a-standard-program) eller [enhet](#create-a-device-program), eller så kan du hoppa över det här steget och skapa ett program senare.  

    > [!TIP]  
    > Om du vill skapa ett nytt program för ett befintligt paket väljer du först paketet. På fliken **Start** går du till gruppen **paket** och väljer **skapa program** för att öppna **guiden Skapa program**.  

#### <a name="create-a-standard-program"></a>Skapa ett standard program

1. På sidan **program typ** i **guiden Skapa paket och program**väljer du **standard program**och väljer sedan **Nästa**.  

2. På sidan **standard program** anger du följande information:  

    - **Namn** – Ange ett namn på programmet med högst 50 tecken.  

        > [!NOTE]  
        > Programnamn i ett paket måste vara unika. När du har skapat ett program kan du inte ändra dess namn.  

    - **Kommando rad**: Ange den kommando rad som ska användas för att starta programmet eller Välj **Bläddra** för att bläddra till filens plats.  

        Om du inte anger något tillägg för ett fil namn Configuration Manager försöker använda. com,. exe och. bat som möjliga tillägg.  

        När klienten kör programmet söker Configuration Manager efter filen på följande platser:

        - I paketet
        - Den lokala Windows-mappen
        - Den lokala *% Path%*

        Programmet Miss lyckas om filen inte hittas.  

    - **Startmapp** (valfritt): Ange mappen som programmet körs från, upp till 127 tecken. Den här mappen kan vara en absolut sökväg på klienten. Det kan också vara en sökväg som är relativ till den distributions plats mapp som innehåller paketet.

    - **Kör**: Ange i vilket läge programmet ska köras på klient datorer. Välj något av följande alternativ:  

        - **Normal**: programmet körs i normal läge baserat på standardinställningar för system och program. Det här är standardläget.  

        - **Minimerad**: programmet körs minimerat på klient enheter. Användarna kan se installations aktiviteten i meddelande fältet eller i aktivitets fältet.  

        - **Maximerat**: programmet körs maximerat på klient enheter. Användare ser all installations aktivitet.  

        - **Dolt**: programmet körs dolt på klient enheter. Användarna ser ingen installations aktivitet.  

    - **Programmet kan köra**: Ange om programmet endast körs när en användare är inloggad, endast när ingen användare är inloggad eller oavsett om en användare är inloggad på klient datorn eller inte.  

    - **Körnings läge**: Ange om programmet ska köras med administrativ behörighet eller med behörigheterna för den användare som för närvarande är inloggad.  

    - **Tillåt att användare visar och interagerar med programinstallationen**: Använd den här inställningen, om det är tillgängligt, för att ange om du vill tillåta att användare interagerar med programinstallationen. Det här alternativet är bara tillgängligt om följande villkor är uppfyllda:

        - Inställningen **program kan** bara köras **när ingen användare är inloggad** eller **om en användare är inloggad**
        - Inställningen **körnings läge** är att **köra med administratörs behörighet**  

    - **Enhets läge**: Ange information om hur programmet körs i nätverket. Välj något av följande alternativ:  

        - **Körs med UNC-namn**: ange att programmet körs med ett Universal Naming Convention namn (UNC). Den här inställningen är standardinställningen.  

        - **Enhets beteckning krävs**: ange att programmet kräver en enhets beteckning för att fullständigt kvalificera platsen. För den här inställningen kan Configuration Manager använda alla tillgängliga enhets bokstäver på klienten.  

        - **Kräver en speciell enhets beteckning**: ange att programmet kräver en speciell enhets beteckning som du anger för att fullständigt kvalificera platsen. Till exempel **Z:**. Om klienten redan använder den angivna enhets beteckningen körs inte programmet.  

    - **Återanslut till distributions plats vid inloggning**: Ange om klienten återansluter till distributions platsen när användaren loggar in. Som standard aktiverar guiden inte det här alternativet.

3. Ange följande information på sidan **krav** i **guiden Skapa paket och program** :  

    - **Kör ett annat program först**: identifiera ett paket och program som körs innan det här paketet och programmet körs.  

    - **Plattforms krav**: Välj **det här programmet kan köras på alla plattformar** eller **så kan det här programmet bara köras på specificerade plattformar**. Välj sedan de OS-versioner som klienter måste ha för att installera det här paketet och programmet.  

    - **Beräknat disk utrymme**: Ange hur mycket disk utrymme som krävs för att köra programmet på datorn. Standardvärdet är **Okänt**. Om det behövs anger du ett heltal som är större än eller lika med noll. Om du anger ett värde väljer du även enhet för värdet.  

    - **Högsta tillåtna körnings tid (minuter)**: Ange den längsta tid som du förväntar dig för att köra programmet på klient datorn. Standardvärdet är **120** minuter. Använd endast heltal som är större än noll.  

        > [!IMPORTANT]  
        > Om du använder underhålls perioder i samma samling som du distribuerar det här programmet till kan en konflikt uppstå om den **längsta tillåtna körnings tiden** är längre än det schemalagda underhålls fönstret. Om du ställer in den maximala körnings tiden på **okänd**börjar programmet köras under underhålls perioden. Den fortsätter sedan att köras efter behov när underhålls perioden stängs. Om du ställer in den maximala körnings tiden på en viss period som är större än längden på alla tillgängliga underhålls fönster, kör klienten inte programmet.  

        Om du ställer in det här värdet på **okänd**Configuration Manager ställer in den längsta tillåtna körnings tiden som 12 timmar (720 minuter).  

        > [!NOTE]  
        > Om programmet överskrider den maximala körnings tiden stoppar Configuration Manager det om följande villkor uppfylls:
        >
        > - Du aktiverar alternativet att **köra med administratörs behörighet**
        > - Du kan inte aktivera alternativet för att **tillåta att användare visar och interagerar med programinstallationen**  

#### <a name="create-a-device-program"></a>Skapa ett enhets program  

1. På sidan **program typ** i **guiden Skapa paket och program**väljer du **program för enhet**och väljer sedan **Nästa**.  

2. På sidan **program för enhet** anger du följande inställningar:  

    - **Namn**: Ange ett namn på programmet med högst 50 tecken.  

        > [!NOTE]  
        > Programnamn i ett paket måste vara unika. När du har skapat ett program kan du inte ändra dess namn.  

    - **Kommentar** (valfritt): Ange en kommentar för det här enhets programmet med högst 127 tecken.  

    - **Hämta mapp**: Ange namnet på mappen på enheten där paketets källfiler ska lagras. Standardvärdet är `\Temp\`.  

    - **Kommando rad**: Ange den kommando rad som ska användas för att starta programmet. Välj **Bläddra**för att bläddra till filens plats.  

    - **Kör kommando rad i Hämta mapp**: Välj det här alternativet om du vill köra programmet från Download-mappen.  

    - **Kör kommando raden från den här mappen**: Välj det här alternativet om du vill ange en annan mapp som programmet ska köras från.  

3. På sidan **krav** anger du följande inställningar:  

    - **Beräknat disk utrymme**: Ange hur mycket disk utrymme som krävs för program varan. Klienten visar det här värdet för användare av mobila enheter innan de installerar programmet.  

    - **Ladda ned program**: Ange information om när den mobila enheten kan hämta det här programmet. Du kan ange **Så snart som möjligt**, **Endast med snabbt nätverk** eller **Endast när enheten är dockad**.  

    - **Ytterligare krav**: Ange eventuella ytterligare krav för programmet. Användarna ser dessa krav innan de installerar program varan. Du kan till exempel meddela användarna om att de måste stänga alla andra program innan de kör programmet.  

## <a name="deploy-packages-and-programs"></a>Distribuera paket och program  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **program hantering**och väljer noden **paket** .  

2. Välj det paket som du vill distribuera. På fliken **Start** i menyfliksområdet väljer du **distribuera**i gruppen **distribution** .  

3. På sidan **Allmänt** i **guiden distribuera program vara**anger du namnet på det paket och program som du vill distribuera. Välj den samling som du vill distribuera paketet och programmet till och eventuella valfria kommentarer.  

    Om du vill lagra paket innehållet i samlingens standard distributions plats grupp väljer du alternativet för att **använda standard distributions plats grupper som är associerade med den här samlingen**. Det här alternativet är inte tillgängligt om du inte har associerat samlingen med en distributions plats grupp.  

4. På sidan **innehåll** väljer du **Lägg till**. Välj de distributions platser eller distributions plats grupper som du vill distribuera innehållet för det här paketet och programmet till.  

5. Konfigurera följande inställningar på sidan **distributions inställningar** :  

    - **Syfte**: Välj något av följande alternativ:

        - **Tillgängligt**: användaren ser det publicerade paketet och programmet i Software Center och kan installera det på begäran.  

        - **Krävs**: paketet och programmet distribueras automatiskt i enlighet med det konfigurerade schemat. I Software Center kan du spåra distributionens status och installera den före tids gränsen.  

        > [!NOTE]
        > Om flera användare är inloggade på enheten, kan det hända att paket och aktivitetssekvensdistributioner inte visas i Software Center.

    - **Skicka väcknings paket**: om du ställer in distributions syftet som **obligatoriskt** och väljer det här alternativet skickar platsen först ett väcknings paket till datorer vid installationens tids gräns. Innan du kan använda det här alternativet måste du konfigurera datorer för Wake On LAN. Mer information finns i [så här konfigurerar du Wake on LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

    - **Tillåt klienter på en avgiftsbelagd Internet-anslutning att hämta innehåll efter installationens tids gräns, vilket kan innebära ytterligare kostnader**  

    > [!NOTE]  
    > När du distribuerar ett paket och program är alternativet för att **distribuera program vara till användarens primära enhet** inte tillgängligt.  

6. Konfigurera när det här paketet och programmet ska distribueras till klient enheter på sidan **Schemaläggning** .  

    Alternativen på den här sidan varierar beroende på om du anger distributions åtgärden till **tillgänglig** eller **obligatorisk**.  

    För **obligatoriska** distributioner konfigurerar du omkörnings beteendet för programmet från den nedrullningsbara menyn **Kör beteende** . Välj bland följande alternativ:  

    | Omkörningsbeteende | Beskrivning |
    |----------------|-------------|
    | **Kör aldrig om distribuerade program** | Klienten kör inte om programmet. Det här problemet inträffar även om programmet ursprungligen misslyckades eller om programfilerna har ändrats. |
    | **Kör alltid om program** | Klienten kör alltid om programmet när distributionen har schemalagts. Det här beteendet inträffar även om programmet redan har körts. Det är användbart med återkommande distributioner när du uppdaterar programmet. |
    | **Kör om när föregående försök misslyckades** | Klienten kör programmet igen när distributionen har schemalagts, endast om den misslyckades på det föregående körnings försöket. |
    | **Kör om när föregående försök genomfördes** | Klienten kör bara programmet igen om det tidigare har körts på klienten. Det här beteendet är användbart med återkommande distributioner när du uppdaterar programmet rutinmässigt, och varje uppdatering kräver att den tidigare uppdateringen har installerats. |

7. Ange följande information på sidan **Användarupplevelse** :  

    - **Tillåt att användare kör programmet oberoende av tilldelningar**: användare kan installera den här program varan från Software Center oavsett schemalagd installations tid.  

    - **Programvaruinstallation**: Programvaran kan installeras utanför angivna underhållsperioder.  

    - **Systemomstart (om det krävs för att slutföra installationen)**: om program varu installationen kräver en omstart av enheten för att slutföras, kan den här åtgärden ske utanför alla konfigurerade underhålls fönster.  

    - **Inbäddade enheter**: när du distribuerar paket och program till Windows Embedded-enheter med aktiverat Skriv filter, kan du ange att de installerar paket och program på det tillfälliga överlägget och genomför ändringar senare. Du kan också spara ändringarna på installations tids gränsen eller under en underhålls period. När du genomför ändringar av installations tids gränsen eller under en underhålls period krävs en omstart och ändringarna sparas på enheten.  

        > [!NOTE]  
        > När du distribuerar ett paket eller program på en Windows Embedded-enhet bör du se till att enheten tillhör en samling som har en angiven underhållsperiod. Mer information om hur underhålls fönster används när du distribuerar paket och program till Windows Embedded-enheter finns i [skapa Windows Embedded-program](../get-started/creating-windows-embedded-applications.md).  

8. Ange följande information på sidan **Distributionsplatser** :  

    - **Distributions alternativ**: Ange den åtgärd som en klient när den använder en distributions plats i dess aktuella gränser grupp. Välj också åtgärden för klienten när den använder en distributions plats från en intilliggande gränser grupp eller standard platsens gränser grupp.

        > [!IMPORTANT]  
        > Om du konfigurerar distributions alternativet för att **köra program från distributions platsen**, se till att aktivera alternativet att **Kopiera innehållet i det här paketet till en paket resurs på distributions platser** på fliken **data åtkomst** i egenskaperna för paketet. Annars är paketet inte tillgängligt att köras från distributions platser.  

    - **Tillåt att klienter använder distributions platser från standard plats begränsnings gruppen**: om det här innehållet inte är tillgängligt från någon distributions plats i den aktuella eller intilliggande begränsnings gruppen aktiverar du det här alternativet för att låta dem testa distributions platser i standard begränsnings gruppen för webbplatsen.

9. Slutför guiden.  

Visa distributionen i noden **distributioner** på arbets ytan **övervakning** och i informations fönstret på fliken paket distribution när du väljer distributionen. Mer information finns i [övervaka paket och program](#monitor-packages-and-programs).  


## <a name="monitor-packages-and-programs"></a>Övervaka paket och program

Om du vill övervaka paket-och program distributioner använder du samma procedurer som du använder för att övervaka program som beskrivs i [övervaka program](monitor-applications-from-the-console.md).  

Paket och program innehåller också ett antal inbyggda rapporter som gör att du kan övervaka information om distributions statusen för paket och program. De här rapporterna tillhör rapportkategorin **Programvarudistribution – paket och program** och **Programvarudistribution – status för paket- och programdistribution**.  

Mer information om hur du konfigurerar rapportering i Configuration Manager finns i [Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md).  


## <a name="manage-packages-and-programs"></a>Hantera paket och program

I arbets ytan **program bibliotek** expanderar du **program hantering**och väljer noden **paket** . Välj det paket som du vill hantera och välj sedan en hanterings aktivitet.  

### <a name="create-prestage-content-file"></a>Skapa förinstallerad innehållsfil

Öppnar **guiden Skapa förinstallerad innehålls fil**för att skapa en fil som innehåller paket innehållet. Använd den här filen för att importera paketet manuellt till en fjärrdistributions plats. Den här åtgärden är användbar när du har låg nätverks bandbredd mellan plats servern och distributions platsen.

### <a name="create-program"></a>Skapa program

Öppnar **guiden Skapa program**för att skapa ett nytt program för det här paketet.

### <a name="export"></a>Exportera

Öppnar **guiden Exportera paket**för att exportera det valda paketet och dess innehåll till en fil. Använd den här filen för att importera filen till en annan hierarki.

Information om hur du importerar paket och program finns i [skapa paket och program](#create-a-package-and-program).

### <a name="deploy"></a>Distribuera

Öppnar **guiden distribuera program vara**för att distribuera det valda paketet och programmet till en samling. Mer information finns i [distribuera paket och program](#deploy-packages-and-programs).

### <a name="distribute-content"></a>Distribuera innehåll

Öppnar **guiden Distribuera innehåll**för att skicka innehållet för ett paket och program till valda distributions platser eller distributions plats grupper.

### <a name="update-distribution-points"></a>Uppdatera distributions platser

Uppdaterar distributionsplatser med det senaste innehållet för det valda paketet och programmet.


## <a name="see-also"></a>Se även

- [Skript](create-deploy-scripts.md)

- [Paketomvandlingshanteraren](../pcm/package-conversion-manager.md)

- [Paketdefinitionsfiler](package-definition-files.md)
