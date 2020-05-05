---
title: Skapa program för Mac-datorer
titleSuffix: Configuration Manager
description: Se vilka överväganden du måste ta med i beräkningen när du skapar och distribuerar program för Mac-datorer.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3b734dc6149c1613d986205577b46160d363d31d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075796"
---
# <a name="create-mac-computer-applications-with-configuration-manager"></a>Skapa program för Mac-datorer med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Tänk på följande när du skapar och distribuerar program för Mac-datorer.  

> [!IMPORTANT]  
>  Procedurerna i det här avsnittet beskriver hur du distribuerar program till Mac-datorer där du har installerat Configuration Manager-klienten. Mac-datorer som du har registrerat med Microsoft Intune stöder inte programdistribution.  

## <a name="general-considerations"></a>Generella saker att tänka på  
 Du kan använda Configuration Manager för att distribuera program till Mac-datorer som kör Configuration Manager Mac-klienten. Stegen för att distribuera program till Mac-datorer liknar stegen för att distribuera program vara till Windows-datorer. Men innan du skapar och distribuerar program för Mac-datorer som hanteras av Configuration Manager bör du tänka på följande:  

-   Innan du kan distribuera Mac-programpaket till Mac-datorer måste du använda verktyget **CMAppUtil** på en Mac-dator för att konvertera programmen till ett format som kan läsas av Configuration Manager.  

-   Configuration Manager stöder inte distribution av Mac-program till användare. I stället måste dessa distributioner göras till en enhet. På samma sätt stöder inte Configuration Manager för distribution av Mac-program den **förinstallerade program varan till användarens primära enhets** alternativ på sidan **distributions inställningar** i **guiden distribuera program vara**.  

-   Mac-program har stöd för simulerad distribution.  

-   Du kan inte distribuera program till Mac-datorer som har syftet **Tillgänglig**.  

-   Möjligheten att skicka aktiveringspaket när du distribuerar programvara stöds inte för Mac-datorer.  

-   Mac-datorer stöder inte Background Intelligent Transfer Service (BITS) för att ladda ned program innehåll. Om det inte går att ladda ned ett program startas det om från början.  

-   Configuration Manager stöder inte globala villkor när du skapar distributions typer för Mac-datorer.  

## <a name="steps-to-create-and-deploy-an-application"></a>Steg för att skapa och distribuera ett program  
 Följande tabell innehåller steg, detaljer och information om hur du skapar och distribuerar program för Mac-datorer.  


|                                         Steg                                          |                                                                                                             Information                                                                                                              |
|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|            **Steg 1**: Förbered Mac-program för Configuration Manager             | Innan du kan skapa Configuration Manager-program från Mac-programpaket måste du använda verktyget **CMAppUtil** på en Mac-dator för att konvertera Mac-programvaran till en Configuration Manager<strong>. cmmac</strong> -fil. |
| **Steg 2**: skapa ett Configuration Manager-program som innehåller Mac-programvaran |                                                                       Använd **guiden Skapa program** för att skapa ett program för Mac-programvaran.                                                                       |
|             **Steg 3**: skapa en distributions typ för Mac-programmet              |                                                              Det här steget krävs bara om du inte automatiskt importerat informationen från programmet.                                                               |
|                        **Steg 4**: Distribuera Mac-programmet                         |                                                                          Använd **guiden distribuera program vara** för att distribuera programmet till Mac-datorer.                                                                          |
|               **Steg 5**: övervaka distributionen av Mac-programmet               |                                                                                 Övervaka programdistributionens förlopp på Mac-datorerna.                                                                                 |

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Kompletterande procedurer för att skapa och distribuera program för Mac-datorer  
 Använd följande procedurer för att skapa och distribuera program för Mac-datorer som hanteras av Configuration Manager.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>Steg 1: Förbered Mac-program för Configuration Manager  
 Processen för att skapa och distribuera Configuration Manager program till Mac-datorer liknar distributions processen för Windows-datorer. Innan du skapar Configuration Manager-program som innehåller Mac-distributions typer måste du dock förbereda programmen med hjälp av verktyget **CMAppUtil** . Verktyget laddas ned tillsammans med installationsfilerna för Mac-klienten. Verktyget **CMAppUtil** kan samla in information om programmet, vilket innefattar avkänningsdata från följande Mac-paket:  

-   Apple Disk Image (.dmg)  

-   Meta Package File (.mpkg)  

-   Mac OS X Installer-paket (.pkg)  

-   Mac OS X-program (.app)  

När **CMAppUtil** har samlat in programinformation skapas en fil med tillägget **.cmmac**. Den här filen innehåller installationsfilerna för Mac-programvaran och information om identifieringsmetoder som kan användas för att utvärdera om programmet redan är installerat. **CMAppUtil** kan också bearbeta **.dmg** -filer som innehåller flera Mac-program och skapa olika distributionstyper för varje program.  

