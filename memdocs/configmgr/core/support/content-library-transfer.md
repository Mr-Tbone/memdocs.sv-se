---
title: Överförings verktyg för innehålls bibliotek
titleSuffix: Configuration Manager
description: Använd verktyget för överföring av innehålls bibliotek för att överföra innehåll från en disk enhet till en annan på en Configuration Manager distributions plats.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7401c80c89b1f1674bdae0b20482d7164837b724
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720088"
---
# <a name="content-library-transfer-tool"></a>Överförings verktyg för innehålls bibliotek

*Gäller för: Configuration Manager (aktuell gren)*

Verktyget för överföring av innehålls bibliotek är ett av de [Configuration Manager verktygen](tools.md). Den överför innehåll från en disk enhet till en annan. Verktyget är avsett att köras på distributions plats system. Den stöder distributions platser som samplaceras med en plats eller ett fjärrplatssystem.  

Verktyget är användbart för scenariot när disk enheten som är värd för innehålls biblioteket blir full. Lägg först till eller identifiera en annan hård disk med tillräckligt med utrymme som värd för innehålls biblioteket. Använd sedan **ContentLibraryTransfer. exe** för att överföra innehåll från den gamla fyllda hård disken till den nya, tomma enheten.
 
När överföringen är klar är innehållet tillgängligt för klient datorer från den nya platsen.



## <a name="usage"></a>Användning 

Kör **ContentLibraryTransfer. exe** som en användare med administratörs behörighet på distributions platsen. 

#### <a name="syntax"></a>Syntax 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Exempel
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Begränsningar

- Kör verktyget lokalt på distributions platsen. Du kan inte köra den från en fjärrdator.  

- Använd bara det när klienterna inte har åtkomst till distributions platsen. Om du kör verktyget när klienterna har åtkomst till innehåll kan innehålls biblioteket på mål enheten ha ofullständiga data. Data överföringen kan Miss förorsakat i ett oanvändbart innehålls bibliotek.  

- Distribuera inte innehåll till distributions platsen när du kör verktyget. Om du kör verktyget när innehållet skrivs till distributions platsen kan innehålls biblioteket på mål enheten ha ofullständiga data. Data överföringen kan Miss förorsakat i ett oanvändbart innehålls bibliotek.



## <a name="see-also"></a>Se även

- [Grundläggande begrepp för innehållshantering](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Innehållsbibliotek](../plan-design/hierarchy/the-content-library.md)
