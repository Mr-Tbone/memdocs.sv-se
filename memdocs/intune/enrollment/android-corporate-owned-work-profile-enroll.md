---
title: Konfigurera Intune-registrering för företagsägda Android Enterprise-enheter med arbetsprofil
titleSuffix: Microsoft Intune
description: Läs om hur du registrerar företagsägda Android Enterprise-enheter med arbetsprofil i Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4934115915c41d696258aa54ee8f4b7c84d1809c
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86465027"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-corporate-owned-devices-with-work-profile"></a>Konfigurera Intune-registrering av företagsägda Android Enterprise-enheter med arbetsprofil

Företagsägda Android Enterprise-enheter med arbetsprofil är enheter för enskilda användare som är avsedda att användas både på jobbet och privat.

Slutanvändare kan hålla personliga data och jobbdata åtskilda med en garanti om att personliga data och program förblir privata. Administratörer kan styra vissa inställningar och funktioner för hela enheten, bland annat:

- Inställningskrav för enhetens lösenord
- Bluetooth och datanätverksväxling
- Skydd mot fabriksåterställning

Intune hjälper dig att distribuera appar och inställningar till företagsägda Android Enterprise-enheter med arbetsprofil. Specifik information om Android Enterprise finns i [Krav för Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## <a name="device-requirements"></a>Krav på enheten

Enheterna måste uppfylla följande krav för att kunna hanteras som företagsägda Android Enterprise-enheter med arbetsprofil:

- Android OS version 8.0 och senare.
- Enheter måste köra en distribution av Android som har anslutningsfunktioner för Google Mobile Services (GMS). Enheter måste ha GMS tillgängligt för att kunna ansluta till GMS.

## <a name="set-up-android-enterprise-corporate-owned-work-profile-device-management"></a>Konfigurera hantering av företagsägda Android Enterprise-enheter med arbetsprofil

Så här konfigurerar du hantering av företagsägda Android Enterprise-enheter med arbetsprofil:

1. Förbered hantering av mobila enheter genom att [ange MDM-utfärdare som **Microsoft Intune**](../fundamentals/mdm-authority-set.md) för instruktioner. Du anger det här objektet bara när du konfigurerar Intune för hantering av mobila enheter.
2. [Anslut ditt Intune-klientkonto till ditt hanterade Google Play-konto](connect-intune-android-enterprise.md).
3. [Skapa en registreringsprofil](#create-an-enrollment-profile).
4. [Skapa en enhetsgrupp](#create-a-device-group).
5. [Registrera de företagsägda enheterna med arbetsprofil](#enroll-the-corporate-owned-work-profile-devices).

### <a name="create-an-enrollment-profile"></a>Skapa en registreringsprofil

> [!NOTE]
> Token för företagsägda enheter med en arbetsprofil upphör inte automatiskt att gälla. Om en administratör bestämmer sig för att återkalla en token visas inte den associerade profilen under **Enheter** > **Android** > **Android-registrering** > **Företagsägda enheter med arbetsprofil (förhandsversion)** . Om du vill se alla profiler som är kopplade till både aktiva och inaktiva token klickar du på **Filtrera** och markera kryssrutorna för principtillståndet ”Aktiv” såväl som ”Inaktiv”. 

Du måste skapa en registreringsprofil så att användarna kan registrera företagsägda enheter med arbetsprofil. När profilen har skapats får den en registreringstoken (slumpmässig sträng) och en QR-kod. Beroende på enhetens Android OS-version kan du använda token eller QR-koden för att [registrera den dedikerade enheten](#enroll-the-corporate-owned-work-profile-devices).

1. Logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj **Enheter** > **Android** > **Android-registrering** > **Företagsägda enheter med arbetsprofil (förhandsversion)** .
2. Välj **Skapa profil** och fyll i fälten.
    - **Namn**: Skriv ett namn som ska användas när du tilldelar profilen till den dynamiska enhetsgruppen.
    - **Beskrivning**: Lägg till en profilbeskrivning (valfritt).
3. Välj **Nästa**.
5. På sidan **Granska och skapa** väljer du **Skapa** för att skapa policyn.

### <a name="create-a-device-group"></a>Skapa en enhetsgrupp

Du kan rikta appar och principer till tilldelade eller dynamiska enhetsgrupper. Du kan konfigurera dynamiska Azure AD-enhetsgrupper att automatiskt fylla i enheter som registreras med en viss registreringsprofil med hjälp av följande steg:

1. Logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj **Grupper** > **Alla grupper** > **Ny grupp**.
2. På bladet **Grupp** fyller du i de obligatoriska fälten så här:
    - **Grupptyp**: Säkerhet
    - **Gruppnamn:** Ange ett intuitivt namn (till exempel Fabrik 1-enheter)
    - **Typ av medlemskap**: Dynamisk enhet
3. Välj **Lägg till dynamisk fråga**.
4. På bladet **Regler för dynamiskt medlemskap** fyller du i fälten så här:
    - **Lägg till dynamisk medlemskapsregel**: Enkel regel
    - **Lägg till enheter där**: enrollmentProfileName
    - Välj **Lika med** i mittenrutan.
    - I det sista fältet anger du registreringsprofilnamnet som du har skapat tidigare.
    Mer information om regler för dynamiskt medlemskap finns i [Regler för dynamiskt medlemskap för grupper i AAD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership). 
5. Välj **Lägg till fråga** > **Skapa**.

### <a name="revoke-tokens"></a>Återkalla token

Du kan omedelbart återkalla token/QR-koden. Då kan token/QR-koden inte längre användas. Du kan använda det här alternativet om du:
  - av misstag delar token/QR-koden med en obehörig part
  - slutför alla registreringar och inte längre behöver token/QR-koden

När du ersätter eller återkallar en token/QR-kod påverkas inte enheter som redan är registrerade.

1. Logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj **Enheter** > **Android** > **Android-registrering** > **Företagsägda enheter med arbetsprofil (förhandsversion)** .
2. Välj den profil du vill arbeta med.
3. Välj **Token**.
5. Välj **Återkalla token** > **Ja** om du vill återkalla token.

## <a name="enroll-the-corporate-owned-work-profile-devices"></a>Registrera företagsägda enheter med arbetsprofil

Nu kan användare [registrera sina företagsägda enheter med arbetsprofil](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> **Microsoft Intune**-appen installeras automatiskt när en företagsägd enhet med arbetsprofil registreras.  Den här appen krävs för registreringen och kan inte avinstalleras. 

## <a name="managing-apps-on-android-enterprise-corporate-owned-work-profile-devices"></a>Hantera appar på företagsägda Android Enterprise-enheter med arbetsprofil

Det är bara appar med tilldelningstypen [Obligatorisk](../apps/apps-deploy.md#assign-an-app) som kan installeras på företagsägda Android Enterprise-enheter med arbetsprofil. Appar installeras från den hanterade Google Play-butiken på samma sätt som Android Enterprise-arbetsprofilenheter.

Appar uppdateras automatiskt på hanterade enheter när apputvecklaren publicerar en uppdatering på Google Play.

Om du vill ta bort en app från en företagsägd Android Enterprise-enhet med arbetsprofil kan du göra något av följande:
- Ta bort den obligatoriska appdistributionen.
- Skapa en avinstallation av distributionen för appen.

## <a name="next-steps"></a>Nästa steg
- [Distribuera Android-appar](../apps/apps-deploy.md)
- [Lägga till Android-konfigurationsprinciper](../configuration/device-profiles.md)
