---
title: Registrera dig eller logga in i Microsoft Intune
description: Så här registrerar du dig för en Microsoft Intune-prenumeration, eller loggar in för att starta din prenumeration.
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
ms.openlocfilehash: ae30e03a03b4d690bdaa9e6a4c73da6ab15226f7
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095815"
---
# <a name="unlicensed-admins"></a>Administratörer utan licens

Du kan bevilja åtkomst till administrationscentret för Intune/Microsoft Endpoint Manager till administratörer utan Intune-licens.

1. Logga in i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Innehavaradministratör** > **Administratörslicensiering**.
2. Välj **Tillåt åtkomst för administratörer utan licens** > **Ja**.
    >[!WARNING]
    >Du kan inte ångra den här inställningen när du har klickat på **Ja**.

3. Från och med nu behöver inte användare som loggar in i administrationscentret för Microsoft Endpoint Manager någon Intune-licens. Deras åtkomst definieras av de roller som tilldelats dem.

Intune har stöd för upp till 350 olicensierade administratörer per säkerhetsgrupp. Administratörer över den här gränsen kan uppleva oförutsägbara beteenden.




