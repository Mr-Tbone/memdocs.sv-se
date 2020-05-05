---
title: Felsöka BitLocker
titleSuffix: Configuration Manager
description: Lär dig hur du felsöker problem med BitLocker-hantering i Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ed8e464e0ab7c17e87e3de2bf72aa0dfb0acd071
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723924"
---
# <a name="troubleshoot-bitlocker"></a>Felsöka BitLocker

*Gäller för: Configuration Manager (aktuell gren)*

Använd informationen i den här artikeln för att felsöka problem med BitLocker-hanteringen i Configuration Manager.

## <a name="server-error-in-self-service"></a>Server fel i självbetjäning

När du försöker öppna självbetjänings portalen (`https://webserver.contoso.com/SelfService`) för första gången visas följande fel meddelande:

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

Åtgärda problemet genom att kontrol lera att du har installerat [förutsättningen](../../plan-design/bitlocker-management.md#prerequisites) för **Microsoft ASP.NET MVC 4,0** på webb servern.

## <a name="see-also"></a>Se även

Mer information om hur du använder BitLocker-händelseloggar finns i [händelse loggar i BitLocker](about-event-logs.md).

En lista över kända fel och möjliga orsaker till händelse logg poster finns i följande artiklar:

- [Klienthändelseloggar](client-event-logs.md)
- [Serverhändelseloggar](server-event-logs.md)

Information om varför klienter rapporterar att de inte är kompatibla med principen för BitLocker-hantering finns i [koder för inkompatibilitet](non-compliance-codes.md).
