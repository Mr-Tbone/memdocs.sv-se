---
title: Snabbstart – Skapa och tilldela en anpassad roll i Intune
description: Snabbstart – Skapa och tilldela en anpassad roll för en fjärrenhetshanterare.
services: microsoft-intune
author: ErikjeMS
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 03/26/2019
ms.author: erikje
ms.assetid: 0b3ac749-4a61-4717-bf08-e0e6a15c3b0a
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7f1f381d0b9f48f26c84785bb7c50434971d6c89
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79357135"
---
# <a name="quickstart-create-and-assign-a-custom-role"></a>Snabbstart: Skapa och tilldela en anpassad roll

I den här Intune-snabbstarten får du skapa en anpassad roll med särskilda behörigheter för en säkerhetsåtgärdsavdelning. Du måste tilldela en grupp med sådana operatörer rollen. Det finns flera standardroller som du kan använda direkt. Men genom att skapa anpassade roller som den här kan du ha exakt åtkomstkontroll till alla delar av ditt system för hantering av mobilenheter.

Om du inte har en Intune-prenumeration [kan du registrera dig för ett kostnadsfritt utvärderingskonto](free-trial-sign-up.md).

## <a name="prerequisites"></a>Krav

- För att kunna slutföra den här snabbstarten måste du först [skapa en grupp](quickstart-create-group.md).

## <a name="sign-in-to-intune"></a>Logga in i Intune

Logga in på [Intune](https://aka.ms/intuneportal) som global administratör eller Intune-tjänstadministratör. Om du har skapat en prenumeration för en Intune-utvärdering, är det konto som du skapade prenumerationen med den globala administratören.

## <a name="create-a-custom-role"></a>Skapa en anpassad roll

När du skapar en anpassad roll kan du ange behörigheter för en mängd olika åtgärder. För säkerhetsåtgärdsrollen konfigurerar vi några läsbehörigheter, så att operatören kan granska en enhets konfigurationer och principer.

1. Välj **Roller** > **Alla roller** > **Lägg till** i Intune.
![Webbläsare](./media/quickstart-create-custom-role/add-custom-role.png)
2. Ange *Säkerhetsåtgärder* i rutan **Namn** under **Lägg till anpassad roll**.
3. Ange *Den här rollen låter en säkerhetsoperatör övervaka enhetskonfigurationen och kompatibilitetsinformationen* i rutan **Beskrivning**.
4. Välj **Konfigurera** > **Företagsenhetsidentifierare** > **Ja** bredvid **Läs** > **OK**.
![Webbläsare](./media/quickstart-create-custom-role/corp-device-id-read.png)
5. Välj **Enhetsefterlevnadsprinciper** > **Ja** bredvid **Läs** > **OK**.
6. Välj **Enhetskonfigurationer** > **Ja** bredvid **Läs** > **OK**.
7. Välj **Organisation** > **Ja** bredvid **Läs** > **OK**.
8. Välj **OK** > **Skapa**.

## <a name="assign-the-role-to-a-group"></a>Tilldela en grupp rollen

Innan din säkerhetsoperatör kan använda de nya behörigheterna måste du tilldela rollen till en grupp som innehåller säkerhetsanvändaren.

1. I Intune väljer du **Roller** > **Alla roller** > **Säkerhetsåtgärder**.
2. Välj **Tilldelningar** > **Tilldela** under **Intune-roller**.
3. Ange *Säkerhetsalternativ* i rutan **Tilldelningsnamn**.
4. Välj **Medlemmar (grupper)**  > **Lägg till**.
5. Välj gruppen **Contoso-testare**.
6. Välj **Välj** > **OK**.
7. Välj **Omfång (grupper)**  > **Välj grupper att inkludera** > **Contoso-testare**.
8. Välj **Välj** > **OK** > **OK**.

Nu är alla i gruppen medlemmar i rollen *Säkerhetsåtgärder* och kan granska följande information om en enhet: företagsenhetsidentifierare, enhetsefterlevnadspolicyer, enhetskonfigurationer och organisationsinformation.

## <a name="clean-up-resources"></a>Rensa resurser

Om du inte vill använda den nya anpassade rollen mer kan du ta bort den. Välj **Roller** > **Alla roller** > välj punkterna bredvid rollen > **Ta bort**.

## <a name="next-steps"></a>Nästa steg

I den här snabbstarten har du skapat en anpassad säkerhetsåtgärdsroll och tilldelat den till en grupp. Mer information om roller i Intune finns i [Rollbaserad administrationskontroll (RBAC) med Microsoft Intune](role-based-access-control.md)

Om du vill följa den här serien med Intune-snabbstarter fortsätter du till nästa snabbstart.

> [!div class="nextstepaction"]
> [Snabbstart: Skapa en e-postenhetsprofil för iOS/iPadOS](../configuration/quickstart-email-profile.md)
