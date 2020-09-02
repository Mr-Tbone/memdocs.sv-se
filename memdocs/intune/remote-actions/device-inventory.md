---
title: Visa enhetsinformation med Microsoft Intune – Azure | Microsoft Docs
description: Visa information om din enhet, till exempel operativsystem, lagringsutrymme, tillverkare och modell. Hämta en lista över installerade appar, kontrollera efterlevnadsprinciper och konfigurera TeamViewer med Microsoft Intune i Azure. Det fungerar ungefär som när du visar en inventering av de enheter som du hanterar.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e71c6bdb-d75c-404f-8e38-24a663be81c2
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e6aa3c887a22c468d8d482ce2d4ba0da8202fceb
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88906828"
---
# <a name="see-device-details-in-intune"></a>Visa enhetsinformation i Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Funktionen **Enheter** tillhandahåller ytterligare information om de enheter som du hanterar, inklusive deras maskinvara och installerade appar.

Den här artikeln beskriver hur du visar alla dina enheter och deras egenskaper i Azure Portal.

## <a name="view-the-device-details"></a>Visa enhetsinformation

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Välj **Enheter** > **Alla enheter** > välj en av enheterna i listan för att öppna informationen:

   - I **Översikt** visas namnet på enheten och några viktiga egenskaper, bland annat om det är en personlig enhet eller företagsenhet, serienummer, primär användare och annat. Du kan göra följande på enheten:
      - [Pensionera](devices-wipe.md#retire)
      - [Rensning](devices-wipe.md#wipe)
      - [Ta bort](devices-wipe.md#delete-devices-from-the-intune-portal)
      - [Fjärrlåsning](device-remote-lock.md)
      - [Synkronisera](device-sync.md)
      - [Återställ lösenord](device-passcode-reset.md)
      - [Starta om](device-restart.md) (Endast Windows)
      - [Börja om på nytt](device-fresh-start.md) (Endast Windows)
      - [Autopilot-återställning](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset) (endast Windows)
      - [Snabbsökning](../configuration/device-restrictions-windows-10.md) (endast Windows 10)
      - [Fullständig genomsökning](../configuration/device-restrictions-windows-10.md) (endast Windows 10)
      - [Uppdatera Windows Defender-säkerhetsinformation](/windows/security/threat-protection/microsoft-defender-antivirus/manage-protection-updates-microsoft-defender-antivirus)
      - [BitLocker-nyckelrotering](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key)
      - [Byta namn på en enhet](device-rename.md)
      - [Ny fjärrhjälpsession](./teamviewer-support.md)
   - Använd **Egenskaper** för att tilldela en [enhetskategori som du skapar](../enrollment/device-group-mapping.md), samt för att ändra ägarskap för enheten till en personlig enhet eller företagets enhet.
   - **Maskinvara** innehåller mycket information om enheten, till exempel enhets-ID, operativsystem och version, lagringsutrymme och mer information.
   - **Identifierade appar** visar alla installerade appar på enheten som Intune hittat och deras versioner. Mer information finns i [Appar som identifieras i Intune](../apps/app-discovered-apps.md).
   - **Enhetsefterlevnad** visar alla tilldelade efterlevnadsprinciper, samt om enheten är kompatibel eller inkompatibel.
   - **Enhetskonfiguration** visar alla enhetskonfigurationsprinciper som är tilldelade till enheten, samt om principen har lyckats eller misslyckats.
   - **Appkonfiguration** 
   - **Konfiguration av slutpunktssäkerhet**
   - **Återställningsnycklar** visar tillgängliga BitLocker-nycklar som hittades för enheten
   - **Hanterade appar** visar en lista över alla hanterade appar som Intune har konfigurerat och som har distribuerats till enheten. 

## <a name="hardware-device-details"></a>Information om maskinvaruenheten
Eventuellt samlas inte all information in, beroende på vilken operatör enheterna använder

> [!Note]  
> Maskin- och programvaruinventeringen uppdateras i Intune-tjänsten var sjunde dag.

|Information|Beskrivning|Plattform| 
|--------------|----------------------|----|  
|Name|Namnet på enheten.|Windows, iOS|
|Hanteringsnamn|Enhetsnamnet används endast i konsolen. Även om du ändrar det här namnet ändras inte namnet på enheten.|Windows, iOS|
|UDID|Enhetens unika enhets-ID.|Windows, iOS|
|ID för Intune-enhet|Ett GUID som unikt identifierar den här enheten.|Windows, iOS|
|Serienummer|Enhetens serienummer från tillverkaren.|Windows, iOS|
|Delad enhet|Enheten delas av flera användare om inställningen är **Ja**.|Windows, iOS|
|Användargodkänd registrering|Enheten har användargodkänd registrering som gör att administratörer kan hantera vissa säkerhetsinställningar på enheten om inställningen är **Ja**.|Windows, iOS|
|Operativsystem|Vilken typ av operativsystem som används på enheten.|Windows, iOS|
|Operativsystemversion|Enhetens operativsystemversion.|Windows, iOS|
|Operativsystemets språk|Språket som är inställt på enhetens operativsystem.|Windows, iOS|
|Versionsnummer|Operativ systemets versionsnummer.|Android|
|Säkerhetskorrigeringsnivå|Säkerhetskorrigeringsnivå för enheten.|Android|
|Totalt lagringsutrymme|Det totala lagringsutrymmet på enheten (i gigabyte).|Windows, iOS|
|Ledigt lagringsutrymme|Det oanvända lagringsutrymmet på enheten (i gigabyte).|Windows, iOS|
|IMEI|Enhetens IMEI (International Mobile Equipment Identity).|Windows, iOS/iPadOS, Android|
|MEID|Enhetens mobilutrustningsnummer.|Windows, iOS/iPadOS, Android|
|Tillverkare|Enhetstillverkaren.|Windows, iOS/iPadOS, Android|
|Modell|Enhetsmodellen.|Windows, iOS/iPadOS, Android|
|Telefonnummer|Telefonnumret som har tilldelats enheten.|Windows, iOS/iPadOS, Android*|
|Abonnentens operatör|Enhetens mobiloperatör.|Windows, iOS/iPadOS, Android|
|Mobilteknik|Radiosystem som används av enheten.|Windows, iOS/iPadOS, Android|
|Wi-Fi MAC|Enhetens MAC-adress.|Windows, iOS/iPadOS, Android|
|ICCID|Det integrerade kretskort-ID:t som är ett unikt ID-nummer för ett SIM-kort.|Windows, iOS/iPadOS, Android|
|Registreringsdatum|Datum och tid då enheten registrerades i Intune.|Windows, iOS/iPadOS, Android|
|Senaste kontakt|Datum och tid då enheten senast var i kontakt med Intune.|Windows, iOS/iPadOS, Android|
|Kod för att kringgå aktiveringslås|Koden som kan användas för att inaktivera aktiveringslåset.|iOS|
|Azure AD-registrerad|Om inställningen är **Ja** är enheten registrerad i Azure Directory.|Windows, iOS/iPadOS, Android|
|Intune-registrerad|Om inställningen är **Ja** är enheten registrerad i Intune|Windows, iOS/iPadOS, Android|
|Efterlevnad|Enhetens kompatibilitetstillstånd.|Windows, iOS/iPadOS, Android|
|EAS-aktiverad|Om inställningen är **Ja** så är enheten synkroniserad med en Exchange-postlåda.|Windows, iOS/iPadOS, Android|
|Aktiverings-ID för EAS|Enhetens identifierare för Exchange ActiveSync.|Windows, iOS/iPadOS, Android|
|Övervakas|Om inställningen är **Ja** så har administratörer utökad kontroll över enheten.|Windows, iOS/iPadOS, Android|
|Krypterad|Om inställningen är **Ja** så krypteras de data som lagras på enheten.|Windows, iOS/iPadOS, Android|

> [!Note]  
> Telefonnumret har inte inventerats på Android Enterprise-dedikerade enheter eller fullständigt hanterade enheter.

## <a name="next-steps"></a>Nästa steg
Se vad mer du kan göra för att [hantera dina enheter](device-management.md) med Intune.