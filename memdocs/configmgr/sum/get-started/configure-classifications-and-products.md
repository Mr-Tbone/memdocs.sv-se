---
title: Konfigurera klassificeringar och produkter
titleSuffix: Configuration Manager
description: Följ dessa steg om du vill konfigurera program uppdaterings klassificeringar och produkter som ska synkroniseras i Configuration Manager-konsolen.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: a5254ba5a25b10df2943eaa7f80b32b17ea3680f
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88591501"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>Konfigurera klassificeringar och produkter som ska synkroniseras  

*Gäller för: Configuration Manager (aktuell gren)*

Metadata för program uppdateringar hämtas under synkroniseringsprocessen i Configuration Manager baserat på de inställningar som du anger i egenskaperna för plats komponent för program uppdatering. När du har synkroniserat program uppdateringar för första gången, eller när nya produkter och klassificeringar släpps, måste du gå till egenskaperna för att välja nya objekt. Använd följande procedur om du vill konfigurera klassificeringar och produkter att synkronisera.  

> [!NOTE]  
> Använd enbart proceduren från det här avsnittet på toppnivåplatsen.  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>Konfigurera klassificeringar och produkter som ska synkroniseras  

1. I **Configuration Manager** -konsolen navigerar du till **Administration**  >  **plats konfiguration**  >  **platser**.

2. Välj den centrala administrations platsen eller den fristående primära platsen.  

3. Klicka på **Konfigurera platskomponenter** i gruppen **Inställningar** på **Start**-fliken och klicka sedan på **Programuppdateringsplats**.

