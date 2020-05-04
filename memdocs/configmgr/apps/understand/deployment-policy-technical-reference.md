---
title: Teknisk referens för program distributions princip
titleSuffix: Configuration Manager
description: Felsöka program distributions principer teknisk referens för Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51d260ede4ed275c401c3b9f9e131134c62ae74e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709791"
---
# <a name="application-deployment-policy"></a>Princip för program distribution

*Gäller för: Configuration Manager (aktuell gren)*

## <a name="policy-creation"></a>Skapa princip

När du distribuerar ett program skapas en instans av [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md) klass som representerar tilldelningen av ett program till en samling. Den här aktiviteten kan spåras i **SMSProv. log**.

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

I Configuration Manager-databasen lagras den här informationen i `CI_CIAssignments` tabellen där `AssignmentType` 2 representerar en program distribution. När tilldelningen skapas identifierar SMS Database Monitor-komponenten en ändring i tabellen och meddelar sedan objekt Replikeringshanteraren att bearbeta CIA-principen (CI Assignment). Object Replication Manager-komponenten skapar sedan principen för program tilldelningen i databasen, som lagras i `Policy` tabellen i databasen och princip-ID: t baseras på programmets unika ID. Den här aktiviteten kan spåras i **objreplmgr. log** genom att referera till unikt tilldelnings-ID, som kan hämtas från SQL-frågan som refereras i avsnittet [innan du börjar](app-deployment-technical-reference.md#before-you-begin) .

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

Principen för program tilldelningen kan visas i databasen med hjälp av en SQL-fråga som liknar nedan.

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>Princip mål

När principen har skapats tilldelar komponenten policy Provider den här principen till resurserna i den samling som är mål för program distributionen. Principens mål information lagras i `ResPolicyMap` tabellen i-databasen. Du kan använda PADBID som returnerades av ovanstående fråga för att spåra aktiviteten i **policypv. log**. PADBID som registrerats i loggen kanske dock inte alltid matchar PADBID som returneras av ovanstående fråga om flera principer bearbetas samtidigt.

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> `ResPolicyMap`tabellen innehåller ingen mål information för program som distribueras som **tillgängliga** för användar samlingar. Software Center frågar en lista över dessa program från hanterings platsen och princip mål information för dessa program genereras dynamiskt när en användare begär ett program från Software Center.

## <a name="next-steps"></a>Nästa steg

- [Program distribution till enhets samlingar](device-deployment-technical-reference.md)
- [Program distribution till användar samlingar](user-deployment-technical-reference.md)
