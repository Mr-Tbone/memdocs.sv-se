---
title: Installera Office 365-appar på macOS-enheter med Microsoft Intune
titleSuffix: ''
description: Så här använder du Microsoft Intune för installera Office 365-appar på macOS-enheter.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2372332a-7e3a-4a9c-91a9-86654e0fabe2
ms.reviewer: aiwang
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 14a4d66cfd5ac0ee3c0938e96794ed12d5b5fde6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989515"
---
# <a name="assign-office-365-to-macos-devices-with-microsoft-intune"></a>Tilldela Office 365 till macOS-enheter med Microsoft Intune

Den här apptypen gör det enkelt för dig att tilldela macOS-enheter till Office 365 2016-appar. Genom att använda den här apptypen kan du installera Word, Excel, PowerPoint, Outlook, OneNote och Teams. För att hålla apparna säkrare och uppdaterade innehåller de här apparna även Microsoft AutoUpdater (MAU). Appar som du vill använda visas som en enda app i listan med appar i Intune-konsolen.

> [!NOTE]
> Microsoft Office 365 ProPlus har bytt namn till **Microsoft 365-appar för företag**. I vår dokumentation kommer vi ofta att referera till det som **Microsoft 365-appar**.

## <a name="before-you-start"></a>Innan du börjar

Innan du börjar lägga till Office 365-appar på macOS-enheter bör du förstå följande:

- Enheterna som du distribuerar dessa appar på måste köra macOS 10.10 eller senare.
- Intune har stöd för att lägga till Office-appar som ingår i Office 2016 för Mac-paket endast.
- Om alla Office-program är öppna när Intune installerar appen kan användare förlora data från filer som inte sparats.

## <a name="select-microsoft-365-apps"></a>Välj Microsoft 365-appar

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Appar** > **Alla appar** > **Lägg till**.
3. Välj **macOS** i avsnittet **Microsoft 365 Apps** i fönstret **Välj apptyp**.
4. 4. Klicka på **Välj**. Stegen i **Lägg till Microsoft 365-appar**visas.

## <a name="step-1---app-suite-information"></a>Steg 1 – Information om appsvit

I det här steget anger du information om appaketet. Den här informationen hjälper dig att identifiera appsviten i Intune och hjälper användarna att hitta appsviten det i företagsportalappen.

1. På sidan **Information om appsvit** kan du bekräfta eller ändra standardvärdena:
    - **Namn på programsvit**: Ange namnet på appsviten så som det visas i företagsportalen. Kontrollera att alla svitnamn du använder är unika. Om samma paketnamn förekommer två gånger visas endast en av apparna för användarna på företagsportalen.
    - **Beskrivning av programsvit**: Ange en beskrivning av appsviten. Exempelvis kan du visa de appar som ingår.
    - **Utgivare**: Microsoft visas som utgivare.
    - **Kategori**: Välj en eller flera av de inbyggda appkategorierna, eller en kategori som du har skapat. Inställningen gör det enklare för användarna att hitta appaketet när de söker på företagsportalen.
    - **Visa denna som en aktuell app i företagsportalen**: Välj det här alternativet för att tydligt visa appsviten på företagsportalens huvudsida när användarna söker efter appar.
    - **Webbadress till information**: Du kan välja att ange en webbadress till en webbplats som innehåller information om den här appen. Webbadressen visas för användarna på företagsportalen.
    - **Sekretesswebbadress**: Du kan välja att ange en webbadress till en webbplats som innehåller sekretessinformation för den här appen. Webbadressen visas för användarna på företagsportalen.
    - **Utvecklare**: Microsoft visas som utvecklare.
    - **Ägare**: Microsoft visas som ägare.
    - **Kommentarer**: Ange eventuella kommentarer som du vill koppla till den här appen.
    - **Logotyp**: Webbläsarens logotyp för Microsoft 365-appar visas med appen när användare söker på företagsportalen.
2. Visa sidan **Omfångstaggar** genom att klicka på **Nästa**.

## <a name="step-2---select-scope-tags-optional"></a>Steg 2 – Välj omfångstaggar (valfritt)
Du kan använda omfångstaggar för att bestämma vem som kan se klientappsinformation i Intune. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

1. Klicka på **Välj omfångstaggar** om du vill lägga till omfångstaggar för appsviten. 
2. Klicka på **Nästa** för att visa sidan **Tilldelningar**.

## <a name="step-3---assignments"></a>Steg 3 – Tilldelningar

1. Välj **Obligatorisk**, **Tillgängligt för registrerade enheter**som grupptilldelning för appsviten. Mer information finns i [Lägg till grupper för att organisera användare och enheter](../fundamentals/groups-add.md) och [Tilldela appar till grupper med Microsoft Intune](apps-deploy.md).

    >[!Note]
    > Du kan inte avinstallera appsviten Microsoft 365 Apps for macOS via Intune.

2. Visa sidan **Granska och skapa** genom att klicka på **Nästa**. 

## <a name="step-4---review--create"></a>Steg 4 – Granska och skapa

1. Granska värdena och inställningarna som du har angett för appsviten.
2. När du är färdig klickar du på **Skapa** för att lägga till appen i Intune.

    Bladet **Översikt** visas. Programsviten visas som en enda post i listan över appar.

## <a name="next-steps"></a>Nästa steg

- Mer information om att lägga till appar för Office 365-appar på Windows 10-enheter finns i [Tilldela Microsoft 365 Apps på Windows 10-enheter med Microsoft Intune](apps-add-office365.md).
- Om du vill veta mer om att inkludera och exkludera apptilldelningar från grupper med användare kan du läsa [Inkludera och exkludera apptilldelningar](apps-inc-exl-assignments.md).
