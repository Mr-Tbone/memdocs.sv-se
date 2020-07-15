---
title: Använda rollbaserad åtkomstkontroll (RBAC) och omfångstaggar för distribuerad IT i Intune | Microsoft Docs
description: Använd omfångstaggar för att filtrera konfigurationsprofiler för specifika roller.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.technology: ''
ms.assetid: a21d3039-f2ed-4f43-b6fa-d00c071edbc4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a229b9159c4c3613edc2d718db1fd0931f94cf9f
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240753"
---
# <a name="use-role-based-access-control-rbac-and-scope-tags-for-distributed-it"></a>Använda rollbaserad åtkomstkontroll (RBAC) och omfångstaggar för distribuerad IT

Du kan använda rollbaserad åtkomstkontroll och omfångstaggar för att se till att rätt administratörer har rätt åtkomst och synlighet för rätt Intune-objekt. Roller avgör vilken åtkomst administratörer har till vilka objekt. Omfångstaggar avgör vilka objekt administratörer kan se.

Anta exempelvis att administratören på regionkontoret i Seattle har rollen som princip- och profilhanterare. Du vill att den här administratören endast ska se och hantera profiler och principer som gäller för Seattle-enheter. Om du vill konfigurera den här åtkomsten gör du följande:

1. Skapa en omfångstagg som heter Seattle.
2. Skapa en rolltilldelning för rollen Princip- och profilhanterare med: 
    - Medlemmar (Grupper) = en säkerhetsgrupp som heter IT-administratörer i Seattle. Alla administratörer i den här gruppen får behörighet att hantera principer och profiler för användare/enheter i Omfånget (Grupper).
    - Omfång (Grupper) = en säkerhetsgrupp som heter Användare i Seattle. Profiler och principer för alla användare/enheter i den här gruppen kan hanteras av administratörerna i Medlemmar (Grupper). 
    - Omfång (Taggar) = Seattle. Administratörer i Medlemmar (Grupper) kan se Intune-objekt som även har omfångstaggen Seattle.
3. Lägg till omfångstaggen Seattle i principer och profiler som du vill att administratörer i Medlemmar (Grupper) ska kunna komma åt.
4. Lägga till omfångstaggen Seattle till enheter som ska vara synliga för administratörer i Medlemmar (Grupper). 

## <a name="default-scope-tag"></a>Standardomfångstagg
Standardomfångstaggen läggs automatiskt till i alla otaggade objekt som stöder omfångstaggar.

Funktionen för standardomfångstaggar liknar funktionen för säkerhetsomfång i Microsoft Endpoint Configuration Manager. 

## <a name="to-create-a-scope-tag"></a>Skapa en omfångstagg

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Administration av klientorganisation** > **Roller** > **Omfång (taggar)**  > **Skapa**.
2. På sidan **Grundinställningar** anger du ett **Namn** och en valfri **Beskrivning**. Välj **Nästa**.
3. På sidan **Tilldelningar** väljer du de grupper som innehåller de enheter som du vill tilldela den här omfångstaggen. Välj **Nästa**.
4. På sidan **Granska + skapa** väljer du **Skapa**.

## <a name="to-assign-a-scope-tag-to-a-role"></a>Tilldela en omfångstagg till en roll

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Administration av klientorganisation** > **Roller** > **Alla roller** > välj en roll > **Tilldelningar** > **Tilldela**.
2. På sidan **Grundläggande** anger du ett **Tilldelningsnamn** och en **Beskrivning**. Välj **Nästa**.
3. På sidan **Administratörsgrupper** väljer du **Välj grupper som ska inkluderas** och väljer de grupper som du vill ha som en del av den här tilldelningen. Användare i de här grupperna får behörighet att hantera användare/enheter i omfånget (grupper). Välj **Nästa**.

    ![Skärmbild av val av medlemsgrupper.](./media/scope-tags/select-member-groups.png)

4. På sidan **Omfångsgrupper** väljer du något av följande alternativ för **Tilldela till**
    - **Valda grupper**: Välj de grupper som innehåller de användare/enheter som du vill hantera. Alla användare/enheter i de valda grupperna kommer att hanteras av användarna i administratörsgrupperna.
    - **Alla användare**: Alla användare kan hanteras av användarna i administratörsgrupperna.
    - **Alla enheter**: Alla enheter kan hanteras av användarna i administratörsgrupperna.
    - **Alla användare och alla enheter**: Alla användare och enheter kan hanteras av användarna i administratörsgrupperna.

5. Välj **Nästa**
6. På sidan **Omfångstaggar** väljer du de taggar som du vill lägga till i den här rollen. Användare i administratörsgrupperna får åtkomst till de Intune-objekt som också har samma omfångstagg. Du kan tilldela högst 100 omfångstaggar till en roll.
7. Välj **Nästa** för att gå till sidan **Granska + skapa**, och välj sedan **Skapa**.

## <a name="assign-scope-tags-to-other-objects"></a>Tilldela omfångstaggar till andra objekt

För objekt som stöder omfångstaggar visas omfångstaggar vanligtvis under **Egenskaper**. Om du till exempel vill tilldela en omfångstagg till en konfigurationsprofil följer du dessa steg:

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **Konfigurationsprofiler** > välj en profil.

2. Välj **Egenskaper** > **Omfång (taggar)**  > **Redigera** > **Välj omfångstaggar** > välj de taggar som du vill lägga till i profilen. Du kan tilldela högst 100 omfångstaggar till ett objekt.
4. Välj **Välj** > **Granska + spara**.

## <a name="scope-tag-details"></a>Information om omfångstaggar
När du arbetar med omfångstaggar bör du beakta följande: 

- Du kan tilldela omfångstaggar till en Intune-objekttyp om klientorganisationen kan ha flera versioner av det objektet (till exempel rolltilldelningar eller appar).
  Följande Intune-objekt är undantag till den här regeln och stöder för närvarande inte omfångstaggar:
    - Windows ESP-profiler
    - Företagsenhetsidentifierare
    - Autopilot-enheter
    - Platser för enhetsefterlevnad
    - Jamf-enheter
- VPP-appar och e-böcker som är associerade med VPP-token ärver de omfångstaggar som tilldelats till den associerade VPP-token.
- När en administratör skapar ett objekt i Intune tilldelas alla omfångstaggar som tilldelats till den administratören automatiskt till det nya objektet.
- Intune RBAC gäller inte för Azure Active Directory-roller. Därför har rollerna Intune-tjänstadministratörer och Globala administratörer fullständig administratörsåtkomst till Intune oavsett vilka omfångstaggar de har.
- Om en rolltilldelning saknar omfångstagg kan IT-administratören se alla objekt baserat på IT-administratörernas behörigheter. Administratörer som saknar omfångstaggar har i princip alla omfångstaggar.
- Du kan endast tilldela en omfångstagg som du har i dina rolltilldelningar.
- Du kan endast ange grupper som visas i Omfång (Grupper) för din rolltilldelning som mål.
- Om du har en omfångstagg tilldelad till din roll kan du inte ta bort alla omfångstaggar på ett Intune-objekt. Det krävs minst en omfångstagg.

## <a name="next-steps"></a>Nästa steg

Lär dig hur omfångstaggar beter sig när det finns [flera rolltilldelningar](role-based-access-control.md#multiple-role-assignments).
Hantera dina [roller](role-based-access-control.md) och [profiler](../configuration/device-profile-assign.md).


