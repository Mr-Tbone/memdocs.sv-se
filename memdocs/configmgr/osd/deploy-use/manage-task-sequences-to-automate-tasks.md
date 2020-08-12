---
title: Hantera aktivitetssekvenser
titleSuffix: Configuration Manager
description: Skapa, redigera, distribuera, importera och exportera aktivitetssekvenser för att hantera dem och automatisera aktiviteter i din miljö.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 609f5d010018fa23dd4a533b2f1079f07d8c2283
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125073"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>Hantera aktivitetssekvenser för att automatisera uppgifter

*Gäller för: Configuration Manager (aktuell gren)*

Använd aktivitetssekvenser för att automatisera steg i din Configuration Managers miljö. De här stegen kan distribuera en operativ system avbildning till en måldator, bygga och avbilda en operativ system avbildning från en uppsättning OS-installationsfiler och avbilda och återställa information om användar tillstånd. Aktivitetssekvenser finns i Configuration Manager-konsolen. I arbets ytan **program bibliotek** expanderar du **operativ system**och väljer **aktivitetssekvenser**. Noden **aktivitetssekvenser** , inklusive undermappar som du skapar, replikeras i Configuration Manager hierarkin. Planerings information finns i [planerings överväganden för automatisering av uppgifter](../plan-design/planning-considerations-for-automating-tasks.md).  

## <a name="create"></a><a name="BKMK_CreateTaskSequence"></a>Fram

Aktivitetssekvenser skapas med hjälp av guiden Skapa aktivitetssekvens. I den här guiden skapas följande typer av aktivitetssekvenser:  

- [Aktivitetssekvens för att installera ett operativ system](create-a-task-sequence-to-install-an-operating-system.md): skapa stegen för att installera ett operativ system. Den innehåller också alternativ för att migrera användar data, inkludera program uppdateringar och installera program.

- [Aktivitetssekvens för att uppgradera ett operativ system](create-a-task-sequence-to-upgrade-an-operating-system.md): skapa stegen för att uppgradera ett operativ system. Den innehåller också alternativ för att inkludera program uppdateringar och installera program.

- [Aktivitetssekvens för att avbilda ett operativ system](create-a-task-sequence-to-capture-an-operating-system.md): skapa stegen för att bygga och avbilda ett operativ system från en referens dator. Du kan inkludera program uppdateringar och installera program på referens datorn innan du fångar avbildningen.

- [Aktivitetssekvens för att avbilda och återställa användar tillstånd](create-a-task-sequence-to-capture-and-restore-user-state.md): Lägg till steg i en befintlig aktivitetssekvens för att avbilda och återställa användar tillstånds data.

- [Anpassad aktivitetssekvens](create-a-custom-task-sequence.md): den här typen lägger inte till några steg i aktivitetssekvensen. När du har skapat aktivitetssekvensen redigerar du den och lägger till steg.

## <a name="edit"></a><a name="BKMK_ModifyTaskSequence"></a>Ras  

Ändra en aktivitetssekvens genom att lägga till eller ta bort steg, lägga till eller ta bort grupper eller genom att ändra ordningen på stegen. Mer information finns i [använda redigeraren för aktivitetssekvens](../understand/task-sequence-editor.md).

## <a name="reduce-the-size-of-task-sequence-policy"></a><a name="bkmk_policysize"></a>Minska storleken på aktivitetssekvensen

<!--6982275-->
När storleken på aktivitetssekvensen överskrider 32 MB, kan klienten inte bearbeta den stora principen. Klienten kan sedan inte köra distribution av aktivitetssekvensen.

Storleken på aktivitetssekvensen som lagras i plats databasen är mindre, men kan fortfarande orsaka problem om den är för stor. När klienten bearbetar hela aktivitetssekvensen kan den utökade storleken orsaka problem över 32 MB.

