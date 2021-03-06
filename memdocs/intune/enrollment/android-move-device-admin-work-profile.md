---
title: Flytta Android-enheter från enhetsadministratör till arbetsprofilhantering
titleSuffix: Microsoft Intune
description: Flytta Android-enheter från enhetsadministratör till arbetsprofilhantering i Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
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
ms.openlocfilehash: fb62a7b592b492d4092b7af7ee29b2bfd50c66e8
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915185"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>Flytta Android-enheter från enhetsadministratör till arbetsprofilhantering

Du kan hjälpa användare att flytta sina Android-enheter från enhetsadministratör till arbetsprofilhantering med hjälp av kompatibilitetsinställningen för att **blockera enheter som hanteras med enhetsadministratör**. Med den här inställningen kan du göra enheter icke-kompatibla om de hanteras med enhetsadministratör. 

När användarna ser att de inte uppfyller kraven av det här skälet, kan de trycka på **Lös**. De tas då till en checklista som vägleder dem genom:
1. Avregistrering från enhetsadministratörshantering
2. Registrering för arbetsprofilhantering
3. Lösning av eventuella efterlevnadsproblem. 

## <a name="prerequisites"></a>Krav

- Användarna måste ha [Android-enhetsadministratörsregistrerade enheter](android-enroll-device-administrator.md) med Android Företagsportal version 5.0.4720.0 eller senare.
- Du konfigurerar Android-arbetsprofilhantering genom [att ansluta ditt Intune-klientkonto till ditt Android Enterprise-konto](connect-intune-android-enterprise.md).
- [Ställ in Android Enterprise-arbetsprofilregistrering](android-work-profile-enroll.md) för den grupp användare som flyttar till Android-arbetsprofilen.
- Överväg att öka användarenhetsgränserna. När du avregistrerar enheter från enhetsadministratörshantering, kan det hända att enhetsposter inte tas bort omedelbart. Om du vill tillhandahålla en buffert under den här perioden, kan du behöva öka enhetsgränskapaciteten så att användarna kan registrera sig för arbetsprofilhantering.
  - [Konfigurera Azure Active Directory-enhet inställningarna](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings) för maximalt antal enheter per användare.
  - Justera [Intune-enhetens gränsbegränsningar](enrollment-restrictions-set.md#create-a-device-limit-restriction) genom att ange enhetsgränsen. 

## <a name="create-device-compliance-policy"></a>Skapa en efterlevnadsprincip för enheter

1. I [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) väljer du **Enheter** > **Efterlevnadsprinciper** > **Principer** > **Skapa princip**.

    ![Skapa princip](./media/android-move-device-admin-work-profile/create-policy.png)

2. På sidan **Skapa en princip** ställer du in **Plattform** till **Android-enhetsadministratör** > **Skapa**.
3. På sidan **Grundinställningar** anger du **Namn** och **Beskrivning** > **Nästa**.

    ![Sidan Grundinställningar](./media/android-move-device-admin-work-profile/basics.png)
    
4. På sidan **Kompatibilitetsinställningar** i avsnittet **Enhetens hälsotillstånd** ställer du in alternativet för att **blockera enheter som hanteras med enhetsadministratör** på **Ja** > **Nästa**.

    ![Blockera enheter](./media/android-move-device-admin-work-profile/block-devices.png)

5. På sidan **Platser** kan du lägga till platser om du vill > **Nästa**.

6. På fliken **Åtgärder för inkompatibilitet** kan du konfigurera [tillgängliga åtgärder för inkompatibilitet](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) för att anpassa slutanvändarnas upplevelse av det här flödet.

    ![Åtgärder vid inkompatibilitet](media/android-move-device-admin-work-profile/noncompliance-actions.png)

    Här är några åtgärder att överväga:

    - **Markera enheten som inkompatibel**: Som standard är den här åtgärden inställd på noll (0) dagar så att enheter markeras som inkompatibla direkt. Om du ändrar det här till fler dagar får användarna en respitperiod där de kan se flödet för att flytta till arbetsprofilhanteringen utan att markeras som inkompatibla. Om du till exempel ställer in 14 dagar har användarna två veckor på sig att flytta från enhetsadministratör till arbetsprofilhantering utan att förlora åtkomsten till resurser.
    - **Skicka push-meddelande till slutanvändare**: Konfigurera det här för att skicka push-meddelanden till enhetsadministratörens enheter. När en användare väljer meddelandet startas Android Företagsportal på sidan **Uppdatera enhetsinställningar** där användaren kan starta flödet för att gå över till arbetsprofilhantering.
    - **Skicka e-post till slutanvändare**: Konfigurera det här för att skicka e-postmeddelanden till användare om flytten från enhetsadministratör till arbetsprofilhantering. Du kan ta med webbadressen nedan i e-postmeddelandet. När en användare väljer webbadressen startas Android Företagsportal på sidan Uppdatera enhetsinställningar där användaren kan starta flödet för att gå över till arbetsprofilhantering.
      - `https://portal.manage.microsoft.com/UpdateSettings.aspx`.
      - För amerikanska myndigheter kan du använda den här länken i stället: `https://portal.manage.microsoft.us/UpdateSettings.aspx`.
  
      > [!NOTE]
      > - Naturligtvis kan du använda användarvänlig hypertext för länkarna i kommunikationen med användarna. Använd dock inte URL-förkortare eftersom länkarna kanske inte fungerar om de ändras på det sättet.
      > - Om Android Företagsportal är öppen och i bakgrunden när en användare trycker på länken, kan han eller hon istället gå till den sista sidan som är öppen.
      > - Användarna måste trycka på länken på en Android-enhet. Om de i stället klistrar in den i en webbläsare så startas inte Android-företagsportalen. 

    Välj **Nästa**.

7. På sidan **Omfångstaggar** väljer du de omfångstaggar som du vill ta med.
8. På sidan **Tilldelningar** tilldelar du principen till en grupp som har enheter som har registrerats med enhetsadministratörshantering > **Nästa**.
9. På sidan **Granska och skapa** bekräftar du alla inställningar och väljer sedan **Skapa**.

## <a name="troubleshooting"></a>Felsökning

[Flödet för slutanvändare som vill flytta till en ny enhetshanteringsinstallation](../user-help/move-to-new-device-management-setup.md) vägleder användaren genom avregistreringen från enhetsadministratörshantering och till en konfiguration med arbetsprofilshantering. Användarna måste ha [Android-enhetsadministratörsregistrerade enheter](android-enroll-device-administrator.md) med Android Företagsportal version 5.0.4720.0 eller senare.

### <a name="user-sees-an-error-after-tapping-resolve"></a>Användaren ser ett fel efter att ha tryckt på Lös
Om användarna ser ett fel efter att ha tryckt på knappen **Lös** beror det förmodligen på någon av följande orsaker:
- Din arbetsprofilsregistrering utfördes inte på rätt sätt (antingen har ett Android Enterprise-konto inte anslutits eller så har registreringsbegränsningarna ställts in för att blockera arbetsprofilsregistrering).
- Enheten kör Android 4.4 eller tidigare, som inte har stöd för arbetsprofilregistrering. 
- Enhetstillverkaren har inte stöd för arbetsprofilregistrering på enhetsmodellen.

### <a name="resolve-button-doesnt-appear-on-the-users-device"></a>Knappen Lös visas inte på användarens enhet
Knappen **Lös** visas inte på användarens enhet om användaren registrerar sig för enhetsadministratörshantering efter att efterlevnadsprincip som beskrivs ovan har visats.

Om du vill att knappen **Lös** ska visas måste användaren skjuta upp installationen och starta om processen från meddelandet.

Använd registreringsbegränsningar för att blockera registrering för enhetsadministratörshantering för att undvika det här problemet.

### <a name="user-sees-an-error-after-tapping-url-to-update-device-settings-page"></a>Användaren ser ett fel efter att ha tryckt på URL:en till sidan Uppdatera enhetsinställningar
Användarna kan se en felsida i webbläsaren när de trycker på URL:en till sidan **Uppdatera enhetsinställningar** för Android Företagsportal. Det här felet kan orsakas av något av följande:
- Enheten är inte en Android.
- Android-enheten saknar företagsportalappen.
- Versionen för Android Företagsportal är tidigare än 5.0.4720.0.
- Android-enheten använder Android 6 eller tidigare. 

## <a name="next-steps"></a>Nästa steg
[Se slutanvändarflödet](../user-help/move-to-new-device-management-setup.md)
[Hantera Android-arbetsprofilenheter med Intune](android-enterprise-overview.md)