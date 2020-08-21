---
title: Självstudie – distribuera Windows 10
titleSuffix: Configuration Manager
description: En själv studie kurs om att använda Desktop Analytics och Configuration Manager för att distribuera Windows 10 till en pilot grupp.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 5c5337433b0d64ec1f6bf1efae97bd2391031f2e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694277"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Självstudie: distribuera Windows 10 till pilot

I den här självstudien används Desktop Analytics och Configuration Manager för att distribuera Windows 10 till en pilot grupp. Den fokuserar på integreringen av moln tjänsten för att leverera insikter om att distribuera Windows med den lokala produkten. Använd Skriv bords analys för att fastställa de bästa enheterna som ska läggas i en pilot grupp. Använd sedan Configuration Manager för att bli uppdaterad med Windows.

I den här guiden får du lära dig att:  

> [!div class="checklist"]  
> * Konfigurera Skriv bords analys i Azure Portal  
> * Anslut Configuration Manager och konfigurera enhets inställningar  
> * Skapa en distributions plan för Skriv bords analys för Windows 10  
> * Använd Configuration Manager för att distribuera Windows 10 till pilot gruppen  

Om du inte har någon Azure-prenumeration kan du skapa ett [kostnadsfritt konto](https://azure.microsoft.com/free) innan du börjar. När den är korrekt konfigurerad, kostar inte användningen av Desktop Analytics någon Azure-kostnad.

Skriv bords analys använder en *Log Analytics arbets yta* i din Azure-prenumeration. En arbetsyta är i grunden en container som innehåller kontoinformation och enkel konfigurationsinformation för kontot. Mer information finns i [hantera arbets ytor](/azure/log-analytics/log-analytics-manage-access?toc=%2fazure%2fazure-monitor%2ftoc.json).



## <a name="prerequisites"></a>Förutsättningar

Innan du börjar den här självstudien måste du kontrol lera att du har följande krav:  

- En aktiv Azure-prenumeration med [**globala administratörs**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions) behörigheter  

    Mer information finns i [krav för Skriv bords analys](overview.md#prerequisites).

- Configuration Manager version 1902 med Samlad uppdatering (4500571) eller senare med **fullständig administratörs** roll  

- Installations medium för den senaste versionen av Windows 10

- Minst en Windows 10-enhet med följande konfigurationer:  

    - Windows 10, version 1709 eller senare, men mindre än den version av installations mediet som du planerar att använda

    - Senaste kumulativa kvalitets uppdateringen för Windows 10  

    - Configuration Manager-klient version 1902 med Samlad uppdatering (4500571) eller senare  

- Affärs godkännande för att konfigurera Windows-diagnostikdata till **valfri (begränsad)** på pilot enheterna  

    Mer information finns i [Sekretess för Desktop Analytics](privacy.md).

- Nätverks anslutning från enheten till följande Internet slut punkter:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net` (endast på Configuration Manager Server roll)
    - `https://*.manage.microsoft.com` (endast på Configuration Manager Server roll)

    Mer information finns i [så här aktiverar du data delning för Skriv bords analys](enable-data-sharing.md#endpoints).  

> [!Important]  
> Dessa krav gäller för de här självstudierna. Mer information om de allmänna kraven för Skriv bords analys med Configuration Manager finns i [krav](overview.md#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Ställ in Desktop Analytics

Använd den här proceduren för att logga in på Desktop Analytics och konfigurera den i din prenumeration. Den här proceduren är en engångs process för att konfigurera Skriv bords analys för din organisation.  

1. Öppna [Skriv bords analys portalen](https://aka.ms/desktopanalytics) i Microsoft 365 enhets hantering som en användare med **globala administratörs** behörigheter. Välj **Starta**.  

2. På sidan **Godkänn service avtal** granskar du service avtalet och väljer **Godkänn**.  

3. På sidan **Bekräfta din prenumeration** finns listan över nödvändiga kvalificerings licenser för Windows-enhetens hälso funktioner i Skriv bords analys. Välj **Nästa** för att fortsätta.  

4. På sidan **ge användare åtkomst** :

    - **Tillåt Skriv bords analys för att hantera katalog roller åt dig**: Skriv bords analys tilldelar automatiskt **arbets ytans ägare** rollen som **Skriv bords administratör** . Om dessa grupper redan är en **Global administratör**sker ingen ändring.  

        Om du inte väljer det här alternativet lägger Desktop Analytics fortfarande till användare som medlemmar i säkerhets gruppen. En **Global administratör** måste tilldela rollen **Desktop Analytics-administratör** manuellt för användarna.  

        Mer information om hur du tilldelar administratörs roll behörigheter i Azure Active Directory och de behörigheter som tilldelats **Desktop Analytics-administratörer**finns [i administratörs roll behörigheter i Azure Active Directory](/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analytics förkonfigurerar säkerhets gruppen **ägare till arbets ytan** i Azure Active Directory för att skapa och hantera arbets ytor och distributions planer. 

        Om du vill lägga till en användare i gruppen skriver du dess namn eller e-postadress i avsnittet **Ange namn eller e-postadress** . När du är klar väljer du **Nästa**.

5. På sidan för att **Konfigurera din arbets yta**:  

    > [!Note]  
    > För att slutföra det här steget måste användaren ha ägar behörigheter för **arbets ytan** och ytterligare åtkomst till Azure-prenumerationen och resurs gruppen. Mer information finns i [krav](overview.md#prerequisites).  

    - Välj din Azure-prenumeration.  

    - Om du vill använda en befintlig arbets yta för Skriv bords analys väljer du den och fortsätter med nästa steg.  

    - Om du vill skapa en arbets yta för Desktop Analytics väljer du **Lägg till arbets yta**.  

        1. Ange ett **namn på arbets ytan**.  

        2. Välj den nedrullningsbara List rutan för att **välja namnet på Azure-prenumerationen för den här arbets ytan**och välj Azure-prenumerationen för den här arbets ytan.  

        3. **Skapa ny** Resurs grupp eller **Använd befintlig**.  

        4. Välj **region** i listan och välj sedan **Lägg till**.  

6. Välj en ny eller befintlig arbets yta och välj sedan **Ange som Desktop Analytics-arbetsyta**.  Välj sedan **Fortsätt** i dialog rutan **Bekräfta och bevilja åtkomst** .  

7. På fliken ny webbläsare väljer du ett konto som du vill använda för att logga in. Välj alternativet att godkänna **för din organisations räkning** och välj **Godkänn**.  


    > [!Note]  
    > Detta medgivande är att tilldela MALogAnalyticsReader-programmet rollen Log Analyticss läsare för arbets ytan. Den här program rollen krävs av Desktop Analytics. Mer information finns i [program rollen MALogAnalyticsReader](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. Gå tillbaka till sidan för att **Konfigurera din arbets yta**och välj **Nästa**.  

9. På sidan **sista steg** väljer **du gå till Skriv bords analys**. Azure Portal visar **Start** sidan för Skriv bords analys.  



## <a name="connect-configuration-manager"></a>Ansluta Configuration Manager

Använd den här proceduren för att uppdatera Configuration Manager, ansluta till Skriv bords analys och konfigurera enhets inställningar. Den här proceduren är en eng ång slö process för att koppla din hierarki till moln tjänsten.  

### <a name="update-configuration-manager"></a>Uppdatera Configuration Manager

Installera Configuration Manager version 1902 Samlad uppdatering (4500571) för att stödja integrering med Desktop Analytics. Mer information om den här uppdateringen finns i samlad [uppdatering för Configuration Manager aktuella grenen, version 1902](https://support.microsoft.com/help/4500571).

1. Uppdatera platsen med den samlade uppdateringen för version 1902. Mer information finns i [Installera uppdateringar i konsolen](../core/servers/manage/install-in-console-updates.md).  

2. Uppdatera klienter. Överväg att använda automatisk klient uppgradering för att förenkla den här processen. Mer information finns i [Uppgradera klienter](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Anslut till tjänsten

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Azure-tjänster** . Välj **Konfigurera Azure-tjänster** i menyfliksområdet.  

2. Konfigurera följande inställningar på sidan **Azure-tjänster** i guiden Azure-tjänster:  

    - Ange ett **namn** för objektet i Configuration Manager  

    - Ange en valfri **Beskrivning** som hjälper dig att identifiera tjänsten  

    - Välj **Skriv bords analys** i listan över tillgängliga tjänster  
  
   Välj **Nästa**.  

3. På sidan **app** väljer du lämplig Azure- **miljö**. Välj sedan **Bläddra** efter webbappen.

4. Välj **skapa** för att enkelt lägga till en Azure AD-App för Skriv bords analys anslutningen.

5. Konfigurera följande inställningar i fönstret **skapa serverprogram** :  

    - **Program namn**: ett eget namn för appen i Azure AD.

    - **Start sidans URL**: det här värdet används inte av Configuration Manager, men krävs av Azure AD. Det här värdet är som standard `https://ConfigMgrService`.  

    - **App-ID-URI**: det här värdet måste vara unikt i din Azure AD-klient. Den finns i åtkomsttoken som används av Configuration Manager-klienten för att begära åtkomst till tjänsten. Det här värdet är som standard `https://ConfigMgrService`.  

    - **Giltighets period för hemlig nyckel**: Välj antingen **1 år** eller **2 år** i list rutan. Ett år är standardvärdet.  

    Välj **Logga in**. När du har autentiserat till Azure visar sidan namnet på **Azure AD-klienten** för referensen.

    > [!Note]  
    > Slutför det här steget som **Global administratör**. Autentiseringsuppgifterna sparas inte av Configuration Manager. Den här personen behöver inte behörigheter i Configuration Manager och behöver inte vara samma konto som kör guiden Azure-tjänster.  

    Välj **OK** för att skapa webbappen i Azure AD och Stäng dialog rutan skapa serverprogram. I dialog rutan Server App väljer du **OK**. Välj sedan **Nästa** på sidan app i guiden Azure-tjänster.  

6. Konfigurera följande inställningar på sidan **diagnostikdata** :  

    - **Kommersiellt ID**: det här värdet ska automatiskt fyllas i med ORGANISATIONens ID  

    - **Windows 10-diagnostisk data nivå**: Välj minst **valfritt (begränsat)**  

    - **Tillåt enhets namn i diagnostikdata**: Välj **Aktivera**  
  
   Välj **Nästa**. Sidan **tillgängliga funktioner** visar de Skriv bords analys funktioner som är tillgängliga med inställningarna för diagnostikdata från föregående sida. Välj **Nästa**.  

7. Konfigurera följande inställningar på sidan **samlingar** :  

    - **Visnings namn**: Skriv bords analys portalen visar den här Configuration Manager anslutningen med det här namnet. Använd den för att skilja mellan olika hierarkier. Till exempel *test labb* eller *produktion*.  

    - **Mål samling**: den här samlingen innehåller alla enheter som Configuration Manager konfigurerar med inställningarna för ditt handels-ID och diagnostikdata. Det är en fullständig uppsättning enheter som Configuration Manager ansluter till Skriv bords analys tjänsten.  

    - **Enheter i mål samlingen använder en användar autentiserad proxy för utgående kommunikation**: som standard är det här värdet **Nej**. Ange till **Ja**om det behövs i din miljö.  

    - **Välj vissa samlingar som ska synkroniseras med Desktop Analytics**: Välj **Lägg till** om du vill inkludera ytterligare samlingar. Dessa samlingar är tillgängliga i Skriv bords analys portalen för gruppering med distributions planer. Se till att inkludera samlingar av pilot-och pilot undantags samlingar.  

        De här samlingarna fortsätter att synkroniseras när deras medlemskap ändras. Din distributions plan använder till exempel en samling med en regel för Windows 7-medlemskap. När enheterna uppgraderar till Windows 10 och Configuration Manager utvärderar samlings medlemskapet, släpps dessa enheter ut ur samlingen och distributions planen.  

8. Slutför guiden.  

Configuration Manager skapar en inställnings princip för att konfigurera enheter i mål samlingen. Den här principen inkluderar inställningar för diagnostikdata för att göra det möjligt för enheter att skicka data till Microsoft. Som standard uppdaterar klienterna principer varje timme. När du har tagit emot de nya inställningarna kan det ta flera timmar innan data är tillgängliga i Skriv bords analys.

> [!Note]  
> Mer information om de här inställningarna finns i [Windows-inställningar](enroll-devices.md#windows-settings).  

Övervaka konfigurationen av dina enheter för Skriv bords analys. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera noden **Skriv bords analys** och välj instrument panelen för **hälso tillstånd för anslutning** .  

Configuration Manager synkroniserar samlingarna inom 60 minuter när anslutningen upprättas. Gå till **Global pilot**i Skriv bords analys portalen och se Configuration Manager enhets samlingar. Det kan ta två till tre dagar innan resten av portalen visar fullständiga data. Mer information finns i [data svars tid](troubleshooting.md#data-latency).

## <a name="create-a-desktop-analytics-deployment-plan"></a>Skapa en distributions plan för Skriv bords analys

Använd den här proceduren för att skapa en distributions plan i Desktop Analytics.

1. Öppna [Skriv bords analys portalen](https://aka.ms/desktopanalytics). Använd autentiseringsuppgifter som har minst behörighet för **arbets ytans deltagare** .  

2. Välj **distributions planer** i gruppen hantera.  

3. I fönstret **distributions planer** väljer du **skapa**.  

4. Konfigurera följande inställningar i fönstret **skapa distributions plan** :  

    - **Namn**: ett unikt namn för distributions planen, till exempel `Windows 10 pilot`  

    - **Produkter och versioner**: Välj vilken Windows 10-version som ska distribueras. Microsoft rekommenderar att du skapar distributions planer som använder den senaste versionen.

    - **Enhets grupper**: Välj en eller flera grupper på fliken Configuration Manager och välj sedan **Ange som mål grupper**. De här grupperna är samlingar som synkroniseras från Configuration Manager.  

    - **Beredskaps regler**: de här reglerna hjälper dig att avgöra vilka enheter som är kvalificerade för uppgradering. Välj **Windows-operativsystem** och konfigurera följande inställningar:  

        - **Mina datorer hämtar automatiskt driv rutiner från Windows Update**: Standardinställningen är **inaktive rad**, vilket rekommenderas när du distribuerar med Configuration Manager.  

        - **Definiera tröskelvärdet för tröskelvärden för låg installation för dina appar**: standardvärdet är `2%` . Appar som är under det här tröskelvärdet anges automatiskt till *lågt antal installationer*. Desktop Analytics validerar inte dessa tillägg under piloten.  

            Om en app installeras på en högre procent andel av datorerna än det här tröskelvärdet markerar distributions planen appen *som en*försvars man. Sedan kan du bestämma vad som är viktigt att testa under pilot fasen.  

    - **Slut för ande datum**: Välj det datum då Windows ska distribueras fullständigt till alla mål enheter.  

5. Välj **Skapa**. Det nya schemat visas i listan över distributions planer medan bearbetningen bearbetas. Begär en data uppdatering på begäran för att påskynda bearbetningen. Mer information finns i [vanliga frågor och svar om Desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

6. Öppna distributions planen genom att välja dess namn.  

7. I gruppen **Förbered** på menyn distributions plan väljer du **identifiera prioritet**.  

    1. På fliken **appar** väljer du att visa endast **granskade** till gångar.  

    2. Markera varje app och välj sedan **Redigera**. Du kan välja mer än en app att redigera samtidigt.  

    3. Välj en prioritets nivå i **prioritets** listan. Om du vill att Desktop Analytics ska validera appen under piloten väljer du **kritisk** eller **viktig**. Den validerar inte appar som marker ATS som **inte viktiga**. Utvärdera dess [kompatibilitet](compat-assessment.md) och andra planera insikter när du tilldelar prioritets nivåer.  

        När du tilldelar prioritets nivåer kan du också välja uppgraderings beslutet.  

    4. Välj **Spara** när du är klar.  

8. Välj **identifiera pilot**i gruppen **Förbered** på menyn distributions plan.  

    1. Granska de rekommenderade enheterna för piloten.  

    2. Välj varje enhet och välj **Lägg till i pilot**. Om du inte godkänner rekommendationen väljer du **Ersätt**.  

        Om du vill ha mer information om hur Skriv bords analys gör dessa rekommendationer väljer du informations ikonen i det övre högra hörnet i fönstret **identifiera pilot** .



## <a name="deploy-windows-10-in-configuration-manager"></a>Distribuera Windows 10 i Configuration Manager

Använd den här proceduren för att distribuera Windows 10 i Configuration Manager till pilot gruppen.

- Om du inte redan har ett måste du först [skapa ett operativ system uppgraderings paket för Windows 10](#bkmk_create-package)  

- Om du inte redan har ett kan du [skapa en aktivitetssekvens för operativ system uppgradering för Windows 10](#bkmk_create-ts)  

- [Distribuera aktivitetssekvensen](#bkmk_deploy-ts) med hjälp av distributions planen för Skriv bords analys  

- [Installera aktivitetssekvensen](#bkmk_install-ts) från Software Center på en riktad enhet  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="create-an-os-upgrade-package-for-windows-10"></a><a name="bkmk_create-package"></a> Skapa ett uppgraderings paket för operativ system för Windows 10

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj sedan noden **uppgraderings paket för operativ system** .  

2. Välj **Lägg till uppgraderings paket för operativ system**i gruppen **skapa** på fliken **Start** i menyfliksområdet. Den här åtgärden startar guiden Lägg till uppgradering av operativ system.  

3. På sidan **data källa** anger du nätverks **Sök vägen** till installationskällfilerna för UPPGRADERINGS paketet för operativ systemet. Till exempel `\\server\share\path`.  

    > [!NOTE]  
    > Installations källorna innehåller setup.exe och andra filer och mappar för att installera operativ systemet.  

4. På sidan **Allmänt** anger du ett unikt **namn** för operativ system uppgraderings paketet.  

5. Slutför guiden Lägg till uppgraderings paket för operativ system.  

#### <a name="distribute-content"></a>Distribuera innehåll

Distribuera sedan operativ Systems uppgraderings paketet till distributions platser.  

1. Välj uppgraderings paketet för operativ systemet i listan. På fliken **Start** i menyfliksområdet väljer du **distribuera innehåll**i gruppen **distribution** . Guiden Distribuera innehåll öppnas.  

2. På sidan **Allmänt** kontrollerar du att innehållet i listan är det innehåll som du vill distribuera och väljer sedan **Nästa**.  

3. På sidan **innehålls mål** väljer du **Lägg till**och sedan **distributions plats**. Välj en befintlig distributions plats och välj sedan **OK**. När du är klar med att lägga till innehålls destinationer väljer du **Nästa**.  

4. Slutför guiden Distribuera innehåll.  


### <a name="create-an-os-upgrade-task-sequence-for-windows-10"></a><a name="bkmk_create-ts"></a> Skapa en aktivitetssekvens för operativ system uppgradering för Windows 10

1. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **operativ system**och välj sedan **aktivitetssekvenser**.  

2. Välj **skapa**aktivitetssekvens i gruppen **skapa** på fliken **Start** i menyfliksområdet.  

3. På sidan **skapa en ny aktivitetssekvens** i guiden skapa aktivitetssekvens väljer du **uppgradera ett operativ system från ett uppgraderings paket**och väljer sedan **Nästa**.  

4. På sidan **information** om aktivitetssekvens anger du ett **namn på aktivitetssekvensen** som identifierar aktivitetssekvensen.  

5. På sidan **Uppgradera operativ systemet Windows** anger du följande inställningar och väljer sedan **Nästa**:  

    - **Uppgraderings paket**: Ange det uppgraderings paket som innehåller källfilerna för operativ system uppgradering.  

    - **Versions index**: om det finns flera tillgängliga OS Edition-index i paketet väljer du det önskade versions indexet. Som standard väljs det första indexet i guiden.  

    - **Produkt nyckel**: Ange produkt nyckeln för Windows för det operativ system som ska installeras. Ange kodade volym licens nycklar eller standard produkt nycklar. Om du använder en standard produkt nyckel separerar du varje grupp om fem tecken med ett bindestreck (-). Till exempel: *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*. När uppgraderingen är för en volym licens version kanske produkt nyckeln inte krävs.  

        > [!Note]  
        > Den här produkt nyckeln kan vara en MAK (Multiple Activation Key) eller en allmän volym licens nyckel (GVLK). En GVLK kallas även för en klient installations nyckel för nyckel hanterings tjänst (KMS). Mer information finns i [Planera för volym aktivering](/windows/deployment/volume-activation/plan-for-volume-activation-client). En lista över konfigurations nycklar för KMS-klienter finns i [bilaga a](/windows-server/get-started/kmsclientkeys) i aktiverings guiden för Windows Server.

6. På sidan **Inkludera uppdateringar** väljer du **Nästa** om du inte vill installera några program uppdateringar.  

7. På sidan **installera program** väljer du **Nästa** om du inte vill installera några program.

8. Slutför guiden skapa aktivitetssekvens.  


### <a name="deploy-the-task-sequence-using-the-desktop-analytics-deployment-plan"></a><a name="bkmk_deploy-ts"></a> Distribuera aktivitetssekvensen med hjälp av distributions planen för Skriv bords analys

1. I Configuration Manager-konsolen går du till **program biblioteket**, expanderar **underhåll av Skriv bords analys**och väljer noden **distributions planer** .  

2. Välj din distributions plan för Windows 10 pilot och välj sedan **distributions Plans information** i menyfliksområdet.  

3. I panelen **pilot status** väljer du **aktivitetssekvens** i list rutan och väljer sedan **distribuera**.  

4. På sidan **Allmänt** i guiden distribuera program vara väljer du **Bläddra** bredvid fältet **program vara** . Välj en aktivitetssekvens för uppgradering av Windows 10 på plats och välj **Nästa**.  

    > [!Note]  
    > Med Desktop Analytics-integrering skapar Configuration Manager automatiskt pilot-och produktions samlingar för distributions planen. Innan du kan använda dem kan det ta tid för dessa samlingar att synkronisera. Mer information finns i [Felsök-data svars tid](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > Den här samlingen är reserverad för distributions Plans enheter för Desktop Analytics. Manuella ändringar av den här samlingen stöds inte.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Välj **Lägg till**på sidan **innehåll** och välj sedan **distributions plats**. Välj en tillgänglig distributions plats som är värd för installations innehållet och välj **OK**. Välj sedan **Nästa**.  

6. På sidan **distributions inställningar** väljer du **Nästa** för att godkänna standardinställningarna. (En tillgänglig installation.)  

7. På sidan **Schemaläggning** väljer du **Nästa** för att godkänna standardinställningarna. (Tillgängligt så snart som möjligt.)  

8. På sidan **användar upplevelse** väljer du **Nästa** för att godkänna standardinställningarna. (Visa i Software Center och Visa bara meddelanden om omstarter av datorn.)  

9. På sidan **aviseringar** väljer du **Nästa** för att godkänna standardinställningarna.  

10. Slutför guiden.  


### <a name="install-the-task-sequence-from-software-center"></a><a name="bkmk_install-ts"></a> Installera aktivitetssekvensen från Software Center

1. Logga in på en enhet som är medlem i pilot distributions planen.  

2. Öppna **Software Center** och installera det tillgängliga operativ systemet för Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Nästa steg

Fortsätt till nästa artikel om du vill lära dig mer om distributions planer för Station ära datorer.
> [!div class="nextstepaction"]  
> [Distributionsplaner](about-deployment-plans.md)