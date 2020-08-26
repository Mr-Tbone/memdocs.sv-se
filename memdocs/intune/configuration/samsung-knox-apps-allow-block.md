---
title: Microsoft Intune-principer för att tillåta/blockera appar för Samsung Knox
titleSuffix: ''
description: Skapa en anpassad profil för att tillåta och blockera appar för Samsung Knox Standard-enheter.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3ee2e89dcfd7ab963dae3b14b5e7d53daaa07ff4
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695995"
---
# <a name="use-custom-policies-in-microsoft-intune-to-allow-and-block-apps-for-samsung-knox-standard-devices"></a>Använd anpassade principer för att tillåta och blockera appar för Samsung Knox Standard-enheter i Microsoft Intune 

I den här artikeln anges hur du skapar en anpassad princip för Microsoft Intune som skapar något av följande:

- En lista över appar som blockeras från att köras på enheten. Appar i den här listan blockeras från att köras även om de redan är installerade när principen tillämpas.
- En lista över appar som enhetens användare tillåts att installera från Google Play Store. Endast de appar som du tar med i listan kan installeras. Inga andra appar kan installeras från butiken.

De här inställningarna kan endast användas av enheter som kör Samsung Knox Standard.

## <a name="create-an-allowed-or-blocked-app-list"></a>Skapa en lista med tillåtna eller blockerade appar

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande inställningar:

    - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ett användbart profilnamn är till exempel **anpassad profil för Android**.
    - **Beskrivning**: Ange en beskrivning som ger en översikt över inställningen, samt annan viktig information.
    - **Plattform**: Välj **Android**.
    - **Profiltyp**: Välj **Anpassad**.

4. I **Anpassade OMA-URI-inställningar** väljer du **Lägg till**. Ange följande inställningar:

    För en lista över appar som blockeras från att köras på enheten:

    - **Namn**: Ange **PreventStartPackages**.
    - **Beskrivning**: Ange en beskrivning som ger en översikt över inställningen och eventuell annan relevant information som gör det enklare att hitta profilen. Ange exempelvis **En lista över appar som blockeras från att köras på enheten**.
    - **OMA-URI** (skiftlägeskänslig): Ange **./Vendor/MSFT/PolicyManager/My/ApplicationManagement/PreventStartPackages**.
    - **Datatyp**: Välj **Sträng**.
    - **Värde**: Ange en lista över de appaketnamn som du vill tillåta. Du kan använda `;`, `:` eller `|` som avgränsare. Ange till exempel `package1;package2;`.

   För en lista över appar som användare tillåts att installera från Google Play (alla andra appar exkluderas):

    - **Namn**: Ange **AllowInstallPackages**.
    - **Beskrivning**: Ange en beskrivning som ger en översikt över inställningen och eventuell annan relevant information som gör det enklare att hitta profilen. Ange till exempel **En lista över appar som användare kan installera från Google Play**.
    - **OMA-URI** (skiftlägeskänslig): Ange **./Vendor/MSFT/PolicyManager/My/ApplicationManagement/AllowInstallPackages**.
    - **Datatyp**: Välj **Sträng**.
    - **Värde**: Ange en lista över de appaketnamn som du vill tillåta. Du kan använda `;`, `:` eller `|` som avgränsare. Ange till exempel `package1;package2;`.

5. Klicka på **OK** för att spara ändringarna.
6. När du är klar väljer du **OK** > **Skapa** för att skapa Intune-profilen. När du är klar visas din profil i listan **Enhetskonfiguration – profiler**.

>[!TIP]
> Du kan hitta paket-ID:et för en app genom att gå till appen i Google Play. Paket-ID finns i webbadressen på appens sida. Paket-ID för Microsoft Word-appen är till exempel **com.microsoft.office.word**.

Appinställningarna tillämpas nästa gång en målenhet checkar in.

## <a name="next-steps"></a>Nästa steg

Profilen har skapats, men den gör inte något än. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