Från och med version 2006 kan du använda [Management Insights](../../core/servers/manage/management-insights.md#operating-system-deployment)för att kontrol lera om det finns 32-MB på klienternas princip storlek för aktivitetssekvens.

Utför följande åtgärder för att minska den övergripande storleken på principen för en aktivitetssekvensdistribution:

- Separera funktionella segment till underordnade aktivitetssekvenser och Använd steget [Kör aktivitetssekvens](../understand/task-sequence-steps.md#child-task-sequence) . Varje aktivitetssekvens har en separat gräns på 32 MB för princip storleken.

    > [!NOTE]
    > Att minska det totala antalet steg och grupper i en aktivitetssekvens har minimal inverkan på princip storleken. Varje steg är vanligt vis ett par KB i principen. Att flytta grupper av steg till en underordnad aktivitetssekvens är mer påverkan.

- Minska antalet program uppdateringar i distributioner till samma samling som aktivitetssekvensen.

- I stället för att ange ett skript i steget [kör PowerShell-skript](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript) kan du referera till det via ett paket.

- Det finns en gräns på 8 KB för storleken på aktivitetssekvensen när den körs. Granska användningen av variabler för anpassad aktivitetssekvens, som också kan bidra till princip storleken.

- Som en sista utväg delar du en komplex, dynamisk aktivitetssekvens i separata aktivitetssekvenser med olika distributioner till olika samlingar.

## <a name="software-center-properties"></a><a name="bkmk_prop-general"></a>Egenskaper för Software Center

Använd följande procedur för att konfigurera information om aktivitetssekvensen som visas i Software Center. Informationen är endast för information.  

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj **aktivitetssekvenser**.  

2. Välj den aktivitetssekvens som du vill redigera och välj **Egenskaper**.  

3. På fliken **Allmänt** finns följande inställningar för Software Center:  

    - **Omstart krävs**: låter användaren veta om en omstart krävs under installationen.  

    - **Hämtnings storlek (MB)**: anger hur många megabyte som visas i Software Center för aktivitetssekvensen.  

    - **Beräknad körnings tid (minuter)**: anger den uppskattade körnings tiden i minuter som visas i Software Center för aktivitetssekvensen.  

## <a name="advanced-settings"></a><a name="bkmk_prop-advanced"></a>Avancerade inställningar

Använd följande procedur för att konfigurera hur aktivitetssekvensen ska användas på den Configuration Manager klienten.  

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj **aktivitetssekvenser**.  

2. Välj den aktivitetssekvens som du vill redigera och välj **Egenskaper**.  

3. Följande inställningar är tillgängliga på fliken **Avancerat** :  

    - **Kör ett annat program först**: Välj det här alternativet om du vill köra ett program i ett annat paket innan aktivitetssekvensen körs. Den här kryssrutan är avmarkerad som standard. Du behöver inte separat distribuera det program som du anger för att köra först.  

        > [!IMPORTANT]
        > Den här inställningen gäller endast för aktivitetssekvenser som körs i det fullständiga operativ systemet. Om du startar aktivitetssekvensen med hjälp av PXE eller start medium ignorerar Configuration Manager den här inställningen.  

        - **Paket**: Bläddra efter det paket som innehåller programmet som ska köras före aktivitetssekvensen.  

        - **Program**: Välj det program som ska köras före den här aktivitetssekvensen.  

        > [!NOTE]  
        > Om det valda programmet inte kan köras på en klient, körs inte aktivitetssekvensen. Om det valda programmet körs utan problem körs det inte igen, även om aktivitetssekvensen körs på nytt på samma klient.  

    - **Förhindra aviseringar om aktivitetssekvenser**: Välj det här alternativet om du vill dölja den **nya program varan** . popup-meddelande är tillgängligt. Du ser fortfarande ikonen **ny program vara** från Software Center i meddelande fältet. Som standard är det här alternativet inaktiverat.  

    - **Inaktivera denna aktivitetssekvens på datorer där den distribueras**: om du väljer det här alternativet inaktive ras Configuration Manager tillfälligt alla distributioner som innehåller den här aktivitetssekvensen. Den tar också bort aktivitetssekvensen från listan över distributioner som är tillgängliga för körning. Aktivitetssekvensen körs inte förrän du aktiverar den. Som standard är det här alternativet inaktiverat.  

    - **Högsta tillåtna körnings tid**: anger den längsta tid i minuter som du förväntar dig att aktivitetssekvensen ska köras på mål datorn. Använd ett heltal som är lika med eller större än noll. Som standard är det här värdet 120 minuter.  

        > [!IMPORTANT]  
        > Om du använder underhålls perioder för den samling som du distribuerar den här aktivitetssekvensen till kan en konflikt uppstå om den **längsta tillåtna körnings tiden** är längre än det schemalagda underhålls fönstret. Om du ställer in den maximala körnings tiden på **0**startar aktivitetssekvensen under underhålls perioden. Den fortsätter att köras tills den har slutförts eller Miss lyckas när underhålls fönstret har stängts. Därför kan aktivitetssekvenser med en maximal körnings tid som är inställd på **0** köras förbi slutet av deras underhålls fönster. Om du ställer in den maximala körnings tiden på en viss period (inte noll) som överskrider längden på alla tillgängliga underhålls fönster, körs inte aktivitetssekvensen. Mer information finns i [använda underhålls](../../core/clients/manage/collections/use-maintenance-windows.md)perioder.  

        Om du ställer in värdet som **0**, utvärderar Configuration Manager den längsta tillåtna körnings tiden som **12** timmar (720 minuter) för att övervaka förloppet. Aktivitetssekvensen startar dock så länge nedräknings perioden inte överskrider värdet för underhålls perioden.  

        > [!NOTE]
        > När den når den maximala kör tiden, om du inte tillåter att användare interagerar med en begärd distribution, stoppas Configuration Manager aktivitetssekvensen. Om själva aktivitetssekvensen inte är stoppad Configuration Manager stoppa övervakningen av aktivitetssekvensen när den når den maximalt tillåtna körnings tiden.

    - **Använd en start avbildning**: Använd den valda start avbildningen när aktivitetssekvensen körs. Välj **Bläddra** för att välja en annan start avbildning. Avmarkera det här alternativet om du vill inaktivera användningen av den valda start avbildningen när aktivitetssekvensen körs.  

    - **Den här aktivitetssekvensen kan köras på valfri plattform**: om du väljer det här alternativet kontrollerar Configuration Manager inte mål datorns plattforms typ när aktivitetssekvensen körs. Det här alternativet är markerat som standard.  

    - Aktivitetssekvensen **kan bara köras på de angivna klient plattformarna**: det här alternativet anger de processorer, OS-versioner och Service Pack som aktivitetssekvensen kan köras på. När du väljer det här alternativet väljer du minst en plattform i listan. Inga plattformar är markerade som standard. Configuration Manager använder den här informationen när utvärderas vilka mål datorer i en samling som tar emot den distribuerade aktivitetssekvensen.  

        > [!NOTE]  
        > När du kör en aktivitetssekvens från startmedia eller PXE ignorerar Configuration Manager det här alternativet. Aktivitetssekvensen körs som om alternativet **det här programmet kan köras på vilken plattform som helst** är markerat.  

## <a name="high-impact-settings"></a>Inställningar med hög effekt

Konfigurera en aktivitetssekvens som hög påverkan och anpassa de meddelanden som användarna får när de kör aktivitetssekvensen.

> [!WARNING]
> Om du använder PXE-distributioner och konfigurerar enhets maskin vara med nätverkskortet som den första startenheten kan de här enheterna automatiskt starta en aktivitetssekvens för operativ system distribution utan användar interaktion. Distributions verifiering hanterar inte den här konfigurationen. Även om den här konfigurationen kan förenkla processen och minska användar interaktionen, medför enheten större risk för oavsiktlig återavbildning.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Ange en aktivitetssekvens som en aktivitet med hög effekt

Använd följande procedur för att ange en aktivitetssekvens som hög påverkan.

> [!NOTE]  
> En aktivitetssekvens som uppfyller vissa villkor definieras automatiskt som hög påverkan. Mer information finns i [Hantera distributioner med hög risk](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj **aktivitetssekvenser**.  

2. Välj den aktivitetssekvens som du vill redigera och välj **Egenskaper**.  

3. På fliken **användar meddelande** väljer du **det här är en aktivitetssekvens med hög effekt**.  

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Skapa ett anpassat meddelande för distributioner med hög risk

Använd följande procedur för att skapa ett anpassat meddelande för distributioner med hög effekt.

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj **aktivitetssekvenser**.  

2. Välj den aktivitetssekvens som du vill redigera och välj **Egenskaper**.  

3. På fliken **användar meddelande** väljer du **Använd anpassad text**.  

    > [!NOTE]
    > Du kan bara ange meddelande text när du väljer alternativet, **det här är en aktivitetssekvens med hög påverkan**.  

4. Konfigurera följande inställningar:  

    > [!Note]  
    > Varje text ruta har en övre gräns på 255 tecken.  

    - **Rubrik text för användar meddelande**: anger den blå text som visas i användar meddelandet för Software Center. Till exempel innehåller det här avsnittet "bekräfta att du vill uppgradera operativ systemet på den här datorn" i standard användar meddelandet ".  

    - **Meddelande text för användar meddelande**: det finns tre text rutor som innehåller bröd texten i det anpassade meddelandet. Alla text rutor kräver att du lägger till text.  

        - Första text rutan: anger huvud texten i texten, vanligt vis med instruktioner för användaren. I det här avsnittet innehåller till exempel det här avsnittet "uppgradering av operativ systemet tar tid och datorn kanske måste startas om flera gånger."  

        - Andra text rutan: anger den fetstilta texten under textens huvuddel. I det här avsnittet innehåller till exempel det här avsnittet "den här uppgraderings uppdateringen installerar det nya operativ systemet och migrerar automatiskt dina appar, data och inställningar."  

        - Tredje text rutan: anger den sista text raden under fet text. I det här avsnittet innehåller till exempel det här avsnittet "Klicka på installera för att börja. Annars klickar du på Avbryt. "  

#### <a name="example"></a>Exempel

Anta att du konfigurerar följande anpassade meddelande i egenskaper.

![Fliken anpassad användar avisering i egenskaper för aktivitetssekvens](../media/user-notification.png)

Följande meddelande visas när slutanvändaren öppnar installationen från Software Center.

![Anpassat meddelande om aktivitetssekvenser till slutanvändaren från Software Center](../media/user-notification-enduser.png)

## <a name="performance-improvements-for-power-plans"></a><a name="bkmk_perf"></a>Prestanda förbättringar för energi scheman

<!--3555926-->

Från och med version 1910 kan du nu köra en aktivitetssekvens med hög prestanda energi schema. Det här alternativet förbättrar den övergripande hastigheten i aktivitetssekvensen. Det konfigurerar Windows så att det använder sitt inbyggda energi schema för hög prestanda, vilket ger högsta möjliga prestanda vid kostnad av större strömförbrukning. Det här alternativet är aktiverat som standard för nya aktivitetssekvenser.

När aktivitetssekvensen startar, i de flesta fall, registreras det för närvarande aktiverade energi schemat. Det växlar sedan till det aktiva energischemat till Windows standard plan för **hög prestanda** . Om aktivitetssekvensen startar om datorn upprepas processen. I slutet av aktivitetssekvensen återställs energischemat till det lagrade värdet. Den här funktionen fungerar både i Windows och Windows PE, men påverkar inte virtuella datorer.

- Om aktivitetssekvensen startar i Windows PE registrerar aktivitetssekvensen inte det aktuella aktiverade energischemat för senare åter användning.

- En aktivitetssekvens för operativ system distribution som återställer avbildningen av datorn (rensning och belastning) bevarar inte energi schema inställningen för det gamla operativ systemet. I slutet av aktivitetssekvensen återställer den **Standardbalanserade** energi planen.

> [!Important]
> Om du vill dra nytta av denna nya Configuration Manager-funktion, när du har uppdaterat platsen, uppdaterar du klienterna till den senaste versionen. Uppdatera även start avbildningar för att inkludera de senaste klient komponenterna. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** . Expandera **operativ system**och välj noden **aktivitetssekvenser** .

1. Skapa eller Välj en befintlig aktivitetssekvens och välj sedan **Egenskaper**.

1. Växla till fliken **prestanda** .

1. Aktivera alternativet att **köra som hög prestanda energi schema**.

> [!Warning]
> Var försiktig med den här inställningen för maskin vara med låg prestanda. Att köra intensiva system åtgärder under en längre tids period kan begränsa maskin vara med låg slut. Kontakta maskin varu tillverkaren om du vill ha mer information.

### <a name="known-issue"></a>Kända problem

<!-- 5554928 -->

När du ändrar inställningar i egenskaper för aktivitetssekvens uppdateras vanligt vis alla befintliga distributioner. När du ändrar den här prestanda inställningen i egenskaper för aktivitetssekvens påverkas inte eventuella befintliga distributioner av aktivitetssekvensen. Om du vill aktivera eller inaktivera den här inställningen för hög prestanda skapar du en ny aktivitetssekvensdistribution.
<!-- MEMDocs#437, SCCMDocs#2107 -->

## <a name="distribute-referenced-content"></a><a name="BKMK_DistributeTS"></a>Distribuera refererat innehåll  

Innan klienterna kör en aktivitetssekvens som refererar till innehåll distribuerar du innehållet till distributions platser. Du kan när som helst välja aktivitetssekvensen och distribuera innehållet för att generera en ny lista över referenspaket för distribution. Om du gör ändringar i aktivitetssekvensen med uppdaterat innehåll måste du distribuera om innehållet innan det är tillgängligt för klienter. Använd följande procedur för att distribuera det innehåll som refereras av en aktivitetssekvens.  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>Process för att distribuera refererat innehåll till distributions platser  

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj noden **aktivitetssekvenser** .  

2. I listan **Aktivitetssekvens** väljer du den aktivitetssekvens som du vill distribuera.  

3. På fliken **Start** i menyfliksområdet väljer du **distribuera innehåll**i gruppen **distribution** . Den här åtgärden startar guiden Distribuera innehåll.  

4. På sidan **Allmänt** kontrollerar du att den korrekta aktivitetssekvensen har valts för distribution.  

5. På sidan **innehåll** kontrollerar du innehållet som ska distribueras, till exempel den Start avbildning som refereras av aktivitetssekvensen.  

6. På sidan **innehålls mål** anger du de samlingar, distributions platser eller distributions plats grupper där du vill distribuera innehållet i aktivitetssekvensen.  

    > [!IMPORTANT]  
    > Om aktivitetssekvensen som du har valt refererar till innehåll som redan har distribuerats till en viss distributions plats, visar inte guiden distributions platsen.  

7. Slutför guiden.  

Du kan också förinstallera innehållet som refereras i aktivitetssekvensen. Configuration Manager skapar en komprimerad, förinstallerad innehålls fil som innehåller filer, associerade beroenden och associerade metadata för det innehåll som du väljer. Sedan importerar du innehållet manuellt på en plats Server, sekundär plats eller distributions plats. Mer information om hur du förinstallerar innehållsfiler finns i [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

## <a name="deploy"></a><a name="BKMK_DeployTS"></a>Distribuera  

Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md).

## <a name="export-and-import"></a><a name="BKMK_ExportImport"></a>Exportera och importera  

Exportera och importera aktivitetssekvenser med eller utan relaterade objekt. Det här refererade innehållet innehåller följande objekt:  

- Operativsystemavbildningar  
- Startavbildningar  
- Paket som klient installations paketet  
- Drivrutinspaket  
- Program med beroenden  

Tänk på följande när du exporterar och importerar aktivitetssekvenser:  

- Configuration Manager exporterar inte lösen ord i aktivitetssekvensen. Om du exporterar och importerar en aktivitetssekvens som innehåller lösen ord redigerar du den importerade aktivitetssekvensen för att ange eventuella lösen ord igen. Granska följande steg som kan innehålla ett lösen ord:  

  - [Anslut till domän eller arbetsgrupp](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  
  - [Anslut till nätverksmappen](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  
  - [Kör kommando rad](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- När du exporterar en aktivitetssekvens med steget **Ange dynamiska variabler** exporterar Configuration Manager inte värden för variabler som du konfigurerar med inställningen för **hemligt värde** . Ange värdena för dessa variabler igen efter att du har importerat aktivitetssekvensen.  

- När du har flera primära platser kan du importera aktivitetssekvenser på den centrala administrations platsen.  

### <a name="process-to-export-task-sequences"></a>Process för att exportera aktivitetssekvenser  

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj noden **aktivitetssekvenser** .  

2. I listan **Aktivitetssekvens** väljer du den aktivitetssekvens som du vill exportera. Om du väljer mer än en aktivitetssekvens lagras alla i en export fil.  

3. På fliken **Start** i menyfliksområdet i gruppen **aktivitetssekvens** väljer du **Exportera**. Den här åtgärden startar guiden Exportera aktivitetssekvens.  

4. På sidan **Allmänt** anger du följande inställningar:  

    - **Fil**: Ange plats och namn för export filen. Om du anger filnamnet direkt ska du se till att inkludera .zip-tillägget i filnamnet. Om du bläddrar efter exportfilen läggs filtillägget till automatiskt.  

    - Om du inte vill exportera beroenden för aktivitetssekvenser avmarkerar du alternativet för att **Exportera alla beroenden för aktivitetssekvenser**. Som standard utförs en sökning efter alla relaterade objekt som sedan exporteras med aktivitetssekvensen. Dessa beroenden omfattar alla program.  

    - Om du inte vill kopiera innehållet från paket källan till export platsen avmarkerar du alternativet för att **Exportera allt innehåll för de valda aktivitetssekvenserna och beroendena**. Om du väljer det här alternativet använder guiden Importera aktivitetssekvens import Sök vägen som den nya paket käll platsen.  

    - **Administratörs kommentarer**: Lägg till en beskrivning av de aktivitetssekvenser som ska exporteras.  

5. Slutför guiden.  

Följande utdatafiler skapas med hjälp av guiden:  

- Om du inte exporterar innehåll: en. zip-fil.  

- Om du exporterar innehåll: en .zip-fil och en mapp med namnet *export*_files, där *export* är namnet på .zip-filen som innehåller det exporterade innehållet.  

Om du inkluderar innehåll när du exporterar en aktivitetssekvens måste du kopiera. zip-filen och mappen *exportera*_files, annars Miss lyckas importen.  

### <a name="process-to-import-task-sequences"></a>Process för att importera aktivitetssekvenser  

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj noden **aktivitetssekvenser** .  

2. På fliken **Start** i menyfliksområdet väljer du **Importera aktivitetssekvens**i gruppen **skapa** . Den här åtgärden startar guiden Importera aktivitetssekvens.  

3. På sidan **Allmänt** i menyfliksområdet anger du den exporterade. zip-filen.  

4. På sidan **Filinnehåll** väljer du vilken åtgärd som ska utföras för vart och ett av de objekt som du importerar. Den här sidan visar alla objekt som Configuration Manager har identifierat för import.  

    - Om objektet aldrig har importerats väljer du **Skapa nytt**.  

    - Om objektet i stället har importerats tidigare väljer du en av följande åtgärder:  

        - **Ignorera dubblett** (standard): den här åtgärden importerar inte objektet. I stället länkas det befintliga objektet till aktivitetssekvensen av guiden.  

        - **Skriv över**: Den här åtgärden skriver över det befintliga objektet med det importerade objektet. För program kan du lägga till en revidering som uppdaterar det befintliga programmet eller skapar ett nytt program.  

5. Slutför guiden.  

När du har importerat aktivitetssekvensen redigerar du den och anger eventuella lösenord som ingick i den ursprungliga aktivitetssekvensen. Av säkerhets skäl exporteras inte lösen ord.  

## <a name="return-to-previous-page-on-failure"></a>Gå tillbaka till föregående sida vid ett haverit

När du kör en aktivitetssekvens och det uppstår ett problem kan du gå tillbaka till en föregående sida i guiden aktivitetssekvens. I tidigare versioner av Configuration Manager var du tvungen att starta om aktivitetssekvensen när det uppstod ett problem. Använd knappen **föregående** i följande scenarier:

- När en dator startas i Windows PE kan start dialog rutan för aktivitetssekvens visas innan aktivitetssekvensen är tillgänglig. När du väljer nästa i det här scenariot visas den sista sidan i aktivitetssekvensen med ett meddelande om att det inte finns några tillgängliga aktivitetssekvenser. Nu kan du välja **föregående** för att söka igen efter tillgängliga aktivitetssekvenser. Du kan upprepa den här processen tills aktivitetssekvensen är tillgänglig.  

- När du kör en aktivitetssekvens, men beroende innehålls paket inte är tillgängliga än på distributions platser, Miss lyckas aktivitetssekvensen. Om innehållet som saknas har distribuerats ännu distribuerar du det nu. Eller vänta tills innehållet är tillgängligt på distributions platserna. Välj sedan **föregående** om du vill att aktivitetssekvensen ska sökas igen för innehållet.

## <a name="collection-and-device-variables"></a><a name="BKMK_CreateTSVariables"></a>Samlings-och enhets variabler

Du kan definiera egna aktivitetssekvensvariabler för datorer och samlingar. Variabler som du definierar för en dator kallas variabler för aktivitetssekvens för aktiviteter per dator. Variabler som definieras för en samling kallas aktivitetssekvensvariabler per samling. Mer information finns i [samlings-och enhets variabler](../understand/using-task-sequence-variables.md#bkmk_set-coll-var).

## <a name="additional-actions"></a><a name="BKMK_AdditionalActionsTS"></a>Ytterligare åtgärder  

Du kan hantera aktivitetssekvenser med hjälp av ytterligare åtgärder när du väljer en aktivitetssekvens.  

### <a name="edit"></a>Redigera

Mer information finns i [använda redigeraren för aktivitetssekvens](../understand/task-sequence-editor.md#bkmk_edit).

### <a name="enable"></a>Aktivera

Aktiverar aktivitetssekvensen så att klienter kan köra den. Du behöver inte omdistribuera en aktivitetssekvens när den har Aktiver ATS.  

### <a name="disable"></a>Inaktivera

Inaktiverar aktivitetssekvensen så att den inte kan köras på datorer. Du kan distribuera en inaktive rad aktivitetssekvens, men datorerna kör inte aktivitetssekvensen förrän du aktiverar den.  

### <a name="export"></a>Exportera

Mer information finns i [Exportera och importera aktivitetssekvenser](#BKMK_ExportImport).

### <a name="copy"></a>Kopiera

Skapar en kopia av den valda aktivitetssekvensen. Den här åtgärden är användbar för att skapa en ny aktivitetssekvens som baseras på en befintlig aktivitetssekvens.

När du skapar en kopia av en aktivitetssekvens i en mapp visas kopian i den mappen tills du uppdaterar aktivitetssekvensnoden. Efter uppdateringen visas kopian i rotmappen.  

### <a name="refresh"></a>Uppdatera

Uppdaterar informationen för den valda aktivitetssekvensen.

### <a name="delete"></a>Ta bort

Tar bort den valda aktivitetssekvensen.

### <a name="create-phased-deployment"></a>Skapa stegvis distribution

Mer information finns i skapa stegvisa [distributioner](create-phased-deployment-for-task-sequence.md).

### <a name="deploy"></a>Distribuera

Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md).

### <a name="distribute-content"></a>Distribuera innehåll

Startar guiden Distribuera innehåll för att skicka det refererade innehållet till distributions platser.

### <a name="create-prestaged-content-file"></a>Skapa förinstallerad innehållsfil

Startar guiden Skapa förinstallerad innehållsfil för att förinstallera innehållet i aktivitetssekvensen. Information om hur du skapar en förinstallerad innehållsfil finns i [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).

### <a name="move"></a>Flytta

Flyttar den markerade aktivitetssekvensen till en annan mapp i noden **aktivitetssekvenser** .

### <a name="set-security-scopes"></a>Ange säkerhets omfattningar

Välj säkerhets omfattningar för den valda aktivitetssekvensen. Mer information finns i [Säkerhetsomfattningar](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).

### <a name="properties"></a>Egenskaper

Mer information finns i [Konfigurera Software Center-egenskaper](#bkmk_prop-general) och [Konfigurera avancerade inställningar för aktivitetssekvens](#bkmk_prop-advanced).

### <a name="view"></a>Vy

<!--3633146-->
Från och med version 1902 är **visnings** åtgärden för aktivitetssekvenser standardvärdet. Med den här åtgärden kan du se stegen i aktivitetssekvensen utan att låsa den för redigering. Mer information finns i [använda redigeraren för aktivitetssekvens](../understand/task-sequence-editor.md#bkmk_view).

## <a name="see-also"></a>Se även

- [Scenarier för att distribuera operativsystem i företag](scenarios-to-deploy-enterprise-operating-systems.md)

- [Använda redigeringsprogrammet för aktivitetssekvenser](../understand/task-sequence-editor.md)

- [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md)

- [Aktivitetssekvenssteg](../understand/task-sequence-steps.md)

- [Samlings-och enhets variabler](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)

- [Skapa stegvisa distributioner](create-phased-deployment-for-task-sequence.md)