1.  Kopiera Mac-programmets installationspaket till den mapp på Mac-datorn där du extraherade innehållet i den **macclient.dmg** -fil som du laddade ned från Microsoft Download Center.  

2.  På samma Mac-dator öppnar du ett terminalfönster och öppnar sedan den mapp där du extraherade innehållet i **macclient.dmg** -filen.  

3.  Navigera till mappen **verktyg** och skriv följande kommando rads kommando:  

     **./CMAppUtil** *<properties\>*  

     Anta till exempel att du vill konvertera innehållet i en Apple Disk Image-fil med namnet **program vara. dmg** som lagras i användarens Skriv bords mapp i en **cmmac** -fil i samma mapp. Du vill också skapa **cmmac** -filer för alla program som finns i disk avbildnings filen. Du gör detta med följande kommandorad:  

     **./CMApputil –c /Users/** *<User Name\>* **/Desktop/MySoftware.dmg -o /Users/** *<User Name\>* **/Desktop -a**  

    > [!NOTE]  
    >  Program namnet får innehålla högst 128 tecken.  

     Du konfigurerar alternativ för **CMAppUtil**med kommandoradsegenskaperna i följande tabell:  

  	|Egenskap|Mer information|  
  	|--------------|----------------------|  
  	|**-h**|Visar tillgängliga egenskaper för kommandoraden.|  
  	|**-r**|Utdata i **detection.xml** för den angivna **.cmmac** -filen till **stdout**. Utdatan innehåller de avkänningsparametrar och den version av **CMAppUtil** som användes för att skapa **.cmmac**-filen.|  
  	|**-c**|Anger käll filen som ska konverteras.|  
  	|**-o**|Anger sökvägen för utdata tillsammans med egenskapen – c.|  
  	|**– a**|Skapar automatiskt. cmmac-filer tillsammans med egenskapen – c för alla program och paket i disk avbildnings filen.|  
  	|**-s**|Hoppar över skapandet av **detection.xml** om inga avkänningsparametrar påträffas, och framtvingar skapande av **.cmmac** -filen utan filen **detection.xml** .|  
  	|**-v**|Visar mer detaljerad information från verktyget **CMAppUtil** tillsammans med diagnostisk information.|  

4.  Kontrollera att **.cmmac** -filen har skapats i den utdatamapp du angav.  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>Skapa ett Configuration Manager-program som innehåller Mac-programvaran  

Använd följande procedur för att hjälpa dig att skapa ett program för Mac-datorer som hanteras av Configuration Manager.  

1.  Välj program **bibliotek** > **program hantering** > **program i**Configuration Manager-konsolen.  

3.  På fliken **Start** går du till gruppen **skapa** och väljer **skapa program**.  

4.  På sidan **Allmänt** i **guiden Skapa program**väljer du **hitta automatiskt information om det här programmet i installationsfiler**.  

    > [!NOTE]  
    >  Om du vill ange information om programmet själv väljer du **Ange programinformationen manuellt**. Mer information om hur du manuellt anger informationen finns i [så här skapar du program med Configuration Manager](../../apps/deploy-use/create-applications.md).  

5.  I listrutan **Typ** väljer du **Mac OS X**.  

6.  I fältet **plats** anger du UNC-sökvägen i formuläret * \\ \\<Server\> \\ \> \\<dela<filename\> * till installations filen för Mac-programmet (**. cmmac** -fil) som ska identifiera programinformation. Alternativt kan du välja **Bläddra** för att bläddra till och ange installations filens plats.  

    > [!NOTE]  
    >  Du måste ha åtkomst till den UNC-sökväg som innehåller programmet.  

7.  Välj **Nästa**.  

8.  På sidan **Importera information** i **guiden Skapa program**granskar du den information som har importer ATS. Om det behövs kan du välja **föregående** för att gå tillbaka och korrigera eventuella fel. Fortsätt genom att välja **Nästa** .  

9. På sidan **allmän information** i **guiden Skapa program**anger du information om programmet, till exempel program namn, kommentarer, version och en valfri referens som hjälper dig att referera till programmet i Configuration Manager-konsolen.  

    > [!NOTE]  
    >  En del programinformation kanske redan finns på den här sidan om den tidigare hämtades från programmets installationsfiler.  

10. Välj **Nästa**, granska programinformationen på sidan **Sammanfattning** och slutför sedan **guiden Skapa program**.  

11. Det nya programmet visas i noden **program** i Configuration Manager-konsolen.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>Steg 3: Skapa en distributionstyp för Mac-programmet  
 Använd följande procedur för att få hjälp att skapa en distributions typ för Mac-datorer som hanteras av Configuration Manager.  

> [!NOTE]  
>  Om du har importerat information om programmet automatiskt i **guiden Skapa program**, kanske en distributions typ för programmet redan har skapats.  

1.  Välj program **bibliotek** > **program hantering** > **program i**Configuration Manager-konsolen.  

