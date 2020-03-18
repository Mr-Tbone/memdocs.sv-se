---
title: Nätverksslutpunkter för Microsoft Intune
titleSuffix: ''
description: Granska slutpunkter för Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: b8d9aef2-8757-4e22-9b24-a0833d27304c
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e1a7c9665f142bf7dd7832e6bac0e016539ddea
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79358734"
---
# <a name="network-endpoints-for-microsoft-intune"></a>Nätverksslutpunkter för Microsoft Intune  

På den här sidan visas IP-adresser och portinställningar som krävs för proxyinställningarna i dina Intune-distributioner.

Då Intune är en molnbaserad tjänst krävs inte någon lokal infrastruktur, till exempel servrar eller gateways.

## <a name="access-for-managed-devices"></a>Åtkomst för hanterade enheter  

Om du vill hantera enheter bakom brandväggar och proxyservrar, måste du aktivera kommunikation för Intune.

- Proxyservern måste ha stöd för både **HTTP (80)** och **HTTPS (443)** eftersom Intune-klienter använder båda protokollen. Windows informationsskydd använder port 444.
- För vissa åtgärder (t.ex. nedladdning av programuppdateringar för den klassiska datoragenten) kräver Intune att det finns en oautentiserad åtkomst till proxyservern för att få åtkomst till manage.microsoft.com

Du kan ändra inställningarna för proxyservern på enskilda klientdatorer. Du kan också använda grupprincipinställningar till att ändra inställningarna för alla klientdatorer som finns bakom en angiven proxyserver.


<!--
> [!NOTE] If Windows 8.1 devices haven't cached proxy server credentials, enrollment might fail because the request doesn't prompt for credentials. Enrollment fails without warning as the request wait for a connection. If users might experience this issue, instruct them to open their browser settings and save proxy server settings to enable a connection.   -->

Hanterade enheter kräver konfigurationer som låter **Alla användare** komma åt tjänster genom brandväggar.

I följande tabeller visas de portar och tjänster som Intune-klienten har åtkomst till:

