---
title: Kontrollera framgångar eller misslyckanden med säkerhetsbaslinjer i Microsoft Intune – Azure | Microsoft Docs
description: Kontrollera status för fel, konflikter och framgångar när du distribuerar säkerhetsbaslinjer till användare och enheter i Microsoft Intune MDM. Se hur du felsöker med klientloggar och rapportfunktioner i Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cecd39bcba7e16cc933086c99bbc0b403381d75d
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461801"
---
# <a name="monitor-security-baselines-and-profiles-in-microsoft-intune"></a>Övervaka säkerhetsbaslinjer och profiler i Microsoft Intune

Intune tillhandahåller flera alternativ för att övervaka dina säkerhetsbaslinjer. Du kan:

- Övervaka en säkerhetsbaslinje och alla enheter som matchar (eller inte matchar) de rekommenderade värdena.
- Övervaka den profil för säkerhetsbaslinjer som gäller för dina användare och enheter.
- Visa hur inställningarna från en vald profil ställs in på en vald enhet.

Du kan också visa *konfiguration av slutpunktssäkerhet* som gäller för enskilda enheter, som innehåller säkerhetsbaslinjer.

Den här artikeln beskriver övervakningsalternativen.

[Säkerhetsbaslinjer i Intune](security-baselines.md) innehåller mer information om funktionen säkerhetsbaslinjer i Microsoft Intune.

## <a name="monitor-the-baseline-and-your-devices"></a>Övervaka baslinjen och dina enheter

När du övervakar en baslinje kan få du inblick i säkerhetstillståndet för dina enheter baserat på Microsofts rekommendationer. Om du vill visa insikterna loggar du in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), går till **Slutpunktsskydd** > **Säkerhetsbaslinjer** och väljer en säkerhetsbaslinjetyp, till exempel *Säkerhetsbaslinje för mobilenhetshantering*. Välj sedan den profilinstans som du vill visa information om i fönstret *Profil*. Detta öppnas i profilernas *egenskapsfönster* där du sedan kan välja någon av profilrapporterna i avsnittet *Övervaka*. 

Det tar upp till 24 timmar innan data visas när du först har tilldelat en baslinje. Senare ändringar tar upp till sex timmar att visas.

När du går in på rapporter och enheter är olika uppgifter tillgängliga.

<!-- UI is changing, unclear how yet: 


- **Device view** – A summary of how many devices are in each status category for the baseline.
- **Per-category** - A view that displays each category in the baseline and includes the percentage of devices for each status group for each baseline category.

Each device is represented by one of the following statuses (used in the *device* view and also the *per-category* views):

- **Matches baseline** - All the settings in the baseline match the recommended settings.
- **Does not match baseline** - One or more settings in the baseline were modified from their default values in the original baseline. The default values in each security baseline are the recommended values for that baseline.

  > [!NOTE]
  > When you create or edit a baseline profile, any change that is made to a default value or configuration setting causes a *Does not match baseline* status to occur. For help to determine the settings that were changed, contact Microsoft Support. 

- **Misconfigured** - At least one setting isn't correctly configured. This status means that the setting is in a conflict, error, or pending state.
- **Not applicable** - At least one setting isn't applicable and isn't applied.

### Device view

The Overview pane displays a chart-based summary of how many devices have a specific status for the baseline; **Security baseline posture for assigned Windows 10 devices**.

![Check the status of the devices](./media/security-baselines-monitor/overview.png)

When a device has different status from different categories in the baseline, the device is represented by a single status. The status that represents the device is taken from the following order of precedence: **Misconfigured**, **Does not match baseline**, **Not applicable**, **Matches baseline**.

For example, if a device has a setting that's classified as *misconfigured* and one or more settings that are classified as *Does not match baseline*, the device is classified as *Misconfigured*.

You can click on the chart to drill through and view a list of devices with various statuses. You can then select individual devices from that list to view details about individual devices. For example:

- Select **Device configuration** > Select the profile with an Error state:

  ![View the status of a profile](./media/security-baselines-monitor/device-configuration-profile-list.png)

- Select the Error profile. A list of all settings in the profile, and their state is shown. Now, you can scroll to find the setting causing the error:

  ![See the setting causing the error](./media/security-baselines-monitor/profile-with-error-status.png)

Use this reporting to see any settings in a profile that are causing an issue. Also get more details of policies and profiles deployed to devices.

> [!NOTE]
> When a property is set to **Not configured** in the baseline, the setting is ignored, and no restrictions are enforced. The property isn't shown in any reporting.

### Per category view

The Overview pane displays a per-category chart for the baseline named **Security baseline posture by category**.  This view displays each category from the baseline, and identifies the percentage of devices that fall into a status classification for each of those categories.

![Per-Category view of status](./media/security-baselines-monitor/monitor-baseline-per-category.png)

Status for **Matches baseline** doesn't display until 100% of devices report that status for the category.

You can sort the by-category view by each column, by selecting up-down arrow icon at the top of the column.
-->

## <a name="monitor-the-profile"></a>Övervaka profilen

Övervakning av profilen ger dig insikt i distributionsstatusen för dina enheter, men inte säkerhetsstatusen baserad på baslinjerekommendationerna.

1. I Intune väljer du **Säkerhetsbaslinjer** > välj en baslinje > för att öppna fönstret *Profiler*.

<!-- More churn  
2. Select a profile. In **Overview**, the image shows how many devices and users have this profile assigned:

   ![See how many devices and users are assigned the security baselines profile](./media/security-baselines-monitor/existing-profile-overview.png)
