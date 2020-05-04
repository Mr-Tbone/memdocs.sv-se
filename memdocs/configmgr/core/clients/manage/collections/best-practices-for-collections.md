---
title: Metod tips för samlingar
titleSuffix: Configuration Manager
description: Få metod tips för samlingar i Configuration Manager.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3e7b108ef48b218ee9d6a31064606b40a68fea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714292"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Metod tips för samlingar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Använd följande metod tips för samlingar i Configuration Manager.  

## <a name="dont-use-incremental-updates-with-many-collections"></a><a name="bkmk_incremental"></a>Använd inte stegvisa uppdateringar med många samlingar

Om du aktiverar alternativet **Använd inkrementella uppdateringar för samlingen** kan den här konfigurationen orsaka förseningar i utvärderingarna om du aktiverar det för många samlingar. Tröskelvärdet är runt 200 samlingar i hierarkin. Det exakta antalet beror på följande faktorer:  

- Totalt antal samlingar  

- Hur ofta nya resurser läggs till och ändras i hierarkin  

- Antalet klienter i hierarkin  

- Komplexiteten för reglerna för samlingsmedlemskap i hierarkin  

## <a name="maintenance-window-size-for-software-updates"></a>Underhålls fönster storlek för program uppdateringar

Du kan konfigurera underhålls fönster för enhets samlingar för att begränsa de tider som Configuration Manager kan installera program vara på dessa enheter. Om du konfigurerar underhålls perioden så att den är för liten, kanske inte klienten kan installera kritiska program uppdateringar, vilket gör att klienten är sårbar för angrepp som begränsas av program uppdateringen.

> [!Tip]
> Viktiga överväganden att tänka på när du planerar underhålls Fönstren:
>
> - Standard körnings tiden för program uppdatering är 60 minuter.
> - När Configuration Manager beräknar om en uppdatering kan installeras lägger den till fem minuter till den maximala kör tiden för en omstart.
> - Den återstående varaktigheten för ett underhålls fönster måste vara längre än den maximala kör tiden för program uppdateringen plus fem minuter.
