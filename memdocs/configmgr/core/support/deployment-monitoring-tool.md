---
title: Distributionsövervakningsverktyget
titleSuffix: Configuration Manager
description: Använd verktyget för distributions övervakning för att felsöka program distributioner på en Configuration Manager-klient.
ms.date: 09/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a27e96cf69ab01b58910ae02fc732940eda8a04
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723378"
---
# <a name="deployment-monitoring-tool"></a>Distributionsövervakningsverktyget

*Gäller för: Configuration Manager (aktuell gren)*

Verktyget för distributions övervakning är ett av de [Configuration Manager verktygen](tools.md). Det är ett grafiskt användar gränssnitt som är utformat för att hjälpa till med fel sökning av program, program uppdateringar och konfigurations bas linje distributioner på en Configuration Manager-klient. Verktyget är skrivskyddat eftersom det inte ändrar någon status på klienten. Du kan använda den på ett säkert sätt för att diagnosticera vanliga distributions scenarier.


## <a name="features"></a>Funktioner

- Kör den som administratör för att felsöka distributioner på en lokal klient.  

- Felsöka distributioner på en fjärran sluten klient. Starta verktyget och Anslut till en fjärrdator som administratör.  

- Exportera till XML alla data som samlas in i verktyget. Dela XML-filen med andra och Använd den som en gemensam plattform för att prata om fel söknings distributioner.  

- Importera tidigare exporterade data till en annan dator och Använd den för att köra verktyget i offline-läge.   


## <a name="usage"></a>Användning

Verktyget för distributions övervakning stöder endast grafiskt användar gränssnitt. Starta verktyget genom att köra **DeploymentMonitoringTool. exe** som administratör. Det finns tre vyer:  

- **Klient egenskaper**: en lista över användbara attribut för enheten och Configuration Manager klienten. Den här vyn är standard.   

- **Distributioner**: Visa alla aktuella riktade distributioner. Välj en distribution i resultat fönstret om du vill visa mer information i informations fönstret.  

- **Alla uppdateringar**: Visa alla program uppdateringar och deras status.  

Om du vill kopiera data i valfri vy markerar du en cell och trycker på **CTRL** + **C**.


### <a name="actions-menu"></a>Åtgärder-menyn

Följande åtgärder är tillgängliga på menyn **åtgärder** :  

- **Anslut till fjärrdator**: Välj en dator att ansluta till. Om du inte anger ett användar namn och lösen ord, används de aktuella autentiseringsuppgifterna. Klicka på **Spara** för att ansluta till fjärrdatorn.  

- **Exportera data**: Välj den fil som du vill skriva data till och klicka på **Spara**. Använd den exporterade XML-filen för fjärrfelsökning på en annan dator.  

- **Importera data**: Välj en fil att importera till verktyget.  

- **Visa logg**: öppnar en associerad loggfil, beroende på vyn:  
    - Klient Egenskaper:`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Distributioner`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Alla uppdateringar:`C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>Se även

- [Distribuera program](../../apps/deploy-use/deploy-applications.md)
- [Distribuera programuppdateringar](../../sum/deploy-use/deploy-software-updates.md)
- [Distribuera konfigurationsbaslinjer](../../compliance/deploy-use/deploy-configuration-baselines.md)