--> 
3. Under **Hantera** > **Egenskaper**, visas en lista över alla inställningar i baslinjen. Du kan också ändra någon av dessa inställningar:

   ![Visa och uppdatera inställningarna i profilen för säkerhetsbaslinjer](./media/security-baselines-monitor/manage-settings.png)

4. I **Övervakare**, kan du se distributionsstatusen för profilen på enskilda enheter, status för varje användare och status för varje inställning i baslinjen:

   ![Se de olika alternativen för övervakare för en profil för säkerhetsbaslinjer](./media/security-baselines-monitor/monitor-status-options.png)

## <a name="view-settings-from-profiles-that-apply-to-a-device"></a>Visa inställningar från profiler som gäller för en enhet

Du kan välja en profil för en säkerhetsbaslinje och visa en detaljerad lista över inställningar från profilen som de gäller för en enskild enhet.  Om du vill visa listan går du till **Slutpunktsskydd** > **Säkerhetsbaslinjer** >  *, väljer säkerhetsbaslinjetypen*  > *och väljer profilen du vill visa* > **Enhetsstatus** för. Du kan också visa listan genom att gå till **Slutpunktsskydd** > **Alla enheter** > *välja en enhet* > **Konfiguration av slutpunktssäkerhet** > *välja en baslinjeversion*.

När du har valt en enhet visar administrationscentret för Microsoft Endpoint Manager en lista över inställningarna från profilen, inklusive den kategori som inställningen är från, och konfigureringstillståndet på enheten. Konfigureringstillstånd innehåller följande värden:

- **Klart** – Inställningen på enheten matchar värdet enligt konfigurationen i profilen. Detta är antingen standardbaslinjen och det rekommenderade värdet, eller ett anpassat värde som angavs av en administratör när profilen konfigurerades.
- **Konflikt** – Inställningen är i konflikt med en annan princip, innehåller ett fel eller väntar på en uppdatering.
- **Inte tillämpligt** – Inställningen är inte tillämpad av profilen.

> [!NOTE]
> Statusvärden för inställningarna uppdateras i en framtida version för att ge mer detaljerad information.

## <a name="view-endpoint-security-configurations-per-device"></a>Visa konfiguration av slutpunktssäkerhet per enhet

Visa information om de säkerhetskonfigurationer som gäller för en enskild enhet. Detta kan hjälpa dig att isolera inställningar som är felkonfigurerade.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Gå till **Enheter** > **Alla enheter** och välj den enhet du vill visa.

3. I kategorin *Övervakare* väljer du **Konfiguration av slutpunktssäkerhet** för att visa en lista över säkerhetskonfigurationer som gäller för enheten.

4. Du kan välja en konfiguration för slutpunktssäkerhet om du vill visa mer information om utvärderingen av den säkerhetskonfigurationen på enheten.

## <a name="troubleshoot-using-per-setting-status"></a>Felsök med hjälp av status per inställning

Du har distribuerat en säkerhetsbaslinje, men distributionsstatusen visar ett fel. I följande steg får du vägledning om hur du felsöker felet.

1. I Intune väljer du **Säkerhetsbaslinjer** > väljer en baslinje > **Profiler**.

2. Välj en profil > under **Övervakare** > **Status per inställning**.

3. Tabellen visar alla inställningar och status för varje inställning. Välj kolumnen **Fel** eller **Konflikt** för att se inställningen som orsakar felet.

### <a name="mdm-diagnostic-information"></a>MDM-diagnostikinformation

Nu vet du vilken den problematiska inställningen är. Nästa steg är att ta reda på varför den här inställningen orsakar ett fel eller en konflikt.

På Windows 10-enheter finns det en inbyggd rapport för MDM-diagnostikinformation. Den här rapporten innehåller standardvärden, aktuella värden, visar en lista över principen, visar om den har distribuerats till enheten eller användaren och mycket mer. Använd den här rapporten för att avgöra varför inställningen orsakar en konflikt eller ett fel.

1. På enheten, gå till **Inställningar** > **Konton** > **Åtkomst till arbete eller skola**.

2. Välj kontot > **Info** > **Avancerad diagnostikrapport** > **Skapa rapport**.

3. Välj **Exportera** och öppna den genererade filen.

4. I rapporten kan du leta efter fel- eller konfliktinställningen i de olika avsnitten i rapporten.

  Titta till exempel i avsnittet **Registrerade konfigurationskällor och målresurser** eller **Ohanterade principer**. Du kan få en uppfattning om varför den orsakar ett fel eller en konflikt.

[Diagnostisera fel i MDM i Windows 10](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10) ger mer information om den här inbyggda rapporten.

> [!TIP]
>
> - Vissa inställningar visar även GUID. Du kan söka efter detta GUID i det lokala registret (regedit) för alla inställda värden.
> - Loggboken kan också innehålla viss felinformation om den problematiska inställningen (**Loggboken** > **Applikationer och tjänsteloggar** >  **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider** > **Admin**).

## <a name="next-steps"></a>Nästa steg

- [Läs mer om säkerhetsbaslinjer](security-baselines.md)
- [Undvika konflikter](security-baselines.md#avoid-conflicts)
- [Övervaka enhetsprofiler](../configuration/device-profile-monitor.md) 
- [Vanliga problem och lösningar](../configuration/device-profile-troubleshoot.md).
- [Felsöka principer och profiler i Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)