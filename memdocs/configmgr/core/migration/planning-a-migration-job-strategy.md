---
title: Planera migreringsjobb
titleSuffix: Configuration Manager
description: Använd migreringsjobb för att konfigurera data som du vill migrera till din Configuration Manager aktuella gren miljö.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87aac20a2ac70e843bf17982375c92804de2b20e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719675"
---
# <a name="plan-a-migration-job-strategy-in-configuration-manager"></a>Planera en jobb strategi för migrering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd migreringsjobb för att konfigurera de data som du vill migrera till din Configuration Manager aktuella gren miljö. Migreringsjobb identifierar de objekt som du planerar att migrera och de körs på platsen på den översta nivån i målhierarkin. Du kan ställa in ett eller flera migreringsjobb per käll plats. På så sätt kan du migrera alla objekt vid en viss tidpunkt eller begränsad del mängder av data med varje jobb.  

 Du kan skapa migreringsjobb när Configuration Manager har samlat in data från en eller flera platser i källhierarkin. Du kan migrera data i valfri ordning från de källplatser där data har samlats in. Med en Configuration Manager 2007-käll plats kan du migrera data endast från den plats där ett objekt skapades. Med käll platser som kör System Center 2012 Configuration Manager eller senare är alla data som du kan migrera tillgängliga på den översta nivån i källhierarkin.  

 Innan du migrerar klienter mellan hierarkier måste du säkerställa att de objekt som används av klienterna har migrerats och att objekten är tillgängliga i målhierarkin. När du t. ex. migrerar från en Configuration Manager 2007 SP2-källhierarki kan du ha en annons om innehåll som har distribuerats till en anpassad samling som har en-klient. I det här scenariot rekommenderar vi att du migrerar samlingen, annonsen och det associerade innehållet innan du migrerar klienten. Den här informationen kan inte kopplas till klienten i målhierarkin om innehållet, samlingen och annonsen inte migreras innan klienten migreras. Om en klient inte associeras med en annons som har körts tidigare (och tillhörande innehåll), kanske klienten erbjuds innehållet för installation i målhierarkin, vilket är onödigt. När klienten migreras efter att alla data har migrerats, associeras klienten med innehållet och annonsen, och om inte annonsen är återkommande, erbjuds inte klienten innehållet för den migrerade annonsen på nytt.  

 För vissa objekt krävs fler åtgärder än att migrera data från källhierarkin till målhierarkin. Om du till exempel vill migrera program uppdateringar för dina klienter till målhierarkin, måste du distribuera en aktiv program uppdaterings plats, konfigurera produkt katalogen och synkronisera program uppdaterings platsen med Windows Server Update Services (WSUS) i målhierarkin.  

##  <a name="types-of-migration-jobs"></a><a name="Types_of_Migration"></a>Typer av migreringsjobb  
 Configuration Manager stöder följande typer av migreringsjobb. Varje Jobbtyp är utformad för att hjälpa dig att definiera de objekt som du kan ta med i jobbet.  

 **Migrering av samling** (stöds bara vid migrering från Configuration Manager 2007 SP2): Migrera objekt som är relaterade till samlingar som du väljer. Som standard innehåller samlings migrering alla objekt som är associerade med medlemmar i samlingen. Du kan exkludera specifika objektinstanser när du använder den här typen av migreringsjobb.  

 **Migrering av objekt**: Migrera enskilda objekt som du väljer. Här väljer du specifika data som ska migreras.  

 **Migrering av tidigare migrerade**objekt: Migrera objekt som du tidigare migrerade när de har uppdaterats i källhierarkin efter den senaste migreringen.  

###  <a name="objects-that-you-can-migrate"></a><a name="Objects_that_can_migrate"></a>Objekt som du kan migrera  
 Alla typer av objekt kan inte migreras med en viss typ av migreringsjobb. Listan nedan visar vilka typer av objekt du kan migrera med de olika migreringsjobben.  

> [!NOTE]  
>  Migrering av samlingar är endast tillgängligt när du migrerar objekt från en Configuration Manager 2007 SP2-källhierarki.  

 **Jobb typer som du kan använda för att migrera varje objekt**  

-   **Annonser** (tillgängliga för migrering från Configuration Manager 2007-käll platser som stöds)  

    -   Migrering av samling  


