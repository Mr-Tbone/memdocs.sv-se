---
title: Registrera iOS/iPadOS-enheter i Intune
titleSuffix: Microsoft Intune
description: Konfigurera registrering av iOS/iPadOS-enheter i Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 439c33a6-e80c-4da9-ba09-a51fc36f62ad
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f3964ec67c9c78e5aedc70ff4f328a66c59c04b
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80696530"
---
# <a name="enroll-iosipados-devices-in-intune"></a>Registrera iOS/iPadOS-enheter i Intune

Intune stöder hantering av mobila enheter (MDM) för iPad och iPhone och ger användarna säker åtkomst till företagets e-post, data och appar.

Som Intune-administratör kan du konfigurera registrering för iOS/iPadOS- och iPadOS-enheter så att du får åtkomst till företagets resurser. Du kan låta användare registrera personligt ägda enheter, även kallat BYOD-registrering (Bring Your Own Device). Du kan också konfigurera registrering av företagsägda enheter.

## <a name="prerequisites-for-iosipados-enrollment"></a>Krav för iOS/iPadOS-registrering

Innan du kan aktivera iOS/iPadOS-enheter måste du göra följande:

- [Kontrollera att enheten är kvalificerad för registrering av Apple-enheter](https://support.apple.com/en-us/HT204142#eligibility).
- [Konfigurera Intune](../fundamentals/setup-steps.md) - följande steg konfigurerar din Intune-infrastruktur. I synnerhet kräver registrering av enheter att du [anger en MDM-utfärdare](../fundamentals/mdm-authority-set.md).
- [Hämta ett certifikat för Apple MDM Push](apple-mdm-push-certificate-get.md) – Apple kräver ett certifikat för att aktivera hantering av iOS/iPadOS- och macOS-enheter.

## <a name="user-owned-iosipados-and-ipados-devices-byod"></a>Användarägda iOS/iPadOS- och iPadOS-enheter (BYOD)

Du kan låta användare registrera sina personliga enheter för Intune-hantering, vilket kallas "bring your own device" eller BYOD. Det finns tre användarregistreringsalternativ:
- Appskyddsprinciper ger den enklaste BYOD-upplevelsen, med hantering endast på appnivå. Om du även vill skydda enheten med en 6-siffrig komplex PIN-kod kan du använda dessa principer tillsammans med Användarregistrering.
- Enhetsregistrering är antagligen det du tänker på när du tänker på en typisk BYOD-registrering. Med Enhetsregistrering har administratörer tillgång till en rad olika hanteringsalternativ.
- Användarregistrering är en enklare registreringsprocess som ger tillgång till en mindre uppsättning enhetshanteringsalternativ. Den här funktionen finns för närvarande som en förhandsversion. 

När alla krav är uppfyllda och du har tilldelat licenser till användarna, kan de ladda ned företagsportalappen för Intune från App Store och följa instruktionerna för registrering i appen. Du kan anpassa företagsportalens sekretesspolicy på iOS/iPad-enheter enligt beskrivningen i [Anpassa Intune-företagsportalens appar, Företagsportal-webbplatsen och Intune-appen](../apps/company-portal-app.md#configuration).

## <a name="company-owned-iosipados-devices"></a>Företagsägda iOS/iPadOS-enheter

Intune stöder följande registreringsmetoder för iOS/iPadOS-enheter som ägs av företaget för organisationer som köper enheter till sina användare:

- Automatisk enhetsregistrering för Apple (ADE)
- Apple School Manager
- Apple Configurator-registrering med installationsassistenten
- Apple Configurator – direkt registrering

Du kan även registrera företagsägda iOS/iPadOS-enheter med ett konto för [enhetsregistreringshantering](device-enrollment-manager-enroll.md).

## <a name="automated-device-enrollment"></a>Automatisk enhetsregistrering

Företag kan köpa iOS/iPadOS-enheter via Apples automatiserade enhetsregistrering (ADE). Med ADE kan du distribuera en registreringsprofil ”over-the-air” för att hantera enheter. Mer information finns i [Programmet för enhetsregistrering](device-enrollment-program-enroll-ios.md).

## <a name="user-enrollment"></a>Användarregistrering
Med Användarregistrering får administratörer tillgång till en deluppsättning hanteringsalternativ jämfört med andra registreringsmetoder. Mer information finns i [Åtgärder, lösenord och andra alternativ som stöds i Användarregistrering](ios-user-enrollment-supported-actions.md) och [Konfigurera Användarregistrering för iOS/iPadOS och iPadOS](ios-user-enrollment.md).

## <a name="apple-school-manager"></a>Apple School Manager

Apple School Manager är ett enhetsregistreringsprogram för skolor. Du kan distribuera en profil för att registrera enheter på samma sätt som i ADE. Lär dig mer om [Apple School Manager](apple-school-manager-set-up-ios.md).

## <a name="apple-configurator"></a>Apple Configurator

Du kan registrera iOS/-enheter med Apple Configurator på en Mac-dator. För att förbereda enheter ansluter du dem med USB och installerar en registreringsprofil. Du kan registrera enheter med Apple Configurator på två sätt:

- Registrering med installationsassistenten – rensar enheten, förbereder den för att köra installationsassistenten och installerar företagets principer för enhetens nya användare.
- Direktregistrering – rensar inte enheten och registrerar den med en fördefinierad princip. Den här metoden är för enheter utan användartillhörighet.

Läs mer om [registrering med Apple Configurator](apple-configurator-enroll-ios.md).

## <a name="use-the-company-portal-on-ade-enrolled-or-apple-configurator-enrolled-devices"></a>Använda företagsportalen på enheter som registrerats med ADE eller Apple Configurator

Enheter som har konfigurerats med användartillhörighet kan installera och köra företagsportalappen för att ladda ned appar och hantera enheter. Efter det att användarna fått sina enheter måste de utföra ett antal ytterligare steg för att slutföra installationen och installera företagsportalsappen.

Användartillhörighet krävs för att ge stöd åt följande:

- Hantering av mobilprogramsappar (MAM, Mobile Application Management)
- Villkorlig åtkomst till e-post och företagsdata
- Företagsportalappen

### <a name="how-users-enroll-corporate-owned-iosipados-devices-with-user-affinity"></a>Hur en användare registrerar företagsägda iOS/iPadOS-enheter med användartillhörighet

1. När användaren startar enheten uppmanas han eller hon att slutföra arbetet med installationsassistenten.
2. Efter installationen uppmanas användarna att ange ett Apple-ID. Användarna måste ange ett Apple-ID för att företagsportalen ska kunna installeras på enheten.
3. Företagsportalappen installeras automatiskt på iOS/iPadOS-enheten från App Store.
4. Användarna bör starta företagsportalappen och logga in med de autentiseringsuppgifter (unikt namn eller UPN) som är associerade med prenumerationen i Intune.
5. Registreringen är färdig när du har loggat in. Användarna kan nu använda den här enheten med fullständiga funktioner.

### <a name="about-corporate-owned-managed-devices-with-no-user-affinity"></a>Om företagsägda hanterade enheter som saknar användartillhörighet

Det går inte att använda företagsportalen i enheter som har konfigurerats utan användartillhörighet. Appen ska därför inte installeras på dessa. Företagsportalen är avsedd för användare som har företagsautentiseringsuppgifter och behöver åtkomst till anpassade företagsresurser (t.ex. e-post). Enheter som har registrerats utan användartillhörighet är inte avsedda för dedikerad användarinloggning. Informationsenheter, POS-enheter (Point Of Sale) och enheter med delade verktyg är typiska exempel på enheter som registrerats utan användartillhörighet.

Om användartillhörighet krävs måste du välja **Användartillhörighet** för enhetens registreringsprofil innan du registrerar enheten. Om du vill ändra tillhörighetsstatus på en enhet måste du ta enheten ur bruk och registrera den på nytt.

## <a name="see-also"></a>Se även

[Felsöka problem med registrering av iOS/iPadOS-enhet i Microsoft Intune](https://support.microsoft.com/help/4039809)
