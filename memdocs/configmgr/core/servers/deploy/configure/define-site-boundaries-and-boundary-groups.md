---
title: Använda gränser och gräns grupper
titleSuffix: Configuration Manager
description: Använd gränser och gräns grupper för att definiera nätverks platser och tillgängliga plats system för enheter som du hanterar.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 385dc1b2f542c964b52515e755a9202ee951bc5c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126383"
---
# <a name="define-site-boundaries-and-boundary-groups"></a>Definiera plats gränser och gräns grupper

*Gäller för: Configuration Manager (aktuell gren)*

*Gränser* i Configuration Manager definiera nätverks platser på intranätet. Dessa platser innehåller enheter som du vill hantera. *Gräns grupper* är logiska grupper av gränser som du konfigurerar.

En hierarki kan innehålla valfritt antal gränser grupper. Varje avgränsnings grupp kan innehålla valfri kombination av följande typer av gränser:  

- IP-undernät  
- Active Directory-platsnamn  
- IPv6-prefix  
- IP-adressintervall  
- VPN (från och med version 2006)

Klienter i intranätet utvärderar sin aktuella nätverksplats och använder sedan informationen för att identifiera gränsgrupper som de tillhör.  

Klienter använder gränsgrupper för att:  

- **Hitta en tilldelad plats:** Med gränser grupper kan klienter hitta en primär plats för klient tilldelning. Det här beteendet kallas även för *automatisk platstilldelning*.  

- **Hitta vissa plats system roller som de kan använda:** Koppla en avgränsnings grupp till vissa plats system roller. Platsen tillhandahåller sedan klienter med den listan över plats system i gränser gruppen. Klienterna använder dessa plats system för åtgärder som att söka efter innehåll eller en närliggande hanterings plats.  

Klienter som är på Internet eller konfigurerade som endast Internet klienter använder inte information om gränser. De här klienterna kan inte använda automatisk platstilldelning. De kan ladda ned innehåll från en Internetbaserad distributions plats från sin tilldelade plats eller en molnbaserad distributions plats.  

Från och med version 1902 kan du associera en Cloud Management Gateway (CMG) med en avgränsnings grupp. Mer information finns i [CMG Hierarchy design](../../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design).<!--3640932-->


## <a name="recommendations"></a><a name="BKMK_BoundaryBestPractices"></a>Rekommenderade

### <a name="use-a-mix-of-the-fewest-boundaries-that-meet-your-needs"></a>Använd en blandning av de minsta gränser som motsvarar dina behov

Använd den gräns typ eller typ som du väljer som fungerar för din miljö. För att förenkla dina hanterings uppgifter använder du gräns typer som låter dig använda det minsta antalet gränser som du kan använda.

### <a name="avoid-overlapping-boundaries-for-automatic-site-assignment"></a>Undvik överlappande gränser för automatisk platstilldelning

Även om varje gräns grupp stöder både platstilldelning och plats system referens, skapar du en separat uppsättning gräns grupper som endast ska användas för platstilldelning. Se till att varje avgränsning i en avgränsnings grupp inte är medlem i en annan avgränsnings grupp med en annan platstilldelning.

- En enda gränser kan inkluderas i flera gränser grupper  

- Varje gränsgrupp kan associeras med en annan primär plats för platstilldelning  

- För en gränser som är medlem i två olika avgränsnings grupper med olika platstilldelning väljer klienter slumpmässigt en plats att ansluta till. Detta är kanske inte för den plats som du vill att klienten ska ansluta till. Den här konfigurationen kallas för *överlappande gränser*.  

    Överlappande gränser är inte ett problem för innehålls platsen. Det kan vara en användbar konfiguration som ger klienter ytterligare resurser eller innehålls platser som de kan använda.  


## <a name="next-steps"></a>Nästa steg

- [Definiera nätverks platser som gränser](boundaries.md)

- [Konfigurera gränser grupper](boundary-groups.md)