-   **Tillgångsinformationskatalog**  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Maskinvarukrav för tillgångsinformation**  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Programlista för tillgångsinformation**  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Gränser**  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Konfigurationsbaslinjer**  

    -   Migrering av samling  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Konfigurations objekt**  

    -   Migrering av samling  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Underhålls fönster**  

    -   Migrering av samling  


-   **Startavbildningar för distribution av operativsystem**  

    -   Migrering av samling  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Drivrutinspaket för distribution av operativsystem**  

    -   Migrering av samling  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Drivrutiner för distribution av operativsystem**  

    -   Migrering av samling  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Avbildningar för distribution av operativsystem**  

    -   Migrering av samling  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Paket för distribution av operativsystem**  

    -   Migrering av samling  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Paket för program varu distribution**  

    -   Migrering av samling  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Regler för avläsning av programvara**  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Paket för distribution av program uppdatering**  

    -   Migrering av samling  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Distributionspaket för programvaruuppdateringar**  

    -   Migrering av samling  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Distribution av programuppdateringar**  

    -   Migrering av samling  


-   **Programuppdateringslistor**  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Aktivitetssekvenser**  

    -   Migrering av samling  

    -   Migrering av objekt  

    -   Migrering av tidigare migrerade objekt  

-   **Virtuella programpaket**  

    -   Migrering av samling  

    -   Migrering av objekt  

    > [!IMPORTANT]  
    >  Du kan migrera ett paket för virtuella program genom att använda objektmigrering, men det går inte att migrera paketen med migreringsjobbtypen för migrering av **tidigare migrerade objekt**. I stället måste du ta bort det migrerade paketet för virtuella program från målplatsen och sedan skapa ett nytt jobb för migrering av det virtuella programmet.  

##  <a name="general-planning-for-all-migration-jobs"></a><a name="About_Migration_Jobs"></a>Allmän planering för alla migreringsjobb  
 Använd guiden Skapa migreringsjobb för att skapa ett migreringsjobb för att migrera objekt till målhierarkin. Den typ av migreringsjobb du skapar avgör vilka objekt som är tillgängliga för migrering. Du kan skapa och använda flera migreringsjobb för att migrera data från samma käll plats eller från flera käll platser. Användning av en viss typ av migreringsjobb förhindrar inte användning av en annan typ av migreringsjobb.  

 När ett migreringsjobb har slutförts tilldelas det statusen **Slutförd** och kan inte köras på nytt. Du kan dock skapa ett nytt migreringsjobb för att migrera ett eller flera av de objekt som migrerades av det ursprungliga jobbet, och i det nya migreringsjobbet kan du även lägga till nya objekt. När du skapar ytterligare migreringsjobb visas de objekt som **har migrerats tidigare.** Du kan välja dessa objekt om du vill migrera dem igen, men om inte objektet har uppdaterats i källhierarkin är det inte nödvändigt att migrera dessa objekt. Om det finns objekt som har uppdaterats i källhierarkin efter den ursprungliga migreringen, kan du identifiera sådana objekt om du använder migreringsjobbtypen **Objekt som modifierats efter migrering**.  

 Du kan ta bort ett migreringsjobb innan det körs. Men när ett migreringsjobb har slutförts visas det fortfarande i Configuration Manager-konsolen och kan inte tas bort. Varje migreringsjobb som har slutförts eller som ännu inte har körts är synligt i Configuration Manager-konsolen tills du är klar med migreringsprocessen och rensar data för migrering.  

> [!NOTE]  
>  När du har avslutat migreringen med åtgärden **Rensa migrering** , kan du konfigurera om samma hierarki som den aktuella källhierarkin för att återställa synligheten till de objekt som du migrerade tidigare.  

 Du kan visa de objekt som finns i alla migreringsjobb i Configuration Manager-konsolen genom att välja migreringsjobb och sedan välja **objekten på fliken jobb** .  

 Använd informationen i nedanstående avsnitt när du planerar migreringsjobb.  

