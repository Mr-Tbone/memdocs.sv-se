---
title: Skapa iOS/iPadOS- eller macOS-enhetsprofiler i Microsoft Intune – Azure | Microsoft Docs
description: Lägg till eller skapa en iOS-, iPadOS- eller macOS-enhetsprofil och konfigurera sedan inställningar för AirPrint, layout för startsidan, appmeddelanden, delad enhet, enkel inloggning och webbinnehållsfilter i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cb8d5b53e136ea22d1edbad7755e198fd4155285
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551394"
---
# <a name="add-ios-ipados-or-macos-device-feature-settings-in-intune"></a>Lägga till funktionsinställningar för iOS-, iPadOS- eller macOS-enheter i Intune

Intune innehåller många funktioner och inställningar som hjälper administratörer att styra iOS-, iPadOS- och macOS-enheter. Administratörerna kan exempelvis:

- Ge användarna åtkomst till AirPrint-skrivare i nätverket
- Lägga till appar och mappar på startsidan, inklusive att lägga till nya sidor
- Välja om och hur appmeddelanden ska visas
- Konfigurera att låsskärmen visar ett meddelande eller en resurstagg, vilket är särskilt användbart för delade enheter
- Ge användarna en säker enkel inloggning för att kunna dela autentiseringsuppgifter mellan appar
- Filtrera webbplatser som innehåller språk som är olämpligt för barn, samt tillåta eller blockera vissa webbplatser

Intune använder ”konfigurationsprofiler” till att skapa och anpassa inställningarna efter din organisations behov. När du har lagt till dessa funktioner i en profil, kan du skicka eller distribuera profilen till iOS/iPadOS- och macOS-enheter i din organisation.

Den här artikeln beskriver de olika funktioner som du kan konfigurera och visar hur du skapar en profil för enhetskonfigurationen. Artikeln innehåller även alla tillgängliga inställningar för [iOS/iPadOS](ios-device-features-settings.md)- och [macOS](macos-device-features-settings.md)-enheter.

> [!NOTE]
> Användargränssnittet i Intune uppdateras till en helskärmsupplevelse och kan ta flera veckor. Innan klienten får den här uppdateringen får du ett något annorlunda arbetsflöde när du skapar eller redigerar de inställningar som beskrivs i den här artikeln.

## <a name="airprint"></a>AirPrint

Airprint är en Apple-funktion som gör det möjligt för enheter att skriva ut till filer över ett trådlöst nätverk. I Intune kan du lägga till information om AirPrint till enheter.

