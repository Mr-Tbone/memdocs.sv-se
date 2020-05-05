---
title: Planera klientmigrering
titleSuffix: Configuration Manager
description: Lär dig mer om de aktiviteter som migrerar klienter från en källhierarki till en Configuration Manager aktuella Branch-målhierarkin.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0885cab43deacf7e7f487e5c20e171f6475b302
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720914"
---
# <a name="plan-a-client-migration-strategy-in-configuration-manager"></a>Planera en strategi för klientmigrering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Om du vill migrera klienter från källhierarkin till en Configuration Manager aktuella gren måls hierarki måste du utföra två uppgifter. Du måste migrera objekten som är kopplade till klienten, och du måste sedan installera om eller återtilldela klienterna från källhierarkin till målhierarkin. Objekten migreras först, så att de är tillgängliga när klienterna migreras. Objekten som är kopplade till klienten migreras med hjälp av migreringsjobb. Information om hur du migrerar de objekt som är associerade med-klienten finns i [Planera en jobb strategi för migrering](../../core/migration/planning-a-migration-job-strategy.md).  

 Använd de följande avsnitten när du planerar att migrera klienter till målhierarkin.  

-   [Planera att migrera klienter till målhierarkin](#Planning_for_Client_Agent_Migration)  

-   [Planera hanteringen av data som finns på klienterna under migrering](#Planning_for_Client_Data_Migration)  

-   [Planera för inventerings-och efterlevnadsprinciper under migrering](#Planning_for_Inventory_data_migration)  

##  <a name="plan-to-migrate-clients-to-the-destination-hierarchy"></a><a name="Planning_for_Client_Agent_Migration"></a> Planera att migrera klienter till målhierarkin  
 När du migrerar klienter från en-källhierarki uppgraderas klient program varan på klient datorn så att den matchar produkt versionen av målhierarkin.  

-   **En Configuration Manager 2007-källhierarki:** När du migrerar klienter från en-källhierarki som kör en version av Configuration Manager som stöds, uppgraderas klient program varan till klient versionen för målhierarkin.  

-   **En källhierarki för System Center 2012 Configuration Manager eller senare:** När du migrerar klienter mellan hierarkier med samma produkt version, ändras eller uppgraderas inte klient program varan. Klienter omtilldelas i stället från källhierarkin till en plats i målhierarkin.  

    > [!NOTE]  
    >  När en hierarkis produktversion inte stöds för migrering till målhierarkin, måste du uppgradera alla platser och klienter i källhierarkin till en kompatibel produktversion. När källhierarkin har uppgraderats till en produktversion som stöds, kan du migrera mellan hierarkierna. Mer information finns i [versioner av Configuration Manager som stöds för migrering](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions) i [krav för migrering](../../core/migration/prerequisites-for-migration.md).  

Använd följande information när du planerar klientmigreringen:  

-   Om du vill uppgradera eller omtilldela klienter från en käll- till en målplats, kan du använda en valfri klientdistributionsmetod som stöds för distribution av klienter i målhierarkin. Några vanliga klientdistributionsmetoder är push-installation av klienter, programvarudistribution, Grupprincip samt klientinstallation baserad på programuppdatering. Mer information finns i [klient installations metoder](../../core/clients/deploy/plan/client-installation-methods.md).  

-   Se till att enheten som kör-klient program varan i källhierarkin uppfyller minimi kraven för maskin vara och kör ett operativ system som stöds av versionen av Configuration Manager i målhierarkin.  

-   Innan du migrerar en-klient ska du köra ett migreringsjobb för att migrera den information som klienten ska använda i målhierarkin.  

-   Klienter som uppgraderas behåller sin körnings historik för distributioner. Detta förhindrar distributioner från att köras i onödan i målhierarkin.  

    -   För Configuration Manager 2007-klienter behålls annons körnings historiken.  

    -   För klienter från System Center 2012 Configuration Manager eller Configuration Manager aktuella grenen behålls distributions körnings historiken.  

-   Du kan migrera klienter från platser i källhierarkin i vilken ordning du vill. Du bör dock överväga att migrera ett begränsat antal klienter i olika faser i stället för att migrera ett stort antal klienter på samma gång. En etappindelad migrering minskar kraven på nätverksbandbredd och serverbearbetning när varje uppgraderad klient skickar in fullständig information om sitt lager och sin regelefterlevnad till den utsedda platsen.  

-   När du migrerar Configuration Manager 2007-klienter avinstalleras den befintliga klient program varan från klient datorn och den nya klient program varan installeras.  

-   Configuration Manager kan inte migrera en Configuration Manager 2007-klient som har App-V-klienten installerad, om inte App-V-klientens version är 4,6 SP1 eller senare.  

Du kan övervaka migreringsprocessen för klienter i noden **migrering** i arbets ytan **Administration** i Configuration Manager-konsolen.  

När du har migrerat klienten till målhierarkin kan du inte längre hantera den enheten med hjälp av källhierarkin, och du bör överväga att ta bort klienten från källhierarkin. Det är visserligen inte obligatoriskt när du migrerar hierarkier, men det kan förhindra att en migrerad klient identifieras i en rapport i källhierarkin eller att ett felaktigt antal resurser beräknas mellan de två hierarkierna under migreringen. Låt oss ta ett exempel. Om en migrerad klient blir kvar i källplatsens databas, skulle du kunna köra en rapport om programuppdateringar där datorn felaktigt pekas ut som att den är en ej hanterad resurs, trots att den nu hanteras av målhierarkin.  

##  <a name="plan-to-handle-data-maintained-on-clients-during-migration"></a><a name="Planning_for_Client_Data_Migration"></a>Planera för att hantera data som underhålls på klienterna under migreringen  
När du migrerar en klient från dess källhierarki till målhierarkin, behålls viss information på enheten, medan annan information inte är tillgänglig på enheten efter migreringen.  

Följande information behålls på klientenheten:  

-   Den unika identifieraren (GUID) som kopplar en klient till dess information i Configuration Manager databasen.  

-   Annons- eller distributionshistoriken, som hindrar klienterna från att i onödan skicka annonser eller distributioner på nytt i målhierarkin.  

Följande information behålls inte på klientenheten:  

-   Filerna i klientcachen. Om klienten behöver dessa filer för att installera program, hämtas de igen från målhierarkin.  

-   Information från källhierarkin om eventuella annonser eller distributioner som inte har körts. Om du vill att klienten ska köra annonserna eller distributionerna efter migreringen, måste du distribuera dem på nytt till klienten i målhierarkin.  

-   Information om inventering. Klienten skickar den här informationen igen till dess tilldelade plats i målhierarkin efter att klienten migreras och de nya klient data har genererats.  

-   Efterlevnadsdata. Klienten skickar den här informationen igen till dess tilldelade plats i målhierarkin efter att klienten migreras och de nya klient data har genererats.  

När en klient migreras behålls inte information som lagras i Configuration Manager klient registret och fil Sök vägen. Tillämpa dessa inställningar igen efter migreringen. Detta är några vanliga inställningar:  

-   Energischeman  

-   Loggningsinställningar  

-   Lokala principinställningar  

Dessutom kan du behöva installera om vissa program.  

##  <a name="plan-for--inventory-and-compliance-data-during-migration"></a><a name="Planning_for_Inventory_data_migration"></a> Planera för inventerings- och efterlevnadsdata under migrering  
Klientens inventerings- och efterlevnadsdata sparas inte när du migrerar en klient till målhierarkin. Dessa uppgifter återskapas i målhierarkin när klienten skickar sina uppgifter till sin tilldelade plats för första gången. Minska behovet av nätverksbandbredd och bearbetning på servern genom att migrera ett mindre antal klienter i etapper i stället för att migrera ett stort antal klienter på samma gång.  

 Dessutom kan du inte migrera anpassningar av maskinvaruinventeringen från en källhierarki. Dessa måste införas i källhierarkin oberoende av migreringen. Information om hur du utökar maskin varu inventeringen finns i [så här konfigurerar du maskin varu inventering](../../core/clients/manage/inventory/configure-hardware-inventory.md).  
