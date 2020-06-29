---
title: Hantera Outlook för iOS och Android med Intune
description: Använd Intunes policyer för appsäkerhet och konfigurering med Outlook för iOS och Android för att skydda åtkomsten till teamens samarbetsmiljöer.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3db207e4c1c75706c1f54762bf74c1757d342ac1
ms.sourcegitcommit: c7afcc3a2232573091c8f36d295a803595708b6c
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/17/2020
ms.locfileid: "84973051"
---
# <a name="manage-messaging-collaboration-access-by-using-outlook-for-ios-and-android-with-microsoft-intune"></a>Hantera åtkomst till meddelandefunktioner med Outlook för iOS och Android i Microsoft Intune

Appen Outlook för iOS och Android är utformad för att användare i organisationen ska kunna att göra mer från sina mobila enheter, genom att sammanföra e-post, kalender, kontakter och andra filer.

De mest avancerade och bredaste skyddsfunktionerna för Office 365-data är tillgängliga när du prenumererar på sviten Enterprise Mobility + Security, som innehåller Microsoft Intune och Azure Active Directory Premium-funktioner, till exempel villkorsstyrd åtkomst. Du bör minst distribuera en princip för villkorsstyrd åtkomst som tillåter anslutning till Outlook för iOS och Android från mobila enheter och en säkerhetspolicy i Intune-appen som skyddar samarbetsmiljön.

