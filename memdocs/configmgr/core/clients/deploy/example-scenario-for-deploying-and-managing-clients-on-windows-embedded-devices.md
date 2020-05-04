---
title: Exempel scenario – distribuera Windows Embedded-klienter
titleSuffix: Configuration Manager
description: Se ett exempel scenario för att distribuera och hantera Configuration Manager-klienter på Windows Embedded-enheter.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18e6252a3528e62153e7226ff285d24cd6ecf013
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713333"
---
# <a name="example-scenario-for-deploying-and-managing-configuration-manager-clients-on-windows-embedded-devices"></a>Exempel scenario för att distribuera och hantera Configuration Manager-klienter på Windows Embedded-enheter

*Gäller för: Configuration Manager (aktuell gren)*

Det här scenariot visar hur du kan hantera Windows Embedded-enheter med Skriv filter med Configuration Manager. om dina inbäddade enheter inte stöder Skriv filter beter de sig som standard Configuration Manager-klienter och dessa procedurer gäller inte.  

Coho vinodlingen & Winery öppnar ett besöks Center och behöver informations kiosker som kör Windows Embedded för att köra interaktiva presentationer. Byggnaden för det nya besöks centret är inte nära IT-avdelningen, så att kioskerna måste fjärrhanteras. Förutom den program vara som kör presentationerna måste dessa enheter köra uppdaterat skydd mot skadlig kod för att uppfylla företagets säkerhets principer. Kioskerna måste köras 7 dagar i veckan, utan avbrott när besöks centret är öppet.  

 Coho kör redan Configuration Manager för att hantera enheter i nätverket. Configuration Manager har kon figurer ATS för att köra Endpoint Protection och installera program uppdateringar och program. Men eftersom IT-teamet inte har hanterat Windows Embedded-enheter tidigare, kör Configuration Manager administratören en pilot för att hantera två kiosker i mottagnings introduktionen.   

 Om du vill hantera dessa Windows Embedded-enheter som har Skriv-filter-aktiverade, utför Configuration Manager administratören följande steg för att installera Configuration Manager-klienten, skydda klienten med hjälp av Endpoint Protection och installera program varan för den interaktiva presentationen.  

