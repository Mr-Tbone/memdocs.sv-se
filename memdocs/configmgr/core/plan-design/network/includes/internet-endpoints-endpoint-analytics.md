---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: c576a4466ce8685cb440d8c804c9a675fbbecb8b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126483"
---
### <a name="endpoints-required-for-configuration-manager-managed-devices"></a>Slut punkter som krävs för Configuration Manager hanterade enheter

Configuration Manager-hanterade enheter skickar data till Intune via anslutningen i Configuration Manager-rollen och de behöver inte direkt åtkomst till det offentliga Microsoft-molnet.

| Slutpunkt  | Funktion  |
|-----------|-----------|
| `https://graph.windows.net` | Används för att automatiskt hämta inställningar när du kopplar din hierarki till Endpoint Analytics på Configuration Manager Server roll. Mer information finns i [Konfigurera proxyservern för en plats system Server](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Används för att synkronisera enhets samling och enheter med slut punkts analys på Configuration Manager Server roll. Mer information finns i [Konfigurera proxyservern för en plats system Server](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### <a name="endpoints-required-for-intune-managed-devices"></a>Slut punkter som krävs för Intune-hanterade enheter

För att registrera enheter till slut punkts analys måste de skicka nödvändiga funktions data till Microsofts offentliga moln. Slut punkts analys använder Windows 10-och Windows Server-anslutna användar upplevelser och telemetri-komponenten (DiagTrack) för att samla in data från Intune-hanterade enheter. Kontrol lera att tjänsten för **anslutna användar upplevelser och telemetri** på enheten körs.

| Slutpunkt  | Funktion  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Används av Intune-hanterade enheter för att skicka [nödvändiga funktions data](../../../../../analytics/data-collection.md#bkmk_datacollection) till data insamlings slut punkten för Intune. |
