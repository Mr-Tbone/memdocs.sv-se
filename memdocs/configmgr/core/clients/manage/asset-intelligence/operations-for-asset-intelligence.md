---
title: Använd Tillgångsinformation
titleSuffix: Configuration Manager
description: Utför vanliga Tillgångsinformation uppgifter i Configuration Manager.
ms.date: 08/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e8159bd9-5c2b-4d25-82f9-78fcfd732ba9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1e272e8e71ceaa15c712cb3a53d9db835747d327
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714173"
---
# <a name="how-to-use-asset-intelligence-in-configuration-manager"></a>Använda Tillgångsinformation i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller information som hjälper dig att hantera vanliga Tillgångsinformation uppgifter i Configuration Manager-hierarkin:  

##  <a name="view-asset-intelligence-information"></a><a name="BKMK_ViewInformation"></a> Visa information om Tillgångsinformation  
 Du kan visa information om Tillgångsinformation på startsidan för **Tillgångsinformation** och i tillgångsinformationsrapporter.  

###  <a name="asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Startsidan för Tillgångsinformation  
 Startsidan för **Tillgångsinformation** innehåller en instrumentpanel som sammanfattar kataloginformationen för Tillgångsinformation. På startsidan kan du visa information om katalogsynkronisering och inventerad programvarustatus. Startsidan för **Tillgångsinformation** är indelad i följande avsnitt:  

- **Katalogsynkronisering**: Innehåller information om huruvida Tillgångsinformation är aktiverat, aktuell status för platsen för synkronisering av tillgångsinformation, synkroniseringsschemat, huruvida kundlicensöversikten importeras, när statusen uppdaterades senast och tiden för nästa schemalagda uppdatering, samt antalet ändringar som gjorts efter installationen av platssystemet för en plats för synkronisering av tillgångsinformation.  

  > [!NOTE]  
  >  Katalogsynkroniseringsavsnittet på startsidan för **Tillgångsinformation** visas bara om en platssystemroll för en plats för synkronisering av tillgångsinformation har installerats.  

- **Inventerad programvarustatus**: Visar antalet och procentandelen inventerad programvara, programvarukategorier och programvarufamiljer som identifierats av Microsoft, som identifierats av en administratör, som väntar på onlineidentifiering eller som är oidentifierade och inte har väntande status. Informationen som visas i tabellformat anger antalet för var och en, och informationen i diagrammet visar procentandelen.  

  Följ stegen nedan om du vill visa tillgångsinformation på startsidan för **Tillgångsinformation** .  

##### <a name="to-view-asset-intelligence-information-on-the-asset-intelligence-home-page"></a>Så här visar du tillgångsinformation på startsidan för Tillgångsinformation  

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2.  Klicka på **Tillgångsinformation** på arbetsytan **Tillgångar och efterlevnad**. Tillgångsinformationsrapporterna visas.  