1. Configuration Manager administratören (administratören) läser om hur Windows Embedded-enheter använder Skriv filter och hur Configuration Manager kan göra detta enklare genom att inaktivera och sedan återaktivera skrivar filter för att bevara en program varu installation.  

    Mer information finns i [Planera för klient distribution till Windows Embedded-enheter](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2. Innan administratören installerar Configuration Manager klienten skapar administratören en ny fråge-baserad enhets samling för Windows Embedded-enheter. Eftersom företaget använder standard namn format för att identifiera sina datorer, kan administratören unikt identifiera Windows Embedded-enheter med de första sex bokstäverna i dator namnet: **WEMDVC**. Administratören använder följande WQL-fråga för att skapa samlingen: **välj SMS_R_System. NetbiosName från sms_r_system där SMS_R_System. NetbiosName som "WEMDVC%"**  

    Med den här samlingen kan administratören hantera Windows Embedded-enheter med olika konfigurations alternativ från de andra enheterna. Administratören kommer att använda den här samlingen för att styra omstarter, distribuera Endpoint Protection med klient inställningar och distribuera programmet för den interaktiva presentationen.  

    Se [skapa samlingar](../../../core/clients/manage/collections/create-collections.md).  

3. Administratören konfigurerar samlingen för en underhålls period för att säkerställa att omstarter som kan krävas för att installera presentations programmet och eventuella uppgraderingar inte sker under Öppet tider för besöks centret. Öppettiderna är måndag till söndag 09:00 till 18:00. Administratören konfigurerar underhålls perioden för varje dag, 18:30 till 06:00.  

4. Mer information finns i [använda underhålls](../../../core/clients/manage/collections/use-maintenance-windows.md)perioder.  

5. Administratören konfigurerar sedan en anpassad enhets klient inställning för att installera Endpoint Protection klienten genom att välja **Ja** för följande inställningar och sedan distribuera den här anpassade klient inställningen till Windows Embedded-enhets samlingen:  

   - **Installera Endpoint Protection-klient på klientdatorer**  

   - **Installera Endpoint Protection på Windows Embedded-enheter med skrivfilter (kräver omstart)**  

   - **Tillåt att Endpoint Protection installeras och startas om utanför underhållsintervallerna**  

     När Configuration Manager-klienten är installerad installerar de här inställningarna Endpoint Protection klienten och ser till att den sparas i operativ systemet som en del av installationen, i stället för att endast skriva till överlägget. Företagets säkerhets principer kräver att program varan för program mot skadlig kod alltid är installerad och att administratören inte vill köra en risk för att kioskerna ska vara oskyddade under en kort tids period om de startar om.  

   > [!NOTE]  
   >  De omstarter som krävs för att installera Endpoint Protection-klienten är en engångshändelse som inträffar under enheternas installation och innan besökscentret tas i drift. Till skillnad från den periodiska distributionen av program eller program definitions uppdateringar är det troligt att den Endpoint Protection klienten är installerad på samma enhet när företaget uppgraderar till nästa version av Configuration Manager.  

    Mer information finns i [konfigurera Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md).  

6. Med konfigurations inställningarna för-klienten på plats förbereder administratören att installera Configuration Manager klienter. Innan administratören kan installera klienterna måste de manuellt inaktivera Skriv filtret på Windows Embedded-enheterna. Administratören läser OEM-dokumentationen som medföljer kioskerna och följer anvisningarna för att inaktivera Skriv filtren.  

    Administratören byter namn på enheten så att den använder företagets standard namngivnings format och installerar sedan klienten manuellt genom att köra CCMSetup med följande kommando från en mappad enhet som innehåller klientens källfiler: **CCMSetup. exe/MP: mpserver. cohovineyardandwinery. com SMSSITECODE = CO1**  

    Det här kommandot installerar klienten, tilldelar klienten till den hanteringsplats som har intranäts-FQDN **mpserver.cohovineyardandwinery.com**samt tilldelar klienten till den primära plats som har namnet **CO1**.  

    Administratören vet att det alltid tar en stund för klienter att installera och skicka tillbaka sin status till platsen. Så att administratören väntar innan de bekräftar att klienterna har installerats, tilldelats platsen och visas som klienter i den samling som de har skapat för Windows Embedded-enheter.  

    Som ytterligare bekräftelse kontrollerar administratören egenskaperna för Configuration Manager på kontroll panelen på enheterna och jämför dem med standard Windows-datorer som hanteras av platsen. På fliken **Komponenter** visar t.ex. **Maskinvaruinventeringsagent** nu **Aktiverad**, och på fliken **Åtgärder** finns det 11 tillgängliga åtgärder, inklusive **Utvärderingscykel för programdistribution** och **Cykel för insamling av identifieringsdata**.  

    För att klienterna ska kunna installeras, tilldelas och tas emot från hanterings platsen aktiverar administratören sedan Skriv filtren manuellt genom att följa instruktionerna från OEM-tillverkaren.  

    Mer information finns i:  

   -   [Distribuera klienter på Windows-datorer](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

   -   [Tilldela klienter till en plats](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7. Nu när Configuration Manager-klienten är installerad på Windows Embedded-enheter bekräftar administratören att de kan hantera dem på samma sätt som de hanterar Windows-standardklienterna. Från Configuration Manager-konsolen kan administratören till exempel fjärrhantera dem genom att använda fjärr styrning, initiera klient princip för dem och Visa klient egenskaper och maskin varu inventering.  

    Eftersom dessa enheter är anslutna till en Active Directory domän behöver administratören inte godkänna dem manuellt som betrodda klienter och bekräftar från den Configuration Manager-konsolen som de är godkända.  

    Mer information finns i [Hantera klienter](../../../core/clients/manage/manage-clients.md).  

8. För att installera program varan för den interaktiva presentationen kör administratören **guiden distribuera program vara** och konfigurerar ett obligatoriskt program. På sidan **användar upplevelse** i guiden i avsnittet **Skriv filter hantering för Windows Embedded-enheter** godkänner de standard alternativet som väljer **genomför ändringar efter deadline eller under ett underhålls fönster (omstart krävs)**.  

    Administratören behåller det här standard alternativet för Skriv filter för att säkerställa att programmet finns kvar efter en omstart, så att det alltid är tillgängligt för besökare som använder informations kioskerna. Det dagliga underhållsfönstret ger en säker period när omstarterna för installation och eventuella uppdateringar kan inträffa.  

    Administratören distribuerar programmet till samlingen Windows Embedded-enheter.  

    Mer information finns i [distribuera program med Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

9. Om du vill konfigurera definitions uppdateringar för Endpoint Protection använder administratören program uppdateringar och kör guiden Skapa regel för automatisk distribution. De väljer mallen **definitions uppdateringar** för att fylla i guiden med inställningar som är lämpliga för Endpoint Protection.  

     De här inställningarna innefattar följande på sidan **Användarupplevelse** i guiden:  

   - **Beteende för tidsgräns**: Kryssrutan **Programvaruinstallation** är inte markerad.  

   - **Skriv filterhantering för Windows Embedded-enheter**: Kryssrutan **Genomför ändringar efter deadline eller under ett underhållsfönster (omstart krävs)** är inte markerad.  

     Administratören behåller standardinställningarna. Tillsammans tillåter de här två alternativen med denna konfiguration att alla programuppdateringsdefinitioner för Endpoint Protection installeras i överlagringen under dagen, och inte väntar på att installeras och bekräftas under underhållsfönstret. Den här konfigurationen är den som bäst uppfyller företagets säkerhetspolicy om att datorer ska köra uppdaterat skydd mot skadlig kod.  

     > [!NOTE]  
     >  Till skillnad från programinstallationer för program kan programuppdateringsdefinitioner för Endpoint Protection inträffa ofta, t.o.m. flera gånger om dagen. Det gäller ofta små filer. För de här typerna av säkerhetsrelaterade distributioner kan det ofta vara en fördel att alltid installera överlagringen istället för att vänta till underhållsfönstret. Configuration Manager-klienten installerar snabbt om program definitions uppdateringarna om enheten startas om, eftersom den här åtgärden startar en utvärderings kontroll och inte väntar till nästa schemalagda utvärdering.  

     Administratören väljer samlingen Windows Embedded-enheter för den automatiska distributions regeln.  

     Mer information finns i  
               Steg 3: Konfigurera Configuration Manager program uppdateringar för att leverera definitions uppdateringar till klient datorer i [konfigurera Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)  

10. Administratören bestämmer sig för att konfigurera en underhålls uppgift som regelbundet genomför alla ändringar i överlagringen. Den här uppgiften ska stödja distributionen av programuppdateringsdefinitioner, för att minska det antal uppdateringar som ansamlas och måste installeras igen varje gång enheten startas om. I administratörens upplevelse gör detta att program mot skadlig kod körs effektivare.  

    > [!NOTE]  
    >  Dessa programdefinitionsuppdateringar skulle bekräftas till avbildningen automatiskt om de inbäddade enheterna körde en annan hanteringsaktivitet som hade stöd för att bekräfta ändringarna. T.ex. skulle installation av en ny version av programmet för de interaktiva presentationerna också bekräfta ändringarna i programuppdateringsdefinitionerna. Även installation av standardprogramuppdateringar varje månad, som görs under underhållsfönstret, skulle bekräfta ändringarna i programuppdateringsdefinitionerna. Men i detta scenario, där standardprogramuppdateringar inte körs och programvaran för de interaktiva presentationerna antagligen inte uppdateras särskilt ofta, kan det ta flera månader innan programdefinitionsuppdateringarna automatiskt bekräftas till avbildningen.  

     Administratören skapar först en anpassad aktivitetssekvens som inte har några andra inställningar än namnet. De kör guiden skapa aktivitetssekvens:  

    1. På sidan **skapa en ny aktivitetssekvens** väljer administratören **skapa en ny anpassad aktivitetssekvens**och klickar sedan på **Nästa**.  

    2. På sidan **information** om aktivitetssekvens anger administratören **underhålls uppgift för att genomföra ändringar på inbäddade enheter** för aktivitetssekvensen och klickar sedan på **Nästa**.  

    3. På sidan **Sammanfattning** väljer administratören **Nästa**och Slutför guiden.  

       Administratören distribuerar sedan den här anpassade aktivitetssekvensen till samlingen Windows Embedded-enheter och konfigurerar schemat så att det körs varje månad. Som en del av distributions inställningarna markerar de kryss rutan **genomför ändringar efter deadline eller under ett underhålls fönster (omstart krävs)** för att spara ändringarna efter en omstart. Om du vill konfigurera den här distributionen väljer administratören den anpassade aktivitetssekvensen som de nyss skapade och klickar sedan på **distribuera** i gruppen **distribution** på fliken **Start** för att starta guiden distribuera program vara:  

    4. På sidan **Allmänt** väljer administratören den samling med Windows Embedded-enheter och klickar sedan på **Nästa**.  

    5. På sidan **distributions inställningar** väljer administratören **syftet** med **obligatorisk**och klickar sedan på **Nästa**.  

    6. På sidan **Schemaläggning** klickar administratören på **nytt** för att ange ett vecko schema under underhålls perioden och klickar sedan på **Nästa**.  

    7. Administratören Slutför guiden utan att göra några ändringar.  

       Mer information finns i  
                 [Hantera aktivitetssekvenser för att automatisera uppgifter](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. För att kioskerna ska köras automatiskt skriver administratören ett skript som konfigurerar enheterna för följande inställningar:  

    - Logga in automatiskt med ett gästkonto som saknar lösenord.  

    - Kör automatiskt det interaktiva presentationsprogrammet vid start.  

      Administratören använder paket och program för att distribuera skriptet till samlingen Windows Embedded-enheter. När administratören kör guiden distribuera program vara markerar de återigen kryss rutan **genomför ändringar efter deadline eller under ett underhålls fönster (omstart krävs)** för att spara ändringarna efter en omstart.  

      Mer information finns i [paket och program](../../../apps/deploy-use/packages-and-programs.md).  

12. Följande morgon kontrollerar administratören de Windows Embedded-enheterna. De bekräftar följande:  

    - Kiosken loggas in automatiskt via gästkontot.  

    - Den interaktiva presentationsprogramvaran körs.  

    - Endpoint Protection-klienten är installerad och har de senaste programuppdateringsdefinitionerna.  

    - Att enheten startades om under underhållsfönstret.  

      Mer information finns i:  

    - [Så här övervakar du Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    - [Övervaka program med Configuration Manager](../../../apps/deploy-use/monitor-applications-from-the-console.md)  

13. Administratören övervakar informations kioskerna och rapporterar den lyckade hanteringen av dem till sin chef. Som ett resultat beställs 20 kiosker till besökscentret.  

     För att undvika manuell installation av Configuration Manager klienten, vilket kräver manuell inaktive ring och sedan aktivering av Skriv filtren, säkerställer administratören att den innehåller en anpassad avbildning som redan omfattar installation och platstilldelning av Configuration Manager klienten. Dessutom namnges enheterna enligt företagets namngivningsformat.  

     Kioskerna levereras till besökscentret en vecka innan det öppnar. Under den här tiden är kioskerna anslutna till nätverket. All enhetshantering för dem sker automatiskt, och det krävs ingen lokal administratör. Administratören bekräftar att kioskerna fungerar på det sätt som krävs:  

    -   Klienterna för kioskerna slutför platstilldelningen och laddar ned den betrodda rotnyckeln från Active Directory-domäntjänsterna.  

    -   Klienterna för kioskerna läggs automatiskt till i samlingen med Windows Embedded-enheter och konfigureras via underhållsfönstret.  

    -   Endpoint Protection-klienten är installerad och har de senaste definitionerna för programuppdateringen för skydd mot skadlig programvara.  

    -   Det interaktiva presentationsprogrammet installeras och körs automatiskt, redo för besökarna.  

14. Efter den här inledande konfigureringen sker eventuella omstarter som kan krävas för uppdateringar enbart när besökscentret är stängt.  
