---
title: Distribuera program
titleSuffix: Configuration Manager
description: Skapa eller simulera en distribution av ett program till en enhet eller användar samling
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a7bbf395a5de98459043609986e51647362e7a0b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075344"
---
# <a name="deploy-applications-with-configuration-manager"></a>Distribuera program med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Skapa eller simulera en distribution av ett program till en enhet eller användar samling i Configuration Manager. Den här distributionen ger instruktioner till Configuration Manager-klienten om hur och när program varan ska installeras.

Innan du kan distribuera ett program måste du skapa minst en distributions typ för programmet. Mer information finns i [skapa program](create-applications.md).

Från och med version 1906 kan du skapa en grupp med program som du kan skicka till en användar-eller enhets samling som en enda distribution. Mer information finns i [skapa program grupper](create-app-groups.md).

Du kan också simulera en programdistribution. Den här simuleringen testar tillämpligheten för en distribution utan att installera eller avinstallera programmet. En simulerad distribution utvärderar identifierings metoden, kraven och beroenden för en distributions typ och rapporterar resultatet i noden **distributioner** på arbets ytan **övervakning** . Mer information finns i [simulera program distributioner](simulate-application-deployments.md).

> [!Note]
> Du kan bara simulera distributionen av nödvändiga program, men inte paket eller program uppdateringar.
>
> MDM-registrerade enheter stöder inte simulerade distributioner, användar upplevelser eller schemaläggnings inställningar.



## <a name="deploy-an-application"></a><a name="bkmk_deploy"></a>Distribuera ett program

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **program hantering**och välj antingen noden **program** eller **program grupper** .

2. Välj ett program eller en program grupp i listan som du vill distribuera. Klicka på **distribuera**i menyfliksområdet.  

