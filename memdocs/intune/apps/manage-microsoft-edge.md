---
title: Hantera Microsoft Edge för iOS och Android med Intune
titleSuffix: ''
description: Använd Intunes policyer för appsäkerhet och konfigurering med Edge för iOS och Android till att skydda åtkomsten till företagets webbplatser.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/05/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2eb5a5e87b54fd8a92fc40c6d1295250d90b05c4
ms.sourcegitcommit: f6b14e6fe694a2a05c6ed92e67089e80a00a0908
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/17/2020
ms.locfileid: "88501192"
---
# <a name="manage-web-access-by-using-edge-for-ios-and-android-with-microsoft-intune"></a>Hantera webbåtkomst med Edge för iOS och Android med Microsoft Intune

Edge för iOS och Android är utformad för att användarna ska kunna surfa på webben och har stöd för flera identiteter. Användarna kan lägga till ett arbetskonto och ett personligt konto för surfning. De två identiteterna är helt separerade, vilket liknar vad som erbjuds i andra Microsoft-mobilappar.

Edge för iOS stöds på iOS 12.0 och senare. Edge för Android stöds på Android 5 och senare.

> [!NOTE]
> Edge för iOS och Android använder inte inställningar som användare anger för den inbyggda webbläsaren på sina enheter, eftersom Edge för iOS och Android inte har åtkomst till de här inställningarna.

De mest avancerade och bredaste skyddsfunktionerna för Office 365-data är tillgängliga när du prenumererar på sviten Enterprise Mobility + Security, som innehåller Microsoft Intune och Azure Active Directory Premium-funktioner, till exempel villkorsstyrd åtkomst. Du bör minst distribuera en princip för villkorsstyrd åtkomst som endast tillåter anslutning till Edge för iOS och Android från mobila enheter och en skyddsprincip för Intune-appen som garanterar att webbupplevelsen skyddas.

> [!NOTE]
> Nya webbklipp (fästa webbappar) på iOS-enheter öppnas i Microsoft Edge för iOS och Android i stället för Intune Managed Browser om det behövs för att öppna i en skyddad webbläsare. För äldre iOS-webbklipp måste du omdirigera dessa webbklipp för att se till att de öppnas i Microsoft Edge för iOS och Android i stället för Managed Browser.

