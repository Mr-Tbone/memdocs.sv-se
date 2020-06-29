---
title: Hantera Office för iOS och Android med Intune
titleSuffix: ''
description: Använd Intunes policyer för appsäkerhet och konfigurering med Office för iOS och Android för att skydda åtkomsten till olika samarbetsmiljöer.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41b85299057f172fec224873607509aaaec60024
ms.sourcegitcommit: c7afcc3a2232573091c8f36d295a803595708b6c
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/17/2020
ms.locfileid: "84977286"
---
# <a name="manage-collaboration-experiences-using-office-for-ios-and-android-with-microsoft-intune"></a>Hantera samarbetsmiljön med Office för iOS och Android med Microsoft Intune

Office för iOS och Android har flera viktiga fördelar, bland annat följande:

- Kombinera Word, Excel och PowerPoint på ett sätt som gör miljön enklare med färre appar att ladda ned och växla mellan. Det krävs betydligt mindre telefonlagring än att installera enskilda appar samtidigt som du får praktiskt taget alla funktioner från befintliga mobilappar som användarna redan känner till och använder.
- Integrera Office Lens-teknik för att ge kameran funktioner som att konvertera bilder till redigerbara Word- och Excel-dokument, skanna PDF-filer och fånga tavelskrift med automatiska digitala förbättringar som gör det enklare att läsa innehållet.
- Lägg till nya funktioner för vanliga uppgifter som ofta uppstår vid arbete på telefonen, som att göra snabba anteckningar, signera PDF-filer, skanna QR-koder och överföra filer mellan enheter.

De mest avancerade och bredaste skyddsfunktionerna för Office 365-data är tillgängliga när du prenumererar på sviten Enterprise Mobility + Security, som innehåller Microsoft Intune och Azure Active Directory Premium-funktioner, till exempel villkorsstyrd åtkomst. Du bör minst distribuera en princip för villkorsstyrd åtkomst som tillåter anslutning till Office för iOS och Android från mobila enheter och en säkerhetspolicy i Intune-appen som skyddar samarbetsmiljön.

