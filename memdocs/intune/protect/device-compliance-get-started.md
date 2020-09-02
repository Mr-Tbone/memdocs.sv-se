---
title: Policyer för efterlevnad för enheter i Microsoft Intune – Azure | Microsoft Docs
description: Kom igång med att använda efterlevnadsprinciper, inklusive inställningar för efterlevnadsprinciper och enhetsefterlevnadsprinciper för Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0ae39f91c4daa67c40c42022f63137f0b23daf80
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911071"
---
# <a name="use-compliance-policies-to-set-rules-for-devices-you-manage-with-intune"></a>Använd efterlevnadsprinciper för att ange regler för enheter som du hanterar med Intune

Många MDM-lösningar för hantering av mobilenheter som Intune, skyddar organisationens data genom att kräva att användare och enheter uppfyller vissa krav. I Intune kan kallas den här funktionen för *efterlevnadsprinciper*.

Efterlevnadsprinciper i Intune:

- Definierar de regler och inställningar som användare och enheter måste följa för att vara kompatibla.
- Inkludera åtgärder som gäller för enheter som inte är kompatibla. Åtgärder för inkompatibilitet kan varna användare om villkoren för inkompatibilitet och skydda data på icke-kompatibla enheter.
- Kan [kombineras med villkorsstyrd åtkomst](#integrate-with-conditional-access) vilket därmed kan blockera användare och enheter som inte uppfyller reglerna.

Efterlevnadsprinciper i Intune har två delar:

- **Inställningar för efterlevnadsprincip** – inställningar för hela klientorganisationen som är en inbyggd efterlevnadsprincip som varje enhet tar emot. Inställningar för efterlevnadsprinciper anger en baslinje för hur en efterlevnadsprincip fungerar i din Intune-miljö, inklusive om enheter som inte har tagit emot några efterlevnadsprinciper är kompatibla eller inkompatibla.

- **Efterlevnadsprincip** – plattformsspecifika regler som du konfigurerar och distribuerar till grupper av användare eller enheter.  Dessa regler definierar krav för enheter, till exempel lägsta operativsystem eller användning av diskkryptering. Enheter måste uppfylla dessa regler för att anses vara kompatibla.

Precis som andra Intune-principer beror utvärderingar av efterlevnadsprinciper för en enhet på när enheten checkar in med Intune och [cykler för princip- och profiluppdatering](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## <a name="compliance-policy-settings"></a>Inställningar för efterlevnadsprinciper

*Inställningar för efterlevnadsprinciper* är inställningar för hela klientorganisationen som avgör hur Intunes efterlevnadstjänst samverkar med dina enheter. De här inställningarna skiljer sig från de inställningar som du konfigurerar i en efterlevnadsprincip för enheter.

Om du vill hantera inställningarna för efterlevnadsprinciper loggar du in på [administrationscenter för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och gå till **slutpunktssäkerhet** > **enhetsefterlevnad** > **inställningar för efterlevnadsprinciper**.

Inställningarna för efterlevnadsprinciper omfattar följande inställningar:

- **Markera enheter utan någon tilldelad efterlevnadsprincip som**

  Den här inställningen avgör hur Intune hanterar enheter som inte har tilldelats en enhetsefterlevnadsprincip. Den här inställningen har två värden:
  - **Kompatibla** (*standard*): Den här säkerhetsfunktionen är av. Enheter som inte har någon efterlevnadsprincip anses vara *kompatibla*.
  - **Ej kompatibel**: Den här säkerhetsfunktionen är på. Enheter som inte tagit emot en enhetsefterlevnadsprincip anses ej kompatibla.

  Om du använder villkorsstyrd åtkomst med enhetsefterlevnadsprinciperna rekommenderar vi att du ändrar den här inställningen till **inte kompatibel** för att säkerställa att endast enheter som har bekräftats som kompatibla kan komma åt dina resurser.

  Om en användare inte är kompatibel eftersom ingen princip har tilldelats, visar [företagsportalsappen](../apps/company-portal-app.md) att inga efterlevnadsprinciper har tilldelats.

- **Förbättrad identifiering av jailbreak** (*gäller endast iOS/iPadOS*)

  Den här inställningen påverkar endast enheter som är föremål för en enhetsefterlevnadsprincip som blockerar jailbrokade enheter.  (Se inställningarna för [Enhetshälsa](compliance-policy-create-ios.md#device-health) för iOS/iPadOS).

  Den här inställningen har två värden:

  - **Inaktiverad** (*standard*): Den här säkerhetsfunktionen är av. Den här har ingen inverkan på enheter som är föremål för en enhetsefterlevnadsprincip som blockerar jailbrokade enheter.
  - **Aktiverad**: Den här säkerhetsfunktionen är på. Enheter som tar emot enhetsefterlevnadsprincipen för att blockera jailbrokade enheter använder förbättrad jailbreak-identifiering.

  När det aktiveras på en tillämplig iOS/iPadOS-enhet:

  - Aktiverar enheten platstjänster på OS-nivå.
  - Tillåter enheten att företagsportalen använder platstjänster.
  - Använder enheten sina platstjänster för att utlösa jailbreak-identifiering oftare i bakgrunden. Användarens platsdata lagras inte av Intune.

  Förbättrad jailbreak-identifiering kör en utvärdering när:

  - Företagsportalsappen öppnas
  - Enheten fysiskt flyttas ett betydande avstånd på cirka 500 meter eller mer. Intune kan inte garantera att varje betydande platsändring resulterar i en kontroll med jailbreak-detektering, detta eftersom kontrollen är beroende av en enhets nätverksanslutning vid tidpunkten.

  På iOS 13 och senare, kräver den här funktionen att användare väljer *Tillåt alltid* när enheten uppmanar dem att fortsätta låta att Företagsportalen använder deras plats i bakgrunden. Om användare inte alltid tillåter åtkomst till platser och har en princip med den här inställningen konfigurerad markeras enheten som inkompatibel.

- **Giltighetsperiod för efterlevnadsstatus (dagar)**

  Ange en period i vilken enheter måste rapporteras på alla mottagna efterlevnadsprinciper. Om en enhet inte kan rapportera efterlevnadsstatus för en princip innan giltighetsperioden går ut, behandlas enheten som inkompatibel.

  Som standard är perioden inställt på 30 dagar. Du kan konfigurera en period från 1 till 120 dagar.

  Du kan visa information om inställningen för enhetsefterlevnad till giltighetsperiod. Logga in på [administrationscenter för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och gå till **Enheter** > **Övervaka** > **Ställ in efterlevnad**. Den här inställningen har namnet **Är aktiv** i *Inställning*-kolumnen.  Mer information om detta och relaterade vyer för kompatibilitetsstatus finns i [Övervaka enhetens kompatibilitet](compliance-policy-monitor.md).

## <a name="device-compliance-policies"></a>Efterlevnadsprinciper för enheter

Efterlevnadsprinciper för Intune-enheter:

- Definierar de regler och inställningar som användare och hanterade enheter måste uppfylla för att vara kompatibla. Exempel på regler är att kräva att enheter kör en lägsta OS-version, inte är jailbreakad eller rotad och ligger på eller under en *hotnivå* som angetts av programvaran för hothantering som du har integrerat med Intune.
- Stöd åtgärder som gäller för enheter som inte uppfyller dina efterlevnadsregler. Exempel på åtgärder inkluderar fjärrlåsning, eller att skicka en enhetsanvändare e-post om enhetens status så att de kan åtgärda den.
- Distribuera till användare i användargrupper eller till enheter i enhetsgrupper. När en efterlevnadsprincip distribueras till en användare så kontrolleras alla användarens enheter för efterlevnad. Användning av enhetsgrupper i det här scenariot hjälper till med kompabilitetsrapportering.

Om du använder villkorsstyrd åtkomst kan principerna för villkorsstyrd åtkomst använda resultaten från enhetsefterlevnad för att blockera åtkomst till resurser från inkompatibla enheter.

De tillgängliga inställningar du kan ange i en efterlevnadsprincip beror den plattformstyp du väljer när du skapar en princip. Olika enhetsplattformar stöder olika inställningar och varje plattformstyp kräver en separat princip.  

Följande ämnen länkar till dedikerade artiklar för olika aspekter av konfigurationsprincipen för enheten.

- [**Åtgärder vid inkompatibilitet**](actions-for-noncompliance.md) – varje efterlevnadsprincip för enheter innehåller en eller flera åtgärder vid inkompatibilitet. De här åtgärderna är regler som tillämpas på enheter som inte uppfyller de villkor som du har angett i principen.

  Som standard inkluderar varje enhets efterlevnadsprincip åtgärden för att markera en enhet som inkompatibel om den inte uppfyller en principregel. Därefter tillämpar principen eventuella ytterligare åtgärder för inkompatibilitet på enheten som du har konfigurerat, baserat på de scheman som du har angett för dessa åtgärder.

  Åtgärder för inkompatibilitet kan hjälpa till att varna användare när deras enhet inte är kompatibel eller skydda data som kan finnas på en enhet. Exempel på åtgärder är:

  - **Skicka e-postaviseringar** till användare och grupper med information om den inkompatibla enheten. Du kan konfigurera principen att skicka ett e-postmeddelande omedelbart när enheten markeras inkompatibel och därefter igen tills dess att enheten blir kompatibel.
  - **Fjärrlåsa enheter** som har varit inkompatibla under en viss tid.
  - **Dra tillbaka enheter** när de har varit inkompatibla under en viss tid. Den här åtgärden tar bort alla företagets data från enheten och tar bort enheten från Intune-hantering.

- [**Konfigurera nätverksplatser**](use-network-locations.md) – stöds av Android-enheter. Du kan konfigurera *nätverksplatser* och sedan använda platserna som en efterlevnadsregel för enheter. Den här typen av regel kan flagga en enhet som inkompatibel när den ligger utanför eller lämnar ett angivet nätverk. Innan du kan ange en platsregel måste du konfigurera nätverksplatserna.

- [**Skapa en princip**](create-compliance-policy.md) – med informationen i den här artikeln kan du granska förutsättningar, arbeta med alternativen för att konfigurera regler, ange åtgärder för inkompatibilitet och tilldela principen till grupper. Den här artikeln innehåller också information om principuppdateringstider.

  Visa efterlevnadsinställningar för enheter för de olika enhetsplattformarna:

  - [Android](compliance-policy-create-android.md)
  - [Android enterprise](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows 8.1 och senare](compliance-policy-create-windows-8-1.md)
  - [Windows 10 och senare](compliance-policy-create-windows.md)

## <a name="monitor-compliance-status"></a>Övervaka kompatibilitetsstatus

Intune innehåller en instrumentpanel för enhetsefterlevnad som du använder för att övervaka kompatibilitetsstatus för enheter och för att gå in på detaljnivå för principer och enheter för mer information. Läs mer om den här instrumentpanelen i [Övervaka enhetsefterlevnad](compliance-policy-monitor.md).

## <a name="integrate-with-conditional-access"></a>Integrera med villkorsstyrd åtkomst

När du använder villkorsstyrd åtkomst kan du konfigurera principer för villkorsstyrd åtkomst så att de använder resultaten från enhetsefterlevnadsprinciperna för att avgöra vilka enheter som kan komma åt organisationens resurser. Den här åtkomstkontrollen är utöver och separat från åtgärder för inkompatibilitet som du inkluderar i efterlevnadsprinciper för enheter.

När en enhet registreras i Intune registreras den i Azure AD. Kompatibilitetsstatus för enheterna rapporteras till Azure AD. Om principerna för villkorsstyrd åtkomst har angetts till *Kräv att enheten har markerats som kompatibel*, använder villkorsstyrd åtkomst denna status för att avgöra om den ska bevilja eller blockera åtkomst till e-post och organisationens övriga resurser.

Om du kommer att använda efterlevnadsstatus för enheter med principer för villkorsstyrd åtkomst, granska hur din klientorganisation har konfigurerat *Markera enheter utan tilldelad efterlevnadsprincip som*, vilket du hanterar under [Inställningar för efterlevnadsprinciper](#compliance-policy-settings).

Mer information om hur du använder villkorsstyrd åtkomst med dina efterlevnadsprinciper för enheter finns i [Enhetsbaserad villkorsstyrd åtkomst](conditional-access-intune-common-ways-use.md#device-based-conditional-access)

Läs mer om villkorsstyrd åtkomst i Azure AD-dokumentationen:

- [Vad är villkorsstyrd åtkomst](/azure/active-directory/conditional-access/overview)
- [Vad är en enhetsidentitet](/azure/active-directory/device-management-introduction)

### <a name="reference-for-non-compliance-and-conditional-access-on-the-different-platforms"></a>Referens för inkompatibilitet och villkorsstyrd åtkomst på olika plattformar

Följande tabell beskriver också hur inkompatibla inställningar hanteras när en efterlevnadsprincip används med en princip för villkorlig åtkomst.

- **Åtgärdad**: Enhetens operativsystem tillämpar efterlevnad. Till exempel om användaren tvingas att ange en PIN-kod.

- **I karantän**: Enhetens operativsystem tillämpar inte efterlevnad. Till exempel tvingar Android- och Android Enterprise-enheter inte användaren att kryptera enheten. När enheten inte uppfyller efterlevnadskraven utförs följande åtgärder:
  - Enheten blockeras om en princip för villkorlig åtkomst tillämpas för användaren.
  - Företagsportalappen meddelar användaren om eventuella efterlevnadsproblem.

---------------------------

|**Principinställning**| **Plattform** |
| --- | ----|
| **Konfiguration av PIN-kod eller lösenord** | - **Android 4.0 och senare**: I karantän<br>- **Samsung Knox Standard 4.0 och senare**: I karantän<br>- **Android Enterprise**: I karantän  <br>  <br>- **iOS 8.0 och senare**: Åtgärdad<br>- **macOS 10.11 och senare**: Åtgärdad  <br>  <br>- **Windows 8.1 och senare**: Åtgärdad|
| **Enhetskryptering** | - **Android 4.0 och senare**: I karantän<br>- **Samsung Knox Standard 4.0 och senare**: I karantän<br>- **Android Enterprise**: I karantän<br><br>- **iOS 8.0 och senare**: Åtgärdad (genom angiven PIN-kod)<br>- **macOS 10.11 och senare**: Åtgärdad (genom angiven PIN-kod)<br><br>- **Windows 8.1 och senare**: Inte tillämpligt|
| **Jailbreakad eller rotad enhet** | - **Android 4.0 och senare**: I karantän (inte en inställning)<br>- **Samsung Knox Standard 4.0 och senare**: I karantän (inte en inställning)<br>- **Android Enterprise**: I karantän (inte en inställning)<br><br>- **iOS 8.0 och senare**: I karantän (inte en inställning)<br>- **macOS 10.11 och senare**: Inte tillämpligt<br><br>- **Windows 8.1 och senare**: Inte tillämpligt |
| **E-postprofil** | - **Android 4.0 och senare**: Inte tillämpligt<br>- **Samsung Knox Standard 4.0 och senare**: Inte tillämpligt<br>- **Android Enterprise**: Inte tillämpligt<br><br>- **iOS 8.0 och senare**: I karantän<br>- **macOS 10.11 och senare**: I karantän<br><br>- **Windows 8.1 och senare**: Inte tillämpligt |
| **Lägsta version av operativsystemet** | - **Android 4.0 och senare**: I karantän<br>- **Samsung Knox Standard 4.0 och senare**: I karantän<br>- **Android Enterprise**: I karantän<br><br>- **iOS 8.0 och senare**: I karantän<br>- **macOS 10.11 och senare**: I karantän<br><br>- **Windows 8.1 och senare**: I karantän|
| **Högsta version av operativsystemet** | - **Android 4.0 och senare**: I karantän<br>- **Samsung Knox Standard 4.0 och senare**: I karantän<br>- **Android Enterprise**: I karantän<br><br>- **iOS 8.0 och senare**: I karantän<br>- **macOS 10.11 och senare**: I karantän<br><br>- **Windows 8.1 och senare**: I karantän |
| **Attestering av hälsotillstånd i Windows** | - **Android 4.0 och senare**: Inte tillämpligt<br>- **Samsung Knox Standard 4.0 och senare**: Inte tillämpligt<br>- **Android Enterprise**: Inte tillämpligt<br><br>- **iOS 8.0 och senare**: Inte tillämpligt<br>- **macOS 10.11 och senare**: Inte tillämpligt<br><br>- **Windows 10**: I karantän<br>- **Windows 8.1 och senare**: I karantän |

---------------------------

## <a name="next-steps"></a>Nästa steg

- [Konfigurera platser](../protect/use-network-locations.md) för användning med Android-enheter
- [Skapa och distribuera princip](../protect/create-compliance-policy.md) och granska förhandskrav
- [Övervaka enhetsefterlevnad](../protect/compliance-policy-monitor.md)
- [Vanliga frågor, problem och lösningar med enhetsprinciper och profiler i Microsoft Intune](../configuration/device-profile-troubleshoot.md)
- [Referens för principentiteter](../developer/reports-ref-policy.md) har information om Intune Data Warehouse-principentiteter