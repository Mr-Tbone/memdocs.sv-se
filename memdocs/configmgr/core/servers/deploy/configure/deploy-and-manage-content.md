---
title: Distribuera innehåll
titleSuffix: Configuration Manager
description: När du har installerat distributions platser för Configuration Manager kan du börja distribuera innehåll till dem.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df26fe91f009a1a4f5d3c5a4f4adb5fe45bbd245
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343158"
---
# <a name="deploy-and-manage-content-for-configuration-manager"></a>Distribuera och hantera innehåll för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du har installerat distributions platser för Configuration Manager kan du börja distribuera innehåll till dem. Normalt överförs innehåll till distributions platser över nätverket, men andra alternativ för att hämta innehåll till distributions platserna finns. När innehålls överföring till en distributions plats kan du uppdatera, distribuera om, ta bort och validera innehållet på distributions platser.  

##  <a name="distribute-content"></a><a name="bkmk_distribute"></a>Distribuera innehåll  
Normalt distribuerar du innehåll till distributions platser så att det är tillgängligt för klient datorer. (Undantaget till detta är när du använder innehålls distribution på begäran för en bestämd distribution.) När du distribuerar innehåll lagrar Configuration Manager innehållsfiler i ett paket och distribuerar sedan paketet till distributions platsen. Innehållet för paketet hämtas från plats serverns innehålls bibliotek. Typer av innehåll som du kan distribuera, inklusive:  

- Program distributions typer  

- Paket  

- Distributionspaket  

- Drivrutinspaket  

- Operativsystemavbildningar  

- Installations program för operativ system  

- Startavbildningar  

- Aktivitetssekvenser  

När du skapar ett paket som innehåller källfiler, till exempel en program distributions typ eller ett distributions paket, blir den plats där paketet skapas som plats ägare för paketets innehålls källa. Configuration Manager kopierar källfilerna från käll fils Sök vägen som du anger för objektet till innehålls biblioteket på den plats server som äger paketets innehålls källa.  Sedan replikerar Configuration Manager informationen till ytterligare platser. (Mer information om detta finns i [innehålls biblioteket](../../../../core/plan-design/hierarchy/the-content-library.md) .)  

Använd följande procedur för att distribuera innehåll till distributions platser.  

#### <a name="to-distribute-content-on-distribution-points"></a>Distribuera innehåll på distributions platser  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  I arbets ytan **program bibliotek** väljer du ett av följande steg för den typ av innehåll som du vill distribuera:  

    - **Program**: Expandera **program hanterings**  >  **program**och välj sedan de program som du vill distribuera.  

    - **Paket**: Expandera **program hanterings**  >   **paket**och välj sedan de paket som du vill distribuera.  

    - **Distributions paket**: **Software Updates**expandera  >   **distributions paket**för program uppdateringar och välj sedan de distributions paket som du vill distribuera.  

    - **Driv rutins paket**: Expandera **Operating Systems**  >   **driv rutins paket**för operativ system och välj sedan de driv rutins paket som du vill distribuera.  

    - **Operativ Systems avbildningar**: **expandera operativ system avbildningar**  >   **Operating System Images**och välj sedan de operativ Systems avbildningar som du vill distribuera.  

    - **Installations**program för operativ system: **expandera operativ**system  >  **installations program för**operativ system och välj sedan de installations program för operativ system som du vill distribuera.  

    - **Start avbildningar**: Expandera **operativ system**  >   **Start avbildningar**och välj sedan de start avbildningar som du vill distribuera.  

    - **Aktivitetssekvenser**: Expandera aktivitetssekvenser för **operativ system**  >   **Task Sequences**och välj sedan den aktivitetssekvens som du vill distribuera. Även om aktivitetssekvenser inte innehåller innehåll har de associerade innehålls beroenden som distribueras.  

      > [!NOTE]  
      > Om du ändrar aktivitetssekvensen måste du distribuera om innehållet.  

3.  Klicka på **Distribuera innehåll** på fliken **Start** i gruppen **Distribution**. Guiden Distribuera innehåll öppnas.  

4.  På sidan **Allmänt** kontrollerar du att innehållet i listan är det innehåll som du vill distribuera, väljer om du vill Configuration Manager identifiera innehålls beroenden som är associerade med det valda innehållet och lägger till beroenden i distributionen. Klicka sedan på **Nästa**.  

    > [!NOTE]  
    > Du har möjlighet att konfigurera **identifiera associerade innehålls beroenden och lägga till dem i distributions** inställningen endast för program innehålls typen. Configuration Manager konfigurerar automatiskt den här inställningen för aktivitetssekvenser och den kan inte ändras.  

