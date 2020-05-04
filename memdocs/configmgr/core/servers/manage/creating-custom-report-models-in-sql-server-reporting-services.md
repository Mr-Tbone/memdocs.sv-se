---
title: Skapa anpassade rapporter
titleSuffix: Configuration Manager
description: Definiera rapport modeller för att uppfylla dina affärs behov och distribuera sedan rapport modellerna till Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 590f3adec168fe6d7f4718505bd6f7d6b9f7c25f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712535"
---
# <a name="creating-custom-report-models-for-configuration-manager-in-sql-server-reporting-services"></a>Skapa anpassade rapport modeller för Configuration Manager i SQL Server Reporting Services

*Gäller för: Configuration Manager (aktuell gren)*

Exempel rapport modeller ingår i Configuration Manager, men du kan även definiera rapport modeller för att uppfylla dina egna affärs behov, och sedan distribuera rapport modellen till Configuration Manager som ska användas när du skapar nya modellbaserade rapporter. De följande tabellerna visar hur du skapar och distribuerar en enkel rapportmodell.  

> [!NOTE]  
>  Se avsnittet [Steps for Creating an Advanced Report Model in SQL Server Reporting Services](#AdvancedReportModel) i den här artikeln om du vill veta hur du skapar en mer avancerad rapportmodell.  

|Steg|Beskrivning|Mer information|  
|----------|-----------------|----------------------|  
|Verifiera att SQL Server Business Intelligence Development Studio är installerat|Rapportmodeller designas och skapas med hjälp av SQL Server Business Intelligence Development Studio. Kontrollera att SQL Server Business Intelligence Development Studio är installerat på datorn där du skapar den anpassade rapportmodellen.|Mer information om SQL Server Business Intelligence Development Studio finns i dokumentationen till SQL Server 2008.|  
|Skapa ett rapportmodellsprojekt|Ett rapportmodellsprojekt innehåller definitionen av datakällan (en .ds-fil), definitionen av en datakällsvy (en .dsv-fil) och rapportmodellen (en .smdl-fil).|Mer information finns i avsnittet [To create the report model project](#BKMK_CreateReportModelProject) i den här artikeln.|  
|Definiera en datakälla för en rapportmodell|När du har skapet ett rapportmodellsprojekt måste du definiera en datakälla från vilket data hämtas. Detta är vanligt vis den Configuration Manager plats databasen.|Mer information finns i avsnittet [To define the data source for the report model](#BKMK_DefineReportModelDataSource) i den här artikeln.|  
|Definiera en datakällsvy för en rapportmodell|När du har definierat datakällorna som du använder i rapportmodellsprojektet är nästa steg att definiera en datakällsvy för projektet. En datakällsvy är en logisk datamodell som bygger på en eller flera datakällor. Datakällsvyer kapslar in åtkomsten till de fysiska objekten, t.ex. tabeller och vyer, som ligger i de bakomliggande datakällorna. SQL Server Reporting Services genererar rapportmodellen från datakällsvyn.<br /><br /> Datakällsvyer underlättar designen av modellen genom att du får tillgång till en lättanvänd representation av alla data som du har angett. Utan att ändra den bakomliggande datakällan kan du ändra namn på tabeller och fält och samla fält och härledda tabeller i en datakällsvy. Om modellen ska bli effektiv ska du bara lägga till de tabeller som du avser att använda i datakällsvyn.|Mer information finns i avsnittet [To define the data source view for the report model](#BKMK_DefineReportModelDataSourceView) i den här artikeln.|  
|Skapa en rapportmodell|En rapportmodell är ett skikt som ligger ovanpå en databas som identifierar affärsobjekt, fält och roller. När den har publicerats kan användare av Report Builder med modellers hjälp ta fram rapporter utan att behöva vara bekanta med databasstrukturer eller förstå och skriva frågor. Modellerna består av uppsättningar av relaterade rapportobjekt som grupperas under ett eget namn, med fördefinierade relationer mellan affärsobjekten och med fördefinierade beräkningar. Modeller definieras med ett XML-språk som kallas SDML (Semantic Model Definition Language). Filnamnstillägget för rapportmodellsfiler är .smdl.|Mer information finns i avsnittet [To create the report model](#BKMK_CreateReportModel) i den här artikeln.|  
|Publicera en rapportmodell|Om du ska kunna tillverka en rapport med hjälp av modellen som du nyss har skapat, måste du publicera den på en rapportserver. Datakällan och datakällsvyn inkluderas i modellen när den publiceras.|Mer information finns i avsnittet [To publish the report model for use in SQL Server Reporting Services](#BKMK_PublishReportModel) i den här artikeln.|  
|Distribuera rapport modellen till Configuration Manager|Innan du kan använda en anpassad rapport modell i **guiden Skapa rapport** för att skapa en modell baserad rapport, måste du distribuera rapport modellen till Configuration Manager.|Mer information finns i avsnittet [To deploy the custom report model to Configuration Manager](#BKMK_DeployReportModel) i den här artikeln.|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>Steg för hur du skapar en enkel rapportmodell i SQL Server Reporting Services  
 Du kan använda följande procedurer för att skapa en enkel rapport modell som användarna på din plats kan använda för att skapa specifika modellbaserade rapporter som baseras på data i en enskild vy av den Configuration Manager databasen. Du skapar en rapportmodell som presenterar information om klientdatorerna på platsen för rapportens upphovsman. Den här informationen hämtas från vyn **v_R_System** i Configuration Manager-databasen.  

 På den dator där du utför åtgärderna ska du kontrollera att SQL Server Business Intelligence Development Studio är installerat och att datorn är nätverksansluten till Reporting Services-platsservern. Mer detaljerad information om SQL Server Business Intelligence Development Studio finns i dokumentationen till SQL Server 2008.  

###  <a name="to-create-the-report-model-project"></a><a name="BKMK_CreateReportModelProject"></a>Skapa rapport modell projektet  

1.  Klicka på **Start**på datorn och välj **Microsoft SQL Server 2008**. Klicka sedan på **SQL Server Business Intelligence Development Studio**.  

2.  När **SQL Server Business Intelligence Development Studio** har öppnats i Microsoft Visual Studio klickar du på **Arkiv**, **Nytt**och sedan **Projekt**.  

3.  Välj **Rapportmodellprojekt** i listan **Mallar** i dialogrutan **Nytt projekt** .  

4.  Ange ett namn för rapportmodellen i rutan **Namn** . I det här exemplet skriver du **Enkel_modell**.  

5.  Skapa rapportmodellprojektet genom att klicka på **OK**.  

6.  Lösningen **Simple_Model** visas i **Solution Explorer**.  

    > [!NOTE]  
    >  Om inte rutan **Solution Explorer** visas klickar du på **Visa**, följt av **Solution Explorer**.  

###  <a name="to-define-the-data-source-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSource"></a>Definiera data källan för rapport modellen  

1.  I **Solution Explorer** -rutan i **SQL Server Business Intelligence Development Studio**högerklickar du på **Datakällor** och väljer **Lägg till ny datakälla**.  

2.  Klicka på **Nästa** på sidan **Välkommen till guiden Datakälla**.  

3.  På sidan **Välj hur anslutningen ska definieras** kontrollerar du att alternativet **Skapa en datakälla baserat på en befintlig eller ny anslutning** har valts och klickar sedan på **Ny**.  

4.  I dialogrutan **Anslutningshanteraren** anger du följande anslutningsegenskaper för datakällan:  

    -   **Server namn**: Ange namnet på Configuration Manager plats databas servern eller Välj den i listan. Om du arbetar med en namngiven instans i stället för standard instansen skriver &lt; *databas server*>\\&lt;*instans namn*>.  

    -   Välj **Använd Windows-autentisering**.  

    -   I listan **Välj eller ange ett databas namn** väljer du namnet på din Configuration Manager plats databas.  

5.  Kontrollera att databasanslutningen fungerar genom att klicka på **Testa anslutning**.  

6.  Om anslutningen fungerar stänger du dialogrutan **Anslutningshanteraren** genom att klicka på **OK** . Om anslutningen inte fungerar kontrollerar du att all information har angetts korrekt. Klicka sedan på **Testa anslutning** igen.  

7.  Kontrollera att **Skapa en ny datakälla baserat på en befintlig eller ny anslutning** är markerat på sidan **Välj hur anslutningen ska anges** , verifiera att datakällan som du nyss angav är markerad i **Dataanslutningar**och klicka sedan på **Nästa**.  

8.  Ange datakällans namn i **Namn på datakälla**och klicka sedan på **Slutför**. I det här exemplet skriver du **Enkel_modell**.  

9. Datakällan **Simple_Model.ds** visas nu i **Solution Explorer** under noden **Datakällor** .  

    > [!NOTE]  
    >  Om du vill redigera en befintlig datakällas egenskaper dubbelklickar du på datakällan i mappen **Datakällor** på **Solution Explorer** -panelen, så visas datakällans egenskaper i Data Source Designer.  

###  <a name="to-define-the-data-source-view-for-the-report-model"></a><a name="BKMK_DefineReportModelDataSourceView"></a>Definiera datakällvyn för rapport modellen  

1.  Högerklicka på **Datakällvyer**i **Solution Explorer** och välj **Lägg till ny datakällvy**.  

2.  Klicka på **Nästa** på sidan **Välkommen till guiden Datakällvy**. Sidan **Välj en datakälla** visas.  

3.  Kontrollera att datakällan **Simple_Model** är vald i fönstret **Relational data sources** och klicka sedan på **Next**.  

4.  På sidan **Markera tabeller och vyer** väljer du att använda följande vy i listan **Tillgängliga objekt** i rapportmodellen: **v_R_System (dbo)**.  

    > [!TIP]  
    >  Du kan sortera objekten i alfabetisk ordning genom att klicka på rubriken **Namn** överst i listan **Tillgängliga objekt** , så blir det lättare att hitta objektet.  

5.  När du har valt vyn klickar **>** du på för att överföra objektet till listan **inkluderade objekt** .  

6.  Godkänn standardvalen om sidan **Name Matching** visas och klicka på **Next**.  

7.  När du har valt de objekt du vill ha klickar du på **Next**, och sedan anger du ett namn på datakällsvyn. I det här exemplet skriver du **Enkel_modell**.  

8.  Klicka på **Slutför**. Datakällsvyn **Simple_Model.dsv** visas i mappen **Data Source Views** i **Solution Explorer**.  

###  <a name="to-create-the-report-model"></a><a name="BKMK_CreateReportModel"></a>Skapa rapport modellen  

1.  Högerklicka på **Rapportmodeller**i **Solution Explorer** och välj **Lägg till ny rapportmodell**.  

2.  Klicka på **Nästa** på sidan **Välkommen till guiden Rapportmodell**.  

3.  Välj datakällsvyn på listan **Available data source views** på sidan **Select Data Source Views** och klicka sedan på **Next**. I det här exemplet skriver du **Enkel_modell.dsv**.  

4.  Godkänn standardvärdena på sidan **Select report model generation rules** och klicka sedan på **Next**.  

5.  På sidan **Samla in modellstatistik** kontrollerar du att **Uppdatera modellstatistik före generering** har valts och sedan klickar du på **Nästa**.  

6.  På sidan **Guiden slutförs** anger du ett namn för rapportmodellen. Kontrollera i det här exemplet att det står **Simple_Model** .  

7.  Slutför guiden och skapa rapportmodellen genom att klicka på **Kör**.  

8.  Slutför guiden genom att klicka på **Slutför**. Rapportmodellen visas i designfönstret.  

###  <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a><a name="BKMK_PublishReportModel"></a> To publish the report model for use in SQL Server Reporting Services  

1.  Högerklicka på rapportmodellen och välj **Deploy**i **Solution Explorer**. Rapportmodellen i det här exemplet är **Simple_Model.smdl**.  

2.  Kontrollera distributionsstatusen längst ned till vänster i fönstret **SQL Server Business Intelligence Development Studio** . Om distributionen har slutförts visas **Distributionen slutfördes** . Om distributionen inte har slutförts visas orsaken till felet i fönstret **Utdata** . Den nya rapportmodellen är nu tillgänglig på SQL Server Reporting Services-webbplatsen.  

3.  Klicka på **Arkiv**och sedan på **Spara alla**innan du stänger **SQL Server Business Intelligence Development Studio**.  

###  <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a><a name="BKMK_DeployReportModel"></a>Distribuera den anpassade rapport modellen till Configuration Manager  

1. Leta reda på den mapp där du sparade det skapade rapportmodellprojektet. Till exempel%*USERPROFILE*% \ Documents\Visual Studio 2008 \\\*&lt;Projects projekt namn\>.*  

2. Kopiera följande filer från rapportmodellprojektmappen till en tillfällig mapp på datorn:  

   -   *Modell namn\> &lt;* **.dsv**  

   -   *Modell namn\> &lt;* **.smdl**  

3. Öppna ovanstående filer i en textredigerare, till exempel Notepad.  

4. Leta upp den första raden i filen i filen _ &lt;Model name\>_**. DSV**och Läs följande:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Ändra raden till följande text:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`  

5. Kopiera allt filinnehåll till Urklipp i Windows.  

6. Stäng fil _ &lt;modellens namn\>_**. DSV**.  

7. Leta upp de tre sista raderna i filen i fil _ &lt;modell namnet\>_**. SMDL**, som visas på följande sätt:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Klistra in innehållet i fil _ &lt;modell namnet\>_**. DSV** direkt före den sista raden i filen (**&lt;SemanticModel\>**).  

9. Spara och Stäng fil _ &lt;modell namnet\>_**. SMDL**.  

10. Kopiera fil _ &lt;modell\>namnet_**. SMDL** till mappen *% ProgramFiles%* \Microsoft Configuration Manager \AdminConsole\XmlStorage\Other på plats servern för Configuration Manager.  

    > [!IMPORTANT]  
    >  När du har kopierat rapport modell filen till Configuration Manager plats Server måste du avsluta och starta om Configuration Manager-konsolen innan du kan använda rapport modellen i **guiden Skapa rapport**.  

##  <a name="steps-for-creating-an-advanced-report-model-in-sql-server-reporting-services"></a><a name="AdvancedReportModel"></a> Steps for Creating an Advanced Report Model in SQL Server Reporting Services  
 Du kan använda följande procedurer för att skapa en avancerad rapport modell som användarna på din plats kan använda för att skapa specifika modellbaserade rapporter som baseras på data i flera vyer av den Configuration Manager databasen. Du skapar en rapportmodell som presenterar information om klientdatorerna och operativsystemet som är installerat på dessa datorer för rapportens upphovsman. Den här informationen hämtas från följande vyer i Configuration Manager-databasen:  

- **V_R_System**: innehåller information om identifierade datorer och Configuration Manager klienten.  

- **V_GS_OPERATING_SYSTEM**: Innehåller information om det operativsystem som är installerat på klientdatorn.  

  Objekt som har valts i de föregående vyerna sammanställs till en lista, tilldelas lämpliga namn och visas sedan i Report Builder, där rapportförfattaren kan använda informationen i rapporter.  

  På den dator där du utför åtgärderna ska du kontrollera att SQL Server Business Intelligence Development Studio är installerat och att datorn är nätverksansluten till Reporting Services-platsservern. Mer information om SQL Server Business Intelligence Development Studio finns i SQL Server-dokumentationen.  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  Klicka på **Start**på datorn och välj **Microsoft SQL Server 2008**. Klicka sedan på **SQL Server Business Intelligence Development Studio**.  

2.  När **SQL Server Business Intelligence Development Studio** har öppnats i Microsoft Visual Studio klickar du på **Arkiv**, **Nytt**och sedan **Projekt**.  

3.  Välj **Rapportmodellprojekt** i listan **Mallar** i dialogrutan **Nytt projekt** .  

4.  Ange ett namn för rapportmodellen i rutan **Namn** . I det här exemplet skriver du **Avancerad_modell**.  

5.  Skapa rapportmodellprojektet genom att klicka på **OK**.  

6.  Lösningen **Avancerad_modell** visas i **Solution Explorer**.  

    > [!NOTE]  
    >  Om inte rutan **Solution Explorer** visas klickar du på **Visa**, följt av **Solution Explorer**.  

#### <a name="to-define-the-data-source-for-the-report-model"></a>To define the data source for the report model  

1.  I **Solution Explorer** -rutan i **SQL Server Business Intelligence Development Studio**högerklickar du på **Datakällor** och väljer **Lägg till ny datakälla**.  

2.  Klicka på **Nästa** på sidan **Välkommen till guiden Datakälla**.  

3.  På sidan **Välj hur anslutningen ska definieras** kontrollerar du att alternativet **Skapa en datakälla baserat på en befintlig eller ny anslutning** har valts och klickar sedan på **Ny**.  

4.  I dialogrutan **Anslutningshanteraren** anger du följande anslutningsegenskaper för datakällan:  

    -   **Server namn**: Ange namnet på Configuration Manager plats databas servern eller Välj den i listan. Om du arbetar med en namngiven instans i stället för standard instansen skriver &lt; *databas server*>\\&lt;*instans namn*>.  

    -   Välj **Använd Windows-autentisering**.  

    -   I listan **Välj eller ange ett databas namn** väljer du namnet på din Configuration Manager plats databas.  

5.  Kontrollera att databasanslutningen fungerar genom att klicka på **Testa anslutning**.  

6.  Om anslutningen fungerar stänger du dialogrutan **Anslutningshanteraren** genom att klicka på **OK** . Om anslutningen inte fungerar kontrollerar du att all information har angetts korrekt. Klicka sedan på **Testa anslutning** igen.  

7.  Kontrollera att alternativet **Skapa en datakälla baserat på en befintlig eller ny anslutning** har valts på sidan **Välj hur anslutningen ska definieras** , och kontrollera att den datakälla som du nyligen har angett är markerad i listrutan **Dataanslutningar** . Klicka sedan på **Nästa**.  

8.  I **Datakällans namn**anger du ett namn för datakällan och klickar sedan på **Slutför**. I det här exemplet skriver du **Avancerad_modell**.  

9. Datakällan **Avancerad_modell.ds** visas under noden **Datakällor** i **Solution Explorer** .  

    > [!NOTE]  
    >  Om du vill redigera en befintlig datakällas egenskaper dubbelklickar du på datakällan i mappen **Datakällor** på **Solution Explorer** -panelen, så visas datakällans egenskaper i Data Source Designer.  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>To define the data source view for the report model  

1. Högerklicka på **Datakällvyer**i **Solution Explorer** och välj **Lägg till ny datakällvy**.  

2. Klicka på **Nästa** på sidan **Välkommen till guiden Datakällvy**. Sidan **Välj en datakälla** visas.  

3. I fönstret **Relationsdatakällor** kontrollerar du att datakällan **Adancerad_modell** har valts och klickar sedan på **Nästa**.  

4. På sidan **Välj tabeller och vyer** i listan **Tillgängliga objekt** väljer du följande vyer som ska användas i rapportmodellen:  

   - **v_R_System (dbo)**  

   - **v_GS_OPERATING_SYSTEM (dbo)**  

     När du har valt varje vy **>** klickar du på för att överföra objektet till listan **inkluderade objekt** .  

   > [!TIP]  
   >  Du kan sortera objekten i alfabetisk ordning genom att klicka på rubriken **Namn** överst i listan **Tillgängliga objekt** , så blir det lättare att hitta objektet.  

5. Om dialogrutan **Namnmatchning** visas behåller du standardinställningarna och klickar sedan på **Nästa**.  

6. När du har valt de objekt som behövs klickar du på **Nästa**och anger sedan ett namn för datakällvyn. I det här exemplet skriver du **Avancerad_modell**.  

7. Klicka på **Slutför**. Datakällvyn **Avancerad_modell.dsv** visas i mappen **Datakällvyer** i **Solution Explorer**.  

#### <a name="to-define-relationships-in-the-data-source-view"></a>Definiera relationer i datakällvyn  

1.  Öppna Design-fönstret genom att dubbelklicka på **Avancerad_modell.dsv**i **Solution Explorer** .  

2.  Högerklicka på namnlisten i fönstret **v_R_System** och välj **Ersätt tabell**. Klicka sedan på **Med ny namngiven fråga**.  

3.  I dialogrutan **Skapa namngiven fråga** klickar du på **Lägg till tabell** -ikonen (vanligtvis den ikon som visas sista i menyfliksområdet).  

4.  Klicka på fliken **Vyer** i dialogrutan **Lägg till tabell** och välj **V_GS_OPERATING_SYSTEM** i listan. Klicka sedan på **Lägg till**.  

5.  Stäng dialogrutan **Lägg till tabell** genom att klicka på **Stäng** .  

6.  Ange följande information i dialogrutan **Skapa namngiven fråga** :  

    -   **Namn:** Ange ett namn för frågan. I det här exemplet skriver du **Avancerad_modell**.  

    -   **Beskrivning:** Ange en beskrivning av frågan. I det här exemplet skriver du **Exempel Reporting Services-rapportmodell**.  

7.  I fönstret **v_R_System** väljer du följande objekt i listan med objekt som ska visas i rapportmodellen:  

    -   **ResourceID**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  I rutan **v_GS_OPERATING_SYSTEM** väljer du följande objekt i listan med objekt som ska visas i rapportmodellen:  

    -   **ResourceID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. Om objekten i de olika vyerna ska ingå i en gemensam lista som visas för rapportförfattaren, måste du ange en relation mellan de två tabellerna eller vyerna. Det gör du genom att koppla ihop dem. Du kopplar ihop de två vyerna med hjälp av objektet **ResourceID**som visas i båda vyerna.  

10. I fönstret **v_R_System** klickar du på och håller in **ResourceID** -objektet och drar det till **ResourceID** -objektet i **v_GS_OPERATING_SYSTEMs** fönstret.  

11. Klicka på **OK.**  

12. Fönstret **Avancerad_modell** ersätter fönstret **v_R_System** och innehåller alla för rapportmodellen nödvändiga objekt från vyn **v_R_System** och vyn **v_GS_OPERATING_SYSTEM** . Nu kan du ta bort fönstret **v_GS_OPERATING_SYSTEM** från Data Source View Designer. Högerklicka på namnlisten i fönstret **v_GS_OPERATING_SYSTEM** och välj **Ta bort tabell från DSV**. Bekräfta borttagningen genom att klicka på **OK** i dialogrutan **Ta bort objekt** .  

13. Klicka på **Arkiv**och sedan på **Spara alla**.  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  Högerklicka på **Rapportmodeller**i **Solution Explorer** och välj **Lägg till ny rapportmodell**.  

2.  Klicka på **Nästa** på sidan **Välkommen till guiden Rapportmodell**.  

3.  På sidan **Välj datakällvy** väljer du datakällvyn i listan **Tillgängliga datakällvyer** och klickar sedan på **Nästa**. I det här exemplet skriver du **Enkel_modell.dsv**.  

4.  Behåll standardinställningarna på sidan **Välj regler för rapportmodellgenerering** och klicka på **Nästa**.  

5.  På sidan **Samla in modellstatistik** kontrollerar du att **Uppdatera modellstatistik före generering** har valts och sedan klickar du på **Nästa**.  

6.  På sidan **Guiden slutförs** anger du ett namn för rapportmodellen. I det här exemplet kontrollerar du att **Avancerad_modell** visas.  

7.  Slutför guiden och skapa rapportmodellen genom att klicka på **Kör**.  

8.  Slutför guiden genom att klicka på **Slutför**.  

9. Rapportmodellen visas i designfönstret.  

#### <a name="to-modify-object-names-in-the-report-model"></a>Ändra objektnamn i rapportmodellen  

1.  Högerklicka på en rapportmodell i **Solution Explorer**och välj alternativet **Vydesigner**. I det här exemplet väljer du **Avancerad_modell.smdl**.  

2.  Högerklicka på ett objektnamn i vydesignfönstret och välj **Byt namn**.  

3.  Ange ett nytt namn för det valda objektet och tryck sedan på Retur. Du kan t.ex. ändra objektnamnet till **CSD_Version_0** för att skapa **Windows Service Pack Version**.  

4.  När du är klar med att ändra objektnamn klickar du på **Arkiv**, följt av **Spara alla**.  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>To publish the report model for use in SQL Server Reporting Services  

1.  Högerklicka på **Advancerad_modell.smdl**i **Solution Explorer** och välj **Distribuera**.  

2.  Kontrollera distributionsstatusen längst ned till vänster i fönstret **SQL Server Business Intelligence Development Studio** . Om distributionen har slutförts visas **Distributionen slutfördes** . Om distributionen inte har slutförts visas orsaken till felet i fönstret **Utdata** . Den nya rapportmodellen är nu tillgänglig på SQL Server Reporting Services-webbplatsen.  

3.  Klicka på **Arkiv**och sedan på **Spara alla**innan du stänger **SQL Server Business Intelligence Development Studio**.  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>To deploy the custom report model to Configuration Manager  

1. Leta reda på den mapp där du sparade det skapade rapportmodellprojektet. Till exempel%*USERPROFILE*% \ Documents\Visual Studio 2008 \\\*&lt;Projects projekt namn\>.*  

2. Kopiera följande filer från rapportmodellprojektmappen till en tillfällig mapp på datorn:  

   -   *Modell namn\> &lt;* **.dsv**  

   -   *Modell namn\> &lt;* **.smdl**  

3. Öppna ovanstående filer i en textredigerare, till exempel Notepad.  

4. Leta upp den första raden i filen i filen _ &lt;Model name\>_**. DSV**och Läs följande:  

    `<DataSourceView xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`

    Ändra raden till följande text:  

    `<DataSourceView xmlns="<https://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView">`

5. Kopiera allt filinnehåll till Urklipp i Windows.  

6. Stäng fil _ &lt;modellens namn\>_**. DSV**.  

7. Leta upp de tre sista raderna i filen i fil _ &lt;modell namnet\>_**. SMDL**, som visas på följande sätt:  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Klistra in innehållet i fil _ &lt;modell namnet\>_**. DSV** direkt före den sista raden i filen (**&lt;SemanticModel\>**).  

9. Spara och Stäng fil _ &lt;modell namnet\>_**. SMDL**.  

10. Kopiera fil _ &lt;modell\>namnet_**. SMDL** till mappen *% ProgramFiles%* \Microsoft Configuration Manager\AdminConsole\XmlStorage\Other på Configuration Manager plats Server.  

    > [!IMPORTANT]  
    >  När du har kopierat rapport modell filen till Configuration Manager plats Server måste du avsluta och starta om Configuration Manager-konsolen innan du kan använda rapport modellen i **guiden Skapa rapport**.  
