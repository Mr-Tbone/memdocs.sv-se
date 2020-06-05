---
title: Registrera iOS/iPadOS-enheter – Användarregistrering
titleSuffix: Microsoft Intune
description: Lär dig hur du konfigurerar Användarregistrering för iOS/iPadOS och iPadOS.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/2/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d98f3f8205490848d9f5137e97e7796eee67a67
ms.sourcegitcommit: 7a5196d4d9736c5cd52a23155c479523e52a097d
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/05/2020
ms.locfileid: "84436779"
---
# <a name="set-up-iosipados-and-ipados-user-enrollment-preview"></a>Konfigurera användarregistrering för iOS/iPadOS och iPadOS (förhandsversion)

Du kan konfigurera registreringen av iOS/iPadOS- och iPadOS-enheter i Intune med hjälp av Apples användarregistreringsprocess. Med Användarregistrering får administratörer tillgång till en enklare deluppsättning hanteringsalternativ jämfört med andra registreringsmetoder.

Mer information om vilka alternativ som är tillgängliga med Användarregistrering finns i [Åtgärder, lösenord och andra alternativ som stöds i Användarregistrering](ios-user-enrollment-supported-actions.md).

> [!NOTE]
> Stöd för Apples användarregistrering i Intune är för närvarande tillgänglig som en förhandsversion.

## <a name="prerequisites"></a>Krav
- [Utfärdare för hantering av mobil enhet (MDM)](../fundamentals/mdm-authority-set.md)
- [Apple MDM-pushcertifikat](apple-mdm-push-certificate-get.md)

## <a name="create-a-user-enrollment-profile-in-intune"></a>Skapa en profil för Användarregistrering i Intune

En registreringsprofil definierar inställningarna som tillämpas på en grupp enheter vid registreringen. 

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **iOS** > **iOS-registrering** > **Registreringstyper (förhandsversion)**  > **Skapa profil** > **iOS/iPadOS**. I den här profilen väljer du registreringsupplevelse för iOS/iPadOS- och iPadOS-slutanvändare på enheter som inte har registrerats via en företagsspecifik Apple-metod. Om du vill göra ändringar kan du redigera profilen i efterhand.

    ![Skapa en Apple-registreringsprofil](./media/ios-user-enrollment/create-profile.png)

2. På sidan **Grundinställningar**, anger du ett **Namn** och **Beskrivning** för profilen för administrationssyfte. Användarna kan inte se den här informationen. Du kan använda fältet **Namn** för att skapa en dynamisk grupp i Azure Active Directory. Använd profilnamnet för att definiera parametern enrollmentProfileName för att tilldela registreringsprofilen till enheter. Läs mer om [dynamiska Azure Active Directory-grupper](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal#rules-for-devices).

    ![Sidan Grundinställningar](./media/ios-user-enrollment/basics-page.png)

3. Välj **Nästa**.

4. På sidan **Inställningar** väljer du något av följande alternativ för **Registreringstyp**:

    ![Sidan Inställningar](./media/ios-user-enrollment/settings-page.png)

    - **Enhetsregistrering**: Alla användare i den här profilen kommer att använda enhetsregistrering.
    - **Användarregistrering**: Alla användare i den här profilen kommer att använda användarregistrering.
    - **Bestäm baserat på användarens val**: Alla användare i den här gruppen får välja vilken typ av registrering som ska användas. När användarna registrerar sina enheter kan de välja mellan **Jag äger den här enheten** och **(Företaget) äger den här enheten**. Om de väljer det andra alternativet registreras enheten via Enhetsregistrering. Om användaren väljer **Jag äger den här enheten** måste han eller hon välja om hela enheten ska skyddas eller endast arbetsrelaterade appar och data. Vilket alternativ slutanvändaren väljer vad gäller ägarskap av enheten avgör endast vilken typ av registrering som implementeras på deras enheter. Det här användarvalet visas inte i attributet Ägarskap för enhet i Intune. Mer information om användarupplevelsen finns i [Konfigurera iOS/iPadOS-enhetsåtkomst till företagsresurser](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp).
    
5. Välj **Nästa**.

6. På sidan **Tilldelningar** väljer du användargrupperna som innehåller de användare som du vill tilldela den här profilen till. Du kan välja att tilldela profilen till alla användare eller till specifika grupper. Alla användare i de valda grupperna använder den registreringstyp du valt ovan. Enhetsgrupper stöds inte i användarregistreringsscenarier eftersom funktionen baseras på användaridentiteter i stället för enheter. Du kan välja att tilldela profilen till alla användare eller till specifika grupper.

    ![Sidan Tilldelningar](./media/ios-user-enrollment/assignments-page.png)

7. Välj **Nästa**.

8. Gå igenom dina val på sidan **Granska och skapa** och tilldela profilen till användarna genom att välja **Skapa**.

    ![Sidan Tilldelningar](./media/ios-user-enrollment/assignments-page.png)


## <a name="profile-priority"></a>Profilprioritet

När du har skapat mer än en profil för registreringstyper kan du ändra profilernas prioritetsordning.

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **iOS** > **iOS-registrering** > **Registreringstyper (förhandsversion)** .
2. Dra och släpp profilerna i listan i den ordning som de ska tillämpas.

Om det uppstår konflikter mellan profiler för en användare används profilen med högre prioritet för användaren.


