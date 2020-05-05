---
title: Hierarkier för migrering
titleSuffix: Configuration Manager
description: Konfigurera en källhierarki och käll platser så att du kan migrera data till din Configuration Manager aktuella gren miljö.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c2e8e2ba57867b3c2a0929cfd670629296fdb9c9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718926"
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-configuration-manager-current-branch"></a>Konfigurera käll-hierarkier och käll platser för migrering till Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Om du vill aktivera migrering av data till din Configuration Manager aktuella gren miljö måste du konfigurera en Configuration Manager-källhierarki och en eller flera käll platser i hierarkin som innehåller data som du vill migrera.  

> [!NOTE]  
>  Åtgärder för migrering körs på platsen på den översta nivån i målhierarkin. Om du konfigurerar migreringen när du använder en Configuration Manager-konsol som är ansluten till en primär underordnad plats måste du tillåta att konfigurationen replikeras till den centrala administrations platsen, starta och sedan replikera status tillbaka till den primära plats som du är ansluten till.  

 Använd informationen och procedurerna i följande avsnitt för att ange källhierarkin och lägga till ytterligare käll platser. När du har slutfört de här procedurerna kan du skapa migreringsjobb och börja migrera data från källhierarkin till målhierarkin.  

-   [Ange en källhierarki för migrering](#BKBM_ConfigSrcHierarchy)  

-   [Identifiera ytterligare käll platser i källhierarkin](#BKBM_ConfigSrcSites)  

##  <a name="specify-a-source-hierarchy-for-migration"></a><a name="BKBM_ConfigSrcHierarchy"></a>Ange en källhierarki för migrering  
 För att migrera data till målhierarkin måste du ange en källhierarki som har de data som du vill migrera. Som standard blir platsen på den högsta nivån i hierarkin en käll plats för källhierarkin. Om du migrerar från en Configuration Manager 2007-hierarki kan du konfigurera ytterligare käll platser för migrering när data har samlats in från den första käll platsen. Om du migrerar från ett System Center 2012 Configuration Manager eller Configuration Manager aktuell Branch-hierarki behöver du inte konfigurera ytterligare käll platser för att migrera data från källhierarkin. Detta beror på att dessa versioner av Configuration Manager använder en delad databas som är tillgänglig på platsen på den översta nivån i källhierarkin. Den delade databasen innehåller all information som du kan migrera.  

 Använd följande procedurer för att ange en källhierarki för migrering och för att identifiera ytterligare käll platser i en Configuration Manager 2007-hierarki.  

 Kör den här proceduren med en Configuration Manager-konsol som är ansluten till målhierarkin:  

### <a name="to-configure-a-source-hierarchy"></a>Konfigurera en källhierarki   

1. Klicka på **Administration**i Configuration Manager-konsolen.  

2. I arbetsytan **Administration** expanderar du **Migrering**och klickar sedan på **Källhierarki**.  

3. Klicka på **Ange**källhierarki i gruppen **migrering** på fliken **Start** .  

4. I dialog rutan **Ange källhierarki** väljer du **ny källhierarki**för **källhierarkin**.  

5. Ange namn eller IP-adress för toppnivå platsen i en källhierarki som stöds för **Configuration Manager plats Server på översta nivån**.  

6. Ange åtkomst konton för käll plats som har följande behörigheter:  

   - Käll plats konto: behörigheten **läsa** till SMS-providern för den angivna platsen på den översta nivån i källhierarkin. Delning och uppgraderingar av distributions platser kräver behörighet att **ändra** och **ta bort** till webbplatsen i källhierarkin.

   - Konto för käll plats databas: **Läs** -och **kör** behörighet till SQL Server databasen för den angivna platsen på den översta nivån i källhierarkin.  

     Om du anger användning av dator kontot använder Configuration Manager dator kontot för toppnivå platsen i målhierarkin. För det här alternativet ser du till att det här kontot är medlem i säkerhets gruppen **distribuerade COM-användare** i den domän där platsen på den översta nivån i källhierarkin finns.  

7. Om du vill dela distributions platser mellan käll-och målhierarkin markerar du kryss rutan **Aktivera delning av distributions platser för käll plats servern** . Om du inte aktiverar delning av distributions platser just nu kan du göra det genom att redigera käll platsens autentiseringsuppgifter när data insamlingen är klar.  

8. Spara ändringarna genom att klicka på **OK**. Dialog rutan **data insamlings status** öppnas och data insamlingen startar automatiskt.  

9. När data insamlingen är klar klickar du på **Stäng** för att stänga dialog rutan **data insamlings status** och Slutför konfigurationen.  

##  <a name="identify-additional-source-sites-of-the-source-hierarchy"></a><a name="BKBM_ConfigSrcSites"></a>Identifiera ytterligare käll platser i källhierarkin  
 När du konfigurerar en källhierarki som stöds konfigureras den översta nivån i hierarkin automatiskt som en käll plats och data samlas in automatiskt från den platsen. Nästa åtgärd som du tar beror på vilken version av Configuration Manager som körs av källhierarkin:  

-   För en Configuration Manager 2007-källhierarki kan du starta migrering från den ursprungliga käll platsen eller konfigurera ytterligare käll platser från källhierarkin när data insamlingen har slutförts för den ursprungliga käll platsen. Om du vill migrera data som endast är tillgängliga från en underordnad plats konfigurerar du ytterligare käll platser för en Configuration Manager 2007-hierarki. Du kan till exempel konfigurera ytterligare käll platser för att samla in data om innehåll som du vill migrera när det skapas på en underordnad plats i källhierarkin och inte är tillgängligt på den översta platsen i källhierarkin.  

-   Du behöver inte konfigurera ytterligare käll platser för System Center 2012 Configuration Manager eller Configuration Manager aktuella grenens källhierarki. Detta beror på att dessa versioner av Configuration Manager använder en delad databas som är tillgänglig på platsen på den översta nivån i källhierarkin. Den delade databasen innehåller all information som du kan migrera från alla platser i källhierarkin. Detta gör de data som du kan migrera tillgängliga från platsen på den översta nivån i källhierarkin.  

När du konfigurerar ytterligare käll platser för en Configuration Manager 2007-källhierarki måste du konfigurera ytterligare käll platser längst upp i källhierarkin till längst ned. Du måste konfigurera en överordnad plats som en käll plats innan du konfigurerar någon av dess underordnade platser som käll platser.  

Använd följande procedur för att konfigurera ytterligare käll platser för Configuration Manager 2007-käll-hierarkier:  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Identifiera ytterligare käll platser i källhierarkin 

1.  Klicka på **Administration**i Configuration Manager-konsolen.  

2.  I arbetsytan **Administration** expanderar du **Migrering**och klickar sedan på **Källhierarki**.  

3.  Välj den plats som du vill konfigurera som käll plats.  

4.  Klicka på **Konfigurera** i gruppen **Källplats** på fliken **Start**.  

5.  I dialog rutan **käll platsens autentiseringsuppgifter** , för käll platsens åtkomst konton, anger du konton som har följande behörigheter:  

    -   Käll plats konto: behörigheten **läsa** till SMS-providern för den angivna platsen på den översta nivån i källhierarkin. Delning och uppgraderingar av distributions platser kräver behörighet att **ändra** och **ta bort** till webbplatsen i källhierarkin.  

    -   Konto för käll plats databas: **Läs** -och **kör** behörighet till SQL Server databasen för den angivna platsen på den översta nivån i källhierarkin.  

    Om du anger användning av dator kontot använder Configuration Manager dator kontot för toppnivå platsen i målhierarkin. För det här alternativet ser du till att det här kontot är medlem i säkerhets gruppen **distribuerade COM-användare** i den domän där platsen på den översta nivån i källhierarkin finns.  

6.  Om du vill dela distributions platser mellan käll-och målhierarkin markerar du kryss rutan **Aktivera delning av distributions platser för käll plats servern** . Om du inte aktiverar delning av distributions platser just nu kan du göra det genom att redigera autentiseringsuppgifterna för käll platsen när data insamlingen är klar.  

7. Spara ändringarna genom att klicka på **OK**. Dialog rutan **data insamlings status** öppnas och data insamlingen startar automatiskt.  

8.  När data insamlingen är klar klickar du på **Stäng** för att slutföra konfigurationen.  
