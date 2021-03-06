---
title: Anpassad per app-VPN-profil för Android-enhetsadministratör i Microsoft Intune – Azure | Microsoft Docs
description: Använd en anpassad profil för per app-VPN-profiler för Android-enhetsadministratören med anslutningstyperna Pulse Secure eller Citrix VPN i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/22/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d035ebf5-85f4-4001-a249-75d24325061a
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c8e09b6010f7fc846fd81281053eaaa722e5ef4
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262803"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Använd en anpassad Microsoft Intune-profil för att skapa en VPN-profil per app för Android-enheter

Du kan skapa en VPN-profil per app för enheter som kör Android 5.0 och senare som hanteras av Intune. Börja med att skapa en VPN-profil som använder antingen Pulse Secure- eller Citrix-anslutningstypen. Skapa sedan en princip för anpassad konfiguration som associerar VPN-profilen med specifika appar.

Den här funktionen gäller för:

- Android-enhetsadministratör

Om du vill använda per app-VPN på Android Enterprise-enheter, så använd en [appkonfigurationsprincip](../apps/app-configuration-vpn-ae.md). Konfigurationsprinciper för appar stöder fler VPN-klientappar. På Android Enterprise-enheter kan du följa stegen i den här artikeln. Men vir rekommenderar inte detta, och du är begränsad till endast Pulse Secure- och Citrix VPN-anslutningar.

När du har tilldelat principen till din Android-enhet eller till användargrupper måste användarna starta Pulse Secure- eller Citrix VPN-klienten. Därefter tillåter VPN-klienten endast trafik från de angivna apparna att använda den öppna VPN-anslutningen.

> [!NOTE]
>
> Endast anslutningstyperna Pulse Secure och Citrix stöds för Android-enhetsadministratörer. Använd en [appkonfigurationsprincip](../apps/app-configuration-vpn-ae.md) på Android Enterprise-enheter.

## <a name="step-1-create-a-vpn-profile"></a>Steg 1: Skapa en VPN-profil

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

    - **Plattform**: Välj **Android-enhetsadministratör**.
    - **Profil**: Välj **VPN**.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ett exempel på ett bra profilnamn är t.ex. **Android device administrator per-app VPN profile for entire company** (VPN-profil per app för Android-enhetsadministratör för hela företaget).
    - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.
7. I **Konfigurationsinställningar**konfigurerar du de inställningar som du vill använda i profilen:

    - [VPN-inställningar för Android-enhetsadministratörs enheter](vpn-settings-android.md).

    Notera **anslutningens namn** , det vill säga det värde som du anger när du skapar VPN-profilen. Detta namn krävs i nästa steg. I det här exemplet är anslutningsnamnet **MyAppVpnProfile**.

8. Välj **Nästa** och fortsätt att skapa din profil. Mer information finns i [Skapa en VPN-profil](vpn-settings-configure.md#create-the-profile).

## <a name="step-2-create-a-custom-configuration-policy"></a>Steg 2: Skapa en anpassad konfigurationsprincip

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

    - **Namn**: Ange ett beskrivande namn för den anpassade profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ett exempel på ett bra profilnamn är **Custom OMA-URI Android VPN profile for entire company** (Anpassad OMA-URI VPN-profil för Android för hela företaget).
    - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.
    - **Plattform**: Välj **Android-enhetsadministratör**.
    - **Profiltyp**: Välj **Anpassad**.

4. Välj **Inställningar** > **Konfigurera**.
5. I fönstret **Anpassade OMA-URI-inställningar** väljer du **Lägg till**.
    - **Namn**: Ange ett namn för inställningen.
    - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.
    - **OMA-URI**: Ange `./Vendor/MSFT/VPN/Profile/*Name*/PackageList`, där *Namn* är anslutningsnamnet som du antecknade i steg 1. I det här exemplet är strängen `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList`.
    - **Datatyp**: Ange **String**.
    - **Värde**: Ange en semikolonavgränsad lista med paket som ska associeras med profilen. Om du till exempel vill att Excel och webbläsaren Google Chrome ska använda VPN-anslutningen anger du `com.microsoft.office.excel;com.android.chrome`.

    :::image type="content" source="./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png" alt-text="Anpassad princip för Android-enhetsadministratör per-app VPN i Microsoft Intune":::

### <a name="set-your-blocked-and-allowed-app-list-optional"></a>Konfigurera listan över blockerade och tillåtna appar (valfritt)

Du kan ange en lista över appar som *inte* kan använda VPN-anslutningen med hjälp av värdet **BLACKLIST** (svartlistat). Alla andra appar ansluter via VPN. Eller så kan du använda värdet **WHITELIST** (vitlistat) för att ange en lista över appar som *får* använda VPN-anslutningen. Appar som inte finns med i listan ansluter inte via VPN-anslutningen.

1. I fönstret **Anpassade OMA-URI-inställningar** väljer du **Lägg till**.
2. Ange ett namn på inställningen.
3. I **OMA-URI** anger du `./Vendor/MSFT/VPN/Profile/*Name*/Mode`, där *Namn* är det VPN-profilnamn som du antecknade i steg 1. I vårt exempel är strängen `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode`.
4. I **Datatyp** anger du **String**.
5. Under **Värde** anger du **SVARTLISTAT** eller **VITLISTAT**.

## <a name="step-3-assign-both-policies"></a>Steg 3: Tilldela båda principerna

[Tilldela båda enhetsprofilerna](device-profile-assign.md) till nödvändiga användare eller enheter.

## <a name="next-steps"></a>Nästa steg

- En lista över alla VPN-inställningar för Android-enhetsadministratörer finns i [Inställningar för Android-enhet för att konfigurera VPN](vpn-settings-android.md).
- I dokumentationen om hur du [konfigurerar VPN-inställningar i Microsoft Intune](vpn-settings-configure.md) hittar du mer information om VPN-inställningar och Intune.
