---
title: Registrera dedikerade eller fullständigt hanterade Android Enterprise-enheter eller företagsägda arbetsprofilsenheter i Intune
titleSuffix: Microsoft Intune
description: Lär dig att registrera dedikerade eller fullständigt hanterade Android Enterprise-enheter eller företagsägda arbetsprofilsenheter i Intune.
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
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9fafc6a48e933fbcce692c560532736808cbf7c4
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915253"
---
# <a name="enroll-your-android-enterprise-dedicated-fully-managed-or-corporate-owned-with-work-profile-devices"></a>Registrera dina dedikerade eller fullständigt hanterade Android Enterprise-enheter eller företagsägda med arbetsprofilsenheter

När du har konfigurerat dina [dedikerade Android Enterprise-enheter](android-kiosk-enroll.md) eller [fullständigt hanterade enheter](android-fully-managed-enroll.md) eller [företagsägda med arbetsprofilenheter](android-corporate-owned-work-profile-enroll.md) i Intune kan du registrera enheterna. Intune-registrering för både dedikerade enheter och fullständigt hanterade enheter börjar med en fabriksåterställning. Hur du registrerar dina Android Enterprise-enheter beror på operativsystemet.

| Registreringsmetod | Lägsta Android OS-version för dedikerade och fullständigt hanterade enheter |
| ----- | ----- |
| NFC (Near Field Communication) | 6.0 |
| Token | 6.0 |
| QR-kod | 7.0 |
| Zero Touch  | 8.0<br><br> För deltagande tillverkare. |
| [Knox Mobile-registrering](./android-samsung-knox-mobile-enroll.md)  | 6.0<br><br> Endast för enheter med Samsung KNOX 2.8 eller senare. |

## <a name="enroll-by-using-near-field-communication-nfc"></a>Registrera med NFC (Near Field Communication)

För enheter 6 och senare som stöder NFC kan du etablera enheter genom att ange en särskilt formaterad NFC-tagg. Du kan använda en egen app eller valfritt verktyg som skapar NFC-taggar. Mer information finns i artikeln om [C-baserad registrering av Android enterprise-enheter med Microsoft Intune](/archive/blogs/cbernier/nfc-based-android-enterprise-device-enrollment-with-microsoft-intune) och i [Googles API-dokumentation för Android-hantering](https://developers.google.com/android/management/provision-device#nfc_method).

## <a name="enroll-by-using-a-token"></a>Registrera med en token

För enheter med Android 6 och senare kan du använda token för att registrera enheten. I Android 6.1 och senare versioner kan du även skanna QR-koder när du använder registreringsmetoden **afw#setup**.

1. Starta den rensade enheten.
2. Välj språk på **välkomstskärmen**.
3. Anslut till ditt **Wi-Fi** och välj **NÄSTA**.
4. Acceptera Googles villkor och välj **NÄSTA**.
5. På Googles inloggningsskärm anger du **afw#setup** istället för ett Gmail-konto och sedan **NÄSTA**.
6. Välj **INSTALLERA** för appen **Android Device Policy**.
7. Fortsätt installationen av principen.  Vissa enheter kan kräva ytterligare godkännande av villkor.
8. På skärmen **Registrera den här enheten** låter du din enhet skanna QR-koden eller så väljer du att ange token manuellt.
9. Följ anvisningarna på skärmen för att slutföra registreringen.

## <a name="enroll-by-using-a-qr-code"></a>Registrera med QR-kod

På enheter med Android 7 och senare kan du skanna QR-koden från registreringsprofilen för att registrera enheten.

> [!Note]
> Webbläsarens zoom kan göra att enheter inte kan skanna QR-koder. Du löser problemet genom att öka webbläsarens zoom.

1. Starta en QR-läsning på Android-enheten genom att trycka flera gånger på den första skärmen du ser efter en rensning.
2. För enheter med Android 7 och 8 devices uppmanas du att installera en QR-läsare. Enheter med Android 9 och senare har redan en installerad QR-läsare.
3. Använd QR-lädaren för att skanna registreringsprofilens QR-kod och följ sedan anvisningarna på skärmen för att registrera.

## <a name="enroll-by-using-google-zero-touch"></a>Registrera genom att använda Google Zero Touch

Om du vill använda Googles Zero Touch-system måste enheten ha stöd för det och vara kopplad till en leverantör som är en del av tjänsten.  Mer information finns på [webbplatsen för Googles Zero Touch-program](https://www.android.com/enterprise/management/zero-touch/).

1. Skapa en ny konfiguration i Zero Touch-konsolen.
2. Välj **Microsoft Intune** i listrutan EMM DPC.
3. I Googles Zero Touch-konsol kopierar du och klistrar in följande JSON i fältet DPC extras. Ersätt strängen *YourEnrollmentToken* med den registreringstoken du har skapat som en del av din registreringsprofil. Omge registreringstoken med dubbla citattecken.

    ```json
    {
        "android.app.extra.PROVISIONING_DEVICE_ADMIN_COMPONENT_NAME": "com.google.android.apps.work.clouddpc/.receivers.CloudDeviceAdminReceiver",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_SIGNATURE_CHECKSUM": "I5YvS0O5hXY46mb01BlRjq4oJJGs2kuUcHvVkAPEXlg",

        "android.app.extra.PROVISIONING_DEVICE_ADMIN_PACKAGE_DOWNLOAD_LOCATION": "https://play.google.com/managed/downloadManagingApp?identifier=setup",

        "android.app.extra.PROVISIONING_ADMIN_EXTRAS_BUNDLE": {
            "com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN": "YourEnrollmentToken"
        }
    }
    ```

4. Välj **Använd**.

## <a name="enroll-by-using-knox-mobile-enrollment"></a>Registrera genom att använda Knox Mobile Enrollment
Om du vill använda Samsungs Knox Mobile Enrollment måste enheten köra Android OS version 6 eller senare och Samsung KNOX 2.8 eller senare. Mer information finns i [Registrerar dina enheter med Knox Mobile Enrollment](./android-samsung-knox-mobile-enroll.md).

## <a name="next-steps"></a>Nästa steg
- [Distribuera Android-appar](../apps/apps-deploy.md)
- [Lägga till Android-konfigurationsprinciper](../configuration/device-profiles.md)