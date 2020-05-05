---
title: Språkpaket
titleSuffix: Configuration Manager
description: Läs mer om språk stöd som är tillgängligt i Configuration Manager.
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ec5581567925ee57300274e50288058e06d80ec0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718191"
---
# <a name="language-packs-in-configuration-manager"></a>Språk paket i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln ger teknisk information om språk stöd i Configuration Manager. Configuration Manager plats servrar och klienter betraktas som neutrala språk. Lägg till stöd för visnings språk genom att installera **Server språk paket** eller **klient språk paket** på en central administrations plats och på primära platser. Du väljer de server-och klient språk som ska stödjas på en plats från de tillgängliga Language Pack-filerna under plats installationen.
 
Installera flera språk på varje plats. Du behöver bara installera de språk som du använder.  

- Varje plats har stöd för flera språk för Configuration Manager-konsoler.  

- Lägg till stöd för de klient språk som du vill stödja genom att installera enskilda klient språk paket på varje plats.  

När du installerar stöd för ett språk som matchar följande komponenter:  

- Visnings språket för en dator: både Configuration Manager-konsolen och klient användar gränssnittet som körs på datorn visar information på det språket.  

- Språk inställningen som används av webbläsaren på en dator: anslutningar till webbaserad information, inklusive Programkatalog eller SQL Server Reporting Services, visas på det språket.  


När du kör Configuration Manager installationen laddar den ned språk paket filer som en del av kraven och omdistribuerbara filer. Du kan också använda [installations hämtaren](setup-downloader.md) för att ladda ned filerna innan du kör installations programmet.   



## <a name="server-languages"></a>Server språk  

Använd följande tabell för att mappa ett språk-ID till ett språk som du vill stödja på servrar. Mer information om språkvariant-ID finns i [språkvariant-ID: n som tilldelats av Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609).  

|Serverspråk|Språkvariant-ID (LCID)|Kod med tre bokstäver|  
|---------------------|------------------------|-----------------------|  
|Engelska (standard)|0409|ENU|  
|Kinesiska (förenklad)|0804|CHS|  
|kinesiska (traditionell, Taiwan)|0404|CHT|  
|Tjeckiska|0405|CSY|  
|Nederländska – Nederländerna|0413|NLD|  
|Franska|040c|FRA|  
|Tyska|0407|DEU|  
|Ungerska|040e|HUN|  
|Italienska – Italien|0410|ITA|  
|Japanska|0411|JPN|  
|Koreansk|0412|KOR|  
|Polska|0415|PLK|  
|Portugisiska – Brasilien|0416|PTB|  
|Portugisiska – Portugal|0816|PTG|  
|Ryska|0419|RUS|  
|Spanska – Spanien|0c0a|ESN|  
|Svenska|041d|SVE|  
|Turkiska|041f|TRK|  



## <a name="client-languages"></a>Klient språk  

Använd följande tabell för att mappa ett språk-ID till ett språk som du vill stödja på klient datorer. Mer information om språkvariant-ID finns i [språkvariant-ID: n som tilldelats av Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609).  

|Klientspråk|Språkvariant-ID (LCID)|Kod med tre bokstäver|  
|---------------------|------------------------|-----------------------|  
|Engelska (standard)|0409|ENG|  
|Kinesiska – förenklad|0804|CHS|  
|kinesiska (traditionell, Taiwan)|0404|CHT|  
|Tjeckiska|0405|CSY|  
|Danska|0406|DAN|  
|Nederländska – Nederländerna|0413|NLD|  
|Finska|040b|FIN|  
|Franska|040c|FRA|  
|Tyska|0407|DEU|  
|Grekiska|0408|ELL|  
|Ungerska|040e|HUN|  
|Italienska – Italien|0410|ITA|  
|Japanska|0411|JPN|  
|Koreansk|0412|KOR|  
|Norska|0414|NOR|  
|Polska|0415|PLK|  
|Portugisiska (Brasilien)|0416|PTB|  
|Portugisiska (Portugal)|0816|PTG|  
|Ryska|0419|RUS|  
|Spanska – Spanien|0c0a|ESN|  
|Svenska|041d|SVE|  
|Turkiska|041f|TRK|  


### <a name="mobile-device-client-languages"></a>Klient språk för mobila enheter  
När du lägger till stöd för mobilen hets språk inkluderas alla klient språk som stöds av mobila enheter. Du kan inte välja enskilda språk paket för stöd för mobila enheter.  



## <a name="identify-installed-language-packs"></a>Identifiera installerade språk paket  
Om du vill identifiera de språk paket som är installerade på en dator som kör Configuration Manager-klienten, letar du efter språkvariant-ID (LCID) för de installerade språk paketen i datorns register. Den här informationen finns i följande register Sök väg:  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

Anpassa maskin varu inventeringen för att samla in den här informationen. Sedan skapar du en anpassad rapport för att Visa språk informationen. Mer information om hur du samlar in anpassad maskin varu inventering finns i [så här konfigurerar du maskin varu inventering](../../../clients/manage/inventory/configure-hardware-inventory.md). Mer information finns i [skapa rapporter](../../manage/operations-and-maintenance-for-reporting.md#create-reports).
