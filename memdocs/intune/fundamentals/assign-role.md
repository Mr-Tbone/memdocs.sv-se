---
title: Tilldela en roll till en Intune-användare
description: Lär dig hur du tilldelar en inbyggd eller anpassad roll till en användare i Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/26/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: a679df157a2623012d19fab2370792cac73f6f2b
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326809"
---
# <a name="assign-a-role-to-an-intune-user"></a>Tilldela en roll till en Intune-användare

Du kan tilldela en [inbyggd](role-based-access-control.md#built-in-roles) eller [anpassad](create-custom-role.md) roll till en Intune-användare.

För att kunna skapa, redigera eller tilldela roller måste ditt konto ha en av följande behörigheter i Azure AD:
- **Global administratör**
- **Intune Service-administratör**

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Administration av klientorganisation** > **Roller** > **Alla roller**.

2. På bladet **Intune-roller – Alla roller** väljer du den inbyggda roll som du vill tilldela > **Tilldelningar** > **Tilldela**.

5. På sidan **Grundläggande inställningar** anger du ett **namn på tilldelningen** och om du vill en **beskrivning av tilldelningen**. Välj sedan **Nästa**.

6. På sidan **Administratörsgrupper** väljer du den grupp som innehåller användaren som du vill ge behörighet till. Välj **Nästa**

7. På sidan **Omfång (grupper)** väljer du en grupp som innehåller de användare/enheter som ovanstående medlem ska kunna hantera. Välj **Nästa**.

8. På sidan **Omfång (taggar)** väljer du de taggar som den här rolltilldelningen ska tillämpas på. Välj **Nästa**.

9. Välj **Skapa** på sidan **Granska + skapa** när du är klar. Den nya tilldelningen visas i listan över tilldelningar.

## <a name="next-steps"></a>Nästa steg
- [Lär dig mer om rollbaserad åtkomstkontroll i Intune](role-based-access-control.md)
- [Skapa en anpassad roll](create-custom-role.md)


