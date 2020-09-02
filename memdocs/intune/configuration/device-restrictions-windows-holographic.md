---
title: Inställningar för Windows Holographic for Business-enheter – Microsoft Intune – Azure | Microsoft Docs
description: Läs om och konfigurera inställningar för enhetsbegränsningar i Microsoft Intune för Windows Holographic for Business. Kontrollera avregistrering, geoposition, lösenord, installation av appar från app store, cookies och popup-fönster i Microsoft Edge, Microsoft Defender, sökningar, moln och lagring, Bluetooth-anslutningar, systemtid och användningsdata.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2cd769b8e3ca4497c095210ea266d225354db24c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912839"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>Enhetsinställningarna för Windows Holographic for Business tillåter eller begränsar funktioner med hjälp av Intune

Den här artikeln beskriver de olika inställningar som du kan styra på Windows Holographic for Business-enheter, till exempel Microsoft Hololens. Använd inställningarna som en del av din lösning för hantering av mobilenheter, för att tillåta eller inaktivera funktioner, kontrollera säkerheten etc.

Som Intune-administratör kan du skapa och tilldela dessa inställningar till dina enheter.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en Windows 10-konfigurationsprofil för enhetsbegränsningar](device-restrictions-configure.md#create-the-profile).

När du skapar en Windows 10-konfigurationsprofil för enhetsbegränsningar finns det fler inställningar än vad som anges i den här artikeln. Inställningarna i den här artikeln stöds på Windows Holographic for Business-enheter.

## <a name="app-store"></a>Appbutik

- **Uppdatera appar automatiskt från Store:** : **Blockera** förhindrar att uppdateringar installeras automatiskt från Microsoft Store. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att appar installerade från Microsoft Store uppdateras automatiskt.

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Installation av betrodd app**: Välj om icke-Microsoft Store-appar kan installeras, även kallat separat inläsning. Separat inläsning är att installera och sedan köra eller testa en app som inte är certifierad av Microsoft Store. Ett exempel kan vara en app som är intern för endast ditt företag. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Blockera**: Förhindrar separat inläsning. Icke-Microsoft Store-appar kan inte installeras.
  - **Tillåt**: Tillåter separat inläsning. Icke-Microsoft Store-appar kan installeras.

  [ApplicationManagement/AllowAllTrustedApps CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Lås upp via utvecklare**: Tillåt att användarna kan ändra utvecklarinställningar i Windows, som att tillåta separat inlästa appar. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Blockera**: Förhindrar utvecklarläge och separat inläsning av appar.
  - **Tillåt**: Tillåter utvecklarläge och separat inläsning av appar.

  [CSP:n ApplicationManagement/AllowDeveloperUnlock](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## <a name="cellular-and-connectivity"></a>Mobilnät och anslutning

- **Bluetooth**: **Blockera** hindrar användare från att aktivera Bluetooth. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att Bluetooth används på enheten.

  [CSP:n Connectivity/AllowBluetooth](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **Bluetooth-identifiering**: **Blockera** hindrar enheten från att identifieras av andra Bluetooth-aktiverade enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att andra Bluetooth-aktiverade enheter, som ett headset, identifierar enheten.

  [CSP:n Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Bluetooth-annonsering**: **Blockera** hindrar enheten från att skicka ut Bluetooth-annonsering. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att enheten skickar ut Bluetooth-annonsering.

  [CSP:n Bluetooth/AllowAdvertising](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## <a name="cloud-and-storage"></a>Moln och lagring

- **Microsoft-konto**: **Blockera** hindrar användare från att associera ett Microsoft-konto med enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta att ett Microsoft-konto läggs till och används.

  [CSP:n Accounts/AllowMicrosoftAccountConnection](/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## <a name="control-panel-and-settings"></a>Kontrollpanel och inställningar

- **Ändring av systemtid**: **Blockera** hindrar användare från att ändra inställningar för datum och tid på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användarna att ändra dessa inställningar.

  [CSP:n Settings/AllowDateTime](/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## <a name="general"></a>Allmänt

- **Manuell avregistrering**: **Blockera** hindrar användare från att ta bort arbetskontot via arbetskontrollpanelen på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

  [CSP:n Experience/AllowManualMDMUnenrollment](/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **Geoplats**: **Blockera** hindrar användare från att aktivera platstjänster på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

  [CSP:n Experience/AllowFindMyDevice](/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **Cortana**: **Blockera** inaktiverar röstassistenten Cortana på enheten. När Cortana är avstängt kan användare fortfarande söka för att hitta objekt på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta användning av Cortana.

  [CSP:n Experience/AllowCortana](/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## <a name="microsoft-edge-browser"></a>Microsoft Edge-webbläsaren

- **Starta upplevelse** > **Tillåt popup-fönster**: **Ja** (standard) tillåter popup-fönster i webbläsaren. **Nej** hindrar popup-fönster i webbläsaren.

  [CSP:n Browser/AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **Favoriter och Sök** > **Visa sökförslag**: **Ja** (standard) innebär att din sökmotor föreslår webbplatser när du skriver sökfraser i adressfältet. **Nej** förhindrar den här funktionen.

  [CSP:n Browser/AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **Sekretess och säkerhet** > **Tillåt lösenordshanteraren**: **Ja** (standard) tillåter Microsoft Edge att automatiskt använda lösenordshanteraren, som gör att användare kan spara och hantera lösenord på enheten. **Nej** hindrar Microsoft Edge från att använda lösenordshanteraren.

  [CSP:n Browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **Sekretess och säkerhet** > **Cookies**: Välj hur cookies ska hanteras i webbläsaren. Alternativen är:
  - **Tillåt**: Cookies sparas på enheten.
  - **Blockera alla cookies**: Cookies sparas på enheten.
  - **Blockera endast cookies från tredje part**: Cookies från tredje part eller partner sparas inte på enheten.

  [CSP:n Browser/AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **Sekretess och säkerhet** > **Skicka Do Not Track-huvuden**: **Ja** skickar Do Not Track-huvuden till webbplatser som kräver spårningsinfo (rekommenderas). **Nej** (standard) skickar inte sidhuvuden som gör att webbplatser kan spåra användaren. Användare kan konfigurera den här inställningen.

  [CSP:n Browser/AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **SmartScreen för Microsoft Edge**: **Kräv** aktiverar Microsoft Defender SmartScreen och hindrar användarna från att inaktivera funktionen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet aktivera SmartScreen och tillåta att användare aktiverar och inaktiverar funktionen.

  [CSP för Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

## <a name="password"></a>lösenordsinställning

- **Lösenord**: **Kräv** tvingar användarna att ange ett lösenord för att komma åt enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta åtkomst till enheter utan lösenord. Gäller endast för lokala konton. Lösenord för domänkonton förblir konfigurerade av Active Directory (AD) och Azure AD.

  [CSP:n DeviceLock/DevicePasswordEnabled](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **Kräv lösenord när enheten återgår från viloläge**: **Kräv** tvingar användarna att ange ett lösenord för att låsa upp enheten när den är inaktiv. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard kräva en PIN-kod eller ett lösenord när enheten varit inaktiv.

  [CSP:n DeviceLock/AllowIdleReturnWithoutPassword](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## <a name="reporting-and-telemetry"></a>Rapportering och telemetri

- **Dela användningsdata**: Välj nivå av diagnostikdata som skickas. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Ingen inställning framtvingas. Användarna väljer vilken nivå som ska skickas. Operativsystemet kan som standard inte dela några data.
  - **Säkerhet**: Information som krävs för att göra Windows säkrare, bland annat data om inställningar för komponenten Enhetlig användarupplevelse och telemetri, Borttagning av skadlig programvara och Microsoft Defender
  - **Grundläggande**: Grundläggande enhetsinformation som kvalitetsrelaterade data, appkompatibilitet, data om appanvändning och data från nivån Säkerhet
  - **Förbättrad**: Ytterligare information, bland annat hur Windows, Windows Server, System Center och appar används, deras prestanda, avancerade tillförlitlighetsdata och data från nivåerna Grundläggande och Säkerhet
  - **Fullständig**: Alla data som behövs för att identifiera och bidra till att lösa problem och data från nivåerna Säkerhet, Grundläggande och Förbättrad.

  [CSP för System/AllowTelemetry](/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

## <a name="search"></a>Sök

- **Sök plats**: **Blockera** hindrar Windows Search från att använda platsinformation. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kan som standard tillåta den här funktionen.

  [CSP:n Search/AllowSearchToUseLocation](/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).