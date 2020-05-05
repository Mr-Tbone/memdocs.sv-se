---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 1b4fb4fb087639d1b3c3075339ce890a9c1dbbca
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723651"
---
Använd följande definitioner för att skilja mellan pilot och produktion:  

- **Pilot**: en delmängd av dina enheter som du vill verifiera innan du distribuerar till en större uppsättning. Använd Skriv bords analys för att markera enheter som unika för pilot uppsättningen. Enheter i piloten är klara att uppgraderas när inga till gångar blockeras. En blockerande till gång är markerad som *kritisk* och *kan inte* uppgraderas.  

- **Produktion**: alla andra enheter som har registrerats till Skriv bords analys som inte finns i piloten. Produktions enheter är redo att uppgraderas när alla till gångar är signerade. Skriv bords analys signerar automatiskt eventuella icke-kritiska till gångar.  

