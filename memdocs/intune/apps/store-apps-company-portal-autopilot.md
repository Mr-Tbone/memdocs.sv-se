---
title: Lägga till och tilldela företagsportalappen för Windows 10 för Autopilot-etablerade enheter
titleSuffix: Microsoft Intune
description: Lägg till och tilldela företagsportalappen för Windows 10 i Intune för Autopilot-etablerade enheter.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d45d73f9c10c9bf7562def73b005c0dd63c7613
ms.sourcegitcommit: 91519f811b58a3e9fd116a4c28e39341ad8af11a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88559529"
---
# <a name="add-and-assign-the-windows-10-company-portal-app-for-autopilot-provisioned-devices"></a>Lägga till och tilldela företagsportalappen för Windows 10 för Autopilot-etablerade enheter

Din användare kan använda företagsportalappen för att hantera enheter och installera appar. Du kan tilldela företagsportalappen för Windows 10 direkt från Intune. 

## <a name="prerequisites"></a>Förutsättningar

För Windows 10 Autopilot-etablerade enheter rekommenderar vi att du kopplar ditt Microsoft Store för företag-konto till Intune. Mer information finns i [Så här hanterar du volymköpta appar från Microsoft Store för företag med Microsoft Intune](windows-store-for-business.md).

Du kan välja att installera **företagsportalappen (offline)** genom att följa stegen nedan. Företagsportalappen installeras i enhetskontexten när den tilldelas till gruppen Autopilot och installeras på enheten innan användaren loggar in.

## <a name="configure-the-store-settings-to-show-the-offline-app"></a>Konfigurera butiksinställningarna för att visa offlineappen

1. Logga in på [Microsoft Store för företag](https://www.microsoft.com/business-store) med ditt administratörskonto.
2. Välj fliken **Hantera** i fönstrets överkant.
3. Välj **Inställningar** i rutan till vänster.
4. Ställ in **Visa offlineappar** i avsnittet om **shoppingupplevelsen** till **På**.  
   Offlinelicensierade appar visas.

## <a name="get-the-offline-company-portal-app-from-the-store"></a>Hämta offlineföretagsportalappen från butiken

1. Sök och välj appen **Företagsportal**.
2. Ange **Licenstyp** till **Offline**.
3. Välj **Hämta appen** för att hämta och lägga till offlineappen Företagsportal i inventeringen.
   För att appen ska visas i Intune måste du antingen vänta tills synkroniseringsschemat är klart eller göra en manuell synkronisering från administrationscentret för Microsoft Endpoint Manager.

## <a name="manually-sync-company-portal-app-with-intune"></a>Synkronisera företagsportalappen manuellt med Intune

1. Logga in på  [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) med ditt administratörskonto.
2. Välj **Administration av klientorganisation** > **Anslutningsappar och token** > **Microsoft Store för företag**.
3. Klicka på **Aktivera**.
4. Om du inte redan gjort det klickar du på länken för att registrera Microsoft Store för företag och kopplar kontot på det sätt som beskrivs tidigare.
5. I listrutan **Språk** väljer du det språk som ska användas vid visning av program från Microsoft Store för företag i Azure Portal. Apparna installeras i slutanvändarens språk om det är tillgängligt oavsett vilket språk de visas i.
6. Klicka på **Synkronisera** för att hämta appar som du har köpt från Microsoft Store i Intune.

## <a name="assign-the-company-portal-app"></a>Tilldela appen Företagsportal

1. Logga in på  [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) med ditt administratörskonto.
2. Välj **Appar** > **Windows**.
3. Välj **Företagsportal (offline)** i listan med Windows-appar.
4. [Tilldela](apps-deploy.md) företagsportalappen som en obligatorisk app till dina valda Autopilot-enhetsgrupper.

## <a name="next-steps"></a>Nästa steg

- Mer information om hur du tilldelar appar finns i [Tilldela appar till grupper](apps-deploy.md).

