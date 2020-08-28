---
title: Nyheter i Desktop Analytics
titleSuffix: Configuration Manager
description: En sammanfattning av de nya funktionerna i den senaste månads versionen av moln tjänsten för Skriv bords analys.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: dd188b80375861cd08784d0574e737bfce7f2d92
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993154"
---
# <a name="whats-new-in-desktop-analytics"></a>Nyheter i Desktop Analytics

Lär dig vad som är nytt varje månad i Skriv bords analys.

> [!TIP]
> Varje månads uppdatering kan ta upp till tre dagar innan distributionen. Vissa funktioner kan distribueras över flera veckor och kanske inte är tillgängliga för alla kunder den första veckan.

Om du vill få ett meddelande när den här sidan uppdateras kopierar du och klistrar in följande URL i din RSS-feed läsare: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="august-2020"></a>Augusti 2020

### <a name="apps-deployed-from-configuration-manager-are-important-by-default"></a>Appar som distribueras från Configuration Manager är viktiga som standard

<!-- 4859763 -->

**Prioritets** konfigurationen för en app är nödvändig för Skriv bords analys för att fastställa vilka enheter som ska ingå i pilot distributioner. En administratör behövde manuellt konfigurera prioriteten för alla appar i Skriv bords analys. Endast när du har validerat piloten kan du fortsätta med en produktions distribution.

Nu för alla appar som du distribuerar med Configuration Manager konfigureras Skriv bords analys automatiskt som standard. Med det här beteendet kan du konfigurera apparna i din miljö snabbare, så att de fortskrider snabbare med en produktions distribution.

