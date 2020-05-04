---
title: Felsöka teknisk referens för program distribution
titleSuffix: Configuration Manager
description: Teknisk referens för fel sökning av program distribution i Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b3513131b73ac2b63cf18f31b1e39e15ee97420
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709819"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>Teknisk referens för program distribution i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln får du lära dig hur program distributioner fungerar.

## <a name="before-you-begin"></a>Innan du börjar

När du felsöker program distributioner finns det flera objekt som kan vara användbara när du ska granska klient loggar. Följande objekt är:

- Programmets CI-ID
- Unikt ID för program
- Unikt ID för distributions typ
- Unikt ID för program distribution (även kallat unikt tilldelnings-ID)
- Syfte för program distribution
- Unikt innehålls-ID
- Samlings-ID och namn
- Samlings typ

För att förenkla fel sökningen kan du köra en SQL-fråga som liknar den Configuration Manager databasen för att hämta den information som anges ovan.

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> När du kör den här frågan **måste** du använda det program namn som anges på fliken Allmän information i program egenskaper, i stället för att använda det lokaliserade program namnet som anges på fliken Software Center i program egenskaper.

## <a name="next-steps"></a>Nästa steg

- [Princip för program distribution](deployment-policy-technical-reference.md)