## <a name="apply-conditional-access"></a>Tillämpa villkorsstyrd åtkomst
Organisationer kan använda principer för villkorsstyrd åtkomst i Azure AD för att säkerställa att användarna endast kan komma åt arbets- eller skolinnehåll med hjälp av Office för iOS och Android. För att göra detta behöver du en princip för villkorsstyrd åtkomst som är riktad mot alla potentiella användare. Information om hur du skapar den här principen finns i [Kräva appskyddsprincip för åtkomst till molnapp med villkorsstyrd åtkomst](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Följ ”Steg 1: Konfigurera en Azure AD-princip för villkorsstyrd åtkomst för Office 365” i [Scenario 1: Office 365-appar kräver godkända appar med appskyddsprinciper](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), vilket tillåter Office för iOS och Android men blockerar andra enhetsklienter med OAuth-funktion från trejde part från att ansluta till Office 365-slutpunkter.

   >[!NOTE]
   > Den här policyn gör att mobila användare kan komma åt alla Office-slutpunkter via lämpliga appar.

## <a name="create-intune-app-protection-policies"></a>Skapa appskyddsprinciper i Intune

Appskyddsprinciper (APP) definierar vilka appar som tillåts och vilka åtgärder de kan utföra med din organisations data. De alternativ som är tillgängliga i appskyddsprincipen gör det möjligt för organisationer att skräddarsy skyddet för deras specifika behov. För vissa är det inte alltid uppenbart vilka principinställningar som krävs för att implementera ett fullständigt scenario. För att hjälpa organisationer att prioritera härdning av mobilklientslutpunkter har Microsoft infört taxonomi för dataskyddsramverket med APP:er för mobilappshantering för iOS och Android.

Dataskyddsramverket för APP:er är indelat i tre olika konfigurationsnivåer där varje nivå bygger på den föregående nivån:

- **Grundläggande dataskydd för företag** (nivå 1) säkerställer att apparna skyddas med en PIN-kod, krypteras och utför åtgärder för selektiv rensning. För Android-enheter verifierar den här nivån Android-enhetsattestering. Det här är en konfiguration på ingångsnivå som ger liknande dataskyddskontroll som policyer för Exchange Online-postlådor och introducerar IT-avdelningen och användarna för APP.
- **Förbättrat dataskydd för företag** (nivå 2) introducerar APP-mekanismer för att förhindra dataläckage och minimikrav för operativsystem. Den här konfigurationen gäller för de flesta mobila användare som har åtkomst till arbets- eller skoldata.
- **Starkt dataskydd för företag** (nivå 3) introducerar avancerade mekanismer för dataskydd, förbättrad PIN-konfiguration och skydd mot mobila hot i appar. Den här konfigurationen passar för användare som hanterar skyddsvärda data.

Om du vill se specifika rekommendationer för varje konfigurationsnivå och minsta antal appar som måste skyddas går du till [Dataskyddsramverk med hjälp av appskyddsprinciper](app-protection-framework.md).

Oavsett om enheten har registrerats i en UEM-lösning (Unified Endpoint Management) måste en Intune-appskyddsprincip skapas för både iOS- och Android-appar med hjälp av stegen i [Hur du skapar och tilldelar skyddsprinciper för appar](app-protection-policies.md). Dessa principer måste minst uppfylla följande villkor:

1. De omfattar alla Microsoft 365-mobilappar som Edge, Outlook, OneDrive, Office eller Teams, eftersom det säkerställer att användare kan komma åt och ändra arbets- eller skoldata inom alla Microsoft-appar på ett säkert sätt.

2. De tilldelas alla användare. Det här gör att alla användare skyddas, oavsett om de använder Office för iOS eller Android.

3. Fastställ vilken ramverksnivå som uppfyller dina krav. De flesta organisationer bör implementera inställningarna som definierats i **Förbättrat dataskydd för företag** (nivå 2) som aktiverar dataskydds- och åtkomstkravskontroller.

Mer information om de tillgängliga inställningarna finns i [Inställningar för Android-appskyddsprinciper](app-protection-policy-settings-android.md) och [Inställningar för iOS-appskyddsprinciper](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> För att kunna tillämpa Intunes appskyddsprinciper mot appar på Android-enheter som inte är registrerade i Intune måste användaren också installera Intune-företagsportalen. Mer information finns i [Vad som händer när din Android-app hanteras av appskyddsprinciper](../fundamentals/end-user-mam-apps-android.md).

## <a name="utilize-app-configuration"></a>Använda appkonfigurering

Office för iOS och Android har stöd för appinställningar som gör att administratörer för enhetlig slutpunktshantering som Microsoft Endpoint Manager kan anpassa appens beteende.

Appkonfigurationen kan antingen levereras via OS-kanalen för mobilenhetshantering (MDM) på registrerade enheter (kanalen [Hanterad appkonfiguration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) för iOS eller kanalen [Android i Enterprise](https://developer.android.com/work/managed-configurations) för Android) eller via Intune-kanalen för appskyddsprincip (APP). Office för iOS och Android har stöd för följande konfigurationsscenarier:

- Tillåt endast arbets- eller skolkonton
- Inställningar för dataskydd

> [!IMPORTANT]
> För konfigurationsscenarier som kräver enhetsregistrering i Android måste enheterna vara registrerade i Android Enterprise och Office för Android måste distribueras via den hanterade Google Play-butiken. Mer information finns i [Konfigurera registrering av Android Enterprise-arbetsprofilenheter](../enrollment/android-work-profile-enroll.md) och [Lägg till appkonfigurationsprinciper för hanterade Android Enterprise-enheter](app-configuration-policies-use-android.md).

Varje konfigurationsscenario markerar sina specifika krav. Till exempel om konfigurationsscenariot kräver enhetsregistrering och därför fungerar med valfri UEM-leverantör, eller kräver Intune-appskyddsprinciper.

> [!NOTE]
> Med Microsoft Endpoint Manager kallas den appkonfiguration som levereras via MDM OS-kanalen en appkonfigurationsprincip (ACP) för **hanterade enheter**. Den appkonfiguration som levereras via kanalen för appskyddsprincip kallas en appkonfigurationsprincip för **hanterade appar**.

## <a name="only-allow-work-or-school-accounts"></a>Tillåt endast arbets- eller skolkonton

En oerhört viktig komponent för Microsoft 365 är respekten för våra största och högt reglerade kunders policyer för datasäkerhet och efterlevnad. Vissa företag har krav på att samla in all kommunikationsinformation i företagsmiljön och se till att enheterna endast används för företagskommunikation. Som stöd för de här kraven kan Office för iOS och Android på registrerade enheter konfigureras för att bara tillåta att ett enda företagskonto etableras i appen.

Du kan lära dig mer om hur du konfigurerar inställningen för organisationens tillåtna kontolägen här:

- [Android-inställning](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Det här konfigurationsscenariot fungerar bara med registrerade enheter. En UEM-leverantör stöds dock. Om du inte använder Microsoft Endpoint Manager måste du titta i UEM-dokumentationen om hur du distribuerar dessa konfigurationsnycklar.

> [!NOTE]
> För tillfället är det bara Office för Android som har stöd för läget med konton som organisationen tillåter.

## <a name="data-protection-app-configuration-scenarios"></a>Appkonfigurationsscenarier för dataskydd

Office för iOS och Android har stöd för appkonfigurationspolicyer för följande dataskyddsinställningar när appen hanteras av Microsoft Endpoint Manager med en Intune-appskyddspolicy tillämpad på arbets- eller skolkontot som är inloggat i appen:

- Hantera filöverföringar via åtgärden Överför filer
- Hantera filöverföringar via åtgärden Dela i närheten

De här inställningarna kan distribueras till appen oavsett status för enhetsregistrering.

### <a name="manage-file-transfers"></a>Hantera filöverföringar

Som standard gör Office så att användare kan dela filer med användare i närheten och överföra filer till stationära system.

|    Tangent    |    Värde    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.office.ShareNearby.IsAllowed.IntuneMAMOnly    |    **true** (standardvärde) aktiverar funktionen Dela i närheten för arbets- eller skolkontot<br>**false** inaktiverar funktionen Dela i närheten för arbets- eller skolkontot    |
|    com.microsoft.office.TransferFiles.IsAllowed.IntuneMAMOnly    |    **true** (standardvärde) aktiverar funktionen Överför filer för arbets- eller skolkontot<br>**false** inaktiverar funktionen Överför filer för arbets- eller skolkontot    |

### <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Distribuera konfigurationsscenarier för appar med Microsoft Endpoint Manager

Om du använder Microsoft Endpoint Manager som MAM-provider kan du läsa mer om att skapa en konfigurationspolicy för hanterade appar i dataskyddsappen i [Lägga till konfigurationspolicyer för hanterade appar utan enhetsregistrering](app-configuration-policies-managed-app.md). När du har skapat konfigurationen kan du tilldela policyn till grupper av användare.

## <a name="next-steps"></a>Nästa steg

- [Vad är appskyddsprinciper?](app-protection-policy.md) 
- [Appkonfigurationsprinciper för Microsoft Intune](app-configuration-policies-overview.md)