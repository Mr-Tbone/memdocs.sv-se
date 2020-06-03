---
title: Distribuera till pilot
titleSuffix: Configuration Manager
description: En instruktions guide för att distribuera till en pilot grupp för Skriv bords analys.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 3aa722415248ad9275c6ad065f0120bfe78d3ce4
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311228"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Så här distribuerar du till pilot med Desktop Analytics

En av fördelarna med Desktop Analytics är att hjälpa till att identifiera den minsta uppsättningen enheter som ger flest faktorer. Den fokuserar på de faktorer som är viktigast för en pilot med Windows-uppgraderingar och uppdateringar. Att se till att piloten är mer framgångs rik gör att du snabbt och säkert kan gå vidare till breda distributioner i produktionen.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

## <a name="identify-devices"></a>Identifiera enheter

Det första steget är att identifiera enheter som ska ingå i piloten. Desktop Analytics rekommenderar enheter som baseras på rapporterade data och du kan ta med eller ersätta enheter i den här listan.

1. Gå till [Skriv bords analys portalen](https://aka.ms/desktopanalytics)och välj **distributions planer**i gruppen hantera.

1. Välj en distributions plan.

1. Välj **identifiera pilot**i menyn förbereda grupp av distributions plan.

Du ser data från Desktop Analytics som visar antalet enheter som rekommenderas, inklusive för bästa täckning. Den här algoritmen baseras främst på användning av viktiga och kritiska appar och bredden på maskinvarukonfigurationer.

Vidta följande åtgärder för listan ytterligare rekommenderade enheter:

- **Lägg till alla i piloten**: lägger till alla rekommenderade enheter i pilot gruppen
- **Lägg till i pilot**: Lägg endast till enskilda enheter
- **Ersätta** vissa enheter från piloten

När du lägger till enheter från **rekommenderade** till den **inkluderade** pilot listan ökar täckningen och redundansen för dina kritiska och viktiga till gångar i piloten. En högre redundans innebär att de till gångar som omfattas har ett statistiskt stort antal enheter som ingår i piloten.

## <a name="global-pilot"></a><a name="bkmk_GlobalPilot"></a>Global pilot

Du kan också fatta systemomfattande beslut om vilka Configuration Manager samlingar som ska tas med eller undantas från piloter. I gruppen globala inställningar på huvud menyn för Skriv bordet väljer du **Global pilot**.

Om du ansluter flera Configuration Manager hierarkier till samma Desktop Analytics-instans, avsöker ett visnings namn för hierarkin samlings namnet i den globala pilot konfigurationen. Det här namnet är egenskapen **visnings namn** i Skriv bords analys anslutningen i Configuration Manager-konsolen.<!-- 4814075 -->

> [!NOTE]
> Stöd för flera hierarkier kräver Configuration Manager version 1910 eller senare.

- Ta inte med samlingar som innehåller fler än 20% av dina totala registrerade enheter till Skriv bords analys. Om du tar med en stor samling visas en varning i portalen. Du kan inkludera flera små samlingar utan varning, men ändå vara försiktig med antalet enheter i din pilot. <!-- 6079184 -->

- För att få korrekta pilot rekommendationer för distributions planer i en speciell Configuration Manager hierarki, inkludera bara samlingar från den hierarkin.

### <a name="example"></a>Exempel

- Du konfigurerar anslutning till Skriv bords analys i Configuration Manager för att rikta in samlingen **alla system** . Den här åtgärden registrerar alla klienter till tjänsten.

- Du konfigurerar också ytterligare samlingar för synkronisering med Desktop Analytics:

  - Alla Windows 10-klienter (3 000 enheter)

  - Alla IT-enheter (200 totalt antal enheter, 150 som kör Windows 10)

  - VD-kontor (20 enheter)

- I de **globala pilot** inställningarna inkluderar du samlingarna **alla Windows 10-klienter** . Du exkluderar **VD-kontoret** .

- Du skapar en distributions plan och väljer samlingen **alla IT-enheter** som **mål grupp**. Du avser endast den här distributions planen för enheter på IT-avdelningen.

- Listan över **pilot enheter som ingår** innehåller en delmängd av de enheter som finns i både **mål gruppen**: **alla IT-enheter** och *listan över globala* pilot listor: **alla Windows 10-klienter**. 150 enheter finns i den här listan eftersom endast 150-enheter i samlingen **alla IT-enheter** kör Windows 10.

- De **ytterligare rekommenderade enhets** listorna innehåller en uppsättning enheter från **mål gruppen** som ger maximal täckning och redundans för viktiga till gångar. Skriv bords analys exkluderar från den här listan över enheter i din globala *undantags* lista för pilot: **VD-kontor**.

## <a name="address-issues"></a>Adress problem

Använd portalen för Skriv bords analys för att granska eventuella rapporterade problem med till gångar som kan blockera distributionen. Godkänn, avvisa eller ändra den föreslagna korrigeringen. Alla objekt måste markeras som **färdiga** eller **klara (med reparation)** innan pilot distributionen startar.

1. Gå till [Skriv bords analys portalen](https://aka.ms/desktopanalytics)och välj **distributions planer**i gruppen hantera.  

2. Välj en distributions plan.  

3. Välj **Förbered pilot**i menyn förbereda grupp av distributions plan.  

4. På fliken **appar** granskar du de appar som behöver dina inaktuella ingångar.  

5. För varje app väljer du appens namn. I informations fönstret granskar du rekommendationen och väljer uppgraderings beslutet. Om du väljer att **inte granska** eller **inte**fungerar, innehåller Desktop Analytics inte enheter med den här appen i pilot distributionen. Om du väljer **klar (med åtgärd)** kan du använda åtgärds **anteckningarna** för att avbilda de åtgärder som ska vidtas för att lösa ett problem, t. ex. *installera om* eller *hitta tillverkarens rekommenderade version*.

6. Upprepa denna granskning för andra till gångar.  

Mer information som hjälper dig med den här gransknings processen finns i [kompatibilitetskontroll](compat-assessment.md).

## <a name="create-software"></a>Skapa program vara

Innan du kan distribuera Windows måste du först skapa program varu objekt i Configuration Manager. Mer information finns [i aktivitetssekvens för uppgradering av Windows 10 på plats](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).

## <a name="deploy-to-pilot-devices"></a>Distribuera till pilot enheter

Configuration Manager använder data från Desktop Analytics för att skapa samlingar för pilot-och produktions distributionerna. De här samlingarna finns i arbets ytan **till gångar och efterlevnad** , noden **enhets samlingar** , mappen **distributions planer** .

> [!IMPORTANT]
> De här samlingarna hanteras av Configuration Manager för distributions planer för Skriv bords analys. Manuella ändringar stöds inte. Om du tar bort någon av de här samlingarna fungerar inte Desktop Analytics och du måste [ansluta Configuration Manager](connect-configmgr.md) igen.<!--7208090-->

För att se till att enheterna är felfria efter varje distributions fas kan du använda följande procedur för att skapa en integrerad stegvis distribution med Desktop Analytics:

1. I Configuration Manager-konsolen går du till **program biblioteket**, expanderar **underhåll av Skriv bords analys**och väljer noden **distributions planer** .  

2. Välj din distributions plan och välj sedan **distributions Plans information** i menyfliksområdet.  

3. Välj **skapa stegvis distribution** i menyfliksområdet. Den här åtgärden startar guiden skapa stegvis distribution.

    > [!Tip]  
    > Om du vill skapa en klassisk aktivitetssekvensdistribution för bara pilot samlingen väljer du **distribuera** i panelen **pilot status** . Den här åtgärden startar guiden distribuera program vara. Mer information finns i [Distribuera en aktivitetssekvens](../osd/deploy-use/deploy-a-task-sequence.md).  

4. Ange ett namn för distributionen och välj den aktivitetssekvens som ska användas. Använd alternativet för att **automatiskt skapa en standard distribution i två faser**och konfigurera sedan följande samlingar:  

    - **Första samlingen**: Sök efter och välj **pilot** samlingen för den här distributions planen. Standard namngivnings konventionen för den här samlingen är `<deployment plan name> (Pilot)` .

    - **Andra samlingen**: Sök efter och välj **produktions** samlingen för den här distributions planen. Standard namngivnings konventionen för den här samlingen är `<deployment plan name> (Production)` .

    > [!Note]  
    > Med Desktop Analytics-integrering skapar Configuration Manager automatiskt pilot-och produktions samlingar för distributions planen. Innan du kan använda dem kan det ta tid för dessa samlingar att synkronisera. Mer information finns i [Felsök-data svars tid](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > De här samlingarna är reserverade för distributions Plans enheter för Desktop Analytics. Manuella ändringar av de här samlingarna stöds inte.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Konfigurera den stegvisa distributionen genom att slutföra guiden. Mer information finns i skapa stegvisa [distributioner](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

    > [!Note]  
    > Använd standardinställningen för att **starta den här fasen automatiskt efter en uppskjutnings period (i dagar)**. Följande kriterier måste uppfyllas för att den andra fasen ska starta:
    >
    > 1. Den första fasen når villkoren för **lyckade distributioner i procent** för att lyckas. Du konfigurerar den här inställningen för den stegvisa distributionen.
    > 1. Du måste granska och fatta uppgraderings beslut i Skriv bords analys för att markera viktiga och viktiga till gångar som *färdiga*. Mer information finns i [Granska till gångar som behöver ett uppgraderings beslut](deploy-prod.md#bkmk_review).
    > 1. Desktop Analytics synkroniseras till Configuration Manager samlingar alla produktions enheter som uppfyller *klara* kriterier.

> [!Important]  
> De här samlingarna fortsätter att synkroniseras när deras medlemskap ändras. Om du t. ex. identifierar ett problem med en till gång och markerar det som **inte**längre uppfyller de *klara* kriterierna. De här enheterna tas bort från produktions distributions samlingen.

## <a name="monitor"></a>Övervaka

### <a name="configuration-manager-console"></a>Configuration Manager-konsolen

Öppna distributions planen. I rutan **förberedelse av uppgraderings beslut – övergripande status** finns en sammanfattning av status för distributions planen. Denna status är för både pilot-och produktions samlingarna. Enheter kan falla i någon av följande kategorier:

- **Uppdaterat**: enheter har uppgraderats till mål versionen av Windows för den här distributions planen

- **Uppgraderings beslut slutfört**: något av följande tillstånd:

  - Enheter med uppmärksamma till gångar som är **klara** eller **färdiga med reparation**

  - Enhetens tillstånd är **blockerad**, [**Ersätt enheten**](about-deployment-plans.md#plan-assets) eller **installera om enheten**

- **Ej granskad**: enheter med anmärknings bara till gångar som **inte har granskats** eller **granskats**

Enhets status uppdateras i panelerna **pilot status** och **produktions status** med följande åtgärder:

- Du gör ändringar i kompatibilitetskontroll
- Enheter uppgraderas till mål versionen av Windows
- Distributionen fortskrider

Du kan också använda Configuration Manager distributions övervakning på samma sätt som en annan aktivitetssekvensdistribution. Mer information finns i [övervaka OS-distributioner](../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="desktop-analytics-portal"></a>Skriv bords analys Portal

Använd [Skriv bords analys portalen](https://aka.ms/desktopanalytics) om du vill visa status för alla distributions planer. Välj distributions plan och välj sedan **plan översikt**.

![Skärm bild av översikt över distributions planen i Desktop Analytics](media/deployment-plan-overview.png)

Välj panelen **pilot** . Den sammanfattar den aktuella statusen för pilot distributionen. Den här panelen visar även data för antalet enheter som inte har startats, pågår, slutförts eller som returnerar problem.

Enheter som rapporterar fel eller andra problem visas också i informations avsnittet om pilot till höger. Välj **Granska**för att få information om det rapporterade problemet. Den här åtgärden ändrar vyn till sidan **distributions status**

Sidan **distributions status** visar enheter i följande kategorier:

- Inte startad
- Pågår
- Slutförd
- Kräver åtgärd – enheter
- Kräver åtgärds problem

**Åtgärds** kategorierna för behov visar samma information, men sorteras på olika sätt.

Välj en speciell lista i valfri vy för att få mer information om det identifierade problemet.

När du tar itu med de här distributions problemen fortsätter instrument panelen att Visa enheternas förlopp. Den uppdaterar när enheter flyttas från **behöver åtgärdas** till **slutfört**.

## <a name="next-steps"></a>Nästa steg

Låt piloten köra ett tag för att samla in drift data. Uppmuntra användare av pilot enheter att testa appar.

När din pilot distribution uppfyller dina lyckade kriterier går du till nästa artikel för att distribuera till produktion.
> [!div class="nextstepaction"]  
> [Distribuera till produktion](deploy-prod.md)  
