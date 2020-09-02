---
title: Konfigurera Intune-registrering för fullständigt hanterade Android Enterprise-enheter
titleSuffix: Microsoft Intune
description: Lär dig hur du registrerar fullständigt hanterade Android Enterprise-enheter i Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b0324755ef4706e1642357ae7a4e7dc90e719a7e
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915202"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-fully-managed-devices"></a>Konfigurera Intune-registrering av fullständigt hanterade Android Enterprise-enheter 

Fullständigt hanterade Android Enterprise-enheter är företagsägda enheter som är associerade med en enskild användare och som endast används för arbete och inte för personligt bruk. Administratörer kan hantera hela enheten och tillämpa principkontroller som inte är tillgängliga för arbetsprofiler, till exempel dessa:
- Tillåt endast appinstallation från hanterad Google Play.
- Blockera avinstallation av hanterade appar.
- Förhindra att användare återställer enheter till fabriksinställningar och så vidare.

Intune hjälper dig att distribuera appar och inställningar till Android Enterprise-enheter, däribland fullständigt hanterade Android Enterprise-enheter. Specifik information om Android Enterprise finns i [Krav för Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## <a name="technical-requirements"></a>Tekniska krav

Du måste ha en fristående Intune-klientorganisation för att hantera fullständigt hanterade Android Enterprise-enheter. Hantering av fullständigt hanterade enheter är inte tillgängligt i hybridläge (SCCM-anslutet) eller i den äldre hanteringskonsolen Silverlight.

Enheter måste uppfylla dessa krav för att kunna hanteras som fullständigt hanterade Android Enterprise-enheter:

- Android OS version 6.0 och senare.
- Enheter måste köra en version av Android som har anslutningsfunktioner för Google Mobile Services (GMS). Enheter måste ha GMS tillgängligt för att kunna ansluta till GMS.

Det finns ingen begränsning på enhetstillverkare/OEM om ovanstående krav är uppfyllda.

## <a name="set-up-android-enterprise-fully-managed-device-management"></a>Konfigurera hantering av fullständigt hanterade Android Enterprise-enheter

För de här stegen om du vill konfigurera hanteringen av fullständigt hanterade Android Enterprise-enheter:

1. Förbered hantering av mobila enheter genom att [ange MDM-utfärdare som **Microsoft Intune**](../fundamentals/mdm-authority-set.md). Du anger det här objektet bara när du konfigurerar Intune för hantering av mobila enheter.
2. [Anslut ditt Intune-klientorganisationskonto till ditt Android Enterprise-konto](connect-intune-android-enterprise.md).
3. [Aktivera företagsägda användarenheter](#enable-corporate-owned-user-devices)
4. [Registrera fullständigt hanterade enheter](#enroll-the-fully-managed-devices).

### <a name="enable-corporate-owned-user-devices"></a>Aktivera företagsägda användarenheter

1. Logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj **Enheter** > **Android** > **Android-registrering**  > **Företagsägda, fullständigt hanterade användarenheter**.
2. Välj **Ja** under **Låt användarna registrera företagsägda användarenheter** .

> [!NOTE]
> Om du har definierat en princip för villkorsstyrd åtkomst för Azure AD som använder beviljandekontrollen *Kräv att enheten är markerad som kompatibel* eller en blockeringsprincip och gäller för **Alla molnappar**, **Android** och **Webbläsare** måste du utesluta **Microsoft Intune**-molnappen från den här principen. Det beror på att Android-konfigureringsprocessen använder en Chrome-flik för att autentisera användarna under registreringen. Mer information finns i [dokumentationen om villkorsstyrd åtkomst för Azure AD](/azure/active-directory/conditional-access/).

När den här inställningen anges till **Ja** får du en token för programregistrering (en slumpmässig sträng) och en QR-kod för din Intune-klient. Den här enda registreringstoken är giltig för alla användare och förfaller inte. Beroende på enhetens Android OS-version kan du använda antingen token eller QR-koden för att registrera enheten.

## <a name="enroll-the-fully-managed-devices"></a>Registrera fullständigt hanterade enheter
Du kan nu [registrera dina fullständigt hanterade enheter](android-dedicated-devices-fully-managed-enroll.md) (men inte när du använder DEM-konton).

## <a name="next-steps"></a>Nästa steg
- [Lägga till konfigurationsprinciper för fullständigt hanterade Android Enterprise-enheter](../configuration/device-restrictions-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile)
- [Konfigurera appkonfigurationsprinciper för fullständigt hanterade Android Enterprise-enheter](../apps/app-configuration-policies-use-android.md)