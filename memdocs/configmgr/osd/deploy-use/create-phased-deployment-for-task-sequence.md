---
title: Skapa stegvisa distributioner
titleSuffix: Configuration Manager
description: Använd stegvisa distributioner för att automatisera distributionen av program vara till flera samlingar.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5af0b7c90225a1f42d55767a0296d7e2263f956f
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110465"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Skapa stegvisa distributioner med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Stegvisa distributioner automatiserar en samordnad, sekvenserad distribution av program vara i flera samlingar. Du kan till exempel distribuera program vara till en pilot samling och sedan automatiskt fortsätta med distributionen baserat på lyckade villkor. Skapa stegvisa distributioner med standardvärdet två faser eller konfigurera flera faser manuellt. 

Skapa stegvisa distributioner för följande objekt:
- **Aktivitetssekvens**  
    - Stegvis distribution av aktivitetssekvenser stöder inte PXE-eller medie installation   
- **Program** (från och med version 1806) <!--1358147-->  
- **Program uppdatering** (från och med version 1810) <!--1358146-->  
    - Du kan inte använda en automatisk distributions regel med en stegvis distribution

> [!Tip]  
> Funktionen för stegvis distribution introducerades först i version 1802 som en [för hands versions funktion](../../core/servers/manage/pre-release-features.md). Från och med version 1806 är det inte längre en för hands versions funktion.<!--1356837-->  



## <a name="prerequisites"></a>Krav