3.  Välj ett program. På fliken **Start** går du till gruppen **program** och väljer **skapa distributions typ** för att skapa en ny distributions typ för det här programmet.  

    > [!NOTE]  
    >  Du kan också starta **guiden skapa distributions typ** från **guiden Skapa program** och från fliken **distributions typer** i dialog rutan<**Egenskaper** för *program namn\> * .  

4.  Välj **Mac OS X**i list rutan **typ** på sidan **Allmänt** i **guiden skapa distributions typ**.  

5.  I fältet **plats** anger \\ \\ du UNC-sökvägen i formuläret\> \\<Server<dela\> \\<filename\> till programmets installations fil (**. cmmac** -fil). Alternativt kan du välja **Bläddra** för att bläddra till och ange installations filens plats.  

    > [!NOTE]  
    >  Du måste ha åtkomst till den UNC-sökväg som innehåller programmet.  

6.  Välj **Nästa**.  

7.  På sidan **Importera information** i **guiden Skapa distributionstyp**granskar du den information som importerades. Om det behövs väljer du **föregående** för att gå tillbaka och korrigera eventuella fel. Fortsätt genom att välja **Nästa** .  

8.  På sidan **Allmän information** i **guiden Skapa distributionstyp**anger du information om programmet, som t.ex. programnamn, kommentarer samt de språk som distributionstypen är tillgänglig på.  

    > [!NOTE]  
    >  En del av distributions typs informationen kanske redan finns på den här sidan om den tidigare hämtades från programmets installationsfiler.  

9. Välj **Nästa**.  

10. På sidan **krav** i **guiden skapa distributions typ**kan du ange de villkor som måste vara uppfyllda innan distributions typen kan installeras på Mac-datorer.  

11. Välj **Lägg till** för att öppna dialog rutan **Skapa krav** och Lägg till ett nytt krav.  

    > [!NOTE]  
    >  Du kan även lägga till nya krav på fliken **Krav** i dialogrutan *<namn på distributionstyp\>* **Egenskaper**.  

12. I listrutan **Kategori** väljer du att det här kravet gäller för en enhet.  

13. I list rutan **villkor** väljer du det villkor som du vill använda för att utvärdera om Mac-datorn uppfyller installations kraven. Innehållet i listan varierar beroende på vilken kategori du väljer.  

14. I list rutan **operator** väljer du den operator som du vill använda för att jämföra det valda villkoret med det angivna värdet för att utvärdera om användaren eller enheten uppfyller installations kraven. Tillgängliga operatörer varierar beroende på vilket villkor som valts.  

15. I fältet **värde** anger du de värden som ska användas med det valda villkoret och den valda operatorn för att bedöma om användaren eller enheten uppfyller installations kravet. Tillgängliga värden varierar beroende på vilket villkor och vilken operatör du väljer.

16. Välj **OK** för att spara krav regeln och stänga dialog rutan **Skapa krav** .  

17. På sidan **krav** i **guiden skapa distributions typ**väljer du **Nästa**.  

18. På sidan **Sammanfattning** i **guiden Skapa distributionstyp**granskar du de åtgärder som guiden ska genomföra.  Om det behövs väljer du **föregående** för att gå tillbaka och ändra inställningarna för distributions typen. Välj **Nästa** för att skapa distributions typen.  

19. När **förlopps** sidan har slutförts granskar du de åtgärder som har vidtagits och väljer sedan **Stäng** för att slutföra **guiden skapa distributions typ**.  

20. Om du startade guiden från **guiden Skapa program**kommer du tillbaka till sidan **distributions typer** .  

###  <a name="deploy-the-mac-application"></a>Distribuera Mac-programmet  
 Stegen för att distribuera ett program till Mac-datorer är samma som stegen för att distribuera ett program till Windows-datorer, förutom följande skillnader:  

-   Distribution av program till användare stöds inte.  

-   Distributioner som har syftet **Tillgänglig** stöds inte.  

-   Alternativet för **att distribuera program varan till användarens primära enhet** på sidan **distributions inställningar** i **guiden distribuera program vara** stöds inte.  

-   Eftersom Mac-datorer inte stöder Software Center ignoreras inställningen **användar meddelanden** på sidan **användar upplevelse** i **guiden distribuera program vara** .  

-   Möjligheten att skicka aktiveringspaket när du distribuerar programvara stöds inte för Mac-datorer.  

> [!NOTE]  
>  Du kan bygga en samling som bara innehåller Mac-datorer. Det gör du genom att skapa en samling som använder en frågeregel och använda exemplet WQL-fråga i avsnittet [så här skapar du frågor](../../core/servers/manage/create-queries.md) .  

 Mer information finns i [distribuera program](../../apps/deploy-use/deploy-applications.md).  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>Steg 5: övervaka distributionen av Mac-programmet  
 Du kan använda samma process för att övervaka program distributioner till Mac-datorer på samma sätt som du övervakar program distributioner till Windows-datorer.  

 Mer information finns i [övervaka program](../deploy-use/monitor-applications-from-the-console.md).  
