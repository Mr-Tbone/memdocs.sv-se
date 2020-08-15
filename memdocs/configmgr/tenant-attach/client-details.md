---
title: Klient organisations anslutning – information om ConfigMgr-klient (för hands version) i administrations centret
titleSuffix: Configuration Manager
description: Visa klient information för Configuration Manager enheter från administrations centret.
ms.date: 07/08/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: dd997508f34b02ef7d2824ffd3a4dfec9cb9066a
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/15/2020
ms.locfileid: "88251886"
---
# <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview"></a><a name="bkmk_mem"></a> Klient anslutning: information om ConfigMgr-klient i administrations Center (för hands version)
<!--6024387, 6374854, 6521921, intune 7552762 pubpreview July 7, 2020-->
*Gäller för: Configuration Manager (aktuell gren)*

Microsoft Endpoint Manager är en integrerad lösning för att hantera alla dina enheter. Microsoft sammanför Configuration Manager och Intune i en enda konsol som kallas **administrations Center för Microsoft Endpoint Manager**. Du kan se information om ConfigMgr-klienter, inklusive samlingar, gräns grupps medlemskap och klient information i real tid för en speciell enhet i administrations centret.

> [!Important]
> - Den här informationen är relaterad till en förhands gransknings funktion som kan ändras avsevärt innan den släpps kommersiellt. Microsoft lämnar inga garantier, uttryckliga eller underförstådda, avseende informationen som visas här.
> - Fliken gränser grupper fungerar endast för fristående platser. Fliken kommer att vara tom i administrations centret för något annat än en fristående primär plats.

## <a name="prerequisites"></a>Krav

- En miljö som är [ansluten till uppladdade enheter](device-sync-actions.md).
- Någon av följande webbläsare:
  - Microsoft Edge, version 77 och senare
  - Google Chrome
- Användar kontot har identifierats med både [Azure Active Directory (Azure AD) identifiering av användare](https://docs.microsoft.com/mem/configmgr/core/servers/deploy/configure/about-discovery-methods#azureaddisc) och [Active Directory användar identifiering](https://docs.microsoft.com/mem/configmgr/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser).
  - Det innebär att användar kontot måste vara ett synkroniserat användar objekt i Azure.

## <a name="permissions"></a>Behörigheter

Användar kontot måste ha följande behörigheter:

- Behörigheten **läsa** för enhetens **samling** i Configuration Manager.
- **Användar rollen administratör** för det Configuration Manager mikrotjänst programmet i Azure AD.
  - Lägg till rollen i Azure AD från **företags program**  >  **Configuration Manager mikrotjänst**  >  **användare och grupper**  >  **Lägg till användare**. Grupper stöds om du har Azure AD Premium.
   > [!TIP]
   > [Rollen program administratör i Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) har tillräcklig behörighet för att lägga till en användare i programmets **Administratörs användar** roll.

## <a name="view-configmgr-client-details"></a>Visa information om ConfigMgr-klient

1. Navigera till i en webbläsare [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Välj **enheter** och sedan **alla enheter**.
1. Välj en enhet som har synkroniserats från Configuration Manager via [klient anslutning](device-sync-actions.md).
1. Välj **klient information (för hands version)**.
   - Den primära platsen uppdaterar följande fält en gång i timmen:
      - **Senaste princip förfrågan**
      - **Senaste aktiva tid**
      - **Senaste hanterings plats**.

   :::image type="content" source="media/6024387-device-details.png" alt-text="Klient information i administrations Center för Microsoft Endpoint Manager" lightbox="media/6024387-device-details.png":::

1. Välj **samlingarna (för hands version)** för att visa klientens samlingar. <!--6024390-->

   :::image type="content" source="media/6024387-device-collections.png" alt-text="Klient samlingar i administrations Center för Microsoft Endpoint Manager" lightbox="media/6024387-device-collections.png":::

## <a name="next-steps"></a>Nästa steg

[Felsöka klient information](troubleshoot-client-details.md)
