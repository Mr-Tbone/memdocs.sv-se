---
title: Skapa och distribuera ett program
titleSuffix: Configuration Manager
description: Skapa och distribuera ett program som innehåller en branschspecifika app och lär dig hur du hanterar appar effektivt.
ms.date: 07/19/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: b2d2a3465aebf66db37722629991078093abaaa7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710512"
---
# <a name="create-and-deploy-an-application-with-configuration-manager"></a>Skapa och distribuera ett program med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I det här avsnittet ska du gå direkt till och skapa ett program med Configuration Manager. I det här exemplet ska du skapa och distribuera ett program som innehåller en branschspecifika app för Windows-datorer som heter **contoso. msi**, som måste installeras på alla datorer som kör Windows 10 i företaget. Under tiden får du lära dig mer om många av de saker du kan göra för att hantera program på ett effektivt sätt.  

 Den här proceduren är utformad för att ge dig en översikt över hur du skapar och distribuerar Configuration Manager-program. Det omfattar dock inte alla konfigurations alternativ, eller hur du skapar och distribuerar program för andra plattformar.  

 Mer information som är relevant för varje plattform finns i något av följande avsnitt:  

- [Skapa Windows-program](creating-windows-applications.md)
- [Skapa Windows Phone-program](../../mdm/deploy-use/management-tasks-applications.md#bkmk_winphone)
- [Skapa program för Mac-datorer](creating-mac-computer-applications.md)
- [Skapa serverprogram för Linux och UNIX](creating-linux-and-unix-server-applications.md)
- [Skapa Windows Embedded-program](creating-windows-embedded-applications.md)


Om du redan är bekant med Configuration Manager-program kan du hoppa över det här avsnittet. Men du kanske vill gå igenom [skapa program](../../apps/deploy-use/create-applications.md) för att lära dig om alla alternativ som är tillgängliga när du skapar och distribuerar program.  

## <a name="before-you-start"></a>Innan du börjar  

Se till att du har granskat informationen i [Introduktion till program hantering](../understand/introduction-to-application-management.md) så att du har för berett din plats för att installera program och du förstår den terminologi som används i det här avsnittet.  

 Se också till att installationsfilerna för **contoso. msi** -appen finns på en tillgänglig plats i nätverket.  

## <a name="create-the-configuration-manager-application"></a>Skapa Configuration Manager-programmet  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>Starta guiden Skapa program och skapa programmet  

1. Välj program **bibliotek** > **program hantering** > **program i**Configuration Manager-konsolen.  

2. På fliken **Start** går du till gruppen **skapa** och väljer **skapa program**.  

3. På sidan **Allmänt** i **guiden Skapa program**väljer du **hitta automatiskt information om det här programmet i installationsfiler**. I förväg fylls en del av informationen i guiden med information som extraheras från filen installation. msi. Ange följande information:  

   - **Typ**: Välj **Windows Installer (\*. msi-fil)**.  

   - **Plats**: Ange platsen ( **eller Välj plats** ) för installations filen **contoso. msi**. Observera att platsen måste anges i formatet * \\\Server\Share\File* Configuration Manager för att det ska gå att hitta installationsfilerna.  

   Du kommer att få något som ser ut som följande skärm bild:  

   ![Guiden program hantering, sidan Allmänt](media/App-management-wizard-general-page.png)  

4. Välj **Nästa**. På sidan **Importera information** visas viss information om appen och eventuella associerade filer som har importer ats till Configuration Manager. När du är färdig väljer du **Nästa** igen.  

5. På sidan **allmän information** kan du ange ytterligare information om programmet som hjälper dig att sortera och hitta det i Configuration Manager-konsolen.  

    Fältet **installations program** gör det dessutom möjligt att ange den fullständiga kommando rad som ska användas för att installera programmet på datorer. Du kan redigera detta om du vill lägga till egna egenskaper (till exempel **/q** för en obevakad installation).  

   > [!TIP]  
   > En del av fälten på den här sidan kan ha fyllts i automatiskt när du importerade programinstallationsfilerna.  

    Du får en skärm som ser ut ungefär som på följande skärm bild:  

    ![Sidan allmän information i guiden program hantering](media/App-management-wizard-general-information-page.png)  

6. Välj **Nästa**. På sidan Sammanfattning kan du bekräfta program inställningarna och sedan slutföra guiden.  

   Du har nu skapat programmet. Du hittar det genom att gå till arbets ytan **program bibliotek** , expandera **program hantering**och sedan välja **program**. För det här exemplet visas:  

   ![Bild av slutgiltig app](media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Granska programmets egenskaper och dess distributionstyp  

Nu när du har skapat ett program kan du förfina program inställningarna om du behöver. Om du vill titta på program egenskaperna väljer du appen och väljer sedan **Egenskaper**på fliken **Start** i gruppen **Egenskaper** .  

 I dialog rutan **<\> contoso-programegenskaper** ser du många objekt som du kan konfigurera för att förfina appens beteende. Mer information om alla inställningar som du kan konfigurera finns i [skapa program](../../apps/deploy-use/create-applications.md). För det här exemplet skulle du bara ändra några egenskaper för programmets distributionstyp.  

 Välj fliken **distributions typer** > **contoso program** distributions typ > **Redigera**.

En dialogruta som liknar denna visas:  

![Sidan Egenskaper för app Management-app](media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>Lägg till ett krav för distributionstypen

 Krav anger villkor som måste vara uppfyllda innan ett program kan installeras på en enhet.  Du kan välja bland inbyggda krav eller skapa egna. I det här exemplet lägger du till ett krav att programmet endast ska installeras på datorer som kör Windows 10.  

1. På sidan Egenskaper för distributions typ som du precis öppnat väljer du fliken **krav** .  

2. Välj **Lägg till** för att öppna dialog rutan **Skapa krav** .  

3. Ange följande information i dialogrutan **Skapa krav** :  

    - **Kategori**: **enhet**  

    - **Villkor**: **operativ system**  

    - **Regeltyp**: **värde**  

    - **Operator**: **en av**  

    - I listan med operativsystem väljer du **Windows 10**.  

    En dialogruta som ser ut så här syns:  

    ![Sidan krav på program hantering](media/App-management-requirements-page.png)  

4. Välj **OK** för att stänga varje egenskaps sida som du har öppnat. Gå sedan tillbaka till listan **program** i Configuration Manager-konsolen.  

> [!TIP]  
> Kraven kan hjälpa till att minska antalet Configuration Manager samlingar som du behöver. Eftersom du precis angav att programmet endast kan installeras på datorer som kör Windows 10 kan du senare distribuera detta till en samling som innehåller datorer som kör många olika operativ system. Men programmet kommer bara att installeras på Windows 10-datorer.

## <a name="add-the-application-content-to-a-distribution-point"></a>Lägg till programinnehållet till en distributionsplats  

Om du vill distribuera programmet till datorer måste du se till att program innehållet kopieras till en distributions plats. Datorer får åtkomst till distributions platsen för att installera programmet.  

> [!TIP]  
> Läs mer om distributions platser och innehålls hantering i Configuration Manager i [Hantera innehåll och innehålls infrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).

1. Välj **program varu bibliotek**i Configuration Manager-konsolen.  

2. I arbets ytan **program bibliotek** expanderar du **program**. Välj sedan det **contoso-program** som du skapade i listan med program.  

3. Välj **distribuera innehåll**i gruppen **distribution** på fliken **Start** .  

4. Kontrol lera att program namnet är korrekt på sidan **Allmänt** i **guiden Distribuera innehåll**och välj sedan **Nästa**.  

5. Granska informationen som ska kopieras till distributions platsen på sidan **innehåll** och välj sedan **Nästa**.  

6. På sidan **innehålls mål** väljer du **Lägg till** för att välja en eller flera distributions platser eller distributions plats grupper som program innehållet ska installeras på.  

7. Slutför guiden.  

Du kan kontrol lera att program innehållet har kopierats till distributions platsen från arbets ytan **övervakning** under**innehålls status**för **distributions status** > .  

## <a name="deploy-the-application"></a>Distribuera programmet  

Distribuera sedan programmet till en enhetssamling i din hierarki. I det här exemplet distribuerar du programmet till enhets samlingen **alla system** .  

> [!TIP]  
> Kom ihåg att endast Windows 10-datorer kommer att installera programmet på grund av de krav som du valde tidigare.

1. Välj program **bibliotek** > **program hantering** > **program i**Configuration Manager-konsolen.  

2. I listan med program väljer du det program som du skapade tidigare (**contoso-program**) och väljer sedan **distribuera**på fliken **Start** i gruppen **distribution** .  

3. På sidan **Allmänt** i **guiden distribuera program vara**väljer du **Bläddra** för att välja enhets samlingen **alla system** .  

4. På sidan **innehåll** kontrollerar du att den distributions plats som du vill att datorer ska installera programmet på är markerat.  

5. På sidan **distributions inställningar** ser du till att distributions åtgärden är inställd på **Installera**och att distributions syftet är inställt på **obligatoriskt**.  

    > [!TIP]  
    > Genom att ange distributions syftet som **obligatoriskt**ser du till att programmet installeras på datorer som uppfyller de krav som du har angett. Om du ställer in värdet på **Tillgängligt**kan användare installera programmet på begäran från Software Center.

6. På sidan **Schemaläggning** kan du ange när programmet ska installeras. I det här exemplet väljer du **Så fort som möjligt efter den tillgängliga tiden**.  

7. På sidan **användar upplevelse** väljer du **Nästa** för att acceptera standardvärdena.  

8. Slutför guiden.  

Använd informationen i följande **övervaka program** avsnittet för att se status för program distributionen.  

## <a name="monitor-the-application"></a>Övervaka programmet

 I det här avsnittet tar du en titt på distributions statusen för programmet som du precis har distribuerat.  

### <a name="to-review-the-deployment-status"></a>Granska distributionsstatusen  

1. I Configuration Manager-konsolen väljer du **övervakning** > av**distributioner**.  

2. I listan över distributioner väljer du **Contoso-programmet**.  

3. På fliken **Start** går du till gruppen **distribution** och väljer **Visa status**.  

4. Välj någon av följande flikar för att se fler status uppdateringar om program distributionen:  

    - **Lyckades**: programmet har installerats på de angivna datorerna.  

    - **Pågår**: programmet har inte slutfört installationen än.  

    - **Fel**: ett fel uppstod när programmet skulle installeras på de angivna datorerna. Mer information om felet visas också.  

    - **Kraven är inte uppfyllda**: inget installations försök har gjorts på de angivna enheterna eftersom de inte uppfyllde kraven som du konfigurerade (i det här exemplet, eftersom de inte körs på Windows 10).  

    - **Okänd**: Configuration Manager kunde inte rapportera status för distributionen. Kontrollera igen senare.  

> [!TIP]  
> Det finns några sätt som du kan övervaka program distributioner på. Fullständig information finns i [övervaka program](../deploy-use/monitor-applications-from-the-console.md).

## <a name="end-user-experience"></a>Upplevelse för slutanvändaren  

Användare som har datorer som hanteras av Configuration Manager och som kör Windows 10 visas ett meddelande som talar om att de måste installera Contoso-programmet. När de har accepterat installationen installeras programmet.  

Från och med Configuration Manager version 1906 kommer den **nya program varan att vara tillgänglig** bara att visa en gång för en användare för ett angivet program och en ny revision. Användaren kommer inte längre att se meddelandet varje gången de loggar in. De ser bara ett annat meddelande för ett program om programmet har ändrats eller omdistribuerats.

## <a name="next-steps"></a>Nästa steg

[Övervakning av program](../deploy-use/monitor-applications-from-the-console.md)
