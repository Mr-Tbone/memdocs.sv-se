---
title: 'Snabbstart: Skapa en e-postenhetsprofil för iOS/iPadOS-enheter'
titleSuffix: Microsoft Intune
description: Lär dig att använda Microsoft Intune för att skapa en e-postenhetsprofil så att iOS/iPadOS-enheter kan anslutas säkert till företagets e-post.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: af7657eb89df14e8429a81616e76d81a5a9ac5c1
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327430"
---
# <a name="quickstart-create-an-email-device-profile-for-iosipados"></a>Snabbstart: Skapa en e-postenhetsprofil för iOS/iPadOS

I den här snabbstartsguiden visas hur du skapar en e-postenhetsprofil för iOS-/iPadOS-enheter. Den här profilen anger inställningar som krävs för att den inbyggda e-postappen på iOS/iPadOS-enhet ska kunna ansluta till företagets e-post. Med e-postenhetsprofiler uppnår du konsekvens över flera enheter och ger slutanvändarna åtkomst till företagets e-post på sina personliga enheter utan de behöver konfigurera något själva. För att ytterligare skydda din e-post kan du använda en e-postprofil för att avgöra om enheterna är kompatibla och sedan konfigurera villkorlig åtkomst så att endast kompatibla enheter får åtkomst till e-post. Mer information om e-postprofiler finns i [Konfigurera e-postinställningar i Microsoft Intune](email-settings-configure.md)

Om du inte har en Intune-prenumeration [kan du registrera dig för ett kostnadsfritt utvärderingskonto](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune"></a>Logga in i Intune

Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) som global administratör eller Intune-tjänstadministratör. Om du har skapat en prenumeration för en Intune-utvärdering, är det konto som du skapade prenumerationen med den globala administratören.

## <a name="create-an-iosipados-email-profile"></a>Skapa en e-postprofil för iOS/iPadOS

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj och gå till **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
   ![Skapa en e-postprofil för iOS/iPadOS i Intune](./media/quickstart-email-profile/ios-create-profile.png)

3. Ange följande egenskaper:
   - **Plattform**: Välj **iOS/iPadOS**
   - **Profil**: Välj **E-post**
  
4. Välj **Skapa**.

5. Ange följande egenskaper i **Grundinställningar**:
   - **Namn**: Ange ett beskrivande namn på den nya profilen. I det här exemplet anger du **iOS måste använda e-postadress**.
   - **Beskrivning**: Ange **iOS/iPadOS-enheter måste använda e-postadressen för arbetet**


        ![Skapa en e-postprofil för användning med iOS/iPadOS-enheter i Intune](./media/quickstart-email-profile/ios-email-profile-name.png)

6. Välj **Nästa**.

7. Välj **Konfigurationsinställningar** och ange följande inställningar (lämna standardinställningarna för alla andra inställningar):
   - **E-postserver**: I den här snabbstarten använder vi **outlook.office365.com**. Den här inställningen anger Exchange-platsen (URL) för e-postservern som iOS/iPadOS-e-postappen använder för att ansluta till e-post.
   - **Kontonamn**: Ange **Företagets e-postadress**.
   - **Användarnamnattribut från AAD**: Namnet är det attribut som Intune hämtar från Azure Active Directory (Azure AD). Intune genererar användarnamnet som används av den här profilen. I den här snabbstartsguiden kommer vi att anta att **User Principal Name** ska användas som användarnamn för profilen (till exempel user1@contoso.com).
   - **E-postadressattribut från AAD**: Den här inställningen är e-postadressen från Azure AD som används för att logga in på Exchange. I den här snabbstarten använder vi **User Principal Name**.
   - **Autentiseringsmetod**: I den här snabbstarten väljer vi **användarnamn och lösenord**. (Du kan också välja **Certifikat** om du redan har konfigurerat ett certifikat för Intune.)

8. Välj **Nästa**.

9. För **Omfångstaggar** (valfritt) väljer du **Nästa**. Vi använder inte en omfångstagg för den här profilen.

10. I **Tilldelningar**använder du listrutan för **Tilldela till** och väljer **Alla användare och alla enheter**.  Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. 

## <a name="clean-up-resources"></a>Rensa resurser

Om du inte planerar att använda profilen du skapade för fler självstudier eller test bör du ta bort den nu.

1. I Intune väljer du**Enheter** > **Enhetskonfiguration**.
2. Välj testprofilen som du skapade, **iOS/iPadOS-enheter måste använda e-postadressen för arbetet**, och välj sedan **Ta bort**. 

## <a name="next-steps"></a>Nästa steg

I den här snabbstarten skapade du en e-postprofil för iOS/iPadOS-enheter. Nu kan du använda den här profilen för att avgöra om en iOS/iPadOS-enhet är kompatibel genom att skapa en efterlevnadsprincip som markerar iOS/iPadOS-enheter som inte matchar profilen som icke-kompatibla. För ytterligare skydd, kan du skapa en villkorlig åtkomstprincip som blockerar icke-kompatibla iOS/iPadOS-enheter från att komma åt e-post. Mer information om efterlevnadsprinciper för enheter i [Kom igång med efterlevnadsprinciper för enheter i Intune](../protect/device-compliance-get-started.md).

> [!div class="nextstepaction"]
> [Självstudie: Skydda e-post i Exchange Online på hanterade enheter](../protect/tutorial-protect-email-on-enrolled-devices.md)
