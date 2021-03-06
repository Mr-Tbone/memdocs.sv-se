---
title: Lägga till anpassade inställningar för Android-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Lägg till eller skapa en anpassad profil för Android-enheter om du vill skapa en WiFi-profil med en i förväg delad nyckel, skapa en VPN-profil per app eller tillåta/blockera appar för Samsung Knox Standard-enheter i Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 494b3892-916e-4b40-9b67-61adec889bdf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8012b11557971ff8a7e3a05360243010d891fa2e
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262786"
---
# <a name="use-custom-settings-for-android-devices-in-microsoft-intune"></a>Använda anpassade inställningar för Android-enheter i Microsoft Intune

Med Microsoft Intune kan du lägga till eller skapa anpassade inställningar för dina Android-enheter med hjälp av en ”anpassad profil”. Anpassade profiler är en funktion i Intune. De gör att du kan lägga till enhetsinställningar och funktioner som inte är inbyggda i Intune.

Anpassade profiler för Android använder OMA-URI-inställningar (Open Mobile Alliance Uniform Resource Identifier) för att konfigurera olika funktioner på Android-enheter. De här inställningarna används vanligtvis av tillverkare av mobila enheter för att styra dessa funktioner.

Med hjälp av en anpassad profil kan du konfigurera och tilldela följande Android-inställningar. Följande inställningar är inte inbyggda i Intune:

- [Skapa en Wi-Fi-profil med en i förväg delad nyckel](/intune/wi-fi-profile-shared-key)
- [Skapa en VPN-profil per app](/intune/android-pulse-secure-per-app-vpn)
- [Tillåta och blockera appar för Samsung Knox Standard-enheter](/intune/samsung-knox-apps-allow-block)
- [Konfigurera webbskydd i Microsoft Defender Advanced Threat Protection för Android](../protect/advanced-threat-protection-manage-android.md)

>[!IMPORTANT]
> Endast de inställningar som anges kan konfigureras med hjälp av en anpassad profil. Android-enheter visar inte hela listan med OMA-URI-inställningar som du kan konfigurera. Om du vill se fler inställningar kan du rösta på detta på [Intunes UserVoice-webbplats](https://microsoftintune.uservoice.com/forums/291681-ideas).

Den här artikeln beskriver hur du skapar en anpassad profil för Android-enheter.

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande inställningar:

    - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ett användbart profilnamn är till exempel **anpassad profil för Android**.
    - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.
    - **Plattform**: Välj **Android**.
    - **Profiltyp**: Välj **Anpassad**.

4. I **Anpassade OMA-URI-inställningar** väljer du **Lägg till**. Ange följande inställningar:

    - **Namn**: Ange ett unikt namn för OMA-URI-inställningen så att du lätt kan hitta den.
    - **Beskrivning**: Ange en beskrivning som ger en översikt över inställningen, samt annan viktig information.
    - **OMA-URI**: Ange den OMA-URI som du vill använda som inställning.
    - **Datatyp**: Välj den datatyp som du vill använda för den här OMA-URI-inställningen. Alternativen är:

      - Sträng
      - Sträng (XML-fil)
      - Datum och tid
      - Heltal
      - Flyttal
      - Boolesk
      - Base64 (fil)

    - **Värde**: Ange det datavärde som du vill associera med den OMA-URI som du har angett. Värdet beror på vilken datatyp du valt. Om du till exempel valde **Datum och tid**, väljer du värdet från en datumväljare.

    När du har lagt till några inställningar kan du välja **Exportera**. **Exportera** skapar en lista över alla värden som du har lagt till i en fil med kommaavgränsade värden (.csv).

5. Klicka på **OK** för att spara ändringarna. Fortsätt att lägga till fler inställningar efter behov.
6. När du är klar väljer du **OK** > **Skapa** för att skapa Intune-profilen. När du är klar visas din profil i listan **Enhetskonfiguration – profiler**.

## <a name="next-steps"></a>Nästa steg

Profilen har skapats, men den gör inte något än. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Skapa en [anpassad profil på Android Enterprise-enheter](custom-settings-android-for-work.md).
