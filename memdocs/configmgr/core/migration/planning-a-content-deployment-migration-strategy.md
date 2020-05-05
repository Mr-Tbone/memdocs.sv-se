---
title: Migrera innehåll
titleSuffix: Configuration Manager
description: Använd distributions platser för att hantera innehåll när du migrerar data till en Configuration Manager aktuella Branch-målhierarkin.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: afb39af5087daaca3b2bb6eb15f33d81d959beec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719689"
---
# <a name="plan-a-content-deployment-migration-strategy-in-configuration-manager"></a>Planera en strategi för migrering av innehålls distribution i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Medan du aktivt migrerar data till en Configuration Manager aktuella Branch-målhierarkin, kan Configuration Manager-klienter i både käll-och mål hierarkier upprätthålla åtkomsten till innehåll som du har distribuerat i källhierarkin. Du kan också använda migrering för att uppgradera eller omtilldela distributions platser från källhierarkin för att bli distributions platser i målhierarkin. När du delar och uppgraderar eller omtilldelar distributionsplatser kan den här strategin hjälpa dig att undvika att behöva distribuera om innehåll till nya servrar i målhierarkin för de klienter du migrerar.  

Även om du kan skapa om och distribuera innehåll i målhierarkin kan du även använda följande alternativ för att hantera det här innehållet:  

-   Dela distributionsplatser i källhierarkin med klienter i målhierarkin.  

-   Uppgradera fristående Configuration Manager 2007 distributions platser eller Configuration Manager 2007 sekundära platser i källhierarkin för att bli distributions platser i målhierarkin.  

-   Omtilldela distributions platser från en Configuration Manager-källhierarki till en plats i målhierarkin.  

