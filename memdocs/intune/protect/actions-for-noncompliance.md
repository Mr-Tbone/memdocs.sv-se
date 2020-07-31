---
title: Inkompatibilitetsmeddelande och åtgärder med Microsoft Intune – Azure | Microsoft Docs
description: Skapa ett e-postmeddelande som ska skickas till inkompatibla enheter. Lägg till åtgärder som ska utföras för enheter som inte uppfyller dina policyer kring efterlevnad. Det här kan vara åtgärder som att ge en respitperiod för att uppnå efterlevnad, att blockera åtkomsten till nätverksresurser eller att återkalla enheten.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: samyada
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e881dc386fa0fe0b98b5e3d4480e1957c251808
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262684"
---
# <a name="configure-actions-for-noncompliant-devices-in-intune"></a>Konfigurera åtgärder för icke-inkompatibla enheter i Intune

För enheter som inte uppfyller dina principer eller regler för efterlevnad kan du lägga till **åtgärder för inkompatibilitet**. Den här funktionen konfigurerar en tidssorterad sekvens med åtgärder, till exempel att skicka e-post till slutanvändaren och mer.

## <a name="overview"></a>Översikt

Som standard innehåller varje efterlevnadsprincip åtgärden för inkompatibilitet, **Markera enheten som inkompatibel**, med ett schema på noll dagar (**0**). När Intune identifierar en enhet som inte är kompatibel gör standardinställningen att Intune omedelbart markerar enheten som inkompatibel. När en enhet märkts som inkompatibel kan den blockeras med [villkorsstyrd åtkomst](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) i Azure Active Directory (AD).

Genom att konfigurera **Åtgärder för inkompatibilitet** får du flexibiliteten att bestämma vad du ska göra med inkompatibla enheter, och när du ska göra det. Du kan t.ex. bestämma dig för att inte blockera enheten omedelbart, och sedan ge användaren en respitperiod att åtgärda problemet.

För varje åtgärd du anger kan du konfigurera ett schema som avgör när åtgärden börjar gälla. Schemat är ett antal dagar efter att enheten markerats som inkompatibel. Du kan också konfigurera flera instanser av en åtgärd. När du ställer in flera instanser av en åtgärd i en princip körs åtgärden igen vid den senare schemalagda tiden om enheten inte är kompatibel.

Alla åtgärder är inte tillgängliga för alla plattformar.

## <a name="available-actions-for-noncompliance"></a>Tillgängliga åtgärder för inkompatibilitet

Följande är tillgängliga åtgärder för inkompatibilitet. Om inget annat anges är varje åtgärd tillgänglig för alla plattformar som stöds av Intune:

- **Markera enhet som inkompatibel**: Som standard anges den här åtgärden för varje efterlevnadsprincip och har ett schema på noll (**0**) dagar, vilket markerar enheter som inkompatibla direkt.

  När du ändrar standardschemat anger du en respitperiod där en användare kan åtgärda problem eller bli kompatibel utan att markeras som icke-kompatibel.

