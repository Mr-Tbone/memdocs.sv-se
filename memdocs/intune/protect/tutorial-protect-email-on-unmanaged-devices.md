---
title: Självstudie – Skydda e-post i Exchange Online på ohanterade enheter
titleSuffix: Microsoft Intune
description: Lär dig att skydda Office 365 Exchange Online med Intunes appskyddsprinciper och Azure AD:s villkorliga åtkomst.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/21/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f8be97edbbba9a998dd223a5a0e9c8982c1a16a1
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326599"
---
# <a name="tutorial-protect-exchange-online-email-on-unmanaged-devices"></a>Självstudie: Skydda e-post i Exchange Online på ohanterade enheter

Lär dig att använda appskyddsprinciper med villkorlig åtkomst för att skydda Exchange Online, även om enheterna inte är registrerade i en enhetshanteringslösning som exempelvis Intune. I den här självstudien får du lära dig att:

> [!div class="checklist"]
> * Skapa en Intune-appskyddsprincip för Outlook-appen. Du kan begränsa hur användaren kan använda appdata genom att förhindra ”Spara som” och begränsa åtgärder för att klippa ut, kopiera och klistra in.
> * Skapa principer för villkorlig åtkomst i Azure Active Directory (Azure AD) som endast tillåter att Outlook-appen får åtkomst till företagets e-post i Exchange Online. Du kan också kräva multifaktorautentisering (MFA) för moderna autentiseringsklienter, till exempel Outlook för iOS och Android.

## <a name="prerequisites"></a>Krav

Du behöver en testklient med följande prenumerationer för den här självstudien:

