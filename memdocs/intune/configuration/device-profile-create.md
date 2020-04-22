---
title: Skapa enhetsprofiler i Microsoft Intune – Azure | Microsoft Docs
description: Lägg till eller konfigurera en enhetskonfigurationsprofil i Microsoft Intune. Välj plattformstyp, konfigurera inställningarna och lägg till en omfångstagg.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d98aceff-eb35-4e3e-8e40-5f300e7335cc
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c2031ba23b49bda4890d2638272e3b808b4bf5a9
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327444"
---
# <a name="create-a-device-profile-in-microsoft-intune"></a>Skapa en enhetsprofil i Microsoft Intune

Med enhetsprofiler kan du lägga till och konfigurera inställningar och sedan skicka dem till enheter i din organisation. [Tillämpa funktioner och inställningar på dina enheter med enhetsprofiler](device-profiles.md) innehåller mer information, inklusive vad du kan göra.

Den här artikeln:

- Se hur du skapar en profil.
- Visar hur du lägger till en omfångstagg för att ”filtrera” profilen.
- Beskriver tillämplighetsregler för Windows 10-enheter och visar hur du skapar en regel.
- Visar en lista med incheckningstider för uppdateringscykeln när enheterna tar emot profiler och eventuella profiluppdateringar.

## <a name="create-the-profile"></a>Skapa profilen

Profiler skapas i [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). I det här administrationscentret väljer du **Enheter**. Du kan välja mellan följande alternativ:

- **Översikt**: Visar status för dina profiler och ytterligare information om de profiler som du har tilldelat till användare och enheter.
- **Övervaka**: Kontrollera status och visa loggar för dina profiler.
- **Per plattform**: Skapa och visa principer och profiler för din plattform. Den här vyn kan också visa funktioner som är specifika för plattformen. Välj exempelvis **Windows**. Då visas Windows-specifika funktioner, till exempel **Windows 10-uppdateringsringar** och **PowerShell-skript**.
- **Princip**: Skapa enhetsprofiler, ladda upp anpassade [PowerShell-skript](../apps/intune-management-extension.md) att köra på enheter och lägg till dataplaner för enheter med hjälp av [eSIM](esim-device-configuration.md).

När du skapar en profil (**konfigurationsprofiler** > **Skapa profil**) väljer du din plattform:

- **Android-enhetsadministratör**
- **Android enterprise**
- **iOS/iPadOS**
- **macOS**
- **Windows 10 och senare**
- **Windows 8.1 och senare**
- **Windows Phone 8.1**

Välj sedan profiltyp. Vilka inställningar du kan konfigurera varierar beroende på vilken plattform du väljer. I följande artiklar beskrivs inställningarna för de olika profiltyperna:

- [Administrativa mallar (Windows)](administrative-templates-windows.md)
- [Anpassad](custom-settings-configure.md)
- [Leveransoptimering (Windows)](delivery-optimization-windows.md)
- [Härledd autentiseringsuppgift (Android Enterprise, iOS, iPadOS)](../protect/derived-credentials.md)
- [Enhetsfunktioner (macOS, iOS, iPadOS)](device-features-configure.md)
- [Inbyggd programvara för enhet (Windows)](device-firmware-configuration-interface-windows.md)
- [Enhetsbegränsningar](device-restrictions-configure.md)
- [Domänanslutning (Windows)](domain-join-configure.md)
- [Versionsuppgradering och lägesväxling (Windows)](edition-upgrade-configure-windows-10.md)
- [Utbildning (iOS, iPadOS)](../fundamentals/education-settings-configure-ios.md)
- [E-post](email-settings-configure.md)
- [Slutpunktsskydd: (macOS, Windows)](../protect/endpoint-protection-configure.md)
- [Tillägg: (macOS)](kernel-extensions-overview-macos.md)
- [Identitetsskydd (Windows)](../protect/identity-protection-configure.md)
- [Helskärmsläge](kiosk-settings.md)
- [Microsoft Defender ATP (Windows)](../protect/advanced-threat-protection.md)
- [Profil för Mobility Extensions (MX) (Android-enhetsadministratör)](android-zebra-mx-overview.md)
- [OEMConfig (Android Enterprise)](android-oem-configuration-overview.md)
- [PKCS-certifikat](../protect/certficates-pfx-configure.md)
- [PKCS-importerat certifikat](../protect/certificates-imported-pfx-configure.md)
- [Inställningsfil: (macOS)](preference-file-settings-macos.md)
- [SCEP-certifikat](../protect/certificates-scep-configure.md)
- [Säker utvärdering (utbildning) (Windows)](education-settings-configure.md)
- [Delad enhet för flera användare (Windows)](shared-user-device-settings.md)
- [Telekom-utgifter (Android-enhetsadministratör, iOS, iPadOS)](telecom-expenses-monitor.md)
- [Betrott certifikat](../protect/certificates-configure.md)
- [VPN](vpn-settings-configure.md)
- [Wi-Fi](wi-fi-settings-configure.md)