### <a name="data-selection"></a>Dataurval  
 När du skapar ett migreringsjobb för en samling måste du välja en eller flera samlingar. När du har valt samlingarna visar guiden Skapa migreringsjobb de objekt som är associerade med samlingarna. Som standard migreras alla objekt som är associerade med de valda samlingarna, men du kan avmarkera de objekt som du inte vill migrera med jobbet. När du avmarkerar ett objekt som har beroende objekt, avmarkeras även de beroende objekten. Alla omarkerade objekt läggs till i en undantags lista. Objekt som ingår i undantagslistan tas bort från automatiska urval i kommande migreringsjobb. Du måste redigera undantagslistan manuellt, om du vill ta bort objekt som inte ska väljas automatiskt för nya migreringsjobb som skapas senare.  

### <a name="site-ownership-for-migrated-content"></a>Plats ägarskap för migrerat innehåll  
 När du migrerar innehåll för distributioner måste du tilldela innehållsobjektet till en plats i målhierarkin. Den här platsen blir sedan ägaren till det innehållet i destinationshierarkin. Även om platsen på den översta nivån i din målhierarki är den plats där du faktiskt migrerar metadata för innehåll, är det den tilldelade platsen som kommer åt de ursprungliga källfilerna för innehållet över nätverket.  

 Om du vill minimera nätverksbandbredden som används vid migrering kan du överföra ägarskapet för innehållet till närmaste tillgängliga plats. Eftersom information om innehållet delas globalt i Configuration Manager kommer den att vara tillgänglig på alla platser.  

 Information om innehållet delas på alla platser i målhierarkin med hjälp av databasreplikering. Men allt innehåll som du tilldelar till en primär plats och sedan distribuerar till distributions platser på andra primära platser överförs med hjälp av filbaserad replikering. Den här överföringen dirigeras genom den centrala administrationsplatsen och sedan till varje ytterligare primär plats. Genom att centralisera paket som du planerar att distribuera till flera primära platser före eller under migreringen när du tilldelar en plats som innehålls ägare, kan du minska data överföringar i nätverk med liten bandbredd.  

