---
title: Övervaka appanvändningen med avläsning av programvara
titleSuffix: Configuration Manager
description: Läs mer om åtgärder som är tillgängliga i Configuration Manager avläsning av program vara.
ms.date: 09/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13d8cce1811c4a27f6a3e7485eea4d65132c2888
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710085"
---
# <a name="software-metering-in-configuration-manager"></a>Avläsning av program vara i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller en referens för alla åtgärder som du kan utföra när du använder Configuration Manager avläsning av program vara.

> [!IMPORTANT]
>  Avläsning av programvara används för att övervaka Windows-skrivbordsappar med filnamn som slutar på **.exe**. Avläsning av programvara övervakar inte moderna Windows-appar (till exempel de som används av Windows 8).

##  <a name="prerequisites-for-software-metering"></a>Krav för avläsning av programvara
Avläsning av programvara har inga externa beroenden, endast beroenden inom produkten.

|Beroende|Mer information|
|----------------|----------------------|
|Klientinställningar för avläsning av programvara|Om du vill använda avläsning av programvara måste klientinställningen **Aktivera avläsning av programvara på klienter** vara aktiverad och distribuerad till datorer. Du kan distribuera inställningar för avläsning av programvara till alla datorer i hierarkin, eller distribuera anpassade inställningar till grupper med datorer. Se **Konfigurera avläsning av program vara** i det här avsnittet.|
|Reporting Services-platsen.|Du måste konfigurera en Reporting Services-plats innan du kan visa rapporter från avläsning av programvara. Mer information finns i [Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md).|

##  <a name="configure-software-metering"></a>Configure software metering
 Den här proceduren konfigurerar standardklientinställningarna för avläsning av programvara och gäller för alla datorer i hierarkin. Om du vill att dessa inställningar bara ska gälla för vissa datorer skapar du en anpassad enhetsklientinställning och distribuerar den till en samling som innehåller de datorer som du vill använda avläsning av programvara för. Mer information om hur du skapar anpassade enhets inställningar finns i [Konfigurera klient inställningar](../../core/clients/deploy/configure-client-settings.md).

1. I Configuration Manager-konsolen klickar du på **Administration** > **klient inställningar** > **standard klient inställningar**.

2. På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.

3. Klicka på **Avläsning av programvara** i dialogrutan **Standardinställningar**.

4. Konfigurera följande i listan **Enhetsinställningar** :

   -   **Aktivera avläsning av programvara på klienter**: Välj **Sant** om du vill aktivera avläsning av programvara.

   -   **Schemalägger datainsamling**: Konfigurera hur ofta data för avläsning av programvara samlas in från klientdatorer. Använd standardvärdet för varje **7 dagar** eller klicka på **Schema** om du vill ange ett anpassat schema.

5. Stäng dialogrutan **Standardinställningar** genom att klicka på **OK** .

   Klientdatorerna konfigureras med de här inställningarna nästa gång de laddar ned klientprinciper. Information om hur du startar princip hämtning för en enskild klient finns i [Hantera klienter](../../core/clients/manage/manage-clients.md).

##  <a name="create-software-metering-rules"></a> Skapa regler för avläsning av programvara
 Använd guiden Skapa regel för avläsning av program vara för att skapa en ny regel för avläsning av program vara för din Configuration Manager-plats.

1.  I Configuration Manager-konsolen klickar du på **till gångar och efterlevnad** > för**avläsning av program vara**.

3.  Klicka på **Skapa regel för avläsning av programvara** i gruppen **Skapa** på fliken **Start**.

