---
title: Hantera klienter på Internet
titleSuffix: Configuration Manager
description: Lär dig mer om att hantera klienter med Cloud Management Gateway och Internetbaserad klient hantering i Configuration Manager.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2840b30bee20d2fa73531b07c095e028979f6274
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715602"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Hantera klienter på Internet med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Normalt i Configuration Manager, är de flesta av de hanterade datorerna och servrarna fysiskt i samma interna nätverk som de plats system servrar som utför hanterings funktionerna. Du kan dock hantera klienter utanför det interna nätverket när de är anslutna till Internet. Den här funktionen kräver inte att klienter ansluter via VPN för att komma åt plats system servrarna.

Configuration Manager kan hantera Internet-anslutna klienter på två sätt:

- Gateway för molnhantering

- Internetbaserad klienthantering

> [!NOTE]
> Du kan ha en kombination av båda tjänsterna för en enda plats. Om en enhet hämtar princip från webbplatsen för både IBCM och CMG, slumpar den mellan dem för kommunikation. Den enda mekanism som är tillgänglig för att kontrol lera kommunikationen är klientautentisering. Om till exempel en Azure AD-ansluten klient inte litar på certifikatet för serverautentisering för den Internetbaserade hanterings platsen, kan det bara använda CMG. Om en domänansluten klient inte litar på certifikatet för serverautentisering för CMG, kan den endast använda den Internetbaserade hanterings platsen.<!-- SCCMDocs#1541 -->

## <a name="cloud-management-gateway"></a>Gateway för molnhantering

Cloud Management Gateway tillhandahåller hantering av Internetbaserade klienter. Den använder en kombination av en Microsoft Azure moln tjänst och en lokal plats system roll som kommunicerar med tjänsten. Internetbaserade klienter använder moln tjänsten för att kommunicera med den lokala Configuration Manager.

### <a name="cmg-advantages"></a>CMG-fördelar

- Ingen ytterligare investering för lokal infrastruktur krävs.  

- Visar inte lokal infrastruktur till Internet.  

- Virtuella datorer i molnet som kör tjänsten hanteras fullständigt av Azure och kräver inget underhåll.  

- Konfigurera och konfigurera enkelt i Configuration Manager-konsolen.  

### <a name="cmg-disadvantages"></a>CMG nack delar  

- Moln prenumerations kostnad.  

- Hanterings data som skickas via moln tjänsten.  

Mer information finns i [Planera för Cloud Management Gateway](cmg/plan-cloud-management-gateway.md).  

## <a name="internet-based-client-management"></a>Internetbaserad klienthantering

Den här metoden förlitar sig på Internet-riktade plats system servrar som klienterna kommunicerar direkt med i hanterings syfte. Det kräver att klienter och plats system servrar konfigureras för internetbaserad klient hantering (IBCM).

### <a name="ibcm-advantages"></a>IBCM-fördelar

- Inget beroende av moln tjänst.  

- Ingen ytterligare kostnad som är associerad med en moln prenumeration.  

- Fullständig kontroll över servrar och roller som tillhandahåller tjänsten.  

### <a name="ibcm-disadvantages"></a>IBCM NACK delar

- Kräv ytterligare investeringar i infrastrukturen.  

- Kostnader för overheadkostnader och drift för ytterligare infrastruktur.  

- Infrastrukturen måste exponeras för Internet.  

Mer information finns i [Planera för internetbaserad klient hantering](plan-internet-based-client-management.md).  
