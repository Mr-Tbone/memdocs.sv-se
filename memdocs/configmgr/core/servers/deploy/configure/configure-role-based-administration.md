---
title: Konfigurera rollbaserad administration
titleSuffix: Configuration Manager
ms.date: 11/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 14258c3e7e2cfe5423b97064a26fdf5616d6b0a4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078625"
---
# <a name="configure-role-based-administration-for-configuration-manager"></a>Konfigurera rollbaserad administration för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I Configuration Manager kombinerar rollbaserad administration säkerhets roller, säkerhets omfattningar och tilldelade samlingar för att definiera den administrativa omfattningen för varje administrativ användare. En administrativ omfattning inkluderar de objekt som en administrativ användare kan visa i Configuration Manager-konsolen och de uppgifter som är relaterade till de objekt som den administrativa användaren har behörighet att utföra. Konfigurationer för rollbaserad administration används per plats i en hierarki.  

 Om du inte redan är bekant med koncept för rollbaserad administration, se [grunderna i rollbaserad administration](../../../understand/fundamentals-of-role-based-administration.md).  

 Informationen i följande procedurer kan hjälpa dig att skapa och konfigurera rollbaserad administration och relaterade säkerhets inställningar:  

- [Skapa anpassade säkerhets roller](#BKMK_CreateSecRole)  
- [Konfigurera säkerhets roller](#BKMK_ConfigSecRole)  
- [Konfigurera säkerhets omfattningar för ett objekt](#BKMK_ConfigSecScope)  
- [Konfigurera samlingar för att hantera säkerhet](#BKMK_ConfigColl)  
- [Skapa en ny administrativ användare](#BKMK_Create_AdminUser)  
- [Ändra den administrativa användarens administrativa omfattning](#BKMK_ModAdminUser)  

## <a name="create-custom-security-roles"></a><a name="BKMK_CreateSecRole"></a> Skapa anpassade säkerhetsroller

 Configuration Manager innehåller flera inbyggda säkerhets roller. Om du kräver fler säkerhetsroller kan du skapa en anpassad säkerhetsroll genom att kopiera en befintlig säkerhetsroll och ändra kopian. Du kan skapa en anpassad säkerhets roll för att ge administrativa användare de ytterligare säkerhets behörigheter de behöver som inte ingår i den säkerhets roll som för närvarande tilldelats. Genom att använda en en anpassad säkerhetsroll kan du ge dem bara de behörigheter de behöver, och undvika att tilldela en säkerhetsroll som ger dem större behörighet än de behöver.  

 Använd följande procedur för att skapa en ny säkerhetsroll genom att använda en befintlig säkerhetsroll som mall.  

### <a name="to-create-custom-security-roles"></a>Skapa anpassade säkerhetsroller

1. I Configuration Manager-konsolen går du till **Administration**.  

2. I arbets ytan **Administration** expanderar du **säkerhet**och väljer sedan **säkerhets roller**.  

   Använd någon av följande processer för att skapa den nya säkerhetsrollen:  

    - Gör så här för att skapa en ny anpassad säkerhetsroll:  

      1. Välj en befintlig säkerhetsroll som du vill använda som källa för den nya säkerhetsrollen.
      2. På fliken **Start** går du till gruppen **säkerhets roll** och väljer **Kopiera**. Den här åtgärden skapar en kopia av käll säkerhets rollen.  
      3. I guiden Kopiera säkerhetsroll anger du ett **Namn** för den nya anpassade säkerhetsrollen.  
      4. I **Säkerhetsåtgärdstilldelningar**expanderar du alla **Säkerhetsåtgärd** -noder för att visa tillgängliga åtgärder.  
      5. Om du vill ändra inställningen för en säkerhets åtgärd väljer du nedpilen i kolumnen **värde** och väljer antingen **Ja** eller **Nej**.

            > [!CAUTION]  
            > När du konfigurerar en anpassad säkerhets roll ska du se till att du inte beviljar behörigheter som inte krävs av administrativa användare som är associerade med den nya säkerhets rollen. **Ändra** värdet för säkerhets åtgärden **säkerhets roller** beviljar till exempel administrativa användare behörighet att redigera alla tillgängliga säkerhets roller – även om de inte är associerade med den säkerhets rollen.  

      6. När du har konfigurerat behörigheterna väljer du **OK** för att spara den nya säkerhets rollen.  

    - Om du vill importera en säkerhets roll som har exporter ATS från en annan Configuration Manager-hierarki utför du följande åtgärder:  

        1. På fliken **Start** går du till gruppen **skapa** och väljer **Importera säkerhets roll**.  
        2. Ange XML-filen som innehåller den säkerhets Rolls konfiguration som du vill importera. Välj **Öppna** för att slutföra proceduren och spara säkerhets rollen.  

            > [!NOTE]  
            > När du har importerat en säkerhetsroll kan du redigera säkerhetsrollens egenskaper för att ändra de objektbehörigheter som associerats med säkerhetsrollen.  

## <a name="configure-security-roles"></a><a name="BKMK_ConfigSecRole"></a> Konfigurera säkerhetsroller

 De grupper av säkerhetsbehörigheter som definierats för en säkerhetsroll kallas säkerhetsåtgärdstilldelningar. Säkerhetsåtgärdstilldelningar representerar en kombination av objekttyper och åtgärder som är tillgängliga för varje objekttyp. Du kan ändra vilka säkerhets åtgärder som är tillgängliga för alla anpassade säkerhets roller, men du kan inte ändra de inbyggda säkerhets roller som Configuration Manager tillhandahåller.  

 Med följande procedur ändrar du säkerhetsåtgärderna för en säkerhetsroll.  

### <a name="to-modify-security-roles"></a>Ändra säkerhetsroller

1. Välj **Administration**i Configuration Manager-konsolen.  
2. I arbets ytan **Administration** expanderar du **säkerhet**och väljer sedan **säkerhets roller**.  
3. Markera den anpassade säkerhetsroll som du vill ändra.  
4. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  
5. Välj fliken **behörigheter** .  
6. I **Säkerhetsåtgärdstilldelningar**expanderar du alla **Säkerhetsåtgärd** -noder för att visa tillgängliga åtgärder.  
7. Om du vill ändra inställningen för en säkerhets åtgärd väljer du nedpilen i kolumnen **värde** och väljer sedan **Ja** eller **Nej**.  

    > [!CAUTION]  
    > När du konfigurerar en anpassad säkerhets roll ska du se till att du inte beviljar behörigheter som inte krävs av administrativa användare som är associerade med den nya säkerhets rollen. **Ändra** värdet för säkerhets åtgärden **säkerhets roller** beviljar till exempel administrativa användare behörighet att redigera alla tillgängliga säkerhets roller – även om de inte är associerade med den säkerhets rollen.  

8. När du har konfigurerat säkerhets åtgärds tilldelningar väljer du **OK** för att spara den nya säkerhets rollen.  

##  <a name="configure-security-scopes-for-an-object"></a><a name="BKMK_ConfigSecScope"></a> Konfigurera säkerhetsomfattningar för ett objekt
 Du hanterar associationen av en säkerhets omfattning för ett objekt från objektet, inte från säkerhets omfattningen. De enda direkta konfigurationer som säkerhetsomfattningar stöder är ändringar i namnet och beskrivningen. För att du ska kunna ändra namnet och beskrivningen för en säkerhetsomfattning när du visar dess egenskaper måste du ha behörigheten **Ändra** för det skyddbara objektet **Säkerhetsomfattningar** .  

 När du skapar ett nytt objekt i Configuration Manager associeras det med varje säkerhets omfattning som är associerad med säkerhets rollerna för det konto som används för att skapa objektet. Det här problemet uppstår när dessa säkerhets roller ger behörigheten **skapa** eller **Ange säkerhets omfattning** . Du kan ändra säkerhets omfattningarna för objektet när du har skapat det.  

 Som exempel har du tilldelats en säkerhets roll som ger dig behörighet att skapa en ny avgränsnings grupp. När du skapar en ny begränsnings grupp har du inget alternativ som du kan tilldela vissa säkerhets omfattningar till. I stället tilldelas de säkerhets omfattningar som är tillgängliga från de säkerhets roller som du är associerad med automatiskt till den nya begränsnings gruppen. När du har sparat den nya begränsnings gruppen kan du redigera de säkerhets omfattningar som är associerade med den nya begränsnings gruppen.  

 Använd följande procedur för att konfigurera de säkerhets omfattningar som har tilldelats ett objekt.  

### <a name="to-configure-security-scopes-for-an-object"></a><a name="bkmk_config-sec-scope"></a>Konfigurera säkerhets omfattningar för ett objekt  

1. I Configuration Manager-konsolen väljer du ett objekt som stöder tilldelning till en säkerhets omfattning.  
2. På fliken **Start** går du till gruppen **klassificera** och väljer **Ange säkerhets omfattningar**.
3. I dialogrutan **Ange säkerhetsomfattningar** markerar och avmarkerar du de säkerhetsomfattningar som objektet är associerat med. Varje objekt som stöder säkerhetsomfattningar måste vara tilldelat till minst en säkerhetsomfattning.  
4. Välj **OK** för att spara de tilldelade säkerhets omfattningarna.  

    > [!NOTE]  
    > När du skapar ett nytt objekt kan du tilldela det till flera säkerhetsomfattningar. Om du vill ändra antalet säkerhets omfattningar som är associerade med objektet måste du ändra den här tilldelningen efter att objektet har skapats.

### <a name="to-configure-security-scopes-for-a-folder-starting-in-version-1906"></a><a name="bkmk_config-folder"></a>Så här konfigurerar du säkerhets omfattningar för en mapp (från och med version 1906)
<!--3600867-->

1. Välj en mapp i Configuration Manager-konsolen.  
1. På fliken **mapp** i menyfliksområdet väljer du **Ange säkerhets omfattningar**.
   - Du kan också högerklicka på mappen och välja **katalog** > **Ange säkerhets omfattningar**.
1. I dialog rutan **Ange säkerhets omfattningar** markerar eller avmarkerar du säkerhets omfattningar för mappen. Varje mapp måste tilldelas minst en säkerhets omfattning. Alla mappar tilldelas **standard** säkerhets omfattningen tills du ändrar den.
1. Välj **OK** för att spara de tilldelade säkerhets omfattningarna.  

    > [!IMPORTANT]  
    > - Befintliga säkerhets roller kommer automatiskt att hämta **mapp klass** behörigheter som läggs till när du installerar Configuration Manager version 1906. Du måste lägga till **mapp klass** behörigheter för alla nya säkerhets roller och kontrol lera att befintliga roller har rätt behörigheter för din miljö.
    > 
    > - Ett objekt är sökbart i mappar utanför en användares säkerhets omfattning om den användaren delar en säkerhets omfattning med den person som skapade objektet. <!--5602690-->

## <a name="configure-collections-to-manage-security"></a><a name="BKMK_ConfigColl"></a> Konfigurera samlingar för att hantera säkerhet

 Det finns inga procedurer för att konfigurera samlingar för rollbaserad administration. Samlingar har ingen rollbaserad administrations konfiguration. I stället tilldelar du samlingar till en administrativ användare när du konfigurerar den administrativa användaren. De säkerhets åtgärder för samlingar som aktive ras i de användardefinierade säkerhets rollerna avgör vilka behörigheter en administrativ användare har för samlingar och samlings resurser (samlings medlemmar).  

 När en administrativ användare har behörighet till en samling, har användaren också behörighet till samlingar som är begränsade till denna samling. Som exempel använder din organisation en samling som heter alla skriv bord. Det finns också en samling med namnet alla Nordamerika skriv bord som är begränsade till samlingen Alla skriv bord. Om en administrativ användare har behörighet till Alla skrivbordsdatorer, har användaren också behörighet till samlingen Alla europeiska skrivbordsdatorer.

 Dessutom kan en administrativ användare inte använda behörigheten **ta bort** eller **ändra** för en samling som tilldelas direkt till dem. Men de kan använda dessa behörigheter på samlingarna som är begränsade till den samlingen. I föregående exempel kan den administrativa användaren ta bort eller ändra samlingen Alla Nordamerika Station ära datorer, men de kan inte ta bort eller ändra samlingen Alla Skriv bords datorer.  

## <a name="create-a-new-administrative-user"></a><a name="BKMK_Create_AdminUser"></a> Skapa en ny administrativ användare

 Om du vill ge enskilda personer eller medlemmar i en säkerhets grupp åtkomst för att hantera Configuration Manager skapar du en administrativ användare i Configuration Manager och anger Windows-kontot för användaren eller användar gruppen. Varje administrativ användare i Configuration Manager måste tilldelas minst en säkerhets roll och en säkerhets omfattning. Du kan även tilldela samlingar, om du vill begränsa den administrativa omfattningen för en administrativ användare.  

 Använd följande procedurer för att skapa nya administrativa användare.  

### <a name="to-create-a-new-administrative-user"></a>Skapa en ny administrativ användare  

1. Välj **Administration**i Configuration Manager-konsolen.  
2. I arbets ytan **Administration** expanderar du **säkerhet**och väljer sedan **administrativa användare**.  
3. På fliken **Start** går du till gruppen **skapa** och väljer **Lägg till användare eller grupp**.  
4. Välj **Bläddra**och välj sedan det användar konto eller den grupp som ska användas för den nya administrativa användaren.  

    > [!NOTE]  
    > För konsolbaserad administration kan endast domänanvändare eller säkerhetsgrupper anges som administrativa användare.

5. För **associerade säkerhets roller**väljer du **Lägg till** för att öppna en lista över tillgängliga säkerhets roller, markerar kryss rutan för en eller flera säkerhets roller och väljer sedan **OK**.  

6. Välj något av följande två alternativ för att definiera beteendet för skydds bara objekt för den nya användaren:  

    - **Alla instanser av objekten som är relaterade till de tilldelade säkerhets rollerna**: med det här alternativet associeras den administrativa användaren med samlingarna **alla** säkerhets omfattningar och samlingarna **alla system** och **alla användare och användar grupper** . De säkerhetsroller som användaren tilldelas avgör användarens åtkomst till objekt. Nya objekt som den administrativa användaren skapar tilldelas säkerhetsomfattningen **Standard** .  

    - **Endast de objekt instanser som tilldelats de angivna säkerhets omfattningarna och samlingarna**: som standard associeras den administrativa användaren med **standard** säkerhets omfattningen och samlingarna **alla system** och **alla användare och användar grupper** . Säkerhetsomfattningarna och samlingarna begränsas dock till dem som ingår i det konto som används när den nya administrativa användaren skapas. Alternativet kan användas för att anpassa den administrativa användarens administrativa omfattning genom att lägga till och ta bort säkerhetsomfattningar och samlingar.  

    > [!IMPORTANT]  
    > Med föregående alternativ associeras varje tilldelad säkerhets omfattning och samling till varje säkerhets roll som tilldelas den administrativa användaren. Du kan använda ett tredje alternativ, **associera tilldelade säkerhets roller med specifika säkerhets omfattningar och samlingar**, för att associera enskilda säkerhets roller med specifika säkerhets omfattningar och samlingar. Det tredje alternativet blir tillgängligt efter att du har skapat den nya administrativa användaren, när du ändrar användaren.  

7. Utför följande, beroende på vad du har valt i steg 6:  

    - Om du har valt **alla instanser av objekten som är relaterade till de tilldelade säkerhets rollerna**väljer du **OK** för att slutföra den här proceduren.  

    - Om du bara har valt **de objekt instanser som tilldelats de angivna säkerhets omfattningarna och samlingarna**, kan du välja **Lägg till** för att välja ytterligare samlingar och säkerhets omfattningar. Eller Välj ett eller flera objekt i listan och ta bort dem genom att välja **ta bort** . Klicka på **OK** för att slutföra den här proceduren.  

## <a name="modify-the-administrative-scope-of-an-administrative-user"></a><a name="BKMK_ModAdminUser"></a>Ändra den administrativa användarens administrativa omfattning

 Du kan ändra den administrativa användarens administrativa omfattning genom att lägga till eller ta bort säkerhetsroller, säkerhetsomfattningar och samlingar som är associerade med användaren. Varje administrativ användare måste vara associerad med minst en säkerhetsroll och en säkerhetsomfattning. Du kanske måste tilldela en eller flera samlingar till användarens administrativa omfattning. De flesta säkerhets roller samverkar med samlingar och fungerar inte som de ska utan en tilldelad samling.  

 Om du ändrar en administrativ användare kan du ändra hur skyddsbara objekt ska associeras med de tilldelade säkerhetsrollerna. Du kan välja följande tre beteenden:  

- **Alla instanser av objekten som är relaterade till de tilldelade säkerhets rollerna**: med det här alternativet associeras den administrativa användaren med samlings området **alla** **system** och **alla användare och användar grupper** . De säkerhetsroller som användaren tilldelas avgör användarens åtkomst till objekt.  

- **Endast de objekt instanser som tilldelats de angivna säkerhets omfattningarna och samlingarna**: med det här alternativet associeras den administrativa användaren med samma säkerhets omfattningar och samlingar som är kopplade till det konto som du använder för att konfigurera den administrativa användaren. Alternativet kan användas för att anpassa användarens administrativa omfattning genom att lägga till och ta bort säkerhetsroller och samlingar.  

- **Associera tilldelade säkerhets roller med specifika säkerhets omfattningar och samlingar: med**det här alternativet kan du skapa specifika associationer mellan enskilda säkerhets roller och specifika säkerhets omfattningar och samlingar för användaren.  

    > [!NOTE]  
    > Alternativet är endast tillgängligt när du ändrar egenskaper för en befintlig administrativ användare.  

Den aktuella konfigurationen för beteenden för skyddsbara objekt, avgör vilken process som används för att tilldela fler säkerhetsroller. Använd följande procedurer, som baseras på olika alternativ för skyddsbara objekt, för att hantera en administrativ användare.  

Använd följande procedur för att visa och hantera konfigurationen för skydds bara objekt för en administrativ användare.  

### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Visa och hantera beteenden för skyddsbara objekt för en administrativ användare  

1. Välj **Administration**i Configuration Manager-konsolen.  
2. I arbets ytan **Administration** expanderar du **säkerhet**och väljer sedan **administrativa användare**.  
3. Välj den administrativa användare som du vill ändra.  
4. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  
5. Välj fliken **säkerhets omfattningar** för att visa den aktuella konfigurationen för skydds bara objekt för den här administrativa användaren.  
6. Om du vill ändra ett beteende väljer du ett nytt alternativ för skyddsbara objekt. När du har ändrat den här konfigurationen kan du se lämplig procedur för att konfigurera säkerhets omfattningar och samlingar och säkerhets roller för den administrativa användaren.  
7. Klicka på **OK** för att slutföra proceduren.  

Använd följande procedur om du vill ändra en administrativ användare som har beteendet för skydds bara objekt inställt på **alla instanser av objekten som är relaterade till de tilldelade säkerhets rollerna**.  

### <a name="for-option-all-instances-of-the-objects-that-are-related-to-the-assigned-security-roles"></a>For-alternativ: alla instanser av objekten som är relaterade till de tilldelade säkerhets rollerna  

1. Välj **Administration**i Configuration Manager-konsolen.  
2. I arbets ytan **Administration** expanderar du **säkerhet**och väljer sedan **administrativa användare**.  
3. Välj den administrativa användare som du vill ändra.  
4. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  
5. Välj fliken **säkerhets omfattningar** för att bekräfta att den administrativa användaren är konfigurerad för **alla instanser av objekten som är relaterade till de tilldelade säkerhets rollerna**.  
6. Om du vill ändra tilldelade säkerhets roller klickar du på fliken **säkerhets roller** .  

    - Om du vill tilldela den här administrativa användaren fler säkerhets roller väljer du **Lägg till**, markerar kryss rutan för varje ytterligare säkerhets roll som du vill tilldela och väljer sedan **OK**.  
    - Om du vill ta bort säkerhets roller väljer du en eller flera säkerhets roller i listan och väljer sedan **ta bort**.

7. Om du vill ändra beteendet för skydds bara objekt klickar du på fliken **säkerhets omfattningar** och väljer ett nytt alternativ för beteendet för skydds bara objekt. När du har ändrat den här konfigurationen kan du se lämplig procedur för att konfigurera säkerhets omfattningar och samlingar och säkerhets roller för den administrativa användaren.  

    > [!NOTE]  
    > När beteendet för det skydd bara objektet är inställt på **alla instanser av objekten som är relaterade till de tilldelade säkerhets rollerna**kan du inte lägga till eller ta bort vissa säkerhets omfattningar och samlingar.  

8. Klicka på **OK** för att slutföra den här proceduren.  

Använd följande procedur för att ändra en administrativ användare som har beteendet för skydds bara objekt inställt på **endast de objekt instanser som tilldelats de angivna säkerhets omfattningarna och samlingarna**.  

### <a name="for-option-only-the-instances-of-objects-that-are-assigned-to-the-specified-security-scopes-and-collections"></a>For-alternativ: endast de objekt instanser som tilldelats de angivna säkerhets omfattningarna och samlingarna  

1. Välj **Administration**i Configuration Manager-konsolen.  
2. I arbets ytan **Administration** expanderar du **säkerhet**och väljer sedan **administrativa användare**.  
3. Välj den administrativa användare som du vill ändra.  
4. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  
5. Välj fliken **säkerhets omfattningar** för att bekräfta att användaren är konfigurerad **enbart för de objekt instanser som tilldelats de angivna säkerhets omfattningarna och samlingarna**.  
6. Om du vill ändra tilldelade säkerhets roller klickar du på fliken **säkerhets roller** .  

    - Om du vill tilldela den här användaren ytterligare säkerhets roller väljer du **Lägg till**, markerar kryss rutan för varje ytterligare säkerhets roll som du vill tilldela och väljer sedan **OK**.  
    - Om du vill ta bort säkerhets roller väljer du en eller flera säkerhets roller i listan och väljer sedan **ta bort**.  
7. Om du vill ändra säkerhets omfattningar och samlingar som är associerade med säkerhets roller, klickar du på fliken **säkerhets omfattningar** .  

    - Om du vill associera nya säkerhets omfattningar eller samlingar med alla säkerhets roller som är kopplade till den här administrativa användaren, väljer du **Lägg till** och väljer något av de fyra alternativen. Om du väljer **säkerhets omfattning** eller **samling**markerar du kryss rutan för ett eller flera objekt för att slutföra markeringen och väljer sedan **OK**.  
    - Om du vill ta bort en säkerhets omfattning eller samling väljer du objektet och väljer sedan **ta bort**.

8. Klicka på **OK** för att slutföra den här proceduren.  

Använd följande procedur för att ändra en administrativ användare som har beteendet för skydds bara objekt inställda på att **associera tilldelade säkerhets roller med vissa säkerhets omfattningar och samlingar**.  

### <a name="for-option-associate-assigned-security-roles-with-specific-security-scopes-and-collections"></a>För alternativ: associera tilldelade säkerhets roller med vissa säkerhets omfattningar och samlingar  

1. Välj **Administration**i Configuration Manager-konsolen.  
2. I arbets ytan **Administration** expanderar du **säkerhet**och väljer sedan **administrativa användare**.  
3. Välj den administrativa användare som du vill ändra.  
4. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  
5. Välj fliken **säkerhets omfattningar** för att bekräfta att den administrativa användaren är konfigurerad för att **associera tilldelade säkerhets roller med vissa säkerhets omfattningar och samlingar**.  
6. Om du vill ändra tilldelade säkerhets roller klickar du på fliken **säkerhets roller** .  

    - Om du vill tilldela den här administrativa användaren fler säkerhets roller väljer du **Lägg till**. I dialog rutan **Lägg till säkerhets roll** markerar du en eller flera tillgängliga säkerhets roller, väljer **Lägg till**och väljer sedan en objekt typ som ska associeras med de valda säkerhets rollerna. Om du väljer **säkerhets omfattning** eller **samling**markerar du kryss rutan för ett eller flera objekt för att slutföra markeringen och väljer sedan **OK**.  

        > [!NOTE]  
        > Du måste konfigurera minst en säkerhetsomfattning innan de valda säkerhetsrollerna kan tilldelas den administrativa användaren. Den säkerhetsomfattning och samling som du konfigurerar associeras med var och en av de valda säkerhetsrollerna, om du väljer flera säkerhetsroller.  

    - Om du vill ta bort säkerhets roller väljer du en eller flera säkerhets roller i listan och väljer sedan **ta bort**.  

7. Om du vill ändra säkerhets omfattningar och samlingar som är associerade med en speciell säkerhets roll, klickar du på fliken **säkerhets omfattningar** , väljer säkerhets rollen och väljer sedan **Redigera**.  

    - Om du vill associera nya objekt med den här säkerhets rollen väljer du **Lägg till**och väljer sedan en objekt typ som ska associeras med de valda säkerhets rollerna. Om du väljer **säkerhets omfattning** eller **samling**markerar du kryss rutan för ett eller flera objekt för att slutföra markeringen och väljer sedan **OK**.  

        > [!NOTE]  
        > Du måste konfigurera minst en säkerhets omfattning.  

    - Om du vill ta bort en säkerhets omfattning eller samling som är associerad med den här säkerhets rollen markerar du objektet och väljer sedan **ta bort**.  

    - När du är färdig med att ändra de associerade objekten väljer du **OK**.  

8. Klicka på **OK** för att slutföra den här proceduren.  

    > [!CAUTION]  
    > Om en säkerhetsroll ger administrativa användare behörighet att distribuera samlingar, kan de administrativa användarna distribuera objekt från alla säkerhetsomfattningar där de har **läsbehörighet** för objekt, även om en sådan säkerhetsomfattning är associerad med en annan säkerhetsroll.  

## <a name="next-steps"></a>Nästa steg

[Konton som används i Configuration Manager](../../../plan-design/hierarchy/accounts.md)