4.  Ange följande information på sidan **Allmänt** i guiden Skapa regel för avläsning av program vara:

    -   **Namn** – Namnet på regeln för avläsning av programvara. Namnet bör vara unikt och beskrivande.

        > [!NOTE]
        >  Regler för avläsning av programvara kan ha samma namn om filnamnet i reglerna är olika.

    -   **Filnamn** – Namnet på den programfil som du vill läsa av. Du kan klicka på **Bläddra** för att öppna dialogrutan **Öppna** där du kan välja den programfil som du vill använda.

        > [!NOTE]
        >  Om du skriver namnet på den körbara filen i rutan **Filnamn** körs ingen kontroll för att avgöra om filen finns eller om den innehåller nödvändig rubrikinformation. Om möjligt klickar du på **Bläddra** och väljer den körbara fil som ska läsas av.
        >
        >  Jokertecken tillåts inte i filnamnet.
        >
        >  Den här rutan är valfri om ett värde för **Ursprungligt filnamn** har angetts.

    -   **Ursprungliga filnamn** – Namnet på den körbara fil som du vill läsa av. Det här namnet matchar information i filens huvud, inte själva filnamnet, och kan användas då den körbara filen har bytt namn men du vill läsa av den med det ursprungliga namnet.

        > [!NOTE]
        >  Jokertecken tillåts inte i det ursprungliga filnamnet.
        >
        >  Den här rutan är valfri om ett värde för **Filnamn** har angetts.

    -   **Version** – Versionen av den körbara fil som du vill läsa av. Du kan använda jokertecknet (&#42;) för att representera en valfri sträng med tecken eller jokertecknet (? ) för att representera ett enskilt Character. Använd standardvärdet (&#42;) om du vill mäta för alla versioner av en körbar fil.

    -   **Språk** – Språk för den körbara fil som du vill läsa av. Standardvärdet är språket för det operativsystem som du använder. Om du väljer att läsa av en körbar fil genom att klicka på knappen **Bläddra** fylls den här rutan i automatiskt om det finns språkinformation i filens huvud. Om du vill läsa av alla språkversioner av en fil väljer du **Valfri** i listrutan.

    -   **Beskrivning** – En valfri beskrivning av regeln för avläsning av programvara.

    -   **Tillämpa den här regeln vid avläsning av programvara på följande klienter** – Välj om du vill tillämpa regeln för avläsning av programvara på alla klienter i hierarkin eller på klienter som är kopplade till den plats som angetts i listan **Plats** .

5.  Fortsätt genom att klicka på **Nästa**.

6.  Granska och bekräfta inställningarna och slutför sedan guiden för att skapa regeln för avläsning av programvara. Den nya regeln för avläsning av programvara visas på noden **Avläsning av programvara** på arbetsytan **Tillgångar och efterlevnad** .

##  <a name="configure-automatic-software-metering-rules"></a> Konfigurera automatiska regler för avläsning av programvara
 Du kan konfigurera Avläsning av program vara i Configuration Manager att automatiskt generera inaktiverade regler för avläsning av program vara från senaste användnings inventerings data som lagras i plats databasen. Du kan konfigurera den här inventeringsinformationen så att avläsningsregler endast skapas för program som används på en angiven procentandel datorer. Du kan också ange det högsta antalet automatiskt genererade regler för avläsning av programvara som tillåts på platsen.

> [!NOTE]
>  Regler för avläsning av programvara som skapas automatiskt är inaktiverade som standard. Innan du kan börja samla in användningsdata från dessa regler måste du aktivera dem.

1.  I Configuration Manager-konsolen klickar du **på till gångar och efterlevnad** > för**avläsning av program vara**och klickar sedan på Egenskaper för avläsning av **program vara**i gruppen **Inställningar** på fliken **Start** .

3.  Konfigurera följande i dialogrutan **Egenskaper för avläsning av programvara** :

    -   **Datalagring (i dagar)** – Anger hur länge data som genereras av regler för avläsning av programvara sparas i platsdatabasen. Standardvärdet är **90** dagar.

    -   Aktivera alternativet **Skapa automatiskt inaktiverade regler för avläsning baserat på aktuella användningsinventeringsdata**.

    -   **Ange hur stor procentandel av datorerna i hierarkin som måste använda ett program innan det automatiskt skapas en regel för avläsning av programvara** – Standardvärdet är **10** procent.

    -   **Ange antalet regler för avläsning av programvara som måste överskridas i hierarkin innan automatiskt skapande av regler ska inaktiveras** – Standardvärdet är **100** regler.

4.  Stäng dialogrutan **Egenskaper för avläsning av programvara** genom klicka på **OK** .

##  <a name="manage-software-metering-rules"></a> Hantera regler för avläsning av programvara
 Välj **Avläsning av programvara** på arbetsytan **Tillgångar och efterlevnad**, välj regeln för avläsning av programvara och välj en hanteringsaktivitet.

 I följande tabell finns mer information om hanteringsaktiviteter som du kan behöva veta lite mer om innan du väljer dem.

|Hanteringsaktivitet|Information|
|---------------------|-------------|
|**Aktivera**<br /><br /> **Inaktivera**|Aktiverar eller inaktiverar en regel för avläsning av programvara. Den här inställningen hämtas till klientdatorer enligt **Avsökningsintervall för klientprincip** i avsnittet **Klientprincip** i klientinställningarna (som standard var 60: e minut).<br /><br /> Se [Konfigurera klient inställningar](../../core/clients/deploy/configure-client-settings.md) .|

##  <a name="monitor-software-metering"></a>Övervaka avläsning av program vara
 Avläsning av program vara i Configuration Manager innehåller ett antal inbyggda rapporter som gör att du kan övervaka information om åtgärder för avläsning av program vara. De här rapporterna tillhör rapportkategorin **Avläsning av programvara**.

 Mer information om hur du konfigurerar rapportering i Configuration Manager finns i [Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md).

 Dessutom kan du skapa frågor och samlingar baserat på data som lagras i Configuration Manager-databasen genom avläsning av program vara.

 Mer information om samlingar i Configuration Manager finns i [Introduktion till samlingar](../../core/clients/manage/collections/introduction-to-collections.md).

 Mer information om frågor i Configuration Manager finns i [Introduktion till frågor](../../core/servers/manage/introduction-to-queries.md).

##  <a name="security-and-privacy-for-software-metering"></a>Säkerhet och sekretess för avläsning av programvara

### <a name="security-issues-for-software-metering"></a>Säkerhetsproblem för avläsning av programvara
 En angripare kan skicka ogiltig information om avläsning av program vara till Configuration Manager, vilket kommer att godkännas av hanterings platsen även om klient inställningen för program varu avläsning är inaktive rad. Detta kan resultera i ett stort antal avläsnings regler som replikeras i hela hierarkin, vilket orsakar en denial of service i nätverket och Configuration Manager plats servrar.

 Eftersom en angripare kan skapa ogiltig information för avläsning av programvara ska du inte betrakta information för avläsning av programvara som auktoritär.

 Avläsning av programvara är aktiverat som standard som en klientinställning.

###  <a name="privacy-information-for-software-metering"></a> Sekretessinformation för avläsning av programvara
 Avläsning av programvara övervakar användningen av program på klientdatorer. Avläsning av programvara är aktiverat som standard. Du måste konfigurera vilka program som ska avläsas. Avläsnings information lagras i Configuration Manager-databasen. Informationen krypteras under överföringen till en hanterings plats, men den lagras inte i krypterad form i Configuration Manager databasen.

 Den här informationen sparas i databasen tills den raderas av platsunderhållsåtgärderna **Ta bort föråldrade programmätningsdata** (var femte dag) och **Ta bort föråldrade sammanfattningsdata för programmätare** (var 270:e dag). Du kan konfigurera borttagningsintervallet. Avläsningsinformation skickas inte till Microsoft.

 Innan du konfigurerar avläsning av programvara bör du tänka igenom dina sekretesskrav.

## <a name="example-scenario-for-using-software-metering"></a>Exempelscenario för att använda Avläsning av programvara
 I det här avsnittet skapar du en exempelregel för Avläsning av programvara som hjälper dig att:

- fastställa hur många exemplar av en viss app som finns på företaget

- identifiera oanvända exemplar av en app

- avgöra vilka användare som regelbundet använder en viss app.

  Woodgrove Bank har distribuerat Microsoft Office 2010 som sin standardprogramsvit för kontorsproduktivitet. Vissa datorer måste dock fortsätta att köra Microsoft Office Word 2003 för att stödja äldre program. IT-avdelningen vill minska support- och licensieringskostnaderna genom att avlägsna dessa exemplar av Word 2003 om det äldre programmet inte längre används. Supportavdelningen vill också veta vilka användare som använder det äldre programmet.

  Sparbankens IT Systems Manager använder avläsning av program vara i Configuration Manager för att uppnå dessa affärs mål. Administratören utför följande åtgärder:

- Kontrollerar förutsättningarna för avläsning av program vara och bekräftar att repor ting Services-platsen är installerad och fungerar.
- Konfigurerar standard klient inställningarna för avläsning av program vara:<br>Administratören aktiverar avläsning av program vara och använder standardschemat för data insamling var sjunde dag.<br>Administratören konfigurerar program varu inventeringen för inventering av filer som har fil namns tillägget. exe genom att konfigurera klient inställningen för program varu inventering **inventera de här fil typerna**.<br>Administratören lägger till en ny regel för avläsning av program vara med namnet **sparbank. exe**för att övervaka det äldre programmet.
- Väntar i sju dagar tills klient datorerna börjar rapportera användnings data för den körbara filen för **sparbank. exe** .
- Administratören använder Configuration Manager-rapportens **installations bas för alla bevakade program varor** för att se vilka datorer som har programmet **sparbank. exe** inläst.
- Efter sex månader kör administratören de rapport **datorer som har ett bevakat program installerat, men har inte kört programmet sedan ett angivet datum**, angett en regel för avläsning av program vara och ett datum sex månader tidigare. Rapporten returnerar 120 datorer som inte har kört programmet under de senaste sex månaderna.
- Administratören gör ytterligare kontroller för att bekräfta att det äldre programmet inte behövs på de identifierade datorerna. Administratören avinstallerar sedan det äldre programmet och kopian av Word 2003 från dessa datorer.<br>Administratören kör rapport **användare som har kört ett angivet bevakat program** för att ge supportavdelningen en lista över användare som fortsätter att använda det äldre programmet.
- Administratören fortsätter att kontrol lera rapporten för avläsning av program vara varje vecka och vidtar åtgärder vid behov.

  Dessa åtgärder leder till minskade kostnader för IT-support och licensiering eftersom program som inte längre behövs kan avlägsnas. Dessutom har supportavdelningen nu tillgång till den lista man efterfrågat över användare som kör det äldre programmet.