## <a name="apply-conditional-access"></a>Tillämpa villkorsstyrd åtkomst
Organisationer kan använda principer för villkorsstyrd åtkomst i Azure AD till att säkerställa att användarna endast kan komma åt arbets- eller skolinnehåll med hjälp av Outlook för iOS och Android. För att göra detta behöver du en princip för villkorsstyrd åtkomst som är riktad mot alla potentiella användare. Information om hur du skapar den här principen finns i [Kräva appskyddsprincip för åtkomst till molnapp med villkorsstyrd åtkomst](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Följ ”Steg 1: Konfigurera en Azure AD-princip för villkorsstyrd åtkomst för Office 365” i [Scenario 1: Office 365-appar kräver godkända appar med policyer för appskydd](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), som tillåter Outlook för iOS och Android men blockerar OAuth-kompatibla Exchange ActiveSync-klienter från att ansluta till Exchange Online.

   > [!NOTE]
   > Den här policyn gör att mobila användare kan komma åt alla Office-slutpunkter via lämpliga appar.

2. Följ ”Steg 2: Konfigurera en Azure AD-princip för villkorsstyrd åtkomst för Exchange Online med ActiveSync (EAS)” i [Scenario 1: Office 365-appar kräver godkända appar med policyer för appskydd](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies), som förhindrar att Exchange ActiveSync-klienter med grundläggande autentisering ansluter till Exchange Online.

   Policyerna ovan använder sig av beviljandekontrollen [Kräv appskyddsprincip](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-technical-reference), som gör att en policy för appskydd i Intune tillämpas på det associerade kontot i Outlook för iOS och Android innan åtkomst beviljas. Om användaren inte har tilldelats någon policy för appskydd i Intune, inte har någon Intune-licens eller om appen inte ingår i policyn för appskydd i Intune förhindrar policyn att användaren får en åtkomsttoken och åtkomst till meddelandedata.

3. Följ slutligen [Gör så här: Blockera äldre autentisering till Azure AD med villkorsstyrd åtkomst](https://docs.microsoft.com/azure/active-directory/conditional-access/block-legacy-authentication) för att blockera äldre autentisering för andra Exchange-protokoll på iOS- och Android-enheter. Den här policyn ska bara riktas mot Office 365 Exchange Online-molnappar samt enhetsplattformarna iOS och Android. Det här gör att mobila appar som använder Exchange Web Services, IMAP4- eller POP3-protokoll med grundläggande autentisering inte kan ansluta till Exchange Online.

## <a name="create-intune-app-protection-policies"></a>Skapa appskyddsprinciper i Intune

Appskyddsprinciper (APP) definierar vilka appar som tillåts och vilka åtgärder de kan utföra med din organisations data. De alternativ som är tillgängliga i appskyddsprincipen gör det möjligt för organisationer att skräddarsy skyddet för deras specifika behov. För vissa är det inte alltid uppenbart vilka principinställningar som krävs för att implementera ett fullständigt scenario. För att hjälpa organisationer att prioritera härdning av mobilklientslutpunkter har Microsoft infört taxonomi för dataskyddsramverket med APP:er för mobilappshantering för iOS och Android.

Dataskyddsramverket för APP:er är indelat i tre olika konfigurationsnivåer där varje nivå bygger på den föregående nivån:

- **Grundläggande dataskydd för företag** (nivå 1) säkerställer att apparna skyddas med en PIN-kod, krypteras och utför åtgärder för selektiv rensning. För Android-enheter verifierar den här nivån Android-enhetsattestering. Det här är en konfiguration på ingångsnivå som ger liknande dataskyddskontroll som policyer för Exchange Online-postlådor och introducerar IT-avdelningen och användarna för APP.
- **Förbättrat dataskydd för företag** (nivå 2) introducerar APP-mekanismer för att förhindra dataläckage och minimikrav för operativsystem. Den här konfigurationen gäller för de flesta mobila användare som har åtkomst till arbets- eller skoldata.
- **Starkt dataskydd för företag** (nivå 3) introducerar avancerade mekanismer för dataskydd, förbättrad PIN-konfiguration och skydd mot mobila hot i appar. Den här konfigurationen passar för användare som hanterar skyddsvärda data.

Om du vill se specifika rekommendationer för varje konfigurationsnivå och minsta antal appar som måste skyddas går du till [Dataskyddsramverk med hjälp av appskyddsprinciper](app-protection-framework.md).

Oavsett om enheten har registrerats i en UEM-lösning (Unified Endpoint Management) måste en Intune-appskyddsprincip skapas för både iOS- och Android-appar med hjälp av stegen i [Hur du skapar och tilldelar skyddsprinciper för appar](app-protection-policies.md). Dessa principer måste minst uppfylla följande villkor:

1. De omfattar alla Microsoft 365-mobilappar som Edge, Outlook, OneDrive, Office eller Teams, eftersom det säkerställer att användare kan komma åt och ändra arbets- eller skoldata inom alla Microsoft-appar på ett säkert sätt.

2. De tilldelas alla användare. Det här gör att alla användare skyddas, oavsett om de använder Outlook för iOS eller Android.

3. Fastställ vilken ramverksnivå som uppfyller dina krav. De flesta organisationer bör implementera inställningarna som definierats i **Förbättrat dataskydd för företag** (nivå 2) som aktiverar dataskydds- och åtkomstkravskontroller.

Mer information om de tillgängliga inställningarna finns i [Inställningar för Android-appskyddsprinciper](app-protection-policy-settings-android.md) och [Inställningar för iOS-appskyddsprinciper](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> För att kunna tillämpa Intunes appskyddsprinciper mot appar på Android-enheter som inte är registrerade i Intune måste användaren också installera Intune-företagsportalen. Mer information finns i [Vad som händer när din Android-app hanteras av appskyddsprinciper](../fundamentals/end-user-mam-apps-android.md).

## <a name="utilize-app-configuration"></a>Använda appkonfigurering

Outlook för iOS och Android har stöd för appinställningar som tillåter administratörer för enhetlig slutpunktshantering som Microsoft Endpoint Manager att anpassa appens beteende.

Appkonfigurationen kan antingen levereras via OS-kanalen för mobilenhetshantering (MDM) på registrerade enheter (kanalen [Hanterad appkonfiguration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) för iOS eller kanalen [Android i Enterprise](https://developer.android.com/work/managed-configurations) för Android) eller via Intune-kanalen för appskyddsprincip (APP). Outlook för iOS och Android har stöd för följande konfigurationsscenarier:

- Tillåt endast arbets- eller skolkonton
- Allmänna appkonfigurationsinställningar
- S/MIME-inställningar
- Inställningar för dataskydd

Detaljerade anvisningar och detaljerad dokumentation om de appkonfigurationsinställningar som Outlook för iOS och Android stöder finns i [Distribuera appkonfigurationsinställningar för Outlook för iOS och Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

## <a name="next-steps"></a>Nästa steg

- [Vad är appskyddsprinciper?](app-protection-policy.md) 
- [Appkonfigurationsprinciper för Microsoft Intune](app-configuration-policies-overview.md)