#### <a name="security-scope"></a>Säkerhets omfattning
Distributioner som skapats av stegvisa distributioner kan inte visas för administrativa användare som inte har säkerhets omfattningen **alla** . Mer information finns i [Säkerhetsomfattningar](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

#### <a name="distribute-content"></a>Distribuera innehåll
Innan du skapar en stegvis distribution distribuerar du det associerade innehållet till en distributions plats.<!--518293-->  

- **Program**: Välj mål programmet i-konsolen och Använd åtgärden **distribuera innehåll** i menyfliksområdet. Mer information finns i [distribuera och hantera innehåll](../../core/servers/deploy/configure/deploy-and-manage-content.md).   

- **Aktivitetssekvens**: du måste skapa refererade objekt som operativ systemets uppgraderings paket innan du skapar aktivitetssekvensen. Distribuera dessa objekt innan du skapar en distribution. Använd åtgärden **distribuera innehåll** för varje objekt eller aktivitetssekvensen. Om du vill visa status för allt refererat innehåll väljer du aktivitetssekvensen och växlar till fliken **referenser** i informations fönstret. Mer information finns i den angivna objekt typen i [förbereda för distribution av operativ system](../get-started/prepare-for-operating-system-deployment.md).   

- **Program uppdatering**: skapa distributions paketet och distribuera det. Använd guiden hämta program uppdateringar. Mer information finns i [Hämta program uppdateringar](../../sum/deploy-use/download-software-updates.md).  



## <a name="phase-settings"></a><a name="bkmk_settings"></a>Fas inställningar

De här inställningarna är unika för stegvisa distributioner. Konfigurera de här inställningarna när du skapar eller redigerar faser för att styra schemaläggningen och beteendet för den stegvisa distributions processen. 


#### <a name="criteria-for-success-of-the-first-phase"></a>Villkor för lyckad första fas  

- **Procent andel lyckade distributioner**: Ange procent andelen enheter som måste Slutför distributionen för att den första fasen ska lyckas. Som standard är det här värdet 95%. Med andra ord anser platsen att den första fasen lyckades när kompatibilitetstillstånd för 95% av enheterna är **klar** för den här distributionen. Webbplatsen fortsätter sedan till den andra fasen och skapar en distribution av program varan till nästa samling.  
- **Antal enheter som har distribuerats**: lades till i Configuration Manager version 1902. Ange det antal enheter som måste Slutför distributionen för att den första fasen ska lyckas. Det här alternativet är användbart när samlingens storlek är variabel och du har ett angivet antal enheter för att Visa lyckade innan du går vidare till nästa fas. <!--3555946-->


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Villkor för att starta den andra fasen av distributionen när den första fasen har lyckats  

- **Starta den här fasen automatiskt efter en uppskjutnings period (i dagar)**: Välj det antal dagar som ska förflyta innan den första fasen påbörjas efter att den första aktiviteten har lyckats. Som standard är det här värdet en dag.  

- **Starta den andra fasen av distributionen manuellt**: platsen startar inte automatiskt den andra fasen när den första fasen har slutförts. Det här alternativet kräver att du startar den andra fasen manuellt. Mer information finns i [gå vidare till nästa fas](manage-monitor-phased-deployments.md#bkmk_move).  

    > [!Note]  
    > Det här alternativet är inte tillgängligt för stegvis distribution av program.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Gör den här program varan tillgänglig under den här tids perioden (i dagar)
<!--1358578-->
Från och med version 1806 konfigurerar du den här inställningen för distributionen i varje fas för att ske gradvis. Det här beteendet minskar risken för distributions problem och minskar belastningen på nätverket som orsakas av distribution av innehåll till klienter. Webbplatsen gör program varan tillgänglig, beroende på konfigurationen för varje fas. Varje klient i en fas har en tids gräns i förhållande till den tid då program varan görs tillgänglig. Tidsfönstret mellan den tillgängliga tiden och tids gränsen är samma för alla klienter i en fas. Standardvärdet för den här inställningen är noll, så som standard är distributionen inte begränsad. Ange inte värdet högre än 30.<!--SCCMDocs-pr issue 2767--> 

![Stegvisa distributions kriterier för lyckade inställningar](media/phased-deployment-criteria-for-success.png)

#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Konfigurera tids gräns beteendet i förhållande till när program varan görs tillgänglig  

- **Installationen krävs så snart som möjligt**: Ange tids gränsen för installationen på enheten så snart enheten är riktad mot målet.  

- **Installationen krävs efter den här tids perioden**: Ange en tids gräns för installation ett visst antal dagar efter att enheten har angetts som mål. Som standard är det här värdet sju dagar.   


<!--### Examples
Include a timeline diagram
-->



## <a name="automatically-create-a-default-two-phase-deployment"></a><a name="bkmk_auto"></a>Skapa automatiskt en standard distribution i två faser

1. Starta guiden skapa stegvis distribution i Configuration Manager-konsolen. Den här åtgärden varierar beroende på vilken typ av program vara som du distribuerar:  

    - **Program** (endast i version 1806 eller senare): gå till **program varu biblioteket**, expandera **program hantering**och välj **program**. Välj ett befintligt program och välj sedan **skapa stegvis distribution** i menyfliksområdet.  

    - **Program uppdatering** (endast i version 1810 eller senare): gå till **program varu biblioteket**, expandera **program uppdateringar**och välj **alla program uppdateringar**. Välj en eller flera uppdateringar och välj sedan **skapa stegvis distribution** i menyfliksområdet.  

        Den här åtgärden är tillgänglig för program uppdateringar från följande noder:  
        - Programuppdateringar  
            - **Alla program uppdateringar**  
            - **Program uppdaterings grupper**   
        - Windows 10-underhåll, **alla Windows 10-uppdateringar**  
        - Office 365-klient hantering, **office 365-uppdateringar**  

    - **Aktivitetssekvens**: gå till arbets ytan **program varu bibliotek** , expandera **operativ system**och välj **aktivitetssekvenser**. Välj en befintlig aktivitetssekvens och välj sedan skapa stegvis **distribution** i menyfliksområdet.  

2. På sidan **Allmänt** anger du den stegvisa distributionen ett **namn**, en **Beskrivning** (valfritt) och väljer **Skapa automatiskt en standard distribution av två faser**.  

3. Välj **Bläddra** och välj en mål samling för både den **första samlings** -och **andra samlings** fälten. För en aktivitetssekvens och program uppdateringar väljer du från enhets samlingar. För ett program väljer du från användar-eller enhets samlingar. Välj **Nästa**.  

    > [!Important]  
    > Guiden skapa stegvis distribution meddelar dig inte om en distribution är potentiellt hög risk. Mer information finns i [Inställningar för att hantera högrisk distributioner](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) och Obs! när du [distribuerar en aktivitetssekvens](deploy-a-task-sequence.md).  

4. På sidan **Inställningar** väljer du ett alternativ för var och en av schemaläggnings inställningarna. Mer information finns i [fas inställningar](#bkmk_settings). Välj **Nästa** när du är klar.  

5. På sidan **faser** , se de två faserna som guiden skapar för de angivna samlingarna. Välj **Nästa**. De här anvisningarna beskriver proceduren för att automatiskt skapa en standard distribution i två faser. Med guiden kan du lägga till, ta bort, ändra ordning på, redigera eller Visa faser för en stegvis distribution. Mer information om dessa ytterligare åtgärder finns i [skapa en stegvis distribution med manuellt konfigurerade faser](#bkmk_manual).  

6. Bekräfta dina val på fliken **Sammanfattning** och välj sedan **Nästa** för att slutföra guiden.  

> [!NOTE]
> Från och med den 21 april 2020 kommer Office 365 ProPlus att byta namn till **Microsoft 365 appar för företag**. Mer information finns i [namn ändring för Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Du kanske fortfarande ser det gamla namnet i Configuration Manager-produkten och dokumentationen medan-konsolen uppdateras.  

## <a name="create-a-phased-deployment-with-manually-configured-phases"></a><a name="bkmk_manual"></a>Skapa en stegvis distribution med manuellt konfigurerade faser
<!--1358148--> 

Från och med version 1806 kan du skapa en stegvis distribution med manuellt konfigurerade faser för en aktivitetssekvens. Lägg till upp till 10 faser från fliken **faser** i guiden skapa stegvis distribution. 

> [!Note]  
> Du kan för närvarande inte skapa faser för ett program manuellt. Guiden skapar automatiskt två faser för program distributioner.


1. Starta guiden skapa stegvis distribution för antingen en aktivitetssekvens eller program uppdateringar.  

2. På sidan **Allmänt** i guiden skapa stegvis distribution anger du den stegvisa distributionen som **namn**, **Beskrivning** (valfritt) och väljer **Konfigurera alla faser manuellt**.  

3. Följande åtgärder är tillgängliga på sidan **faser** i guiden skapa stegvis distribution:  

    - **Filtrera** listan över distributions faser. Ange en tecken sträng för en Skift läges okänslig matchning av kolumnerna order, namn eller samling. 

    - **Lägg till** en ny fas:  

        1. På sidan **Allmänt** i guiden Lägg till fas anger du ett **namn** för fasen och bläddrar sedan till mål **fasens samling**. De ytterligare inställningarna på den här sidan är desamma som när du normalt distribuerar en aktivitetssekvens eller program uppdateringar.  

        2. På sidan **fas inställningar** i guiden Lägg till fas konfigurerar du schemaläggnings inställningarna och väljer **Nästa** när du är klar. Mer information finns i [Inställningar](#bkmk_settings).   

            > [!Note]  
            > Du kan inte redigera fas inställningarna, **procent andelen lyckade distributioner** eller **antalet enheter som har distribuerats** (version 1902 eller senare) i den första fasen. Den här inställningen gäller bara för faser som har en tidigare fas.  

        3. Inställningarna på sidorna **användar upplevelse** och **distributions platser** i guiden Lägg till fas är desamma som när du normalt distribuerar en aktivitetssekvens eller program uppdateringar.  

        4. Granska inställningarna på sidan **Sammanfattning** och slutför sedan guiden Lägg till fas.  

    - **Redigera**: den här åtgärden öppnar den valda fasens fönstret Egenskaper, som har flikar på samma sätt som sidorna i guiden Lägg till fas.  

    - **Ta bort**: den här åtgärden tar bort den valda fasen.  

       > [!Warning]  
       > Det finns ingen bekräftelse och inget sätt att ångra den här åtgärden.  

    - **Flytta upp** eller **Flytta ned**: guiden ordnar faserna genom att lägga till dem. Den senast tillagda fasen är sist i listan. Om du vill ändra ordningen väljer du en fas och använder sedan knapparna för att flytta fasens plats i listan.  

       > [!Important]  
       > Granska fas inställningarna när du har ändrat ordningen. Kontrol lera att följande inställningar fortfarande stämmer överens med dina krav för den här stegvisa distributionen:  
       > 
       > - Kriterier för lyckad föregående fas  
       > - Villkor för att starta den här fasen av distributionen efter en lyckad föregående fas   

5. Välj **Nästa**. Granska inställningarna på sidan **Sammanfattning** och slutför sedan guiden skapa stegvis distribution.  


När du har skapat en stegvis distribution öppnar du dess egenskaper för att göra ändringar:  

- **Lägg till** ytterligare faser i en befintlig stegvis distribution.  

- Om fasen inte är aktiv kan du **redigera**, **ta bort**eller **Flytta** upp eller ned den. Du kan inte flytta den innan en aktiv fas.  

- När en fas är aktiv är den skrivskyddad. Du kan inte redigera den, ta bort den eller flytta dess plats i listan. Det enda alternativet är att **Visa** egenskaperna för fasen.  

- En program fas distribution är alltid skrivskyddad.  



## <a name="next-steps"></a>Nästa steg

Hantera och övervaka stegvisa distributioner:
- [Program](manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)
- [Program uppdatering](manage-monitor-phased-deployments.md?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Aktivitetssekvens](manage-monitor-phased-deployments.md)  

