---
title: Dataskyddsramverk med appskyddsprinciper
titleSuffix: Microsoft Intune
description: Lär dig hur appskyddsprinciper (APP, App Protection Policies) säkerställer att organisationens data förblir säkra eller förvaras i en hanterad app, oavsett om enheten är registrerad.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0803563dc525b0835602d54d4bde3de1345aeb33
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913383"
---
# <a name="data-protection-framework-using-app-protection-policies"></a>Dataskyddsramverk med appskyddsprinciper 

I takt med att fler organisationer implementerar strategier med mobila enheter för åtkomst till arbets- eller skoldata blir det ytterst viktigt att skydda mot dataläckage. Intune-lösningen för hantering av mobilprogram som skyddar mot dataläckage är appskyddsprinciper (APP). APP är regler som säkerställer att organisationens data förblir säkra eller förvaras i en hanterad app. Mer information finns i [översikten av Appskyddsprinciper](app-protection-policy.md).

När du konfigurerar appskyddsprinciper gör de olika inställningarna och alternativen att organisationer kan skräddarsy skyddet för efter sina särskilda behov. På grund av den här flexibiliteten är det inte alltid uppenbart vilken permutation av principinställningar som krävs för att implementera ett fullständigt scenario. I syfte att hjälpa organisationer att prioritera arbete med förstärkning av klientslutpunkter har Microsoft infört en ny taxonomi för [säkerhetskonfigurationer i Windows 10](https://aka.ms/secconframework), och Intune använder en liknande taxonomi för sitt APP-dataskyddsramverk för hantering av mobilappar.  

Ramverket för APP-dataskyddskonfiguration är indelat i tre olika konfigurationsscenarier:

- Nivå 1: Grundläggande dataskydd för företag – Microsoft rekommenderar den här konfigurationen som lägsta dataskyddskonfiguration för företagsenheter.

- Nivå 2: Förbättrat dataskydd för företag – Microsoft rekommenderar den här konfigurationen för enheter vars användare får åtkomst till känslig eller konfidentiell information. Den här konfigurationen gäller för de flesta mobila användare som har åtkomst till arbets- eller skoldata. Vissa av kontrollerna kan påverka användarupplevelsen.

- Nivå 3: Starkt dataskydd för företag – Microsoft rekommenderar den här konfigurationen för enheter som körs av organisationer med ett större eller mer avancerat säkerhetsteam, eller för specifika användare eller grupper som utsätts för ovanligt hög risk (användare som hanterar mycket känsliga data, där otillåtet yppande skulle orsaka omfattande materiella förluster för organisationen). Organisationer som kan antas vara föremål för välfinansierade och avancerade angrepp bör eftersträva den här konfigurationen.

## <a name="app-data-protection-framework-deployment-methodology"></a>Distributionsmetod för ramverket för APP-dataskydd

Som med alla distributioner av ny programvara, funktioner eller inställningar överlag rekommenderar Microsoft att du investerar i en ringmetod för att testa validering innan du distribuerar ramverket för APP-dataskydd. Att definiera distributionsringar är vanligtvis en engångshändelse (eller åtminstone något som sker sällan), men IT-avdelningen bör kontrollera dessa grupper för att se till att sekvensen fortfarande är korrekt.

Microsoft rekommenderar följande distributionsringsmetod för ramverket för APP-dataskydd:

| Distributionsring  | Klient  | Utvärderingsverktyg  | Utdata  | Tidslinje  |
|--------------------|------------------------|-------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------|
| Kvalitetskontroll  | Klientorganisation före produktion  | Mobilkapacitetsägare, säkerhet, riskbedömning, sekretess, UX  | Validering av funktionellt scenario, utkastdokumentation  | 0–30 dagar  |
| Förhandsgranskning  | Klientorganisation för produktion  | Mobilkapacitetsägare, UX  | Validering av slutanvändarscenario, användarriktad dokumentation  | 7–14 dagar, efter kvalitetskontroll  |
| Produktion  | Klientorganisation för produktion  | Mobilkapacitetsägare, IT-support  | E.t.  | 7 dagar till flera veckor, efter förhandsgranskning  |

Som anges i tabellen ovan bör alla ändringar av appskyddsprinciper först utföras i en förproduktionsmiljö så att man förstår effekterna av principändringar. När testningen är klar kan ändringarna flyttas till produktion och tillämpas på en delmängd av produktionsanvändarna, vanligtvis IT-avdelningen och andra tillämpliga grupper. Slutligen kan distributionen slutföras till övriga mobilanvändare. Det kan ta längre tid att distribuera till produktion, beroende på hur stor påverkan ändringen medför. Om det inte finns någon användarpåverkan bör ändringen ske snabbt, men om ändringen resulterar i användarpåverkan kan distributionen behöva gå långsammare eftersom användarna behöver meddelas om ändringar.

När du testar ändringar i en APP bör du vara medveten om [leveranstiming](app-protection-policy-delivery.md). Statusen för APP-leverans för en viss användare kan övervakas. Mer information finns i [Så här övervakar du appskyddsprinciper](app-protection-policies-monitor.md).

Enskilda APP-inställningar för varje app kan valideras på enheter med hjälp av Edge och URL:en *about:Intunehelp*. Mer information finns i [Granska säkerhetsloggar för klientappar](app-protection-policy-settings-log.md) och [Använda Microsoft Edge för iOS och Android för att komma åt loggar för hanterade appar](manage-microsoft-edge.md#use-edge-for-ios-and-android-to-access-managed-app-logs).

## <a name="app-data-protection-framework-settings"></a>Inställningar för ramverket för APP-dataskydd

Följande inställningar för appskyddsprincip bör aktiveras för tillämpliga appar och tilldelas till alla mobilanvändare. Mer information om varje principinställning finns i [Inställningar för iOS-appskyddsprinciper](app-protection-policy-settings-ios.md) och [Inställningar för Android-appskyddsprinciper](app-protection-policy-settings-android.md).

Microsoft rekommenderar att du granskar och kategoriserar användningsscenarier och sedan konfigurerar användare med hjälp av de normativa riktlinjerna för den nivån. Precis som med alla ramverk kan inställningar inom en motsvarande nivå behöva justeras baserat på organisationens behov, eftersom dataskydd måste utvärdera hotmiljön, riskbenägenheten och påverkan på användbarheten.  

### <a name="conditional-access-policies"></a>Villkorliga åtkomstprinciper
För att säkerställa att endast appar som har stöd för appskyddsprinciper får åtkomst till arbets- eller skolkontodata, krävs principer för villkorsstyrd åtkomst för Azure Active Directory. Se **Scenario 1: Office 365-appar kräver godkända appar med appskyddsprinciper** i [Kräva appskyddsprincip för molnappsåtkomst med villkorsstyrd åtkomst](/azure/active-directory/conditional-access/app-protection-based-conditional-access) för stegen för att implementera de specifika principerna.

### <a name="apps-to-include-in-the-app-protection-policies"></a>Appar som ska ingå i appskyddsprinciperna  

För varje appskyddsprincip bör följande centrala Microsoft-appar inkluderas:

- Edge
- Excel
- Kontor
- OneDrive
- OneNote
- Outlook
- PowerPoint
- Microsoft Teams
- Microsoft To-Do
- Word
- Microsoft SharePoint

Principerna bör inkludera andra Microsoft-appar baserat på affärsbehov, ytterligare offentliga appar från tredje part som har integrerat den Intune SDK som används i organisationen samt verksamhetsspecifika appar som har integrerat [Intune SDK](../developer/app-sdk.md) (eller som har omslutits).

### <a name="level-1-enterprise-basic-data-protection"></a>Nivå 1: Grundläggande dataskydd för företag

Nivå 1 är den lägsta dataskyddskonfigurationen för en mobil företagsenhet. Den här konfigurationen ersätter behovet av grundläggande Exchange Online-principer för enhetsåtkomst genom att kräva en PIN-kod för åtkomst till arbets- eller skoldata, kryptera data i arbets- eller skolkonton samt ge möjligheten att selektivt rensa skol- eller arbetsdata. Till skillnad från Exchange Online-principer för enhetsåtkomst gäller dock nedanstående inställningar för appskyddsprincip för alla appar som väljs i principen. Det säkerställer att dataåtkomst skyddas även utanför scenarier för mobila meddelanden.

Principerna på nivå 1 tillämpar en rimlig dataåtkomstnivå och minimerar samtidigt påverkan på användare. De speglar även de standardmässiga inställningarna för dataskydd och åtkomstkrav vid skapande av en appskyddsprincip i Microsoft Endpoint Manager.  

#### <a name="data-protection"></a>Dataskydd

| Inställningen | Beskrivning av inställning |             Värde  |             Plattform        |
|-----------------|--------------------------------------------------------|-----------------------|----------------------------------------|
| Dataöverföring |             Säkerhetskopiera organisationsdata till …  |             Tillåt  |             iOS/iPadOS, Android        |
| Dataöverföring |       Skicka organisationsdata till andra appar  |             Alla appar  |             iOS/iPadOS, Android        |
| Dataöverföring |       Ta emot data från andra appar  |             Alla appar  |             iOS/iPadOS, Android        |
| Dataöverföring |       Begränsa klipp ut, kopiera och klistra in mellan  appar  |             Alla appar  |             iOS/iPadOS, Android        |
| Dataöverföring |       Tangentbord från tredje part  |             Tillåt  |             iOS/iPadOS        |
| Dataöverföring |       Godkända tangentbord  |             Krävs inte  |             Android        |
| Dataöverföring |       Skärmdump och Google Assistant  |             Tillåt  |             Android        |
| Kryptering |             Kryptera organisationsdata  |             Kräver  |             iOS/iPadOS, Android        |
| Kryptering |       Kryptera organisationsdata på registrerade enheter  |             Kräver  |             Android        |
| Funktioner  |             Synkronisera app med inbyggd kontaktapp  |             Tillåt  |             iOS/iPadOS, Android        |
| Funktioner  |       Utskrift av organisationsdata  |             Tillåt  |             iOS/iPadOS, Android        |
| Funktioner  |       Begränsa överföring av webbinnehåll till andra appar  |             Alla appar  |             iOS/iPadOS, Android        |
| Funktioner  |       Meddelanden om organisationsdata  |             Tillåt  |             iOS/iPadOS, Android        |

#### <a name="access-requirements"></a>Åtkomstkrav 

| Inställningen  | Värde  | Plattform  | Obs!  |
|----------------------------------------------------------------|---------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PIN-kod för åtkomst  | Kräver  | iOS/iPadOS, Android  |   |
| Typ av PIN-kod  | Numeriskt  | iOS/iPadOS, Android  |   |
| Enkel PIN-kod  | Tillåt  | iOS/iPadOS, Android  |   |
| Välja minimilängd för PIN-kod  | 4  | iOS/iPadOS, Android  |   |
| Biometrik i stället för PIN-kod för åtkomst  | Tillåt  | iOS/iPadOS, Android  |   |
| Åsidosätt biometrik i stället för PIN-kod för åtkomst  | Kräver  | iOS/iPadOS, Android  |   |
| Tidsgräns (minuters aktivitet)  | 720  | iOS/iPadOS, Android  |   |
| Face ID i stället för PIN-kod för åtkomst  | Tillåt  | iOS/iPadOS  |   |
| Återställ PIN-kod efter antal dagar  | Nej  | iOS/iPadOS, Android  |   |
| PIN-appkod när enhetens PIN-kod har ställts in  | Kräver  | iOS/iPadOS, Android  | Om enheten registreras i Intune kan administratörer överväga att ange detta till "Inte obligatoriskt" om de tillämpar en stark PIN-kod för enheten via en efterlevnadsprincip för enheter.  |
| Arbets- eller skolkontoautentiseringsuppgifter för åtkomst  | Krävs inte  | iOS/iPadOS, Android  |   |
| Kontrollera åtkomstbehörigheterna på nytt efter (minuters inaktivitet)  | 30  | iOS/iPadOS, Android  |   |

#### <a name="conditional-launch"></a>Villkorlig start 

| Inställningen | Beskrivning av inställning |          Värde/åtgärd  |          Plattform        | Obs! |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Appvillkor |       Högsta antal PIN-försök  |          5/Återställ PIN-kod  |          iOS/iPadOS, Android  |                  |
| Appvillkor |       Offline-respitperiod  |          720/Blockera åtkomst (minuter)  |          iOS/iPadOS, Android  |                  |
| Appvillkor |       Offline-respitperiod  |          90/Rensa data (dagar)  |          iOS/iPadOS, Android  |                  |
| Enhetsvillkor  |       Jailbrokade/rotade enheter  |        Ej tillämpligt/Blockera åtkomst  |          iOS/iPadOS, Android  |                  |
| Enhetsvillkor  |       SafetyNet-enhetsattestering  |          Grundläggande integritet och certifierade enheter/Blockera åtkomst  |          Android  |          <p>Den här inställningen konfigurerar Googles SafetyNet-attestering på slutanvändarenheter. Grundläggande integritet kontrollerar enhetens integritet. Rotade enheter, emulatorer, virtuella enheter och enheter med tecken på manipulation misslyckas med grundläggande integritet. </p><p> Grundläggande integritet och certifierade kontrollerar enhetens kompatibilitet med Google-tjänster. Endast oförändrade enheter som har certifierats av Google kan godkännas av den här kontrollen.</p>  |
| Enhetsvillkor  |       Kräv hotgenomsökning för appar  |        Ej tillämpligt/Blockera åtkomst  |          Android  |          Den här inställningen säkerställer att Googles Verify Apps-genomsökning aktiveras för slutanvändarenheter. Om det här konfigureras blockeras slutanvändaren från åtkomst tills användaren aktiverar Googles appgenomsökning på sin Android-enhet.        |

#### <a name="level-2-enterprise-enhanced-data-protection"></a>Nivå 2: Förbättrat dataskydd för företag

Nivå 2 är den dataskyddskonfiguration som rekommenderas som standard för enheter vars användare får åtkomst till mer känslig information. De här enheterna är ett naturligt mål för angripare i dagens företagsvärld. De här rekommendationerna förutsätter inte att det finns en stor personal med säkerhetsexperter och bör därför vara genomförbara för de flesta företagsorganisationer. Den här konfigurationen utökar konfigurationen på nivå 1 genom att begränsa dataöverföringsscenarier och kräva en lägsta operativsystemversion.

I policyinställningarna som tillämpas på nivå 2 ingår alla policyinställningar som rekommenderas för nivå 1, men nedan visas bara de inställningar som har lagts till eller ändrats för att implementera fler kontroller och en mer avancerad konfiguration än nivå 1. De här inställningarna kan ha en något högre påverkan på användare eller program, men de upprätthåller en nivå av dataskydd som bättre motsvarar riskerna för användare med åtkomst till känslig information på mobila enheter.

#### <a name="data-protection"></a>Dataskydd

| Inställningen | Beskrivning av inställning |             Värde  |             Plattform        | Obs! |
|---------------|----------------------------------------------------------|-----------------------------------------------|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Dataöverföring |       Säkerhetskopiera organisationsdata till …  |          Blockera  |          iOS/iPadOS, Android  |                  |
| Dataöverföring |       Skicka organisationsdata till andra appar  |          Principhanterade appar  |          iOS/iPadOS, Android  |          <p>Med iOS/iPad kan administratörer konfigurera det här värdet så att det blir "Principhanterade appar", "Principhanterade appar med operativsystemdelning" eller "Principhanterade appar med Öppna i/Dela-filtrering". </p><p>Principhanterade appar med operativsystemdelning är tillgängliga när enheten också har registrerats med Intune. Den här inställningen tillåter dataöverföring till andra principhanterade appar samt filöverföringar till andra appar som hanteras av Intune. </p><p>Principhanterade appar med Öppna i/Dela-filtrering filtrerar dialogrutorna Öppna i/Dela i operativsystemet så att endast principhanterade appar visas. </p><p> Mer information finns i [Inställningar för iOS-appskyddsprinciper](app-protection-policy-settings-ios.md).</p> |
| Dataöverföring |       Välj vilka appar som ska undantas  |          Standard / skype;app-settings;calshow;itms;itmss;itms-apps;itms-appss;itms-services;  |          iOS/iPadOS  |                  |
| Dataöverföring |       Spara kopior av organisationsdata  |          Blockera  |          iOS/iPadOS, Android  |                  |
| Dataöverföring |       Tillåt användare att spara kopior i utvalda tjänster  |          OneDrive för företag, SharePoint Online |          iOS/iPadOS, Android  |                  |
| Dataöverföring |       Överför telekommunikationsdata till  |          Alla appar |          iOS/iPadOS, Android  |                  |
| Dataöverföring |       Begränsa klipp ut, kopiera och klistra in mellan appar  |          Principhanterade appar med inklistring  |          iOS/iPadOS, Android  |                  |
| Dataöverföring |       Skärmdump och Google Assistant  |          Blockera  |          Android  |                  |
| Funktioner |       Begränsa överföring av webbinnehåll till andra appar  |          Microsoft Edge  |          iOS/iPadOS, Android  |                  |
| Funktioner |       Meddelanden om organisationsdata  |          Blockera organisationsdata  |          iOS/iPadOS, Android  |          En lista över appar som stöder den här inställningen finns i [Inställningar för iOS-appskyddsprinciper](app-protection-policy-settings-ios.md) och [Inställningar för Android-appskyddsprinciper](app-protection-policy-settings-android.md).       |

#### <a name="conditional-launch"></a>Villkorlig start

| Inställningen | Beskrivning av inställning |          Värde/åtgärd  |          Plattform        | Obs! |
|--------------------|----------------------------|-----------------------------------------------------------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enhetsvillkor  |       Lägsta operativsystemversion  |          *Format: Major.Minor.Build <br>Exempel:   12.4.6*/Blockera åtkomst |          iOS/iPadOS        | Microsoft rekommenderar att du konfigurerar den lägsta iOS-huvudversionen till att matcha de iOS-versioner som stöds för Microsoft-appar.   Microsoft-appar stöder en N-1-metod där N är den aktuella iOS-huvudversionen. För mindre och byggbaserade versionsvärdet rekommenderar Microsoft att du kontrollerar att enheterna är uppdaterade med respektive säkerhetsuppdateringar. De senaste rekommendationerna från Apple finns i [Apple security updates](https://support.apple.com/en-us/HT201222) (Säkerhetsuppdateringar från Apple) |
| Enhetsvillkor  |       Lägsta operativsystemversion  |          *Format: Major.Minor<br> Exempel: 5.0*/Blockera åtkomst   |          Android        | Microsoft rekommenderar att du konfigurerar den lägsta Android-huvudversionen till att matcha de Android-versioner som stöds för Microsoft-appar. OEM-tillverkare och enheter som följer rekommenderade krav för Android Enterprise måste ha stöd för den aktuella leveransversionen plus en bokstavsuppgradering.   För närvarande rekommenderar Android 8.0 och senare för kunskapsarbetare.   De senaste rekommendationerna för Android finns i [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/) (Rekommenderade krav för Android Enterprise) |
| Enhetsvillkor  |       Lägsta korrigeringsversion  |          *Format:   ÅÅÅÅ-MM-DD <br> Exempel: 2020-01-01*/Blockera åtkomst  |          Android        | Android-enheter kan ta emot månatliga säkerhetskorrigeringar, men versionen är beroende av OEM-tillverkare och/eller operatörer. Organisationer bör se till att distribuerade Android-enheter tar emot säkerhetsuppdateringar innan de implementerar den här inställningen. De senaste korrigeringsversionerna finns i [Android Security Bulletins](https://source.android.com/security/bulletin/).  |

#### <a name="level-3-enterprise-high-data-protection"></a>Nivå 3: Starkt dataskydd för företag 

Nivå 3 är den dataskyddskonfiguration som rekommenderas som standard för organisationer med stora och avancerade säkerhetsorganisationer, eller för specifika användare och grupper som utsätts för ovanligt hög risk från angrepp. Sådana organisationer är ofta föremål för välfinansierade och avancerade angrepp, vilket berättigar de ytterligare begränsningar och kontroller som beskrivs. Den här konfigurationen utökar konfigurationen på nivå 2 genom att begränsa ytterligare dataöverföringsscenarier, öka komplexiteten för PIN-konfigurationen samt lägga till identifiering av mobila hot.  

I policyinställningarna som tillämpas på nivå 3 ingår alla policyinställningar som rekommenderas för nivå 2, men nedan visas bara de inställningar som lagts till eller ändrats för att implementera fler kontroller och en mer avancerad konfiguration än nivå 2. Dessa principinställningar har potentiellt stor påverkan på användare eller program, och ger därmed en säkerhetsnivå som är lämplig med tanke på de risker som gällande organisationer utsätts för.  

#### <a name="data-protection"></a>Dataskydd

| Inställningen | Beskrivning av inställning |             Värde  |             Plattform        | Obs! |
|---------------|---------------------------------------|----------------------------------------|--------------------------------------|---------------------------------------------------------------------------------------------------------|
| Dataöverföring |       Överför telekommunikationsdata till  |          Valfri principhanterad uppringningsapp |          Android  | Administratörer kan också konfigurera den här inställningen för att använda en uppringningsapp som inte har stöd för appskyddsprinciper genom att välja **En specifik uppringningsapp** och tillhandahålla värden för **Paket-id för uppringningsapp** och **Namn på uppringningsapp**.   |
| Dataöverföring |       Överför telekommunikationsdata till  |          En specifik uppringningsapp |          iOS/iPadOS  |  |
| Dataöverföring |       Webbadresschema för uppringningsapp  |          *replace_with_dialer_app_url_scheme* |          iOS/iPadOS  | På iOS/iPadOS måste det här värdet ersättas med URL-schemat för den anpassade uppringningsappen som används. Om URL-schemat är okänt kontaktar du appens utvecklare för mer information. Mer information om URL-scheman finns [Defining a Custom URL Scheme for Your App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app) (Definiera ett anpassat URL-schema för appen).|
| Dataöverföring |       Ta emot data från andra appar  |          Principhanterade appar  |          iOS/iPadOS, Android         |  |
| Dataöverföring |       Tangentbord från tredje part  |          Blockera  |          iOS/iPadOS        | På iOS/iPadOS blockeras alla tangentbord från tredje part i appen.  |
| Dataöverföring |       Godkända tangentbord  |          Kräver  |          Android        |  |
| Dataöverföring |       Välj tangentbord som ska godkännas  |          *lägg till/ta bort tangentbord*  |          Android        | Med Android måste tangentbord väljas för att kunna användas baserat på dina distribuerade Android-enheter.  |
| Funktioner |       Utskrift av organisationsdata  |          Blockera  |          iOS/iPadOS, Android         |  |

#### <a name="access-requirements"></a>Åtkomstkrav

|       Inställning  |          Värde  |          Plattform  |
|-----------------------------------------------------------|--------------------|---------------------------------|
|       Enkel PIN-kod  |          Blockera  |          iOS/iPadOS, Android  |
|       Välj minimilängd för PIN-kod  |          6  |          iOS/iPadOS, Android  |
|       Återställ PIN-kod efter antal dagar  |          Ja  |          iOS/iPadOS, Android  |
|       Antal dagar  |          365  |          iOS/iPadOS, Android  |

#### <a name="conditional-launch"></a>Villkorlig start

| Inställningen | Beskrivning av inställning |          Värde/åtgärd  |          Plattform        | Obs! |
|----------------------------|--------------------------------------|-------------------|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Enhetsvillkor  |       Lägsta operativsystemversion  |          *Format: Major.Minor<br> Exempel: 8.0*/Blockera åtkomst   |          Android        | Microsoft rekommenderar att du konfigurerar den lägsta Android-huvudversionen till att matcha de Android-versioner som stöds för Microsoft-appar. OEM-tillverkare och enheter som följer rekommenderade krav för Android Enterprise måste ha stöd för den aktuella leveransversionen plus en bokstavsuppgradering.   För närvarande rekommenderar Android 8.0 och senare för kunskapsarbetare.   De senaste rekommendationerna för Android finns i [Android Enterprise Recommended requirements](https://www.android.com/enterprise/recommended/requirements/) (Rekommenderade krav för Android Enterprise) |
|       Enhetsvillkor  |          Jailbrokade/rotade enheter  |        Ej tillämpligt/Rensa data  |          iOS/iPadOS, Android        |  |
|       Enhetsvillkor  |          Högsta tillåtna hotnivå  |          Skyddad/Blockera åtkomst  |          iOS/iPadOS, Android        | <p>Oregistrerade enheter kan kontrolleras med avseende på hot med hjälp av Mobile Threat Defense. Mer information finns i [Mobile Threat Defense för oregistrerade enheter](https://aka.ms/mtdmamdocs).      </p><p>     Om enheten har registrerats kan den här inställningen hoppas över och Mobile Threat Defense i stället distribueras för registrerade enheter. Mer information finns i [Mobile Threat Defense för registrerade enheter](../protect/mtd-device-compliance-policy-create.md).</p> |

## <a name="next-steps"></a>Nästa steg

Administratörer kan implementera ovanstående konfigurationsnivåer i sin ringdistributionsmetod för testning och produktionsanvändning genom att importera exemplet [JSON-mallar för ramverket för konfiguration av Intune-appskyddsprinciper](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AppProtectionPolicies) med [PowerShell-skript i Intune](https://github.com/microsoftgraph/powershell-intune-samples).

## <a name="see-also"></a>Se även

- [Skapa och distribuera appskyddsprinciper med Microsoft Intune](app-protection-policies.md)
- [Tillgängliga inställningar för Android-appskyddsprinciper med Microsoft Intune](app-protection-policy-settings-android.md)
- [Tillgängliga inställningar för iOS/iPadOS-appskyddsprinciper med Microsoft Intune](app-protection-policy-settings-ios.md)
- Appar från tredje part, till exempel Salesforce-mobilappen fungerar med Intune på specifika sätt för att skydda företagsdata. Läs mer om hur Salesforce-appen i synnerhet fungerar med Intune (inklusive MDM-appkonfigurationsinställningar) i [Salesforce-appen och Microsoft Intune](https://gallery.technet.microsoft.com/Salesforce-App-and-Intune-c47d44ee/file/188000/1/Salesforce%20App%20and%20Intune%20for%20external.pdf).