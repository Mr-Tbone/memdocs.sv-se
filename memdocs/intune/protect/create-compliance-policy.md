---
title: Skapa enhetsefterlevnadsprinciper i Microsoft Intune – Azure | Microsoft Docs
description: Skapa enhetsefterlevnadsprinciper, översikt över status och allvarlighetsgrader, använda statusen InGracePeriod, arbeta med villkorsstyrd åtkomst, hantera enheter utan en tilldelad princip, samt skillnader i efterlevnad i Azure-portalen och den klassiska portalen i Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b437a72a2380fea215746aa76b35898c6fc60b16
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551372"
---
# <a name="create-a-compliance-policy-in-microsoft-intune"></a>Skapa en efterlevnadsprincip i Microsoft Intune

Enhetsefterlevnadsprinciper är en viktig funktion när du använder Intune för att skydda din organisations resurser. I Intune kan du skapa regler och inställningar som enheter måste uppfylla för att anses vara kompatibla, till exempel en lägsta operativsystemversion. Om enheten inte är kompatibel kan du blockera åtkomst till data och resurser med hjälp av [villkorlig åtkomst](conditional-access.md).

Du kan också vidta åtgärder vid inkompatibilitet genom att exempelvis skicka ett e-postmeddelande till användaren. En översikt över vad efterlevnadsprinciper gör och hur de används finns i avsnittet om att [komma igång med enhetsefterlevnad](device-compliance-get-started.md).

Den här artikeln:

- Visar kraven och stegen för att skapa en efterlevnadsprincip.
- Visar hur du tilldelar principen till dina användare och enhetsgrupper.
- Beskriver ytterligare funktioner, inklusive omfångstaggar för att ”filtrera” dina principer, samt vad du kan göra på enheter som inte är kompatibla.
- Visar en lista med incheckningstider för uppdateringscykeln när enheterna tar emot principuppdateringar.

## <a name="before-you-begin"></a>Innan du börjar

Om du vill använda enhetsefterlevnadsprinciper måste du:

- Använd följande prenumerationer:

  - Intune
  - Om du använder villkorlig åtkomst måste du ha Azure Active Directory (AD) Premium-utgåvan. I listan [Priser för Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) visas vad som finns i de olika utgåvorna. Intune-efterlevnad kräver inte Azure AD.

- Använd en plattform som stöds:

  - Android-enhetsadministratör
  - Android enterprise
  - iOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Registrera enheter i Intune (krävs för att kunna se efterlevnadsstatusen)

- Registrera enheter för en användare, eller registrera utan någon primär användare. Enheter som har registrerats för flera användare stöds inte.

> [!NOTE]
> Användargränssnittet i Intune uppdateras till en helskärmsupplevelse och kan ta flera veckor. Innan klienten får den här uppdateringen får du ett något annorlunda arbetsflöde när du skapar eller redigerar de inställningar som beskrivs i den här artikeln.

## <a name="create-the-policy"></a>Skapa principen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Enheter** > **Efterlevnadsprinciper** > **Principer** > **Skapa princip**.

3. Välj en **plattform** för den här principen utifrån följande alternativ:
   - *Android-enhetsadministratör*
   - *Android enterprise*
   - *iOS/iPadOS*
   - *macOS*
   - *Windows Phone 8.1*
   - *Windows 8.1 och senare*
   - *Windows 10 och senare*

    För *Android Enterprise* väljer du även en **principtyp**:
     - *Efterlevnadsprincip för ägare av Android-enhet*
     - *Efterlevnadsprincip för Android-arbetsprofil*

    Öppna sedan konfigurationsfönstret **Skapa princip** genom att välja **Skapa**.

4. Ange ett **Namn** på fliken **Grundläggande information** som sedan kan hjälpa dig att identifiera dem. Till exempel är ett bra principnamn **Markera jailbrokade iOS/iPadOS-enheter som inkompatibla**.

   Du kan också välja att ange en **Beskrivning**.
  
5. Visa de tillgängliga kategorierna på fliken **Kompatibilitetsinställningar** och konfigurera inställningarna för principen.  Läs en beskrivning av inställningarna för respektive plattform i följande artiklar:
   - [Android-enhetsadministratör](compliance-policy-create-android.md)
   - [Android enterprise](compliance-policy-create-android-for-work.md)
   - [iOS/iPadOS](compliance-policy-create-ios.md)
   - [macOS](compliance-policy-create-mac-os.md)
   - [Windows Phone 8.1, Windows 8.1 och senare](compliance-policy-create-windows-8-1.md)
   - [Windows 10 och senare](compliance-policy-create-windows.md)  

6. Du kan framtvinga efterlevnad baserat på enhetens plats på fliken **Platser**. Välj från befintliga platser. Om du inte har någon tillgänglig plats ännu kan du läsa mer i [Använda platser (nätverksgräns)](use-network-locations.md).
   > [!TIP]
   > **Platser** är endast tillgängligt för *Android-enhetsadministratörs*plattformen.