- Azure Active Directory Premium ([kostnadsfri utvärderingsversion](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
- Intune-prenumeration ([kostnadsfri utvärderingsversion](../fundamentals/free-trial-sign-up.md))
- En Office 365 Business-prenumeration med Exchange ([kostnadsfri utvärderingsversion](https://go.microsoft.com/fwlink/p/?LinkID=510938))

## <a name="sign-in-to-intune"></a>Logga in i Intune

I den här självstudien ska du logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) som [global administratör](../fundamentals/users-add.md#types-of-administrators) eller Intune-[tjänstadministratör](../fundamentals/users-add.md#types-of-administrators). Om du har skapat en prenumeration för Intune-utvärdering är det konto som du skapade prenumerationen med den globala administratören.

## <a name="create-the-app-protection-policy"></a>Skapa appskyddsprincipen

I den här självstudien ska vi konfigurera en Intune-appskyddsprincip för iOS för Outlook-appen som skapar skydd på appnivå. Vi kommer att kräva en PIN-kod för att öppna appen i arbetssammanhang. Vi begränsar också datadelning mellan appar och förhindrar att företagets data sparas på en privat plats.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Appar** > **Appskyddsprinciper** > **Skapa princip** och välj **iOS/iPad** som plattform.

3. Konfigurera följande inställningar på sidan **Grundläggande**:

   - **Namn**: Ange **Principtest för Outlook-app**.
   - **Beskrivning**: Ange **Principtest för Outlook-app**.

   Värdet för **Platform** är inställt på ditt föregående val.

   Fortsätt genom att klicka på **Next** .

4. På sidan **Appar** kan du välja hur du vill tillämpa den här principen på appar på olika enheter. Konfigurera följande alternativ:

   - För **Rikta mot alla typer av appar**: Välj **Nej**. För **Apptyper** markerar du kryssrutan för **Appar på ohanterade enheter**.
   - Klicka på **Välj offentliga appar**. I applistan väljer du **Outlook** och sedan **Välj**.  Outlook visas nu under *Offentliga appar*.

   Fortsätt genom att klicka på **Next** .

5. Sidan med **Dataskydd** innehåller inställningar som avgör hur användarna interagerar med data i de appar som den här appskyddsprincipen gäller för. Konfigurera följande alternativ:

   Under *Dataöverföring* konfigurerar du följande inställningar och lämnar alla andra inställningar på standardvärdena:

   - För **Skicka organisationsdata till andra appar** väljer du **Ingen**.  
   - För **Ta emot data från andra appar** väljer du **Ingen**.  
   - För **Spara kopior av organisationsdata** väljer du **Blockera**.  
   - I **Begränsa klipp ut, kopiera och klistra in mellan andra appar** väljer du **Blockerad**. 

   ![Välj dataflyttinställningar för Outlook-appens skyddsprincip](./media/tutorial-protect-email-on-unmanaged-devices/data-protection-settings.png)

   Fortsätt genom att välja **Nästa**.

6. Sidan **Åtkomstkrav** innehåller inställningar som gör att du kan konfigurera de krav för PIN-kod och autentiseringsuppgifter som användarna måste uppfylla för att få åtkomst till appar i en arbetskontext. Konfigurera följande inställningar och lämna alla andra inställningar på standardvärdena:

   - I **PIN-kod för åtkomst** väljer du **Ja**.
   - För **Arbets- eller skolkontoautentiseringsuppgifter för åtkomst** väljer du **Kräv**.

   ![Välj åtkomståtgärder för Outlook-appens skyddsprincip](./media/tutorial-protect-email-on-unmanaged-devices/access-requirements-settings.png)

   Fortsätt genom att välja **Nästa**.

7. Sidan **Villkorsstyrd start** innehåller inställningar med vilka du anger krav för inloggningssäkerhet för din appskyddsprincip. I den här självstudien behöver du inte konfigurera de här inställningarna.

   Fortsätt genom att klicka på **Next** .

8. På sidan **Tilldelningar** kan du tilldela appskyddsprincipen till grupper av användare. I den här självstudien tilldelar du inte den här principen till en grupp.  
 Du behöver inte konfigurera de här inställningarna.

   Fortsätt genom att klicka på **Next** .

9. På sidan **Nästa: Granska och skapa** för att granska de värden och inställningar som du angav för den här appskyddsprincipen. Klicka på **Skapa** för att skapa appskyddsprincipen i Intune.

Appskyddsprincipen för Outlook skapas. Härnäst kommer du att konfigurera villkorlig åtkomst som kräver att enheterna ska använda Outlook-appen.

## <a name="create-conditional-access-policies"></a>Skapa principer för villkorlig åtkomst

Nu ska vi skapa två principer för villkorlig åtkomst som gäller för alla enhetsplattformar.  

- Den första principen kräver att moderna autentiseringsklienter använder den godkända Outlook-appen och Multi-Factor authentication (MFA). Moderna autentiseringsklienter är Outlook för iOS och Outlook för Android.  

- Den andra principen kräver Exchange ActiveSync-klienter som använder den godkända Outlook-appen. (För närvarande stöder Exchange Active Sync inte andra villkor än enhetsplattform). Du kan konfigurera principer för villkorlig åtkomst i Azure AD-portalen eller i Intune-portalen. Eftersom vi redan är i Intune-portalen, skapar vi principen här.  

### <a name="create-an-mfa-policy-for-modern-authentication-clients"></a>Skapa en MFA-princip för moderna autentiseringsklienter  

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Slutpunktssäkerhet** >  **Villkorlig åtkomst** > **Ny princip**.  

3. I **Namn** anger du **Testprincip för moderna autentiseringsklienter**.  

4. Under **Tilldelningar** väljer du **Användare och grupper**. På fliken **Inkludera** väljer du **Alla användare** och sedan **Klar**.

5. Under **Tilldelningar** väljer du **Molnappar eller åtgärder**. Eftersom vi vill skydda e-posten i Office 365 Exchange Online, väljer vi det genom att följa dessa steg:

   1. På fliken **Inkludera** väljer du **Välj appar**.
   2. Välj **Välj**.
   3. I listan med program väljer du **Office 365 Exchange Online** och sedan **Välj**.
   4. Välj **Klar** om du vill återgå till rutan Ny princip.

   ![Välj Office 365 Exchange Online-appen](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-cloud-apps.png)

6. Under **Tilldelningar** väljer du **Villkor** > **Enhetsplattformar**.

   1. Under **Konfigurera** väljer du **Ja**.
   2. På fliken **Inkludera**, väljer du **Alla enheter**.
   3. Välj **Klar**.

7. Välj **Klientappar** i fönstret **Villkor**.

   1. Under **Konfigurera** väljer du **Ja**.
   2. Välj **Mobilappar och skrivbordsklienter** och **Moderna autentiseringsklienter**.
   3. Avmarkera alla andra kryssrutor.
   4. Välj **Klar** > **Klar** om du vill återgå till rutan Ny princip.

   ![Välj Mobila appar och klienter](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-client-apps.png)

8. Under **Åtkomstkontroller** väljer du **Bevilja**.

   1. I rutan **Bevilja** väljer du **Bevilja åtkomst**.
   2. Välj **Kräv multifaktorautentisering**.
   3. Välj **Kräv godkänd klientapp**.
   4. Under **För flera kontroller** väljer du **Kräv alla valda kontroller**. Den här inställningen garanterar att båda kraven som du har valt tillämpas när en enhet försöker få åtkomst till e-post.
   5. Välj **Välj**.

   ![Välj åtkomstkontroller](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-mfa.png)

9. Under **Aktivera princip** väljer du **På** och sedan **Skapa**.

   ![Skapa princip](./media/tutorial-protect-email-on-unmanaged-devices/enable-policy.png)  

Principen för villkorlig åtkomst för moderna autentiseringsklienter skapas. Nu kan du skapa en princip för Exchange Active Sync-klienter.

### <a name="create-a-policy-for-exchange-active-sync-clients"></a>Skapa en princip för Exchange Active Sync-klienter

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Slutpunktssäkerhet** > **Villkorlig åtkomst** > **Ny princip**.

3. I **Namn** anger du **Testprincip för EAS-klienter**.

4. Under **Tilldelningar** väljer du **Användare och grupper**. På fliken *Inkludera* väljer du **Alla användare** och sedan **Klar**.

5. Under **Tilldelningar** väljer du **Molnappar eller åtgärder**. Välj ett e-postmeddelande i Office 365 Exchange Online med följande steg:

   1. På fliken *Inkludera* väljer du **Välj appar**.
   2. Välj **Välj**.
   3. I listan med *program* väljer du **Office 365 Exchange Online** och sedan **Välj**, därefter **Klar**.
  
6. Under **Tilldelningar** väljer du **Villkor** > **Enhetsplattformar**.

   1. Under **Konfigurera** väljer du **Ja**.
   2. På fliken **Inkludera**, väljer du **Alla enheter** och sedan **Klar**.

7. Välj **Klientappar** i fönstret **Villkor**.

   1. Under **Konfigurera** väljer du **Ja**.
   2. Välj **Mobila appar och skrivbordsklienter**.
   3. Välj **Exchange ActiveSync-klienter** och **Tillämpa bara principen på plattformar som stöds**.  
   4. Avmarkera alla andra kryssrutor.  
   5. Välj **Klar** och sedan **Klar** igen.  

   ![Tillämpa på plattformar som stöds](./media/tutorial-protect-email-on-unmanaged-devices/eas-client-apps.png)  

8. Under **Åtkomstkontroller** väljer du **Bevilja**.

   1. I rutan **Bevilja** väljer du **Bevilja åtkomst**.
   2. Välj **Kräv godkänd klientapp**. Avmarkera alla andra kryssrutor.
   3. Välj **Välj**.

   ![Kräv godkänd klientapp](./media/tutorial-protect-email-on-unmanaged-devices/eas-grant-access.png)

9. Under **Aktivera princip** väljer du **På** och sedan **Skapa**.

Dina appskyddsprinciper och din villkorlig åtkomst är nu på plats och är redo för att testas.

## <a name="try-it-out"></a>Prova nu

Med de principer som du har skapat måste enheter registreras i Intune och använda Outlook-mobilappen för att få åtkomst till e-post i Office 365. Försök logga in på Exchange Online med autentiseringsuppgifter för en användare i testklienten för att testa det här scenariot på en iOS-enhet.

1. Om du vill testa på en iPhone går du till **Inställningar** > **Lösenord och konton** > **Lägg till konto** > **Exchange**.

2. Ange e-postadressen för en användare i testklienten och tryck sedan på **Nästa**.  
3. Tryck på **Logga in**.

4. Ange testanvändarens lösenord och tryck på **Logga in**.

5. Meddelandet **Mer information krävs** visas, vilket innebär att du uppmanas att konfigurera MFA. Gå vidare och konfigurera en extra verifieringsmetod.

6. Därefter visas ett meddelande om att du försöker öppna den här resursen med en app som inte har godkänts av din IT-avdelning. Meddelandet innebär att du är blockerad från att använda den interna e-postappen. Avbryt inloggningen.

7. Öppna Outlook-appen och välj **Inställningar** > **Lägg till konto** > **Lägg till e-postkonto**.

8. Ange e-postadressen för en användare i testklienten och tryck sedan på **Nästa**.

9. Tryck på **Logga in med Office 365**. Du uppmanas till ytterligare autentisering och registrering. När du har loggat in kan du testa åtgärder som klipp ut, kopiera, klistra in och ”Spara som”.

## <a name="clean-up-resources"></a>Rensa resurser

När testprinciperna inte längre behövs kan du ta bort dem.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** **Efterlevnadsprinciper**.

3. I listan **Principnamn** väljer du snabbmenyn ( **...** ) för testprincipen och sedan **Ta bort**. Välj **Ja** för att bekräfta.

4. Välj **Slutpunktssäkerhet** > **Villkorlig åtkomst**.

5. I listan **Principnamn** väljer du snabbmenyn ( **...** ) för varje testprincip och sedan **Ta bort**. Välj **Ja** för att bekräfta.

## <a name="next-steps"></a>Nästa steg
I de här självstudierna har du skapat appskyddsprinciper som begränsar vad användaren kan göra med Outlook-appen. Du har även skapat principer för villkorlig åtkomst som kräver att Outlook-appen och MFA för moderna autentiseringsklienter används. Läs om hur du använder Intune med villkorlig åtkomst för att skydda andra appar och tjänster i [Konfigurera villkorlig åtkomst](conditional-access.md).