|Domains    |IP-adress      |
|-----------|----------------|
|login.microsoftonline.com <br> *.officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net| Läs mer i informationen om [webbadresser och IP-adressintervall för Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) |
|portal.manage.microsoft.com<br> m.manage.microsoft.com |52.175.12.209<br>20.188.107.228<br>52.138.193.149<br>51.144.161.187<br>52.160.70.20<br>52.168.54.64 <br>13.72.226.202<br>52.189.220.232|
| sts.manage.microsoft.com | 13.93.223.241 <br>52.170.32.182 <br>52.164.224.159 <br>52.174.178.4 <br>13.75.122.143 <br>52.163.120.84<br>13.73.112.122<br>52.237.192.112|
|manage.microsoft.com <br>i.manage.microsoft.com <br>r.manage.microsoft.com <br>a.manage.microsoft.com <br>p.manage.microsoft.com <br>enterpriseenrollment.manage.microsoft.com <br>EnterpriseEnrollment-s.manage.microsoft.com |40.83.123.72<br>13.76.177.110<br>52.169.9.87<br>52.174.26.23<br>104.40.82.191<br>13.82.96.212<br>52.147.8.239<br>40.115.69.185|
|portal.fei.msua01.manage.microsoft.com <br>m.fei.msua01.manage.microsoft.com<br>portal.fei.msua02.manage.microsoft.com<br>m.fei.msua02.manage.microsoft.com<br>portal.fei.msua04.manage.microsoft.com <br>m.fei.msua04.manage.microsoft.com<br>portal.fei.msua05.manage.microsoft.com <br>m.fei.msua05.manage.microsoft.com<br>portal.fei.amsua0502.manage.microsoft.com <br>m.fei.amsua0502.manage.microsoft.com<br>portal.fei.msua06.manage.microsoft.com <br>m.fei.msua06.manage.microsoft.com<br>portal.fei.amsua0602.manage.microsoft.com <br>m.fei.amsua0602.manage.microsoft.com<br>fei.amsua0202.manage.microsoft.com <br>portal.fei.amsua0202.manage.microsoft.com <br>m.fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0402.manage.microsoft.com <br>m.fei.amsua0402.manage.microsoft.com|52.160.70.20<br>52.168.54.64 |
|portal.fei.msub01.manage.microsoft.com <br>m.fei.msub01.manage.microsoft.com<br>portal.fei.amsub0102.manage.microsoft.com <br>m.fei.amsub0102.manage.microsoft.com<br>fei.msub02.manage.microsoft.com <br>portal.fei.msub02.manage.microsoft.com <br>m.fei.msub02.manage.microsoft.com<br>portal.fei.msub03.manage.microsoft.com <br>m.fei.msub03.manage.microsoft.com<br>portal.fei.msub05.manage.microsoft.com <br>m.fei.msub05.manage.microsoft.com<br>portal.fei.amsub0202.manage.microsoft.com <br>m.fei.amsub0202.manage.microsoft.com<br>portal.fei.amsub0302.manage.microsoft.com <br>m.fei.amsub0302.manage.microsoft.com<br>portal.fei.amsub0502.manage.microsoft.com<br>m.fei.amsub0502.manage.microsoft.com|52.138.193.149<br>51.144.161.187|
|portal.fei.msuc01.manage.microsoft.com <br>m.fei.msuc01.manage.microsoft.com<br>portal.fei.msuc02.manage.microsoft.com <br>m.fei.msuc02.manage.microsoft.com<br>portal.fei.msuc03.manage.microsoft.com <br>m.fei.msuc03.manage.microsoft.com<br>portal.fei.msuc05.manage.microsoft.com <br>m.fei.msuc05.manage.microsoft.com|52.175.12.209<br>20.188.107.228|
|portal.fei.amsud0101.manage.microsoft.com<br>m.fei.amsud0101.manage.microsoft.com|13.72.226.202|
|fef.msua01.manage.microsoft.com|138.91.243.97|
|fef.msua02.manage.microsoft.com|52.177.194.236|
|fef.msua04.manage.microsoft.com|23.96.112.28|
|fef.msua05.manage.microsoft.com|138.91.244.151|
|fef.msua06.manage.microsoft.com|13.78.185.97|
|fef.msua07.manage.microsoft.com|52.175.208.218|
|fef.msub01.manage.microsoft.com|137.135.128.214|
|fef.msub02.manage.microsoft.com|137.135.130.29|
|fef.msub03.manage.microsoft.com|52.169.82.238|
|fef.msub05.manage.microsoft.com|23.97.166.52|
|fef.msuc01.manage.microsoft.com|52.230.19.86|
|fef.msuc02.manage.microsoft.com|23.98.66.118|
|fef.msuc03.manage.microsoft.com|23.101.0.100|
|fef.msuc05.manage.microsoft.com|52.230.16.180|
|fef.amsua0202.manage.microsoft.com|52.165.165.17|
|fef.amsua0402.manage.microsoft.com|40.69.157.122|
|fef.amsua0502.manage.microsoft.com|13.85.68.142|
|fef.amsua0602.manage.microsoft.com|52.161.28.64|
|fef.amsub0102.manage.microsoft.com|40.118.98.207|
|fef.amsub0202.manage.microsoft.com|40.69.208.122|
|fef.amsub0302.manage.microsoft.com|13.74.145.65|
|enterpriseregistration.windows.net|52.175.211.189|
|fef.amsua0102.manage.microsoft.com|52.242.211.0|
|fef.amsua0702.manage.microsoft.com|52.232.225.75|
|fef.amsub0502.manage.microsoft.com|40.67.219.144|
|fef.msud01.manage.microsoft.com|20.40.178.139|
|Admin.manage.microsoft.com|52.224.221.227<br>52.161.162.117<br>52.178.44.195<br>52.138.206.56<br>52.230.21.208<br>13.75.125.10|
|wip.mam.manage.microsoft.com|52.187.76.84<br>13.76.5.121<br>52.165.160.237<br>40.86.82.163<br>52.233.168.142<br>168.63.101.57<br>52.187.196.98<br>52.237.196.51|
|mam.manage.microsoft.com|104.40.69.125<br>13.90.192.78<br>40.85.174.177<br>40.85.77.31<br>137.116.229.43<br>52.163.215.232<br>52.174.102.180<br>52.187.196.173<br>52.156.162.48|
|*.manage.microsoft.com|40.82.248.224/28<br>20.189.105.0/24<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>40.119.8.128/25<br>40.74.25.0/24<br>40.82.249.128/25<br>40.80.184.128/25<br>52.150.137.0/25|


