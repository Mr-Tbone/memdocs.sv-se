---
author: aczechowski
ms.author: aaroncz
ms.reviewer: acabello
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 431c88b07889f7c80d2723425aaef2245c7f06bc
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268799"
---
Använd följande definitioner för att skilja mellan pilot och produktion:  

- **Pilot**: en delmängd av dina enheter som du vill verifiera innan du distribuerar till en större uppsättning. Använd Skriv bords analys för att markera enheter som unika för pilot uppsättningen. Enheter i piloten är klara att uppgraderas när inga till gångar blockeras. En blockerande till gång är markerad som *kritisk* och *kan inte* uppgraderas.  

- **Produktion**: alla andra enheter som har registrerats till Skriv bords analys som inte finns i piloten. Produktions enheter är redo att uppgraderas när alla till gångar är signerade. Skriv bords analys signerar automatiskt eventuella icke-kritiska till gångar.  
