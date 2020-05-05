---
title: Metodtips för programuppdateringar
titleSuffix: Configuration Manager
description: Använd dessa metod tips för program uppdateringar i Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: dc0d416fdd186dbbeb4c61d48b688072bb830485
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723994"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Metod tips för program uppdateringar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller metod tips för program uppdateringar i Configuration Manager. Informationen är sorterad i metod tips för inledande installation och för pågående åtgärder.  



## <a name="installation-best-practices"></a><a name="bkmk_install"></a>Metod tips för installation  

Använd följande metod tips när du installerar program uppdateringar i Configuration Manager.  


### <a name="use-a-shared-wsus-database-for-software-update-points"></a><a name="bkmk_shared-susdb"></a>Använd en delad WSUS-databas för program uppdaterings platser  

Om du installerar fler än en programuppdateringsplats på en primär plats, använder du samma WSUS-databas för varje programuppdateringsplats i samma Active Directory-skog. Om du delar samma databas minimerar den avsevärt, men eliminerar inte helt, klienten och nätverkets prestanda påverkan som du kan uppleva när klienter växlar till en ny program uppdaterings plats. En delta sökning sker fortfarande när en klient växlar till en ny program uppdaterings plats som delar en databas med den gamla program uppdaterings platsen, men genomsökningen är mycket mindre än så är det om WSUS-servern har en egen databas. Mer information om växling av program uppdaterings platser finns i [byte av program uppdaterings punkt](plan-for-software-updates.md#BKMK_SUPSwitching).  

> [!IMPORTANT]  
>  Dela även lokala mappar för WSUS-innehåll när du använder en delad WSUS-databas för program uppdaterings platser.  

Mer information om hur du delar WSUS-databasen finns i följande blogg inlägg:  

- [Så här implementerar du en delad SUSDB för Configuration Manager program uppdaterings platser](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103)  

- [Att tänka på för flera WSUS-instanser som delar en innehålls databas när du använder Configuration Manager](https://blogs.technet.microsoft.com/wsus/2014/03/22/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb/)  


### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-to-use-a-named-instance-and-the-other-to-use-the-default-instance"></a><a name="bkmk_sql-instance"></a>När Configuration Manager och WSUS använder samma SQL Server konfigurerar du en för att använda en namngiven instans och den andra för att använda standard instansen  

När Configuration Manager-och WSUS-databaserna delar samma instans av SQL Server kan du enkelt fastställa resursanvändningen mellan de två programmen. Använd olika SQL Server-instanser för Configuration Manager och WSUS. Den här konfigurationen gör det enklare att felsöka och diagnostisera resursanvändnings problem som kan uppstå för varje program.  


### <a name="specify-the-store-updates-locally-setting"></a><a name="bkmk_store-local"></a>Ange inställningen "Spara uppdateringar lokalt"  

När du installerar WSUS väljer du inställningen för att **lagra uppdateringar lokalt**. Den här inställningen gör att WSUS hämtar de licens villkor som är associerade med program uppdateringar. Villkoren hämtas under synkroniseringsprocessen och lagras på WSUS-serverns lokala hård disk. Om du inte väljer den här inställningen kan klient datorerna inte söka efter program uppdateringar som har licens villkor. Komponenten **WSUS Synchronization Manager** i program uppdaterings platsen verifierar att den här inställningen är aktive rad var 60: e minut som standard.  



## <a name="operational-best-practices"></a><a name="bkmk_operation"></a>Metod tips för användning  

Använd följande metoder när du använder programvaruuppdateringar:  


### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a><a name="bkmk_object-limit"></a>Begränsa program uppdateringar till 1000 i en enda program uppdaterings distribution  

Begränsa antalet program uppdateringar till 1000 i varje program uppdaterings distribution. När du skapar en regel för automatisk distribution ska du kontrol lera att de angivna kriterierna inte resulterar i fler än 1000 program uppdateringar. Om du distribuerar program uppdateringar manuellt ska du inte välja fler än 1000 uppdateringar.  


### <a name="create-a-new-software-update-group-each-time-an-adr-runs-for-patch-tuesday-and-for-general-deployments"></a><a name="bkmk_new-group"></a>Skapa en ny program uppdaterings grupp varje gången en ADR körs för "korrigerings tisdag" och för allmänna distributioner  

Det finns en gräns på 1000 program uppdateringar i en distribution. När du skapar en automatisk distributions regel (ADR) anger du om du vill använda en befintlig uppdaterings grupp eller skapa en ny uppdaterings grupp varje gång regeln körs. Om du anger kriterier i en ADR som resulterar i flera program uppdateringar och regeln körs enligt ett återkommande schema, skapar du en ny program uppdaterings grupp varje gången regeln körs. Det här beteendet förhindrar att distributionen överskrider gränsen på 1000 program uppdateringar per distribution.  


### <a name="use-an-existing-software-update-group-for-adrs-for-endpoint-protection-definition-updates"></a><a name="bkmk_same-group"></a>Använd en befintlig program uppdaterings grupp för automatisk distribution för Endpoint Protection definitions uppdateringar  

När du använder en ADR för att distribuera Endpoint Protection definitions uppdateringar regelbundet, använder du alltid en befintlig program uppdaterings grupp. Annars skapar ADR flera hundratals program uppdaterings grupper över tid. Definitions uppdaterings utgivare anger vanligt vis att definitions uppdateringar ska upphöra att gälla när de ersätts av fyra senare uppdateringar. Därför innehåller program uppdaterings gruppen som skapas av ADR aldrig fler än fyra definitions uppdateringar för utgivaren: en aktiv och tre ersatta.  



## <a name="see-also"></a>Se även  
 [Planera programuppdateringar](plan-for-software-updates.md)