4. Ange de programuppdateringsklassificeringar som du vill synkronisera programuppdateringar för på fliken **Klassificeringar** .  

    Alla programuppdateringar får en angiven klassificering så att de olika uppdateringstyperna lätt kan sorteras. Under synkroniseringsprocessen synkroniserar programuppdateringsmetadata för de angivna klassificeringarna. Configuration Manager ger möjlighet att synkronisera program uppdateringar med följande uppdaterings klassificeringar:  

     - **Kritiska uppdateringar**: anger en mycket utgiven korrigering för ett särskilt problem som åtgärdar en kritisk, ej säkerhetsrelaterad bugg.  
     - **Definitions uppdateringar**: anger en mycket publicerad och frekvent program uppdatering som innehåller tillägg till en produkts definitions databas.  
     - **Funktions paket**: anger nya produkt funktioner som distribueras utanför en produkt lansering och som vanligt vis ingår i nästa fullständiga produkt lansering.  
     - **Säkerhets uppdateringar**: anger en mycket utgiven korrigering för en produktspecifik, säkerhetsrelaterad säkerhets risk.  
     - **Service Pack**: anger en testad, kumulativ uppsättning av alla snabb korrigeringar, säkerhets uppdateringar, viktiga uppdateringar och uppdateringar som tillämpas på en produkt. Dessutom kan service packs innehålla ytterligare korrigeringar för problem som hittas internt sedan produkten lanseras.  
     - **Verktyg**: anger ett verktyg eller en funktion som hjälper till att slutföra en eller flera uppgifter.  
     - **Samlade uppdateringar**: anger en testad, kumulativ uppsättning snabb korrigeringar, säkerhets uppdateringar, viktiga uppdateringar och uppdateringar som paketeras tillsammans för enkel distribution. En samlad uppdatering hanterar vanligt vis ett speciellt utrymme, till exempel en säkerhets-eller produkt komponent.  
     - **Uppdateringar**: anger en mycket utgiven korrigering för ett enskilt problem. En uppdatering åtgärdar en icke-kritisk, icke-säkerhetsrelaterad bugg.  
     - **Uppgradering**: anger en uppgradering för funktioner och funktioner i Windows 10. Dina program uppdaterings platser och platser måste köra minst WSUS 6,2 med [snabb korrigeringen 3095113](https://support.microsoft.com/kb/3095113) för att få **uppgraderings** klassificeringen. Mer information om hur du installerar den här uppdateringen och andra uppdateringar för **uppgraderingar**finns i [krav för program uppdateringar](../plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012).
    
    > [!NOTE]
    > Du kan markera kryss rutan **Inkludera uppdatering av Microsoft-Surface-drivrutiner och inbyggd program vara** för att synkronisera Microsoft Surface-drivrutiner.<!--1098490--> Alla program uppdaterings platser måste köra Windows Server 2016 eller senare för att kunna synkronisera Surface-drivrutiner. Om du aktiverar en program uppdaterings plats på en dator som kör Windows Server 2012 efter att du har aktiverat Surface-drivrutiner, är genomsöknings resultaten för driv rutins uppdateringarna inte korrekta. Detta resulterar i att felaktiga efterlevnadsprinciper visas i Configuration Manager-konsolen och i Configuration Manager rapporter. Mer information finns i [Hantera Surface-drivrutiner med Configuration Manager](../deploy-use/surface-drivers.md).

5. På fliken **Produkter** anger du de produkter som du vill synkronisera programuppdateringar för och klickar sedan på **Stäng**.  

    - Configuration Manager lagrar en lista med produkter och produkt familjer som du kan välja från när du först installerar program uppdaterings platsen. Produkter och produkt familjer som släpps efter Configuration Manager släpps kanske inte är tillgängliga för att väljas förrän du slutför synkroniseringen av program uppdateringar, som uppdaterar listan över tillgängliga produkter och produkt familjer som du kan välja mellan.  

    - Metadata för varje programuppdatering definierar de produkter som uppdateringen är tillämplig för. En produkt är en viss version av ett operativsystem eller ett program, exempelvis Windows Server 2012. En produktfamilj är det grundläggande operativsystem eller program som de enskilda produkterna hämtas från. Ett exempel på en produktfamilj är Windows, där Windows Server 2012 ingår. Du kan ange en produktserie eller enskilda produkter inom en produktserie. De fler produkter du väljer, desto längre tid tar det att synkronisera program uppdateringar.  

    - När program uppdateringar tillämpas på flera produkter och minst en av produkterna har valts för synkronisering, visas alla produkter i Configuration Manager-konsolen även om vissa produkter inte har valts. Om Windows Server 2012 till exempel är det enda operativ system som du har valt, och om en program uppdatering gäller för Windows 8 och Windows Server 2012, visas båda produkterna i Configuration Manager-konsolen.  

    > [!NOTE]  
    > **Windows 10, version 1903 och senare** har lagts till i Microsoft Update som sin egen produkt, i stället för att vara en del av **Windows 10** -produkten som tidigare versioner. Den här ändringen gjorde att du utför ett antal manuella åtgärder för att se till att dina klienter ser dessa uppdateringar. Vi har hjälpt till att minska antalet manuella åtgärder som du behöver vidta för den nya produkten i Configuration Manager version 1906. <!--4682946-->
    >
    > När du uppdaterar till Configuration Manager version 1906 och har **Windows 10** -produkten vald för synkronisering sker följande åtgärder automatiskt:
    > - Produkten **Windows 10, version 1903 och senare** har lagts till för synkronisering.
    > - [Automatiska distributions regler](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) som innehåller **Windows 10** -produkten kommer att uppdateras för att inkludera **Windows 10, version 1903 och senare**.
    > - [Service planer](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) uppdateras för att omfatta produkten **Windows 10, version 1903 och senare** .


## <a name="configuring-products-for-versions-of-windows-10"></a>Konfigurera produkter för versioner av Windows 10

### <a name="windows-10-version-1909"></a>Windows 10, version 1909

Windows 10, version 1909 delar ett gemensamt kärn operativ system med Windows 10, version 1903. Båda dessa versioner servas med samma ackumulerade uppdateringar. Mer information om Windows 10, version 1909 finns i blogg inlägget för [leverans alternativ för Windows 10, version 1909](https://aka.ms/1909mechanics) .

För att se till att både Windows 10 version 1909 och Windows 10, version 1903-klienter installerar uppdateringar från Configuration Manager:

- Godkänn uppdateringar för både 1909-och 1903-versioner av Windows 10.
  - Uppdateringarna har olika titlar och tillämplighets regler för varje operativ system version.
  - Om du godkänner varje uppdatering per version och arkitektur för operativ systemet hanteras den normala godkännande processen för administratörer.
- Installationsfilerna för ackumulerad uppdatering är desamma för både 1909-och 1903-versionerna av Windows 10.
  - Configuration Manager laddar bara ned uppdateringens källfiler en gång.

#### <a name="feature-updates-for-windows-10-version-1909"></a>Funktions uppdateringar för Windows 10, version 1909

När du godkänner funktions uppdateringar för Windows 10, version 1909, finns det några olika alternativ:

- Windows 10, version 1903-klienter erbjuds ett [aktiverings paket](https://support.microsoft.com/en-us/help/4517245/feature-update-via-windows-10-version-1909-enablement-package), lanseras 12 november 2019.
  - Aktiverings paketet är en liten snabb installation av filen som aktiverar Windows 10, version 1909-funktionerna och startar om enheten.
  - Krav för aktiverings paketet är:
    - En minsta kumulativ uppdatering av [KB4517389](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4517389), publicerad den 8 oktober 2019.
    - En minimal underhålls uppdatering av [KB4520390](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4520390), publicerad den 24 september 2019.
  - Den här uppdateringen, precis som andra funktions uppdateringar, är inte tillgänglig för import från `https:\\catalog.update.microsoft.com` .
  - Uppdateringen synkroniseras automatiskt med WSUS om du har valt produkt-och **uppgraderings** klassificering i **Windows 10, version 1903 och senare** , för synkronisering.
  - Gå till arbets ytan **program bibliotek** i Configuration Manager-konsolen, expandera **Windows 10 service**och välj noden **alla Windows 10-uppdateringar** . Sök efter villkoren "aktivering" eller "4517245".

    > [!TIP]
    > Eftersom dessa är funktions uppdateringar finns de inte i noden **alla program uppdateringar** .

- Windows 10, version 1809 och tidigare klienter uppgraderas med en enda direkt funktions uppdatering.
  - Detta är precis som alla andra tidigare installationer för funktions uppdateringar som du har gjort för Windows 10.

> [!NOTE]
> Både aktiverings paketet och den traditionella funktions uppdateringen för Windows 10, version 1909, visas som "installerad" i rapportering, oavsett vilken sökväg som användes för att installera den.

### <a name="windows-10-version-1903-and-later"></a>Windows 10, version 1903 och senare

**Windows 10, version 1903 och senare** har lagts till i Microsoft Update som sin egen produkt, i stället för att vara en del av **Windows 10**  -produkten som tidigare versioner. Den här ändringen gjorde att du utför ett antal manuella åtgärder för att se till att dina klienter ser dessa uppdateringar. Vi har hjälpt till att minska antalet manuella åtgärder som du behöver vidta för den nya produkten i Configuration Manager version 1906. <!--4682946-->

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1906"></a>Windows 10, version 1903 och senare med Configuration Manager version 1906
När du uppdaterar till Configuration Manager version 1906 och har **Windows 10** -produkten vald för synkronisering sker följande åtgärder automatiskt:
- Produkten **Windows 10, version 1903 och senare** har lagts till för synkronisering.
- [Automatiska distributions regler](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) som innehåller **Windows 10** -produkten kommer att uppdateras för att inkludera **Windows 10, version 1903 och senare**.
- [Service planer](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) uppdateras för att omfatta produkten **Windows 10, version 1903 och senare** .

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1902"></a>Windows 10, version 1903 och senare med Configuration Manager version 1902
Om du använder Configuration Manager 1902 med Windows 10, version 1903-klienter måste du:
- Välj produkten **Windows 10, version 1903 och senare** för synkronisering.
- Uppdatera eventuella [automatiska distributions regler](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) för Windows 10, version 1903-klienter.
- Uppdatera [Service planer](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) för Windows 10, version 1903-klienter.

## <a name="windows-insider-program"></a><a name="bkmk_WIfB"></a> Windows Insider program
<!--3556023-->
Från och med september 2019 kan du underhålla och uppdatera enheter som kör Windows Insider Preview-versioner med Configuration Manager. Den här ändringen innebär att du kan hantera dessa enheter utan att ändra dina normala processer eller aktivera Windows Update för företag. Du kan hämta funktions uppdateringar och kumulativa uppdateringar för Windows Insider Preview-versioner till Configuration Manager precis som med andra Windows 10-uppdateringar eller uppgraderingar. Mer information finns i avsnittet [Publicera för hands version av Windows 10-funktions uppdateringar till WSUS](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054) -blogg inlägget.

För ytterligare information om stöd för Windows Insider i Configuration Manager, se [stöd för Windows 10](../../core/plan-design/configs/support-for-windows-10.md#bkmk_WIfB-support).

### <a name="prerequisites"></a>Förutsättningar

- Configuration Manager version 1906 eller högre, konfigurerad för [hantering av program uppdateringar](../plan-design/plan-for-software-updates.md).
- Windows 10-enheter som kör [Windows Insider Preview-version](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-get-started).
- En samling som innehåller Windows Insider-enheter.

### <a name="enable-windows-insider-upgrades-and-updates"></a>Aktivera Windows Insider-uppgraderingar och uppdateringar

Du måste aktivera produkter och klassificeringar för Windows Insider-uppgraderingar och uppdateringar. Funktions uppdateringar, ackumulerade uppdateringar och andra uppdateringar för Windows Insider finns under produkt kategorin **Windows Insider för hands version** .

1. I **Configuration Manager** -konsolen navigerar du till **Administration**  >  **plats konfiguration**  >  **platser**.
2. Välj den centrala administrations platsen eller den fristående primära platsen.  
3. Klicka på **Konfigurera platskomponenter** i gruppen **Inställningar** på **Start**-fliken och klicka sedan på **Programuppdateringsplats**.
4. På fliken **produkter** kontrollerar du att följande produkter har valts för synkronisering:
    - Windows Insider för hands version
    - Windows 10, version 1903 och senare
5. På fliken **klassificeringar** kontrollerar du att följande klassificeringar har valts för synkronisering:
    - Uppgraderingen
    - Säkerhetsuppdateringar
    - Uppdateringar (valfritt)
6. Stäng egenskaperna för komponenten för **program uppdaterings plats**genom att klicka på **OK** .

### <a name="upgrading-windows-insider-devices"></a>Uppgradera Windows Insider-enheter

När uppgraderingarna för Windows-Insiders är synkroniserade kan du se dem från **program varu biblioteket**  >  **Windows 10-Underhåll**av  >  **alla Windows 10-uppdateringar**.

![Windows Insiders funktions uppdateringar för Windows 10-underhåll](media/3556023-windows-insiders-pre-release-feature-update.png)

Distribuera funktions uppdateringar för Windows Insider till din mål samling precis som med andra uppgraderingar. Men du vill ha följande saker i åtanke när du distribuerar dessa funktions uppdateringar:

- Dessa uppgraderingar gäller för alla Windows 10-klienter 1903 eller tidigare, med matchande arkitektur, utgåva och språk.
- Det finns licens villkor, distributionen måste godkänna villkoren för att kunna installeras.
- Överväg att använda [tråd prioritet i klient inställningar](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority).
- Dynamisk uppdatering installerar automatiskt viktiga uppdateringar, inklusive den senaste kumulativa uppdateringen, direkt från Microsoft Update. Det här beteendet startas med funktions uppdateringar för Windows 10 version 1903. 
  - Du kan uttryckligen [inaktivera dynamisk uppdatering i klient inställningar](../../core/clients/deploy/about-client-settings.md#bkmk_du) eller med en [setupconfig.ini-fil](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options). 
  - Mer information finns i blogg inlägget för [dynamisk uppdatering i Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) .

Mer information om hur du distribuerar uppgraderingar finns i [hantera Windows som en tjänst](../../osd/deploy-use/manage-windows-as-a-service.md).


### <a name="keeping-insider-devices-up-to-date"></a>Hålla Insider-enheter aktuella

Kumulativa uppdateringar för Windows Insider är tillgängliga för WSUS och efter tillägg för Configuration Manager. Dessa ackumulerade uppdateringar publiceras med en frekvens som liknar Windows 10 version 1903 kumulativa uppdateringar. Kumulativa Windows Insider-uppdateringar finns i produkt kategorin **Windows Insider för hands version** och klassificeras som antingen **säkerhets uppdateringar** eller **uppdateringar**. Du kan distribuera de kumulativa uppdateringarna för Windows Insider med en vanlig program uppdaterings process som att använda [automatiska distributions regler](../deploy-use/automatically-deploy-software-updates.md) eller stegvisa [distributioner](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json).

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> Utökade säkerhets uppdateringar och Configuration Manager

[ESU-programmet (Extended Security updates)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) är ett sista utväg-alternativ för kunder som behöver köra vissa äldre Microsoft-produkter efter Supportens slut. Den innehåller viktiga och/eller viktiga säkerhets uppdateringar (enligt definitionen i [Microsoft Security Response Center (MSRC)](https://www.microsoft.com/msrc)) i högst tre år efter produktens slut på datum för utökad support.

Produkter som ligger utanför support livs cykeln stöds inte för användning med Configuration Manager. Detta omfattar alla produkter som omfattas av ESU-programmet. Till exempel Windows 7. Säkerhets uppdateringar som släpps under ESU-programmet publiceras till Windows Server Update Services (WSUS). De här uppdateringarna visas i Configuration Manager-konsolen. Även om produkter som omfattas av ESU-programmet inte längre stöds för användning med Configuration Manager, kan den [senaste utgivna versionen av Configuration Manager aktuella grenen](../../core/servers/manage/updates.md#version-details) användas för att distribuera och installera Windows-säkerhetsuppdateringar som lanseras i programmet. Den senaste versionen kan också användas för att distribuera Windows 10 till enheter som kör Windows 7.

Klient hanterings funktioner som inte är relaterade till Windows program uppdaterings hantering eller operativ system distribution kommer inte längre att testas på de operativ system som omfattas av ESU-programmet och vi garanterar inte att de kommer att fortsätta att fungera. Vi rekommenderar starkt att du uppgraderar eller migrerar till en aktuell version av operativ systemen så snart som möjligt för att få klient hanterings stöd.


## <a name="next-steps"></a>Nästa steg

Starta synkroniseringen av program uppdateringar för att hämta program uppdateringar baserat på de nya kriterierna. Mer information finns i [Synkronisera program uppdateringar](synchronize-software-updates.md).
