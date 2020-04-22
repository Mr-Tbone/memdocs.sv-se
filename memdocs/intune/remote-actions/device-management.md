---
title: Hantera enheter med Microsoft Intune – Azure | Microsoft Docs
description: Granska de enheter du hanterar med Microsoft Intune. Du kan exportera en enhetslista i csv-format, visa dina Azure Active Directory-anslutna enheter, granska en ändringslogg över åtgärder på enheten, använda TeamViewer-anslutningsprogrammet så att IT-administratörer via fjärranslutning kan felsöka Android-enheter samt visa alla åtgärder som du kan köra på dina enheter.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/14/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d2412418-d91a-4767-a3d6-bc88bb29caa2
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 98451e7ffd6aef9e5fb298af96b91074f39c383e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80325274"
---
# <a name="what-is-microsoft-intune-device-management"></a>Vad är enhetshantering i Microsoft Intune?

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Som IT-administratör måste du se till att hanterade enheter tillhandahåller de resurser som användarna behöver för att utföra sitt arbete, samtidigt som du måste skydda dessa data så att de inte utsätts för risk.

Arbetsbelastningen **Enheter** ger dig insikter om de enheter du hanterar och gör att du kan aktivera fjärråtgärder på dessa enheter.

## <a name="get-to-your-devices"></a>Kom åt dina enheter

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Välj **Enheter**. Den här vyn visar detaljerad information om enskilda enheter och vad du kan göra med dem, inklusive:

   - **Översikt** visar en visuell ögonblicksbild av de registrerade enheterna, hur många enheter som använder de olika plattformarna och mer.
   - **Alla enheter** visar en lista över de registrerade enheter du hanterar.

     Använd funktionen **Exportera** för att skapa en .zip-lista över alla enheter i steg om 10 000 (Internet Explorer) eller 30 000 (Microsoft Edge, Chrome).

     Välj valfri enhet för att [visa ytterligare information om enheten](device-inventory.md), till exempel maskinvaruinformation, installerade appar, principer och mer.

   - **Azure AD-enheter** visar en lista över de enheter som registrerats för eller anslutits till Azure Active Directory (Azure AD). Läs mer om [Azure AD-enhetshantering](https://docs.microsoft.com/azure/active-directory/device-management-introduction).
   - **Enhetsåtgärder** omfattar en historik över de fjärråtgärder som körts på olika enheter, däribland åtgärden, dess status, vem som startade åtgärden och när den utfördes.

     ![Skärmbild som visar när enhetsåtgärder övervakas](./media/device-management/monitor-device-actions.png)

   - **Granskningsloggar** är en post med aktiviteter som genererar en ändring i Intune. [Granskningsloggar](../fundamentals/monitor-audit-logs.md) innehåller mer information.
   - **TeamViewer-anslutningsprogram** är en tjänst som gör att användare av Intune-hanterade Android-enheter kan få fjärrhjälp från sin IT-administratör. Läs mer om [TeamViewer](teamviewer-support.md).
   - **Hjälp och Support** innehåller en genväg till felsökningstips, att begära support eller kontrollera status för Intune.

## <a name="available-device-actions"></a>Tillgängliga enhetsåtgärder
Vilka åtgärder som är tillgängliga beror på enhetsplattformen och enhetens konfiguration.

- [Visa enhetsinventeringen](device-inventory.md)
- Kör åtgärder för fjärransluten enhet:
  - [Autopilot-återställning](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
  - [BitLocker Key-rotation](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) (endast Windows)
  - [Ta bort](devices-wipe.md#delete-devices-from-the-intune-portal)
  - [Inaktivera aktiveringslås](device-activation-lock-disable.md) (Endast iOS)
  - [Börja om på nytt](device-fresh-start.md) (Endast Windows)
  - [Fullständig genomsökning](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) (endast Windows 10)
  - [Hitta enhet](device-locate.md) (Endast iOS)
  - [Borttappat läge](device-lost-mode.md) (Endast iOS)
  - [Snabbsökning](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) (endast Windows 10)
  - [Fjärrstyrning för Android](teamviewer-support.md)
  - [Fjärrlåsning](device-remote-lock.md)
  - [Byta namn på en enhet](device-rename.md)
  - [Återställ lösenord](device-passcode-reset.md)
  - [Starta om](device-restart.md) (Endast Windows)
  - [Pensionera](devices-wipe.md#retire)
  - [Uppdatera Windows Defender-säkerhetsinformation](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/manage-protection-updates-windows-defender-antivirus)
  - [PIN-återställning av Windows 10](device-windows-pin-reset.md)
  - [Rensning](devices-wipe.md#wipe)
  - [Skicka anpassade meddelanden](custom-notifications.md#send-a-custom-notification-to-a-single-device) (Android, iOS/iPadOS)
  - [Synkronisera enhet](device-sync.md)
- [Massenhetsåtgärder](bulk-device-actions.md)

## <a name="next-steps"></a>Nästa steg

- Välj en enhet för att visa mer information om den här enheten i **Alla enheter**.
- Välj **Enhetsåtgärder** för att se status för de åtgärder som vidtas på enheter som du hanterar.