### <a name="role-based-administration-security-scopes-for-migrated-data"></a>Rollbaserade administrations säkerhets omfattningar för migrerade data  
 När du migrerar data till en målhierarkin måste du tilldela en eller flera rollbaserade administrations säkerhets omfattningar till de objekt vars data migreras. På så sätt säkerställer du att endast administrativa användare har tillgång till information som har migrerats. De säkerhetsomfattningar som du anger definieras av migreringsjobbet och används för varje objekt som migreras med jobbet. Om du behöver använda olika säkerhets omfattningar för olika objekt uppsättningar och du vill tilldela dessa omfattningar under migreringen, måste du migrera de olika objekt uppsättningarna genom att använda olika migreringsjobb.  

 Innan du konfigurerar ett migreringsjobb bör du granska hur rollbaserad administration fungerar i Configuration Manager. Vid behov kan du konfigurera en eller flera säkerhets omfattningar för de data som du migrerar för att kontrol lera vem som ska ha åtkomst till de migrerade objekten i målhierarkin.  

 Mer information om säkerhets omfattningar och rollbaserad administration finns i [grunderna i rollbaserad administration för Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="review-migration-actions"></a>Granska migreringsåtgärder  
 När du konfigurerar ett migreringsjobb visar guiden Skapa migreringsjobb en lista med åtgärder som du måste vidta för att säkerställa en lyckad migrering och en lista över åtgärder som Configuration Manager vidtar under migreringen av valda data. Granska informationen noga för att kontrol lera det förväntade resultatet.  

### <a name="schedule-migration-jobs"></a>Schemalägg migreringsjobb  
 Som standard körs ett migreringsjobb direkt efter att det har skapats. Du kan dock ange när migreringsjobbet ska köras när du skapar jobbet eller genom att redigera egenskaperna för jobbet. Du kan schemalägga migreringsjobbet så att det körs enligt följande:  

-   Kör jobbet nu  

-   Kör jobbet vid en viss starttid  

-   Kör inte jobbet  

### <a name="specify-conflict-resolution-for-migrated-data"></a>Ange konfliktlösning för migrerade data  
 Som standard skriver inte migreringsjobb över data i mål databasen om du inte konfigurerar migreringsjobbet att hoppa över eller skriva över data som tidigare har migrerats till mål databasen.  

##  <a name="plan-for-collection-migration-jobs"></a><a name="About_Collection_Migration"></a>Planera för migrering av samlingar  
 Migrering av samlingar är endast tillgängligt när du migrerar data från en-källhierarki som kör en version av Configuration Manager 2007 som stöds. Du måste ange en eller fler samlingar att migrera när du migrerar per samling. För varje samling du anger väljs alla relaterade objekt för migrering automatiskt i migreringsjobbet. Exempel: Om du väljer en specifik samling användare så identifieras samlingsmedlemmarna och du kan migrera distributionerna som är associerade med den samlingen. Du kan alternativt välja andra distributionsobjekt att migrera som är associerade med de medlemmarna. Alla valda objekt läggs till i listan med objekt som kan migreras.  

 När du migrerar en samling migrerar Configuration Manager även samlings inställningar, inklusive underhålls fönster och Collection-variabler, men det går inte att migrera samlings inställningar för AMT-klient etablering.  

 Använd informationen i följande avsnitt om du vill veta mer om ytterligare konfigurationer som kan tillämpas på samlings migreringsjobb.  

### <a name="exclude-objects-from-collection-migration-jobs"></a>Uteslut objekt från migrering av samlingar  
 Du kan exkludera specifika objekt från ett samlingsmigreringsjobb. När du undantar ett särskilt objekt från ett migreringsjobb, läggs det objektet till i en global undantags lista som innehåller alla objekt som du har exkluderat från migreringsjobb som skapats för alla käll platser i den aktuella källhierarkin. Objekt i undantags listan är fortfarande tillgängliga för migrering i framtida jobb men inkluderas inte automatiskt när du skapar ett nytt samlings jobb baserat migreringsjobb.  

 Du kan redigera undantagslistan och ta bort objekt som du tidigare har exkluderat. När du har tagit bort ett objekt från undantagslistan väljs den sedan automatiskt när en associerad samling anges när ett nytt migreringsjobb skapas.  

### <a name="unsupported-collections"></a>Samlingar som inte stöds  
 Configuration Manager kan migrera alla standard användar samlingar, enhets samlingar och de flesta anpassade samlingar från en Configuration Manager 2007-källhierarki. Configuration Manager kan dock inte migrera samlingar som innehåller användare och enheter i samma samling.  

 Det går inte att migrera följande samlingar:  

-   En samling som innehåller användare och enheter.  

-   En samling som har en referens till en samling av en annan resurs typ. Till exempel en enhets-baserad samling som antingen har en under samling eller en länk till en användardefinierad samling. I det här exemplet migreras bara samlingen på den översta nivån.  

-   En samling som har en regel för att inkludera okända datorer. Samlingen migreras men regeln för inkludering av okända datorer migreras inte.  

### <a name="empty-collections"></a>Tomma samlingar  
 En tom samling har inga resurser som är associerade med den. När Configuration Manager migrerar en tom samling konverteras samlingen till en organisatorisk mapp som inte har några användare eller enheter. Den här mappen skapas med namnet på den tomma samlingen under noden **användar samlingar** eller **enhets samlingar** i arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen.  

### <a name="linked-collections-and-subcollections"></a>Länkade samlingar och undersamlingar  
 När du migrerar samlingar som är länkade till andra samlingar eller som har under samlingar, skapar Configuration Manager en mapp under noden **användar samlingar** eller **enhets samlingar** utöver de länkade samlingarna och under samlingarna.  

### <a name="collection-dependencies-and-include-objects"></a>Samlingsberoenden och inkluderade objekt  
 När du anger en samling som ska migreras i guiden Skapa migreringsjobb väljs alla beroende samlingar automatiskt för att inkluderas i jobbet. Med det här beteendet garanteras att alla nödvändiga resurser är tillgängliga efter migreringen.  

 Exempel: du väljer en samling för enheter som kör Windows 10 och heter **Win_10**. Den här samlingen är begränsad till en samling som har alla klient operativ system och heter **All_Clients**. Samlings **All_Clients** väljs automatiskt för migrering.  

### <a name="collection-limiting"></a>Samlingsbegränsning  
 Med Configuration Manager aktuella grenen är samlingar globala data och utvärderas på varje plats i hierarkin. Därför bör du planera hur du ska begränsa omfattningen för en samling som har migrerats. Under migreringen kan du identifiera en samling i målhierarkin och använda den till att begränsa omfattningen för samlingen du migrerar, så att den migrerade samlingen inte inkluderar oväntade medlemmar.  

 I Configuration Manager 2007 utvärderas till exempel samlingar på den plats där de skapas och på underordnade platser. En annons kan bara distribueras på en underordnad plats, vilket begränsar omfattningen för den annonsen och en underordnade platsen. I jämförelse, med Configuration Manager aktuella grenen, utvärderas samlingarna på varje plats och associerade annonser utvärderas sedan för varje plats. Med samlingsbegränsning kan du finjustera tilläggen av samlingsmedlemmar, baserat på en annan samling för att undvika att oväntade samlingsmedlemmar läggs till.  

### <a name="site-code-replacement"></a>Ersätta platskoder  
 När du migrerar en samling med villkor som identifierar en Configuration Manager 2007-plats måste du ange en speciell plats i målhierarkin. På så sätt förblir den migrerade samlingen funktionell i målhierarkin och omfattningen ökas inte.  

### <a name="specify-behavior-for-migrated-advertisements"></a>Ange beteende för migrerade annonser  
 Som standard inaktiverar Collection-baserade migreringsjobb annonser som migreras till målhierarkin. Det här gäller alla program som är associerade med annonsen. När du skapar ett samlat migreringsjobb som innehåller annonser visas alternativet **Aktivera program för distribution i Configuration Manager efter att en annonsering har migrerats** på sidan **Inställningar** i guiden Skapa migreringsjobb. Om du väljer det här alternativet aktiveras program som är associerade med annonserna när de har migrerats. Vi rekommenderar att du inte väljer det här alternativet. Aktivera i stället programmen när de har migrerats när du kan verifiera klienterna som ska ta emot dem.  

> [!NOTE]  
>  Du ser alternativet **Aktivera program för distribution i Configuration Manager efter att en annonsering har migrerats** alternativ endast när du skapar ett samlings jobb med migreringsjobb och migreringsjobbet innehåller annonser.  

 Om du vill aktivera ett program efter migreringen avmarkerar du **inaktivera det här programmet på datorer där det annonseras** på fliken **Avancerat** i program egenskaperna.  

##  <a name="plan-for-object-migration-jobs"></a><a name="About_Object_Migration"></a>Planera för migrering av objekt  
 Till skillnad från samlingsmigrering måste du välja varje objekt och objektinstans som du vill migrera. Du kan välja enskilda objekt (t. ex. annonser från en Configuration Manager 2007-hierarki eller en publikation från ett System Center 2012 Configuration Manager eller Configuration Manager aktuella Branch-hierarki) för att lägga till i listan med objekt som ska migreras för ett specifikt migreringsjobb. De objekt som du inte lägger till i migreringslistan migreras inte till målplatsen med objektmigreringsjobbet.  

 Objektbaserade migreringsjobb har inte några ytterligare konfigurationer att planera för utöver de som gäller för alla migreringsjobb.  

##  <a name="plan-for-previously-migrated-object-migration-jobs"></a><a name="About_Object_Migrations"></a>Planera för tidigare migrerade objekt för migrering  
 När ett objekt som du redan har migrerat till målhierarkin uppdateras i källhierarkin kan du migrera det objektet igen genom att använda jobbtypen **Objekt som modifierats efter migrering**. När du till exempel byter namn på eller uppdaterar källfiler för ett paket i källhierarkin, ökar paket versionen i källhierarkin. När paketversionen ökas kan paketet identifieras för migrering med den här jobbtypen.  

 Den här jobbtypen liknar objektmigreringstypen, förutom att när du väljer objekt som ska migreras kan du bara välja bland objekt som redan har uppdaterats efter att de migrerades i ett tidigare migreringsjobb.   

 När du väljer den här jobb typen konfigureras konflikt lösnings beteendet på sidan **Inställningar** i guiden Skapa migreringsjobb så att tidigare migrerade objekt skrivs över. Det går inte att ändra den här inställningen.  

> [!NOTE]  
>  Det här migreringsjobbet kan identifiera objekt som uppdateras automatiskt av källhierarkin och objekt som en administrativ användare uppdaterar.  
