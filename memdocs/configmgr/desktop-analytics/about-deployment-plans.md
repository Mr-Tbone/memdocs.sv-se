---
title: Distributions planer i Desktop Analytics
titleSuffix: Configuration Manager
description: Lär dig mer om distributions planer i Desktop Analytics.
ms.date: 07/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 0e9f1551f75c1cb8499c5eab846588ee6ddc1d80
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693394"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Om distributions planer i Desktop Analytics

Skriv bords analys samlar in och analyserar enhets-, program-och driv rutins data i din organisation. Baserat på den här analysen och dina inaktuella ininformation kan du använda tjänsten för att skapa distributions planer för Windows 10. Distributions planer har följande funktioner:  

- Rekommendera automatiskt vilka enheter som ska ingå i piloterna  

- Identifiera kompatibilitetsproblem och föreslå lösningar  

- Utvärdera distributionens hälso tillstånd före, under och efter uppdateringar  

- Spåra förloppet för din distribution  

Som en del av din distributions plan utför du följande åtgärder:  

- Definiera vilka versioner av Windows 10 som du vill distribuera  

- Välj vilka grupper av enheter som du vill distribuera till  

- Skapa beredskaps regler för distributionen  

- Definiera betydelsen för dina appar  

- Välj pilot enheter utifrån automatiska rekommendationer  

- Bestäm hur du ska åtgärda problem med appar utifrån rekommendationer från Desktop Analytics  

