---
title: Lägga till anpassade inställningar för Android Enterprise-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Lägga till eller skapa en anpassad profil för Android Enterprise-enheter i Microsoft Intune
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
ms.assetid: 4724d6e5-05e5-496c-9af3-b74f083141f8
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 827b5eb8b65aa59212b9ef990def3c5f191baf7c
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79334437"
---
# <a name="use-custom-settings-for-android-enterprise-devices-in-microsoft-intune"></a>Använda anpassade inställningar för Android Enterprise-enheter i Microsoft Intune

Med Microsoft Intune kan du lägga till eller skapa anpassade inställningar för dina Android Enterprise Work Profile-enheter med hjälp av en ”anpassad profil”. Anpassade profiler är en funktion i Intune. De gör att du kan lägga till enhetsinställningar och funktioner som inte är inbyggda i Intune.

Anpassade profiler för Android Enterprise använder OMA-URI-inställningar (Open Mobile Alliance Uniform Resource Identifier) för att styra funktioner på Android Enterprise-enheter. De här inställningarna används vanligtvis av tillverkare av mobila enheter för att styra dessa funktioner.

Intune har stöd för följande begränsade antal anpassade Android Enterprise-profiler:

- ./Vendor/MSFT/WiFi/Profile/SSID/Settings: [Så här skapar du en Wi-Fi-profil med en i förväg delad nyckel](wi-fi-profile-shared-key.md) har några exempel.
- ./Vendor/MSFT/VPN/Profile/Name/PackageList: [Skapa en VPN-profil per app](android-pulse-secure-per-app-vpn.md) har några exempel.
- ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste: Se [exemplet](#example) i den här artikeln. Den här inställningen är också tillgänglig i användargränssnittet. Mer information finns i [Enhetsinställningarna för Android Enterprise tillåter eller begränsar funktioner](device-restrictions-android-for-work.md).

Om du behöver ytterligare inställningar går du till [OEMConfig för Android Enterprise](android-oem-configuration-overview.md).

Den här artikeln beskriver hur du skapar en anpassad profil för Android Enterprise-enheter. Den innehåller också ett exempel på en anpassad profil som blockerar kopierings- och inklistringsfunktionerna.

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande inställningar:

    - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ett bra profilnamn är till exempel **Anpassad profil för Android Enterprise**.
    - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.
    - **Plattform**: Välj **Android Enterprise**.
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

## <a name="example"></a>Exempel

I det här exemplet skapar du en anpassad profil som begränsar kopierings- och inklistringsåtgärder mellan arbetsappar och personliga appar på Android Enterprise-enheter.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande inställningar:

    - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ange till exempel **android ent blockera kopiera klistra in anpassad profil**.
    - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.
    - **Plattform**: Välj **Android Enterprise**.
    - **Profiltyp**: Välj **Anpassad**.

4. I **Anpassade OMA-URI-inställningar** väljer du **Lägg till**. Ange följande inställningar:

    - **Namn**: Ange något som exempelvis `Block copy and paste`.
    - **Beskrivning**: Ange något som exempelvis `Blocks copy/paste between work and personal apps`.
    - **OMA-URI**: Ange `./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste`.
    - **Datatyp**: Välj **Booleskt** så att värdet för den här OMA-URI:n är **Sant** eller **Falskt**.
    - **Värde**: Välj **Sant**.

5. När du har angett inställningarna bör din miljö likna följande bild:

    ![Blockera kopiering och inklistring för Android-arbetsprofil.](./media/custom-settings-android-for-work/custom-policy-afw-copy-paste.png)

När du tilldelar den här profilen till Android Enterprise-enheter som du hanterar blockeras kopierings- och inklistringsfunktionerna mellan appar i arbetsprofiler och personliga profiler.

## <a name="next-steps"></a>Nästa steg

Profilen har skapats, men den gör inte något än. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Skapa en [anpassad profil på Android-enheter](custom-settings-android.md).
