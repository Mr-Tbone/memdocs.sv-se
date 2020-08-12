---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: ca735cde1da5d563b9a7772fdaa55834e307312e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125972"
---
### <a name="server-connectivity-endpoints"></a>Slut punkter för Server anslutning

Tjänst anslutnings punkten måste kommunicera med följande slut punkter:

| Slutpunkt  | Funktion  |
|-----------|-----------|
| `https://aka.ms` | Används för att hitta tjänsten |
| `https://graph.windows.net` | Används för att automatiskt hämta inställningar som CommercialId när du kopplar din hierarki till Desktop Analytics (på Configuration Manager Server roll). Mer information finns i [Konfigurera proxyservern för en plats system Server](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Används för att synkronisera medlemskap i enhets samlingar, distributions planer och status för enhets beredskap med Desktop Analytics (endast på Configuration Manager Server roll). Mer information finns i [Konfigurera proxyservern för en plats system Server](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://dc.services.visualstudio.com` | För diagnostikdata från lokal tjänst anslutning för att få insikter om hälso tillståndet för moln anslutna tjänster.<!--7541816--> |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>Slut punkter för användar upplevelse och diagnostisk komponent

Klient enheter måste kommunicera med följande slut punkter:

| Slutpunkt  | Funktion  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Slut punkt för anslutna användar upplevelser och diagnostisk komponent. Används av enheter som kör Windows 10, version 1809 eller senare, eller version 1803 med den kumulativa uppdateringen för 2018-09 eller senare installerad. |
| `https://v10.events.data.microsoft.com` | Slut punkt för anslutna användar upplevelser och diagnostisk komponent. Används av enheter som kör Windows 10, version 1803 _utan_ den kumulativa uppdateringen av 2018-09. |
| `https://v10.vortex-win.data.microsoft.com` | Slut punkt för anslutna användar upplevelser och diagnostisk komponent. Används av enheter som kör Windows 10, version 1709 eller tidigare. |
| `https://vortex-win.data.microsoft.com` | Slut punkt för anslutna användar upplevelser och diagnostisk komponent. Används av enheter som kör Windows 7 och Windows 8,1 |

### <a name="client-connectivity-endpoints"></a>Klient anslutnings slut punkter

Klient enheter måste kommunicera med följande slut punkter:

| Index | Slutpunkt  | Funktion  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | Aktiverar kompatibilitetsrapporten för att skicka data till Microsoft. |
| 2 | `http://adl.windows.com` | Tillåter att kompatibilitetsrapporten tar emot de senaste kompatibilitetsinställningarna från Microsoft. |
| 3 | `https://watson.telemetry.microsoft.com` | [Windows Felrapportering (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Krävs för att övervaka distributions hälsan i Windows 10, version 1803 eller tidigare. |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Windows Felrapportering (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Krävs för enhetens hälso rapporter i Windows 10, version 1809 eller senare. |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Windows Felrapportering (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Krävs för att övervaka distributions hälsan i Windows 10, version 1809 eller senare. |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Windows Felrapportering (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Krävs för att övervaka distributions hälsan i Windows 10, version 1809 eller senare. |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Windows Felrapportering (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Krävs för att övervaka distributions hälsan i Windows 10, version 1809 eller senare. |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Windows Felrapportering (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Krävs för att övervaka distributions hälsan i Windows 10, version 1809 eller senare. |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Windows Felrapportering (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Krävs för att övervaka distributions hälsan i Windows 10, version 1809 eller senare. |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Windows Felrapportering (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Krävs för att övervaka distributions hälsan i Windows 10, version 1809 eller senare. |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [Online Crash Analysis (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Krävs för enhetens hälso rapporter i Windows 10, version 1809 eller senare. |
| 12 | `https://oca.telemetry.microsoft.com`  | [Online Crash Analysis (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Krävs för att övervaka distributions hälsan i Windows 10, version 1803 eller tidigare. |
| 13 | `https://login.live.com` | Krävs för att ge en mer tillförlitlig enhets identitet för Skriv bords analys. <br> <br>Om du vill inaktivera slut användar Microsoft-konto åtkomst använder du princip inställningar i stället för att blockera slut punkten. Mer information finns i [Microsoft-konto i företaget](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| 14 | `https://v20.events.data.microsoft.com` | Slut punkt för anslutna användar upplevelser och diagnostisk komponent. |
