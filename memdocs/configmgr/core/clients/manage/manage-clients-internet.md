---
title: Hantera klienter på Internet
titleSuffix: Configuration Manager
description: Lär dig mer om att hantera klienter med Cloud Management Gateway och Internetbaserad klient hantering i Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c00d480b993498c5fa27e2a4d91a5f2a3bc130ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710631"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Hantera klienter på Internet med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Normalt i Configuration Manager, är de flesta av de hanterade datorerna och servrarna fysiskt i samma interna nätverk som de plats system servrar som utför hanterings funktionerna. Du kan dock hantera klienter utanför det interna nätverket när de är anslutna till Internet. Den här funktionen kräver inte att klienter ansluter via VPN för att komma åt plats system servrarna.

Configuration Manager kan hantera Internet-anslutna klienter på två sätt:

-   Gateway för molnhantering

-   Internetbaserad klienthantering


## <a name="cloud-management-gateway"></a>Gateway för molnhantering

Cloud Management Gateway tillhandahåller hantering av Internetbaserade klienter. Den använder en kombination av en Microsoft Azure moln tjänst och en ny plats system roll som kommunicerar med tjänsten. Internetbaserade klienter använder moln tjänsten för att kommunicera med den lokala Configuration Manager.

#### <a name="advantages"></a>Fördelar  

-   Ingen ytterligare investering för lokal infrastruktur krävs.  

-   Visar inte lokal infrastruktur till Internet.  

-   Virtuella datorer i molnet som kör tjänsten hanteras fullständigt av Azure och kräver inget underhåll.  

-   Konfigurera och konfigurera enkelt i Configuration Manager-konsolen.  

#### <a name="disadvantages"></a>Nackdelar  

-   Moln prenumerations kostnad.  

-   Hanterings data som skickas via moln tjänsten.  

Mer information finns i [Planera för Cloud Management Gateway](cmg/plan-cloud-management-gateway.md).  



## <a name="internet-based-client-management"></a>Internetbaserad klienthantering

Den här metoden förlitar sig på Internet-riktade plats system servrar som klienterna kommunicerar med i hanterings syfte. Det kräver att klienter och plats system servrar konfigureras för internetbaserad hantering.

#### <a name="advantages"></a>Fördelar  

-   Inget beroende av moln tjänst.  

-   Ingen ytterligare kostnad som är associerad med en moln prenumeration.  

-   Fullständig kontroll över servrar och roller som tillhandahåller tjänsten.  

#### <a name="disadvantages"></a>Nackdelar  

-   Kräv ytterligare investeringar i infrastrukturen.  

-   Kostnader för overheadkostnader och drift för ytterligare infrastruktur.  

-   Infrastrukturen måste exponeras för Internet.  

Mer information finns i [Planera för internetbaserad klient hantering](plan-internet-based-client-management.md).  