###  <a name="asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a>Tillgångsinformation rapporter  
 Det finns över 60 tillgångsinformationsrapporter med information som samlas in av Tillgångsinformation. Många av de här rapporterna länkar till mer specifika rapporter där du kan fråga efter allmän information och öka detaljnivån till mer utförlig information. Tillgångsinformation rapporter finns i Configuration Manager-konsolen på arbets ytan **övervakning** under noden **rapportering** . Rapporterna innehåller information om maskinvara, licenshantering och programvara. Mer information om rapporter i Configuration Manager finns i [Introduktion till rapportering](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  Antalet installerade program och licenser som rapporteras i tillgångsinformationsrapporterna kan skilja sig från de verkliga antal som används i miljön. Detta beror på komplexa beroenden och begränsningar i inventeringen av programvarulicenser för program som är installerade i företagsmiljöer. Tillgångsinformationsrapporterna bör inte användas som den enda källan för att fastställa korrekt antal köpta programvarulicenser.  

 Följ stegen nedan om du vill visa tillgångsinformation med hjälp av tillgångsinformationsrapporter.  

##### <a name="to-view-collected-asset-intelligence-information-by-using-asset-intelligence-reports"></a>Så här visar du insamlad tillgångsinformation med hjälp av tillgångsinformationsrapporter  

1.  Klicka på **övervakning**i Configuration Manager-konsolen.  

2.  Expandera **Rapportering** på arbetsytan **Övervakning**, expandera **Rapporter**och klicka på **Tillgångsinformation**. Tillgångsinformationsrapporterna visas.  

    > [!WARNING]  
    >  Om det inte finns några rapportmappar under noden **Rapporter** kontrollerar du att du har konfigurerat rapportering. Mer information finns i [Configuring repor ting](../../../../core/servers/manage/configuring-reporting.md).  

3.  Markera den tillgångsinformationsrapport dom du vill köra och klicka sedan på **Kör** i gruppen **Rapporteringsgrupp** på fliken **Start**.  

##  <a name="synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_SynchronizeTheCatalog"></a>Synkronisera Tillgångsinformations katalogen  
 Du kan synkronisera den lokala tillgångsinformationskatalogen med System Center Online för att hämta den senaste kategoriseringen av programvarutitlar. När du begär katalogsynkronisering manuellt med System Center Online kan det ta 15 minuter eller längre att slutföra synkroniseringen med System Center Online. Configuration Manager uppdaterar inställningen **senaste lyckade uppdatering** på Start sidan för **tillgångsinformation** med den aktuella tiden när synkroniseringen har slutförts.  

> [!NOTE]  
>  Först måste du installera en platssystemroll för platsen för synkronisering av tillgångsinformation genom att följa motsvarande anvisningar. Information om hur du installerar en Tillgångsinformation plats för synkronisering finns i [konfigurera tillgångsinformation](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Skapa ett synkroniseringsschema för tillgångsinformationskatalogen genom att följa stegen nedan.  

#### <a name="to-create-a-synchronization-schedule-for-the-asset-intelligence-catalog"></a>Så här skapar du ett synkroniseringsschema för tillgångsinformationskatalogen  

1. Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2. Klicka på **Tillgångsinformation** på arbetsytan **Tillgångar och efterlevnad**.  

3. Gå till gruppen **Skapa** på fliken **Start** , klicka på **Synkronisera**och sedan på **Schemalägg synkronisering**.  

4. Välj **Aktivera synkronisering enligt schema** i dialogrutan **Schema för synkroniseringspunkt för tillgångsinformation**och konfigurera ett enkelt eller anpassat schema.  

5. Spara ändringarna genom att klicka på **OK**.  

   > [!NOTE]  
   >  Information om synkroniseringsschemat, inklusive nästa schemalagda synkronisering, finns under noden **Tillgångsinformation** på arbetsytan **Tillgångar och efterlevnad** på den översta nivån i hierarkin.  

   Följ stegen nedan om du vill synkronisera tillgångsinformationskatalogen manuellt.  

> [!WARNING]  
>  System Center Online accepterar bara en manuell synkroniseringsbegäran under en 12-timmarsperiod.  

###  <a name="to-manually-synchronize-the-asset-intelligence-catalog"></a><a name="BKMK_ManuallySynchronizeCatalog"></a> Så här synkroniserar du tillgångsinformationskatalogen manuellt  

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2.  Klicka på **Tillgångsinformation** på arbetsytan **Tillgångar och efterlevnad**.  

3.  Gå till gruppen **Skapa** på fliken **Start** , klicka på **Synkronisera**, klicka på **Synkronisera tillgångsinformationskatalog**och sedan på **OK**.  

##  <a name="customize-the-asset-intelligence-catalog"></a><a name="BKMK_CustomizeCatalog"></a>Anpassa Tillgångsinformations katalogen  
 Information om kategoriseringen av tillgångsinformationskatalogen som fås från System Center Online lagras i platsdatabasen med läsbehörighet och kan inte ändras eller tas bort. Du kan dock skapa, ändra och ta bort anpassad kataloginformation om programvarukategorier, programvarufamiljer, programvaruetiketter och maskinvarukrav. Sedan kan du använda anpassade kategoriseringsdata i stället för informationen från System Center Online för befintlig eller användardefinierad information om programvarutitlar. När du ändrar eller lägger till kategoriseringsinformation betraktas kataloginformationen som användardefinierad. Användardefinierad kategoriseringsinformation lagras i andra databastabeller än validerad kataloginformation.  

###  <a name="software-categories"></a><a name="BKMK_SoftwareCategories"></a>Program varu kategorier  
 Programvarukategorier i Tillgångsinformation används för att göra en bred kategorisering av inventerade programvarutitlar och fungerar också som grupperingar på hög nivå av mer specifika programvarufamiljer. En programvarukategori kan till exempel vara elbolag, och en programvarufamilj i den programvarukategorin kan vara olja och gas eller hydroelektrisk. Många programvarukategorier är fördefinierade i tillgångsinformationskatalogen och fler användardefinierade kategorier kan skapas för att definiera inventerad programvara ytterligare. Valideringstillståndet för alla fördefinierade programvarukategorier är alltid **Verifierad**, medan anpassad information om programvarukategorier som läggs till i tillgångsinformationskatalogen är **Användardefinierad**.  

 Följ stegen nedan om du vill skapa en användardefinierad programvarukategori.  

##### <a name="to-create-a-user-defined-software-category"></a>Så här skapar du en användardefinierad programvarukategori  

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2.  Klicka på **Tillgångsinformation** på arbetsytan **Tillgångar och efterlevnad**och klicka sedan på **Katalog**.  

3.  Klicka på **Skapa programvarukategori** i gruppen **Skapa** på fliken **Start**.  

4.  Ange ett namn för den nya programvarukategorin och, om du vill, en beskrivning på sidan **Allmänt** .  

    > [!NOTE]  
    >  Valideringstillståndet för alla nya anpassade programvarukategorier är alltid **Användardefinierad**.  

     Klicka på **Nästa**.  

5.  Granska inställningarna på sidan **Sammanfattning** och klicka sedan på **Nästa**.  

6.  På sidan **Slutförande** klickar du på **Stäng** och stänger guiden.  

###  <a name="software-families"></a><a name="BKMK_SoftwareFamilies"></a>Program varu familjer  
 Programvarufamiljer i Tillgångsinformation används för att ytterligare definiera inventerade programvarutitlar i programvarukategorier. En programvarukategori kan till exempel vara elbolag, och en programvarufamilj i den programvarukategorin kan vara olja och gas eller hydroelektrisk. Många programvarufamiljer är fördefinierade i tillgångsinformationskatalogen och fler användardefinierade familjer kan skapas för att definiera inventerad programvara. Valideringstillståndet för alla fördefinierade programvarufamiljer är alltid **Verifierad**, medan anpassad information om programvarufamiljer som läggs till i tillgångsinformationskatalogen är **Användardefinierad**.  

 Följ stegen nedan om du vill skapa en användardefinierad programvarufamilj.  

##### <a name="to-create-a-user-defined-software-family"></a>Så här skapar du en användardefinierad programvarufamilj  

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2.  Klicka på **Tillgångsinformation** på arbetsytan **Tillgångar och efterlevnad**och klicka sedan på **Katalog**.  

3.  Klicka på **Skapa programvarufamilj** i gruppen **Skapa** på fliken **Start**.  

4.  Ange ett namn för den nya programvarufamiljen och, om du vill, en beskrivning på sidan **Allmänt** .  

    > [!NOTE]  
    >  Valideringstillståndet för alla nya anpassade programvarufamiljer är alltid **Användardefinierad**.  

5.  Granska inställningarna på sidan **Sammanfattning** och klicka sedan på **Nästa**.  

6.  På sidan **Slutförande** klickar du på **Stäng** och stänger guiden.  

###  <a name="software-labels"></a><a name="BKMK_SoftwareLabels"></a>Program varu etiketter  
 Med anpassade programvaruetiketter i Tillgångsinformation kan du skapa filter som du kan använda för att gruppera programvarutitlar och visa dem med hjälp av tillgångsinformationsrapporter. Du kan till exempel skapa programvaruetiketten Shareware, associera den med ett antal program och sedan köra en rapport som visar alla titlar med programvaruetiketten Shareware. Valideringstillståndet är **Användardefinierad** för alla anpassade programvaruetiketter som du lägger till i tillgångsinformationskatalogen.  

 Följ stegen nedan om du vill skapa en användardefinierad anpassad etikett.  

##### <a name="to-create-a-user-defined-software-label"></a>Så här skapar du en användardefinierad programvaruetikett  

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2.  Klicka på **Tillgångsinformation** på arbetsytan **Tillgångar och efterlevnad**och klicka sedan på **Katalog**.  

3.  Klicka på **Skapa programvaruetikett** i gruppen **Skapa** på fliken **Start**.  

4.  Ange ett namn för den nya programvarufamiljen och, om du vill, en beskrivning på sidan **Allmänt** .  

    > [!NOTE]  
    >  Valideringstillståndet för alla nya anpassade programvaruetiketter är alltid **Användardefinierad**.  

5.  Granska inställningarna på sidan **Sammanfattning** och klicka sedan på **Nästa**.  

6.  På sidan **Slutförande** klickar du på **Stäng** och stänger guiden.  

###  <a name="hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a>Maskin varu krav  
 Informationen om maskinvarukrav hjälper dig att kontrollera att relevanta datorer uppfyller maskinvarukraven för programvarutitlarna innan programvaran distribueras till dem. Många maskinvarukrav är fördefinierade i tillgångsinformationskatalogen och du kan skapa ny användardefinierad information om maskinvarukrav för att uppfylla anpassade krav. Valideringstillståndet för alla fördefinierade maskinvarukrav är alltid **Verifierad**, medan användardefinierad information om maskinvarukrav som läggs till i tillgångsinformationskatalogen är **Användardefinierad**.  

> [!IMPORTANT]  
>  Maskin varu kraven som visas i Configuration Manager-konsolen hämtas från Tillgångsinformation-katalogen på den lokala datorn och baseras inte på information om inventerade program varu titlar från System Center 2012 Configuration Manager-klienter. Information om maskinvarukraven uppdateras inte som en del av synkroniseringsprocessen med System Center Online. Du kan skapa användardefinierade maskinvarukrav för inventerad programvara som saknar associerade maskinvarukrav.  

 Följ stegen nedan om du vill skapa användardefinierade maskinvarukrav.  

##### <a name="to-create-a-user-defined-hardware-requirements"></a>Så här skapar du användardefinierade maskinvarukrav  

1. Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2. Klicka på **Tillgångsinformation** på arbetsytan **Tillgångar och efterlevnad**och klicka sedan på **Maskinvarukrav**.  

3. Klicka på **Skapa maskinvarukrav** i gruppen **Skapa** på fliken **Start**.  

4. Ange följande information på sidan **Allmänt** :  

   1. **Programvarunamn**: Anger programvarutiteln som maskinvarukraven associeras med. Programvarutiteln får inte redan finnas i tillgångsinformationskatalogen.  

   2. **Valideringstillstånd**: Visar valideringstillståndet som **Användardefinierad** för maskinvarukraven. Du kan inte ändra den här inställningen.  

   3. **Lägsta processorkrav (MHz)**: Anger den lägsta processorhastigheten i megahertz (MHz) som programvarutiteln kräver.  

   4. **Minsta RAM (kB)**: Anger den minsta mängden RAM-minne i kilobyte (kB) som programvarutiteln kräver.  

   5. **Minsta diskutrymme (kB)**: Anger den minsta mängden ledigt diskutrymme i kB som programvarutiteln kräver.  

   6. **Minsta diskstorlek (kB)**: Anger den minsta hårddiskstorleken i kB som programvarutiteln kräver.  

      Klicka på **Nästa**.  

5. Granska inställningarna på sidan **Sammanfattning** och klicka sedan på **Nästa**.  

6. På sidan **Slutförande** klickar du på **Stäng** och stänger guiden.  

###  <a name="modify-categorization-information-for-inventoried-software"></a><a name="BKMK_ModifyCategorization"></a>Ändra kategoriserings information för Inventerad program vara  
 Fördefinierad programvara i tillgångsinformationskatalogen är konfigurerad med specifik kategoriseringsinformation, till exempel produktnamn, leverantör, programvarukategori och programvarufamilj. Om den fördefinierade kategoriseringsinformationen inte uppfyller dina krav kan du ändra informationen i egenskaperna för programvarutiteln. När du ändrar kategoriseringsinformation för fördefinierad programvara ändras valideringstillståndet för programvaran från **Verifierad** till **Användardefinierad**.  

> [!IMPORTANT]  
>  Kategoriseringsinformationen kan bara ändras på platsen på den högsta nivån.  

 Följ stegen nedan om du vill ändra kategoriseringsinformationen för inventerad programvara.  

##### <a name="to-modify-the-categorizations-for-software-titles"></a>Så här ändrar du kategoriseringarna för programvarutitlar  

1. Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2. Klicka på **Tillgångsinformation** på arbetsytan **Tillgångar och efterlevnad**och klicka sedan på **Inventerad programvara**.  

3. Välj en eller flera programvarutitlar som du vill ändra kategoriseringar för.  

4. På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  

5. Du kan ändra följande kategoriseringsinformation på fliken **Allmänt** :  

   -   **Produktnamn**: Anger namnet på den inventerade programvarutiteln.  

   -   **Leverantör**: Anger namnet på leverantören som utvecklat den inventerade programvarutiteln.  

   -   **Kategori**: Anger den programvarukategori som för närvarande är kopplad till den inventerade programvarutiteln.  

   -   **Familj**: Anger den programvarufamilj som för närvarande är kopplad till den inventerade programvarutiteln.  

6. Spara ändringarna genom att klicka på **OK**.  

   Följ stegen nedan om du vill återställa programvara till den ursprungliga kategoriseringsinformationen.  

### <a name="revert-categorization-information-to-original-settings-for-software"></a>Återställa kategoriseringsinformation till ursprungliga inställningar för programvara  
 Configuration Manager lagrar kategoriserings information som erhållits från System Center Online i databasen. Informationen kan inte tas bort. När informationen har ändrats kan du återställa kategoriseringsinformationen till kategoriseringen i System Center Online. Inventerad programvara som inte finns i tillgångsinformationskatalogen kan också återställas till de ursprungliga inställningarna.  

 Följ stegen nedan om du vill återställa kategoriseringsinformationen till de ursprungliga inställningarna.  

##### <a name="to-revert-categorization-information-to-original-settings"></a>Så här återställer du kategoriseringsinformation till ursprungsinställningarna  

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2.  Klicka på **Tillgångsinformation** på arbetsytan **Tillgångar och efterlevnad**och klicka sedan på **Inventerad programvara**.  

3.  Välj en eller flera programvarutitlar som du vill återställa till de ursprungliga inställningarna. Det går bara att återställa programvara som har tillståndet **Användardefinierad** .  

    > [!TIP]  
    >  Klicka på kolumnen **Tillstånd** om du vill sortera efter valideringstillstånd. Genom att sortera kan du visa all programvara efter valideringstillstånd och snabbt välja flera objekt som du vill återställa till ursprungsinställningarna.  

4.  Klicka på **Återställ** i gruppen **Produkt** på fliken **Start**.  

5.  Klicka på **Ja** om du vill återställa programvaran till den ursprungliga kategoriseringsinformationen.  

6.  Om du återställer kategoriseringsinformation för programvara som finns i tillgångsinformationskatalogen ändras valideringstillståndet från **Användardefinierad** till **Verifierad**. Om du återställer programvara som inte finns i katalogen ändras valideringstillståndet från **Användardefinierad** till **Ej kategoriserade**.  

##  <a name="request-a-catalog-update-for-uncategorized-software-titles"></a><a name="BKMK_RequestCatalogUpdate"></a>Begär en katalog uppdatering för Okategoriserade program varu titlar  
 Information om okategoriserade programvarutitlar kan skickas till System Center Online för undersökning och kategorisering. Om en okategoriserad programvarutitel skickas, och om det finns minst fyra kategoriseringsförfrågningar från kunder om samma programvarutitel, så identifieras, kategoriseras och tillgängliggörs kategoriseringsinformationen för programvarutiteln för alla kunder som använder tjänsten System Center Online. Microsoft ger högst prioritet till de programvarutitlar som har flest kategoriseringsförfrågningar. Det är inte troligt att anpassade program och affärsprogram tilldelas en kategori, och som bästa praxis bör du inte skicka dessa programvarutitlar till Microsoft för kategorisering.  

 När information om programvarutitlar skickas till System Center Online för kategorisering gäller följande villkor:  

-   Endast grundläggande information om programvarutitlar skickas till System Center Online. Informationen om programvarutitlarna som ska kategoriseras kan granskas innan den skickas.  

-   Information om programvarulicenser skickas aldrig.  

-   Programvarutitlar som överförs blir offentligt tillgängliga som en del av System Center Online-katalogen och kan laddas ned av andra kunder.  

-   Källan för programvarutiteln lagras inte i System Center Online-katalogen. Programvarutitlar som innehåller konfidentiell eller upphovsrättsskyddad information bör dock inte skickas för kategorisering av System Center Online.  

> [!NOTE]  
>  Mer information om Tillgångsinformation sekretess information finns i [säkerhet och sekretess för tillgångsinformation](../../../../core/clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md).  

 Följ stegen nedan om du vill begära kategorisering av programvarutitlar för tillgångsinformationskatalogen från System Center Online.  

#### <a name="to-request-a-catalog-update-for-uncategorized-software-titles"></a>Så här begär du en kataloguppdatering för okategoriserade programvarutitlar  

1.  Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2.  Klicka på **Tillgångsinformation** på arbetsytan **Tillgångar och efterlevnad**och klicka sedan på **Inventerad programvara**.  

3.  Välj ett eller flera produktnamn som ska skickas till System Center Online för kategorisering. Endast okategoriserade inventerade programvarutitlar kan skickas till System Center Online för kategorisering. Om en inventerad programvarutitel har kategoriserats av en administratör och lett till ett användardefinierat tillstånd måste du högerklicka på den inventerade programvarutiteln och sedan klicka på **Återställ** för att återställa programvarutiteln till tillståndet **Ej kategoriserade** innan den kan skickas till System Center Online för kategorisering.  

    > [!NOTE]  
    >  Configuration Manager kan bearbeta upp till 2000 program varu titlar för kategorisering i taget. Om du väljer fler än 2000 program varu titlar bearbetas bara de första 2000-program varu titlarna. Du måste välja de återstående program titlarna för kategorisering i batchar som är mindre än 2000.  

    > [!TIP]  
    >  Klicka på kolumnen **Tillstånd** om du vill sortera efter valideringstillstånd. På så sätt kan du se alla okategoriserade produktnamn och snabbt välja flera objekt som du vill skicka för kategorisering.  

4.  Klicka på **Begär kataloguppdatering** i gruppen **Produkt** på fliken **Start**.  

5.  Granska sekretessmeddelandet för begäran om System Center Online-kategorisering. Klicka på **Information** om du vill visa informationen som skickas till System Center Online.  

6.  Välj **Jag har läst och förstått det här meddelandet**och klicka sedan på **OK** för att tillåta att de valda programvarutitlarna skickas för kategorisering.  

7.  Kontrollera att tillståndet för de inventerade programvarutitlarna som skickats till System Center Online för kategorisering har ändrats från **Ej kategoriserade** till **Väntar**.  

    > [!NOTE]  
    >  Programvara som skickats till System Center Online för kategorisering och som har valideringstillståndet **Väntar** på en central administrationsplats visas fortfarande med valideringstillståndet **Ej kategoriserade** på underordnade primära platser.  

##  <a name="resolve-software-details-conflicts"></a><a name="BKMK_ResolveSoftwareDetails"></a> Lösa programvaruinformationskonflikter  
 När nyligen uppdaterad information om programvarukategorisering har tagits emot från System Center Online som står i konflikt med befintlig programvaruinformation kan du välja hur konflikten ska lösas. Programvara som är i konflikt har valideringstillståndet **Uppdaterbar**. När en konflikt har lösts bevaras informationen om programvarukategoriseringen i tillgångsinformationskatalogen baserat på den inställning du anger. En programinformationskonflikt uppstår inte för samma programvarukategoriseringsvärde igen såvida inte System Center Online-värdet ändras efter att konflikten har lösts.  

 Följ stegen nedan om du vill lösa en konflikt med programvaruinformation.  

#### <a name="to-resolve-a-software-details-conflict"></a>Så här löser du en konflikt med programvaruinformation  

1. Klicka på **Tillgångar och efterlevnad** i Configuration Manager-konsolen.  

2. Klicka på **Tillgångsinformation** på arbetsytan **Tillgångar och efterlevnad**och klicka sedan på **Inventerad programvara**.  

3. Titta i kolumnen **Tillstånd** efter programvarutitlar med tillståndet **Uppdaterbar** .  

4. Välj den programvarutitel som du behöver lösa en konflikt för och klicka på **Lös konflikt** i gruppen **Produkt** på fliken **Start**.  

5. Gå igenom följande information:  

   -   **Lokalt värde**: Anger den befintliga programkategoriseringsinformationen i tillgångsinformationskatalogen som är i konflikt med nyare information från System Center Online.  

   -   **Hämtat värde**: Anger den nya programkategoriseringsinformationen från System Center Online för motstridig information i tillgångsinformationskatalogen.  

6. Välj någon av följande inställningar när du ska lösa programinformationskonflikten:  

   - **Behåll informationen i den lokalt redigerade katalogen**: Löser konflikten med programvaruinformationen genom att behålla den befintliga programkategoriseringsinformationen från tillgångsinformationskatalogen. Om du väljer den här inställningen ändras tillståndet för programvarutiteln från **Uppdaterbar** till **Användardefinierad**.  

   - **Skriv över informationen i den lokalt redigerade katalogen med informationen i System Center Online-katalogen**: Löser konflikten med programvaruinformationen genom att skriva över den befintliga programkategoriseringsinformationen i tillgångsinformationskatalogen med den nya informationen från System Center Online. Om du väljer den här inställningen ändras tillståndet för programvarutiteln från **Uppdaterbar** till **Verifierad**.  

     Spara konfliktlösningen genom att klicka på **OK** .  
