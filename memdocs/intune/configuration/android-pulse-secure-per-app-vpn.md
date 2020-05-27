---
title: Per-app-anpassad VPN-profil för Android i Microsoft Intune – Azure | Microsoft Docs
description: Läs mer om att skapa en VPN-profil per app för Android-enhetsadministratörers enheter som hanteras av Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
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
ms.openlocfilehash: 367ac927650ebf08c245b1ff554ad01db3bf3792
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990160"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Använd en anpassad Microsoft Intune-profil för att skapa en VPN-profil per app för Android-enheter

Du kan skapa en VPN-profil per app för enheter som kör Android 5.0 och senare som hanteras av Intune. Börja med att skapa en VPN-profil som använder antingen Pulse Secure- eller Citrix-anslutningstypen. Skapa sedan en princip för anpassad konfiguration som associerar VPN-profilen med specifika appar.

> [!NOTE]
> Om du vill använda VPN per app på Android Enterprise-enheter kan du också använda de här stegen. Men vi rekommenderar att du använder en [konfigurationsprincip för appar](../apps/app-configuration-policies-use-android.md) för VPN-klientprogramvaran.

När du har tilldelat principen till din Android-enhet eller till användargrupper måste användarna starta Pulse Secure- eller Citrix VPN-klienten. Därefter tillåter VPN-klienten endast trafik från de angivna apparna att använda den öppna VPN-anslutningen.

> [!NOTE]
>
> Endast anslutningstyperna Pulse Secure och Citrix stöds för den här profilen.

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

    > [!div class="mx-imgBorder"]
    >![Exempel på anpassad princip för VPN per app för Android-enhetsadministratör](./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png)

### <a name="set-your-app-list-to-blacklist-or-whitelist-optional"></a>Ange applistan som svartlistad eller vitlistad (valfritt)

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