5.  På fliken **innehåll** , om den visas, kontrollerar du att innehållet i listan är det innehåll som du vill distribuera och klickar sedan på **Nästa**.  

    > [!NOTE]  
    > Sidan **innehåll** visas bara när den **identifiera associerade innehålls beroenden och Lägg till dem i den här distributions** inställningen väljs på sidan **Allmänt** i guiden.  

6.  På sidan **innehålls mål** klickar du på **Lägg till**, väljer något av följande och följer sedan det associerade steget:  

    - **Samlingar**: Välj **användar samlingar** eller **enhets samlingar**, klicka på samlingen som är kopplad till en eller flera distributions plats grupper och klicka sedan på **OK**.  

        > [!NOTE]  
        > Endast samlingar som är associerade med en distributions plats grupp visas. Mer information om hur du kopplar samlingar till distributions plats grupper finns i [Hantera distributions plats grupper](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) i avsnittet [Installera och konfigurera distributions platser för Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) .  

    - **Distributions plats**: Välj en befintlig distributions plats och klicka sedan på **OK**. Distributions platser som tidigare har tagit emot innehållet visas inte.  

    - **Distributions plats grupp**: Välj en befintlig distributions plats grupp och klicka sedan på **OK**. Distributions plats grupper som tidigare har tagit emot innehållet visas inte.  

    När du är klar med att lägga till innehålls mål klickar du på **Nästa**.  

7.  På sidan **Sammanfattning** granskar du inställningarna för distributionen innan du fortsätter. Klicka på **Nästa**om du vill distribuera innehållet till de valda målen.  

8.  **Förlopps** sidan visar förloppet för distributionen.  

