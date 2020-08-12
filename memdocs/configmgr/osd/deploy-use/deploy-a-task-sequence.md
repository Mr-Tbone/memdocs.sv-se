---
title: Distribuera en aktivitetssekvens
titleSuffix: Configuration Manager
description: Använd den här informationen för att distribuera en aktivitetssekvens till datorerna i en samling.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b2abcdb0-72e0-4c70-a4b8-7827480ba5b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fea9088a11310aedc95d2fdbeacdb98650eef361
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125210"
---
# <a name="deploy-a-task-sequence"></a>Distribuera en aktivitetssekvens

*Gäller för: Configuration Manager (aktuell gren)*

När du har skapat en aktivitetssekvens och distribuerar det refererade innehållet kan du distribuera det till en enhets samling. Den här åtgärden gör att aktivitetssekvensen kan köras på en enhet. En distribuerad aktivitetssekvens kan köras automatiskt eller när den installeras av en användare av enheten.

> [!WARNING]  
> Du kan du hantera beteendet för aktivitetssekvensdistributioner med hög risk. En distribution med hög risk är en distribution som installeras automatiskt och kan orsaka oönskade resultat. En aktivitetssekvens som har syftet **obligatoriskt** och som distribuerar ett operativ system betraktas till exempel som en distribution med hög risk. Mer information finns i [Inställningar för att hantera distributioner med hög risk](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

## <a name="process"></a>Process

Använd följande procedur för att distribuera en aktivitetssekvens till datorerna i en samling.  

> [!NOTE]  
> Status meddelanden för aktivitetssekvensdistribution visas i meddelande fönstret på en primär plats, men de visas inte på en central administrations plats.  

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj noden **aktivitetssekvenser** .  

2. I listan **Aktivitetssekvens** väljer du den aktivitetssekvens som du vill distribuera.  

3. På fliken **Start** i menyfliksområdet väljer du **distribuera**i gruppen **distribution** .  

    > [!NOTE]  
    > Om **distribuera** inte är tillgängligt har aktivitetssekvensen en referens som inte är giltig. Korrigera referensen och försök sedan att distribuera aktivitetssekvensen igen.  

4. På sidan **Allmänt** anger du följande information.  

    - **Aktivitetssekvens**: Ange den aktivitetssekvens som ska distribueras. Den här rutan visar den valda aktivitetssekvensen som standard.  

    - **Samling**: Välj den samling som innehåller de datorer som ska köra aktivitetssekvensen.  

        Distribuera inte en aktivitetssekvens som installerar ett operativ system till olämpliga samlingar, till exempel en samling av alla data Center servrar. Se till att den valda samlingen endast innehåller de datorer som du vill köra aktivitetssekvensen på.  

        Mer information om distributioner med hög risk finns i [distributioner med hög risk](#bkmk_high-risk).

    - **Använd standard distributions plats grupper som är associerade med den här samlingen**: lagra innehållet i aktivitetssekvensen i samlingens standard distributions plats grupp. Om du inte har associerat den valda samlingen med en distributions plats grupp är det här alternativet nedtonat.  

    - **Distribuera automatiskt innehåll för beroenden**: om något refererat innehåll har beroenden skickar platsen även beroende innehåll till distributions platser.  

    - **Hämta innehåll i förväg för den här aktivitetssekvensen**: Mer information finns i [Konfigurera innehåll i förcachen](configure-precache-content.md).  

    - **Välj distributionsmall**: Spara och ange en Distributionsmall för en aktivitetssekvens.<!--1357391-->  

        > [!IMPORTANT]  
        > Vissa objekt sparas inte i mallen.<!--510610--> Se till att tillämpa följande objekt när du kör distributions guiden:  
        >
        > - Program varu installation
        > - Schemaläggning
        > - Hämta innehåll i förväg

    - **Kommentarer (valfritt)**: Ange ytterligare information som beskriver distributionen av aktivitetssekvensen.  

5. På sidan **distributions inställningar** anger du följande information:  

    - **Syfte**: Välj något av följande alternativ i listrutan:  

        - **Tillgängligt**: användaren ser aktivitetssekvensen i Software Center och kan installera den på begäran.  

        - **Obligatoriskt**: Configuration Manager kör aktivitetssekvensen automatiskt enligt det konfigurerade schemat. Om aktivitetssekvensen inte är dold kan en användare fortfarande spåra distributionens status. De kan också använda Software Center för att installera aktivitetssekvensen före tids gränsen.  

        > [!NOTE]
        > Om flera användare är inloggade på enheten, kan det hända att paket och aktivitetssekvensdistributioner inte visas i Software Center.  

    - **Gör tillgängligt för följande**: Ange om aktivitetssekvensen är tillgänglig för någon av följande typer:  

        - Endast Configuration Manager klienter  
        - Configuration Manager klienter, media och PXE  
        - Endast media och PXE  
        - Endast media och PXE (dolt)  

        > [!IMPORTANT]  
        > Använd inställningen **Endast media och PXE (dolt)** för automatiserade aktivitetssekvensdistributioner. Om du vill att datorn ska starta automatiskt till distributionen utan användar interaktion väljer du **Tillåt obevakad distribution av operativ system** och ställer in variabeln **SMSTSPreferredAdvertID** som en del av mediet. Mer information om variabler för aktivitetssekvens finns i [variabler för aktivitetssekvens](../understand/task-sequence-variables.md#SMSTSPreferredAdvertID).  

    - **Skicka väcknings paket**: om distributionen **krävs** och du väljer det här alternativet skickar platsen ett väcknings paket till datorer innan klienten kör distributionen. Det här paketet aktiverar datorn från vila vid installationens tids gräns. Innan du använder det här alternativet måste datorer och nätverk konfigureras för Wake On LAN. Mer information finns i [Planera aktivering av klienter](../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    - **Tillåt klienter på en avgiftsbelagd Internet-anslutning att hämta innehåll efter installationens tids gräns, vilket kan innebära ytterligare kostnader**: det här alternativet är bara tillgängligt för **nödvändiga** distributioner. När du har en anpassad aktivitetssekvens som installerar ett program, men inte distribuerar ett operativ system, kan du ange om du vill tillåta att klienter laddar ned innehåll efter en installations tids gräns när de använder avgiftsbelagda Internet anslutningar. Internet leverantörer debiteras ibland av den mängd data som du använder när du använder en avgiftsbelagd Internet-anslutning.  

        > [!NOTE]  
        > Även om det kan fungera att använda en avgiftsbelagd Internet-anslutning för aktivitetssekvenser som inte distribuerar ett operativ system, stöds det inte.  

6. På sidan **Schemaläggning** anger du följande information:  

    > [!IMPORTANT]  
    > När en Windows PE-klient startar från PXE eller start mediet utvärderar klienten inte distributions scheman. Dessa scheman inkluderar Start-, förfallo-och tids gräns tider. Konfigurera endast scheman i distributioner till klienter som startar från det fullständiga Windows OS. Du kan fundera på andra metoder, som t.ex. underhållsfönster, för att styra aktiva aktivitetssekvenser som distribueras till klienter som startar från Windows PE.  

    - **Schemalägg när distributionen ska vara tillgänglig**: Ange datum och tid då aktivitetssekvensen är tillgänglig för körning på måldatorn. När du väljer alternativet **UTC** är aktivitetssekvensen tillgänglig för flera datorer på samma gång. Annars är distributionen tillgänglig vid olika tidpunkter, enligt den lokala tiden på varje dator.  

        Om start tiden infaller före den begärda tiden laddar klienten ned innehållet i aktivitetssekvensen vid start tiden.  

    - **Schemalägg när distributionen ska upphöra att gälla**: Ange datum och tid då aktivitetssekvensen upphör att gälla på måldatorn. När du väljer alternativet **UTC** , förfaller aktivitetssekvensen på flera mål datorer samtidigt. Annars upphör distributionen vid olika tidpunkter, enligt den lokala tiden på varje dator.  

    - **Tilldelnings schema**: Ange när klienten kör aktivitetssekvensen för en **obligatorisk** distribution. Du kan lägga till flera scheman. Tilldelnings schemat kan ha en av följande konfigurationer:  

        - Ett visst datum och en angiven tid  
        - Månatligt, veckovis eller anpassat upprepnings mönster  
        - Så snart som möjligt  
        - Logga in eller logga ut händelser  

        > [!NOTE]  
        > Om du schemalägger en start tid för en begärd distribution som är tidigare än datum och tid då aktivitetssekvensen är tillgänglig, laddar Configuration Manager-klienten innehållet vid den tilldelade start tiden. Detta inträffar även om du har schemalagt att aktivitetssekvensen är tillgänglig vid ett senare tillfälle.<!--SCCMDocs issue 777-->  

    - **Omkörnings beteende**: Ange när aktivitetssekvensen körs igen. Välj något av följande alternativ:  

        - **Kör aldrig om distribuerade program**: om klienten tidigare har kört aktivitetssekvensen körs den inte igen. Aktivitetssekvensen körs inte igen även om den ursprungligen misslyckades eller om du har ändrat filerna i aktivitetssekvensen.  

        - **Kör alltid om program**: aktivitetssekvensen körs alltid om på klienten när distributionen har schemalagts. Den körs på samma gång även om aktivitetssekvensen redan har körts. Den här inställningen är användbar när du använder återkommande distributioner där aktivitetssekvensen uppdateras regelbundet.  

            > [!IMPORTANT]  
            > Det här alternativet är markerat som standard. Den har dock ingen påverkan förrän du tilldelar en nödvändig distribution. En användare kan alltid köra om tillgängliga distributioner.  

        - **Kör om när föregående försök misslyckades**: aktivitetssekvensen kör om när distributionen har schemalagts, endast om den tidigare inte kunde köras. Den här inställningen är användbar för en obligatorisk distribution. Om det senaste försöket att köra inte lyckades, försöker den automatiskt att köras enligt tilldelnings schema.  

        - **Kör om när föregående försök genomfördes**: aktivitetssekvensen körs bara på nytt om den har körts tidigare på klienten. Den här inställningen är användbar när du använder återkommande distributioner där aktivitetssekvensen uppdateras regelbundet och varje uppdatering kräver att den tidigare uppdateringen har installerats.  

        > [!NOTE]  
        > En användare kan köra en tillgänglig aktivitetssekvensdistribution igen. Innan du distribuerar en tillgänglig aktivitetssekvens i en produktions miljö måste du först testa vad som händer om en användare kör aktivitetssekvensen flera gånger.  

7. Ange följande information på sidan **Användarupplevelse** :  

    - **Tillåt att användare kör programmet oberoende av tilldelningar**: Ange om en användare kan köra en nödvändig distribution utanför tilldelnings schemat. Det här alternativet är alltid aktiverat för tillgängliga distributioner.  

    - **Visa förlopp för aktivitetssekvens**: Ange om den Configuration Manager klienten ska visa förloppet för aktivitetssekvensen.  

    - **Program varu installation**: Ange om användaren får installera program varan utanför en konfigurerad underhålls period efter den schemalagda tiden.  

    - **Systemomstart (om det krävs för att slutföra installationen)**: Ange om användaren får starta om datorn efter en programvaruinstallation som ligger utanför ett konfigurerat underhållsfönster efter tilldelningstiden.  

    - **Skriv filter hantering för Windows Embedded-enheter**: den här inställningen styr installations beteendet på Windows Embedded-enheter som är aktiverade med ett Skriv filter. Välj alternativet för att genomföra ändringar vid installationens tids gräns eller under en underhålls period. När du väljer det här alternativet krävs en omstart och ändringarna sparas på enheten. Annars installeras programmet på det tillfälliga överlägget och genomförs senare. När du distribuerar en aktivitetssekvens till en Windows Embedded-enhet ser du till att enheten är medlem i en samling som har en konfigurerad underhålls period.  

    - **Tillåt att aktivitetssekvensen körs för klient på Internet**: Ange om aktivitetssekvensen tillåts köras på en Internetbaserad klient.

        Den här inställningen stöds för distribution av en aktivitetssekvens för Windows 10-uppgradering på plats till Internetbaserade klienter via Cloud Management Gateway (CMG). Mer information finns i [distribuera uppgradering av Windows 10 på plats via CMG](#deploy-windows-10-in-place-upgrade-via-cmg).

        Från och med version 2006 kan du distribuera en aktivitetssekvens med en start avbildning till en enhet som kommunicerar via CMG. Användaren måste starta aktivitetssekvensen från Software Center.<!--6997525-->

        > [!NOTE]
        > När en Azure Active Directory (Azure AD)-ansluten klient kör en aktivitetssekvens för operativ Systems distribution kommer klienten i det nya operativ systemet inte att ansluta automatiskt till Azure AD. Även om den inte är Azure AD-ansluten, hanteras klienten fortfarande.
        >
        > När du kör en aktivitetssekvens för operativ system distribution på en Internetbaserad klient, som antingen är Azure AD-ansluten eller använder tokenbaserad autentisering, måste du ange egenskapen **CCMHOSTNAME** i steget [Installera Windows och ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) .

        I version 2002 och tidigare stöds inte åtgärder som kräver ett start medium med den här inställningen. Använd endast det här alternativet för allmänna program varu installationer eller skriptbaserade aktivitetssekvenser som kör åtgärder i standard operativ systemet.

        > [!NOTE]
        > Starta aktivitetssekvensen från Software Center för alla Internetbaserade scenarier för aktivitetssekvenser. De stöder inte Windows PE-, PXE-eller aktivitetssekvens-media.

8. På sidan **aviseringar** anger du de aviserings inställningar som du vill använda för den här distributionen av aktivitetssekvensen.  

9. Ange följande information på sidan **Distributionsplatser** :  

    - **Distributions alternativ**: Mer information finns i [distributions alternativ](#bkmk_deploy-options).

    - **Använd en fjärrdistributions plats om det inte finns någon lokal distributions plats**: Ange om klienter kan använda distributions platser från en intilliggande gränser grupp för att ladda ned det innehåll som krävs av aktivitetssekvensen.  

    - **Tillåt att klienter använder distributions platser från standard plats begränsnings gruppen**: Ange om klienter ska ladda ned innehåll från en distributions plats i platsens standard begränsnings grupp när den inte är tillgänglig från en distributions plats i den aktuella eller intilliggande begränsnings gruppen.  

        > [!Note]  
        > Från och med version 1810, när en enhet kör en aktivitetssekvens och behöver hämta innehåll, använder den gränser grupp beteenden som liknar Configuration Manager-klienten. Mer information finns i [stöd för aktivitetssekvenser för gränser grupper](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd).<!--1359025-->  

10. Om du vill spara inställningarna och använda dem igen går du till fliken **Sammanfattning** och väljer **Spara som mall**. Ange ett namn för mallen och välj de inställningar som ska sparas.  

11. Slutför guiden.  

### <a name="deployment-options"></a><a name="bkmk_deploy-options"></a>Distributions alternativ

<!-- MEMDocs#328, SCCMDocs#2114 -->

De här alternativen finns på fliken **distributions platser** i aktivitetssekvensdistribution. De är dynamiska baserat på andra val i en aktivitetssekvens distribution och attribut. Du kan inte alltid se alla alternativ.

> [!NOTE]  
> När du använder multicast för att distribuera ett operativ system laddar du ned innehållet till datorerna antingen efter behov eller innan aktivitetssekvensen körs.  

- **Ladda ned innehåll lokalt när du behöver genom att köra aktivitetssekvensen**: ange att klienter laddar ned innehåll från distributions platsen när de behövs i aktivitetssekvensen. Klienten startar aktivitetssekvensen. När ett steg i aktivitetssekvensen kräver innehåll hämtas det innan steget körs.  

- **Hämta allt innehåll lokalt innan aktivitetssekvensen startas**: ange att klienterna ska ladda ned allt innehåll från distributions platsen innan aktivitetssekvensen körs. Om du gör aktivitetssekvensen tillgänglig för PXE-och start medie distributioner på sidan **distributions inställningar** visas inte det här alternativet.  

- **Få åtkomst till innehållet direkt från en distributions plats vid behov genom att köra aktivitetssekvensen**: ange att klienter kör innehållet från distributions platsen. Det här alternativet är bara tillgängligt om du aktiverar alla paket som är kopplade till aktivitetssekvensen för att använda en paket resurs på distributions platsen. Om du vill aktivera innehållet för att använda en paketdelning går du till fliken **Dataåtkomst** i **Egenskaper** för varje paket.  

> [!IMPORTANT]  
> För bästa säkerhet väljer du alternativen för att **Ladda ned innehåll lokalt när det behövs av aktivitetssekvensen som körs** eller **Ladda ned allt innehåll lokalt innan aktivitetssekvensen startas**. När du väljer något av dessa alternativ Configuration Manager hash-kodar paketet, så att det kan säkerställa paket integriteten. När du väljer alternativet för att **komma åt innehåll direkt från en distributions plats vid behov genom att köra aktivitetssekvensen**, verifierar Configuration Manager inte paketets hash innan du kör det angivna programmet. Eftersom platsen inte kan garantera paket integriteten är det möjligt för användare med administratörs behörighet att ändra eller manipulera paket innehåll.  

#### <a name="example-1-one-deployment-option"></a>Exempel 1: ett distributions alternativ

Du distribuerar en aktivitetssekvens för operativ Systems distribution som rensar disken och tillämpar en avbildning. På sidan **distributions inställningar** gör du det tillgängligt för ett alternativ som inkluderar media och PXE:

:::image type="content" source="media/deploy-setting-make-available.png" alt-text="Distribuera aktivitetssekvens, gör den tillgänglig för följande":::

På sidan **distributions platser** finns det bara ett distributions alternativ:

- **Ladda ned innehåll lokalt när du behöver genom att köra aktivitetssekvensen**

:::image type="content" source="media/deploy-option-1.png" alt-text="Distribuera aktivitetssekvens, ett distributions alternativ":::

Alternativet att **Ladda ned allt innehåll lokalt innan aktivitetssekvensen startas** är inte tillgängligt eftersom distributionen görs tillgänglig för media och PXE.

Alternativet att **komma åt innehåll direkt från en distributions plats när det behövs av aktivitetssekvensen som körs** är inte tillgängligt. Inte allt innehåll som refereras till använder en paket resurs.

#### <a name="example-2-two-deployment-options"></a>Exempel 2: två distributions alternativ

Du distribuerar en aktivitetssekvens för operativ Systems distribution som rensar disken och tillämpar en avbildning. På sidan **distributions inställningar** gör du det bara tillgängligt för **Configuration Manager klienter**. På sidan **distributions platser** finns det två tillgängliga distributions alternativ:

- **Ladda ned innehåll lokalt när du behöver genom att köra aktivitetssekvensen**
- **Hämta allt innehåll lokalt innan aktivitetssekvensen startas**

:::image type="content" source="media/deploy-option-2.png" alt-text="Distribuera aktivitetssekvens, två distributions alternativ":::

Alternativet att **komma åt innehåll direkt från en distributions plats när det behövs av aktivitetssekvensen som körs** är inte tillgängligt. Inte allt innehåll som refereras till använder en paket resurs.

#### <a name="example-3-three-deployment-options"></a>Exempel 3: tre distributions alternativ

Du har flera paket med administrativa skript och tillhör ande innehåll. På fliken **data åtkomst** i paket egenskaperna konfigurerar du alla för att **Kopiera innehållet i det här paketet till en paket resurs på distributions platser**.

Du skapar en aktivitetssekvens som bara har flera **installations paket** steg för dessa skript paket och distribuerar det. På sidan **distributions inställningar** är det enda alternativet att endast vara tillgängligt för **Configuration Manager klienter**. Det här alternativet är endast tillgängligt. Aktivitetssekvensen är inte för operativ system distribution, eftersom den inte har någon kopplad start avbildning. På sidan **distributions platser** finns det tre tillgängliga distributions alternativ:

- **Ladda ned innehåll lokalt när du behöver genom att köra aktivitetssekvensen**
- **Hämta allt innehåll lokalt innan aktivitetssekvensen startas**
- **Få åtkomst till innehållet direkt från en distributions plats vid behov genom att köra aktivitetssekvensen**

:::image type="content" source="media/deploy-option-3.png" alt-text="Distribuera aktivitetssekvens, tre distributions alternativ":::

## <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Distribuera uppgradering av Windows 10 på plats via CMG

<!-- 1357149 -->
Aktivitetssekvensen Windows 10 på plats-uppgradering stöder distribution till Internetbaserade klienter som hanteras via [Cloud Management Gateway](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG). Den här möjligheten gör att fjärran vändare enklare kan uppgradera till Windows 10 utan att behöva ansluta till intranätet.

Se till att allt innehåll som refereras till av aktivitetssekvensen för uppgradering på plats distribueras till en innehålls aktive rad CMG. (Aktivera [inställningen CMG](../../core/clients/manage/cmg/setup-cloud-management-gateway.md#settings): **Tillåt att CMG fungerar som en moln distributions plats och hantera innehåll från Azure Storage**.) Du kan också använda en [moln distributions plats](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Annars kan inte enheterna köra aktivitetssekvensen.

När du distribuerar en aktivitetssekvens för uppgradering använder du följande inställningar:

- **Tillåt att aktivitetssekvensen körs för klient på Internet**på fliken Användar upplevelse i distributionen.  

- Välj något av följande alternativ på fliken distributions platser i distributionen:

  - **Hämta innehåll lokalt vid behov genom att köra aktivitetssekvensen**. Från och med version 1910 kan aktivitetssekvensen Ladda ned paket på begäran från en innehålls aktive rad CMG eller en moln distributions plats. Den här ändringen ger ytterligare flexibilitet för distributioner av Windows 10 på plats till Internet-baserade enheter.<!--3601238-->

  - **Hämta allt innehåll lokalt innan aktivitetssekvensen startas**. I Configuration Manager version 1906 och tidigare fungerar andra alternativ som **Hämta innehåll lokalt när det behövs av aktivitetssekvensen som körs** inte i det här scenariot. Motorn för aktivitetssekvenser kan inte ladda ned innehåll från en moln källa. Den Configuration Manager klienten måste ladda ned innehållet från moln källan innan aktivitetssekvensen startas. Du kan fortfarande använda det här alternativet i version 1910 om det behövs för att uppfylla dina krav.

- (*Valfritt*) **Hämta innehåll i förväg för den här aktivitetssekvensen**på fliken Allmänt i distributionen. Mer information finns i [Konfigurera förinställt innehåll för cache](configure-precache-content.md).  

> [!NOTE]
> Starta aktivitetssekvensen från Software Center. Det här scenariot stöder inte Windows PE-, PXE-eller aktivitetssekvens-media.

## <a name="high-risk-deployments"></a><a name="bkmk_high-risk"></a>Distributioner med hög risk

När du distribuerar en högrisk distribution, till exempel ett operativ system, visar fönstret **Välj samling** bara de anpassade samlingar som uppfyller de verifierings inställningar för distribution som kon figurer ATS i platsens egenskaper. Distributioner med hög risk är alltid begränsade till anpassade samlingar, samlingar som du skapar och den inbyggda samlingen **Okända datorer** . När du skapar en distribution med hög risk kan du inte välja en inbyggd samling, till exempel **alla system**. Om du vill se alla anpassade samlingar som innehåller färre klienter än den konfigurerade maximala storleken inaktiverar du alternativet för att **dölja samlingar med ett större antal medlemmar än platsens minsta storleks konfiguration**. Mer information finns i [Inställningar för att hantera distributioner med hög risk](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

Verifieringsinställningarna för distribution baseras på samlingens aktuella medlemskap. När du har distribuerat aktivitetssekvensen utvärderas Configuration Manager inte om samlings medlemskapet för inställningarna för hög risk distribution.  

Anta till exempel att du ställer in **standard storleken** på 100 och den **maximala storleken** till 1000. När du skapar en distribution med hög risk visar fönstret **Välj samling** endast samlingar som innehåller färre än 100 klienter. Om du avmarkerar inställningen **Dölj samlingar med ett större antal medlemmar än platsens minsta storleks konfiguration** visas samlingar som innehåller färre än 1000 klienter.  

När du väljer en samling som innehåller en plats roll gäller följande:  

- Om samlingen innehåller en plats system Server och du konfigurerade inställningarna för distributions verifiering för att blockera samlingar med plats system servrar uppstår ett fel. Du kan inte fortsätta att skapa distributionen.  

- Om något av följande villkor gäller, visar guiden distribuera program vara en varning med hög risk. För att fortsätta måste du godkänna för att skapa en distribution med hög risk. Platsen genererar ett gransknings status meddelande.  

  - Om samlingen innehåller en plats system Server och du har konfigurerat inställningarna för distributions verifiering för att varna vid samlingar med plats system servrar  

  - Om samlingen överskrider standard storlek svärdet

  - Om samlingen innehåller en server  

## <a name="see-also"></a>Se även

[Hantera aktivitetssekvenser för att automatisera uppgifter](manage-task-sequences-to-automate-tasks.md)
