---
title: Nätverksinfrastruktur
titleSuffix: Configuration Manager
description: Konfigurera brand väggar, portar och domäner för att förbereda för Configuration Manager kommunikation.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 816b48f7dac3703c1d45fdbc0bf8ad7dc9528caa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719843"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Överväganden för nätverks infrastruktur för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

För att förbereda nätverket för att stödja Configuration Manager kan du behöva konfigurera vissa infrastruktur komponenter. Öppna exempelvis brand Väggs portar för att överföra kommunikationen som används av Configuration Manager.  

## <a name="ports-and-protocols"></a>Portar och protokoll

Olika Configuration Manager funktioner använder olika nätverks portar. Vissa portar krävs och en del som du kan anpassa.

De flesta Configuration Manager-kommunikation använder vanliga portar som port 80 för HTTP eller 443 för HTTPS. Vissa plats system roller har stöd för användning av anpassade webbplatser och anpassade portar. Mer information finns i [webbplatser för plats system servrar](websites-for-site-system-servers.md).

Innan du distribuerar Configuration Manager ska du identifiera de portar som du planerar att använda och konfigurera brand väggar efter behov.

När du har installerat Configuration Manager behöver du inte glömma att uppdatera brand väggar på enheter och nätverket om du behöver ändra en port. Ändra också portens konfiguration i Configuration Manager.

Mer information finns i följande artiklar:

- [Konfigurera klientkommunikationsportar](../../clients/deploy/configure-client-communication-ports.md)
- [Portar som används i Configuration Manager](../hierarchy/ports.md)


## <a name="internet-access-requirements"></a>Krav för Internet-åtkomst

Vissa Configuration Manager funktioner är beroende av Internet anslutning för fullständig funktionalitet. Om din organisation begränsar nätverkskommunikation med Internet med en brand vägg eller proxyserver, så se till att tillåta nödvändiga slut punkter.

Mer information finns i [krav för Internet åtkomst](internet-endpoints.md)


## <a name="proxy-servers"></a>Proxyservrar

Du kan ange separata proxyservrar för olika plats system servrar och klienter. Du gör dessa konfigurationer när du installerar en plats system roll eller-klient, eller ändra dem senare efter behov.

Mer information finns i [stöd för proxy server](proxy-server-support.md).