Om du till exempel väljer **iOS/iPadOS** som plattform, ser alternativen för profiltypen ut ungefär så här:

> [!div class="mx-imgBorder"]
> ![Skapa iOS/iPadOS-profil i Intune](./media/device-profile-create/create-device-profile.png)

## <a name="scope-tags"></a>Omfångstaggar

När du har lagt till inställningarna kan du också lägga till en omfångstagg i profilen. Omfångstaggar filtrerar profiler till vissa IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Och används i distribuerad IT.

Mer information om omfångstaggar och vad du kan göra finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

## <a name="applicability-rules"></a>Tillämpbarhetsregler

Gäller för:

- Windows 10 och senare

Med tillämplighetsregler kan administratörer rikta in sig på enheter i en grupp som uppfyller specifika villkor. Du kan till exempel skapa en profil för enhetsbegränsningar som gäller för gruppen **Alla Windows 10-enheter**. Och du vill att profilen endast ska tilldelas till enheter som kör Windows 10 Enterprise.

För att utföra den här åtgärden skapar du en **tillämpbarhetsregel**. Dessa regler är utmärkta för följande scenarier:

- Du använder Windows 10 Education (EDU). På universitetet Bellows College vill du sikta på alla Windows 10 EDU-enheter mellan RS3 och RS4.
- Du vill rikta in dig på alla användare i personalavdelningen på Contoso, men endast de enheter som kör Windows 10 Professional eller Enterprise.

För att du ska kunna nå dessa scenarier kan du:

- Skapa en enhetsgrupp som innehåller alla enheter på Bellows College. Lägg till en tillämplighetsregel i profilen så att den gäller om lägsta operativsystemversion är `16299` och den högsta versionen är `17134`. Tilldela den här profilen till enhetsgruppen Bellows College.

  När den är tilldelad gäller profilen för enheter mellan de lägsta och högsta versionerna som du anger. För enheter som inte är mellan de lägsta och högsta versionerna som du anger visas statusen som **Ej tillämpligt**.

- Skapa en användargrupp som omfattar alla användare i personalavdelningen (HR) på Contoso. Lägg till en tillämpbarhetsregel i profilen så att den gäller för enheter som kör Windows 10 Professional eller Enterprise. Tilldela den här profilen till gruppen HR-användare.

  När den är tilldelad tillämpas profilen på enheter som kör Windows 10 Professional eller Enterprise. För enheter som inte kör dessa versioner visas deras status som **Ej tillämpliga**.

- Om det finns två profiler med exakt samma inställningar tillämpas profilen utan en tillämplighetsregel. 

  Till exempel, ProfileA är riktad mot enhetsgruppen med Windows 10, aktiverar BitLocker och har inte någon tillämplighetsregel. ProfileB är riktad mot samma Windows 10-enhetsgrupp, aktiverar BitLocker och har en tillämplighetsregel för att endast tillämpa profilen på Windows 10 Enterprise.

  När båda profilerna tilldelas tillämpas ProfileA eftersom den inte har en tillämplighetsregel. 

När du tilldelar profilen till grupperna fungerar tillämplighetsreglerna som ett filter så att profilen endast tillämpas på de enheter som uppfyller dina kriterier.

### <a name="add-a-rule"></a>Lägg till en regel

1. Välj **Tillämpbarhetsregler**. Du kan välja **Regel**, **Egenskap** och **OS-utgåva**:

    > [!div class="mx-imgBorder"]
    > ![Lägg till en tillämplighetsregel till en enhetskonfigurationsprofil i Microsoft Intune](./media/device-profile-create/applicability-rules.png)

