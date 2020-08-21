---
title: Säkerhet och sekretess för migrering
titleSuffix: Configuration Manager
description: Få rekommenderade säkerhets metoder och sekretess information för migrering till din Configuration Manager aktuella gren miljö.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f219c6c6d4c9a5cbf04b1295c99184f345e68b83
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692867"
---
# <a name="security-and-privacy-for-migration-to-configuration-manager-current-branch"></a>Säkerhet och sekretess för migrering till Configuration Manager aktuella grenen

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller rekommenderade säkerhets metoder och sekretess information för migrering till din Configuration Manager aktuella gren miljö.  

## <a name="security-best-practices-for-migration"></a>Rekommenderade säkerhets metoder för migrering  
 Använd följande rekommenderade säkerhets metoder för migrering.  

|Regelverk för säkerhet|Mer information|  
|----------------------------|----------------------|  
|Använd dator kontot för käll platsens SMS-provider-konto och käll platsens SQL Server konto i stället för ett användar konto.|Om du måste använda ett användar konto för migrering tar du bort konto informationen när migreringen är klar.|  
|Använd IPsec när du migrerar innehåll från en distributions plats på en käll plats till en distributions plats på mål platsen.|Även om det migrerade innehållet hash-kodas för att identifiera manipulering, kommer migreringen att Miss förväntas om data ändras när den överförs.|  
|Begränsa och övervaka de administrativa användare som kan skapa migreringsjobb.|Integriteten för databasen i målhierarkin beror på integriteten hos de data som den administrativa användaren väljer att importera från källhierarkin. Dessutom kan den här administrativa användaren läsa alla data från källhierarkin.|  

### <a name="security-issues-for-migration"></a>Säkerhets problem för migrering  
Migreringen har följande säkerhets problem:  

-   Klienter som blockeras från en käll plats kan tilldelas till målhierarkin innan deras klient post migreras.  

     Även om Configuration Manager behåller statusen blockerad för klienter som du migrerar, kan klienten tilldela till målhierarkin om tilldelningen sker innan migreringen av klient posten har slutförts.  

-   Gransknings meddelanden migreras inte.  

När du migrerar data från en käll plats till en målplats förlorar du all gransknings information från källhierarkin.  

## <a name="privacy-information-for-migration"></a>Sekretess information för migrering  
 Vid migrering identifieras information från de plats databaser som du identifierar i en käll infrastruktur och lagrar dessa data till databasen i målhierarkin. Den information som Configuration Manager kan upptäcka från en käll plats eller hierarki beror på vilka funktioner som har Aktiver ATS i käll miljön samt de hanterings åtgärder som utfördes i käll miljön.  

 Mer information om säkerhets-och sekretess information finns i något av följande avsnitt:  

-   Mer information om sekretess information för Configuration Manager 2007 finns i [säkerhet och sekretess för Configuration Manager 2007](/previous-versions/system-center/configuration-manager-2007/bb680768(v=technet.10)) i dokumentations biblioteket för Configuration Manager 2007.  

-   Mer information om sekretess information för System Center 2012 Configuration Manager finns i  [säkerhet och sekretess för system center 2012 Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg682033(v=technet.10)) i dokumentations biblioteket för system center 2012 Configuration Manager.  

-   Mer information om sekretess information för Configuration Manager finns i [säkerhet och sekretess för Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

Du kan migrera vissa eller alla data som stöds från en käll plats till en målhierarkin.  

Migrering är inte aktiverat som standard och kräver flera konfigurations steg. Information om migrering skickas inte till Microsoft.  

Innan du migrerar data från en-källhierarki bör du tänka igenom dina sekretess krav.