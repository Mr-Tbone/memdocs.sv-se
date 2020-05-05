---
title: Så här skapar du distributions planer
titleSuffix: Configuration Manager
description: En instruktions guide för att skapa distributions planer i Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8c42576f35d285fc7285466c4208d7ccaf370daa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723707"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Skapa distributions planer i Desktop Analytics

Den här artikeln innehåller stegen för att skapa en distributions plan i Desktop Analytics. Innan du börjar bör du först [lära dig om distributions planer](about-deployment-plans.md).

## <a name="create-a-plan-for-windows-10"></a>Skapa en plan för Windows 10

Följ stegen i det här avsnittet för att använda Desktop Analytics för att skapa en plan för att distribuera Windows 10.

1. Öppna [Skriv bords analys portalen](https://aka.ms/desktopanalytics). Använd autentiseringsuppgifter som har minst behörighet för **arbets ytans deltagare** .  

2. Välj **distributions planer** i gruppen hantera.  

3. I fönstret **distributions planer** väljer du **skapa**.  

4. Konfigurera följande inställningar i fönstret **skapa distributions plan** :  

    - **Namn**: ett unikt namn för distributions planen  

    - **Produkter och versioner**: Välj vilken Windows 10-version som ska distribueras. Microsoft rekommenderar att du skapar distributions planer som använder den senaste versionen.  

    - **Enhets grupper**: Välj en eller flera grupper i samma hierarki. De här grupperna är [enhets samlingar](connect-configmgr.md#bkmk_Collections) som synkroniseras från Configuration Manager.

        Om du ansluter flera Configuration Manager hierarkier till samma Desktop Analytics-instans, avsöker ett visnings namn för hierarkin samlings namnet i den globala pilot konfigurationen. Det här namnet är egenskapen **visnings namn** i Skriv bords analys anslutningen i Configuration Manager-konsolen.<!-- 4814075 -->

        > [!NOTE]
        > Stöd för flera hierarkier kräver Configuration Manager version 1910 eller senare.
        >
        > Om du väljer samlingar för flera hierarkier visas en varning i portalen. Du kan inte skapa distributions planen med samlingar från flera hierarkier.<!-- 4814075 -->

    - **Beredskaps regler**: de här reglerna hjälper dig att avgöra vilka enheter som är kvalificerade för uppgradering. Mer information finns i [beredskaps regler](#readiness-rules).  

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

## <a name="readiness-rules"></a>Beredskaps regler

De här reglerna hjälper dig att avgöra vilka enheter som är kvalificerade för uppgradering på plats. Du kan ställa in de här reglerna när du skapar distributions planen eller redigera dem senare.

Ändra beredskaps reglerna:

1. I portalen för Skriv bords analys väljer du distributions planen.
1. Bredvid namnet väljer du **Redigera**.
1. Välj **beredskaps regler**.
1. Välj **Windows-operativsystem**.
1. Gör nödvändiga ändringar och välj **Spara**.

För **Windows OS** -uppgraderingar finns det två tillgängliga regler: enhets driv rutiner och Windows-program.

### <a name="device-drivers"></a>Enhetsdrivrutiner

Konfigurera om enheterna ska få driv rutiner från Windows Update. Värdet är **inaktiverat** som standard. Aktivera den här regeln när du använder Windows Update för företag för att hantera uppdateringar inklusive driv rutiner. Om du använder Configuration Manager för att hantera program uppdateringar ställer du in den här regeln på **av**.

### <a name="windows-applications"></a>Windows-program

Apparna som Skriv bords analys *visar som beskrivet* baseras på tröskelvärdet för låg installation. Ange det här tröskelvärdet i beredskaps reglerna för distributions planen. Som standard är det här tröskelvärdet **2,0%**. Du kan ändra värdet från `0.0` till. `10.0`


## <a name="next-steps"></a>Nästa steg

Fortsätt till nästa artikel för att distribuera till pilot enheter.
> [!div class="nextstepaction"]  
> [Distribuera till piloten](deploy-pilot.md)  