En lista över de inställningar som du kan konfigurera i Intune finns i [AirPrint på iOS/iPadOS](ios-device-features-settings.md#airprint) och [AirPrint på macOS](macos-device-features-settings.md#airprint).

Mer information om AirPrint finns i [Om AirPrint](https://support.apple.com/HT201311) på Apples webbplats.

Gäller för:

- iOS 7.0 och senare
- iPadOS 13.0 och senare
- macOS 10.10 och senare

## <a name="app-notifications"></a>Appmeddelanden

Välj hur appar på iOS- och iPadOS-enheter får aviseringar. Till exempel, skicka aviseringar från Intune så att de visas i meddelandecentret, visas på låsskärmen eller spelar upp ett ljud.

En lista över de inställningar som du kan konfigurera i Intune finns i [Appaviseringar i iOS/iPadOS](ios-device-features-settings.md#app-notifications).

Mer information om den här funktionen finns i [Aviseringar](https://developer.apple.com/notifications/) på Apples webbplats.

Gäller för:

- iOS 9.3 och senare
- iPadOS 13.0 och senare

## <a name="associated-domains"></a>Tillhörande domäner

Med tillhörande domäner kan du skapa en relation mellan dina domäner, till exempel `contoso.com` och dina appar. Med den här funktionen kan du:

- Dela data och autentiseringsuppgifter mellan appar och webbplatser i din organisation.
- Använda appinställningar som baseras på din webbplats, till exempel tillägg för enkel inloggning, universella länkar och lösenord.

  Du kan till exempel skapa en associerad domän för att tillåta automatisk inloggningsinformation, till exempel ett lösenord, för webbplatser som associeras med din app.

En lista över de inställningar som du kan konfigurera i Intune finns i [Tillhörande domäner på macOS](macos-device-features-settings.md#associated-domains).

Mer information om den här funktionen finns i [Konfigurera en apps tillhörande domäner](https://developer.apple.com/documentation/security/password_autofill/setting_up_an_app_s_associated_domains) på Apples webbplats.

Gäller för:

- macOS 10.15 och senare

## <a name="home-screen-layout"></a>Startsideslayout

Dessa inställningar konfigurerar applayouten och mappar på dockan och startskärmen på iOS- och iPadOS-enheter. Du kan:

- Använd inställningarna för **Dockning** för att lägga till appar eller mappar på skärmen. Du kan till exempel visa Safari och e-postappen på enhetens docka.
- Lägg till de **sidor** som du vill ska visas på startskärmen, samt de appar som du vill ska visas på varje sida. Lägg till exempel till en **Contoso**-sida och lägga till inställningsappen på den här sidan.

En lista över de inställningar som du kan konfigurera i Intune finns i [Layout för startskärmen på macOS/iPadOS](ios-device-features-settings.md#home-screen-layout).

Gäller för:

- iOS 9.3 och senare
- iPadOS 13.0 och senare

## <a name="lock-screen-message"></a>Meddelande på låsskärm

Använd de här inställningarna för att visa ett anpassat meddelande eller text i inloggningsfönstret och på låsskärmen. Du kan till exempel skriva ett meddelande av typen ”Upphittad enhet återlämnas till...” och visa resurstagginformation.

En lista över de inställningar som du kan konfigurera i Intune finns i [Aviseringsinställningar för låsskärmen i iOS/iPadOS](ios-device-features-settings.md#lock-screen-message).

Mer information om aviseringar på låsskärmen finns i [Aviseringar på låsskärmen](https://developer.apple.com/documentation/devicemanagement/lockscreenmessage) på Apples webbplats.

Gäller för:

- iOS 9.3 och senare
- iPadOS 13.0 och senare

## <a name="login-items"></a>Inloggningsobjekt

Använd den här funktionen för att välja appar, anpassade appar, filer och mappar som öppnas när användare loggar in på enheterna.

En lista över de inställningar som du kan konfigurera i Intune finns i [Inloggningsobjekt på macOS](macos-device-features-settings.md#login-items).

Gäller för:

- macOS 10.13 och senare

## <a name="login-window"></a>Inloggningsfönstret

Styr utseendet på inloggningsskärmen och funktioner som är tillgängliga för användarna innan de loggar in. Du kan till exempel lägga till en banderoll med ett anpassat meddelande, välja om vila-knappen visas med mera.

En lista över de inställningar som du kan konfigurera i Intune finns i [Inloggningsfönster i macOS](macos-device-features-settings.md#login-window).

Gäller för:

- macOS 10.7 och senare

## <a name="single-sign-on"></a>Enkel inloggning

De flesta verksamhetsspecifika appar kräver av säkerhetsskäl någon nivå av användarautentisering. I många fall kräver den här autentiseringen att användaren anger samma autentiseringsuppgifter upprepade gånger. För att förbättra användarupplevelsen kan utvecklare skapa appar som använder enkel inloggning (SSO). Med enkel inloggning minskar antalet gånger som en användare måste ange autentiseringsuppgifter.

Om du vill använda enkel inloggning, måste du ha:

- En app som är kodad för att leta efter användarens autentiseringsuppgifter lagrade i enkel inloggning på enheten.
- Intune måste ha konfigurerats för enkel inloggning för iOS/iPadOS-enheter.

![Fönstret Enkel inloggning](./media/device-features-configure/sso-blade.png)

En lista över de inställningar som du kan konfigurera i Intune finns i [Enkel inloggning i iOS/iPadOS](ios-device-features-settings.md#single-sign-on).

Gäller för:

- iOS 7.0 och senare
- iPadOS 13.0 och senare

## <a name="single-sign-on-app-extension"></a>Tillägg för enkel inloggning

De här inställningarna konfigurerar ett apptillägg som möjliggör enkel inloggning (SSO) för iOS-, iPadOS-och macOS-enheter. De flesta verksamhetsspecifika appar och företagswebbplatser kräver någon nivå av säker användarautentisering. I många fall kräver den här autentiseringen att användaren anger samma autentiseringsuppgifter upprepade gånger. SSO ger användare åtkomst till appar och webbplatser när de har angett sina autentiseringsuppgifter en gång. SSO ger också bättre autentisering för användarna och minskar antalet upprepade förfrågningar om autentiseringsuppgifter.

Använd de här inställningarna i Intune för att konfigurera ett apptillägg för enkel inloggning som har skapats av din organisation, identitetsprovider, Microsoft eller Apple. Tillägget för SSO-appen hanterar autentisering för dina användare. De här inställningarna konfigurerar apptillägg för enkel inloggning av omdirigerings- och inloggningsinformationstyp.

- Omdirigeringstypen är utformad för moderna autentiseringsprotokoll som OAuth och SAML2. Microsoft har ett apptillägg för enkel inloggning av Azure AD-omdirigeringstyp för iOS/iPad som kan aktiv ras med inställningarna för apptillägget för enkel inloggning.
- Inloggningsinformationstypen är utformad för autentiseringsflöden med anrop och svar. Du kan välja mellan ett Kerberos-specifikt tillägg för autentiseringsuppgifter från Apple och ett generiskt för autentiseringsuppgifter.

En lista över de inställningar som du kan konfigurera i Intune finns i [iOS/iPadOS SSO-apptillägg](ios-device-features-settings.md#single-sign-on-app-extension) och [macOS SSO-apptillägg](macos-device-features-settings.md#single-sign-on-app-extension).

Mer information om hur du utvecklar ett SSO-apptillägg finns i [Utökningsbar företags-SSO](https://developer.apple.com/videos/play/tech-talks/301) på Apples webbplats. Om du vill läsa Apples beskrivning av funktionen går du till [Nyttolastinställningar av tillägg för enkel inloggning](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web). 

> [!NOTE]
> Funktionen **Apptillägget enkel inloggning** skiljer sig från funktionen **Enkel inloggning**:
>
> - Inställningarna i **Apptillägg för enkel inloggning** gäller för iPadOS 13.0 (och senare), iOS 13.0 (och senare), samt macOS 10.15 (och senare). Inställningarna för **Enkel inloggning** gäller för iPadOS 13.0 (och senare) och iOS 7.0 (och senare).
>
> - Inställningarna i **Apptillägg för enkel inloggning** definierar tillägg som används av identitetsproviders eller organisationer som vill tillhandahålla en sömlös företagsinloggning. Inställningarna i **Enkel inloggning** definierar Kerberos-kontoinformationen för när användare får åtkomst till servrar eller appar.
>
> - **Apptillägget enkel inloggning** använder Apples operativsystem för att autentisera. Det kan därför ge en slutanvändaren en upplevelse som är bättre än **enkel inloggning**.
>
> - Ur ett utvecklingsperspektiv kan du med **apptillägget för enkel inloggning** använda vilken typ av omdirigerings-SSO eller SSO-autentisering som helst. Med **enkel inloggning** kan du endast använda Kerberos SSO-autentisering.
>
> - **Apptillägget för enkel inloggning** i Kerberos har utvecklats av Apple och är inbyggt i plattformarna iOS/iPadOS 13.0+ och macOS 10.15+. Det inbyggda Kerberos-tillägget kan användas för att logga in användare i interna appar och webbplatser som stöder Kerberos-autentisering. **Enkel inloggning** är inte en Apple-implementering av Kerberos.
>
> - Det inbyggda **apptillägget för enkel inloggning** i Kerberos hanterar Kerberos-anrop för webbsidor och appar på samma sätt som i **Enkel inloggning**. Det inbyggda Kerberos-tillägget stöder dock lösenordsändringar och fungerar bättre i företagsnätverk. När du väljer mellan Kerberos **apptillägg för enkel inloggning** och **enkel inloggning**, rekommenderar vi att du använder tillägget tack vare dess förbättrade prestanda och funktioner.

Gäller för:

- iOS 13.0 och senare
- iPadOS 13.0 och senare
- macOS 10.15 och senare

## <a name="wallpaper"></a>Skrivbordsunderlägg

Lägg till en anpassad PNG-, JPG- eller JPEG-bild till övervakade iOS/iPadOS-enheter. Använd exempelvis Intune för att lägga till en företagslogotyp på låsskärmen på dina enheter.

En lista över de inställningar som du kan konfigurera i Intune finns i [Bakgrundsbild i iOS/iPadOS](ios-device-features-settings.md#wallpaper).

Gäller för:

- iOS
- iPadOS 13.0 och senare

## <a name="web-content-filter"></a>Webbinnehållsfilter

De här inställningarna använder Apples inbyggda autofilteralgoritm för att utvärdera webbsidor och blockera vuxeninnehåll och vuxenspråk. Du kan också skapa en lista över tillåtna webblänkar och begränsade webblänkar. Du kan till exempel endast tillåta att `contoso`-webbplatser öppnas.

En lista över de inställningar som du kan konfigurera i Intune finns i [Webbinnehållsfilter i iOS/iPadOS](ios-device-features-settings.md#web-content-filter).

Gäller för:

- iOS 7.0 och senare
- iPadOS 13.0 och senare

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

    - **Plattform**: Välj plattform för dina enheter. Alternativen är:  

        - **iOS/iPadOS**
        - **macOS**

    - **Profil**: Välj **Enhetsfunktioner**.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Till exempel är ett användbart principnamn **macOS: Konfigurerar inloggningsskärmen**.
    - **Beskrivning**: Ange en beskrivning av principen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.

7. Under **Konfigurationsinställningar**  visas olika inställningar som du kan konfigurera beroende på vilken plattform du väljer. Välj din plattform för detaljerade inställningar:

    - [iOS/iPadOS](ios-device-features-settings.md)
    - [macOS](macos-device-features-settings.md)

8. Välj **Nästa**.
9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar**väljer du de användare eller grupper som ska ta emot din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

## <a name="next-steps"></a>Nästa steg

Profilen skapas, men den kanske inte gör något än. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Visa alla enhetsfunktionsinställningar för [iOS/iPadOS](ios-device-features-settings.md)- och [macOS](macos-device-features-settings.md)-enheter.
