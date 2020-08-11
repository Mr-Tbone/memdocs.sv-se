---
title: Felsöka Desktop Analytics
titleSuffix: Configuration Manager
description: Teknisk information som hjälper dig att felsöka problem med Desktop Analytics.
ms.date: 08/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: e83e8d5d967b4cd3bbcb817c149cd40284bb5f9c
ms.sourcegitcommit: 66c58078a32af3872d98f7c62af4f8047ee81b50
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/11/2020
ms.locfileid: "88089953"
---
# <a name="troubleshoot-desktop-analytics"></a>Felsöka Desktop Analytics

Använd informationen i den här artikeln för att felsöka problem med Desktop Analytics integrerat med Configuration Manager.

## <a name="confirm-prerequisites"></a>Bekräfta krav

Många vanliga problem orsakas av att nödvändiga komponenter saknas. Bekräfta först följande konfigurationer:

- [Förutsättningar](overview.md#prerequisites)  

- [Uppdatering av Windows-komponenter](enroll-devices.md#update-devices)  

- [Så här aktiverar du data delning](enable-data-sharing.md), som omfattar följande ämnen:  

  - Internet-slutpunkter som klienter måste ansluta till  

  - Autentisering av proxyserver  

  - Diagnostiska data nivåer  

## <a name="monitor-connection-health"></a>Övervaka anslutningsstatus

Använd instrument panelen för **anslutningens hälso tillstånd** i Configuration Manager för att öka detalj nivån i kategorier efter enhets hälsa. Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera noden **Skriv bords analys** och välj instrument panelen för **hälso tillstånd för anslutning** .  

Mer information finns i [övervaka anslutnings hälsa](monitor-connection-health.md).

> [!NOTE]
> Configuration Manager anslutningen till Skriv bords analys förlitar sig på tjänst anslutnings punkten. Eventuella ändringar av den här plats system rollen kan påverka synkroniseringen med moln tjänsten. Mer information finns i [om tjänst anslutnings punkten](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

Från och med version 2002, om Configuration Manager-platsen inte kan ansluta till obligatoriska slut punkter för en moln tjänst, genererar den en kritisk status meddelande-ID 11488. När den inte kan ansluta till tjänsten ändras SMS_SERVICE_CONNECTOR komponent status till kritisk. Visa detaljerad status i noden [komponent status](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) i Configuration Manager-konsolen.<!-- 5566763 -->

## <a name="log-files"></a>Loggfiler

Mer information finns i [loggfiler för Desktop Analytics](../core/plan-design/hierarchy/log-files.md#desktop-analytics)

Från och med Configuration Manager version 1906 använder du **DesktopAnalyticsLogsCollector.ps1** verktyget från Configuration Manager installations katalog för att felsöka Desktop Analytics. Den kör vissa grundläggande fel söknings steg och samlar in relevanta loggar i en enda arbets katalog. Mer information finns i [loggar insamlare](log-collector.md).

### <a name="enable-verbose-logging"></a>Aktivera utförlig loggning

1. Gå till följande register nyckel på tjänst anslutnings punkten:`HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Ange värdet **LoggingLevel** till`0`  

## <a name="azure-ad-applications"></a><a name="bkmk_AzureADApps"></a>Azure AD-program

Desktop Analytics lägger till följande program i Azure AD:

- **Configuration Manager mikrotjänst**: ansluter Configuration Manager med Skriv bords analys. Den här appen har inga åtkomst krav.  

- **MALogAnalyticsReader**: övervakar din Azure Log Analytics-arbetsyta för att se till att den dagliga ögonblicks bilden har kopierats. Mer information finns i [program rollen MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

- **Skriv bords analys**: aktiverar Configuration Manager hämtning av distributions Plans information och status för enhets beredskap från Skriv bords analys.

Om du behöver etablera dessa appar när du har slutfört installationen går du till fönstret **anslutna tjänster** . Välj **Konfigurera användare och appar åtkomst**och etablera apparna.  

- **Azure AD-App för Configuration Manager**. Om du behöver etablera eller felsöka anslutnings problem när du har slutfört installationen, se [skapa och importera app för Configuration Manager](#create-and-import-app-for-configuration-manager). Den här appen kräver data för att **skriva cm-samling** och **läsa cm-samlings data** i **Configuration Manager tjänst-** API: et.  

    > [!NOTE]
    > Desktop Analytics stöder flera Configuration Manager hierarkier som rapporterar till en enda Azure AD-klient.<!-- 4814075 --> Om du har flera hierarkier i din miljö som kon figurer ATS med samma handels-ID kan du använda [olika appar](connect-configmgr.md#bkmk_connect) för varje hierarki för att dela Azure AD-klienten och Desktop Analytics-instansen.

### <a name="create-and-import-app-for-configuration-manager"></a>Skapa och importera app för Configuration Manager

Om du inte kan skapa Azure AD-appen för Configuration Manager i guiden Konfigurera Azure-tjänster, eller om du vill återanvända en befintlig app, måste du skapa och importera den manuellt. Använd följande steg när du har slutfört den [inledande onboarding](set-up.md#initial-onboarding) på Skriv bordet Analytics-portalen:

#### <a name="create-app-in-azure-ad"></a>Skapa app i Azure AD

1. Öppna [Azure Portal](https://portal.azure.com) som en användare med *globala administratörs* behörigheter, gå till **Azure Active Directory**och välj **Appregistreringar**. Välj sedan **ny registrering**.  

2. Konfigurera följande inställningar på panelen **skapa** :  

    - **Namn**: ett unikt namn som identifierar appen, till exempel:`Desktop-Analytics-Connection`  

    - **Konto typer som stöds**: **konton endast i den här organisatoriska katalogen (contoso)**

    - **Omdirigerings-URI (valfritt)**: **webb**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    Välj **Registrera**.  

3. Välj appen, anteckna **program** -ID och **katalog (** klient) ID. Värdena är GUID som används för att konfigurera Configuration Manager anslutningen.  

4. I menyn **Hantera** väljer du **certifikat & hemligheter**. Välj **Ny klienthemlighet**. Ange en **Beskrivning**, ange en förfallo tid och välj sedan **Lägg till**. Kopiera **värdet** för nyckeln, som används för att konfigurera Configuration Manager anslutningen.

    > [!Important]  
    > Detta är den enda möjligheten att kopiera nyckelvärdet. Om du inte kopierar den nu måste du skapa en ny nyckel.  
    >
    > Spara nyckelvärdet på en säker plats.  

5. I menyn **Hantera** väljer du **API-behörigheter**.  

    1. I panelen **API-behörigheter** väljer du **Lägg till en behörighet**.  

    2. I panelen **API-behörigheter för begäran** växlar du till de **API: er som används i organisationen**.  

    3. Sök efter och välj **Configuration Manager mikrotjänst-** API: et.  

    4. Välj gruppen **program behörigheter** . Expandera **CmCollectionData**och välj båda följande behörigheter: **skriva cm samlings data** och **läsa cm-Datadata**.  

    5. Välj **Lägg till behörigheter**.  

6. På panelen **API-behörigheter** väljer du **bevilja administratörs medgivande...**. Välj **Ja**.  

#### <a name="import-app-in-configuration-manager"></a>Importera app i Configuration Manager

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Azure-tjänster** . Välj **Konfigurera Azure-tjänster** i menyfliksområdet.  

2. Konfigurera följande inställningar på sidan **Azure-tjänster** i guiden Azure-tjänster:  

    - Ange ett **namn** för objektet i Configuration Manager.  

    - Ange en valfri **Beskrivning** som hjälper dig att identifiera tjänsten.  

    - Välj **Skriv bords analys** i listan över tillgängliga tjänster.  
  
   Välj **Nästa**.  

3. På sidan **app** väljer du lämplig Azure- **miljö**. Välj sedan **Importera** för webb programmet. Konfigurera följande inställningar i fönstret **Importera appar** :  

    - **Namn på Azure AD-klient organisation**: det här namnet är det som namnges i Configuration Manager  

    - **Azure AD-klient-ID**: **katalog-ID: t** som du KOPIERAde från Azure AD  

    - **Klient-ID**: det **program-ID** som du KOPIERADE från Azure AD-appen  

    - **Hemlig nyckel**: det nyckel **värde** som du KOPIERAde från Azure AD-appen  

    - **Förfallo datum för hemlig nyckel**: samma förfallo datum för nyckeln  

    - **URI för app-ID**: den här inställningen ska automatiskt fylla i med följande värde:`https://cmmicrosvc.manage.microsoft.com/`  
  
   Välj **Verifiera**och välj sedan **OK** för att stänga fönstret Importera appar. Välj **Nästa** på sidan app i guiden Azure-tjänster.  

Om du vill fortsätta med resten av guiden på sidan **diagnostikdata** , se [Anslut till tjänsten](connect-configmgr.md#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Felsök appen i Configuration Manager

Om du har problem med att skapa eller importera appen ska du först kontrol lera **SMSAdminUI. log** efter det aktuella felet. Kontrol lera sedan följande konfigurationer:

- Du har registrerat klienten på Skriv bordet Analytics-tjänsten. Mer information finns i [så här konfigurerar du Skriv bords analys](set-up.md).

- Alla nödvändiga slut punkter är tillgängliga. Mer information finns i [slut punkter](enable-data-sharing.md#endpoints).

- Se till att användaren som loggar in har rätt behörigheter. Mer information finns i [krav](overview.md#prerequisites).

- Se till att användaren kan logga in i Azure i allmänhet. Den här åtgärden avgör om det finns några allmänna problem med Azure AD-autentisering.

- Kontrol lera status meddelanden för **SMS_SERVICE_CONNECTOR** -komponenten om *Desktop Analytics Worker*.

### <a name="maloganalyticsreader-application-role"></a><a name="bkmk_MALogAnalyticsReader"></a>MALogAnalyticsReader program roll

När du konfigurerar Desktop Analytics godkänner du din organisations räkning. Detta medgivande är att tilldela MALogAnalyticsReader-programmet rollen Log Analyticss läsare för arbets ytan. Den här program rollen krävs av Desktop Analytics.

Om det uppstår ett problem med den här processen under installationen kan du använda följande process för att manuellt lägga till den här behörigheten:

1. Gå till [Azure Portal](https://portal.azure.com)och välj **alla resurser**. Välj arbets ytan av typen **Log Analytics**.  

2. I menyn arbets yta väljer du **åtkomst kontroll (IAM)** och väljer sedan **Lägg till**.  

3. Konfigurera följande inställningar på panelen **Lägg till behörigheter** :  

    - **Roll**: **läsare**  

    - **Tilldela åtkomst till**: **Azure AD-användare,-grupp eller-program**  

    - **Välj**: **MALogAnalyticsReader**  

4. Välj **Spara**.

Portalen visar ett meddelande om att roll tilldelningen lades till.

## <a name="data-latency"></a>Datasvarstid

<!-- 3846531 -->
När du först konfigurerar Desktop Analytics, registrerar nya klienter eller konfigurerar nya distributions planer kan rapporterna i Configuration Manager och skriv bords analys portalen inte Visa fullständiga data direkt. Det kan ta 2-3 dagar innan följande steg uppstår:

- Aktiva enheter skicka diagnostikdata till Skriv bords analys tjänsten
- Tjänsten bearbetar data
- Tjänsten synkroniseras med din Configuration Manager webbplats

När du synkroniserar enhets samlingar från Configuration Manager-hierarkin till Desktop Analytics kan det ta upp till en timme innan dessa samlingar visas i Skriv bords analys portalen. När du skapar en distributions plan i Desktop Analytics kan det ta upp till en timme innan de nya samlingarna som är kopplade till distributions planen visas i Configuration Manager hierarkin. De primära platserna skapar samlingarna och den centrala administrations platsen synkroniseras med Desktop Analytics. Configuration Manager kan ta upp till 24 timmar att utvärdera och uppdatera medlemskap i samlingar. Uppdatera samlings medlemskapet manuellt för att påskynda processen.<!-- 4984639 -->

> [!Note]
> För manuella samlings uppdateringar som visar ändringar måste SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker-komponenten först synkronisera. Det kan ta upp till en timme för den här processen att köras. Mer information finns i **M365ADeploymentPlanWorker. log**.

I Skriv bords analys portalen finns det två typer av data: **Administratörs data** och **diagnostikdata**:

- **Administratörs data** refererar till alla ändringar du gör i konfigurationen av arbets ytan. Till exempel när du ändrar en till gångs **uppgraderings beslut** eller **prioritet** ändrar du administratörs data. Dessa ändringar har ofta en sammansatt funktion eftersom de kan ändra beredskaps statusen hos en enhet med till gången i fråga installerad.

- **Diagnostikdata** avser systemmetadata som laddats upp från klient enheter till Microsoft. Dessa data ger Skriv bords analys. Den innehåller attribut som enhets inventering och status för säkerhets-och funktions uppdatering.

Som standard uppdateras alla data i Skriv bords analys portalen automatiskt varje dag. Uppdateringen innehåller ändringar i diagnostikdata från två dagar sedan och eventuella ändringar som du gör i konfigurationen (administratörs data). Den bör vara synlig i din station ära Analytics-Portal med 08:00 AM UTC varje dag.

När du gör ändringar i administratörs data kan du utlösa en uppdatering på begäran av administratörs data i din arbets yta. Från valfri sida i Skriv bords analys portalen öppnar du utfällda data valuta:

![Skärm bild av fliken utfällbar data valuta i Analytics Portal för Station ära datorer](media/data-currency-flyout.png)

Välj sedan **tillämpa ändringar**:

![Skärm bild av expanderad data valuta utfälld i Skriv bords analys Portal](media/data-currency-flyout-expand.png)

Den här processen tar i allmänhet mellan 15-60 minuter. Tiden beror på arbets ytans storlek och omfattningen av de ändringar som behöver processer. När du begär en data uppdatering på begäran resulterar det inte i några ändringar av diagnostikdata.  Mer information finns i [vanliga frågor och svar om Desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Om du inte ser ändringar som uppdaterats inom de tids ramar som anges ovan väntar du en till 24 timmar för nästa dagliga uppdatering. Om du ser längre fördröjningar kan du kontrol lera instrument panelen för hälso tillstånd. Kontakta Microsoft-supporten om tjänsten rapporterar som felfri.<!-- 3896921 -->

> [!IMPORTANT]
> Alternativet Skriv bords analys för att **Visa senaste data** är föråldrat. Den här åtgärden kommer att tas bort i en framtida version av Desktop Analytics-tjänsten. Mer information finns i [föråldrade funktioner](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

## <a name="service-notifications"></a>Tjänstmeddelanden

<!-- 4982509 -->

Skriv bords analys portalen kan visa meddelande banderoller för administratörer. Dessa aviseringar gör att Microsoft kan kommunicera med dig om viktiga händelser och problem. Följande avsnitt innehåller information om de meddelanden som du kan se.

### <a name="see-whats-new-this-month-in-desktop-analytics"></a>Se vad som är nytt den här månaden i Skriv bords analys

Detta informations meddelande gör att du kan känna till ändringar i tjänsten. Mer information finns i [Nyheter i Desktop Analytics](whats-new.md) ( `https://aka.ms/danews` ).

### <a name="there-are-new-prerequisites-to-continue-using-desktop-analytics-review-the-new-requirements"></a>Det finns nya krav. Om du vill fortsätta använda Skriv bords analys granskar du de nya kraven

Detta informations meddelande gör att du kan tänka på ändringar i kraven. Till exempel en ny Internet-slutpunkt eller program uppdatering. Mer information finns i [krav](overview.md#prerequisites) ( `https://aka.ms/daprereqs` ).

### <a name="were-investigating-an-issue-that-impacts-desktop-analytics"></a>Vi undersöker ett problem som påverkar Desktop Analytics

Detta varnings meddelande anger att Microsoft är medveten om ett problem som påverkar Desktop Analytics-tjänsten. Problemet är vanligt vis när du skapar ögonblicks bilder. När du ser det här meddelandet undersöker Microsoft problemet för att fastställa omfattningen och källan till påverkan. Du behöver inte kontakta Microsoft Support. Mer information finns i [data flöde](privacy.md#data-flow).

### <a name="were-investigating-an-issue-with-data-latency-if-you-enrolled-new-devices-or-changed-any-assets-in-the-last-24-hours-they-may-not-appear-right-away"></a>Vi undersöker ett problem med data svars tiden. Om du har registrerat nya enheter eller ändrat några till gångar under de senaste 24 timmarna, kanske de inte visas omedelbart

Detta varnings meddelande anger att Microsoft är medveten om ett problem som påverkar Desktop Analytics-tjänsten. Microsoft övervakar kontinuerligt tjänsten för att bekräfta att alla komponenter uppdaterar ögonblicks bilder vid rätt tidpunkt. Under den här övervakningen slutfördes inte någon av dessa komponenter som förväntat. När du ser det här meddelandet undersöker Microsoft problemet. Du behöver inte kontakta Microsoft Support. Mer information finns i [data flöde](privacy.md#data-flow).

Om du nyligen har [registrerat enheter](enroll-devices.md) eller ändrat [till gångar](about-assets.md)väntar du tills Microsoft löser problemet. Du behöver inte upprepa några åtgärder.

### <a name="weve-resolved-a-temporary-issue-with-data-latency-daily-refresh-of-portal-data-is-delayed"></a>Vi har löst ett tillfälligt problem med data fördröjning. Daglig uppdatering av Portal data är försenad

Med det här meddelandet vet du att det uppstod ett problem med data svars tiden. Tjänsten bearbetar fortfarande ögonblicks bilden och uppdatering av data är fördröjd. Mer information finns i [data svars tid](#data-latency).

### <a name="weve-resolved-an-issue-with-data-latency-if-you-enrolled-new-devices-or-changed-any-assets-in-the-last-24-hours-they-may-not-appear-right-away"></a>Vi har löst ett problem med data svars tiden. Om du har registrerat nya enheter eller ändrat några till gångar under de senaste 24 timmarna, kanske de inte visas omedelbart

Med det här meddelandet vet du att Microsoft har löst ett tidigare rapporterat problem med data svars tiden. Du kan se inaktuella data för morgon dagens ögonblicks bilder. Om du har [registrerat enheter](enroll-devices.md) eller gjort ändringar i enhets konfigurationen under de senaste 24 timmarna visas de inte direkt i portalen. Du kan fortsätta att använda Desktop Analytics för att kategorisera [till gångar](about-assets.md) och förbereda [distributions planer](about-deployment-plans.md). De här åtgärderna kan använda data från föregående ögonblicks bild.

### <a name="weve-resolved-an-issue-with-desktop-analytics-daily-refresh-of-the-portal-data-is-on-track"></a>Vi har löst ett problem med Desktop Analytics. Daglig uppdatering av Portal data är på spåret

I det här meddelandet kan du se att Microsoft har identifierat en ögonblicks bilds komponent som slutade fungera under bearbetningen. Microsoft startade om komponenten, vilket tar tid att bearbeta ögonblicks bilden. Microsoft övervakar kontinuerligt tjänsten för att bekräfta att alla komponenter uppdaterar ögonblicks bilder vid rätt tidpunkt.