9. På sidan **bekräftelse** visas om innehållet har tilldelats till punkterna. Information om hur du övervakar innehålls distributionen finns i [Övervaka innehåll som du har distribuerat med Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

##  <a name="use-prestaged-content"></a><a name="bkmk_prestage"></a>Använd förinstallerat innehåll  
Du kan förinstallera innehållsfiler för program och paket typer:  

- I Configuration Manager-konsolen väljer du det innehåll som du behöver och använder sedan **guiden Skapa förinstallerad innehålls fil** för att skapa en komprimerad, förinstallerad innehålls fil som innehåller filerna och associerade metadata för det innehåll som du har valt.  

- Sedan kan du manuellt importera innehållet på en plats Server, sekundär plats eller distributions plats.  

- När du importerar den förinstallerade innehålls filen på en plats server läggs innehållsfilerna till i innehålls biblioteket på plats servern och registreras sedan i plats Server databasen.  

- När du importerar den förinstallerade innehålls filen på en distributions plats läggs innehållsfilerna till i innehålls biblioteket på distributions platsen och ett status meddelande skickas till plats servern som informerar platsen om att innehållet är tillgängligt på distributions platsen.  

**Begränsningar och överväganden för förinstallerat innehåll:**  

- **När distributions platsen finns på plats servern**ska du inte aktivera distributions platsen för förinstallerat innehåll. Använd i stället proceduren i [så här förbereder du innehåll på en distributions plats på en plats Server](#bkmk_dpsiteserver).  

- **När distributions platsen har kon figurer ATS som en mottagar distributions plats**ska du inte aktivera distributions platsen för förinstallerat innehåll. Den förinstallerade innehålls konfigurationen för en distributions plats åsidosätter konfigurationen av mottagar distributions platsen. En mottagar distributions plats som är konfigurerad för förinstallerat innehåll tar inte emot innehåll från käll distributions platsen och tar inte emot innehåll från plats servern.  

- **Innehålls biblioteket måste skapas på distributions platsen innan du kan förinstallera innehåll till distributions platsen**. Distribuera innehåll över nätverket minst en gång innan du förinstallerar innehåll på distributions platsen.  

- **När du förinstallerar innehåll för ett paket med en lång paket käll Sök väg** (till exempel fler än 140 tecken) kan kommando rads verktyget extrahera innehåll Miss lyckas med att extrahera innehållet för det paketet till innehålls biblioteket.  

Information om när du ska förinstallera innehållsfiler finns i *förinstallerat innehåll* i avsnittet [Hantera nätverks bandbredd för innehålls hantering](../../../plan-design/hierarchy/manage-network-bandwidth.md) .  

Använd följande avsnitt för att förinstallera innehåll.  

###  <a name="step-1-create-a-prestaged-content-file"></a><a name="BKMK_CreatePrestagedContentFile"></a>Steg 1: skapa en förinstallerad innehålls fil  
Du kan skapa en komprimerad, förinstallerad innehålls fil som innehåller filerna och associerade metadata för det innehåll som du väljer i Configuration Manager-konsolen. Använd följande procedur för att skapa en förinstallerad innehålls fil.  

##### <a name="to-create-a-prestaged-content-file"></a>Så här skapar du en förinstallerad innehålls fil  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  I arbets ytan **program bibliotek** väljer du ett av följande steg för den typ av innehåll som du vill förinstallera:  

    - **Program**: Expandera **program hantering**, klicka på **program**och välj sedan de program som du vill förinstallera.  

    - **Paket**: Expandera **program hantering**, klicka på **paket**och välj sedan de paket som du vill förinstallera.  

    - **Driv rutins paket**: Expandera **operativ system**, klicka på **driv rutins paket**och välj sedan de driv rutins paket som du vill förinstallera.  

    - **Operativ Systems avbildningar**: Expandera **operativ**system, klicka på **operativ Systems avbildningar**och välj sedan de operativ Systems avbildningar som du vill förinstallera.  

    - **Installations program för operativ system**: Expandera **operativ system**, klicka på **installations program för operativ system**och välj sedan de installations program för operativ system som du vill förinstallera.  

    - **Start avbildningar**: Expandera **operativ system**, klicka på **Start avbildningar**och välj sedan de start avbildningar som du vill förinstallera.  

    - **Aktivitetssekvenser**: Expandera **operativ system**, klicka på **aktivitetssekvenser**och välj sedan den aktivitetssekvens som du vill förinstallera.  

3.  På fliken **Start** går du till gruppen **distribution** och klickar på Skapa förinstallerad **innehålls fil**. Guiden Skapa förinstallerad innehålls fil öppnas.  

    > [!NOTE]  
    > **För program:** På fliken **Start** i gruppen **program** klickar du på **Skapa förinstallerad innehålls fil**.  
    >   
    > **För paket:** **Home** &lt; Klicka på **Skapa förinstallerad innehålls fil**i gruppen *PackageName*> på fliken Start.  

4.  På sidan **Allmänt** klickar du på **Bläddra**, väljer platsen för den förinstallerade innehålls filen, anger ett namn på filen och klickar sedan på **Spara**. Du använder den här förinstallerade innehålls filen på primära plats servrar, sekundära plats servrar eller distributions platser för att importera innehållet och metadata.  

5.  För program väljer du **Exportera alla beroenden** för att Configuration Manager identifiera och lägga till de beroenden som är associerade med programmet till den förinstallerade innehålls filen. Denna inställning är förinställd.  

6.  I **Administratörs kommentarer**anger du valfria kommentarer om den förinstallerade innehålls filen och klickar sedan på **Nästa**.  

7.  På sidan **innehåll** kontrollerar du att det innehåll som listas är det innehåll som du vill lägga till i den förinstallerade innehålls filen. Klicka sedan på **Nästa**.  

8.  På sidan **innehålls platser** anger du de distributions platser som innehållsfilerna ska hämtas från för den förinstallerade innehålls filen. Du kan välja fler än en distributions plats för att hämta innehållet. Distributions platserna visas i avsnittet innehålls platser. I kolumnen **innehåll** visas hur många av de valda paketen eller programmen som är tillgängliga på varje distributions plats. Configuration Manager börjar med den första distributions platsen i listan för att hämta det valda innehållet och flyttar sedan ned i listan för att hämta det återstående innehåll som krävs för den förinstallerade innehålls filen. Klicka på **Flytta upp** eller **Flytta ned** för att ändra prioritetsordningen för distributions platserna. Om distributions platserna i listan inte innehåller allt det valda innehållet, måste du lägga till distributions platser i listan som innehåller innehållet eller avsluta guiden, distribuera innehållet till minst en distributions plats och sedan starta om guiden.  

9. Bekräfta informationen på sidan **Sammanfattning** . Du kan gå tillbaka till föregående sidor och göra ändringar. Klicka på **Nästa** för att skapa den förinstallerade innehålls filen.  

10. Sidan **förlopp** visar det innehåll som läggs till i den förinstallerade innehålls filen.  

11. På sidan **slut för ande** kontrollerar du att den förinstallerade innehålls filen har skapats och klickar sedan på **Stäng**.  

###  <a name="step-2-assign-the-content-to-distribution-points"></a><a name="BKMK_AssignContentToDistributionPoint"></a>Steg 2: Tilldela innehållet till distributions platser  
 När du har förinstallerat innehålls filen tilldelar du innehållet till distributions platser.  

> [!NOTE]  
> När du använder en förinstallerad innehålls fil för att återställa innehålls biblioteket på en plats Server och inte behöver förinstallera innehållsfilerna på en distributions plats kan du hoppa över den här proceduren.  

 Använd följande procedur för att tilldela innehållet i den förinstallerade innehålls filen till distributions platser.  

> [!IMPORTANT]  
> Kontrol lera att de distributions platser som du vill förinstallera konfigureras som förinstallerade distributions platser eller att innehållet distribueras till distributions platserna med hjälp av nätverket.  

##### <a name="to-assign-the-content-to-distribution-points"></a>Tilldela innehållet till distributions platser  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  I arbets ytan **program bibliotek** väljer du ett av följande steg för den typ av innehåll som du valde när du skapade den förinstallerade innehålls filen:  

    - **Program**: Expandera **program hantering**, klicka på **program**och välj sedan de program som du har förinstallerat.  

    - **Paket**: Expandera **program hantering**, klicka på **paket**och välj sedan de paket som du har förinstallerat.  

    - **Distributions paket**: Expandera **program uppdateringar**, klicka på **distributions paket**och välj sedan de distributions paket som du har förinstallerat.  

    - **Driv rutins paket**: Expandera **operativ system**, klicka på **driv rutins paket**och välj sedan de driv rutins paket som du har förinstallerat.  

    - **Operativ Systems avbildningar**: Expandera **operativ**system, klicka på **operativ Systems avbildningar**och välj sedan de operativ Systems avbildningar som du har förinstallerat.  

    - **Installations program för operativ system**: Expandera **operativ**system, klicka på **installations program för operativ system**och välj sedan de installations program för operativ system som du har förinstallerat.  

    - **Start avbildningar**: Expandera **operativ system**, klicka på **Start avbildningar**och välj sedan de start avbildningar som du har förinstallerat.  

3.  Klicka på **Distribuera innehåll** på fliken **Start** i gruppen **Distribution**. Guiden Distribuera innehåll öppnas.  

4.  På sidan **Allmänt** kontrollerar du att innehållet i listan är det innehåll som du har förinstallerat, väljer om du vill Configuration Manager identifiera innehålls beroenden som är associerade med det valda innehållet och lägger till beroenden i distributionen. Klicka sedan på **Nästa**.  

    > [!NOTE]  
    > Du har möjlighet att konfigurera **identifiera associerade innehålls beroenden och lägga till dem i distributions** inställningen endast för program innehålls typen. Configuration Manager konfigurerar automatiskt den här inställningen för aktivitetssekvenser och den kan inte ändras.  

5.  På sidan **innehåll** , om det visas, kontrol lera att innehållet i listan är det innehåll som du vill distribuera och klicka sedan på **Nästa**.  

    > [!NOTE]  
    > Sidan **innehåll** visas bara när den **identifiera associerade innehålls beroenden och Lägg till dem i den här distributions** inställningen väljs på sidan **Allmänt** i guiden.  

6.  På sidan **innehålls mål** klickar du på **Lägg till**, väljer något av följande som innehåller de distributions platser som ska förinstalleras och följer sedan motsvarande steg:  

    - **Samlingar**: Välj **användar samlingar** eller **enhets samlingar**, klicka på samlingen som är kopplad till en eller flera distributions plats grupper och klicka sedan på **OK**.  

      > [!NOTE]  
      > Endast samlingar som är associerade med en distributions plats grupp visas.  Mer information finns i [Hantera distributions plats grupper](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) i avsnittet [Installera och konfigurera distributions platser för Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) .  

    - **Distributions plats**: Välj en befintlig distributions plats och klicka sedan på **OK**. Distributions platser som tidigare har tagit emot innehållet visas inte.  

    - **Distributions plats grupp**: Välj en befintlig distributions plats grupp och klicka sedan på **OK**. Distributions plats grupper som tidigare har tagit emot innehållet visas inte.  

    När du är klar med att lägga till innehålls mål klickar du på **Nästa**.  

7.  På sidan **Sammanfattning** granskar du inställningarna för distributionen innan du fortsätter. Klicka på **Nästa**om du vill distribuera innehållet till de valda målen.  

8.  **Förlopps** sidan visar förloppet för distributionen.  

9. På sidan **bekräftelse** visas om innehållet har tilldelats till distributions platserna eller inte. Information om hur du övervakar innehålls distributionen finns i [Övervaka innehåll som du har distribuerat med Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

###  <a name="step-3-extract-the-content-from-the-prestaged-content-file"></a><a name="BKMK_ExportContentFromPrestagedContentFile"></a>Steg 3: extrahera innehållet från den förinstallerade innehålls filen  
När du har skapat den förinstallerade innehålls filen och tilldelat innehållet till distributions platser kan du extrahera innehållsfilerna till innehålls biblioteket på en plats Server eller distributions plats. Normalt har du kopierat den förinstallerade innehålls filen till en bärbar enhet, till exempel en USB-enhet eller har bränt innehåll till media som en DVD och har den tillgänglig på den plats Server eller distributions plats som kräver innehållet.  

Använd följande procedur för att manuellt exportera innehållsfilerna från den förinstallerade innehålls filen med hjälp av kommando rads verktyget extrahera innehåll.  

> [!IMPORTANT]  
> När du kör kommando rads verktyget extrahera innehåll skapar verktyget en temporär fil som skapar den förinstallerade innehålls filen. Sedan kopieras filen till målmappen och den temporära filen tas bort. Du måste ha tillräckligt med disk utrymme för den här temporära filen, annars Miss lyckas processen. Den temporära filen skapas på följande plats:  
>   
> - Den temporära filen skapas i samma mapp som du anger som målmapp för den förinstallerade innehålls filen.  

> [!IMPORTANT]  
> Användaren som kör kommando rads verktyget extrahera innehåll måste ha **Administratörs** behörighet på den dator som du extraherar det förinstallerade innehållet från.  

##### <a name="to-extract-the-content-files-from-the-prestaged-content-file"></a>Extrahera innehållsfilerna från den förinstallerade innehålls filen  

1.  Kopiera den förinstallerade innehålls filen till den dator som du vill extrahera innehållet från.  

2.  Kopiera kommando rads verktyget extrahera innehåll från &lt; *ConfigMgrInstallationPath*> \Bin- \\ &lt; *plattformen*> till den dator som du vill extrahera den förinstallerade innehålls filen från.  

3.  Öppna kommando tolken och navigera till mappen för den förinstallerade innehålls filen och verktyget extrahera innehåll.  

    > [!NOTE]  
    > Du kan extrahera en eller flera filer med förinstallerat innehåll på en plats Server, sekundär plats Server eller distributions plats.  

4.  Skriv **extractcontent/p:** &lt; *PrestagedFileLocation* > **\\** &lt; *PrestagedFileName* >  **/s** för att importera en enskild fil.  

    Skriv **extractcontent/p:** &lt; *PrestagedFileLocation* >  **/s** för att importera alla förinstallerade filer i den angivna mappen.  

    Skriv till exempel **extractcontent/p: D:\PrestagedFiles\MyPrestagedFile.pkgx/s** där `D:\PrestagedFiles\` är PrestagedFileLocation, `MyPrestagedFile.pkgx` är namnet på den förinstallerade filen och `/S` informerar Configuration Manager att bara extrahera innehållsfiler som är nyare än vad som finns på distributions platsen.  

    När du extraherar den förinstallerade innehålls filen på en plats server läggs innehållsfilerna till i innehålls biblioteket på plats servern och innehållet är tillgängligt i plats Server databasen. När du exporterar den förinstallerade innehålls filen på en distributions plats läggs innehållsfilerna till i innehålls biblioteket på distributions platsen, distributions platsen skickar ett status meddelande till den överordnade primära plats servern och sedan registreras tillgänglighets innehållet i plats databasen.  

    > [!IMPORTANT]  
    > I följande scenario måste du uppdatera innehåll som du har extraherat från en förinstallerad innehålls fil när innehållet uppdateras till en ny version:  
    >   
    >  1.  Du skapar en förinstallerad innehålls fil för version 1 av ett paket.  
    >  2.  Du uppdaterar källfilerna för paketet med version 2.  
    >  3.  Du extraherar den förinstallerade innehålls filen (version 1 av paketet) på en distributions plats.  
    >   
    > Configuration Manager distribuerar inte paket version 2 automatiskt till distributions platsen. Du måste skapa en ny förinstallerad innehålls fil som innehåller den nya fil versionen och sedan extrahera innehållet, uppdatera distributions platsen för att distribuera de filer som har ändrats eller distribuera om alla filer i paketet.  

###  <a name="how-to-prestage-content-on-a-distribution-point-on-a-site-server"></a><a name="bkmk_dpsiteserver"></a>Förinstallera innehåll på en distributions plats på en plats Server  
När en distributions plats installeras på en plats Server måste du använda följande procedur för att kunna Förinstallera innehåll. Detta beror på att innehållsfilerna redan finns i innehålls biblioteket.  

Om distributions platsen inte är aktive rad för förinstallerat innehåll eller om distributions platsen inte finns på en plats Server, se avsnittet [använda förinstallerat innehåll](#bkmk_prestage) i det här avsnittet.  

##### <a name="to-prestage-content-on-distribution-points-located-on-a-site-server"></a>För att förinstallera innehåll på distributions platser som finns på en plats Server  

1.  Använd följande steg för att kontrol lera att distributions platsen inte är aktive rad för förinstallerat innehåll.  

    1.  Klicka på **Administration**i Configuration Manager-konsolen.  

    2.  Klicka på **distributions platser**i arbets ytan **Administration** och välj sedan den distributions plats som finns på plats servern.  

    3.  På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  

    4.  På fliken **Allmänt** kontrollerar du att kryss rutan **Aktivera den här distributions platsen för förinstallerat innehåll** inte är markerad.  

2.  Skapa den förinstallerade innehålls filen med hjälp av avsnittet [steg 1: skapa en förinstallerad innehålls fil](#BKMK_CreatePrestagedContentFile) i det här avsnittet.  

3.  Tilldela innehållet till distributions platsen med hjälp av [stegen 2: Tilldela innehållet till distributions platser](#BKMK_AssignContentToDistributionPoint) i det här avsnittet.  

4.  På plats servern extraherar du innehållet från den förinstallerade innehålls filen genom att följa [stegen 3: extrahera innehållet från den förinstallerade innehålls filen](#BKMK_ExportContentFromPrestagedContentFile) i det här avsnittet.  

    > [!NOTE]  
    > När distributions platsen finns på en sekundär plats väntar du minst 10 minuter, och sedan använder du en Configuration Manager-konsol som är ansluten till den överordnade primära platsen och tilldelar innehållet till distributions platsen på den sekundära platsen.  

##  <a name="manage-the-content-you-have-distributed"></a><a name="bkmk_manage"></a>Hantera det innehåll som du har distribuerat  
Du har följande alternativ för att hantera innehåll:  
- [Uppdatera innehåll](#update-content)
- [Distribuera om innehåll](#redistribute-content)
- [Ta bort innehåll](#remove-content)
- [verifiera innehåll](#validate-content)

### <a name="update-content"></a>Uppdatera innehåll
När käll fils platsen för en distribution uppdateras genom att lägga till nya filer eller ersätta befintliga filer med en nyare version, kan du uppdatera innehållsfilerna på distributions platserna genom att använda åtgärden **Uppdatera distributions platser** eller **Uppdatera innehåll** :  
- Innehållsfilerna kopieras från den ursprungliga paket käll platsen till innehålls biblioteket på den plats som äger paketets innehålls källa
- Paket versionen ökas  
- Varje instans av innehålls biblioteket på plats servrar och distributions platser uppdateras bara med de filer som har ändrats  

> [!WARNING]  
> Paket versionen för program är alltid 1. När du uppdaterar innehållet för en program distributions typ skapar Configuration Manager ett nytt innehålls-ID för distributions typen och paketet refererar till det nya innehålls-ID: t.  

#### <a name="to-update-content-on-distribution-points"></a>Uppdatera innehåll på distributions platser  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  I arbets ytan **program bibliotek** väljer du ett av följande steg för den typ av innehåll som du vill distribuera:  

    - **Program**: Expandera **program hanterings**  >  **program**och välj sedan de program som du vill distribuera. Klicka på fliken **distributions typer** och välj sedan den distributions typ som du vill uppdatera.  

    - **Paket**: Expandera **program hanterings**  >  **paket**och välj sedan de paket som du vill uppdatera.  

    - **Distributions paket**: **Software Updates**expandera  >  **distributions paket**för program uppdateringar och välj sedan de distributions paket som du vill uppdatera.  

    - **Driv rutins paket**: Expandera **Operating Systems**  >  **driv rutins paket**för operativ system och välj sedan de driv rutins paket som du vill uppdatera.  

    - **Operativ Systems avbildningar**: **expandera operativ system avbildningar**  >  **Operating System Images**och välj sedan de operativ Systems avbildningar som du vill uppdatera.  

    - **Installations**program för operativ system: Expandera operativ system **Operating Systems**  >  **installations program**för operativ system och välj sedan de installations program för operativ system som du vill uppdatera.  

    - **Start avbildningar**: Expandera **operativ system**  >   **Start avbildningar**och välj sedan de start avbildningar som du vill uppdatera.  

3.  På fliken **Start** går du till gruppen **distribution** och klickar på **Uppdatera distributions platser**. Klicka sedan på **OK** för att bekräfta att du vill uppdatera innehållet.  

    > [!NOTE]  
    > Om du vill uppdatera innehållet för program klickar du på fliken **distributions typer** , högerklickar på distributions typ, klickar på **Uppdatera innehåll**och bekräftar sedan att du vill uppdatera innehållet genom att klicka på **OK** .  

    > [!NOTE]  
    > När du uppdaterar innehåll för start avbildningar öppnas guiden Hantera distributions plats. Granska informationen på sidan **Sammanfattning** och slutför sedan guiden för att uppdatera innehållet.  

### <a name="redistribute-content"></a>Distribuera om innehåll
Du kan distribuera om ett paket för att kopiera alla innehållsfiler i paketet till distributions platser eller distributions plats grupper och därmed skriva över de befintliga filerna.  

Använd den här åtgärden för att reparera innehållsfiler i paketet eller skicka om innehållet när den första distributionen Miss lyckas. Du kan distribuera om ett paket från:  

- Paket egenskaper  
- Egenskaper för distributions plats  
- Egenskaper för distributions plats grupp.  


#### <a name="to-redistribute-content-from-package-properties"></a>Distribuera om innehåll från paket egenskaper  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  I arbets ytan **program bibliotek** väljer du ett av följande steg för den typ av innehåll som du vill distribuera:  

    - **Program**: Expandera **program hanterings**  >   **program**och välj sedan det program som du vill distribuera om.  

    - **Paket**: Expandera **program hanterings**  >  **paket**och välj sedan det paket som du vill distribuera om.  

    - **Distributions paket**: **Software Updates**expandera  >   **distributions paket**för program uppdateringar och välj sedan det distributions paket som du vill distribuera om.  

    - **Driv rutins paket**: Expandera **Operating Systems**  >  **driv rutins paket**för operativ system och välj sedan det driv rutins paket som du vill distribuera om.  

    - **Operativ Systems avbildningar**: **expandera operativ system avbildningar**  >  **Operating System Images**och välj sedan den operativ Systems avbildning som du vill distribuera om.  

    - **Installations**program för operativ system: **expandera operativ system installations**  >  **Operating System Installers**program och välj sedan de installations program för operativ system som du vill distribuera om.  

    - **Start avbildningar**: Expandera **operativ system**  >   **Start avbildningar**och välj sedan den Start avbildning som du vill distribuera om.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  

4.  Klicka på fliken **innehålls platser** , Välj den distributions plats eller distributions plats grupp som du vill distribuera om innehållet i, klicka på **distribuera**om och klicka sedan på **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-properties"></a>Distribuera om innehåll från distributions plats egenskaper  

1.  Klicka på **Administration**i Configuration Manager-konsolen.  

2.  Klicka på **distributions platser**i arbets ytan **Administration** och välj sedan den distributions plats som du vill distribuera om innehållet i.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  

4.  Klicka på fliken **innehåll** , Välj det innehåll som du vill distribuera om, klicka på **distribuera**om och klicka sedan på **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-group-properties"></a>Distribuera om innehåll från egenskaper för distributions plats grupp  

1.  Klicka på **Administration**i Configuration Manager-konsolen.  

2.  Klicka på **distributions plats grupper**i arbets ytan **Administration** och välj sedan den distributions plats grupp som du vill distribuera om innehållet i.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  

4.  Klicka på fliken **innehåll** , Välj det innehåll som du vill distribuera om, klicka på **distribuera**om och klicka sedan på **OK**.  

    > [!IMPORTANT]  
    > Innehållet i paketet distribueras om till alla distributions platser i distributions plats gruppen.  


#### <a name="use-the-sdk-to-force-replication-of-content"></a>Använd SDK för att framtvinga replikering av innehåll
Du kan använda klass metoden **RetryContentReplication** Windows Management INSTRUMENTATION (WMI) från Configuration Manager SDK för att tvinga distributions hanteraren att kopiera innehåll från käll platsen till innehålls biblioteket.  

Använd bara den här metoden för att tvinga replikering när du måste omdistribuera innehållet när det har uppstått problem med normal replikering av innehåll (som vanligt vis bekräftas med hjälp av noden övervakning i-konsolen).   

Mer information om SDK-alternativet finns [i RetryContentReplication-metod i klass SMS_CM_UpdatePackages](../../../../develop/reference/sum/retrycontentreplication-method-in-class-sms_cm_updatepackages.md).

### <a name="remove-content"></a>Ta bort innehåll
När du inte längre behöver innehåll på dina distributions platser kan du ta bort innehållsfilerna på distributions platsen.  

- Paket egenskaper  
- Egenskaper för distributions plats  
- Egenskaper för distributions plats grupp.  

Men när innehållet associeras med ett annat paket som har distribuerats till samma distributions plats kan du inte ta bort innehållet.  

#### <a name="to-remove-package-content-files-from-distribution-points"></a>Så här tar du bort paketets innehållsfiler från distributions platser  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  I arbets ytan **program bibliotek** väljer du ett av följande steg för den typ av innehåll som du vill ta bort:  

    - **Program**: Expandera **program hanterings**  >  **program**och välj sedan det program som du vill ta bort.  

    - **Paket**: Expandera **program hanterings**  >  **paket**och välj sedan det paket som du vill ta bort.  

    - **Distributions paket**: **Software Updates**expandera  >  **distributions paket**för program uppdateringar och välj sedan det distributions paket som du vill ta bort.  

    - **Driv rutins paket**: Expandera **Operating Systems**  >  **driv rutins paket**för operativ system och välj sedan det driv rutins paket som du vill ta bort.  

    - **Operativ Systems avbildningar**: **expandera operativ system avbildningar**  >  **Operating System Images**och välj sedan den operativ Systems avbildning som du vill ta bort.  

    - **Installations**program för operativ system: **expandera operativ system installations**  >  **Operating System Installers**program och välj sedan det installations program för operativ system som du vill ta bort.  

    - **Start avbildningar**: Expandera **operativ system**  >  **Start avbildningar**och välj sedan den Start avbildning som du vill ta bort.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  

4.  Klicka på fliken **innehålls platser** , Välj den distributions plats eller distributions plats grupp som du vill ta bort innehållet från, klicka på **ta bort**och sedan på **OK**.  

#### <a name="to-remove-package-content-from-distribution-point-properties"></a>Ta bort paket innehåll från distributions plats egenskaper  

1.  Klicka på **Administration**i Configuration Manager-konsolen.  

2.  Klicka på **distributions platser**i arbets ytan **Administration** och välj sedan den distributions plats där du vill ta bort innehållet.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  

4.  Klicka på fliken **innehåll** , Välj det innehåll som du vill ta bort, klicka på **ta bort**och klicka sedan på **OK**.  

#### <a name="to-remove-content-from-distribution-point-group-properties"></a>Ta bort innehåll från egenskaper för distributions plats grupp  

1.  Klicka på **Administration**i Configuration Manager-konsolen.  

2.  Klicka på **distributions plats grupper**i arbets ytan **Administration** och välj sedan den distributions plats grupp som du vill ta bort innehållet i.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  

4.  Klicka på fliken **innehåll** , Välj det innehåll som du vill ta bort, klicka på **ta bort**och klicka sedan på **OK**.  


### <a name="validate-content"></a>Verifiera innehåll
Med innehålls validerings processen verifieras integriteten för innehållsfiler på distributions platser. Du aktiverar innehålls validering enligt ett schema, eller så kan du starta innehålls validering manuellt från egenskaperna för distributions platser och paket.  

När innehålls validerings processen startar verifierar Configuration Manager innehållsfilerna på distributions platser, och om filhashen är oväntad för filerna på distributions platsen skapar Configuration Manager ett status meddelande som du kan granska i arbets ytan **övervakning** .  

Mer information om hur du konfigurerar schema för innehålls validering finns i [konfigurationer för distributions](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) platser i avsnittet [Installera och konfigurera distributions platser för Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) .  


#### <a name="to-initiate-content-validation-for-all-content-on-a-distribution-point"></a>Initiera innehålls validering för allt innehåll på en distributions plats  

1.  Klicka på **Administration**i Configuration Manager-konsolen.  

2.  Klicka på **distributions platser**i arbets ytan **Administration** och välj sedan den distributions plats som du vill validera innehållet i.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  

4.  På fliken **innehåll** väljer du det paket där du vill verifiera innehållet, klickar på **validera**, klickar på **OK**och klickar sedan på **OK**. Innehålls validerings processen initieras för paketet på distributions platsen.  

5.  Om du vill visa resultatet av innehålls validerings processen expanderar du **distributions status**på arbets ytan **övervakning** och klickar på noden **innehålls status** . Innehållet för varje paket typ (till exempel program, program uppdaterings paket och start avbildning) visas. Mer information om övervakning av innehålls status finns i [Övervaka innehåll som du har distribuerat med Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

#### <a name="to-initiate-content-validation-for-a-package"></a>Initiera innehålls validering för ett paket  

1.  I Configuration Manage-konsolen klickar du på **Programbibliotek**.  

2.  I arbets ytan **program bibliotek** väljer du ett av följande steg för den typ av innehåll som du vill verifiera:  

    - **Program**: Expandera **program hanterings**  >  **program**och välj sedan det program som du vill validera.  

    - **Paket**: Expandera **program hanterings**  >  **paket**och välj sedan det paket som du vill validera.  

    - **Distributions paket**: **Software Updates**expandera  >  **distributions paket**för program uppdateringar och välj sedan det distributions paket som du vill validera.  

    - **Driv rutins paket**: Expandera **Operating Systems**  >  **driv rutins paket**för operativ system och välj sedan det driv rutins paket som du vill validera.  

    - **Operativ Systems avbildningar**: **expandera operativ system avbildningar**  >  **Operating System Images**och välj sedan den operativ Systems avbildning som du vill validera.  

    - **Installations**program för operativ system: **expandera operativ system installations**  >   **Operating System Installers**program och välj sedan de installations program för operativ system som du vill validera.  

    - **Start avbildningar**: Expandera **operativ system**  >  **Start avbildningar**och välj sedan den Start avbildning som du vill förinstallera.  

3.  På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  

4.  På fliken **innehålls platser** väljer du den distributions plats eller distributions plats grupp som du vill validera innehållet i, klickar på **validera**, klickar på **OK**och klickar sedan på **OK**. Innehålls validerings processen startar för innehållet på den valda distributions platsen eller distributions plats gruppen.  

5.  Om du vill visa resultatet av innehålls validerings processen expanderar du **distributions status**på arbets ytan **övervakning** och klickar på noden **innehålls status** . Innehållet för varje paket typ (till exempel program, program uppdaterings paket och start avbildning) visas. Mer information om övervakning av innehålls status finns i [Övervaka innehåll som du har distribuerat med Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  
