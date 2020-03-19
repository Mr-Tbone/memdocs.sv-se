---
title: Enhetsbegränsningsinställningar för Windows 10 i Microsoft Intune – Azure | Microsoft Docs
description: Se en lista med alla inställningar och deras beskrivningar för att skapa enhetsbegränsningar i enheter med Windows 10 och senare. Använd dessa inställningar i en konfigurationsprofil för att styra skärmbilder, lösenordskrav, inställningar för helskärmsläge, appar i butiken, Microsoft Edge-webbläsaren, Microsoft Defender, åtkomst till molnet, startmenyn och mer i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/10/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8586e5c25ec3db4a736d84381e691ecebe6fae32
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361685"
---
# <a name="windows-10-and-newer-device-settings-to-allow-or-restrict-features-using-intune"></a>Enhetsinställningar för Windows 10 (och senare) för att tillåta eller begränsa funktioner med hjälp av Intune

Den här artikeln beskriver alla olika inställningar som du kan styra på enheter med Windows 10 och senare. Som en del av din MDM-lösning (hantering av mobilenheter) använder du dessa inställningar för att tillåta eller inaktivera funktioner, ange lösenordsregler, anpassa låsskärmen, använda Microsoft Defender och mer.

Dessa inställningar läggs till en profil för enhetskonfiguration i Intune som sedan tilldelas eller distribueras till dina Windows 10-enheter.