##  <a name="share-distribution-points-between-source-and-destination-hierarchies"></a><a name="About_Shared_DPs_in_Migration"></a> Dela distributionsplatser mellan käll- och målhierarkier  
Under migrering kan du dela distributionsplatser från källhierarkin med målhierarkin. Du kan använda delade distributionsplatser för att se till att innehåll som du migrerar från en källhierarki omedelbart blir tillgängligt för klienter i målhierarkin utan att behöva skapa om innehållet, och sedan distribuera det till nya distributionsplatser i målhierarkin. När klienter i målhierarkin begär innehåll som distribuerats till distributionsplatser som du har delat kan de delade distributionsplatserna erbjudas till klienterna som giltiga innehållsplaceringar.  

 Förutom att det är en giltig innehålls plats för klienter i målhierarkin medan migreringen från källhierarkin fortfarande är aktiv, är det möjligt att uppgradera eller omtilldela en distributions plats till målhierarkin. Du kan uppgradera Configuration Manager 2007 delade distributions platser och omtilldela System Center 2012 Configuration Manager delade distributions platser. När du uppgraderar eller omtilldelar en delad distributionsplats tas distributionsplatsen bort från källhierarkin och blir en distributionsplats i målhierarkin. När du har uppgraderat eller omtilldelat en delad distributionsplats kan du fortsätta använda distributionsplatsen i målhierarkin efter att migreringen från källhierarkin är klar. Mer information om hur du uppgraderar en delad distributions plats finns i [Planera för att uppgradera Configuration Manager 2007 delade distributions platser](#Planning_to_Upgrade_DPs). Mer information om hur du omtilldelar en delad distributions plats finns i [Planera omtilldelning av Configuration Manager distributions platser](#BKMK_ReassignDistPoint).  

 Du kan välja att dela distributionsplatser från vilken källplats som helst i källhierarkin. När du delar distributions platser för en käll plats delas underordnade sekundära platser på varje kvalificerande distributions plats på den primära platsen och på var och en av de primära platserna. För att kvalificera sig för att vara en delad distributions plats måste den plats system server som är värd för distributions platsen konfigureras med ett fullständigt kvalificerat domän namn (FQDN). Eventuella distributions platser som har kon figurer ATS med ett NetBIOS-namn ignoreras.  

> [!TIP]  
>  Configuration Manager 2007 kräver inte att du konfigurerar ett fullständigt domän namn för plats system servrar.  

Använd följande information som hjälp att planera för delade distributionsplatser:  

-   Distributionsplatser som du delar måste uppfylla förutsättningarna för delade distributionsplatser. Mer information om de här kraven finns i [obligatoriska konfigurationer för migrering](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) i [krav för migrering](../../core/migration/prerequisites-for-migration.md).  

-   Delningen av distributionsplatsen är en platsomfattande inställning som delar alla kvalificerade distributionsplatser på en källplats och alla direkt underordnade sekundära platser. Du kan inte välja att dela enskilda distributionsplatser när du aktiverar delning av distributionsplatser.  

-   Klienter i målhierarkin kan ta emot information om innehållsplacering för paket som distribueras till distributionsplatser som delas från källhierarkin. För distributions platser från en Configuration Manager 2007-källhierarki inkluderar detta gren distributions platser, distributions platser på server resurser och standard distributions platser.  

    > [!WARNING]  
    >  Om du ändrar källhierarkin är delade distributionsplatser från den ursprungliga källhierarkin inte längre tillgängliga och kan inte erbjudas till klienterna i målhierarkin som giltiga innehållsplaceringar. Om du konfigurerar om migreringen så att den använder den ursprungliga källhierarkin återställs de tidigare delade distributionsplatserna som giltiga servrar för innehållsplacering.  

-   När du migrerar ett paket som en delad distributionsplats är värddator för måste paketversionen förbli densamma i käll- och målhierarkierna. Om paketen i käll- och målhierarkin har olika versioner kan inte klienter i målhierarkin hämta innehållet från den delade distributionsplatsen. Så om du uppdaterar ett paket i källhierarkin måste du migrera om paketdata innan klienter i målhierarkin kan hämta detta innehåll från en delad distributionsplats.  

    > [!NOTE]  
    >  När du visar information om ett paket som finns på en delad distributions plats, uppdateras inte det antal paket som visas som **värdbaserade migrerade paket** på käll platsens fliken **delade distributions platser** förrän nästa data insamlings cykel har slutförts.  

-   Du kan visa delade distributions platser och deras egenskaper i noden **källhierarki** på arbets ytan **Administration** i Configuration Manager-konsolen som ansluter till målhierarkin.  

-   Du kan inte använda en delad distributions plats från en Configuration Manager 2007-källhierarki som värd för paket för Microsoft Application Virtualization (App-V). App-V-paket måste migreras och konverteras för användning med klienter i målhierarkin. Du kan dock använda en delad distributions plats från en System Center 2012 Configuration Manager eller Configuration Manager aktuell Branch-källhierarki som värd för App-V-paket för klienter i en målhierarkin.  

-   När du delar en skyddad distributions plats från en Configuration Manager 2007-källhierarki skapar målhierarkin en avgränsnings grupp som innehåller de skyddade nätverks platserna för den distributions platsen. Du kan inte ändra den här gränser gruppen i målhierarkin. Men om du ändrar skyddad avgränsnings information för distributions platsen i Configuration Manager 2007-källhierarkin, återspeglas ändringen i målhierarkin när nästa data insamlings cykel har slutförts.  

    > [!NOTE]  
    >  System Center 2012 Configuration Manager och Configuration Manager aktuella gren webbplatser använder begreppet primära distributions platser i stället för skyddade distributions platser. Detta villkor gäller endast för distributions platser som delas från Configuration Manager 2007-käll platser.  

De kvalificerade distributions platserna visas inte i Configuration Manager-konsolen innan du delar distributions platser från en käll plats. När du har delat distributionsplatserna visas bara de distributionsplatser för vilka delningen lyckats.  

När du har delat distributionsplatser kan du ändra konfigurationen för alla delade distributionsplatser i källhierarkin. Ändringar som du gör i konfigurationen för en distributionsplats avspeglas i målhierarkin när nästa datainsamlingscykel slutförts. Distributionsplatser som du uppdaterade så att de är kvalificerade för delning, delas automatiskt. De som inte längre är kvalificerade slutar dela distributionsplatser. Du kan till exempel ha en distributions plats som inte har kon figurer ATS med ett intranät-FQDN och som inte ursprungligen delades med målhierarkin. När du har konfigurerat FQDN för den distributions platsen identifierar nästa data insamlings cykel den här konfigurationen och distributions platsen delas sedan med målhierarkin.  

##  <a name="plan-to-upgrade-configuration-manager-2007-shared-distribution-points"></a><a name="Planning_to_Upgrade_DPs"></a>Planera uppgraderingen Configuration Manager 2007 delade distributions platser  
När du migrerar från en Configuration Manager 2007-källhierarki kan du uppgradera en delad distributions plats så att den blir en Configuration Manager nuvarande gren distributions plats. Du kan uppgradera distributions platser på primära platser och sekundära platser. Uppgraderings processen tar bort distributions platsen från Configuration Manager 2007-hierarkin och gör den till en plats system server i målhierarkin. Den här processen kopierar också det befintliga innehållet på distributions platsen till en ny plats på distributions plats datorn. Uppgraderingsprocessen ändrar sedan kopian av innehållet för att skapa SIS (Single Instance Store) som ska användas med innehållsdistribution i målhierarkin. När du uppgraderar en distributions plats behöver du därför inte omdistribuera migrerat innehåll som finns på distributions platsen för Configuration Manager 2007.  

När Configuration Manager har konverterat innehållet till det enskilda instans lagret Configuration Manager tar bort det ursprungliga käll innehållet på distributions plats datorn för att frigöra disk utrymme. Configuration Manager använder inte den ursprungliga käll innehålls platsen.  

Alla Configuration Manager 2007-distributions platser som du kan dela är inte tillgängliga för uppgradering till Configuration Manager aktuella grenen. För att vara kvalificerad för uppgradering måste en distributions plats för Configuration Manager 2007 uppfylla villkoren för uppgradering. Dessa villkor omfattar den plats system server som distributions platsen är installerad på och den typ av Configuration Manager 2007-distributions plats som är installerad. Du kan t.ex. inte uppgradera någon typ av distributionsplats som är installerad på platsserverdatorn på en primär plats, men du kan uppgradera en standarddistributionsplats som är installerad på platsserverdatorn på en sekundär plats.  

> [!NOTE]  
>  Du kan bara uppgradera de Configuration Manager 2007 delade distributions platser som finns på en dator som kör en operativ system version som stöds för distributions platser i målhierarkin. Även om du kan dela en Configuration Manager 2007-distributions plats som finns på en dator som kör Windows Vista, kan du inte uppgradera den här delade distributions platsen eftersom operativ systemet inte stöds av Configuration Manager aktuella grenen för användning som distributions plats.  

I följande tabell visas de platser som stöds för varje typ av Configuration Manager 2007-distributions plats som du kan uppgradera.  

|Distributionsplatstyper|Distributionsplats på en annan platssystemdator än platsservern|Distributionsplats på en annan platssystemdator än platsservern som är värd för andra platssystemroller|Distributionsplats på en sekundär platsserver|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|Standarddistributionsplats|Ja|Inga|Ja|  
|Distributionsplats på serverresurser<sup>1</sup>|Ja|Inga|Inga|  
|Grendistribution|Ja|Inga|Inga|  

 <sup>1</sup> Configuration Manager aktuella grenen stöder inte server resurser för plats system, men det stöder uppgradering av en distributions plats för Configuration Manager 2007 som finns på en server resurs. När du uppgraderar en Configuration Manager 2007-distributions plats som finns på en server resurs, konverteras distributions plats typen automatiskt till en server, och du måste välja den enhet på distributions plats datorn som ska lagra innehålls lagringen för den enskilda instansen.  

> [!WARNING]  
>  Innan du uppgraderar en gren distributions plats avinstallerar du Configuration Manager 2007-klient program varan. När du uppgraderar en gren distributions plats där Configuration Manager 2007-klientprogrammet är installerad, tas det innehåll som tidigare distribuerades till datorn bort från datorn och uppgraderingen av distributions platsen Miss lyckas.  

Om du vill identifiera distributions platser som är tillgängliga för uppgradering i Configuration Manager-konsolen i noden **källhierarki** väljer du en käll plats och sedan fliken **delade distributions platser** . de kvalificerade distributions platserna visar **Ja** i kolumnen **berättigande för uppgradering** .  

När du uppgraderar en distributions plats som är installerad på en sekundär plats Server Configuration Manager 2007 avinstalleras den sekundära platsen från källhierarkin. Även om det här scenariot kallas för en uppgradering av en sekundär plats så gäller detta bara systemrollen för distributionsplatsen. Resultatet är att den sekundära platsen inte uppgraderas och i stället avinstalleras. Detta lämnar en distributions plats från målhierarkin på datorn som var den sekundära plats servern. Om du planerar att uppgradera distributions platsen på en sekundär plats, se [Planera att uppgradera Configuration Manager 2007 sekundära platser](#BKMK_UpgradeSS) i den här artikeln.  

###  <a name="distribution-point-upgrade-process"></a><a name="BKIMK_UpgradeProcess"></a> Uppgraderingsprocessen för distributionsplatser  
Du kan använda Configuration Manager-konsolen för att uppgradera Configuration Manager 2007-distributions platser som du har delat med målhierarkin. När du uppgraderar en delad distributions plats avinstalleras distributions platsen från Configuration Manager 2007-platsen. Den installeras sedan som en distributions plats som är kopplad till en primär eller sekundär plats som du anger i målhierarkin. Med uppgraderingsprocessen skapas en kopia av det migrerade innehållet som lagras på distributionsplatsen och sedan konverteras den här kopian till innehållslagringen för den enskilda instansen. När Configuration Manager konverterar ett paket till innehålls lagringen för den enskilda instansen raderas det paketet från SMSPKG-resursen på distributions plats datorn om inte paketet har en eller flera annonser som har ställts in för att **köra program från distributions platsen**.  

För att uppgradera distributions platsen använder Configuration Manager det **åtkomst konto för käll plats** som har kon figurer ATS för att samla in data från käll PLATSens SMS-provider. Även om det här kontot bara kräver **Läs** behörighet för plats objekt för att samla in data från käll platsen, måste det också ha behörigheten **ta bort** och **ändra** till **plats** klassen för att kunna ta bort distributions platsen från Configuration Manager 2007-platsen under uppgraderingen.  

> [!NOTE]  
>  Configuration Manager kan endast konvertera innehåll till ett enda instans lager på en distributions plats i taget. När du ställer in flera uppgraderingar av distributions platser köas distributions platserna för uppgradering och bearbetas en i taget.  

Innan du uppgraderar en delad distributionsplats ska du kontrollera att allt innehåll som distribueras till distributionsplatsen har migrerats. Innehåll som du inte migrerar innan du uppgraderar distributionsplatsen är inte tillgängligt i målhierarkin efter uppgraderingen. När du uppgraderar en distributionsplats konverteras innehållet i de migrerade paketen till ett format som är kompatibelt med den enskilda instanslagringen i målhierarkin.  

Om du vill uppgradera en distributions plats inifrån Configuration Manager-konsolen måste Configuration Manager 2007-plats system servern uppfylla följande villkor:  

-   Distributionsplatskonfigurationen och platsen måste vara tillämpliga för uppgradering.  

-   Distributions plats datorn måste ha tillräckligt med disk utrymme för att innehållet ska kunna konverteras från Configuration Manager 2007-innehålls lagrings formatet till det enskilda instans lagrings formatet. Den här konverteringen kräver ett tillgängligt ledigt diskutrymme motsvarande storleken på det största paket som lagras på distributionsplatsen.  

-   Distributionsplatsdatorn måste köra en operativsystemsversion som stöds som en distributionsplats i målhierarkin.  

    > [!NOTE]  
    >  När Configuration Manager kontrollerar om en distributions plats är berättigad, verifierar den inte operativ Systems versionen för distributions plats datorn.  

Om du vill uppgradera en distributions plats expanderar du **migrering**i arbets ytan **Administration** , expanderar noden **källhierarki** och väljer sedan den plats som har den distributions plats som du vill uppgradera. Sedan väljer du den distributionsplats som du vill uppgradera på fliken **Delade distributionsplatser** .  

Du kan bekräfta att distributionsplatsen är klar för uppgradering genom att granska statusen i kolumnen **Tillämplig för omtilldelning** .  Klicka sedan på fliken **distributions platser** i menyfliksområdet för Configuration Manager konsolen, i gruppen **distributions plats** , väljer du **omtilldela**. Då öppnas en guide som du kan använda för att slutföra uppgraderingen av distributions platsen.  

När du uppgraderar en delad distributionsplats måste du tilldela distributionsplatsen till en valfri primär eller sekundär plats i målhierarkin. När distributions platsen har uppgraderats hanterar du distributions platsen som en distributions plats i målhierarkin, till exempel andra distributions platser.  

Du kan övervaka förloppet för en distributions plats uppgradering i Configuration Manager-konsolen genom att välja noden **migrering av distributions plats** under noden **migrering** i arbets ytan **Administration** . Du kan också visa information i **Migmctrl.log** på servern för den centrala administrationsplatsen i målhierarkin eller i **distmgr.log** på platsservern i destinationshierarkin som hanterar den uppgraderade distributionsplatsen.  

> [!NOTE]  
>  När du uppgraderar en distributions plats till målhierarkin tas plats system rollen för distributions platsen bort från käll platsen för Configuration Manager 2007. Paket som har skickats till distributions platsen uppdateras dock inte i Configuration Manager 2007-hierarkin. I Configuration Manager 2007-konsolen fortsätter paket som har skickats till distributions platsen att lista plats system datorn som en distributions plats med en **okänd** **typ** . Efterföljande uppdateringar av paketet i Configuration Manager 2007 resulterar i rapporterings fel i distributions hanteraren i Distmgr. log för den platsen när platsen försöker uppdatera paketet på det okända plats systemet.  

Om du väljer att inte uppgradera en delad distributions plats kan du fortfarande installera en distributions plats från målhierarkin på en tidigare Configuration Manager 2007-distributions plats. Innan du kan installera den nya distributions platsen måste du först avinstallera alla Configuration Manager 2007-plats system roller från distributions plats datorn. Detta omfattar Configuration Manager 2007-platsen om det är plats serverdatorn. När du avinstallerar en distributions plats för Configuration Manager 2007 tas inte innehåll som har distribuerats till distributions platsen bort från datorn.  

###  <a name="plan-to-upgrade-configuration-manager-2007-secondary-sites"></a><a name="BKMK_UpgradeSS"></a>Planera uppgradering Configuration Manager 2007 sekundära platser  
 När du använder migrering för att uppgradera en delad distributions plats som finns på en Configuration Manager 2007 sekundär plats Server, Configuration Manager uppgradera distributions plats system rollen som en distributions plats i målhierarkin. Den sekundära platsen avinstalleras också från källhierarkin. Resultatet är en Configuration Manager aktuell gren distributions plats, men ingen sekundär plats.  

 För att en distributions plats på plats serverdatorn ska vara kvalificerad för uppgradering måste Configuration Manager kunna avinstallera den sekundära platsen och var och en av plats system rollerna på den datorn. Normalt är en delad distributions plats på en Configuration Manager 2007-server resurs tillgänglig för uppgradering. När det finns en serverdelning på den sekundära platsservern är dock den sekundära platsen och alla delade distributionsplatser på den datorn inte tillämpliga för uppgradering. Detta beror på att Server resursen behandlas som ett ytterligare plats system objekt när processen försöker avinstallera den sekundära platsen, och den här processen kan inte avinstallera det här objektet. I det här scenariot kan du aktivera en standarddistributionsplats på den sekundära platsservern och sedan omdistribuera innehållet till den standarddistributionsplatsen. Den här processen använder inte nätverks bandbredd, och när det är klart kan du avinstallera distributions platsen på Server resursen, ta bort Server resursen och sedan uppgradera distributions platsen och den sekundära platsen.  

 Innan du uppgraderar en delad distributions plats granskar du distributions plats konfigurationen i Configuration Manager 2007 för att undvika att uppgradera en distributions plats på en sekundär plats som du fortfarande vill använda med Configuration Manager 2007. Det här är en bra rutin, eftersom när du har uppgraderat en delad distributions plats som finns på en sekundär plats server tas plats system servern bort från Configuration Manager 2007-hierarkin och är inte längre tillgänglig för användning med den hierarkin. När den sekundära platsen tas bort kopplas eventuella återstående distributionsplatser på den sekundära platsen bort. Det innebär att de blir ohanterade från Configuration Manager 2007 och inte längre delas eller är kvalificerade för uppgradering.  

> [!WARNING]  
>  När du visar delade distributions platser i Configuration Manager-konsolen finns det ingen synlig indikation på att en delad distributions plats finns på en fjärran sluten plats system Server eller på den sekundära plats servern.  

 Om du har en sekundär plats på en fjärran sluten nätverks plats som huvudsakligen används för att styra distributionen av innehåll till den fjärrplatsen bör du överväga att uppgradera sekundära platser som har en delad distributions plats. Eftersom du kan konfigurera bandbredds kontroll för när du distribuerar innehåll till en Configuration Manager aktuell gren distributions plats, kan du ofta uppgradera en sekundär plats till en distributions plats, konfigurera distributions platsen för bandbredds kontroller och undvika att installera en sekundär plats på den nätverks platsen i målhierarkin.  

 Processen att uppgradera en delad distributions plats på en sekundär plats Server är samma som alla andra distributions plats uppgraderingar. Innehållet kopieras och konverteras till det enskilda instans arkivet som används av målhierarkin. Men när du uppgraderar en delad distributions plats som finns på en sekundär plats Server avinstallerar uppgraderings processen även hanterings platsen (om den finns) och avinstallerar sedan den sekundära platsen från servern. Resultatet är att den sekundära platsen tas bort från Configuration Manager 2007-hierarkin. För att avinstallera den sekundära platsen använder Configuration Manager det konto som har kon figurer ATS för att samla in data från käll platsen.  

 Under uppgraderingen uppstår en fördröjning mellan när den sekundära Configuration Manager 2007-platsen är avinstallerad och när installationen av distributions platsen i målhierarkin börjar. Data insamlings cykeln bestämmer den här fördröjningen på upp till fyra timmar. Fördröjningen är avsedd att ge tiden för den sekundära platsen att avinstalleras innan den nya distributions plats installationen påbörjas.  

 Mer information om hur du uppgraderar en delad distributions plats finns i [Planera för att uppgradera Configuration Manager 2007 delade distributions platser](#Planning_to_Upgrade_DPs).  

##  <a name="plan-to-reassign-configuration-manager-distribution-points"></a><a name="BKMK_ReassignDistPoint"></a>Planera omtilldelningen Configuration Manager distributions platser  
 När du migrerar från en version av System Center 2012 Configuration Manager som stöds till en hierarki med samma version kan du omtilldela en delad distributions plats från källhierarkin till en plats i målhierarkin. Detta är till exempel begreppet att uppgradera en distributions plats för Configuration Manager 2007 så att den blir en distributions plats i målhierarkin. Du kan omtilldela distributions platser från primära platser och sekundära platser. Åtgärden att omtilldela en distributions plats tar bort distributions platsen från källhierarkin och gör datorn och dess distributions plats till en plats system Server för den plats som du har valt i målhierarkin.  

 När du omtilldelar en distributionsplats behöver du inte omdistribuera migrerat innehåll som har distributionsplatsen för källplatsen som värd. Till skillnad från uppgraderingen av en Configuration Manager 2007-distributions plats kräver omtilldelning av en distributions plats inte ytterligare disk utrymme på distributions plats datorn. Detta beror på att från och med System Center 2012 Configuration Manager använder distributions platser det enskilda instans lagrings formatet för innehåll. Innehållet på distributions plats datorn behöver inte konverteras när distributions platsen omtilldelas mellan hierarkier.  

 För att en System Center 2012-Configuration Manager distributions plats ska vara berättigad till omtilldelning måste den uppfylla följande kriterier:  

-   En delad distributionsplats måste installeras på en annan dator än platsservern.  

-   En delad distributionsplats kan inte samordnas med några ytterligare platssystemroller.  

Om du vill identifiera distributions platser som är tillgängliga för omtilldelning i Configuration Manager-konsolen i noden **källhierarki** väljer du en käll plats och sedan fliken **delade distributions platser** . de kvalificerade distributions platserna visar **Ja** i kolumnen **berättigande för omtilldelning** (den här kolumnen heter **giltig för uppgradering** innan System Center 2012 R2 Configuration Manager).  

###  <a name="distribution-point-reassignment-process"></a><a name="BKMK_ReassignProcess"></a> Omtilldelningsprocessen för distributionsplatser  
 Du kan använda Configuration Manager-konsolen för att omtilldela distributions platser som du har delat från en aktiv-källhierarki. När du omtilldelar en delad distributions plats avinstalleras distributions platsen från sin käll plats och installeras sedan som en distributions plats som är kopplad till en primär eller sekundär plats som du anger i målhierarkin.  

 För att omtilldela distributions platsen använder målhierarkin det åtkomst konto för käll plats som har kon figurer ATS för att samla in data från käll platsens SMS-provider. Information om nödvändiga behörigheter och ytterligare krav finns i [krav för migrering](../../core/migration/prerequisites-for-migration.md).  

## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrera flera delade distributions platser på samma gång
Från och med version 1610 kan du använda **omtilldela distributions platsen** för att Configuration Manager processen parallellt med omtilldelningen av upp till 50 delade distributions platser på samma gång. Detta inkluderar delade distributions platser från käll platser som stöds och som kör:  
- Configuration Manager 2007
- System Center 2012 Configuration Manager
- System Center 2012 R2 Configuration Manager
- Configuration Manager (aktuell gren)

När du omtilldelar distributions platser måste varje distributions plats kvalificeras för att antingen uppgraderas eller omtilldelas. Namnet på åtgärden och processen som ingår (uppgradera eller omtilldela) beror på vilken version av Configuration Manager käll platsen körs på. Slut resultaten för båda åtgärderna är desamma: distributions platsen tilldelas till en av dina Current Branch-platser med innehållet på plats.

Före version 1610 kunde Configuration Manager endast bearbeta en distributions plats i taget. Nu kan du tilldela så många distributions platser som du vill med följande varningar:  
- Även om du inte kan välja distributions platser som ska omtilldelas när du har köade fler än en, kommer Configuration Manager att bearbeta dem parallellt i stället för att vänta en innan du startar nästa.  
- Som standard bearbetas upp till 50 distributions platser parallellt i taget. När omtilldelningen av den första distributions platsen är färdig börjar Configuration Manager bearbeta 51st och så vidare.  
- När du använder Configuration Manager SDK kan du ändra **SharedDPImportThreadLimit** för att justera antalet omtilldelade distributions platser som Configuration Manager kan bearbeta parallellt.


##  <a name="assign-content-ownership-when-migrating-content"></a><a name="About_Migrating_Content"></a>Tilldela innehålls ägarskap vid migrering av innehåll  
 När du migrerar innehåll för distributioner måste du tilldela innehållsobjektet till en plats i målhierarkin. Den här platsen blir sedan ägaren till det innehållet i destinationshierarkin. Även om platsen på den översta nivån i målhierarkin är den plats som migrerar metadata för innehåll, är den tilldelade platsen som använder de ursprungliga källfilerna för innehållet i nätverket.  

 Om du vill minimera nätverksbandbredden som används när du migrerar innehåll kan du överföra ägarskap för innehåll till en plats i målhierarkin som är nära i nätverket till innehållsplatsen i källhierarkin. Eftersom information om innehållet i målhierarkin delas globalt är den tillgänglig på alla platser.  

 Även om information om innehållet delas på alla platser med hjälp av databasreplikering, så överförs allt innehåll som du tilldelar till en primär plats och sedan distribuerar till distributions platser på andra primära platser med hjälp av filbaserad replikering. Den här överföringen dirigeras genom den centrala administrationsplatsen och sedan till den ytterligare primära platsen. Du kan minska data överföringar i nätverk med liten bandbredd genom att centralisera paket som du planerar att distribuera till flera primära platser före eller under migreringen när du tilldelar en plats som innehålls ägare.