2. I **Regel** väljer du om du vill inkludera eller exkludera användare eller grupper. Alternativen är:

    - **Tilldela profil om**: Innehåller användare eller grupper som uppfyller de kriterier som du anger.
    - **Tilldela inte en profil om**: Exkluderar användare eller grupper som uppfyller de kriterier som du anger.

3. I **Egenskap** väljer du ditt filter. Alternativen är: 

    - **Operativsystemutgåva**: I listan markerar du de Windows 10-versioner som du vill inkludera (eller exkludera) i din regel.
    - **Operativsystemversion**: Ange det **lägsta** och **högsta** versionnumret för Windows 10 som du vill inkludera (eller exkludera) i din regel. Båda värdena måste anges.

      Du kan till exempel ange `10.0.16299.0` (RS3 eller 1709) för lägsta version och `10.0.17134.0` (RS4 eller 1803) för högsta version. Eller så kan du vara mer ingående och ange `10.0.16299.001` för lägsta version och `10.0.17134.319` för högsta version.

4. Välj **Lägg till** för att spara dina ändringar.

## <a name="refresh-cycle-times"></a>Uppdatera cykeltider

Intune använder olika uppdateringscykler till att söka efter uppdateringar av konfigurationsprofiler. Om enheten nyligen har registrerats körs incheckningarna oftare. [Princip-och profil uppdaterings cykler](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) visar de uppskattade uppdateringstiderna.

Användarna kan när de vill öppna företagsportalappen och synkronisera enheten för att söka efter profiluppdateringar.

## <a name="recommendations"></a>Rekommendationer

När du skapar profiler bör du tänka på följande rekommendationer:

- Namnge dina principer så att du vet vad de är och vad de gör. Alla [efterlevnadsprinciper](../protect/create-compliance-policy.md) och [konfigurationsprofiler](../configuration/device-profile-create.md) har en valfri **Beskrivnings**egenskap. Var specifik och inkludera information som beskriver profilen för andra personer i **Beskrivning**.

  Några exempel på konfigurationsprofiler är:

  **Profilnamn**: Adminmall – konfigurationsprofil för OneDrive för alla Windows 10-användare  
  **Profilbeskrivning**: Mallprofil för OneDrive-administratör som innehåller minimi- och basinställningar för alla Windows 10-användare. Skapad av user@contoso.com för att hindra användare från att dela organisationsdata till personliga OneDrive-konton.

  **Profilnamn**: VPN-profil för alla iOS/iPadOS-användare  
  **Profilbeskrivning**: VPN-profil som innehåller minimi- och basinställningar för alla iOS/iPadOS-användare som ansluter sig till Contosos VPN. Skapas av user@contoso.com så att användarna autentiseras automatiskt på VPN i stället för att uppmana användarna att ange sina användarnamn och lösenord.

- Skapa din profil efter dess uppgift, till exempel konfigurera Microsoft Edge-inställningar, aktivera Microsoft Defender Antivirus-inställningar, blockera olåsta iOS/iPadOS-enheter och så vidare.

- Skapa profiler som gäller för vissa grupper, till exempel marknadsföring, försäljning, IT-administratörer eller enligt plats eller skolsystem.

- Skilj användarprinciper från enhetsprinciper.

  [Administrativa mallar i Intune](administrative-templates-windows.md) har till exempel hundratals ADMX-inställningar. Dessa mallar visar om en inställning gäller för användare eller enheter. När du skapar administrativa mallar tilldelar du användarinställningarna till en användargrupp och tilldelar enhetsinställningarna till en enhetsgrupp.

  Följande bild visar ett exempel på en inställning som kan gälla för användare och/eller tillämpas på enheter:

  > [!div class="mx-imgBorder"]
  > ![Intune-administratörsmall som tillämpas på användare och enheter](./media/device-profile-create/setting-applies-to-user-and-device.png)

- Varje gång du skapar en begränsad princip bör du informera användarna om detta. Om du till exempel vill ändra lösenordskravet från 4 tecken till 6 tecken, meddelar du användarna detta innan du tilldelar principen.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
