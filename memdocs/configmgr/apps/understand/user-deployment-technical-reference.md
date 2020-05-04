---
title: Teknisk referens för app-distribution till användare
titleSuffix: Configuration Manager
description: Felsöka program distributioner till användares tekniska referens för Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: b8e9dbfe-a046-4e06-8dec-cf0bc41ba095
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b44aad1db96b4191b9c9537acea4e64b1d30fde6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710799"
---
# <a name="application-deployment-policy-for-users"></a>Program distributions princip för användare

*Gäller för: Configuration Manager (aktuell gren)*

När ett program distribueras till en användar samling skapas principen för distributionen endast för nödvändiga distributioner. För tillgängliga distributioner skapas principen när användaren försöker installera programmet från Software Center. Den här artikeln förklarar distributions processen för nödvändiga och tillgängliga distributioner.

> [!TIP]
> All information som behövs för att granska klient loggarna kan erhållas genom att köra SQL-frågan som refereras i avsnittet [innan du börjar](app-deployment-technical-reference.md#before-you-begin) .

## <a name="required-deployments"></a>Nödvändiga distributioner

Principen för en obligatorisk program distribution till en användar samling är riktad till alla användare i samlingen när distributionen skapas. Bearbetning på klient sidan för dessa distributioner liknar en nödvändig distribution till en enhets samling. Distributions aktivering sker vid den definierade tillgängliga tiden och tvång sker vid den definierade tids gränsen. Mer information finns i [program distribution till enhets samlingar](device-deployment-technical-reference.md).

## <a name="available-deployments"></a>Tillgängliga distributioner

Program som distribueras till en användar samling som tillgängliga fungerar annorlunda. Med den här förändringen kan administratören göra program tillgängliga för användarna utan att orsaka resurs konkurrens för principer. När en användare startar Software Center, frågas en lista över program som är tillgängliga för användaren från hanterings platsen i real tid. Den här begäran görs till den `CMUserService_WindowsAuth` virtuella katalogen på hanterings platsen och kan visas i **SCClient_ [username]. log** på klienten.

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

När hanterings platsen tar emot den här begäran frågar den listan över program som är tillgängliga för användaren genom att `usp_GetApplicationPropertyValuesFiltered` köra den lagrade proceduren. Den här aktiviteten kan spåras i **UserService. log** på hanterings platsen.

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

Software Center tar emot listan och visar de program som användaren kan installera. När användaren klickar på programmet, frågas ytterligare information om programmet från hanterings platsen, som inbegriper körning av lagrade procedurer som usp_GetApplicationInfo, usp_GetAppModelApplicationSupersedence, usp_GetDeploymentTypeForAnApp osv.

Distributionen aktive ras när användaren väljer programmet och klickar på knappen **Installera** , och ett DCM-Agent jobb skapas för att utvärdera programmet. Om programmet är tillämpligt skapas ett annat DCM Agent-jobb för att ladda ned och använda programmet. Den här aktiviteten kan spåras i **DCMAgent. log** på klienten.

## <a name="next-steps"></a>Nästa steg

- [Förstå klient komponenter för program distribution](client-components-technical-reference.md)