> [!Note]
> Alla alternativ finns inte tillgängliga i alla utgåvor av Windows. Information om vilka versioner som stöds finns i [princip-CSP:er](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) (en annan Microsoft-webbplats öppnas).

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en enhetskonfigurationsprofil](device-restrictions-configure.md#create-the-profile).

## <a name="app-store"></a>Appbutik

De här inställningarna använder [CSP för ApplicationManagement-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement), som även visar de Windows-versioner som stöds.

- **Appbutik** (endast mobil): **Blockera** förhindrar att slutanvändare får åtkomst till App Store på mobila enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta slutanvändare att komma åt App Store.
- **Uppdatera appar automatiskt från Store:** : **Blockera** förhindrar att uppdateringar installeras automatiskt från Microsoft Store. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att appar installerade från Microsoft Store uppdateras automatiskt.

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Installation av betrodd app**: Välj om icke-Microsoft Store-appar kan installeras, även kallat separat inläsning. Separat inläsning är att installera och sedan köra eller testa en app som inte är certifierad av Microsoft Store. Ett exempel kan vara en app som är intern för endast ditt företag. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Blockera**: Förhindrar separat inläsning. Icke-Microsoft Store-appar kan inte installeras.
  - **Tillåt**: Tillåter separat inläsning. Icke-Microsoft Store-appar kan installeras.
- **Lås upp via utvecklare**: Tillåter Windows utvecklarinställningar, till exempel att separat inlästa appar ska kunna ändras av slutanvändarna. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Blockera**: Förhindrar utvecklarläge och separat inläsning av appar.
  - **Tillåt**: Tillåter utvecklarläge och separat inläsning av appar.

  [Aktivera din enhet för utveckling](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development) innehåller mer information om den här funktionen.
  
  [ApplicationManagement/AllowAllTrustedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Dela appdata mellan användare**: Välj **Tillåt** för att dela programdata mellan olika användare på samma enhet och med andra instanser av den appen. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet förhindra delning av data med andra användare och andra instanser av samma app.

  [ApplicationManagement/AllowSharedUserAppData CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowshareduserappdata)

- **Använd endast privat katalog**: **Tillåt** tillåter endast att appar laddas ned från en privat katalog och inte laddas ned från den offentliga katalogen, inklusive butikskataloger. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att appar laddas ned från en privat katalog och en offentlig katalog.

  [ApplicationManagement/RequirePrivateStoreOnly CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-requireprivatestoreonly)

- **Start av appar från Store**: **Blockera** inaktiverar alla appar som har förinstallerats på enheten eller hämtats från Microsoft Store. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att dessa appar öppnas.

  [ApplicationManagement/DisableStoreOriginatedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-disablestoreoriginatedapps)

- **Installera appdata på systemvolym**: **Blockera** hindrar appar från att lagra data på enhetens systemvolym. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att appar lagrar data på systemdiskvolymen.

  [ApplicationManagement/RestrictAppDataToSystemVolume CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictappdatatosystemvolume)

- **Installera appar på systemenhet**: **Blockera** hindrar appar från att installera på enhetens systemenhet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta att appar installeras på systemenheten.

  [ApplicationManagement/RestrictAppToSystemVolume CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictapptosystemvolume)

- **Spel-DVR (endast stationär dator)** : **Blockera** inaktiverar Windows-inspelning och -sändning av spel. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan operativsystemet tillåta inspelning och sändning av spel.

  [ApplicationManagement/AllowGameDVR CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

- **Endast appar från Store**: Den här inställningen styr användarupplevelsen när användare installerar appar från andra platser än Microsoft Store. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Som standard kan operativsystemet tillåta att slutanvändare installerar appar från andra platser än Microsoft Store, inklusive appar som definierats i andra principinställningar.  
  - **Överallt**: Stänger av apprekommendationer och låter användarna installera appar från valfri plats.  
  - **Endast Store**: Tvingar slutanvändare att endast installera appar från Microsoft Store.
  - **Rekommendationer**: Vid installation av en app från webben som är tillgänglig i Microsoft Store visas ett meddelande för användare där de rekommenderas att ladda ned den från Store.  
  - **Prioritera Store**: Varnar användare när de installerar appar från andra platser än Microsoft Store.

  [CSP för SmartScreen/EnableAppInstallControl](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enableappinstallcontrol)

- **Användarkontroll över installationer**: **Blockera** förhindrar att användare ändrar installationsalternativ som vanligtvis är reserverade för systemadministratörer, till exempel att ange den katalog som filerna ska installeras till. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan Windows Installer hindra användare från att ändra de här installationsalternativen, och några av säkerhetsfunktionerna i Windows Installer kringgås.

  [ApplicationManagement/MSIAllowUserControlOverInstall CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Installera appar med förhöjd behörighet**: **Blockera** säger till Windows Installer att använda förhöjda behörigheter när alla program installeras på systemet. De här behörigheterna används för alla program. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Som standard kan systemet använda den aktuella användarens behörigheter när det installerar program som en systemadministratör inte distribuerar eller erbjuder. 

  [ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Startappar**: Ange en lista över appar som ska öppnas när en användare loggar in på enheten. Glöm inte att använda en semikolonavgränsad lista över paketfamiljenamn (PFN) för Windows-program. Manifestet i Windows-apparna måste använda en startåtgärd för att den här principen ska fungera.

  [ApplicationManagement/LaunchAppAfterLogOn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-launchappafterlogon)

## <a name="cellular-and-connectivity"></a>Mobilnät och anslutning

De här inställningarna använder CSP:er för [anslutningsprincip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity) och [Wi-Fi-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wifi), som även visar de Windows-versioner som stöds.

- [CSP för Wi-Fi-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wifi)

- **Mobildatakanal**: Välj huruvida slutanvändare kan använda data, till exempel för webbsurfning, när de har anslutning till ett mobilnät. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Slutanvändare kan stänga av det.
  - **Blockera**: Tillåt inte mobildatakanalen. Slutanvändare kan inte aktivera det.
  - **Tillåt (kan inte redigeras)** : Tillåter mobildatakanalen. Slutanvändare kan inte stänga av det.

- **Datanätverksväxling**: **Blockera** förhindrar dataroaming av mobildata på enheten. **Inte konfigurerat** (standard): tillåter roaming mellan nätverk vid åtkomst till data.
- **VPN över mobilt nätverk**: **Blockera** hindrar enheten från att komma åt VPN-anslutningar när den är ansluten till ett mobilt nätverk. **Inte konfigurerat** (standard) tillåter VPN att använda alla anslutningar, däribland mobildata.
- **VPN-nätverksväxling över mobilt nätverk**: **Block** hindrar att enheten kommer åt VPN-anslutningar när roaming används i ett mobilnät. **Inte konfigurerat** (standard) tillåter VPN-anslutningar vid roaming.
- **Connected Devices Service**: **Blockera** inaktiverar komponenten Connected Devices Platform (CDP). CDP möjliggör identifiering och anslutning till andra enheter (via Bluetooth/LAN eller moln) för fjärrstart av appar, fjärrmeddelanden, fjärrappsessioner och andra upplevelser mellan flera enheter. **Not configured** (default) tillåter Connected Devices Service, som möjliggör identifiering och anslutning till andra Bluetooth-enheter.
- **NFC**: **Blockera** hindrar NFC-funktioner (närfältskommunikation ). **Inte konfigurerat** (standard) tillåter användare att aktivera och konfigurera NFC-funktioner på enheten.
- **Trådlöst**: **Blockera** hindrar användare från att aktivera, konfigurera och använda Wi-Fi-anslutningar på enheten. **Inte konfigurerat** (standard) tillåter Wi-Fi-anslutningar.
- **Anslut automatiskt till trådlösa surfpunkter**: **Blockera** hindrar enheter från att automatiskt ansluta till Wi-Fi-hotspots. **Inte konfigurerat** (standard) tillåter att enheter automatiskt ansluter till kostnadsfria Wi-Fi-hotspots och automatiskt godkänner eventuella villkor för anslutningen.
- **Manuell trådlös konfiguration**: **Blockera** hindrar enheter från att ansluta till Wi-Fi utanför MDM-serverinstallerade nätverk. **Inte konfigurerat** (standard) tillåter slutanvändare att lägga till och konfigurera sina egna nätverks-SSID för Wi-Fi-anslutningar.
- **Sökintervall för trådlöst nätverk**: Ange hur ofta enheterna ska söka efter trådlösa nätverk. Ange ett värde mellan 1 (mest frekvent) till 500 (minst frekvent). Standardvärdet är `0` (noll).

### <a name="bluetooth"></a>Bluetooth

De här inställningarna använder [CSP för Bluetooth-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth), som även visar de Windows-versioner som stöds.

- **Bluetooth**: **Blockera** hindrar användare från att aktivera Bluetooth. **Inte konfigurerat** (standard) tillåter Bluetooth på enheten.
- **Bluetooth-identifiering**: **Blockera** hindrar enheten från att identifieras av andra Bluetooth-aktiverade enheter. **Inte konfigurerat** (standard) tillåter andra Bluetooth-aktiverade enheter, till exempel ett headset, att identifiera enheten.
- **Bluetooth-förhandsparkoppling**: **Blockera** hindrar specifika Bluetooth-enheter från att automatiskt parkopplas med en värdenhet. **Inte konfigurerat** (standard) tillåter automatisk parkoppling med värdenheten.
- **Bluetooth-annonsering**: **Blockera** hindrar enheten från att skicka ut Bluetooth-annonsering. **Inte konfigurerat** (standard) tillåter att enheten skickar ut Bluetooth-annonsering.
- **Bluetooth-tillåtna tjänster**: **Lägg till** en lista över tillåtna Bluetooth-tjänster och -profiler som hexadecimala strängar, till exempel `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`.

  [Användningsguiden för ServicesAllowedList](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) innehåller information om tjänstlistan.

## <a name="cloud-and-storage"></a>Moln och lagring

De här inställningarna använder [CSP för kontoprincip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts), som även visar de Windows-versioner som stöds.

- **Microsoft-konto**: **Blockera** hindrar slutanvändare från att associera ett Microsoft-konto med enheten. **Inte konfigurerat** (standard) tillåter tillägg och användning av ett Microsoft-konto.
- **Andra konton än Microsoft-konton**: **Blockera** hindrar slutanvändare från att lägga till icke-Microsoft-konton via användargränssnittet. **Inte konfigurerat** (standard) tillåter användare att lägga till e-postkonton som inte associeras med ett Microsoft-konto.
- **Synkroniseringsinställningar för Microsoft-konto**: **Inte konfigurerat** (standard) tillåter att enhets- och appinställningar som associeras med ett Microsoft-konto synkroniseras mellan enheter. **Blockera** förhindrar den här synkroniseringen.
- **Inloggningsassistent för Microsoft-konton**: När det här är inställt på **Inte konfigurerat** (standard) kan slutanvändare starta och stoppa tjänsten **Inloggningsassistent för Microsoft-konton** (wlidsvc). Den här operativsystemtjänsten tillåter att användare loggar in på sitt Microsoft-konto. **Inaktivera** hindrar slutanvändare från att kontrollera Inloggningsassistent för Microsoft-konton (wlidsvc).

## <a name="cloud-printer"></a>Molnskrivare

De här inställningarna använder [CSP för EnterpriseCloudPrint-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint), som även visar de Windows-versioner som stöds.

- **URL för skrivaridentifiering**: Ange URL:en för identifiering av molnskrivare. Ange till exempel `https://cloudprinterdiscovery.contoso.com`.
- **URL för utfärdare av skrivaråtkomst**: Ange URL för autentiseringsslutpunkt för att hämta OAuth-token. Ange till exempel `https://azuretenant.contoso.com/adfs`.
- **GUID för inbyggd Azure-klientapp**: Ange GUID för ett klientprogram som har behörighet att hämta OAuth-token från OAuthAuthority. Ange till exempel `E1CF1107-FF90-4228-93BF-26052DD2C714`.
- **Resurs-URI för utskriftstjänst**: Ange OAuth resurs-URI för utskriftstjänster som konfigurerats i Azure-portalen. Ange till exempel `http://MicrosoftEnterpriseCloudPrint/CloudPrint`.
- **Maxantal skrivare att fråga efter**: Ange maximalt antal skrivare som du vill att frågor körs mot. Standardvärdet är `20`.
- **Resurs-URI för identifiering av utskriftstjänst**: Ange OAuth resurs-URI för identifiering av utskriftstjänster som konfigurerats i Azure-portalen. Ange till exempel `http://MopriaDiscoveryService/CloudPrint`.

> [!TIP]
> När du har konfigurerat en [Windows Server Hybrid Cloud Print](https://docs.microsoft.com/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-overview) kan du konfigurera dessa inställningar och sedan distribuera till dina Windows-enheter.

## <a name="control-panel-and-settings"></a>Kontrollpanel och inställningar

- **Inställningar**: **Blockera** hindrar slutanvändare från att komma åt appen Inställningar i Windows. **Inte konfigurerat** (standard) gör att användarna kan öppna appen Inställningar på enheten.
  - **System**: **Blockera** hindrar åtkomst till området System i appen Inställningar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
    - **Ändra energialternativinställningar (endast stationär dator)** : **Blockera** hindrar slutanvändare från att ändra energialternativinställningar på enheten. **Inte konfigurerat** (standard) tillåter användare att ändra energialternativinställningarna.
  - **Enheter**: **Blockera** hindrar åtkomst till området Enheter i appen Inställningar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
  - **Nätverk och Internet**: **Blockera** hindrar åtkomst till området Nätverk och Internet i appen Inställningar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
  - **Anpassning**: **Blockera** hindrar åtkomst till området Personanpassning i appen Inställningar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
  - **Appar**: **Blockera** hindrar åtkomst till området Appar i appen Inställningar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
  - **Konton**: **Blockera** hindrar åtkomst till området Konton i appen Inställningar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
  - **Tid och språk**: **Blockera** hindrar åtkomst till området Tid och språk i appen Inställningar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
    - **Ändring av systemtid**: **Blockera** hindrar slutanvändare från att ändra inställningar för datum och tid på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Användarna kan ändra inställningarna.
    - **Ändra regionsinställningar** (endast skrivbordsversion): **Blockera** hindrar slutanvändare från att ändra de nationella inställningarna på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Användarna kan ändra inställningarna.
    - **Ändra språkinställningar (endast stationär dator)** : **Blockera** hindrar slutanvändare från att ändra språkinställningarna på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Användarna kan ändra inställningarna.

      [CSP för inställningsprincip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings)

  - **Spel**: **Blockera** hindrar åtkomst till området Spel i appen Inställningar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
  - **Hjälpmedel**: **Blockera** hindrar åtkomst till området Hjälpmedel i appen Inställningar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
  - **Sekretess**: **Blockera** hindrar åtkomst till området Sekretess i appen Inställningar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
  - **Uppdatering och säkerhet**: **Blockera** hindrar åtkomst till området Uppdatering och säkerhet i appen Inställningar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

## <a name="display"></a>Visning

De här inställningarna använder [CSP för visningsprincip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-display), som även visar de Windows-versioner som stöds.

Med GDI DPI-skalning kan program som inte är DPI-medvetna bli DPI-medvetna per övervakare.

- **Aktivera GDI-skalning för appar**: **Lägg till** de äldre appar som du aktivera GDI DPI-skalning för. Ange till exempel `filename.exe` eller `%ProgramFiles%\Path\Filename.exe`.

  GDI DPI-skalning aktiveras för alla äldre program i listan.

- **Stäng av GDI-skalning för appar**: **Lägg till** de äldre appar som du vill inaktivera GDI DPI-skalning för. Ange till exempel `filename.exe` eller `%ProgramFiles%\Path\Filename.exe`.

  GDI DPI-skalning stängs av för alla äldre program i listan.

Du kan även **Importera** en .csv-fil med listan över appar.

## <a name="general"></a>Allmänt

De här inställningarna använder [CSP för upplevelseprincip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience), som även visar de Windows-versioner som stöds. 

- **Skärmdump** (endast mobil): **Blockera** hindrar slutanvändare från att få skärmbilder på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Kopiera och klistra in (endast mobil)** : **Blockera** hindrar slutanvändare från att använda kopiera och klistra in mellan appar på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Manuell avregistrering**: **Blockera** hindrar slutanvändare från att ta bort arbetskontot via arbetskontrollpanelen på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

  Den här principinställningen gäller inte om datorn är Azure AD-ansluten och automatisk registrering har aktiverats.

- **Manuell installation av rotcertifikat** (endast mobil): **Blockera** hindrar slutanvändare från att manuellt installera rotcertifikat och mellanliggande CAP-certifikat. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Kamera**: **Blockera** hindrar slutanvändare från att använda kameran på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

  [CSP för kamera](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-camera)

- **OneDrive-filsynkronisering**: **Blockera** hindrar slutanvändare från att synkronisera filer till OneDrive från enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Flyttbara lagringsmedier**: **Blockera** hindrar slutanvändare från att använda externa lagringsenheter, till exempel SD-kort, med enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Geoplats**: **Blockera** hindrar slutanvändare från att aktivera platstjänster på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Internetdelning**: **Blockera** hindrar delning av Internetanslutning på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Telefonåterställning**: **Blockera** hindrar slutanvändare från att rensa eller utföra en fabriksåterställning av enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **USB-anslutning**: **Blockera** hindrar åtkomst till externa lagringsenheter via en USB-anslutning på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. USB-laddning påverkas inte av den här inställningen.
- **Stöldskyddsläge** (endast mobil): **Blockera** hindrar slutanvändare från att välja inställningar för stöldskyddsläge på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Cortana**: **Blockera** inaktiverar röstassistenten Cortana på enheten. När Cortana är avstängt kan användare fortfarande söka för att hitta objekt på enheten. **Inte konfigurerat** (standard) tillåter Cortana.
- **Röstinspelning** (endast mobil): **Blockera** hindrar slutanvändare från att använda enhetens röstinspelning på enheten. **Inte konfigurerat** (standard) tillåter röstinspelning för appar.
- **Ändra enhetsnamn** (endast mobil): **Blockera** hindrar slutanvändare från att ändra enhetens namn. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Lägg till konfigurationspaket**: **Blockera** hindrar den runtime-konfigurationsagent som installerar konfigurationspaket på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Ta bort konfigurationspaket**: **Blockera** hindrar den runtime-konfigurationsagent som tar bort konfigurationspaket från enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Enhetsidentifiering**: **Blockera** hindrar enheten från att identifieras av andra enheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Växla mellan aktiviteter** (endast mobil): **Blockera** hindrar aktivitetsväxling på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Dialogruta om SIM-kortsfel** (endast mobil): **Blockera** felmeddelanden från att visas på enheten om inget SIM-kort har upptäckts. **Inte konfigurerat** (standard) visar felmeddelandena.
- **Ink-arbetsytan**: Välj om och hur användaren kommer åt ink-arbetsytan. Alternativen är:
  - **Inte konfigurerat** (standard): Aktiverar Ink-arbetsytan och användaren kan använda den ovanför låsskärmen.
  - **Inaktiverad på låsskärmen**: Ink-arbetsytan och funktionen är aktiverade. Men användaren kan inte komma åt den ovanför låsskärmen.
  - **Inaktiverad**: Åtkomsten till ink-arbetsytan är inaktiverad. Funktionen är inaktiverad.

  [CSP för WindowsInkWorkspace-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsinkworkspace)

- **Automatisk omdistribution**: Välj **Tillåt** för att användare med administrativ behörighet ska kunna ta bort alla användardata och inställningar med hjälp av **Ctrl + Win + R** på enhetens låsskärm. Enheten omkonfigureras automatiskt och omregistreras för hantering. **Inte konfigurerad** (standard) förhindrar den här funktionen.
- **Användarna måste ansluta till nätverket när enheten ställs in**: Välj **Kräv** för att göra så att enheten ansluter till ett nätverk innan användarna går vidare från sidan Nätverk under installationen av Windows. **Inte konfigurerat** (standard) tillåter att användare går vidare från sidan Nätverk även om enheten inte är ansluten till ett nätverk.

  Inställningen börjar gälla nästa gång enheten rensas eller återställs. Som alla andra Intune-konfigurationer måste enheten vara registrerad och hanteras av Intune för att ta emot konfigurationsinställningar. När den har registrerats och tar emot principer tillämpas inställningen under nästa Windows-installation om enheten återställs.

  [CSP för TenantLockdown](https://docs.microsoft.com/windows/client-management/mdm/tenantlockdown-csp)

- **Direkt minnesåtkomst**: **Blockera** förhindrar direkt minnesåtkomst (DMA) för alla underordnade PCI-portar med enhetsbyte vid drift tills en användare loggar in i Windows. **Aktiverad** (standard) ger åtkomst till DMA, även när en användare inte har loggat in.

  [CSP för DataProtection/AllowDirectMemoryAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

- **Avsluta processer från Aktivitetshanteraren**: Den här inställningen avgör om icke-administratörer kan använda Aktivitetshanteraren för att avsluta uppgifter. **Blockera** förhindrar standardanvändare (icke-administratörer) att använda Aktivitetshanteraren till att avsluta en process eller uppgift på enheten. **Inte konfigurerad** (standard) låter standardanvändare att avsluta en process eller uppgift med Aktivitetshanteraren.

## <a name="locked-screen-experience"></a>Låsskärm

- **Aviseringar från Åtgärdscenter (endast mobil)** : **Blockera** hindrar aviseringar från Åtgärdscenter från att visas på enhetens låsskärm. **Inte konfigurerat** (standard) tillåter användare att välja vilka appar som visar meddelanden på låsskärmen.

  [CSP för AboveLock/AllowActionCenterNotifications](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#AboveLock_AllowActionCenterNotifications)

- **URL till bild på låst skärm (endast stationär dator)** : Anger URL till en bild i formatet JPG, JPEG eller PNG som används som bakgrundsbild för låsskärmen i Windows. Ange till exempel `https://contoso.com/image.png`. Den här inställningen låser bilden och kan inte ändras efteråt.

  [CSP för Personalization/LockScreenImageUrl](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp)

- **Skärmtidsgräns kan ställas in av användaren (endast Mobile)** : **Tillåt** låter användare konfigurera skärmtidsgränsen. **Inte konfigurerat** (standard) ger inte användarna det här alternativet.

  [CSP för DeviceLock/AllowScreenTimeoutWhileLockedUserConfig](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_AllowScreenTimeoutWhileLockedUserConfig)

- **Cortana på låst skärm** (endast stationär dator): **Blockera** hindrar användare från att interagera med Cortana när enheten är på låsskärmen. **Inte konfigurerat** (standard) tillåter interaktion med Cortana.

  [CSP för AboveLock/AllowCortanaAboveLock](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowcortanaabovelock)

- **Popup-meddelanden på låst skärm**: **Blockera** hindrar popup-meddelanden från att visas på enhetens låsskärm. **Inte konfigurerat** (standard) tillåter dessa meddelanden.

  [CSP för AboveLock/AllowToasts](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)

- **Skärmtidsgräns (endast mobil)** : Ange varaktigheten (i sekunder) från skärmlåsning till avstängning av skärmen. Värden som stöds är 11–1800. Ange till exempel `300` för att ställa in tidsgränsen på 5 minuter.

  [CSP för DeviceLock/ScreenTimeoutWhileLocked](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_ScreenTimeoutWhileLocked)

## <a name="messaging"></a>Meddelandefunktion

De här inställningarna använder [CSP för meddelandeprincip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-messaging), som även visar de Windows-versioner som stöds.

- **Meddelandesynkronisering (endast mobil)** : **Blockera** hindrar textmeddelanden från att säkerhetskopieras och återställas och hindrar meddelandesynkronisering mellan Windows-enheter. Inaktivera hjälper till att förhindra att information lagras på servrar utanför organisationens kontroll. **Inte konfigurerat** (standard) tillåter användare att ändra de här inställningarna och synkronisera sina meddelanden.
- **MMS (endast mobil)** : **Blockera** inaktiverar funktionen för att skicka och ta emot MMS på enheten. På företag används den här principen för att inaktivera MMS på enheter som en del av kraven för granskning eller hantering. **Inte konfigurerat** (standard) tillåter att MMS skickas och tas emot.
- **RCS (endast mobil)** : **Blockera** inaktiverar funktionen för att skicka och ta emot Rich Communication Services (RCS) på enheten. På företag används den här principen för att inaktivera RCS på enheter som en del av kraven för granskning eller hantering. **Inte konfigurerat** (standard) tillåter att RCS skickas och tas emot.

## <a name="microsoft-edge-browser"></a>Microsoft Edge-webbläsaren

De här inställningarna använder [CSP för webbläsarprincip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser), som även visar de Windows-versioner som stöds.

### <a name="use-microsoft-edge-kiosk-mode"></a>Använda helskärmsläget i Microsoft Edge

De tillgängliga inställningarna varierar beroende på vad du väljer. Alternativen är:

- **Nej** (standard): Microsoft Edge körs inte i helskärmsläge. Alla Microsoft Edge-inställningar kan ändras och konfigureras.
- **Digital/interaktiv signering (helskärmsenhet för enstaka app)** : Filtrerar Microsoft Edge-inställningar som gäller för digital/interaktiv signering med Microsoft Edge-helskärmsläge för användning med enskilda appar i Windows 10-helskärmsläge. Välj den här inställningen om du vill öppna URL:en i helskärmsläge och endast visa innehållet på webbplatsen. Mer information om den här funktionen finns i [Konfigurera digital signering](https://docs.microsoft.com/windows/configuration/setup-digital-signage).
- **Offentlig surfning InPrivate (helskärmsenhet för enstaka app)** : Filtrerar Microsoft Edge-inställningar som kan användas i Microsoft Edge-helskärmsläge med offentlig InPrivate-surfning när Windows 10-helskärmsläge används med enstaka appar. Kör en version av Microsoft Edge med flera flikar.
- **Normalt läge (helskärmsenhet för flera appar)** : Filtrerar Microsoft Edge-inställningar som kan användas i normalt helskärmsläge med Microsoft Edge. Kör en fullständig version av Microsoft Edge med alla webbläsarens funktioner.
- **Offentlig surfning (helskärmsenhet för flera appar)** : Filtrerar Microsoft Edge-inställningar som kan användas med offentliga surfning i Windows 10-helskärmsläge för flera appar.  Kör en version av InPrivate i Microsoft Edge med flera flikar.

> [!TIP]
> Mer information om vad dessa alternativ gör finns i [Typer av konfigurationer för Microsoft Edge-helskärmsläge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

Den här profilen för enhetsbegränsning är direkt kopplad till profilen för helskärmsläge som du skapar med [inställningarna för Windows-helskärmsläge](kiosk-settings-windows.md). Sammanfattningsvis:

1. Skapa profilen med [inställningar för Windows-helskärmsläge](kiosk-settings-windows.md) för att köra enheten i helskärmsläge. Välj Microsoft Edge som programmet och ställ in helskärmsläge för Microsoft Edge i profilen för helskärmsläge.
2. Skapa profilen för enhetsbegränsning som beskrivs i den här artikeln och konfigurera specifika funktioner och inställningar som tillåts i Microsoft Edge. Var noga med att välja samma typ av Microsoft Edge-helskärmsläge som du valde i profilen för helskärmsläge ([inställningarna för Windows-helskärmsläge](kiosk-settings-windows.md)). 

    [Inställningar som stöds för helskärmsläge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-policies-for-kiosk-mode) är en bra resurs.

> [!IMPORTANT] 
> Var noga med att tilldela den här Microsoft Edge-profilen till samma enheter som profilen för helskärmsläge ([inställningarna för Windows-helskärmsläge](kiosk-settings-windows.md)).

[ConfigureKioskMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configurekioskmode)

### <a name="start-experience"></a>Startupplevelse

- **Starta Microsoft Edge med**: Välj vilka sidor som ska öppnas när Microsoft Edge startar. Alternativen är:
  - **Anpassade startsidor**: Ange startsidorna, till exempel `http://www.contoso.com`. Microsoft Edge läser in de startsidor som du anger.
  - **Sidan Ny flik**: Microsoft Edge läser in det som anges i inställningen **Webbadress till Ny flik**.
  - **Senaste sessionssidan**: Microsoft Edge läser in den senaste sessionssidan.
  - **Startsidor i lokala appinställningar**: Microsoft Edge startar med den standardstartsida som definieras av operativsystemet.

- **Tillåt användaren att ändra startsidor**: **Ja** (standard) låter användarna ändra startsidorna. Administratörer kan använda `EdgeHomepageUrls` till att ange de startsidor som användarna ser som standard när de öppnar Microsoft Edge. **Nej** blockerar användarna från att ändra startsidorna.
- **Tillåt webbinnehåll på sidan Ny flik**: När det här anges till **Ja** (standard), öppnar Microsoft Edge den URL som anges i inställningen **Webbadress till Ny flik**. Om inställningen **Webbadress till Ny flik** är tom öppnar Microsoft Edge den sida för ny flik som anges i Microsoft Edge-inställningarna. Användare kan ändra det. När den anges till **Nej** öppnar Microsoft Edge en ny flik med en tom sida. Användare kan inte ändra det.
- **Webbadress till Ny flik**: Ange den webbadress som ska öppnas på sidan Ny flik. Ange till exempel `https://www.bing.com` eller `https://www.contoso.com`.

- **Hemknapp**: Ange vad som händer när hemknappen väljs. Alternativen är:
  - **Startsidor**: Öppnar det alternativ som du valde i inställningen **Starta Microsoft Edge med**
  - **Sidan Ny flik**: Öppnar den webbadress som du angav i inställningen **Webbadress till Ny flik**.
  - **Webbadress till hemknapp**: Anger den URL som ska öppnas. Ange till exempel `https://www.bing.com` eller `https://www.contoso.com`.
  - **Dölj hemknapp**: Döljer hemknappen
- **Tillåt användarna att ändra hemknappen**: **Ja** låter användarna ändra hemknappen. Användarens ändringar åsidosätter eventuella administratörsinställningar för hemknappen. **Nej** (standard) blockerar användare från att ändra administratörens konfiguration av startknappen.
- **Visa sidan Välkomstprogram (endast Mobile)** : **Ja** (standard) visar introduktionssidan för första användning i Microsoft Edge. **Nej** hindrar introduktionssidan från att visas första gången du kör Microsoft Edge. Den här funktionen låter företag, exempelvis organisationer som registrerat sig för nollutsläppskonfigurationer, att blockera den här sidan.
- **Plats för webbadresslista till välkomstprogram**  (endast Windows 10 Mobile): Ange den webbadress som pekar på den XML-fil som innehåller webbadresserna för välkomstsidan. Ange till exempel `https://www.contoso.com/sites.xml`.

- **Uppdatera webbläsaren efter inaktivitetstid**: Ange efter hur många minuters inaktivitet som webbläsaren ska uppdateras, från 0–1 440 minuter. Standardvärdet är `5` minuter. När värdet är `0` (noll) uppdateras inte webbläsaren efter en viss tids inaktivitet.

  Den här inställningen är endast tillgänglig när du kör med [offentlig InPrivate-surfning (helskärmsläge för enstaka app)](#use-microsoft-edge-kiosk-mode).

- **Tillåt popup-fönster** (endast stationär dator): **Ja** (standard) tillåter popup-fönster i webbläsaren. **Nej** hindrar popup-fönster i webbläsaren.
- **Skicka intranätstrafik till Internet Explorer** (endast stationär dator): **Ja** låter användarna öppna intranätwebbplatser i Internet Explorer i stället för i Microsoft Edge. Den här inställningen är till för bakåtkompatibilitet. **Inte konfigurerat** (standard) tillåter att användarna använder Microsoft Edge.
- **Plats för webbplatslista för företagsläge** (endast stationär dator): Ange den URL som pekar på den XML som innehåller en lista med webbplatser som öppnas i företagsläge. Användarna kan inte ändra denna lista. Ange till exempel `https://www.contoso.com/sites.xml`.
- **Meddelande när webbplatser öppnas i Internet Explorer**: Använd den här inställningen för att konfigurera att Microsoft Edge ska visa ett meddelande innan en webbplats öppnas i Internet Explorer 11. Alternativen är:
  - **Visa inte meddelande**: Operativsystemets standardbeteende används, vilket kan innebära att ett meddelande inte visas.
  - **Visa meddelande om att webbplatsen har öppnats i Internet Explorer 11**: Visa meddelandet när webbplatser öppnas i IE. Webbplatser öppnas i Internet Explorer. 
  - **Visa meddelande med alternativ för att öppna webbsidor i Microsoft Edge**: Visa meddelande när webbplatser öppnas i Microsoft Edge. Meddelandet innehåller länken **Fortsätt i Microsoft Edge** för att användarna ska kunna välja Microsoft Edge i stället för Internet Explorer.

  > [!IMPORTANT]
  > Den här inställningen kräver att du använder inställningen **Plats för webbplatslista för företagsläge** inställningen **Skicka intranätstrafik till Internet Explorer** eller båda inställningarna.

- **Tillåt Microsoft-kompatibilitetslista**: **Ja** (standard) tillåter användning av en Microsoft-kompatibilitetslista. **Nej** förhindrar Microsoft-kompatibilitetslistan i Microsoft Edge. Med den här listan från Microsoft kan Microsoft Edge korrekt visa webbplatser med kända kompatibilitetsproblem.
- **Läs in startsidor och sidan Ny flik i förväg**: **Ja** (standard) använder standardbeteendet för operativsystemet, som kan vara att läsa in dessa sidor i förväg. Förinläsningen minimerar den tid det tar att starta Microsoft Edge och läsa in nya flikar. **Nej** förhindrar att Microsoft Edge läser in startsidor och sidan Ny flik i förväg.
- **Starta startsidor och sidan Ny flik i förväg**: **Ja** (standard) använder standardbeteendet för operativsystemet, som kan vara att starta dessa sidor i förväg. Genom att starta Microsoft Edge i förväg förbättras prestandan och den tid som krävs för att starta Microsoft Edge minimeras. **Nej** förhindrar att Microsoft Edge startar startsidor och sidan Ny flik i förväg.

### <a name="favorites-and-search"></a>Favoriter och sökning

- **Visa fältet Favoriter**: Välj vad som ska hända i fältet Favoriter på valfri Microsoft Edge-sida. Alternativen är:
  - **På sidorna Start och Ny flik**: Visar fältet Favoriter när Microsoft Edge startar samt på alla flikar. Slutanvändare kan ändra den här inställningen.
  - **På alla sidor**: Visar fältet Favoriter på alla sidor. Slutanvändare kan inte ändra den här inställningen.
  - **Dolt**: Döljer fältet Favoriter på alla sidor. Slutanvändare kan inte ändra den här inställningen.
- **Tillåt ändringar av favoriter**: **Ja** (standard) använder standardinställningen för operativsystemet, vilket tillåter användare att ändra listan. **Nej** hindrar slutanvändare från att lägga till, importera, sortera och redigera i listan Favoriter.
  - **Listan Favoriter**: Lägg till en lista med webbadresser i filen med Favoriter. Lägg exempelvis till `http://contoso.com/favorites.html`.
- **Synkronisera favoriter mellan Microsoft-webbläsare (endast stationär dator)** : **Ja** tvingar Windows att synkronisera favoriter mellan Internet Explorer och Microsoft Edge. Tillägg, borttagningar, modifieringar och sorteringsändringar i Favoriter delas mellan webbläsarna.  **Nej** (standard) använder operativsystemets standard, vilket kan ge användarna möjlighet att synkronisera favoriter mellan webbläsarna.
- **Standardsökmotor**: Välj den standardsökmotor som ska användas på enheten. Användarna kan ändra det här värdet när som helst. Alternativen är:
  - Sökmotor i Microsoft Edge-klientinställningarna
  - Bing
  - Google
  - Yahoo
  - Anpassat värde: I **Webbadress till OpenSearch Xml** anger du en HTTPS-URL med den XML-fil som innehåller det korta namnet och URL:en till sökmotorn som minimikrav. Ange till exempel `https://www.contoso.com/opensearch.xml`.
- **Visa sökförslag**: **Ja** (standard) innebär att din sökmotor föreslår webbplatser när du skriver sökfraser i adressfältet. **Nej** förhindrar den här funktionen.
- **Tillåta ändringar av sökmotorn**: **Ja** (standard) tillåter användare att lägga till nya sökmotorer eller att ändra standardsökmotorn i Microsoft Edge. Välj **Nej** om du vill hindra användarna från att anpassa sökmotorn.

  Den här inställningen är endast tillgänglig med [normalläge (helskärmsläge för flera appar)](#use-microsoft-edge-kiosk-mode).

### <a name="privacy-and-security"></a>Sekretess och säkerhet

- **Tillåt InPrivate-surfning**: **Ja** (standard) tillåter InPrivate-surfning i Microsoft Edge. När alla InPrivate-flikar har stängts tar Microsoft Edge bort surfdata från enheten. **Nej** förhindrar att slutanvändarna öppnar InPrivate-surfningssessioner.
- **Spara webbhistorik**: **Ja** (standard) tillåter att surfhistoriken sparas i Microsoft Edge. **Nej** hindrar att surfhistoriken sparas.
- **Rensa webbdata vid avslut** (endast stationär dator): **Ja** rensar historik och webbdata när användaren avslutar Microsoft Edge. **Nej** (standard) använder operativsystemets standard, vilket kan innebära att webbdata cachelagras.
- **Synkronisera webbläsarens inställningar mellan användarens enheter**: Välj hur du vill synkronisera webbläsarinställningar mellan enheter. Alternativen är:
  - **Tillåt**: Tillåt synkronisering av Microsoft Edge-webbläsarinställningar mellan användarens enheter
  - **Blockera och aktivera åsidosättning av användaren**: Blockera synkronisering av Microsoft Edge-webbläsarinställningar mellan användarens enheter. Användarna kan åsidosätta den här inställningen.
  - **Blockera**: Blockerar synkronisering av Microsoft Edge-webbläsarinställningar mellan användarenheter. Användarna kan inte åsidosätta den här inställningen.

När ”Blockera och aktivera åsidosättning av användaren” är markerat kan användare åsidosätta admininställningen.

- **Tillåt lösenordshanteraren**: **Ja** (standard) tillåter Microsoft Edge att automatiskt använda lösenordshanteraren, som gör att användare kan spara och hantera lösenord på enheten. **Nej** hindrar Microsoft Edge från att använda lösenordshanteraren.
- **Cookies**: Välj hur cookies ska hanteras i webbläsaren. Alternativen är:
  - **Tillåt**: Cookies sparas på enheten.
  - **Blockera alla cookies**: Cookies sparas på enheten.
  - **Blockera endast cookies från tredje part**: Cookies från tredje part eller partner sparas inte på enheten.
- **Tillåt autofyll i formulär**: **Ja** (standard) tillåter användare att ändra inställningarna för Komplettera automatiskt i webbläsaren och fylla i formulärfält automatiskt. **Nej** inaktiverar funktionen Autofyll i Microsoft Edge.
- **Skicka Do Not Track-huvuden**: **Ja** skickar Do Not Track-huvuden till webbplatser som kräver spårningsinfo (rekommenderas). **Nej** (standard) skickar inte huvuden, vilket gör att webbplatser kan spåra användaren. Användaren kan konfigurera.
- **Visa localhost-IP-adress via WebRTC**: **Ja** (standard) tillåter att användarnas LocalHost-IP-adress visas vid telefonsamtal med detta protokoll. **Nej** förhindrar att användarnas localhost-IP-adress visas. 
- **Tillåt datainsamling för levande panel**: **Ja** (standard) tillåter Microsoft Edge att samla in information från Live-paneler som är fästa på Start-menyn. **Nej** förhindrar insamling av den här informationen, vilket kan ge användarna en begränsad funktion.
- **Användaren kan åsidosätta certifikatfel**: **Ja** (standard) tillåter användare att få åtkomst till webbplatser som har fel gällande Secure Sockets Layer/Transport Layer Security (SSL/TLS). **Nej** (rekommenderas för ökad säkerhet) förhindrar användare från att komma åt webbplatser med SSL- eller TLS-fel.

### <a name="additional"></a>Ytterligare

- **Tillåt Microsoft Edge-webbläsare** (endast mobil): **Ja** (standard) tillåter att Microsoft Edge-webbläsaren används på den mobila enheten. **Nej** förhindrar att Microsoft Edge används på enheten. Om du väljer **Nej** tillämpas de enskilda inställningarna endast på den stationära datorn.
- **Tillåt listruta i adressfältet**: **Ja** (standard) tillåter att Microsoft Edge visar en listruta i adressfältet med förslag. **Nej** hindrar Microsoft Edge från att visa en listruta med förslag när du skriver. När det här är inställt på **Nej** åstadkommer du följande:
  - Hjälper till att minimera nätverksbandbredden mellan Microsoft Edge och Microsoft-tjänster.
  - Inaktivera **Visa sök- och webbplatsförslag när jag skriver** i Microsoft Edge > Inställningar.
- **Tillåt helskärmsläge**: **Ja** (standard) tillåter Microsoft Edge att använda helskärmsläge, vilket endast visar webbinnehållet och döljer användargränssnittet i Microsoft Edge. **Nej** förhindrar helskärmsläge i Microsoft Edge.
- **Tillåt sidan about:flags**: **Ja** (standard) använder operativsystemets standardvärde, vilket kan tillåta åtkomst till sidan `about:flags`. Sidan `about:flags` gör att användare kan ändra inställningar för utvecklare och aktivera experimentella funktioner. **Nej** hindrar slutanvändare från att komma åt sidan `about:flags` i Microsoft Edge.
- **Tillåt utvecklarverktyg**: **Ja** (standard) tillåter användare att använda F12-utvecklarverktygen till att skapa och felsöka webbplatser som standard. **Nej** hindrar slutanvändare från att använda F12-utvecklarverktygen.
- **Tillåt JavaScript**: **Ja** (standard) Tillåter att skript, exempelvis JavaScript, körs i Microsoft Edge-webbläsaren. **Nej** förhindrar att Java-skript körs i webbläsaren.
- **Användaren kan installera tillägg**: **Ja** tillåter att slutanvändarna installerar Microsoft Edge-tillägg på enheten. **Nej** förhindrar installationen.
- **Tillåt separat inläsning av utvecklartillägg**: **Ja** (standard) använder operativsystemets standardvärde, vilket kan tillåta separat inläsning. Separat inläsning installerar och kör overifierade tillägg. **Nej** hindrar Microsoft Edge från att utföra separat inläsning med hjälp av funktionen **Läs in tillägg**. Det förhindrat inte separat inläsning av tillägg på andra sätt, till exempel via PowerShell.
- **Tillägg som krävs**: Välj vilka tillägg som inte ska kunna inaktiveras av slutanvändarna i Microsoft Edge. Ange paketfamiljenamnet och välj **Lägg till**. [Hitta ett paketfamiljenamn (PFN) för VPN per app](https://docs.microsoft.com/configmgr/protect/deploy-use/find-a-pfn-for-per-app-vpn) innehåller viss vägledning.

  Du kan också **Importera** en CSV-fil som innehåller paketfamiljenamnen. Eller så kan du **Exportera** paketfamiljenamn som du anger.

## <a name="network-proxy"></a>Nätverksproxy

De här inställningarna använder [CSP för NetworkProxy-princip](https://docs.microsoft.com/windows/client-management/mdm/networkproxy-csp), som även visar de Windows-versioner som stöds.

- **Identifiera proxyinställningar automatiskt**: **Blockera** hindrar enheten från att automatiskt identifiera ett PAC-skript (Proxy Auto Config). **Inte konfigurerat** (standard) aktiverar den här funktionen. När det här alternativet är aktiverat kommer enheten att försöka hitta sökvägen till ett PAC-skript.
- **Använd proxyskript**: Välj **Tillåt** för att ange en sökväg till ditt PAC-skript för att konfigurera proxyservern. **Inte konfigurerat** (standard) tillåter inte att du anger URL:en till ett PAC-skript.
  - **Ställ in webbadress till skript**: Ange webbadressen för ett PAC-skript som du vill använda för att konfigurera proxyservern.
- **Använd manuell proxyserver**: Välj **Tillåt** för att manuellt ange namn eller IP-adress samt TCP-portnummer för en proxyserver. **Inte konfigurerat** (standard) tillåter inte att du manuellt anger uppgifter för en proxyserver.
  - **Adress**: Ange namn eller IP-adress för proxyservern.
  - **Portnummer**: Ange portnumret till proxyservern.
  - **Proxyundantag**: Ange de webbadresser som inte får använda proxyservern. Använd semikolon för att avgränsa varje objekt.
  - **Använd ingen proxyserver för lokal adress**: **Inte konfigurerat** (standard) förhindrar användning av en proxyserver för lokala adresser på ditt intranät. **Tillåt** använder en proxyserver för lokala adresser.

## <a name="password"></a>lösenordsinställning

De här inställningarna använder [CSP för DeviceLock-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock), som även visar de Windows-versioner som stöds.

- **Lösenord**: Slutanvändaren **måste** ange ett lösenord för att få åtkomst till enheten. **Inte konfigurerat** (standard) tillåter åtkomst till enheten utan lösenord. Gäller endast för lokala konton. Lösenord för domänkonton förblir konfigurerade av Active Directory (AD) och Azure AD.

  - **Lösenordstyp som krävs**: Välj typ av lösenord. Alternativen är:
    - **Inte konfigurerad**: Lösenordet kan innehålla siffror och bokstäver.
    - **Numeriskt**: Lösenordet får bara innehålla siffror.
    - **Alfanumeriskt**: Lösenordet måste innehålla en blandning av siffror och bokstäver.
  - **Minsta lösenordslängd**: Ange det minsta antal siffror eller tecken som krävs från 4 till 16. Ange till exempel `6` för att kräva minst sex tecken i lösenordet.
  
    > [!IMPORTANT]
    > När lösenordskravet ändras på ett Windows-skrivbord påverkas användarna nästa gång de loggar in, eftersom det är då enheten går från inaktiv till aktiv. Användare med lösenord som uppfyller kravet uppmanas ändå att ändra sina lösenord.
    
  - **Antal felaktiga inloggningar innan enheten rensas**: Ange det antal autentiseringsfel som tillåts innan enheten kan rensas, upp till 11. Det giltiga tal som du anger beror på utgåvan. I [CSP för DeviceLock/MaxDevicePasswordFailedAttempts](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) anges de värden som stöds. `0` (noll) kan inaktivera funktionen för rensning av enheten.

    Den här inställningen har även olika effekt beroende på version. Specifik information om den här inställningen finns i [DeviceLock/MaxDevicePasswordFailedAttempts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts).

  - **Maximalt antal minuter av inaktivitet innan skärmen låses**: Anger hur lång tid en enhet måste vara inaktiv innan skärmen låses.
  - **Lösenordets giltighetstid (dagar)** : Ange det antal dagar efter vilket enhetens lösenord måste ändras, 1 till 365. Ange till exempel `90` om lösenordet ska upphöra efter 90 dagar.
  - **Förhindra återanvändning av tidigare lösenord**: Ange antal tidigare använda lösenord som inte får återanvändas, från 1–24. Ange till exempel `5` om användare inte ska kunna ange ett nytt lösenord till sina nuvarande lösenord eller något av de föregående fyra lösenorden.
  - **Kräv lösenord när enheten återgår från viloläge** (Mobile och Holographic): Välj **Kräv** så att användarna måste ange ett lösenord för att låsa upp enheten när den är inaktiv. **Inte konfigurerat** (standard) kräver inte PIN-kod eller lösenord när enheten återställs från inaktivt tillstånd.
  - **Enkla lösenord**: Ställ in på **Blockera** om du vill att användarna inte ska kunna skapa enkla lösenord, som `1234` eller `1111`. Ange till **Inte konfigurerat** (standard) om användarna ska kunna skapa lösenord som `1234` eller `1111`. Dessutom tillåter eller blockerar den här inställningen användningen av Windows-bildlösenord.
- **Automatisk kryptering under AADJ**: **Blockera** förhindrar automatisk BitLocker-enhetskryptering när enheten förbereds för första användning, när enheten är ansluten till Azure AD. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Mer om [BitLocker-enhetskryptering](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-device-encryption-overview-windows-10#bitlocker-device-encryption).

  [Security/PreventAutomaticDeviceEncryptionForAzureADJoinedDevices CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-security#security-preventautomaticdeviceencryptionforazureadjoineddevices)

- **Princip för FIPS-standard (Federal Information Processing Standard)** : **Tillåt** använder FIPS-principen (Federal Information Processing Standard), som är standarden för kryptering, hashing och signering för amerikanska myndigheter. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Standardinställningen för operativsystemet använder kanske inte FIPS.

  [Cryptography/AllowFipsAlgorithmPolicy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-cryptography#cryptography-allowfipsalgorithmpolicy)

- **Windows Hello-enhetsautentisering**: **Tillåt** att användare använder en Windows Hello-tillbehörsenhet, t.ex. en telefon, ett fitnessband eller en IoT-enhet, för att logga in på en Windows 10-dator. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Standardinställningen för operativsystemet kan förhindra att Windows Hello-tillbehörsenheter autentiseras med Windows.

  [Authentication/AllowSecondaryAuthenticationDevice CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowsecondaryauthenticationdevice)

- **Webbinloggning** (inaktuell): Aktiverar stöd för Windows-inloggning för providrar som inte är ADFS-federerade providrar (Active Directory Federation Services), till exempel SAML (Security Assertion Markup Language). SAML använder säkra token som ger möjlighet att använda enkel inloggning med webbläsare. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Aktiverad**: Providern för webbautentiseringsuppgifter är aktiverad för inloggning.
  - **Inaktiverad**: Providern för webbautentiseringsuppgifter är inaktiverad för inloggning.

  Den här inställningen tas bort i en kommande version. Använd inte den här inställningen.

  [Authentication/EnableWebSignIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-enablewebsignin)

- **Önskad domän för Azure AD-klientorganisation**: Ange ett befintligt domännamn i din Azure AD-organisation. När användare i den här domänen loggar in behöver de inte ange domännamnet. Ange till exempel `contoso.com`. Användare i domänen `contoso.com` kan logga in med sina användarnamn, till exempel `abby` i stället för `abby@contoso.com`.

  [Authentication/PreferredAadTenantDomainName CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-preferredaadtenantdomainname)

## <a name="per-app-privacy-exceptions"></a>Sekretessundantag per app

Du kan lägga till appar som ska ha en annan sekretess jämfört med vad du har definierat i ”Standardsekretess”.

- **Paketnamn**: Namne på appens paketfamilj.
- **Appnamn**: Namnet på appen.

### <a name="exceptions"></a>Undantag

- **Kontoinformation**: Definiera om den här appen kan komma åt användarnamn, bild och annan kontaktinformation.
- **Bakgrundsappar**: Definiera om den här appen kan köras i bakgrunden.
- **Kalender**: Definiera om den här appen kan komma åt kalendern.
- **Samtalshistorik**: Definiera om den här appen kan komma åt samtalshistoriken.
- **Kamera**: Definiera om den här appen kan komma åt kameran.
- **Kontakter**: Definiera om den här appen kan komma åt kontakter.
- **E-post**: Definiera om den här appen kan komma åt och skicka e-post.
- **Plats**: Definiera om den här appen kan komma åt platsinformation.
- **Meddelandefunktion**: Ange om den här appen kan läsa eller skicka SMS- och MMS-meddelanden.
- **Mikrofon**: Definiera om den här appen kan använda mikrofonen.
- **Rörelse**: Definiera om den här appen kan komma åt rörelseinformation.
- **Meddelanden**: Definiera om den här appen kan komma åt meddelanden.
- **Telefon**: Definiera om den här appen kan komma åt telefonen.
- **Radio**: Vissa appar kan använda radiofunktioner (t.ex. Bluetooth) i din enhet till att skicka och ta emot data. De behöver därför kunna sätta igång eller stänga av de här radiofunktionerna. Definiera om den här appen kan styra dessa radiofunktioner.
- **Uppgifter**: Definiera om den här appen kan komma åt dina uppgifter.
- **Betrodda enheter**: Välj om den här appen kan använda betrodda enheter. Betrodda enheter är maskinvara som du redan har anslutit eller som medföljer enheten. Du kan t.ex. använda tv-apparater, projektorer osv. som betrodda enheter.
- **Feedback och diagnostik**: Definiera om den här appen kan komma åt diagnostisk information.
- **Synkronisering med enheter**: Välj om den här appen automatiskt kan dela och synkronisera information med trådlösa enheter som inte uttryckligen kopplats ihop med enheten.

## <a name="personalization"></a>Anpassning

De här inställningarna använder [CSP för personanpassningsprincip](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp), som även visar de Windows-versioner som stöds.

- **URL för skrivbordsbakgrundsbild (endast stationär dator)** : Ange URL:en till en bild i formatet .jpg, .jpeg eller .png som du vill använda som skrivbordsbakgrund i Windows. Användare kan inte ändra bilden. Ange till exempel `https://contoso.com/logo.png`.

## <a name="printer"></a>Skrivare

- **Skrivare**: Lista över lokala skrivare som har lagts till.
- **Standardskrivare**: Ange standardskrivaren.
- **Användarbehörighet att lägga till nya skrivare**: Tillåt eller blockera användning av lokala skrivare.

## <a name="privacy"></a>Sekretess

De här inställningarna använder [CSP för sekretesspolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy), som även visar de Windows-versioner som stöds.

- **Anpassning av inmatning**: **Blockera** förhindrar användning av röst för diktering och för samtal med Cortana och andra appar som använder Microsofts molnbaserade röstigenkänning. Det är inaktiverat och användarna kan inte aktivera onlinebaserad taligenkänning via inställningarna. **Inte konfigurerat** (standard) låter användarna välja. Om du tillåter dessa tjänster kan det hända att Microsoft samlar in röstdata för att förbättra tjänsten.
- **Automatiskt godkännande av frågor om användarens medgivande till parkoppling och sekretess**: Välj **Tillåt** så att Windows automatiskt godkänner meddelanden om medgivande till parkoppling och sekretess när appar körs. **Inte konfigurerat** (standard) förhindrar automatiskt godkännande av fönstret med användarmedgivande för parkoppling och sekretess när appar öppnas.
- **Publicera användaraktiviteter**: **Blockera** förhindrar delad användning och identifiering av nyligen använda resurser i aktivitetsfeeden. **Inte konfigurerat** (standard) aktiverar den här funktionen så att appar kan publicera slutanvändaraktiviteter.
- **Endast lokala aktiviteter**: **Blockera** förhindrar delad användning och identifiering av nyligen använda resurser i aktivitetsväxlingen, enbart baserat på lokal aktivitet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

Du kan konfigurera den information som alla appar på enheten kan komma åt. Du kan också definiera undantag per app med hjälp av **Sekretessundantag per app**.

### <a name="exceptions"></a>Undantag

- **Kontoinformation**: Definiera om den här appen kan komma åt användarnamn, bild och annan kontaktinformation.
- **Bakgrundsappar**: Definiera om den här appen kan köras i bakgrunden.
- **Kalender**: Definiera om den här appen kan komma åt kalendern.
- **Samtalshistorik**: Definiera om den här appen kan komma åt samtalshistoriken.
- **Kamera**: Definiera om den här appen kan komma åt kameran.
- **Kontakter**: Definiera om den här appen kan komma åt kontakter.
- **E-post**: Definiera om den här appen kan komma åt och skicka e-post.
- **Plats**: Definiera om den här appen kan komma åt platsinformation.
- **Meddelandefunktion**: Ange om den här appen kan läsa eller skicka SMS- och MMS-meddelanden.
- **Mikrofon**: Definiera om den här appen kan använda mikrofonen.
- **Rörelse**: Definiera om den här appen kan komma åt rörelseinformation.
- **Meddelanden**: Definiera om den här appen kan komma åt meddelanden.
- **Telefon**: Definiera om den här appen kan komma åt telefonen.
- **Radio**: Vissa appar kan använda radiofunktioner (t.ex. Bluetooth) i din enhet till att skicka och ta emot data. De behöver därför kunna sätta igång eller stänga av de här radiofunktionerna. Definiera om den här appen kan styra dessa radiofunktioner.
- **Uppgifter**: Definiera om den här appen kan komma åt dina uppgifter.
- **Betrodda enheter**: Välj om den här appen kan använda betrodda enheter. Betrodda enheter är maskinvara som du redan har anslutit eller som medföljer enheten. Du kan t.ex. använda tv-apparater, projektorer osv. som betrodda enheter.
- **Feedback och diagnostik**: Välj om den här appen ska komma åt diagnostisk information.
- **Synkronisering med enheter** – Definiera om den här appen automatiskt kan dela och synkronisera information med trådlösa enheter som inte uttryckligen kopplats ihop med den här datorn, surfplattan eller telefonen.

## <a name="projection"></a>Projektion

De här inställningarna använder [CSP för WirelessDisplay-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay), som även visar de Windows-versioner som stöds.

- **Användarindata från trådlösa visningsmottagare**: **Blockera** hindrar användarindata från trådlösa visningsmottagare. **Inte konfigurerat** (standard) tillåter att en trådlös display skickar indata från tangentbord, mus, penna och pekfunktion tillbaka till källenheten.
- **Projektion till den här datorn**: **Blockera** hindrar andra enheter från att hitta enheten för projektion. **Inte konfigurerat** (standard) tillåter att enheten kan identifieras och projicera till enheten ovanför låsskärmen.
- **Kräv en PIN-kod för parkoppling**: Välj **Kräv** för att alltid fråga efter en PIN-kod vid anslutning till en projektionsenhet. **Inte konfigurerat** (standard) kräver inte någon PIN-kod för att enheten ska parkopplas till en projektionsenhet.

## <a name="reporting-and-telemetry"></a>Rapportering och telemetri

- **Dela användningsdata**: Välj nivå av diagnostikdata som skickas. Alternativen är:
  - **Inte konfigurerad**: Inga data delas.
  - **Säkerhet**: Information som krävs för att hålla Windows säkrare, däribland data om inställningar för komponenten Enhetlig användarupplevelse och telemetri, Borttagning av skadlig programvara samt Microsoft Defender.
  - **Grundläggande**: Grundläggande enhetsinformation såsom kvalitetsrelaterade data, appkompatibilitet, appanvändningsdata och data från nivån Säkerhet.
  - **Förbättrad**: Ytterligare information som omfattar: hur Windows, Windows Server, System Center och appar används, hur de presterar, avancerade tillförlitlighetsdata samt data från både nivåerna Grundläggande och Säkerhet.
  - **Fullständig**: Alla data som behövs för att identifiera och bidra till att lösa problem, plus data från nivåerna Säkerhet, Grundläggande och Förbättrad.

  [CSP för System/AllowTelemetry](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

- **Skicka Microsoft Edge-webbdata till Microsoft 365 Analytics**: Om du vill använda denna funktion kan du ange inställningar för **Dela användningsdata** till **Utökad** eller **Fullständig**. Den här funktionen styr vilka data Microsoft Edge skickar till Microsoft 365 Analytics för Enterprise-enheter med ett konfigurerat kommersiellt ID. Alternativen är:
  - **Inte konfigurerad**: Intune varken ändrar eller uppdaterar den här inställningen. Standardinställningen för operativsystemet skickar kanske inte webbhistorik.
  - **Skicka endast data för intranät**: Låter administratören skicka historik för intranät
  - **Skicka endast data för Internet**: Låter administratören skicka historik för Internet
  - **Skicka endast data för Internet**: Låter administratören skicka historik för Internet

  [CSP för Browser/ConfigureTelemetryForMicrosoft365Analytics](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configuretelemetryformicrosoft365analytics)

- **Telemetriproxyserver**: Ange det fullständiga domännamnet (FQDN) eller IP-adressen för en proxyserver för att vidarebefordra anslutna användarupplevelser och telemetribegäranden som använder en SSL-anslutning (Secure Sockets Layer). Formatet för den här inställningen är *server*:*port*. Om den namngivna proxyn misslyckas, eller om det inte finns någon proxy angiven när den här principen aktiveras, överförs inte de anslutna användarupplevelserna och telemetridata, utan de finns kvar på den lokala enheten.

  Exempelformat:

  ```
  IPv4: 192.246.246.106:100
  IPv6: [2001:4898:4010:4013:95c1:a8b2:953c:c633]:100
  FQDN: www.contoso.com:345
  ```

  [CSP för System/TelemetryProxy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-telemetryproxy)

Klicka på **OK** för att spara ändringarna.

## <a name="search"></a>Sök

De här inställningarna använder [CSP för sökpolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search), som även visar de Windows-versioner som stöds. 

- **Säker sökning (endast mobil)** : Styr hur Cortana filtrerar innehåll för vuxna i sökresultaten. Alternativen är:
  - **Användardefinierad**: Tillåter att slutanvändare väljer sina egna inställningar.
  - **Strikt**: Högsta filtrering mot vuxet innehåll.
  - **Måttlig**: Måttlig filtrering mot vuxet innehåll. Giltiga sökresultat filtreras inte.
- **Visa webbresultat i sökning**: När det här anges till **Blockera** kan användare inte söka, och webbresultat visas inte i sökning. **Inte konfigurerat** (standard) tillåter användare att söka på webben, och resultaten visas på enheten.

## <a name="start"></a>Start

De här inställningarna använder [CSP för startpolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start), som även visar de Windows-versioner som stöds.  

- **Layout för Start-menyn**: Åsidosätt standardlayouten för Start-menyn och anpassa Start-menyn på skrivbordsenheter. Ladda upp en XML-fil som innehåller dina anpassningar, inklusive den ordning som apparna visas i listan och mer. Användarna kan inte ändra den layout för Start-menyn som du anger.
- **Fäst webbplatser på paneler i Start-menyn**: Importera bilder från Microsoft Edge som visas som länkar i Windows Start-menyn för stationära enheter.
- **Ta bort appar från aktivitetsfältet**: **Blockera** förhindrar användare från att ta bort appar från aktivitetsfältet. **Inte konfigurerat** (standard) tillåter användare att ta bort appar från aktivitetsfältet.
- **Snabbt användarbyte**: **Blockera** förhindrar växling mellan användare som är inloggade samtidigt utan utloggning. **Inte konfigurerat** (standard) visar **Växla användare** på användarpanelen.
- **Appar som används oftast**: **Blockera** döljer de appar som oftast används från att visas på Start-menyn. Detta inaktiverar även motsvarande reglage i appen Inställningar. **Inte konfigurerat** (standard) visar de mest använda apparna.
- **Nyligen tillagda appar**: **Blockera** döljer nyligen tillagda appar från att visas på Start-menyn. Detta inaktiverar även motsvarande reglage i appen Inställningar. **Inte konfigurerat** (standard) visar nyligen tillagda appar på Start-menyn.
- **Starta skärmläge**: Välj hur Start-skärmen ska visas. Alternativen är:
  - **Användardefinierad**: Framtvingar inte storleken på Start. Användare kan ange storleken.
  - **Helskärm**: Framtvingar helskärmsstorlek på Start.
  - **Inte helskärm**: Framtvingar storlek som inte är helskärm på Start.
- **Nyligen öppnade objekt i snabblistor**: **Blockera** döljer de senaste snabblistorna från att visas på Start-menyn och i aktivitetsfältet. Detta inaktiverar även motsvarande reglage i appen Inställningar. **Inte konfigurerat** (standard) visar senast öppnade objekt i snabblistorna.
- **Applista**: Välj hur listorna med alla appar visas. Alternativen är:
  - **Användardefinierad**: Ingen inställning framtvingas. Användare väljer du applistan visas på enheten.
  - **Dölj**: Dölj listan med alla appar.
  - **Dölj och inaktivera appen Inställningar**: Dölj listan med alla appar och inaktivera **Visa applistan på Start-menyn** i appen Inställningar.
  - **Döljer och inaktiverar appen Inställningar**: Dölj listan med alla appar, ta bort knappen för alla appar och inaktivera **Visa applistan på Start-menyn** i appen Inställningar.
- **Strömknapp**: **Blockera** döljer strömknappen från att visas på Start-menyn. **Inte konfigurerat** (standard) visar strömknappen.
- **Användarpanel**: **Blockera** döljer användarpanelen så att den inte visas på Start-menyn. **Inte konfigurerat** (standard) visar användarpanelen och anger även följande inställningar:
  - **Lås**: **Blockera** döljer alternativet **Lås** från att visas i användarpanelen på Start-menyn. **Inte konfigurerat** (standard) visar alternativet **Lås**.
  - **Logga ut**: **Blockera** döljer alternativet **Logga ut** från att visas i användarpanelen på Start-menyn. **Inte konfigurerat** (standard) visar alternativet **Logga ut**.
- **Stäng av**: **Blockera** döljer alternativen **Uppdatera och stäng av** och **Stäng av** från att visas i strömknappen på Start-menyn. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Viloläge**: **Blockera** döljer alternativet **Strömsparläge** från att visas i strömknappen på Start-menyn. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Viloläge**: **Blockera** döljer alternativet **Viloläge** från att visas i strömknappen på Start-menyn. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Växla konto**: **Blockera** döljer **Växla konto** från att visas i användarpanelen på Start-menyn. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Omstartsalternativ**:  **Blockera** döljer alternativen **Uppdatera och starta om** och **Starta om** från att visas i strömknappen på Start-menyn. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Dokument på Start**: Dölj eller visa mappen Dokument i Start-menyn i Windows. Alternativen är:
  - **Inte konfigurerat** (standard): Ingen inställning framtvingas. Användare väljer att visa eller dölja genvägen.
  - **Dölj**: Genvägen döljs, och inställningen inaktiveras i appen Inställningar.
  - **Visa**: Genvägen visas, och inställningen inaktiveras i appen Inställningar.
- **Nedladdningar på Start**: Dölj eller visa mappen Nedladdningar i Start-menyn i Windows. Alternativen är:
  - **Inte konfigurerat** (standard): Ingen inställning framtvingas. Användare väljer att visa eller dölja genvägen.
  - **Dölj**: Genvägen döljs, och inställningen inaktiveras i appen Inställningar.
  - **Visa**: Genvägen visas, och inställningen inaktiveras i appen Inställningar.
- **Utforskaren på Start**: Dölj eller visa Utforskaren på Start-menyn i Windows. Alternativen är:
  - **Inte konfigurerat** (standard): Ingen inställning framtvingas. Användare väljer att visa eller dölja genvägen.
  - **Dölj**: Genvägen döljs, och inställningen inaktiveras i appen Inställningar.
  - **Visa**: Genvägen visas, och inställningen inaktiveras i appen Inställningar.
- **Hemgrupp på Start**: Dölj eller visa genvägen till Hemgrupp på Start-menyn i Windows. Alternativen är:
  - **Inte konfigurerat** (standard): Ingen inställning framtvingas. Användare väljer att visa eller dölja genvägen.
  - **Dölj**: Genvägen döljs, och inställningen inaktiveras i appen Inställningar.
  - **Visa**: Genvägen visas, och inställningen inaktiveras i appen Inställningar.
- **Musik på Start**: Dölj eller visa mappen Musik i Start-menyn i Windows. Alternativen är:
  - **Inte konfigurerat** (standard): Ingen inställning framtvingas. Användare väljer att visa eller dölja genvägen.
  - **Dölj**: Genvägen döljs, och inställningen inaktiveras i appen Inställningar.
  - **Visa**: Genvägen visas, och inställningen inaktiveras i appen Inställningar.
- **Nätverk på Start**: Dölj eller visa Nätverk på Start-menyn i Windows. Alternativen är:
  - **Inte konfigurerat** (standard): Ingen inställning framtvingas. Användare väljer att visa eller dölja genvägen.
  - **Dölj**: Genvägen döljs, och inställningen inaktiveras i appen Inställningar.
  - **Visa**: Genvägen visas, och inställningen inaktiveras i appen Inställningar.
- **Personlig mapp på Start**: Dölj eller visa den personliga mappen i Start-menyn i Windows. Alternativen är:
  - **Inte konfigurerat** (standard): Ingen inställning framtvingas. Användare väljer att visa eller dölja genvägen.
  - **Dölj**: Genvägen döljs, och inställningen inaktiveras i appen Inställningar.
  - **Visa**: Genvägen visas, och inställningen inaktiveras i appen Inställningar.
- **Bilder på Start**: Dölj eller visa mappen för bilder i Start-menyn i Windows. Alternativen är:
  - **Inte konfigurerat** (standard): Ingen inställning framtvingas. Användare väljer att visa eller dölja genvägen.
  - **Dölj**: Genvägen döljs, och inställningen inaktiveras i appen Inställningar.
  - **Visa**: Genvägen visas, och inställningen inaktiveras i appen Inställningar.
- **Inställningar på Start**: Dölj eller visa genvägen till Inställningar på Start-menyn i Windows. Alternativen är:
  - **Inte konfigurerat** (standard): Ingen inställning framtvingas. Användare väljer att visa eller dölja genvägen.
  - **Dölj**: Genvägen döljs, och inställningen inaktiveras i appen Inställningar.
  - **Visa**: Genvägen visas, och inställningen inaktiveras i appen Inställningar.
- **Videor på Start**: Dölj eller visa mappen för videor i Start-menyn i Windows. Alternativen är:
  - **Inte konfigurerat** (standard): Ingen inställning framtvingas. Användare väljer att visa eller dölja genvägen.
  - **Dölj**: Genvägen döljs, och inställningen inaktiveras i appen Inställningar.
  - **Visa**: Genvägen visas, och inställningen inaktiveras i appen Inställningar.

## <a name="microsoft-defender-smart-screen"></a>Microsoft Defender SmartScreen

- **SmartScreen för Microsoft Edge**: **Kräv** inaktiverar Microsoft Defender SmartScreen och hindrar användarna från att aktivera funktionen. **Inte konfigurerat** (standard) aktiverar SmartScreen. Hjälper till att skydda användarna mot potentiella hot och hindrar användare från att stänga av den.

  Microsoft Edge använder Microsoft Defender SmartScreen (aktiverat) för att skydda användarna mot potentiella nätfiskeförsök och skadlig programvara.

  [CSP för Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Åtkomst till skadlig webbplats**: **Blockera** hindrar användarna från att ignorera varningarna från Microsoft Defender SmartScreen-filtret och blockerar dem från att gå till webbplatsen. **Inte konfigurerat** (standard) tillåter användare att ignorera varningarna och fortsätta till webbplatsen.

  [CSP för Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Overifierad filhämtning**: **Blockera** hindrar användarna från att ignorera varningarna från Microsoft Defender SmartScreen-filtret och blockerar dem från att hämta overifierade filer. **Inte konfigurerat** (standard) tillåter användare att ignorera varningarna och fortsätta ladda ned de overifierade filerna.

  [CSP för Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

## <a name="windows-spotlight"></a>Windows Spotlight

De här inställningarna använder [CSP för upplevelseprincip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience), som även visar de Windows-versioner som stöds.

- **Windows Spotlight**: **Blockera** inaktiverar Windows Spotlight på låsskärmen, Windows-tips, Microsoft-konsumentfunktioner och liknande funktioner. Om målet är att minimera nätverkstrafik från enheter anger du det här till **Blockera**. **Inte konfigurerat** (standard) tillåter Windows Spotlight-funktioner och kan styras av slutanvändare. När det här är aktiverat kan du även tillåta eller blockera följande inställningar:

  - **Windows Spotlight på låsskärm**: **Blockera** hindrar Windows Spotlight från att visa information på enhetens låsskärm. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
  - **Tredjepartsförslag i Windows Spotlight**: **Blockera** hindrar Windows Spotlight från att föreslå innehåll som inte har publicerats av Microsoft. **Inte konfigurerat** (standard) tillåter app- och innehållsförslag från partnerutgivare av programvara i Windows Spotlight-funktioner, till exempel låsskärmen, föreslagna appar på Start-menyn och Windows-tips.
  - **Konsumentfunktioner**: **Blockera** stänger av funktioner som vanligtvis endast är till för konsumenter, till exempel startförslag, medlemskapsaviseringar, appinstallation efter välkomstprogram (OOBE) och omdirigeringspaneler. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
  - **Windows-tips**: **Blockera** inaktiverar popup-Windows-tips. **Inte konfigurerat** (standard) tillåter att popup-Windows-tips visas.
  - **Windows Spotlight i Åtgärdscenter**: **Blockera** hindrar att Windows Spotlight-meddelanden visas i Åtgärdscenter. **Inte konfigurerat** (standard) kan visa meddelanden i Åtgärdscenter som föreslår appar eller funktioner som hjälper användarna att bli mer produktiva i Windows.
  - **Windows Spotlight-anpassning**: **Blockera** hindrar Windows från att använda diagnostikdata till att ge användaren anpassade funktioner. **Inte konfigurerat** (standard) tillåter att Microsoft använder diagnostikdata för att ge anpassade rekommendationer, tips och erbjudanden om att skräddarsy Windows för användarens behov.
  - **Välkommen till Windows-skärm**: **Blockera** stänger av funktionen för välkomst till Windows i Windows Spotlight. Välkommen till Windows-skärm visas inte när det finns uppdateringar och ändringar av Windows och dess program. **Inte konfigurerat** (standard) tillåter Välkommen till Windows-skärmen, där användarinformation om nya eller uppdaterade funktioner visas.

## <a name="microsoft-defender-antivirus"></a>Microsoft Defender Antivirus

De här inställningarna använder [CSP för Defender-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender), som även visar de Windows-versioner som stöds.

- **Realtidsövervakning**: **Aktivera** aktiverar genomsökning i realtid efter skadlig programvara, spionprogram och annan oönskad programvara. Användaren kan inte inaktivera den här inställningen. 

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du aktiverar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare konfigurerade tillstånd. Som standard aktiverar operativsystemet den här funktionen och tillåter att användare ändrar den.

  Intune stänger inte av den här funktionen. Om du vill inaktivera den använder du en anpassad URI.

  [CSP för Defender/AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

- **Beteendeövervakning** **Aktivera** aktiverar övervakning av funktionssätt och söker efter kända tecken på misstänkt aktivitet på enheter. Användare kan inte stänga av beteendeövervakning. 

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du aktiverar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare konfigurerade tillstånd. Som standard aktiverar operativsystemet beteendeövervakning och tillåter att användare ändrar den.

  Intune stänger inte av den här funktionen. Om du vill inaktivera den använder du en anpassad URI.

  [CSP för Defender/AllowBehaviorMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **NIS (Network Inspection System)** : NIS hjälper till att skydda enheter mot nätverksbaserade säkerhetsrisker. Det använder signaturer för kända problem från Microsoft Endpoint Protection Center för att identifiera och blockera skadlig trafik.

  **Aktivera** aktiverar nätverksskydd och nätverksblockering. Användaren kan inte inaktivera den här inställningen. När detta är aktiverat blockeras användarna från att ansluta till kända sårbarheter.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du aktiverar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare konfigurerade tillstånd. Som standard aktiverar operativsystemet NIS och tillåter att användare ändrar det.

  Intune stänger inte av den här funktionen. Om du vill inaktivera den använder du en anpassad URI.

  [CSP för Defender/EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Sök igenom alla hämtningar**: **Aktivera** aktiverar den här inställningen, och Defender genomsöker alla filer som laddas ned från Internet. Användarna kan inte inaktivera den här inställningen. 

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du aktiverar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare konfigurerade tillstånd. Som standard aktiverar operativsystemet den här inställningen och tillåter att användare ändrar den.

  Intune stänger inte av den här funktionen. Om du vill inaktivera den använder du en anpassad URI.

  [CSP för Defender/AllowIOAVProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

- **Sök igenom skript som har lästs in via Microsoft-webbläsare**: **Aktivera** gör att Defender genomsöker skript som används i Internet Explorer. Användarna kan inte inaktivera den här inställningen. 

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du aktiverar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare konfigurerade tillstånd. Som standard aktiverar operativsystemet den här inställningen och tillåter att användare ändrar den.

  Intune stänger inte av den här funktionen. Om du vill inaktivera den använder du en anpassad URI.

  [CSP för Defender/AllowScriptScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **Användaråtkomst till Defender**: **Blockera** döljer Microsoft Defender-användargränssnittet för slutanvändarna. Alla Microsoft Defender-meddelanden döljs också.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du blockerar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare konfigurerade tillstånd. Som standard tillåter operativsystemet användare att komma åt och ändra användargränssnittet i Microsoft Defender.

  Intune stänger inte av den här funktionen. Om du vill inaktivera den använder du en anpassad URI.

  När den här inställningen ändras börjar den gälla nästa gång användarens dator startas om.

  [CSP för Defender/AllowUserUIAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **Intervall för uppdatering av säkerhetsinsikter (i timmar)** : Ange det intervall som Defender använder för att söka efter ny säkerhetsinformation, 0 till 24. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Standardvärdet för operativsystemet kan söka efter uppdateringar var 8:e timme.
  - **Kontrollera inte**: Defender söker inte efter nya uppdateringar av säkerhetsinformation.
  - **1–24**: `1` kontrollerar varje timme, `2` kontrollerar varannan timme, `24` kontrollerar varje dag och så vidare.
  
  [CSP för Defender/SignatureUpdateInterval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)
  
- **Övervaka fil- och programaktivitet**: Tillåter att Defender övervakar fil- och programaktivitet på enheter. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Standardinställningen för operativsystemet kan övervaka alla filer.
  - **Övervakning har inaktiverats**
  - **Övervaka alla filer**
  - **Övervaka enbart inkommande filer**
  - **Övervaka enbart utgående filer**

  [CSP för Defender/RealTimeScanDirection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

- **Dagar innan skadlig kod i karantän tas bort**: Fortsätt att spåra åtgärdad skadlig kod i det antal dagar du anger, så att du manuellt kan kontrollera tidigare berörda enheter. Om du anger antalet dagar till `0`, hålls skadlig programvara kvar i karantänmappen och tas inte bort automatiskt. När det här är inställt på `90` lagras karantänobjekt i 90 dagar i systemet och tas sedan bort.

  [CSP för Defender/DaysToRetainCleanedMalware](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **Gräns för processoranvändning under genomsökning**: Låter dig begränsa hur mycket processorkraft som genomsökningar får använda (från `0` till `100`).
- **Sök igenom arkivfiler**: **Aktivera** aktiverar Defender så att det söker igenom arkivfiler, till exempel ZIP- eller CAB-filer. Användarna kan inte inaktivera den här inställningen.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du aktiverar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare konfigurerade tillstånd. Som standard aktiverar operativsystemet den här genomsökningen och tillåter att användare ändrar den.

  Intune stänger inte av den här funktionen. Om du vill inaktivera den använder du en anpassad URI.

  [CSP för Defender/AllowArchiveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **Sök igenom inkommande e-postmeddelanden**: **Aktivera** tillåter att Defender söker igenom e-postmeddelanden när de tas emot på enheten. När detta aktiveras parsar motorn postlådan och e-postfilerna för att analysera e-postmeddelandets brödtext och bifogade filer. Du kan genomsöka formaten .pst (Outlook), .dbx, .mbx, MIME (Outlook Express), och BinHex (Mac).

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du aktiverar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare konfigurerade tillstånd. Som standard inaktiverar operativsystemet den här genomsökningen och tillåter att användare ändrar den.

  Intune stänger inte av den här funktionen. Om du vill inaktivera den använder du en anpassad URI.

  [CSP för Defender/AllowEmailScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **Sök igenom flyttbara drivrutiner vid fullständig genomsökning**: **Aktivera** aktiverar Defender-genomsökningar av flyttbara enheter under en fullständig genomsökning. Användarna kan inte inaktivera den här inställningen.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du aktiverar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare konfigurerade tillstånd. Som standard tillåter operativsystemet Defender att genomsöka flyttbara enheter, till exempel USB-minnen, och gör att användarna kan ändra den här inställningen.

  Under en snabb genomsökning kan flyttbara enheter fortfarande genomsökas.

  Intune stänger inte av den här funktionen. Om du vill inaktivera den använder du en anpassad URI.

  [CSP för Defender/AllowFullScanRemovableDriveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

- **Sök igenom mappade nätverksdrivrutiner vid fullständig genomsökning**: **Aktivera** gör att Defender genomsöker filer på mappade nätverksenheter. Om filerna på enheten är skrivskyddade kan Defender inte ta bort eventuell skadlig kod i dem. Användarna kan inte inaktivera den här inställningen.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du aktiverar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare konfigurerade tillstånd. Som standard aktiverar operativsystemet den här funktionen och tillåter att användare ändrar den.

  Under en snabb genomsökning kan mappade nätverksenheter fortfarande genomsökas.

  Intune stänger inte av den här funktionen. Om du vill inaktivera den använder du en anpassad URI.

  [CSP för Defender/AllowFullScanOnMappedNetworkDrives](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **Sök igenom filer öppnade från nätverksmappar**: **Aktivera** gör att Defender genomsöker filer som öppnats från nätverksmappar eller delade nätverksenheter, till exempel filer som nås via en UNC-sökväg. Användarna kan inte inaktivera den här inställningen. Om filerna på enheten är skrivskyddade kan Defender inte ta bort eventuell skadlig kod i dem.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du aktiverar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare konfigurerade tillstånd. Som standard genomsöker operativsystemet filer som öppnats från nätverksmappar och tillåter att användare ändrar den.

  Intune stänger inte av den här funktionen. Om du vill inaktivera den använder du en anpassad URI.

  [CSP för Defender/AllowScanningNetworkFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **Molnskydd**: **Aktivera** aktiverar Microsoft Active Protection Service, som samlar in information om aktivitet relaterad till skadlig kod från enheter som du hanterar. Användarna kan inte ändra denna inställning. 

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du aktiverar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare konfigurerade tillstånd. Som standard tillåter operativsystemet att Microsoft Active Protection Service tar emot information och att användarna ändrar den här inställningen.

  Intune stänger inte av den här funktionen. Om du vill inaktivera den använder du en anpassad URI.

  [CSP för Defender/AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

- **Be användarna att skicka exempel**: Anger om potentiellt skadliga filer som kan kräva ytterligare analys ska skickas automatiskt till Microsoft. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen. Standardvärdet för operativsystemet kan skicka säkra exempel automatiskt.
  - **Fråga alltid**
  - **Fråga innan personlig information skickas**
  - **Skicka aldrig data**
  - **Skicka alla data utan att fråga**: Data skickas automatiskt.

  [CSP för Defender/SubmitSamplesConsent](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

- **Tidpunkt för daglig snabbsökning**: Välj vilken timme en daglig snabbsökning ska köras. **Inte konfigurerad** kör ingen daglig genomsökning. Om du vill göra fler anpassningar konfigurerar du inställningen **Typ av systemgenomsökning som ska utföras**.

  [Defender/ScheduleQuickScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

- **Typ av systemgenomsökning som ska utföras**: Schemalägg en systemgenomsökning, inklusive genomsökningsnivå och dag och tid då genomsökningen ska köras. Alternativen är:
  - **Inte konfigurerad**: Schemalägger inte en systemgenomsökning på enheten. Slutanvändarna kan manuellt köra genomsökningar efter behov och önskemål på sina enheter.
  - **Inaktivera**: Inaktiverar alla systemgenomsökningar på enheten. Välj det här alternativet om du använder en virusskyddslösning från tredje part som söker igenom enheter.
  - **Snabbsökning**: Söker på vanliga platser där det kan finnas skadlig kod, till exempel registernycklar och kända startmappar i Windows.
    - **Schemalagd dag**: Välj vilken dag genomsökningen ska köras.
    - **Schemalagd tid**: Välj vilken timme genomsökningen ska köras.
  - **Fullständig genomsökning**: Letar på vanliga platser där det kan finnas skadlig kod och söker också igenom alla filer och mappar på enheten.
    - **Schemalagd dag**: Välj vilken dag genomsökningen ska köras.
    - **Schemalagd tid**: Välj vilken timme genomsökningen ska köras.

  > [!TIP]
  > Den här inställningen kan orsaka en konflikt med inställningen **Tidpunkt för daglig snabbsökning**. Några rekommendationer:  
  >
  > - Om du vill schemalägga en daglig snabb genomsökning och en veckovis fullständig genomsökning gör du följande:
  >   1. Konfigurera inställningen **Tidpunkt för daglig snabbsökning**.
  >   2. Konfigurera **Typ av systemgenomsökning som ska utföras** till en fullständig genomsökning.
  > 
  > - Om du bara vill ha en snabb genomsökning dagligen (ingen fullständig genomsökning) använder du antingen inställningen **Tidpunkt för daglig snabbsökning** eller **Typ av systemgenomsökning som ska utföras**. Om du till exempel vill köra en snabbgenomsökning varje tisdag 06:00 konfigurerar du inställningen **Typ av systemgenomsökning som ska utföras**.
  > 
  > - Konfigurera inte inställningen **Tidpunkt för daglig snabbsökning** samtidigt som **Typ av systemgenomsökning som ska utföras** är inställd på **Snabbsökning**. Dessa inställningar kan orsaka en konflikt och genomsökningen kanske inte körs.

  [Defender/ScanParameter CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)  
  [Defender/ScheduleScanDay CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)  
  [Defender/ScheduleScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime)

- **Identifiera potentiellt oönskade program**: Välj nivå av skydd när Windows identifierar potentiellt oönskade program. Alternativen är:
  - **Inte konfigurerat** (standard): Skydd mot potentiellt oönskade program för Microsoft Defender inaktiveras.
  - **Blockera**: Microsoft Defender identifierar potentiellt oönskade program och blockerar identifierade objekt. Dessa objekt visas i historiken tillsammans med andra hot.
  - **Granska**: Microsoft Defender identifierar potentiellt oönskade program men vidtar inga åtgärder. Du kan granska information om det program som Microsoft Defender skulle vidta åtgärder mot. Till exempel kan du söka efter händelser som skapats av Microsoft Defender i Loggboken.

  Mer information om potentiellt oönskade appar finns i [Identifiera och blockera potentiellt oönskade program](https://docs.microsoft.com/windows/threat-protection/windows-defender-antivirus/detect-block-potentially-unwanted-apps-windows-defender-antivirus).

  [CSP för Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **Medgivande till att skicka stickprov**: För närvarande har den här inställningen ingen inverkan. Använd inte den här inställningen. Det kan tas bort i en framtida version.

- **Kontinuerligt skydd**: **Blockera** förhindrar genomsökning av filer som har öppnats eller laddats ned. Användare kan inte aktivera det.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Om du blockerar inställningen och sedan ändrar tillbaka den till **Inte konfigurerad** låter Intune inställningen vara kvar i dess tidigare OS-konfigurerade tillstånd. Som standard aktiverar operativsystemet den här funktionen och tillåter att användare ändrar den.

  Intune aktiverar inte den här funktionen. Om du vill aktivera den använder du en anpassad URI.

  [CSP för Defender/AllowOnAccessProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **Åtgärder vid hot om identifierad skadlig kod**: Välj hur du vill hantera hot från skadlig kod. **Inte konfigurerad** (standard) låter Microsoft Defender välja det bästa alternativet. När alternativet ställs in på **Aktivera**, väljer du vilka åtgärder du vill att Defender ska vidta för varje hotnivå den identifierar: låg, måttlig, hög och allvarlig. Alternativen är:
  
  - **Rensa**
  - **Karantän**
  - **Ta bort**
  - **Tillåt**
  - **Användardefinierad**
  - **Blockera**

  Om din åtgärd inte är möjlig väljer Windows Defender det bästa alternativet för att oskadliggöra hotet. 

  [CSP för Defender/ThreatSeverityDefaultAction](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

### <a name="microsoft-defender-antivirus-exclusions"></a>Microsoft Defender antivirusundantag

- **Filer och mappar som ska undantas från genomsökningar och realtidsskydd**: Lägger till en eller flera filer och mappar som **C:\Sökväg** eller **%ProgramFiles%\Sökväg\filnamn.exe** i undantagslistan. Dessa filer och mappar tas inte med i realtidsgenomsökningar eller schemalagda genomsökningar.
- **Filnamnstillägg som ska undantas från genomsökningar och realtidsskydd**: Lägg till ett eller flera filnamnstillägg som **jpg** eller **txt** i undantagslistan. Filer med dessa filnamnstillägg tas inte med i realtidsgenomsökningar eller schemalagda genomsökningar.
- **Processer som ska undantas från genomsökningar och realtidsskydd**: Lägg till en eller flera processer av typen **.exe**, **.com** eller **.scr** i undantagslistan. Dessa processer tas inte med i realtidsgenomsökningar eller schemalagda genomsökningar.

## <a name="power-settings"></a>Energiinställningar

### <a name="battery"></a>Batteri

- **Batterinivå för aktivering av energisparläge**: Ange den laddningsnivå för batteriet då energisparläge ska aktiveras, 0 till 100, när enheten använder batteridrift. Ange ett procentvärde som anger batteriets laddningsnivå. Standardvärdet är 70 %. När detta anges 70 % aktiveras energisparläge när batteriet har 70 % eller mindre laddning.

  [CSP för Power/EnergySaverBatteryThresholdOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdonbattery)

- **Stängning av lock (endast mobil)** : Välj vad som ska hända när enheten använder batteridrift och locket stängs. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Ingen åtgärd**: Enheten förblir aktiverad och fortsätter att använda batteridrift.
  - **Viloläge**: Enheten försätts i strömsparläge och använder en liten mängd batteriladdning. Datorn förblir på, och öppnade appar och filer lagras i RAM (Random Access Memory).
  - **Viloläge**: Enheten försätts i viloläge. Öppnade appar och filer lagras på hårddisken, och enheten stängs av.
  - **Stäng av**: Enheten stängs av. Öppnade appar och filer stängs utan att sparas.

  [CSP för Power/SelectLidCloseActionOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactiononbattery)

- **Strömknapp**: Välj vad som ska hända när enheten använder batteridrift och strömknappen väljs. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Ingen åtgärd**: Enheten förblir aktiverad och fortsätter att använda batteridrift.
  - **Viloläge**: Enheten försätts i strömsparläge och använder en liten mängd batteriladdning. Datorn förblir på, och öppnade appar och filer lagras i RAM (Random Access Memory).
  - **Viloläge**: Enheten försätts i viloläge. Öppnade appar och filer lagras på hårddisken, och enheten stängs av.
  - **Stäng av**: Enheten stängs av. Öppnade appar och filer stängs utan att sparas.

  [CSP för Power/SelectPowerButtonActionOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactiononbattery)

- **Vila**: Välj vad som ska hända när enheten använder batteridrift och knappen Strömsparläge väljs. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Ingen åtgärd**: Enheten förblir aktiverad och fortsätter att använda batteridrift.
  - **Viloläge**: Enheten försätts i strömsparläge och använder en liten mängd batteriladdning. Datorn förblir på, och öppnade appar och filer lagras i RAM (Random Access Memory).
  - **Viloläge**: Enheten försätts i viloläge. Öppnade appar och filer lagras på hårddisken, och enheten stängs av.
  - **Stäng av**: Enheten stängs av. Öppnade appar och filer stängs utan att sparas.

  [CSP för Power/SelectSleepButtonActionOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactiononbattery)

- **Hybridströmsparläge**: När enheten använder batteridrift förhindrar **Inaktivera** enheten från att försättas i hybridströmsparläge. I hybridströmsparläge lagras öppna appar och filer i RAM och på hårddisken. Detta använder en liten mängd batteriladdning. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

  [CSP för Power/TurnOffHybridSleepOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeponbattery)

### <a name="pluggedin"></a>PluggedIn

- **Batterinivå för aktivering av energisparläge**: Ange den laddningsnivå för batteriet då energisparläge ska aktiveras, 0 till 100, när enheten är ansluten till ström. Ange ett procentvärde som anger batteriets laddningsnivå. Standardvärdet är 70 %. När detta anges 70 % aktiveras energisparläge när batteriet har 70 % eller mindre laddning.

  [CSP för Power/EnergySaverBatteryThresholdPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdpluggedin)

- **Stängning av lock (endast mobil)** : Välj vad som ska hända när enheten är ansluten till ström och locket stängs. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Ingen åtgärd**: Enheten förblir aktiverad.
  - **Viloläge**: Enheten försätts i strömsparläge. Datorn förblir på, och öppnade appar och filer lagras i RAM (Random Access Memory).
  - **Viloläge**: Enheten försätts i viloläge. Öppnade appar och filer lagras på hårddisken, och enheten stängs av.
  - **Stäng av**: Enheten stängs av. Öppnade appar och filer stängs utan att sparas.
  
    [CSP för Power/SelectLidCloseActionPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactionpluggedin)
  
- **Strömknapp**: Välj vad som ska hända när enheten är ansluten till ström och strömknappen väljs. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Ingen åtgärd**: Enheten förblir aktiverad.
  - **Viloläge**: Enheten försätts i strömsparläge. Datorn förblir på, och öppnade appar och filer lagras i RAM (Random Access Memory).
  - **Viloläge**: Enheten försätts i viloläge. Öppnade appar och filer lagras på hårddisken, och enheten stängs av.
  - **Stäng av**: Enheten stängs av. Öppnade appar och filer stängs utan att sparas.

  [CSP för Power/SelectPowerButtonActionPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactionpluggedin)

- **Vila**: Välj vad som ska hända när enheten är ansluten till ström och knappen Strömsparläge väljs. Alternativen är:

  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Ingen åtgärd**: Enheten förblir aktiverad.
  - **Viloläge**: Enheten försätts i strömsparläge. Datorn förblir på, och öppnade appar och filer lagras i RAM (Random Access Memory).
  - **Viloläge**: Enheten försätts i viloläge. Öppnade appar och filer lagras på hårddisken, och enheten stängs av.
  - **Stäng av**: Enheten stängs av. Öppnade appar och filer stängs utan att sparas.

  [CSP för Power/SelectSleepButtonActionPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactionpluggedin)

- **Hybridströmsparläge**: När enheten är ansluten till ström förhindrar **Inaktivera** enheten från att försättas i hybridströmsparläge. I hybridströmsparläge lagras öppna appar och filer i RAM och på hårddisken. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

  [CSP för Power/TurnOffHybridSleepPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeppluggedin)

## <a name="next-steps"></a>Nästa steg

Mer teknisk information om varje inställning och vilka utgåvor av Windows som stöds finns i [CSP-referens för Windows 10-princip](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider)