Som standard uppdaterar Desktop Analytics distributions plan data dagligen. Alla ändringar du gör i en distributions plan, till exempel tilldelning av prioritet för en app eller att välja en enhet som ska ingå i en pilot, tar upp till 24 timmar att bearbeta. För att påskynda processen, begär en data uppdatering på begäran. Mer information finns i [vanliga frågor och svar om Desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

När du har anslutit Skriv bords analys till Configuration Manager väljer du samlingarna i distributions planerna. Med den här integrationen kan du distribuera Windows till en samling baserat på Desktop Analytics-data.

Distributions planer stöder anpassning av de tre senaste versionerna av Windows 10. Desktop Analytics lägger till stöd för en ny Windows 10-version inom 45 dagar efter att den är tillgänglig. Vid detta tillfälle kommer tjänsten också att ta bort den äldsta versionen. Du kommer inte att kunna använda några distributions planer som är riktade till den äldsta versionen. Om du har några pågående distributions planer som är riktade till den äldsta versionen som stöds i Desktop Analytics, slutför du distributionen inom 45 dagar efter att en ny Windows 10-version är tillgänglig.

## <a name="readiness-rules"></a>Beredskaps regler

Följande beredskaps regler är tillgängliga i distributions planer:

- Anger om enheterna automatiskt ska ta emot driv rutiner från Windows Update. Om enheterna får driv rutins uppdateringar från Windows Update markeras alla driv rutins problem som identifieras som en del av beredskaps utvärderingen automatiskt som **klara**.  

- Tröskelvärde för antal låga installationer för dina Windows-appar. Om en app installeras på en högre procent andel av datorerna än det här tröskelvärdet markerar distributions planen appen **som en**försvars man. Den här taggen innebär att du kan bestämma hur viktigt appen ska testa under pilot fasen.  

## <a name="plan-assets"></a>Planera till gångar

<!-- 4670224 -->

Även om [till gångar](about-assets.md) -delen visar enheter och appar, innehåller **plan till gångar** -ytan under en bestämd distributions plan ytterligare information.

### <a name="devices"></a>Enheter

Se **Windows Upgrade-beslutet** för varje enhet i distributions planen.

Windows Upgrade-beslutet att **ersätta enheten** kan bero på någon av följande orsaker:

- En processor kontroll för Windows 10 misslyckades. Mer information finns i [minimi kraven för maskin vara](/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- Det har ett BIOS-block
- Det finns inte tillräckligt med minne
- En nödvändig start komponent i systemet har en blockerad driv rutin
- Den speciella fabrikat och modell kan inte uppgraderas
- Det finns en komponent i visnings klass med ett driv rutins block som har alla följande attribut:
  - Du åsidosätter inte
  - Det finns ingen driv rutin i den nya OS-versionen
  - Den finns inte redan på Windows Update
- Det finns en annan plug-and-Play-komponent på systemet som blockerar uppgraderingen
- Det finns en trådlös komponent som använder en XP-emulerad driv rutin
- En nätverks komponent med en aktiv anslutning kommer att förlora sin driv rutin. Med andra ord kan det gå förlorat nätverks anslutningen efter uppgraderingen.

Windows Upgrade-beslutet om att **Installera** om innebär att uppgraderingen måste installeras om i stället för en uppgradering på plats.

Ett **blockerat** Windows-uppgraderings beslut kan orsakas av följande orsaker:

- Det **går inte**att ange uppgraderings beslutet för en eller flera till gångar.

- Inventerings data för den enheten är ofullständiga och Desktop Analytics kan inte utföra en fullständig kompatibilitetskontroll.

### <a name="apps"></a>Appar

Ange **uppgraderings beslutet** och **prioriteten** för den här appen i den här distributions planen. Mer information finns i [så här skapar du distributions planer](create-deployment-plans.md).

I informationen om appen kan du också se följande information: rekommendationer, kompatibilitets riskfaktorer och kända problem med Microsoft. Använd den här informationen för att ange **uppgraderings beslutet**. Mer information finns i [kompatibilitetskontroll](compat-assessment.md).

Apparna som Skriv bords analys *visar som en* uppdatering baseras på tröskelvärdet för låg installations antal för beredskaps reglerna i distributions planen. Mer information finns i [beredskaps regler](create-deployment-plans.md#readiness-rules).

   > [!Tip]
   > Mer information om app-kategorin "ej viktiga" finns i [beslut om automatisk uppgradering av system-och Store-appar](about-assets.md#bkmk_plan-autoapp). <!-- 3587232 -->

**Informationen om program versioner** är inaktive rad som standard, så den här fliken kombinerar alla versioner av appar med samma namn och utgivare.<!-- 5542186 --> Standard beteendet hjälper till att minska det totala antalet appar som visas, vilket hjälper dig att minska dina ansträngningar att kommentera apparna. Antalet appar i panelen för att ange **appar visas också** i den här inställningen. I stället för hundratals instanser av Microsoft Edge finns det till exempel en instans för alla versioner. Du kan fatta beslut en gång för alla versioner. Om du behöver fatta beslut om vissa versioner av en app aktiverar du den här inställningen. Du kan också konfigurera den här inställningen när du arbetar på globala till gångs nivå. Mer information finns i [om till gångar – appar](about-assets.md#apps).

När **information om program versioner** är inaktive rad, visar fönstret programinformation antalet program versioner och språk som den kombinerar. Om du sparar ändringar i appens information gäller den för alla versioner. Ange exempelvis **uppgraderings beslutet** eller **prioriteten**. Vissa värden visar flera, vilket innebär att det inte finns ett konsekvent värde för alla versioner. Tjänsten ger fortfarande kompatibilitets riskbedömningar för varje version. Aktivera program versions **information** om du vill se en riskbedömning av kompatibilitet för en speciell program version.

### <a name="drivers"></a>Drivrutiner

Se listan över driv rutiner som ingår i den här distributions planen. Ange **uppgraderings beslutet**, granska Microsofts rekommendation och se riskfaktorer för kompatibilitet.

## <a name="importance"></a>Betydelse

Ange *vikten* av apparna som en del av distributions planen. Desktop Analytics identifierar de här apparna som installerade på mål enheterna. Med den här inställningen kan Desktop Analytics avgöra vilka enheter den innehåller i distributionens pilot fas.

Om en app är installerad på mindre än 2% av de riktade enheterna har den marker ATS som **låg installations antal**. Två procent är standardvärdet. Du kan justera tröskelvärdet i beredskaps inställningarna från 0 till 10%. Med Desktop Analytics märks automatiskt apparna som **klara att uppgradera**.  

För appar väljer du en viktig betydelse för **kritiska**, **viktiga**eller **inte viktiga**. Om du markerar ett som kritiskt eller viktigt inkluderar Desktop Analytics i pilot distributionen vissa enheter med den appen. Tjänsten innehåller fler instanser av en kritisk app i piloten. Om du markerar en app som inte är viktig ställer Skriv bords analys automatiskt in den så att den är **klar att uppgradera**.

## <a name="pilot-devices"></a>Pilot enheter

Skriv bords analys kombinerar din prioritets information med globala pilot inställningar. Sedan skapas en rekommendation för vilka enheter som ska ingå i pilot distributionen. Den rekommenderade pilot distributionen innehåller enheter med olika maskinvarukonfigurationer och en eller flera instanser av alla kritiska och viktiga appar. Om en app har marker ATS som kritisk rekommenderar tjänsten fler enheter med appen i piloten.

## <a name="deployment-plans-in-configuration-manager"></a>Distributions planer i Configuration Manager

När du har skapat en distributions plan använder du Configuration Manager för att distribuera produkterna. När distributionen startar övervakar Desktop Analytics distributionen baserat på inställningarna i planen.

## <a name="next-steps"></a>Nästa steg

- [Lär dig mer om Desktop Analytics-till gångar](about-assets.md): enheter, driv rutiner och appar  

- [Lär dig mer om säkerhets-och funktions uppdateringar](about-updates.md)  

- [Skapa en distributions plan](create-deployment-plans.md)