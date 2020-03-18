---
title: Användarenhetsassociation – Intune-informationslager
titleSuffix: Microsoft Intune
description: Entiteten UserDeviceAssociation innehåller användarenhetsassociationer i din organisation.
keywords: Intune-informationslager
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 777484A7-09CE-4409-987F-76B3F87DFE93
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6127b365a04ad48a9cbaa98bdef821c4d1334181
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339897"
---
# <a name="reference-for-user-device-association-entity"></a>Referens för entiteten för användarenhetsassociationer

Entiteten **userDeviceAssociation** innehåller användarenhetsassociationer i din organisation.

## <a name="userdeviceassociations"></a>userDeviceAssociations


|        Name        |                                           Beskrivning                                            |        Exempel         |
|--------------------|--------------------------------------------------------------------------------------------------|------------------------|
|      userKey       |              Unikt id för användaren i informationslagret. (Surrogatnyckel).               |          123           |
|     deviceKey      |                      Unikt id för enheten i informationslagret.                      |          123           |
| createdDateTimeUTC |           Datum och tid när användarenhetsassociationen skapades. Använder UTC-formatet.           | 2016-11-23 12:00:00 |
|     isDeleted      | Anger att användaren har avregistrerat enheten och att associationen inte är aktuell längre. |       Sant/falskt       |
|  endedDateTimeUTC  |              Datum och tid i UTC när IsDeleted ändrades till <strong>True</strong>.               | 2017-06-23 12:00:00 |

## <a name="next-steps"></a>Nästa steg

- Mer information om [Intune-informationslagret](reports-nav-create-intune-reports.md).
