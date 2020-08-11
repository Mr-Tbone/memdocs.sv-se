---
title: Klient koppling – program (för hands version) i administrations centret
titleSuffix: Configuration Manager
description: Installera program för att ladda upp Configuration Manager enheter från administrations centret.
ms.date: 08/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 963dda08-87b8-4e80-90a7-25625efe8861
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: c82feac1b9c841d90be66989c220c7b528597b7d
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/10/2020
ms.locfileid: "88057603"
---
# <a name="tenant-attach-install-an-application-from-the-admin-center-preview"></a><a name="bkmk_apps"></a>Klient anslutning: installera ett program från administrations centret (för hands version)
<!--cm 6024389, in 7220536 pubpreview Aug 10, 2020-->
*Gäller för: Configuration Manager (aktuell gren)*

> [!Important]
> - Den här informationen är relaterad till en förhands gransknings funktion som kan ändras avsevärt innan den släpps kommersiellt. Microsoft lämnar inga garantier, uttryckliga eller underförstådda, avseende informationen som visas här.

Microsoft Endpoint Manager är en integrerad lösning för att hantera alla dina enheter. Microsoft sammanför Configuration Manager och Intune i en enda konsol som kallas **administrations Center för Microsoft Endpoint Manager**. Från administrations centret för Microsoft Endpoint Management kan du starta en applikations installation i real tid för en ansluten klient enhet.

   :::image type="content" source="media/6024389-tenant-attach-application-list.png" alt-text="Program i administrations Center för Microsoft Endpoint Manager" lightbox="media/6024389-tenant-attach-application-list.png":::

## <a name="prerequisites"></a>Förutsättningar

- Alla krav för klient [anslutning: ConfigMgr-klient information](client-details.md#prerequisites).
- [Samlad uppdatering för Microsoft Endpoint Configuration Manager version 2002](https://support.microsoft.com/help/4560496/) och motsvarande version av konsolen installerad
- Aktivera den valfria funktionen **Godkänn program begär Anden för användare per enhet**. Mer information finns i avsnittet [Enable optional features from updates](../core/servers/manage/install-in-console-updates.md#bkmk_options).
- Minst ett program som distribueras till en enhets samling med **en administratör måste godkänna en begäran om detta program på enhets** alternativ uppsättningen i distributionen. Mer information finns i [godkänna program](../apps/deploy-use/app-approval.md#bkmk_opt).
   - Användarens mål program eller program utan godkännande alternativ uppsättningen visas inte i program listan när du använder Configuration Manager version 2002.

## <a name="permissions"></a>Behörigheter

Användar kontot måste ha följande behörigheter:

- Behörigheten **läsa** för enhetens **samling** i Configuration Manager.
- **Läs** behörighet för **programmet** i Configuration Manager.
- **Godkännande** behörighet för **programmet** i Configuration Manager.
- **Användar rollen administratör** för det Configuration Manager mikrotjänst programmet i Azure AD. 
  - Lägg till rollen i Azure AD från **företags program**  >  **Configuration Manager mikrotjänst**  >  **användare och grupper**  >  **Lägg till användare**. Grupper stöds om du har Azure AD Premium.
   > [!TIP]
   > [Rollen program administratör i Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) har tillräcklig behörighet för att lägga till en användare i programmets **Administratörs användar** roll.

## <a name="deploy-an-application-to-a-device"></a><a name="bkmk_deploy"></a>Distribuera ett program till en enhet

1. Navigera till i en webbläsare [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Välj **enheter** och sedan **alla enheter**.
1. Välj en enhet som har synkroniserats från Configuration Manager via [klient anslutning](device-sync-actions.md).
1. Välj **program**.
1. Välj programmet och klicka på **Installera**.

   :::image type="content" source="media/6024389-tenant-attach-application-install.png" alt-text="Programinstallation från administrations Center för Microsoft Endpoint Manager" lightbox="media/6024389-tenant-attach-application-install.png":::

Du kan exportera alla data som för närvarande finns i vyn till en. csv-fil. Välj alternativet **Exportera** längst upp på sidan för att skapa filen. Om vyn överskrider 500 rader exporteras endast de första 500.

## <a name="application-status"></a>Program status

Du kan filtrera program listan baserat på statusen. Program status kan vara något av följande:

- **Tillgängligt**: programmet har aldrig installerats på enheten.
- **Installerat**: programmet är installerat på enheten.
- **Installerar**: programmet håller på att installeras.
- **Installation begärd**: installationen har begärts, men klienten har inte godkänt begäran ännu.
   - Om enheten är offline kommer installations förfrågan att bekräftas när den kommer tillbaka online och tar emot principen.  
- **Misslyckades**: det gick inte att installera programmet.
- **Kraven är inte uppfyllda**: program kraven har inte uppfyllts.
- **Inte installerat**: programmet är inte installerat. Normalt sett visas denna status om en annan distribution eller en användare har tagit bort programmet.


## <a name="next-steps"></a>Nästa steg

[Felsöka program](troubleshoot-applications.md)