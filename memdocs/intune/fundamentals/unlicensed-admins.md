---
title: Olicensierade administratörer i Microsoft Intune
description: Lär dig hur du ger olicensierade administratörer behörighet för åtkomst till Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: c6dcd41377234bbb1b40e513f16c3393d763b17f
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088198"
---
# <a name="unlicensed-admins"></a>Administratörer utan licens

Du kan bevilja åtkomst till administrationscentret för Intune/Microsoft Endpoint Manager till administratörer utan Intune-licens.

1. Logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Innehavaradministration** > **Roller** > **Administratörslicensiering**.
2. Välj **Tillåt åtkomst för administratörer utan licens** > **Ja**.
    >[!WARNING]
    >Du kan inte ångra den här inställningen när du har klickat på **Ja**.

3. Från och med nu behöver inte användare som loggar in i administrationscentret för Microsoft Endpoint Manager någon Intune-licens. Deras åtkomst definieras av de roller som tilldelats dem.

Intune har stöd för upp till 350 olicensierade administratörer per säkerhetsgrupp och gäller bara för direktmedlemmar. Administratörer över den här gränsen kan uppleva oförutsägbara beteenden.