> [!Note]  
> När du visar egenskaperna för en befintlig distribution motsvarar följande avsnitt flikar i fönstret distributions egenskaper:  
>
> - [Allmänt](#bkmk_deploy-general)
> - [Innehåll](#bkmk_deploy-content)
> - [Distributions inställningar](#bkmk_deploy-settings)
> - [Schemaläggning](#bkmk_deploy-sched)
> - [Användarupplevelse](#bkmk_deploy-ux)
> - [Aviseringar](#bkmk_deploy-alerts)


### <a name="deployment-general-information"></a><a name="bkmk_deploy-general"></a>**Allmän** information om distribution

Ange följande information på sidan **Allmänt** i guiden distribuera program vara:  

- **Program vara**: det här värdet visar det program som ska distribueras. Klicka på **Bläddra** för att välja ett annat program.  

- **Samling**: Klicka på **Bläddra** och välj den samling som programmet ska distribueras till.  

- **Använd standard distributions plats grupper som är associerade med samlingen**: lagra program innehållet i samlingens standard distributions plats grupp. Om du inte har associerat den valda samlingen med en distributions plats grupp är det här alternativet nedtonat.  

- **Distribuera automatiskt innehåll för beroenden**: om någon av distributions typerna i programmet har beroenden skickar platsen även beroende program innehåll till distributions platser.  

    >[!Note]  
    > Om du uppdaterar det beroende programmet efter att ha distribuerat det primära programmet, distribuerar inte platsen automatiskt något nytt innehåll för beroendet.  

- **Kommentarer (valfritt)**: Ange en beskrivning av distributionen om du vill.  


### <a name="deployment-content-options"></a><a name="bkmk_deploy-content"></a>Alternativ för distributions **innehåll**

På sidan **innehåll** klickar du på **Lägg till** för att distribuera innehållet för det här programmet till en distributions plats eller en distributions plats grupp.

Om du har valt alternativet för att **använda standard distributions platser som är associerade med den här samlingen** på sidan Allmänt fylls det här alternativet i automatiskt. Endast en medlem av säkerhets rollen **program administratör** kan ändra den.

Om program innehållet redan är distribuerat visas de här.


### <a name="deployment-settings"></a><a name="bkmk_deploy-settings"></a>**Distributions inställningar**

På sidan **distributions inställningar** anger du följande information:  

- **Åtgärd**: Välj i list rutan om distributionen ska **Installera** eller **Avinstallera** programmet.  

    > [!NOTE]  
    > Om du skapar en distribution för att **Installera** en app och en annan distribution för att **Avinstallera** samma app på samma enhet, prioriteras **installations** distributionen.  

    Du kan inte ändra åtgärden för en distribution när du har skapat den.  

- **Syfte**: Välj något av följande alternativ i listrutan:  

  - **Tillgängligt**: användaren ser programmet i Software Center. De kan installera det på begäran.  

  - **Obligatoriskt**: klienten installerar appen automatiskt enligt det schema som du har angett. Om programmet inte är dolt kan en användare spåra distributionens status. De kan också använda Software Center för att installera programmet före tids gränsen.  

    > [!NOTE]  
    > När du anger distributions åtgärden som **avinstalleras**anges distributions syftet automatiskt som **obligatoriskt**. Du kan inte ändra det här beteendet.  

- **Tillåt slutanvändare att försöka reparera det här programmet**: startar i version 1810, om du har skapat programmet med en reparations kommando rad aktiverar du det här alternativet. Användare ser ett alternativ i Software Center för att **Reparera** programmet.<!--1357866-->  

- **Fördistribuera program vara till användarens primära enhet**: om distributionen är till en användare väljer du det här alternativet för att distribuera programmet till användarens primära enhet. Den här inställningen kräver inte att användaren loggar in innan distributionen körs. Välj inte det här alternativet om användaren måste interagera med installationen. Det här alternativet är endast tillgängligt när distributionen **krävs**.  

- **Skicka väcknings paket**: om distributionen **krävs**skickar Configuration Manager ett väcknings paket till datorer innan klienten kör distributionen. Det här paketet aktiverar datorerna vid installationens tids gräns. Innan du använder det här alternativet måste datorer och nätverk konfigureras för Wake On LAN. Mer information finns i [Planera aktivering av klienter](../../core/clients/deploy/plan/plan-wake-up-clients.md).  

- **Tillåt klienter på en avgiftsbelagd Internet-anslutning att hämta innehåll efter installationens tids gräns, vilket kan innebära ytterligare kostnader**: det här alternativet är bara tillgängligt för distributioner med syftet **obligatoriskt**.  

- **Uppgradera automatiskt ersatta versioner av det här programmet**: klienten uppgraderar alla ersatta versioner av programmet med det ersättande programmet.

    > [!Note]  
    > Det här alternativet fungerar oavsett administratörs godkännande. Om en administratör redan har godkänt den ersatta versionen behöver de inte också godkänna ersättnings versionen. Godkännande är endast för nya begär Anden, som inte ersätter uppgraderingar.<!--515824-->  
    >
    > För **tillgängligt** installations syfte kan du aktivera eller inaktivera det här alternativet. <!--1351266-->


#### <a name="approval-settings"></a><a name="bkmk_approval"></a>Inställningar för godkännande

Program godkännande beteendet beror på om du aktiverar den rekommenderade valfria funktionen, **godkänner program begär Anden för användare per enhet**.

- **En administratör måste godkänna en begäran om det här programmet på enheten**: om du aktiverar den valfria funktionen godkänner administratören alla användar förfrågningar för programmet innan användaren kan installera den på den begärda enheten. Om administratören godkänner begäran kan användaren bara installera programmet på den enheten. Användaren måste skicka en annan begäran om att installera programmet på en annan enhet. Det här alternativet är nedtonat när distributions syftet **krävs**, eller när du distribuerar programmet till en enhets samling.

- **Kräv administratörs godkännande om användare begär det här programmet**: om du inte aktiverar den valfria funktionen godkänner administratören alla användar förfrågningar för programmet innan användaren kan installera det. Det här alternativet är nedtonat när distributions syftet **krävs**, eller när du distribuerar programmet till en enhets samling.  

Mer information finns i [godkänna program](app-approval.md).


#### <a name="deployment-properties-deployment-settings"></a>Distributions **Inställningar** för distributions egenskaper

När du visar egenskaperna för en distribution, om det stöds av distributions typ tekniken, visas följande alternativ på fliken **distributions inställningar** :

**Stäng automatiskt de körbara filer som körs och som du angav på fliken installations beteende i dialog rutan Egenskaper för distributions typ**. Mer information finns i [kontrol lera att körbara filer körs innan du installerar ett program](#bkmk_exe-check).



### <a name="deployment-scheduling-settings"></a><a name="bkmk_deploy-sched"></a>Inställningar för distributions **Schemaläggning**

På sidan **Schemaläggning** anger du när programmet distribueras eller är tillgängligt för klient enheter.

Som standard gör Configuration Manager distributions principen tillgänglig för klienter direkt. Om du vill skapa distributionen, men inte göra den tillgänglig för klienter förrän ett senare datum, konfigurerar du alternativet för att **schemalägga att programmet ska vara tillgängligt**. Välj sedan datum och tid, inklusive om det är baserat på UTC eller klientens lokala tid.

Om distributionen **krävs**anger du även **installations tids gränsen**. Som standard är den här tids gränsen så snart som möjligt.

Du måste till exempel distribuera ett nytt affärs program. Alla användare behöver installera den en viss tid, men du vill ge dem möjlighet att välja tidigt. Du måste också se till att platsen har distribuerat innehållet till alla distributions platser. Du schemalägger att programmet ska vara tillgängligt på fem dagar från idag. Det här schemat ger dig tid att distribuera innehållet och bekräfta dess status. Sedan anger du tids gränsen för installationen för en månad från idag. Användarna ser programmet i Software Center när det är tillgängligt på fem dagar. Om de inte gör det installerar-klienten automatiskt programmet vid installationens tids gräns.

Om programmet som du distribuerar ersätter ett annat program anger du tids gränsen för installationen när användarna får det nya programmet. Ange **tids gränsen för installationen** för att uppgradera användare med det ersatta programmet.


#### <a name="delay-enforcement-with-a-grace-period"></a>Fördröj tvång med en respitperiod

Du kanske vill ge användarna mer tid för att installera nödvändiga program *utöver* de tids gränser som du anger. Det här beteendet krävs vanligt vis när en dator stängs av under en längre tid och måste installera många program. Till exempel, när en användare returnerar från semestern, måste de vänta en stund när klienten installerar förfallna distributioner. Du kan lösa det här problemet genom att definiera en tvingande respitperiod.

- Konfigurera först den här Grace-perioden med egenskapen **respitperiod för tvång efter distributionens tids gräns (timmar)** i klient inställningar. Mer information finns i [dator agents](../../core/clients/deploy/about-client-settings.md#computer-agent) gruppen. Ange ett värde mellan **1** och **120** timmar.  

- På sidan **Schemaläggning** i en obligatorisk program distribution aktiverar du alternativet att **fördröja tvång av distributionen enligt användar inställningar, upp till den Respitperiod som definierats i klient inställningarna**. Den tvingande Grace-perioden gäller alla distributioner med det här alternativet aktiverat och riktas mot enheter som du också distribuerar klient inställningen till.

Efter tids gränsen installerar klienten programmet i det första icke-affärsfönstret, som användaren har konfigurerat, upp till den här Grace-perioden. Användaren kan dock fortfarande öppna Software Center och installera programmet när som helst. När Grace-perioden går ut återgår tvång till det normala beteendet för förfallna distributioner.

![Diagram över tids linje för Grace-period](media/grace-period.svg)

<!-- SCCMDocs issue #1599 -->

> [!Note]  
> I de flesta fall åtgärdar den här funktionen när enheten stängs av medan användaren inte är på kontoret. Som tekniskt sett startar Grace-perioden när klienten hämtar principer efter distributionens tids gräns. Samma sak uppstår om du stoppar Configuration Manager klient tjänsten (CcmExec) och sedan startar om den vid ett senare tillfälle efter distributionens tids gräns.

### <a name="deployment-user-experience-settings"></a><a name="bkmk_deploy-ux"></a>Inställningar för distributions **användar upplevelse**

På sidan **användar upplevelse** anger du information om hur användarna kan interagera med programinstallationen.

- **Användar meddelanden**: Ange om du vill visa meddelanden i Software Center på den konfigurerade tillgängliga tiden. Den här inställningen styr även om användarna ska meddelas på klient datorerna. För tillgängliga distributioner kan du inte välja alternativet att **dölja i Software Center och alla meddelanden**.  

    - **När program varu ändringar krävs visar du ett dialog fönster för användaren i stället för ett popup-meddelande**<!--3555947-->: Från och med version 1902 väljer du det här alternativet för att ändra användar upplevelsen till mer påträngande. Den gäller endast för nödvändiga distributioner. Mer information finns i [Planera för Software Center](../plan-design/plan-for-software-center.md#bkmk_impact).

- **Program varu installation** och **omstart av systemet**: Konfigurera bara de här inställningarna för nödvändiga distributioner. De anger beteenden när distributionen når tids gränsen utanför eventuella definierade underhålls fönster. Mer information om underhålls perioder finns i [använda underhålls](../../core/clients/manage/collections/use-maintenance-windows.md)perioder.  

- **Skriv filter hantering för Windows Embedded-enheter**: den här inställningen styr installations beteendet på Windows Embedded-enheter som är aktiverade med ett Skriv filter. Välj alternativet för att genomföra ändringar vid installationens tids gräns eller under en underhålls period. När du väljer det här alternativet krävs en omstart och ändringarna sparas på enheten. Annars installeras programmet på det tillfälliga överlägget och genomförs senare.  

    - När du distribuerar en program uppdatering till en Windows Embedded-enhet ser du till att enheten är medlem i en samling som har en konfigurerad underhålls period. Mer information om underhålls Windows-och Windows Embedded-enheter finns i [skapa Windows Embedded-program](../get-started/creating-windows-embedded-applications.md).  


### <a name="deployment-alerts"></a><a name="bkmk_deploy-alerts"></a>Distributions **aviseringar**

På sidan **aviseringar** konfigurerar du hur Configuration Manager genererar aviseringar för den här distributionen. Om du också använder System Center Operations Manager konfigurerar du även aviseringarna. Du kan bara konfigurera aviseringar för nödvändiga distributioner. 


## <a name="create-a-phased-deployment"></a><a name="bkmk_phased"></a>Skapa en stegvis distribution

<!--1358147-->
Från och med version 1806 skapar du en stegvis distribution för ett program. Med stegvisa distributioner kan du dirigera en samordnad, sekvenserad distribution av program vara utifrån anpassningsbara kriterier och grupper. Du kan t. ex. distribuera programmet till en pilot samling och sedan fortsätta distributionen automatiskt baserat på lyckade villkor.

Mer information finns i följande artiklar:  

- [Skapa en fasindelad distribution](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Hantera och övervaka fasindelade distributioner](../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  



## <a name="delete-a-deployment"></a><a name="bkmk_delete"></a>Ta bort en distribution

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **program hantering**och välj antingen noden **program** eller **program grupper** .  

2. Välj det program eller den program grupp som innehåller den distribution som du vill ta bort.  

3. Växla till fliken **distributioner** i informations fönstret och välj distributionen.  

4. Klicka på **ta bort**på fliken **distribution** och **distributions** gruppen i menyfliksområdet.  

När du tar bort en program distribution tas alla instanser av programmet som klienten redan har installerat bort. Om du vill ta bort de här programmen distribuerar du programmet till datorer att **Avinstallera**. Om du tar bort en program distribution eller tar bort en resurs från samlingen som du distribuerar till, visas inte längre programmet i Software Center.



## <a name="user-notifications-for-required-deployments"></a><a name="bkmk_notify"></a>Användar meddelanden för nödvändiga distributioner

När användarna får nödvändig program vara och väljer inställningen **vilo läge och Påminn mig** , kan de välja mellan följande alternativ:  

- **Senare**: anger att meddelanden ska schemaläggas baserat på de meddelande inställningar som kon figurer ATS i klient inställningar.  

- **Fast tid**: anger att meddelandet har schemalagts att visas efter den valda tiden. Om du till exempel väljer 30 minuter visas meddelandet igen om 30 minuter.  

![Dator agent grupp i inställningar för standard klient](media/ComputerAgentSettings.png)

Den maximala tiden för vilo läge baseras alltid på de aviserings värden som kon figurer ATS i klient inställningarna vid varje tidpunkt längs drift tids linjen. Ett exempel:  

- Du konfigurerar **distributions tids gränsen på mer än 24 timmar, Påminn användarna var som än är (timmar)** på sidan **dator agent** under 10 timmar.  

- Klienten visar meddelande dialog rutan mer än 24 timmar innan tids gränsen för distributionen.  

- Dialog rutan visar vilo läges alternativ upp till men aldrig större än 10 timmar.  

- När tids gränsen för distributionen närmar sig visar dialog rutan färre alternativ. De här alternativen är konsekventa med relevanta klient inställningar för varje komponent i distributions tids linjen.  

För en distribution med hög risk, till exempel en aktivitetssekvens som distribuerar ett operativ system, är användar aviserings upplevelsen mer påträngande. I stället för ett tillfälligt meddelande i aktivitets fältet visas en dialog ruta som följande visas varje gång du får ett meddelande om att kritiskt program varu underhåll krävs:

![Dialog rutan nödvändig program vara meddelar dig om kritiskt program varu underhåll](media/client-toast-notification.png)



## <a name="check-for-running-executable-files"></a><a name="bkmk_exe-check"></a>Sök efter körning av körbara filer

Konfigurera en distribution för att kontrol lera om vissa körbara filer körs på klienten. Använd det här alternativet om du vill söka efter processer som kan störa installationen av programmet. Om någon av dessa körbara filer körs, blockerar klienten installationen av distributions typen. Användaren måste stänga den körbara fil som körs innan klienten kan installera distributions typen. För distributioner med syftet obligatorisk kan klienten automatiskt stänga den körbara filen som körs.

1. Öppna dialog rutan **Egenskaper** för distributions typen.  

2. Växla till fliken **installations beteende** och klicka på **Lägg till**.  

3. Ange namnet på den körbara filens målfil i dialog rutan **Lägg till körbar fil** . Alternativt kan du ange ett eget namn för programmet som hjälper dig att identifiera det i listan.  

4. Klicka på **OK**och sedan på **OK** för att stänga fönstret Egenskaper för distributions typ.  

5. När du distribuerar programmet väljer du alternativet för att **automatiskt stänga alla körbara filer som du har angett på fliken installations beteende i dialog rutan Egenskaper för distributions typ**. Det här alternativet finns på fliken **distributions inställningar** i distributions egenskaperna.  

> [!Note]
> Om du konfigurerar ett program för att söka efter körning av körbara filer och inkluderar det i steget [installera program](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) , kommer aktivitetssekvensen inte att installera den. Om du inte konfigurerar den här aktivitetssekvensen för att fortsätta med felet Miss lyckas hela aktivitetssekvensen.

### <a name="client-behaviors-and-user-notifications"></a>Klient beteenden och användar meddelanden

När klienterna har tagit emot distributionen gäller följande:  

- Om du har distribuerat programmet som **tillgängligt**och en användare försöker installera det, ber klienten användaren att stänga de angivna körbara filerna innan du fortsätter med installationen.  

- Om du har distribuerat programmet efter **behov**och angett att **automatiskt stänga alla körbara filer som du har angett på fliken installations beteende i dialog rutan Egenskaper för distributions typ**, visar klienten ett meddelande. Det informerar användaren om att de angivna körbara filerna stängs automatiskt när tids gränsen för programinstallationen har nåtts.  

    - Schemalägg dessa dialog rutor i **dator agent** gruppen för klient inställningar. Mer information finns i [dator agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

    - Om du inte vill att användaren ska se dessa meddelanden väljer du alternativet att **dölja i Software Center och alla meddelanden** på fliken **användar upplevelse** i distributionens egenskaper. Mer information finns i [Inställningar för distribution av användar upplevelser](#bkmk_deploy-ux).  

- Om du har distribuerat programmet vid **behov**och inte angav att **automatiskt stänga eventuella körbara filer som du har angett på fliken installations beteende i dialog rutan Egenskaper för distributions typ**, Miss lyckas installationen av appen om ett eller flera av de angivna programmen körs.  



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Distribuera användar tillgängliga program på Azure AD-anslutna enheter

<!-- 1322613 -->
Om du distribuerar program som tillgängliga för användare kan de söka efter och installera dem via Software Center på Azure Active Directory (Azure AD)-enheter.  

### <a name="prerequisites"></a>Krav

- Aktivera HTTPS på hanterings platsen  

- Integrera webbplatsen med [Azure AD](../../core/servers/deploy/configure/azure-services-wizard.md) för **moln hantering**  

    - Konfigurera [identifiering av Azure AD-användare](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

- Distribuera ett program som tillgängligt för en samling användare från Azure AD  

- Distribuera alla program innehåll till en [moln distributions plats](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- Aktivera klient inställningen **Använd nya Software Center** i [dator agent](../../core/clients/deploy/about-client-settings.md#computer-agent) gruppen  

- Klientens operativ system måste vara Windows 10 och ansluten till Azure AD. Antingen som enbart molnbaserad domänanslutna eller hybrid Azure AD-anslutna.  

- För att stödja Internetbaserade klienter:  

    - [Gateway för molnhantering](../../core/clients/manage/cmg/plan-cloud-management-gateway.md)  

    - Aktivera klient inställningen: **Aktivera användar princip begär Anden från Internet klienter** i [klient princip](../../core/clients/deploy/about-client-settings.md#client-policy) gruppen  

- Stöd för klienter på intranätet:  

    - Lägg till moln distributions platsen i en begränsande grupp som används av klienterna  

    - Klienterna måste matcha det fullständigt kvalificerade domän namnet (FQDN) för den HTTPS-aktiverade hanterings platsen  



## <a name="next-steps"></a>Nästa steg

- [Övervakning av program](monitor-applications-from-the-console.md)
- [Felsöka programdistributioner](troubleshoot-application-deployment.md)
- [Hanterings uppgifter för program](management-tasks-applications.md)
- [Användarhandbok för Software Center](../../core/understand/software-center.md)
