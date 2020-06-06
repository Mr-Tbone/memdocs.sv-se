---
title: Konfigurera innehåll i förcachen
titleSuffix: Configuration Manager
description: Lär dig hur klienter kan hämta operativ systemets distributions innehåll innan en användare installerar aktivitetssekvensen.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec465f3dee33ca311aec120e74a2994a81a90ec9
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455233"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>Konfigurera innehåll i förinställt cacheminne för aktivitetssekvenser

*Gäller för: Configuration Manager (aktuell gren)*

<!--1021244-->
Med funktionen för cachelagring för tillgängliga distributioner av aktivitetssekvenser kan klienter Ladda ned relevant innehåll innan en användare installerar aktivitetssekvensen. Klienten kan cachelagra innehåll i förväg för aktivitetssekvenser som [uppgraderar ett operativ system](create-a-task-sequence-to-upgrade-an-operating-system.md) eller [installerar en OS-avbildning](create-a-task-sequence-to-install-an-operating-system.md).

> [!Note]  
> Configuration Manager aktiverar den här funktionen som standard i version 1910. I version 1906 eller tidigare aktiverar Configuration Manager inte den här valfria funktionen som standard. Du måste aktivera den här funktionen innan du använder den. Mer information finns i avsnittet [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Till exempel vill du bara ha en enda uppgradering på plats för alla användare och flera arkitekturer och språk. I tidigare versioner börjar innehållet laddas ned när användaren installerar en tillgänglig aktivitetssekvensdistribution från Software Center. Den här fördröjningen lägger till ytterligare tid innan installationen kan starta. Allt innehåll som refereras i aktivitetssekvensen har laddats ned. Det här innehållet innehåller uppgraderings paketet för operativ systemet för alla språk och arkitekturer. Om varje uppgraderings paket ungefär 3 GB är i storlek är det totala innehållet mycket stort.

Med hjälp av cachelagrat innehåll kan du välja att klienten bara ska ladda ned tillämpligt innehåll och allt annat refererat innehåll så fort det tar emot distributionen. När användaren klickar på **Installera** i Software Center är innehållet klart. Installationen startar snabbt eftersom innehållet finns på den lokala hård disken.

I Configuration Manager version 1902 och tidigare gäller det här beteendet endast för *uppgraderings paketet för operativ systemet*. Det paketet är det enda innehåll som du anger för den matchande arkitekturen eller språket. Om aktivitetssekvensen till exempel också refererar till flera driv rutins paket laddar klienten ned alla. Motorn för aktivitetssekvenser utvärderar villkoren i stegen när aktivitetssekvensen körs, inte i förväg. Klienten använder taggarna på paket egenskaperna för att avgöra vilket innehåll som ska förcachelagras.

Från och med version 1906,<!--4224642--> Du kan använda för cachelagring för att minska bandbredds förbrukningen för följande innehålls typer:

- Uppgraderings paket för operativ system
- Operativsystemavbildningar
- Drivrutinspaket
- Paket

## <a name="configure-pre-caching"></a>Konfigurera för cachelagring

Det finns tre steg för att konfigurera funktionen för för cache:

1. [Skapa och konfigurera paketen](#bkmk_createpkg)
2. [Skapa en aktivitetssekvens med villkorliga steg](#bkmk_createts)
3. [Distribuera aktivitetssekvensen och aktivera för cachelagring](#bkmk_deploy)


### <a name="1-create-and-configure-the-packages"></a><a name="bkmk_createpkg"></a>1. skapa och konfigurera paketen

Klienten utvärderar attributen för paketen för att avgöra vilket innehåll som hämtas under för cachelagring.  

#### <a name="os-upgrade-package"></a>Uppgraderings paket för operativ system

Skapa [uppgraderings paket för operativ system](../get-started/manage-operating-system-upgrade-packages.md) för vissa arkitekturer och språk. Ange **arkitekturen** och **språket** på fliken **data källa** för egenskaperna.

#### <a name="os-image"></a>OS-avbildning

Skapa [OS-avbildningar](../get-started/manage-operating-system-images.md) för vissa arkitekturer och språk. Ange **arkitekturen** och **språket** på fliken **data källa** för egenskaperna.

#### <a name="driver-package"></a>Drivrutinspaket

Skapa [driv rutins paket](../get-started/manage-drivers.md#BKMK_ManagingDriverPackages) för vissa maskin varu modeller. Ange **modellen** på fliken **Allmänt** i egenskaperna.

För att avgöra vilka driv rutins paket som laddas ned under för cachelagring, utvärderar klienten modellen mot egenskapen **namn** för **Win32_ComputerSystemProduct** WMI-klassen.

> [!TIP]
> Den faktiska frågan använder en `LIKE` instruktion med jokertecken: `select * from win32_computersystemproduct where name like "%yourstring%"` . Om du till exempel anger `Surface` som modell matchar frågan alla modeller som innehåller strängen.<!-- 6315551 -->

#### <a name="package"></a>Paket

Skapa [paket](../../apps/deploy-use/packages-and-programs.md) för vissa arkitekturer och språk. Ange **arkitekturen** och **språket** på fliken **Allmänt** i egenskaperna.


### <a name="2-create-a-task-sequence"></a><a name="bkmk_createts"></a>2. skapa en aktivitetssekvens

Skapa en aktivitetssekvens med villkorliga steg för olika språk och arkitekturer, eller olika maskin varu modeller för driv rutins paket.

|Innehåll|Steg|
|---------|---------|
|Uppgraderings paket för operativ system|[Uppgradera operativ system](../understand/task-sequence-steps.md#BKMK_UpgradeOS)|
|OS-avbildning|[Använd OS-avbildning](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)|
|Drivrutinspaket|[Använd drivrutinspaket](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage)|
|Paket|[Installera paket](../understand/task-sequence-steps.md#BKMK_InstallPackage)|

Till exempel använder följande **uppgraderings operativ system** den engelska versionen:  

![Redigeraren för aktivitetssekvens visar flera uppgraderings operativ Systems steg för ENU, DEU och JPN](../media/precacheproperties2.png)

![Redigeraren för aktivitetssekvens, fliken Alternativ, visar WMI WQL-frågan för språkvariant-och OSArchitecture](../media/precacheoptions2.png)  

> [!Tip]
> Följande WMI-fråga rekommenderas för den engelska (USA) OS-och 64-bitars arkitekturen:
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage='1033'
> ```
>
> Lägg först till språket genom att välja **operativ systemets språk** villkor. Redigera sedan WMI-frågan för att inkludera arkitektur satsen.

### <a name="3-deploy-the-task-sequence"></a><a name="bkmk_deploy"></a>3. distribuera aktivitetssekvensen

[Distribuera aktivitetssekvensen](deploy-a-task-sequence.md). Konfigurera följande inställningar för funktionen för cache:  

- På fliken **Allmänt** väljer du **Hämta innehåll i förväg för den här aktivitetssekvensen**.  

- På fliken **distributions inställningar** konfigurerar du aktivitetssekvensen som **tillgänglig**.  

- På fliken **Schemaläggning** väljer du den för tillfället valda tiden för inställningen, **Schemalägg när distributionen ska vara tillgänglig**. Klienten startar för cachelagring av innehåll vid distributionens tillgängliga tid. När en riktad klient tar emot den här principen, är den tillgängliga tiden tidigare, vilket innebär att hämtningen av förcachen börjar bli omedelbart. Om klienten får den här principen men den tillgängliga tiden är i framtiden, startar klienten inte för cachelagring av innehåll förrän den tillgängliga tiden infaller.  

- På fliken **distributions platser** konfigurerar du inställningarna för **distributions alternativ** . Om innehållet inte lagras i förväg innan en användare startar installationen, använder klienten dessa inställningar.  

    > [!Important]  
    > För en aktivitetssekvens som installerar en OS-avbildning ska du inte använda distributions alternativet för att **Ladda ned innehåll lokalt när du behöver genom att köra aktivitetssekvensen**. När aktivitetssekvensen rensar disken innan den tillämpar OS-avbildningen tar den bort-klientcachen. Eftersom innehållet är borta Miss lyckas aktivitetssekvensen.<!-- SCCMDocs-PR #1338 --> De här distributions alternativen är dynamiska baserat på andra alternativ som du väljer för distributionen. Mer information finns i [Distribuera en aktivitetssekvens](deploy-a-task-sequence.md#bkmk_deploy-options).<!-- MEMDocs#328, SCCMDocs#2114 -->

## <a name="user-experience"></a>Användarupplevelse

- När klienten tar emot distributions principen börjar den i förväg cachelagra innehållet efter distributionens tillgängliga tid. Det här innehållet innehåller alla refererade paket, men endast det uppgraderings paket för operativ system som matchar arkitekturen och språkattributen för paketet.  

- När klienten gör distributionen tillgänglig för användare visas ett meddelande som informerar användarna om den nya distributionen. Nu syns aktivitetssekvensen i Software Center. Användaren kan gå till Software Center och klicka på **Installera** för att starta installationen.  

- Om klienten inte har cachelagrat innehållet fullständigt när användaren installerar aktivitetssekvensen använder klienten de inställningar som du anger på fliken **distributions alternativ** i distributionen.  

## <a name="see-also"></a>Se även

- [Skapa en aktivitetssekvens för att uppgradera ett operativsystem](create-a-task-sequence-to-upgrade-an-operating-system.md)
- [Scenario för att uppgradera Windows till den senaste versionen](upgrade-windows-to-the-latest-version.md)