## <a name="apply-conditional-access"></a>Tillämpa villkorsstyrd åtkomst
Organisationer kan använda principer för villkorsstyrd åtkomst i Azure AD för att säkerställa att användarna endast kan komma åt arbets- eller skolinnehåll med hjälp av Edge för iOS och Android. För att göra detta behöver du en princip för villkorsstyrd åtkomst som är riktad mot alla potentiella användare. Information om hur du skapar den här principen finns i [Kräva appskyddsprincip för åtkomst till molnapp med villkorsstyrd åtkomst](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Följ [Scenario 2: Webbläsarbaserade appar kräver godkända appar med appskyddsprinciper](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-2-browser-apps-require-approved-apps-with-app-protection-policies), vilket tillåter Edge för iOS och Android, men blockerar andra webbläsare för mobila enheter från att ansluta till Office 365-slutpunkter.

   >[!NOTE]
   > Den här principen garanterar att mobilanvändare kan komma åt alla Office 365-slutpunkter från Edge för iOS och Android. Den här principen förhindrar också att användare använder InPrivate för att få åtkomst till Office 365-slutpunkter.

Med villkorsstyrd åtkomst kan du också rikta in dig på lokala webbplatser som du har exponerat för externa användare via [Azure AD-programproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="create-intune-app-protection-policies"></a>Skapa appskyddsprinciper i Intune

Appskyddsprinciper (APP) definierar vilka appar som tillåts och vilka åtgärder de kan utföra med din organisations data. De alternativ som är tillgängliga i appskyddsprincipen gör det möjligt för organisationer att skräddarsy skyddet för deras specifika behov. För vissa är det inte alltid uppenbart vilka principinställningar som krävs för att implementera ett fullständigt scenario. För att hjälpa organisationer att prioritera härdning av mobilklientslutpunkter har Microsoft infört taxonomi för dataskyddsramverket med APP:er för mobilappshantering för iOS och Android.

Dataskyddsramverket för APP:er är indelat i tre olika konfigurationsnivåer där varje nivå bygger på den föregående nivån:

- **Grundläggande dataskydd för företag** (nivå 1) säkerställer att apparna skyddas med en PIN-kod, krypteras och utför åtgärder för selektiv rensning. För Android-enheter verifierar den här nivån Android-enhetsattestering. Det här är en konfiguration på ingångsnivå som ger liknande dataskyddskontroll som policyer för Exchange Online-postlådor och introducerar IT-avdelningen och användarna för APP.
- **Förbättrat dataskydd för företag** (nivå 2) introducerar APP-mekanismer för att förhindra dataläckage och minimikrav för operativsystem. Den här konfigurationen gäller för de flesta mobila användare som har åtkomst till arbets- eller skoldata.
- **Starkt dataskydd för företag** (nivå 3) introducerar avancerade mekanismer för dataskydd, förbättrad PIN-konfiguration och skydd mot mobila hot i appar. Den här konfigurationen passar för användare som hanterar skyddsvärda data.

Om du vill se specifika rekommendationer för varje konfigurationsnivå och minsta antal appar som måste skyddas går du till [Dataskyddsramverk med hjälp av appskyddsprinciper](app-protection-framework.md).

Oavsett om enheten har registrerats i en UEM-lösning (Unified Endpoint Management) måste en Intune-appskyddsprincip skapas för både iOS- och Android-appar med hjälp av stegen i [Hur du skapar och tilldelar skyddsprinciper för appar](app-protection-policies.md). Dessa principer måste minst uppfylla följande villkor:

1. De omfattar alla Microsoft 365-mobilappar som Edge, Outlook, OneDrive, Office eller Teams, eftersom det säkerställer att användare kan komma åt och ändra arbets- eller skoldata inom alla Microsoft-appar på ett säkert sätt.

2. De tilldelas alla användare. Detta säkerställer att alla användare skyddas, oavsett om de använder Edge för iOS eller Android.

3. Fastställ vilken ramverksnivå som uppfyller dina krav. De flesta organisationer bör implementera inställningarna som definierats i **Förbättrat dataskydd för företag** (nivå 2) som aktiverar dataskydds- och åtkomstkravskontroller.

Mer information om de tillgängliga inställningarna finns i [Inställningar för Android-appskyddsprinciper](app-protection-policy-settings-android.md) och [Inställningar för iOS-appskyddsprinciper](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> För att kunna tillämpa Intunes appskyddsprinciper mot appar på Android-enheter som inte är registrerade i Intune måste användaren också installera Intune-företagsportalen. Mer information finns i [Vad som händer när din Android-app hanteras av appskyddsprinciper](../fundamentals/end-user-mam-apps-android.md).

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>Enkel inloggning till Azure AD-anslutna webbappar i principskyddade webbläsare

Edge för iOS och Android kan dra nytta av enkel inloggning (SSO) till alla webbappar (SaaS och lokala) som är Azure AD-anslutna. Med enkel inloggning kan användare få åtkomst till Azure AD-anslutna webbappar via Edge för iOS och Android utan att behöva ange sina autentiseringsuppgifter på nytt.

Enkel inloggning kräver att din enhet har registrerats av antingen Microsoft Authenticator-appen för iOS-enheter eller på Intune-företagsportalen i Android. När användarna har något av dessa,uppmanas de att registrera sina enheter när de går till en Azure AD-ansluten webbapp i en principskyddad webbläsare (detta gäller bara om enheten inte redan är registrerad). När enheten är registrerad med användarens konto som hanteras av Intune kommer kontot att ha enkel inloggning aktiverat för Azure AD-anslutna webbappar.

> [!NOTE]
> Enhetsregistrering är en enkel incheckning med Azure AD-tjänsten. Det kräver inte fullständig enhetsregistrering och inte ger IT-avdelningen ytterligare behörighet på enheten.

## <a name="utilize-app-configuration-to-manage-the-browsing-experience"></a>Använd appkonfiguration för att hantera webbupplevelsen

Edge för iOS och Android stöder appinställningar som tillåter enhetlig slutpunktshantering, t.ex. Microsoft Endpoint Manager, så att administratörer kan anpassa appens beteende.

Appkonfigurationen kan antingen levereras via OS-kanalen för mobilenhetshantering (MDM) på registrerade enheter (kanalen [Hanterad appkonfiguration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) för iOS eller kanalen [Android i Enterprise](https://developer.android.com/work/managed-configurations) för Android) eller via Intune-kanalen för appskyddsprincip (APP). Edge för iOS och Android har stöd för följande konfigurationsscenarier:

- Tillåt endast arbets- eller skolkonton
- Allmänna appkonfigurationsinställningar
- Inställningar för dataskydd

> [!IMPORTANT]
> För konfigurationsscenarier som kräver enhetsregistrering på Android måste enheterna vara registrerade i Android Enterprise och Edge för Android måste distribueras via den hanterade Google Play-butiken. Mer information finns i [Konfigurera registrering av Android Enterprise-arbetsprofilenheter](../enrollment/android-work-profile-enroll.md) och [Lägg till appkonfigurationsprinciper för hanterade Android Enterprise-enheter](app-configuration-policies-use-android.md).

Varje konfigurationsscenario markerar sina specifika krav. Till exempel om konfigurationsscenariot kräver enhetsregistrering och därför fungerar med valfri UEM-leverantör, eller kräver Intune-appskyddsprinciper.

> [!NOTE]
> Med Microsoft Endpoint Manager kallas den appkonfiguration som levereras via MDM OS-kanalen en appkonfigurationsprincip (ACP) för **hanterade enheter**. Den appkonfiguration som levereras via kanalen för appskyddsprincip kallas en appkonfigurationsprincip för **hanterade appar**.

## <a name="only-allow-work-or-school-accounts"></a>Tillåt endast arbets- eller skolkonton

En oerhört viktig komponent för Microsoft 365 är respekten för våra största och högt reglerade kunders policyer för datasäkerhet och efterlevnad. Vissa företag har krav på att samla in all kommunikationsinformation i företagsmiljön och se till att enheterna endast används för företagskommunikation. För att stödja dessa krav kan Edge för iOS och Android på registrerade enheter konfigureras för att bara tillåta att ett enda företagskonto tillhandahålls i appen.

Du kan lära dig mer om hur du konfigurerar inställningen för organisationens tillåtna kontolägen här:

- [Android-inställning](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS-inställning](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Det här konfigurationsscenariot fungerar bara med registrerade enheter. En UEM-leverantör stöds dock. Om du inte använder Microsoft Endpoint Manager måste du titta i UEM-dokumentationen om hur du distribuerar dessa konfigurationsnycklar.

## <a name="general-app-configuration-scenarios"></a>Allmänna appkonfigurationsscenarier

Edge för iOS och Android ger administratörer möjlighet att anpassa standardkonfigurationen för flera inställningar i appen. Den här funktionen erbjuds för närvarande bara när Edge för iOS och Android har en Intune-appskyddsprincip tillämpad för det arbets- eller skolkonto som är inloggat i appen och principinställningarna levereras via en appkonfigurationsprincip för hanterade appar.

> [!IMPORTANT]
> Microsoft Edge för Android har inte stöd för Chromium-inställningar som är tillgängliga i Managed Google Play.

Edge har stöd för följande inställningar för konfiguration:

- Funktioner för sidan Ny flik
- Bokmärkesfunktioner
- Appbeteendefunktioner
- Funktioner för helskärmsläge

De här inställningarna kan distribueras till appen oavsett status för enhetsregistrering.

### <a name="new-tab-page-experiences"></a>Funktioner för sidan Ny flik

Edge för iOS och Android erbjuder organisationer flera alternativ för att anpassa funktionen för sidan Ny flik.

#### <a name="organization-logo-and-brand-color"></a>Organisationens logotyp och varumärkesfärg

Med de här inställningarna kan du anpassa sidan Ny flik för Microsoft Edge för iOS och Android och visa din organisations logotyp och varumärkesfärg som sidbakgrund.

För att ladda upp organisationens logotyp och färg utför du först följande steg:
1. I [Microsoft Endpoint Manager](https://endpoint.microsoft.com) navigerar du till **Administration av klientorganisation** -> **Anpassning** -> **Company Identity Branding (Företagsanpassning)** .
2. Om du vill ställa in ditt varumärkes logotyp väljer du ”Endast organisationslogotyp” bredvid **Visa i sidhuvud**. Transparenta bakgrundslogotyper rekommenderas.
3. Om du vill ange bakgrundsfärg för ditt varumärke väljer du en **Temafärg**. Edge för iOS och Android använder en ljusare nyans av färgen på sidan Ny flik, vilket gör att sidan har hög läsbarhet.

Använd sedan följande nyckel-/värdepar för att hämta din organisations varumärke till Edge för iOS och Android:

|    Tangent    |    Värde    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    Värdet **true** visar organisationens varumärkeslogotyp<br>Värdet **false** (standard) visar inte en logotyp    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    Värdet **true** visar organisationens varumärkesfärg<br>Värdet **false** (standard) visar inte en färg    |

#### <a name="homepage-shortcut"></a>Genväg till startsida

Med den här inställningen kan du konfigurera en genväg till startsidan för Edge för iOS och Android. Genvägen till startsidan som du konfigurerar visas som den första ikonen under sökfältet när användaren öppnar en ny flik i Edge för iOS och Android. Användaren kommer inte att kunna redigera eller ta bort den här genvägen i sin hanterade kontext. Genvägen till startsidan visar namnet på din organisation för att särskilja den. 

|    Tangent    |    Värde    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    Ange en giltig URL. Felaktiga URL:er är blockerade som en säkerhetsåtgärd.<br>Exempelvis: `https://www.bing.com`     |

#### <a name="multiple-top-site-shortcuts"></a>Flera genvägar till vanliga webbplatser

På samma sätt som du konfigurerar en genväg till startsidan kan du konfigurera flera genvägar till vanliga webbplatser på nya flikar i Edge för iOS och Android. Användaren kan inte redigera eller ta bort de här genvägarna i en hanterad kontext. Obs! Du kan konfigurera totalt åtta genvägar, inklusive genväg till en startsida. Om du har konfigurerat en genväg till en startsida, kommer det att åsidosätta den första webbplatsen på översta nivån som har konfigurerats. 

|    Tangent    |    Värde    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    Ange en uppsättning adressvärden. Varje genväg till en vanlig webbplats består av en rubrik och en webbadress. Avgränsa rubriken och URL:en med tecknet `|`.<br>Exempelvis: `GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

#### <a name="industry-news"></a>Branschnyheter

Du kan konfigurera upplevelsen på sidan Ny flik i Edge för iOS och Android så att den visar branschnyheter som är relevanta för din organisation. När du aktiverar den här funktionen använder Edge för iOS och Android din organisations domännamn för att samla nyheter från webben om din organisation, organisationens bransch och konkurrenter, så att användarna kan hitta relevanta externa nyheter från den centrala sidan Ny flik i Edge för iOS och Android. Branschnyheter är inaktiverat som standard. 

|    Tangent    |    Värde    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    Värdet **true** visar branschnyheter på sidan Ny flik<br>Värdet **false** (standard) döljer branschnyheter från sidan Ny flik    |

### <a name="bookmark-experiences"></a>Bokmärkesfunktioner

Edge för iOS och Android erbjuder organisationer flera alternativ för att hantera bokmärken.

#### <a name="managed-bookmarks"></a>Hanterade bokmärken

För enkel åtkomst kan du konfigurera bokmärken som du vill att användarna har tillgängliga när de använder Edge för iOS och Android.

- Bokmärken visas endast för arbets- eller skolkontot och visas inte för personliga konton.
- Bokmärken kan inte tas bort eller ändras av användare.
- Bokmärken visas överst i listan. Alla bokmärken som användare skapar visas under de här bokmärkena.
- Om du har aktiverat omdirigering av Application Proxy kan du lägga till Application Proxy-webbappar med antingen deras interna eller externa URL-adress.
- Lägg till prefixet **http://** eller **https://** till alla URL:er när du lägger till dem i listan.
- Bokmärken skapas i en mapp som namngivits efter organisationens namn som definieras i Azure Active Directory.

|    Tangent    |    Värde    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    Värdet för den här konfigurationen är en lista över bokmärken. Varje bokmärke består av bokmärkets rubrik och bokmärkets URL. Avgränsa rubriken och URL:en med tecknet `|`.<br> Exempelvis: `Microsoft Bing|https://www.bing.com`<p>Om du vill konfigurera fler bokmärken avgränsar du varje par med två tecken `||`.<br>Exempel:<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

#### <a name="my-apps-bookmark"></a>Bokmärket Mina appar

Som standard har användare bokmärket Mina appar konfigurerat i organisationsmappen i Edge för iOS och Android.

|    Tangent    |    Värde    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    Värdet **true** (standard) visar Mina appar bland bokmärkena för Edge för iOS och Android<br>Värdet **false** döljer Mina appar i Edge för iOS och Android    |

### <a name="app-behavior-experiences"></a>Appbeteendefunktioner

Edge för iOS och Android erbjuder organisationer flera alternativ för att hantera appens beteende.

#### <a name="default-protocol-handler"></a>Standardhanterare för protokoll

Som standard använder Edge för iOS och Android HTTPS-protokollhanteraren när användaren inte anger protokollet i URL:en. I allmänhet anses detta vara en bra metod, men den kan inaktiveras.

|    Tangent    |    Värde    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.defaultHTTPS     |     Värdet **true** (standard), standardhanterare för protokoll är HTTPS<br>Värdet **false**, standardhanterare för protokoll är HTTP     |

#### <a name="disable-data-sharing-for-personalization"></a>Inaktivera datadelning för anpassning

Som standard frågar Edge för iOS och Android användare om insamling av dataanvändning och delning av webbhistorik för att personanpassa deras surfupplevelse. Organisationer kan inaktivera delning av dessa data genom att förhindra att denna fråga visas för slutanvändarna.

|    Tangent    |    Värde    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.disableShareUsageData    |     Värdet **true** inaktiverar frågan så att den inte visas för slutanvändarna<br>Värdet **false** (standard) anger att användarna tillfrågas om att dela användningsdata    |
|     com.microsoft.intune.mam.managedbrowser.disableShareBrowsingHistory    |     Värdet **true** inaktiverar frågan så att den inte visas för slutanvändarna<br>Värdet **false** (standard) anger att användarna tillfrågas om att dela webbhistorik     |

#### <a name="disable-specific-features"></a>Inaktivera specifika funktioner

Edge för iOS och Android gör det möjligt för organisationer att inaktivera vissa funktioner som är aktiverade som standard. Konfigurera följande inställning för att inaktivera dessa funktioner:

|    Tangent    |    Värde    |
|-----------------------|-----------------------|
|    com.microsoft.intune.mam.managedbrowser.disabledFeatures    |    Värdet **password** inaktiverar frågor om att spara lösenord åt slutanvändaren<br>Värdet **inprivate** inaktiverar InPrivate-surfning<p>Om du vill inaktivera flera funktioner kan du separera värden med `|`. Om du till exempel vill inaktivera både InPrivate och lösenordslagring använder du `inprivate|password`.     |

> [!NOTE]
> Edge för Android stöder inte inaktivering av lösenordshanteraren.

#### <a name="disable-extensions"></a>Inaktivera tillägg

Du kan inaktivera tilläggsramverket inom Edge för Android för att hindra användare från att installera tilläggsappar. För att göra det, konfigurerar du följande inställning:

|    Tangent    |    Värde    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.disableExtensionFramework    |    Värdet **true** inaktiverar tilläggsramverket<br>Värdet **false** (standard) aktiverar tilläggsramverket    |

### <a name="kiosk-mode-experiences-on-android-devices"></a>Funktioner för helskärmsläge på Android-enheter

Edge för Android kan aktiveras som en helskärmsapp med följande inställningar:

|    Tangent    |    Värde    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.enableKioskMode    |    Värdet **true** aktiverar helskärmsläge för Edge för Android<br>Värdet **false** (standard) inaktiverar helskärmsläge    |
|    com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode    |    Värdet **true** visar adressfältet i helskärmsläge<br> Värdet **false** (standard) döljer adressfältet när helskärmsläge är aktiverat    |
|    com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode    |    Värdet **true** visar det nedersta åtgärdsfältet i helskärmsläge<br> Värdet **false** (standard) döljer det nedersta fältet när helskärmsläge är aktiverat    |

## <a name="data-protection-app-configuration-scenarios"></a>Appkonfigurationsscenarier för dataskydd

Edge för iOS och Android stöder appkonfigurationsprinciper för följande inställningar för dataskydd när appen hanteras av Microsoft Endpoint Manager med en Intune-appskyddsprincip tillämpad på arbets- eller skolkontot som är inloggat i appen och principinställningarna levereras via en appkonfigurationsprincip för hanterade appar:

- Hantera kontosynkronisering
- Hantera begränsade webbplatser
- Hantera proxykonfiguration
- Hantera webbplatser för enkel inloggning med NTLM

De här inställningarna kan distribueras till appen oavsett status för enhetsregistrering.

### <a name="manage-account-synchronization"></a>Hantera kontosynkronisering

Som standard ger Microsoft Edge-synkronisering användarna åtkomst till sina webbläsardata på alla sina inloggade enheter. Data som stöds av synkronisering inkluderar:

- Favoriter
- Lösenord
- Adresser med mera (automatisk ifyllning i formulär)

Synkroniseringsfunktionen aktiveras via användarmedgivande och användarna kan aktivera eller inaktivera synkronisering för var och en av de datatyper som anges ovan. Mer information finns i [Microsoft Edge-synkronisering](https://docs.microsoft.com/DeployEdge/microsoft-edge-enterprise-sync).

Organisationer har möjlighet att inaktivera Edge-synkronisering på iOS och Android. 

|Tangent  |Värde  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.account.syncDisabled     |Värdet **true** (standard) tillåter Edge-synkronisering<br>Värdet **false** inaktiverar Edge-synkronisering          |

### <a name="manage-restricted-web-sites"></a>Hantera begränsade webbplatser

Organisationer kan definiera vilka webbplatser som användare kan komma åt inom arbets- eller skolkontokontexten i Edge för iOS och Android. Om du använder en lista över tillåtna kan användarna bara komma åt webbplatser som uttryckligen angetts. Om du använder en lista över blockerade får användarna åtkomst till alla webbplatser utom de platser som uttryckligen blockerats. Du bör endast införa antingen listan över tillåtna eller blockerade listan, inte båda. Om du inför båda kommer listan över tillåtna att respekteras.

Organisationen definierar också vad som händer när en användare försöker navigera till en begränsad webbplats. Dessa övergångar tillåts som standard. Om organisationen tillåter det kan begränsade webbplatser öppnas i den personliga kontokontexten, i Azure AD-kontots InPrivate-kontext eller om webbplatsen är helt blockerad. Mer information om de olika scenarier som stöds finns i [Begränsade webbplatsövergångar i Microsoft Edge för mobil](https://techcommunity.microsoft.com/t5/intune-customer-success/restricted-website-transitions-in-microsoft-edge-mobile/ba-p/1381333). Genom att tillåta övergångar förblir organisationens användare skyddade, samtidigt som företagets resurser är säkra.

> [!NOTE]
> Edge för iOS och Android kan endast blockera åtkomst till webbplatser när de öppnas direkt. Den blockerar inte åtkomst när användare använder mellanliggande tjänster (till exempel en översättningstjänst) för åtkomst till webbplatsen.

Använd nyckel/värde-paren nedan för att konfigurera en lista över tillåtna eller blockerade webbplatser för Edge för iOS och Android. 

|Tangent  |Värde  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs     |Motsvarande värde för nyckeln är en lista med URL:er. Du anger alla URL:er som du vill tillåta som ett enda värde, avgränsade med ett vertikalstreck `|`.<p>**Exempel:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs     |Motsvarande värde för nyckeln är en lista med URL:er. Du anger alla URL:er som du vill blockera som ett enda värde, avgränsade med ett vertikalstreck `|`.<br>**Exempel:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock     |Värdet **true** (standard) tillåter att iOS och Android att övergår till begränsade webbplatser. När personliga konton inte är inaktiverade uppmanas användarna att antingen växla till den personliga kontexten för att öppna den begränsade webbplatsen eller lägga till ett personligt konto. Om com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked har angetts som true kan användarna öppna den begränsade webbplatsen i InPrivate-kontexten.<p>Värdet **false** förhindrar övergång för användare i Edge för iOS och Android. Användare får helt enkelt se ett meddelande om att webbplatsen de försöker besöka är blockerad.         |
|com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked     |Värdet **true** tillåter att begränsade webbplatser öppnas i Azure AD-kontots InPrivate-kontext. Om Azure AD-kontot är det enda konto som konfigurerats i Edge för iOS och Android, öppnas den begränsade webbplatsen automatiskt i InPrivate-kontexten. Om användaren har konfigurerat ett personligt konto uppmanas användaren att välja mellan att öppna InPrivate eller växla till det personliga kontot.<p> Värdet **false** (standard) kräver att den begränsade webbplatsen öppnas i användarens personliga konto. Om personliga konton är inaktiverade blockeras webbplatsen.<p>För att den här inställningen ska börja gälla måste com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock anges som true.          |
|com.microsoft.intune.mam.managedbrowser.durationOfOpenInPrivateSnackBar     | Ange hur många sekunder som användare ska se meddelandet ”Länken öppnades med InPrivate-läge. Din organisation kräver att InPrivate-läge används för det här innehållet.” Som standard visas meddelandet i 7 sekunder.

Följande webbplatser är alltid tillåtna oavsett inställningarna i tillåtetlistan eller blockeratlistan:
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

#### <a name="url-formats-for-allowed-and-blocked-site-list"></a>URL-format för listan över tillåtna och blockerade webbplatser 

Du kan använda olika URL-format för att skapa dina webbplatslistor med tillåtna/blockerade. De här tillåtna mönstren beskrivs i tabellen nedan.

- Lägg till prefixet **http://** eller **https://** till alla URL:er när du lägger till dem i listan.
- Du kan använda jokertecknet (\*) enligt reglerna i följande lista med tillåtna mönster.
- Ett jokertecken kan endast motsvara hela värdnamnet (avgränsat med punkter) eller hela delar av sökvägen (avgränsade med snedstreck). `http://*contoso.com` och  **stöds till exempel inte**.
- Du kan ange portnummer i adressen. Om du inte anger ett portnummer, används följande värden:
  - Port 80 för http
  - Port 443 för http
- Jokertecken i portnummer stöds **inte**. `http://www.contoso.com:*` och `http://www.contoso.com:*/` stöds inte. 

    |    URL    |    Information    |    Matchar    |    Matchar inte    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    Matchar en enstaka sida    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    Matchar en enstaka sida    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*`   |    Matchar alla URL:er som börjar med `www.contoso.com`    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    Matchar alla underordnade domäner under `contoso.com`    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    Matchar alla underordnade som slutar med `contoso.com/`    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
    `http://www.contoso.com/images`    |    Matchar en enstaka mapp    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    Matchar en enstaka sida, med ett portnummer    |    `http://www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    Matchar en enstaka, säker sida    |    `https://www.contoso.com`    |    `http://www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    Matchar en enstaka mapp och alla undermappar    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- Följande är några exempel på indata som du inte kan ange:
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - IP-adresser
  - `https://*`
  - `http://*`
  - `https://*contoso.com`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

### <a name="manage-proxy-configuration"></a>Hantera proxykonfiguration

Edge för iOS och Android och [Azure AD-programproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) kan användas tillsammans för att ge användare åtkomst till intranätplatser på deras mobila enheter. Exempel: 

- En användare använder Outlook-mobilappen som skyddas av Intune. Användaren klickar sedan på en länk till en intranätplats i ett e-postmeddelande och Edge för iOS och Android identifierar att den här intranätplatsen har gjorts tillgänglig för användaren via programproxyn. Användaren omdirigeras automatiskt via programproxyn för att autentisera med alla tillämpliga multifaktorautentiseringar och principer för villkorlig åtkomst innan de når intranätplatsen. Användaren kan nu komma åt interna webbplatser även på sina mobila enheter, och länken i Outlook fungerar som förväntat.
- En användare öppnar Edge för iOS och Android på sin iOS- eller Android-enhet. Om Edge för iOS och Android skyddas med Intune, och programproxyn är aktiverad, kan användaren gå till en intranätplats med den interna URL:en som brukar användas. Edge för iOS och Android identifierar att den här intranätplatsen har gjorts tillgänglig för användaren med programproxyn. Användaren omdirigeras automatiskt via programproxyn för att autentisera innan de når intranätplatsen. 

Innan du börjar:

- Konfigurera dina interna program via Azure AD-programproxyn.
  - Se [installationsdokumentationen](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy) för att konfigurera programproxy och publicera program.
- Appen Edge för iOS och Android måste ha en [Intune-appskyddsprincip](app-protection-policy.md) tilldelad.
- Microsoft-appar måste ha en appskyddsprincip som har inställningen **Begränsa överföring av webbinnehåll till andra appar** för dataöverföring inställd på **Microsoft Edge**.

> [!NOTE]
> Det kan ta upp till 24 timmar innan omdirigeringsdata för en uppdaterad programproxy börjar gälla i Edge för iOS och Android.

Rikta nyckel/värde-paret nedan för Edge för iOS för att aktivera programproxyn:

|    Tangent    |    Värde    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    Värdet **true** aktiverar scenarier för omdirigering av proxy i Azure AD App<br>Värdet **false** (standard) förhindrar proxyscenarier i Azure AD App    |

> [!NOTE]
> Edge för Android använder inte den här nyckeln. I stället använder Edge för Android konfigurationen för Azure AD-programproxy automatiskt så länge det inloggade Azure AD-kontot har en appskyddsprincip tillämpad.

Mer information om hur du kan använda Edge för iOS och Android och en Azure AD-programproxy tillsammans för sömlös (och skyddad) åtkomst till lokala webbappar finns i [Bättre tillsammans: Intune och Azure Active Directory samarbetar för att förbättra användaråtkomsten](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254). Det här blogginlägget hänvisar till Intune Managed Browser, men innehållet gäller även för Edge för iOS och Android.

### <a name="manage-ntlm-single-sign-on-sites"></a>Hantera webbplatser för enkel inloggning med NTLM

Organisationer kan kräva att användare autentiseras med NTLM för att komma åt intranätswebbplatser. Som standard uppmanas användarna att ange autentiseringsuppgifter varje gång de ansluter till en webbplats som kräver NTLM-autentisering eftersom cachelagring av NTLM-autentiseringsuppgifter är inaktiverat. 

Organisationer kan aktivera cachelagring av NTLM-autentiseringsuppgifter för vissa webbplatser. För dessa webbplatser cachelagras autentiseringsuppgifterna som standard i 30 dagar efter att användaren har angett autentiseringsuppgifter och autentiserats.


|Tangent  |Värde  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.NTLMSSOURLs     |Motsvarande värde för nyckeln är en lista med URL:er. Du anger alla URL:er som du vill tillåta som ett enda värde, avgränsade med ett vertikalstreck `|`.<p>**Exempel:**<br>`URL1|URL2`<br>`http://app.contoso.com/|https://expenses.contoso.com`<p>Mer information om vilka typer av URL-format som stöds finns i [URL-format för listan över tillåtna och blockerade webbplatser](#url-formats-for-allowed-and-blocked-site-list).         |
|com.microsoft.intune.mam.managedbrowser.durationOfNTLMSSO     |Antal timmar som autentiseringsuppgifter cachelagras, standardvärdet är 720 timmar         |

## <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Distribuera konfigurationsscenarier för appar med Microsoft Endpoint Manager

Om du använder Microsoft Endpoint Manager som leverantör för mobilappshantering kan du använda följande steg för att skapa en appkonfigurationsprincip för hanterade appar. När konfigurationen har skapats kan du tilldela dess inställningar till grupper av användare.

1. Logga in på [Microsoft Endpoint Manager](https://endpoint.microsoft.com).

2. Välj **Appar** och sedan **Appkonfigurationsprinciper**.

3. På bladet **Appkonfigurationsprinciper** väljer du **Lägg till** och väljer **Hanterade appar**.

4. I avsnittet **Grundläggande** anger du ett **Namn** och en valfri **Beskrivning** för appkonfigurationsinställningarna.

5. För **Offentliga appar** väljer du **Välj offentliga appar**. Gå sedan till bladet **Riktade appar** och välj **Edge för iOS och Android** genom att välja både iOS- och Android-plattformsapparna. Klicka på **Välj** för att spara de valda offentliga apparna.

6. Klicka på **Nästa** för att slutföra de grundläggande inställningarna för appens konfigurationsprincip.

7. I avsnittet **Inställningar** expanderar du **Edge-konfigurationsinställningarna**.

8. Om du vill hantera inställningarna för dataskydd konfigurerar du önskade inställningar på motsvarande sätt:

    - För **Omdirigering av programproxy** väljer du bland de tillgängliga alternativen: **Aktivera**, **Inaktivera** (standard).

    - För **URL för genväg till startsida** anger du en giltig URL som innehåller antingen prefixet *http://* eller *https://* . Felaktiga URL:er är blockerade som en säkerhetsåtgärd.

    - För **Hanterade bokmärken** anger du titel och en giltig URL som innehåller antingen prefixet *http://* eller *https://* .

    - För **Tillåtna URL:er** anger du en giltig URL (endast dessa URL:er tillåts, inga andra webbplatser kan nås). Mer information om vilka typer av URL-format som stöds finns i [URL-format för listan över tillåtna och blockerade webbplatser](#url-formats-for-allowed-and-blocked-site-list).

    - För **Blockerade URL:er** anger du en giltig URL (endast dessa URL:er blockeras). Mer information om vilka typer av URL-format som stöds finns i [URL-format för listan över tillåtna och blockerade webbplatser](#url-formats-for-allowed-and-blocked-site-list).

    - För **Omdirigera ej betrodda webbplatser till privat kontext** väljer du bland de tillgängliga alternativen: **Aktivera** (standard), **Inaktivera**.

    > [!NOTE]
    > Om både Tillåtna URL:er och Blockerade URL:er definieras i principen är det endast listan över tillåtna som följs.

9. Om du vill lägga till ytterligare konfigurationsinställningar för appar som inte visas i principen ovan, expanderar du noden **Allmänna konfigurationsinställningar** och anger nyckel/värde-par enligt detta.

10. När du har konfigurerat inställningarna väljer du **Nästa**.

11. I avsnittet **Tilldelningar** väljer du **Välj grupper som ska inkluderas**. Välj den Azure AD-grupp som du vill tilldela appkonfigurationsprincipen och sedan **Välj**.

12. När du är färdig med tilldelningarna väljer du **Nästa**.

13. På bladet **Skapa appkonfigurationsprincip Granska + skapa** granskar du inställningarna som har konfigurerats och väljer **Skapa**.

Den nya konfigurationsprincipen visas på bladet **Appkonfiguration**.

## <a name="use-edge-for-ios-and-android-to-access-managed-app-logs"></a>Använda Edge för iOS och Android till att komma åt loggar för hanterade appar

Användare med Edge för iOS och Android installerad på sin iOS- eller Android-enhet kan se hanteringsstatus för alla appar som har publicerats av Microsoft. De kan skicka loggar för att felsöka sina hanterade iOS- eller Android-appar med hjälp av följande steg:

1. Öppna Edge för iOS och Android på enheten.
2. Skriv in `about:intunehelp` i adressrutan.
3. Edge för iOS och Android startar felsökningsläge.

En lista över de inställningar som finns lagrade i apploggarna finns i [Granska loggarna för klientappskydd](app-protection-policy-settings-log.md).

Mer information om hur du visar loggar på Android-enheter finns i [Skicka loggar till IT-administratören via e-post](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android).

## <a name="next-steps"></a>Nästa steg

- [Vad är appskyddsprinciper?](app-protection-policy.md) 
- [Appkonfigurationsprinciper för Microsoft Intune](app-configuration-policies-overview.md)