## <a name="network-requirements-for-powershell-scripts-and-win32-apps"></a>Nätverkskrav för PowerShell-skript och Win32-appar  

Om du använder Intune för att distribuera PowerShell-skript eller Win32-appar måste du också bevilja åtkomst till slutpunkter som din klient för närvarande finns i.

|ASU | Lagringsnamn | CDN |
| --- | --- |--- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0701<br>AMSUA0702 | naprodimedatapri<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502 | euprodimedatapri<br>euprodimedatasec<br>euprodimedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUD0101| approdimedatapri<br>approdimedatasec<br>approdimedatahotifx | approdimedatapri.azureedge.net<br>approdimedatasec.azureedge.net<br>approdimedatahotfix.azureedge.net |

## <a name="windows-push-notification-services-wns"></a>Windows Push Notification Services (WNS)  

Kräv användning av Windows Push Notification Services (WNS) för Intune-hanterade Windows-enheter som hanteras med hjälp av hantering av mobilenheter (MDM), enhetsåtgärder och andra omedelbara aktiviteter. Mer information finns i [Allowing Windows Notification traffic through enterprise firewalls](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config) (Tillåta Windows-meddelandetrafik via företagets brandväggar).  

## <a name="delivery-optimization-port-requirements"></a>Portkrav för Leveransoptimering  

### <a name="port-requirements"></a>Portkrav  

För peer-till-peer-trafik använder Leveransoptimering 7680 för TCP/IP eller 3544 för NAT-överträdelse (Teredo fungerar också). För kommunikation mellan klient och tjänst används HTTP eller HTTPS via port 80/443.

### <a name="proxy-requirements"></a>Proxykrav  

Om du vill använda Leveransoptimering måste du tillåta byteintervallbegäran. Mer information finns i [Proxy requirements for Windows Update](https://docs.microsoft.com/windows/deployment/update/windows-update-troubleshooting) (Proxykrav för Windows Update).

### <a name="firewall-requirements"></a>Brandväggsförutsättningar  

Tillåt följande värdnamn via brandväggen för att stödja Leveransoptimering.
För kommunikation mellan klienter och molntjänsten Leveransoptimering:
- \*.do.dsp.mp.microsoft.com

För Leveransoptimering-metadata:
- \*.dl.delivery.mp.microsoft.com
- \*.emdl.ws.microsoft.com

## <a name="apple-device-network-information"></a>Nätverksinformation för Apple-enhet  

|Används för|Värdnamn (IP-adress/undernät)|Protokoll|Port|
|-----|--------|------|-------|
|Hämta och visa innehåll från Apple-servrar|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br> \*.phobos.itunes-apple.com.akadns.net |    HTTP    |      80      |
|Kommunikation med APNS-servrar|#-courier.push.apple.com<br>”#” är ett slumpmässigt tal från 0 till 50.|    TCP     |  5223 och 443  |
|Olika funktioner, bland annat åtkomst till Internet, iTunes-butiken, macOS App Store, iCloud, meddelanden osv. |phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net| HTTP/HTTPS |  80 eller 443   |

Mer information finns i Apples [TCP- och UDP-portar som används av Apples programprodukter](https://support.apple.com/HT202944), [Om macOS, iOS/iPadOS och iTunes serveranslutningar för värden och iTunes bakgrundsprocesser](https://support.apple.com/HT201999) och [Om dina macOS- och iOS/iPadOS-klienter inte kommer åt Apples push-meddelanden](https://support.apple.com/HT203609).  