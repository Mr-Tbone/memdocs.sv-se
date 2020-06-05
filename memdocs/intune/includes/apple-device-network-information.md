---
title: inkludera fil
description: inkludera fil
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/02/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: bc8bb79d4f950edc303fb12504ef1a4a8dda9a64
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347276"
---
## <a name="apple-device-network-information"></a>Nätverksinformation för Apple-enhet

|**Används för**|**Värdnamn (IP-adress/undernät)**|**Protokoll**|**Port**|
|------------|-----------|------------|-----------|
|Hämta och visa innehåll från Apple-servrar|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br>\*.phobos.itunes-apple.com.akadns.net|HTTP|80|
|Kommunikation med APNS-servrar|#-courier.push.apple.com<br>”#” är ett slumpmässigt tal från 0 till 50.|TCP|5223 och 443|
|Olika funktioner, bland annat åtkomst till Internet, iTunes-butiken, macOS App Store, iCloud, meddelanden etc.|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 eller 443|

Mer information finns i:

- [TCP- och UDP-portar som används av Apples programvaruprodukter](https://support.apple.com/HT202944)
- [Om macOS-, iOS/iPadOS-och iTunes-serverns värdanslutningar och bakgrundsprocesser i iTunes](https://support.apple.com/HT201999)
- [Om dina macOS- och iOS/iPadOS-klienter inte får push-meddelanden från Apple](https://support.apple.com/HT203609)