7. Gå till fliken **Åtgärder vid inkompatibilitet** och ange en sekvens med åtgärder som ska tillämpas automatiskt på enheter som inte uppfyller den här efterlevnadspolicyn.

   Du kan lägga till flera åtgärder och konfigurera scheman och ytterligare information för vissa åtgärder. Du kan exempelvis ändra schemat för standardåtgärden *Markera enheten som inkompatibel* så att den inträffar efter en dag. Du kan sedan lägga till en åtgärd om du vill skicka ett e-postmeddelande till användaren som varnar om att enheten inte är kompatibel. Du kan också lägga till åtgärder som låser eller drar tillbaka enheter som inte är kompatibla.

   Information om vilka åtgärder du kan konfigurera finns [Lägga till åtgärder för inkompatibla enheter](actions-for-noncompliance.md), som även innehåller information om hur du skapar e-postmeddelanden som skickas till användarna.

   Ett annat exempel visar hur du använder Platser och lägger till minst en plats till en efterlevnadsprincip. I det här fallet tillämpas standardåtgärden för inkompatibilitet när du väljer minst en plats. Om enheten inte är ansluten till någon av de valda platserna utvärderas den som inkompatibel. Du kan konfigurera schemat så att användarna ges en respitperiod, exempelvis en dag.

8. Gå till fliken **Omfångstaggar** och välj taggar för att filtrera principer till specifika grupper, t.ex. `US-NC IT Team` eller `JohnGlenn_ITDepartment`. När du har lagt till inställningarna kan du också lägga till en omfångstagg till efterlevnadsprinciperna. 

   Mer information om användning av omfångstaggar finns i [Använda omfångstaggar för att filtrera principer](../fundamentals/scope-tags.md).

9. Tilldela dina grupper principen på fliken **Tilldelningar**.  

   Välj **+ Välj grupper att ta med** och tilldela sedan principen till en eller flera grupper. Principen gäller för dessa grupper från det att du sparar principen efter nästa steg. 

10. Granska inställningarna på fliken **Granska och skapa** och välj **Skapa** när du är redo att spara efterlevnadsprincipen.  

    De användare eller enheter som omfattas av din princip utvärderas för efterlevnad när de checkar in med Intune.

<!-- Evaluate option  - pending details as to its fate with this new Full Screen UI udpate  

### Evaluate how many users are targeted

When you assign the policy, you can also **Evaluate** how many users are affected. This feature calculates users; it doesn't calculate devices.

1. In Intune, select **Devices** > **Compliance policies** > **Policies**.

2. Select a *policy* > **Assignments** > **Evaluate**. A message shows you how many users are targeted by this policy.

If the **Evaluate** button is grayed out, make sure the policy is assigned to one or more groups.
-->

## <a name="refresh-cycle-times"></a>Uppdatera cykeltider

Intune använder olika uppdateringscykler för att söka efter uppdateringar av efterlevnadsprinciper. Om enheten nyligen har registrerats körs incheckningarna oftare. [Princip-och profil uppdaterings cykler](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) visar de uppskattade uppdateringstiderna.

Användarna kan när de vill öppna företagsportalappen och synkronisera enheten för att söka efter principuppdateringar.

### <a name="assign-an-ingraceperiod-status"></a>Tilldela en InGracePeriod-status

Statusen InGracePeriod för en tilldelad policy för efterlevnad är ett värde. Värdet fastställs genom en kombinationen av en enhets respitperiod och en enhets faktiska status för den tilldelade policyn för efterlevnad.

Specifikt innebär det att om en enhet har statusen NonCompliant för en tilldelad efterlevnadsprincip och:

- enheten inte har någon tilldelad respitperiod, så är det tilldelade värdet för policyn för efterlevnad är NonCompliant
- enheten har en respitperiod som har löpt ut, så är det tilldelade värdet för policyn för efterlevnad är NonCompliant
- enheten har en respitperiod som ligger i framtiden, så är det tilldelade värdet för policyn för efterlevnad är InGracePeriod

Följande tabell innehåller en sammanfattning av de här punkterna:

|Faktisk efterlevnadsstatus|Värde för tilldelad respitperiod|Effektiv efterlevnadsstatus|
|---------|---------|---------|
|NonCompliant |Ingen tilldelad respitperiod |NonCompliant |
|NonCompliant |Gårdagens datum|NonCompliant|
|NonCompliant |Morgondagens datum|InGracePeriod|

Mer information om hur du övervakar enhetsefterlevnadsprinciper finns i [Övervaka efterlevnadsprinciper för Intune-enhet](compliance-policy-monitor.md).

### <a name="assign-a-resulting-compliance-policy-status"></a>Tilldela en resulterande status för policy för efterlevnad

Om en enhet har flera policyer för efterlevnad och enheten har olika efterlevnadsstatus för två eller fler av de tilldelade policyerna för efterlevnad tilldelas en enda resulterande efterlevnadsstatus. Den här tilldelningen baseras på en konceptuell allvarlighetsgrad som tilldelas till varje efterlevnadsstatus. Varje efterlevnadsstatus har följande allvarlighetsgrad:

|Status  |Allvarlighetsgrad  |
|---------|---------|
|Okänt     |1|
|NotApplicable     |2|
|godkända|3|
|InGracePeriod|4|
|NonCompliant|5|
|Fel|6|

När en enhet har flera policyer för efterlevnad tilldelas den högsta allvarlighetsgraden av alla policyer till den enheten.

Anta exempelvis att en enhet har tre tilldelade efterlevnadsprinciper: en med statusen Okänd (allvarlighetsgrad = 1), en med statusen Kompatibel (allvarlighetsgrad = 3) och en med statusen InGracePeriod (allvarlighetsgrad = 4). Statusen InGracePeriod har högst allvarlighetsgrad. Därför har alla tre principerna efterlevnadsstatusen InGracePeriod.

## <a name="next-steps"></a>Nästa steg

[Övervaka dina principer](compliance-policy-monitor.md).
