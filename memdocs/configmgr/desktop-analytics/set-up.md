---
title: Ställ in Desktop Analytics
titleSuffix: Configuration Manager
description: En instruktions guide för att konfigurera och integrera med Desktop Analytics.
ms.date: 02/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: facfb2be1972933524c7ad632537fc8306939c1c
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700760"
---
# <a name="how-to-set-up-desktop-analytics"></a>Konfigurera Skriv bords analys

Använd den här proceduren för att logga in på Desktop Analytics och konfigurera den i din prenumeration. Den här proceduren är en engångs process för att konfigurera Skriv bords analys för din organisation.  

> [!Important]  
> Information om de allmänna kraven för Skriv bords analys med Configuration Manager finns i [krav](overview.md#prerequisites).  

## <a name="initial-onboarding"></a>Inledande onboarding

1. Öppna [Skriv bords analys portalen](https://aka.ms/desktopanalytics) i Microsoft 365 enhets hantering som en användare med rollen **Global administratör** . Välj **Starta**. Alternativt går du till arbets ytan **program bibliotek** i Configuration Manager-konsolen, väljer noden **Skriv bords analys** och väljer **Planera distributioner**.

2. På sidan **Godkänn service avtal** granskar du service avtalet och väljer **Godkänn**.  

3. På sidan **Bekräfta prenumerationen** granskar du listan över nödvändiga kvalificerings licenser. Ändra inställningen till **Ja** bredvid **har du en av de stödda eller högre prenumerationerna**och välj sedan **Nästa**.  

4. På sidan **ge användare åtkomst** :

    - **Tillåt Skriv bords analys för att hantera katalog roller åt dig**: Skriv bords analys tilldelar automatiskt **arbets ytans ägare** rollen som **Skriv bords administratör** . Om dessa grupper redan är en **Global administratör**sker ingen ändring.

        Om du inte väljer det här alternativet lägger Desktop Analytics fortfarande till användare som medlemmar i säkerhets gruppen. En **Global administratör** måste tilldela rollen **Desktop Analytics-administratör** manuellt för användarna.

        Mer information om hur du tilldelar administratörs roll behörigheter i Azure Active Directory och de behörigheter som tilldelats **Desktop Analytics-administratörer**finns [i administratörs roll behörigheter i Azure Active Directory](/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analytics förkonfigurerar säkerhets gruppen **ägare till arbets ytan** i Azure Active Directory för att skapa och hantera arbets ytor och distributions planer.

        Om du vill lägga till en användare i gruppen skriver du dess namn eller e-postadress i avsnittet **Ange namn eller e-postadress** . När du är klar väljer du **Nästa**.

5. På sidan för att **Konfigurera din arbets yta**:  

    > [!NOTE]  
    > För att slutföra det här steget måste användaren ha ägar behörigheter för **arbets ytan** och ytterligare åtkomst till Azure-prenumerationen och resurs gruppen. Mer information finns i [krav](overview.md#prerequisites).  

    - Om du vill använda en befintlig arbets yta för Skriv bords analys väljer du den och fortsätter med nästa steg.  

        > [!TIP]  
        > Du kan bara ha en Desktop Analytics-arbetsyta per Azure AD-klient. Enheter kan bara skicka diagnostikdata till en arbets yta.  

    - Om du vill skapa en arbets yta för Desktop Analytics väljer du **Lägg till arbets yta**.  

        1. Ange ett globalt unikt **namn på arbets ytan**.

        2. Välj den nedrullningsbara List rutan för att **välja namnet på Azure-prenumerationen för den här arbets ytan**och välj Azure-prenumerationen för den här arbets ytan.  

        3. **Skapa ny** Resurs grupp eller **Använd befintlig**.

        4. Välj **region** i listan och välj sedan **Lägg till**.  

6. Välj en ny eller befintlig arbets yta och välj sedan **Ange som Desktop Analytics-arbetsyta**.  Välj sedan **Fortsätt** i dialog rutan **Bekräfta och bevilja åtkomst** .  

7. På fliken ny webbläsare väljer du ett konto som du vill använda för att logga in. Välj alternativet att godkänna **för din organisations räkning** och välj **Godkänn**.  

    > [!Note]  
    > Detta medgivande är att tilldela MALogAnalyticsReader-programmet rollen Log Analyticss läsare för arbets ytan. Den här program rollen krävs av Desktop Analytics. Mer information finns i [program rollen MALogAnalyticsReader](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. Gå tillbaka till sidan för att **Konfigurera din arbets yta**och välj **Nästa**.  

9. På sidan **sista steg** väljer **du gå till Skriv bords analys**.

Azure Portal visar **Start** sidan för Skriv bords analys.

## <a name="next-steps"></a>Nästa steg

Fortsätt till nästa artikel för att ansluta Configuration Manager med Desktop Analytics.
> [!div class="nextstepaction"]  
> [Ansluta Configuration Manager](connect-configmgr.md)