Mer information finns i [Asset-Apps](about-assets.md#apps).

<!-- 6049643 -->

### <a name="improved-processing-of-diagnostic-data-during-snapshot-generation"></a>Förbättrad bearbetning av diagnostikdata under skapandet av ögonblicks bilder

Microsoft har förbättrat hur de samlar in och bearbetar Windows-diagnostikdata från enheter som registrerats i Skriv bords analys. Dessa förbättringar ökar tillförlitligheten för den dagliga ögonblicks bilds genereringen och förbereder för nya funktioner i utvecklingen. Som ett resultat av detta arbete inaktiverade Microsoft tillfälligt antalet **enheter som startade den här appen under de senaste 30 dagarna** i distributions planer. Mer information finns i [Asset-Apps](about-assets.md#usage).

## <a name="july-2020"></a>Juli 2020

### <a name="windows-10-version-2004-now-available-in-desktop-analytics"></a>Windows 10, version 2004, nu tillgängligt i Desktop Analytics

<!-- 7370207 -->

När du övervakar säkerhets-och funktions uppdateringar i Skriv bords analys portalen visas nu Windows 10, version 2004. När du skapar en distributions plan kan du välja Windows 10, version 2004, som mål version.

### <a name="improved-support-for-viewing-the-portal-from-any-device"></a>Förbättrat stöd för att Visa portalen från valfri enhet

<!-- 6270240 -->

Nu kan du Visa Skriv bords analys portalen i administrations centret för Microsoft Endpoint Manager från olika enhets typer. Nu uppfyller rikt linjerna för tillgänglighet för webb innehåll (WCAG) 2,1 för en bildskärms upplösning som är låg som 320 x 256 bild punkter. Följande bild är till exempel av portalen från en Apple iPhone 8:

:::image type="content" source="media/dashboard-iphone8.png" alt-text="Skriv bords analys Portal på en iPhone 8":::

### <a name="notifications-for-service-impacting-events"></a>Meddelanden om händelser som påverkar tjänsten

<!-- 4982509 -->

Skriv bords analys portalen kan nu Visa meddelande banderoller. Dessa aviseringar gör att Microsoft kan kommunicera med dig om viktiga händelser och problem. Till exempel kända problem med tjänsten, data fördröjningen eller nya krav. Mer information finns i [tjänst aviseringar](troubleshooting.md#service-notifications).

## <a name="june-2020"></a>Juni 2020

### <a name="improvement-to-prerequisites"></a>Förbättringar av krav

Skriv bords analys kräver inte längre att du distribuerar en Microsoft 365 tjänst i din Azure Active Directory (Azure AD)-klient. **Office 365-klient admin** -appen i Azure AD är nu appen för **Skriv bords analys** , för att aktivera Configuration Manager hämtning av information och status från tjänsten.

## <a name="may-2020"></a>Maj 2020

### <a name="reduce-the-number-of-apps-for-review"></a>Minska antalet appar för granskning

<!-- 5542186 -->

För att hjälpa till att konsolidera och minska antalet appar som visas på sidan till gångar i portalen kombinerar den nu alla versioner av appar med samma namn och utgivare. Antalet appar i panelen för att ange appar visas **i den här** inställningen. I stället för hundratals instanser av Microsoft Edge finns det till exempel en instans för alla versioner. Du kan fatta beslut en gång för alla versioner. Om du behöver fatta beslut om vissa versioner av en app kan du konfigurera det här beteendet.

Mer information finns i [om till gångar – appar](about-assets.md#apps).

## <a name="march-2020"></a>Mars 2020

### <a name="support-for-multiple-hierarchies"></a>Stöd för flera hierarkier

<!-- 4814075, 6079184 -->

Nu kan du ansluta flera Configuration Manager hierarkier till en enda Azure Active Directory-klient med ett enda kommersiellt ID för Skriv bords analys. Portalen kategoriserar enheter från olika hierarkier och förbättrar upplevelsen för globala pilot-och distributions planer.

- När du konfigurerar din globala pilot visas en varning om du inkluderar samlingar som innehåller fler än 20% av dina totala registrerade enheter.
- När du skapar en distributions plan visar portalen en varning om du väljer samlingar för flera hierarkier.

> [!NOTE]
> Stöd för flera hierarkier kräver Configuration Manager version 1910 eller senare.

Mer information finns i följande artiklar:

- [Global pilot](deploy-pilot.md#bkmk_GlobalPilot)
- [Så här skapar du distributions planer](create-deployment-plans.md)

### <a name="identify-compatibility-safeguards"></a>Identifiera kompatibilitet för skydd

<!-- 5746559 -->

Windows-kompatibilitetsproblem klassificerar vissa appar och driv rutiner med en *skydds*åtgärd, vilket kan leda till att Windows 10 Miss lyckas eller återställs. Skriv bords analys kan nu hjälpa dig att identifiera dessa skydd i förväg, så att du kan åtgärda till gången innan du distribuerar uppdateringen. Mer information finns i [kompatibilitetskontroll-skydd](compat-assessment.md#safeguards).

## <a name="january-2020"></a>Januari 2020

### <a name="additional-app-usage-detail"></a>Ytterligare information om användning av appar

<!-- 5533890 -->

När du väljer en app för att se mer information innehåller informations fönstret nu ytterligare information om användning. Du kan använda dessa data för att hjälpa till att förstå installations området för en app, samt enheter där användarna regelbundet använder appen. Mer information finns i [om till gångar – användning av appar](about-assets.md#usage).

### <a name="provide-feedback-on-desktop-analytics"></a>Ge feedback om Desktop Analytics

<!-- 5451636 -->

Om du vill dela din feedback om Desktop Analytics väljer du ikonen **Skicka ett leende** överst i portalen på höger sida. Mer information finns i [dela produkt](get-support.md#bkmk_feedback)information.

## <a name="october-2019"></a>Oktober 2019

### <a name="improvements-to-compatibility-recommendations"></a>Förbättringar av kompatibilitets rekommendationer

<!-- 3594545 -->

Skriv bords analys innehåller nu ytterligare information när den upptäcker att Windows-uppgraderingen kommer att helt eller delvis ta bort ett program eller en driv rutin. Mer information finns i [kompatibilitetskontroll](compat-assessment.md#asset-is-removed-during-upgrade).

### <a name="migrate-from-windows-analytics-to-existing-tenant"></a>Migrera från Windows Analytics till befintlig klient

<!-- 5202803 -->

Du kan nu migrera indata från en befintlig Windows Analytics-arbetsyta efter registreringen till Desktop Analytics.

## <a name="september-2019"></a>September 2019

### <a name="migrate-inputs-from-windows-analytics"></a>Migrera indata från Windows Analytics

<!-- 4252663 -->

Under onboarding kan du nu migrera indata från en befintlig Windows Analytics-arbetsyta.

### <a name="offboard-from-desktop-analytics"></a>Avpublicera från Skriv bords analys

<!-- 4972396 -->

Om du konfigurerar Desktop Analytics i din miljö, men vill sluta använda tjänsten, kan du nu stänga ditt konto. Om du ändrar dig i 90 dagar kan du återaktivera kontot. Mer information finns i [så här stänger du ditt konto](account-close.md).

## <a name="august-2019"></a>Augusti 2019

### <a name="reset-your-account"></a>Återställa konto

<!-- 3733897 -->

Om du konfigurerar Desktop Analytics i din miljö, men vill börja om med onboarding och registrering, kan du nu återställa det. Mer information om processen finns i [återställa ditt konto](account-reset.md).

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a>Automatiskt uppgraderings beslut av system-och Store-appar

<!-- 3587232 -->

För att minska dina insatser i att kommentera viktiga appar, markeras vissa typer av appar automatiskt som *inte viktiga*. Distributions planens uppgraderings beslut för de här apparna är också markerat som *klart*. Följande appar är kompatibla och bör fortsätta att fungera när du har uppgraderat Windows:

- Systemappar och komponenter som publicerats av Microsoft

- Appar som hanteras och uppdateras från Microsoft Store

Mer information finns i [beslut om automatisk uppgradering av system-och Store-appar](about-assets.md#bkmk_plan-autoapp).

## <a name="whats-new-in-configuration-manager"></a>Vad är nytt i Configuration Manager

Skriv bords analys dokumenten avser alltid funktioner i den senaste versionen av Configuration Manager aktuella grenen. Mer information om de senaste ändringarna i Configuration Manager finns i följande artiklar:

<!-- - [What's new in version 1910](../core/plan-design/changes/whats-new-in-version-1910.md#bkmk_da) -->

- [Nyheter i version 1906](../core/plan-design/changes/whats-new-in-version-1906.md#bkmk_da)

## <a name="deprecated-features"></a>Föråldrade funktioner

När Microsoft planerar att ta bort en viktig funktion i Skriv bords analys tjänsten, meddelas ändringen i förväg som en Configuration Manager föråldrad funktion. Mer information finns i [föråldrade funktioner](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).
