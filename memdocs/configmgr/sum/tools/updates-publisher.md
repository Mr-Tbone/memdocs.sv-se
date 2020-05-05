---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Använd System Center Updates Publisher för att hantera anpassade uppdateringar
ms.date: 11/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc1e662eb8eca4740e70743d0971e2d65410f3f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717701"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Gäller för: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) är ett fristående verktyg som gör det möjligt för oberoende program varu leverantörer eller branschspecifika program utvecklare att hantera anpassade uppdateringar. Den här anpassade uppdaterings hanteringen inkluderar uppdateringar som har beroenden, t. ex. driv rutiner och uppdaterings paket.

Med Updates Publisher kan du:

-   Importera uppdateringar från externa kataloger (uppdaterings kataloger som inte kommer från Microsoft).
-   Ändra uppdaterings definitioner, inklusive tillämpbarhet och distributions-metadata.
-   Exportera uppdateringar till externa kataloger.
-   Publicera uppdateringar på en uppdaterings Server.

När du har publicerat uppdateringar på en uppdaterings Server kan du använda Configuration Manager för att identifiera och distribuera uppdateringarna till dina hanterade enheter.

## <a name="workspaces"></a>Arbetsytor
När du öppnar Updates Publisher används den som standard i noden översikt i *arbets ytan uppdateringar.*

![Uppdatera Publisher-konsolen](media/console1.png)


Updates Publisher har fyra arbets ytor som hjälper dig att organisera den.


**Arbets yta för uppdateringar:** Använd den här arbets ytan för att [skapa](create-updates-with-updates-publisher.md) och [Hantera](manage-updates-with-updates-publisher.md) program uppdateringar och uppdaterings paket. I den här arbets ytan ingår att tilldela uppdateringar och paket till en publikation, publicera och exportera till en annan Updates Publisher-lagringsplats.

**Arbets yta för publikationer:** I den här arbets ytan [hanterar du publikationer](updates-publisher-publications.md). En publikation är en grupp med uppdateringar som du skapar för att förenkla exporten och publiceringen av uppdateringarna.

Hantering av publikationer innehåller publicerings uppdateringar till en server så att dina klienter kan hitta och installera dem, exportera uppdateringar och paket som ska användas av andra uppdateringar av Publisher-installationer eller ändra innehållet i eller information om en publikation.

**Arbets ytan regler:** Här kan du [Hantera tillämplighets regler](updates-publisher-applicability-rules.md) som kan sparas och sedan användas med uppdateringar som du distribuerar. Det finns två typer av regler:

-   Installerbara regler – de här reglerna hjälper dig att avgöra om en klient ska installera en uppdatering.
-   Installerade regler – de här reglerna kontrollerar om en uppdatering redan har installerats.

**Arbets yta för kataloger:** Använd den här arbets ytan för att lägga till och [hantera program uppdaterings kataloger](updates-publisher-catalogs.md). I den här arbets ytan ingår import av program uppdateringar från dessa kataloger till den uppdaterade utgivarens lagrings plats.

## <a name="whats-new-in-system-center-updates-publisher"></a>Vad är nytt i System Center Updates Publisher

>[!NOTE] 
> Den senaste versionen av System Center Updates Publisher släpptes den 6 november 2019. Mer information finns i avsnittet [versions historik](#release-history) .

Det finns ett nytt redigerings läge System Center Updates Publisher som hjälper dig att redigera dina uppdateringar. När du aktiverar redigerings läget läggs **arbets ytan kategorier** till på Start skärmen. En ny **Detectoid** -knapp läggs också till i **arbets ytan uppdateringar** när redigerings läget är aktiverat.

### <a name="to-enable-authoring-mode"></a>Aktivera redigerings läge

1. I det övre vänstra hörnet i konsolen klickar du på fliken **Updates Publisher** - **Egenskaper** och väljer sedan **alternativ**.
1. Gå till **redigerings** alternativen.
1. Markera kryss rutan **Aktivera redigerings läge**.

![Aktivera redigerings läge för Updates Publisher](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>Om arbets ytan kategorier

Arbets ytan kategorier gör det möjligt för uppdaterings redigerare att organisera uppdateringar som hör ihop. Om du till exempel är en OEM-tillverkare kanske du vill organisera dina uppdateringar baserat på modeller eller produkt linjer. Du kan definiera flera kategorier och underordnade kategorier, men inte för summering av underordnade kategorier eftersom du är begränsad till två nivåer.

![Skärm bild av arbets ytan kategorier](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Tilldela en uppdatering till en kategori

När du har skapat din uppdatering kan du tilldela den till en kategori genom att markera uppdateringen och sedan klicka på knappen **kategorisera** . Du kan också högerklicka på uppdateringen och välja **kategorisera**.

![Skärm bild av kategorisering av en uppdatering](media/scup-categorize-update.png)

### <a name="about-detectoids"></a>Om detectoids

När du har aktiverat redigerings läget kan du skapa detectoids för uppdateringar. Detectoids är användbara när du har flera uppdateringar som använder samma regel (eller en uppsättning regler) för att fastställa tillämplighet. I dessa instanser skapar du en detectoid och tilldelar den som ett krav för en uppdatering. Du kan tilldela flera detectoids till en rediged uppdatering.


### <a name="create-a-detectoid"></a>Skapa en detectoid

1. Öppna **arbets ytan uppdateringar**.
1. Klicka på knappen **Detectoid** i menyfliksområdet.
1. Följ anvisningarna i guiden för att skapa din detectoid.



![Uppdatera förutsättningar med en detectoid](media/scup-detectoid-as-prerequisite.png)

## <a name="release-history"></a>Versions historik

- [2019 RTW-version 6.0.394.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/SCUP-adds-support-for-update-categories/ba-p/990111). Lanserad november, 6, 2019
- Samlad [uppdaterings version 6.0.283.0 från KB4462765](https://support.microsoft.com/help/4462765/update-rollup-for-system-center-updates-publisher). Publicerad 7 september 2018.
- [2017 RTW-version 6.0.276.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/System-Center-Updates-Publisher-adds-support-for-new-OSes/ba-p/274986). Publicerad 26 mars 2018.


## <a name="next-steps"></a>Nästa steg
Kom igång genom att först [Installera](install-updates-publisher.md)och sedan [Konfigurera alternativ](updates-publisher-options.md) för Updates Publisher.