- **Skicka e-post till slutanvändare**: Den här åtgärden skickar ett e-postmeddelande till användaren.
När du aktiverar den här åtgärden:

  - Välj en *Mall för aviseringsmeddelande* som den här åtgärden skickar. Du måste [Skapa en mall för aviseringsmeddelande](#create-a-notification-message-template) innan du kan tilldela en till den här åtgärden. När du skapar ett anpassat meddelande anpassar du ämnet och meddelandetexten, och du kan lägga till företagets logotyp, företagets namn och ytterligare kontaktinformation.
  - Välj att skicka meddelandet till ytterligare mottagare genom att välja en eller flera av dina Azure AD-grupper.

När e-postmeddelandet skickas lägger Intune till information om den inkompatibla enheten i e-postmeddelandet.

- **Fjärrlåsa en icke-kompatibel enhet**: Använd den här åtgärden för att utfärda ett fjärrlås för en enhet. Användaren uppmanas i så fall att ange en PIN-kod eller ett lösenord för att låsa upp enheten. Mer om funktionen [Fjärrlåsning](../remote-actions/device-remote-lock.md).

  Följande plattformar stöder den här åtgärden:
  - Android:
    - Android-enhetsadministratör
    - Fullständigt hanterad, dedikerad och företagsägd arbetsprofil för Android
    - Android Enterprise-arbetsprofil
    - Android Enterprise-kioskenheter
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobil
  - Windows Phone 8.1 och senare

- **Ta den icke-kompatibla enheten ur bruk**: Den här åtgärden tar bort alla företagets data från enheten och tar bort enheten från Intune-hanteringen. För att förhindra oavsiktlig rensning av en enhet har den här åtgärden stöd för ett schema på minst **30** dagar.

  Följande plattformar stöder den här åtgärden:
  - Android:
    - Android-enhetsadministratör
    - Ägare av Android Enterprise-enhet
    - Android Enterprise-arbetsprofil
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobil
  - Windows Phone 8.1 och senare

  Läs mer om att [ta bort enheter](../remote-actions/devices-wipe.md#retire).

- **Skicka push-meddelande till slutanvändare**: Konfigurera den här åtgärden för att skicka ett push-meddelande om inkompatibilitet till en enhet via Företagsportal-appen eller Intune-appen på enheten.

  Följande plattformar stöder den här åtgärden:
  - Android:
    - Android-enhetsadministratör
    - Ägare av Android Enterprise-enhet
    - Android Enterprise-arbetsprofil
  - iOS/iPadOS

  Push-meddelandet skickas den första gången som en enhet checkar in med Intune och är inte kompatibel med policyn för efterlevnad. När en användare väljer meddelandet öppnas Företagsportal-appen eller Intune-appen med information om orsaken till inkompatibiliteten. Användaren kan sedan vidta åtgärder för att lösa problemet. Informationen om inkompatibilitet i meddelandet genereras av Intune och kan inte anpassas.

  > [!IMPORTANT]
  > Intune, Företagsportal-appen och Microsoft Intune-appen kan inte garantera att ett anpassat meddelande levereras. Aviseringar kan visas efter flera timmars fördröjning, om de visas alls. Det här gäller även när användare har inaktiverat push-meddelanden.
  >
  > Förlita dig inte på den här aviseringsmetoden för brådskande meddelanden.

  Varje instans av åtgärden skickar ett meddelande en gång. Om du vill skicka samma meddelande igen från en princip konfigurerar du ytterligare instanser av åtgärden i principen, var och en med ett annat schema.
  
  Du kan till exempel schemalägga den första åtgärden för noll dagar och sedan lägga till en andra instans av åtgärden som är inställd på tre dagar. Den här fördröjningen före det andra meddelandet ger användaren några dagar för att lösa problemet och undvika det andra meddelandet.

  För att undvika att skicka skräppost till användare med för många dubbletter av meddelanden kan du granska och effektivisera vilka efterlevnadspolicyer som innehåller ett push-meddelande om regelefterlevnad, och granska de scheman som används så att inte samma avisering skickas för ofta.

  Tänk på att:
  - För en enda princip som innehåller flera instanser av en push-avisering för samma dag skickas bara ett enda meddelande för den dagen.

  - När flera efterlevnadspolicyer omfattar samma efterlevnadsvillkor och inkluderar åtgärden för push-meddelande med samma schema skickas flera meddelanden till samma enhet samma dag i Intune.

## <a name="before-you-begin"></a>Innan du börjar

Du kan [lägga till åtgärder för inkompatibilitet](#add-actions-for-noncompliance) när du konfigurerar efterlevnadsprinciper för enheter, eller senare genom att redigera principen. Du kan lägga till ytterligare åtgärder till varje princip för att uppfylla dina behov. Tänk på att varje efterlevnadsprincip automatiskt inkluderar standardåtgärden vid inkompatibilitet som markerar enheter som inkompatibla, med ett schema inställt på noll dagar.

Du måste ha konfigurerat villkorlig Azure AD-åtkomst för att kunna använda principer för enhetsefterlevnad till att blockera enheter från företagets resurser. Mer information finns i [Villkorlig åtkomst i Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) eller [Vanliga sätt att använda villkorlig åtkomst med Intune](conditional-access-intune-common-ways-use.md).

Se följande plattformsspecifika vägledning när du ska skapa en efterlevnadsprincip för enheter:

- [Android](compliance-policy-create-android.md)
- [Android-arbetsprofiler](compliance-policy-create-android-for-work.md)
- [iOS](compliance-policy-create-ios.md)
- [macOS](compliance-policy-create-mac-os.md)
- [Windows](compliance-policy-create-windows.md)

## <a name="create-a-notification-message-template"></a>Skapa en mall för aviseringsmeddelanden

Om du vill skicka ett e-postmeddelande till användarna skapar du en mall för aviseringsmeddelanden. När en enhet är inkompatibel visas informationen som du anger i mallen i e-postmeddelandet som skickas till användarna.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Slutpunktsskydd** > **Enhetsefterlevnad** > **Meddelanden** > **Skapa meddelande**.
3. Ange följande information under *Grundläggande*:

   - **Namn**
   - **Ämne**
   - **Meddelande**

4. Under *Grundläggande* konfigurerar du följande alternativ för meddelandet:

   - **E-postsidhuvud – infoga företagets logotyp** (standard = *Aktivera*) – logotypen du laddar upp som en del av varumärkesanpassningen i Företagsportal används i e-postmallar. Läs mer om varumärkesanpassning av företagsportalen i [Varumärkesanpassning för företagsidentitet](../apps/company-portal-app.md#customizing-the-user-experience).
   - **E-postsidfot – infoga företagets namn** (standard = *Aktivera*)
   - **E-postsidfot – Infoga kontaktinformation** (standard = *Aktivera*)
   - **Länk till företagsportalens webbplats** (standard = *Inaktivera*) – om du anger *Aktivera* innehåller e-postmeddelandet en länk till företagsportalens webbplats.

   > [!div class="mx-imgBorder"]
   > ![Exempel på ett meddelande om bristande regelefterlevnad i Intune](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   Fortsätt genom att välja **Nästa**.

5. Under **Granska + skapa** granskar du dina konfigurationer för att säkerställa att meddelandemallen är redo att användas. Välj **Skapa** för att skapa meddelandet.

### <a name="view-and-edit-notifications"></a>Visa och redigera meddelanden

Meddelanden som har skapats är tillgängliga på sidan *Efterlevnadsprinciper* > *Meddelanden*. På denna sida kan du välja ett meddelande vars konfiguration du vill se:

- Välj **Skicka förhandsgranskad e-post** om du vill skicka en förhandsversion av meddelandet till det konto som du använder för att logga in till Intune. 
- Gör en ändring genom att välja **Redigera** för *Grundläggande inställningar* eller *Omfångstaggar*.

## <a name="add-actions-for-noncompliance"></a>Lägga till åtgärder vid inkompatibilitet

När du skapar en princip för enhetsefterlevnad skapar Intune automatiskt en åtgärd för inkompatibilitet. Om en enhet inte uppfyller din efterlevnadsprincip markerar den här åtgärden enheten som inkompatibel. Du kan anpassa hur länge enheten ska markeras som inkompatibel. Det går inte att ta bort åtgärden.

Du kan lägga till valfria åtgärder när du skapar en princip för efterlevnad, eller uppdatera en befintlig princip.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Efterlevnadsprinciper** > **Principer**, välj en av dina principer och välj sedan **Egenskaper**.

   Har du inte någon princip än? Skapa en princip för [Android](compliance-policy-create-android.md), [iOS](compliance-policy-create-ios.md), [Windows](compliance-policy-create-windows.md) eller någon annan plattform.

   > [!NOTE]
   > JAMF-enheter och enheter som är mål för enhetsgrupper kan inte ta emot efterlevnadsåtgärder just nu.

3. Välj **Åtgärder för inkompatibilitet** > **Lägg till**.

4. Välj din **åtgärd**:

   - **Skicka e-post till slutanvändare**: Välj att skicka ett e-postmeddelande till användaren om enheten inte är kompatibel. Du kan också:
     - Välj den **meddelandemall** som du skapade tidigare
     - Ange eventuella **ytterligare mottagare** genom att välja grupper

   - **Fjärrlåsa en icke-kompatibel enhet**: Lås enheten när den är inkompatibel. Den här åtgärden tvingar användaren att ange en PIN-kod eller ett lösenord för att låsa upp enheten.

   - **Ta den icke-kompatibla enheten ur bruk**: Ta bort alla företagets data från enheten och ta bort enheten från Intune-hanteringen när den är inkompatibel.

   - **Skicka push-meddelande till slutanvändare**: Konfigurera den här åtgärden för att skicka ett push-meddelande om inkompatibilitet till en enhet via Företagsportal-appen eller Intune-appen på enheten.

5. Konfigurera ett **schema**: Ange hur många dagar (0 till 365) efter en inkompatibilitet som åtgärden ska utlösas på användarnas enheter. (*Ta icke-kompatibel enhet ur bruk* har stöd för minst 30 dagar.) Efter den här respittiden kan du tillämpa en [princip för villkorlig åtkomst](conditional-access-intune-common-ways-use.md). Om du anger **0** (noll) dagar tillämpas den villkorliga åtkomsten **omedelbart**. Om en enhet till exempel inte är kompatibel kan du använda villkorlig åtkomst för att blockera åtkomsten till e-post, SharePoint och andra organisationsresurser omedelbart.

   När du skapar en efterlevnadsprincip skapas automatiskt åtgärden **Markera enheten som inkompatibel**, och den ställs automatiskt in på **0** dagar (omedelbart). Med den här åtgärden bedöms enheten som icke-kompatibel direkt när den checkar in. Om du även använder villkorlig åtkomst träder den villkorliga åtkomsten i kraft direkt. Om du vill tillåta en respitperiod ändrar du **Schema** för åtgärden **Markera enheten som inkompatibel**.

   I efterlevnadsprincipen kanske du även vill meddela användaren. Du kan lägga till åtgärden **Skicka e-post till slutanvändare**. I åtgärden **Skicka e-post** anger du två dagar för **Schema**. Om enheten eller slutanvändaren fortfarande bedöms som icke-kompatibel dag två skickas e-postmeddelandet dag två. Om du vill skicka e-post till användaren på dag fem i lägger du till en annan åtgärd och anger fem dagar för **Schema**.

   Mer information om efterlevnad och de inbyggda åtgärderna finns i [översikt över efterlevnad](device-compliance-get-started.md).

6. När du är klar väljer du **Lägg till** > **OK** för att spara ändringarna.

## <a name="next-steps"></a>Nästa steg

[Övervaka dina principer](compliance-policy-monitor.md).
